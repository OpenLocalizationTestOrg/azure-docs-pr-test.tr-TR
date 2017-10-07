---
title: aaaAzure App Service ve mevcut Azure hizmetlerine etkileri
description: "Açıklayan yeni Azure App Service'nasıl hello ve mevcut Azure hizmetlerinde özelliklerini etkileyebilir."
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
ms.openlocfilehash: a831a88fee38465e5b0b7c2c2340cf8a0d64c864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a><span data-ttu-id="10793-103">Azure Uygulama Hizmeti ve var olan Azure hizmetleri</span><span class="sxs-lookup"><span data-stu-id="10793-103">Azure App Service and existing Azure services</span></span>
<span data-ttu-id="10793-104">Bu makalede Azure Hizmetleri hello değişiklik toobring birlikte bir parçası olarak çeşitli Azure hizmetlerine hello değişiklikleri tooexisting özetlenmektedir [Azure App Service](https://azure.microsoft.com/services/app-service/), yeni bir tümleşik sunum.</span><span class="sxs-lookup"><span data-stu-id="10793-104">This article outlines hello changes tooexisting Azure services as part of hello change toobring together several Azure services into [Azure App Service](https://azure.microsoft.com/services/app-service/), a new integrated offering.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a><span data-ttu-id="10793-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="10793-105">Overview</span></span>
<span data-ttu-id="10793-106">[Azure uygulama hizmeti](https://azure.microsoft.com/services/app-service/) , geliştiricilerin toocreate web ve mobil uygulamaları herhangi bir platform ve herhangi bir aygıt için sağlayan bir yeni ve benzersiz bir bulut hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="10793-106">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a new and unique cloud service that enables developers toocreate web and mobile apps for any platform and any device.</span></span> <span data-ttu-id="10793-107">Kodlama işlevleri tasarlanmış tümleşik bir çözüm toostreamline yinelenen uygulama hizmetidir, kurumsal ve SaaS sistemlerle tümleştirmek ve güvenlik, güvenilirlik ve ölçeklendirilebilirlik, ihtiyaçlarını iş süreçlerini otomatikleştirmek.</span><span class="sxs-lookup"><span data-stu-id="10793-107">App Service is an integrated solution designed toostreamline repeated coding functions, integrate with enterprise and SaaS systems, and automate business processes while meeting your needs for security, reliability, and scalability.</span></span>

<span data-ttu-id="10793-108">Uygulama hizmeti getirir birlikte var olan Azure aşağıdaki hello Hizmetleri - [Web siteleri](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), ve [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) hizmeti, tek bir birleştirilmiş sırada güçlü yeni özellikler ekleme.</span><span class="sxs-lookup"><span data-stu-id="10793-108">App Service brings together hello following existing Azure services - [Websites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), and [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) into a single combined service, while adding powerful new capabilities.</span></span>  <span data-ttu-id="10793-109">Uygulama hizmeti toohost hello şu uygulama türlerini sağlar:</span><span class="sxs-lookup"><span data-stu-id="10793-109">App Service allows you toohost hello following app types:</span></span>

* <span data-ttu-id="10793-110">Web Apps</span><span class="sxs-lookup"><span data-stu-id="10793-110">Web Apps</span></span>
* <span data-ttu-id="10793-111">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="10793-111">Mobile Apps</span></span>
* <span data-ttu-id="10793-112">API Apps</span><span class="sxs-lookup"><span data-stu-id="10793-112">API Apps</span></span>
* <span data-ttu-id="10793-113">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="10793-113">Logic Apps</span></span>

<span data-ttu-id="10793-114">Merhaba aşağıdaki tabloda açıklanmaktadır nasıl mevcut Azure Hizmetleri eşleme tooApp hizmeti ve hello uygulama türleri içinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="10793-114">hello following table explains how existing Azure services map tooApp Service and hello app types available within it.</span></span>

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%"><span data-ttu-id="10793-115">Var olan Azure hizmeti</span><span class="sxs-lookup"><span data-stu-id="10793-115">Existing Azure Service</span></span></th>
<th align="left", style="width:10%"><span data-ttu-id="10793-116">Azure App Service</span><span class="sxs-lookup"><span data-stu-id="10793-116">Azure App Service</span></span></th>
<th align="left", style="width:80%"><span data-ttu-id="10793-117">Neler değişti</span><span class="sxs-lookup"><span data-stu-id="10793-117">What changed</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="10793-118">Azure Web Siteleri</span><span class="sxs-lookup"><span data-stu-id="10793-118">Azure Websites</span></span></td>
<td align="left"><span data-ttu-id="10793-119">Web Apps</span><span class="sxs-lookup"><span data-stu-id="10793-119">Web Apps</span></span></td>
<td align="left"><li><span data-ttu-id="10793-120">Azure Web siteleri için uygulama kesinlikle sınırlı toochanging hello adı Web siteleri tooWeb uygulamaları hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="10793-120">For Azure Websites, App Service is strictly limited toochanging hello name  Websites tooWeb Apps.</span></span>
<p><li><span data-ttu-id="10793-121">Web sitelerinin tüm mevcut örnekleri App Service'te Web uygulamalarını sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="10793-121">All your existing instances of Websites are now Web Apps in App Service.</span></span></p>
<p><li><span data-ttu-id="10793-122">Varolan sitelerinizi hello aracılığıyla erişebilirsiniz <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, altındaki tüm var olan siteler bulacaksınız burada <em>Web Apps</em>.</span><span class="sxs-lookup"><span data-stu-id="10793-122">You can access your existing websites via hello <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, where you will find all your existing sites under <em>Web Apps</em>.</span></span></p>
<p><li><span data-ttu-id="10793-123"><em>Web barındırma planına</em> artık <em>App Service planı</em>.</span><span class="sxs-lookup"><span data-stu-id="10793-123"><em>Web Hosting Plan</em> is now <em>App Service Plan</em>.</span></span> <span data-ttu-id="10793-124">Bir <em>App Service planı</em> uygulama her türlü Web, mobil, mantığı veya API uygulamaları gibi uygulama hizmeti barındırabilir.</span><span class="sxs-lookup"><span data-stu-id="10793-124">An <em>App Service Plan</em> can host any app type of App Service, such as Web, Mobile, Logic, or API apps.</span></span></p>
<p><li><span data-ttu-id="10793-125">Azure App Service Web Apps genel kullanılabilirlik olması.</span><span class="sxs-lookup"><span data-stu-id="10793-125">Azure App Service Web Apps is in General Availability.</span></span></p>
<p><li><span data-ttu-id="10793-126"><a href="http://azure.microsoft.com/services/app-service/web/">Web Apps hakkında daha fazla bilgi</a>.</span><span class="sxs-lookup"><span data-stu-id="10793-126"><a href="http://azure.microsoft.com/services/app-service/web/">Learn more about Web Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="10793-127">Azure Mobile Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="10793-127">Azure Mobile Services</span></span></td>
<td align="left"><span data-ttu-id="10793-128">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="10793-128">Mobile Apps</span></span></td>
<td align="left"><p><li><span data-ttu-id="10793-129">Mobile Services toobe bağımsız bir hizmet olarak kullanılabilir devam etmek ve tam olarak desteklenen kalır.</span><span class="sxs-lookup"><span data-stu-id="10793-129">Mobile Services continue toobe available as a standalone service and remain fully supported.</span></span></p>
<p><li><span data-ttu-id="10793-130">Mobile Apps tüm hello işlevselliğini Mobile Services ve daha fazlasını tümleştirir App Service içinde bir uygulama türüdür.</span><span class="sxs-lookup"><span data-stu-id="10793-130">Mobile Apps is an app type in App Service, which integrates all of hello functionality of Mobile Services and more.</span></span></p>
<p><li><span data-ttu-id="10793-131">Çok kolaydır<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">Mobile Services tooMobile uygulamaları geçiş</a>.</span><span class="sxs-lookup"><span data-stu-id="10793-131">It is easy too<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrate from Mobile Services tooMobile Apps</a>.</span></span></p>
<p><li><span data-ttu-id="10793-132">Uygulama hizmeti bir parçası olarak, Mobile Apps Mobile Services ötesinde şirket içi ve SaaS sistemleri ile tümleştirme gibi yeni özellikler hazırlama yuvaları, Web işleri, daha iyi ölçeklendirme seçenekleri ve daha fazla bilgi alın.</span><span class="sxs-lookup"><span data-stu-id="10793-132">As part of App Service, Mobile Apps get new capabilities beyond Mobile Services, such as  integration with on-premises and SaaS systems, staging slots, WebJobs, better scaling options, and more.</span></span></p>
<p><li><span data-ttu-id="10793-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Mobile Apps hakkında daha fazla bilgi</a>.</span><span class="sxs-lookup"><span data-stu-id="10793-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Learn more about Mobile Apps</a>.</span></span></p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><span data-ttu-id="10793-134">API Apps</span><span class="sxs-lookup"><span data-stu-id="10793-134">API Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="10793-135">API uygulamaları kolayca oluşturmanıza ve hello bulutta API'lerini geliştirmenize olanak sağlayan bir App Service içinde yeni bir uygulama türüdür.</span><span class="sxs-lookup"><span data-stu-id="10793-135">API Apps is a new app type in App Service that lets you easily build and consume APIs in hello cloud.</span></span></p>
<p><li><span data-ttu-id="10793-136"><a href="http://azure.microsoft.com/services/app-service/api/">API Apps hakkında daha fazla bilgi</a>.</span><span class="sxs-lookup"><span data-stu-id="10793-136"><a href="http://azure.microsoft.com/services/app-service/api/">Learn more about API Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><span data-ttu-id="10793-137">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="10793-137">Logic Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="10793-138">Logic Apps, App Service'te kolayca iş süreçlerini otomatikleştirmek olanak sağlayan yeni bir uygulama türüdür.</span><span class="sxs-lookup"><span data-stu-id="10793-138">Logic Apps is a new app type in App Service that lets you easily automate business processes.</span></span></p>
<p><li><span data-ttu-id="10793-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Logic Apps hakkında daha fazla bilgi</a>.</span><span class="sxs-lookup"><span data-stu-id="10793-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Learn more about Logic Apps</a>.</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="10793-140">Azure BizTalk Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="10793-140">Azure BizTalk Services</span></span></td>
<td align="left"><span data-ttu-id="10793-141">BizTalk API uygulamaları</span><span class="sxs-lookup"><span data-stu-id="10793-141">BizTalk API Apps</span></span></td>
<td align="left">
<li><p><span data-ttu-id="10793-142">BizTalk Services toobe bağımsız bir hizmet olarak kullanılabilir devam etmek ve tam olarak desteklenen kalır.</span><span class="sxs-lookup"><span data-stu-id="10793-142">BizTalk Services continue toobe available as a standalone service and remain fully supported.</span></span></p>
<li><p><span data-ttu-id="10793-143">BizTalk Services tüm hello özelliklerini uygulama hizmetinde API uygulamaları etkinleştirme kullanıcıları tooperform Kurumsal uygulama tümleştirmesi ve B2B tümleştirme senaryolarına herhangi biriyle hello App Service'deki uygulama türleri olarak tümleşiktir.</span><span class="sxs-lookup"><span data-stu-id="10793-143">All hello capabilities of BizTalk Services are integrated into App Service as API Apps enabling users tooperform enterprise application integration and B2B integration scenarios with any of hello app types in App Service.</span></span></p>
<li><p><span data-ttu-id="10793-144">Logic Apps ile artık bir görsel tasarım deneyimi toocreate iş akışlarını kullanarak iş süreçlerini otomatik hale getirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="10793-144">With Logic Apps, you can now automate business processes using a visual design experience toocreate workflows.</span></span></p></td>
</tr>
</tbody>
</table>

<span data-ttu-id="10793-145">toolearn daha, lütfen şu adresi ziyaret [uygulama hizmeti belgeleri](https://azure.microsoft.com/documentation/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="10793-145">toolearn more, please visit [App Service documentation](https://azure.microsoft.com/documentation/services/app-service/).</span></span>

