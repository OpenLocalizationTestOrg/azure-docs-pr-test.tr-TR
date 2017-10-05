---
title: "Azure portalında gezinme için başvuru"
description: "Farklı kullanıcı deneyimleri için App Service Web Yönetim Portalı ve Azure portalı arasında bilgi edinin"
services: app-service
documentationcenter: 
author: jaime-espinosa
manager: erikre
editor: jimbe
ms.assetid: 0cc6a3cc-bd89-4a96-9177-d25f6fb737bb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: jaime-espinosa
ms.openlocfilehash: d1ef6e87d82df0840e49412154df40cc937b320c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="reference-for-navigating-the-azure-portal"></a><span data-ttu-id="28936-103">Azure portalında gezinme için başvuru</span><span class="sxs-lookup"><span data-stu-id="28936-103">Reference for navigating the Azure portal</span></span>
<span data-ttu-id="28936-104">Azure Web siteleri artık adlı [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="28936-104">Azure Websites are now called [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="28936-105">Tüm bu ad değişikliği yansıtacak şekilde ve Azure Portal yönergeler sağlamak için Belgelerimizi güncelleştiriyoruz.</span><span class="sxs-lookup"><span data-stu-id="28936-105">We're updating all of our documentation to reflect this name change and to provide instructions for the Azure Portal.</span></span> <span data-ttu-id="28936-106">Bu işlem yapılana kadar Azure portalında Web Apps ile çalışmak için bu belgede bir kılavuz olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28936-106">Until that process is done, you can use this document as a guide for working with Web Apps in the Azure portal.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="the-future-of-the-azure-classic-portal"></a><span data-ttu-id="28936-107">Klasik Azure portalı geleceği</span><span class="sxs-lookup"><span data-stu-id="28936-107">The future of the Azure Classic Portal</span></span>
<span data-ttu-id="28936-108">Klasik Azure portalı marka değişiklikleri fark edeceksiniz, ancak bu Azure Portal tarafından değiştirilen sürecinde portalıdır.</span><span class="sxs-lookup"><span data-stu-id="28936-108">While you will notice the branding changes on the Azure Classic Portal, that portal is in the process of being replaced by the Azure Portal.</span></span> <span data-ttu-id="28936-109">Klasik Portalı'nı aşamalı olarak Sonlandırılmakta gibi yeni yazılım geliştirme için odak Azure Portalı'na kaydırma.</span><span class="sxs-lookup"><span data-stu-id="28936-109">As the classic portal is being phased out, the focus for new development is shifting to the Azure Portal.</span></span> <span data-ttu-id="28936-110">Tüm yaklaşan yeni özellikler Web uygulamaları için Azure Portalı'nda gelecektir.</span><span class="sxs-lookup"><span data-stu-id="28936-110">All upcoming new features for Web Apps will come in the Azure Portal.</span></span> <span data-ttu-id="28936-111">Web uygulamaları sunmaya sahip en son ve en büyük avantajlarından yararlanmak için Azure Portalı'nı kullanarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="28936-111">Start using the Azure Portal to take advantage of the latest and greatest that Web Apps have to offer.</span></span>

## <a name="layout-differences-between-the-azure-classic-portal-and-azure-portal"></a><span data-ttu-id="28936-112">Düzen farklarını Klasik Azure portalı ve Azure portalı</span><span class="sxs-lookup"><span data-stu-id="28936-112">Layout differences between the Azure Classic Portal and Azure Portal</span></span>
<span data-ttu-id="28936-113">Klasik portalda tüm Azure hizmetlerini sol tarafında listelenir.</span><span class="sxs-lookup"><span data-stu-id="28936-113">In the classic portal, all the Azure services are listed on the left hand side.</span></span> <span data-ttu-id="28936-114">Klasik portalda Gezinti ağaç yapısı, burada hizmetinden başlatmak ve her bir öğeye gidin izler.</span><span class="sxs-lookup"><span data-stu-id="28936-114">Navigation in the classic portal follows a tree structure, where you start from the service and navigate into each element.</span></span> <span data-ttu-id="28936-115">Bu yapı bağımsız bileşenler yönetirken iyi çalışır.</span><span class="sxs-lookup"><span data-stu-id="28936-115">This structure works well when managing independent components.</span></span> <span data-ttu-id="28936-116">Ancak, Azure üzerinde oluşturulan uygulamaların birbirine bağlı hizmetler koleksiyonu olan ve bu ağaç yapısı Hizmetleri koleksiyonları ile çalışmak için ideal değil.</span><span class="sxs-lookup"><span data-stu-id="28936-116">However, applications built on Azure are a collection of interconnected services, and this tree structure isn't ideal for working with collections of services.</span></span> 

<span data-ttu-id="28936-117">Azure portal uygulamaları için uçtan birden çok hizmet bileşenlerini içeren derleme kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="28936-117">The Azure portal makes it easy to build applications end-to-end with components from multiple services.</span></span> <span data-ttu-id="28936-118">Portal olarak düzenlenmiş *Yolculuklar*.</span><span class="sxs-lookup"><span data-stu-id="28936-118">The portal is organized as *journeys*.</span></span> <span data-ttu-id="28936-119">A *gezisine* bir dizi *dikey*, farklı bileşenler için kapsayıcı olduğu.</span><span class="sxs-lookup"><span data-stu-id="28936-119">A *journey* is a series of *blades*, which are containers for the different components.</span></span> <span data-ttu-id="28936-120">Örneğin, otomatik bir web uygulaması için ölçeklendirmeyi ayarlama bir *gezisine* aldığı, birkaç Kanatlar aşağıdaki örnekte gösterildiği gibi: **web sitesi** (dikey penceresi başlığı henüz yeni terimlerle kullanılacak güncelleştirildiğini değil) dikey penceresinde **ayarları** dikey penceresinde ve **ölçeğini** dikey.</span><span class="sxs-lookup"><span data-stu-id="28936-120">For example, setting up auto-scaling for a web app is a *journey* which takes you several blades as shown in the following example: the **web-site** blade (that blade title has not yet been updated to use the new terminology), the **Settings** blade, and the **Scale out** blade.</span></span> <span data-ttu-id="28936-121">Örnekte, otomatik ölçeklendirme CPU kullanımı, bu yüzden de bağımlı ayarlanan bir **CPU yüzdesi** dikey.</span><span class="sxs-lookup"><span data-stu-id="28936-121">In the example, auto scaling is being set up to depend on CPU usage, so there is also a **CPU Percentage** blade.</span></span> <span data-ttu-id="28936-122">İçinde bileşenleri *dikey* denir *bölümleri*, kutucukları gibi arayın.</span><span class="sxs-lookup"><span data-stu-id="28936-122">The components within the *blades* are called *parts*, which look like tiles.</span></span> 

![](./media/app-service-web-app-azure-portal/AutoScaling.png)

## <a name="navigation-example-create-a-web-app"></a><span data-ttu-id="28936-123">Gezinti örnek: bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="28936-123">Navigation example: create a web app</span></span>
<span data-ttu-id="28936-124">Yeni web uygulamaları oluşturma 1-2-3 hala kadar kolaydır.</span><span class="sxs-lookup"><span data-stu-id="28936-124">Creating new web apps is still as easy as 1-2-3.</span></span> <span data-ttu-id="28936-125">Aşağıdaki resimde Klasik Portalı'nı ve portal-değil çok çalıştıran ve bir web uygulaması hale getirmek için gereken adımları sayısında değiştiğini göstermek için yana gösterir.</span><span class="sxs-lookup"><span data-stu-id="28936-125">The following image shows the classic portal and the portal side-by-side to demonstrate that not much has changed in the number of steps needed to get a web app up and running.</span></span> 

![](./media/app-service-web-app-azure-portal/CreateWebApp.png)

<span data-ttu-id="28936-126">Portalda web uygulamaları, WordPress gibi popüler galeri uygulamalar dahil olmak üzere en yaygın türleri arasından seçim yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28936-126">In the portal you can choose from the most common types of web apps, including popular gallery applications like WordPress.</span></span> <span data-ttu-id="28936-127">Kullanılabilir uygulamaların tam listesi için ziyaret [Azure Marketi].</span><span class="sxs-lookup"><span data-stu-id="28936-127">For a full list of available applications, visit the [Azure Marketplace].</span></span>

<span data-ttu-id="28936-128">URL, belirttiğiniz bir web uygulaması oluşturduğunuzda uygulama hizmeti planı ve klasik portalda yapmak gibi portal konumda.</span><span class="sxs-lookup"><span data-stu-id="28936-128">When you create a web app, you specify URL, App Service plan, and location in the portal just as you do in the classic portal.</span></span> 

![](./media/app-service-web-app-azure-portal/CreateWebAppSettings.png)

<span data-ttu-id="28936-129">Buna ek olarak, portal, diğer genel ayarları tanımlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="28936-129">In addition, the portal lets you define other common settings.</span></span> <span data-ttu-id="28936-130">Örneğin, [kaynak grupları](../azure-resource-manager/resource-group-overview.md) ilgili Azure kaynaklarını görmeyi ve yönetmeyi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="28936-130">For example, [resource groups](../azure-resource-manager/resource-group-overview.md) make it simple to see and manage related Azure resources.</span></span> 

## <a name="navigation-example-settings-and-features"></a><span data-ttu-id="28936-131">Gezinti örnek: ayarları ve özellikleri</span><span class="sxs-lookup"><span data-stu-id="28936-131">Navigation example: settings and features</span></span>
<span data-ttu-id="28936-132">Tüm ayarları ve özellikleri artık mantıksal olarak gezinmek tek bir dikey pencerede gruplandırılır.</span><span class="sxs-lookup"><span data-stu-id="28936-132">All the settings and features are now logically grouped in a single blade, from which you can navigate.</span></span>

![](./media/app-service-web-app-azure-portal/WebAppSettings.png)

<span data-ttu-id="28936-133">Örneğin, özel etki alanlarını tıklayarak oluşturabileceğiniz **özel etki alanları ve SSL** içinde **ayarları** dikey.</span><span class="sxs-lookup"><span data-stu-id="28936-133">For example, you can create custom domains by clicking **Custom domains and SSL** in the **Settings** blade.</span></span>

![](./media/app-service-web-app-azure-portal/ConfigureWebApp.png)

<span data-ttu-id="28936-134">Bir izleme uyarısı ayarlamak için tıklatın **istekleri ve hataları** ve ardından **eklemek uyarı**.</span><span class="sxs-lookup"><span data-stu-id="28936-134">To set up a monitoring alert, click **Requests and errors** and then **Add Alert**.</span></span>

![](./media/app-service-web-app-azure-portal/Monitoring.png)

<span data-ttu-id="28936-135">Tanılama etkinleştirmek için **tanılama günlükleri** içinde **ayarları** dikey.</span><span class="sxs-lookup"><span data-stu-id="28936-135">To enable diagnostics, click **Diagnostics logs** in the **Settings** blade.</span></span>

![](./media/app-service-web-app-azure-portal/Diagnostics.png)

<span data-ttu-id="28936-136">Uygulama ayarlarını yapılandırmak için tıklatın **uygulama ayarları** içinde **ayarları** dikey.</span><span class="sxs-lookup"><span data-stu-id="28936-136">To configure application settings, click **Application settings** in the **Settings** blade.</span></span> 

![](./media/app-service-web-app-azure-portal/AppSettingsPreview.png)

<span data-ttu-id="28936-137">Marka adı dışında birkaç portalında yeniden adlandırılmış veya silinmiş bunları bulmayı kolaylaştırmak için farklı bir şekilde gruplandırılmış.</span><span class="sxs-lookup"><span data-stu-id="28936-137">Other than the brand name, a few things in the portal have been renamed or grouped differently to make it easier to find them.</span></span> <span data-ttu-id="28936-138">Örneğin, uygulama ayarları için karşılık gelen sayfasının ekran görüntüsü aşağıda verilmiştir (**yapılandırma**) Klasik Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="28936-138">For example, below is a screenshot of the corresponding page for app settings (**Configure**) in the classic portal.</span></span>

![](./media/app-service-web-app-azure-portal/AppSettings.png)

## <a name="more-resources"></a><span data-ttu-id="28936-139">Daha Fazla Kaynak</span><span class="sxs-lookup"><span data-stu-id="28936-139">More Resources</span></span>
[Azure Portal]: https://portal.azure.com
<span data-ttu-id="28936-140">[Azure Marketi]: /marketplace/</span><span class="sxs-lookup"><span data-stu-id="28936-140">[Azure Marketplace]: /marketplace/</span></span>

> [!NOTE]
> <span data-ttu-id="28936-141">Azure hesabı için kaydolmadan önce Azure App Service’i kullanmaya başlamak isterseniz, App Service’te hemen kısa süreli bir başlangıç web uygulaması oluşturabileceğiniz [App Service’i Deneyin](https://azure.microsoft.com/try/app-service/) sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="28936-141">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="28936-142">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="28936-142">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="28936-143">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="28936-143">What's changed</span></span>
* <span data-ttu-id="28936-144">Web Sitelerinden App Service’e kadar değiştirme kılavuzu için bkz. [Azure App Service ve Mevcut Azure Hizmetlerine Etkileri](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="28936-144">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

