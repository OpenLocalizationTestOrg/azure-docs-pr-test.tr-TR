---
title: "Azure Data Lake Store için tanılama günlüklerini aaaViewing | Microsoft Docs"
description: "Anlamak nasıl toosetup ve erişim Azure Data Lake Store için tanılama günlükleri "
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: f6e75eb1-d0ae-47cf-bdb8-06684b7c0a94
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 11fbf7f517f97abdcaf809c1ebeeb51424ab2c1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-store"></a><span data-ttu-id="ce8cc-103">Azure Data Lake Store için tanılama günlüklerine erişme</span><span class="sxs-lookup"><span data-stu-id="ce8cc-103">Accessing diagnostic logs for Azure Data Lake Store</span></span>
<span data-ttu-id="ce8cc-104">Hesabınız için nasıl tooenable tanılama günlük Data Lake Store hesabınızı ve nasıl tooview hello günlükleri için toplanan hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-104">Learn about how tooenable diagnostic logging for your Data Lake Store account and how tooview hello logs collected for your account.</span></span>

<span data-ttu-id="ce8cc-105">Kuruluşlar hello verileri, hello verileri ne sıklıkta erişildiğine, ne kadar veri erişen kullanıcılar listesi gibi bilgiler sağlayan hesap toocollect veri erişimi denetim izleri hello depolanan kendi Azure Data Lake Store için tanılama günlük kaydını etkinleştirebilirsiniz Hesap, vs.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-105">Organizations can enable diagnostic logging for their Azure Data Lake Store account toocollect data access audit trails that provides information such as list of users accessing hello data, how frequently hello data is accessed, how much data is stored in hello account, etc.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce8cc-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ce8cc-106">Prerequisites</span></span>
* <span data-ttu-id="ce8cc-107">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-107">**An Azure subscription**.</span></span> <span data-ttu-id="ce8cc-108">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ce8cc-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ce8cc-109">**Azure Data Lake Store hesabı**.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-109">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="ce8cc-110">Merhaba yönergeleri izleyin [Azure Data Lake hello Azure Portal kullanarak Store ile çalışmaya başlama](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ce8cc-110">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](data-lake-store-get-started-portal.md).</span></span>

