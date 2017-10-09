---
title: aaaDeploy hello Azure Otomasyonu DSC Site Recovery Mobility hizmetiyle | Microsoft Docs
description: "Nasıl toouse Azure Otomasyonu DSC tooautomatically dağıtmak hello Azure Site Recovery Mobility hizmeti ve Azure Aracısı VMware sanal ve fiziksel sunucu çoğaltma tooAzure açıklar"
services: site-recovery
documentationcenter: 
author: krnese
manager: lorenr
editor: 
ms.assetid: 1f8cd3ac-0522-48eb-a5f0-679ee9192ddb
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: krnese
ms.openlocfilehash: 52cdd13ceb61718a21137180c55db86919af5929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-mobility-service-with-azure-automation-dsc-for-replication-of-vm"></a>VM çoğaltması için Azure Otomasyonu DSC ile Merhaba Mobility hizmetini dağıtma
Operations Management Suite biz kapsamlı yedekleme ve iş sürekliliği planınızın bir parçası olarak kullanabileceğiniz olağanüstü durum kurtarma çözümü sağlar.

Biz bu gezisine Hyper-V ile birlikte Hyper-V çoğaltma kullanılarak başlatıldı. Ancak müşteriler kendi bulut birden fazla hiper ve platformlar olduğundan genişletilmiş toosupport heterojen Kurulum sunuyoruz.

VMware iş yükleri ve/veya fiziksel sunucuları bugün çalıştırıyorsanız, Azure, hedef olduğunda bir yönetim sunucusu tüm hello Azure Site Recovery bileşenleri, ortam toohandle hello iletişim ve veri çoğaltma, Azure ile çalışır.

## <a name="deploy-hello-site-recovery-mobility-service-by-using-automation-dsc"></a>Automation DSC kullanarak Hello Site Recovery Mobility hizmeti dağıtma
Bu yönetim sunucusu yaptığı bir hızlı dökümünü yaparak başlayalım.

Hello yönetim sunucusu, çeşitli sunucu rolleri çalıştırır. Bu roller, biri *yapılandırma*, hangi iletişimi düzenler ve veri çoğaltma ve kurtarma işlemlerini yönetir.

Ayrıca, hello *işlem* rol çoğaltma ağ geçidi olarak davranır. Bu rolü korumalı kaynak makinelerden çoğaltma verilerini alıp, önbelleğe alma, sıkıştırma ve şifreleme iyileştirir ve tooan Azure depolama hesabı gönderir. Hello işlevleri hello işlem rolü için birini de toopush yükleme hello Mobility hizmeti tooprotected makinelerin ve VMware vm'lerinin otomatik bulma gerçekleştirin.

Bir azure'dan ise hello *ana hedef* rolü, bu işlemin bir parçası olarak hello çoğaltma verileri işleyecek.

Merhaba korumalı makineler için biz üzerinde hello kullanan *Mobility hizmeti*. Bu bileşen tooreplicate tooAzure istediğiniz dağıtılan tooevery (VMware VM veya fiziksel sunucu) makinesidir. Merhaba makinede veri Yazar yakalar ve bunları toohello yönetim sunucusu (işlem rolü) iletir.

İş sürekliliği ile ilgilenirken önemli toounderstand iş yüklerinizi, altyapı ve hello bileşenleri dahil değil. Ardından Kurtarma süresi hedefi (RTO) ve kurtarma noktası hedefi (RPO) hello gereksinimleri karşılayabilir. Bu bağlamda anahtar tooensuring hello Mobility hizmeti olan beklediğiniz gibi iş yüklerinizi korunur.

Bu nedenle nasıl, iyileştirilmiş bir şekilde, bazı Operations Management Suite bileşenleri Yardım ile güvenilir bir korumalı kurulum olmasını sağlayabilirsiniz?

Bu makalede, Azure Otomasyonu istenen durum yapılandırması (DSC), Site Recovery, tooensure birlikte nasıl kullanabileceğinize bir örnek sağlar:

* Merhaba Mobility hizmeti ve Azure VM Aracısı tooprotect istediğiniz dağıtılan toohello Windows makinelerdir.
* Azure hello çoğaltma hedefi olduğunda hello Mobility hizmeti ve Azure VM Aracısı her zaman çalışır.

## <a name="prerequisites"></a>Ön koşullar
* Bir depo toostore gerekli hello Kurulumu
* Parola tooregister hello yönetim sunucusu ile bir depo toostore hello gerekli

  > [!NOTE]
  > Her yönetim sunucusu için benzersiz bir parola oluşturulur. Birden çok yönetim sunucusu toodeploy kullanacaksanız, bu hello parola hello passphrase.txt dosyasında depolanan doğru tooensure sahip.
  >
  >
* Windows Management Framework (WMF) koruma (Automation DSC gereksinimini) için tooenable istediğiniz hello makinelerde yüklü 5.0

  > [!NOTE]
  > WMF 4.0 yüklü olan toouse DSC for Windows makineler istiyorsanız hello bölümüne bakın [bağlantısı kesilmiş ortamlarda kullanım DSC](## Use DSC in disconnected environments).
  

Merhaba Mobility hizmeti hello komut satırı yüklenebilir ve birkaç bağımsız değişken kabul eder. İşte bu nedenle Burada, alabilir bunları DSC Yapılandırması kullanılarak bir yerde saklayın ve toohave hello ikili dosyaları (bunları, kurulumdan ayıkladıktan sonra) gerekir.

## <a name="step-1-extract-binaries"></a>1. adım: Extract ikili dosyalar
1. Bu kurulum için gereken tooextract hello dosyalar Dizin Yönetim sunucunuzda aşağıdaki toohello göz atın:

    **\Microsoft azure Site Recovery\home\svsystems\pushinstallsvc\repository**

    Bu klasörde, adlandırılmış bir MSI dosyası görmeniz gerekir:

    **Microsoft ASR_UA_version_Windows_GA_date_Release.exe**

    Komut tooextract hello Yükleyici aşağıdaki hello kullan:

    **.\Microsoft-ASR_UA_9.1.0.0_Windows_GA_02May2016_release.exe /q /x:C:\Users\Administrator\Desktop\Mobility_Service\Extract**
2. Tüm dosyaları seçin ve tooa sıkıştırılmış (ZIP) klasör gönderin.

Artık hello ikili dosyaları Automation DSC kullanarak hello Mobility hizmeti tooautomate hello Kurulumu ihtiyacınız vardır.

### <a name="passphrase"></a>Parola
Ardından, bu sıkıştırılmış klasörü tooplace istediğiniz yere toodetermine gerekir. Merhaba kurulum için gereken gösterilen daha sonra toostore hello parola olarak bir Azure depolama hesabı kullanabilirsiniz. Merhaba Aracısı sonra hello yönetim sunucusu hello işleminin bir parçası olarak kaydeder.

Merhaba yönetim sunucusunu dağıttığınızda aldığınız hello parola tooa metin dosyası passphrase.txt kaydedilebilir.

Merhaba daraltılmış klasörü ve hello parola hello Azure depolama hesabı adanmış bir kapsayıcıda yerleştirin.

![Klasör konumu](./media/site-recovery-automate-mobilitysevice-install/folder-and-passphrase-location.png)

Bu dosya paylaşımındaki ağınızdaki tookeep tercih ederseniz, bunu yapabilirsiniz. Daha sonra kullanacaksınız hello DSC kaynağı erişimi vardır ve hello Kurulum ve parola alabilirsiniz tooensure yeterlidir.

## <a name="step-2-create-hello-dsc-configuration"></a>2. adım: hello DSC yapılandırması oluştur
WMF 5. 0'Hello Kurulum bağlıdır. Automation DSC aracılığıyla hello yapılandırma Hello makine toosuccessfully için uygulama, WMF 5.0 toobe mevcut gerekiyor.

Merhaba ortamı örnek DSC yapılandırması aşağıdaki hello kullanır:

```powershell
configuration ASRMobilityService {

    $RemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    $RemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    $RemoteAzureAgent = 'http://go.microsoft.com/fwlink/p/?LinkId=394789'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node localhost {

        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            Ensure = 'Present'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
```
Merhaba yapılandırması yeterlidir hello aşağıdaki:

* Merhaba değişkenleri hello yapılandırma tooget hello burada parola ve toostore hello çıktı tooget hello Mobility hizmeti ve hello Azure VM Aracısı ikili dosyaları nerede hello söyler.
* böylece kullanabileceğiniz hello yapılandırma hello xPSDesiredStateConfiguration DSC kaynağı alacak `xRemoteFile` hello depodan toodownload hello dosyaları.
* Merhaba yapılandırmasını toostore hello ikili dosyaları istediğiniz bir dizin oluşturur.
* Merhaba arşiv kaynak hello dosyaları hello sıkıştırılmış klasörden ayıklayın.
* Merhaba paket yükleme kaynağı hello Mobility hizmeti UNIFIEDAGENT hello yükler. EXE yükleyici hello belirli bağımsız değişkenlere sahip. (Merhaba bağımsız değişkenleri oluşturmak hello değişkenleri ortamınız değiştirilen toobe tooreflect gerekir.)
* Merhaba paket AzureAgent kaynak Azure'da çalışan her VM üzerinde önerilen hello Azure VM aracısı yükler. Hello Azure VM aracısı ayrıca olası tooadd uzantıları toohello VM yük devretme sonrasında kolaylaştırır.
* Merhaba Hizmet kaynağı veya kaynakları hello Mobility Hizmetleri ilgili hello Azure hizmetlerinin her zaman çalıştığından emin olun ve.

Merhaba yapılandırma olarak Kaydet **ASRMobilityService**.

> [!NOTE]
> Böylece Hello Aracısı doğru bağlanır ve hello doğru parolayı kullanır, yapılandırma tooreflect hello gerçek yönetim sunucusu tooreplace hello CSIP unutmayın.
>
>

## <a name="step-3-upload-tooautomation-dsc"></a>3. adım: tooAutomation DSC karşıya yükle
Yaptığınız hello DSC yapılandırması gerekli bir DSC kaynakları Modülü (xPSDesiredStateConfiguration) alacağı için hello DSC yapılandırma karşıya yüklemeden önce otomasyon modülü tooimport gerekiyor.

Oturum açma tooyour Otomasyon hesabı Gözat çok**varlıklar** > **modülleri**, tıklatıp **Gözat galeri**.

Merhaba modülü burada aratın ve tooyour hesap içeri aktarın.

![İçeri aktarma modülü](./media/site-recovery-automate-mobilitysevice-install/search-and-import-module.png)

Bu tamamladığınızda, hello Azure Resource Manager modüllerini yüklü olduğu tooyour makine gidin ve tooimport yeni oluşturulan hello DSC yapılandırması devam edin.

### <a name="import-cmdlets"></a>İçeri aktarma cmdlet'leri
PowerShell'de tooyour Azure aboneliği oturum açın. Ortamınızı Hello cmdlet'leri tooreflect değiştirin ve Automation hesabı bilgilerinizi bir değişkende Yakala:

```powershell
$AAAccount = Get-AzureRmAutomationAccount -ResourceGroupName 'KNOMS' -Name 'KNOMSAA'
```

Merhaba yapılandırma tooAutomation DSC cmdlet'i aşağıdaki hello kullanarak karşıya yükle:

```powershell
$ImportArgs = @{
    SourcePath = 'C:\ASR\ASRMobilityService.ps1'
    Published = $true
    Description = 'DSC Config for Mobility Service'
}
$AAAccount | Import-AzureRmAutomationDscConfiguration @ImportArgs
```

### <a name="compile-hello-configuration-in-automation-dsc"></a>Automation DSC Hello yapılandırmasında derleme
Ardından, tooregister düğümleri tooit başlayabilmeniz toocompile hello Automation DSC yapılandırmasında gerekir. Bu cmdlet'i aşağıdaki hello çalıştırarak elde:

```powershell
$AAAccount | Start-AzureRmAutomationDscCompilationJob -ConfigurationName ASRMobilityService
```

Hello yapılandırma barındırılan toohello DSC çekme hizmeti temel olarak dağıtıyorsunuz için bu işlem birkaç dakika sürebilir.

Merhaba yapılandırma derledikten sonra PowerShell (Get-AzureRmAutomationDscCompilationJob) kullanarak veya hello kullanarak hello iş bilgilerini alabilir [Azure portal](https://portal.azure.com/).

![İş alma](./media/site-recovery-automate-mobilitysevice-install/retrieve-job.png)

Şimdi başarıyla yayımlandı ve DSC yapılandırma tooAutomation DSC karşıya.

## <a name="step-4-onboard-machines-tooautomation-dsc"></a>4. adım: Yerleşik makineler tooAutomation DSC
> [!NOTE]
> Bu senaryo Tamamlanıyor hello önkoşulları Windows makinelerinizi hello en son sürümüyle WMF güncelleştirilir biridir. Karşıdan yükle ve platformunuza hello gelen hello doğru sürümünü yüklemek [Yükleme Merkezi'nden](https://www.microsoft.com/download/details.aspx?id=50395).
>
>

Şimdi bir metaconfig tooyour düğümleri uygulanacağını DSC için oluşturacaksınız. toosucceed Bu, seçilen Otomasyon hesabınızda Azure tooretrieve hello uç noktası URL'si ve hello birincil anahtarı gerekir. Bu değerleri altında bulabilirsiniz **anahtarları** hello üzerinde **tüm ayarları** dikey penceresinde hello Otomasyon hesabı için.

![Anahtar değerleri](./media/site-recovery-automate-mobilitysevice-install/key-values.png)

Bu örnekte, tooprotect Site RECOVERY'yi kullanarak istediğiniz bir Windows Server 2012 R2 fiziksel sunucu vardır.

### <a name="check-for-any-pending-file-rename-operations-in-hello-registry"></a>Dosya yeniden adlandırma işlemleri hello kayıt defterinde beklemedeki denetle
Merhaba Automation DSC noktayla tooassociate hello sunucu başlamadan önce beklemede olan dosya yeniden adlandırma işlemleri hello kayıt defterinde için denetlemenizi öneririz. Son tamamlama hello Kurulum yasaklayabilir tooa yeniden başlatma bekleniyor.

Hiçbir yeniden başlatma bekleniyor hello sunucuda olduğunu cmdlet tooverify aşağıdaki hello çalıştırın:

```powershell
Get-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\' | Select-Object -Property PendingFileRenameOperations
```
Bu boş gösterir, Tamam tooproceed demektir. Aksi durumda, bu hello sunucunun bir bakım penceresi sırasında yeniden tarafından bulundurmalıdır.

Merhaba sunucuda tooapply hello yapılandırma hello PowerShell Tümleşik komut dosyası ortamı (ISE) başlatın ve komut dosyası izleyen hello çalıştırın. Merhaba Automation DSC hizmeti ile Merhaba yerel Configuration Manager altyapısı tooregister istemek ve hello özel yapılandırma (ASRMobilityService.localhost) almak aslında bir DSC yerel yapılandırma budur.

```powershell
[DSCLocalConfigurationManager()]
configuration metaconfig {
    param (
        $URL,
        $Key
    )
    node localhost {
        Settings {
            RefreshFrequencyMins = '30'
            RebootNodeIfNeeded = $true
            RefreshMode = 'PULL'
            ActionAfterReboot = 'ContinueConfiguration'
            ConfigurationMode = 'ApplyAndMonitor'
            AllowModuleOverwrite = $true
        }

        ResourceRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }

        ConfigurationRepositoryWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
            ConfigurationNames = 'ASRMobilityService.localhost'
        }

        ReportServerWeb AzureAutomationDSC {
            ServerURL = $URL
            RegistrationKey = $Key
        }
    }
}
metaconfig -URL 'https://we-agentservice-prod-1.azure-automation.net/accounts/<YOURAAAccountID>' -Key '<YOURAAAccountKey>'

Set-DscLocalConfigurationManager .\metaconfig -Force -Verbose
```

Bu yapılandırma hello yerel Configuration Manager altyapısı tooregister kendisini Otomasyonu DSC'ye neden olur. Ayrıca, hello altyapısı nasıl çalışacağını, yapılandırma değişikliklerini (ApplyAndAutoCorrect) ise ne yapmanız gerektiğini ve yeniden başlatma gerekli olduğunda nasıl, hello yapılandırmasıyla devam etmemelisiniz belirler.

Bu komut dosyasını çalıştırdıktan sonra hello düğümü Otomasyonu DSC'ye tooregister başlamanız gerekir.

![Düğüm kayıt işlemi sürüyor](./media/site-recovery-automate-mobilitysevice-install/register-node.png)

Toohello Azure portalına geri dönün, o hello yeni kayıtlı düğüm hello Portalı'nda artık göründükten görebilirsiniz.

![Merhaba Portalı'nda kayıtlı düğümü](./media/site-recovery-automate-mobilitysevice-install/registered-node.png)

Merhaba sunucuda düğümü hello cmdlet tooverify doğru kayıtlı PowerShell aşağıdaki hello çalıştırabilirsiniz:

```powershell
Get-DscLocalConfigurationManager
```

Merhaba yapılandırma çekilen ve uygulanan toohello sunucu alındıktan sonra Bu cmdlet'i aşağıdaki hello çalıştırarak doğrulayabilirsiniz:

```powershell
Get-DscConfigurationStatus
```

Merhaba çıktısı hello sunucu yapılandırmasıyla başarıyla çekilen gösterilmektedir:

![Çıktı](./media/site-recovery-automate-mobilitysevice-install/successful-config.png)

Ayrıca, hello Mobility hizmeti Kurulumu konumunda bulunan kendi günlük sahip *SystemDrive*\ProgramData\ASRSetupLogs.

İşte bu kadar. Şimdi başarıyla dağıtılan ve Site Recovery kullanarak tooprotect istediğiniz hello makinedeki hello Mobility hizmeti kayıtlı. DSC hello gerekli hizmetleri zaman çalışır durumda olduğundan emin olun.

![Başarılı dağıtım](./media/site-recovery-automate-mobilitysevice-install/successful-install.png)

Merhaba yönetim sunucusu hello başarılı dağıtım algılandıktan sonra korumayı yapılandırın ve Site Recovery kullanarak hello makinesinde çoğaltmayı etkinleştirin.

## <a name="use-dsc-in-disconnected-environments"></a>Bağlantısı kesilmiş ortamlarda DSC kullanın
Makinelerinizi bağlı toohello Internet değilseniz, hala DSC toodeploy üzerinde kullanır ve tooprotect istediğiniz hello iş yükleri üzerinde hello Mobility hizmetini yapılandırın.

Kendi DSC istek sunucusuyla ortamınızda örneği tooessentially hello Automation DSC'den alma aynı yetenekleri sağlar. Diğer bir deyişle, (kaydedildikten sonra) hello istemcileri hello yapılandırma çeker toohello DSC uç noktası. Ancak, başka bir toomanually itme hello DSC yapılandırma tooyour makineler, yerel olarak veya uzaktan seçenektir.

Bu örnekte, hello bilgisayar adı için ek bir parametre yoktur. Merhaba uzak dosyalar, artık tooprotect istediğiniz hello makineler tarafından erişilebilir olması gereken bir uzak paylaşım bulunur. Merhaba hello komut dosyasının sonuna hello yapılandırma enacts ve ardından tooapply hello DSC yapılandırma toohello hedef bilgisayarı başlatır.

### <a name="prerequisites"></a>Ön koşullar
Bu hello xPSDesiredStateConfiguration PowerShell Modülü yüklü olduğundan emin olun. WMF 5.0 yüklü olduğu Windows makineler için hello xPSDesiredStateConfiguration modülü cmdlet hello hedef makinede aşağıdaki hello çalıştırarak yükleyebilirsiniz:

```powershell
Find-Module -Name xPSDesiredStateConfiguration | Install-Module
```

Ayrıca indirin ve toodistribute gerektiğinde Merhaba modülü kaydedin, WMF 4.0 sahip tooWindows makineler. Bu cmdlet, PowerShellGet (WMF 5.0) mevcut olduğu bir makinede çalıştırın:

```powershell
Save-Module -Name xPSDesiredStateConfiguration -Path <location>
```

Ayrıca bu hello WMF 4.0 için olun [Windows 8.1 güncelleştirmesi KB2883200](https://www.microsoft.com/download/details.aspx?id=40749) hello makinelerde yüklü.

Merhaba aşağıdaki yapılandırma WMF 5.0 ve WMF 4.0 tooWindows makineler gönderilemez:

```powershell
configuration ASRMobilityService {
    param (
        [Parameter(Mandatory=$true)]
        [ValidateNotNullOrEmpty()]
        [System.String] $ComputerName
    )

    $RemoteFile = '\\myfileserver\share\asr.zip'
    $RemotePassphrase = '\\myfileserver\share\passphrase.txt'
    $RemoteAzureAgent = '\\myfileserver\share\AzureVmAgent.msi'
    $LocalAzureAgent = 'C:\Temp\AzureVmAgent.msi'
    $TempDestination = 'C:\Temp\asr.zip'
    $LocalPassphrase = 'C:\Temp\Mobility_service\passphrase.txt'
    $Role = 'Agent'
    $Install = 'C:\Program Files (x86)\Microsoft Azure Site Recovery'
    $CSEndpoint = '10.0.0.115'
    $Arguments = '/Role "{0}" /InstallLocation "{1}" /CSEndpoint "{2}" /PassphraseFilePath "{3}"' -f $Role,$Install,$CSEndpoint,$LocalPassphrase

    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    node $ComputerName {      
        File Directory {
            DestinationPath = 'C:\Temp\ASRSetup\'
            Type = 'Directory'            
        }

        xRemoteFile Setup {
            URI = $RemoteFile
            DestinationPath = $TempDestination
            DependsOn = '[File]Directory'
        }

        xRemoteFile Passphrase {
            URI = $RemotePassphrase
            DestinationPath = $LocalPassphrase
            DependsOn = '[File]Directory'
        }

        xRemoteFile AzureAgent {
            URI = $RemoteAzureAgent
            DestinationPath = $LocalAzureAgent
            DependsOn = '[File]Directory'
        }

        Archive ASRzip {
            Path = $TempDestination
            Destination = 'C:\Temp\ASRSetup'
            DependsOn = '[xRemotefile]Setup'
        }

        Package Install {
            Path = 'C:\temp\ASRSetup\ASR\UNIFIEDAGENT.EXE'
            Ensure = 'Present'
            Name = 'Microsoft Azure Site Recovery mobility Service/Master Target Server'
            ProductId = '275197FC-14FD-4560-A5EB-38217F80CBD1'
            Arguments = $Arguments
            DependsOn = '[Archive]ASRzip'
        }

        Package AzureAgent {
            Path = 'C:\Temp\AzureVmAgent.msi'
            Ensure = 'Present'
            Name = 'Windows Azure VM Agent - 2.7.1198.735'
            ProductId = '5CF4D04A-F16C-4892-9196-6025EA61F964'
            Arguments = '/q /l "c:\temp\agentlog.txt'
            DependsOn = '[Package]Install'
        }

        Service ASRvx {
            Name = 'svagents'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service ASR {
            Name = 'InMage Scout Application Service'
            State = 'Running'
            DependsOn = '[Package]Install'
        }

        Service AzureAgentService {
            Name = 'WindowsAzureGuestAgent'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }

        Service AzureTelemetry {
            Name = 'WindowsAzureTelemetryService'
            State = 'Running'
            DependsOn = '[Package]AzureAgent'
        }
    }
}
ASRMobilityService -ComputerName 'MyTargetComputerName'

Start-DscConfiguration .\ASRMobilityService -Wait -Force -Verbose
```

Automation DSC'den alabilir, şirket ağı toomimic hello yetenekleri üzerinde kendi DSC istek sunucusuyla tooinstantiate istiyorsanız bkz [DSC web çekme sunucusu kurma](https://msdn.microsoft.com/powershell/dsc/pullserver?f=255&MSPPError=-2147217396).

## <a name="optional-deploy-a-dsc-configuration-by-using-an-azure-resource-manager-template"></a>İsteğe bağlı: DSC yapılandırması bir Azure Resource Manager şablonu kullanarak dağıtın
Bu makale, kendi DSC yapılandırma tooautomatically nasıl oluşturabileceğinizi üzerinde odaklanılmış hello Mobility hizmeti ve hello Azure VM Aracısı--dağıtmak ve bunlar hello makinelerde tooprotect istediğiniz çalıştığından emin olun. Biz de bu DSC yapılandırması tooa yeni veya var olan Azure Otomasyon hesabı dağıtacağınız bir Azure Resource Manager şablonu vardır. Merhaba şablon hello değişkenleri ortamınız için içerecek giriş parametreleri toocreate Otomasyon varlıkları kullanır.

Merhaba şablon dağıttıktan sonra bu kılavuzu tooonboard içinde toostep 4 yalnızca makinelerinizi başvurabilir.

Merhaba şablon yeterlidir hello aşağıdaki:

1. Var olan Otomasyon hesabını kullanabilir veya yeni bir tane oluşturun
2. Giriş parametreleri için alın:
   * ASRRemoteFile--hello Mobility hizmeti Kurulumu depoladığınız hello konumu
   * ASRPassphrase--hello passphrase.txt dosyasını depoladığınız hello konumu
   * ASRCSEndpoint--yönetim sunucunuzun başlangıç IP adresi
3. Merhaba xPSDesiredStateConfiguration PowerShell modülünü içeri aktarın
4. Oluşturma ve hello DSC yapılandırmasını derleme

Makinelerinizi koruması için ekleme başlayabilmeniz adımları önceki tüm hello hello doğru sırada gerçekleşir.

Merhaba şablonla dağıtımı için yönergeler bulunur [GitHub](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/DSC).

PowerShell kullanarak Hello şablonu dağıtma:

```powershell
$RGDeployArgs = @{
    Name = 'DSC3'
    ResourceGroupName = 'KNOMS'
    TemplateFile = 'https://raw.githubusercontent.com/krnese/AzureDeploy/master/OMS/MSOMS/DSC/azuredeploy.json'
    OMSAutomationAccountName = 'KNOMSAA'
    ASRRemoteFile = 'https://knrecstor01.blob.core.windows.net/asr/ASR.zip'
    ASRRemotePassphrase = 'https://knrecstor01.blob.core.windows.net/asr/passphrase.txt'
    ASRCSEndpoint = '10.0.0.115'
    DSCJobGuid = [System.Guid]::NewGuid().ToString()
}
New-AzureRmResourceGroupDeployment @RGDeployArgs -Verbose
```

## <a name="next-steps"></a>Sonraki adımlar
Merhaba Mobility hizmeti aracıları dağıttıktan sonra şunları yapabilirsiniz [çoğaltmayı etkinleştirme](site-recovery-vmware-to-azure.md) hello sanal makineler için.
