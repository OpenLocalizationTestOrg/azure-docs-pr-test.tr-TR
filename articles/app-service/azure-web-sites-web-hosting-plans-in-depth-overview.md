---
title: "Azure App Service planlarına ayrıntılı genel bakış | Microsoft Docs"
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
ms.openlocfilehash: f97be571d104e3cc1c6ee732886fa7133ba0dc83
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-app-service-plans-in-depth-overview"></a><span data-ttu-id="e6f09-104">Azure App Service planlarına ayrıntılı genel bakış</span><span class="sxs-lookup"><span data-stu-id="e6f09-104">Azure App Service plans in-depth overview</span></span>

<span data-ttu-id="e6f09-105">Uygulama hizmeti planları, uygulamalarınızı barındırmak için kullanılan fiziksel kaynakları koleksiyonunu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="e6f09-105">App Service plans represent the collection of physical resources used to host your apps.</span></span>

<span data-ttu-id="e6f09-106">App Service planları şunları tanımlar:</span><span class="sxs-lookup"><span data-stu-id="e6f09-106">App Service plans define:</span></span>

- <span data-ttu-id="e6f09-107">Bölge (Batı ABD, Doğu ABD, vb.)</span><span class="sxs-lookup"><span data-stu-id="e6f09-107">Region (West US, East US, etc.)</span></span>
- <span data-ttu-id="e6f09-108">Ölçek sayısı (bir, iki, üç örnekleri, vb.)</span><span class="sxs-lookup"><span data-stu-id="e6f09-108">Scale count (one, two, three instances, etc.)</span></span>
- <span data-ttu-id="e6f09-109">(Küçük, Orta, büyük) örnek boyutu</span><span class="sxs-lookup"><span data-stu-id="e6f09-109">Instance size (Small, Medium, Large)</span></span>
- <span data-ttu-id="e6f09-110">SKU (Ücretsiz, Paylaşılan, Temel, Standart, Premium)</span><span class="sxs-lookup"><span data-stu-id="e6f09-110">SKU (Free, Shared, Basic, Standard, Premium)</span></span>

<span data-ttu-id="e6f09-111">İçinde Apps, Mobile Apps, API uygulamaları, işlev uygulamalarının (veya işlevler), web [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) bir uygulama hizmeti planındaki tüm çalışma.</span><span class="sxs-lookup"><span data-stu-id="e6f09-111">Web Apps, Mobile Apps, API Apps, Function Apps (or Functions), in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) all run in an App Service plan.</span></span>  <span data-ttu-id="e6f09-112">Aynı abonelikte ve bölgede uygulamalarda uygulama hizmeti planı paylaşabilir.</span><span class="sxs-lookup"><span data-stu-id="e6f09-112">Apps in the same subscription, and region can share an App Service plan.</span></span> 

<span data-ttu-id="e6f09-113">Tüm uygulamalar için atanan bir **uygulama hizmeti planı** tanımladığı kaynakları paylaşır.</span><span class="sxs-lookup"><span data-stu-id="e6f09-113">All applications assigned to an **App Service plan** share the resources defined by it.</span></span> <span data-ttu-id="e6f09-114">Bu paylaşımı para birden fazla uygulama tek bir uygulama hizmeti planında barındırdığında kaydeder.</span><span class="sxs-lookup"><span data-stu-id="e6f09-114">This sharing saves money when hosting multiple apps in a single App Service plan.</span></span>

<span data-ttu-id="e6f09-115">Bu sırada **App Service planınızı** **Ücretsiz** ve **Paylaşılan** SKU’larından **Temel**, **Standart** ve **Premium** SKU’larına ölçeklendirerek daha fazla kaynak ve özelliğe erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6f09-115">Your **App Service plan** can scale from **Free** and **Shared** SKUs to **Basic**, **Standard**, and **Premium** SKUs giving you access to more resources and features along the way.</span></span>

