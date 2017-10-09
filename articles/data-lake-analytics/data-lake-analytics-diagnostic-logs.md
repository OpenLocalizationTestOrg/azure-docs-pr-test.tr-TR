---
title: "Azure Data Lake Analytics için tanılama günlüklerini aaaViewing | Microsoft Docs"
description: "Nasıl toosetup ve erişim tanılama günlükleri için Azure Data Lake analytics anlama "
services: data-lake-analytics
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf5633d4-bc43-444e-90fc-f90fbd0b7935
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 4cd1eb6f585c1ef96c358340232ef85721a972b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-analytics"></a><span data-ttu-id="21871-103">Azure Data Lake Analytics için tanılama günlüklerine erişme</span><span class="sxs-lookup"><span data-stu-id="21871-103">Accessing diagnostic logs for Azure Data Lake Analytics</span></span>

<span data-ttu-id="21871-104">Tanılama günlük toocollect veri erişimi denetim izleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="21871-104">Diagnostic logging allows you toocollect data access audit trails.</span></span> <span data-ttu-id="21871-105">Bu günlükler gibi bilgileri sağlayın:</span><span class="sxs-lookup"><span data-stu-id="21871-105">These logs provide information such as:</span></span>

* <span data-ttu-id="21871-106">Merhaba veri erişilen kullanıcıların listesi.</span><span class="sxs-lookup"><span data-stu-id="21871-106">A list of users that accessed hello data.</span></span>
* <span data-ttu-id="21871-107">Merhaba verileri ne sıklıkla erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="21871-107">How frequently hello data is accessed.</span></span>
* <span data-ttu-id="21871-108">Ne kadar veri hello hesabında depolanır.</span><span class="sxs-lookup"><span data-stu-id="21871-108">How much data is stored in hello account.</span></span>

## <a name="enable-logging"></a><span data-ttu-id="21871-109">Günlü kaydını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="21871-109">Enable logging</span></span>

1. <span data-ttu-id="21871-110">Toohello üzerinde oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="21871-110">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="21871-111">Data Lake Analytics hesabınızı açın ve seçin **tanılama günlükleri** hello gelen __İzleyici__ bölümü.</span><span class="sxs-lookup"><span data-stu-id="21871-111">Open your Data Lake Analytics account and select **Diagnostic logs** from hello __Monitor__ section.</span></span> <span data-ttu-id="21871-112">Ardından, __tanılamayı açın__.</span><span class="sxs-lookup"><span data-stu-id="21871-112">Next, select __Turn on diagnostics__.</span></span>

    ![Tanılama toocollect denetim üzerinde açın ve günlükleri isteği](./media/data-lake-analytics-diagnostic-logs/turn-on-logging.png)

