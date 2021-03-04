# ---------SCRIPT  ADMIN---------
### NOMBRE DE USUARIOS Y SSID

```PowerShell
(Get-WmiObject -Class Win32_Account | Select-Object Name).name |out-file usuarios.txt
```
### Nombre de programas instalados
```PowerShell
(Get-WmiObject -Class Win32_Product).name |out-file programas.txt
```
### Información sobre actualizaciones instaladas
```PowerShell
Get-HotFix | Select-Object HotFixID,InstalledOn |out-file actualizaciones.txt
```
### carpetas compartidas 
```PowerShell
(Get-WmiObject -Class Win32_Share| Select-Object name, path).name| out-file carpetas.txt
(Get-WmiObject -Class Win32_Share| Select-Object name, path).path| out-file rutas.txt
```
# ------------SCRIPT PCNEW----------



### actualizar pc
```PowerShell
Install-Module PSWindowsUpdate
Get-WindowsUpdate
Start-Sleep -Seconds 30
```
### crear usuarios
```PowerShell
gc C:\Users\keipo\Desktop\practica1\usuarios.txt | % {
$pass=ConvertTo-SecureString $_ -asplaintext -force
New-LocalUser $_ -Password $pass 
}
Start-Sleep -Seconds 100
```
### instalar programa
```PowerShell
Install-package|% {gc C:\Users\keipo\Desktop\practica1\programas.txt}
Start-Sleep -Seconds 200 
```
### actualizaciones y comparar
```PowerShell
Get-HotFix | Select-Object HotFixID,InstalledOn 
```
### crear carpeta con permiso
```PowerShell
$rutas=gc C:\Users\keipo\Desktop\practica1\rutas.txt
gc C:\Users\keipo\Desktop\practica1\carpetas.txt |% {
New-SmbShare -Name $_ -Path $ruta –FullAccess administrador -ReadAccess Everyone
}
```
