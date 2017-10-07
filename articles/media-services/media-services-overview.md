---
title: "aaaAzure Media Services genel bakış | Microsoft Docs"
description: "Bu konu Azure Media Services’e genel bir bakış sağlar."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 7a5e9723-c379-446b-b4d6-d0e41bd7d31f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/04/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 81f9f4d9ff75effea30c10fd09449e9d2025f377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-overview"></a><span data-ttu-id="3ab91-103">Azure Media Services’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="3ab91-103">Azure Media Services overview</span></span> 

<span data-ttu-id="3ab91-104">Microsoft Azure Media Services, geliştiricilerin, toobuild ölçeklenebilir medya yönetimi ve teslimi uygulamaları sağlayan genişletilebilir bulut tabanlı bir platformdur.</span><span class="sxs-lookup"><span data-stu-id="3ab91-104">Microsoft Azure Media Services is an extensible cloud-based platform that enables developers toobuild scalable media management and delivery applications.</span></span> <span data-ttu-id="3ab91-105">Media Services toosecurely karşıya yükleme sağlayan REST API'leri dayanır, depolamak, kodlamak ve video ve ses içeriklerini hem isteğe bağlı ve canlı akış teslimi toovarious istemcileri için (örneğin, TV, PC ve mobil aygıtlar) paketi.</span><span class="sxs-lookup"><span data-stu-id="3ab91-105">Media Services is based on REST APIs that enable you toosecurely upload, store, encode, and package video or audio content for both on-demand and live streaming delivery toovarious clients (for example, TV, PC, and mobile devices).</span></span>

<span data-ttu-id="3ab91-106">Yalnızca Media Services’i kullanarak uçtan uca iş akışları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ab91-106">You can build end-to-end workflows using entirely Media Services.</span></span> <span data-ttu-id="3ab91-107">Ayrıca, iş akışınızın bazı bölümleri için üçüncü taraf bileşenleri toouse da tercih edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ab91-107">You can also choose toouse third-party components for some parts of your workflow.</span></span> <span data-ttu-id="3ab91-108">Örneğin, bir üçüncü taraf kodlayıcısı kullanarak kodlayın.</span><span class="sxs-lookup"><span data-stu-id="3ab91-108">For example, encode using a third-party encoder.</span></span> <span data-ttu-id="3ab91-109">Daha sonra Media Services’i kullanarak yükleyin, koruyun, paketleyin ve teslim edin.</span><span class="sxs-lookup"><span data-stu-id="3ab91-109">Then, upload, protect, package, deliver using Media Services.</span></span>

<span data-ttu-id="3ab91-110">İçeriğinizi Canlı toostream seçin veya isteğe bağlı içerik teslim.</span><span class="sxs-lookup"><span data-stu-id="3ab91-110">You can choose toostream your content live or deliver content on-demand.</span></span> <span data-ttu-id="3ab91-111">Merhaba konu aynı zamanda tooother ilgili konulara bağlantılar içerir.</span><span class="sxs-lookup"><span data-stu-id="3ab91-111">hello topic also links tooother relevant topics.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="3ab91-112">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="3ab91-112">Media Services learning paths</span></span>
<span data-ttu-id="3ab91-113">AMS öğrenme yollarını burada görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3ab91-113">You can view AMS learning paths here:</span></span>