3. <span data-ttu-id="21871-114">Gelen __tanılama ayarları__hello durum too__On__ ayarlamak ve günlüğe kaydetme seçeneklerini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="21871-114">From __Diagnostics settings__, set hello status too__On__ and select logging options.</span></span>

    <span data-ttu-id="21871-115">![Tanılama toocollect denetim üzerinde açın ve istek günlükleri](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "tanılama günlüklerini etkinleştirme")</span><span class="sxs-lookup"><span data-stu-id="21871-115">![Turn on diagnostics toocollect audit and request logs](./media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span></span>

   * <span data-ttu-id="21871-116">Ayarlama **durum** çok**üzerinde** tooenable tanılama günlük.</span><span class="sxs-lookup"><span data-stu-id="21871-116">Set **Status** too**On** tooenable diagnostic logging.</span></span>

   * <span data-ttu-id="21871-117">Üç farklı yolla toostore/işlem hello veri seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21871-117">You can choose toostore/process hello data in three different ways.</span></span>

     * <span data-ttu-id="21871-118">Seçin __arşiv tooa depolama hesabı__ toostore bir Azure depolama hesabında günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="21871-118">Select __Archive tooa storage account__ toostore logs in an Azure storage account.</span></span> <span data-ttu-id="21871-119">Tooarchive hello veri istiyorsanız bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="21871-119">Use this option if you want tooarchive hello data.</span></span> <span data-ttu-id="21871-120">Bu seçeneği seçerseniz, bir Azure depolama hesabı toosave hello günlüklerine sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="21871-120">If you select this option, you must provide an Azure storage account toosave hello logs to.</span></span>

     * <span data-ttu-id="21871-121">Seçin **tooan olay hub'ı akış** toostream günlük veri tooan Azure olay hub'ı.</span><span class="sxs-lookup"><span data-stu-id="21871-121">Select **Stream tooan Event Hub** toostream log data tooan Azure Event Hub.</span></span> <span data-ttu-id="21871-122">Gerçek zamanlı gelen günlüklerini analiz bir aşağı akış işleme ardışık varsa bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="21871-122">Use this option if you have a downstream processing pipeline that is analyzing incoming logs in real time.</span></span> <span data-ttu-id="21871-123">Bu seçeneği belirlerseniz, hello Azure Event Hub'ın toouse istediğiniz hello ayrıntılarını sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="21871-123">If you select this option, you must provide hello details for hello Azure Event Hub you want toouse.</span></span>

     * <span data-ttu-id="21871-124">Seçin __tooLog Analytics Gönder__ toosend hello veri toohello günlük analizi hizmeti.</span><span class="sxs-lookup"><span data-stu-id="21871-124">Select __Send tooLog Analytics__ toosend hello data toohello Log Analytics service.</span></span> <span data-ttu-id="21871-125">Günlüklerini analiz edin ve toouse günlük analizi toogather isterseniz bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="21871-125">Use this option if you want toouse Log Analytics toogather and analyze logs.</span></span>
   * <span data-ttu-id="21871-126">Tooget denetim günlüklerini veya istek günlüklerini ya da hem isteyip istemediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="21871-126">Specify whether you want tooget audit logs or request logs or both.</span></span>  <span data-ttu-id="21871-127">İstek günlüğü her API isteği yakalar.</span><span class="sxs-lookup"><span data-stu-id="21871-127">A request log captures every API request.</span></span> <span data-ttu-id="21871-128">Bir denetim günlüğü bu API isteğiyle tetiklenen tüm işlemleri kaydeder.</span><span class="sxs-lookup"><span data-stu-id="21871-128">An audit log records all operations that are triggered by that API request.</span></span>

   * <span data-ttu-id="21871-129">İçin __arşiv tooa depolama hesabı__, gün tooretain hello veri hello sayısını belirtin.</span><span class="sxs-lookup"><span data-stu-id="21871-129">For __Archive tooa storage account__, specify hello number of days tooretain hello data.</span></span>

   * <span data-ttu-id="21871-130">__Kaydet__ düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="21871-130">Click __Save__.</span></span>

        > [!NOTE]
        > <span data-ttu-id="21871-131">Ya da seçmelisiniz __arşiv tooa depolama hesabı__, __tooan olay hub'ı akış__ veya __tooLog Analytics Gönder__ hello tıklatmadan önce __kaydetmek__düğmesi.</span><span class="sxs-lookup"><span data-stu-id="21871-131">You must select either __Archive tooa storage account__, __Stream tooan Event Hub__ or __Send tooLog Analytics__ before clicking hello __Save__ button.</span></span>

<span data-ttu-id="21871-132">Tanılama ayarları etkinleştirildiğinde, toohello döndürebilir __tanılama günlükleri__ dikey tooview hello günlükleri.</span><span class="sxs-lookup"><span data-stu-id="21871-132">Once you have enabled diagnostic settings, you can return toohello __Diagnostics logs__ blade tooview hello logs.</span></span>

## <a name="view-logs"></a><span data-ttu-id="21871-133">Günlükleri görüntüle</span><span class="sxs-lookup"><span data-stu-id="21871-133">View logs</span></span>

### <a name="use-hello-data-lake-analytics-view"></a><span data-ttu-id="21871-134">Merhaba Data Lake Analytics görünümünü kullanın</span><span class="sxs-lookup"><span data-stu-id="21871-134">Use hello Data Lake Analytics view</span></span>

1. <span data-ttu-id="21871-135">, Data Lake Analytics hesabı dikey penceresinde altında **izleme**seçin **tanılama günlüklerini** ve ardından bir girişi toodisplay için günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="21871-135">From your Data Lake Analytics account blade, under **Monitoring**, select **Diagnostic Logs** and then select an entry toodisplay logs for.</span></span>

    <span data-ttu-id="21871-136">![Görünüm tanılama günlük](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "tanılama günlükleri görüntüleme")</span><span class="sxs-lookup"><span data-stu-id="21871-136">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span></span>

2. <span data-ttu-id="21871-137">Merhaba günlükleri tarafından ayrılır **denetim günlüklerini** ve **isteği günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="21871-137">hello logs are categorized by **Audit Logs** and **Request Logs**.</span></span>

    ![günlük girişleri](./media/data-lake-analytics-diagnostic-logs/diagnostic-log-entries.png)

   * <span data-ttu-id="21871-139">İstek günlüklerini hello Data Lake Analytics hesabı üzerinde yapılan her API isteği yakalayın.</span><span class="sxs-lookup"><span data-stu-id="21871-139">Request logs capture every API request made on hello Data Lake Analytics account.</span></span>
   * <span data-ttu-id="21871-140">Denetim günlüklerini benzer toorequest günlüklerin ancak hello işlemleri çok daha ayrıntılı bir dökümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="21871-140">Audit Logs are similar toorequest Logs but provide a much more detailed breakdown of hello operations.</span></span> <span data-ttu-id="21871-141">Örneğin, bir tek karşıya yükleme API çağrısının istek günlüğü, Denetim günlüğü "Ekle" işlemlerinde neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="21871-141">For example, a single upload API call in a request log can result in multiple "Append" operations in its audit log.</span></span>

3. <span data-ttu-id="21871-142">Merhaba tıklatın **karşıdan** oturum bir günlük girişi toodownload için bağlantı.</span><span class="sxs-lookup"><span data-stu-id="21871-142">Click hello **Download** link for a log entry toodownload that log.</span></span>

### <a name="use-hello-azure-storage-account-that-contains-log-data"></a><span data-ttu-id="21871-143">Günlük verilerini içeren hello Azure depolama hesabı kullan</span><span class="sxs-lookup"><span data-stu-id="21871-143">Use hello Azure Storage account that contains log data</span></span>

1. <span data-ttu-id="21871-144">Günlüğe kaydetme için Data Lake Analytics ile ilişkili hello Azure depolama hesabı dikey açın ve ardından __BLOB'lar__.</span><span class="sxs-lookup"><span data-stu-id="21871-144">Open hello Azure Storage account blade associated with Data Lake Analytics for logging, and then click __Blobs__.</span></span> <span data-ttu-id="21871-145">Merhaba **Blob hizmeti** iki kapsayıcı dikey penceresinde listelenir.</span><span class="sxs-lookup"><span data-stu-id="21871-145">hello **Blob service** blade lists two containers.</span></span>

    <span data-ttu-id="21871-146">![Görünüm tanılama günlük](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "tanılama günlükleri görüntüleme")</span><span class="sxs-lookup"><span data-stu-id="21871-146">![View diagnostic logging](./media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span></span>

   * <span data-ttu-id="21871-147">Merhaba kapsayıcı **Öngörüler günlükleri denetim** hello denetim günlüklerini içerir.</span><span class="sxs-lookup"><span data-stu-id="21871-147">hello container **insights-logs-audit** contains hello audit logs.</span></span>
   * <span data-ttu-id="21871-148">Merhaba kapsayıcı **Öngörüler günlükleri istekleri** hello isteği günlükleri içerir.</span><span class="sxs-lookup"><span data-stu-id="21871-148">hello container **insights-logs-requests** contains hello request logs.</span></span>
2. <span data-ttu-id="21871-149">Bu kapsayıcılara hello günlükleri yapı izlenerek hello altında depolanır:</span><span class="sxs-lookup"><span data-stu-id="21871-149">Within these containers, hello logs are stored under hello following structure:</span></span>

        resourceId=/
          SUBSCRIPTIONS/
            <<SUBSCRIPTION_ID>>/
              RESOURCEGROUPS/
                <<RESOURCE_GRP_NAME>>/
                  PROVIDERS/
                    MICROSOFT.DATALAKEANALYTICS/
                      ACCOUNTS/
                        <DATA_LAKE_ANALYTICS_NAME>>/
                          y=####/
                            m=##/
                              d=##/
                                h=##/
                                  m=00/
                                    PT1H.json

   > [!NOTE]
   > <span data-ttu-id="21871-150">Merhaba `##` hello yolundaki girişleri hello yıl, ay, gün ve hangi hello günlük oluşturulduğu saat.</span><span class="sxs-lookup"><span data-stu-id="21871-150">hello `##` entries in hello path contain hello year, month, day, and hour in which hello log was created.</span></span> <span data-ttu-id="21871-151">Data Lake Analytics bir dosya kadar her saat oluşturur `m=` her zaman değerini içeren `00`.</span><span class="sxs-lookup"><span data-stu-id="21871-151">Data Lake Analytics creates one file every hour, so `m=` always contains a value of `00`.</span></span>

    <span data-ttu-id="21871-152">Örnek olarak, hello tam yolunu tooan denetim günlüğü olabilir:</span><span class="sxs-lookup"><span data-stu-id="21871-152">As an example, hello complete path tooan audit log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=04/m=00/PT1H.json

    <span data-ttu-id="21871-153">Benzer şekilde, hello tam yolunu tooa istek günlüğü olabilir:</span><span class="sxs-lookup"><span data-stu-id="21871-153">Similarly, hello complete path tooa request log could be:</span></span>

        https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=14/m=00/PT1H.json

## <a name="log-structure"></a><span data-ttu-id="21871-154">Günlük yapısı</span><span class="sxs-lookup"><span data-stu-id="21871-154">Log structure</span></span>

<span data-ttu-id="21871-155">Denetim hello ve yapılandırılmış bir JSON biçiminde günlüklerin isteyin.</span><span class="sxs-lookup"><span data-stu-id="21871-155">hello audit and request logs are in a structured JSON format.</span></span>

### <a name="request-logs"></a><span data-ttu-id="21871-156">İstek günlükleri</span><span class="sxs-lookup"><span data-stu-id="21871-156">Request logs</span></span>

<span data-ttu-id="21871-157">Merhaba JSON biçimli istek günlüğünde örnek girişi İşte.</span><span class="sxs-lookup"><span data-stu-id="21871-157">Here's a sample entry in hello JSON-formatted request log.</span></span> <span data-ttu-id="21871-158">Her bir blob olarak adlandırılan bir kök nesnesi vardır **kayıtları** günlük nesnelerinin bir dizisi içerir.</span><span class="sxs-lookup"><span data-stu-id="21871-158">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_analytics_account_name>",
             "category": "Requests",
             "operationName": "GetAggregatedJobHistory",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {
                 "HttpMethod":"POST",
                 "Path":"/JobAggregatedHistory",
                 "RequestContentLength":122,
                 "ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8",
                 "StartTime":"2016-07-07T21:02:52.472Z",
                 "EndTime":"2016-07-07T21:02:53.456Z"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a><span data-ttu-id="21871-159">İstek günlüğü şeması</span><span class="sxs-lookup"><span data-stu-id="21871-159">Request log schema</span></span>

| <span data-ttu-id="21871-160">Ad</span><span class="sxs-lookup"><span data-stu-id="21871-160">Name</span></span> | <span data-ttu-id="21871-161">Tür</span><span class="sxs-lookup"><span data-stu-id="21871-161">Type</span></span> | <span data-ttu-id="21871-162">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21871-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21871-163">time</span><span class="sxs-lookup"><span data-stu-id="21871-163">time</span></span> |<span data-ttu-id="21871-164">Dize</span><span class="sxs-lookup"><span data-stu-id="21871-164">String</span></span> |<span data-ttu-id="21871-165">Merhaba günlüğünün Hello zaman damgası (UTC) cinsinden</span><span class="sxs-lookup"><span data-stu-id="21871-165">hello timestamp (in UTC) of hello log</span></span> |
| <span data-ttu-id="21871-166">resourceId</span><span class="sxs-lookup"><span data-stu-id="21871-166">resourceId</span></span> |<span data-ttu-id="21871-167">Dize</span><span class="sxs-lookup"><span data-stu-id="21871-167">String</span></span> |<span data-ttu-id="21871-168">işlemi sürdü hello kaynak Hello tanıtıcısı yerleştirin</span><span class="sxs-lookup"><span data-stu-id="21871-168">hello identifier of hello resource that operation took place on</span></span> |
| <span data-ttu-id="21871-169">category</span><span class="sxs-lookup"><span data-stu-id="21871-169">category</span></span> |<span data-ttu-id="21871-170">Dize</span><span class="sxs-lookup"><span data-stu-id="21871-170">String</span></span> |<span data-ttu-id="21871-171">Merhaba günlük kategorisi.</span><span class="sxs-lookup"><span data-stu-id="21871-171">hello log category.</span></span> <span data-ttu-id="21871-172">Örneğin, **istekleri**.</span><span class="sxs-lookup"><span data-stu-id="21871-172">For example, **Requests**.</span></span> |
| <span data-ttu-id="21871-173">operationName</span><span class="sxs-lookup"><span data-stu-id="21871-173">operationName</span></span> |<span data-ttu-id="21871-174">Dize</span><span class="sxs-lookup"><span data-stu-id="21871-174">String</span></span> |<span data-ttu-id="21871-175">Oturum hello işlemin adı.</span><span class="sxs-lookup"><span data-stu-id="21871-175">Name of hello operation that is logged.</span></span> <span data-ttu-id="21871-176">Örneğin, GetAggregatedJobHistory.</span><span class="sxs-lookup"><span data-stu-id="21871-176">For example, GetAggregatedJobHistory.</span></span> |
| <span data-ttu-id="21871-177">resultType</span><span class="sxs-lookup"><span data-stu-id="21871-177">resultType</span></span> |<span data-ttu-id="21871-178">Dize</span><span class="sxs-lookup"><span data-stu-id="21871-178">String</span></span> |<span data-ttu-id="21871-179">Merhaba işlemi, örneğin, 200 Hello durumu.</span><span class="sxs-lookup"><span data-stu-id="21871-179">hello status of hello operation, For example, 200.</span></span> |
| <span data-ttu-id="21871-180">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="21871-180">callerIpAddress</span></span> |<span data-ttu-id="21871-181">Dize</span><span class="sxs-lookup"><span data-stu-id="21871-181">String</span></span> |<span data-ttu-id="21871-182">Merhaba istekte hello istemcinin Hello IP adresi</span><span class="sxs-lookup"><span data-stu-id="21871-182">hello IP address of hello client making hello request</span></span> |
| <span data-ttu-id="21871-183">correlationId</span><span class="sxs-lookup"><span data-stu-id="21871-183">correlationId</span></span> |<span data-ttu-id="21871-184">Dize</span><span class="sxs-lookup"><span data-stu-id="21871-184">String</span></span> |<span data-ttu-id="21871-185">Merhaba günlük Hello tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="21871-185">hello identifier of hello log.</span></span> <span data-ttu-id="21871-186">Bu değer, kullanılan toogroup bir dizi ilgili günlük girişlerini olabilir.</span><span class="sxs-lookup"><span data-stu-id="21871-186">This value can be used toogroup a set of related log entries.</span></span> |
| <span data-ttu-id="21871-187">identity</span><span class="sxs-lookup"><span data-stu-id="21871-187">identity</span></span> |<span data-ttu-id="21871-188">Nesne</span><span class="sxs-lookup"><span data-stu-id="21871-188">Object</span></span> |<span data-ttu-id="21871-189">Merhaba günlük oluşturulan hello kimliği</span><span class="sxs-lookup"><span data-stu-id="21871-189">hello identity that generated hello log</span></span> |
| <span data-ttu-id="21871-190">properties</span><span class="sxs-lookup"><span data-stu-id="21871-190">properties</span></span> |<span data-ttu-id="21871-191">JSON</span><span class="sxs-lookup"><span data-stu-id="21871-191">JSON</span></span> |<span data-ttu-id="21871-192">Ayrıntılar için Hello sonraki bölümüne (istek günlük özellikleri Şeması) bakın</span><span class="sxs-lookup"><span data-stu-id="21871-192">See hello next section (Request log properties schema) for details</span></span> |

#### <a name="request-log-properties-schema"></a><span data-ttu-id="21871-193">İstek günlüğü özellikleri şeması</span><span class="sxs-lookup"><span data-stu-id="21871-193">Request log properties schema</span></span>

| <span data-ttu-id="21871-194">Ad</span><span class="sxs-lookup"><span data-stu-id="21871-194">Name</span></span> | <span data-ttu-id="21871-195">Tür</span><span class="sxs-lookup"><span data-stu-id="21871-195">Type</span></span> | <span data-ttu-id="21871-196">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21871-196">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21871-197">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="21871-197">HttpMethod</span></span> |<span data-ttu-id="21871-198">Dize</span><span class="sxs-lookup"><span data-stu-id="21871-198">String</span></span> |<span data-ttu-id="21871-199">Merhaba HTTP hello işlemi için kullanılan yöntem.</span><span class="sxs-lookup"><span data-stu-id="21871-199">hello HTTP Method used for hello operation.</span></span> <span data-ttu-id="21871-200">Örneğin, alın.</span><span class="sxs-lookup"><span data-stu-id="21871-200">For example, GET.</span></span> |
| <span data-ttu-id="21871-201">Yol</span><span class="sxs-lookup"><span data-stu-id="21871-201">Path</span></span> |<span data-ttu-id="21871-202">Dize</span><span class="sxs-lookup"><span data-stu-id="21871-202">String</span></span> |<span data-ttu-id="21871-203">Merhaba yolu hello işlem üzerinde gerçekleştirildi</span><span class="sxs-lookup"><span data-stu-id="21871-203">hello path hello operation was performed on</span></span> |
| <span data-ttu-id="21871-204">RequestContentLength</span><span class="sxs-lookup"><span data-stu-id="21871-204">RequestContentLength</span></span> |<span data-ttu-id="21871-205">Int</span><span class="sxs-lookup"><span data-stu-id="21871-205">int</span></span> |<span data-ttu-id="21871-206">Merhaba HTTP isteğinin Hello içerik uzunluğu</span><span class="sxs-lookup"><span data-stu-id="21871-206">hello content length of hello HTTP request</span></span> |
| <span data-ttu-id="21871-207">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="21871-207">ClientRequestId</span></span> |<span data-ttu-id="21871-208">Dize</span><span class="sxs-lookup"><span data-stu-id="21871-208">String</span></span> |<span data-ttu-id="21871-209">Bu istek benzersiz olarak tanıtan hello tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="21871-209">hello identifier that uniquely identifies this request</span></span> |
| <span data-ttu-id="21871-210">StartTime</span><span class="sxs-lookup"><span data-stu-id="21871-210">StartTime</span></span> |<span data-ttu-id="21871-211">Dize</span><span class="sxs-lookup"><span data-stu-id="21871-211">String</span></span> |<span data-ttu-id="21871-212">hangi hello alınan sunucu hello isteği Hello zaman</span><span class="sxs-lookup"><span data-stu-id="21871-212">hello time at which hello server received hello request</span></span> |
| <span data-ttu-id="21871-213">EndTime</span><span class="sxs-lookup"><span data-stu-id="21871-213">EndTime</span></span> |<span data-ttu-id="21871-214">Dize</span><span class="sxs-lookup"><span data-stu-id="21871-214">String</span></span> |<span data-ttu-id="21871-215">Merhaba zaman hangi hello sunucu bir yanıt gönderdi.</span><span class="sxs-lookup"><span data-stu-id="21871-215">hello time at which hello server sent a response</span></span> |

### <a name="audit-logs"></a><span data-ttu-id="21871-216">Denetim günlükleri</span><span class="sxs-lookup"><span data-stu-id="21871-216">Audit logs</span></span>

<span data-ttu-id="21871-217">Merhaba JSON biçimli Denetim günlüğüne örnek girişi İşte.</span><span class="sxs-lookup"><span data-stu-id="21871-217">Here's a sample entry in hello JSON-formatted audit log.</span></span> <span data-ttu-id="21871-218">Her bir blob olarak adlandırılan bir kök nesnesi vardır **kayıtları** günlük nesnelerinin bir dizisi içerir.</span><span class="sxs-lookup"><span data-stu-id="21871-218">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records":
      [        
        . . . .
        ,
        {
             "time": "2016-07-28T19:15:16.245Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_ANALYTICS_account_name>",
             "category": "Audit",
             "operationName": "JobSubmitted",
             "identity": "user@somewhere.com",
             "properties": {
                 "JobId":"D74B928F-5194-4E6C-971F-C27026C290E6",
                 "JobName": "New Job",
                 "JobRuntimeName": "default",
                 "SubmitTime": "7/28/2016 7:14:57 PM"
                 }
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a><span data-ttu-id="21871-219">Denetim günlüğü şeması</span><span class="sxs-lookup"><span data-stu-id="21871-219">Audit log schema</span></span>

| <span data-ttu-id="21871-220">Ad</span><span class="sxs-lookup"><span data-stu-id="21871-220">Name</span></span> | <span data-ttu-id="21871-221">Tür</span><span class="sxs-lookup"><span data-stu-id="21871-221">Type</span></span> | <span data-ttu-id="21871-222">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21871-222">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21871-223">time</span><span class="sxs-lookup"><span data-stu-id="21871-223">time</span></span> |<span data-ttu-id="21871-224">Dize</span><span class="sxs-lookup"><span data-stu-id="21871-224">String</span></span> |<span data-ttu-id="21871-225">Merhaba günlüğünün Hello zaman damgası (UTC) cinsinden</span><span class="sxs-lookup"><span data-stu-id="21871-225">hello timestamp (in UTC) of hello log</span></span> |
| <span data-ttu-id="21871-226">resourceId</span><span class="sxs-lookup"><span data-stu-id="21871-226">resourceId</span></span> |<span data-ttu-id="21871-227">Dize</span><span class="sxs-lookup"><span data-stu-id="21871-227">String</span></span> |<span data-ttu-id="21871-228">işlemi sürdü hello kaynak Hello tanıtıcısı yerleştirin</span><span class="sxs-lookup"><span data-stu-id="21871-228">hello identifier of hello resource that operation took place on</span></span> |
| <span data-ttu-id="21871-229">category</span><span class="sxs-lookup"><span data-stu-id="21871-229">category</span></span> |<span data-ttu-id="21871-230">Dize</span><span class="sxs-lookup"><span data-stu-id="21871-230">String</span></span> |<span data-ttu-id="21871-231">Merhaba günlük kategorisi.</span><span class="sxs-lookup"><span data-stu-id="21871-231">hello log category.</span></span> <span data-ttu-id="21871-232">Örneğin, **denetim**.</span><span class="sxs-lookup"><span data-stu-id="21871-232">For example, **Audit**.</span></span> |
| <span data-ttu-id="21871-233">operationName</span><span class="sxs-lookup"><span data-stu-id="21871-233">operationName</span></span> |<span data-ttu-id="21871-234">Dize</span><span class="sxs-lookup"><span data-stu-id="21871-234">String</span></span> |<span data-ttu-id="21871-235">Oturum hello işlemin adı.</span><span class="sxs-lookup"><span data-stu-id="21871-235">Name of hello operation that is logged.</span></span> <span data-ttu-id="21871-236">Örneğin, JobSubmitted.</span><span class="sxs-lookup"><span data-stu-id="21871-236">For example, JobSubmitted.</span></span> |
| <span data-ttu-id="21871-237">resultType</span><span class="sxs-lookup"><span data-stu-id="21871-237">resultType</span></span> |<span data-ttu-id="21871-238">Dize</span><span class="sxs-lookup"><span data-stu-id="21871-238">String</span></span> |<span data-ttu-id="21871-239">Bir alt durum hello iş durumu (operationName).</span><span class="sxs-lookup"><span data-stu-id="21871-239">A substatus for hello job status (operationName).</span></span> |
| <span data-ttu-id="21871-240">resultSignature</span><span class="sxs-lookup"><span data-stu-id="21871-240">resultSignature</span></span> |<span data-ttu-id="21871-241">Dize</span><span class="sxs-lookup"><span data-stu-id="21871-241">String</span></span> |<span data-ttu-id="21871-242">Merhaba iş durumu (operationName) ilgili ek ayrıntılar.</span><span class="sxs-lookup"><span data-stu-id="21871-242">Additional details on hello job status (operationName).</span></span> |
| <span data-ttu-id="21871-243">identity</span><span class="sxs-lookup"><span data-stu-id="21871-243">identity</span></span> |<span data-ttu-id="21871-244">Dize</span><span class="sxs-lookup"><span data-stu-id="21871-244">String</span></span> |<span data-ttu-id="21871-245">İstenen hello işlemi hello kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="21871-245">hello user that requested hello operation.</span></span> <span data-ttu-id="21871-246">Örneğin, susan@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="21871-246">For example, susan@contoso.com.</span></span> |
| <span data-ttu-id="21871-247">properties</span><span class="sxs-lookup"><span data-stu-id="21871-247">properties</span></span> |<span data-ttu-id="21871-248">JSON</span><span class="sxs-lookup"><span data-stu-id="21871-248">JSON</span></span> |<span data-ttu-id="21871-249">Ayrıntılar için Hello sonraki bölümüne (Denetim günlüğü özellikleri Şeması) bakın</span><span class="sxs-lookup"><span data-stu-id="21871-249">See hello next section (Audit log properties schema) for details</span></span> |

> [!NOTE]
> <span data-ttu-id="21871-250">**resultType** ve **resultSignature** bir işlemin hello sonucunu bilgileri sağlayın ve bir işlemin tamamlanması, yalnızca bir değer içerebilir.</span><span class="sxs-lookup"><span data-stu-id="21871-250">**resultType** and **resultSignature** provide information on hello result of an operation, and only contain a value if an operation has completed.</span></span> <span data-ttu-id="21871-251">Örneğin, yalnızca bir değer içerir, **operationName** değerini içeren **JobStarted** veya **JobEnded**.</span><span class="sxs-lookup"><span data-stu-id="21871-251">For example, they only contain a value when **operationName** contains a value of **JobStarted** or **JobEnded**.</span></span>
>
>

#### <a name="audit-log-properties-schema"></a><span data-ttu-id="21871-252">Denetim günlüğü özellikleri şeması</span><span class="sxs-lookup"><span data-stu-id="21871-252">Audit log properties schema</span></span>

| <span data-ttu-id="21871-253">Ad</span><span class="sxs-lookup"><span data-stu-id="21871-253">Name</span></span> | <span data-ttu-id="21871-254">Tür</span><span class="sxs-lookup"><span data-stu-id="21871-254">Type</span></span> | <span data-ttu-id="21871-255">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21871-255">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21871-256">JobId</span><span class="sxs-lookup"><span data-stu-id="21871-256">JobId</span></span> |<span data-ttu-id="21871-257">Dize</span><span class="sxs-lookup"><span data-stu-id="21871-257">String</span></span> |<span data-ttu-id="21871-258">Merhaba kimliği atanan toohello işi</span><span class="sxs-lookup"><span data-stu-id="21871-258">hello ID assigned toohello job</span></span> |
| <span data-ttu-id="21871-259">JobName</span><span class="sxs-lookup"><span data-stu-id="21871-259">JobName</span></span> |<span data-ttu-id="21871-260">Dize</span><span class="sxs-lookup"><span data-stu-id="21871-260">String</span></span> |<span data-ttu-id="21871-261">Merhaba işi için sağlanan hello adı</span><span class="sxs-lookup"><span data-stu-id="21871-261">hello name that was provided for hello job</span></span> |
| <span data-ttu-id="21871-262">JobRunTime</span><span class="sxs-lookup"><span data-stu-id="21871-262">JobRunTime</span></span> |<span data-ttu-id="21871-263">Dize</span><span class="sxs-lookup"><span data-stu-id="21871-263">String</span></span> |<span data-ttu-id="21871-264">Merhaba çalışma zamanı tooprocess hello iş kullanılan</span><span class="sxs-lookup"><span data-stu-id="21871-264">hello runtime used tooprocess hello job</span></span> |
| <span data-ttu-id="21871-265">SubmitTime</span><span class="sxs-lookup"><span data-stu-id="21871-265">SubmitTime</span></span> |<span data-ttu-id="21871-266">Dize</span><span class="sxs-lookup"><span data-stu-id="21871-266">String</span></span> |<span data-ttu-id="21871-267">Başlangıç saati (UTC) bu hello iş gönderildi</span><span class="sxs-lookup"><span data-stu-id="21871-267">hello time (in UTC) that hello job was submitted</span></span> |
| <span data-ttu-id="21871-268">StartTime</span><span class="sxs-lookup"><span data-stu-id="21871-268">StartTime</span></span> |<span data-ttu-id="21871-269">Dize</span><span class="sxs-lookup"><span data-stu-id="21871-269">String</span></span> |<span data-ttu-id="21871-270">gönderisine (UTC) sonra çalışan Hello zaman hello iş başlatıldı</span><span class="sxs-lookup"><span data-stu-id="21871-270">hello time hello job started running after submission (in UTC)</span></span> |
| <span data-ttu-id="21871-271">EndTime</span><span class="sxs-lookup"><span data-stu-id="21871-271">EndTime</span></span> |<span data-ttu-id="21871-272">Dize</span><span class="sxs-lookup"><span data-stu-id="21871-272">String</span></span> |<span data-ttu-id="21871-273">Merhaba süresi hello işi sona erdi</span><span class="sxs-lookup"><span data-stu-id="21871-273">hello time hello job ended</span></span> |
| <span data-ttu-id="21871-274">Paralellik</span><span class="sxs-lookup"><span data-stu-id="21871-274">Parallelism</span></span> |<span data-ttu-id="21871-275">Dize</span><span class="sxs-lookup"><span data-stu-id="21871-275">String</span></span> |<span data-ttu-id="21871-276">Data Lake Analytics birim gönderme sırasında bu iş için istenen Hello sayısı</span><span class="sxs-lookup"><span data-stu-id="21871-276">hello number of Data Lake Analytics units requested for this job during submission</span></span> |

> [!NOTE]
> <span data-ttu-id="21871-277">**SubmitTime**, **StartTime**, **EndTime**, ve **paralellik** üzerinde bir işlemi bilgileri sağlayın.</span><span class="sxs-lookup"><span data-stu-id="21871-277">**SubmitTime**, **StartTime**, **EndTime**, and **Parallelism** provide information on an operation.</span></span> <span data-ttu-id="21871-278">Bu girişler yalnızca bir değer varsa, işlemi başlatıldı veya tamamlanmış olan içerir.</span><span class="sxs-lookup"><span data-stu-id="21871-278">These entries only contain a value if that operation has started or completed.</span></span> <span data-ttu-id="21871-279">Örneğin, **SubmitTime** yalnızca sonra bir değer içeriyor **operationName** hello değerine sahip **JobSubmitted**.</span><span class="sxs-lookup"><span data-stu-id="21871-279">For example, **SubmitTime** only contains a value after **operationName** has hello value **JobSubmitted**.</span></span>

## <a name="process-hello-log-data"></a><span data-ttu-id="21871-280">İşlem hello günlük verileri</span><span class="sxs-lookup"><span data-stu-id="21871-280">Process hello log data</span></span>

<span data-ttu-id="21871-281">Azure Data Lake Analytics hakkında bir örnek sağlar tooprocess ve hello günlük verilerini çözümleyin.</span><span class="sxs-lookup"><span data-stu-id="21871-281">Azure Data Lake Analytics provides a sample on how tooprocess and analyze hello log data.</span></span> <span data-ttu-id="21871-282">Merhaba örneğini şurada bulabilirsiniz [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span><span class="sxs-lookup"><span data-stu-id="21871-282">You can find hello sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span></span>

## <a name="next-steps"></a><span data-ttu-id="21871-283">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="21871-283">Next steps</span></span>
* [<span data-ttu-id="21871-284">Azure Data Lake Analytics'e genel bakış</span><span class="sxs-lookup"><span data-stu-id="21871-284">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
