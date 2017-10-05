---
title: "Azure Resource Manager tabanlı PowerShell komutları için Azure Web uygulaması | Microsoft Docs"
description: "Yeni Azure Resource Manager tabanlı PowerShell komutlarının Azure Web uygulamaları yönetmek için nasıl kullanılacağını öğrenin."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: 4231fbba-61e5-4f92-b958-531c066fb87f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/29/2016
ms.author: aelnably
ms.openlocfilehash: 8d574f051a327ba0409e6f25a5886af673d3d5e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-based-powershell-to-manage-azure-web-apps"></a>Azure Web uygulamaları yönetmek için Azure Resource Manager tabanlı PowerShell kullanma
> [!div class="op_single_selector"]
> * [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [Azure PowerShell](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

Microsoft Azure PowerShell sürümü 1.0.0 yeni komutları eklenmiştir, kullanıcı Web uygulamaları yönetmek için Azure Resource Manager tabanlı PowerShell komutlarını kullanma olanağı verir.

Kaynak gruplarını yönetme hakkında bilgi edinmek için [Azure PowerShell kullanarak Azure Resource Manager ile](../powershell-azure-resource-manager.md). 

Parametreleri ve seçenekleri PowerShell cmdlet'lerinin tam listesi hakkında bilgi edinmek için [Cmdlet başvurusu, Web uygulamasını Azure Resource Manager tabanlı PowerShell cmdlet'lerinin tam](https://msdn.microsoft.com/library/mt619237.aspx)

## <a name="managing-app-service-plans"></a>Uygulama hizmeti yönetme planları
### <a name="create-an-app-service-plan"></a>Bir uygulama hizmeti planı oluştur
Bir uygulama hizmeti planı oluşturmak için kullanın **yeni AzureRmAppServicePlan** cmdlet'i.

Farklı Parametreler açıklamalarını şunlardır:

* **Ad**: uygulama hizmeti planının adı.
* **Konum**: hizmet planı konumu.
* **ResourceGroupName**: yeni oluşturulan uygulama hizmeti planı içeren kaynak grubu.
* **Katman**: İstenen fiyatlandırma Katmanı (varsayılan serbest, paylaşılan, temel, standart ve Premium diğer seçeneklerdir.)
* **WorkerSize**: (varsayılan temel, standart veya Premium katmanı parametresi belirtildiyse, küçük. çalışan boyutu Diğer Orta ve büyük seçenekleridir.)
* **NumberofWorkers**: uygulamasında çalışan sayısı hizmet planı (varsayılan değer 1'dir). 

Bu cmdlet kullanılarak örnek:

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a>Bir uygulama hizmeti ortamı'nda bir uygulama hizmeti planı oluştur
Uygulama hizmeti ortamı'nda bir uygulama hizmeti planı oluşturmak için aynı komutunu **yeni AzureRmAppServicePlan** komutu ek parametre ana'nın adını ve ana'nın kaynak grubu adı belirtin.

Bu cmdlet kullanılarak örnek:

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

Uygulama hizmeti ortamı hakkında daha fazla bilgi edinmek için [uygulama hizmeti ortamı giriş](app-service-app-service-environment-intro.md)

### <a name="list-existing-app-service-plans"></a>Var olan uygulama hizmeti planları listesi
Var olan uygulama hizmeti planları listelemek için kullanın **Get-AzureRmAppServicePlan** cmdlet'i.

Aboneliğinizdeki tüm uygulama hizmeti planları listelemek için kullanın: 

    Get-AzureRmAppServicePlan

Belirli kaynak grubundaki tüm uygulama hizmeti planları listelemek için kullanın:

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

Belirli uygulama hizmeti planı almak için kullanın:

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a>Var olan bir App Service planı Yapılandır
Var olan bir uygulama hizmeti planı ayarları değiştirmek için kullanın **kümesi AzureRmAppServicePlan** cmdlet'i. Katmanı, çalışan boyutu ve çalışanların sayısını değiştirebilirsiniz 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a>Bir uygulama hizmeti planı ölçeklendirme
Var olan bir uygulama hizmeti planı ölçeklendirmek için kullanın:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-the-worker-size-of-an-app-service-plan"></a>Bir uygulama hizmeti planı çalışan boyutunu değiştirme
Var olan bir uygulama hizmeti planında çalışanları boyutunu değiştirmek için kullanın:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-the-tier-of-an-app-service-plan"></a>Bir uygulama hizmeti planı katmanını değiştirme
Var olan bir uygulama hizmeti planı katmanını değiştirmek için kullanın:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a>Var olan bir uygulama hizmeti planı silme
Var olan bir uygulama hizmeti planı silmek için tüm atanmış web uygulamaları taşınmış veya silinmiş ilk gerekir. Ardından kullanarak **Kaldır AzureRmAppServicePlan** cmdlet uygulama hizmeti planı silebilirsiniz.

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a>App Service Web uygulamaları yönetme
### <a name="create-a-web-app"></a>Web Uygulaması oluşturma
Bir web uygulaması oluşturmak için kullanın **yeni AzureRmWebApp** cmdlet'i.

Farklı Parametreler açıklamalarını şunlardır:

* **Ad**: web uygulamasının adı.
* **AppServicePlan**: web uygulamasını barındırmak için kullanılan hizmeti planının adı.
* **ResourceGroupName**: uygulama hizmeti planı barındıran kaynak grubu.
* **Konum**: web uygulaması konumu.

Bu cmdlet kullanılarak örnek:

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a>Bir uygulama hizmeti ortamı'nda bir Web uygulaması oluşturma
Uygulama hizmeti ortamı (ASE'de) bir web uygulaması oluşturmak için. Aynı **yeni AzureRmWebApp** ana adının ve kaynak grubu adı, ana belirtmek için ek parametreler komutuyla ait.

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

Uygulama hizmeti ortamı hakkında daha fazla bilgi edinmek için [uygulama hizmeti ortamı giriş](app-service-app-service-environment-intro.md)

### <a name="delete-an-existing-web-app"></a>Var olan bir Web uygulamasının Sil
Kullanabileceğiniz mevcut bir web uygulamasını silmek için **Kaldır AzureRmWebApp** cmdlet, web uygulamasının adını ve kaynak grubu adı belirtmeniz gerekir.

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a>Var olan Web Apps listesi
Mevcut web uygulamaları listelemek için kullanmak **Get-AzureRmWebApp** cmdlet'i.

Aboneliğinizdeki tüm web uygulamaları listelemek için kullanın:

    Get-AzureRmWebApp

Belirli bir kaynak grubunun altındaki tüm web uygulamaları listelemek için kullanın:

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

Belirli web uygulamasını almak için kullanın:

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a>Var olan bir Web uygulamasını yapılandırma
Var olan bir web uygulaması için yapılandırmaları ve ayarları değiştirmek için kullanın **kümesi AzureRmWebApp** cmdlet'i. Parametrelerin tam bir listesi için denetleme [Cmdlet başvuru bağlantısı](https://msdn.microsoft.com/library/mt652487.aspx)

(1) örnek: bağlantı dizelerini değiştirmek için bu cmdlet'i kullanın.

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

(2) örnek: ekleme veya uygulama ayarlarını değiştirme

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


(3) örnek: 64-bit modunda çalıştırmak için web uygulaması ayarlayın

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-the-state-of-an-existing-web-app"></a>Var olan bir Web uygulamasının durumunu değiştirme
#### <a name="restart-a-web-app"></a>Bir web uygulaması yeniden
Bir web uygulaması yeniden başlatmak için web uygulamasının adını ve kaynak grubu belirtmeniz gerekir.

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a>Bir web uygulamasını Durdur
Bir web uygulaması durdurmak için web uygulamasının adını ve kaynak grubu belirtmeniz gerekir.

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a>Bir web uygulaması başlatın
Bir web uygulaması başlatmak için web uygulamasının adını ve kaynak grubu belirtmeniz gerekir.

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a>Web uygulaması yayımlama profillerini yönet
Her web uygulaması, uygulamalarınızı yayımlamak için kullanılan bir yayımlama profili varsa, çeşitli işlemleri profilleri yayımlama çalıştırılabilir.

#### <a name="get-publishing-profile"></a>Yayımlama profilini Al
Bir web uygulaması için yayımlama profili almak için kullanın:

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

Bu komut, bir metin dosyasına yayımlama profili iyi çıkış olarak komut satırı için yayımlama profili görüntülemektedir.

#### <a name="reset-publishing-profile"></a>Yayımlama profilini Sıfırla
FTP ve web yayımlama parolası her ikisi de sıfırlamak için web uygulaması için kullanım dağıtın:

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a>Web uygulaması sertifikaları yönetme
Web uygulaması sertifikaları yönetme hakkında bilgi edinmek için [PowerShell kullanarak SSL sertifikalarını bağlama](app-service-web-app-powershell-ssl-binding.md)

### <a name="next-steps"></a>Sonraki Adımlar
* Azure Resource Manager PowerShell desteği hakkında bilgi edinmek için [Azure PowerShell kullanarak Azure Resource Manager ile.](../powershell-azure-resource-manager.md)
* Uygulama hizmeti ortamları hakkında bilgi edinmek için [uygulama hizmeti ortamı giriş.](app-service-app-service-environment-intro.md)
* PowerShell kullanarak uygulama hizmeti SSL sertifikalarını yönetme hakkında bilgi edinmek için [PowerShell kullanarak SSL sertifikalarını bağlama.](app-service-web-app-powershell-ssl-binding.md)
* Azure Web uygulamaları için Azure Resource Manager tabanlı PowerShell cmdlet'lerinin tam listesi hakkında bilgi edinmek için [, Web uygulamaları Azure Resource Manager PowerShell cmdlet'lerinin Azure Cmdlet başvurusu.](https://msdn.microsoft.com/library/mt619237.aspx)
* * Uygulama hizmeti CLI kullanarak yönetme hakkında bilgi edinmek için [Using Azure Resource Manager-Based XPlat CLI Azure Web uygulaması için.](app-service-web-app-azure-resource-manager-xplat-cli.md)

