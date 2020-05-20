# Vamos a crear una OU (unidad organizativa) a base de script de Powershell. #
Una vez que tenemos un dominio al que llamaremos: mdef.es
Creamos la unidad organizativa a la que llamaremos EEAUTO
```
New-ADOrganizationalUnit -Name "EEAUTO" -Path "dc=Mdef,dc=es"
```

## La OU tendrá difentes grupos de seguridad dentro de ella, por lo que los crearemos leyendo desde un txt.
Para ello en un Block de notas introduciremos los siguientes grupos con el nombre DEPARTAMENTOS (ejemplo):
```
Secretaría
Jefatura de Estudios
Informática
Personal
Taller de Enseñanza
Automoviles
Permisos de Conducir
Escuadrilla de Alumnos
Psicología
Relaciones con la SEA
ALUMNOS
```

Ahora los crearemos con el siguiente script:
```
foreach($departamentos in get-content C:\Users\Administrador\Desktop\Departamentos.txt)
{
New-ADGroup -Name $departamentos -SamAccountName $departamentos -GroupCategory security -GroupScope Global -DisplayName $departamentos -Path "OU=EEAUTO,dc=mdef,dc=es " -Description $departamentos
}
```
## Tambien crearemos un grupo de distribucción donde mas adelante incluiremos a todos los usuarios.
```
New-ADGroup -Name "TODO EL PERSONAL" -SamAccountName TODOELPERSONAL -GroupCategory Distribution -GroupScope Global -DisplayName "TODO EL PERSONAL" -Path "OU=EEAUTO,dc=mdef,dc=es" -Description "GRUPO DE TODO EL PERSONAL"
```
## Ahora crearemos todos los usuarios de forma masiva leyendo de un .txt
Para ello como hicimos anteriormente con los grupos, crearemos un block de notas con lo siguiente: 
```
Roberto,Garcia,Madrid
Manuel,Perez,Bilbao
María,Ruiz,Madrid
José,Puyol,Barcelona
Alberto,Romero,Sevilla
```
Dependiendo de los datos que queramos incluir podremos ir ampliandolo con mas "," y en el script siguiente introducirlos con "splits" por ejemplo:
```
-name -surname -givenname -emailaddress -samaccountname -accountpassword -displayname -department  -country  -city -Enabled  -Passthru ETC
```

## Ahora ejecutaremos el siguiente script para crear los usuarios donde pondremos como contraseña "Usuario_nuevo1"
```
foreach($elemento in get-content C:\Users\Administrador\Desktop\UsuariosEEAUTO.txt)
{
New-ADUser -sAMAccountName $elemento.split(",")[0] -Name $elemento.split(",")[0] -DisplayName $elemento.split(",")[0] -Surname $elemento.split(",")[1] -Country ES -City $elemento.split(",")[2] -Path "OU=EEAUTO,DC=mdef,DC=es" -PasswordNeverExpires $true -AccountPassword (ConvertTo-SecureString Usuario_nuevo1 -AsPlainText -force) -Enabled $true
}
```

## Ahora como dijimos anteriormente moveremos todos los usuarios al grupo de distribucción
```
get-aduser -searchbase "OU=EEAUTO,DC=mdef,dc=es" -filter {objectclass -eq "user" } | foreach {add-adgroupmember -identity "cn=todoelpersonal,OU=EEAUTO,DC=mdef,dc=es" -Members $_}
```

## Y para distribuir los usuarios por los diferentes grupos segun sean sus departamentos usaremos el siguiente script de ejemplo:
(María al grupo de secretaría)
```
remove-adgroupmember –identity "cn=secretaría,OU=EEAUTO,DC=mdef,dc=es"-members María
```

#CON ESTO YA ESTARÍA CREADA LA OU
## Ahora vamos con las Políticas de Grupo

Para hacer otras diferentes podremos consultar esta web : https://getadmx.com/
o descargar esta hoja de calculo: https://www.microsoft.com/en-us/download/confirmation.aspx?id=25250

