---
title: "aaaAzure App Service planlarına ayrıntılı genel bakış | Microsoft Docs"
description: "Azure uygulama hizmeti iş için nasıl uygulama hizmeti planları ve bunların, yönetim deneyimi nasıl yararlı öğrenin."
keywords: "app service, azure app service, ölçek, ölçeklenebilir, app service planı, app service maliyeti"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: dea3f41e-cf35-481b-a6bc-33d7fc9d01b1
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: b384790d9e69b234ca69ac591164c48a4b6ed210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-plans-in-depth-overview"></a><span data-ttu-id="1097a-104">Azure App Service planlarına ayrıntılı genel bakış</span><span class="sxs-lookup"><span data-stu-id="1097a-104">Azure App Service plans in-depth overview</span></span>

<span data-ttu-id="1097a-105">Uygulama hizmeti planları, uygulamalarınızı kullanılan fiziksel kaynakları toohost hello koleksiyonunu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="1097a-105">App Service plans represent hello collection of physical resources used toohost your apps.</span></span>

<span data-ttu-id="1097a-106">App Service planları şunları tanımlar:</span><span class="sxs-lookup"><span data-stu-id="1097a-106">App Service plans define:</span></span>

- <span data-ttu-id="1097a-107">Bölge (Batı ABD, Doğu ABD, vb.)</span><span class="sxs-lookup"><span data-stu-id="1097a-107">Region (West US, East US, etc.)</span></span>
- <span data-ttu-id="1097a-108">Ölçek sayısı (bir, iki, üç örnekleri, vb.)</span><span class="sxs-lookup"><span data-stu-id="1097a-108">Scale count (one, two, three instances, etc.)</span></span>
- <span data-ttu-id="1097a-109">(Küçük, Orta, büyük) örnek boyutu</span><span class="sxs-lookup"><span data-stu-id="1097a-109">Instance size (Small, Medium, Large)</span></span>
- <span data-ttu-id="1097a-110">SKU (Ücretsiz, Paylaşılan, Temel, Standart, Premium)</span><span class="sxs-lookup"><span data-stu-id="1097a-110">SKU (Free, Shared, Basic, Standard, Premium)</span></span>

<span data-ttu-id="1097a-111">İçinde Apps, Mobile Apps, API uygulamaları, işlev uygulamalarının (veya işlevler), web [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) bir uygulama hizmeti planındaki tüm çalışma.</span><span class="sxs-lookup"><span data-stu-id="1097a-111">Web Apps, Mobile Apps, API Apps, Function Apps (or Functions), in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) all run in an App Service plan.</span></span>  <span data-ttu-id="1097a-112">Uygulamaları hello bir uygulama hizmeti planı aynı abonelikte ve bölgede paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1097a-112">Apps in hello same subscription, and region can share an App Service plan.</span></span> 

<span data-ttu-id="1097a-113">Atanan tüm uygulamalar için tooan **uygulama hizmeti planı** tanımladığı hello kaynakları paylaşır.</span><span class="sxs-lookup"><span data-stu-id="1097a-113">All applications assigned tooan **App Service plan** share hello resources defined by it.</span></span> <span data-ttu-id="1097a-114">Bu paylaşımı para birden fazla uygulama tek bir uygulama hizmeti planında barındırdığında kaydeder.</span><span class="sxs-lookup"><span data-stu-id="1097a-114">This sharing saves money when hosting multiple apps in a single App Service plan.</span></span>

<span data-ttu-id="1097a-115">**Uygulama hizmeti planı** gelen ölçeklendirebilirsiniz **serbest** ve **paylaşılan** SKU'ları çok**temel**, **standart**, ve **Premium** , vermiş SKU'ları erişim toomore kaynakları ve özellikleri hello boyunca yolu.</span><span class="sxs-lookup"><span data-stu-id="1097a-115">Your **App Service plan** can scale from **Free** and **Shared** SKUs too**Basic**, **Standard**, and **Premium** SKUs giving you access toomore resources and features along hello way.</span></span>

