---
title: "aaaAzure yedekleme - kullanım PowerShell tooback DPM iş yüklerini | Microsoft Docs"
description: "Bilgi nasıl toodeploy ve Data Protection Manager (PowerShell kullanarak DPM için) Azure Backup yönetme"
services: backup
documentationcenter: 
author: NKolli1
manager: shreeshd
editor: 
ms.assetid: e9bd223c-2398-4eb1-9bf3-50e08970fea7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/23/2017
ms.author: adigan;anuragm;trinadhk;markgal
ms.openlocfilehash: 27d2b4b3127b68c9da564697eb61dc3ccbc34b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-data-protection-manager-dpm-servers-using-powershell"></a>Dağıtma ve PowerShell kullanarak Data Protection Manager (DPM) sunucuları için yedekleme tooAzure yönetme
> [!div class="op_single_selector"]
> * [ARM](backup-dpm-automation.md)
> * [Klasik](backup-dpm-automation-classic.md)
>
>

Bu makale size nasıl gösterir toouse PowerShell toosetup Azure yedekleme, bir DPM sunucusu ve toomanage yedekleme ve kurtarma.

## <a name="setting-up-hello-powershell-environment"></a>Merhaba PowerShell ortamını ayarlama
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

Data Protection Manager tooAzure PowerShell toomanage yedeklemelerden kullanabilmeniz için önce toohave hello sağ ortamında PowerShell gerekir. Merhaba PowerShell oturumu Hello başlangıcında komutu tooimport hello sağ modülleri aşağıdaki hello çalıştırın ve toocorrectly başvuru hello DPM cmdlet'leri izin emin olun:

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome toohello DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a>Kurulumu'nu ve kaydı
toobegin:

