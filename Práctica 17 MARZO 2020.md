# SCRIPT PARA LISTAR PROGRAMAS INICIADOS DESDE QUE SE ARRANCO EL PC

Get-WmiObject win32_process | Sort-Object Processid | Select-Object Processid,Name,CommandLine |out-file programas.txt

#SCRIPT PARA AVISA DE QUE SE HA INICIADO UN NUEVOPROCESO

Register-WMIEvent -Query "SELECT * FROM Win32_ProcessStartTrace " -Action {Write-Host "Nuevo proceso abierto"} 
