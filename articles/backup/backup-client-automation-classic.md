---
title: aaaUse PowerShell toomanage Windows Server Yedekleme azure'da | Microsoft Docs
description: "Dağıtın ve PowerShell kullanarak Windows Server Yedekleme yönetin."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: e7e269e2-1f11-41a9-957b-a2155de6a1e0
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: saurse;markgal;nkolli;trinadhk
ms.openlocfilehash: 72292e510b0f059102440bd49a195be4ef700a6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-windows-serverwindows-client-using-powershell"></a>Dağıtma ve PowerShell kullanarak Windows Server/Windows İstemcisi için yedekleme tooAzure yönetme
> [!div class="op_single_selector"]
> * [ARM](backup-client-automation.md)
> * [Klasik](backup-client-automation-classic.md)
>
>

Bu makalede, Windows Server veya Windows iş istasyonu veri tooa toouse PowerShell tooback yedekleme kasası nasıl açıklanmaktadır. Microsoft, tüm yeni dağıtımlar için kurtarma Hizmetleri kasalarının kullanılmasını önerir. Yeni bir Azure yedekleme kullanıcı yoksa ve bir yedekleme kasası, aboneliğinizde oluşturmadıysanız, hello makale kullanırsınız [dağıtma ve PowerShell kullanarak Data Protection Manager veri tooAzure yönetmek](backup-client-automation.md) bir kurtarma Hizmetleri kasasına verilerinizi depolamak için. 

