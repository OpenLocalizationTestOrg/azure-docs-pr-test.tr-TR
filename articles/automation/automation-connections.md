---
title: "Azure Otomasyonu aaaConnection varlıkları | Microsoft Docs"
description: "Azure Automation bağlantı varlıkları hello gerekli bilgileri tooconnect tooan dış hizmet veya uygulama bir runbook veya DSC yapılandırması içerir. Bu makale, bağlantıları hello ayrıntılarını açıklar ve nasıl metinsel ve grafik yazma içinde toowork onlarla."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: f0239017-5c66-4165-8cca-5dcb249b8091
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/13/2017
ms.author: magoedte; bwren
ms.openlocfilehash: f0f6b9fb960789b34af7b60eb1069313fdcf071c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connection-assets-in-azure-automation"></a>Azure Automation bağlantı varlıkları

Bir Otomasyon bağlantı varlığı hello gerekli bilgileri tooconnect tooan dış hizmet veya uygulama bir runbook veya DSC yapılandırması içerir. Bu, bir kullanıcı adı ve URL veya bir bağlantı noktası gibi ek tooconnection bilgi parola gibi kimlik doğrulaması için gereken bilgiler içerebilir. bir bağlantı Hello değerini tooa belirli uygulamada bir varlık karşılıklı toocreating olarak bağlamak için hello özelliklerin tümünü birden fazla değişken engelliyor. Hello kullanıcı bağlantı tek bir yerde hello değerleri düzenleyebilirsiniz ve bağlantı tooa runbook veya DSC yapılandırması hello adı tek bir parametre geçirebilirsiniz. bir bağlantı hello runbook veya hello DSC yapılandırması erişilebilen için özellikler Hello **Get-AutomationConnection** etkinlik.

