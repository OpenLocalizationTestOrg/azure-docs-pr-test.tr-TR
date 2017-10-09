---
title: "aaaCall REST uç HTTP + Swagger ile Azure Logic Apps bağlayıcı | Microsoft Docs"
description: "Swagger aracılığıyla logic apps Merhaba HTTP + Swagger bağlayıcı ile tooREST uç noktaları bağlayın"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: eccfd87c-c5fe-4cf7-b564-9752775fd667
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: baaa57689ff41fcd052f9d86086e36619ddec46e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http--swagger-action"></a><span data-ttu-id="8aa11-103">Merhaba HTTP + Swagger eylem ile başlayın</span><span class="sxs-lookup"><span data-stu-id="8aa11-103">Get started with hello HTTP + Swagger action</span></span>

<span data-ttu-id="8aa11-104">İlk sınıf bağlayıcı tooany REST uç noktası aracılığıyla oluşturabileceğiniz bir [Swagger belgesinin](https://swagger.io) kullandığınızda Merhaba HTTP + Swagger eylem mantığı uygulama akışınızda.</span><span class="sxs-lookup"><span data-stu-id="8aa11-104">You can create a first-class connector tooany REST endpoint through a [Swagger document](https://swagger.io) when you use hello HTTP + Swagger action in your logic app workflow.</span></span> <span data-ttu-id="8aa11-105">Logic apps toocall birinci sınıf bir mantıksal Uygulama Tasarımcısı deneyim herhangi bir REST uç nokta da genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8aa11-105">You can also extend logic apps toocall any REST endpoint with a first-class Logic App Designer experience.</span></span>

<span data-ttu-id="8aa11-106">toocreate logic apps, bağlayıcılar ile nasıl görürüm toolearn [yeni bir mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="8aa11-106">toolearn how toocreate logic apps with connectors, see [Create a new logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a><span data-ttu-id="8aa11-107">HTTP kullan + tetikleyicinin veya bir eylem olarak Swagger</span><span class="sxs-lookup"><span data-stu-id="8aa11-107">Use HTTP + Swagger as a trigger or an action</span></span>

<span data-ttu-id="8aa11-108">Merhaba HTTP + Swagger tetikleyici ve eylem iş hello aynı hello [HTTP eylemi](connectors-native-http.md) ancak hello API yapısı ve hello çıkışlarından göstererek mantığı Uygulama Tasarımcısı'nda daha iyi bir deneyim sağlamak [Swagger meta verileri](https://swagger.io) .</span><span class="sxs-lookup"><span data-stu-id="8aa11-108">hello HTTP + Swagger trigger and action work hello same as hello [HTTP action](connectors-native-http.md) but provide a better experience in Logic App Designer by exposing hello API structure and outputs from hello [Swagger metadata](https://swagger.io).</span></span> <span data-ttu-id="8aa11-109">Tetikleyici olarak da hello HTTP + Swagger Bağlayıcısı'nı da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8aa11-109">You can also use hello HTTP + Swagger connector as a trigger.</span></span> <span data-ttu-id="8aa11-110">Tooimplement yoklama tetikleyicinin isterseniz, açıklanan hello yoklama desenler izleyen [özel API'leri toocall mantığı uygulamalardan diğer API'leri, hizmetleri ve sistemleri oluşturmak](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span><span class="sxs-lookup"><span data-stu-id="8aa11-110">If you want tooimplement a polling trigger, follow hello polling pattern that's described in [Create custom APIs toocall other APIs, services, and systems from logic apps](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span></span>

<span data-ttu-id="8aa11-111">Daha fazla bilgi edinmek [mantığı uygulama tetikleyiciler ve Eylemler](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8aa11-111">Learn more about [logic app triggers and actions](connectors-overview.md).</span></span>

<span data-ttu-id="8aa11-112">Toouse nasıl hello HTTP + Swagger örneği İşte işlem olarak bir mantıksal uygulama bir iş akışında bir eylemi.</span><span class="sxs-lookup"><span data-stu-id="8aa11-112">Here's an example of how toouse hello HTTP + Swagger operation as an action in a workflow in a logic app.</span></span>

1. <span data-ttu-id="8aa11-113">Select hello **yeni adım** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="8aa11-113">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="8aa11-114">Seçin **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="8aa11-114">Select **Add an action**.</span></span>
3. <span data-ttu-id="8aa11-115">Merhaba eylem arama kutusuna yazın **swagger** toolist Merhaba HTTP + Swagger eylem.</span><span class="sxs-lookup"><span data-stu-id="8aa11-115">In hello action search box, type **swagger** toolist hello HTTP + Swagger action.</span></span>
   
    ![HTTP + Swagger seçin eylemi](./media/connectors-native-http-swagger/using-action-1.png)
4. <span data-ttu-id="8aa11-117">Merhaba Swagger belgesinin URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="8aa11-117">Type hello URL for a Swagger document:</span></span>
   
   * <span data-ttu-id="8aa11-118">CORS etkinleştirdiyseniz ve toowork hello mantığı Uygulama Tasarımcısı hello URL gelen bir HTTPS uç noktası olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8aa11-118">toowork from hello Logic App Designer, hello URL must be an HTTPS endpoint and have CORS enabled.</span></span>
   * <span data-ttu-id="8aa11-119">Merhaba Swagger belgesinin bu gereksinimi karşılamıyorsa, kullanabileceğiniz [Azure Storage ile CORS'yi](#hosting-swagger-from-storage) toostore hello belge.</span><span class="sxs-lookup"><span data-stu-id="8aa11-119">If hello Swagger document doesn't meet this requirement, you can use [Azure Storage with CORS enabled](#hosting-swagger-from-storage) toostore hello document.</span></span>
5. <span data-ttu-id="8aa11-120">Tıklatın **sonraki** tooread ve işleme gelen hello Swagger belgesinin.</span><span class="sxs-lookup"><span data-stu-id="8aa11-120">Click **Next** tooread and render from hello Swagger document.</span></span>
6. <span data-ttu-id="8aa11-121">Merhaba HTTP çağrısı için gerekli olan parametreleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8aa11-121">Add in any parameters that are required for hello HTTP call.</span></span>
   
    ![Tam HTTP eylemi](./media/connectors-native-http-swagger/using-action-2.png)
7. <span data-ttu-id="8aa11-123">toosave ve mantıksal uygulamanızı yayımlamak için tıklayın **kaydetmek** tasarımcı araç.</span><span class="sxs-lookup"><span data-stu-id="8aa11-123">toosave and publish your logic app, click **Save** on designer toolbar.</span></span>

### <a name="host-swagger-from-azure-storage"></a><span data-ttu-id="8aa11-124">Azure depolama biriminden konak Swagger</span><span class="sxs-lookup"><span data-stu-id="8aa11-124">Host Swagger from Azure Storage</span></span>
<span data-ttu-id="8aa11-125">Tooreference değil barındırılan veya hello Tasarımcısı için hello güvenlik ve çıkış noktaları arası gereksinimlerini karşılamıyor Swagger belgesinin isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8aa11-125">You might want tooreference a Swagger document that's not hosted, or that doesn't meet hello security and cross-origin requirements for hello designer.</span></span> <span data-ttu-id="8aa11-126">tooresolve Bu sorun, Azure depolama alanına hello Swagger belgesinin depolar ve CORS tooreference hello belge etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="8aa11-126">tooresolve this issue, you can store hello Swagger document in Azure Storage and enable CORS tooreference hello document.</span></span>  

<span data-ttu-id="8aa11-127">Hello adımları toocreate şunlardır, yapılandırma ve Azure depolama alanına Swagger belgeleri depolar:</span><span class="sxs-lookup"><span data-stu-id="8aa11-127">Here are hello steps toocreate, configure, and store Swagger documents in Azure Storage:</span></span>

1. <span data-ttu-id="8aa11-128">[Azure Blob storage ile Azure depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="8aa11-128">[Create an Azure storage account with Azure Blob storage](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="8aa11-129">tooperform Bu adım, izinleri ayarlama çok**genel erişim**.</span><span class="sxs-lookup"><span data-stu-id="8aa11-129">tooperform this step, set permissions too**Public Access**.</span></span>

2. <span data-ttu-id="8aa11-130">CORS hello blob üzerindeki etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="8aa11-130">Enable CORS on hello blob.</span></span> 

   <span data-ttu-id="8aa11-131">tooautomatically bu ayarı yapılandırmak için kullanabileceğiniz [bu PowerShell Betiği](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span><span class="sxs-lookup"><span data-stu-id="8aa11-131">tooautomatically configure this setting, you can use [this PowerShell script](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span></span>

3. <span data-ttu-id="8aa11-132">Merhaba Swagger dosyası toohello blob karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8aa11-132">Upload hello Swagger file toohello blob.</span></span> 

   <span data-ttu-id="8aa11-133">Bu adımı hello gerçekleştirebilirsiniz [Azure portal](https://portal.azure.com) veya gibi bir araçtan [Azure Storage Gezgini](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="8aa11-133">You can perform this step from hello [Azure portal](https://portal.azure.com) or from a tool like [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

4. <span data-ttu-id="8aa11-134">Azure Blob Depolama bir HTTPS bağlantısı toohello belgesinde başvuru.</span><span class="sxs-lookup"><span data-stu-id="8aa11-134">Reference an HTTPS link toohello document in Azure Blob storage.</span></span> 

   <span data-ttu-id="8aa11-135">Merhaba bağlantı bu biçimi kullanır:</span><span class="sxs-lookup"><span data-stu-id="8aa11-135">hello link uses this format:</span></span>

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a><span data-ttu-id="8aa11-136">Teknik Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="8aa11-136">Technical details</span></span>
<span data-ttu-id="8aa11-137">Aşağıda verilmiştir hello ayrıntıları hello tetikleyiciler ve Eylemler için bu HTTP + Swagger bağlayıcısını destekler.</span><span class="sxs-lookup"><span data-stu-id="8aa11-137">Following are hello details for hello triggers and actions that this HTTP + Swagger connector supports.</span></span>

## <a name="http--swagger-triggers"></a><span data-ttu-id="8aa11-138">HTTP + Swagger Tetikleyicileri</span><span class="sxs-lookup"><span data-stu-id="8aa11-138">HTTP + Swagger triggers</span></span>
<span data-ttu-id="8aa11-139">Bir tetikleyici bir mantıksal uygulama tanımlı kullanılan toostart hello iş akışı olabilecek bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="8aa11-139">A trigger is an event that can be used toostart hello workflow that's defined in a logic app.</span></span> [<span data-ttu-id="8aa11-140">Tetikleyiciler hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="8aa11-140">Learn more about triggers.</span></span>](connectors-overview.md) <span data-ttu-id="8aa11-141">Merhaba HTTP + Swagger Bağlayıcısı bir tetikleyici vardır.</span><span class="sxs-lookup"><span data-stu-id="8aa11-141">hello HTTP + Swagger connector has one trigger.</span></span>

| <span data-ttu-id="8aa11-142">Tetikleyici</span><span class="sxs-lookup"><span data-stu-id="8aa11-142">Trigger</span></span> | <span data-ttu-id="8aa11-143">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8aa11-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8aa11-144">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="8aa11-144">HTTP + Swagger</span></span> |<span data-ttu-id="8aa11-145">Bir HTTP çağrısı yapmak ve hello yanıt içeriği döndürür</span><span class="sxs-lookup"><span data-stu-id="8aa11-145">Make an HTTP call and return hello response content</span></span> |

## <a name="http--swagger-actions"></a><span data-ttu-id="8aa11-146">HTTP + Swagger Eylemler</span><span class="sxs-lookup"><span data-stu-id="8aa11-146">HTTP + Swagger actions</span></span>
<span data-ttu-id="8aa11-147">Bir eylem, bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="8aa11-147">An action is an operation that's carried out by hello workflow that's defined in a logic app.</span></span> [<span data-ttu-id="8aa11-148">Eylemler hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="8aa11-148">Learn more about actions.</span></span>](connectors-overview.md) <span data-ttu-id="8aa11-149">Merhaba HTTP + Swagger bağlayıcının bir olası eylem.</span><span class="sxs-lookup"><span data-stu-id="8aa11-149">hello HTTP + Swagger connector has one possible action.</span></span>

| <span data-ttu-id="8aa11-150">Eylem</span><span class="sxs-lookup"><span data-stu-id="8aa11-150">Action</span></span> | <span data-ttu-id="8aa11-151">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8aa11-151">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8aa11-152">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="8aa11-152">HTTP + Swagger</span></span> |<span data-ttu-id="8aa11-153">Bir HTTP çağrısı yapmak ve hello yanıt içeriği döndürür</span><span class="sxs-lookup"><span data-stu-id="8aa11-153">Make an HTTP call and return hello response content</span></span> |

### <a name="action-details"></a><span data-ttu-id="8aa11-154">Eylem ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="8aa11-154">Action details</span></span>
<span data-ttu-id="8aa11-155">Merhaba HTTP + Swagger bağlayıcı olası bir eylem ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="8aa11-155">hello HTTP + Swagger connector comes with one possible action.</span></span> <span data-ttu-id="8aa11-156">Aşağıda, her hello Eylemler, gerekli ve isteğe bağlı giriş alanları ve bunların kullanımıyla ilişkili çıkış ayrıntıları karşılık gelen hello hakkında bilgi verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="8aa11-156">Following is information about each of hello actions, their required and optional input fields, and hello corresponding output details that are associated with their usage.</span></span>

#### <a name="http--swagger"></a><span data-ttu-id="8aa11-157">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="8aa11-157">HTTP + Swagger</span></span>
<span data-ttu-id="8aa11-158">Giden HTTP isteğinden Swagger meta verileri Yardım olun.</span><span class="sxs-lookup"><span data-stu-id="8aa11-158">Make an HTTP outbound request with assistance of Swagger metadata.</span></span>
<span data-ttu-id="8aa11-159">Bir yıldız işareti (*) gerekli bir alan anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="8aa11-159">An asterisk (*) means a required field.</span></span>

| <span data-ttu-id="8aa11-160">Görünen ad</span><span class="sxs-lookup"><span data-stu-id="8aa11-160">Display name</span></span> | <span data-ttu-id="8aa11-161">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="8aa11-161">Property name</span></span> | <span data-ttu-id="8aa11-162">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8aa11-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8aa11-163">Yöntemi *</span><span class="sxs-lookup"><span data-stu-id="8aa11-163">Method*</span></span> |<span data-ttu-id="8aa11-164">Yöntemi</span><span class="sxs-lookup"><span data-stu-id="8aa11-164">method</span></span> |<span data-ttu-id="8aa11-165">HTTP fiili toouse.</span><span class="sxs-lookup"><span data-stu-id="8aa11-165">HTTP verb toouse.</span></span> |
| <span data-ttu-id="8aa11-166">URI *</span><span class="sxs-lookup"><span data-stu-id="8aa11-166">URI*</span></span> |<span data-ttu-id="8aa11-167">URI</span><span class="sxs-lookup"><span data-stu-id="8aa11-167">uri</span></span> |<span data-ttu-id="8aa11-168">Merhaba HTTP isteği için URI.</span><span class="sxs-lookup"><span data-stu-id="8aa11-168">URI for hello HTTP request.</span></span> |
| <span data-ttu-id="8aa11-169">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="8aa11-169">Headers</span></span> |<span data-ttu-id="8aa11-170">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="8aa11-170">headers</span></span> |<span data-ttu-id="8aa11-171">HTTP üstbilgileri tooinclude JSON nesnesinin.</span><span class="sxs-lookup"><span data-stu-id="8aa11-171">A JSON object of HTTP headers tooinclude.</span></span> |
| <span data-ttu-id="8aa11-172">Gövde</span><span class="sxs-lookup"><span data-stu-id="8aa11-172">Body</span></span> |<span data-ttu-id="8aa11-173">Gövde</span><span class="sxs-lookup"><span data-stu-id="8aa11-173">body</span></span> |<span data-ttu-id="8aa11-174">Merhaba HTTP istek gövdesi.</span><span class="sxs-lookup"><span data-stu-id="8aa11-174">hello HTTP request body.</span></span> |
| <span data-ttu-id="8aa11-175">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="8aa11-175">Authentication</span></span> |<span data-ttu-id="8aa11-176">Kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="8aa11-176">authentication</span></span> |<span data-ttu-id="8aa11-177">İstek için kimlik doğrulama toouse.</span><span class="sxs-lookup"><span data-stu-id="8aa11-177">Authentication toouse for request.</span></span> <span data-ttu-id="8aa11-178">Daha fazla bilgi için bkz: Merhaba [HTTP Bağlayıcısı](connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="8aa11-178">For more information, see hello [HTTP connector](connectors-native-http.md#authentication).</span></span> |

<span data-ttu-id="8aa11-179">**Çıkış Ayrıntıları**</span><span class="sxs-lookup"><span data-stu-id="8aa11-179">**Output details**</span></span>

<span data-ttu-id="8aa11-180">HTTP yanıtı</span><span class="sxs-lookup"><span data-stu-id="8aa11-180">HTTP response</span></span>

| <span data-ttu-id="8aa11-181">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="8aa11-181">Property Name</span></span> | <span data-ttu-id="8aa11-182">Veri türü</span><span class="sxs-lookup"><span data-stu-id="8aa11-182">Data type</span></span> | <span data-ttu-id="8aa11-183">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8aa11-183">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8aa11-184">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="8aa11-184">Headers</span></span> |<span data-ttu-id="8aa11-185">Nesne</span><span class="sxs-lookup"><span data-stu-id="8aa11-185">object</span></span> |<span data-ttu-id="8aa11-186">Yanıt Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="8aa11-186">Response headers</span></span> |
| <span data-ttu-id="8aa11-187">Gövde</span><span class="sxs-lookup"><span data-stu-id="8aa11-187">Body</span></span> |<span data-ttu-id="8aa11-188">Nesne</span><span class="sxs-lookup"><span data-stu-id="8aa11-188">object</span></span> |<span data-ttu-id="8aa11-189">Yanıt nesnesi</span><span class="sxs-lookup"><span data-stu-id="8aa11-189">Response object</span></span> |
| <span data-ttu-id="8aa11-190">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="8aa11-190">Status Code</span></span> |<span data-ttu-id="8aa11-191">Int</span><span class="sxs-lookup"><span data-stu-id="8aa11-191">int</span></span> |<span data-ttu-id="8aa11-192">HTTP durum kodu</span><span class="sxs-lookup"><span data-stu-id="8aa11-192">HTTP status code</span></span> |

### <a name="http-responses"></a><span data-ttu-id="8aa11-193">HTTP yanıtları</span><span class="sxs-lookup"><span data-stu-id="8aa11-193">HTTP responses</span></span>
<span data-ttu-id="8aa11-194">Çağrıları toovarious Eylemler yaparken, belirli yanıtları alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8aa11-194">When making calls toovarious actions, you might get certain responses.</span></span> <span data-ttu-id="8aa11-195">Karşılık gelen yanıtları ve açıklamaları özetleyen tablosu aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="8aa11-195">Following is a table that outlines corresponding responses and descriptions.</span></span>

| <span data-ttu-id="8aa11-196">Ad</span><span class="sxs-lookup"><span data-stu-id="8aa11-196">Name</span></span> | <span data-ttu-id="8aa11-197">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8aa11-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8aa11-198">200</span><span class="sxs-lookup"><span data-stu-id="8aa11-198">200</span></span> |<span data-ttu-id="8aa11-199">TAMAM</span><span class="sxs-lookup"><span data-stu-id="8aa11-199">OK</span></span> |
| <span data-ttu-id="8aa11-200">202</span><span class="sxs-lookup"><span data-stu-id="8aa11-200">202</span></span> |<span data-ttu-id="8aa11-201">Kabul edildi</span><span class="sxs-lookup"><span data-stu-id="8aa11-201">Accepted</span></span> |
| <span data-ttu-id="8aa11-202">400</span><span class="sxs-lookup"><span data-stu-id="8aa11-202">400</span></span> |<span data-ttu-id="8aa11-203">Hatalı istek</span><span class="sxs-lookup"><span data-stu-id="8aa11-203">Bad request</span></span> |
| <span data-ttu-id="8aa11-204">401</span><span class="sxs-lookup"><span data-stu-id="8aa11-204">401</span></span> |<span data-ttu-id="8aa11-205">Yetkilendirilmemiş</span><span class="sxs-lookup"><span data-stu-id="8aa11-205">Unauthorized</span></span> |
| <span data-ttu-id="8aa11-206">403</span><span class="sxs-lookup"><span data-stu-id="8aa11-206">403</span></span> |<span data-ttu-id="8aa11-207">Yasak</span><span class="sxs-lookup"><span data-stu-id="8aa11-207">Forbidden</span></span> |
| <span data-ttu-id="8aa11-208">404</span><span class="sxs-lookup"><span data-stu-id="8aa11-208">404</span></span> |<span data-ttu-id="8aa11-209">Bulunamadı</span><span class="sxs-lookup"><span data-stu-id="8aa11-209">Not Found</span></span> |
| <span data-ttu-id="8aa11-210">500</span><span class="sxs-lookup"><span data-stu-id="8aa11-210">500</span></span> |<span data-ttu-id="8aa11-211">İç sunucu hatası.</span><span class="sxs-lookup"><span data-stu-id="8aa11-211">Internal server error.</span></span> <span data-ttu-id="8aa11-212">Bilinmeyen bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="8aa11-212">Unknown error occurred.</span></span> |

- - -
## <a name="next-steps"></a><span data-ttu-id="8aa11-213">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8aa11-213">Next steps</span></span>

* [<span data-ttu-id="8aa11-214">Mantıksal uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8aa11-214">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="8aa11-215">Diğer bağlayıcıları Bul</span><span class="sxs-lookup"><span data-stu-id="8aa11-215">Find other connectors</span></span>](apis-list.md)