<span data-ttu-id="1097a-116">Uygulama hizmeti planınızı çok ayarlarsanız**temel** SKU veya daha yüksek hello denetleyebilirsiniz sonra **boyutu** ve ölçeklendirme hello VM'ler sayısı.</span><span class="sxs-lookup"><span data-stu-id="1097a-116">If your App Service plan is set too**Basic** SKU or higher, then you can control hello **size** and scale count of hello VMs.</span></span>

<span data-ttu-id="1097a-117">Örneğin, planınız yapılandırılmış toouse iki "küçük" Merhaba standart hizmet katmanındaki ise, bu planla ilişkili tüm uygulamalar hem örneklerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1097a-117">For example, if your plan is configured toouse two "small" instances in hello standard service tier, all apps that are associated with that plan run on both instances.</span></span> <span data-ttu-id="1097a-118">Uygulamaların erişim toohello standart hizmet katmanı özellikleri de vardır.</span><span class="sxs-lookup"><span data-stu-id="1097a-118">Apps also have access toohello standard service tier features.</span></span> <span data-ttu-id="1097a-119">Plan örneği uygulamaları çalıştırdığınız tam olarak yönetilen ve yüksek oranda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1097a-119">Plan instances on which apps are running are fully managed and highly available.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1097a-120">Merhaba **SKU** ve **ölçek** Merhaba uygulama hizmeti planı hello maliyet ve değil hello sayısını içinde barındırılan uygulamalar belirler.</span><span class="sxs-lookup"><span data-stu-id="1097a-120">hello **SKU** and **Scale** of hello App Service plan determines hello cost and not hello number of apps hosted in it.</span></span>

<span data-ttu-id="1097a-121">Bu makalede katmanı ve bir uygulama hizmeti planının ölçek ve nasıl uygulamalarınızı yönetmeye çalışırken oyuna geldikleri gibi hello anahtar özelliklerini inceler.</span><span class="sxs-lookup"><span data-stu-id="1097a-121">This article explores hello key characteristics, such as tier and scale, of an App Service plan and how they come into play while managing your apps.</span></span>

## <a name="apps-and-app-service-plans"></a><span data-ttu-id="1097a-122">Uygulamalar ve uygulama hizmeti planları</span><span class="sxs-lookup"><span data-stu-id="1097a-122">Apps and App Service plans</span></span>

<span data-ttu-id="1097a-123">Uygulama hizmeti bir uygulamada verilen herhangi bir zamanda yalnızca bir uygulama hizmeti plan ile ilişkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="1097a-123">An app in App Service can be associated with only one App Service plan at any given time.</span></span>

<span data-ttu-id="1097a-124">Uygulamaları ve planları içerdiği bir **kaynak grubu**.</span><span class="sxs-lookup"><span data-stu-id="1097a-124">Both apps and plans are contained in a **resource group**.</span></span> <span data-ttu-id="1097a-125">Bir kaynak grubu içinde olan her kaynak için hello yaşam döngüsü sınırı olarak görev yapar.</span><span class="sxs-lookup"><span data-stu-id="1097a-125">A resource group serves as hello lifecycle boundary for every resource that's within it.</span></span> <span data-ttu-id="1097a-126">Kaynak grupları toomanage uygulama tüm hello parçaları birlikte kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1097a-126">You can use resource groups toomanage all hello pieces of an application together.</span></span>

<span data-ttu-id="1097a-127">Tek bir kaynak grubu birden çok uygulama hizmeti planları olduğundan farklı uygulamalar toodifferent fiziksel kaynakları tahsis edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1097a-127">Because a single resource group can have multiple App Service plans, you can allocate different apps toodifferent physical resources.</span></span>

<span data-ttu-id="1097a-128">Örneğin, geliştirme, test ve üretim ortamları arasında kaynakları ayırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1097a-128">For example, you can separate resources among dev, test, and production environments.</span></span> <span data-ttu-id="1097a-129">Üretim ve geliştirme ve test için ayrı ortamlara sahip kaynakları ayırmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="1097a-129">Having separate environments for production and dev/test lets you isolate resources.</span></span> <span data-ttu-id="1097a-130">Bu şekilde, uygulamalarınızı yeni bir sürümü karşı test yük Merhaba aynı rekabet edemez kaynaklar gerçek müşteriler hizmet veren, üretim uygulamalarınızı olarak.</span><span class="sxs-lookup"><span data-stu-id="1097a-130">In this way, load testing against a new version of your apps does not compete for hello same resources as your production apps, which are serving real customers.</span></span>

