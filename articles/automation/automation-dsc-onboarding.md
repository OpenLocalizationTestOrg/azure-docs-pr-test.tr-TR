---
title: "Azure Otomasyonu DSC yönetimine aaaOnboarding makineler | Microsoft Docs"
description: "Azure Otomasyonu DSC ile yönetimi için nasıl toosetup makineleri"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
ms.assetid: da13e1f5-2a1c-443b-8e3b-9f0d6f9e4810
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 12/13/2016
ms.author: eslesar
ms.openlocfilehash: ef15801fec2ffea4ba62dcba2fbe9af09268e424
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="onboarding-machines-for-management-by-azure-automation-dsc"></a>Azure Otomasyonu DSC tarafından Yönetim için hazırlama makineler

## <a name="why-manage-machines-with-azure-automation-dsc"></a>Neden Azure Otomasyonu DSC makinelerle yönetme?

Gibi [PowerShell istenen durum Yapılandırması](https://technet.microsoft.com/library/dn249912.aspx), tüm Bulut veya şirket içi veri merkezinde Azure Otomasyonu istenen durum yapılandırması olan DSC düğümleri (fiziksel ve sanal makineler) için basit ancak güçlü, yapılandırma yönetimi hizmeti. Bu ölçeklenebilirliği makineler binlerce arasında hızlı ve kolay bir şekilde bir merkezi, güvenli konumdan sağlar. Her makine bunları bildirim temelli yapılandırmaları ve gösteren raporları görüntüleme Ata uyumluluk istenen toohello durumu, belirtilen kullanıcının, kolayca yerleşik makineler olabilir. Hello Azure Otomasyonu DSC Yönetimi katmanıdır, tooDSC hangi hello Azure Otomasyonu yönetim katmanı olan tooPowerShell komut dosyası. Diğer bir deyişle, hello Azure Otomasyonu yardımcı olacak şekilde PowerShell komut dosyalarını yönetebilir, ayrıca, DSC yapılandırmalarını yönetmenize yardımcı olur. Azure Otomasyonu DSC, daha hello yararları hakkında toolearn bkz [Azure Otomasyonu DSC genel bakış](automation-dsc-overview.md).

Azure Otomasyonu DSC kullanılan toomanage makineler çeşitli olabilir:

* Azure sanal makineleri (Klasik)
* Azure sanal makineleri
* Amazon Web Hizmetleri (AWS) sanal makineler
* Windows fiziksel/sanal makineleri şirket içi veya bulutta Azure/AWS dışında
* Şirket içi, Azure veya Azure dışında bir bulut Linux fiziksel/sanal makineleri

Ayrıca, hazır toomanage makine hello bulut yapılandırmasından olup olmadığı, Azure Automation DSC de yalnızca rapor uç noktası olarak kullanılabilir. Azure Otomasyonu durumda düğüm uyumluluk hello ile ilgili zengin raporlama ayrıntıları görüntüle istenen ve bu DSC şirket içi aracılığıyla tooset (anında iletme) istenen yapılandırma sağlar.

Aşağıdaki bölümlerde hello yerleşik nasıl makine tooAzure Automation DSC her tür kullanabilir ana hatlarını vermektedir.

## <a name="azure-virtual-machines-classic"></a>Azure sanal makineleri (Klasik)

Azure Otomasyonu DSC'ye hello Azure portal veya PowerShell kullanarak yapılandırma yönetimi için kolayca yerleşik Azure sanal makineleri (Klasik) kullanabilirsiniz. Merhaba başlık altında ve tooremote hello VM uygulamasına sahip bir yönetici olmadan hello Azure VM istenen durum yapılandırması uzantısı hello VM Azure Otomasyonu DSC'ye kaydeder. Hello Azure VM istenen durum yapılandırması uzantısı adımları tootrack ilerleme durumunu zaman uyumsuz olarak çalışır veya sorun giderme olduğundan, sağlanan hello [ **sorun giderme Azure sanal makine ekleme** ](#troubleshooting-azure-virtual-machine-onboarding)bölümüne bakın.

### <a name="azure-portal"></a>Azure portalına

Merhaba, [Azure portal](http://portal.azure.com/), tıklatın **Gözat** -> **sanal makineleri (Klasik)**. Merhaba Windows tooonboard istediğiniz VM seçin. Merhaba sanal makinenin Pano dikey penceresinde **tüm ayarları** -> **uzantıları** -> **Ekle**  ->   **Azure Otomasyonu DSC** -> **oluşturma**. Merhaba girin [PowerShell DSC Local Configuration Manager değerleri](https://msdn.microsoft.com/powershell/dsc/metaconfig4) kullanım örneği, Otomasyon hesabınızın kayıt anahtarı ve kayıt URL'si ve bir düğüm yapılandırması tooassign toohello VM için isteğe bağlı olarak gereklidir.

![](./media/automation-dsc-onboarding/DSC_Onboarding_1.png)

toofind hello kayıt URL'si ve anahtar hello Otomasyon hesabı tooonboard hello makine için bkz: Merhaba [ **güvenli kayıt** ](#secure-registration) bölümüne bakın.

### <a name="powershell"></a>PowerShell

```powershell
# log in tooboth Azure Service Management and Azure Resource Manager
Add-AzureAccount
Add-AzureRmAccount

# fill in correct values for your VM/Automation account here
$VMName = ""
$ServiceName = ""
$AutomationAccountName = ""
$AutomationAccountResourceGroup = ""

# fill in hello name of a Node Configuration in Azure Automation DSC, for this VM tooconform to
$NodeConfigName = ""

# get Azure Automation DSC registration info
$Account = Get-AzureRmAutomationAccount -ResourceGroupName $AutomationAccountResourceGroup -Name $AutomationAccountName
$RegistrationInfo = $Account | Get-AzureRmAutomationRegistrationInfo

# use hello DSC extension tooonboard hello VM for management with Azure Automation DSC
$VM = Get-AzureVM -Name $VMName -ServiceName $ServiceName

$PublicConfiguration = ConvertTo-Json -Depth 8 @{
    SasToken = ""
    ModulesUrl = "https://eus2oaasibizamarketprod1.blob.core.windows.net/automationdscpreview/RegistrationMetaConfigV2.zip"
    ConfigurationFunction = "RegistrationMetaConfigV2.ps1\RegistrationMetaConfigV2"

# update these PowerShell DSC Local Configuration Manager defaults if they do not match your use case.
# See https://technet.microsoft.com/library/dn249922.aspx?f=255&MSPPError=-2147217396 for more details
    Properties = @{
    RegistrationKey = @{
        UserName = 'notused'
        Password = 'PrivateSettingsRef:RegistrationKey'
    }
    RegistrationUrl = $RegistrationInfo.Endpoint
    NodeConfigurationName = $NodeConfigName
    ConfigurationMode = "ApplyAndMonitor"
    ConfigurationModeFrequencyMins = 15
    RefreshFrequencyMins = 30
    RebootNodeIfNeeded = $False
    ActionAfterReboot = "ContinueConfiguration"
    AllowModuleOverwrite = $False
    }
}

$PrivateConfiguration = ConvertTo-Json -Depth 8 @{
    Items = @{
        RegistrationKey = $RegistrationInfo.PrimaryKey
    }
}

$VM = Set-AzureVMExtension `
    -VM $vm `
    -Publisher Microsoft.Powershell `
    -ExtensionName DSC `
    -Version 2.19 `
    -PublicConfiguration $PublicConfiguration `
    -PrivateConfiguration $PrivateConfiguration `
    -ForceUpdate

$VM | Update-AzureVM
```

## <a name="azure-virtual-machines"></a>Azure sanal makineleri

Azure Otomasyonu DSC hello Azure portal, Azure Resource Manager şablonları veya PowerShell kullanarak Azure sanal makineleri yapılandırma yönetimi için kolayca yerleşik sağlar. Merhaba başlık altında ve tooremote hello VM uygulamasına sahip bir yönetici olmadan hello Azure VM istenen durum yapılandırması uzantısı hello VM Azure Otomasyonu DSC'ye kaydeder. Hello Azure VM istenen durum yapılandırması uzantısı adımları tootrack ilerleme durumunu zaman uyumsuz olarak çalışır veya sorun giderme olduğundan, sağlanan hello [ **sorun giderme Azure sanal makine ekleme** ](#troubleshooting-azure-virtual-machine-onboarding)bölümüne bakın.

### <a name="azure-portal"></a>Azure portalına

Merhaba, [Azure portal](https://portal.azure.com/), toohello Azure Automation hesabını tooonboard sanal makineleri istediğiniz yere gidin. Merhaba Otomasyon hesabı Panoda tıklatın **DSC düğümleri** -> **eklemek Azure VM**.

Altında **seçin sanal makineleri tooonboard**daha fazla Azure sanal makineleri tooonboard veya seçin.

![](./media/automation-dsc-onboarding/DSC_Onboarding_2.png)

Altında **kayıt verilerini yapılandırma**, hello girin [PowerShell DSC Local Configuration Manager değerleri](https://msdn.microsoft.com/powershell/dsc/metaconfig4) kullanım örneği ve bir düğüm yapılandırması tooassign toohello VM için isteğe bağlı olarak gereklidir.

![](./media/automation-dsc-onboarding/DSC_Onboarding_3.png)

### <a name="azure-resource-manager-templates"></a>Azure Resource Manager şablonları

Azure sanal makineler dağıtılabilir ve Azure Resource Manager şablonları aracılığıyla edildi tooAzure Automation DSC. Bkz: [VM DSC uzantısı aracılığıyla ve Azure Otomasyonu DSC yapılandırma](https://azure.microsoft.com/documentation/templates/dsc-extension-azure-automation-pullserver/) bir örnek şablon için bu onboards var olan bir VM tooAzure Automation DSC. gerçekleştirilecek toofind hello kayıt anahtarı ve kayıt URL'si bu şablonda giriş olarak hello bkz [ **güvenli kayıt** ](#secure-registration) bölümüne bakın.

### <a name="powershell"></a>PowerShell

Merhaba [Register-AzureRmAutomationDscNode](/powershell/module/azurerm.automation/register-azurermautomationdscnode) cmdlet hello PowerShell aracılığıyla Azure portalında sanal makinelerinizde kullanılan tooonboard olabilir.

## <a name="amazon-web-services-aws-virtual-machines"></a>Amazon Web Hizmetleri (AWS) sanal makineler

Kolayca yerleşik Amazon Web Hizmetleri sanal makineler tarafından hello AWS DSC Araç Seti kullanarak Azure Otomasyonu DSC yapılandırma yönetimi için kullanabilirsiniz. Merhaba araç hakkında daha fazla bilgiyi [burada](https://blogs.msdn.microsoft.com/powershell/2016/04/20/aws-dsc-toolkit/).

## <a name="physicalvirtual-windows-machines-on-premises-or-in-a-cloud-other-than-azureaws"></a>Windows fiziksel/sanal makineleri şirket içi veya bulutta Azure/AWS dışında

Şirket içi Windows makinelerini ve Windows Azure olmayan Bulutları (örneğin, Amazon Web Hizmetleri) makinelerinizde de olabilir edildi tooAzure Otomasyonu DSC, giden erişim toohello sahip oldukları sürece birkaç basit adımda üzerinden internet:

1. Emin hello en son sürümünü olun [WMF 5](http://aka.ms/wmf5latest) yüklü hello makinelerde tooonboard tooAzure Automation DSC istiyor.
2. Merhaba bölümündeki yönergeleri izleyin [ **oluşturma DSC metaconfigurations** ](#generating-dsc-metaconfigurations) toogenerate DSC metaconfigurations hello içeren klasörü gerekli.
3. Uzaktan hello PowerShell DSC meta yapılandırmasını toohello makineler tooonboard istediğiniz uygulayın. **Merhaba makinesinin bu komutu çalıştırmak, hello en son sürümünü olmalıdır [WMF 5](http://aka.ms/wmf5latest) yüklü**:

    ```powershell
    Set-DscLocalConfigurationManager -Path C:\Users\joe\Desktop\DscMetaConfigs -ComputerName MyServer1, MyServer2
    ```

4. Merhaba PowerShell DSC metaconfigurations uzaktan uygulanamıyor varsa, 2. adımda her makine tooonboard üzerine hello metaconfigurations klasörüne kopyalayın. ' I çağırın **kümesi DscLocalConfigurationManager** her makine tooonboard yerel olarak.
5. Hello Azure portal veya cmdlet'ler, Azure Otomasyon hesabınızda hello makineler tooonboard şimdi gösterisini DSC düğümleri olarak kayıtlı onay kullanıyor.

## <a name="physicalvirtual-linux-machines-on-premises-in-azure-or-in-a-cloud-other-than-azure"></a>Şirket içi, Azure veya Azure dışında bir bulut Linux fiziksel/sanal makineleri

Şirket içi Linux makineler için Azure, Linux makinelerde ve Linux Azure olmayan bulut makinelerinizde de olabilir edildi tooAzure Otomasyonu DSC, giden erişim toohello sahip oldukları sürece birkaç basit adımda üzerinden internet:

1. Emin hello en son sürümünü olun [PowerShell istenen durum yapılandırması Linux için](https://github.com/Microsoft/PowerShell-DSC-for-Linux) yüklü hello makinelerde tooonboard tooAzure Automation DSC istiyor.
2. Merhaba, [PowerShell DSC Local Configuration Manager varsayılanları](https://msdn.microsoft.com/powershell/dsc/metaconfig4) , kullanım büyük küçük harf duyarlı ve tooonboard makineleri gibi istediğiniz, bunlar **her ikisi de** isteneceğini ve tooAzure Automation DSC Rapor:

   + Her Linux makine tooonboard tooAzure üzerinde Otomasyonu DSC, PowerShell DSC Local Configuration Manager varsayılan olarak hello kullanarak Register.py tooonboard kullanın:

     `/opt/microsoft/dsc/Scripts/Register.py <Automation account registration key> <Automation account registration URL>`

   + toofind hello kayıt anahtarı ve kayıt Automation hesabınız için URL'i hello [ **güvenli kayıt** ](#secure-registration) bölümüne bakın.

     Merhaba, PowerShell DSC Local Configuration Manager varsayılan olarak **yapmak** **değil** tooonboard makineleri bunlar yalnızca tooAzure Automation DSC rapor, ancak değil çekme şekilde istediğiniz veya kullanım örneği eşleşmesi yapılandırma veya PowerShell modülleri, adım 3-6 izleyin. Aksi takdirde, doğrudan toostep 6 devam edin.

3. Merhaba hello içindeki yönergeleri izleyin [ **oluşturma DSC metaconfigurations** ](#generating-dsc-metaconfigurations) gerekli hello DSC metaconfigurations içeren klasörü toogenerate bölümünde.
4. Uzaktan hello PowerShell DSC meta yapılandırmasını toohello makineler tooonboard istediğiniz Uygula:

    ```powershell
    $SecurePass = ConvertTo-SecureString -String "<root password>" -AsPlainText -Force
    $Cred = New-Object System.Management.Automation.PSCredential "root", $SecurePass
    $Opt = New-CimSessionOption -UseSsl -SkipCACheck -SkipCNCheck -SkipRevocationCheck

    # need a CimSession for each Linux machine tooonboard

    $Session = New-CimSession -Credential $Cred -ComputerName <your Linux machine> -Port 5986 -Authentication basic -SessionOption $Opt

    Set-DscLocalConfigurationManager -CimSession $Session -Path C:\Users\joe\Desktop\DscMetaConfigs
    ```

Merhaba makinesinin bu komutu çalıştırmak, hello en son sürümünü olmalıdır [WMF 5](http://aka.ms/wmf5latest) yüklü.

1. Merhaba PowerShell DSC metaconfigurations her Linux makine tooonboard için uzaktan uygulayamazsınız, hello meta yapılandırmasını karşılık gelen toothat makine hello Linux makine üzerine 5. adımda hello klasörünü kopyalayın. ' I çağırın `SetDscLocalConfigurationManager.py` yerel olarak tooonboard tooAzure Automation DSC istediğiniz her Linux makinesinde:

   `/opt/microsoft/dsc/Scripts/SetDscLocalConfigurationManager.py -configurationmof <path toometaconfiguration file>`

2. Hello Azure portal veya cmdlet'ler, Azure Otomasyon hesabınızda hello makineler tooonboard şimdi gösterisini DSC düğümleri olarak kayıtlı onay kullanıyor.

## <a name="generating-dsc-metaconfigurations"></a>DSC metaconfigurations oluşturma

toogenerically tooAzure Otomasyonu DSC, herhangi bir makine yerleşik bir [DSC meta yapılandırmasını](https://msdn.microsoft.com/en-us/powershell/dsc/metaconfig) olabilir uygulanan, hello DSC Aracısı hello makine toopull bildirir ve/veya tooAzure Automation DSC rapor, oluşturulur. Azure Otomasyonu DSC DSC metaconfigurations bir PowerShell DSC yapılandırması ya da hello Azure Automation PowerShell cmdlet'lerini kullanarak oluşturulabilir.

> [!NOTE]
> DSC metaconfigurations hello gereken gizli tooonboard makine tooan Otomasyon hesabı Yönetim için içerir. Oluşturduğunuz tüm DSC metaconfigurations korumak veya kullandıktan sonra silin emin tooproperly olun.

### <a name="using-a-dsc-configuration"></a>DSC Yapılandırması'nı kullanarak

1. Yerel ortamınızdaki bir makinede Hello PowerShell ISE'yi yönetici olarak açın. Merhaba makine hello en son sürümünü olmalıdır [WMF 5](http://aka.ms/wmf5latest) yüklü.
2. Komut dosyası yerel olarak aşağıdaki hello kopyalayın. Bu komut dosyası metaconfigurations ve komut tookick hello meta yapılandırmasını oluşturma devre dışı oluşturmak için PowerShell DSC yapılandırması içerir.

    ```powershell
    # hello DSC configuration that will generate metaconfigurations
    [DscLocalConfigurationManager()]
    Configuration DscMetaConfigs
    {

        param
        (
            [Parameter(Mandatory=$True)]
            [String]$RegistrationUrl,

            [Parameter(Mandatory=$True)]
            [String]$RegistrationKey,

            [Parameter(Mandatory=$True)]
            [String[]]$ComputerName,

            [Int]$RefreshFrequencyMins = 30,

            [Int]$ConfigurationModeFrequencyMins = 15,

            [String]$ConfigurationMode = "ApplyAndMonitor",

            [String]$NodeConfigurationName,

            [Boolean]$RebootNodeIfNeeded= $False,

            [String]$ActionAfterReboot = "ContinueConfiguration",

            [Boolean]$AllowModuleOverwrite = $False,

            [Boolean]$ReportOnly
        )

        if(!$NodeConfigurationName -or $NodeConfigurationName -eq "")
        {
            $ConfigurationNames = $null
        }
        else
        {
            $ConfigurationNames = @($NodeConfigurationName)
        }

        if($ReportOnly)
        {
        $RefreshMode = "PUSH"
        }
        else
        {
        $RefreshMode = "PULL"
        }

        Node $ComputerName
        {

            Settings
            {
                RefreshFrequencyMins = $RefreshFrequencyMins
                RefreshMode = $RefreshMode
                ConfigurationMode = $ConfigurationMode
                AllowModuleOverwrite = $AllowModuleOverwrite
                RebootNodeIfNeeded = $RebootNodeIfNeeded
                ActionAfterReboot = $ActionAfterReboot
                ConfigurationModeFrequencyMins = $ConfigurationModeFrequencyMins
            }

            if(!$ReportOnly)
            {
            ConfigurationRepositoryWeb AzureAutomationDSC
                {
                    ServerUrl = $RegistrationUrl
                    RegistrationKey = $RegistrationKey
                    ConfigurationNames = $ConfigurationNames
                }

                ResourceRepositoryWeb AzureAutomationDSC
                {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
                }
            }

            ReportServerWeb AzureAutomationDSC
            {
                ServerUrl = $RegistrationUrl
                RegistrationKey = $RegistrationKey
            }
        }
    }

    # Create hello metaconfigurations
    # TODO: edit hello below as needed for your use case
    $Params = @{
        RegistrationUrl = '<fill me in>';
        RegistrationKey = '<fill me in>';
        ComputerName = @('<some VM tooonboard>', '<some other VM tooonboard>');
        NodeConfigurationName = 'SimpleConfig.webserver';
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 15;
        RebootNodeIfNeeded = $False;
        AllowModuleOverwrite = $False;
        ConfigurationMode = 'ApplyAndMonitor';
        ActionAfterReboot = 'ContinueConfiguration';
        ReportOnly = $False;  # Set too$True toohave machines only report tooAA DSC but not pull from it
    }

    # Use PowerShell splatting toopass parameters toohello DSC configuration being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    DscMetaConfigs @Params
    ```

3. Merhaba kayıt anahtarı ve URL, Automation hesabı, yanı sıra hello makineler tooonboard hello adlarını doldurun. Diğer tüm parametreler isteğe bağlıdır. toofind hello kayıt anahtarı ve kayıt Automation hesabınız için URL'i hello [ **güvenli kayıt** ](#secure-registration) bölümüne bakın.
4. Merhaba makineler tooreport DSC durum bilgileri tooAzure Automation DSC istiyor, ancak yapılandırma veya PowerShell modülleri çekme değil, hello ayarlamak **sadece rapor** parametresi tootrue.
5. Merhaba komut dosyasını çalıştırın. Adlı bir klasör şimdi olmalıdır **DscMetaConfigs** hello PowerShell DSC metaconfigurations hello makineler tooonboard (Yönetici) olarak için çalışma dizininizi içeren:

    ```powershell
    Set-DscLocalConfigurationManager -Path ./DscMetaConfigs
    ```

### <a name="using-hello-azure-automation-cmdlets"></a>Hello Azure Automation cmdlet'leri kullanma

Kullanım örneği Hello PowerShell DSC Local Configuration Manager Varsayılanları eşlemek ve bunlar isteneceğini hem tooAzure Automation DSC rapor şekilde tooonboard makineler istiyorsanız hello Azure Automation cmdlet'leri hello DSC oluşturmanın basitleştirilmiş bir yöntem sağlar. gerekli metaconfigurations:

1. Yerel ortamınızdaki bir makinede Hello PowerShell konsolunu veya PowerShell ISE'yi yönetici olarak açın.
2. TooAzure Kaynak Yöneticisi'ni kullanarak bağlanmak **Add-AzureRmAccount**
3. Merhaba Otomasyon gelen tooonboard istediğiniz hello makineler tooonboard düğümleri istediğiniz toowhich hesabı için hello PowerShell DSC metaconfigurations yükleyin:

    ```powershell
    # Define hello parameters for Get-AzureRmAutomationDscOnboardingMetaconfig using PowerShell Splatting
    $Params = @{

        ResourceGroupName = 'ContosoResources'; # hello name of hello ARM Resource Group that contains your Azure Automation Account
        AutomationAccountName = 'ContosoAutomation'; # hello name of hello Azure Automation Account where you want a node on-boarded to
        ComputerName = @('web01', 'web02', 'sql01'); # hello names of hello computers that hello meta configuration will be generated for
        OutputFolder = "$env:UserProfile\Desktop\";
    }
    # Use PowerShell splatting toopass parameters toohello Azure Automation cmdlet being invoked
    # For more info about splatting, run: Get-Help -Name about_Splatting
    Get-AzureRmAutomationDscOnboardingMetaconfig @Params
    ```
    
4. Adlı bir klasör şimdi olmalıdır ***DscMetaConfigs***, hello PowerShell DSC metaconfigurations hello makineler tooonboard (Yönetici) olarak için içeren:
    
    ```powershell
    Set-DscLocalConfigurationManager -Path $env:UserProfile\Desktop\DscMetaConfigs
    ```

## <a name="secure-registration"></a>Güvenli kayıt

Makineler güvenli bir şekilde yerleşik tooan (Azure Otomasyonu DSC dahil) bir DSC düğümü tooauthenticate tooa PowerShell V2 DSC çekme veya Raporlama sunucusu verir hello WMF 5 DSC kaydı protokolü aracılığıyla Azure Automation hesabını kullanabilirsiniz. Merhaba düğümü kaydeder toohello sunucuda bir **kayıt URL'si**, kimlik doğrulama kullanarak bir **kayıt anahtarı**. Kayıt sırasında hello DSC düğümü ve DSC çekme/raporlama sunucusu kimlik doğrulaması toohello sunucu sonrası kaydı için bu düğümü toouse için benzersiz bir sertifika anlaşmaları. Bu işlem, bir başka bir düğüm bir gibi tehlikeye kimliğine bürünmek ve kötü amaçlı olarak davranmakta edildi düğümleri engeller. Kayıt sonra hello kayıt anahtarını yeniden kimlik doğrulaması için kullanılmaz ve hello düğümden silinir.

Merhaba DSC kaydı hello protokolünden için gereken hello bilgiler alabilirsiniz **anahtarları Yönet** dikey penceresinde hello Azure Önizleme portalı. Bu dikey penceresinde hello hello anahtar simgesine tıklayarak açın **Essentials** paneli hello Otomasyon hesabı için.

![](./media/automation-dsc-onboarding/DSC_Onboarding_4.png)

* Kayıt URL'si hello URL hello anahtarları Yönet dikey penceresinde bir alandır.
* Kayıt anahtarı hello anahtarları Yönet dikey penceresinde hello birincil erişim tuşunu veya ikincil erişim anahtarını değil. Her iki anahtar kullanılabilir.

Ek güvenlik için herhangi bir anda bir Otomasyon hesabı hello birincil ve ikincil erişim anahtarlarını üretilebilir (Merhaba üzerinde **anahtarları Yönet** dikey) önceki anahtar kullanılarak tooprevent gelecekteki düğümü kayıtlar.

## <a name="troubleshooting-azure-virtual-machine-onboarding"></a>Sorun giderme Azure sanal makine ekleme

Azure Otomasyonu DSC, yapılandırma yönetimi için Azure Windows Vm'lerini kolayca eklemeyi olanak tanır. Merhaba başlık altında hello Azure VM istenen durum yapılandırması uzantısı kullanılan tooregister hello Azure Otomasyonu DSC VM ' dir. Hello Azure VM istenen durum yapılandırması uzantısı zaman uyumsuz olarak çalışır olduğundan, ilerleme durumunu izleme ve sorun giderme yürütülmesinin önemli olabilir.

> [!NOTE]
> Bir Azure Windows VM tooAzure hello Azure VM istenen durum yapılandırması uzantısını kullanır Automation DSC tooan saat hello düğümü tooshow için ayarlama Azure Otomasyonu'nda kayıtlı olarak ele geçirebilir ekleme herhangi bir yöntemini. Toohello yüklemesinde Windows Management Framework 5.0 hello VM gerekli tooonboard hello VM tooAzure Automation DSC olduğu hello Azure VM DSC uzantısı tarafından son budur.

hello Azure VM istenen durum yapılandırması uzantısı'hello Azure Portalı'nda tootroubleshoot veya Görünüm hello durumunu gidin toohello edildi olan VM tıklatın ardından -> **tüm ayarları** -> **uzantıları**   ->  **DSC**. Daha fazla ayrıntı için tıklattığınız **ayrıntılı durumunu görüntüleme**.

[![](./media/automation-dsc-onboarding/DSC_Onboarding_5.png)](https://technet.microsoft.com/library/dn249912.aspx)

## <a name="certificate-expiration-and-reregistration"></a>Sertifika geçerlilik süresi ve saklanması

Bir Azure Otomasyonu DSC DSC düğüm olarak bir makine kaydolduktan sonra pek çok neden tooreregister hello bu düğümünde gelecekteki ihtiyacınız vardır:

* Kaydolduktan sonra her düğüme benzersiz bir sertifikası bir yıl sonra süresi dolar kimlik doğrulaması için otomatik olarak görüşür. Şu anda, bir yılın zamanından sonra tooreregister hello düğümleri gerekiyor süre sonu yaklaştığı zaman hello PowerShell DSC kaydı Protokolü otomatik olarak sertifikalarını yenileyemiyor. Yeniden önce her düğüm Windows Management Framework 5.0 RTM çalıştığından emin olun. Bir düğümün kimlik doğrulama sertifikasının süresi dolar ve hello düğümü değil yeniden kaydetme, hello düğümü Azure Automation oluşturulamıyor toocommunicate olacak ve 'Unresponsive.' işaretlenir 90 gün saklanması gerçekleştirilen veya küçük hello sertifika sona erme saati veya hello sertifika sona erme saati sonra herhangi bir noktada oluşturulan ve kullanılan yeni bir sertifika içinde neden olur.
* toochange herhangi [PowerShell DSC Local Configuration Manager değerleri](https://msdn.microsoft.com/powershell/dsc/metaconfig4) ConfigurationMode gibi hello düğümünün ilk kaydı sırasında kümesi. Şu anda bu DSC Aracısı değerleri yalnızca yeniden kayıt işlemi değiştirilebilir. Merhaba tek özel durum hello düğüm toohello düğümü atanan yapılandırması kullanılır--bu doğrudan Azure Otomasyonu DSC değiştirilebilir.

Yeniden kayıt işlemi hello düğümü başlangıçta hello ekleme yöntemlerden birini kullanarak kaydettiğiniz aynı şekilde bu belgede açıklanan hello gerçekleştirilebilir. Azure Otomasyonu DSC düğüm toounregister yeniden önce gerekmez.

## <a name="related-articles"></a>İlgili makaleler

* [Azure Otomasyonu DSC genel bakış](automation-dsc-overview.md)
* [Azure Otomasyonu DSC cmdlet'leri](/powershell/module/azurerm.automation/#automation)
* [Azure Otomasyonu DSC fiyatlandırması](https://azure.microsoft.com/pricing/details/automation/)