## Script deshabilitar la herencia
```
Set-GPInheritance -Target "ou=EEAUTO,dc=mdef,dc=es" -IsBlocked 1
```
## Script forzar políticas
```
Set-GPLink -Name "Default Domain Policy" -Target "dc=mdef,dc=es" -Enforced Yes
```

## Deshabilitar acceso a Windows Update
```
New-GPO -Name "Windows Update" -Comment "Deshabilita Windows update"
Set-ItemProperty -Path HKLM:\Software\Policies\Microsoft\Windows\WindowsUpdate -Name DisableWindowsUpdateAccess -Value 1
New-GPLink -Name "Windows Update" -Target "OU=EEAUTO,DC=mdef,DC=es"
```
## Insertar un Fondo de Pantalla predeterminado
```
New-GPO -Name "Programas" -Comment "Deshabilita instalación o desinstalación de programas"
Set-ItemProperty -Path HKCU\Software\Policies\Microsoft\Windows\Personalization   -Name LockScreenImage  -Value 1
New-GPLink -Name "Programas" -Target "OU=EEAUTO,DC=mdef,DC=es"
```
### La Imagen= C:\windows\web\screen\fondodepantalla.jpg

## Negar acceso al disco extraible 
```
New-GPO -Name "Prohibir USB" -Comment "Prohibir la ejecución de discos extraibles"
Set-ItemProperty -Path HKCU\Software\Policies\Microsoft\Windows\RemovableStorageDevices\{53f5630d-b6bf-11d0-94f2-00a0c91efb8b}   -Name Deny_Execute  -Value 1
New-GPLink -Name "Prohibir USB" -Target "OU=EEAUTO,DC=mdef,DC=es"
```

## Prohibir ajustes de barra de herramientas del escritorio
```
New-GPO -Name "Barra de herramientas" -Comment "Deshabilita Ajuste barra de herramientas"
Set-ItemProperty -Path HKLM:\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer -Name NoMovingBands -Value 0
New-GPLink -Name "Barra de herramientas" -Target "OU=EEAUTO,DC=mdef,DC=es"
```
## Deshabilitar el firewall
``` 
New-GPO -Name "Firewall" -Comment "Deshabilitar el Firewall"
Set-GPRegistryValue -Name "Firewall" -Key "HKLM\SOFTWARE\Policies\Microsoft\WindowsFirewall\DomainProfile" -ValueName EnableFirewall -Type DWord -Value 0
Set-GPRegistryValue -Name "Firewall" -Key "HKLM\SOFTWARE\Policies\Microsoft\WindowsFirewall\StandardProfile" -ValueName EnableFirewall -Type DWord -Value 0
New-GPLink -Name "Firewall" -Target "OU=EEAUTO,DC=mdef,DC=es"
```

## Ocultar el icono de Internet Explorer en el escritorio
```
New-GPO -Name "Icono IE -Comment "Ocultar iconos IE en escritorio"
Set-ItemProperty -Path HKLM:\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer -Name NoInternetIcon -Value 0
New-GPLink -Name "Icono IE" -Target "OU=EEAUTO,DC=mdef,DC=es"
```

## Deshabilitar el asistente de cortana
```
New-GPO -Name "Cortana" -Comment "Deshabilita las funciones de Cortana"
Set-GPRegistryValue -Name "Cortana" -Key "HKLM\SOFTWARE\Policies\Microsoft\Windows\Windows Search" -ValueName AllowCortana -Type DWord -Value 0
Set-GPRegistryValue -Name "Cortana" -Key "HKLM\SOFTWARE\Policies\Microsoft\Windows\Windows Search" -ValueName AllowCortanaAboveLock -Type DWord -Value 0
Set-GPRegistryValue -Name "Cortana" -Key "HKLM\SOFTWARE\Policies\Microsoft\Windows\Windows Search" -ValueName AllowSearchToUseLocation -Type DWord -Value 0
New-GPLink -Name "Cortana" -Target "OU=EEAUTO,DC=mdef,DC=es"
```
