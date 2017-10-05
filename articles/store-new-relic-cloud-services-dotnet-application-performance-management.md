---
title: New Relic Azure ile kullanma | Microsoft Docs
description: "New Relic hizmetine Azure uygulamanızı izlemek ve yönetmek için kullanmayı öğrenin."
services: 
documentationcenter: .net
author: nickfloyd
manager: timlt
editor: 
ms.assetid: b01011be-c344-4e33-987d-c93dac1971fb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2016
ms.author: nickfloyd@newrelic.com
ms.openlocfilehash: f4f13c909a6ff640d403f5264004176c087925dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="new-relic-application-performance-management-on-azure"></a><span data-ttu-id="c8abd-103">Azure üzerinde yeni Relic uygulama performans yönetimi</span><span class="sxs-lookup"><span data-stu-id="c8abd-103">New Relic Application Performance Management on Azure</span></span>
<span data-ttu-id="c8abd-104">New Relic'ın dünya çapındaki performans ekleyebilirsiniz barındırılan uygulamalar için Azure izleme.</span><span class="sxs-lookup"><span data-stu-id="c8abd-104">You can add New Relic's world-class performance monitoring to your Azure hosted applications.</span></span> <span data-ttu-id="c8abd-105">İzleme, sorun giderme ve Azure uygulamalarınızı ayarlama için kapsamlı özellikler yanı sıra, ayrıca Azure kullanarak bir indirimli fiyat New Relic ürünleri için uygundur.</span><span class="sxs-lookup"><span data-stu-id="c8abd-105">Along with comprehensive capabilities for monitoring, troubleshooting, and tuning your Azure apps, you are also eligible for a discounted price for New Relic products by using Azure.</span></span>

