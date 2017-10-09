---
title: "Azure Otomasyonu aaaCredential varlıkları | Microsoft Docs"
description: "Azure Otomasyonu kimlik bilgisi varlıkları hello runbook veya DSC yapılandırması tarafından erişilen kullanılan tooauthenticate tooresources olabilir güvenlik kimlik bilgilerini içerir. Bu makalede nasıl toocreate varlıklar kimlik bilgisi ve bunları bir runbook veya DSC yapılandırma açıklanmaktadır."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 3209bf73-c208-425e-82b6-df49860546dd
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/14/2017
ms.author: bwren
ms.openlocfilehash: 46f23a8f79d5863265af9cf84f6003e30f8e7d39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="credential-assets-in-azure-automation"></a>Azure Otomasyonu kimlik bilgisi varlıkları
Bir Otomasyon kimlik bilgisi varlığı tutan bir [PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) bir kullanıcı adı ve parola gibi güvenlik kimlik bilgileri içeren bir nesne. Merhaba kullanıcı adı ve hello PSCredential nesnesinin tooprovide toosome uygulama parolası veya kimlik doğrulaması gerektiren hizmet ayıklamak veya runbook'ları ve DSC yapılandırmaları kimlik doğrulaması için bir PSCredential nesnesi kabul cmdlet'leri kullanabilir. kimlik bilgileri Hello özellikleri Azure Otomasyonu'nda güvenli bir şekilde depolanır ve hello runbook ya da DSC yapılandırması hello ile erişilen [Get-AutomationPSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) etkinlik.

> [!NOTE]
> Azure Automation güvenli varlıkların kimlik bilgileri, sertifikalar, bağlantıları ve şifrelenmiş değişkenler içerir. Bu varlıklar şifrelenir ve hello Azure her Otomasyon hesabı için oluşturulan benzersiz bir anahtar kullanarak otomasyon depolanır. Bu anahtarı bir sertifika tarafından şifrelenir ve Azure Otomasyonu'nda depolanır. Güvenli bir varlık depolamak önce hello Otomasyon hesabının hello anahtarı hello ana sertifikayı kullanarak şifresi çözülür ve tooencrypt hello varlık kullanılır.  

## <a name="windows-powershell-cmdlets"></a>Windows PowerShell cmdlet'leri
Aşağıdaki tablonun hello Hello cmdlet'leri kullanılan toocreate olan ve Windows PowerShell ile automation kimlik bilgisi varlıkları yönetin.  Merhaba bir parçası olarak sevk [Azure PowerShell Modülü](/powershell/azure/overview) olduğu Automation runbook'ları ve DSC yapılandırmaları için kullanılabilir.

