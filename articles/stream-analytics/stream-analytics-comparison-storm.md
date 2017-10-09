---
title: "Analytics platformları: Apache Storm karşılaştırma tooStream Analytics | Microsoft Docs"
description: "Apache Storm karşılaştırma tooStream analizi kullanarak bulut analizi platformu seçme kılavuzu edinin. Özellikler ve farklar anlayın."
keywords: "Analiz platformu analytics platformları, bulut analizi platformu, storm karşılaştırma"
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: b9aac017-9866-4d0a-b98f-6f03881e9339
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/27/2017
ms.author: samacha
ms.openlocfilehash: 5a0ec5b2439596f0da962f04b776472031660062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="choosing-a-streaming-analytics-platform-comparing-apache-storm-and-azure-stream-analytics"></a><span data-ttu-id="1f50f-105">Akış analizi platformu seçme: Apache Storm ve Azure akış analizi karşılaştırma</span><span class="sxs-lookup"><span data-stu-id="1f50f-105">Choosing a streaming analytics platform: comparing Apache Storm and Azure Stream Analytics</span></span>
<span data-ttu-id="1f50f-106">Azure veri akışı çözümleme için birden çok çözümü sağlar: [Azure akış analizi](https://docs.microsoft.com/azure/stream-analytics/) ve [Azure hdınsight'ta Apache Storm](https://azure.microsoft.com/services/hdinsight/apache-storm/).</span><span class="sxs-lookup"><span data-stu-id="1f50f-106">Azure provides multiple solutions for analyzing streaming data: [Azure Streaming Analytics](https://docs.microsoft.com/azure/stream-analytics/) and [Apache Storm on Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-storm/).</span></span> <span data-ttu-id="1f50f-107">Her iki analytics platformları bir PaaS çözümün hello fayda sağlar.</span><span class="sxs-lookup"><span data-stu-id="1f50f-107">Both analytics platforms provide hello benefits of a PaaS solution.</span></span> <span data-ttu-id="1f50f-108">Ancak hello platformları nasıl yapılandırmak ve bunları yönetmek gibi yeteneklerini de önemli farklılıklar vardır.</span><span class="sxs-lookup"><span data-stu-id="1f50f-108">But hello platforms have some significant differences in their capabilities as well as in how you configure and manage them.</span></span> 

<span data-ttu-id="1f50f-109">Bu makale, Apache Storm ve Azure akış analizi bulut analizi platformu olarak arasında seçim özellikleri toohelp yan yana karşılaştırmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="1f50f-109">This article provides a side-by-side comparison of features toohelp you choose between Apache Storm and Azure Stream Analytics as a cloud analytics platform.</span></span> 

## <a name="general-features"></a><span data-ttu-id="1f50f-110">Genel Özellikler</span><span class="sxs-lookup"><span data-stu-id="1f50f-110">General features</span></span>

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="1f50f-111">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-111">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="1f50f-112">
                    <strong>Azure akış analizi</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-112">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="1f50f-113">
                    <strong>Hdınsight üzerinde Apache Storm</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-113">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="1f50f-114">
                    <strong>Açık kaynak?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-114">
                    <strong>Open source?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="1f50f-115">Hayır.</span><span class="sxs-lookup"><span data-stu-id="1f50f-115">No.</span></span> <span data-ttu-id="1f50f-116">Azure Stream Analytics olan bir Microsoft özel sunar.</span><span class="sxs-lookup"><span data-stu-id="1f50f-116">Azure Stream Analytics is a Microsoft proprietary offering.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="1f50f-117">Evet.</span><span class="sxs-lookup"><span data-stu-id="1f50f-117">Yes.</span></span> <span data-ttu-id="1f50f-118">Apache Storm bir lisanslı Apache teknolojisidir.</span><span class="sxs-lookup"><span data-stu-id="1f50f-118">Apache Storm is an Apache licensed technology.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="1f50f-119">
                    <strong>Microsoft Destek?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-119">
                    <strong>Microsoft support?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="1f50f-120">Evet</span><span class="sxs-lookup"><span data-stu-id="1f50f-120">Yes</span></span> </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="1f50f-121">Evet</span><span class="sxs-lookup"><span data-stu-id="1f50f-121">Yes</span></span> </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="1f50f-122">
                    <strong>Donanım gereksinimleri</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-122">
                    <strong>Hardware requirements</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="1f50f-123">yok.</span><span class="sxs-lookup"><span data-stu-id="1f50f-123">None.</span></span> <span data-ttu-id="1f50f-124">Azure Stream Analytics bir Azure hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="1f50f-124">Azure Stream Analytics is an Azure Service.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="1f50f-125">yok.</span><span class="sxs-lookup"><span data-stu-id="1f50f-125">None.</span></span> <span data-ttu-id="1f50f-126">Apache Storm bir Azure hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="1f50f-126">Apache Storm is an Azure Service.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="1f50f-127">
                    <strong>Üst düzey birim</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-127">
                    <strong>Top-level unit</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="1f50f-128">Kullanıcılar, dağıtmak ve akış işi izleyin.</span><span class="sxs-lookup"><span data-stu-id="1f50f-128">Users deploy and monitor streaming jobs.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="1f50f-129">Kullanıcıların dağıtmak ve diğer iş yüklerini (toplu dahil) yanı sıra birden çok Storm işleri barındırabilir tüm küme izleyin.</span><span class="sxs-lookup"><span data-stu-id="1f50f-129">Users deploy and monitor a whole cluster, which can host multiple Storm jobs as well as other workloads (including batch).</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="1f50f-130">
                    <strong>Fiyatlandırma</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-130">
                    <strong>Pricing</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="1f50f-131">İşlenen veri hacmi tarafından fiyatlandırılır ve iş hello saat başına gerekli akış birim sayısını hello çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="1f50f-131">Priced by volume of data processed and hello number of streaming units required per hour that hello job is running.</span></span> 
                </p>
                    <p><span data-ttu-id="1f50f-132">Daha fazla bilgi için bkz: <a href="http://azure.microsoft.com/pricing/details/stream-analytics/">Stream Analytics fiyatları</a>.</span><span class="sxs-lookup"><span data-stu-id="1f50f-132">For more information, see <a href="http://azure.microsoft.com/pricing/details/stream-analytics/">Stream Analytics Pricing</a>.</span></span></p>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="1f50f-133">Merhaba birimi satın alma küme dayalıdır ve hello küme dağıtılan işleri bağımsız çalışıyor, başlangıç zamanında dayalı olarak ücretlendirilir.</span><span class="sxs-lookup"><span data-stu-id="1f50f-133">hello unit of purchase is cluster-based, and is charged based on hello time hello cluster is running, independent of jobs deployed.</span></span>
                </p>
                <p>
<span data-ttu-id="1f50f-134">Daha fazla bilgi için bkz: <a href="http://azure.microsoft.com/pricing/details/hdinsight/">Hdınsight fiyatlandırma</a>.</span><span class="sxs-lookup"><span data-stu-id="1f50f-134">For more information, see <a href="http://azure.microsoft.com/pricing/details/hdinsight/">HDInsight pricing</a>.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="authoring"></a><span data-ttu-id="1f50f-135">Yazma</span><span class="sxs-lookup"><span data-stu-id="1f50f-135">Authoring</span></span>

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="1f50f-136">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-136">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="1f50f-137">
                    <strong>Azure akış analizi</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-137">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="1f50f-138">
                    <strong>Hdınsight üzerinde Apache Storm</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-138">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="1f50f-139">
                    <strong>Özellikleri: SQL DSL?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-139">
                    <strong>Capabilities: SQL DSL?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="1f50f-140">Evet.</span><span class="sxs-lookup"><span data-stu-id="1f50f-140">Yes.</span></span> <span data-ttu-id="1f50f-141">Stream Analytics, Dönüşümlerin oluşturmak için SQL benzeri bir dil sağlar.</span><span class="sxs-lookup"><span data-stu-id="1f50f-141">Stream Analytics provides a SQL-like language for creating transformations.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="1f50f-142">Hayır.</span><span class="sxs-lookup"><span data-stu-id="1f50f-142">No.</span></span> <span data-ttu-id="1f50f-143">Kullanıcılar Java veya C# kod yazmak veya Trident API'leri kullanın.</span><span class="sxs-lookup"><span data-stu-id="1f50f-143">Users write code in Java or C#, or use Trident APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="1f50f-144">
                    <strong>Özellikleri: Geçici işleçler?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-144">
                    <strong>Capabilities: Temporal operators?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="1f50f-145">Varsayılan olarak, pencerelenmiş toplamlar ve zamana bağlı birleştirmeler desteklenir.</span><span class="sxs-lookup"><span data-stu-id="1f50f-145">Windowed aggregates and temporal joins are supported by default.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="1f50f-146">Geçici işleçler hello kullanıcı tarafından uygulanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1f50f-146">Temporal operators must be implemented by hello user.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="1f50f-147">
                    <strong>Geliştirme deneyimi</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-147">
                    <strong>Development experience</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="1f50f-148">Kullanıcılar oluşturma hata ayıklama ve canlı akış alan türetilmiş örnek verileri kullanarak işlerini hello Azure portalı üzerinden izleme.</span><span class="sxs-lookup"><span data-stu-id="1f50f-148">Users can create, debug, and monitor jobs through hello Azure portal, using sample data derived from a live stream.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="1f50f-149">.NET kullanarak kullanıcıların geliştirmek, hata ayıklama ve Visual Studio üzerinden izlemek.</span><span class="sxs-lookup"><span data-stu-id="1f50f-149">Users using .NET can develop, debug, and monitor through Visual Studio.</span></span> <span data-ttu-id="1f50f-150">Java veya diğer dilleri kullanarak kullanıcıların hello kendi seçtikleri IDE kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f50f-150">Users using Java or other languages can use hello IDE of their choice.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="1f50f-151">
                    <strong>Hata ayıklama desteği</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-151">
                    <strong>Debugging support</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="1f50f-152">Temel iş durumunu ve işlemlerini günlüklerini kullanılabilir toohelp hata ayıklama ' dir.</span><span class="sxs-lookup"><span data-stu-id="1f50f-152">Basic job status and operations logs are available toohelp debug.</span></span> <span data-ttu-id="1f50f-153">Stream Analytics kullanıcıların hangi içerik veya ne kadar içerik hello günlükleri (yani, ayrıntılı mod) dahil belirtin şu anda izin vermez.</span><span class="sxs-lookup"><span data-stu-id="1f50f-153">Stream Analytics currently does not let users specify what content or how much content is included in hello logs (i.e., verbose mode).</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="1f50f-154">Ayrıntılı günlükleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1f50f-154">Detailed logs are available.</span></span> <span data-ttu-id="1f50f-155">Kullanıcılar, Visual Studio veya toohello kümede günlüğe kaydetme ve hello günlükleri doğrudan erişimini günlükleri erişebilir.</span><span class="sxs-lookup"><span data-stu-id="1f50f-155">Users can access logs in Visual Studio or by logging in toohello cluster and accessing hello logs directly.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="1f50f-156">
                    <strong>Özel kod kullanarak genişletilebilirlik?</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-156">
                    <strong>Extensibility using custom code?</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="1f50f-157">Kısmen JavaScript UDF'ler ile destekler.</span><span class="sxs-lookup"><span data-stu-id="1f50f-157">Partially support with JavaScript UDFs.</span></span> <span data-ttu-id="1f50f-158">Daha fazla bilgi için bkz: <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-javascript-user-defined-functions">JavaScript UDF tümleştirme</a>.</span><span class="sxs-lookup"><span data-stu-id="1f50f-158">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-javascript-user-defined-functions">JavaScript UDF integration</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="1f50f-159">Evet.</span><span class="sxs-lookup"><span data-stu-id="1f50f-159">Yes.</span></span> <span data-ttu-id="1f50f-160">Kullanıcılar, C#, Java veya üzerinde Storm desteklenen herhangi bir dil özel kod yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f50f-160">Users can write custom code in C#, Java, or any other language supported on Storm.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="data-sources-inputs-and-outputs"></a><span data-ttu-id="1f50f-161">Veri kaynakları (girdileri) ve çıkışları</span><span class="sxs-lookup"><span data-stu-id="1f50f-161">Data sources (inputs) and outputs</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="1f50f-162">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-162">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="1f50f-163">
                    <strong>Azure akış analizi</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-163">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="1f50f-164">
                    <strong>Hdınsight üzerinde Apache Storm</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-164">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="1f50f-165">
                 <strong>Giriş veri kaynakları</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-165">
                 <strong>Input data sources</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="1f50f-166">Azure Event Hubs ile Azure Blob Depolama.</span><span class="sxs-lookup"><span data-stu-id="1f50f-166">Azure Event Hubs and Azure Blob storage.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="1f50f-167">Bağlayıcılar, Azure Event Hubs, Azure Service Bus, Kafka ve daha fazla bilgi için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1f50f-167">Connectors are available for Azure Event Hubs, Azure Service Bus, Kafka, and more.</span></span> <span data-ttu-id="1f50f-168">Kullanıcıların özel kod kullanarak ek bağlayıcı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f50f-168">Users can create additional connectors using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="1f50f-169">
                    <strong>Giriş veri biçimleri</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-169">
                    <strong>Input data formats</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="1f50f-170">Avro, JSON, CSV</span><span class="sxs-lookup"><span data-stu-id="1f50f-170">Avro, JSON, CSV</span></span> </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="1f50f-171">Kullanıcıların özel kod kullanarak herhangi bir biçimde uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f50f-171">Users can implement any format using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="1f50f-172">
                    <strong>Çıkışları</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-172">
                    <strong>Outputs</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="1f50f-173">İş akışında birden çok çıkış olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f50f-173">A streaming job can have multiple outputs.</span></span> <span data-ttu-id="1f50f-174">Desteklenen çıkışları Azure Event Hubs, Azure Blob Depolama, Azure Table storage, Azure SQL DB ve Power BI ' dir.</span><span class="sxs-lookup"><span data-stu-id="1f50f-174">Supported outputs are Azure Event Hubs, Azure Blob storage, Azure Table storage, Azure SQL DB, and Power BI.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="1f50f-175">Storm birçok çıkışları bir topolojisinde destekler ve her çıktı aşağı akış işleme için Özel mantık olabilir.</span><span class="sxs-lookup"><span data-stu-id="1f50f-175">Storm supports many outputs in a topology, and each output can have custom logic for downstream processing.</span></span> <span data-ttu-id="1f50f-176">Power BI, Azure Event Hubs, Azure Blob Depolama, Azure Cosmos DB, SQL ve HBase, Storm bağlayıcıları içerir.</span><span class="sxs-lookup"><span data-stu-id="1f50f-176">Storm includes connectors for Power BI, Azure Event Hubs, Azure Blob storage, Azure Cosmos DB, SQL, and HBase.</span></span> <span data-ttu-id="1f50f-177">Kullanıcıların özel kod kullanarak ek bağlayıcı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f50f-177">Users can create additional connectors using custom code.</span></span>    
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="1f50f-178">
                    <strong>Kodlama verileri biçimleri</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-178">
                    <strong>Data-encoding formats</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="1f50f-179">Veri UTF-8 kullanarak biçimlendirilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f50f-179">Data must be formatted using UTF-8.</span></span>
                </p>
            </td>   
            <td width="246" valign="top">
                <p>
<span data-ttu-id="1f50f-180">Kullanıcıların özel kod kullanarak veri kodlama biçimi uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f50f-180">Users can implement any data encoding format using custom code.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="management-and-operations"></a><span data-ttu-id="1f50f-181">Yönetim ve işlemler</span><span class="sxs-lookup"><span data-stu-id="1f50f-181">Management and operations</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="1f50f-182">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-182">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="1f50f-183">
                    <strong>Azure akış analizi</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-183">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="1f50f-184">
                    <strong>Hdınsight üzerinde Apache Storm</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-184">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="1f50f-185">
                    <strong>İş dağıtım modeli</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-185">
                    <strong>Job deployment model</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="1f50f-186">Azure portalı, PowerShell ve REST API'leri.</span><span class="sxs-lookup"><span data-stu-id="1f50f-186">Azure portal, PowerShell, and REST APIs.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="1f50f-187">Azure portal, PowerShell, Visual Studio ve REST API'leri.</span><span class="sxs-lookup"><span data-stu-id="1f50f-187">Azure portal, PowerShell, Visual Studio, and REST APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="1f50f-188">
                    <strong>İzleme (istatistikleri, sayaçları, vb.)</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-188">
                    <strong>Monitoring (stats, counters, etc.)</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="1f50f-189">İzleme Azure portalı ve REST API'leri kullanılarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="1f50f-189">Monitoring is implemented using Azure portal and REST APIs.</span></span> <span data-ttu-id="1f50f-190">Kullanıcılar ayrıca Azure uyarılar yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f50f-190">Users can also configure Azure alerts.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="1f50f-191">İzleme hello Storm kullanıcı Arabirimi ve REST API'leri kullanılarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="1f50f-191">Monitoring is implemented using hello Storm UI and REST APIs.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="1f50f-192">
                    <strong>Ölçeklenebilirlik</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-192">
                    <strong>Scalability</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="1f50f-193">Ölçeklenebilirlik akış birimleri (SUs) hello sayısı için her bir iş tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="1f50f-193">Scalability is determined by hello number of Streaming Units (SUs) for each job.</span></span> <span data-ttu-id="1f50f-194">Her akış birimi too1 MB/saniye, en fazla 50 birimleriyle işler.</span><span class="sxs-lookup"><span data-stu-id="1f50f-194">Each Streaming Unit processes up too1 MB/second, with a maximum 50 units.</span></span> <span data-ttu-id="1f50f-195">Daha fazla bilgi için bkz: <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-jobs">ölçek tooincrease işleme</a>.</span><span class="sxs-lookup"><span data-stu-id="1f50f-195">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-jobs">Scale tooincrease throughput</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="1f50f-196">Ölçeklenebilirlik hello hello Hdınsight Storm kümesi düğüm sayısı tarafından belirlenir.</span><span class="sxs-lookup"><span data-stu-id="1f50f-196">Scalability is determined by hello number of nodes in hello HDInsight Storm cluster.</span></span> <span data-ttu-id="1f50f-197">Merhaba düğüm sayısı üst sınırı Hello hello kullanıcının Azure kota tarafından tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="1f50f-197">hello top limit on hello number of nodes is defined by hello user's Azure quota.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="1f50f-198">
                    <strong>Veri işleme sınırları</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-198">
                    <strong>Data processing limits</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="1f50f-199">Kullanıcılar, veri işleme artırın veya artırarak veya azaltarak, akış birim hello sayısını 1 GB/saniye üst sınır tarafından masrafları iyileştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f50f-199">Users can increase data processing or optimize costs by increasing or decreasing hello number of Streaming Units, with an upper limit of 1 GB/second.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="1f50f-200">Kullanıcıların küme boyutu yukarı veya aşağı ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f50f-200">Users can scale cluster size up or down.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="1f50f-201">
                    <strong>Stop/Sürdür</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-201">
                    <strong>Stop/Resume</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="1f50f-202">Durdur ve durdurulmuş son yerden devam edin.</span><span class="sxs-lookup"><span data-stu-id="1f50f-202">Stop and resume from last place stopped.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="1f50f-203">Durdurun ve son sürdürme Filigran üzerinde temel durdurulmuş yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="1f50f-203">Stop and resume from last place stopped based on a watermark.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="1f50f-204">
                    <strong>Hizmet ve framework güncelleştirme</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-204">
                    <strong>Service and framework update</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="1f50f-205">Kapalı kalma süresi ile otomatik düzeltme eki uygulama.</span><span class="sxs-lookup"><span data-stu-id="1f50f-205">Automatic patching with no downtime.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="1f50f-206">Kapalı kalma süresi ile otomatik düzeltme eki uygulama.</span><span class="sxs-lookup"><span data-stu-id="1f50f-206">Automatic patching with no downtime.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="1f50f-207">
                    <strong>Garantili SLA ile bir yüksek oranda kullanılabilir hizmeti aracılığıyla iş sürekliliği</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-207">
                    <strong>Business continuity through a Highly Available Service with guaranteed SLAs</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <ul>
                <li><span data-ttu-id="1f50f-208">% 99,9 çalışma süresi SLA'sı</span><span class="sxs-lookup"><span data-stu-id="1f50f-208">SLA of 99.9% uptime</span></span></li>
                <li><span data-ttu-id="1f50f-209">Hatalardan otomatik kurtarma</span><span class="sxs-lookup"><span data-stu-id="1f50f-209">Auto-recovery from failures</span></span></li>
                <li><span data-ttu-id="1f50f-210">Durum bilgisi olan geçici işleçler yerleşik kurtarılması</span><span class="sxs-lookup"><span data-stu-id="1f50f-210">Built-in recovery of stateful temporal operators</span></span></li>
                </ul>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="1f50f-211">Merhaba Storm kümesi % 99,9 çalışma süresi SLA'sı.</span><span class="sxs-lookup"><span data-stu-id="1f50f-211">SLA of 99.9% uptime of hello Storm cluster.</span></span> 
                </p>
                <p>
<span data-ttu-id="1f50f-212">Apache Storm hataya dayanıklı akış platformudur.</span><span class="sxs-lookup"><span data-stu-id="1f50f-212">Apache Storm is a fault-tolerant streaming platform.</span></span> <span data-ttu-id="1f50f-213">Ancak, akış Çalıştır kesintisiz işleri hello kullanıcının sorumluluk tooensure olur.</span><span class="sxs-lookup"><span data-stu-id="1f50f-213">However, it is hello user's responsibility tooensure that streaming jobs run uninterrupted.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>

## <a name="advanced-features"></a><span data-ttu-id="1f50f-214">Gelişmiş özellikler</span><span class="sxs-lookup"><span data-stu-id="1f50f-214">Advanced features</span></span> ##

<table border="1" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="1f50f-215">
                    <strong> </strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-215">
                    <strong> </strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p><span data-ttu-id="1f50f-216">
                    <strong>Azure akış analizi</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-216">
                    <strong>Azure Stream Analytics</strong>
                </span></span></p>
            </td>
            <td width="246" valign="top">
                <p><span data-ttu-id="1f50f-217">
                    <strong>Hdınsight üzerinde Apache Storm</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-217">
                    <strong>Apache Storm on HDInsight</strong>
                </span></span></p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="1f50f-218">
                    <strong>Geç varış ve sıra dışı olay işleme</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-218">
                    <strong>Late arrival and out-of-order event handling</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="1f50f-219">Yerleşik yapılandırılabilir ilkeleri olayları yeniden sıralamak, olayları bırakın veya olay zamanını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1f50f-219">Built-in configurable policies can reorder events, drop events, or adjust event time.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="1f50f-220">Kullanıcılar bu senaryo mantığı toohandle uygulamalıdır.</span><span class="sxs-lookup"><span data-stu-id="1f50f-220">Users must implement logic toohandle this scenario.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="1f50f-221">
                    <strong>Başvuru verileri</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-221">
                    <strong>Reference data</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="1f50f-222">Başvuru verileri Azure Blob Depolama en fazla 100 MB bellek içi önbellek ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1f50f-222">Reference data is available from Azure Blob storage with a maximum of 100 MB of in-memory cache.</span></span> <span data-ttu-id="1f50f-223">Başvuru verileri hello hizmeti tarafından yenilenir.</span><span class="sxs-lookup"><span data-stu-id="1f50f-223">Reference data is refreshed by hello service.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="1f50f-224">Veri boyutu sınırı.</span><span class="sxs-lookup"><span data-stu-id="1f50f-224">No limits on data size.</span></span> <span data-ttu-id="1f50f-225">Bağlayıcılar, HBase, Azure Cosmos DB, SQL Server ve Azure için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1f50f-225">Connectors are available for HBase, Azure Cosmos DB, SQL Server, and Azure.</span></span> <span data-ttu-id="1f50f-226">Kullanıcıların özel kod kullanarak ek bağlayıcı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1f50f-226">Users can create additional connectors using custom code.</span></span> <span data-ttu-id="1f50f-227">Başvuru verileri için özel kod kullanarak yenilenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="1f50f-227">Reference data must be refreshed using custom code.</span></span>
                </p>
            </td>
        </tr>
        <tr>
            <td width="174" valign="top">
                <p><span data-ttu-id="1f50f-228">
                    <strong>Machine Learning ile tümleştirme</strong>
                </span><span class="sxs-lookup"><span data-stu-id="1f50f-228">
                    <strong>Integration with Machine Learning</strong>
                </span></span></p>
            </td>
            <td width="204" valign="top">
                <p>
<span data-ttu-id="1f50f-229">Azure Machine Learning modellerini işlevleri işi oluşturma sırasında yapılandırılabilir yayımladı.</span><span class="sxs-lookup"><span data-stu-id="1f50f-229">Published Azure Machine Learning models can be configured as functions during job creation.</span></span> <span data-ttu-id="1f50f-230">Daha fazla bilgi için bkz: <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-with-machine-learning-functions">Machine Learning işlevleri için ölçek</a>.</span><span class="sxs-lookup"><span data-stu-id="1f50f-230">For more information, see <a href="https://docs.microsoft.com/azure/stream-analytics/stream-analytics-scale-with-machine-learning-functions">Scale for Machine Learning functions</a>.</span></span>
                </p>
            </td>
            <td width="246" valign="top">
                <p>
<span data-ttu-id="1f50f-231">Storm Cıvatalar üzerinden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1f50f-231">Available through Storm Bolts.</span></span>
                </p>
            </td>
        </tr>
    </tbody>
</table>
