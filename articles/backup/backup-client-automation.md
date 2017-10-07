---
title: "Windows Server tooAzure yukarı aaaUse PowerShell tooback | Microsoft Docs"
description: "Bilgi nasıl toodeploy ve Azure PowerShell kullanarak yedekleme yönetme"
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 65218095-2996-44d9-917b-8c84fc9ac415
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: saurse;markgal;jimpark;nkolli;trinadhk
ms.openlocfilehash: f13224f53abd6fbd132fee4347b0b99e8f5e2678
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

Bu makale size nasıl gösterir toouse Azure yedekleme Windows Server veya Windows İstemcisi ayarlama ve yedekleme ve kurtarma yönetmek için PowerShell.

## <a name="install-azure-powershell"></a>Azure PowerShell'i yükleme
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

Bu makalede hello Azure Resource Manager (ARM) ve hello bir kaynak grubu bir kurtarma Hizmetleri kasasına toouse etkinleştirmek MS çevrimiçi yedekleme PowerShell cmdlet'leri odaklanır.

Azure PowerShell 1.0 Ekim 2015'te yayımlanmıştır. Bu sürüm hello 0.9.8 yayın başarılı oldu ve bazı önemli değişiklikler hakkında özellikle hello adlandırma deseni hello cmdlet'lerinin getirildi. 1.0 cmdlet'leri izleyin hello adlandırma deseni {fiil}-AzureRm {isim}; Merhaba 0.9.8 adlarında değil ancak **Rm** (örneğin, New-Azureresourcegroup yerine New-Azurermresourcegroup). Azure PowerShell 0.9.8 kullanıldığında, önce hello Resource Manager moduna hello çalıştırarak etkinleştirmelisiniz **Switch-AzureMode AzureResourceManager** komutu. Bu komut 1.0 veya üstü gerekli değildir.

Merhaba 0.9.8 ortamında hello 1.0 veya sonraki ortamı için yazılan komut dosyalarınızı toouse istiyorsanız dikkatle güncelleştirin ve test hello betikleri bir ön üretim ortamında üretim tooavoid kullanmadan önce beklenmeyen etkisi.

