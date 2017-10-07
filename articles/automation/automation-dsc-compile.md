---
title: "Azure Otomasyonu DSC yapılandırmalarında aaaCompiling | Microsoft Docs"
description: "Bu makalede nasıl toocompile istenen durum Yapılandırması'nı (DSC) yapılandırmaları Azure Automation için."
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
ms.openlocfilehash: b195311318a2d7431c4d6b29f4b9a5f3a0a0a9a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="compiling-configurations-in-azure-automation-dsc"></a>Azure Otomasyonu DSC yapılandırmalarında derleme

İstenen durum Yapılandırması'nı (DSC) yapılandırmaları Azure Automation iki yolla derleyebilirsiniz: hello Azure portalı ve Windows PowerShell ile. Merhaba aşağıdaki tabloda, ne zaman belirlemenize yardımcı hangi yöntemi her hello özelliklerine göre toouse:

### <a name="azure-portal"></a>Azure portalına

* Etkileşimli kullanıcı arabirimi ile basit yöntemi
* Form tooprovide basit parametre değerleri
* İş durumu kolayca izleme
* İle Azure oturum açma kimliği doğrulanmış erişim

### <a name="windows-powershell"></a>Windows PowerShell

* Windows PowerShell cmdlet'leri ile komut satırından çağırma
* Birden çok adımı otomatik Çözümle eklenebilir
* Basit ve karmaşık parametre değerlerini sağlayın
* İş durumu izleme
* Gerekli istemci toosupport PowerShell cmdlet'leri
* Geçişi ConfigurationData
* Kimlik bilgilerini kullanan yapılandırmaları derleme

Bir derleme yöntem karar verdikten sonra toostart derleme aşağıda hello ilgili yordamları izleyebilirsiniz.

## <a name="compiling-a-dsc-configuration-with-hello-azure-portal"></a>DSC yapılandırması hello Azure portal ile derleme

