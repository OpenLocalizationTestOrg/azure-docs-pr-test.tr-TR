---
title: "Azure Data Lake Store için tanılama günlükleri görüntüleme | Microsoft Docs"
description: "Kurulum ve Azure Data Lake Store için tanılama günlüklerine erişmek öğrenme "
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
ms.openlocfilehash: b7a38ec445ef0ce13f3f1931e8ee246dce6412a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-store"></a><span data-ttu-id="88102-103">Azure Data Lake Store için tanılama günlüklerine erişme</span><span class="sxs-lookup"><span data-stu-id="88102-103">Accessing diagnostic logs for Azure Data Lake Store</span></span>
<span data-ttu-id="88102-104">Data Lake Store hesabınız için tanılama günlüğünü etkinleştirin ve hesabınız için toplanan günlükleri görüntüleme hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="88102-104">Learn about how to enable diagnostic logging for your Data Lake Store account and how to view the logs collected for your account.</span></span>

<span data-ttu-id="88102-105">Kuruluşlar, verileri ne sıklıkta erişildiğine, verilerine erişen kullanıcılara listesi gibi bilgiler sağlayan veri erişimi denetim izleri toplamak Azure Data Lake Store hesapları için tanılama günlük kaydını etkinleştirebilir ne kadar verinin depolanma biçimini hesap, vs.</span><span class="sxs-lookup"><span data-stu-id="88102-105">Organizations can enable diagnostic logging for their Azure Data Lake Store account to collect data access audit trails that provides information such as list of users accessing the data, how frequently the data is accessed, how much data is stored in the account, etc.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88102-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="88102-106">Prerequisites</span></span>
* <span data-ttu-id="88102-107">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="88102-107">**An Azure subscription**.</span></span> <span data-ttu-id="88102-108">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="88102-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="88102-109">**Azure Data Lake Store hesabı**.</span><span class="sxs-lookup"><span data-stu-id="88102-109">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="88102-110">[Azure Portal'ı kullanarak Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md) bölümündeki yönergeleri uygulayın.</span><span class="sxs-lookup"><span data-stu-id="88102-110">Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).</span></span>

