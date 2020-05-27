He creado un script con un resumen de lo dado en la Asignatura de ISO (ASIR1)
La escructura es la siguiente: 
 (En el apartado del directorio activo, esta configurado como que el dominio es ANDEL.LOCAL)

## PROCESOS DEL SISTEMA

#### LISTAR PROCESOS
#### INFORMACIÓN DE UN PROCESO CONCRETO
#### RUTA DE LOS PROCESOS
#### LISTAR SERVICIOS
#### CONEXIÓN DE LOS PROCESOS
#### HILOS
#### RELACIÓN PROCESOS/HILOS

## GESTIÓN DE ARCHIVOS

#### INFORMACIÓN DE ARCHIVOS
#### INFORMACIÓN DE ARCHIVOS OCULTOS
#### VER PARTICIONES
#### VER TIPO PARTICIONES
#### CREAR PARTICIONES
#### DAR FORMATO
#### CREAR DISCO VIRTUAL
#### MONTAR DISCO
#### DESFRAGMENTAR
#### CIFRAR DISCO
#### DESCIFRAR DISCO
#### VER RECURSOS COMPARTIDA
#### CREAR RECURSO COMPARTIDO
#### ELIMINAR ARCHIVO
#### RENOMBRAR ARCHIVO
#### COMPRIMIR ARCHIVO
#### DESCOMPRIMIR ARCHIVO
#### VER PERMISOS
#### OBTENER HASH ARCHIVO
#### INTEGRIDAD

## HARDWARE"

#### SISTEMA OPERATIVO/PARTICIÓN
#### FABRICANTE PLACA BASE
#### VERSIÓN DE LA BIOS
#### BUSES CONECTADOS
#### INFORMACIÓN DEL PROCESADOR
#### INFORMACIÓN DISCOS
#### SERIAL FABRICANTE EQUIPO
#### BATERIA RESTANTE ESTIMADA
#### IMPRESORAS EN EQUIPO
#### RESUMEN

## PROGRAMAS

#### PROGRAMAS INSTALADOS Y VERSIÓN
#### LISTAR PROGRAMAS LIBRERÍA
#### INSTALAR PROGRAMA
#### DESINSTALAR PROGRAMA
#### ACTUALIZACIONES
#### BUSCAR ACTUALIZACIÓN
#### INICIAR ANTIVIRUS

## CAPAS

#### RED
#### INTERNET
#### TRANSPORTE
#### APLICACIÓN

## DIRECTORIO ACTIVO

#### Crear unidad Organizativa
#### Creación de grupos
#### Usuarios
#### Copiar Usuario A GRUPOS
#### Borrar
#### GPO

## COPIA DE SEGURIDAD"

## PROGRAMAR TAREA"

#### VER TODAS LAS TAREAS PROGRAMAS
#### PROGRAMAR TAREAS
#### DESHABILITAR TAREA
#### HABILITAR TAREA
#### ANULAR TAREA

## COSITAS

#### FECHA Y HORA
#### LOCALIZACIÓN CPU
#### TIEMPO CLIMATOLÓGICO
#### SINTETIZADOR DE VOZ
#### OBTENER INFORMACIÓN WLAN


## Salir




