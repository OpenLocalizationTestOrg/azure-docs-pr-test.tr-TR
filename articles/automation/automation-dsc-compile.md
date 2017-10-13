---
title: "Azure Otomasyonu DSC yapılandırmalarında derleme | Microsoft Docs"
description: "Bu makalede, Azure Otomasyonu istenen durum Yapılandırması'nı (DSC) yapılandırmaları derlemek açıklar."
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
ms.assetid: 49f20b31-4fa5-4712-b1c7-8f4409f1aecc
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 02/07/2017
ms.author: magoedte; eslesar
ms.openlocfilehash: 1aadd604e676659475f00760af3b0bdfb13a4792
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="compiling-configurations-in-azure-automation-dsc"></a>Azure Otomasyonu DSC yapılandırmalarında derleme

İstenen durum Yapılandırması'nı (DSC) yapılandırmaları Azure Automation iki yolla derleyebilirsiniz: Azure portalında ve Windows PowerShell ile. Aşağıdaki tabloda, her özelliklerine göre hangi yöntemi kullanmak ne zaman belirlemenize yardımcı olur:

### <a name="azure-portal"></a>Azure portalına

* Etkileşimli kullanıcı arabirimi ile basit yöntemi
* Basit parametre değerlerini sağlamak için form
* İş durumu kolayca izleme
* İle Azure oturum açma kimliği doğrulanmış erişim

### <a name="windows-powershell"></a>Windows PowerShell

* Windows PowerShell cmdlet'leri ile komut satırından çağırma
* Birden çok adımı otomatik Çözümle eklenebilir
* Basit ve karmaşık parametre değerlerini sağlayın
* İş durumu izleme
* PowerShell cmdlet'leri desteklemek için gereken istemci
* Geçişi ConfigurationData
* Kimlik bilgilerini kullanan yapılandırmaları derleme

Bir derleme yöntem karar verdikten sonra ilgili derleme başlatmak için aşağıdaki yordamları izleyebilirsiniz.

## <a name="compiling-a-dsc-configuration-with-the-azure-portal"></a>DSC yapılandırması Azure portal ile derleme

