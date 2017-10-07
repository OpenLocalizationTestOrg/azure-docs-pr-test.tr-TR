---
title: "aaaDeploy ve PowerShell kullanarak Azure VM'ler için yedekleme yönetme | Microsoft Docs"
description: "Bilgi nasıl toodeploy ve Azure PowerShell kullanarak yedekleme yönetin."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 2e24b1d9-4375-4049-a28d-e3bc01152f32
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;trinadhk;jimpark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f3ecd3f94c5e3e8fc8018e8786302edd4847744b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azurermbackup-cmdlets-tooback-up-virtual-machines"></a>Sanal makineler yukarı AzureRM.Backup cmdlet'leri tooback kullanın
> [!div class="op_single_selector"]
> * [Resource Manager](backup-azure-vms-automation.md)
> * [Klasik](backup-azure-vms-classic-automation.md)
>
>

Bu makale size nasıl gösterir yedekleme ve kurtarma Azure VM'ler için Azure PowerShell toouse. Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır: Resource Manager ve Klasik. Bu makalede hello Klasik dağıtım modeli tooback veri tooa yedekleme kasası yukarı kullanmayı ele alır. Aboneliğinizde bir yedekleme kasası oluşturmadıysanız, bu makalede, Resource Manager sürümü hello bkz [kullanım AzureRM.RecoveryServices.Backup cmdlet'leri tooback sanal makineleri yedeklemek](backup-azure-vms-automation.md). Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.

> [!IMPORTANT]
> Şimdi, yedekleme kasaları tooRecovery Hizmetleri kasaları yükseltebilirsiniz. Ayrıntılar için hello makalesine bakın [kurtarma Hizmetleri kasası bir yedekleme kasası tooa yükseltme](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft tooupgrade önerir tooRecovery Hizmetleri kasalarının yedekleme kasaları.<br/> 15 Ekim 2017 sonra PowerShell toocreate yedekleme kasaları kullanamazsınız. **1 Kasım 2017’ye kadar**:
>- Kalan tüm yedekleme kasaları otomatik olarak yükseltilen tooRecovery Hizmetleri kasalarının olacaktır.
>- Mümkün tooaccess hello Klasik Portalı'nda, yedekleme verilerinizi olmayacaktır. Bunun yerine, hello Azure portal tooaccess kurtarma Hizmetleri kasalarının, yedekleme verilerinizi kullanın.
>

## <a name="concepts"></a>Kavramlar
Bu makalede belirli toohello PowerShell cmdlet'leri sanal makineleri yedeklemek tooback kullanılan bilgilerini sağlar. Azure sanal makinelerini koruma hakkında giriş bilgileri için lütfen bkz [azure'da VM yedekleme altyapınızı planlama](backup-azure-vms-introduction.md).

> [!NOTE]
> Başlamadan önce hello okuma [Önkoşullar](backup-azure-vms-prepare.md) Azure Backup ve hello gerekli toowork [sınırlamalar](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm) hello geçerli VM yedekleme çözümünün.
>
>

toouse PowerShell etkili bir şekilde ele şu anda toounderstand hello hiyerarşi nesnelerin ve nereden toostart.

![Nesne hiyerarşisi](./media/backup-azure-vms-classic-automation/object-hierarchy.png)

Merhaba iki en önemli akışı VM korumasını etkinleştirmek ve bir kurtarma noktasından geri yüklenmesi. Bu makalenin Hello odak bu iki senaryo hello PowerShell cmdlet'leri tooenable ile çalışma sırasında adept hale toohelp noktasıdır.

## <a name="setup-and-registration"></a>Kurulumu'nu ve kaydı
toobegin:

1. [En son PowerShell indirme](https://github.com/Azure/azure-powershell/releases) (gerekli minimum sürüm: 1.0.0)
2. Hello Azure yedekleme PowerShell cmdlet'leri kullanılabilir hello aşağıdaki komutu yazarak bulabilirsiniz:

```
PS C:\> Get-Command *azurermbackup*

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Backup-AzureRmBackupItem                           1.0.1      AzureRM.Backup
Cmdlet          Disable-AzureRmBackupProtection                    1.0.1      AzureRM.Backup
Cmdlet          Enable-AzureRmBackupContainerReregistration        1.0.1      AzureRM.Backup
Cmdlet          Enable-AzureRmBackupProtection                     1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupContainer                         1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupItem                              1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupJob                               1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupJobDetails                        1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupRecoveryPoint                     1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Get-AzureRmBackupVaultCredentials                  1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupRetentionPolicyObject             1.0.1      AzureRM.Backup
Cmdlet          New-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Register-AzureRmBackupContainer                    1.0.1      AzureRM.Backup
Cmdlet          Remove-AzureRmBackupProtectionPolicy               1.0.1      AzureRM.Backup
Cmdlet          Remove-AzureRmBackupVault                          1.0.1      AzureRM.Backup
Cmdlet          Restore-AzureRmBackupItem                          1.0.1      AzureRM.Backup
Cmdlet          Set-AzureRmBackupProtectionPolicy                  1.0.1      AzureRM.Backup
Cmdlet          Set-AzureRmBackupVault                             1.0.1      AzureRM.Backup
Cmdlet          Stop-AzureRmBackupJob                              1.0.1      AzureRM.Backup
Cmdlet          Unregister-AzureRmBackupContainer                  1.0.1      AzureRM.Backup
Cmdlet          Wait-AzureRmBackupJob                              1.0.1      AzureRM.Backup
```

Merhaba aşağıdaki Kurulum ve kayıt görevler PowerShell ile otomatik olarak yapılabilir:

* Yedekleme kasası oluşturma
* Merhaba VM'ler hello Azure Backup hizmeti ile kaydetme

### <a name="create-a-backup-vault"></a>Yedekleme kasası oluşturma
> [!WARNING]
> Azure Backup hello için ilk kez kullanan müşteriler için aboneliğiniz ile birlikte kullanılan tooregister hello Azure Backup sağlayıcı toobe gerekir. Bu komutu aşağıdaki hello çalıştırarak yapılabilir: Register-AzureRmResourceProvider - ProviderNamespace "Microsoft.Backup"
>
>

Hello kullanarak yeni bir yedekleme kasası oluşturma **yeni AzureRmBackupVault** cmdlet'i. Merhaba yedekleme kasası olan bir ARM kaynak tooplace gereken şekilde bir kaynak grubu içinde. Yükseltilmiş bir Azure PowerShell konsolunda hello aşağıdaki komutları çalıştırın:

```
PS C:\> New-AzureRmResourceGroup –Name “test-rg” –Location “West US”
PS C:\> $backupvault = New-AzureRmBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

Tüm hello yedekleme kasalarının listesi hello kullanarak belirli bir abonelikte alabilirsiniz **Get-AzureRmBackupVault** cmdlet'i.

> [!NOTE]
> Uygun toostore hello yedekleme kasası nesnesine bir değişken değil. Merhaba kasası nesne birçok Azure yedekleme cmdlet'lerini için bir giriş olarak gereklidir.
>
>

### <a name="registering-hello-vms"></a>Merhaba VM'ler kaydetme
Merhaba ilk adım yapılandırma doğrultusunda Azure Backup ile yedekleme tooregister makine ya da VM Azure yedek kasası ile değil. Merhaba **Register-AzureRmBackupContainer** cmdlet'i bir Azure Iaas sanal makinenin hello giriş bilgilerini alır ve hello belirtilen kasası ile kaydeder. Merhaba kayıt işlemi hello Azure sanal makinesi hello yedek kasası ile ilişkilendirir ve parçaları VM hello yedekleme yaşam döngüsü ile Merhaba.

VM hello Azure Backup hizmeti ile kaydetme bir üst düzey kapsayıcısı nesnesi oluşturur. Bir kapsayıcı genellikle yedeklenebilir birden çok öğe içeriyor, ancak sanal makineleri hello durumda olacaktır hello kapsayıcısı için yalnızca bir yedekleme öğesi.

```
PS C:\> $registerjob = Register-AzureRmBackupContainer -Vault $backupvault -Name "testvm" -ServiceName "testvm"
```

## <a name="backup-azure-vms"></a>Azure sanal makinelerini yedekleme
### <a name="create-a-protection-policy"></a>Bir koruma ilkesi oluşturun
Zorunlu toocreate yeni bir koruma İlkesi toostart yedeğini Vm'leriniz değil. bir 'varsayılan kullanılan tooquickly etkinleştir koruma olabilir ve daha sonra hello sağ ayrıntılarla düzenlenen ilke' Hello kasası gelir. Hello kullanarak hello kasasına kullanılabilir hello ilkelerinin bir listesini alabilirsiniz **Get-AzureRmBackupProtectionPolicy** cmdlet:

```
PS C:\> Get-AzureRmBackupProtectionPolicy -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DefaultPolicy             AzureVM            Daily              26-Aug-15 12:30:00 AM
```

> [!NOTE]
> PowerShell'de hello BackupTime alanının Hello saat dilimi UTC değil. Merhaba yedekleme saati hello Azure portal gösterildiğinde, ancak hello saat dilimi hizalanmış tooyour yerel hello UTC uzaklığı birlikte sistemidir.
>
>

Bir yedekleme İlkesi, en az bir bekletme ilkesi ile ilişkilidir. Merhaba bekletme ilkesi ne kadar bir kurtarma noktası Azure yedekleme ile tutulan tanımlar. Merhaba **yeni AzureRmBackupRetentionPolicy** cmdlet bekletme ilkesi bilgileri tutun PowerShell nesneler oluşturur. Bu bekletme ilkesi nesneler toohello girdi olarak kullanılır *yeni AzureRmBackupProtectionPolicy* cmdlet'ini veya doğrudan hello *etkinleştir AzureRmBackupProtection* cmdlet'i.

Bir yedekleme İlkesi zaman ve ne sıklıkta hello öğenin yedekleme yapılır tanımlar. Merhaba **yeni AzureRmBackupProtectionPolicy** cmdlet'i, yedekleme ilkesi bilgilerini tutan bir PowerShell nesnesi oluşturur. Merhaba yedekleme İlkesi bir giriş toohello kullanılan *etkinleştir AzureRmBackupProtection* cmdlet'i.

```
PS C:\> $Daily = New-AzureRmBackupRetentionPolicyObject -DailyRetention -Retention 30
PS C:\> $newpolicy = New-AzureRmBackupProtectionPolicy -Name DailyBackup01 -Type AzureVM -Daily -BackupTime ([datetime]"3:30 PM") -RetentionPolicy $Daily -Vault $backupvault

Name                      Type               ScheduleType       BackupTime
----                      ----               ------------       ----------
DailyBackup01             AzureVM            Daily              01-Sep-15 3:30:00 PM
```

### <a name="enable-protection"></a>Korumayı etkinleştir
Koruma etkinleştirme işlemi iki nesne kapsar - hello öğesi ve hello İlkesi ve her iki gereksinim toobelong toohello aynı Kasa. Hello İlkesi hello öğeyle ilişkili silindikten sonra hello yedekleme iş akışı hello tanımlı zamanlamasında ilkenin etkisini gösterip.

```
PS C:\> Get-AzureRmBackupContainer -Type AzureVM -Status Registered -Vault $backupvault | Get-AzureRmBackupItem | Enable-AzureRmBackupProtection -Policy $newpolicy
```

### <a name="initial-backup"></a>İlk yedekleme
Merhaba yedekleme zamanlaması hello tam ilk kopya hello öğesi için ve hello artımlı kopya hello sonraki yedeklemeler için yapma ilgilenebilmek. Ancak, tooforce hello ilk yedekleme toohappen belirli bir zamanda veya hatta hemen istiyorsanız sonra hello kullanın **yedekleme AzureRmBackupItem** cmdlet:

```
PS C:\> $container = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -Name "testvm"
PS C:\> $backupjob = Get-AzureRmBackupItem -Container $container | Backup-AzureRmBackupItem
PS C:\> $backupjob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

> [!NOTE]
> hello StartTime saat dilimini hello ve PowerShell içinde gösterilen EndTime alan UTC değil. Ancak, Hello benzer bilgiler hello Azure portal gösterildiğinde hello saat dilimi hizalanmış tooyour yerel sistem saatini ' dir.
>
>

### <a name="monitoring-a-backup-job"></a>Bir yedekleme işi izleme
Azure Backup çoğu uzun süre çalışan işlemleri, bir iş olarak modelled. Bu işlem, her zaman tookeep hello Azure portal açık gerek kalmadan kolay tootrack ilerleme kolaylaştırır.

tooget hello son bir devam eden işin durumunu, kullanım hello **Get-AzureRmBackupJob** cmdlet'i.

```
PS C:\> $joblist = Get-AzureRmBackupJob -Vault $backupvault -Status InProgress
PS C:\> $joblist[0]

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Backup          InProgress      01-Sep-15 12:24:01 PM  01-Jan-01 12:00:00 AM
```

Bu işleri - gereksiz, ek kod olan - tamamlanması için yoklama yerine basit toouse hello olan **bekleme AzureRmBackupJob** cmdlet'i. Bir komut dosyası kullanıldığında, hello cmdlet hello işi tamamlar veya hello belirtilen zaman aşımı değerine ulaşılana kadar hello yürütme duraklatılır.

```
PS C:\> Wait-AzureRmBackupJob -Job $joblist[0] -Timeout 43200
```


## <a name="restore-an-azure-vm"></a>Bir Azure VM geri yükleme
Sipariş toorestore yedekleme verilerini, hello zaman içinde nokta verilerini tutan hello kurtarma noktası ve madde yedeklenen tooidentify hello gerekir. Bu bilgiler sağlanan toohello geri yükleme-AzureRmBackupItem cmdlet'i tooinitiate hello kasa toohello müşterinin hesap verilerini geri yükleme olur.

### <a name="select-hello-vm"></a>Merhaba VM seçin
tanımlayan tooget hello PowerShell nesnesi Merhaba doğru yedekleme öğesi, hello kapsayıcı hello kasasında gelen toostart gerekir ve nesne hiyerarşisi aşağı, şekilde çalışır. Merhaba VM, kullanım hello temsil eden tooselect hello kapsayıcı **Get-AzureRmBackupContainer** cmdlet'i ve o toohello kanal **Get-AzureRmBackupItem** cmdlet'i.

```
PS C:\> $backupitem = Get-AzureRmBackupContainer -Vault $backupvault -Type AzureVM -name "testvm" | Get-AzureRmBackupItem
```

### <a name="choose-a-recovery-point"></a>Bir kurtarma noktası seçin
Hello kullanarak hello yedekleme öğesi için tüm hello kurtarma noktalarını şimdi listeleyebilirsiniz **Get-AzureRmBackupRecoveryPoint** cmdlet'ini ve hello kurtarma noktası toorestore'i seçin. Genellikle hello en son kullanıcıların çekme *AppConsistent* noktası hello listesinde.

```
PS C:\> $rp =  Get-AzureRmBackupRecoveryPoint -Item $backupitem
PS C:\> $rp

RecoveryPointId    RecoveryPointType  RecoveryPointTime      ContainerName
---------------    -----------------  -----------------      -------------
15273496567119     AppConsistent      01-Sep-15 12:27:38 PM  iaasvmcontainer;testvm;testv...
```

Merhaba değişkeni ```$rp``` kurtarma noktaları dizisidir hello ters sırada süresini sıralanmış yedekleme öğesi seçili - hello en son kurtarma noktası dizini 0 için. Standart PowerShell dizi toopick hello kurtarma noktası dizin kullanın. Örneğin: ```$rp[0]``` hello en son kurtarma noktası seçin.

### <a name="restoring-disks"></a>Diskleri geri yükleme
Azure PowerShell ve hello Azure portal aracılığıyla yapılır hello geri yükleme işlemleri arasındaki en önemli fark yoktur. PowerShell ile Merhaba diskleri ve yapılandırma bilgilerini hello kurtarma noktasından geri yükleme sırasında hello geri yükleme işlemi durdurur. Bir sanal makine oluşturmaz.

> [!WARNING]
> Merhaba geri yükleme AzureRmBackupItem VM oluşturmaz. Yalnızca hello diskleri geri yükler toohello belirtilen depolama hesabı. Bu olduğu değil hello aynı davranışı hello Azure portal karşılaşırsınız.
>
>

```
PS C:\> $restorejob = Restore-AzureRmBackupItem -StorageAccountName "DestAccount" -RecoveryPoint $rp[0]
PS C:\> $restorejob

WorkloadName    Operation       Status          StartTime              EndTime
------------    ---------       ------          ---------              -------
testvm          Restore         InProgress      01-Sep-15 1:14:01 PM   01-Jan-01 12:00:00 AM
```

Hello kullanarak hello geri yükleme işlemi hello ayrıntılarını alabilirsiniz **Get-AzureRmBackupJobDetails** hello geri yükleme işi tamamlandıktan sonra cmdlet'i. Merhaba *ErrorDetails* özelliği, toorebuild hello VM hello bilgileri olacaktır.

```
PS C:\> $restorejob = Get-AzureRmBackupJob -Job $restorejob
PS C:\> $details = Get-AzureRmBackupJobDetails -Job $restorejob
```

### <a name="build-hello-vm"></a>Merhaba VM oluşturma
Yapı hello VM geri hello diskleri dışında yapılabilir hello eski Azure Service Management PowerShell cmdlet'leri, yeni Azure Resource Manager şablonları hello veya hatta hello Azure portal kullanarak. Hızlı bir örnekte göstereceğiz nasıl tooget hello Azure Hizmet Yönetimi cmdlet'lerini kullanarak vardır.

```
$properties  = $details.Properties

$storageAccountName = $properties["Target Storage Account Name"]
$containerName = $properties["Config Blob Container Name"]
$blobName = $properties["Config Blob Name"]

$keys = Get-AzureStorageKey -StorageAccountName $storageAccountName
$storageAccountKey = $keys.Primary
$storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey


$destination_path = "C:\Users\admin\Desktop\vmconfig.xml"
Get-AzureStorageBlobContent -Container $containerName -Blob $blobName -Destination $destination_path -Context $storageContext


$obj = [xml](((Get-Content -Path $destination_path -Encoding UniCode)).TrimEnd([char]0x00))
$pvr = $obj.PersistentVMRole
$os = $pvr.OSVirtualHardDisk
$dds = $pvr.DataVirtualHardDisks
$osDisk = Add-AzureDisk -MediaLocation $os.MediaLink -OS $os.OS -DiskName "panbhaosdisk"
$vm = New-AzureVMConfig -Name $pvr.RoleName -InstanceSize $pvr.RoleSize -DiskName $osDisk.DiskName

if (!($dds -eq $null))
{
    foreach($d in $dds.DataVirtualHardDisk)
    {
        $lun = 0
        if(!($d.Lun -eq $null))
        {
            $lun = $d.Lun
        }
        $name = "panbhadataDisk" + $lun
        Add-AzureDisk -DiskName $name -MediaLocation $d.MediaLink
        $vm | Add-AzureDataDisk -Import -DiskName $name -LUN $lun
    }
}

New-AzureVM -ServiceName "panbhasample" -Location "SouthEast Asia" -VM $vm
```

Toobuild geri hello disklerden VM hakkında daha fazla bilgi için aşağıdaki cmdlet'leri hello hakkında okuyun:

* [Ekleme AzureDisk](https://msdn.microsoft.com/library/azure/dn495252.aspx)
* [AzureVMConfig yeni](https://msdn.microsoft.com/library/azure/dn495159.aspx)
* [Yeni-AzureVM](https://msdn.microsoft.com/library/azure/dn495254.aspx)

## <a name="code-samples"></a>Kod örnekleri
### <a name="1-get-hello-completion-status-of-job-sub-tasks"></a>1. İş alt görevleri Hello tamamlanma durumunu Al
tootrack hello tamamlanma durumunu tek tek alt görevler, kullanabileceğiniz hello **Get-AzureRmBackupJobDetails** cmdlet:

```
PS C:\> $details = Get-AzureRmBackupJobDetails -JobId $backupjob.InstanceId -Vault $backupvault
PS C:\> $details.SubTasks

Name                                                        Status
----                                                        ------
Take Snapshot                                               Completed
Transfer data tooBackup vault                               InProgress
```

### <a name="2-create-a-dailyweekly-report-of-backup-jobs"></a>2. Yedekleme işleri günlük/haftalık raporunu oluşturma
Yöneticiler genellikle hangi yedekleme işleri hello son 24 saat çalışan tooknow Bu yedekleme işlerini hello durumunu istiyor. Ayrıca, aktarılan veri miktarını hello yolu tooestimate yöneticilere sunar aylık veri kullanımı. Aşağıdaki Hello komut dosyası hello Azure Backup hizmeti hello ham veri çeker ve hello PowerShell konsolunda hello bilgileri görüntüler.

```
param(  [Parameter(Mandatory=$True,Position=1)]
        [string]$backupvaultname,

        [Parameter(Mandatory=$False,Position=2)]
        [int]$numberofdays = 7)


#Initialize variables
$DAILYBACKUPSTATS = @()
$backupvault = Get-AzureRmBackupVault -Name $backupvaultname
$enddate = ([datetime]::Today).AddDays(1)
$startdate = ([datetime]::Today)

for( $i = 1; $i -le $numberofdays; $i++ )
{
    # We query one day at a time because pulling 7 days of data might be too much
    $dailyjoblist = Get-AzureRmBackupJob -Vault $backupvault -From $startdate -too$enddate -Type AzureVM -Operation Backup
    Write-Progress -Activity "Getting job information for hello last $numberofdays days" -Status "Day -$i" -PercentComplete ([int]([decimal]$i*100/$numberofdays))

    foreach( $job in $dailyjoblist )
    {
        #Extract hello information for hello reports
        $newstatsobj = New-Object System.Object
        $newstatsobj | Add-Member -Type NoteProperty -Name Date -Value $startdate
        $newstatsobj | Add-Member -Type NoteProperty -Name VMName -Value $job.WorkloadName
        $newstatsobj | Add-Member -Type NoteProperty -Name Duration -Value $job.Duration
        $newstatsobj | Add-Member -Type NoteProperty -Name Status -Value $job.Status

        $details = Get-AzureRmBackupJobDetails -Job $job
        $newstatsobj | Add-Member -Type NoteProperty -Name BackupSize -Value $details.Properties["Backup Size"]
        $DAILYBACKUPSTATS += $newstatsobj
    }

    $enddate = $enddate.AddDays(-1)
    $startdate = $startdate.AddDays(-1)
}

$DAILYBACKUPSTATS | Out-GridView
```

Özellikleri toothis rapor çıktısı grafik tooadd istiyorsanız, hello TechNet blog gönderisi öğrenin [PowerShell ile Grafikleme](http://blogs.technet.com/b/richard_macdonald/archive/2009/04/28/3231887.aspx)

## <a name="next-steps"></a>Sonraki adımlar
Windows Server, koruma için hello PowerShell makale PowerShell tooengage Azure kaynaklarınızı ile kullanmayı tercih ediyorsanız kullanıma [dağıtma ve yönetme yedekleme için Windows Server](backup-client-automation-classic.md). Ayrıca DPM yedeklemelerini yönetmek için PowerShell makale olduğu [dağıtma ve yönetme yedekleme DPM için](backup-dpm-automation-classic.md). Bu makaleler her ikisi de Resource Manager dağıtımları ve bunun yanı sıra klasik dağıtımlar için bir sürümüne sahipsiniz.