```
  Function Mostrar-MensajeCuadroDialogo {Param
           ([string]$Mensaje,[string]$Titulo,[System.Windows.Forms.MessageBoxButtons]$Botones,[System.Windows.Forms.MessageBoxIcon]$Icono)
           return [System.Windows.Forms.MessageBox]::Show($Mensaje, $Titulo, $Botones, $Icono)} $dia=get-date
CLS
Write-Host "  PABLO QUEIPO SHELL"
Write-Host "Seleccione una opcion"

echo "1 - PROCESOS DEL SISTEMA"
echo "2 - GESTIÓN DE ARCHIVOS"
echo "3 - HARDWARE"
echo "4 - PROGRAMAS"
echo "5 - CAPAS"
echo "6 - DIRECTORIO ACTIVO"
echo "7 - COPIA DE SEGURIDAD"
echo "8 - PROGRAMAR TAREA"
echo "9 - COSITAS"
echo "10 - Salir"
$pruebax = Read-Host
switch ($pruebax)
{ 
    <# -------------------------------------------PROCESOS DEL SISTEMA-------------------------------------------------------------- #>
 1{ cls
     Write-Host "  PABLO QUEIPO SHELL"
     Write-Host "Seleccione una opcion"
     echo "1 - LISTAR PROCESOS"
     echo "2 - INFORMACIÓN DE UN PROCESO CONCRETO"
     echo "3 - RUTA DE LOS PROCESOS"
     echo "4 - LISTAR SERVICIOS"
     echo "5 - CONEXIÓN DE LOS PROCESOS"
     echo "6 - HILOS"
     echo "7 - RELACIÓN PROCESOS/HILOS"
     $pruebapro = Read-Host
      switch ($pruebapro)
         { 
            1{get-process
            write-host "Numero de procesos"(Get-Process).count}
            2{Write-Host "Nombre del Proceso"
            $proces=read-host
            get-process $proces |select *}
            3{ps | select Name, Path}
            4{get-service
            write-host "Numero de servicios"(Get-service).count}
            5{netstat -ano}
            6{(Get-Process | select name,Threads).Threads.id}
            7{(Get-WmiObject -Class Win32_Thread) | %{
            $_.Handle, (Get-Process -Id $_.ProcessHandle).ProcessName}}
         }
  }
    <# -------------------------------------------FIN PROCESOS DEL SISTEMA-------------------------------------------------------------- #>
    <# -------------------------------------------GESTIÓN DE ARCHIVOS-------------------------------------------------------------- #>
2{ cls
     Write-Host "  PABLO QUEIPO SHELL"
     Write-Host "Seleccione una opcion"
     echo "1 - INFORMACIÓN DE ARCHIVOS"
     echo "2 - INFORMACIÓN DE ARCHIVOS OCULTOS"
     echo "3 - VER PARTICIONES"
     echo "4 - VER TIPO PARTICIONES"
     echo "5 - CREAR PARTICIONES"
     echo "6 - DAR FORMATO"
     echo "7 - CREAR DISCO VIRTUAL"
     echo "8 - MONTAR DISCO"
     echo "9 - DESFRAGMENTAR"
     echo "10 - CIFRAR DISCO"
     echo "11 - DESCIFRAR DISCO"
     echo "12 - VER RECURSOS COMPARTIDA"
     echo "13 - CREAR RECURSO COMPARTIDO"
     echo "14 - ELIMINAR ARCHIVO"
     echo "15 - RENOMBRAR ARCHIVO"
     echo "16 - COMPRIMIR ARCHIVO"
     echo "17 - DESCOMPRIMIR ARCHIVO"
     echo "18 - VER PERMISOS"
     echo "19 - OBTENER HASH ARCHIVO"
     echo "20 - INTEGRIDAD"
     $pruebapro = Read-Host
      switch ($pruebapro)
         { 
            1{Get-ChildItem -Path $home
            write-host "EL NUMERO DE ARCHIVOS ES" (Get-ChildItem -Path $home).count}
            2{Get-ChildItem -Path $home –Hidden
            write-host "EL NUMERO DE ARCHIVOS OCULTOS ES" (Get-ChildItem -Path $home -Hidden).count}
            3{get-partition}
            4{(Get-Disk).PartitionStyle}
            5{$disk=read-host "INTRODUZCA NUMERO DE DISCO DONDE CREARA LA PARTICIÓN"
              $TAMA=read-host "INTRODUZCA TAMAÑO DEL DISCO"
              $letra=read-host "ASIGNE LETRA"
              New-Partition -DiskNumber $DISK -Size $TAMA -DriveLetter $letra
              Mostrar-MensajeCuadroDialogo -Mensaje "Ha creado una particion de $tama Gb en $letra" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Information}
            6{$letra=read-host "ASIGNE LETRA"
            Format-Volume -DriveLetter $letra
            Mostrar-MensajeCuadroDialogo -Mensaje "Formato dado a $letra" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Information}
            7{$rutaa=read-host "INTRODUZCA RUTA"
              $TAMAN=read-host "INTRODUZCA TAMAÑO"
            New-VHD –Path $rutaa.vhdx –SizeBytes $TAMAN
            Mostrar-MensajeCuadroDialogo -Mensaje "Ha creado un Disco Virtual en $rutaa" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Information}
            8{$rutaa=read-host "INTRODUZCA RUTA A MONTAR"
            Mount-VHD –Path $rutaa
            Mostrar-MensajeCuadroDialogo -Mensaje "Ha montado el Disco Virtual de $rutaa" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Information}
            9{cls
            
            $letra=READ-HOST "INTRODUZCA LETRA DE LA UNIDAD A DESFRAGMENTAR, su disco tiene las letra/s:" (get-partition | select DriveLetter).driveletter
             Optimize-Volume $LETRA -Defrag}
            10{$cifra=read-host "INTRODUZCA LETRA DEL DISCO ej: f:"
            Enable-BitLocker -MountPoint $cifra -RecoveryPasswordProtector -UsedSpaceOnly -Verbose
            Mostrar-MensajeCuadroDialogo -Mensaje "Ha cifrado el disco $letra" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Information}
            11{$cifra=read-host "INTRODUZCA LETRA DEL DISCO ej f:"
            Disable-BitLocker -MountPoint $cifra
            Mostrar-MensajeCuadroDialogo -Mensaje "Ha descifrado el disco $letra" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Information}
            12{get-smbshare}
            13{$carpc=read-host "INTRODUZCA NOMBRE DE LA CARPETA"
               $rut=read-host "INTRODUZCA RUTA"
            New-SmbShare -Name $carpc -Path $rut}
            14{$ruta=read-host "INTRODUZCA RUTA Y ARCHIVO"
            Remove-Item $ruta
            Mostrar-MensajeCuadroDialogo -Mensaje "Archivo $RUTA ha sido borrado" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Hand}
            15{$origi=read-host "INTRODUZCA RUTA Y ARCHIVO ORIGINAL"
               $nuevo=read-host "INTRODUZCA RUTA Y ARCHIVO NUEVO"
            Rename-Item $origi $nuevo}
            16{	$ruta1=read-host "INTRODUZCA RUTA (Incluyendo extensión del archivo)"
                $ruta2=read-host "INTRODUZCA RUTA (Incluyendo extensión .zip)"
                Compress-Archive -LiteralPath $ruta1 –CompressionLevel Optimal -DestinationPath $ruta2
                Mostrar-MensajeCuadroDialogo -Mensaje "Ha comprimido el archivo en la ruta $ruta2" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Information}
            17{$ruta=read-host "INTRODUZCA RUTA Y ARCHIVO A DESCOMPRIMIR"
              $ruta2=read-host "INTRODUZCA RUTA DONDE DESCOMPRIMIR"
            Expand-Archive -LiteralPath $ruta -DestinationPath $ruta2}
            18{get-acl}
            19{	$RUTA=Read-Host "INTRODUZCA RUTA DEL ARCHIVO"
            Get-FileHash $RUTA -Algorithm SHA512}
            20 {$archi1=read-host "INTRODUZCA ARCHIVO 1"
                $archi2=read-host "INTRODUZCA ARCHIVO 2"
                function comprobarhashear($hash1,$hash2){
                if($hash1 -eq $hash2)
                {"Es igual"}
                else
                {"Es distinto"}}
                comprobarhashear (Get-FileHash $archi1).hash (Get-FileHash $archi2).hash
            }

        }
}
<# -------------------------------------------FIN GESTIÓN DE ARCHIVOS-------------------------------------------------------------- #>
       <# ---------------------------------------------------HARDWARE-------------------------------------------------------------- #>
 3{
     cls
     Write-Host "  PABLO QUEIPO SHELL"
     Write-Host "Seleccione una opcion"
     echo "1 - SISTEMA OPERATIVO/PARTICIÓN"
     echo "2 - FABRICANTE PLACA BASE"
     echo "3 - VERSIÓN DE LA BIOS"
     echo "4 - BUSES CONECTADOS"
     echo "5 - INFORMACIÓN DEL PROCESADOR"
     echo "6 - INFORMACIÓN DISCOS"
     echo "7 - SERIAL FABRICANTE EQUIPO"
     echo "8 - BATERIA RESTANTE ESTIMADA"
     echo "9 - IMPRESORAS EN EQUIPO"
     echo "10 - RESUMEN"
     $hardw = Read-Host
        cls
      switch ($hardw)
         { 
            1{(Get-WmiObject Win32_AutochkSetting).SettingID}
            2{(Get-WmiObject Win32_BaseBoard).Manufacturer}
            3{(Get-WmiObject Win32_BIOS).Version}
            4{(Get-WmiObject Win32_Bus).DeviceID}
            5{Get-WmiObject Win32_Processor}
            6{(Get-Disk)}
            7{(Get-WmiObject Win32_SystemEnclosure)}
            8{Get-WmiObject Win32_Battery}
            9{Get-WmiObject Win32_Printer}
            10{$ComputerSystem=Get-WmiObject Win32_ComputerSystem
              $BaseBoard=Get-WmiObject Win32_BaseBoard
              $BIOS=Get-WmiObject Win32_BIOS
              $Processor=Get-WmiObject Win32_Processor
              $Battery=Get-WmiObject Win32_Battery
              [PSCustomObject]@{
              Model = $ComputerSystem.Model
              ManufacturerBoard = $BaseBoard.Manufacturer
              BIOSVersion = $BIOS.SMbiosbiosversion
              BIOSSerialNumber = $BIOS.serialnumber
              ManufacturerProcessor=$Processor.Manufacturer
              MaxClockSpeed=$Processor.MaxClockSpeed
              DeviceIDBattery=$Battery.DeviceID.trim()}}
         }
 }    
         <# -------------------------------------------FIN HARDWARE-------------------------------------------------------------- #>
<# ------------------------------------------------ PROGRAMAS ------------------------------------------------------------------#>
4{
     cls
     Write-Host "  PABLO QUEIPO SHELL"
     Write-Host "Seleccione una opcion"
     echo "1 - PROGRAMAS INSTALADOS Y VERSIÓN"
     echo "2 - LISTAR PROGRAMAS LIBRERÍA"
     echo "3 - INSTALAR PROGRAMA"
     echo "4 - DESINSTALAR PROGRAMA"
     echo "5 - ACTUALIZACIONES"
     echo "6 - BUSCAR ACTUALIZACIÓN"
     echo "7 - INICIAR ANTIVIRUS"
     $PROG = Read-Host
        cls
      switch ($PROG)
         { 
            1{(Get-Package | Select-Object Name, Version)
              WRITE-HOST "Numero de programas Instalados" ((Get-Package).name).count}
            2{Find-Package}
            3{write-host "Nombre del programa"
              $program=read-host
              Find-Package $program | Install-Package
              Mostrar-MensajeCuadroDialogo -Mensaje "Ha Instalado el Programa de $program" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Information}
            4{write-host "Nombre del programa"
              $programp=read-host
              Find-Package $programp | uninstall-Package
              Mostrar-MensajeCuadroDialogo -Mensaje "Ha desinstalado el Programa de $programp" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Information}
            5{Get-HotFix}
            6{$kb=Read-Host ‘Numero de Actualización’ 
             ((Get-HotFix).hotfixid | Select-String $kb)}
            7{Start-MpScan}
         }
}

<# ------------------------------------------------ FIN PROGRAMAS ------------------------------------------------------------------#>
<# ------------------------------------------------ CAPAS ------------------------------------------------------------------#>
<# ------------------------------------------------ RED ------------------------------------------------------------------#>
5{
     cls
     Write-Host "  PABLO QUEIPO SHELL"
     Write-Host "Seleccione una opcion"
     echo "1 - RED"
     echo "2 - INTERNET"
     echo "3 - TRANSPORTE"
     echo "4 - APLICACIÓN"

     $prupro = Read-Host
      switch ($prupro)
         { 
            1{cls
            Write-Host "  PABLO QUEIPO SHELL"
     Write-Host "Seleccione una opcion"
     echo "1 - TARJETA DE RED"
     echo "2 - INFORMACIÓN ADAPTADOR DE RED"
     echo "3 - ADAPTADOR DE RED MAS INFO"
     echo "4 - HABILITAR/DESHABILITAR ADAPTADOR RED"
     echo "5 - ELEMENTOS ADAPTADOR DE RED"
     echo "6 - HABILITAR/DESHABILITAR ELEMENTOS ADAPTADOR RED"
     echo "7 - CAMBIAR NOMBRE ADAPTADOR"
     echo "8 - ESTADISTICAS ADAPTADORES"
     $RED = Read-Host
        cls
      switch ($RED)
         { 
            1{Get-Command -Module NetAdapter}
            2{Get-NetAdapterHardwareInfo
              Get-NetAdapter -Physical}
            3{Get-NetAdapterAdvancedProperty -Name "*" -AllProperties}
            4{  cls
                Write-Host "Seleccione una opcion"
                echo "1 - HABILITAR ADAPTADOR RED"
                echo "2 - DESHABILITAR ADAPTADOR RED"
                $ADA = Read-Host
                cls
                switch ($ADA)
                { 
                    1{$ADA=READ-HOST "NOMBRE DEL ADAPTADOR"
                    Enable-NetAdapter -Name $ADA}
                    2{$ADA=READ-HOST "NOMBRE DEL ADAPTADOR"
                    Disable-NetAdapter -Name $ADA}
                }
              }
            5{Get-NetAdapterBinding}
            6{  cls
            Write-Host "Seleccione una opcion"
                echo "1 - HABILITAR ADAPTADOR RED"
                echo "2 - DESHABILITAR ADAPTADOR RED"
                $ADAPT = Read-Host
                cls
                switch ($ADAPT)
                { 
                    1{$ADAPT=READ-HOST "NOMBRE DEL ADAPTADOR"
                      $ELE=READ-HOST "NOMBRE DEL ELEMENTO"
                      Enable-NetAdapterBinding -Name $ADAPT -ComponentID $ELE}
                    2{$ADAPT=READ-HOST "NOMBRE DEL ADAPTADOR"
                      $ELE=READ-HOST "NOMBRE DEL ELEMENTO"
                      Disable-NetAdapterBinding -Name $ADAPT -ComponentID $ELE}
                }
              }
              7{$adaptar=read-host "NOMBRE DEL ADATADOR"
              $newname= read-host "NUEVO NOMBRE ADAPTADOR"
              Rename-NetAdapter -Name $adaptar -NewName $newname}
              8{Get-NetAdapterStatistics}
        }
        }
        <# ------------------------------------------------ FIN RED ------------------------------------------------------------------#>
        <# ------------------------------------------------ INTERNET ------------------------------------------------------------------#>
        2{
        cls
        Write-Host "  PABLO QUEIPO SHELL"
     Write-Host "Seleccione una opcion"
     echo "1 - DIRECCIONES FÍSICA"
     echo "2 - DIRECCIONES FÍSICAS ASOCIADAS"
     echo "3 - CONFIGURACIONES DE PROTOCOLO IP"
     echo "4 - DIRECCIONES IP DEL SISTEMA"
     echo "5 - CAMBIAR DIRECCION IP"
     echo "6 - ELIMINAR DIRECCIÓN IP"
     echo "7 - TABLA DE ENRUTAMIENTO"
     echo "8 - TEST DE CONEXIÓN"
     $ppro = Read-Host
      switch ($ppro)
         { 
            1{Get-NetAdapter | Select-Object Name,MacAddress}
            2{Get-NetNeighbor}
            3{Get-NetIPv4Protocol
              Get-NetIPv6Protocol}
            4{Get-NetIPConfiguration
             Get-NetIPAddress}
            5{cls
            Write-Host "Seleccione una opcion"
             echo "1 - DIRECCIONES IPV6"
             echo "2 - DIRECCIONES IPV6"
            $IPV = Read-Host
            switch ($IPV)
                { 
                1{$INTER=READ-HOST "ADAPTADOR"
                 $ipn=Read-Host "NUMERO DE IP"
                 $PUERTAE=Read-Host "PUERTA DE ENLACE POR DEFECTO"
                New-NetIPAddress -InterfaceAlias $INTER -IPAddress $ipn -PrefixLength 24 -DefaultGateway $PUERTAE}
                2{$INTER=READ-HOST "ADAPTADOR"
                  $ipn=Read-Host "NUMERO DE IP"
                New-NetIPAddress –InterfaceAlias $INTER –IPAddress $ipn}
                }
              }
            6{$ipn=Read-Host "NUMERO DE IP"
            $PUERTAE=Read-Host "PUERTA DE ENLACE POR DEFECTO"
            Remove-NetIPAddress -IPAddress $ipn -DefaultGateway $PUERTAE}
            7{Get-NetRoute}
            8{$ipn=Read-Host "NUMERO DE IP"
            Test-Connection $ipn}

          }
        }
        <# ------------------------------------------------ FIN INTERNET ------------------------------------------------------------------#>
        <# ------------------------------------------------ TRANSPORTE ------------------------------------------------------------------#>
         3{cls
     Write-Host "Seleccione una opcion"
     echo "1 - TCP"
     echo "2 - UDP"
     $TRA = Read-Host
      switch ($TRA)
         { 
            1{cls
     Write-Host "Seleccione una opcion"
     echo "1 - AJUSTES TCP"
     echo "2 - CONEXIONES TCP ACTUALES"
     echo "3 - PUERTOS TCP UTILIZADOS"
     $ppro = Read-Host
      switch ($ppro)
         { 
            1{Get-NetTCPSetting}
            2{Get-NetTCPConnection}
            3{Get-NetTCPConnection | Select-Object LocalPort,Remoteport,state}
          }
             }
          2{cls
     Write-Host "Seleccione una opcion"
     echo "1 - AJUSTES UDP"
     echo "2 - CONEXIONES UDP ACTUALES"
     echo "3 - PUERTOS UDP ABIERTOS"
     $UDP = Read-Host
      switch ($UDP)
         { 
            1{Get-NetUDPSetting}
            2{Get-NetUDPendpoint}
            3{Get-NetUDPendpoint | Select-Object LocalPort}
          }
          }
          }
        }
        <# ------------------------------------------------ FIN TRANSPORTE ------------------------------------------------------------------#>
         <# ------------------------------------------------ APLICACIÓN ------------------------------------------------------------------#>
         4{cls
         Write-Host "  PABLO QUEIPO SHELL"
     Write-Host "Seleccione una opcion"
     echo "1 - CONSULTA RESOLUCIÓN NOMBRES"
     echo "2 - CONTENIDO CACHE DNS"
     echo "3 - LIMPIAR CACHE DNS"
     echo "4 - DIRECCIONES SERVIDORES DNS"
     echo "5 - CAMBIAR SERVIDORES DNS"
     $TRA = Read-Host
      switch ($TRA)
         { 
            1{$dns=read-host "INTRODUZCA DIRECCIÓN"
            Resolve-DnsName $dns}
            2{Get-DnsClientCache}
            3{Clear-DnsClientCache
              Mostrar-MensajeCuadroDialogo -Mensaje "Ha limpiado el el contenido de la cache DNS" -Titulo "Pablo Queipo SHELL $dia"  -Botones OK -Icono Information}
            4{Get-DnsClientServerAddress}
            5{$INTERF=READ-HOST "INTERFACE"
             $pri=read-host "INTRODUZCA DIRECCIÓN ORIGEN"
             $SEC=READ-HOST "INTRODUZCA DIRECCIÓN DESTINO"
            Set-DNSClientServerAddress –interfaceAlias $INTERF –ServerAddresses ($pri,$SEC)}
         }
         } 
         <# ------------------------------------------------------ FIN APLICACIÓN ------------------------------------------------------------------#>
    }
}
<# ------------------------------------------------ FIN CAPAS ------------------------------------------------------------------#>

<# ------------------------------------------------ DIRECTORIO ACTIVO ------------------------------------------------------------------#>
6{
cls
Write-Host "  PABLO QUEIPO SHELL"
Write-Host "Seleccione una opcion"
echo "1 - Crear unidad Organizativa"
echo "2 - Creación de grupos"
echo "3 - Usuarios"
echo "4 - Copiar Usuario a Grupos"
echo "5 - Borrar"
echo "6 - GPO"
<# -------- -------------#>
$prue1 = Read-Host
switch ($prue1)
    { 
     <#CREAR OU#>
     1{cls
     Write-Host "  PABLO QUEIPO SHELL"
     $NOMBREOU= READ-HOST "INTRODUZCA EL NOMBRE DE LA UNIDAD ORGANIZATIVA"
     $DOMI= READ-HOST "INTRODUZCA DOMINIO DONDE QUIERE CREARLO ejemplo <DC=DOMINIO,DC=DOMINIO>"
      New-ADOrganizationalUnit -Name $NOMBREOU -Path "$DOMI"
      Mostrar-MensajeCuadroDialogo -Mensaje "Creada Unidad Organizativa $NOMBREOU" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Information
      }
     <# CREAR GRUPO#>
     2{cls
       Write-Host "  PABLO QUEIPO SHELL"
       $NombreGrupo=read-host "INTRODUZCA EL NOMBRE DEL GRUPO"
       $UNIDADGRUPO=READ-HOST "DESCRIPCIÓN DEL GRUPO"
       $RUTA=READ-HOST "INTRODUZCA EL NOMBRE DE LA OU y RUTA DONDE QUIERE CREAR EL GRUPO ejemplo <OU=UNIDAD ORGANIZATIVA,DC=DOMINIO,DC=DOMINIO>"
       New-ADGroup -Name $NombreGrupo -SamAccountName $NombreGrupo -GroupCategory Distribution -GroupScope Global -DisplayName $NombreGrupo -Path "$RUTA" -Description $UNIDADGRUPO
       Mostrar-MensajeCuadroDialogo -Mensaje "Creado Grupo $NombreGrupo" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Information
       }
     <# CREAR USUARIO#>
     3{ cls   
              Write-Host "  PABLO QUEIPO SHELL"
              $nameuser=Read-Host "Nombre del nuevo usuario"
              $surnameuser=Read-Host "Apellido del nuevo usuario"
              $Telefono=Read-Host "Telefono"
              $Ciudad=Read-Host "Ciudad"
              $Contraseña=Read-Host "Contraseña"
              $ruta=read-host "Introduzca ruta donde quiere crearlo ejemplo <OU=UNIDAD ORGANIZATIVA,DC=DOMINIO,DC=DOMINIO>"
              New-ADUser -sAMAccountName $nameuser -Name $nameuser -DisplayName $nameuser -Surname $surnameuser -fax 9163726932 -Mobile $Telefono -Country ES -City $Ciudad -Path "$ruta" -PasswordNeverExpires $true -AccountPassword (ConvertTo-SecureString $Contraseña -AsPlainText -force) -Enabled $true
              Mostrar-MensajeCuadroDialogo -Mensaje "Usuario creado $BORRAROU" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Information
             
       }
       <# COPIAR USUARIOS  #>
       4{   $nombregrupo=read-host "INTRODUZCA NOMBRE DEL GRUPO DESTINO"
            $USER=READ-HOST "INTRODUZCA NOMBRE DEL USUARIO"
            add-adgroupmember –identity $nombregrupo –members $USER}
     
      <# BORRAR#>
      5{ cls
            Write-Host "  PABLO QUEIPO SHELL"
            echo "1 - USUARIO"
            echo "2 - ORDENADOR"
            echo "3 - GRUPO"
            echo "4 - OU"
            echo "5 - ELIMINAR PROTECCION DE OU"
            $opcion1=Read-Host "Eliga una opcion"
            switch ($opcion1)
            {
            1{ 
            $BORRARUSUARIO=READ-HOST "NOMBRE DEL USUARIO QUE QUIERE BORRAR"
            Remove-aduser -identity $BORRARUSUARIO
            Mostrar-MensajeCuadroDialogo -Mensaje "Borrado usuario $BORRARUSUARIO" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Hand
             }
            2{
            $BORRARPC=READ-HOST "NOMBRE DEL ORDENADOR QUE QUIERE BORRAR"
            remove-adcomputer -identity $BORRARPC
            Mostrar-MensajeCuadroDialogo -Mensaje "Borrado PC $BORRARPC" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Hand 
             }
            3{
            $BORRARGRUPO=READ-HOST "NOMBRE DEL GRUPO QUE QUIERE BORRAR"
            Remove-ADGroup -Identity $BORRARGRUPO
            Mostrar-MensajeCuadroDialogo -Mensaje "Borrado Grupo $BORRARGRUPO" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Hand 
             }
            4{
            $BORRAROU=READ-HOST "NOMBRE DE LA OU QUE QUIERE BORRAR"
            Remove-ADOrganizationalUnit -Identity $BORRAROU
            Mostrar-MensajeCuadroDialogo -Mensaje "Borrada OU $BORRAROU" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Hand 
            } 
            5{$elimi=read-host "NOMBRE DE LA OU y dominio ejemplo <OU=UNIDAD ORGANIZATIVA,DC=DOMINIO,DC=DOMINIO>"
            Get-ADOrganizationalUnit -Identity "$elimi" |
            Set-ADObject -ProtectedFromAccidentalDeletion:$false -PassThru }
            }
       }
       <# GPO #>
       6{ cls
            Write-Host "  PABLO QUEIPO SHELL"
            echo "1 - HERENCIA"
            echo "2 - FORZAR POLÍTICA"
            echo "3 - CREAR GPO"
            echo "4 - VINCULAR GPO"
            echo "5 - LISTAR GPO"
            echo "6 - PERMISOS GPO"
            echo "7 - RENOMBRAR GPO"
            echo "8 - ELIMINAR GPO"
            echo "9 - REPORTE DE GPO"
            echo "10 - ACTUALIZAR GPO"
            $ELEC=Read-Host "Eliga una opcion"
            switch ($ELEC)
             {
                1{ cls
                     echo "1 - INFORMACIÓN SOBRE HERENCIAS"
                    echo "2 - EJECUTAR HERENCIAS"
                    $ELI=READ-HOST "INTRODUZCA UNA OPCIÓN"
                    switch ($ELI)
                        {
                        1{CLS
                          $desnot=read-host	"INTRODUZCA OU y Dominio ejemplo <OU=UNIDAD ORGANIZATIVA,DC=DOMINIO,DC=DOMINIO>"
                         Get-GPInheritance "$desnot"}
                        2{cls
                            $HERENCIA=READ-HOST "NOMBRE DE LA OU y Dominio ejemplo <OU=UNIDAD ORGANIZATIVA,DC=DOMINIO,DC=DOMINIO>"
                            echo "1 - si"
                            echo "0 - no"
                            $heren= Read-Host "INTRODUZCA 1 O 2"
                            Set-GPInheritance -Target "$HERENCIA" -IsBlocked $heren
                            Mostrar-MensajeCuadroDialogo -Mensaje "Herencia $heren" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Information}
                        }
                        
                  }
                2{
                  cls
            $forza= Read-Host "Yes or No"
            $domini=Read-host "INTRODUZCA DOMINIO ejemplo <DC=DOMINIO,DC=DOMINIO>"
            Set-GPLink -Name "Default Domain Policy" -Target "$domini" -Enforced $forza
            Mostrar-MensajeCuadroDialogo -Mensaje "Forzar $forza" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Information    
                 }
                3 {cls
                    Write-Host "  PABLO QUEIPO SHELL"
                    echo "1 - Deshabilitar Windows Update"
                    echo "2 - Deshabilitar Windows Defender"
                    echo "3 - Deshabilitar Cortana"
                    echo "4 - Deshabilitar animacion primer inicio sesión"
                    echo "5 - Notificaciones"
                    echo "6 - Deshabilitar Firewall"
                     $opcion2=Read-Host "Eliga una opcion"
                    switch ($opcion2)
                    {
                    1{ 
                     $desup=Read-Host "NOMBRE DE LA OU y dominio ejemplo <OU=UNIDAD ORGANIZATIVA,DC=DOMINIO,DC=DOMINIO>"
                     New-GPO -Name "Windows Update" -Comment "Deshabilita Windows update"
                     Set-ItemProperty -Path HKLM:\Software\Policies\Microsoft\Windows\WindowsUpdate -Name DisableWindowsUpdateAccess -Value 1
                     New-GPLink -Name "Windows Update" -Target "$desup"
                     Mostrar-MensajeCuadroDialogo -Mensaje "Ha deshabilitado Windows update de $desup" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Information
                     }
                    2{
                    $desdef=read-host "NOMBRE DE LA OU y Dominio ejemplo <OU=UNIDAD ORGANIZATIVA,DC=DOMINIO,DC=DOMINIO>"
                    New-GPO -Name "Windows Defender" -Comment "Deshabilita Windows Defender Antivirus"
                    Set-GPRegistryValue -Name "Windows Defender" -Key "HKLM\Software\Policies\Microsoft\Windows Defender" -ValueName DisableAntiSpyware -Type DWord -Value 1
                    New-GPLink -Name "Windows Defender" -Target "$desdef"
                    Mostrar-MensajeCuadroDialogo -Mensaje "Ha deshabilitado Windows Defender de $desdef" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Information
                    }
                   3{ 
                    $descor=Read-host "Nombre de la OU y dominio ejemplo <OU=UNIDAD ORGANIZATIVA,DC=DOMINIO,DC=DOMINIO>"
                    New-GPO -Name "Cortana" -Comment "Deshabilita las funciones de Cortana"
                    Set-GPRegistryValue -Name "Cortana" -Key "HKLM\SOFTWARE\Policies\Microsoft\Windows\Windows Search" -ValueName AllowCortana -Type DWord -Value 0
                    Set-GPRegistryValue -Name "Cortana" -Key "HKLM\SOFTWARE\Policies\Microsoft\Windows\Windows Search" -ValueName AllowCortanaAboveLock -Type DWord -Value 0
                    Set-GPRegistryValue -Name "Cortana" -Key "HKLM\SOFTWARE\Policies\Microsoft\Windows\Windows Search" -ValueName AllowSearchToUseLocation -Type DWord -Value 0
                    New-GPLink -Name "Cortana" -Target "$descor"
                    Mostrar-MensajeCuadroDialogo -Mensaje "Ha deshabilitado las funciones de Cortana de $descor" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Information
                    }
                   4{
                    $desini=read-host "Nombre de la OU y Dominio ejemplo <OU=UNIDAD ORGANIZATIVA,DC=DOMINIO,DC=DOMINIO>"
                    New-GPO -Name "Animación de inicio" -Comment "Deshabilita la animación del primer inicio de sesión"
                    Set-GPRegistryValue -Name "Animación de inicio" -Key "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" -ValueName EnableFirstLogonAnimation -Type DWord -Value 0
                    New-GPLink -Name "Animación de inicio" -Target "$desini"
                    Mostrar-MensajeCuadroDialogo -Mensaje "Ha deshabilitado la animación de $desini" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Information
                   }
                   5{
                   cls
                    echo "1 - DesHabilitar"
                    echo "2 - habilitar"

                     $opcion3=Read-Host "Elija una opcion"
                    switch ($opcion3)
                    {
                         1{ 
                          $desnot=Read-Host "Nombre de la OU y Dominio ejemplo <OU=UNIDAD ORGANIZATIVA,DC=DOMINIO,DC=DOMINIO>"
                          New-GPO -Name "Notificaciones equipo" -Comment "Deshabilita las notificaciones"
                          Set-GPRegistryValue -Name "Notificaciones equipo" -Key "HKLM\SOFTWARE\Policies\Microsoft\Windows Defender Security Center\Notifications" -ValueName DisableNotifications -Type DWord -Value 1
                          New-GPLink -Name "Notificaciones equipo" -Target "$desnot"

                          New-GPO -Name "Notificaciones usuario" -Comment "Deshabilita las notificaciones"
                          Set-GPRegistryValue -Name "Notificaciones usuario" -Key "HKCU\Software\Policies\Microsoft\Windows\CurrentVersion\PushNotifications" -ValueName NoToastApplicationNotification -Type DWord -Value 1
                          Set-GPRegistryValue -Name "Notificaciones usuario" -Key "HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer" -ValueName TaskbarNoNotification -Type DWord -Value 1
                          Set-GPRegistryValue -Name "Notificaciones usuario" -Key "HKCU\Software\Policies\Microsoft\Windows\Explorer" -ValueName DisableNotificationCenter -Type DWord -Value 1
                          New-GPLink -Name "Notificaciones usuario" -Target "$desnot"
                          Mostrar-MensajeCuadroDialogo -Mensaje "Ha deshabilitado las notificaciones de $desnot" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Information
                           }
                         2{
                         $desnot=Read-Host "Nombre de la OU y dominio ejemplo <OU=UNIDAD ORGANIZATIVA,DC=DOMINIO,DC=DOMINIO>"
                         New-GPO -Name "Notificaciones equipo" -Comment "habilita las notificaciones"
                         Set-GPRegistryValue -Name "Notificaciones equipo" -Key "HKLM\SOFTWARE\Policies\Microsoft\Windows Defender Security Center\Notifications" -ValueName DisableNotifications -Type DWord -Value 0
                         New-GPLink -Name "Notificaciones equipo" -Target "$desnot"

                        New-GPO -Name "Notificaciones usuario" -Comment "habilita las notificaciones"
                        Set-GPRegistryValue -Name "Notificaciones usuario" -Key "HKCU\Software\Policies\Microsoft\Windows\CurrentVersion\PushNotifications" -ValueName NoToastApplicationNotification -Type DWord -Value 0
                        Set-GPRegistryValue -Name "Notificaciones usuario" -Key "HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer" -ValueName TaskbarNoNotification -Type DWord -Value 0
                        Set-GPRegistryValue -Name "Notificaciones usuario" -Key "HKCU\Software\Policies\Microsoft\Windows\Explorer" -ValueName DisableNotificationCenter -Type DWord -Value 0
                        New-GPLink -Name "Notificaciones usuario" -Target "$desnot"
                        Mostrar-MensajeCuadroDialogo -Mensaje "Ha habilitado las notificaciones de $desnot" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Information
                         }
                       }
                      }
                    6{
                    $desfir=read-host "Nombre de la OU"
                    New-GPO -Name "Firewall" -Comment "Deshabilita el Firewall"
                    Set-GPRegistryValue -Name "Firewall" -Key "HKLM\SOFTWARE\Policies\Microsoft\WindowsFirewall\DomainProfile" -ValueName EnableFirewall -Type DWord -Value 0
                    Set-GPRegistryValue -Name "Firewall" -Key "HKLM\SOFTWARE\Policies\Microsoft\WindowsFirewall\StandardProfile" -ValueName EnableFirewall -Type DWord -Value 0
                    New-GPLink -Name "Firewall" -Target "OU=$desfir,DC=andel,DC=local"
                    Mostrar-MensajeCuadroDialogo -Mensaje "Ha deshabilitado el Firewall de $desfir" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Information
                    }
                   }
                }
                4{$gpna=read-host "INTRODUZCA NOMBRE DE GPO"
                $RUT=read-host "INTRODUZCA RUTA ejemplo <OU=UNIDAD ORGANIZATIVA,DC=DOMINIO,DC=DOMINIO>"
                New-GPLink -Name $gpna -Target "$RUT" }
                5{Get-Gpo -All}
                6{$gpos=read-host "INTRODUZCA NOMBRE DE LA GPO"
                  Get-GPPermission -Name $gpos -All }
                7{CLS
                  $nom=read-host "INTRODUZCA NOMBRE DE LA GPO"
                  $nuenom=read-host "INTRODUZCA NUEVO NOMBRE DE LA GPO"
                Rename-GPO -Name $nom -TargetName $nuenom
                Mostrar-MensajeCuadroDialogo -Mensaje "La GPO $nom ha cambiado de nombre a $nuenom" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Information}
                8{$nombreg=read-host "INTRODUZCA EL NOMBRE DE LA GPO"
                  Remove-GPO -Name $nombreg
                  Mostrar-MensajeCuadroDialogo -Mensaje "Ha borrado la GPO $nombreg" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Hand}
                9{cls
                    echo "1 - Formato XML"
                    echo "2 - Formato HTML"
                    $opcionfor=Read-Host "Eliga una opcion"
                    switch ($opcionfor)
                         {
                            1{$gps=read-host "INTRODUZCA GPO"
                            Get-GPOReport -Name $gps -ReportType Xml}
                            2{$gps=read-host "INTRODUZCA GPO"
                            Get-GPOReport -Name $gps -ReportType Html}
                         }
                  }
                10{Invoke-GPUpdate 
                Mostrar-MensajeCuadroDialogo -Mensaje "Ha actualizado las GPO" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Information}
            }
         }
        }
}
         <# ------------------------------------------------ FIN DIRECTORIO ACTIVO ------------------------------------------------------------------#>
         <# ------------------------------------------------ COPIA DE SEGURIDAD ------------------------------------------------------------------#>

        
 7{ cls
    Write-Host "  PABLO QUEIPO SHELL" 
    $copiase=read-host "INTRODUZCA RUTA DEL ARCHIVO (incluyendo la extensión del fichero)"
    $copiade=read-host "INTRODUZCA RUTA DESTINO (incluyendo la extensión .zip)"
    Compress-Archive -LiteralPath "$copiase" –CompressionLevel Optimal -DestinationPath $copiade
    $nombrehash= (get-date).ToString("yyyyMMdd")
    Get-FileHash $copiade | out-file $nombrehash
    Mostrar-MensajeCuadroDialogo -Mensaje "Ha creado una copia de seguridad en $copiade" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Information
}
 <# ------------------------------------------------ FIN COPIA DE SEGURIDAD ------------------------------------------------------------------#>
  <# ------------------------------------------------ PROGRAMAR TAREA ------------------------------------------------------------------#>
    8{              cls
                    Write-Host "  PABLO QUEIPO SHELL"
                    Write-Host "Seleccione una opcion"
                    echo "1 - VER TODAS LAS TAREAS PROGRAMAS"
                    echo "2 - PROGRAMAR TAREAS"
                    echo "3 - DESHABILITAR TAREA"
                    echo "4 - HABILITAR TAREA"
                    echo "5 - ANULAR TAREA"
                    $PROGa = Read-Host
                    cls
                    switch ($PROGa)
                        { 
                            1{Get-ScheduledTask}
                            2{CLS
                    $app=read-host "INTRODUZCA PROGRAMA"
                    $nombreta=read-host "INTRODUZCA NOMBRE DE LA TAREA"
                    $desci=read-host "INTRODUZCA DESCRIPCIÓN DE LA TAREA"
                    $hor=read-host "INTRODUZCA HORA ejemplo: 16:25pm"
                    $action=New-ScheduledTaskAction -Execute $app
                    $trigger=New-ScheduledTaskTrigger -Daily -At $hor
                    Register-ScheduledTask -Action $action -Trigger $trigger -TaskName $nombreta -Description $desci
                    Mostrar-MensajeCuadroDialogo -Mensaje "Ha creado la tarea $nombreta a la hora $hor" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Information}
                        3{ $nombreta=read-host "INTRODUZCA NOMBRE DE LA TAREA"
                        Disable-ScheduledTask -TaskName $nombreta
                        Mostrar-MensajeCuadroDialogo -Mensaje "Ha deshabilitado la tarea $nombreta" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Exclamation}
                        4{ $nombreta=read-host "INTRODUZCA NOMBRE DE LA TAREA"
                        Enable-ScheduledTask -TaskName $nombreta
                        Mostrar-MensajeCuadroDialogo -Mensaje "Ha activado la tarea $nombreta" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Information}
                        5{ $nombreta=read-host "INTRODUZCA NOMBRE DE LA TAREA"
                        Unregister-ScheduledTask -TaskName $nombreta
                        Mostrar-MensajeCuadroDialogo -Mensaje "Ha anulado la tarea $nombreta" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono Exclamation}
                        }
              }
  <# ------------------------------------------------ FIN PROGRAMAR TAREA ------------------------------------------------------------------#>
  <# ------------------------------------------------ COSITAS ------------------------------------------------------------------#>
 9{  cls
     Write-Host "  PABLO QUEIPO SHELL"
     Write-Host "Seleccione una opcion"
     echo "1 - FECHA Y HORA"
     echo "2 - LOCALIZACIÓN CPU"
     echo "3 - TIEMPO CLIMATOLÓGICO"
     echo "4 - SINTETIZADOR DE VOZ"
     echo "5 - OBTENER INFORMACION WLAN"
     $PROGa = Read-Host
        cls
      switch ($PROGa)
         { 
            1{$dime=get-date
              Add-Type -AssemblyName System.speech 
              $narrador = New-Object System.Speech.Synthesis.SpeechSynthesizer 
              $narrador.Speak("Hola, Hoy es $dime")
              get-date
              Mostrar-MensajeCuadroDialogo -Mensaje "HOY ES $DIA. Que tenga un buen día" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono None
            }
            2{Invoke-RestMethod  -Uri  ' http://ipinfo.io '
              $lugar= (Invoke-RestMethod  -Uri  ' http://ipinfo.io ' | select city).city
              $region= (Invoke-RestMethod  -Uri  ' http://ipinfo.io ' | select region).region
              $CP= (Invoke-RestMethod  -Uri  ' http://ipinfo.io ' | select postal).postal
              Add-Type -AssemblyName System.speech 
              $narrador = New-Object System.Speech.Synthesis.SpeechSynthesizer 
              $narrador.Speak("Usted está en $lugar,en la provincia de $region.Su codigo postal es el $CP")}
            3{($lugar=read-host "INTRODUZCA LUGAR")
                cls
               (curl wttr.in/$lugar.?format="%l:+%c+%t" | select content).content
               $audio= (curl wttr.in/$lugar.?format="%l:+%c+%t" | select content).content
               Add-Type -AssemblyName System.speech 
               $narrador = New-Object System.Speech.Synthesis.SpeechSynthesizer 
               $narrador.Speak("La tempertura en $audio")}
            4{ $sinteti=read-host "INTRODUZCA LO QUE QUIERE DECIR"
               Add-Type -AssemblyName System.speech 
               $narrador = New-Object System.Speech.Synthesis.SpeechSynthesizer 
               $narrador.Speak("$sinteti")}
            5{ cls
                Write-Host "  PABLO QUEIPO SHELL"
                Write-Host "Seleccione una opcion"
                echo "1 - DISPOSITIVOS A LOS QUE HA SIDO CONECTADO SU PC"
                echo "2 - OBTENER INFORMACION /CONTRASEÑA"
                $PROGa = Read-Host
                cls
                switch ($PROGa)
                { 
                    1{netsh wlan show profile}
                    2{$DISPO=read-host "INTRODUZCA DISPOSITIVO"
                    netsh wlan show profile name=$DISPO key=clear
                    write-host "La contraseña debe aparecer en el apartado- Contenido de la clave"}
                 }
            }
        }
}
   <# ------------------------------------------------ FIN COSITAS ------------------------------------------------------------------#>
           <#----------------------------------------------------- SALIR -------------------------------------------------------------#>
10{cls
Write-Host "  PABLO QUEIPO SHELL"
            Mostrar-MensajeCuadroDialogo -Mensaje "Gracias por todo" -Titulo "Pablo Queipo SHELL $dia" -Botones OK -Icono None
            }
    
    <# -------------------------------------------------------------FIN DIRECTORIO ACTIVO------------------------------------------------- #>
    }
    ```
    
