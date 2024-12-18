### Praktikumis 13 õppisin powershelli syntaxi ja kuidas seal skripte kirjutada. Praktikum võttis mul aega umbes 6 tundi.
## pildid valjud failist
![image](https://github.com/user-attachments/assets/da45ce58-87c9-4426-81a7-ba3709355f5d)
![image](https://github.com/user-attachments/assets/f5daabff-7cb5-4138-a20d-74e7aa2dc094)
![image](https://github.com/user-attachments/assets/528d0229-69ed-4cff-ba85-a192117f0300)

'''
#$nr:	küsimuse number
#$param: mis parameetriga tegemist (võimalikult lühidalt)
#$sisu:	väljastatav sisu
function valjasta{
	param ($nr, $param, $sisu)
	$fail = ".\skripti_tulemus.txt"
	$aeg = Get-Date -Format "HH:mm:ss.fff"
	if($sisu -eq $null){
		$rida = "$nr.	$aeg	${param}:	NULL"
		Write-Output $rida
		$rida | Out-File -FilePath $fail -Append
	}elseif($sisu.GetType().Name -eq "Object[]"){
		$rida = "$nr.	$aeg	${param}:"
		Write-Output $rida $sisu
		$rida | Out-File -FilePath $fail -Append
		$sisu | Out-File -FilePath $fail -Append
	}else{
		$rida = "$nr.	$aeg	${param}:	$sisu"
		Write-Output $rida
		$rida | Out-File -FilePath $fail -Append
	}
}



#1yl muutujad
$hostname = hostname
$PS_version = $PSVersionTable.PSVersion.ToString()
$windows_version = Get-ComputerInfo | Select-Object Osname, OsVersion
#2yl muutujad
$network = Get-CimInstance Win32_NetworkAdapterConfiguration -Filter "IPEnabled='True'"
$ipAddress = $network.IPAddress[0]
$subnetMask = $network.IPSubnet[0]
$gateway = $network.DefaultIPGateway
$dhcpEnabled = $network.DHCPEnabled 
$macAddress = $network.MACAddress
#3yl muutujad
$cpu = Get-CimInstance Win32_Processor
$ram = [math]::Round((Get-CimInstance Win32_ComputerSystem).TotalPhysicalMemory / 1GB, 2)
#4yl muutujad
$gpu = Get-CimInstance Win32_VideoController
$gpuName = $gpu.Name
$driverVersion = $gpu.DriverVersion
$driverDate = $gpu.DriverDate
$screenResolution = "$($gpu.CurrentHorizontalResolution) x $($gpu.CurrentVerticalResolution)"
#5yl muutjuad
$drives = Get-CimInstance Win32_LogicalDisk -Filter "DriveType=3"
$Cdrives = Get-CimInstance Win32_LogicalDisk -Filter "DeviceID='C:'"
$totalSpace = [math]::Round($drives.Size / 1GB, 2)
$freeSpace = [math]::Round($Cdrives.FreeSpace / 1GB, 2)

#7yl muutujad
$users = Get-CimInstance Win32_UserAccount
$localUsers = $users | Where-Object { $_.LocalAccount -eq $true }
$disabledUsers = $localUsers | Where-Object { $_.Disabled -eq $true }
#8yl muutujad
$processCount = (Get-Process).Count
#yl 9 muutujad
$recentProcesses = Get-Process | Where-Object { $_.StartTime -ne $null } |
    Sort-Object StartTime -Descending | Select-Object -First 10 -Property Name, Id, StartTime
#yl 10 muutujad
$currentDateTime = Get-Date




#1yl
Valjasta 1 "host" $hostname
valjasta 1 "PS-ver" $PS_version
valjasta 1 "Windows-ver" $windows_version

#2yl
valjasta 2 "adapter" ($network)
valjasta 2 "IP-address" ($ipAddress)
valjasta 2 "Mask" ($subnetMask)
valjasta 2 "Gateway" ($gateway)
valjasta 2 "DHCP" ($dhcpEnabled)
valjasta 2 "MAC" ($macAddress)

#3yl
valjasta 3 "protsessori kirjeldus" $cpu
valjasta 3 "RAM" $ram

#4yl
valjasta 4 "GPU-name" $gpuName
valjasta 4 "driver-ver" $driverVersion
valjasta 4 "driver-kuupaev" $driverDate
valjasta 4 "ekraani lahutus" $screenResolution

#5yl
valjasta 5 "part-tabel" $drives
valjasta 5 "arvuti-kettamaht" $totalSpace
valjasta 5 "ruum-C_kettal" $freeSpace

#6yl
$pciDevices = Get-CimInstance Win32_PnPSignedDriver | Where-Object DeviceClass -eq "System"

if ($pciDevices) {
    $pciInfo = $pciDevices | ForEach-Object { "{0} | {1} | {2}" -f $_.Description, $_.Manufacturer, $_.DriverVersion }
    valjasta 6 "PCI devices" $pciInfo
}


#7yl
valjasta 7 "kasutajad" $users
valjasta 7 "local kasutajad" $localUsers
valjasta 7 "keelatud" $disabledUsers

#8yl
valjasta 8 "active protsesside arv" $processCount

#9yl
valjasta 9 "10 viimast kaivitatud protsessi" $recentProcesses

#10yl
valjasta 10 "aeg ja kuupaev" $currentDateTime
'''
