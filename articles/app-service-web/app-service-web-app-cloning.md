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
# <a name="azure-app-service-app-cloning-using-powershell"></a><span data-ttu-id="d93f5-103">Azure App Service uygulaması PowerShell kullanarak kopyalama</span><span class="sxs-lookup"><span data-stu-id="d93f5-103">Azure App Service App Cloning Using PowerShell</span></span>
<span data-ttu-id="d93f5-104">Microsoft Azure PowerShell Hello sürümünde yeni bir seçenek süredir sürüm 1.1.0 hello kullanıcı hello özelliği tooclone mevcut bir Web uygulaması yeni oluşturulan tooa uygulamayı farklı bir bölge veya hello verirsiniz tooNew-AzureRMWebApp eklenen aynı bölgede.</span><span class="sxs-lookup"><span data-stu-id="d93f5-104">With hello release of Microsoft Azure PowerShell version 1.1.0 a new option has been added tooNew-AzureRMWebApp that would give hello user hello ability tooclone an existing Web App tooa newly created app in a different region or in hello same region.</span></span> <span data-ttu-id="d93f5-105">Bu müşteriler toodeploy uygulamaları birkaç farklı bölgelerdeki hızla ve kolayca olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="d93f5-105">This will enable customers toodeploy a number of apps across different regions quickly and easily.</span></span>

