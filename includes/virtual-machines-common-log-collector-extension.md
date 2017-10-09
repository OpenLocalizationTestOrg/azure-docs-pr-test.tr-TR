
Microsoft Azure bulut hizmeti ile ilgili sorunları tanılama hello sorunları ortaya çıktığında sanal makinelerde hello hizmetin günlük dosyalarını toplama gerektirir. Bir veya daha fazla bulut hizmeti Vm'lerden (web rolleri ve çalışan rolleri için) ve aktarım hello toplanan dosyaları tooan Azure depolama hesabı – tüm uzaktan oturum açma olmadan günlüklerinin hello AzureLogCollector uzantısı isteğe bağlı tooperfom tek seferlik koleksiyonunu kullanabilirsiniz Merhaba VM'ler tooany.

> [!NOTE]
> Oturum hello bilgilerin çoğunu açıklamalarını http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.asp bulunabilir.
> 
> 

Toplanan dosyaları toobe hello türlerini bağımlı koleksiyon iki moddan vardır.

* Azure Konuk Aracısı günlükleri yalnızca (GA). Bu koleksiyon modu tüm hello günlükleri ilgili tooAzure Konuk aracıları ve diğer Azure bileşenleri içerir.
* Tüm günlükleri (tam). Bu koleksiyon modu artı GA modunda tüm dosyaları toplar:
  
  * Sistem ve uygulama olay günlükleri
  * HTTP Hata günlüklerini
  * IIS günlükleri
  * Kurulum günlükleri
  * diğer sistem günlükleri

Her iki koleksiyon modlarında yapı izlenerek hello koleksiyonunu kullanarak ek veri koleksiyon klasörleri belirtilebilir:

* **Ad**: hello zip dosyası toobe içinde alt hello adı olarak kullanılacak hello koleksiyonunun hello adı toplanmadı.
* **Konum**: hello sanal makinedeki hello yol toohello klasörünü nereye dosya toplanacak.
* **SearchPattern**: hello düzeni dosyaları toobe hello adlarının toplanır. Varsayılan değer "*"
* **Özyinelemeli**: hello dosyaları hello klasörü altında toplanan yinelemeli olacaksa.

## <a name="prerequisites"></a>Ön koşullar
* Uzantı oluşturulan toosave ZIP dosyaları için toohave bir depolama hesabı gerekir.
* Azure PowerShell cmdlet'leri V0.8.0 kullandığınızdan emin olmanız gerekir veya üstü. Daha fazla bilgi için bkz: [Azure indirmeleri](https://azure.microsoft.com/downloads/).

