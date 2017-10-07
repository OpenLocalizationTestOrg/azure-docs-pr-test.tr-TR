---
title: Azure ile New Relic aaaUsing | Microsoft Docs
description: "Nasıl toouse New Relic hizmet toomanage hello ve Azure uygulamanızı izlemek öğrenin."
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
ms.openlocfilehash: 81e5f1b694264e3586ac75d40edd8afe185493d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="new-relic-application-performance-management-on-azure"></a><span data-ttu-id="420a8-103">Azure üzerinde yeni Relic uygulama performans yönetimi</span><span class="sxs-lookup"><span data-stu-id="420a8-103">New Relic Application Performance Management on Azure</span></span>
<span data-ttu-id="420a8-104">New Relic'ın dünya çapındaki performans ekleyebilirsiniz tooyour izleme Azure barındırılan uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="420a8-104">You can add New Relic's world-class performance monitoring tooyour Azure hosted applications.</span></span> <span data-ttu-id="420a8-105">İzleme, sorun giderme ve Azure uygulamalarınızı ayarlama için kapsamlı özellikler yanı sıra, ayrıca Azure kullanarak bir indirimli fiyat New Relic ürünleri için uygundur.</span><span class="sxs-lookup"><span data-stu-id="420a8-105">Along with comprehensive capabilities for monitoring, troubleshooting, and tuning your Azure apps, you are also eligible for a discounted price for New Relic products by using Azure.</span></span>