<span data-ttu-id="e6f09-116">Uygulama hizmeti planınızı ayarlanmışsa **temel** SKU veya daha yüksek kontrol edebilirsiniz sonra **boyutu** ve ölçeklendirme VM'ler sayısı.</span><span class="sxs-lookup"><span data-stu-id="e6f09-116">If your App Service plan is set to **Basic** SKU or higher, then you can control the **size** and scale count of the VMs.</span></span>

<span data-ttu-id="e6f09-117">Örneğin, planınız standart hizmet katmanında iki "küçük" örneklerini kullanmak için yapılandırdıysanız, bu planla ilişkili tüm uygulamalar hem örneklerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e6f09-117">For example, if your plan is configured to use two "small" instances in the standard service tier, all apps that are associated with that plan run on both instances.</span></span> <span data-ttu-id="e6f09-118">Uygulamalar ayrıca standart hizmet katmanı özelliklerine erişime sahiptir.</span><span class="sxs-lookup"><span data-stu-id="e6f09-118">Apps also have access to the standard service tier features.</span></span> <span data-ttu-id="e6f09-119">Plan örneği uygulamaları çalıştırdığınız tam olarak yönetilen ve yüksek oranda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e6f09-119">Plan instances on which apps are running are fully managed and highly available.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e6f09-120">App Service planının **SKU** ve **Ölçek** değeri, planda barındırılan uygulama sayısını değil planın maliyetini belirler.</span><span class="sxs-lookup"><span data-stu-id="e6f09-120">The **SKU** and **Scale** of the App Service plan determines the cost and not the number of apps hosted in it.</span></span>

<span data-ttu-id="e6f09-121">Bu makalede katmanı ve bir uygulama hizmeti planı ve nasıl uygulamalarınızı yönetmeye çalışırken oyuna geldikleri ölçek gibi anahtar özelliklerini inceler.</span><span class="sxs-lookup"><span data-stu-id="e6f09-121">This article explores the key characteristics, such as tier and scale, of an App Service plan and how they come into play while managing your apps.</span></span>

## <a name="apps-and-app-service-plans"></a><span data-ttu-id="e6f09-122">Uygulamalar ve uygulama hizmeti planları</span><span class="sxs-lookup"><span data-stu-id="e6f09-122">Apps and App Service plans</span></span>

<span data-ttu-id="e6f09-123">Uygulama hizmeti bir uygulamada verilen herhangi bir zamanda yalnızca bir uygulama hizmeti plan ile ilişkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="e6f09-123">An app in App Service can be associated with only one App Service plan at any given time.</span></span>

<span data-ttu-id="e6f09-124">Uygulamaları ve planları içerdiği bir **kaynak grubu**.</span><span class="sxs-lookup"><span data-stu-id="e6f09-124">Both apps and plans are contained in a **resource group**.</span></span> <span data-ttu-id="e6f09-125">Bir kaynak grubu içinde olan her kaynak için yaşam döngüsü sınırı olarak görev yapar.</span><span class="sxs-lookup"><span data-stu-id="e6f09-125">A resource group serves as the lifecycle boundary for every resource that's within it.</span></span> <span data-ttu-id="e6f09-126">Bir uygulamanın tüm parçaları birlikte yönetmek için kaynak gruplarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6f09-126">You can use resource groups to manage all the pieces of an application together.</span></span>

<span data-ttu-id="e6f09-127">Tek bir kaynak grubu birden çok uygulama hizmeti planları olduğundan farklı uygulamalar farklı fiziksel kaynaklara tahsis edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6f09-127">Because a single resource group can have multiple App Service plans, you can allocate different apps to different physical resources.</span></span>

<span data-ttu-id="e6f09-128">Örneğin, geliştirme, test ve üretim ortamları arasında kaynakları ayırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6f09-128">For example, you can separate resources among dev, test, and production environments.</span></span> <span data-ttu-id="e6f09-129">Üretim ve geliştirme ve test için ayrı ortamlara sahip kaynakları ayırmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="e6f09-129">Having separate environments for production and dev/test lets you isolate resources.</span></span> <span data-ttu-id="e6f09-130">Bu şekilde, uygulamalarınızı yeni bir sürümü karşı test yük gerçek müşteriler hizmet veren, üretim uygulamalarınızı aynı kaynaklara için rekabet edemez.</span><span class="sxs-lookup"><span data-stu-id="e6f09-130">In this way, load testing against a new version of your apps does not compete for the same resources as your production apps, which are serving real customers.</span></span>