* [<span data-ttu-id="3ab91-114">AMS Canlı Akış İş Akışı</span><span class="sxs-lookup"><span data-stu-id="3ab91-114">AMS Live Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-live/)
* [<span data-ttu-id="3ab91-115">AMS İsteğe Bağlı Akış İş Akışı</span><span class="sxs-lookup"><span data-stu-id="3ab91-115">AMS on-Demand Streaming Workflow</span></span>](https://azure.microsoft.com/documentation/learning-paths/media-services-streaming-on-demand/)

## <a name="prerequisites"></a><span data-ttu-id="3ab91-116">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3ab91-116">Prerequisites</span></span>

<span data-ttu-id="3ab91-117">Azure Media Services'i kullanarak toostart hello şunlara sahip olmanız:</span><span class="sxs-lookup"><span data-stu-id="3ab91-117">toostart using Azure Media Services, you should have hello following:</span></span>

* <span data-ttu-id="3ab91-118">Bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="3ab91-118">An Azure account.</span></span> <span data-ttu-id="3ab91-119">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3ab91-119">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="3ab91-120">Ayrıntılar için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="3ab91-120">For details, see [Azure Free Trial](https://azure.microsoft.com).</span></span>
* <span data-ttu-id="3ab91-121">Bir Azure Media Services hesabı.</span><span class="sxs-lookup"><span data-stu-id="3ab91-121">An Azure Media Services account.</span></span> <span data-ttu-id="3ab91-122">Daha fazla bilgi için bkz. [Hesap Oluşturma](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="3ab91-122">For more information, see [Create Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="3ab91-123">(İsteğe bağlı) Geliştirme ortamı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3ab91-123">(Optional) Set up development environment.</span></span> <span data-ttu-id="3ab91-124">Geliştirme ortamınız için .NET veya REST API’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="3ab91-124">Choose .NET or REST API for your development environment.</span></span> <span data-ttu-id="3ab91-125">Daha fazla bilgi için bkz. [Ortam Ayarlama](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="3ab91-125">For more information, see [Set up environment](media-services-dotnet-how-to-use.md).</span></span>

    <span data-ttu-id="3ab91-126">Ayrıca, nasıl çok bilgi[tooAMS API program aracılığıyla bağlanma](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="3ab91-126">Also, learn how too[connect  programmatically tooAMS API](media-services-use-aad-auth-to-access-ams-api.md).</span></span>
* <span data-ttu-id="3ab91-127">Standart veya premium akış uç noktası başlatılmış durumda.</span><span class="sxs-lookup"><span data-stu-id="3ab91-127">A standard or premium streaming endpoint in started state.</span></span>  <span data-ttu-id="3ab91-128">Daha fazla bilgi için bkz. [Akış uç noktalarını yönetme](media-services-portal-manage-streaming-endpoints.md)</span><span class="sxs-lookup"><span data-stu-id="3ab91-128">For more information, see [Managing streaming endpoints](media-services-portal-manage-streaming-endpoints.md)</span></span>

## <a name="sdks-and-tools"></a><span data-ttu-id="3ab91-129">SDK’lar ve araçlar</span><span class="sxs-lookup"><span data-stu-id="3ab91-129">SDKs and tools</span></span>

<span data-ttu-id="3ab91-130">toobuild Media Services çözümleri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3ab91-130">toobuild Media Services solutions, you can use:</span></span>

* [<span data-ttu-id="3ab91-131">Media Services REST API'si</span><span class="sxs-lookup"><span data-stu-id="3ab91-131">Media Services REST API</span></span>](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)
* <span data-ttu-id="3ab91-132">Merhaba kullanılabilir istemci SDK'ları biri:</span><span class="sxs-lookup"><span data-stu-id="3ab91-132">One of hello available client SDKs:</span></span>
    * <span data-ttu-id="3ab91-133">[.NET için Azure Media Services SDK](https://github.com/Azure/azure-sdk-for-media-services),</span><span class="sxs-lookup"><span data-stu-id="3ab91-133">[Azure Media Services SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services),</span></span>
    * <span data-ttu-id="3ab91-134">[Java için Azure SDK](https://github.com/Azure/azure-sdk-for-java),</span><span class="sxs-lookup"><span data-stu-id="3ab91-134">[Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java),</span></span>
    * <span data-ttu-id="3ab91-135">[Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php),</span><span class="sxs-lookup"><span data-stu-id="3ab91-135">[Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php),</span></span>
    * <span data-ttu-id="3ab91-136">[Node.js için Azure Media Services](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (Bu, Microsoft dışı bir Node.js SDK sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="3ab91-136">[Azure Media Services for Node.js](https://github.com/michelle-becker/node-ams-sdk/blob/master/lib/request.js) (This is a non-Microsoft version of a Node.js SDK.</span></span> <span data-ttu-id="3ab91-137">Bu topluluk tarafından korunur ve şu anda hello AMS API'lerinin % 100 kapsamını yok).</span><span class="sxs-lookup"><span data-stu-id="3ab91-137">It is maintained by a community and currently does not have a 100% coverage of hello AMS APIs).</span></span>
* <span data-ttu-id="3ab91-138">Mevcut araçlar:</span><span class="sxs-lookup"><span data-stu-id="3ab91-138">Existing tools:</span></span>
    * [<span data-ttu-id="3ab91-139">Azure portal</span><span class="sxs-lookup"><span data-stu-id="3ab91-139">Azure portal</span></span>](https://portal.azure.com/)
    * <span data-ttu-id="3ab91-140">[Azure-Media-Services-Gezgini](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure Media Services Gezgini (AMSE), Windows için bir Winforms/C# uygulamasıdır)</span><span class="sxs-lookup"><span data-stu-id="3ab91-140">[Azure-Media-Services-Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (Azure Media Services Explorer (AMSE) is a Winforms/C# application for Windows)</span></span>

## <a name="concepts-and-overview"></a><span data-ttu-id="3ab91-141">Kavramlar ve genel bakış</span><span class="sxs-lookup"><span data-stu-id="3ab91-141">Concepts and overview</span></span>
<span data-ttu-id="3ab91-142">Azure Media Services kavramları hakkında bilgi edinmek için bkz. [Kavramlar](media-services-concepts.md).</span><span class="sxs-lookup"><span data-stu-id="3ab91-142">For Azure Media Services concepts, see [Concepts](media-services-concepts.md).</span></span>

<span data-ttu-id="3ab91-143">Bir nasıl-tooall hello ana bileşenlerinin Azure Media Services tanıtan tooseries için bkz: [Azure Media Services adım adım öğreticiler](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series).</span><span class="sxs-lookup"><span data-stu-id="3ab91-143">For a how-tooseries that introduces you tooall hello main components of Azure Media Services, see [Azure Media Services Step-by-Step tutorials](https://docs.com/fukushima-shigeyuki/3439/english-azure-media-services-step-by-step-series).</span></span> <span data-ttu-id="3ab91-144">Bu seri kavramları harika bir genel bakış vardır ve hello AMSE aracını toodemonstrate AMS görevler kullanır.</span><span class="sxs-lookup"><span data-stu-id="3ab91-144">This series has a great overview of concepts and it uses hello AMSE tool toodemonstrate AMS tasks.</span></span> <span data-ttu-id="3ab91-145">AMSE aracı bir Windows aracıdır.</span><span class="sxs-lookup"><span data-stu-id="3ab91-145">AMSE tool is a Windows tool.</span></span> <span data-ttu-id="3ab91-146">Bu araç, programlama aracılığıyla elde edebileceğiniz ile Merhaba görevlerin çoğunu destekler [.NET için AMS SDK](https://github.com/Azure/azure-sdk-for-media-services), [Java için Azure SDK](https://github.com/Azure/azure-sdk-for-java), veya [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php).</span><span class="sxs-lookup"><span data-stu-id="3ab91-146">This tool supports most of hello tasks you can achieve programmatically with [AMS SDK for .NET](https://github.com/Azure/azure-sdk-for-media-services), [Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java), or  [Azure PHP SDK](https://github.com/Azure/azure-sdk-for-php).</span></span>

## <a name="supported-scenarios-and-availability-of-media-services-across-data-centers"></a><span data-ttu-id="3ab91-147">Desteklenen senaryolar ve veri merkezleri arasında Media Services kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="3ab91-147">Supported scenarios and availability of Media Services across data centers</span></span>

<span data-ttu-id="3ab91-148">Ayrıntılı bilgi için bkz. [AMS senaryoları ve veri merkezleri arasında özelliklerin ve hizmetlerin kullanılabilirliği](scenarios-and-availability.md).</span><span class="sxs-lookup"><span data-stu-id="3ab91-148">For detailed information, see [AMS scenarios and availability of features and services across data centers](scenarios-and-availability.md).</span></span>

## <a name="service-level-agreement-sla"></a><span data-ttu-id="3ab91-149">Hizmet Düzeyi Sözleşmesi (SLA)</span><span class="sxs-lookup"><span data-stu-id="3ab91-149">Service Level Agreement (SLA)</span></span>

* <span data-ttu-id="3ab91-150">Media Services Kodlama için, REST API işlemlerinin %99,9 kullanılabilirliğini garanti ediyoruz.</span><span class="sxs-lookup"><span data-stu-id="3ab91-150">For Media Services Encoding, we guarantee 99.9% availability of REST API transactions.</span></span>
* <span data-ttu-id="3ab91-151">Akış için, standart veya premium akış uç noktası satın alındığında mevcut medya içeriğinin %99,9 kullanılabilirliği garantisi ile isteklere başarıyla hizmet vereceğiz.</span><span class="sxs-lookup"><span data-stu-id="3ab91-151">For Streaming, we will successfully service requests with a 99.9% availability guarantee for existing media content when a standard or premium streaming endpoint is purchased.</span></span>
* <span data-ttu-id="3ab91-152">Canlı kanallar için çalışan harici bağlantı hello süre en az % 99,9 sahip olma olasılığı garanti ediyoruz.</span><span class="sxs-lookup"><span data-stu-id="3ab91-152">For Live Channels, we guarantee that running Channels will have external connectivity at least 99.9% of hello time.</span></span>
* <span data-ttu-id="3ab91-153">İçerik koruma için biz biz başarıyla önemli istekleri en az başlangıç saati % 99,9 oranda karşılayacağımızı garanti ediyoruz.</span><span class="sxs-lookup"><span data-stu-id="3ab91-153">For Content Protection, we guarantee that we will successfully fulfill key requests at least 99.9% of hello time.</span></span>
* <span data-ttu-id="3ab91-154">Dizin Oluşturucu için başarıyla bir kodlamaya ayrılan ile işlenen dizin oluşturucu görevi isteklerine hizmet vereceğiz birim başlangıç saati % 99,9 oranda.</span><span class="sxs-lookup"><span data-stu-id="3ab91-154">For Indexer, we will successfully service Indexer Task requests processed with an Encoding Reserved Unit 99.9% of hello time.</span></span>

<span data-ttu-id="3ab91-155">Daha fazla bilgi için bkz. [Microsoft Azure SLA](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="3ab91-155">For more information, see [Microsoft Azure SLA](https://azure.microsoft.com/support/legal/sla/).</span></span>

<span data-ttu-id="3ab91-156">Merhaba veri merkezlerinde kullanılabilirliği hakkında daha fazla bilgi için bkz [Avaiability](scenarios-and-availability.md#availability) bölümü.</span><span class="sxs-lookup"><span data-stu-id="3ab91-156">For information about availability in datacenters, see hello [Avaiability](scenarios-and-availability.md#availability) section.</span></span>

## <a name="support"></a><span data-ttu-id="3ab91-157">Destek</span><span class="sxs-lookup"><span data-stu-id="3ab91-157">Support</span></span>

<span data-ttu-id="3ab91-158">[Azure Desteği](https://azure.microsoft.com/support/options/), Media Services de dahil olmak üzere Azure için destek seçenekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="3ab91-158">[Azure Support](https://azure.microsoft.com/support/options/) provides support options for Azure, including Media Services.</span></span>

## <a name="provide-feedback"></a><span data-ttu-id="3ab91-159">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="3ab91-159">Provide feedback</span></span>

[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