[Merhaba son PowerShell yayın indirme](https://github.com/Azure/azure-powershell/releases) (gerekli minimum sürüm: 1.0.0)

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-recovery-services-vault"></a>Kurtarma hizmetleri kasası oluşturma
Aşağıdaki adımları hello kurtarma Hizmetleri kasası oluşturmada size yol açar. Kurtarma Hizmetleri kasasına yedekleme Kasası ' farklıdır.

1. Azure Backup hello için ilk kez kullanıyorsanız hello kullanmalısınız **Register-AzureRMResourceProvider** cmdlet tooregister hello Azure Recovery hizmeti sağlayıcısı aboneliğinizle.

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. tooplace ihtiyacınız hello kurtarma Hizmetleri kasası bir ARM kaynak olduğundan, bir kaynak grubu içinde. Varolan bir kaynak grubunu kullanın veya yeni bir tane oluşturun. Yeni bir kaynak grubu oluştururken hello kaynak grubu için hello ad ve konum belirtin.  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "WestUS"
    ```
3. Kullanım hello **yeni AzureRmRecoveryServicesVault** cmdlet toocreate hello yeni Kasa. Toospecify hello hello kasa için aynı konumu hello kaynak grubu için kullanıldığından emin olun.

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "WestUS"
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

Merhaba komutu çalıştırmak **Get-AzureRmRecoveryServicesVault**, ve hello Abonelikteki tüm kasalarını listelenir.

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


## <a name="installing-hello-azure-backup-agent"></a>Hello Azure Backup aracısını yükleme
Hello Azure Backup aracısını yüklemeden önce indirildi ve Windows Server hello mevcut toohave hello yükleyici gerekir. Hello hello Installer hello en son sürümünü elde edebilirsiniz [Microsoft Download Center](http://aka.ms/azurebackup_agent) veya hello kurtarma Hizmetleri Kasası'nın Pano sayfası. Kolay erişilebilecek bir konuma tooan gibi Hello yükleyici Kaydet * C:\Downloads\*.

Alternatif olarak, PowerShell tooget hello Yükleyici'yi kullanın:
 
 ```
 $MarsAURL = 'Http://Aka.Ms/Azurebackup_Agent'
 $WC = New-Object System.Net.WebClient
 $WC.DownloadFile($MarsAURL,'C:\downloads\MARSAgentInstaller.EXE')
 C:\Downloads\MARSAgentInstaller.EXE /q
 ```

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

## <a name="registering-windows-server-or-windows-client-machine-tooa-recovery-services-vault"></a>Windows Server veya Windows istemci makine tooa kurtarma Hizmetleri kasası kaydetme
Merhaba kurtarma Hizmetleri kasası oluşturduktan sonra hello en son aracı hello kasa kimlik bilgilerini indirin ve C:\Downloads gibi uygun bir konuma depolayın.

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
```

Merhaba Windows Server veya Windows istemci makinesi üzerinde hello çalıştırmak [başlangıç OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet tooregister hello makine hello kasası ile.
Bu ve diğer cmdlet'leri yedekleme için kullanılan hello MSONLINE modülünden Mars AgentInstaller hello yükleme işleminin bir parçası olarak eklenen hangi hello ' dir. 

Merhaba aracı yükleyici hello $Env güncelleştirmez: PSModulePath değişkeni. Bu modül otomatik-yüklemesi başarısız anlamına gelir. tooresolve bu yapabilirsiniz hello aşağıdaki:

```
PS C:\>  $Env:psmodulepath += ';C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules
```

Alternatif olarak, el ile hello modülü betiğinizde şu şekilde yükleyebilirsiniz:

```
PS C:\>  Import-Module  'C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules\MSOnlineBackup'

```

Merhaba çevrimiçi yedekleme cmdlet'leri yük sonra hello kasa kimlik bilgilerini Kaydet:


```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :WestUS
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
PS C:\> $PassPhrase = ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force 
PS C:\> $PassCode   = 'AzureR0ckx'
PS C:\> Set-OBMachineSetting -EncryptionPassPhrase $PassPhrase
Server properties updated successfully
```

> [!IMPORTANT]
> Ayarlandıktan sonra hello parola bilgilerini güvenli ve güvenli tutar. Olan değil siz bu parolayı olmadan Azure mümkün toorestore verileri.
>
>

## <a name="back-up-files-and-folders"></a>Dosya ve klasörleri yedekleme
Windows sunucularını ve istemcilerini tooAzure yedekleme tüm yedeklemeleri bir ilke tarafından yönetilir. Hello İlkesi üç bölümden oluşur:

1. A **yedekleme zamanlaması** yedeklemeler alınır ve hello hizmeti ile eşitlenmiş toobe gerektiğinde belirtir.
2. A **bekletme zamanlaması** Azure'da ne kadar süreyle tooretain hello kurtarma noktaları belirtir.
3. A **dosya ekleme/çıkarma belirtimi** belirleyen ne yedeklenmelidir.

Yedekleme, otomatikleştirme beri bu belgede, hiçbir şey yapılandırılmış varsayıyoruz. Hello kullanarak yeni bir yedekleme ilkesi oluşturarak başlayın [yeni OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet'i.

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
Initializing
Taking snapshot of volumes...
Preparing storage...
Generating backup metadata information and preparing hello metadata VHD...
Data transfer is in progress. It might take longer since it is hello first backup and all data needs toobe transferred...
Data transfer completed and all backed up data is in hello cloud. Verifying data integrity...
Data transfer completed
In progress...
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

### <a name="choosing-a-backup-point-from-which-toorestore"></a>Hangi toorestore bir yedekleme noktasının seçme
Merhaba çalıştırarak yedekleme noktalarının bir listesini alma [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) uygun parametreleri cmdlet'iyle. Bizim örneğimizde, son yedekleme noktası hello kaynak birim hello seçeceğiz *D:* ve toorecover belirli bir dosya kullanın.

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

Hello kullanarak hello geri yükleme işlemi şimdi tetikleyebilir [başlangıç OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) seçili hello komutunu ```$item``` hello hello çıktısından ```Get-OBRecoverableItem``` cmdlet:

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
