---
title: "Azure Automation bağlantı varlıkları | Microsoft Docs"
description: "Bağlantı varlıkları Azure Automation runbook ya da DSC yapılandırması bir dış hizmet veya uygulamaya bağlanmak için gereken bilgileri içerir. Bu makalede, bağlantıları ve bunlarla metinsel ve grafik yazma çalışma konusunda ayrıntılar açıklanmaktadır."
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
ms.openlocfilehash: 3cf85651332c85ddf7ef26c21619b5e3a0b89b79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="connection-assets-in-azure-automation"></a>Azure Automation bağlantı varlıkları

Bir Otomasyon bağlantı varlığı runbook ya da DSC yapılandırması bir dış hizmet veya uygulamaya bağlanmak için gereken bilgileri içerir. Bu, bir kullanıcı adı ve bağlantı bilgilerini bir URL veya bir bağlantı noktası gibi ek olarak parola gibi kimlik doğrulaması için gereken bilgiler içerebilir. Bağlantı değerini birden fazla değişken oluşturma aksine bir varlık içindeki belirli bir uygulamaya bağlanmak için özelliklerin tümünü engelliyor. Bir bağlantının adını runbook veya DSC yapılandırması tek bir parametre olarak geçirebilir ve kullanıcı tek bir yerde bir bağlantı için değerleri düzenleyebilirsiniz. Bağlantı için özellikler, runbook veya DSC yapılandırması ile erişilebilen **Get-AutomationConnection** etkinlik.