## <a name="what-is-new-relic"></a><span data-ttu-id="c8abd-106">New Relic nedir?</span><span class="sxs-lookup"><span data-stu-id="c8abd-106">What is New Relic?</span></span>
<span data-ttu-id="c8abd-107">İle [New Relic ürünleri](https://newrelic.com/products), uygulama hataları gidermek, olası sorunları öncesinde kalır ve tüm ortamınız performansını anlamak.</span><span class="sxs-lookup"><span data-stu-id="c8abd-107">With [New Relic products](https://newrelic.com/products), you can solve app errors, stay ahead of potential issues, and understand the performance of your entire environment.</span></span> <span data-ttu-id="c8abd-108">Performans sorunlarını belirler ve tanılarken size zaman kazandırmak için tasarlanmıştır ve bu sorunları çözmek için gereken verileri parmaklarınızın ucuna kadar getirir.</span><span class="sxs-lookup"><span data-stu-id="c8abd-108">It is designed to save you time when identifying and diagnosing performance issues, and it puts the information you need to solve these issues at your fingertips.</span></span>

<span data-ttu-id="c8abd-109">New Relic yükleme süresini ve web işlemleri, hem sunucu ve kullanıcılarınızın tarayıcılarda verimliliğini izler.</span><span class="sxs-lookup"><span data-stu-id="c8abd-109">New Relic tracks the load time and throughput for your web transactions, both from the server and your users' browsers.</span></span> <span data-ttu-id="c8abd-110">Veritabanında harcadığınız ne kadar süre yavaş sorguları analiz eder ve web istekleri, çalışma süresini izleme ve uyarı, parçaları uygulama özel durumları ve tüm çok daha fazla sağlayan gösterir.</span><span class="sxs-lookup"><span data-stu-id="c8abd-110">It shows how much time you spend in the database, analyzes slow queries and web requests, provides uptime monitoring and alerting, tracks application exceptions, and a whole lot more.</span></span> 

## <a name="special-pricing"></a><span data-ttu-id="c8abd-111">Özel fiyatlandırma</span><span class="sxs-lookup"><span data-stu-id="c8abd-111">Special pricing</span></span>
<span data-ttu-id="c8abd-112">Yeni Relic standart Azure kullanıcılara ücretsizdir.</span><span class="sxs-lookup"><span data-stu-id="c8abd-112">New Relic Standard is free to Azure users.</span></span> <span data-ttu-id="c8abd-113">Yeni Relic Pro örnek boyutu dayanarak Azure bulut hizmetlerini sunulur.</span><span class="sxs-lookup"><span data-stu-id="c8abd-113">New Relic Pro is offered based on instance size for Azure Cloud Services.</span></span> <span data-ttu-id="c8abd-114">Fiyatlandırma bilgileri için bkz: [New Relic sayfa](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) Azure Marketi veya kişi New Relic (sales@newrelic.com) kuruluş düzeyinde fiyatlandırma için.</span><span class="sxs-lookup"><span data-stu-id="c8abd-114">For pricing information, see the [New Relic page](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) in the Azure Marketplace or contact New Relic (sales@newrelic.com) for enterprise-level pricing.</span></span>

<span data-ttu-id="c8abd-115">New Relic Aracısı dağıttığınızda azure müşterilerine yeni Relic Pro, iki hafta deneme aboneliği alırsınız.</span><span class="sxs-lookup"><span data-stu-id="c8abd-115">Azure customers receive a two week trial subscription of New Relic Pro when they deploy the New Relic agent.</span></span>

## <a name="sign-up-for-new-relic-using-the-azure-store"></a><span data-ttu-id="c8abd-116">New Relic Azure deposu kullanmak için kaydolun</span><span class="sxs-lookup"><span data-stu-id="c8abd-116">Sign up for New Relic using the Azure Store</span></span>
<span data-ttu-id="c8abd-117">New Relic Azure Web rolleri ve çalışan rolleri ile sorunsuz şekilde entegre olur.</span><span class="sxs-lookup"><span data-stu-id="c8abd-117">New Relic integrates seamlessly with Azure Web Roles and Worker roles.</span></span> <span data-ttu-id="c8abd-118">Hızlı bir şekilde ve kolayca doğrudan Azure Mağazası'ndan New Relic kaydolun.</span><span class="sxs-lookup"><span data-stu-id="c8abd-118">You can quickly and easily sign up for New Relic directly from the Azure Store.</span></span> <span data-ttu-id="c8abd-119">Yönergeler için bkz: [Azure depolama kayıt yönergelerini](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) New Relic gelen.</span><span class="sxs-lookup"><span data-stu-id="c8abd-119">For instructions, see the [Azure store sign-up instructions](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) from New Relic.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="c8abd-120">Verilerinizi görüntüleme</span><span class="sxs-lookup"><span data-stu-id="c8abd-120">View your data</span></span>
<span data-ttu-id="c8abd-121">Oturum açtığınız sonra New Relic'ın inanılmaz uygulama izleme ve veri odaklı analiz yararlanabilir.</span><span class="sxs-lookup"><span data-stu-id="c8abd-121">Once you've signed up, you can take advantage of New Relic's amazing application monitoring and data-driven analysis.</span></span> <span data-ttu-id="c8abd-122">New Relic, uygulamanızın performansını denetlemek için:</span><span class="sxs-lookup"><span data-stu-id="c8abd-122">To check your app's performance in New Relic:</span></span>

1. <span data-ttu-id="c8abd-123">Azure Portalı'ndan Yönet'i seçin.</span><span class="sxs-lookup"><span data-stu-id="c8abd-123">From the Azure Portal, select Manage.</span></span>
2. <span data-ttu-id="c8abd-124">New Relic hesabı e-posta ve parola ile oturum açın.</span><span class="sxs-lookup"><span data-stu-id="c8abd-124">Sign in with your New Relic account email and password.</span></span>
3. <span data-ttu-id="c8abd-125">Tüm uygulama verileri görüntülemek için uygulama dizinden uygulamanızı seçin [APM genel bakış sayfasında](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page).</span><span class="sxs-lookup"><span data-stu-id="c8abd-125">Select your app from the Application index to view all your app's data in the [APM overview page](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page).</span></span>

## <a name="using-new-relic-with-azure"></a><span data-ttu-id="c8abd-126">New Relic Azure ile kullanma</span><span class="sxs-lookup"><span data-stu-id="c8abd-126">Using New Relic with Azure</span></span>
<span data-ttu-id="c8abd-127">New Relic ve Azure kullanma hakkında daha fazla bilgi için bkz: [New Relic'ın belgeleri sitesi](https://docs.newrelic.com/docs/agents/net-agent/azure-installation)dahil:</span><span class="sxs-lookup"><span data-stu-id="c8abd-127">For more information about using New Relic and Azure, see [New Relic's Documentation site](https://docs.newrelic.com/docs/agents/net-agent/azure-installation), including:</span></span> 

* [<span data-ttu-id="c8abd-128">New Relic .NET için</span><span class="sxs-lookup"><span data-stu-id="c8abd-128">New Relic for .NET</span></span>](https://docs.newrelic.com/docs/agents/net-agent/getting-started/new-relic-net)
* [<span data-ttu-id="c8abd-129">Azure bulut hizmetindeki .NET çalışan rolü izleme</span><span class="sxs-lookup"><span data-stu-id="c8abd-129">Instrument a .NET Worker Role on Azure Cloud service</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/instrument-net-worker-role-azure-cloud-service)
* [<span data-ttu-id="c8abd-130">Microsoft Azure bulut platformu için New Relic</span><span class="sxs-lookup"><span data-stu-id="c8abd-130">New Relic for the Microsoft Azure Cloud platform</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services)
* [<span data-ttu-id="c8abd-131">Microsoft Azure uygulaması için New Relic Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="c8abd-131">New Relic for the Microsoft Azure App Services</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-portal)
* [<span data-ttu-id="c8abd-132">Yeni Relic/Azure sorun giderme</span><span class="sxs-lookup"><span data-stu-id="c8abd-132">New Relic/Azure troubleshooting</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-troubleshooting)

