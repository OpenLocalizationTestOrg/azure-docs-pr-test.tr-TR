# <a name="common-errors-during-classic-tooazure-resource-manager-migration"></a>Klasik tooAzure Resource Manager geçiş sırasında yaygın hatalar
Bu makale katalogları, Azure Klasik dağıtım modeli toohello Azure Resource Manager yığından Iaas kaynakların hello geçiş sırasında en yaygın hataları ve bunları azaltmanın yollarını hello.

## <a name="list-of-errors"></a>Hata listesi
| Hata dizesi | Risk azaltma |
| --- | --- |
| İç sunucu hatası |Bazı durumlarda bu tekrar denendiğinde geçen, geçici bir hatadır. Toopersist, devam ederse [Azure desteğine başvurun](../articles/azure-supportability/how-to-create-azure-support-request.md) platform günlüklerinin araştırma gerektiği. <br><br> **Not:** hello olay hello destek ekibi tarafından izlenir sonra bu olabilir olarak Lütfen tüm kendinden azaltma çalışmayın ortamınızda istenmeyen sonuçları. |
| HostedService {barındırılan hizmet adı} içindeki {dağıtım adı} Dağıtımı bir PaaS dağıtımı (Web/Çalışan) olduğundan, dağıtımın geçirilmesi desteklenmiyor. |Bu, dağıtım web/çalışan rolü içerdiğinde gerçekleşir. Geçiş yalnızca sanal makineler için desteklenen olduğundan, lütfen hello web/çalışan rolü hello dağıtımdan kaldırın ve geçiş işlemini yeniden deneyin. |
| Şablon {şablon-adı} dağıtımı başarısız oldu. CorrelationId={guid} |Geçiş hizmeti Hello arka uç içinde hello Azure Kaynak Yöneticisi yığınında Azure Resource Manager şablonları toocreate kaynakları kullanırız. Genellikle şablonları ıdempotent olduğundan, bu hata geçmiş hello geçiş işlemi tooget güvenli bir şekilde yeniden deneyebilir. Toopersist bu hata devam ederse, lütfen [Azure desteğine başvurun](../articles/azure-supportability/how-to-create-azure-support-request.md) ve hello correlationıd değeri verin. <br><br> **Not:** hello olay hello destek ekibi tarafından izlenir sonra bu olabilir olarak Lütfen tüm kendinden azaltma çalışmayın ortamınızda istenmeyen sonuçları. |
| Merhaba sanal ağ {sanal ağ-adı} yok. |Merhaba yeni Azure portalında hello sanal ağ oluşturduysanız, bu durum oluşabilir. Merhaba gerçek sanal ağ adı hello düzenini izler "grubu * <VNET name>" |
| HostedService {barındırılan-hizmet-adı} içindeki VM {vm-adı}, Azure Resource Manager'da desteklenmeyen bir Uzantı {uzantı-adı} içeriyor. Toouninstall önerilen geçirme işlemine devam etmeden önce VM hello ondan. |BGInfo 1.* gibi XML uzantıları Azure Resource Manager’da desteklenmez. Bu nedenle bu uzantılar geçirilemez. Bu uzantılar sol yüklü hello sanal makine varsa, bunlar otomatik olarak hello geçişi tamamlamadan önce kaldırılır. |
| HostedService {barındırılan-service-adı} içindeki VM {vm-adı}, VMSnapshot/VMSnapshotLinux Uzantısı içeriyor. Bu uzantının şu an için geçişi desteklenmemektedir. VM hello kaldırın ve yeniden hello geçiş tamamlandıktan sonra Azure Kaynak Yöneticisi'ni kullanarak ekleyin |Bu hello sanal makine için Azure Backup yapılandırıldığı hello senaryodur. Bu şu anda desteklenmeyen bir senaryodur olduğundan, lütfen https://aka.ms/vmbackupmigration adresindeki hello geçici çözüm izleyin |
| VM {vm-adı} {barındırılan-service-adı} içindeki durumu VM hello bildirilmedi uzantı {uzantı-adı} içeriyor. Bu nedenle bu VM geçirilemez. Bu hello uzantı durumunu bildirilen emin olun veya hello uzantısını VM hello Kaldır ve geçiş yeniden deneyin. <br><br> HostedService {barındırılan-hizmet-adı} içindeki VM {vm-adı}, İşleyici Durumu: {işleyici-durumu} bildiren bir Uzantı {uzantı-adı} içeriyor. Bu nedenle, hello VM geçirilemez. Rapor edilen hello uzantısı işleyici durumu {status işleyici} olduğundan emin olun veya VM hello kaldırın ve geçiş yeniden deneyin. <br><br> VM Aracısı VM {vm-adı} {barındırılan-service-adı} içindeki için raporlama hello hazır değil olarak genel aracı durumu. Dinamik geçirilip bir uzantıya sahipse, bu nedenle, hello VM, geçirilmesi değil. Bu hello VM Aracısı hazır olarak genel aracı durumu raporlama emin olun. Toohttps://aka.MS/classiciaasmigrationfaqs bakın. |Azure Konuk Aracısı & VM uzantıları giden internet erişimi toohello VM depolama hesabı toopopulate durumlarını gerekir. Durum hatasının yaygın nedenleri <li> Giden erişim toohello engelleyen ağ güvenlik grubu Internet <li> Merhaba VNET şirket içi DNS sunucuları ve DNS bağlantısı varsa kaybolur <br><br> Toosee desteklenmeyen bir durumu devam ederseniz, bu onay hello uzantıları tooskip kaldırın ve ile geçiş ilerler. |
| HostedService {barındırılan hizmet adı} içindeki {dağıtım adı} Dağıtımı birden fazla Kullanılabilirlik Kümesine sahip olduğundan, dağıtımın geçirilmesi desteklenmiyor. |Şu anda yalnızca bir veya daha az kullanılabilirlik kümesine sahip barındırılan hizmetler geçirilebilir. Bu soruna geçici bir çözüm toowork Lütfen hello kullanılabilirlik kümeleri ve sanal makine bu kullanılabilirlik kümeleri tooa farklı barındırılan hizmetin ek taşıyın. |
| HostedService içinde {dağıtım-adı} dağıtımı için geçiş desteklenmiyor {barındırılan-service-name hello HostedService içeriyor olsa bile, hello kullanılabilirlik kümesi parçası olmayan Vm'lere sahip olduğundan. |Merhaba geçici bir çözüm bu senaryo için tek bir kullanılabilirlik tüm hello sanal makinelerine ayarlayın veya barındırılan hello hizmetinde kullanılabilirlik kümesi hello tüm sanal makineleri kaldırma tooeither taşıma değildir. |
| Depolama hesabı/HostedService/sanal ağ {sanal ağ-adı} Geçirilmekte olan hello işleminin olduğunu ve bu nedenle değiştirilemiyor |Bu hata hello kaynakta hello "Hazırlama" geçiş işlemi tamamlanmış ve değişiklik toohello kaynak yapacağı bir işlem tetiklenir olur. Merhaba kilitlendiğinde nedeniyle hello Yönetim düzeyi "Hazırlama" işleminden sonra herhangi bir değişiklik toohello kaynak engellenir. Merhaba "İptal" geçiş işlemi tooroll geri hello "Hazırlama" işlemi veya toounlock hello Yönetim düzeyi, hello "Yürüt" geçiş işlemi toocomplete geçiş çalıştırabilirsiniz. |
| Durumu: RoleStateUnknown olan bir VM’e sahip olduğundan HostedService {barındırılan-hizmet-adı} için geçişe izin verilmiyor. Geçiş, yalnızca zaman hello aşağıdakilerden biri VM olduğu hello durumları - çalışıyor, durduruldu, durduruldu serbest izin verilir. |Merhaba VM genellikle bir güncelleştirme işlem sırasında sistemin yeniden başlatılması gibi hello HostedService olduğunda, bir durum geçişi gerçekleştiriyor uzantı yükleme vs. Merhaba güncelleştirme işlemi toocomplete hello HostedService üzerinde için geçişi denemeden önce önerilir. |
| HostedService {barındırılan-service-adı} {dağıtım-adı} dağıtımda VM {vm-adı} olan fiziksel blob boyutu {size-of-the-vhd-blob-backing-the-data-disk} bayt hello VM veri diski mantıksal boyutu {eşleşmiyor sahip veri diski {veri disk adı} içerir. size-of-the-Data-disk-specified-in-the-VM-api} bayt sayısı. Geçiş hello Azure Resource Manager VM için hello veri diski boyutu belirtmeden devam edecek. | Bu hata hello boyutu hello VM API modelinde güncelleştirmeden hello VHD blob yeniden boyutlandırılabilir olur. Ayrıntılı sorun giderme adımları [aşağıdadır](#vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-the-vm-data-disk-logical-size-bytes).|
| Bulut Hizmetinde {Bulut-Hizmeti-Adı} VM’si {VM-adı} için medya bağlantısı veri-diski-Uri’si} olan veri diski {veri-diski-adı} doğrulanırken bir depolama özel durumu oluştu. Lütfen bu hello VHD medya bağlantısı bu sanal makine için erişilebilir olduğundan emin olun | Hello Hello diskleri VM silinmiş veya artık erişilebilir değildir, bu hata oluşabilir. Lütfen VM mevcut hello emin hello diskleri olun.|
| HostedService {barındırılan-hizmet-adı} içindeki VM {vm-adı}, blob adı {vhd-blob-adı} olan ve Azure Resource Manager'da desteklenmeyen bir MediaLink'li {vhd-uri’si} Disk içeriyor. | Merhaba blob Hello adına sahip bir "/" işlem kaynak sağlayıcısı şu anda desteklenmeyen da bu hata oluşur. |
| Merhaba bölgesel kapsamda olmadığından geçiş HostedService {bulut hizmet adı} {dağıtım-adı} dağıtımda için izin verilmiyor. Bu dağıtım tooregional kapsamı taşımak için lütfen toohttp://aka.ms/regionalscope bakın. | 2014'te, ağ kaynakları küme düzeyi kapsam tooregional kapsamdan taşınır Azure duyurdu. Ayrıntılar için bkz. [http://aka.ms/regionalscope] (http://aka.ms/regionalscope). Geçirilmekte olan hello dağıtım otomatik olarak tooa bölgesel kapsama taşır bir güncelleştirme işlemi yapılmamış olduğunda bu hata oluşur. En iyi çözüm tooeither bir uç nokta tooa VM eklemek veya bir veri toohello VM disk ve geçiş yeniden olabilir. <br> Bkz: [nasıl uç noktaları sanal bir makinede Klasik Windows Azure yedekleme tooset](../articles/virtual-machines/windows/classic/setup-endpoints.md#create-an-endpoint) veya [bir veri diski tooa Windows hello Klasik dağıtım modeliyle oluşturulan sanal makinenin ekleme](../articles/virtual-machines/windows/classic/attach-disk.md)|


## <a name="detailed-mitigations"></a>Ayrıntılı sorun giderme

### <a name="vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-hello-vm-data-disk-logical-size-bytes"></a>Verileri blob boyutu bayt sayısı, Fiziksel Disk ile VM hello VM veri diski mantıksal boyutu bayt eşleşmiyor.

Bu, Hello mantıksal disk boyutu, veri hello gerçek VHD blob boyutu ile eşitlenmiş alabilirsiniz ortaya çıkar. Bu, aşağıdaki komutları hello kullanarak kolayca doğrulanabilir:

#### <a name="verifying-hello-issue"></a>Merhaba sorunu doğrulanıyor

```PowerShell
# Store hello VM details in hello VM object
$vm = Get-AzureVM -ServiceName $servicename -Name $vmname

# Display hello data disk properties
# NOTE hello data disk LogicalDiskSizeInGB below which is 11GB. Also note hello MediaLink Uri of hello VHD blob as we'll use this in hello next step
$vm.VM.DataVirtualHardDisks


HostCaching         : None
DiskLabel           : 
DiskName            : coreosvm-coreosvm-0-201611230636240687
Lun                 : 0
LogicalDiskSizeInGB : 11
MediaLink           : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
SourceMediaLink     : 
IOType              : Standard
ExtensionData       : 

# Now get hello properties of hello blob backing hello data disk above
# NOTE hello size of hello blob is about 15 GB which is different from LogicalDiskSizeInGB above
$blob = Get-AzureStorageblob -Blob "coreosvm-dd1.vhd" -Container vhds 

$blob

ICloudBlob        : Microsoft.WindowsAzure.Storage.Blob.CloudPageBlob
BlobType          : PageBlob
Length            : 16106127872
ContentType       : application/octet-stream
LastModified      : 11/23/2016 7:16:22 AM +00:00
SnapshotTime      : 
ContinuationToken : 
Context           : Microsoft.WindowsAzure.Commands.Common.Storage.AzureStorageContext
Name              : coreosvm-dd1.vhd
```

#### <a name="mitigating-hello-issue"></a>Azaltıcı hello sorunu

```PowerShell
# Convert hello blob size in bytes tooGB into a variable which we'll use later
$newSize = [int]($blob.Length / 1GB)

# See hello calculated size in GB
$newSize

15

# Store hello disk name of hello data disk as we'll use this tooidentify hello disk toobe updated
$diskName = $vm.VM.DataVirtualHardDisks[0].DiskName

# Identify hello LUN of hello data disk tooremove
$lunToRemove = $vm.VM.DataVirtualHardDisks[0].Lun

# Now remove hello data disk from hello VM so that hello disk isn't leased by hello VM and it's size can be updated
Remove-AzureDataDisk -LUN $lunToRemove -VM $vm | Update-AzureVm -Name $vmname -ServiceName $servicename

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureVM       213xx1-b44b-1v6n-23gg-591f2a13cd16   Succeeded  

# Verify we have hello right disk that's going toobe updated
Get-AzureDisk -DiskName $diskName

AffinityGroup        : 
AttachedTo           : 
IsCorrupted          : False
Label                : 
Location             : East US
DiskSizeInGB         : 11
MediaLink            : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
DiskName             : coreosvm-coreosvm-0-201611230636240687
SourceImageName      : 
OS                   : 
IOType               : Standard
OperationDescription : Get-AzureDisk
OperationId          : 0c56a2b7-a325-123b-7043-74c27d5a61fd
OperationStatus      : Succeeded

# Now update hello disk toohello new size
Update-AzureDisk -DiskName $diskName -ResizedSizeInGB $newSize -Label $diskName

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureDisk     cv134b65-1b6n-8908-abuo-ce9e395ac3e7 Succeeded 

# Now verify that hello "DiskSizeInGB" property of hello disk matches hello size of hello blob 
Get-AzureDisk -DiskName $diskName


AffinityGroup        : 
AttachedTo           : 
IsCorrupted          : False
Label                : coreosvm-coreosvm-0-201611230636240687
Location             : East US
DiskSizeInGB         : 15
MediaLink            : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
DiskName             : coreosvm-coreosvm-0-201611230636240687
SourceImageName      : 
OS                   : 
IOType               : Standard
OperationDescription : Get-AzureDisk
OperationId          : 1v53bde5-cv56-5621-9078-16b9c8a0bad2
OperationStatus      : Succeeded

# Now we'll add hello disk back toohello VM as a data disk. First we need tooget an updated VM object
$vm = Get-AzureVM -ServiceName $servicename -Name $vmname

Add-AzureDataDisk -Import -DiskName $diskName -LUN 0 -VM $vm -HostCaching ReadWrite | Update-AzureVm -Name $vmname -ServiceName $servicename

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureVM       b0ad3d4c-4v68-45vb-xxc1-134fd010d0f8 Succeeded      
```

### <a name="moving-a-vm-tooa-different-subscription-after-completing-migration"></a>Geçişi tamamladıktan sonra VM tooa farklı bir abonelik taşıma

Merhaba geçiş işlemini tamamladıktan sonra toomove hello VM tooanother abonelik isteyebilirsiniz. Ancak, gizli veya sertifikanın varsa, bir anahtar kasası kaynak hello başvuran VM'yi taşıma hello şu anda desteklenmiyor. yönergeler aşağıda Hello tooworkaround hello sorunu izin verir. 

#### <a name="powershell"></a>PowerShell
```powershell
$vm = Get-AzureRmVM -ResourceGroupName "MyRG" -Name "MyVM"
Remove-AzureRmVMSecret -VM $vm
Update-AzureRmVM -ResourceGroupName "MyRG" -VM $vm
```
#### <a name="azure-cli-20"></a>Azure CLI 2.0

```bash
az vm update -g "myrg" -n "myvm" --set osProfile.Secrets=[]
```