1. [En son PowerShell indirme](https://github.com/Azure/azure-powershell/releases) (gerekli minimum sürüm: 1.0.0)
2. Çok geçerek Hello Azure yedekleme cmdlet'leri etkinleştirmek*AzureResourceManager* hello kullanarak moduna **Switch-AzureMode** komutunu:

```
PS C:\> Switch-AzureMode AzureResourceManager
```

Merhaba aşağıdaki Kurulum ve kayıt görevler PowerShell ile otomatik olarak yapılabilir:

* Kurtarma Hizmetleri kasası oluşturma
* Hello Azure Backup aracısını yükleme
* Hello Azure Backup hizmeti ile kaydetme
* Ağ ayarları
* Şifreleme ayarları

## <a name="create-a-recovery-services-vault"></a>Kurtarma hizmetleri kasası oluşturma
Aşağıdaki adımları hello kurtarma Hizmetleri kasası oluşturmada size yol açar. Kurtarma Hizmetleri kasasına yedekleme Kasası ' farklıdır.

1. Azure Backup hello için ilk kez kullanıyorsanız hello kullanmalısınız **Register-AzureRMResourceProvider** cmdlet tooregister hello Azure Recovery hizmeti sağlayıcısı aboneliğinizle.

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. tooplace ihtiyacınız hello kurtarma Hizmetleri kasası bir ARM kaynak olduğundan, bir kaynak grubu içinde. Varolan bir kaynak grubunu kullanın veya yeni bir tane oluşturun. Yeni bir kaynak grubu oluştururken hello kaynak grubu için hello ad ve konum belirtin.  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. Kullanım hello **yeni AzureRmRecoveryServicesVault** cmdlet toocreate yeni bir kasa. Toospecify hello hello kasa için aynı konumu hello kaynak grubu için kullanıldığından emin olun.

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. Depolama artıklık toouse Hello türünü belirtin; kullanabileceğiniz [yerel olarak yedekli depolama (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) veya [coğrafi olarak yedekli depolama (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage). Merhaba aşağıdaki örnek tooGeoRedundant testVault için hello - BackupStorageRedundancy seçeneği ayarlanmış gösterir.

   > [!TIP]
   > Çok sayıda Azure yedekleme cmdlet'lerini girdi olarak hello kurtarma Hizmetleri kasası nesnesi gerektirir. Bu nedenle, bu kullanışlı toostore hello yedekleme kurtarma Hizmetleri kasası, bir değişkende nesnesidir.
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-hello-vaults-in-a-subscription"></a>Bir abonelikte görünüm hello kasaları
Kullanım **Get-AzureRmRecoveryServicesVault** tooview hello hello geçerli Abonelikteki tüm kasalarının listesi. Yeni bir kasa oluşturulduğunu bu komutu toocheck veya toosee kullanabilirsiniz hangi kasalarını hello abonelikte kullanılabilir.

Get-AzureRmRecoveryServicesVault Hello komutunu çalıştırın ve hello Abonelikteki tüm kasalarını listelenir.

```
PS C:\> Get-AzureRmRecoveryServicesVault
Name              : Contoso-vault
ID                : /subscriptions/1234
Type              : Microsoft.RecoveryServices/vaults
Location          : WestUS
ResourceGroupName : Contoso-docs-rg
SubscriptionId    : 1234-567f-8910-abc
Properties        : Microsoft.Azure.Commands.RecoveryServices.ARSVaultProperties
```


## <a name="installing-hello-azure-backup-agent-on-a-dpm-server"></a>Bir DPM sunucusu üzerinde Hello Azure Backup aracısını yükleme
Hello Azure Backup aracısını yüklemeden önce indirildi ve Windows Server hello mevcut toohave hello yükleyici gerekir. Hello hello Installer hello en son sürümünü elde edebilirsiniz [Microsoft Download Center](http://aka.ms/azurebackup_agent) veya hello kurtarma Hizmetleri Kasası'nın Pano sayfası. Kolay erişilebilecek bir konuma tooan gibi Hello yükleyici Kaydet * C:\Downloads\*.

komutu yükseltilmiş bir PowerShell konsolunda aşağıdaki hello çalıştırmak tooinstall hello Aracısı **hello DPM sunucusunda**:

```
PS C:\> MARSAgentInstaller.exe /q
```

Bu, tüm hello varsayılan seçeneklerle hello aracı yükler. Merhaba yükleme hello arka planda birkaç dakika sürer. Merhaba belirtmezseniz */nu* seçeneği hello **Windows Update** hello yükleme toocheck herhangi bir güncelleştirme için hello sonunda penceresi açılır.

Merhaba Aracısı hello yüklü programlar listesinde görüntülenir. toosee hello listesi yüklü programlar, çok Git**Denetim Masası** > **programları** > **programlar ve Özellikler**.

![Yüklü aracı](./media/backup-dpm-automation/installed-agent-listing.png)

### <a name="installation-options"></a>Yükleme Seçenekleri
toosee aşağıdaki kullanım hello hello commandline kullanılabilir tüm hello seçenekleri komutu:

```
PS C:\> MARSAgentInstaller.exe /?
```

Merhaba mevcut Seçenekler şunlardır:

| Seçenek | Ayrıntılar | Varsayılan |
| --- | --- | --- |
| /q |Sessiz yükleme |- |
| p: "Konum" |Yol toohello yükleme klasörünü hello Azure Yedekleme aracısı. |C:\Program Files\Microsoft Azure kurtarma Hizmetleri Aracısı |
| / s: "Konum" |Hello Azure Backup aracısı için yol toohello Önbellek klasörü. |C:\Program Files\Microsoft Azure kurtarma Hizmetleri Agent\Scratch |
| /m |Katılımı tooMicrosoft güncelleştirme |- |
| /nu |Yükleme tamamlandıktan sonra güncelleştirmeleri denetleme |- |
| /d |Microsoft Azure kurtarma Hizmetleri Aracısı kaldırır |- |
| /ph |Proxy konağı adresi |- |
| /PO |Proxy ana bilgisayar bağlantı noktası numarası |- |
| /PU |Proxy konağı kullanıcı |- |
| /pw |Proxy parolası |- |

## <a name="registering-dpm-tooa-recovery-services-vault"></a>DPM tooa kurtarma Hizmetleri kasası kaydetme
Merhaba kurtarma Hizmetleri kasası oluşturduktan sonra hello en son aracı hello kasa kimlik bilgilerini indirin ve C:\Downloads gibi uygun bir konuma depolayın.

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
PS C:\> $credsfilename
C:\downloads\testvault\_Sun Apr 10 2016.VaultCredentials
```

Merhaba Hello DPM sunucusunda çalıştırın [başlangıç OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet tooregister hello makine hello kasası ile.

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :West US
Machine registration succeeded.
```

### <a name="initial-configuration-settings"></a>İlk yapılandırma ayarları
Merhaba DPM sunucusu ile Merhaba kaydedildikten sonra kurtarma Hizmetleri kasası, varsayılan abonelik ayarlarını başlatır. Bu abonelik ayarlar, ağ, şifreleme ve hello hazırlama alanı içerir. gereksinim duyduğunuz toofirst toochange abonelik ayarlarını almak bir tanıtıcı (hello kullanarak hello varolan varsayılan) ayarları [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

Tüm değişiklikleri yapılmış toothis yerel PowerShell nesnesi olan ```$setting``` ve ardından hello tam nesne taahhüt tooDPM ve Azure Backup toosave hello kullanarak bunları [kümesi DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet'i. Toouse hello gereksinim ```–Commit``` değişiklikleri hello bayrağı tooensure kaldı. Hello ayarları değil uygulanan ve olması kaydedilen sürece Azure yedekleme tarafından kullanılır.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="networking"></a>Ağ
Merhaba bağlantı hello DPM makine toohello hello Azure Backup hizmeti, bir proxy sunucu üzerinden internet ise, hello proxy sunucusu ayarları başarılı yedeklemeler için sağlanmalıdır. Bu hello kullanarak yapılır ```-ProxyServer```ve ```-ProxyPort```, ```-ProxyUsername``` ve hello ```ProxyPassword``` hello parametrelerle [kümesi DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet'i. Bu örnekte, olmadığından hiçbir Ara sunucunun biz açıkça herhangi bir proxy ile ilgili bilgi temizleme.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

Bant genişliği kullanımı ile seçenekleri de denetlenebilir ```-WorkHourBandwidth``` ve ```-NonWorkHourBandwidth``` hello haftanın belirli bir dizi için. Bu örnekte, biz herhangi azaltma ayarlıyorsanız değil.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

## <a name="configuring-hello-staging-area"></a>Merhaba hazırlama alanı yapılandırma
Merhaba DPM sunucusunda çalışan hello Azure Yedekleme aracısı, (yerel hazırlama alanı) hello buluttan geri yüklenen veriler için geçici depolama gerekir. Merhaba hazırlama alanı hello kullanarak yapılandırma [kümesi DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet'i ve hello ```-StagingAreaPath``` parametresi.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

Merhaba yukarıdaki örnekte, hello hazırlama alanı çok ayarlanacak*C:\StagingArea* hello PowerShell nesnesindeki ```$setting```. Merhaba belirtilen klasör zaten var, aksi takdirde hello abonelik ayarlarını hello son yürütme başarısız olur emin olun.

### <a name="encryption-settings"></a>Şifreleme ayarları
Merhaba gönderilen yedekleme verileri tooAzure yedekleme şifrelenmiş tooprotect hello hello veri gizliliğini ' dir. Merhaba şifreleme parolası hello "parola" toodecrypt hello geri yükleme hello aynı anda verilerdir. Önemli tookeep bu bilgileri güvenlidir ve ayarlandıktan sonra güvenli.

Merhaba aşağıdaki örnekte, hello ilk komut hello dizesini sayıya dönüştürür ```passphrase123456789``` adlı tooa güvenli dize atar hello güvenli dize toohello değişkeni ```$Passphrase```. İkinci komut Hello ayarlar hello güvenli dize ```$Passphrase``` yedeklemeleri şifrelemek için başlangıç parolası.

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> Ayarlandıktan sonra hello parola bilgilerini güvenli ve güvenli tutar. Bu parola olmadan mümkün toorestore verileri azure'dan olmaz.
>
>

Bu noktada, tüm gerekli hello değişiklikleri toohello yaptığınız ```$setting``` nesnesi. Toocommit hello değişiklikleri unutmayın.

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-tooazure-backup"></a>Veri tooAzure yedekleme koruma
Bu bölümde, bir üretim sunucusu tooDPM ekleyin ve hello veri toolocal DPM depolama ve ardından tooAzure yedekleme daha sonra koruyun. Merhaba örneklerde, biz gösterilmektedir nasıl tooback dosya ve klasörler. Merhaba mantığı kolayca genişletilmiş toobackup herhangi bir DPM desteklenen veri kaynağı olabilir. Tüm DPM yedeklemelerini dört bölümden ile koruma grubu (PG) tarafından yönetilir:

1. **Grup üyeleri** tüm hello korunabilir nesneler listesi (olarak da bilinen *veri kaynakları* dpm'de) hello tooprotect istediğiniz aynı koruma grubunda. Örneğin, yedekleme farklı gereksinimlere sahip, bir koruma grubu ve SQL Server veritabanlarını başka bir koruma grubunda tooprotect üretim VM'ler isteyebilirsiniz. Üretim sunucusundaki herhangi bir veri kaynağı yedekleyebilirsiniz önce DPM Aracısı hello sunucuda yüklü olduğundan ve DPM tarafından yönetilen toomake emin hello gerekir. Merhaba adımlarını izleyin [yükleme, DPM Aracısı hello](https://technet.microsoft.com/library/bb870935.aspx) ve toohello bağlama uygun DPM sunucusu.
2. **Veri koruma yöntemini** hello hedef yedekleme konumları - bant, disk ve bulut belirtir. Bizim örneğimizde biz veri toohello yerel disk ve toohello bulut korur.
3. A **yedekleme zamanlaması** yedeklemeler gerçekleştirilecek toobe gerektiğinde ve ne sıklıkta hello verilerin hello DPM sunucusu ile Merhaba üretim sunucusu arasında eşitlenmesi gerektiğini belirtir.
4. A **bekletme zamanlaması** Azure'da ne kadar süreyle tooretain hello kurtarma noktaları belirtir.

### <a name="creating-a-protection-group"></a>Koruma grubu oluşturma
Başlangıç hello kullanarak yeni bir koruma grubu oluşturarak [yeni DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet'i.

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

cmdlet'i yukarıdaki Hello koruma adlı bir grup oluşturur *ProtectGroup01*. Mevcut bir koruma grubunun ayrıca sonraki tooadd yedekleme toohello Azure bulut değiştirilebilir. Ancak, toomake herhangi bir değişiklik toohello koruma grubu - yeni veya varolan - ihtiyacımız tooget bir tanıtıcı üzerinde bir *değiştirilebilir* hello kullanarak nesnesi [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet'i.

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-toohello-protection-group"></a>Grup üyeleri toohello koruma grubu ekleme
Her DPM aracısının yüklü olduğu hello sunucusunda veri kaynakları listesi hello bilir. tooadd datasource toohello koruma grubu, DPM Aracısı gereksinimlerini toofirst hello hello veri kaynakları geri toohello DPM sunucusu listesini gönderin. Seçili ve toohello koruma grubuna eklenen bir veya daha fazla veri kaynakları olan. Bu olan tooachieve Hello PowerShell adımlar gerekir:

1. DPM Aracısı hello DPM tarafından yönetilen tüm sunucuların listesi getirilemedi.
2. Belirli bir sunucu seçin.
3. Merhaba sunucusundaki tüm veri kaynakları listesi getirilemedi.
4. Bir veya daha fazla veri kaynakları seçin ve bunları toohello koruma grubu Ekle

hangi hello DPM aracısının yüklü olduğundan ve hello DPM sunucusu tarafından yönetilen sunucuları Hello listesi ile Merhaba edinilen [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet'i. Biz filtrelemek ve yalnızca PS adıyla yapılandırın, bu örnekte *productionserver01* yedekleme için.

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

Şimdi üzerinde hello veri kaynaklarının listesini getirme ```$server``` hello kullanarak [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet'i. Bu örnekte, biz hello birim için filtre * D:\* tooconfigure yedekleme için istediğimizi. Bu veri kaynağı sonra toohello koruma grubuna eklenen hello kullanarak [Ekle DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet'i. Toouse hello unutmayın *değiştirilebilir* koruma grubu nesnesi ```$MPG``` toomake hello ekler.

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

Veri kaynakları toohello koruma grubu seçilen tüm hello ekleyene kadar gerektiği gibi birçok kez bu adımı yineleyin. Yalnızca bir datasource ve hello koruma grubunu oluşturmak için tam hello iş akışı ile başlayın ve daha sonraki bir noktada daha fazla veri kaynakları toohello koruma grubuna ekleyin.

### <a name="selecting-hello-data-protection-method"></a>Merhaba veri koruma yöntemi seçme
Merhaba datasources toohello koruma grubuna eklendikten sonra hello sonraki hello kullanarak toospecify hello koruma yöntemini adımdır [kümesi DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet'i. Bu örnekte, hello koruma grubu yerel disk ve bulut yedekleme için kurulur. Hello kullanarak tooprotect toocloud istediğiniz toospecify hello datasource etmeniz [Ekle DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet'iyle - çevrimiçi bayrağı.

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-hello-retention-range"></a>Merhaba bekletme aralığını ayarlama
Ayarlama hello bekletme hello kullanarak hello yedekleme noktaları için [kümesi DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet'i. Hello kullanarak Hello yedekleme zamanlaması tanımlanmış önce tek tooset hello bekletme görünebilir ancak ```Set-DPMPolicyObjective``` cmdlet'i sonra değiştirilebilen varsayılan yedekleme zamanlaması otomatik olarak ayarlar. Bu her zaman mümkün tooset hello yedekleme zamanlaması önce ve sonra bekletme ilkesi hello.

Merhaba aşağıdaki örnekte, hello cmdlet'i disk yedeklemeleri hello bekletme parametreleri ayarlar. Bu yedeklemeler 10 gün ve eşitleme verileri için 6 saatte bir hello üretim sunucusu ve hello DPM sunucusu arasındaki korur. Merhaba ```SynchronizationFrequencyMinutes``` ne sıklıkta bir yedekleme noktasının, ancak nasıl oluşturulduğunu tanımlamıyor genellikle veri kopyalanan toohello DPM sunucusu değil.  Bu ayar, yedeklemeler çok büyük hale gelmesini engeller.

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

(DPM başvuruyor toothem çevrimiçi yedeklemeler) tooAzure giderek yedeklemeler için hello bekletme aralıkları için yapılandırılabilir [üst öğe Son şeması (GFS) kullanarak bekletme'uzun süreli](backup-azure-backup-cloud-as-tape.md). Diğer bir deyişle, günlük, haftalık, aylık ve yıllık bekletme ilkeleri içeren bir birleşik bekletme ilkesi tanımlayabilirsiniz. Bu örnekte, biz istiyoruz hello karmaşık bekletme düzeni temsil eden bir dizi oluşturmak ve ardından hello kullanarak hello bekletme aralığı yapılandırın [kümesi DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet'i.

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-hello-backup-schedule"></a>Set hello yedekleme zamanlaması
Merhaba koruma hedefi hello kullanarak belirtirseniz, DPM bir varsayılan yedekleme zamanlaması otomatik olarak ayarlar. ```Set-DPMPolicyObjective``` cmdlet'i. toochange hello varsayılan zamanlamaların kullanmak hello [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet hello tarafından izlenen [kümesi DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet'i.

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

Örneğin, yukarıdaki hello içinde ```$onlineSch``` hello varolan çevrimiçi koruma zamanlamasını hello GFS düzeni hello koruma grubu için içeren bir dizi dört öğelerle:

1. ```$onlineSch[0]```Merhaba günlük zamanlama içerir
2. ```$onlineSch[1]```Merhaba haftalık zamanlama içerir
3. ```$onlineSch[2]```Merhaba aylık zamanlama içerir
4. ```$onlineSch[3]```Merhaba yıllık çizelge içerir

Bu nedenle toomodify hello haftalık zamanlama gerekiyorsa, toorefer toohello gerekir ```$onlineSch[1]```.

### <a name="initial-backup"></a>İlk yedekleme
Hello için veri kaynağı ilk kez, DPM gereksinimlerini yedekleme ilk çoğaltma, oluşturduğunda DPM çoğaltma birimi korumalı hello datasource toobe tam bir kopyasını oluşturur. Bu etkinlik için belirli bir saat ya da zamanlanabilir veya hello kullanarak el ile tetiklenebilir [kümesi DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) hello parametre cmdlet'iyle ```-NOW```.

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-hello-size-of-dpm-replica--recovery-point-volume"></a>DPM çoğaltma ve kurtarma noktası birimi Hello boyutunu değiştirme
Ayrıca DPM çoğaltma birimi ve birim gölge kopya kullanarak hello boyutunu değiştirebilirsiniz [kümesi DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) aşağıdaki örneğine hello olduğu gibi cmdlet: Get-DatasourceDiskAllocation - Datasource $DS Set-DatasourceDiskAllocation - Datasource $DS - Protectiongroup'u $MPG-el ile - ReplicaArea (2 gb) - ShadowCopyArea (2 gb)

### <a name="committing-hello-changes-toohello-protection-group"></a>Uygulanıyor hello değişiklikleri toohello koruma grubu
Son olarak, DPM hello yeni koruma grubu yapılandırması başına hello yedek almadan önce kaydedilmiş toobe hello değişiklikleri gerekir. Bu hello kullanarak elde [kümesi DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet'i.

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-hello-backup-points"></a>Görünüm hello yedekleme noktaları
Merhaba kullanabilirsiniz [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet tooget bir veri kaynağı için tüm kurtarma noktalarının bir listesi. Bu örnekte, şunları yapacağız:

* Fetch tüm PGs hello DPM sunucusunda hello ve bir dizide saklanan```$PG```
* Merhaba datasources karşılık gelen toohello Al```$PG[0]```
* Tüm hello kurtarma noktaları için bir veri kaynağı alın.

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a>Azure üzerinde korunan verileri geri yükleme
Verileri geri birleşimidir bir ```RecoverableItem``` nesne ve ```RecoveryOption``` nesne. Merhaba önceki bölümde, biz bir veri kaynağı için hello yedekleme noktalarının bir listesini aldı.

Merhaba aşağıdaki örnekte, toorestore bir Hyper-V sanal makineden Azure yedekleme hello ile Birleşen yedekleme noktaları tarafından hedef kurtarma için nasıl ekleyebileceğiniz gösterilmektedir. Bu örnek içerir:

* Hello kullanarak bir kurtarma seçeneği oluşturma [yeni DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet'i.
* Hello kullanarak yedekleme noktaları getirilirken hello dizisi ```Get-DPMRecoveryPoint``` cmdlet'i.
* Gelen bir yedekleme noktası toorestore seçme.

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

Merhaba komutları herhangi bir veri kaynağı türü için kolayca genişletilebilir.

## <a name="next-steps"></a>Sonraki adımlar
* DPM hakkında daha fazla bilgi için bkz: tooAzure yedekleme [giriş tooDPM yedekleme](backup-azure-dpm-introduction.md)
