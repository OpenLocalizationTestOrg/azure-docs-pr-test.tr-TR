---
title: "aaaAutomated yedekleme SQL Server 2014 Azure Virtual Machines için | Microsoft Docs"
description: "SQL Server 2014 Azure'da çalışan VM'ler için Hello otomatik yedekleme özelliğini açıklar. Bu makalede hello Kaynak Yöneticisi'ni kullanarak belirli tooVMs ' dir."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: bdc63fd1-db49-4e76-87d5-b5c6a890e53c
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 07/05/2017
ms.author: jroth
ms.openlocfilehash: c6803d8ef9f80e44a2f87918d87e099f1b562483
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automated-backup-for-sql-server-2014-virtual-machines-resource-manager"></a>SQL Server 2014 sanal makineler (Resource Manager) için otomatik yedekleme

> [!div class="op_single_selector"]
> * [SQL Server 2014](virtual-machines-windows-sql-automated-backup.md)
> * [SQL Server 2016](virtual-machines-windows-sql-automated-backup-v2.md)

Otomatik yedekleme otomatik olarak yapılandırır [yönetilen yedekleme tooMicrosoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) SQL Server 2014 Standard veya Enterprise çalıştıran bir Azure VM üzerindeki tüm mevcut ve yeni veritabanları için. Bu, dayanıklı Azure blob depolama alanını tooconfigure normal veritabanı yedeklemeleri sağlar. Otomatik yedekleme bağlıdır hello üzerinde [SQL Server Iaas Aracısı uzantısı](virtual-machines-windows-sql-server-agent-extension.md).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a>Ön koşullar
toouse otomatik yedekleme önkoşulları aşağıdaki hello göz önünde bulundurun:

**İşletim sistemi**:

- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016

**SQL Server sürümü/yayını**:

- SQL Server 2014 Standard
- SQL Server 2014 Enterprise

> [!IMPORTANT]
> Otomatik yedekleme SQL Server 2014 ile çalışır. SQL Server 2016 kullanıyorsanız, veritabanlarınızı otomatik yedekleme v2 tooback kullanabilirsiniz. Daha fazla bilgi için bkz: [otomatik yedekleme v2 SQL Server 2016 Azure Virtual Machines için](virtual-machines-windows-sql-automated-backup-v2.md).

**Veritabanı yapılandırması**:

- Hedef veritabanlarına hello tam kurtarma modeli kullanmanız gerekir. Daha fazla bilgi hello tam kurtarma modeli için hello etkisi hakkında yedeklemeleri üzerinde [yedekleme altında tam kurtarma modeli hello](https://technet.microsoft.com/library/ms190217.aspx).
- Hedef veritabanlarına hello varsayılan SQL Server örneğinde olması gerekir. SQL Server Iaas uzantısı Hello adlandırılmış örnekleri desteklemez.

**Azure dağıtım modeli**:

- Resource Manager

**Azure PowerShell**:

- [Merhaba en son Azure PowerShell komutlarını yüklemek](/powershell/azure/overview) tooconfigure PowerShell ile otomatik yedekleme planlıyorsanız.

> [!NOTE]
> Otomatik yedekleme hello üzerinde SQL Server Iaas Aracısı uzantısı kullanır. Geçerli SQL sanal makineye Galerisi görüntülerini varsayılan olarak bu uzantı ekleyin. Daha fazla bilgi için bkz: [SQL Server Iaas Aracısı uzantısı](virtual-machines-windows-sql-server-agent-extension.md).

## <a name="settings"></a>Ayarlar

Merhaba aşağıdaki tabloda otomatik yedekleme için yapılandırılmış hello seçenekleri açıklanmaktadır. Merhaba gerçek yapılandırma adımlarını hello Azure portalında veya Azure Windows PowerShell komutlarını kullanmadığınıza bağlı olarak farklılık gösterir.

| Ayar | Aralık (varsayılan) | Açıklama |
| --- | --- | --- |
| **Otomatik Yedekleme** | Etkinleştir/devre dışı bırak (devre dışı) | Etkinleştirir veya SQL Server 2014 Standard veya Enterprise çalıştıran bir Azure VM için otomatik yedekleme devre dışı bırakır. |
| **Saklama süresi** | 1-30 gün (30 gün) | gün tooretain bir yedekleme Hello sayısı. |
| **Depolama hesabı** | Azure depolama hesabı | Blob depolama alanına otomatik yedekleme dosyalarını depolamak için bir Azure depolama hesabı toouse. Bir kapsayıcı sırasında bu konumu toostore tüm yedekleme dosyaları oluşturulur. Merhaba yedekleme dosyası adlandırma hello tarih, saat ve makine adını içerir. |
| **Şifreleme** | Etkinleştir/devre dışı bırak (devre dışı) | Etkinleştirir veya şifreleme devre dışı bırakır. Şifreleme etkinleştirildiğinde, hello kullanılan sertifikaları toorestore hello yedekleme bulunur hello belirtilen depolama hesabı hello aynı `automaticbackup` bir kapsayıcı kullanılarak hello aynı adlandırma kuralı. Merhaba parola değişirse, bu parola ile yeni bir sertifika oluşturulur, ancak toorestore önceki yedeklemeleri hello eski sertifika kalır. |
| **Parola** | Parola metin | Şifreleme anahtarları için bir parola. Yalnızca budur şifreleme etkin olup olmadığını gerekli. Sipariş toorestore şifreli bir yedekleme hello doğru parolayı ve hello yedeğin alındığı hello zamanında kullanılan ilgili sertifika olmalıdır. |

## <a name="configuration-in-hello-portal"></a>Merhaba Portal Yapılandırması

Hello Azure portal tooconfigure otomatik yedekleme sağlama sırasında veya var olan SQL Server 2014 VM'ler için kullanabilirsiniz.

### <a name="new-vms"></a>Yeni sanal makineleri

Merhaba Resource Manager dağıtım modelinde yeni bir SQL Server 2014 sanal makine oluşturduğunuzda hello Azure portal tooconfigure otomatik yedekleme kullanın.

Merhaba, **SQL Server ayarları** dikey penceresinde, select **otomatik yedekleme**. Merhaba aşağıdaki Azure portal ekran görüntüsü gösterir hello **SQL otomatik yedekleme** dikey.

![Azure portalında SQL otomatik yedekleme yapılandırması](./media/virtual-machines-windows-sql-automated-backup/azure-sql-arm-autobackup.png)

Bağlam için hello tam üzerinde konusuna [azure'da bir SQL Server sanal makine sağlama](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>Var olan sanal makineleri

Var olan SQL Server sanal makineler için SQL Server sanal makine seçin. Merhaba seçip **SQL Server yapılandırma** hello bölümünü **ayarları** dikey.

![Var olan VM'ler için SQL otomatik yedekleme](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-existing-vms.png)

Merhaba, **SQL Server yapılandırma** dikey penceresinde hello tıklatın **Düzenle** hello düğmesini otomatik yedekleme bölümü.

![SQL otomatik yedekleme var olan VM'ler için yapılandırma](./media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-configuration.png)

Tamamlandığında, hello tıklatın **Tamam** hello hello alt düğmesinde **SQL Server yapılandırma** dikey toosave değişikliklerinizi.

Otomatik yedekleme hello için ilk kez etkinleştiriyorsanız Azure hello SQL Server Iaas Aracısı hello arka planda yapılandırır. Bu süre boyunca hello Azure portal otomatik yedekleme yapılandırıldığını gösterilmeyebilir. Merhaba Aracısı toobe yüklü, birkaç dakika bekleyin yapılandırılmış. Bu hello sonra Azure portalı hello yeni ayarları yansıtır.

> [!NOTE]
> Otomatik yedekleme bir şablon kullanarak da yapılandırabilirsiniz. Daha fazla bilgi için bkz: [otomatik yedekleme için Azure Hızlı Başlangıç şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).

## <a name="configuration-with-powershell"></a>PowerShell ile yapılandırma

PowerShell tooconfigure otomatik yedekleme kullanabilirsiniz. Başlamadan önce şunları yapmalısınız:

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
Enable                      : False
EnableEncryption            : False
RetentionPeriod             : -1
StorageUrl                  : NOTSET
StorageAccessKey            : 
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : 
FullBackupFrequency         : 
FullBackupStartTime         : 
FullBackupWindowHours       : 
LogBackupFrequency          : 
```

Çıktı gösteriyorsa **etkinleştirmek** çok ayarlanır**yanlış**, tooenable otomatik yedekleme sahip. Merhaba iyi haber etkinleştirme ve otomatik yedekleme hello yapılandırma olan şekilde. Bu bilgi Hello sonraki bölüme bakın.

> [!NOTE] 
> Hemen bir değişiklik yaptıktan sonra hello ayarlarını denetleyin, hello eski yapılandırma değerlerini geri alırsınız mümkündür. Birkaç dakika bekleyin ve hello ayarlarını kontrol edin yeniden değişikliklerinizi uygulandığından emin toomake.

### <a name="configure-automated-backup"></a>Otomatik yedeklemeyi yapılandırın
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

Merhaba kullanmak **yeni AzureRmVMSqlServerAutoBackupConfig** komut tooenable ve hello otomatik yedekleme ayarlarını toostore yedeklemeler hello Azure depolama hesabı yapılandırın. Bu örnekte, 10 gün boyunca tutulur toobe hello yedeklemeleri ayarlanır. Merhaba ikinci komut, **kümesi AzureRmVMSqlServerExtension**, güncelleştirmelerinin hello Azure VM bu ayarlarla belirtilen.

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

Birkaç dakika tooinstall alın ve hello SQL Server Iaas Aracısı Yapılandırma.

> [!NOTE]
> Diğer ayarları için **yeni AzureRmVMSqlServerAutoBackupConfig** yalnızca tooSQL Server 2016 ve otomatik yedekleme v2 geçerlidir. SQL Server 2014 hello ayarları aşağıdaki desteklemiyor: **BackupSystemDbs**, **BackupScheduleType**, **FullBackupFrequency**,  **FullBackupStartHour**, **FullBackupWindowInHours**, ve **LogBackupFrequencyInMinutes**. Bu ayarları bir SQL Server 2014 sanal makinede tooconfigure çalışırsanız, bir hata, ancak hello ayarları uygulanmamış. Bu ayarları bir SQL Server 2016 sanal makinede toouse istiyorsanız, bkz: [otomatik yedekleme v2 SQL Server 2016 Azure Virtual Machines için](virtual-machines-windows-sql-automated-backup-v2.md).

tooenable şifreleme hello önceki betik toopass hello değiştirme **EnableEncryption** parametresi hello için bir parola (güvenli dize) ile birlikte **CertificatePassword** parametresi. Merhaba aşağıdaki betiği hello önceki örnekte hello otomatik yedekleme ayarlarını etkinleştirir ve şifreleme ekler.

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname

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
    -ResourceGroupName $storage_resourcegroupname

# Apply hello Automated Backup settings toohello VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a>Sonraki adımlar

Otomatik yedekleme yönetilen yedekleme Azure Vm'lerinde yapılandırır. Çok önemlidir[yönetilen yedekleme hello belgelerini gözden geçirin](https://msdn.microsoft.com/library/dn449496.aspx) toounderstand hello davranışı ve etkileri.

Ek yedekleme bulmak ve izleyen konu hello Azure Vm'lerde SQL Server için kılavuzunda geri yükleyebilirsiniz: [yedekleme ve geri yükleme Azure Virtual Machines'de SQL Server için](virtual-machines-windows-sql-backup-recovery.md).

Diğer kullanılabilir Otomasyon görevler hakkında daha fazla bilgi için bkz: [SQL Server Iaas Aracısı uzantısı](virtual-machines-windows-sql-server-agent-extension.md).

Azure Vm'lerinde SQL Server çalıştırma hakkında daha fazla bilgi için bkz: [Azure sanal makinelere genel bakış SQL Server'da](virtual-machines-windows-sql-server-iaas-overview.md).

