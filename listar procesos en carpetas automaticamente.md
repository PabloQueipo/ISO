# listar procesos en carpetas automaticamente

foreach($veces in 168)
{
    $fecha = (Get-Date).ToString("yyyy\\MM\\dd")
    mkdir $fecha -Force

    $hora = (Get-Date).Hour
    New-Item -Name $hora -Path $fecha -ItemType Directory -Force

    (Get-Process).Name > ([String]($fecha+"\"+$hora+"\procesos.txt"))
    (Get-Service).Name > ([String]($fecha+"\"+$hora+"\servicios.txt"))
    (Get-Process).Threads > ([String]($fecha+"\"+$hora+"\hilos.txt"))

    Start-Sleep -Seconds 3600
}






# OTRA MANERA

foreach($veces in 168)
{
    [String]$mes = (get-date).Month
    [String]$ano = (get-date).Year
    [String]$dia = (get-date).Day
    [String]$hora = (get-date).hour
    [String]$ruta0 = $ano+"\"+$mes+"\"+$dia
    mkdir $ruta0 
    
    foreach($horas in 0..24)
    {
    $procesos= (get-process).Name |sort
    $hilos= (Get-Process).Threads |sort
    $servicios= (get-service).name |sort

        New-Item -Name $hora -Path $ruta0 -ItemType Directory -force
        (Get-Process).name > ([string]($ruta0+"\"+$hora+"\procesos.txt"))
        (Get-service).name > ([string]($ruta0+"\"+$hora+"\servicios.txt"))
        (Get-Process).threads > ([string]($ruta0+"\"+$hora+"\hilos.txt"))
       
       start-sleep -Seconds 3600
       
    }
}
