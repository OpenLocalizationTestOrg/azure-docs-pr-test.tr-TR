---
title: aaaWeb uygulama PowerShell kullanarak kopyalama
description: "Bilgi nasıl tooclone PowerShell kullanarak, Web uygulamaları toonew Web uygulamaları."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: f9a5cfa1-fbb0-41e6-95d1-75d457347a35
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: b8882370d6db6939f8e4473ccc1414091bdcb8f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-powershell"></a>Azure App Service uygulaması PowerShell kullanarak kopyalama
Microsoft Azure PowerShell Hello sürümünde yeni bir seçenek süredir sürüm 1.1.0 hello kullanıcı hello özelliği tooclone mevcut bir Web uygulaması yeni oluşturulan tooa uygulamayı farklı bir bölge veya hello verirsiniz tooNew-AzureRMWebApp eklenen aynı bölgede. Bu müşteriler toodeploy uygulamaları birkaç farklı bölgelerdeki hızla ve kolayca olanak tanır.

Uygulama kopyalama şu anda yalnızca premium katmanı uygulama hizmeti planları için desteklenir. Merhaba yeni özellik kullandığı aynı hello Web Apps yedekleme özelliği olarak sınırlamalar bakın [Azure App Service'te bir web uygulaması yedekleme](web-sites-backup.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

Azure Kaynak Yöneticisi'ni kullanma hakkında toolearn tabanlı Azure PowerShell cmdlet'leri toomanage Web Apps onay [Azure Web uygulaması için Azure Resource Manager tabanlı PowerShell komutları](app-service-web-app-azure-resource-manager-powershell.md)

## <a name="cloning-an-existing-app"></a>Mevcut bir uygulamayı kopyalama
Senaryo: Var olan bir web uygulamasının Orta Güney ABD bölgesindeki tooclone hello içeriği tooa yeni web uygulaması Kuzey Orta ABD bölgesindeki hello kullanıcı ister. Bu, hello - SourceWebApp seçeneği hello PowerShell cmdlet toocreate yeni bir web uygulaması hello Azure Resource Manager sürümü kullanılarak gerçekleştirilebilir.

Merhaba kaynak bilerek hello kaynak web uygulamasını içeren grup adı, biz aşağıdaki PowerShell komut tooget hello kaynak web uygulamanızın bilgilerle (Bu durumda kaynak webapp adlı) hello kullanabilirsiniz:

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

toocreate yeni bir uygulama hizmeti planı, şu örnek aşağıdaki hello olduğu gibi yeni AzureRmAppServicePlan komutunu kullanabilirsiniz

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

Merhaba yeni AzureRmWebApp komutunu kullanarak, biz hello Kuzey Orta ABD bölgesinde hello yeni web uygulaması oluşturma ve tooan varolan premium katmanı App Service planı tie, ayrıca biz aynı kaynak hello kaynak web uygulaması grubu ya da yeni bir kaynak grubu tanımlamak hello kullanabilirsiniz , hello aşağıda gösterilmektedir:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

tüm ilişkili dağıtım yuvası da dahil olmak üzere var olan bir web uygulamasının hello kullanıcının toouse gerekecek tooclone Merhaba IncludeSourceWebAppSlots parametresi, PowerShell komutunu aşağıdaki hello hello yeni AzureRmWebApp komutu bu parametresiyle hello kullanımını göstermektedir:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

tooclone hello içinde var olan bir web uygulaması aynı bölgede hello kullanıcı yeni bir kaynak grubu ve yeni bir uygulama hizmeti planı hello toocreate gerekir aynı bölge ve ardından kullanarak hello PowerShell komut tooclone hello web uygulaması

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a>Var olan bir uygulama tooan uygulama hizmeti ortamı kopyalama
Senaryo: Var olan bir web uygulamasının Orta Güney ABD bölgesindeki hello kullanıcı var olan uygulama hizmeti ortamı (ana) tooclone hello içeriği tooa yeni web uygulaması tooan ister.

Merhaba kaynak bilerek hello kaynak web uygulamasını içeren grup adı, biz aşağıdaki PowerShell komut tooget hello kaynak web uygulamanızın bilgilerle (Bu durumda kaynak webapp adlı) hello kullanabilirsiniz:

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

Merhaba ana'nın adını ve hello ana ait olduğu kaynak grubu adı hello bilerek hello kullanıcı hello varolan ana, aşağıdaki hello toocreate hello yeni web uygulamasını gösteren hello yeni AzureRmWebApp komutu kullanabilirsiniz:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

toolegacy neden Hello konum parametresi gereklidir, ancak ASE'de bir uygulama oluşturma hello durumda yoksayılır. 

## <a name="cloning-an-existing-app-slot"></a>Varolan bir uygulaması yuvası kopyalama
Senaryo: hello kullanıcı tooclone var olan bir Web uygulaması yuvası tooeither yeni bir Web uygulaması veya yeni bir Web uygulaması yuvası ister. Yeni Web uygulaması hello olabilir hello hello özgün Web uygulaması yuvası olarak veya farklı bir bölgede aynı bölge.

Merhaba kaynak bilerek hello kaynak web uygulamasını içeren grup adı, biz tooget hello kaynak web uygulaması yuvası ait bilgileri (Bu durumda kaynak webappslot olarak adlandırılır) bağlı tooWeb uygulama kaynak-webapp PowerShell komutunu aşağıdaki hello kullanabilirsiniz:

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

Merhaba kaynak web uygulaması tooa yeni web uygulaması bir kopyasını oluşturma Hello şunları gösterir:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a>Bir uygulama kopyalanırken yapılandırma trafik Yöneticisi
Birden çok bölgede web uygulamaları oluşturma ve bu web uygulamaları Azure Traffic Manager tooroute trafiği tooall yapılandırma, olan müşterilerin uygulamaları, sahip mevcut bir web uygulaması kopyalarken yüksek oranda kullanılabilir bir n önemli bir senaryo tooinsure hello seçeneği tooconnect her iki web uygulamaları tooeither yeni bir trafik Yöneticisi profili veya varolan bir - yalnızca Azure Resource Manager sürümünün Not trafik Yöneticisi desteklenir.

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a>Bir uygulama kopyalama sırasında yeni bir Traffic Manager profili oluşturma
Senaryo: hello kullanıcı her iki web uygulamaları içeren bir Azure Resource Manager trafik Yöneticisi profili yapılandırırken tooclone bir web uygulaması tooanother bölge ister. Yeni bir Traffic Manager profili yapılandırırken hello kaynak web uygulaması tooa yeni web uygulaması bir kopyasını oluşturma Hello şunları gösterir:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-tooan-existing-traffic-manager-profile"></a>Yeni kopyalanmış Web uygulaması tooan varolan trafik Yöneticisi profili ekleme
Senaryo: hello kullanıcı zaten bir Azure Resource Manager trafik Yöneticisi profili varsa kendisinin tooadd istediğiniz her ikisi de web uygulamaları uç noktalar olarak. toodo tooassemble önce bu nedenle, ihtiyacımız var olan trafik Yöneticisi Profil Kimliği Merhaba, biz hello abonelik kimliği, kaynak grubu adı ve hello varolan trafik Yöneticisi profil adı gerekir.

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

Merhaba trafik Yöneticisi kimliğine sahip sonra hello aşağıdaki tooan varolan trafik Yöneticisi profili eklenirken hello kaynak web uygulaması tooa yeni web uygulaması bir kopyasını oluşturma gösterilmektedir:

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a>Geçerli kısıtlamaları
Bu özellik şu anda önizlemede değil, zaman içinde tooadd yeni özellikler çalışıyoruz, liste aşağıdaki hello uygulama kopyalama hello geçerli sürümü bilinen sınırlamalar hello:

* Otomatik ölçek ayarları klonlanmış değil
* Yedekleme zamanlaması ayarları klonlanmış değil
* VNET ayarlarını klonlanmış değil
* App Insights otomatik olarak hello hedef web uygulamasında belirlenmedi
* Kolay kimlik doğrulama ayarları klonlanmış değil
* Kudu uzantısı değil kopyalanamıyor
* İpucu kuralları klonlanmış değil
* Veritabanı içeriğini değil kopyalanamıyor

### <a name="references"></a>Başvurular
* [Azure Resource Manager PowerShell komutlarını Azure Web uygulaması için temel](app-service-web-app-azure-resource-manager-powershell.md)
* [Azure Portal kullanarak Web uygulaması kopyalama](app-service-web-app-cloning-portal.md)
* [Azure App Service'in web uygulamasında yedekleyin](web-sites-backup.md)
* [Azure Traffic Manager Önizleme için Azure Resource Manager desteği](../traffic-manager/traffic-manager-powershell-arm.md)
* [Giriş tooApp hizmeti ortamı](app-service-app-service-environment-intro.md)
* [Azure PowerShell’i Azure Resource Manager ile kullanma](../powershell-azure-resource-manager.md)