<span data-ttu-id="1097a-131">Tek bir kaynak grubu içinde birden çok planına sahip olduğunuzda, coğrafi bölgeler kapsayan bir uygulama da tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1097a-131">When you have multiple plans in a single resource group, you can also define an application that spans geographical regions.</span></span>

<span data-ttu-id="1097a-132">Örneğin, iki bölgelerde çalışan yüksek oranda kullanılabilir bir uygulama, en az iki planları, her bölge için bir tane ve her plan ile ilişkili bir uygulama içerir.</span><span class="sxs-lookup"><span data-stu-id="1097a-132">For example, a highly available app running in two regions includes at least two plans, one for each region, and one app associated with each plan.</span></span> <span data-ttu-id="1097a-133">Böyle bir durumda hello uygulama tüm hello kopyalarını ardından tek bir kaynak grubu içinde yer alır.</span><span class="sxs-lookup"><span data-stu-id="1097a-133">In such a situation, all hello copies of hello app are then contained in a single resource group.</span></span> <span data-ttu-id="1097a-134">Birden çok planları ve birden çok uygulama ile bir kaynak grubu büyük kolay toomanage, Denetim ve görünüm hello hello uygulama durumunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="1097a-134">Having a resource group with multiple plans and multiple apps makes it easy toomanage, control, and view hello health of hello application.</span></span>

## <a name="create-an-app-service-plan-or-use-existing-one"></a><span data-ttu-id="1097a-135">Bir uygulama hizmeti planı oluşturun veya varolan bir kullanın</span><span class="sxs-lookup"><span data-stu-id="1097a-135">Create an App Service plan or use existing one</span></span>

<span data-ttu-id="1097a-136">Bir uygulama oluşturduğunuzda, bir kaynak grubu oluşturmayı düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1097a-136">When you create an app, you should consider creating a resource group.</span></span> <span data-ttu-id="1097a-137">Üzerinde bu uygulama daha büyük bir uygulama için bir bileşen ise diğer yandan Merhaba, büyük bu uygulama için ayrılan hello kaynak grubunda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1097a-137">On hello other hand, if this app is a component for a larger application, create it within hello resource group that's allocated for that larger application.</span></span>

<span data-ttu-id="1097a-138">Merhaba uygulama tamamen yeni bir uygulama veya daha büyük bir parçası olup olmadığını belirtir, var olan bir planı toohost toouse seçebilirsiniz, ya da yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1097a-138">Whether hello app is an altogether new application or part of a larger one, you can choose toouse an existing plan toohost it or create a new one.</span></span> <span data-ttu-id="1097a-139">Daha fazla kapasite ve beklenen yükü soru karardır.</span><span class="sxs-lookup"><span data-stu-id="1097a-139">This decision is more a question of capacity and expected load.</span></span>

<span data-ttu-id="1097a-140">Yeni bir uygulama hizmeti uygulamanızı yalıtma öneririz ne zaman planlama:</span><span class="sxs-lookup"><span data-stu-id="1097a-140">We recommend isolating your app into a new App Service plan when:</span></span>

- <span data-ttu-id="1097a-141">Yoğun bir kaynak uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="1097a-141">App is resource-intensive.</span></span>
- <span data-ttu-id="1097a-142">Uygulama hello öğesinden farklı ölçeklendirme etkenleri var olan bir planı barındırılan diğer uygulamalar vardır.</span><span class="sxs-lookup"><span data-stu-id="1097a-142">App has different scaling factors from hello other apps hosted in an existing plan.</span></span>
- <span data-ttu-id="1097a-143">Uygulamanın farklı bir coğrafi bölgede kaynak gerekir.</span><span class="sxs-lookup"><span data-stu-id="1097a-143">App needs resource in a different geographical region.</span></span>