1. Otomasyon hesabınızdan tıklatın **DSC yapılandırmaları**.
2. Bir yapılandırma tooopen kendi dikey tıklayın.
3. Tıklatın **derleme**.
4. Merhaba yapılandırma hiçbir parametrelere sahipse, toocompile istediğinizi istendiğinde tooconfirm olacaktır. Merhaba yapılandırma parametrelere sahipse, hello **derleme yapılandırma** parametre değerlerini sağlayabilmesi için dikey penceresi açılır. Merhaba bkz [ **temel parametreleri** ](#basic-parameters) bölümünde aşağıdaki parametreler hakkında daha fazla ayrıntı için.
5. Merhaba **derleme işi** hello derleme işin durumunu izleyebilir ve hello düğüm yapılandırmaları (MOF yapılandırma belgeler) Azure Automation DSC çekme sunucusuna hello üzerinde yerleştirilen toobe neden dikey penceresi açılır.

## <a name="compiling-a-dsc-configuration-with-windows-powershell"></a>DSC Yapılandırması Windows PowerShell ile derleme

Kullanabileceğiniz [ `Start-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/start-azurermautomationdsccompilationjob) toostart Windows PowerShell ile derleme. Aşağıdaki örnek kod hello başlatır adlı bir DSC yapılandırma derlenmesini **SampleConfig**.

```powershell
Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "SampleConfig"
```

`Start-AzureRmAutomationDscCompilationJob`derleme döndürür durumunu tootrack kullanabileceğiniz nesne işi. Bu derleme iş nesnesi ile sonra kullanabileceğiniz [ `Get-AzureRmAutomationDscCompilationJob` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjob) toodetermine hello hello derleme işi durumunu ve [ `Get-AzureRmAutomationDscCompilationJobOutput` ](/powershell/module/azurerm.automation/get-azurermautomationdsccompilationjoboutput) tooview kendi akışlar (çıktı). Aşağıdaki örnek kod hello başlatır hello derlenmesini **SampleConfig** yapılandırması tamamlandı ve onun akışları görüntüler kadar bekler.

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
DSC yapılandırmaları, parametre türleri ve özellikler, works dahil olmak üzere parametresi bildiriminde hello aynı Azure Otomasyon çalışma kitabı olduğu gibi. Bkz: [Azure Otomasyonu runbook başlatma](automation-starting-a-runbook.md) toolearn runbook parametreleri hakkında daha fazla bilgi.

Merhaba aşağıdaki örnek kullanır adlı iki parametre **FeatureName** ve **olmasına**, toodetermine hello değerlerini hello özelliklerinde **ParametersExample.sample** düğümü derleme sırasında oluşturulan yapılandırma.

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

DSC yapılandırmaları'hello Azure Otomasyonu DSC portalında veya Azure PowerShell ile temel parametrelerini kullanmak hazırlayabilirsiniz:

### <a name="portal"></a>Portal

Merhaba Portalı'nda tıkladıktan sonra parametre değerlerini girebilirsiniz **derleme**.

![alternatif metin](./media/automation-dsc-compile/DSC_compiling_1.png)

### <a name="powershell"></a>PowerShell

PowerShell parametrelerinde gerektiren bir [hashtable](http://technet.microsoft.com/library/hh847780.aspx) burada hello anahtar hello parametre adı ile eşleşen ve hello değerine eşit hello parametre değeri.

```powershell
$Parameters = @{
    "FeatureName" = "Web-Server"
    "IsPresent" = $False
}

Start-AzureRmAutomationDscCompilationJob -ResourceGroupName "MyResourceGroup" -AutomationAccountName "MyAutomationAccount" -ConfigurationName "ParametersExample" -Parameters $Parameters
```

PSCredentials parametre olarak geçirme hakkında daha fazla bilgi için bkz: <a href="#credential-assets"> **kimlik bilgisi varlıkları** </a> aşağıda.

## <a name="configurationdata"></a>ConfigurationData
**ConfigurationData** tooseparate yapısal PowerShell DSC kullanırken hiçbir ortam belirli yapılandırma yapılandırmasından sağlar. Bkz: ["Ne" PowerShell DSC "nerede" ayırarak](http://blogs.msdn.com/b/powershell/archive/2014/01/09/continuous-deployment-using-dsc-with-minimal-change.aspx) toolearn hakkında daha fazla **ConfigurationData**.

> [!NOTE]
> Kullanabileceğiniz **ConfigurationData** Azure PowerShell kullanarak Azure Otomasyonu DSC, ancak hello Azure portal derlerken.

Merhaba aşağıdaki örnek DSC yapılandırmasını kullanan **ConfigurationData** hello aracılığıyla **$ConfigurationData** ve **$AllNodes** anahtar sözcükler. Ayrıca hello gerekir [ **xWebAdministration** Modülü](https://www.powershellgallery.com/packages/xWebAdministration/) Bu, örneğin:

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

PowerShell ile Merhaba DSC yapılandırması yukarıda derleyebilirsiniz. PowerShell aşağıda Hello iki düğüm yapılandırmaları toohello Azure Automation DSC çekme sunucusuna ekler: **ConfigurationDataSample.MyVM1** ve **ConfigurationDataSample.MyVM3**:

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

Varlık başvuruları olan hello Azure Otomasyonu DSC yapılandırmaları ve runbook'ları aynı. Daha fazla bilgi için Hello aşağıdakilere bakın:

* [Sertifikalar](automation-certificates.md)
* [Bağlantılar](automation-connections.md)
* [Kimlik Bilgileri](automation-credentials.md)
* [Değişkenler](automation-variables.md)

### <a name="credential-assets"></a>Kimlik bilgisi varlıkları

Azure Otomasyonu DSC yapılandırmalarında kullanarak kimlik bilgisi varlıkları başvurabilir sırada **Get-AzureRmAutomationCredential**, kimlik bilgisi varlıkları de geçirilebilir içinde parametreleri aracılığıyla isterseniz. Bir yapılandırma parametresi, uzun sürerse **PSCredential** yazın yeniden PSCredential nesnesinin yerine bu parametrenin değeri olarak bir Azure Otomasyonu kimlik bilgisi varlığı toopass hello dize adı gerekiyor. Merhaba arka planda hello Azure Otomasyonu kimlik bilgisi varlığı bu ada sahip alınabilir ve toohello yapılandırma geçirildi.

Kimlik bilgileri tutma düğüm yapılandırmaları (MOF yapılandırma belgeler) güvenliğini hello kimlik hello düğüm yapılandırması MOF dosyasındaki şifrelenmesini gerektirir. Azure Otomasyonu bunu bir adım daha fazla sürer ve hello tüm MOF dosyası şifreler. Ancak, şu anda, PowerShell DSC, olduğundan kesebilirsiniz düğüm yapılandırması MOF oluşturma sırasında düz metin olarak yüzdelik kimlik bilgilerini toobe için PowerShell DSC Azure Otomasyonu hello tüm MOF dosyası sonra şifreleme bilmiyor söylemelisiniz kendi derleme işi aracılığıyla oluşturma.

PowerShell DSC oluşturulan hello düğüm yapılandırması MOF dosyalarından düz metinde yüzdelik kimlik bilgilerini toobe için uygun olduğunu anlayabilirsiniz kullanarak [ **ConfigurationData**](#configurationdata). Geçmesi `PSDscAllowPlainTextPassword = $true` aracılığıyla **ConfigurationData** hello DSC yapılandırması görünür ve kimlik bilgilerini kullanan her düğüm bloğun adı.

Merhaba aşağıdaki örnekte bir Otomasyon kimlik bilgisi varlığı kullanan bir DSC yapılandırması gösterilmektedir.

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

PowerShell ile Merhaba DSC yapılandırması yukarıda derleyebilirsiniz. PowerShell aşağıda Hello iki düğüm yapılandırmaları toohello Azure Automation DSC çekme sunucusuna ekler: **CredentialSample.MyVM1** ve **CredentialSample.MyVM2**.

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
İmzalı düğüm yapılandırması uygulanan toohello düğümü olan hello yapılandırmayı yetkili bir kaynaktan geldiğinden emin hello DSC aracısı tarafından yönetilen bir düğümde yerel olarak doğrulanır.

> [!NOTE]
> İçeri aktarma kullanabilirsiniz yapılandırmaları Azure Automation hesabınızda oturumu, ancak Azure Otomasyonu desteklememektedir imzalı yapılandırmaları derleme.

> [!NOTE]
> Bir düğüm yapılandırma dosyası 1 MB tooallow büyük olmalıdır, Azure Automation'a içeri toobe.

Bilgi edinebilirsiniz nasıl https://msdn.microsoft.com/en-us/powershell/wmf/5.1/dsc-improvements#how-to-sign-configuration-and-module adresindeki toosign düğüm yapılandırmaları.

### <a name="importing-a-node-configuration-in-hello-azure-portal"></a>Bir düğüm yapılandırması hello Azure portal içeri aktarma

1. Otomasyon hesabınızdan tıklatın **DSC düğüm yapılandırmaları**.

    ![DSC düğüm yapılandırmaları](./media/automation-dsc-compile/node-config.png)
2. Merhaba, **DSC düğüm yapılandırmaları** dikey penceresinde tıklatın **bir NodeConfiguration eklemek**.
3. Merhaba, **alma** dikey penceresinde hello klasör simgesine sonraki toohello tıklatın **düğümü yapılandırma dosyası** textbox toobrowse, yerel bilgisayarınızda bir düğüm yapılandırma dosyası (MOF) için.

    ![Yerel dosya gözatın.](./media/automation-dsc-compile/import-browse.png)
4. Hello bir ad girin **yapılandırma adı** metin kutusu. Bu adı hello düğüm yapılandırması derlenmiş olduğu hello yapılandırmasının hello adıyla eşleşmelidir.
5. **Tamam** düğmesine tıklayın.

### <a name="importing-a-node-configuration-with-powershell"></a>Düğüm yapılandırması PowerShell ile içeri aktarma

Merhaba kullanabilirsiniz [alma AzureRmAutomationDscNodeConfiguration](/powershell/module/azurerm.automation/import-azurermautomationdscnodeconfiguration) cmdlet tooimport Otomasyon hesabınızda bir düğüm yapılandırması.

```powershell
Import-AzureRmAutomationDscNodeConfiguration -AutomationAccountName "MyAutomationAccount" -ResourceGroupName "MyResourceGroup" -ConfigurationName "MyNodeConfiguration" -Path "C:\MyConfigurations\TestVM1.mof"
```