<span data-ttu-id="d93f5-106">Uygulama kopyalama şu anda yalnızca premium katmanı uygulama hizmeti planları için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="d93f5-106">App cloning is currently only supported for premium tier app service plans.</span></span> <span data-ttu-id="d93f5-107">Merhaba yeni özellik kullandığı aynı hello Web Apps yedekleme özelliği olarak sınırlamalar bakın [Azure App Service'te bir web uygulaması yedekleme](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="d93f5-107">hello new feature uses hello same limitations as Web Apps Backup feature, see [Back up a web app in Azure App Service](web-sites-backup.md).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

<span data-ttu-id="d93f5-108">Azure Kaynak Yöneticisi'ni kullanma hakkında toolearn tabanlı Azure PowerShell cmdlet'leri toomanage Web Apps onay [Azure Web uygulaması için Azure Resource Manager tabanlı PowerShell komutları](app-service-web-app-azure-resource-manager-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="d93f5-108">toolearn about using Azure Resource Manager based Azure PowerShell cmdlets toomanage your Web Apps check [Azure Resource Manager based PowerShell commands for Azure Web App](app-service-web-app-azure-resource-manager-powershell.md)</span></span>

## <a name="cloning-an-existing-app"></a><span data-ttu-id="d93f5-109">Mevcut bir uygulamayı kopyalama</span><span class="sxs-lookup"><span data-stu-id="d93f5-109">Cloning an existing App</span></span>
<span data-ttu-id="d93f5-110">Senaryo: Var olan bir web uygulamasının Orta Güney ABD bölgesindeki tooclone hello içeriği tooa yeni web uygulaması Kuzey Orta ABD bölgesindeki hello kullanıcı ister.</span><span class="sxs-lookup"><span data-stu-id="d93f5-110">Scenario: An existing web app in South Central US region, hello user would like tooclone hello contents tooa new web app in North Central US region.</span></span> <span data-ttu-id="d93f5-111">Bu, hello - SourceWebApp seçeneği hello PowerShell cmdlet toocreate yeni bir web uygulaması hello Azure Resource Manager sürümü kullanılarak gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="d93f5-111">This can be accomplished by using hello Azure Resource Manager version of hello PowerShell cmdlet toocreate a new web app with hello -SourceWebApp option.</span></span>

<span data-ttu-id="d93f5-112">Merhaba kaynak bilerek hello kaynak web uygulamasını içeren grup adı, biz aşağıdaki PowerShell komut tooget hello kaynak web uygulamanızın bilgilerle (Bu durumda kaynak webapp adlı) hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d93f5-112">Knowing hello resource group name that contains hello source web app, we can use hello following PowerShell command tooget hello source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="d93f5-113">toocreate yeni bir uygulama hizmeti planı, şu örnek aşağıdaki hello olduğu gibi yeni AzureRmAppServicePlan komutunu kullanabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="d93f5-113">toocreate a new App Service Plan, we can use New-AzureRmAppServicePlan command as in hello following example</span></span>

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

<span data-ttu-id="d93f5-114">Merhaba yeni AzureRmWebApp komutunu kullanarak, biz hello Kuzey Orta ABD bölgesinde hello yeni web uygulaması oluşturma ve tooan varolan premium katmanı App Service planı tie, ayrıca biz aynı kaynak hello kaynak web uygulaması grubu ya da yeni bir kaynak grubu tanımlamak hello kullanabilirsiniz , hello aşağıda gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="d93f5-114">Using hello New-AzureRmWebApp command, we can create hello new web app in hello North Central US region, and tie it tooan existing premium tier App Service Plan, moreover we can use hello same resource group as hello source web app, or define a new resource group, hello following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

<span data-ttu-id="d93f5-115">tüm ilişkili dağıtım yuvası da dahil olmak üzere var olan bir web uygulamasının hello kullanıcının toouse gerekecek tooclone Merhaba IncludeSourceWebAppSlots parametresi, PowerShell komutunu aşağıdaki hello hello yeni AzureRmWebApp komutu bu parametresiyle hello kullanımını göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="d93f5-115">tooclone an existing web app including all associated deployment slots, hello user will need toouse hello IncludeSourceWebAppSlots parameter, hello following PowerShell command demonstrates hello use of that parameter with hello New-AzureRmWebApp command:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

<span data-ttu-id="d93f5-116">tooclone hello içinde var olan bir web uygulaması aynı bölgede hello kullanıcı yeni bir kaynak grubu ve yeni bir uygulama hizmeti planı hello toocreate gerekir aynı bölge ve ardından kullanarak hello PowerShell komut tooclone hello web uygulaması</span><span class="sxs-lookup"><span data-stu-id="d93f5-116">tooclone an existing web app within hello same region, hello user will need toocreate a new resource group and a new app service plan in hello same region, and then using hello following PowerShell command tooclone hello web app</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a><span data-ttu-id="d93f5-117">Var olan bir uygulama tooan uygulama hizmeti ortamı kopyalama</span><span class="sxs-lookup"><span data-stu-id="d93f5-117">Cloning an existing App tooan App Service Environment</span></span>
<span data-ttu-id="d93f5-118">Senaryo: Var olan bir web uygulamasının Orta Güney ABD bölgesindeki hello kullanıcı var olan uygulama hizmeti ortamı (ana) tooclone hello içeriği tooa yeni web uygulaması tooan ister.</span><span class="sxs-lookup"><span data-stu-id="d93f5-118">Scenario: An existing web app in South Central US region, hello user would like tooclone hello contents tooa new web app tooan existing App Service Environment (ASE).</span></span>

<span data-ttu-id="d93f5-119">Merhaba kaynak bilerek hello kaynak web uygulamasını içeren grup adı, biz aşağıdaki PowerShell komut tooget hello kaynak web uygulamanızın bilgilerle (Bu durumda kaynak webapp adlı) hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d93f5-119">Knowing hello resource group name that contains hello source web app, we can use hello following PowerShell command tooget hello source web app's information (in this case named source-webapp):</span></span>

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

<span data-ttu-id="d93f5-120">Merhaba ana'nın adını ve hello ana ait olduğu kaynak grubu adı hello bilerek hello kullanıcı hello varolan ana, aşağıdaki hello toocreate hello yeni web uygulamasını gösteren hello yeni AzureRmWebApp komutu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d93f5-120">Knowing hello ASE's name, and hello resource group name that hello ASE belongs to, hello user can use hello New-AzureRmWebApp command toocreate hello new web app in hello existing ASE, hello following demonstrates that:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

<span data-ttu-id="d93f5-121">toolegacy neden Hello konum parametresi gereklidir, ancak ASE'de bir uygulama oluşturma hello durumda yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="d93f5-121">hello Location parameter is required due toolegacy reason, but in hello case of creating an app in an ASE it will be ignored.</span></span> 

## <a name="cloning-an-existing-app-slot"></a><span data-ttu-id="d93f5-122">Varolan bir uygulaması yuvası kopyalama</span><span class="sxs-lookup"><span data-stu-id="d93f5-122">Cloning an existing App Slot</span></span>
<span data-ttu-id="d93f5-123">Senaryo: hello kullanıcı tooclone var olan bir Web uygulaması yuvası tooeither yeni bir Web uygulaması veya yeni bir Web uygulaması yuvası ister.</span><span class="sxs-lookup"><span data-stu-id="d93f5-123">Scenario: hello user would like tooclone an existing Web App Slot tooeither a new Web App or a new Web App slot.</span></span> <span data-ttu-id="d93f5-124">Yeni Web uygulaması hello olabilir hello hello özgün Web uygulaması yuvası olarak veya farklı bir bölgede aynı bölge.</span><span class="sxs-lookup"><span data-stu-id="d93f5-124">hello new Web App can be in hello same region as hello original Web App slot or in a different region.</span></span>

<span data-ttu-id="d93f5-125">Merhaba kaynak bilerek hello kaynak web uygulamasını içeren grup adı, biz tooget hello kaynak web uygulaması yuvası ait bilgileri (Bu durumda kaynak webappslot olarak adlandırılır) bağlı tooWeb uygulama kaynak-webapp PowerShell komutunu aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d93f5-125">Knowing hello resource group name that contains hello source web app, we can use hello following PowerShell command tooget hello source web app slot's information (in this case named source-webappslot) tied tooWeb App source-webapp:</span></span>

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

<span data-ttu-id="d93f5-126">Merhaba kaynak web uygulaması tooa yeni web uygulaması bir kopyasını oluşturma Hello şunları gösterir:</span><span class="sxs-lookup"><span data-stu-id="d93f5-126">hello following demonstrates creating a clone of hello source web app tooa new web app:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a><span data-ttu-id="d93f5-127">Bir uygulama kopyalanırken yapılandırma trafik Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="d93f5-127">Configuring Traffic Manager while cloning a App</span></span>
<span data-ttu-id="d93f5-128">Birden çok bölgede web uygulamaları oluşturma ve bu web uygulamaları Azure Traffic Manager tooroute trafiği tooall yapılandırma, olan müşterilerin uygulamaları, sahip mevcut bir web uygulaması kopyalarken yüksek oranda kullanılabilir bir n önemli bir senaryo tooinsure hello seçeneği tooconnect her iki web uygulamaları tooeither yeni bir trafik Yöneticisi profili veya varolan bir - yalnızca Azure Resource Manager sürümünün Not trafik Yöneticisi desteklenir.</span><span class="sxs-lookup"><span data-stu-id="d93f5-128">Creating multi-region web apps and configuring Azure Traffic Manager tooroute traffic tooall these web apps, is a n important scenario tooinsure that customers' apps are highly available, when cloning an existing web app you have hello option tooconnect both web apps tooeither a new traffic manager profile or an existing one - note that only Azure Resource Manager version of Traffic Manager is supported.</span></span>

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a><span data-ttu-id="d93f5-129">Bir uygulama kopyalama sırasında yeni bir Traffic Manager profili oluşturma</span><span class="sxs-lookup"><span data-stu-id="d93f5-129">Creating a new Traffic Manager profile while cloning a App</span></span>
<span data-ttu-id="d93f5-130">Senaryo: hello kullanıcı her iki web uygulamaları içeren bir Azure Resource Manager trafik Yöneticisi profili yapılandırırken tooclone bir web uygulaması tooanother bölge ister.</span><span class="sxs-lookup"><span data-stu-id="d93f5-130">Scenario: hello user would like tooclone an web app tooanother region, while configuring an Azure Resource Manager traffic manager profile that include both web apps.</span></span> <span data-ttu-id="d93f5-131">Yeni bir Traffic Manager profili yapılandırırken hello kaynak web uygulaması tooa yeni web uygulaması bir kopyasını oluşturma Hello şunları gösterir:</span><span class="sxs-lookup"><span data-stu-id="d93f5-131">hello following demonstrates creating a clone of hello source web app tooa new web app while configuring a new Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-tooan-existing-traffic-manager-profile"></a><span data-ttu-id="d93f5-132">Yeni kopyalanmış Web uygulaması tooan varolan trafik Yöneticisi profili ekleme</span><span class="sxs-lookup"><span data-stu-id="d93f5-132">Adding new cloned Web App tooan existing Traffic Manager profile</span></span>
<span data-ttu-id="d93f5-133">Senaryo: hello kullanıcı zaten bir Azure Resource Manager trafik Yöneticisi profili varsa kendisinin tooadd istediğiniz her ikisi de web uygulamaları uç noktalar olarak.</span><span class="sxs-lookup"><span data-stu-id="d93f5-133">Scenario: hello user already have an Azure Resource Manager traffic manager profile that he would like tooadd both web apps as endpoints.</span></span> <span data-ttu-id="d93f5-134">toodo tooassemble önce bu nedenle, ihtiyacımız var olan trafik Yöneticisi Profil Kimliği Merhaba, biz hello abonelik kimliği, kaynak grubu adı ve hello varolan trafik Yöneticisi profil adı gerekir.</span><span class="sxs-lookup"><span data-stu-id="d93f5-134">toodo so, we first need tooassemble hello existing traffic manager profile id, we will need hello subscription id, resource group name and hello existing traffic manager profile name.</span></span>

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

<span data-ttu-id="d93f5-135">Merhaba trafik Yöneticisi kimliğine sahip sonra hello aşağıdaki tooan varolan trafik Yöneticisi profili eklenirken hello kaynak web uygulaması tooa yeni web uygulaması bir kopyasını oluşturma gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="d93f5-135">After having hello traffic manger id, hello following demonstrates creating a clone of hello source web app tooa new web app while adding them tooan existing Traffic Manager profile:</span></span>

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a><span data-ttu-id="d93f5-136">Geçerli kısıtlamaları</span><span class="sxs-lookup"><span data-stu-id="d93f5-136">Current Restrictions</span></span>
<span data-ttu-id="d93f5-137">Bu özellik şu anda önizlemede değil, zaman içinde tooadd yeni özellikler çalışıyoruz, liste aşağıdaki hello uygulama kopyalama hello geçerli sürümü bilinen sınırlamalar hello:</span><span class="sxs-lookup"><span data-stu-id="d93f5-137">This feature is currently in preview, we are working tooadd new capabilities over time, hello following list are hello known restrictions on hello current version of app cloning:</span></span>

* <span data-ttu-id="d93f5-138">Otomatik ölçek ayarları klonlanmış değil</span><span class="sxs-lookup"><span data-stu-id="d93f5-138">Auto scale settings are not cloned</span></span>
* <span data-ttu-id="d93f5-139">Yedekleme zamanlaması ayarları klonlanmış değil</span><span class="sxs-lookup"><span data-stu-id="d93f5-139">Backup schedule settings are not cloned</span></span>
* <span data-ttu-id="d93f5-140">VNET ayarlarını klonlanmış değil</span><span class="sxs-lookup"><span data-stu-id="d93f5-140">VNET settings are not cloned</span></span>
* <span data-ttu-id="d93f5-141">App Insights otomatik olarak hello hedef web uygulamasında belirlenmedi</span><span class="sxs-lookup"><span data-stu-id="d93f5-141">App Insights are not automatically set up on hello destination web app</span></span>
* <span data-ttu-id="d93f5-142">Kolay kimlik doğrulama ayarları klonlanmış değil</span><span class="sxs-lookup"><span data-stu-id="d93f5-142">Easy Auth settings are not cloned</span></span>
* <span data-ttu-id="d93f5-143">Kudu uzantısı değil kopyalanamıyor</span><span class="sxs-lookup"><span data-stu-id="d93f5-143">Kudu Extension are not cloned</span></span>
* <span data-ttu-id="d93f5-144">İpucu kuralları klonlanmış değil</span><span class="sxs-lookup"><span data-stu-id="d93f5-144">TiP rules are not cloned</span></span>
* <span data-ttu-id="d93f5-145">Veritabanı içeriğini değil kopyalanamıyor</span><span class="sxs-lookup"><span data-stu-id="d93f5-145">Database content are not cloned</span></span>

### <a name="references"></a><span data-ttu-id="d93f5-146">Başvurular</span><span class="sxs-lookup"><span data-stu-id="d93f5-146">References</span></span>
* [<span data-ttu-id="d93f5-147">Azure Resource Manager PowerShell komutlarını Azure Web uygulaması için temel</span><span class="sxs-lookup"><span data-stu-id="d93f5-147">Azure Resource Manager based PowerShell commands for Azure Web App</span></span>](app-service-web-app-azure-resource-manager-powershell.md)
* [<span data-ttu-id="d93f5-148">Azure Portal kullanarak Web uygulaması kopyalama</span><span class="sxs-lookup"><span data-stu-id="d93f5-148">Web App Cloning using Azure Portal</span></span>](app-service-web-app-cloning-portal.md)
* [<span data-ttu-id="d93f5-149">Azure App Service'in web uygulamasında yedekleyin</span><span class="sxs-lookup"><span data-stu-id="d93f5-149">Back up a web app in Azure App Service</span></span>](web-sites-backup.md)
* [<span data-ttu-id="d93f5-150">Azure Traffic Manager Önizleme için Azure Resource Manager desteği</span><span class="sxs-lookup"><span data-stu-id="d93f5-150">Azure Resource Manager support for Azure Traffic Manager Preview</span></span>](../traffic-manager/traffic-manager-powershell-arm.md)
* [<span data-ttu-id="d93f5-151">Giriş tooApp hizmeti ortamı</span><span class="sxs-lookup"><span data-stu-id="d93f5-151">Introduction tooApp Service Environment</span></span>](app-service-app-service-environment-intro.md)
* [<span data-ttu-id="d93f5-152">Azure PowerShell’i Azure Resource Manager ile kullanma</span><span class="sxs-lookup"><span data-stu-id="d93f5-152">Using Azure PowerShell with Azure Resource Manager</span></span>](../powershell-azure-resource-manager.md)