## <a name="what-is-new-relic"></a><span data-ttu-id="420a8-106">New Relic nedir?</span><span class="sxs-lookup"><span data-stu-id="420a8-106">What is New Relic?</span></span>
<span data-ttu-id="420a8-107">İle [New Relic ürünleri](https://newrelic.com/products), uygulama hataları gidermek, olası sorunları öncesinde kalır ve tüm ortamınız hello performansını anlamak.</span><span class="sxs-lookup"><span data-stu-id="420a8-107">With [New Relic products](https://newrelic.com/products), you can solve app errors, stay ahead of potential issues, and understand hello performance of your entire environment.</span></span> <span data-ttu-id="420a8-108">Tanımlama ve performans sorunlarını tanılama zaman tasarlanmış toosave olduğunu ve bu sorunları toosolve parmaklarınızın ucunda gereksinim hello bilgileri koyar.</span><span class="sxs-lookup"><span data-stu-id="420a8-108">It is designed toosave you time when identifying and diagnosing performance issues, and it puts hello information you need toosolve these issues at your fingertips.</span></span>

<span data-ttu-id="420a8-109">Yeni Relic parçaları hello saat ve web işlemleri, hem hello sunucusuna gelen ve kullanıcılarınızın tarayıcılarda verimliliğini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="420a8-109">New Relic tracks hello load time and throughput for your web transactions, both from hello server and your users' browsers.</span></span> <span data-ttu-id="420a8-110">Merhaba veritabanında harcadığınız ne kadar süre yavaş sorguları analiz eder ve web istekleri, çalışma süresini izleme ve uyarı, parçaları uygulama özel durumları ve tüm çok daha fazla sağlayan gösterir.</span><span class="sxs-lookup"><span data-stu-id="420a8-110">It shows how much time you spend in hello database, analyzes slow queries and web requests, provides uptime monitoring and alerting, tracks application exceptions, and a whole lot more.</span></span> 

## <a name="special-pricing"></a><span data-ttu-id="420a8-111">Özel fiyatlandırma</span><span class="sxs-lookup"><span data-stu-id="420a8-111">Special pricing</span></span>
<span data-ttu-id="420a8-112">Yeni Relic standart ücretsiz tooAzure kullanıcı sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="420a8-112">New Relic Standard is free tooAzure users.</span></span> <span data-ttu-id="420a8-113">Yeni Relic Pro örnek boyutu dayanarak Azure bulut hizmetlerini sunulur.</span><span class="sxs-lookup"><span data-stu-id="420a8-113">New Relic Pro is offered based on instance size for Azure Cloud Services.</span></span> <span data-ttu-id="420a8-114">Merhaba fiyatlandırma bilgileri için bkz: [New Relic sayfa](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) içinde Azure Marketi hello veya New Relic başvurun (sales@newrelic.com) kuruluş düzeyinde fiyatlandırma için.</span><span class="sxs-lookup"><span data-stu-id="420a8-114">For pricing information, see hello [New Relic page](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) in hello Azure Marketplace or contact New Relic (sales@newrelic.com) for enterprise-level pricing.</span></span>

<span data-ttu-id="420a8-115">Merhaba New Relic Aracısı dağıttığınızda azure müşterilerine yeni Relic Pro, iki hafta deneme aboneliği alırsınız.</span><span class="sxs-lookup"><span data-stu-id="420a8-115">Azure customers receive a two week trial subscription of New Relic Pro when they deploy hello New Relic agent.</span></span>

## <a name="sign-up-for-new-relic-using-hello-azure-store"></a><span data-ttu-id="420a8-116">New Relic hello Azure deposu kullanmak için kaydolun</span><span class="sxs-lookup"><span data-stu-id="420a8-116">Sign up for New Relic using hello Azure Store</span></span>
<span data-ttu-id="420a8-117">New Relic Azure Web rolleri ve çalışan rolleri ile sorunsuz şekilde entegre olur.</span><span class="sxs-lookup"><span data-stu-id="420a8-117">New Relic integrates seamlessly with Azure Web Roles and Worker roles.</span></span> <span data-ttu-id="420a8-118">Hızlı bir şekilde ve kolayca doğrudan hello Azure Mağazası ' New Relic için kaydolun.</span><span class="sxs-lookup"><span data-stu-id="420a8-118">You can quickly and easily sign up for New Relic directly from hello Azure Store.</span></span> <span data-ttu-id="420a8-119">Merhaba yönergeler için bkz [Azure depolama kayıt yönergelerini](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) New Relic gelen.</span><span class="sxs-lookup"><span data-stu-id="420a8-119">For instructions, see hello [Azure store sign-up instructions](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) from New Relic.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="420a8-120">Verilerinizi görüntüleme</span><span class="sxs-lookup"><span data-stu-id="420a8-120">View your data</span></span>
<span data-ttu-id="420a8-121">Oturum açtığınız sonra New Relic'ın inanılmaz uygulama izleme ve veri odaklı analiz yararlanabilir.</span><span class="sxs-lookup"><span data-stu-id="420a8-121">Once you've signed up, you can take advantage of New Relic's amazing application monitoring and data-driven analysis.</span></span> <span data-ttu-id="420a8-122">toocheck New Relic, uygulamanızın performansını:</span><span class="sxs-lookup"><span data-stu-id="420a8-122">toocheck your app's performance in New Relic:</span></span>

1. <span data-ttu-id="420a8-123">Hello Azure Portalı ' Yönet'i seçin.</span><span class="sxs-lookup"><span data-stu-id="420a8-123">From hello Azure Portal, select Manage.</span></span>
2. <span data-ttu-id="420a8-124">New Relic hesabı e-posta ve parola ile oturum açın.</span><span class="sxs-lookup"><span data-stu-id="420a8-124">Sign in with your New Relic account email and password.</span></span>
3. <span data-ttu-id="420a8-125">Uygulamanızı hello uygulama dizini tooview tüm uygulamanızın veri hello seçin [APM genel bakış sayfasında](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page).</span><span class="sxs-lookup"><span data-stu-id="420a8-125">Select your app from hello Application index tooview all your app's data in hello [APM overview page](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page).</span></span>

## <a name="using-new-relic-with-azure"></a><span data-ttu-id="420a8-126">New Relic Azure ile kullanma</span><span class="sxs-lookup"><span data-stu-id="420a8-126">Using New Relic with Azure</span></span>
<span data-ttu-id="420a8-127">New Relic ve Azure kullanma hakkında daha fazla bilgi için bkz: [New Relic'ın belgeleri sitesi](https://docs.newrelic.com/docs/agents/net-agent/azure-installation)dahil:</span><span class="sxs-lookup"><span data-stu-id="420a8-127">For more information about using New Relic and Azure, see [New Relic's Documentation site](https://docs.newrelic.com/docs/agents/net-agent/azure-installation), including:</span></span> 

* [<span data-ttu-id="420a8-128">New Relic .NET için</span><span class="sxs-lookup"><span data-stu-id="420a8-128">New Relic for .NET</span></span>](https://docs.newrelic.com/docs/agents/net-agent/getting-started/new-relic-net)
* [<span data-ttu-id="420a8-129">Azure bulut hizmetindeki .NET çalışan rolü izleme</span><span class="sxs-lookup"><span data-stu-id="420a8-129">Instrument a .NET Worker Role on Azure Cloud service</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/instrument-net-worker-role-azure-cloud-service)
* [<span data-ttu-id="420a8-130">New Relic hello Microsoft Azure bulut platformu</span><span class="sxs-lookup"><span data-stu-id="420a8-130">New Relic for hello Microsoft Azure Cloud platform</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services)
* [<span data-ttu-id="420a8-131">New Relic hello Microsoft Azure App Services için</span><span class="sxs-lookup"><span data-stu-id="420a8-131">New Relic for hello Microsoft Azure App Services</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-portal)
* [<span data-ttu-id="420a8-132">Yeni Relic/Azure sorun giderme</span><span class="sxs-lookup"><span data-stu-id="420a8-132">New Relic/Azure troubleshooting</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-troubleshooting)

