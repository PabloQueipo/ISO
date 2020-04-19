en un archivo txt llamado usuarios pondriamos lo siguente por ejemplo:
```
pepe,garcia,madrid,secretaria
jose,sanchez,huelva,Informatica
Carlos,Hidalgo,Barcelona,RRHH
etc
```
#CREAR USUARIOS LISTADOS DE UN ARCHIVO TXT
```
 foreach($elemento in get-content c:\users\administrador\desktop\usuarios.txt)
 {
 New-ADUser -sAMAccountName $elemento.split(",")[0] -name $elemento.split(",")[0] -office $elemento.split(",")[3] -DisplayName CiberDelincuente -Surname $elemento.split(",")[1] -fax 9100000000 -Mobile 60000000 -emailAddress ciberdelincuente@andel.es -country ES -City $elemento.split(",")[2] -path "OU=Asir1,OU=Alumnos,DC=andel,DC=local" -PasswordNeverExpires $true -AccountPassword (CovertTo-secureString andel_1928 -AsPlainText -Force) -enable $true
 }
```

#CREAR GPO PARA DICHO GRUPO (uno de ejemplo)
```
New-GPO -Name "Firewall" -Comment "Deshabilita el Firewall"
Set-GPRegistryValue -Name "Firewall" -Key "HKLM\SOFTWARE\Policies\Microsoft\WindowsFirewall\DomainProfile" -ValueName EnableFirewall -Type DWord -Value 0
Set-GPRegistryValue -Name "Firewall" -Key "HKLM\SOFTWARE\Policies\Microsoft\WindowsFirewall\StandardProfile" -ValueName EnableFirewall -Type DWord -Value 0
New-GPLink -Name "Firewall" -Target "OU=Asir1,DC=Alumnos,DC_andel,DC=local"
```
