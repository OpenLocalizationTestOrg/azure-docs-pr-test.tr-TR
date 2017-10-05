---
title: Azure App Service ve mevcut Azure hizmetlerine etkileri
description: "Var olan Azure hizmetlerinde yeni Azure App Service ve özelliklerini nasıl etkisi açıklanmaktadır."
services: app-service
documentationcenter: 
author: yochay
manager: nirma
editor: 
ms.assetid: 86c6a292-3c33-49f4-890c-89cc0321b397
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2016
ms.author: yochaykk
ms.openlocfilehash: ed967fda7a216ed49532be54228ebe888cf16b6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a><span data-ttu-id="99e2e-103">Azure Uygulama Hizmeti ve var olan Azure hizmetleri</span><span class="sxs-lookup"><span data-stu-id="99e2e-103">Azure App Service and existing Azure services</span></span>
<span data-ttu-id="99e2e-104">Bu makalede, çeşitli Azure hizmetlerine bir araya getirme değiştirilecek bir parçası olarak mevcut Azure hizmetlerine değişiklikler özetlenmektedir [Azure App Service](https://azure.microsoft.com/services/app-service/), yeni bir tümleşik sunum.</span><span class="sxs-lookup"><span data-stu-id="99e2e-104">This article outlines the changes to existing Azure services as part of the change to bring together several Azure services into [Azure App Service](https://azure.microsoft.com/services/app-service/), a new integrated offering.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a><span data-ttu-id="99e2e-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="99e2e-105">Overview</span></span>
<span data-ttu-id="99e2e-106">[Azure uygulama hizmeti](https://azure.microsoft.com/services/app-service/) geliştiricilerin web ve herhangi bir platform ve herhangi bir aygıt için mobil uygulamaları oluşturmalarına olanak veren bir yeni ve benzersiz bir bulut hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="99e2e-106">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a new and unique cloud service that enables developers to create web and mobile apps for any platform and any device.</span></span> <span data-ttu-id="99e2e-107">Uygulama, yinelenen kodlama işlevleri kolaylaştırmak, kurumsal ve SaaS sistemlerle tümleştirmek ve güvenlik, güvenilirlik ve ölçeklendirilebilirlik, ihtiyaçlarını iş süreçlerini otomatikleştirmek için tasarlanmış tümleşik bir çözüm hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="99e2e-107">App Service is an integrated solution designed to streamline repeated coding functions, integrate with enterprise and SaaS systems, and automate business processes while meeting your needs for security, reliability, and scalability.</span></span>

<span data-ttu-id="99e2e-108">Uygulama hizmeti getirir birlikte aşağıdaki mevcut Azure Hizmetleri - [Web siteleri](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), ve [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) eklenirken hizmeti, tek bir birleştirilmiş güçlü yeni özellikleri.</span><span class="sxs-lookup"><span data-stu-id="99e2e-108">App Service brings together the following existing Azure services - [Websites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), and [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) into a single combined service, while adding powerful new capabilities.</span></span>  <span data-ttu-id="99e2e-109">Uygulama hizmeti aşağıdaki uygulama türlerini barındırmanıza olanak sağlar:</span><span class="sxs-lookup"><span data-stu-id="99e2e-109">App Service allows you to host the following app types:</span></span>

* <span data-ttu-id="99e2e-110">Web Apps</span><span class="sxs-lookup"><span data-stu-id="99e2e-110">Web Apps</span></span>
* <span data-ttu-id="99e2e-111">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="99e2e-111">Mobile Apps</span></span>
* <span data-ttu-id="99e2e-112">API Apps</span><span class="sxs-lookup"><span data-stu-id="99e2e-112">API Apps</span></span>
* <span data-ttu-id="99e2e-113">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="99e2e-113">Logic Apps</span></span>

<span data-ttu-id="99e2e-114">Aşağıdaki tabloda, uygulama hizmeti nasıl mevcut Azure hizmetlerine eşlemesine ve içinde kullanılabilir uygulama türleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="99e2e-114">The following table explains how existing Azure services map to App Service and the app types available within it.</span></span>

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%"><span data-ttu-id="99e2e-115">Var olan Azure hizmeti</span><span class="sxs-lookup"><span data-stu-id="99e2e-115">Existing Azure Service</span></span></th>
<th align="left", style="width:10%"><span data-ttu-id="99e2e-116">Azure App Service</span><span class="sxs-lookup"><span data-stu-id="99e2e-116">Azure App Service</span></span></th>
<th align="left", style="width:80%"><span data-ttu-id="99e2e-117">Neler değişti</span><span class="sxs-lookup"><span data-stu-id="99e2e-117">What changed</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="99e2e-118">Azure Web Siteleri</span><span class="sxs-lookup"><span data-stu-id="99e2e-118">Azure Websites</span></span></td>
<td align="left"><span data-ttu-id="99e2e-119">Web Apps</span><span class="sxs-lookup"><span data-stu-id="99e2e-119">Web Apps</span></span></td>
<td align="left"><li><span data-ttu-id="99e2e-120">Azure Web siteleri için App Service Web Apps için Web siteleri adını değiştirmek için kesinlikle sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="99e2e-120">For Azure Websites, App Service is strictly limited to changing the name  Websites to Web Apps.</span></span>
<p><li><span data-ttu-id="99e2e-121">Web sitelerinin tüm mevcut örnekleri App Service'te Web uygulamalarını sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="99e2e-121">All your existing instances of Websites are now Web Apps in App Service.</span></span></p>
<p><li><span data-ttu-id="99e2e-122">Varolan sitelerinizi aracılığıyla erişebilirsiniz <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, altındaki tüm var olan siteler bulacaksınız burada <em>Web Apps</em>.</span><span class="sxs-lookup"><span data-stu-id="99e2e-122">You can access your existing websites via the <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, where you will find all your existing sites under <em>Web Apps</em>.</span></span></p>
<p><li><span data-ttu-id="99e2e-123"><em>Web barındırma planına</em> artık <em>App Service planı</em>.</span><span class="sxs-lookup"><span data-stu-id="99e2e-123"><em>Web Hosting Plan</em> is now <em>App Service Plan</em>.</span></span> <span data-ttu-id="99e2e-124">Bir <em>App Service planı</em> uygulama her türlü Web, mobil, mantığı veya API uygulamaları gibi uygulama hizmeti barındırabilir.</span><span class="sxs-lookup"><span data-stu-id="99e2e-124">An <em>App Service Plan</em> can host any app type of App Service, such as Web, Mobile, Logic, or API apps.</span></span></p>
<p><li><span data-ttu-id="99e2e-125">Azure App Service Web Apps genel kullanılabilirlik olması.</span><span class="sxs-lookup"><span data-stu-id="99e2e-125">Azure App Service Web Apps is in General Availability.</span></span></p>
<p><li><span data-ttu-id="99e2e-126"><a href="http://azure.microsoft.com/services/app-service/web/">Web Apps hakkında daha fazla bilgi</a>.</span><span class="sxs-lookup"><span data-stu-id="99e2e-126"><a href="http://azure.microsoft.com/services/app-service/web/">Learn more about Web Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="99e2e-127">Azure Mobile Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="99e2e-127">Azure Mobile Services</span></span></td>
<td align="left"><span data-ttu-id="99e2e-128">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="99e2e-128">Mobile Apps</span></span></td>
<td align="left"><p><li><span data-ttu-id="99e2e-129">Mobile Services bağımsız bir hizmet olarak kullanılabilir ve tam olarak desteklenen kalması için devam edin.</span><span class="sxs-lookup"><span data-stu-id="99e2e-129">Mobile Services continue to be available as a standalone service and remain fully supported.</span></span></p>
<p><li><span data-ttu-id="99e2e-130">Mobile Apps, Mobile Services ve daha fazlasını işlevselliğini tümünün tümleştirir App Service içinde bir uygulama türüdür.</span><span class="sxs-lookup"><span data-stu-id="99e2e-130">Mobile Apps is an app type in App Service, which integrates all of the functionality of Mobile Services and more.</span></span></p>
<p><li><span data-ttu-id="99e2e-131">Kolay <a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">mobil uygulamaları için Mobile Services geçirme</a>.</span><span class="sxs-lookup"><span data-stu-id="99e2e-131">It is easy to <a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrate from Mobile Services to Mobile Apps</a>.</span></span></p>
<p><li><span data-ttu-id="99e2e-132">Uygulama hizmeti bir parçası olarak, Mobile Apps Mobile Services ötesinde şirket içi ve SaaS sistemleri ile tümleştirme gibi yeni özellikler hazırlama yuvaları, Web işleri, daha iyi ölçeklendirme seçenekleri ve daha fazla bilgi alın.</span><span class="sxs-lookup"><span data-stu-id="99e2e-132">As part of App Service, Mobile Apps get new capabilities beyond Mobile Services, such as  integration with on-premises and SaaS systems, staging slots, WebJobs, better scaling options, and more.</span></span></p>
<p><li><span data-ttu-id="99e2e-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Mobile Apps hakkında daha fazla bilgi</a>.</span><span class="sxs-lookup"><span data-stu-id="99e2e-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Learn more about Mobile Apps</a>.</span></span></p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><span data-ttu-id="99e2e-134">API Apps</span><span class="sxs-lookup"><span data-stu-id="99e2e-134">API Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="99e2e-135">API uygulamaları kolayca oluşturmanıza ve bulut API'leri kullanmasına olanak sağlayan bir App Service içinde yeni bir uygulama türüdür.</span><span class="sxs-lookup"><span data-stu-id="99e2e-135">API Apps is a new app type in App Service that lets you easily build and consume APIs in the cloud.</span></span></p>
<p><li><span data-ttu-id="99e2e-136"><a href="http://azure.microsoft.com/services/app-service/api/">API Apps hakkında daha fazla bilgi</a>.</span><span class="sxs-lookup"><span data-stu-id="99e2e-136"><a href="http://azure.microsoft.com/services/app-service/api/">Learn more about API Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><span data-ttu-id="99e2e-137">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="99e2e-137">Logic Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="99e2e-138">Logic Apps, App Service'te kolayca iş süreçlerini otomatikleştirmek olanak sağlayan yeni bir uygulama türüdür.</span><span class="sxs-lookup"><span data-stu-id="99e2e-138">Logic Apps is a new app type in App Service that lets you easily automate business processes.</span></span></p>
<p><li><span data-ttu-id="99e2e-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Logic Apps hakkında daha fazla bilgi</a>.</span><span class="sxs-lookup"><span data-stu-id="99e2e-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Learn more about Logic Apps</a>.</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="99e2e-140">Azure BizTalk Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="99e2e-140">Azure BizTalk Services</span></span></td>
<td align="left"><span data-ttu-id="99e2e-141">BizTalk API uygulamaları</span><span class="sxs-lookup"><span data-stu-id="99e2e-141">BizTalk API Apps</span></span></td>
<td align="left">
<li><p><span data-ttu-id="99e2e-142">BizTalk Services bağımsız bir hizmet olarak kullanılabilir ve tam olarak desteklenen kalması için devam edin.</span><span class="sxs-lookup"><span data-stu-id="99e2e-142">BizTalk Services continue to be available as a standalone service and remain fully supported.</span></span></p>
<li><p><span data-ttu-id="99e2e-143">BizTalk Services tüm özelliklerini uygulama hizmetinde API uygulamaları etkinleştirme kullanıcıların Kurumsal uygulama tümleştirmesi ve uygulama türlerinin herhangi biriyle B2B tümleştirme senaryolarına App Service'te gerçekleştirmesini olarak tümleşiktir.</span><span class="sxs-lookup"><span data-stu-id="99e2e-143">All the capabilities of BizTalk Services are integrated into App Service as API Apps enabling users to perform enterprise application integration and B2B integration scenarios with any of the app types in App Service.</span></span></p>
<li><p><span data-ttu-id="99e2e-144">Logic Apps ile iş süreçlerini iş akışları oluşturmak için bir görsel tasarım deneyimi kullanarak otomatikleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99e2e-144">With Logic Apps, you can now automate business processes using a visual design experience to create workflows.</span></span></p></td>
</tr>
</tbody>
</table>

<span data-ttu-id="99e2e-145">Daha fazla bilgi için lütfen ziyaret [uygulama hizmeti belgeleri](https://azure.microsoft.com/documentation/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="99e2e-145">To learn more, please visit [App Service documentation](https://azure.microsoft.com/documentation/services/app-service/).</span></span>