## <a name="enable-diagnostic-logging-for-your-data-lake-store-account"></a><span data-ttu-id="ce8cc-111">Data Lake Store hesabınız için tanılama günlük kaydını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="ce8cc-111">Enable diagnostic logging for your Data Lake Store account</span></span>
1. <span data-ttu-id="ce8cc-112">Yeni toohello oturum [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ce8cc-112">Sign on toohello new [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ce8cc-113">Data Lake Store hesabınızı açın ve Data Lake Store hesabı dikey penceresinden tıklayın **ayarları**ve ardından **tanılama günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-113">Open your Data Lake Store account, and from your Data Lake Store account blade, click **Settings**, and then click **Diagnostic logs**.</span></span>
3. <span data-ttu-id="ce8cc-114">Merhaba, **tanılama günlükleri** dikey penceresinde tıklatın **tanılamayı açın**.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-114">In hello **Diagnostics logs** blade, click **Turn on diagnostics**.</span></span>

    <span data-ttu-id="ce8cc-115">![Tanılama günlük kaydını etkinleştir](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "tanılama günlüklerini etkinleştirme")</span><span class="sxs-lookup"><span data-stu-id="ce8cc-115">![Enable diagnostic logging](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "Enable diagnostic logs")</span></span>

3. <span data-ttu-id="ce8cc-116">Merhaba, **tanılama** dikey penceresinde hello değişiklikleri tooconfigure tanılama günlük kaydını aşağıdaki olun.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-116">In hello **Diagnostic** blade, make hello following changes tooconfigure diagnostic logging.</span></span>
   
    <span data-ttu-id="ce8cc-117">![Tanılama günlük kaydını etkinleştir](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "tanılama günlüklerini etkinleştirme")</span><span class="sxs-lookup"><span data-stu-id="ce8cc-117">![Enable diagnostic logging](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span></span>
   
   * <span data-ttu-id="ce8cc-118">Ayarlama **durum** çok**üzerinde** tooenable tanılama günlük.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-118">Set **Status** too**On** tooenable diagnostic logging.</span></span>
   * <span data-ttu-id="ce8cc-119">Farklı şekillerde toostore/işlem hello veri seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-119">You can choose toostore/process hello data in different ways.</span></span>
     
        * <span data-ttu-id="ce8cc-120">Çok olarak Hello seçeneğini**arşiv tooa depolama hesabı** toostore tooan Azure depolama hesabı günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-120">Select hello option too**Archive tooa storage account** toostore logs tooan Azure Storage account.</span></span> <span data-ttu-id="ce8cc-121">Daha sonraki bir tarihte toplu işlenen tooarchive hello veri istiyorsanız bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-121">You use this option if you want tooarchive hello data that will be batch-processed at a later date.</span></span> <span data-ttu-id="ce8cc-122">Bu seçeneği belirlerseniz toosave hello günlükleri için bir Azure Storage hesabı sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-122">If you select this option you must provide an Azure Storage account toosave hello logs to.</span></span>
        
        * <span data-ttu-id="ce8cc-123">Çok olarak Hello seçeneğini**tooan event hub'ı akış** toostream günlük veri tooan Azure olay hub'ı.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-123">Select hello option too**Stream tooan event hub** toostream log data tooan Azure Event Hub.</span></span> <span data-ttu-id="ce8cc-124">Büyük olasılıkla bir aşağı akış işleme varsa bu seçeneği kullanacağı gerçek zamanlı tooanalyze gelen günlüklerine kanalı.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-124">Most likely you will use this option if you have a downstream processing pipeline tooanalyze incoming logs at real time.</span></span> <span data-ttu-id="ce8cc-125">Bu seçeneği belirlerseniz, hello Azure Event Hub'ın toouse istediğiniz hello ayrıntılarını sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-125">If you select this option, you must provide hello details for hello Azure Event Hub you want toouse.</span></span>

        * <span data-ttu-id="ce8cc-126">Çok olarak Hello seçeneğini**tooLog Analytics Gönder** toouse hello Azure günlük analizi hizmeti tooanalyze oluşturulan hello günlük verileri.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-126">Select hello option too**Send tooLog Analytics** toouse hello Azure Log Analytics service tooanalyze hello generated log data.</span></span> <span data-ttu-id="ce8cc-127">Bu seçeneği seçerseniz, kullanım hello Günlük çözümlemesi gerçekleştireceği hello hello Operations Management Suite çalışma alanı için ayrıntıları sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-127">If you select this option, you must provide hello details for hello Operations Management Suite workspace that you would use hello perform log analysis.</span></span>
     
   * <span data-ttu-id="ce8cc-128">Tooget denetim günlüklerini veya istek günlüklerini ya da hem isteyip istemediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-128">Specify whether you want tooget audit logs or request logs or both.</span></span>
   * <span data-ttu-id="ce8cc-129">Merhaba hello veri korunması gereken gün sayısını belirtin.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-129">Specify hello number of days for which hello data must be retained.</span></span> <span data-ttu-id="ce8cc-130">Bekletme, yalnızca Azure depolama hesabı tooarchive günlük verileri kullanıyorsanız geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-130">Retention is only applicable if you are using Azure storage account tooarchive log data.</span></span>
   * <span data-ttu-id="ce8cc-131">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-131">Click **Save**.</span></span>

<span data-ttu-id="ce8cc-132">Tanılama ayarları etkinleştirildiğinde, hello günlüklerini hello izleyebilirsiniz **tanılama günlüklerini** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-132">Once you have enabled diagnostic settings, you can watch hello logs in hello **Diagnostic Logs** tab.</span></span>

## <a name="view-diagnostic-logs-for-your-data-lake-store-account"></a><span data-ttu-id="ce8cc-133">Data Lake Store hesabınız için tanılama günlüklerini görüntüle</span><span class="sxs-lookup"><span data-stu-id="ce8cc-133">View diagnostic logs for your Data Lake Store account</span></span>
<span data-ttu-id="ce8cc-134">Data Lake Store hesabınız için tooview hello günlük verileri iki yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-134">There are two ways tooview hello log data for your Data Lake Store account.</span></span>

* <span data-ttu-id="ce8cc-135">Merhaba Data Lake Store hesabından ayarlarını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="ce8cc-135">From hello Data Lake Store account settings view</span></span>
* <span data-ttu-id="ce8cc-136">Merhaba verilerinin depolandığı hello Azure depolama hesabından</span><span class="sxs-lookup"><span data-stu-id="ce8cc-136">From hello Azure Storage account where hello data is stored</span></span>

### <a name="using-hello-data-lake-store-settings-view"></a><span data-ttu-id="ce8cc-137">Hello kullanarak Data Lake deposu ayarları görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="ce8cc-137">Using hello Data Lake Store Settings view</span></span>
1. <span data-ttu-id="ce8cc-138">Data Lake Store hesabınızdaki **ayarları** dikey penceresinde tıklatın **tanılama günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-138">From your Data Lake Store account **Settings** blade, click **Diagnostic Logs**.</span></span>
   
    <span data-ttu-id="ce8cc-139">![Görünüm tanılama günlük](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "tanılama günlükleri görüntüleme")</span><span class="sxs-lookup"><span data-stu-id="ce8cc-139">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span></span> 
2. <span data-ttu-id="ce8cc-140">Merhaba, **tanılama günlükleri** dikey penceresinde hello günlükleri tarafından kategorilere görmelisiniz **denetim günlüklerini** ve **isteği günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-140">In hello **Diagnostic Logs** blade, you should see hello logs categorized by **Audit Logs** and **Request Logs**.</span></span>
   
   * <span data-ttu-id="ce8cc-141">İstek günlüklerini hello Data Lake Store hesabı üzerinde yapılan her API isteği yakalayın.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-141">Request logs capture every API request made on hello Data Lake Store account.</span></span>
   * <span data-ttu-id="ce8cc-142">Denetim günlüklerini benzer toorequest günlüklerin ancak hello Data Lake Store hesabında gerçekleştirilen hello işlemler çok daha ayrıntılı bir dökümünü sağlar.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-142">Audit Logs are similar toorequest Logs but provide a much more detailed breakdown of hello operations being performed on hello Data Lake Store account.</span></span> <span data-ttu-id="ce8cc-143">Örneğin, bir istek günlüklerini tek karşıya yükleme API çağrısında hello denetim günlüklerini "Ekle" işlemlerinde neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-143">For example, a single upload API call in request logs might result in multiple "Append" operations in hello audit logs.</span></span>
3. <span data-ttu-id="ce8cc-144">Merhaba tıklatın **karşıdan** her karşı bağlantı günlüğü girişi toodownload hello günlükleri.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-144">Click hello **Download** link against each log entry toodownload hello logs.</span></span>

### <a name="from-hello-azure-storage-account-that-contains-log-data"></a><span data-ttu-id="ce8cc-145">Azure depolama hesabı Hello günlük verilerini içeren</span><span class="sxs-lookup"><span data-stu-id="ce8cc-145">From hello Azure Storage account that contains log data</span></span>
1. <span data-ttu-id="ce8cc-146">Hello Azure depolama hesabı için günlük kaydını Data Lake Store ile ilişkili dikey penceresini açın ve Bloblar'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-146">Open hello Azure Storage account blade associated with Data Lake Store for logging, and then click Blobs.</span></span> <span data-ttu-id="ce8cc-147">Merhaba **Blob hizmeti** iki kapsayıcı dikey penceresinde listelenir.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-147">hello **Blob service** blade lists two containers.</span></span>
   
    <span data-ttu-id="ce8cc-148">![Görünüm tanılama günlük](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "tanılama günlükleri görüntüleme")</span><span class="sxs-lookup"><span data-stu-id="ce8cc-148">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span></span>
   
   * <span data-ttu-id="ce8cc-149">Merhaba kapsayıcı **Öngörüler günlükleri denetim** hello denetim günlüklerini içerir.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-149">hello container **insights-logs-audit** contains hello audit logs.</span></span>
   * <span data-ttu-id="ce8cc-150">Merhaba kapsayıcı **Öngörüler günlükleri istekleri** hello isteği günlükleri içerir.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-150">hello container **insights-logs-requests** contains hello request logs.</span></span>
2. <span data-ttu-id="ce8cc-151">Bu kapsayıcılara hello günlükleri yapı izlenerek hello altında depolanır.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-151">Within these containers, hello logs are stored under hello following structure.</span></span>
   
    <span data-ttu-id="ce8cc-152">![Görünüm tanılama günlük](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "tanılama günlükleri görüntüleme")</span><span class="sxs-lookup"><span data-stu-id="ce8cc-152">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "View diagnostic logs")</span></span>
   
    <span data-ttu-id="ce8cc-153">Örnek olarak, hello tam yolunu tooan denetim günlüğü olabilir`https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`</span><span class="sxs-lookup"><span data-stu-id="ce8cc-153">As an example, hello complete path tooan audit log could be `https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`</span></span>
   
    <span data-ttu-id="ce8cc-154">Merhaba tam yolunu tooa istek günlüğü similary, olabilir`https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`</span><span class="sxs-lookup"><span data-stu-id="ce8cc-154">Similary, hello complete path tooa request log could be `https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`</span></span>

## <a name="understand-hello-structure-of-hello-log-data"></a><span data-ttu-id="ce8cc-155">Merhaba günlük verilerini Hello yapısını anlama</span><span class="sxs-lookup"><span data-stu-id="ce8cc-155">Understand hello structure of hello log data</span></span>
<span data-ttu-id="ce8cc-156">Denetim hello ve günlüklerin bir JSON biçiminde isteyin.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-156">hello audit and request logs are in a JSON format.</span></span> <span data-ttu-id="ce8cc-157">Bu bölümde, istek için JSON hello yapısı bakın ve Denetim günlükleri.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-157">In this section, we look at hello structure of JSON for request and audit logs.</span></span>

### <a name="request-logs"></a><span data-ttu-id="ce8cc-158">İstek günlükleri</span><span class="sxs-lookup"><span data-stu-id="ce8cc-158">Request logs</span></span>
<span data-ttu-id="ce8cc-159">Merhaba JSON biçimli istek günlüğünde örnek girişi İşte.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-159">Here's a sample entry in hello JSON-formatted request log.</span></span> <span data-ttu-id="ce8cc-160">Her bir blob olarak adlandırılan bir kök nesnesi vardır **kayıtları** günlük nesnelerinin bir dizisi içerir.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-160">Each blob has one root object called **records** that contains an array of log objects.</span></span>

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Requests",
             "operationName": "GETCustomerIngressEgress",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {"HttpMethod":"GET","Path":"/webhdfs/v1/Samples/Outputs/Drivers.csv","RequestContentLength":0,"ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8","StartTime":"2016-07-07T21:02:52.472Z","EndTime":"2016-07-07T21:02:53.456Z"}
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a><span data-ttu-id="ce8cc-161">İstek günlüğü şeması</span><span class="sxs-lookup"><span data-stu-id="ce8cc-161">Request log schema</span></span>
| <span data-ttu-id="ce8cc-162">Ad</span><span class="sxs-lookup"><span data-stu-id="ce8cc-162">Name</span></span> | <span data-ttu-id="ce8cc-163">Tür</span><span class="sxs-lookup"><span data-stu-id="ce8cc-163">Type</span></span> | <span data-ttu-id="ce8cc-164">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ce8cc-164">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ce8cc-165">time</span><span class="sxs-lookup"><span data-stu-id="ce8cc-165">time</span></span> |<span data-ttu-id="ce8cc-166">Dize</span><span class="sxs-lookup"><span data-stu-id="ce8cc-166">String</span></span> |<span data-ttu-id="ce8cc-167">Merhaba günlüğünün Hello zaman damgası (UTC) cinsinden</span><span class="sxs-lookup"><span data-stu-id="ce8cc-167">hello timestamp (in UTC) of hello log</span></span> |
| <span data-ttu-id="ce8cc-168">resourceId</span><span class="sxs-lookup"><span data-stu-id="ce8cc-168">resourceId</span></span> |<span data-ttu-id="ce8cc-169">Dize</span><span class="sxs-lookup"><span data-stu-id="ce8cc-169">String</span></span> |<span data-ttu-id="ce8cc-170">Merhaba işlemi sürdü hello kaynak Kimliğini yerleştirin</span><span class="sxs-lookup"><span data-stu-id="ce8cc-170">hello ID of hello resource that operation took place on</span></span> |
| <span data-ttu-id="ce8cc-171">category</span><span class="sxs-lookup"><span data-stu-id="ce8cc-171">category</span></span> |<span data-ttu-id="ce8cc-172">Dize</span><span class="sxs-lookup"><span data-stu-id="ce8cc-172">String</span></span> |<span data-ttu-id="ce8cc-173">Merhaba günlük kategorisi.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-173">hello log category.</span></span> <span data-ttu-id="ce8cc-174">Örneğin, **istekleri**.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-174">For example, **Requests**.</span></span> |
| <span data-ttu-id="ce8cc-175">operationName</span><span class="sxs-lookup"><span data-stu-id="ce8cc-175">operationName</span></span> |<span data-ttu-id="ce8cc-176">Dize</span><span class="sxs-lookup"><span data-stu-id="ce8cc-176">String</span></span> |<span data-ttu-id="ce8cc-177">Oturum hello işlemin adı.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-177">Name of hello operation that is logged.</span></span> <span data-ttu-id="ce8cc-178">Örneğin, getfilestatus.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-178">For example, getfilestatus.</span></span> |
| <span data-ttu-id="ce8cc-179">resultType</span><span class="sxs-lookup"><span data-stu-id="ce8cc-179">resultType</span></span> |<span data-ttu-id="ce8cc-180">Dize</span><span class="sxs-lookup"><span data-stu-id="ce8cc-180">String</span></span> |<span data-ttu-id="ce8cc-181">Merhaba işlemi, örneğin, 200 Hello durumu.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-181">hello status of hello operation, For example, 200.</span></span> |
| <span data-ttu-id="ce8cc-182">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="ce8cc-182">callerIpAddress</span></span> |<span data-ttu-id="ce8cc-183">Dize</span><span class="sxs-lookup"><span data-stu-id="ce8cc-183">String</span></span> |<span data-ttu-id="ce8cc-184">Merhaba istekte hello istemcinin Hello IP adresi</span><span class="sxs-lookup"><span data-stu-id="ce8cc-184">hello IP address of hello client making hello request</span></span> |
| <span data-ttu-id="ce8cc-185">correlationId</span><span class="sxs-lookup"><span data-stu-id="ce8cc-185">correlationId</span></span> |<span data-ttu-id="ce8cc-186">Dize</span><span class="sxs-lookup"><span data-stu-id="ce8cc-186">String</span></span> |<span data-ttu-id="ce8cc-187">toogroup bir dizi ilgili günlük girişlerini birlikte kullanılabilecek hello günlük Hello kimliği</span><span class="sxs-lookup"><span data-stu-id="ce8cc-187">hello id of hello log that can used toogroup together a set of related log entries</span></span> |
| <span data-ttu-id="ce8cc-188">identity</span><span class="sxs-lookup"><span data-stu-id="ce8cc-188">identity</span></span> |<span data-ttu-id="ce8cc-189">Nesne</span><span class="sxs-lookup"><span data-stu-id="ce8cc-189">Object</span></span> |<span data-ttu-id="ce8cc-190">Merhaba günlük oluşturulan hello kimliği</span><span class="sxs-lookup"><span data-stu-id="ce8cc-190">hello identity that generated hello log</span></span> |
| <span data-ttu-id="ce8cc-191">properties</span><span class="sxs-lookup"><span data-stu-id="ce8cc-191">properties</span></span> |<span data-ttu-id="ce8cc-192">JSON</span><span class="sxs-lookup"><span data-stu-id="ce8cc-192">JSON</span></span> |<span data-ttu-id="ce8cc-193">Ayrıntılar için aşağıya bakın</span><span class="sxs-lookup"><span data-stu-id="ce8cc-193">See below for details</span></span> |

#### <a name="request-log-properties-schema"></a><span data-ttu-id="ce8cc-194">İstek günlüğü özellikleri şeması</span><span class="sxs-lookup"><span data-stu-id="ce8cc-194">Request log properties schema</span></span>
| <span data-ttu-id="ce8cc-195">Ad</span><span class="sxs-lookup"><span data-stu-id="ce8cc-195">Name</span></span> | <span data-ttu-id="ce8cc-196">Tür</span><span class="sxs-lookup"><span data-stu-id="ce8cc-196">Type</span></span> | <span data-ttu-id="ce8cc-197">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ce8cc-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ce8cc-198">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="ce8cc-198">HttpMethod</span></span> |<span data-ttu-id="ce8cc-199">Dize</span><span class="sxs-lookup"><span data-stu-id="ce8cc-199">String</span></span> |<span data-ttu-id="ce8cc-200">Merhaba HTTP hello işlemi için kullanılan yöntem.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-200">hello HTTP Method used for hello operation.</span></span> <span data-ttu-id="ce8cc-201">Örneğin, alın.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-201">For example, GET.</span></span> |
| <span data-ttu-id="ce8cc-202">Yol</span><span class="sxs-lookup"><span data-stu-id="ce8cc-202">Path</span></span> |<span data-ttu-id="ce8cc-203">Dize</span><span class="sxs-lookup"><span data-stu-id="ce8cc-203">String</span></span> |<span data-ttu-id="ce8cc-204">Merhaba yolu hello işlem üzerinde gerçekleştirildi</span><span class="sxs-lookup"><span data-stu-id="ce8cc-204">hello path hello operation was performed on</span></span> |
| <span data-ttu-id="ce8cc-205">RequestContentLength</span><span class="sxs-lookup"><span data-stu-id="ce8cc-205">RequestContentLength</span></span> |<span data-ttu-id="ce8cc-206">Int</span><span class="sxs-lookup"><span data-stu-id="ce8cc-206">int</span></span> |<span data-ttu-id="ce8cc-207">Merhaba HTTP isteğinin Hello içerik uzunluğu</span><span class="sxs-lookup"><span data-stu-id="ce8cc-207">hello content length of hello HTTP request</span></span> |
| <span data-ttu-id="ce8cc-208">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="ce8cc-208">ClientRequestId</span></span> |<span data-ttu-id="ce8cc-209">Dize</span><span class="sxs-lookup"><span data-stu-id="ce8cc-209">String</span></span> |<span data-ttu-id="ce8cc-210">Merhaba bu istek benzersiz olarak tanıtan kimliği</span><span class="sxs-lookup"><span data-stu-id="ce8cc-210">hello Id that uniquely identifies this request</span></span> |
| <span data-ttu-id="ce8cc-211">StartTime</span><span class="sxs-lookup"><span data-stu-id="ce8cc-211">StartTime</span></span> |<span data-ttu-id="ce8cc-212">Dize</span><span class="sxs-lookup"><span data-stu-id="ce8cc-212">String</span></span> |<span data-ttu-id="ce8cc-213">hangi hello alınan sunucu hello isteği Hello zaman</span><span class="sxs-lookup"><span data-stu-id="ce8cc-213">hello time at which hello server received hello request</span></span> |
| <span data-ttu-id="ce8cc-214">EndTime</span><span class="sxs-lookup"><span data-stu-id="ce8cc-214">EndTime</span></span> |<span data-ttu-id="ce8cc-215">Dize</span><span class="sxs-lookup"><span data-stu-id="ce8cc-215">String</span></span> |<span data-ttu-id="ce8cc-216">Merhaba zaman hangi hello sunucu bir yanıt gönderdi.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-216">hello time at which hello server sent a response</span></span> |

### <a name="audit-logs"></a><span data-ttu-id="ce8cc-217">Denetim günlükleri</span><span class="sxs-lookup"><span data-stu-id="ce8cc-217">Audit logs</span></span>
<span data-ttu-id="ce8cc-218">Merhaba JSON biçimli Denetim günlüğüne örnek girişi İşte.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-218">Here's a sample entry in hello JSON-formatted audit log.</span></span> <span data-ttu-id="ce8cc-219">Her bir blob olarak adlandırılan bir kök nesnesi vardır **kayıtları** günlük nesnelerinin bir dizisi içerir</span><span class="sxs-lookup"><span data-stu-id="ce8cc-219">Each blob has one root object called **records** that contains an array of log objects</span></span>

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-08T19:08:59.359Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Audit",
             "operationName": "SeOpenStream",
             "resultType": "0",
             "correlationId": "381110fc03534e1cb99ec52376ceebdf;Append_BrEKAmg;25.66.9.145",
             "identity": "A9DAFFAF-FFEE-4BB5-A4A0-1B6CBBF24355",
             "properties": {"StreamName":"adl://<data_lake_store_account_name>.azuredatalakestore.net/logs.csv"}
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a><span data-ttu-id="ce8cc-220">Denetim günlüğü şeması</span><span class="sxs-lookup"><span data-stu-id="ce8cc-220">Audit log schema</span></span>
| <span data-ttu-id="ce8cc-221">Ad</span><span class="sxs-lookup"><span data-stu-id="ce8cc-221">Name</span></span> | <span data-ttu-id="ce8cc-222">Tür</span><span class="sxs-lookup"><span data-stu-id="ce8cc-222">Type</span></span> | <span data-ttu-id="ce8cc-223">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ce8cc-223">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ce8cc-224">time</span><span class="sxs-lookup"><span data-stu-id="ce8cc-224">time</span></span> |<span data-ttu-id="ce8cc-225">Dize</span><span class="sxs-lookup"><span data-stu-id="ce8cc-225">String</span></span> |<span data-ttu-id="ce8cc-226">Merhaba günlüğünün Hello zaman damgası (UTC) cinsinden</span><span class="sxs-lookup"><span data-stu-id="ce8cc-226">hello timestamp (in UTC) of hello log</span></span> |
| <span data-ttu-id="ce8cc-227">resourceId</span><span class="sxs-lookup"><span data-stu-id="ce8cc-227">resourceId</span></span> |<span data-ttu-id="ce8cc-228">Dize</span><span class="sxs-lookup"><span data-stu-id="ce8cc-228">String</span></span> |<span data-ttu-id="ce8cc-229">Merhaba işlemi sürdü hello kaynak Kimliğini yerleştirin</span><span class="sxs-lookup"><span data-stu-id="ce8cc-229">hello ID of hello resource that operation took place on</span></span> |
| <span data-ttu-id="ce8cc-230">category</span><span class="sxs-lookup"><span data-stu-id="ce8cc-230">category</span></span> |<span data-ttu-id="ce8cc-231">Dize</span><span class="sxs-lookup"><span data-stu-id="ce8cc-231">String</span></span> |<span data-ttu-id="ce8cc-232">Merhaba günlük kategorisi.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-232">hello log category.</span></span> <span data-ttu-id="ce8cc-233">Örneğin, **denetim**.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-233">For example, **Audit**.</span></span> |
| <span data-ttu-id="ce8cc-234">operationName</span><span class="sxs-lookup"><span data-stu-id="ce8cc-234">operationName</span></span> |<span data-ttu-id="ce8cc-235">Dize</span><span class="sxs-lookup"><span data-stu-id="ce8cc-235">String</span></span> |<span data-ttu-id="ce8cc-236">Oturum hello işlemin adı.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-236">Name of hello operation that is logged.</span></span> <span data-ttu-id="ce8cc-237">Örneğin, getfilestatus.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-237">For example, getfilestatus.</span></span> |
| <span data-ttu-id="ce8cc-238">resultType</span><span class="sxs-lookup"><span data-stu-id="ce8cc-238">resultType</span></span> |<span data-ttu-id="ce8cc-239">Dize</span><span class="sxs-lookup"><span data-stu-id="ce8cc-239">String</span></span> |<span data-ttu-id="ce8cc-240">Merhaba işlemi, örneğin, 200 Hello durumu.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-240">hello status of hello operation, For example, 200.</span></span> |
| <span data-ttu-id="ce8cc-241">correlationId</span><span class="sxs-lookup"><span data-stu-id="ce8cc-241">correlationId</span></span> |<span data-ttu-id="ce8cc-242">Dize</span><span class="sxs-lookup"><span data-stu-id="ce8cc-242">String</span></span> |<span data-ttu-id="ce8cc-243">toogroup bir dizi ilgili günlük girişlerini birlikte kullanılabilecek hello günlük Hello kimliği</span><span class="sxs-lookup"><span data-stu-id="ce8cc-243">hello id of hello log that can used toogroup together a set of related log entries</span></span> |
| <span data-ttu-id="ce8cc-244">identity</span><span class="sxs-lookup"><span data-stu-id="ce8cc-244">identity</span></span> |<span data-ttu-id="ce8cc-245">Nesne</span><span class="sxs-lookup"><span data-stu-id="ce8cc-245">Object</span></span> |<span data-ttu-id="ce8cc-246">Merhaba günlük oluşturulan hello kimliği</span><span class="sxs-lookup"><span data-stu-id="ce8cc-246">hello identity that generated hello log</span></span> |
| <span data-ttu-id="ce8cc-247">properties</span><span class="sxs-lookup"><span data-stu-id="ce8cc-247">properties</span></span> |<span data-ttu-id="ce8cc-248">JSON</span><span class="sxs-lookup"><span data-stu-id="ce8cc-248">JSON</span></span> |<span data-ttu-id="ce8cc-249">Ayrıntılar için aşağıya bakın</span><span class="sxs-lookup"><span data-stu-id="ce8cc-249">See below for details</span></span> |

#### <a name="audit-log-properties-schema"></a><span data-ttu-id="ce8cc-250">Denetim günlüğü özellikleri şeması</span><span class="sxs-lookup"><span data-stu-id="ce8cc-250">Audit log properties schema</span></span>
| <span data-ttu-id="ce8cc-251">Ad</span><span class="sxs-lookup"><span data-stu-id="ce8cc-251">Name</span></span> | <span data-ttu-id="ce8cc-252">Tür</span><span class="sxs-lookup"><span data-stu-id="ce8cc-252">Type</span></span> | <span data-ttu-id="ce8cc-253">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ce8cc-253">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ce8cc-254">StreamName</span><span class="sxs-lookup"><span data-stu-id="ce8cc-254">StreamName</span></span> |<span data-ttu-id="ce8cc-255">Dize</span><span class="sxs-lookup"><span data-stu-id="ce8cc-255">String</span></span> |<span data-ttu-id="ce8cc-256">Merhaba yolu hello işlem üzerinde gerçekleştirildi</span><span class="sxs-lookup"><span data-stu-id="ce8cc-256">hello path hello operation was performed on</span></span> |

## <a name="samples-tooprocess-hello-log-data"></a><span data-ttu-id="ce8cc-257">Örnekleri tooprocess hello günlük verileri</span><span class="sxs-lookup"><span data-stu-id="ce8cc-257">Samples tooprocess hello log data</span></span>
<span data-ttu-id="ce8cc-258">Azure Data Lake Store hakkında bir örnek sağlar tooprocess ve hello günlük verilerini çözümleyin.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-258">Azure Data Lake Store provides a sample on how tooprocess and analyze hello log data.</span></span> <span data-ttu-id="ce8cc-259">Merhaba örneğini şurada bulabilirsiniz [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span><span class="sxs-lookup"><span data-stu-id="ce8cc-259">You can find hello sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span></span> 

## <a name="see-also"></a><span data-ttu-id="ce8cc-260">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="ce8cc-260">See also</span></span>
* [<span data-ttu-id="ce8cc-261">Azure Data Lake Store'a Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="ce8cc-261">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
* [<span data-ttu-id="ce8cc-262">Data Lake Store'da verilerin güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="ce8cc-262">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)