<span data-ttu-id="e6f09-131">Tek bir kaynak grubu içinde birden çok planına sahip olduğunuzda, coğrafi bölgeler kapsayan bir uygulama da tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6f09-131">When you have multiple plans in a single resource group, you can also define an application that spans geographical regions.</span></span>

<span data-ttu-id="e6f09-132">Örneğin, iki bölgelerde çalışan yüksek oranda kullanılabilir bir uygulama, en az iki planları, her bölge için bir tane ve her plan ile ilişkili bir uygulama içerir.</span><span class="sxs-lookup"><span data-stu-id="e6f09-132">For example, a highly available app running in two regions includes at least two plans, one for each region, and one app associated with each plan.</span></span> <span data-ttu-id="e6f09-133">Böyle bir durumda, uygulamanın tüm kopyalarını ardından tek bir kaynak grubu içinde yer alır.</span><span class="sxs-lookup"><span data-stu-id="e6f09-133">In such a situation, all the copies of the app are then contained in a single resource group.</span></span> <span data-ttu-id="e6f09-134">Birden çok planları ve birden çok uygulama ile bir kaynak grubu olması yönetmek, denetlemek ve uygulama durumunu görüntülemek kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="e6f09-134">Having a resource group with multiple plans and multiple apps makes it easy to manage, control, and view the health of the application.</span></span>

## <a name="create-an-app-service-plan-or-use-existing-one"></a><span data-ttu-id="e6f09-135">Bir uygulama hizmeti planı oluşturun veya varolan bir kullanın</span><span class="sxs-lookup"><span data-stu-id="e6f09-135">Create an App Service plan or use existing one</span></span>

<span data-ttu-id="e6f09-136">Bir uygulama oluşturduğunuzda, bir kaynak grubu oluşturmayı düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6f09-136">When you create an app, you should consider creating a resource group.</span></span> <span data-ttu-id="e6f09-137">Öte yandan, bu uygulama daha büyük bir uygulama için bir bileşen varsa, bu büyük uygulama için ayrılmış kaynak grubunda oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e6f09-137">On the other hand, if this app is a component for a larger application, create it within the resource group that's allocated for that larger application.</span></span>

<span data-ttu-id="e6f09-138">Uygulama bir tamamen yeni uygulama ya da daha büyük bir parçası olup olmadığını da barındırmak veya yeni bir tane oluşturmak için var olan bir planı kullanmayı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6f09-138">Whether the app is an altogether new application or part of a larger one, you can choose to use an existing plan to host it or create a new one.</span></span> <span data-ttu-id="e6f09-139">Daha fazla kapasite ve beklenen yükü soru karardır.</span><span class="sxs-lookup"><span data-stu-id="e6f09-139">This decision is more a question of capacity and expected load.</span></span>

<span data-ttu-id="e6f09-140">Yeni bir uygulama hizmeti uygulamanızı yalıtma öneririz ne zaman planlama:</span><span class="sxs-lookup"><span data-stu-id="e6f09-140">We recommend isolating your app into a new App Service plan when:</span></span>

- <span data-ttu-id="e6f09-141">Yoğun bir kaynak uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="e6f09-141">App is resource-intensive.</span></span>
- <span data-ttu-id="e6f09-142">Uygulama, var olan bir planı barındırılan diğer uygulamalardan farklı ölçeklendirme Etkenler vardır.</span><span class="sxs-lookup"><span data-stu-id="e6f09-142">App has different scaling factors from the other apps hosted in an existing plan.</span></span>
- <span data-ttu-id="e6f09-143">Uygulamanın farklı bir coğrafi bölgede kaynak gerekir.</span><span class="sxs-lookup"><span data-stu-id="e6f09-143">App needs resource in a different geographical region.</span></span>

