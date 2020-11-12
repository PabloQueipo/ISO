# LISTAMOS USUARIOS EN CADA ORDENADOR :raising_hand:
```Powershell
$adsi = [ADSI]"WinNT://$env:COMPUTERNAME"
$adsi.Children | Where-Object {$_.SchemaClassName  -eq 'user'} | Select-Object name |out-file usuarios.txt
```
# LISTAR PROGRAMAS INSTALADOS EN UN PC :floppy_disk:
```Powershell
Get-Package | Select-Object name | Out-File aplicaciones.txt
```
# LISTAR TODAS LAS CARPETAS Y ATRIBUTOS 
```Powershell
(Get-SmbShare).Path | ls -Force | gi -Force | select FullName, @{n="Attr";e={[string]$_.attributes}} |out-file carpetas.txt
```
# CREAR OU :house:
```Powershell
New-ADOrganizationalUnit -Name PRUEBA -Path "OU=PRUEBA,dc=Dominio,dc=local"
```
# CREAR USUARIOS Y RECURSOS COMPARTIDOS RECOGIDOS DEL FICHERO ANTERIORMENTE CREADO Y MAPEARLA :family:
```Powershell
foreach($elemento in Get-Content .\usuarios.txt)
{
    $elemento
    New-ADUSer -Name $elemento -Sam $elemento -Path "OU=PRUEBA,DC=Dominio,DC=Local" -AccountPassword (ConvertTo-SecureString "Contraseña" -AsPlainText -force) -Enable $true
    New-SmbShare -Name $elemento -Path F:\carpeta -ReadAccess todos
    New-PSDrive -Name $elemento -PSProvider FileSystem -Root \\localhost\empresa
    cd empresa:/
    Start-Sleep -Seconds 5
}
```
# INSTALAR APLICACIONES A LOS USUARIOS :cd:
```Powershell
foreach ($item in gc aplicaciones.txt)
{
    Install-Package -name $item
}
```
---------------------------------------------------------------------------------------------------------------------
## CREARLO EN MODO NINJA: :boom:

https://www.jmsolanes.net/es/unidades-organizativas-powershell/