Bir bağlantı oluşturduğunuzda belirtmelisiniz bir *bağlantı türü*. Merhaba bağlantı türü bir özellikler kümesi tanımlayan bir şablondur. Merhaba bağlantı, bağlantı türü tanımlanmış her bir özellik için değerleri tanımlar. Bağlantı türleri tümleştirme modüllerinde eklenen tooAzure Otomasyon olan veya hello ile oluşturulan [Azure Otomasyon API](http://msdn.microsoft.com/library/azure/mt163818.aspx) hello tümleştirme modülü bir bağlantı türü içeriyorsa ve Otomasyon hesabınızda içeri aktarıldı. Aksi takdirde, toocreate bir meta veri dosyası toospecify bir Otomasyon bağlantı türü gerekir.  Bu ilgili daha fazla bilgi için bkz: [tümleştirme modülleri](automation-integration-modules.md).  

>[!NOTE] 
>Azure Automation güvenli varlıkların kimlik bilgileri, sertifikalar, bağlantıları ve şifrelenmiş değişkenler içerir. Bu varlıklar şifrelenir ve hello Azure her Otomasyon hesabı için oluşturulan benzersiz bir anahtar kullanarak otomasyon depolanır. Bu anahtarı bir sertifika tarafından şifrelenir ve Azure Otomasyonu'nda depolanır. Güvenli bir varlık depolamak önce hello Otomasyon hesabının hello anahtarı hello ana sertifikayı kullanarak şifresi çözülür ve tooencrypt hello varlık kullanılır.

## <a name="windows-powershell-cmdlets"></a>Windows PowerShell cmdlet'leri

Aşağıdaki tablonun hello Hello cmdlet'leri kullanılan toocreate olan Otomasyon bağlantıları ve Windows PowerShell ile yönetin. Merhaba bir parçası olarak sevk [Azure PowerShell Modülü](/powershell/azure/overview) olduğu Automation runbook'ları ve DSC yapılandırmaları için kullanılabilir.

|Cmdlet|Açıklama|
|:---|:---|
|[Get-AzureRmAutomationConnection](/powershell/module/azurerm.automation/get-azurermautomationconnection)|Bir bağlantı alır. Merhaba bağlantının alanlarının hello değerlerle karma tablosu da içerir.|
|[AzureRmAutomationConnection yeni](/powershell/module/azurerm.automation/new-azurermautomationconnection)|Yeni bir bağlantı oluşturur.|
|[Remove-AzureRmAutomationConnection](/powershell/module/azurerm.automation/remove-azurermautomationconnection)|Varolan bir bağlantıyı kaldırın.|
|[Set-AzureRmAutomationConnectionFieldValue](/powershell/module/azurerm.automation/set-azurermautomationconnectionfieldvalue)|Merhaba mevcut bir bağlantı için belirli bir alanın değerini ayarlar.|

## <a name="activities"></a>Etkinlikler

Aşağıdaki tablonun hello Hello etkinlikleri, runbook veya DSC yapılandırması kullanılan tooaccess bağlantılardır.

|Etkinlikler|Açıklama|
|---|---|
|[Get-AutomationConnection](/powershell/module/azure/get-azureautomationconnection?view=azuresmps-3.7.0)|Bir bağlantı toouse alır. Merhaba hello bağlantı özelliklerini içeren bir karma tablo döndürür.|

>[!NOTE] 
>Değişkenlerle yapmaktan kaçınmalısınız hello – Name parametresinde **Get - AutomationConnection** bu runbook'ları veya DSC yapılandırmaları ve bağlantı varlıkları arasındaki bağımlılıkları tasarım zamanında getirebileceğinden.

## <a name="creating-a-new-connection"></a>Yeni bir bağlantı oluşturma

### <a name="toocreate-a-new-connection-with-hello-azure-portal"></a>toocreate hello Azure portalı ile yeni bir bağlantı

1. Otomasyon hesabınızdan hello tıklatın **varlıklar** bölümü tooopen hello **varlıklar** dikey.
2. Merhaba tıklatın **bağlantıları** bölümü tooopen hello **bağlantıları** dikey.
3. Tıklatın **Bağlantı Ekle** hello dikey penceresinde hello üstünde.
4. Merhaba, **türü** açılan listesinde, select hello türü toocreate istediğiniz bağlantı. Merhaba form bu türdeki hello özelliklerini sunacaktır.
5. Merhaba form tamamlamak ve ' **oluşturma** toosave hello yeni bağlantı.

### <a name="toocreate-a-new-connection-with-hello-azure-classic-portal"></a>toocreate hello Klasik Azure portalı ile yeni bir bağlantı

1. Otomasyon hesabınızdan tıklatın **varlıklar** hello penceresinin hello üstünde.
2. Merhaba penceresinin Hello altında tıklatın **ayar Ekle**.
3. Tıklatın **Bağlantı Ekle**.
4. Merhaba, **bağlantı türü** açılan listesinde, select hello türü toocreate istediğiniz bağlantı.  Başlangıç Sihirbazı'nı bu türdeki hello özelliklerini sunacaktır.
5. Merhaba sihirbazını tamamlayın ve hello onay kutusunu toosave hello yeni bağlantısına tıklayın.

### <a name="toocreate-a-new-connection-with-windows-powershell"></a>Windows PowerShell ile yeni bir bağlantı toocreate

Windows hello kullanarak PowerShell ile yeni bir bağlantı oluşturmak [yeni AzureRmAutomationConnection](/powershell/module/azurerm.automation/new-azurermautomationconnection) cmdlet'i. Bu cmdlet adlı bir parametre içeriyor **ConnectionFieldValues** , bekliyor bir [karma tablosu](http://technet.microsoft.com/library/hh847780.aspx) hello bağlantı türü tarafından tanımlanan hello özelliklerin her biri için değerleri tanımlama.

Otomasyon hello ile biliyorsanız [farklı çalıştır hesabı](automation-sec-configure-azure-runas-account.md) hello hizmet sorumlusunu kullanarak tooauthenticate runbook'ları hello alternatif toocreating hello hello hello portalı, farklı çalıştır hesabı olarak sağlanan PowerShell Betiği Aşağıdaki örnek komutlar hello kullanarak yeni bir bağlantı varlığı oluşturur.  

    $ConnectionAssetName = "AzureRunAsConnection"
    $ConnectionFieldValues = @{"ApplicationId" = $Application.ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Cert.Thumbprint; "SubscriptionId" = $SubscriptionId}
    New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $AutomationAccountName -Name $ConnectionAssetName -ConnectionTypeName AzureServicePrincipal -ConnectionFieldValues $ConnectionFieldValues 

Otomasyon hesabınızı oluşturduğunuzda, çünkü otomatik olarak çeşitli genel modüller hello bağlantı türü ile birlikte varsayılan içerir mümkün toouse hello betik toocreate hello bağlantı varlığı olan **AzurServicePrincipal**toocreate hello **AzureRunAsConnection** bağlantı varlığı.  Farklı kimlik doğrulama yöntemiyle toocreate yeni bir bağlantı varlık tooconnect tooa hizmet veya uygulama çalışırsanız hello bağlantısı türü zaten Otomasyon hesabınızda tanımlı olmadığı için başarısız olur, aklınızda önemli tookeep olmasıdır.  Nasıl toocreate kendi bağlantı türü, özel veya hello modülünden hakkında daha fazla bilgi için [PowerShell Galerisi](https://www.powershellgallery.com), bkz: [tümleştirme modülleri](automation-integration-modules.md)
  
## <a name="using-a-connection-in-a-runbook-or-dsc-configuration"></a>Bir runbook ya da DSC yapılandırması bir bağlantı kullanarak

Bir runbook ya da DSC yapılandırması hello ile bir bağlantı alma **Get-AutomationConnection** cmdlet'i.  Merhaba kullanamazsınız [Get-AzureRmAutomationConnection](https://docs.microsoft.com/powershell/resourcemanager/azurerm.automation/v1.0.12/Get-AzureRmAutomationConnection?redirectedfrom=msdn) etkinlik.  Bu etkinlik hello bağlantı hello farklı alanların hello değerlerini alır ve bunları döndürür bir [karma tablosu](http://go.microsoft.com/fwlink/?LinkID=324844) sonra kullanılabilecek hello runbook ya da DSC yapılandırması hello uygun komutlarla.

### <a name="textual-runbook-sample"></a>Metin biçiminde runbook örneği

Merhaba aşağıdaki örnek komutlar nasıl toouse hello farklı çalıştır hesabı tooauthenticate runbook'unuzda Azure Resource Manager kaynaklarıyla daha önce belirtildiği göstermektedir.  Merhaba bağlantı kullanır hello sertifika tabanlı hizmet sorumlusu başvuruda bulunan, hello farklı çalıştır hesabını temsil eden varlık olmayan kimlik bilgileri.  

    $Conn = Get-AutomationConnection -Name AzureRunAsConnection 
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint 

### <a name="graphical-runbook-samples"></a>Grafik runbook örnekleri

Eklediğiniz bir **Get-AutomationConnection** etkinlik tooa grafik runbook hello bağlantıda hello grafik Düzenleyicisi ve seçim hello Kitaplık bölmesinde sağ tıklanarak **toocanvas eklemek**.

![](media/automation-connections/connection-add-canvas.png)

Merhaba aşağıdaki resimde grafik bir runbook'ta bağlantı kullanma örneği gösterilmektedir.  Merhaba budur metin biçiminde runbook ile Merhaba farklı çalıştır hesabını kullanarak kimlik doğrulaması için yukarıda gösterilen aynı örneği.  Bu örnek hello kullanır **sabit değer** hello için veri kümesi **farklı çalıştır bağlantısını Al** aktivitesi kimlik doğrulaması için bir bağlantı nesnesi kullanır.  A [ardışık düzen bağlantısına](automation-graphical-authoring-intro.md#links-and-workflow) hello ServicePrincipalCertificate parametre kümesi tek bir nesne bekleniyor beri burada kullanılır.

![](media/automation-connections/automation-get-connection-object.png)

## <a name="next-steps"></a>Sonraki adımlar

- Gözden geçirme [grafik yazma içinde bağlantılar](automation-graphical-authoring-intro.md#links-and-workflow) toodirect ve denetim hello nasıl gerçekleştiğini mantığı runbook'larınızdaki toounderstand.  

- Azure Automation tümleştirme modülü olarak kendi PowerShell modülleri toowork oluşturmak için daha fazla Azure Otomasyonu'nun PowerShell modülleri ve kullanımını en iyi uygulamalar hakkında toolearn bkz [tümleştirme modülleri](automation-integration-modules.md).  