<span data-ttu-id="e6f09-144">Böylece uygulamanız için yeni bir kaynak kümesini ayırmak ve uygulamalarınızın daha fazla denetim kazanmak.</span><span class="sxs-lookup"><span data-stu-id="e6f09-144">This way you can allocate a new set of resources for your app and gain greater control of your apps.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="e6f09-145">App Service planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e6f09-145">Create an App Service plan</span></span>

> [!TIP]
> <span data-ttu-id="e6f09-146">Bir uygulama hizmeti ortamı varsa, App Service ortamları için belirli şuradaki belgelere gözden geçirebilirsiniz: [bir uygulama hizmeti ortamı'nda bir uygulama hizmeti planı oluştur](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span><span class="sxs-lookup"><span data-stu-id="e6f09-146">If you have an App Service Environment, you can review the documentation specific to App Service Environments here: [Create an App Service plan in an App Service Environment](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span></span>

<span data-ttu-id="e6f09-147">Uygulama hizmeti planı gözatma deneyimi veya uygulaması oluşturma işleminin bir parçası olarak boş bir uygulama hizmeti planı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6f09-147">You can create an empty App Service plan from the App Service plan browse experience or as part of app creation.</span></span>

<span data-ttu-id="e6f09-148">İçinde [Azure portal](https://portal.azure.com), tıklatın **yeni** > **Web + mobil**ve ardından **Web uygulaması** veya diğer uygulama hizmeti uygulaması türü.</span><span class="sxs-lookup"><span data-stu-id="e6f09-148">In the [Azure portal](https://portal.azure.com), click **New** > **Web + mobile**, and then select **Web App** or other App Service app kind.</span></span>

![Azure Portalı'nda bir uygulama oluşturun.][createWebApp]

<span data-ttu-id="e6f09-150">Ardından, seçin veya yeni uygulaması için uygulama hizmeti planı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e6f09-150">You can then select or create the App Service plan for the new app.</span></span>

 ![Bir uygulama hizmeti planı oluşturun.][createASP]

<span data-ttu-id="e6f09-152">Bir uygulama hizmeti planı oluşturmak için tıklatın **[+] oluştur yeni**, türü **uygulama hizmeti planı** adlandırın ve ardından uygun bir seçin **konumu**.</span><span class="sxs-lookup"><span data-stu-id="e6f09-152">To create an App Service plan, click **[+] Create New**, type the **App Service plan** name, and then select an appropriate **Location**.</span></span> <span data-ttu-id="e6f09-153">Tıklatın **fiyatlandırma katmanı**ve ardından hizmet için uygun bir fiyatlandırma katmanı seçin.</span><span class="sxs-lookup"><span data-stu-id="e6f09-153">Click **Pricing tier**, and then select an appropriate pricing tier for the service.</span></span> <span data-ttu-id="e6f09-154">Seçin **tüm görüntüle** daha seçenekleri gibi fiyatlandırma görünümüne **serbest** ve **paylaşılan**.</span><span class="sxs-lookup"><span data-stu-id="e6f09-154">Select **View all** to view more pricing options, such as **Free** and **Shared**.</span></span> <span data-ttu-id="e6f09-155">Fiyatlandırma katmanı seçtikten sonra tıklatın **seçin** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e6f09-155">After you have selected the pricing tier, click the **Select** button.</span></span>

## <a name="move-an-app-to-a-different-app-service-plan"></a><span data-ttu-id="e6f09-156">Bir uygulama için farklı bir uygulama hizmeti planı taşıma</span><span class="sxs-lookup"><span data-stu-id="e6f09-156">Move an app to a different App Service plan</span></span>

<span data-ttu-id="e6f09-157">Bir uygulama farklı bir uygulama hizmeti planında taşıyabilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e6f09-157">You can move an app to a different App Service plan in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e6f09-158">Aynı kaynak grubunu ve coğrafi bölge planları olduğu sürece, uygulamaları planları arasında taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6f09-158">You can move apps between plans as long as the plans are in the same resource group and geographical region.</span></span>

<span data-ttu-id="e6f09-159">Bir uygulamayı başka bir plana taşımak için:</span><span class="sxs-lookup"><span data-stu-id="e6f09-159">To move an app to another plan:</span></span>

- <span data-ttu-id="e6f09-160">Taşımak istediğiniz uygulamaya gidin.</span><span class="sxs-lookup"><span data-stu-id="e6f09-160">Navigate to the app that you want to move.</span></span>
- <span data-ttu-id="e6f09-161">İçinde **menü**, Ara **App Service planı** bölümü.</span><span class="sxs-lookup"><span data-stu-id="e6f09-161">In the **Menu**, look for the **App Service Plan** section.</span></span>
- <span data-ttu-id="e6f09-162">Seçin **değişiklik uygulama hizmeti planı** işlemini başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="e6f09-162">Select **Change App Service plan** to start the process.</span></span>

<span data-ttu-id="e6f09-163">**Uygulama hizmeti planını Değiştir** açılır **uygulama hizmeti planı** Seçici.</span><span class="sxs-lookup"><span data-stu-id="e6f09-163">**Change App Service plan** opens the **App Service plan** selector.</span></span> <span data-ttu-id="e6f09-164">Bu noktada, bu uygulamaya taşımak için var olan bir planı seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6f09-164">At this point, you can pick an existing plan to move this app into.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e6f09-165">Select uygulama hizmeti planı kullanıcı Arabirimi, aşağıdaki ölçütlere göre filtrelenen:</span><span class="sxs-lookup"><span data-stu-id="e6f09-165">The select App Service plan UI is filtered by the following criteria:</span></span>
> - <span data-ttu-id="e6f09-166">Aynı kaynak grubunda var</span><span class="sxs-lookup"><span data-stu-id="e6f09-166">Exists within the same Resource Group</span></span>
> - <span data-ttu-id="e6f09-167">Aynı coğrafi bölgede var</span><span class="sxs-lookup"><span data-stu-id="e6f09-167">Exists in the same Geographical Region</span></span>
> - <span data-ttu-id="e6f09-168">İçinde aynı Web alanı var.</span><span class="sxs-lookup"><span data-stu-id="e6f09-168">Exists within the same Webspace</span></span>
>
> <span data-ttu-id="e6f09-169">Bir Web alanı, sunucu kaynaklarını gruplandırması tanımlayan bir App Service içinde mantıksal bir yapıdır.</span><span class="sxs-lookup"><span data-stu-id="e6f09-169">A Webspace is a logical construct within App Service which defines a grouping of server resources.</span></span> <span data-ttu-id="e6f09-170">Coğrafi bölge (örneğin, Batı ABD), uygulama hizmeti kullanan müşteriler ayırmak için birçok Web alanları içeriyor.</span><span class="sxs-lookup"><span data-stu-id="e6f09-170">A Geographical region (such as West US) contains many Webspaces in order to allocate customers using App Service.</span></span> <span data-ttu-id="e6f09-171">Şu anda, uygulama hizmeti kaynaklar arasında izlemiyor taşınmasını mümkün değil.</span><span class="sxs-lookup"><span data-stu-id="e6f09-171">Currently, App Service resources aren’t able to be moved between Webspaces.</span></span>
>

![Uygulama hizmeti planı Seçici.][change]

<span data-ttu-id="e6f09-173">Her plan kendi fiyatlandırma katmanı vardır.</span><span class="sxs-lookup"><span data-stu-id="e6f09-173">Each plan has its own pricing tier.</span></span> <span data-ttu-id="e6f09-174">Örneğin, bir site ücretsiz katmanından bir taşıma için standart katmanı, özellikleri ve kaynakları standart katmanı kullanmak için atanmış tüm uygulamaları etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="e6f09-174">For example, moving a site from a Free tier to a Standard tier, enables all apps assigned to it to use the features and resources of the Standard tier.</span></span>

## <a name="clone-an-app-to-a-different-app-service-plan"></a><span data-ttu-id="e6f09-175">Bir uygulama için farklı bir uygulama hizmeti plan kopyalama</span><span class="sxs-lookup"><span data-stu-id="e6f09-175">Clone an app to a different App Service plan</span></span>

<span data-ttu-id="e6f09-176">Farklı bir bölgeye uygulama taşımak istiyorsanız, bir uygulama alternatiftir kopyalama.</span><span class="sxs-lookup"><span data-stu-id="e6f09-176">If you want to move the app to a different region, one alternative is app cloning.</span></span> <span data-ttu-id="e6f09-177">Kopyalama, yeni veya var olan uygulama hizmeti planındaki tüm bölgelerdeki uygulamanızı bir kopyasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e6f09-177">Cloning makes a copy of your app in a new or existing App Service plan in any region.</span></span>

<span data-ttu-id="e6f09-178">Bulabileceğiniz **kopya uygulama** içinde **geliştirme araçları** menüsünün bölümünde.</span><span class="sxs-lookup"><span data-stu-id="e6f09-178">You can find **Clone App** in the **Development Tools** section of the menu.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e6f09-179">Kopyalama sırasında hakkında bilgi edinebilirsiniz bazı sınırlamalara sahiptir [Azure portalını kullanarak Azure uygulama hizmeti kopyalama](../app-service-web/app-service-web-app-cloning-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e6f09-179">Cloning has some limitations that you can read about at [Azure App Service App cloning using Azure portal](../app-service-web/app-service-web-app-cloning-portal.md).</span></span>

## <a name="scale-an-app-service-plan"></a><span data-ttu-id="e6f09-180">Ölçek bir uygulama hizmeti planı</span><span class="sxs-lookup"><span data-stu-id="e6f09-180">Scale an App Service plan</span></span>

<span data-ttu-id="e6f09-181">Bir planı ölçeklendirmek için üç yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="e6f09-181">There are three ways to scale a plan:</span></span>

- <span data-ttu-id="e6f09-182">**Fiyatlandırma katmanı değişikliği plan**.</span><span class="sxs-lookup"><span data-stu-id="e6f09-182">**Change the plan’s pricing tier**.</span></span> <span data-ttu-id="e6f09-183">Bir planı temel katmandaki, standart ve standart katmanı özellikleri kullanmak için atanmış tüm uygulamalar için dönüştürülebilir.</span><span class="sxs-lookup"><span data-stu-id="e6f09-183">A plan in the Basic tier can be converted to Standard, and all apps assigned to it to use the features of the Standard tier.</span></span>
- <span data-ttu-id="e6f09-184">**Planın örnek boyutunu değiştirin**.</span><span class="sxs-lookup"><span data-stu-id="e6f09-184">**Change the plan’s instance size**.</span></span> <span data-ttu-id="e6f09-185">Örnek olarak, büyük örnekleri kullanmak için bir plan küçük örnekleri kullanan temel katmandaki değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="e6f09-185">As an example, a plan in the Basic tier that uses small instances can be changed to use large instances.</span></span> <span data-ttu-id="e6f09-186">Şimdi bu planla ilişkili tüm uygulamalar, büyük örnek boyutu sunar CPU kaynaklarını ve ek bellek kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6f09-186">All apps that are associated with that plan now can use the additional memory and CPU resources that the larger instance size offers.</span></span>
- <span data-ttu-id="e6f09-187">**Planın örnek sayısı değiştirme**.</span><span class="sxs-lookup"><span data-stu-id="e6f09-187">**Change the plan’s instance count**.</span></span> <span data-ttu-id="e6f09-188">Örneğin, üç örneklerine giden ölçeklendirilmiş bir standart planı 10 örneklerine genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="e6f09-188">For example, a Standard plan that's scaled out to three instances can be scaled to 10 instances.</span></span> <span data-ttu-id="e6f09-189">Premium planı 20 örneklerine (tabi kullanılabilirlik) genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="e6f09-189">A Premium plan can be scaled out to 20 instances (subject to availability).</span></span> <span data-ttu-id="e6f09-190">Şimdi bu planla ilişkili tüm uygulamalar, büyük örnek sayısı sunar CPU kaynaklarını ve ek bellek kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6f09-190">All apps that are associated with that plan now can use the additional memory and CPU resources that the larger instance count offers.</span></span>

<span data-ttu-id="e6f09-191">Fiyatlandırma katmanı ve örnek boyutunu tıklatarak değiştirebilirsiniz **ölçeği Artır** uygulamayı veya uygulama hizmeti planı ayarları altında öğesi.</span><span class="sxs-lookup"><span data-stu-id="e6f09-191">You can change the pricing tier and instance size by clicking the **Scale Up** item under settings for either the app or the App Service plan.</span></span> <span data-ttu-id="e6f09-192">Değişiklikler için uygulama hizmeti planı uygulamak ve onu barındıran tüm uygulamaları etkiler.</span><span class="sxs-lookup"><span data-stu-id="e6f09-192">Changes apply to the App Service plan and affect all apps that it hosts.</span></span>

 ![Bir uygulama ölçeklendirmek için değerleri ayarlayın.][pricingtier]

## <a name="app-service-plan-cleanup"></a><span data-ttu-id="e6f09-194">Uygulama hizmeti planı temizleme</span><span class="sxs-lookup"><span data-stu-id="e6f09-194">App Service plan cleanup</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e6f09-195">**Uygulama hizmeti planları** sahip olan işlem kapasitesini yedek devam beri hala ücretlendirme kendileri için ilişkilendirilmiş uygulama yok.</span><span class="sxs-lookup"><span data-stu-id="e6f09-195">**App Service plans** that have no apps associated to them still incur charges since they continue to reserve the compute capacity.</span></span>

<span data-ttu-id="e6f09-196">Bir uygulama hizmeti planında barındırılan son uygulama silindiğinde beklenmeyen ücretlerden kaçınmak için sonuç boş uygulama hizmeti planı de silinir.</span><span class="sxs-lookup"><span data-stu-id="e6f09-196">To avoid unexpected charges, when the last app hosted in an App Service plan is deleted, the resulting empty App Service plan is also deleted.</span></span>

## <a name="summary"></a><span data-ttu-id="e6f09-197">Özet</span><span class="sxs-lookup"><span data-stu-id="e6f09-197">Summary</span></span>

<span data-ttu-id="e6f09-198">Uygulama hizmeti planları, bir özellik kümesini ve Web siteleriniz arasında paylaşabileceğiniz kapasite temsil eder.</span><span class="sxs-lookup"><span data-stu-id="e6f09-198">App Service plans represent a set of features and capacity that you can share across your apps.</span></span> <span data-ttu-id="e6f09-199">Uygulama hizmeti planları bir kaynak grubu için belirli uygulamaları ayırmak ve daha fazla Azure kaynak kullanımınızı iyileştirmek için esneklik sağlar.</span><span class="sxs-lookup"><span data-stu-id="e6f09-199">App Service plans give you the flexibility to allocate specific apps to a set of resources and further optimize your Azure resource utilization.</span></span> <span data-ttu-id="e6f09-200">Bu şekilde, test ortamınızda, tasarruf istiyorsanız bir planı birden çok uygulama arasında paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6f09-200">This way, if you want to save money on your testing environment, you can share a plan across multiple apps.</span></span> <span data-ttu-id="e6f09-201">Ayrıca verimlilik, üretim ortamınız için birden çok bölgeler ve planları arasında ölçeklendirme tarafından en üst düzeye çıkarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6f09-201">You can also maximize throughput for your production environment by scaling it across multiple regions and plans.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="e6f09-202">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="e6f09-202">What's changed</span></span>

- <span data-ttu-id="e6f09-203">Sitelerinden App Service'e değiştirme kılavuzu için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="e6f09-203">For a guide to the change from Websites to App Service, see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[pricingtier]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png
