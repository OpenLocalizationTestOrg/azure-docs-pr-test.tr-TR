---
title: "aaaAzure Resource Manager tabanlı PowerShell komutları için Azure Web uygulaması | Microsoft Docs"
description: "Nasıl toouse hello yeni Azure Resource Manager tabanlı PowerShell komutları toomanage Azure Web Apps hakkında bilgi edinin."
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
ms.openlocfilehash: bbb821e89daa315280436e84e11316217bb644d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-based-powershell-toomanage-azure-web-apps"></a>Azure Resource Manager-based PowerShell tooManage Azure Web uygulamaları kullanma
> [!div class="op_single_selector"]
> * [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md)
> * [Azure PowerShell](app-service-web-app-azure-resource-manager-powershell.md)
> 
> 

Microsoft Azure PowerShell sürümü 1.0.0 yeni komutları eklenmiştir, hello kullanıcı hello özelliği toouse Azure Resource Manager tabanlı PowerShell komutları toomanage Web Apps verin.

Kaynak gruplarını yönetme hakkında toolearn bkz [Azure PowerShell kullanarak Azure Resource Manager ile](../powershell-azure-resource-manager.md). 

toolearn parametreleri hello PowerShell cmdlet'leri için seçenekler ve hello tam listesi hakkında bkz hello [Cmdlet başvurusu, Web uygulamasını Azure Resource Manager tabanlı PowerShell cmdlet'lerinin tam](https://msdn.microsoft.com/library/mt619237.aspx)

## <a name="managing-app-service-plans"></a>Uygulama hizmeti yönetme planları
### <a name="create-an-app-service-plan"></a>Bir uygulama hizmeti planı oluştur
bir uygulama hizmeti planı toocreate hello kullan **yeni AzureRmAppServicePlan** cmdlet'i.

Merhaba farklı parametreler açıklamalarını şunlardır:

* **Ad**: hello uygulama hizmeti planının adı.
* **Konum**: hizmet planı konumu.
* **ResourceGroupName**: yeni oluşturulan hello uygulama hizmeti planı içeren kaynak grubu.
* **Katman**: hello istenen fiyatlandırma Katmanı (varsayılan serbest, paylaşılan, temel, standart ve Premium diğer seçeneklerdir.)
* **WorkerSize**: Merhaba boyutu çalışanı (varsayılan temel, standart veya Premium hello katmanı parametresi belirtildiyse, küçük. Diğer Orta ve büyük seçenekleridir.)
* **NumberofWorkers**: (varsayılan değer 1'dir) hello uygulama hizmeti planında hello çalışan sayısı. 

Örnek toouse Bu cmdlet:

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -Tier Premium -WorkerSize Large -NumberofWorkers 10

### <a name="create-an-app-service-plan-in-an-app-service-environment"></a>Bir uygulama hizmeti ortamı'nda bir uygulama hizmeti planı oluştur
toocreate bir uygulama hizmeti planı uygulama hizmeti ortamı'nda, kullanım hello aynı komut **yeni AzureRmAppServicePlan** ek parametreler toospecify hello ana'nın adı ve ana'nın kaynak grubu adıyla komutu.

Örnek toouse Bu cmdlet:

    New-AzureRmAppServicePlan -Name ContosoAppServicePlan -Location "South Central US" -ResourceGroupName ContosoAzureResourceGroup -AseName constosoASE -AseResourceGroupName contosoASERG -Tier Premium -WorkerSize Large -NumberofWorkers 10

uygulama hizmeti ortamı, denetimi hakkında daha fazla toolearn [giriş tooApp hizmeti ortamı](app-service-app-service-environment-intro.md)

### <a name="list-existing-app-service-plans"></a>Var olan uygulama hizmeti planları listesi
toolist hello var olan uygulama hizmeti planları kullanın **Get-AzureRmAppServicePlan** cmdlet'i.

toolist, aboneliğinizdeki tüm uygulama hizmeti planları kullanın: 

    Get-AzureRmAppServicePlan

toolist belirli kaynak grubundaki tüm uygulama hizmeti planları kullanın:

    Get-AzureRmAppServicePlan -ResourceGroupname ContosoAzureResourceGroup

tooget belirli uygulama hizmeti planı kullanın:

    Get-AzureRmAppServicePlan -Name ContosoAppServicePlan


### <a name="configure-an-existing-app-service-plan"></a>Var olan bir App Service planı Yapılandır
var olan bir uygulama hizmeti planı toochange hello ayarlarını kullan hello **kümesi AzureRmAppServicePlan** cmdlet'i. Merhaba katmanı, çalışan boyutu ve çalışan hello sayısı değiştirebilirsiniz 

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard -WorkerSize Medium -NumberofWorkers 9

#### <a name="scaling-an-app-service-plan"></a>Bir uygulama hizmeti planı ölçeklendirme
tooscale bir var olan uygulama hizmeti planı, kullanın:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -NumberofWorkers 9

#### <a name="changing-hello-worker-size-of-an-app-service-plan"></a>Bir uygulama hizmeti planı Hello çalışan boyutu değiştirme
çalışan bir var olan uygulama hizmeti planında, kullanım toochange hello boyutu:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -WorkerSize Medium

#### <a name="changing-hello-tier-of-an-app-service-plan"></a>Merhaba bir uygulama hizmeti planı katmanını değiştirme
toochange hello katmanına bir var olan uygulama hizmeti planı, kullanın:

    Set-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Tier Standard

### <a name="delete-an-existing-app-service-plan"></a>Var olan bir uygulama hizmeti planı silme
toodelete var olan bir uygulama hizmeti planı, tüm web uygulamaları gerek toobe taşınmış veya silinmiş ilk atanır. Hello kullanarak **Kaldır AzureRmAppServicePlan** cmdlet hello uygulama hizmeti planı silebilirsiniz.

    Remove-AzureRmAppServicePlan -Name ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup

## <a name="managing-app-service-web-apps"></a>App Service Web uygulamaları yönetme
### <a name="create-a-web-app"></a>Web Uygulaması oluşturma
toocreate bir web uygulaması kullanın hello **yeni AzureRmWebApp** cmdlet'i.

Merhaba farklı parametreler açıklamalarını şunlardır:

* **Ad**: hello web uygulamasının adı.
* **AppServicePlan**: hello hizmet planı toohost hello web uygulaması kullanılan ad.
* **ResourceGroupName**: hello uygulama hizmeti planı barındıran kaynak grubu.
* **Konum**: Merhaba web uygulama konumu.

Örnek toouse Bu cmdlet:

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"

### <a name="create-a-web-app-in-an-app-service-environment"></a>Bir uygulama hizmeti ortamı'nda bir Web uygulaması oluşturma
toocreate bir web uygulaması bir uygulama hizmeti ortamı (ana). Kullanım hello aynı **yeni AzureRmWebApp** ek parametreler toospecify hello ana adı hello ana ait hello kaynak grubu adı ile komutu.

    New-AzureRmWebApp -Name ContosoWebApp -AppServicePlan ContosoAppServicePlan -ResourceGroupName ContosoAzureResourceGroup -Location "South Central US"  -ASEName ContosoASEName -ASEResourceGroupName ContosoASEResourceGroupName

uygulama hizmeti ortamı, denetimi hakkında daha fazla toolearn [giriş tooApp hizmeti ortamı](app-service-app-service-environment-intro.md)

### <a name="delete-an-existing-web-app"></a>Var olan bir Web uygulamasının Sil
toodelete hello kullanabileceğiniz var olan bir web uygulamasının **Kaldır AzureRmWebApp** cmdlet'ini toospecify hello hello web uygulaması adını ve hello kaynak grubu adı gerekiyor.

    Remove-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup


### <a name="list-existing-web-apps"></a>Var olan Web Apps listesi
toolist hello varolan web uygulamaları, hello kullanma **Get-AzureRmWebApp** cmdlet'i.

toolist, aboneliğinizdeki tüm web uygulamaları kullanın:

    Get-AzureRmWebApp

toolist belirli kaynak grubundaki tüm web uygulamaları kullanın:

    Get-AzureRmWebApp -ResourceGroupname ContosoAzureResourceGroup

tooget belirli web uygulaması kullanın:

    Get-AzureRmWebApp -Name ContosoWebApp

### <a name="configure-an-existing-web-app"></a>Var olan bir Web uygulamasını yapılandırma
toochange hello ayarları ve var olan bir web uygulaması için yapılandırmaları kullanmak hello **kümesi AzureRmWebApp** cmdlet'i. Parametrelerin tam bir listesi için hello denetleyin [Cmdlet başvuru bağlantısı](https://msdn.microsoft.com/library/mt652487.aspx)

Örnek (1): Bu cmdlet toochange bağlantı dizelerini kullanın

    $connectionstrings = @{ ContosoConn1 = @{ Type = “MySql”; Value = “MySqlConn”}; ContosoConn2 = @{ Type = “SQLAzure”; Value = “SQLAzureConn”} }
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -ConnectionStrings $connectionstrings

(2) örnek: ekleme veya uygulama ayarlarını değiştirme

    $appsettings = @{appsetting1 = "appsetting1value"; appsetting2 = "appsetting2value"}
    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -AppSettings $appsettings


(3) örnek: Merhaba web uygulama toorun 64-bit modunda ayarlayın.

    Set-AzureRmWebApp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -Use32BitWorkerProcess $False

### <a name="change-hello-state-of-an-existing-web-app"></a>Var olan bir Web uygulamasının Hello durumunu değiştir
#### <a name="restart-a-web-app"></a>Bir web uygulaması yeniden
bir web uygulaması toorestart, hello web uygulamasının hello ad ve kaynak grubu belirtmeniz gerekir.

    Restart-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="stop-a-web-app"></a>Bir web uygulamasını Durdur
bir web uygulaması toostop, hello web uygulamasının hello ad ve kaynak grubu belirtmeniz gerekir.

    Stop-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

#### <a name="start-a-web-app"></a>Bir web uygulaması başlatın
bir web uygulaması toostart, hello web uygulamasının hello ad ve kaynak grubu belirtmeniz gerekir.

    Start-AzureRmWebapp -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-publishing-profiles"></a>Web uygulaması yayımlama profillerini yönet
Her web uygulaması kullanılan toopublish olabilir bir yayımlama profili uygulamalarınızı sahip, çeşitli işlemleri profilleri yayımlama çalıştırılabilir.

#### <a name="get-publishing-profile"></a>Yayımlama profilini Al
Yayımlama profilini kullan bir web uygulaması için tooget hello:

    Get-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup -OutputFile .\publishingprofile.txt

Bu komut, profil toohello komut satırı de yayımlama hello profili tooa metin dosyası yayımlama hello çıktı görüntülemektedir.

#### <a name="reset-publishing-profile"></a>Yayımlama profilini Sıfırla
tooreset her ikisi de hello yayımlama parolası kullanmak bir web uygulaması için FTP ve web dağıtmak için:

    Reset-AzureRmWebAppPublishingProfile -Name ContosoWebApp -ResourceGroupName ContosoAzureResourceGroup

### <a name="manage-web-app-certificates"></a>Web uygulaması sertifikaları yönetme
toolearn nasıl toomanage web uygulaması sertifikalar hakkında bkz [PowerShell kullanarak SSL sertifikalarını bağlama](app-service-web-app-powershell-ssl-binding.md)

### <a name="next-steps"></a>Sonraki Adımlar
* Azure Resource Manager PowerShell desteği hakkında toolearn bakın [Azure PowerShell kullanarak Azure Resource Manager ile.](../powershell-azure-resource-manager.md)
* Uygulama hizmeti ortamları hakkında toolearn bakın [giriş tooApp hizmeti ortamı.](app-service-app-service-environment-intro.md)
* PowerShell kullanarak uygulama hizmeti SSL sertifikaların yönetilmesi hakkında toolearn bakın [PowerShell kullanarak SSL sertifikalarını bağlama.](app-service-web-app-powershell-ssl-binding.md)
* toolearn hello tam listesi için Azure Web uygulamaları, Azure Resource Manager tabanlı PowerShell cmdlet'leri hakkında bkz [, Web uygulamaları Azure Resource Manager PowerShell cmdlet'lerinin Azure Cmdlet başvurusu.](https://msdn.microsoft.com/library/mt619237.aspx)
* * Uygulama hizmeti, CLI kullanarak yönetme hakkında toolearn bkz [Using Azure Resource Manager-Based XPlat CLI Azure Web uygulaması için.](app-service-web-app-azure-resource-manager-xplat-cli.md)