1. Otomasyon hesabınızdan tıklatın **DSC yapılandırmaları**.
2. Kendi dikey penceresini açmak için bir yapılandırma öğesini tıklatın.
3. Tıklatın **derleme**.
4. Yapılandırma hiçbir parametrelere sahipse, derlemeniz isteyip istemediğinizi onaylamanız istenir. Yapılandırma parametreleri, varsa **derleme yapılandırma** parametre değerlerini sağlayabilmesi için dikey penceresi açılır. Bkz: [ **temel parametreleri** ](#basic-parameters) bölümünde aşağıdaki parametreler hakkında daha fazla ayrıntı için.
5. **Derleme işi** derleme işin durumu ve neden Azure Automation DSC çekme Sunucusu'nda yerleştirilecek düğüm yapılandırmaları (MOF yapılandırma belgeler) izleyebilmeniz için dikey penceresi açılır.

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a>DSC Yapılandırması Windows PowerShell ile derleme

Kullanabileceğiniz [ `Start-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) Windows PowerShell ile derleme başlatmak için. Aşağıdaki örnek kod adlı bir DSC yapılandırma derlenmesini başlatır **SampleConfig**.

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

`Start-AzureRmAutomationDscCompilationJob`durumunu izlemek için kullanabileceğiniz bir derleme iş nesnesi döndürür. Bu derleme iş nesnesi ile sonra kullanabileceğiniz [ `Get-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) derleme işi durumunu belirlemek için ve [ `Get-AzureRmAutomationDscCompilationJobOutput` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) kendi akışlar (çıktı) görüntülemek için. Aşağıdaki örnek kod derlenmesini başlatır **SampleConfig** yapılandırması tamamlandı ve onun akışları görüntüler kadar bekler.

```powershell
$CompilationJob = Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"

while($CompilationJob.EndTime –eq $null -and $CompilationJob.Exception –eq $null)
{
    $CompilationJob = $CompilationJob | Get-AzureRmAutomationDscCompilationJob
    Start-Sleep -Seconds 3
}

$CompilationJob | Get-AzureRmAutomationDscCompilationJobOutput –Stream Any
```

## <a name="basic-parameters"></a>Temel parametreleri
DSC yapılandırmaları, parametre türleri ve özellikleriyle birlikte parametresi bildiriminde Azure Otomasyon çalışma kitabı olduğu gibi aynı şekilde çalışır. Bkz: [Azure Otomasyonu runbook başlatma](automation-starting-a-runbook.md) runbook parametreleri hakkında daha fazla bilgi edinmek için.

Aşağıdaki örnek adlı iki parametre kullanır **FeatureName** ve **olmasına**özelliklerinde değerleri belirlemek için **ParametersExample.sample** düğümü derleme sırasında oluşturulan yapılandırma.

```powershell
Configuration ParametersExample
{
    param(
        [Parameter(Mandatory=$true)]

        [string] $FeatureName,

        [Parameter(Mandatory=$true)]
        [boolean] $IsPresent
    )

    $EnsureString = "Present"
    if($IsPresent -eq $false)
    {
        $EnsureString = "Absent"
    }

    Node "sample"
    {
        WindowsFeature ($FeatureName + "Feature")
        {
            Ensure = $EnsureString
            Name = $FeatureName
        }
    }
}
```

Azure Otomasyonu DSC portalında veya Azure PowerShell ile temel parametrelerini kullanmak DSC yapılandırmaları hazırlayabilirsiniz:

### <a name="portal"></a>Portal

Portalda, tıkladıktan sonra parametre değerlerini girebilirsiniz **derleme**.

![alternatif metin](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a>PowerShell

PowerShell parametrelerinde gerektiren bir [hashtable](http://technet.microsoft.com/library/hh847780.aspx) burada anahtarının parametre adıyla eşleştiği ve değerin parametre değeri eşittir.

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

PSCredentials parametre olarak geçirme hakkında daha fazla bilgi için bkz: <a href="#credential-assets"> **kimlik bilgisi varlıkları** </a> aşağıda.

## <a name="configurationdata"></a>ConfigurationData
**ConfigurationData** , PowerShell DSC kullanırken hiçbir ortamı belirli yapılandırması yapısal yapılandırmasından ayırmanıza olanak tanır. Bkz: ["Ne" PowerShell DSC "nerede" ayırarak](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) hakkında daha fazla bilgi için **ConfigurationData**.

> [!NOTE]
> Kullanabileceğiniz **ConfigurationData** Azure PowerShell kullanarak Azure Otomasyonu DSC, ancak Azure Portalı'ndaki derlerken.

Aşağıdaki örnek DSC yapılandırmasını kullanan **ConfigurationData** aracılığıyla **$ConfigurationData** ve **$AllNodes** anahtar sözcükler. Ayrıca gerekir [ **xWebAdministration** Modülü](https://www.powershellgallery.com/packages/xWebAdministration/) Bu, örneğin:

```powershell
Configuration ConfigurationDataSample
{
    Import-DscResource -ModuleName xWebAdministration -Name MSFT_xWebsite

    Write-Verbose $ConfigurationData.NonNodeData.SomeMessage

    Node $AllNodes.Where{$_.Role -eq "WebServer"}.NodeName
    {
        xWebsite Site
        {
            Name = $Node.SiteName
            PhysicalPath = $Node.SiteContents
            Ensure   = "Present"
        }
    }
}
```

Yukarıdaki PowerShell DSC yapılandırması derleyebilirsiniz. Aşağıdaki PowerShell iki düğüm yapılandırmaları Azure Automation DSC çekme sunucusuna ekler: **ConfigurationDataSample.MyVM1** ve **ConfigurationDataSample.MyVM3**:

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "MyVM1"
            Role = "WebServer"
        },
        @{
            NodeName = "MyVM2"
            Role = "SQLServer"
        },
        @{
            NodeName = "MyVM3"
            Role = "WebServer"
        }
    )

    NonNodeData = @{
        SomeMessage = "I love Azure Automation DSC!"
    }
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ConfigurationDataSample" -ConfigurationData $ConfigData
```

## <a name="assets"></a>Varlıklar

Varlık başvuruları Azure Otomasyonu DSC yapılandırmaları ve runbook'ları aynıdır. Daha fazla bilgi için aşağıdakilere bakın:

* [Sertifikalar](automation-certificates.md)
* [Bağlantılar](automation-connections.md)
* [Kimlik Bilgileri](automation-credentials.md)
* [Değişkenler](automation-variables.md)

### <a name="credential-assets"></a>Kimlik bilgisi varlıkları

Azure Otomasyonu DSC yapılandırmalarında kullanarak kimlik bilgisi varlıkları başvurabilir sırada **Get-AzureRmAutomationCredential**, kimlik bilgisi varlıkları de geçirilebilir içinde parametreleri aracılığıyla isterseniz. Bir yapılandırma parametresi, uzun sürerse **PSCredential** bir Azure Otomasyonu kimlik bilgisi varlığı dize adını bir PSCredential nesnesi yerine bu parametrenin değeri olarak geçirmenize gerek sonra yazın. Arka planda Azure Otomasyonu kimlik bilgisi varlığı bu ada sahip alınabilir ve yapılandırmaya geçirildi.

Kimlik bilgileri tutma düğüm yapılandırmaları (MOF yapılandırma belgeler) güvenli kimlik bilgileri düğüm yapılandırması MOF dosyasındaki şifrelenmesini gerektirir. Azure Otomasyonu bunu bir adım daha fazla sürer ve tüm MOF dosyası şifreler. Ancak, şu anda, PowerShell DSC Azure Otomasyonu tüm MOF dosyası neslini sonra şifreleme, PowerShell DSC bilmiyor çünkü için kimlik bilgilerini düz metin olarak düğüm yapılandırması MOF oluşturma sırasında yüzdelik kesebilirsiniz söylemelisiniz derleme işi.

İçin kimlik bilgilerini düz metin olarak oluşturulan düğüm yapılandırması MOF dosyalarından yüzdelik uygundur PowerShell DSC anlayabilirsiniz kullanarak [ **ConfigurationData**](#configurationdata). Geçmesi `PSDscAllowPlainTextPassword = $true` aracılığıyla **ConfigurationData** DSC yapılandırması görüntülenir ve kimlik bilgilerini kullanan her düğüm bloğun adı.

Aşağıdaki örnekte bir Otomasyon kimlik bilgisi varlığı kullanan bir DSC yapılandırmasını gösterir.

```powershell
Configuration CredentialSample
{
    $Cred = Get-AzureRmAutomationCredential -ResourceGroupName "ResourceGroup01" -AutomationAccountName "AutomationAcct" -Name "SomeCredentialAsset"

    Node $AllNodes.NodeName
    {
        File ExampleFile
        {
            SourcePath = "\\Server\share\path\file.ext"
            DestinationPath = "C:\destinationPath"
            Credential = $Cred
        }
    }
}
```

Yukarıdaki PowerShell DSC yapılandırması derleyebilirsiniz. Aşağıdaki PowerShell iki düğüm yapılandırmaları Azure Automation DSC çekme sunucusuna ekler: **CredentialSample.MyVM1** ve **CredentialSample.MyVM2**.

```powershell
$ConfigData = @{
    AllNodes = @(
        @{
            NodeName = "*"
            PSDscAllowPlainTextPassword = $True
        },
        @{
            NodeName = "MyVM1"
        },
        @{
            NodeName = "MyVM2"
        }
    )
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "CredentialSample" -ConfigurationData $ConfigData
```

## <a name="importing-node-configurations"></a>Düğüm yapılandırmaları alma

Ayrıca Azure dışında derlediğiniz düğümü configuratons (MOF dosyalarından) içe aktarabilirsiniz. Bu bir avantajı, o düğümü confiturations imzalanabilir ' dir.
İmzalı düğüm yapılandırması düğüme uygulanan yapılandırma yetkili bir kaynaktan geldiğinden emin olduktan DSC aracı tarafından yönetilen bir düğümde yerel olarak doğrulanır.

> [!NOTE]
> İçeri aktarma kullanabilirsiniz yapılandırmaları Azure Automation hesabınızda oturumu, ancak Azure Otomasyonu desteklememektedir imzalı yapılandırmaları derleme.

> [!NOTE]
> Bir düğüm yapılandırma dosyası Azure Automation'a içeri aktarılacak izin vermek için 1 MB'tan büyük olmalıdır.

Düğüm yapılandırmaları https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module adresindeki oturum öğrenebilirsiniz.

### <a name="importing-a-node-configuration-in-the-azure-portal"></a>Azure portalında bir düğüm yapılandırması içe aktarma

1. Otomasyon hesabınızdan tıklatın **DSC düğüm yapılandırmaları**.

    ![DSC düğüm yapılandırmaları](./media/automation-dsc-compile/node-config.png)
2. İçinde **DSC düğüm yapılandırmaları** dikey penceresinde tıklatın **bir NodeConfiguration eklemek**.
3. İçinde **alma** dikey penceresinde yanındaki klasör simgesine tıklayın **düğümü yapılandırma dosyası** , yerel bilgisayarınızda bir düğüm yapılandırma dosyası (MOF) göz atmak için metin kutusu.

    ![Yerel dosya gözatın.](./media/automation-dsc-compile/import-browse.png)
4. Bir ad girin **yapılandırma adı** metin kutusu. Bu ad, düğüm yapılandırması derlenen yapılandırmasının adı eşleşmelidir.
5. **Tamam** düğmesine tıklayın.

### <a name="importing-a-node-configuration-with-powershell"></a>Düğüm yapılandırması PowerShell ile içeri aktarma

Kullanabileceğiniz [alma AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) düğüm yapılandırması Otomasyon hesabınızda içeri aktarmak için cmdlet.

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```