Bir bağlantı oluşturduğunuzda belirtmelisiniz bir *bağlantı türü*. Bağlantı türü bir özellikler kümesi tanımlayan bir şablondur. Bağlantı, bağlantı türü tanımlanmış her bir özellik için değerleri tanımlar. Bağlantı türleri için Azure Automation tümleştirme modülleri eklenir veya ile oluşturulan [Azure Otomasyon API](http://msdn.microsoft.com/library/azure/mt163818.aspx) tümleştirme modülü bir bağlantı türü içeriyorsa ve Otomasyon hesabınızda içeri aktarıldı. Aksi halde, bir Otomasyon bağlantı türünü belirtmek için bir meta veri dosyası oluşturmanız gerekir.  Bu ilgili daha fazla bilgi için bkz: [tümleştirme modülleri](automation-integration-modules.md).  

>[!NOTE] 
>Azure Automation güvenli varlıkların kimlik bilgileri, sertifikalar, bağlantıları ve şifrelenmiş değişkenler içerir. Bu varlıklar şifrelenir ve her Otomasyon hesabı için oluşturulan benzersiz bir anahtar kullanarak Azure Automation depolanır. Bu anahtarı bir sertifika tarafından şifrelenir ve Azure Otomasyonu'nda depolanır. Güvenli bir varlık depolamak önce anahtar Otomasyon hesabı için sertifika aracılığıyla çözülür ve varlık şifrelemek için kullanılan.

## <a name="windows-powershell-cmdlets"></a>Windows PowerShell cmdlet'leri

Aşağıdaki tabloda yer alan cmdlet'ler Windows PowerShell ile Automation bağlantıları oluşturma ve yönetme için kullanılır. Bir parçası olarak sevk [Azure PowerShell Modülü](/powershell/azure/overview) olduğu Automation runbook'ları ve DSC yapılandırmaları için kullanılabilir.

|Cmdlet|Açıklama|
|:---|:---|
|[Get-AzureRmAutomationConnection](/powershell/module/azurerm.automation/get-azurermautomationconnection)|Bir bağlantı alır. Bağlantının alanların değerlerini içeren bir karma tablosu da içerir.|
|[AzureRmAutomationConnection yeni](/powershell/module/azurerm.automation/new-azurermautomationconnection)|Yeni bir bağlantı oluşturur.|
|[Remove-AzureRmAutomationConnection](/powershell/module/azurerm.automation/remove-azurermautomationconnection)|Varolan bir bağlantıyı kaldırın.|
|[Set-AzureRmAutomationConnectionFieldValue](/powershell/module/azurerm.automation/set-azurermautomationconnectionfieldvalue)|Mevcut bir bağlantı için belirli bir alanın değerini ayarlar.|

## <a name="activities"></a>Etkinlikler

Aşağıdaki tablodaki etkinlikler bir runbook ya da DSC yapılandırması bağlantıları erişmek için kullanılır.

|Etkinlikler|Açıklama|
|---|---|
|[Get-AutomationConnection](/powershell/module/azure/get-azureautomationconnection?view=azuresmps-3.7.0)|Kullanmak için bir bağlantı alır. Bağlantının özelliklerini içeren bir karma tablo döndürür.|

>[!NOTE] 
>Yapmaktan kaçınmalısınız Name parametresinde ile **Get - AutomationConnection** bu runbook'ları veya DSC yapılandırmaları ve bağlantı varlıkları arasındaki bağımlılıkları tasarım zamanında getirebileceğinden.

## <a name="creating-a-new-connection"></a>Yeni bir bağlantı oluşturma

### <a name="to-create-a-new-connection-with-the-azure-portal"></a>Azure portalı ile yeni bir bağlantı oluşturmak için

1. Otomasyon hesabınızdan tıklatın **varlıklar** açmak için bölümü **varlıklar** dikey.
2. Tıklatın **bağlantıları** açmak için bölümü **bağlantıları** dikey.
3. Tıklatın **Bağlantı Ekle** dikey pencerenin üstündeki.
4. İçinde **türü** açılan listesinde, oluşturmak istediğiniz bağlantı türünü seçin. Form belirli türü için özellikler sunacaktır.
5. Formu tamamlayıp tıklatın **oluşturma** yeni bağlantı kaydetmek için.

### <a name="to-create-a-new-connection-with-the-azure-classic-portal"></a>Azure Klasik portalı ile yeni bir bağlantı oluşturmak için

1. Otomasyon hesabınızdan tıklatın **varlıklar** pencerenin üstündeki.
2. Pencerenin alt kısmındaki tıklatın **ayar Ekle**.
3. Tıklatın **Bağlantı Ekle**.
4. İçinde **bağlantı türü** açılan listesinde, oluşturmak istediğiniz bağlantı türünü seçin.  Sihirbazın bu türdeki özelliklerini sunacaktır.
5. Sihirbazı tamamlamak ve yeni bağlantıyı kaydetmek için onay kutusunu işaretleyin.

### <a name="to-create-a-new-connection-with-windows-powershell"></a>Windows PowerShell ile yeni bir bağlantı oluşturmak için

Windows PowerShell ile yeni bir bağlantı oluşturmak [yeni AzureRmAutomationConnection](/powershell/module/azurerm.automation/new-azurermautomationconnection) cmdlet'i. Bu cmdlet adlı bir parametre içeriyor **ConnectionFieldValues** , bekliyor bir [karma tablosu](http://technet.microsoft.com/library/hh847780.aspx) bağlantı türü tarafından tanımlanan özelliklerin her biri için değerleri tanımlama.

Otomasyon ile biliyorsanız [farklı çalıştır hesabı](automation-sec-configure-azure-runas-account.md) runbook'ları oluşturma alternatif olarak sağlanan hizmet sorumlusu, PowerShell Betiği kullanılarak kimlik doğrulaması için farklı çalıştır hesap portalı, yeni bir oluşturur Aşağıdaki örnek komutlar kullanarak bağlantı varlığı.  

    $ConnectionAssetName = "AzureRunAsConnection"
    $ConnectionFieldValues = @{"ApplicationId" = $Application.ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Cert.Thumbprint; "SubscriptionId" = $SubscriptionId}
    New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $AutomationAccountName -Name $ConnectionAssetName -ConnectionTypeName AzureServicePrincipal -ConnectionFieldValues $ConnectionFieldValues 

Otomasyon hesabınızı oluşturduğunuzda, çünkü otomatik olarak çeşitli genel modüller bağlantı türü ile birlikte varsayılan içerir bağlantı varlığı oluşturmak için komut dosyası kullanabilmek için **AzurServicePrincipal** için oluşturma **AzureRunAsConnection** bağlantı varlığı.  Farklı kimlik doğrulama yöntemiyle bir hizmet veya uygulamaya bağlanmak için yeni bir bağlantı varlığı oluşturmayı denerseniz, bağlantı türü zaten Otomasyon hesabınızda tanımlanmadığı da başarısız olacağı için bunu göz önünde bulundurmanız önemlidir.  Özel veya modülünden için kendi bağlantı türünün nasıl oluşturulacağı konusunda daha fazla bilgi [PowerShell Galerisi](https://www.powershellgallery.com), bkz: [tümleştirme modülleri](automation-integration-modules.md)
  
## <a name="using-a-connection-in-a-runbook-or-dsc-configuration"></a>Bir runbook ya da DSC yapılandırması bir bağlantı kullanarak

Bir runbook ya da DSC yapılandırması ile bir bağlantı alma **Get-AutomationConnection** cmdlet'i.  Kullanamazsınız [Get-AzureRmAutomationConnection](https://docs.microsoft.com/powershell/resourcemanager/azurerm.automation/v1.0.12/Get-AzureRmAutomationConnection?redirectedfrom=msdn) etkinlik.  Bu etkinlik bağlantıdaki farklı alanların değerlerini alır ve bunları olarak döndüren bir [karma tablosu](http://go.microsoft.com/fwlink/?LinkID=324844) sonra kullanılabilir runbook ya da DSC yapılandırması uygun komutlarla.

### <a name="textual-runbook-sample"></a>Metin biçiminde runbook örneği

Aşağıdaki örnek komutlar runbook'unuzda Azure Resource Manager kaynaklarıyla kimlik doğrulaması yapmak için daha önce belirtildiği farklı çalıştır hesabının nasıl kullanılacağı gösterilmektedir.  Bağlantı varlığı temsil eden kimlik bilgilerini değil, sertifika tabanlı hizmet sorumlusu başvuruda bulunan farklı çalıştır hesabını kullanır.  

    $Conn = Get-AutomationConnection -Name AzureRunAsConnection 
    Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint 

### <a name="graphical-runbook-samples"></a>Grafik runbook örnekleri

Eklediğiniz bir **Get-AutomationConnection** grafik Düzenleyicisi Kitaplık bölmesinde bağlantısı sağ tıklatıp seçerek bir grafik runbook etkinliği **tuvale Ekle**.

![](media/automation-connections/connection-add-canvas.png)

Aşağıdaki resimde, grafik bir runbook'ta bağlantı kullanma örneği gösterilmektedir.  Bu, metin biçiminde runbook ile farklı çalıştır hesabını kullanarak kimlik doğrulaması için yukarıda gösterilen aynı örnektir.  Bu örnekte **sabit değer** veri kümesi için **farklı çalıştır bağlantısını Al** aktivitesi kimlik doğrulaması için bir bağlantı nesnesi kullanır.  A [ardışık düzen bağlantısına](automation-graphical-authoring-intro.md#links-and-workflow) ServicePrincipalCertificate parametre kümesi tek bir nesne bekleniyor beri burada kullanılır.

![](media/automation-connections/automation-get-connection-object.png)

## <a name="next-steps"></a>Sonraki adımlar

- Gözden geçirme [grafik yazma içinde bağlantılar](automation-graphical-authoring-intro.md#links-and-workflow) yönlendirmek ve runbook'larınızın mantığında akışını denetlemek nasıl anlamak için.  

- Azure Automation tümleştirme modülü olarak çalışmak için kendi PowerShell modüllerinizi oluşturmak için Azure Otomasyonu'nun PowerShell modülleri ve kullanımını en iyi uygulamalar hakkında daha fazla bilgi için bkz: [tümleştirme modülleri](automation-integration-modules.md).  