## <a name="enable-diagnostic-logging-for-your-data-lake-store-account"></a><span data-ttu-id="88102-111">Data Lake Store hesabınız için tanılama günlük kaydını etkinleştir</span><span class="sxs-lookup"><span data-stu-id="88102-111">Enable diagnostic logging for your Data Lake Store account</span></span>
1. <span data-ttu-id="88102-112">Yeni [Azure Portal](https://portal.azure.com)'da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="88102-112">Sign on to the new [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="88102-113">Data Lake Store hesabınızı açın ve Data Lake Store hesabı dikey penceresinden tıklayın **ayarları**ve ardından **tanılama günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="88102-113">Open your Data Lake Store account, and from your Data Lake Store account blade, click **Settings**, and then click **Diagnostic logs**.</span></span>
3. <span data-ttu-id="88102-114">İçinde **tanılama günlükleri** dikey penceresinde tıklatın **tanılamayı açın**.</span><span class="sxs-lookup"><span data-stu-id="88102-114">In the **Diagnostics logs** blade, click **Turn on diagnostics**.</span></span>

    <span data-ttu-id="88102-115">![Tanılama günlük kaydını etkinleştir](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "tanılama günlüklerini etkinleştirme")</span><span class="sxs-lookup"><span data-stu-id="88102-115">![Enable diagnostic logging](./media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "Enable diagnostic logs")</span></span>

3. <span data-ttu-id="88102-116">İçinde **tanılama** dikey penceresinde tanılama günlük kaydını yapılandırmak için aşağıdaki değişiklikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="88102-116">In the **Diagnostic** blade, make the following changes to configure diagnostic logging.</span></span>
   
    <span data-ttu-id="88102-117">![Tanılama günlük kaydını etkinleştir](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "tanılama günlüklerini etkinleştirme")</span><span class="sxs-lookup"><span data-stu-id="88102-117">![Enable diagnostic logging](./media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")</span></span>
   
   * <span data-ttu-id="88102-118">Ayarlama **durum** için **üzerinde** tanılama günlük kaydını etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="88102-118">Set **Status** to **On** to enable diagnostic logging.</span></span>
   * <span data-ttu-id="88102-119">Depolama/verileri farklı şekillerde işlemi seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88102-119">You can choose to store/process the data in different ways.</span></span>
     
        * <span data-ttu-id="88102-120">Seçeneğini **bir depolama hesabı arşive** bir Azure depolama hesabı günlükleri depolamak için.</span><span class="sxs-lookup"><span data-stu-id="88102-120">Select the option to **Archive to a storage account** to store logs to an Azure Storage account.</span></span> <span data-ttu-id="88102-121">Daha sonraki bir tarihte toplu işlenen verileri arşivlemek istiyorsanız bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="88102-121">You use this option if you want to archive the data that will be batch-processed at a later date.</span></span> <span data-ttu-id="88102-122">Bu seçeneği belirlerseniz günlüklerine kaydetmek için bir Azure depolama hesabı sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="88102-122">If you select this option you must provide an Azure Storage account to save the logs to.</span></span>
        
        * <span data-ttu-id="88102-123">Seçeneğini **bir olay hub'ına akış** Azure olay Hub'ına günlük veri akışı için.</span><span class="sxs-lookup"><span data-stu-id="88102-123">Select the option to **Stream to an event hub** to stream log data to an Azure Event Hub.</span></span> <span data-ttu-id="88102-124">Büyük olasılıkla gerçek zamanda gelen günlüklerini çözümlemek için bir aşağı akış işleme ardışık varsa bu seçeneği kullanır.</span><span class="sxs-lookup"><span data-stu-id="88102-124">Most likely you will use this option if you have a downstream processing pipeline to analyze incoming logs at real time.</span></span> <span data-ttu-id="88102-125">Bu seçeneği belirlerseniz, kullanmak istediğiniz Azure olay Hub ayrıntılarını sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="88102-125">If you select this option, you must provide the details for the Azure Event Hub you want to use.</span></span>

        * <span data-ttu-id="88102-126">Seçeneğini **için günlük analizi Gönder** oluşturulan günlük verileri çözümlemek için Azure günlük analizi hizmeti kullanmak için.</span><span class="sxs-lookup"><span data-stu-id="88102-126">Select the option to **Send to Log Analytics** to use the Azure Log Analytics service to analyze the generated log data.</span></span> <span data-ttu-id="88102-127">Bu seçeneği belirlerseniz, gerçekleştirme Günlük çözümlemesi kullanacağınız için Operations Management Suite çalışma ayrıntıları sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="88102-127">If you select this option, you must provide the details for the Operations Management Suite workspace that you would use the perform log analysis.</span></span>
     
   * <span data-ttu-id="88102-128">Denetim günlükleri veya istek günlüklerini veya her ikisini de almak isteyip istemediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="88102-128">Specify whether you want to get audit logs or request logs or both.</span></span>
   * <span data-ttu-id="88102-129">Verilerin korunması gereken gün sayısını belirtin.</span><span class="sxs-lookup"><span data-stu-id="88102-129">Specify the number of days for which the data must be retained.</span></span> <span data-ttu-id="88102-130">Bekletme, yalnızca günlük verileri arşivlemek için Azure depolama hesabı kullanıyorsanız geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="88102-130">Retention is only applicable if you are using Azure storage account to archive log data.</span></span>
   * <span data-ttu-id="88102-131">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="88102-131">Click **Save**.</span></span>

<span data-ttu-id="88102-132">Tanılama ayarları etkinleştirildiğinde, günlüklerde izleyebilirsiniz **tanılama günlüklerini** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="88102-132">Once you have enabled diagnostic settings, you can watch the logs in the **Diagnostic Logs** tab.</span></span>

## <a name="view-diagnostic-logs-for-your-data-lake-store-account"></a><span data-ttu-id="88102-133">Data Lake Store hesabınız için tanılama günlüklerini görüntüle</span><span class="sxs-lookup"><span data-stu-id="88102-133">View diagnostic logs for your Data Lake Store account</span></span>
<span data-ttu-id="88102-134">Data Lake Store hesabınız için günlük verileri görüntülemek için iki yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="88102-134">There are two ways to view the log data for your Data Lake Store account.</span></span>

* <span data-ttu-id="88102-135">Data Lake Store hesabından ayarlarını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="88102-135">From the Data Lake Store account settings view</span></span>
* <span data-ttu-id="88102-136">Verilerin depolandığı Azure depolama hesabından</span><span class="sxs-lookup"><span data-stu-id="88102-136">From the Azure Storage account where the data is stored</span></span>

### <a name="using-the-data-lake-store-settings-view"></a><span data-ttu-id="88102-137">Veri Gölü deposu ayarları görünümünü kullanma</span><span class="sxs-lookup"><span data-stu-id="88102-137">Using the Data Lake Store Settings view</span></span>
1. <span data-ttu-id="88102-138">Data Lake Store hesabınızdaki **ayarları** dikey penceresinde tıklatın **tanılama günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="88102-138">From your Data Lake Store account **Settings** blade, click **Diagnostic Logs**.</span></span>
   
    <span data-ttu-id="88102-139">![Görünüm tanılama günlük](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "tanılama günlükleri görüntüleme")</span><span class="sxs-lookup"><span data-stu-id="88102-139">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")</span></span> 
2. <span data-ttu-id="88102-140">İçinde **tanılama günlüklerini** dikey penceresinde tarafından kategorilere günlükleri görmelisiniz **denetim günlüklerini** ve **isteği günlükleri**.</span><span class="sxs-lookup"><span data-stu-id="88102-140">In the **Diagnostic Logs** blade, you should see the logs categorized by **Audit Logs** and **Request Logs**.</span></span>
   
   * <span data-ttu-id="88102-141">İstek günlüklerini Data Lake Store hesabında yapılan her API isteği yakalayın.</span><span class="sxs-lookup"><span data-stu-id="88102-141">Request logs capture every API request made on the Data Lake Store account.</span></span>
   * <span data-ttu-id="88102-142">Denetim günlüklerini günlükleri isteği ancak Data Lake Store hesabı üzerinde gerçekleştirilen işlemler çok daha ayrıntılı bir dökümünü sağlamak için benzerdir.</span><span class="sxs-lookup"><span data-stu-id="88102-142">Audit Logs are similar to request Logs but provide a much more detailed breakdown of the operations being performed on the Data Lake Store account.</span></span> <span data-ttu-id="88102-143">Örneğin, bir istek günlüklerini tek karşıya yükleme API çağrısında denetim günlüklerini "Ekle" işlemlerinde neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="88102-143">For example, a single upload API call in request logs might result in multiple "Append" operations in the audit logs.</span></span>
3. <span data-ttu-id="88102-144">Tıklatın **karşıdan** günlükleri indirmek için her günlük girişinin karşı bağlantı.</span><span class="sxs-lookup"><span data-stu-id="88102-144">Click the **Download** link against each log entry to download the logs.</span></span>

### <a name="from-the-azure-storage-account-that-contains-log-data"></a><span data-ttu-id="88102-145">Azure depolama hesabından günlük verilerini içeren</span><span class="sxs-lookup"><span data-stu-id="88102-145">From the Azure Storage account that contains log data</span></span>
1. <span data-ttu-id="88102-146">Günlüğe kaydetme için Data Lake Store ile ilişkili Azure depolama hesabı dikey penceresini açın ve Bloblar'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="88102-146">Open the Azure Storage account blade associated with Data Lake Store for logging, and then click Blobs.</span></span> <span data-ttu-id="88102-147">**Blob hizmeti** iki kapsayıcı dikey penceresinde listelenir.</span><span class="sxs-lookup"><span data-stu-id="88102-147">The **Blob service** blade lists two containers.</span></span>
   
    <span data-ttu-id="88102-148">![Görünüm tanılama günlük](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "tanılama günlükleri görüntüleme")</span><span class="sxs-lookup"><span data-stu-id="88102-148">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")</span></span>
   
   * <span data-ttu-id="88102-149">Kapsayıcı **Öngörüler günlükleri denetim** denetim günlüklerini içerir.</span><span class="sxs-lookup"><span data-stu-id="88102-149">The container **insights-logs-audit** contains the audit logs.</span></span>
   * <span data-ttu-id="88102-150">Kapsayıcı **Öngörüler günlükleri istekleri** isteği günlükleri içerir.</span><span class="sxs-lookup"><span data-stu-id="88102-150">The container **insights-logs-requests** contains the request logs.</span></span>
2. <span data-ttu-id="88102-151">Bu kapsayıcılara günlükleri aşağıdaki yapısı altında depolanır.</span><span class="sxs-lookup"><span data-stu-id="88102-151">Within these containers, the logs are stored under the following structure.</span></span>
   
    <span data-ttu-id="88102-152">![Görünüm tanılama günlük](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "tanılama günlükleri görüntüleme")</span><span class="sxs-lookup"><span data-stu-id="88102-152">![View diagnostic logging](./media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "View diagnostic logs")</span></span>
   
    <span data-ttu-id="88102-153">Örnek olarak, Denetim günlüğü tam yolunu olabilir`https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`</span><span class="sxs-lookup"><span data-stu-id="88102-153">As an example, the complete path to an audit log could be `https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`</span></span>
   
    <span data-ttu-id="88102-154">İstek günlüğü tam yolunu similary, olabilir`https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`</span><span class="sxs-lookup"><span data-stu-id="88102-154">Similary, the complete path to a request log could be `https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`</span></span>

## <a name="understand-the-structure-of-the-log-data"></a><span data-ttu-id="88102-155">Günlük verilerinin yapısını anlama</span><span class="sxs-lookup"><span data-stu-id="88102-155">Understand the structure of the log data</span></span>
<span data-ttu-id="88102-156">Denetim ve istek günlüklerini bir JSON biçimindedir.</span><span class="sxs-lookup"><span data-stu-id="88102-156">The audit and request logs are in a JSON format.</span></span> <span data-ttu-id="88102-157">Bu bölümde, JSON yapısı istek için bakın ve Denetim günlükleri.</span><span class="sxs-lookup"><span data-stu-id="88102-157">In this section, we look at the structure of JSON for request and audit logs.</span></span>

### <a name="request-logs"></a><span data-ttu-id="88102-158">İstek günlükleri</span><span class="sxs-lookup"><span data-stu-id="88102-158">Request logs</span></span>
<span data-ttu-id="88102-159">Burada JSON biçimli istek günlüğüne örnek girişi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="88102-159">Here's a sample entry in the JSON-formatted request log.</span></span> <span data-ttu-id="88102-160">Her bir blob olarak adlandırılan bir kök nesnesi vardır **kayıtları** günlük nesnelerinin bir dizisi içerir.</span><span class="sxs-lookup"><span data-stu-id="88102-160">Each blob has one root object called **records** that contains an array of log objects.</span></span>

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

#### <a name="request-log-schema"></a><span data-ttu-id="88102-161">İstek günlüğü şeması</span><span class="sxs-lookup"><span data-stu-id="88102-161">Request log schema</span></span>
| <span data-ttu-id="88102-162">Ad</span><span class="sxs-lookup"><span data-stu-id="88102-162">Name</span></span> | <span data-ttu-id="88102-163">Tür</span><span class="sxs-lookup"><span data-stu-id="88102-163">Type</span></span> | <span data-ttu-id="88102-164">Açıklama</span><span class="sxs-lookup"><span data-stu-id="88102-164">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88102-165">time</span><span class="sxs-lookup"><span data-stu-id="88102-165">time</span></span> |<span data-ttu-id="88102-166">Dize</span><span class="sxs-lookup"><span data-stu-id="88102-166">String</span></span> |<span data-ttu-id="88102-167">Timestamp (UTC) günlük</span><span class="sxs-lookup"><span data-stu-id="88102-167">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="88102-168">resourceId</span><span class="sxs-lookup"><span data-stu-id="88102-168">resourceId</span></span> |<span data-ttu-id="88102-169">Dize</span><span class="sxs-lookup"><span data-stu-id="88102-169">String</span></span> |<span data-ttu-id="88102-170">İşlemi sürdü kaynak Kimliğini yerleştirin</span><span class="sxs-lookup"><span data-stu-id="88102-170">The ID of the resource that operation took place on</span></span> |
| <span data-ttu-id="88102-171">category</span><span class="sxs-lookup"><span data-stu-id="88102-171">category</span></span> |<span data-ttu-id="88102-172">Dize</span><span class="sxs-lookup"><span data-stu-id="88102-172">String</span></span> |<span data-ttu-id="88102-173">Günlük kategorisi.</span><span class="sxs-lookup"><span data-stu-id="88102-173">The log category.</span></span> <span data-ttu-id="88102-174">Örneğin, **istekleri**.</span><span class="sxs-lookup"><span data-stu-id="88102-174">For example, **Requests**.</span></span> |
| <span data-ttu-id="88102-175">operationName</span><span class="sxs-lookup"><span data-stu-id="88102-175">operationName</span></span> |<span data-ttu-id="88102-176">Dize</span><span class="sxs-lookup"><span data-stu-id="88102-176">String</span></span> |<span data-ttu-id="88102-177">Oturum açmış işlemin adı.</span><span class="sxs-lookup"><span data-stu-id="88102-177">Name of the operation that is logged.</span></span> <span data-ttu-id="88102-178">Örneğin, getfilestatus.</span><span class="sxs-lookup"><span data-stu-id="88102-178">For example, getfilestatus.</span></span> |
| <span data-ttu-id="88102-179">resultType</span><span class="sxs-lookup"><span data-stu-id="88102-179">resultType</span></span> |<span data-ttu-id="88102-180">Dize</span><span class="sxs-lookup"><span data-stu-id="88102-180">String</span></span> |<span data-ttu-id="88102-181">Örneğin, 200 işlem durumu.</span><span class="sxs-lookup"><span data-stu-id="88102-181">The status of the operation, For example, 200.</span></span> |
| <span data-ttu-id="88102-182">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="88102-182">callerIpAddress</span></span> |<span data-ttu-id="88102-183">Dize</span><span class="sxs-lookup"><span data-stu-id="88102-183">String</span></span> |<span data-ttu-id="88102-184">İsteği yapan istemcinin IP adresi</span><span class="sxs-lookup"><span data-stu-id="88102-184">The IP address of the client making the request</span></span> |
| <span data-ttu-id="88102-185">correlationId</span><span class="sxs-lookup"><span data-stu-id="88102-185">correlationId</span></span> |<span data-ttu-id="88102-186">Dize</span><span class="sxs-lookup"><span data-stu-id="88102-186">String</span></span> |<span data-ttu-id="88102-187">Bir dizi ilgili günlük girişlerini gruplamak için kullanılan kimliği için günlük</span><span class="sxs-lookup"><span data-stu-id="88102-187">The id of the log that can used to group together a set of related log entries</span></span> |
| <span data-ttu-id="88102-188">identity</span><span class="sxs-lookup"><span data-stu-id="88102-188">identity</span></span> |<span data-ttu-id="88102-189">Nesne</span><span class="sxs-lookup"><span data-stu-id="88102-189">Object</span></span> |<span data-ttu-id="88102-190">Günlük oluşturulan kimliği</span><span class="sxs-lookup"><span data-stu-id="88102-190">The identity that generated the log</span></span> |
| <span data-ttu-id="88102-191">properties</span><span class="sxs-lookup"><span data-stu-id="88102-191">properties</span></span> |<span data-ttu-id="88102-192">JSON</span><span class="sxs-lookup"><span data-stu-id="88102-192">JSON</span></span> |<span data-ttu-id="88102-193">Ayrıntılar için aşağıya bakın</span><span class="sxs-lookup"><span data-stu-id="88102-193">See below for details</span></span> |

#### <a name="request-log-properties-schema"></a><span data-ttu-id="88102-194">İstek günlüğü özellikleri şeması</span><span class="sxs-lookup"><span data-stu-id="88102-194">Request log properties schema</span></span>
| <span data-ttu-id="88102-195">Ad</span><span class="sxs-lookup"><span data-stu-id="88102-195">Name</span></span> | <span data-ttu-id="88102-196">Tür</span><span class="sxs-lookup"><span data-stu-id="88102-196">Type</span></span> | <span data-ttu-id="88102-197">Açıklama</span><span class="sxs-lookup"><span data-stu-id="88102-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88102-198">HttpMethod</span><span class="sxs-lookup"><span data-stu-id="88102-198">HttpMethod</span></span> |<span data-ttu-id="88102-199">Dize</span><span class="sxs-lookup"><span data-stu-id="88102-199">String</span></span> |<span data-ttu-id="88102-200">İşlem için kullanılan HTTP yöntem.</span><span class="sxs-lookup"><span data-stu-id="88102-200">The HTTP Method used for the operation.</span></span> <span data-ttu-id="88102-201">Örneğin, alın.</span><span class="sxs-lookup"><span data-stu-id="88102-201">For example, GET.</span></span> |
| <span data-ttu-id="88102-202">Yol</span><span class="sxs-lookup"><span data-stu-id="88102-202">Path</span></span> |<span data-ttu-id="88102-203">Dize</span><span class="sxs-lookup"><span data-stu-id="88102-203">String</span></span> |<span data-ttu-id="88102-204">Yolun işlemi üzerinde gerçekleştirildi</span><span class="sxs-lookup"><span data-stu-id="88102-204">The path the operation was performed on</span></span> |
| <span data-ttu-id="88102-205">RequestContentLength</span><span class="sxs-lookup"><span data-stu-id="88102-205">RequestContentLength</span></span> |<span data-ttu-id="88102-206">Int</span><span class="sxs-lookup"><span data-stu-id="88102-206">int</span></span> |<span data-ttu-id="88102-207">HTTP isteğinin içerik uzunluğu</span><span class="sxs-lookup"><span data-stu-id="88102-207">The content length of the HTTP request</span></span> |
| <span data-ttu-id="88102-208">ClientRequestId</span><span class="sxs-lookup"><span data-stu-id="88102-208">ClientRequestId</span></span> |<span data-ttu-id="88102-209">Dize</span><span class="sxs-lookup"><span data-stu-id="88102-209">String</span></span> |<span data-ttu-id="88102-210">Bu istek benzersiz olarak tanıtan kimliği</span><span class="sxs-lookup"><span data-stu-id="88102-210">The Id that uniquely identifies this request</span></span> |
| <span data-ttu-id="88102-211">StartTime</span><span class="sxs-lookup"><span data-stu-id="88102-211">StartTime</span></span> |<span data-ttu-id="88102-212">Dize</span><span class="sxs-lookup"><span data-stu-id="88102-212">String</span></span> |<span data-ttu-id="88102-213">Sunucu isteği aldığınız zaman</span><span class="sxs-lookup"><span data-stu-id="88102-213">The time at which the server received the request</span></span> |
| <span data-ttu-id="88102-214">EndTime</span><span class="sxs-lookup"><span data-stu-id="88102-214">EndTime</span></span> |<span data-ttu-id="88102-215">Dize</span><span class="sxs-lookup"><span data-stu-id="88102-215">String</span></span> |<span data-ttu-id="88102-216">Sunucu yanıt gönderilme saati</span><span class="sxs-lookup"><span data-stu-id="88102-216">The time at which the server sent a response</span></span> |

### <a name="audit-logs"></a><span data-ttu-id="88102-217">Denetim günlükleri</span><span class="sxs-lookup"><span data-stu-id="88102-217">Audit logs</span></span>
<span data-ttu-id="88102-218">Burada JSON biçimli Denetim günlüğüne örnek girişi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="88102-218">Here's a sample entry in the JSON-formatted audit log.</span></span> <span data-ttu-id="88102-219">Her bir blob olarak adlandırılan bir kök nesnesi vardır **kayıtları** günlük nesnelerinin bir dizisi içerir</span><span class="sxs-lookup"><span data-stu-id="88102-219">Each blob has one root object called **records** that contains an array of log objects</span></span>

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

#### <a name="audit-log-schema"></a><span data-ttu-id="88102-220">Denetim günlüğü şeması</span><span class="sxs-lookup"><span data-stu-id="88102-220">Audit log schema</span></span>
| <span data-ttu-id="88102-221">Ad</span><span class="sxs-lookup"><span data-stu-id="88102-221">Name</span></span> | <span data-ttu-id="88102-222">Tür</span><span class="sxs-lookup"><span data-stu-id="88102-222">Type</span></span> | <span data-ttu-id="88102-223">Açıklama</span><span class="sxs-lookup"><span data-stu-id="88102-223">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88102-224">time</span><span class="sxs-lookup"><span data-stu-id="88102-224">time</span></span> |<span data-ttu-id="88102-225">Dize</span><span class="sxs-lookup"><span data-stu-id="88102-225">String</span></span> |<span data-ttu-id="88102-226">Timestamp (UTC) günlük</span><span class="sxs-lookup"><span data-stu-id="88102-226">The timestamp (in UTC) of the log</span></span> |
| <span data-ttu-id="88102-227">resourceId</span><span class="sxs-lookup"><span data-stu-id="88102-227">resourceId</span></span> |<span data-ttu-id="88102-228">Dize</span><span class="sxs-lookup"><span data-stu-id="88102-228">String</span></span> |<span data-ttu-id="88102-229">İşlemi sürdü kaynak Kimliğini yerleştirin</span><span class="sxs-lookup"><span data-stu-id="88102-229">The ID of the resource that operation took place on</span></span> |
| <span data-ttu-id="88102-230">category</span><span class="sxs-lookup"><span data-stu-id="88102-230">category</span></span> |<span data-ttu-id="88102-231">Dize</span><span class="sxs-lookup"><span data-stu-id="88102-231">String</span></span> |<span data-ttu-id="88102-232">Günlük kategorisi.</span><span class="sxs-lookup"><span data-stu-id="88102-232">The log category.</span></span> <span data-ttu-id="88102-233">Örneğin, **denetim**.</span><span class="sxs-lookup"><span data-stu-id="88102-233">For example, **Audit**.</span></span> |
| <span data-ttu-id="88102-234">operationName</span><span class="sxs-lookup"><span data-stu-id="88102-234">operationName</span></span> |<span data-ttu-id="88102-235">Dize</span><span class="sxs-lookup"><span data-stu-id="88102-235">String</span></span> |<span data-ttu-id="88102-236">Oturum açmış işlemin adı.</span><span class="sxs-lookup"><span data-stu-id="88102-236">Name of the operation that is logged.</span></span> <span data-ttu-id="88102-237">Örneğin, getfilestatus.</span><span class="sxs-lookup"><span data-stu-id="88102-237">For example, getfilestatus.</span></span> |
| <span data-ttu-id="88102-238">resultType</span><span class="sxs-lookup"><span data-stu-id="88102-238">resultType</span></span> |<span data-ttu-id="88102-239">Dize</span><span class="sxs-lookup"><span data-stu-id="88102-239">String</span></span> |<span data-ttu-id="88102-240">Örneğin, 200 işlem durumu.</span><span class="sxs-lookup"><span data-stu-id="88102-240">The status of the operation, For example, 200.</span></span> |
| <span data-ttu-id="88102-241">correlationId</span><span class="sxs-lookup"><span data-stu-id="88102-241">correlationId</span></span> |<span data-ttu-id="88102-242">Dize</span><span class="sxs-lookup"><span data-stu-id="88102-242">String</span></span> |<span data-ttu-id="88102-243">Bir dizi ilgili günlük girişlerini gruplamak için kullanılan kimliği için günlük</span><span class="sxs-lookup"><span data-stu-id="88102-243">The id of the log that can used to group together a set of related log entries</span></span> |
| <span data-ttu-id="88102-244">identity</span><span class="sxs-lookup"><span data-stu-id="88102-244">identity</span></span> |<span data-ttu-id="88102-245">Nesne</span><span class="sxs-lookup"><span data-stu-id="88102-245">Object</span></span> |<span data-ttu-id="88102-246">Günlük oluşturulan kimliği</span><span class="sxs-lookup"><span data-stu-id="88102-246">The identity that generated the log</span></span> |
| <span data-ttu-id="88102-247">properties</span><span class="sxs-lookup"><span data-stu-id="88102-247">properties</span></span> |<span data-ttu-id="88102-248">JSON</span><span class="sxs-lookup"><span data-stu-id="88102-248">JSON</span></span> |<span data-ttu-id="88102-249">Ayrıntılar için aşağıya bakın</span><span class="sxs-lookup"><span data-stu-id="88102-249">See below for details</span></span> |

#### <a name="audit-log-properties-schema"></a><span data-ttu-id="88102-250">Denetim günlüğü özellikleri şeması</span><span class="sxs-lookup"><span data-stu-id="88102-250">Audit log properties schema</span></span>
| <span data-ttu-id="88102-251">Ad</span><span class="sxs-lookup"><span data-stu-id="88102-251">Name</span></span> | <span data-ttu-id="88102-252">Tür</span><span class="sxs-lookup"><span data-stu-id="88102-252">Type</span></span> | <span data-ttu-id="88102-253">Açıklama</span><span class="sxs-lookup"><span data-stu-id="88102-253">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88102-254">StreamName</span><span class="sxs-lookup"><span data-stu-id="88102-254">StreamName</span></span> |<span data-ttu-id="88102-255">Dize</span><span class="sxs-lookup"><span data-stu-id="88102-255">String</span></span> |<span data-ttu-id="88102-256">Yolun işlemi üzerinde gerçekleştirildi</span><span class="sxs-lookup"><span data-stu-id="88102-256">The path the operation was performed on</span></span> |

## <a name="samples-to-process-the-log-data"></a><span data-ttu-id="88102-257">Günlük verileri işlemek için örnekleri</span><span class="sxs-lookup"><span data-stu-id="88102-257">Samples to process the log data</span></span>
<span data-ttu-id="88102-258">Azure Data Lake Store işlemek ve günlük verilerini analiz konusunda bir örnek sağlar.</span><span class="sxs-lookup"><span data-stu-id="88102-258">Azure Data Lake Store provides a sample on how to process and analyze the log data.</span></span> <span data-ttu-id="88102-259">Örnek: bulabilirsiniz [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span><span class="sxs-lookup"><span data-stu-id="88102-259">You can find the sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).</span></span> 

## <a name="see-also"></a><span data-ttu-id="88102-260">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="88102-260">See also</span></span>
* [<span data-ttu-id="88102-261">Azure Data Lake Store'a Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="88102-261">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
* [<span data-ttu-id="88102-262">Data Lake Store'da verilerin güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="88102-262">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)