> [!IMPORTANT]
> Şimdi, yedekleme kasaları tooRecovery Hizmetleri kasaları yükseltebilirsiniz. Ayrıntılar için hello makalesine bakın [kurtarma Hizmetleri kasası bir yedekleme kasası tooa yükseltme](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft tooupgrade önerir tooRecovery Hizmetleri kasalarının yedekleme kasaları.<br/> 15 Ekim 2017 sonra PowerShell toocreate yedekleme kasaları kullanamazsınız. **1 Kasım 2017’ye kadar**:
>- Kalan tüm yedekleme kasaları otomatik olarak yükseltilen tooRecovery Hizmetleri kasalarının olacaktır.
>- Mümkün tooaccess hello Klasik Portalı'nda, yedekleme verilerinizi olmayacaktır. Bunun yerine, hello Azure portal tooaccess kurtarma Hizmetleri kasalarının, yedekleme verilerinizi kullanın.
>

## <a name="install-azure-powershell"></a>Azure PowerShell'i yükleme
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

Azure PowerShell 1.0 Ekim 2015'te yayımlanmıştır. Bu sürüm hello 0.9.8 yayın başarılı oldu ve bazı önemli değişiklikler hakkında özellikle hello adlandırma deseni hello cmdlet'lerinin getirildi. 1.0 cmdlet'leri izleyin hello adlandırma deseni {fiil}-AzureRm {isim}; Merhaba 0.9.8 adlarında değil ancak **Rm** (örneğin, New-Azureresourcegroup yerine New-Azurermresourcegroup). Azure PowerShell 0.9.8 kullanıldığında, önce hello Resource Manager moduna hello çalıştırarak etkinleştirmelisiniz **Switch-AzureMode AzureResourceManager** komutu. Bu komut 1.0 veya üstü gerekli değildir.

Merhaba 0.9.8 ortamında hello 1.0 veya sonraki ortamı için yazılan komut dosyalarınızı toouse istiyorsanız, dikkatlice hello komut bir ön üretim ortamında üretim tooavoid kullanmadan önce sınamanız beklenmeyen etkisi.

[Merhaba son PowerShell yayın indirme](https://github.com/Azure/azure-powershell/releases) (gerekli minimum sürüm: 1.0.0)

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-backup-vault"></a>Yedekleme kasası oluşturma
> [!WARNING]
> Azure Backup hello için ilk kez kullanan müşteriler için aboneliğiniz ile birlikte kullanılan tooregister hello Azure Backup sağlayıcı toobe gerekir. Bu komutu aşağıdaki hello çalıştırarak yapılabilir: Register-AzureProvider - ProviderNamespace "Microsoft.Backup"
>
>

Hello kullanarak yeni bir yedekleme kasası oluşturma **yeni AzureRMBackupVault** cmdlet'i. Merhaba yedekleme kasası olan bir ARM kaynak tooplace gereken şekilde bir kaynak grubu içinde. Yükseltilmiş bir Azure PowerShell konsolunda hello aşağıdaki komutları çalıştırın:

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

Kullanım hello **Get-AzureRMBackupVault** cmdlet toolist hello yedekleme kasaları bir abonelik.

## <a name="installing-hello-azure-backup-agent"></a>Hello Azure Backup aracısını yükleme
Hello Azure Backup aracısını yüklemeden önce indirildi ve Windows Server hello mevcut toohave hello yükleyici gerekir. Hello hello Installer hello en son sürümünü elde edebilirsiniz [Microsoft Download Center](http://aka.ms/azurebackup_agent) veya hello yedekleme kasasının Pano sayfası. Kolay erişilebilecek bir konuma tooan gibi Hello yükleyici Kaydet * C:\Downloads\*.

tooinstall hello Aracısı, komutu yükseltilmiş bir PowerShell konsolunda aşağıdaki hello çalıştırın:

```
PS C:\> MARSAgentInstaller.exe /q
```

Bu, tüm hello varsayılan seçeneklerle hello aracı yükler. Merhaba yükleme hello arka planda birkaç dakika sürer. Merhaba belirtmezseniz */nu* seçeneği sonra hello **Windows Update** hello yükleme toocheck herhangi bir güncelleştirme için hello sonunda penceresi açılır. Bir kez yüklendikten sonra hello Aracısı hello yüklü programlar listesinde gösterilir.

toosee hello listesi yüklü programlar, çok Git**Denetim Masası** > **programları** > **programlar ve Özellikler**.

![Yüklü aracı](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a>Yükleme Seçenekleri
Tüm seçeneklerin aracılığıyla hello toosee komut satırı Merhaba, hello aşağıdaki komutu kullanın:

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

## <a name="registering-with-hello-azure-backup-service"></a>Hello Azure Backup hizmeti ile kaydetme
Hello Azure Backup hizmeti ile kaydedebilmek için o hello tooensure gerek [Önkoşullar](backup-configure-vault.md) karşılanır. Yapmanız gerekir:

* Geçerli bir Azure aboneliğiniz
* Bir yedekleme kasası sahip

toodownload hello kasa kimlik bilgileri Hello çalıştırmak, **Get-AzureRMBackupVaultCredentials** cmdlet'i, uygun bir konumda gibi bir Azure PowerShell konsolunda ve deposu * C:\Downloads\*.

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

Merhaba kasası ile kaydediliyor hello makine yapılır hello kullanarak [başlangıç OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet:

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration -VaultCredentials $cred -Confirm:$false

CertThumbprint      : 7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName : test-vault
Region              : West US

Machine registration succeeded.
```

> [!IMPORTANT]
> Göreli yollar toospecify hello kasa kimlik bilgileri dosyası kullanmayın. Bir giriş toohello cmdlet'ini olarak mutlak bir yol sağlamalısınız.
>
>

## <a name="networking-settings"></a>Ağ ayarları
Internet proxy sunucu üzerinden gerçekleşir toohello Windows hello Hello bağlantısını makine olduğunda hello proxy ayarlarını toohello aracı da sağlanabilir. Bu örnekte, olmadığından hiçbir Ara sunucunun biz açıkça herhangi bir proxy ile ilgili bilgi temizleme.

Bant genişliği kullanımı ile Merhaba seçenekleri de denetlenebilir ```work hour bandwidth``` ve ```non-work hour bandwidth``` hello haftanın belirli bir dizi için.

Ayar Hello proxy ve bant genişliği ayrıntıları yapılır hello kullanarak [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a>Şifreleme ayarları
Merhaba gönderilen yedekleme verileri tooAzure yedekleme şifrelenmiş tooprotect hello hello veri gizliliğini ' dir. Merhaba şifreleme parolası hello "parola" toodecrypt hello geri yükleme hello aynı anda verilerdir.

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
Server properties updated successfully
```

> [!IMPORTANT]
> Ayarlandıktan sonra hello parola bilgilerini güvenli ve güvenli tutar. Bu parola olmadan mümkün toorestore verileri azure'dan olmaz.
>
>

## <a name="back-up-files-and-folders"></a>Dosya ve klasörleri yedekleme
Tüm yedeklemelerinizi Windows sunucularını ve istemcilerini tooAzure yedekleme İlkesi tarafından yönetilir. Hello İlkesi üç bölümden oluşur:

1. A **yedekleme zamanlaması** yedeklemeler alınır ve hello hizmeti ile eşitlenmiş toobe gerektiğinde belirtir.
2. A **bekletme zamanlaması** Azure'da ne kadar süreyle tooretain hello kurtarma noktaları belirtir.
3. A **dosya ekleme/çıkarma belirtimi** belirleyen ne yedeklenmelidir.

Yedekleme, otomatikleştirme beri bu belgede, hiçbir şey yapılandırılmış varsayıyoruz. Hello kullanarak yeni bir yedekleme ilkesi oluşturarak başlayın [yeni OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet'i ve bunu kullanma.

```
PS C:\> $newpolicy = New-OBPolicy
```

Bu zaman hello İlkesi boş olduğunu ve diğer cmdlet'ler gerekli toodefine ne öğeleri dahil etmek veya hariç, yedeklemeler çalışacak ve burada hello yedeklemeleri depolanacak.

### <a name="configuring-hello-backup-schedule"></a>Merhaba yedekleme zamanlamasını yapılandırma
ilk Merhaba hello İlkesi 3 bölümleri hale hello kullanılarak oluşturulan hello yedekleme zamanlaması [yeni OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet'i. Merhaba yedekleme zamanlaması yedeklemeleri gerçekleştirilecek toobe gerektiğinde tanımlar. Bir zamanlama oluştururken toospecify 2 giriş parametreleri gerekir:

* **Merhaba haftanın günlerini** hello yedekleme çalıştırmanız gerekir. Merhaba yedekleme işi yalnızca bir gün veya her gün hello haftanın veya arasındaki herhangi bir birleşimini çalıştırabilirsiniz.
* **Merhaba saatlerinde** hello yedekleme ne zaman çalışmalı. Too3 hello yedekleme harekete geçirildiğinde hello günün farklı saatlerinde tanımlayabilirsiniz.

Örneğin, 4'e her Cumartesi ve Pazar çalışan bir yedekleme ilkesi yapılandırabilirsiniz.

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

Merhaba yedekleme zamanlaması bir ilkeyle ilişkilendirilmiş toobe gerekir ve bu hello kullanarak elde [kümesi OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet'i.

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a>Bir bekletme ilkesi yapılandırma
Merhaba Bekletme İlkesi yedekleme işlerini oluşturulan noktaları korunur ne kadar süreyle kurtarma tanımlar. Hello kullanarak yeni bir bekletme ilkesi oluşturulurken [yeni OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet'ini hello yedekleme kurtarma noktalarının hello gün sayısı gereken Azure yedekleme ile korunduğunu toobe belirtebilirsiniz. Aşağıdaki Hello örnek bir bekletme ilkesi 7 gün olarak ayarlar.

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

Merhaba bekletme ilkesi hello cmdlet'ini kullanarak hello ana ilkesiyle ilişkili olmalıdır [kümesi OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):

```
PS C:\> Set-OBRetentionPolicy -Policy $newpolicy -RetentionPolicy $retentionpolicy

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          :
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```
### <a name="including-and-excluding-files-toobe-backed-up"></a>Yedeklenen dosyaları toobe hariç ve dahil
Bir ```OBFileSpec``` nesnesi eklenen ve bir yedek dışlanan hello dosyaları toobe tanımlar. Bu bir kapsam hello çıkışı dosya ve klasörlerin bir makinede korumalı kurallar kümesidir. Birçok ekleme veya hariç tutma kuralları gerektiği gibi dosya ve bir ilke ile ilişkilendirmek gibi sahip olabilir. Yeni bir OBFileSpec nesnesi oluştururken şunları yapabilirsiniz:

* Merhaba dosya ve klasörleri toobe dahil belirtin
* Dışlanan dosya ve klasörleri toobe hello belirtin
* Özyinelemeli bir klasör (veya) olup yalnızca üst düzey dosyalarında hello belirtilen klasör hello yedeklenmelidir verilerin yedeğini yukarı belirtin.

Merhaba ikinci hello yeni OBFileSpec komutta hello - özyinelemesiz bayrağı kullanılarak elde edilir.

Merhaba aşağıdaki örnekte, biz birimi yedekleyin C: ve D: ve hello OS ikili hello Windows klasöründeki ve herhangi bir geçici klasörde dosyaları hariç. hello kullanarak iki dosya belirtimleri oluşturacağız şekilde toodo [yeni OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - eklenmesi, diğeri dışarıda bırakma için. Merhaba Dosya belirtimleri oluşturduktan sonra hello kullanarak hello İlkesi ile ilişkili [Ekle OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet'i.

```
PS C:\> $inclusions = New-OBFileSpec -FileSpec @("C:\", "D:\")

PS C:\> $exclusions = New-OBFileSpec -FileSpec @("C:\windows", "C:\temp") -Exclude

PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $inclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid


PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $exclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\windows
                  IsExclude:True
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\temp
                  IsExclude:True
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```

### <a name="applying-hello-policy"></a>Hello İlkesi uygulama
Şimdi hello İlkesi tamamlandıktan ve ilişkili bir yedekleme zamanlaması, bekletme ilkesi ve dosyaların bir ekleme/çıkarma listesi vardır. Bu ilkeyi şimdi için Azure Backup toouse kaydedilmiş olabilir. İlke, yeni oluşturulan hello uygulamadan önce mevcut hiçbir yedekleme ilkeleri hello kullanarak hello sunucuyla ilişkili olduğundan emin olun [Kaldır OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet'i. Hello ilkesi kaldırma için onay ister. tooskip hello onay kullanmak hello ```-Confirm:$false``` hello cmdlet ile bayrağı.

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want tooremove this backup policy? This will delete all hello backed up data. [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
```

Uygulanıyor hello İlkesi yapılır hello kullanarak [kümesi OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet'i. Bu ayrıca onaylamanız istenir. tooskip hello onay kullanmak hello ```-Confirm:$false``` hello cmdlet ile bayrağı.

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want toosave this backup policy ? [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s)
DsList : {DataSource
         DatasourceId:4508156004108672185
         Name:C:\
         FileSpec:FileSpec
         FileSpec:C:\
         IsExclude:False
         IsRecursive:True,

         FileSpec
         FileSpec:C:\windows
         IsExclude:True
         IsRecursive:True,

         FileSpec
         FileSpec:C:\temp
         IsExclude:True
         IsRecursive:True,

         DataSource
         DatasourceId:4508156005178868542
         Name:D:\
         FileSpec:FileSpec
         FileSpec:D:\
         IsExclude:False
         IsRecursive:True
    }
PolicyName : c2eb6568-8a06-49f4-a20e-3019ae411bac
RetentionPolicy : Retention Days : 7
              WeeklyLTRSchedule :
              Weekly schedule is not set

              MonthlyLTRSchedule :
              Monthly schedule is not set

              YearlyLTRSchedule :
              Yearly schedule is not set
State : Existing PolicyState : Valid
```

Hello kullanarak hello mevcut bir yedekleme İlkesi hello ayrıntılarını görüntüleyebilirsiniz [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet'i. Daha fazla hello kullanarak ayrıntıya [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet'i hello yedekleme zamanlamasını ve hello için [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) hello bekletme ilkeleri için cmdlet

```
PS C:> Get-OBPolicy | Get-OBSchedule
SchedulePolicyName : 71944081-9950-4f7e-841d-32f0a0a1359a
ScheduleRunDays : {Saturday, Sunday}
ScheduleRunTimes : {16:00:00}
State : Existing

PS C:> Get-OBPolicy | Get-OBRetentionPolicy
RetentionDays : 7
RetentionPolicyName : ca3574ec-8331-46fd-a605-c01743a5265e
State : Existing

PS C:> Get-OBPolicy | Get-OBFileSpec
FileName : *
FilePath : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
FileSpec : D:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\
FileSpec : C:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\windows
FileSpec : C:\windows
IsExclude : True
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\temp
FileSpec : C:\temp
IsExclude : True
IsRecursive : True
```

### <a name="performing-an-ad-hoc-backup"></a>Bir geçici yedekleme gerçekleştirme
Bir yedekleme İlkesi ayarladıktan sonra hello yedeklemeleri hello zamanlama meydana gelir. Bir geçici yedekleme tetikleme ayrıca hello kullanarak olası [başlangıç OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:

```
PS C:> Get-OBPolicy | Start-OBBackup
Taking snapshot of volumes...
Preparing storage...
Estimating size of backup items...
Estimating size of backup items...
Transferring data...
Verifying backup...
Job completed.
hello backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a>Verileri Azure yedekten geri yükleyin
Bu bölümde, veri kurtarma Azure Backup otomatikleştirmek için hello adımlarında size yol gösterir. Bunu yapmak, böylece hello aşağıdaki adımları içerir:

1. Merhaba kaynak birimi seçin
2. Bir yedekleme noktası toorestore seçin
3. Bir öğe toorestore seçin
4. Tetikleyici hello geri yükleme işlemi

### <a name="picking-hello-source-volume"></a>Çekme hello kaynak birim
Sipariş toorestore öğeyi Azure Backup'da, ilk tooidentify hello kaynak hello öğesinin gerekir. Biz hello bağlamında bir Windows Server veya Windows İstemcisi hello komutları yürütülürken bu yana hello makine zaten tanımlanmış. Merhaba kaynağı tanımlayan bir hello sonraki adım içeren tooidentify hello birimdir. Bu makineden yedeklenen alınabilir hello yürüterek birimleri veya kaynakları listesini [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet'i. Bu komut, bu sunucu/istemciden yedeklenen tüm hello kaynakları bir dizi döndürür.

```
PS C:> $source = Get-OBRecoverableSource
PS C:> $source
FriendlyName : C:\
RecoverySourceName : C:\
ServerName : myserver.microsoft.com

FriendlyName : D:\
RecoverySourceName : D:\
ServerName : myserver.microsoft.com
```

### <a name="choosing-a-backup-point-toorestore"></a>Bir yedekleme noktası toorestore seçme
Merhaba yedekleme noktaları listesi hello yürüterek alınabilir [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) uygun parametreleri cmdlet'iyle. Bizim örneğimizde, son yedekleme noktası hello kaynak birim hello seçeceğiz *D:* ve toorecover belirli bir dosya kullanın.

```
PS C:> $rps = Get-OBRecoverableItem -Source $source[1]
IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :

IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 17-Jun-15 6:31:31 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :
```
Merhaba nesne ```$rps``` yedekleme noktaları dizisidir. Hello ilk öğe hello son noktası ve hello n. öğeyi hello eski noktasıdır. kullanacağız toochoose hello son noktası, ```$rps[0]```.

### <a name="choosing-an-item-toorestore"></a>Bir öğe toorestore seçme
tooidentify hello tam dosya veya klasör toorestore, yinelemeli olarak kullanın hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet'i. Bu şekilde hello klasör hiyerarşisini yalnızca hello kullanarak gözatılabilir ```Get-OBRecoverableItem```.

Bu örnekte, biz toorestore hello dosyanın istiyorsanız *finances.xls* Biz bu kullanarak başvuru hello nesne ```$filesFolders[1]```.

```
PS C:> $filesFolders = Get-OBRecoverableItem $rps[0]
PS C:> $filesFolders
IsDir : True
ItemNameFriendly : D:\MyData\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\
LocalMountPoint : D:\
MountPointName : D:\
Name : MyData
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime : 15-Jun-15 8:49:29 AM

PS C:> $filesFolders = Get-OBRecoverableItem $filesFolders[0]
PS C:> $filesFolders
IsDir : False
ItemNameFriendly : D:\MyData\screenshot.oxps
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\screenshot.oxps
LocalMountPoint : D:\
MountPointName : D:\
Name : screenshot.oxps
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 228313
ItemLastModifiedTime : 21-Jun-14 6:45:09 AM

IsDir : False
ItemNameFriendly : D:\MyData\finances.xls
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\finances.xls
LocalMountPoint : D:\
MountPointName : D:\
Name : finances.xls
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 96256
ItemLastModifiedTime : 21-Jun-14 6:43:02 AM
```

Hello kullanarak öğeleri toorestore için arama yapabilirsiniz ```Get-OBRecoverableItem``` cmdlet'i. Örneğimizde, toosearch için *finances.xls* biz şu komutu çalıştırarak hello dosyada bir tanıtıcı alabilir:

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-hello-restore-process"></a>Merhaba geri yükleme işlemini tetikler
tootrigger hello geri yükleme işlemi, ilk toospecify hello kurtarma seçenekleri ihtiyacımız var. Bu hello kullanarak yapılabilir [yeni OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet'i. Bu örnek, toorestore hello dosyaları çok istediğimizi varsayalım*C:\temp*. Ayrıca hello hedef klasörü zaten mevcut dosyalarda tooskip istiyoruz varsayalım *C:\temp*. toocreate böyle bir kurtarma seçeneği, komutu aşağıdaki hello kullanın:

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

Şimdi hello kullanarak geri yüklemeyi tetikleyecek [başlangıç OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) seçili hello komutunu ```$item``` hello hello çıktısından ```Get-OBRecoverableItem``` cmdlet:

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
hello recovery operation completed successfully.
```


## <a name="uninstalling-hello-azure-backup-agent"></a>Hello Azure Backup aracısını kaldırma
Kaldırma hello Azure Yedekleme aracısı, komutu aşağıdaki hello kullanarak gerçekleştirilebilir:

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

Merhaba Aracısı ikili dosyalarının hello makineden kaldırma bazı sonuçları tooconsider sahiptir:

* Merhaba dosya filtresi hello makineden kaldırır ve değişiklikleri izleme durduruldu.
* Tüm ilke bilgilerine hello makineden kaldırıldı, ancak hello ilkesi bilgileri hello hizmetinde depolanan toobe devam eder.
* Tüm yedekleme zamanlamaları kaldırılır ve daha fazla yedekleme alınır.

Ancak, Azure kalırken depolanan verileri hello ve hello bekletme ilkesi Kurulum göredir, tarafından korunur. Eski noktalarını otomatik olarak eski.

## <a name="remote-management"></a>Uzaktan Yönetim
Tüm hello yönetim hello Azure Yedekleme aracısı, ilkeler ve veri kaynakları çevresinde uzaktan PowerShell aracılığıyla gerçekleştirilebilir. Uzaktan yönetilecek hello makine doğru şekilde hazırlanmış toobe gerekir.

Varsayılan olarak, hello WinRM hizmeti el ile başlatma için yapılandırılır. Merhaba başlangıç türü çok ayarlanmalıdır*otomatik* ve hello hizmet başlatılabilir. WinRM hizmeti hello tooverify çalıştığından, hello Status özelliği hello değeri olmalıdır *çalıştıran*.

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

PowerShell uzaktan iletişim için yapılandırılmış olması gerekir.

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up tooreceive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

Merhaba makine artık uzaktan - hello hello aracı yüklemesinden başlatma yönetilebilir. Örneğin, komut dosyası izleyen hello hello aracı toohello uzak makine kopyalar ve onu yükler.

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a>Sonraki adımlar
Azure yedekleme için Windows Server/istemcisi bakın hakkında daha fazla bilgi için

* [Giriş tooAzure yedekleme](backup-introduction-to-azure-backup.md)
* [Windows sunucularını yedekleme](backup-configure-vault.md)