## <a name="add-hello-extension"></a>Merhaba uzantısı Ekle
Kullanabileceğiniz [Microsoft Azure PowerShell](https://msdn.microsoft.com/library/dn495240.aspx) cmdlet'leri veya [Hizmet Yönetimi REST API'lerine](https://msdn.microsoft.com/library/ee460799.aspx) tooadd hello AzureLogCollector uzantısı.

Bulut Hizmetleri için var olan Azure Powershell cmdlet'ini hello **kümesi AzureServiceExtension**, bulut hizmet rolü örneklerinin üzerinde kullanılan tooenable hello uzantısı olabilir. Bu uzantı Bu cmdlet'i etkinleştirilmiş her zaman, günlük toplama seçili hello rol örneklerinde seçili roller tetiklenir.

Sanal makineler için mevcut Azure Powershell cmdlet'ini hello **kümesi AzureVMExtension**, sanal makinelerde kullanılan tooenable hello uzantısı olabilir. Bu uzantı hello cmdlet'leri aracılığıyla etkinleştirilmiş her zaman, günlük toplama her örneğinde tetiklenir.

Dahili olarak, bu uzantı hello JSON tabanlı PublicConfiguration ve PrivateConfiguration kullanır. Merhaba, ortak ve özel yapılandırması için örnek JSON hello düzenini aşağıdadır.

### <a name="publicconfiguration"></a>PublicConfiguration
    {
        "Instances":  "*",
        "Mode":  "Full",
        "SasUri":  "SasUri tooyour storage account with sp=wl",
        "AdditionalData":
        [
          {
                  "Name":  "StorageData",
                  "Location":  "%roleroot%storage",
                  "SearchPattern":  "*.*",
                  "Recursive":  "true"
          },
          {
                "Name":  "CustomDataFolder2",
                "Location":  "c:\customFolder",
                "SearchPattern":  "*.log",
                "Recursive":  "false"
          },
        ]
    }

### <a name="privateconfiguration"></a>PrivateConfiguration
    {

    }

> [!NOTE]
> Bu uzantının gerekmez **privateConfiguration**. Merhaba yalnızca boş bir yapı sağlayabilir **– PrivateConfiguration** bağımsız değişkeni.
> 
> 

Merhaba iki birini izleyin adımları tooadd hello AzureLogCollector tooone veya daha fazla örneğini bir bulut hizmeti veya sanal makineye hangi Tetikleyiciler hello her VM toorun koleksiyonunda ve tooAzure hesap hello toplanan dosya gönderme seçili roller Belirtilen.

## <a name="adding-as-a-service-extension"></a>Bir hizmeti uzantı olarak ekleme
1. Merhaba yönergeleri tooconnect Azure PowerShell tooyour abonelik izleyin.
2. Merhaba hizmet adı, yuva, rolleri ve rol örnekleri toowhich tooadd istediğiniz ve hello AzureLogCollector uzantısını etkinleştirmek belirtin.
   
        #Specify your cloud service name
        $ServiceName = 'extensiontest2'
   
        #Specify hello slot. 'Production' or 'Staging'
        $slot = 'Production'
   
        #Specified hello roles on which hello extension will be installed and enabled
        $roles = @("WorkerRole1","WebRole1")
   
        #Specify hello instances on which extension will be installed and enabled.  Use wildcard * for all instances
        $instances = @("*")
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
3. Dosyaları toplanacak hello ek veri klasörü belirtin (Bu adım isteğe bağlıdır).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
   
   > [!NOTE]
   > Belirteci kullanabilirsiniz `%roleroot%` bir sabit sürücü kullanmayan beri toospecify hello rol kök sürücüsünde.
   > 
   > 
4. Hello Azure depolama hesabı adı ve anahtar toowhich toplanan dosyaları karşıya yüklenebilir sağlayın.
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
5. Merhaba SetAzureServiceLogCollector.ps1 (Merhaba hello makalenin sonunda yer alan) için bir bulut hizmeti aşağıdaki tooenable hello AzureLogCollector uzantısı olarak çağırın. Merhaba yürütme tamamlandığında, yüklenen hello dosyasını altında bulabilirsiniz`https://YouareStorageAccountName.blob.core.windows.net/vmlogs`
   
        .\SetAzureServiceLogCollector.ps1 -ServiceName YourCloudServiceName  -Roles $roles  -Instances $instances –Mode $mode -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey -AdditionDataLocationList $AdditionalDataList

Merhaba, toohello komut iletilen hello parametrelerinin hello tanımı aşağıdadır. (Bu aşağıda da kopyalanır.)

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
      [Parameter(Mandatory=$true)]
    [string]   $ServiceName,

    [Parameter(Mandatory=$false)]
    [string[]] $Roles ,

    [Parameter(Mandatory=$false)]
    [string[]] $Instances,

    [Parameter(Mandatory=$false)]
    [string]   $Slot = 'Production',

    [Parameter(Mandatory=$false)]
    [string]   $Mode = 'Full',

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountName,

    [Parameter(Mandatory=$false)]
    [string]   $StorageAccountKey,

    [Parameter(Mandatory=$false)]
    [PSObject[]] $AdditionDataLocationList = $null
    )

* *ServiceName*: Bulut hizmeti adı.
* *Rolleri*: "WebRole1" veya "WorkerRole1" gibi rollerinin bir listesi.
* *Örnekleri*: rol örneklerinin hello adlarının bir listesini virgülle ayrılmış--hello joker karakter dizesi kullanın ("*") tüm rol örnekleri için.
* *Yuva*: Yuva adı. "Üretim" veya "Hazırlama".
* *Mod*: Koleksiyon modu. "Tam" veya "GA".
* *StorageAccountName*: toplanan verileri depolamak için ad, Azure depolama hesabı.
* *StorageAccountKey*: ad, Azure depolama hesabı anahtarı.
* *AdditionalDataLocationList*: Yapı izlenerek hello listesi:
  
      {
      String Name,
      String Location,
      String SearchPattern,
      Bool   Recursive
      }

## <a name="adding-as-a-vm-extension"></a>Bir VM uzantısı olarak ekleme
Merhaba yönergeleri tooconnect Azure PowerShell tooyour abonelik izleyin.