<span data-ttu-id="1097a-144">Böylece uygulamanız için yeni bir kaynak kümesini ayırmak ve uygulamalarınızın daha fazla denetim kazanmak.</span><span class="sxs-lookup"><span data-stu-id="1097a-144">This way you can allocate a new set of resources for your app and gain greater control of your apps.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="1097a-145">App Service planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1097a-145">Create an App Service plan</span></span>

> [!TIP]
> <span data-ttu-id="1097a-146">Bir uygulama hizmeti ortamı varsa, hello belgeleri belirli tooApp hizmeti ortamları burada gözden geçirebilirsiniz: [bir uygulama hizmeti ortamı'nda bir uygulama hizmeti planı oluştur](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span><span class="sxs-lookup"><span data-stu-id="1097a-146">If you have an App Service Environment, you can review hello documentation specific tooApp Service Environments here: [Create an App Service plan in an App Service Environment](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span></span>

<span data-ttu-id="1097a-147">Uygulama hizmeti planı gözatma deneyimi hello veya uygulaması oluşturma işleminin bir parçası olarak boş bir uygulama hizmeti planı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1097a-147">You can create an empty App Service plan from hello App Service plan browse experience or as part of app creation.</span></span>

<span data-ttu-id="1097a-148">Merhaba, [Azure portal](https://portal.azure.com), tıklatın **yeni** > **Web + mobil**ve ardından **Web uygulaması** veya diğer uygulama hizmeti uygulaması türü.</span><span class="sxs-lookup"><span data-stu-id="1097a-148">In hello [Azure portal](https://portal.azure.com), click **New** > **Web + mobile**, and then select **Web App** or other App Service app kind.</span></span>

![Hello Azure portalında bir uygulama oluşturun.][createWebApp]

<span data-ttu-id="1097a-150">Ardından, seçin veya hello hello yeni uygulaması için uygulama hizmeti planı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1097a-150">You can then select or create hello App Service plan for hello new app.</span></span>

 ![Bir uygulama hizmeti planı oluşturun.][createASP]

<span data-ttu-id="1097a-152">toocreate bir uygulama hizmeti planı tıklatın **[+] oluştur yeni**, türü hello **uygulama hizmeti planı** adlandırın ve ardından uygun bir seçin **konumu**.</span><span class="sxs-lookup"><span data-stu-id="1097a-152">toocreate an App Service plan, click **[+] Create New**, type hello **App Service plan** name, and then select an appropriate **Location**.</span></span> <span data-ttu-id="1097a-153">Tıklatın **fiyatlandırma katmanı**ve ardından hello hizmeti için uygun bir fiyatlandırma katmanı seçin.</span><span class="sxs-lookup"><span data-stu-id="1097a-153">Click **Pricing tier**, and then select an appropriate pricing tier for hello service.</span></span> <span data-ttu-id="1097a-154">Seçin **tüm görüntüle** daha seçenekleri gibi fiyatlandırma tooview **serbest** ve **paylaşılan**.</span><span class="sxs-lookup"><span data-stu-id="1097a-154">Select **View all** tooview more pricing options, such as **Free** and **Shared**.</span></span> <span data-ttu-id="1097a-155">Fiyatlandırma katmanı hello seçtikten sonra hello tıklatın **seçin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1097a-155">After you have selected hello pricing tier, click hello **Select** button.</span></span>

## <a name="move-an-app-tooa-different-app-service-plan"></a><span data-ttu-id="1097a-156">Bir uygulama tooa farklı uygulama hizmeti planı taşıma</span><span class="sxs-lookup"><span data-stu-id="1097a-156">Move an app tooa different App Service plan</span></span>

<span data-ttu-id="1097a-157">Bir uygulama tooa farklı uygulama hizmeti planı hello taşıyabilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1097a-157">You can move an app tooa different App Service plan in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="1097a-158">Merhaba planları hello olduğu sürece, uygulamaları planları arasında taşıyabilirsiniz aynı kaynak grubunu ve coğrafi bölge.</span><span class="sxs-lookup"><span data-stu-id="1097a-158">You can move apps between plans as long as hello plans are in hello same resource group and geographical region.</span></span>

<span data-ttu-id="1097a-159">bir uygulama tooanother planı toomove:</span><span class="sxs-lookup"><span data-stu-id="1097a-159">toomove an app tooanother plan:</span></span>

- <span data-ttu-id="1097a-160">Toomove istediğiniz toohello uygulamasına gidin.</span><span class="sxs-lookup"><span data-stu-id="1097a-160">Navigate toohello app that you want toomove.</span></span>
- <span data-ttu-id="1097a-161">Merhaba, **menü**, Merhaba Ara **App Service planı** bölümü.</span><span class="sxs-lookup"><span data-stu-id="1097a-161">In hello **Menu**, look for hello **App Service Plan** section.</span></span>
- <span data-ttu-id="1097a-162">Seçin **değişiklik uygulama hizmeti planı** toostart hello işlemi.</span><span class="sxs-lookup"><span data-stu-id="1097a-162">Select **Change App Service plan** toostart hello process.</span></span>

<span data-ttu-id="1097a-163">**Uygulama hizmeti planını Değiştir** açılır hello **uygulama hizmeti planı** Seçici.</span><span class="sxs-lookup"><span data-stu-id="1097a-163">**Change App Service plan** opens hello **App Service plan** selector.</span></span> <span data-ttu-id="1097a-164">Bu noktada, bu uygulamaya var olan bir planı toomove seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1097a-164">At this point, you can pick an existing plan toomove this app into.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1097a-165">Merhaba select uygulama hizmeti planı kullanıcı Arabirimi tarafından hello ölçütleri aşağıdaki filtre:</span><span class="sxs-lookup"><span data-stu-id="1097a-165">hello select App Service plan UI is filtered by hello following criteria:</span></span>
> - <span data-ttu-id="1097a-166">Merhaba içinde aynı mevcut kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="1097a-166">Exists within hello same Resource Group</span></span>
> - <span data-ttu-id="1097a-167">Hello aynı var. coğrafi bölge</span><span class="sxs-lookup"><span data-stu-id="1097a-167">Exists in hello same Geographical Region</span></span>
> - <span data-ttu-id="1097a-168">Merhaba içinde aynı mevcut Web alanı</span><span class="sxs-lookup"><span data-stu-id="1097a-168">Exists within hello same Webspace</span></span>
>
> <span data-ttu-id="1097a-169">Bir Web alanı, sunucu kaynaklarını gruplandırması tanımlayan bir App Service içinde mantıksal bir yapıdır.</span><span class="sxs-lookup"><span data-stu-id="1097a-169">A Webspace is a logical construct within App Service which defines a grouping of server resources.</span></span> <span data-ttu-id="1097a-170">Coğrafi bölge (örneğin, Batı ABD) uygulama hizmetini kullanarak sipariş tooallocate müşteriler birçok Web alanları içeriyor.</span><span class="sxs-lookup"><span data-stu-id="1097a-170">A Geographical region (such as West US) contains many Webspaces in order tooallocate customers using App Service.</span></span> <span data-ttu-id="1097a-171">Şu anda, uygulama hizmeti kaynaklarına arasında izlemiyor taşınmış mümkün toobe değil.</span><span class="sxs-lookup"><span data-stu-id="1097a-171">Currently, App Service resources aren’t able toobe moved between Webspaces.</span></span>
>

![Uygulama hizmeti planı Seçici.][change]

<span data-ttu-id="1097a-173">Her plan kendi fiyatlandırma katmanı vardır.</span><span class="sxs-lookup"><span data-stu-id="1097a-173">Each plan has its own pricing tier.</span></span> <span data-ttu-id="1097a-174">Örneğin, bir site ücretsiz katmanı tooa standart katmanından bir taşıma, tooit toouse hello özellikleri ve kaynakları hello standart katmanı atanmış tüm uygulamaları etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="1097a-174">For example, moving a site from a Free tier tooa Standard tier, enables all apps assigned tooit toouse hello features and resources of hello Standard tier.</span></span>

## <a name="clone-an-app-tooa-different-app-service-plan"></a><span data-ttu-id="1097a-175">Bir uygulama tooa farklı uygulama hizmeti planı Kopyala</span><span class="sxs-lookup"><span data-stu-id="1097a-175">Clone an app tooa different App Service plan</span></span>

<span data-ttu-id="1097a-176">Toomove hello uygulama tooa farklı bir bölgeye istiyorsanız, bir uygulama alternatiftir kopyalama.</span><span class="sxs-lookup"><span data-stu-id="1097a-176">If you want toomove hello app tooa different region, one alternative is app cloning.</span></span> <span data-ttu-id="1097a-177">Kopyalama, yeni veya var olan uygulama hizmeti planındaki tüm bölgelerdeki uygulamanızı bir kopyasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1097a-177">Cloning makes a copy of your app in a new or existing App Service plan in any region.</span></span>

<span data-ttu-id="1097a-178">Bulabileceğiniz **kopya uygulama** hello içinde **geliştirme araçları** hello menüsünün bölümünde.</span><span class="sxs-lookup"><span data-stu-id="1097a-178">You can find **Clone App** in hello **Development Tools** section of hello menu.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1097a-179">Kopyalama sırasında hakkında bilgi edinebilirsiniz bazı sınırlamalara sahiptir [Azure portalını kullanarak Azure uygulama hizmeti kopyalama](../app-service-web/app-service-web-app-cloning-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1097a-179">Cloning has some limitations that you can read about at [Azure App Service App cloning using Azure portal](../app-service-web/app-service-web-app-cloning-portal.md).</span></span>

## <a name="scale-an-app-service-plan"></a><span data-ttu-id="1097a-180">Ölçek bir uygulama hizmeti planı</span><span class="sxs-lookup"><span data-stu-id="1097a-180">Scale an App Service plan</span></span>

<span data-ttu-id="1097a-181">Bir plan üç yolu tooscale vardır:</span><span class="sxs-lookup"><span data-stu-id="1097a-181">There are three ways tooscale a plan:</span></span>

- <span data-ttu-id="1097a-182">**Değişiklik hello planı katmanı fiyatlandırma**.</span><span class="sxs-lookup"><span data-stu-id="1097a-182">**Change hello plan’s pricing tier**.</span></span> <span data-ttu-id="1097a-183">Bir planı hello temel katmanındaki dönüştürülmüş tooStandard olabilir ve tüm uygulamalar tooit toouse hello standart katmanı hello özelliklerini atanmış.</span><span class="sxs-lookup"><span data-stu-id="1097a-183">A plan in hello Basic tier can be converted tooStandard, and all apps assigned tooit toouse hello features of hello Standard tier.</span></span>
- <span data-ttu-id="1097a-184">**Merhaba planın örnek boyutunu değiştirin**.</span><span class="sxs-lookup"><span data-stu-id="1097a-184">**Change hello plan’s instance size**.</span></span> <span data-ttu-id="1097a-185">Örnek olarak, bir planı küçük örnekleri kullanan hello temel katmanındaki değiştirilen toouse büyük örnekleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1097a-185">As an example, a plan in hello Basic tier that uses small instances can be changed toouse large instances.</span></span> <span data-ttu-id="1097a-186">Şimdi bu planla ilişkili tüm uygulamalar hello ek bellek ve büyük örnek boyutu teklifleri hello CPU kaynaklarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1097a-186">All apps that are associated with that plan now can use hello additional memory and CPU resources that hello larger instance size offers.</span></span>
- <span data-ttu-id="1097a-187">**Merhaba planın örnek sayısı değiştirme**.</span><span class="sxs-lookup"><span data-stu-id="1097a-187">**Change hello plan’s instance count**.</span></span> <span data-ttu-id="1097a-188">Örneğin, toothree örnekleri ölçeklendirilmiş bir standart planı ölçeklendirilmiş too10 örnekleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1097a-188">For example, a Standard plan that's scaled out toothree instances can be scaled too10 instances.</span></span> <span data-ttu-id="1097a-189">Premium planı too20 örnekleri (konu tooavailability) genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="1097a-189">A Premium plan can be scaled out too20 instances (subject tooavailability).</span></span> <span data-ttu-id="1097a-190">Şimdi bu planla ilişkili tüm uygulamalar hello ek bellek ve büyük örnek sayısı teklifleri hello CPU kaynaklarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1097a-190">All apps that are associated with that plan now can use hello additional memory and CPU resources that hello larger instance count offers.</span></span>

<span data-ttu-id="1097a-191">Fiyatlandırma katmanı ve örnek boyutunda hello tıklayarak hello değiştirebileceğiniz **ölçeği Artır** hello uygulama ya da hello uygulama hizmeti planı ayarları altında öğesi.</span><span class="sxs-lookup"><span data-stu-id="1097a-191">You can change hello pricing tier and instance size by clicking hello **Scale Up** item under settings for either hello app or hello App Service plan.</span></span> <span data-ttu-id="1097a-192">Değişiklikler toohello uygulama hizmeti planı uygulamak ve onu barındıran tüm uygulamaları etkiler.</span><span class="sxs-lookup"><span data-stu-id="1097a-192">Changes apply toohello App Service plan and affect all apps that it hosts.</span></span>

 ![Bir uygulama yukarı değerleri tooscale ayarlayın.][pricingtier]

## <a name="app-service-plan-cleanup"></a><span data-ttu-id="1097a-194">Uygulama hizmeti planı temizleme</span><span class="sxs-lookup"><span data-stu-id="1097a-194">App Service plan cleanup</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1097a-195">**Uygulama hizmeti planları** tooreserve hello işlem kapasitesini devam hala ücretlendirme hiçbir ilişkili uygulamalar toothem sahip.</span><span class="sxs-lookup"><span data-stu-id="1097a-195">**App Service plans** that have no apps associated toothem still incur charges since they continue tooreserve hello compute capacity.</span></span>

<span data-ttu-id="1097a-196">tooavoid bir uygulama hizmeti planında barındırılan hello son uygulama silindiğinde, beklenmeyen ücretleri hello elde edilen boş uygulama hizmeti planı da silinir.</span><span class="sxs-lookup"><span data-stu-id="1097a-196">tooavoid unexpected charges, when hello last app hosted in an App Service plan is deleted, hello resulting empty App Service plan is also deleted.</span></span>

## <a name="summary"></a><span data-ttu-id="1097a-197">Özet</span><span class="sxs-lookup"><span data-stu-id="1097a-197">Summary</span></span>

<span data-ttu-id="1097a-198">Uygulama hizmeti planları, bir özellik kümesini ve Web siteleriniz arasında paylaşabileceğiniz kapasite temsil eder.</span><span class="sxs-lookup"><span data-stu-id="1097a-198">App Service plans represent a set of features and capacity that you can share across your apps.</span></span> <span data-ttu-id="1097a-199">Uygulama hizmeti esneklik tooallocate belirli uygulamaları tooa kaynak kümesi hello ve daha fazla Azure kaynak kullanımınızı iyileştirmek verin planlar.</span><span class="sxs-lookup"><span data-stu-id="1097a-199">App Service plans give you hello flexibility tooallocate specific apps tooa set of resources and further optimize your Azure resource utilization.</span></span> <span data-ttu-id="1097a-200">Bu şekilde, test ortamınızda, toosave para istiyorsanız bir planı birden çok uygulama arasında paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1097a-200">This way, if you want toosave money on your testing environment, you can share a plan across multiple apps.</span></span> <span data-ttu-id="1097a-201">Ayrıca verimlilik, üretim ortamınız için birden çok bölgeler ve planları arasında ölçeklendirme tarafından en üst düzeye çıkarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1097a-201">You can also maximize throughput for your production environment by scaling it across multiple regions and plans.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="1097a-202">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="1097a-202">What's changed</span></span>

- <span data-ttu-id="1097a-203">Web siteleri tooApp hizmet gelen bir kılavuzu toohello değişiklik için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="1097a-203">For a guide toohello change from Websites tooApp Service, see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[pricingtier]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png
