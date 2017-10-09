---
title: "aaaAutomated yedekleme v2 için SQL Server 2016 Azure sanal makineleri | Microsoft Docs"
description: "SQL Server 2016 Azure'da çalışan VM'ler için Hello otomatik yedekleme özelliğini açıklar. Bu makalede hello Kaynak Yöneticisi'ni kullanarak belirli tooVMs ' dir."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: ebd23868-821c-475b-b867-06d4a2e310c7
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/05/2017
ms.author: jroth
ms.openlocfilehash: a322792fb22c76bfa74fafb711b8b1927a6e2b3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-v2-for-sql-server-2016-azure-virtual-machines-resource-manager"></a>SQL Server 2016 Azure sanal makineleri için (Resource Manager) yedekleme v2 otomatik

> [!div class="op_single_selector"]
> * [SQL Server 2014](virtual-machines-windows-sql-automated-backup.md)
> * [SQL Server 2016](virtual-machines-windows-sql-automated-backup-v2.md)

Otomatik yedekleme v2 otomatik olarak yapılandırır [yönetilen yedekleme tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) Azure VM'de SQL Server 2016 Standard, Enterprise veya Geliştirici sürümlerini çalıştıran tüm mevcut ve yeni veritabanları için. Bu, dayanıklı Azure blob depolama alanını tooconfigure normal veritabanı yedeklemeleri sağlar. Otomatik yedekleme v2 bağlıdır hello üzerinde [SQL Server Iaas Aracısı uzantısı](virtual-machines-windows-sql-server-agent-extension.md).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a>Ön koşullar
toouse otomatik yedekleme v2 hello aşağıdaki önkoşulları gözden geçirin:

**İşletim sistemi**:

- Windows Server 2012 R2
- Windows Server 2016

**SQL Server sürümü/yayını**:

- SQL Server 2016 Standard
- SQL Server 2016 Enterprise
- SQL Server 2016 Developer

> [!IMPORTANT]
> Otomatik yedekleme v2 SQL Server 2016 ile çalışır. SQL Server 2014 kullanıyorsanız, veritabanlarınızı otomatik yedekleme v1 tooback kullanabilirsiniz. Daha fazla bilgi için bkz: [otomatik yedekleme SQL Server 2014 Azure Virtual Machines için](virtual-machines-windows-sql-automated-backup.md).

**Veritabanı yapılandırması**:

- Hedef veritabanlarına hello tam kurtarma modeli kullanmanız gerekir. Daha fazla bilgi hello tam kurtarma modeli için hello etkisi hakkında yedeklemeleri üzerinde [yedekleme altında tam kurtarma modeli hello](https://technet.microsoft.com/library/ms190217.aspx).
- Sistem veritabanlarının toouse tam kurtarma modeli yok. Ancak, günlük yedekleri toobe Model veya MSDB alınan ihtiyacınız varsa, tam kurtarma modeli kullanmanız gerekir.
- Hedef veritabanlarına hello varsayılan SQL Server örneğinde olması gerekir. SQL Server Iaas uzantısı Hello adlandırılmış örnekleri desteklemez.

**Azure dağıtım modeli**:

- Resource Manager

> [!NOTE]
> Otomatik yedekleme dayanır hello üzerinde **SQL Server Iaas Aracısı uzantısı**. Geçerli SQL sanal makineye Galerisi görüntülerini varsayılan olarak bu uzantı ekleyin. Daha fazla bilgi için bkz: [SQL Server Iaas Aracısı uzantısı](virtual-machines-windows-sql-server-agent-extension.md).

## <a name="settings"></a>Ayarlar
Merhaba aşağıdaki tabloda otomatik yedekleme v2 için yapılandırılabilir hello seçenekleri açıklanmaktadır. Merhaba gerçek yapılandırma adımlarını hello Azure portalında veya Azure Windows PowerShell komutlarını kullanmadığınıza bağlı olarak farklılık gösterir.

### <a name="basic-settings"></a>Temel ayarlar

| Ayar | Aralık (varsayılan) | Açıklama |
| --- | --- | --- |
| **Otomatik Yedekleme** | Etkinleştir/devre dışı bırak (devre dışı) | Etkinleştirir veya SQL Server 2016 Standard veya Enterprise çalıştıran bir Azure VM için otomatik yedekleme devre dışı bırakır. |
| **Saklama süresi** | 1-30 gün (30 gün) | gün tooretain yedeklemeler Hello sayısı. |
| **Depolama hesabı** | Azure depolama hesabı | Blob depolama alanına otomatik yedekleme dosyalarını depolamak için bir Azure depolama hesabı toouse. Bir kapsayıcı sırasında bu konumu toostore tüm yedekleme dosyaları oluşturulur. Merhaba yedekleme dosyası adlandırma hello tarih, saat ve veritabanı GUID'si içerir. |
| **Şifreleme** |Etkinleştir/devre dışı bırak (devre dışı) | Etkinleştirir veya şifreleme devre dışı bırakır. Şifreleme etkinleştirildiğinde, hello kullanılan sertifikaları toorestore hello yedekleme bulunur hello belirtilen depolama hesabı hello aynı **automaticbackup** bir kapsayıcı kullanılarak hello aynı adlandırma kuralı. Merhaba parola değişirse, bu parola ile yeni bir sertifika oluşturulur, ancak toorestore önceki yedeklemeleri hello eski sertifika kalır. |
| **Parola** |Parola metin | Şifreleme anahtarları için bir parola. Yalnızca budur şifreleme etkin olup olmadığını gerekli. Sipariş toorestore şifreli bir yedekleme hello doğru parolayı ve hello yedeğin alındığı hello zamanında kullanılan ilgili sertifika olmalıdır. |

### <a name="advanced-settings"></a>Gelişmiş ayarlar

| Ayar | Aralık (varsayılan) | Açıklama |
| --- | --- | --- |
| **Sistem Veritabanı Yedeklemeleri** | Etkinleştir/devre dışı bırak (devre dışı) | Etkinleştirildiğinde, bu özellik ayrıca hello sistem veritabanlarını yedekleyin: Master, MSDB ve Model. Merhaba MSDB ve modeli veritabanları için günlük yedekleri toobe gerçekleştirilecek istiyorsanız, bunların tam kurtarma modunda olduğunu doğrulayın. Günlük yedeklemeler için ana hiçbir zaman alınır. Ve yedekleme TempDB için alınır. |
| **Yedekleme zamanlaması** | El ile otomatik / (otomatik) | Varsayılan olarak, hello Günlük büyüme üzerinde temel hello yedekleme zamanlaması otomatik olarak belirlenir. El ile yedekleme zamanlaması hello kullanıcı toospecify hello zaman penceresi için yedeklemeler sağlar. Bu durumda, yedeklemeler yalnızca şimdiye kadar sürer hello yerinde sıklığı belirtilen ve belirli bir günde zaman penceresi sırasında hello belirtilen. |
| **Tam yedekleme sıklığı** | Günlük/Haftalık | Tam yedeklemelerinin sıklığını. Her iki durumda da, tam yedeklemeler hello sonraki zamanlanmış zaman penceresi sırasında başlar. Haftalık seçili olduğunda, yedeklemelerin tüm veritabanları başarıyla yedeklediyseniz kadar birden fazla gün kapsayabilir. |
| **Tam yedekleme başlangıç saati** | 00:00 – 23:00 (01:00) | Başlangıç sırasında tam yedeklemeler gerçekleştirilebildiği belirli bir gün zamanı. |
| **Tam yedekleme zaman penceresi** | 1 – 23 saat (1 saat) | Hangi sırasında tam yedeklemeler gerçekleştirilebildiği belirli bir gün hello zaman penceresinin süresi. |
| **Günlük yedekleme sıklığı** | 5 – 60 dakika (60 dakika) | Günlük yedekleme sıklığı. |

## <a name="understanding-full-backup-frequency"></a>Tam yedekleme sıklığını anlama
Bu önemli toounderstand hello günlük ve haftalık tam yedeklemeler arasındaki farktır. Bu çaba içinde iki örnek senaryolar üzerinden size yol gösterir.

### <a name="scenario-1-weekly-backups"></a>Senaryo 1: Haftalık yedekleri
Çok büyük veritabanları sayısını içeren bir SQL Server VM var.

Pazartesi günü, ayarlar aşağıdaki hello ile otomatik yedekleme v2 etkinleştirin:

- Yedekleme zamanlaması: **el ile**
- Tam yedekleme sıklığını: **haftalık**
- Tam yedekleme başlangıç saati: **01:00**
- Tam yedekleme zaman penceresi: **1 saat**

Bu, o hello sonraki kullanılabilir Yedekleme penceresi 1 saat 1 sabah Salı olduğu anlamına gelir. O anda aynı anda veritabanlarınızı bir yedekleme otomatik yedekleme başlar. Bu senaryoda, veritabanlarınızı tam yedeklemeler için ilk birkaç veritabanları hello tamamlayacak yeterli büyüklükte. Ancak, bir saat sonra tüm hello veritabanları yedeklendi.

Bu durumda, sonraki gün, 1 saat 1 sabah Çarşamba veritabanları hello kalan hello yedekleme otomatik yedekleme başlar. Bu süre içinde tüm veritabanları yedeklenmiş, yeniden hello sonraki gün aynı hello deneyecek zaman. Tüm veritabanları başarıyla yedeklendi kadar devam eder.

Salı yeniden ulaştıktan sonra bir kez daha tüm veritabanlarını yedekleme otomatik yedekleme başlar.

Bu senaryo, otomatik yedekleme yalnızca hello belirtilen zaman penceresi içinde çalışır ve her veritabanı haftada bir kez yukarı yedeklenen gösterir. Bu, ayrıca yedeklemeler toospan hello birden çok gün servis talebi için burada olası toocomplete değil tüm yedeklemeler tek bir günde, olası olduğunu gösterir.

### <a name="scenario-2-daily-backups"></a>Senaryo 2: Günlük yedeklemeler
Çok büyük veritabanları sayısını içeren bir SQL Server VM var.

Pazartesi günü, ayarlar aşağıdaki hello ile otomatik yedekleme v2 etkinleştirin:

- Yedekleme zamanlaması: el ile
- Tam yedekleme sıklığını: günlük
- Tam yedekleme başlangıç saati: 22:00
- Tam yedekleme zaman penceresi: 6 saat

Bu, o hello sonraki kullanılabilir Yedekleme penceresi 10 PM 6 saat boyunca Pazartesi altındadır anlamına gelir. O anda aynı anda veritabanlarınızı bir yedekleme otomatik yedekleme başlar.

Ardından, 6 saat boyunca 10 Salı günü, tüm veritabanlarının tam yedeklemeler yeniden başlatılacak.

> [!IMPORTANT]
> Günlük yedeklemeler zamanlarken, tüm veritabanları, bu süre içinde yedeklenebilir geniş zaman penceresi tooensure zamanla tavsiye edilir. Bu, özellikle çok miktarda veri tooback sahip olduğu yukarı hello durumda önemlidir.

## <a name="configuration-in-hello-portal"></a>Merhaba Portal Yapılandırması

Hello Azure portal tooconfigure otomatik yedekleme v2 sağlama sırasında veya var olan SQL Server 2016 VM'ler için kullanabilirsiniz.

### <a name="new-vms"></a>Yeni sanal makineleri

Merhaba Resource Manager dağıtım modelinde yeni bir SQL Server 2016 sanal makine oluşturduğunuzda hello Azure portal tooconfigure otomatik yedekleme v2 kullanın. 

Merhaba, **SQL Server ayarları** dikey penceresinde, select **otomatik yedekleme**. Merhaba aşağıdaki Azure portal ekran görüntüsü gösterir hello **SQL otomatik yedekleme** dikey.

![Azure portalında SQL otomatik yedekleme yapılandırması](./media/virtual-machines-windows-sql-automated-backup-v2/automated-backup-blade.png)

> [!NOTE]
> Otomatik yedekleme v2 varsayılan olarak devre dışıdır.

Bağlam için hello tam üzerinde konusuna [azure'da bir SQL Server sanal makine sağlama](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>Var olan sanal makineleri

Var olan SQL Server sanal makineler için SQL Server sanal makine seçin. Merhaba seçip **SQL Server yapılandırma** hello bölümünü **ayarları** dikey.

![Var olan VM'ler için SQL otomatik yedekleme](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration.png)

Merhaba, **SQL Server yapılandırma** dikey penceresinde hello tıklatın **Düzenle** hello düğmesini otomatik yedekleme bölümü.

![SQL otomatik yedekleme var olan VM'ler için yapılandırma](./media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration-edit.png)

Tamamlandığında, hello tıklatın **Tamam** hello hello alt düğmesinde **SQL Server yapılandırma** dikey toosave değişikliklerinizi.

Otomatik yedekleme hello için ilk kez etkinleştiriyorsanız Azure hello SQL Server Iaas Aracısı hello arka planda yapılandırır. Bu süre boyunca hello Azure portal otomatik yedekleme yapılandırıldığını gösterilmeyebilir. Merhaba Aracısı toobe yüklü, birkaç dakika bekleyin yapılandırılmış. Bu hello sonra Azure portalı hello yeni ayarları yansıtır.

## <a name="configuration-with-powershell"></a>PowerShell ile yapılandırma

PowerShell tooconfigure otomatik yedekleme v2 kullanabilirsiniz. Başlamadan önce şunları yapmalısınız:

- [Karşıdan yükleme ve en son Azure PowerShell hello](http://aka.ms/webpi-azps).
- Windows PowerShell'i açın ve hesabınızla ilişkilendirebilirsiniz. Merhaba hello adımları izleyerek bunu yapabilirsiniz [aboneliğinizi yapılandırma](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) konu sağlama hello bölümü.

### <a name="install-hello-sql-iaas-extension"></a>Merhaba SQL Iaas uzantısı yükleyin
SQL Server sanal makineden hello Azure portal sağlanan, hello SQL Server Iaas uzantısı zaten yüklü olmalıdır. Bu VM için çağırarak yüklü olup olmadığını belirlemek **Get-AzureRmVM** komutu ve hello inceleyerek **uzantıları** özelliği.

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions 
```

SQL Server Iaas Aracısı uzantısı Hello yüklediyseniz, "Sqlıaasagent" veya "SQLIaaSExtension" olarak listelenen görmeniz gerekir. **ProvisioningState** için hello uzantısı "Başarılı" göstermesi gerekir. 

Yüklü değil ya da sağlanan toobe başarısız olursa, komutu aşağıdaki hello ile yükleyebilirsiniz. Toplama toohello VM adını ve kaynak grubunda de hello bölge belirtmeniz gerekir (**$region**), VM bulunur.

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region 
```

### <a id="verifysettings"></a>Geçerli ayarlarını doğrulayın
Sağlama işlemi sırasında otomatik yedekleme etkinleştirilirse, geçerli yapılandırmanızı PowerShell toocheck kullanabilirsiniz. Merhaba çalıştırmak **Get-AzureRmVMSqlServerExtension** komut ve hello inceleyin **AutoBackupSettings** özelliği:

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

Çıktı benzer toohello aşağıdaki almanız gerekir:

```
Enable                      : True
EnableEncryption            : False
RetentionPeriod             : 30
StorageUrl                  : https://test.blob.core.windows.net/
StorageAccessKey            :  
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : Manual
FullBackupFrequency         : WEEKLY
FullBackupStartTime         : 2
FullBackupWindowHours       : 2
LogBackupFrequency          : 60
```

Çıktı gösteriyorsa **etkinleştirmek** çok ayarlanır**yanlış**, tooenable otomatik yedekleme sahip. Merhaba iyi haber etkinleştirme ve otomatik yedekleme hello yapılandırma olan şekilde. Bu bilgi Hello sonraki bölüme bakın.

> [!NOTE] 
> Hemen bir değişiklik yaptıktan sonra hello ayarlarını denetleyin, hello eski yapılandırma değerlerini geri alırsınız mümkündür. Birkaç dakika bekleyin ve hello ayarlarını kontrol edin yeniden değişikliklerinizi uygulandığından emin toomake.

### <a name="configure-automated-backup-v2"></a>Otomatik yedekleme v2 yapılandırın
Toomodify yanı sıra PowerShell tooenable otomatik yedekleme yapılandırması ve davranış herhangi bir zamanda kullanabilirsiniz. 

İlk olarak, seçin veya yedekleme dosyalarını hello için bir depolama hesabı oluşturun. Merhaba aşağıdaki komut dosyasını bir depolama hesabı seçer veya henüz yoksa oluşturur.

```powershell
$storage_accountname = “yourstorageaccount”
$storage_resourcegroupname = $resourcegroupname

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region } 
```

> [!NOTE]
> Otomatik yedekleme premium depolama alanına depolanmasını yedeklemeleri desteklemez, ancak Premium depolama kullanan VM diskleri yedeklemelerden alabilir.

Merhaba kullanmak **yeni AzureRmVMSqlServerAutoBackupConfig** komut tooenable ve hello Azure depolama hesabında hello otomatik yedekleme v2 ayarları toostore yedeklemelerini yapılandırın. Bu örnekte, 10 gün boyunca tutulur toobe hello yedeklemeleri ayarlanır. Sistem Veritabanı Yedeklemeleri etkinleştirilir. Tam yedeklemeler için haftalık iki saat 20:00 başlayarak bir zaman penceresi ile zamanlanır. Günlük yedeklemeler için 30 dakikada zamanlanır. Merhaba ikinci komut, **kümesi AzureRmVMSqlServerExtension**, güncelleştirmelerinin hello Azure VM bu ayarlarla belirtilen.

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname 
```

Birkaç dakika tooinstall alın ve hello SQL Server Iaas Aracısı Yapılandırma. 

tooenable şifreleme hello önceki betik toopass hello değiştirme **EnableEncryption** parametresi hello için bir parola (güvenli dize) ile birlikte **CertificatePassword** parametresi. Merhaba aşağıdaki betiği hello önceki örnekte hello otomatik yedekleme ayarlarını etkinleştirir ve şifreleme ekler.

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

ayarlarınızı uygulanır, tooconfirm [hello otomatik yedekleme yapılandırması doğrulayın](#verifysettings).

### <a name="disable-automated-backup"></a>Otomatik yedekleme devre dışı bırak
Otomatik yedekleme, hello aynı komut dosyası çalıştırma hello toodisable **-etkinleştirmek** parametresi toohello **yeni AzureRmVMSqlServerAutoBackupConfig** komutu. Merhaba hello yokluğu **-etkinleştirmek** parametresi sinyalleri hello komutu toodisable hello özelliği. Yüklemesine gibi birkaç dakika toodisable otomatik yedekleme alabilir.

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a>Örnek komut dosyası
Merhaba aşağıdaki komut dosyası değişkenleri kümesinin tooenable özelleştirebilir ve VM için otomatik yedeklemeyi yapılandırın sağlar. Sizin durumunuzda, gereksinimlerinize göre toocustomize hello komut dosyası gerekebilir. Örneğin, sistem veritabanlarının toodisable hello yedekleme istediyseniz toomake değişikliklerinin veya şifrelemeyi etkinleştirmeniz.

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10
$backupscheduletype = "Manual"
$fullbackupfrequency = "Weekly"
$fullbackupstarthour = "20"
$fullbackupwindow = "2"
$logbackupfrequency = "30"

# ResourceGroupName is hello resource group which is hosting hello VM where you are deploying hello SQL IaaS Extension 

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account toostore hello backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType $backupscheduletype -FullBackupFrequency $fullbackupfrequency `
    -FullBackupStartHour $fullbackupstarthour -FullBackupWindowInHours $fullbackupwindow `
    -LogBackupFrequencyInMinutes $logbackupfrequency

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a>Sonraki adımlar
Otomatik yedekleme v2 yönetilen yedekleme Azure Vm'lerinde yapılandırır. Çok önemlidir[yönetilen yedekleme hello belgelerini gözden geçirin](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello davranışı ve etkileri.

Ek yedekleme bulmak ve izleyen konu hello Azure Vm'lerde SQL Server için kılavuzunda geri yükleyebilirsiniz: [yedekleme ve geri yükleme Azure Virtual Machines'de SQL Server için](virtual-machines-windows-sql-backup-recovery.md).

Diğer kullanılabilir Otomasyon görevler hakkında daha fazla bilgi için bkz: [SQL Server Iaas Aracısı uzantısı](virtual-machines-windows-sql-server-agent-extension.md).

Azure Vm'lerinde SQL Server çalıştırma hakkında daha fazla bilgi için bkz: [Azure sanal makinelere genel bakış SQL Server'da](virtual-machines-windows-sql-server-iaas-overview.md).