1. Merhaba hizmet adı, VM ve hello koleksiyon modu belirtin.
   
        #Specify your cloud service name
        $ServiceName = 'YourCloudServiceName'
   
        #Specify hello VM name
        $VMName = "'YourVMName'"
   
        #Specify hello collection mode, "Full" or "GA"
        $mode = "GA"
   
        Specify hello additional data folder for which files will be collected (this step is optional).
   
        #add one location
        $a1 = New-Object PSObject
   
        $a1 | Add-Member -MemberType NoteProperty -Name "Name" -Value "StorageData"
        $a1 | Add-Member -MemberType NoteProperty -Name "SearchPattern" -Value "*"
        $a1 | Add-Member -MemberType NoteProperty -Name "Location" -Value "%roleroot%storage"  #%roleroot% is normally E: or F: drive
        $a1 | Add-Member -MemberType NoteProperty -Name "Recursive" -Value "true"
   
        $AdditionalDataList+= $a1
              #more locations can be added....
2. Hello Azure depolama hesabı adı ve anahtar toowhich toplanan dosyaları karşıya yüklenebilir sağlayın.
   
        $StorageAccountName = 'YourStorageAccountName'
        $StorageAccountKey  = ‘YouStorageAccountKey'
3. Merhaba SetAzureVMLogCollector.ps1 (Merhaba hello makalenin sonunda yer alan) için bir bulut hizmeti aşağıdaki tooenable hello AzureLogCollector uzantısı olarak çağırın. Merhaba yürütme tamamlandığında, yüklenen hello dosyasını https://YouareStorageAccountName.blob.core.windows.net/vmlogs altında bulabilirsiniz

Merhaba, toohello komut iletilen hello parametrelerinin hello tanımı aşağıdadır. (Bu aşağıda da kopyalanır.)

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
        [Parameter(Mandatory=$true)]
      [string]   $ServiceName,

      [Parameter(Mandatory=$false)]
      [string] $VMName ,

        [Parameter(Mandatory=$false)]
      [string]   $Mode = 'Full',

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountName,

      [Parameter(Mandatory=$false)]
      [string]   $StorageAccountKey,

      [Parameter(Mandatory=$false)]
      [PSObject[]] $AdditionDataLocationList = $null
      )

* ServiceName: Bulut hizmeti adınız.
* Merhaba VM VMName hello adı.
* : Koleksiyon modu. "Tam" veya "GA".
* StorageAccountName: toplanan verileri depolamak için Azure depolama hesabının adı.
* StorageAccountKey: Azure depolama hesabı anahtarı adı.
* AdditionalDataLocationList: Listesini yapı izlenerek hello:

```
      {
        String Name,
        String Location,
        String SearchPattern,
        Bool   Recursive
      }
```

## <a name="extention-powershell-script-files"></a>Uzantı PowerShell komut dosyaları
SetAzureServiceLogCollector.ps1

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Roles ,

                  [Parameter(Mandatory=$false)]
                  [string[]] $Instances = '*',

                  [Parameter(Mandatory=$false)]
                  [string]   $Slot = 'Production',

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject

    if ($Instances -ne $null -and $Instances.Count -gt 0)  #Instances should be seperated by ,
    {
        $instanceText = $Instances[0]
        for ($i = 1;$i -lt $Instances.Count;$i++)
        {
              $instanceText = $instanceText+ "," + $Instances[$i]
          }
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value $instanceText
    }
    else  #For all instances if not specified.  hello value should be a space or *
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value " "
    }

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json
    "publicConfig is:  $publicConfigJSON"

    #we just provide a empty privateConfig object
    $privateconfig = "{
    }"

    if ($Roles -ne $null)
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot -Role $Roles -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }
    else
    {
          Set-AzureServiceExtension -Service $ServiceName -Slot $Slot  -ExtensionName 'AzureLogCollector' -ProviderNamespace Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.0 -Verbose
    }

    #
    #This is an optional step: generate a sasUri toohello container so it can be shared with other people if nened
    #
    $SasExpireTime = [DateTime]::Now.AddMinutes(120).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rl -Context $context
    $SasUri = $SasUri + "&restype=container&comp=list"
    Write-Output "hello container for uploaded file can be accessed using this link:`r`n$sasuri"