| Cmdlet'leri | Açıklama |
|:--- |:--- |
| [Get-AzureAutomationCredential](/powershell/module/azure/get-azureautomationcredential?view=azuresmps-3.7.0) |Bir kimlik bilgisi varlığı ilgili bilgileri alır. Merhaba kimlik bilgisi kendisi yalnızca alabilir gelen **Get-AutomationPSCredential** etkinlik. |
| [AzureAutomationCredential yeni](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |Yeni bir Otomasyon kimlik bilgisi oluşturur. |
| [Remove - AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |Otomasyon kimlik bilgileri kaldırır. |
| [Set - AzureAutomationCredential](/powershell/module/azure/new-azureautomationcredential?view=azuresmps-3.7.0) |Ayarlar, var olan Otomasyon kimlik bilgileri özelliklerini hello. |

## <a name="runbook-activities"></a>Runbook etkinlikleri
Aşağıdaki tablonun hello Hello etkinlikleri bir runbook'un ve DSC yapılandırmaları kullanılan tooaccess kimlik bilgileridir.

| Etkinlikler | Açıklama |
|:--- |:--- |
| Get-AutomationPSCredential |Bir runbook ya da DSC yapılandırması bir kimlik bilgisi toouse alır. Döndürür bir [System.Management.Automation.PSCredential](http://msdn.microsoft.com/library/system.management.automation.pscredential) nesnesi. |

> [!NOTE]
> Değişkenleri yapmaktan kaçınmalısınız hello – Get-AutomationPSCredential bu runbook'lar ya da DSC yapılandırmaları arasındaki bağımlılıkları karmaşık hale ve kimlik bilgisi varlıkları tasarım zamanında beri parametresinin adı.
> 
> 

## <a name="creating-a-new-credential-asset"></a>Yeni bir kimlik bilgisi varlığı oluşturma

### <a name="toocreate-a-new-credential-asset-with-hello-azure-portal"></a>toocreate hello Azure portalı ile yeni bir kimlik bilgisi varlığı
1. Otomasyon hesabınızdan hello tıklatın **varlıklar** bölümü tooopen hello **varlıklar** dikey.
2. Merhaba tıklatın **kimlik bilgileri** bölümü tooopen hello **kimlik bilgileri** dikey.
3. Tıklatın **bir kimlik bilgisi Ekle** hello dikey penceresinde hello üstünde.
4. Merhaba form tamamlamak ve ' **oluşturma** toosave hello yeni kimlik bilgisi.

### <a name="toocreate-a-new-credential-asset-with-windows-powershell"></a>toocreate Windows PowerShell ile yeni bir kimlik bilgisi varlığı
Merhaba aşağıdaki örnek komutlar nasıl toocreate yeni bir Otomasyon kimlik bilgisi göstermektedir. Bir PSCredential nesnesi ilk hello adı ve parola ile oluşturulur ve toocreate hello kimlik bilgisi varlığı kullanılır. Alternatif olarak, hello kullanabileceğinizi **Get-Credential** cmdlet toobe tootype adı ve parola istenir.

    $user = "MyDomain\MyUser"
    $pw = ConvertTo-SecureString "PassWord!" -AsPlainText -Force
    $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $user, $pw
    New-AzureAutomationCredential -AutomationAccountName "MyAutomationAccount" -Name "MyCredential" -Value $cred

### <a name="toocreate-a-new-credential-asset-with-hello-azure-classic-portal"></a>toocreate hello Klasik Azure portalı ile yeni bir kimlik bilgisi varlığı
1. Otomasyon hesabınızdan tıklatın **varlıklar** hello penceresinin hello üstünde.
2. Merhaba penceresinin Hello altında tıklatın **ayar Ekle**.
3. Tıklatın **kimlik bilgisi Ekle**.
4. Merhaba, **kimlik bilgisi türü** açılan listesinde, select **PowerShell kimlik bilgisi**.
5. Merhaba sihirbazını tamamlayın ve hello onay kutusunu toosave hello yeni kimlik bilgisi'ı tıklatın.

## <a name="using-a-powershell-credential"></a>PowerShell kimlik bilgisi kullanma
Bir runbook ya da hello DSC yapılandırması bir kimlik bilgisi varlığı almak **Get-AutomationPSCredential** etkinlik. Bu döndürür bir [PSCredential nesnesinin](http://msdn.microsoft.com/library/system.management.automation.pscredential.aspx) bir etkinlik veya PSCredential parametresi gerektiriyor cmdlet'ini kullanabilirsiniz. Merhaba kimlik bilgisi nesnesi toouse hello özelliklerini tek tek de alabilirsiniz. Merhaba nesne hello kullanıcı adı ve hello güvenli parola özelliğine veya hello kullanabilirsiniz **GetNetworkCredential** yöntemi tooreturn bir [NetworkCredential](http://msdn.microsoft.com/library/system.net.networkcredential.aspx) bir güvenli sağlayacak nesnesi Merhaba parola sürümü.

### <a name="textual-runbook-sample"></a>Metin biçiminde runbook örneği
Merhaba aşağıdaki örnek komutlar bir PowerShell toouse bir runbook'ta nasıl kimlik bilgisi göstermektedir. Bu örnekte, hello kimlik bilgisi alınır ve kendi kullanıcı adı ve parola toovariables atanmış.

    $myCredential = Get-AutomationPSCredential -Name 'MyCredential'
    $userName = $myCredential.UserName
    $securePassword = $myCredential.Password
    $password = $myCredential.GetNetworkCredential().Password


### <a name="graphical-runbook-sample"></a>Grafik runbook örneği
Eklediğiniz bir **Get-AutomationPSCredential** etkinlik tooa grafik runbook sağ tıklayarak hello grafik Düzenleyicisi ve seçerek hello Kitaplık bölmesinde hello kimlik bilgisi **toocanvas eklemek**.

![Kimlik bilgisi toocanvas Ekle](media/automation-credentials/credential-add-canvas.png)

Merhaba aşağıdaki resimde bir grafik runbook'ta kimlik bilgilerini kullanarak bir örnek gösterilmektedir.  Bu durumda, bu runbook tooAzure kaynaklar için kullanılan tooprovide kimlik doğrulaması açıklandığı gibi yüklenmekte olan [Azure AD kullanıcı hesabı kimlik doğrulaması Runbook'larla](automation-create-aduser-account.md).  Merhaba ilk etkinlik erişim toohello Azure aboneliğine sahip hello kimlik bilgisi alır.  Merhaba **Add-AzureAccount** etkinlik sonra bu kimlik bilgisi tooprovide kimlik doğrulaması için kullanır bundan sonra gelen tüm etkinlikler.  A [ardışık düzen bağlantısına](automation-graphical-authoring-intro.md#links-and-workflow) bu yana işte **Get-AutomationPSCredential** tek bir nesne bekleniyor.  

![Kimlik bilgisi toocanvas Ekle](media/automation-credentials/get-credential.png)

## <a name="using-a-powershell-credential-in-dsc"></a>DSC içinde bir PowerShell kimlik bilgisi kullanma
Azure Otomasyonu DSC yapılandırmalarında kullanarak kimlik bilgisi varlıkları başvurabilir sırada **Get-AutomationPSCredential**, kimlik bilgisi varlıkları de geçirilebilir içinde parametreleri aracılığıyla isterseniz. Daha fazla bilgi için bkz: [Azure Otomasyonu DSC yapılandırmalarında derleme](automation-dsc-compile.md#credential-assets).

## <a name="next-steps"></a>Sonraki Adımlar
* toolearn grafik yazma içinde daha bağlantıları hakkında bkz [grafik yazma içindeki bağlantılar](automation-graphical-authoring-intro.md#links-and-workflow)
* Otomasyon, toounderstand hello farklı kimlik doğrulama yöntemlerini bkz [Azure Automation güvenliği](automation-security-overview.md)
* Grafik runbook'ları ile çalışmaya tooget bakın [ilk grafik runbook Uygulamam](automation-first-runbook-graphical.md)
* PowerShell iş akışı runbook'ları ile başlatılan tooget bakın [ilk PowerShell iş akışı runbook Uygulamam](automation-first-runbook-textual.md) 