SetAzureVMLogCollector.ps1

    [CmdletBinding(SupportsShouldProcess = $true)]

    param (
                  [Parameter(Mandatory=$true)]
                  [string]   $ServiceName,

                  [Parameter(Mandatory=$false)]
                  [string] $VMName ,

                  [Parameter(Mandatory=$false)]
                  [string]   $Mode = 'Full',

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountName,

                  [Parameter(Mandatory=$false)]
                  [string]   $StorageAccountKey,

                  [Parameter(Mandatory=$false)]
                  [PSObject[]] $AdditionDataLocationList = $null
            )

    $publicConfig = New-Object PSObject
    $publicConfig | Add-Member -MemberType NoteProperty -Name "Instances" -Value "*"

    if ($Mode -ne $null )
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value $Mode
    }
    else
    {
        $publicConfig | Add-Member -MemberType NoteProperty -Name "Mode" -Value "Full"
    }

    #
    #we need tooget hello Sasuri from StorageAccount and containers
    #
    $context = New-AzureStorageContext -Protocol https -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

    $ContainerName = "azurelogcollectordata"
    $existingContainer = Get-AzureStorageContainer -Context $context |  Where-Object { $_.Name -like $ContainerName}
    if ($existingContainer -eq $null)
    {
        "Container ($ContainerName) doesn't exist. Creating it now.."
        New-AzureStorageContainer -Context $context -Name $ContainerName -Permission off
    }

    $ExpiryTime =  [DateTime]::Now.AddMinutes(90).ToString("o")
    $SasUri = New-AzureStorageContainerSASToken -ExpiryTime $ExpiryTime -FullUri -Name $ContainerName -Permission rwl -Context $context
    $publicConfig | Add-Member -MemberType NoteProperty -Name "SasUri" -Value $SasUri

    #
    #Add AdditionalData toocollect data from additional folders
    #
    if ($AdditionDataLocationList -ne $null )
    {
      $publicConfig | Add-Member -MemberType NoteProperty -Name "AdditionalData" -Value $AdditionDataLocationList
    }

    #
    # Convert it tooJSON format
    #
    $publicConfigJSON = $publicConfig | ConvertTo-Json

    Write-Output "PublicConfigurtion is: \r\n$publicConfigJSON"

    #
    #we just provide a empty privateConfig object
    #
    $privateconfig = "{
    }"

    if ($VMName -ne $null )
    {
          $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
          $VM.VM.OSVirtualHardDisk.OS

          if ($VM.VM.OSVirtualHardDisk.OS -like '*Windows*')
          {
                Set-AzureVMExtension -VM $VM -ExtensionName "AzureLogCollector" -Publisher Microsoft.WindowsAzure.Compute -PublicConfiguration $publicConfigJSON -PrivateConfiguration $privateconfig -Version 1.* | Update-AzureVM -Verbose

                #
                #We will check hello VM status toofind if operation by extension has been completed or not. hello completion of hello operation,either succeed or fail, can be indicated by
                #hello presence of SubstatusList field.
                #
                $Completed = $false
                while ($Completed -ne $true)
                {
                        $VM = Get-AzureVM -ServiceName $ServiceName -Name $VMName
                        $status = $VM.ResourceExtensionStatusList | Where-Object {$_.HandlerName -eq "Microsoft.WindowsAzure.Compute.AzureLogCollector"}

                        if ( ($status.Code -ne 0) -and ($status.Status -like '*error*'))
                        {
                            Write-Output "Error status is returned: $($Status.ExtensionSettingStatus.FormattedMessage.Message)."
                              $Completed = $true
                        }
                        elseif (($status.ExtensionSettingStatus.SubstatusList -eq $null -or $status.ExtensionSettingStatus.SubstatusList.Count -lt 1))
                        {
                              $Completed = $false
                              Write-Output "Waiting for operation toocomplete..."
                        }
                        else
                        {
                              $Completed = $true
                              Write-Output "Operation completed."

                        $UploadedFileUri = $Status.ExtensionSettingStatus.SubStatusList[0].FormattedMessage.Message
                              $blob = New-Object Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob($UploadedFileUri)

                      #
                            # This is an optional step:  For easier access toohello file, we can generate a read-only SasUri directly toohello file
                              #
                              $ExpiryTimeRead =  [DateTime]::Now.AddMinutes(120).ToString("o")
                              $ReadSasUri = New-AzureStorageBlobSASToken -ExpiryTime $ExpiryTimeRead  -FullUri  -Blob  $blob.name -Container $blob.Container.Name -Permission r -Context $context

                            Write-Output "hello uploaded file can be accessed using this link: $ReadSasUri"

                              #
                              #This is an optional step:  Remove hello extension after we are done
                              #
                              Get-AzureVM -ServiceName $ServiceName -Name $VMName | Set-AzureVMExtension -Publisher Microsoft.WindowsAzure.Compute -ExtensionName "AzureLogCollector" -Version 1.* -Uninstall | Update-AzureVM -Verbose

                        }
                        Start-Sleep -s 5
                }
          }
          else
          {
              Write-Output "VM OS Type is not Windows, hello extension cannot be enabled"
          }

    }
    else
    {
      Write-Output "VM name is not specified, hello extension cannot be enabled"
    }

## <a name="next-steps"></a>Sonraki Adımlar
Şimdi inceleyin veya çok basit bir konumdan günlüklerinizi kopyalayın.

