---
title: "REST uç HTTP + Swagger ile çağrı Azure Logic Apps bağlayıcı | Microsoft Docs"
description: "HTTP + Swagger ile Swagger aracılığıyla mantığı uygulamalardan REST Uç noktalara bağlanmak Bağlayıcısı"
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
ms.openlocfilehash: 3e9229d94e96aad7b769d0e55d208d856e3b80bc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-the-http--swagger-action"></a><span data-ttu-id="3a938-103">HTTP + Swagger ile başlama eylemi</span><span class="sxs-lookup"><span data-stu-id="3a938-103">Get started with the HTTP + Swagger action</span></span>

<span data-ttu-id="3a938-104">Tüm REST uç noktası aracılığıyla birinci sınıf bir bağlayıcı oluşturabilirsiniz bir [Swagger belgesinin](https://swagger.io) kullandığınızda, HTTP + Swagger mantığı uygulama akışınızın eylem.</span><span class="sxs-lookup"><span data-stu-id="3a938-104">You can create a first-class connector to any REST endpoint through a [Swagger document](https://swagger.io) when you use the HTTP + Swagger action in your logic app workflow.</span></span> <span data-ttu-id="3a938-105">Birinci sınıf bir mantıksal Uygulama Tasarımcısı deneyim herhangi bir REST uç nokta çağırmak için mantıksal uygulamalar da genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3a938-105">You can also extend logic apps to call any REST endpoint with a first-class Logic App Designer experience.</span></span>

<span data-ttu-id="3a938-106">Logic apps ile bağlayıcılar oluşturmayı öğrenmek için bkz: [yeni bir mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3a938-106">To learn how to create logic apps with connectors, see [Create a new logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a><span data-ttu-id="3a938-107">HTTP kullan + tetikleyicinin veya bir eylem olarak Swagger</span><span class="sxs-lookup"><span data-stu-id="3a938-107">Use HTTP + Swagger as a trigger or an action</span></span>

<span data-ttu-id="3a938-108">HTTP + tetiklemek Swagger ve aynı iş eylemi [HTTP eylemi](connectors-native-http.md) ancak API yapısı ve çıkışlarından göstererek mantığı Uygulama Tasarımcısı'nda daha iyi bir deneyim sağlamak [Swagger meta verileri](https://swagger.io).</span><span class="sxs-lookup"><span data-stu-id="3a938-108">The HTTP + Swagger trigger and action work the same as the [HTTP action](connectors-native-http.md) but provide a better experience in Logic App Designer by exposing the API structure and outputs from the [Swagger metadata](https://swagger.io).</span></span> <span data-ttu-id="3a938-109">HTTP de kullanabilirsiniz + Swagger bağlayıcı tetikleyici olarak.</span><span class="sxs-lookup"><span data-stu-id="3a938-109">You can also use the HTTP + Swagger connector as a trigger.</span></span> <span data-ttu-id="3a938-110">Yoklama Tetik uygulamak istiyorsanız, açıklanan yoklama modeli izleyen [diğer API'leri, hizmetleri ve sistemleri mantığı uygulamalardan çağırmak için özel API oluşturma](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span><span class="sxs-lookup"><span data-stu-id="3a938-110">If you want to implement a polling trigger, follow the polling pattern that's described in [Create custom APIs to call other APIs, services, and systems from logic apps](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span></span>

<span data-ttu-id="3a938-111">Daha fazla bilgi edinmek [mantığı uygulama tetikleyiciler ve Eylemler](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3a938-111">Learn more about [logic app triggers and actions](connectors-overview.md).</span></span>

<span data-ttu-id="3a938-112">Kullanım HTTP + Swagger işlem olarak bir mantıksal uygulama bir iş akışında bir eylemi nasıl örnek aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="3a938-112">Here's an example of how to use the HTTP + Swagger operation as an action in a workflow in a logic app.</span></span>

1. <span data-ttu-id="3a938-113">Seçin **yeni adım** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="3a938-113">Select the **New Step** button.</span></span>
2. <span data-ttu-id="3a938-114">Seçin **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="3a938-114">Select **Add an action**.</span></span>
3. <span data-ttu-id="3a938-115">Eylem arama kutusuna yazın **swagger** listesi HTTP + Swagger eylem.</span><span class="sxs-lookup"><span data-stu-id="3a938-115">In the action search box, type **swagger** to list the HTTP + Swagger action.</span></span>
   
    ![HTTP + Swagger seçin eylemi](./media/connectors-native-http-swagger/using-action-1.png)
4. <span data-ttu-id="3a938-117">Swagger belgesinin URL'sini yazın:</span><span class="sxs-lookup"><span data-stu-id="3a938-117">Type the URL for a Swagger document:</span></span>
   
   * <span data-ttu-id="3a938-118">Mantıksal Uygulama Tasarımcısı'ndan çalışmak için URL bir HTTPS uç noktası olması gerekir ve CORS etkinleştirdiniz.</span><span class="sxs-lookup"><span data-stu-id="3a938-118">To work from the Logic App Designer, the URL must be an HTTPS endpoint and have CORS enabled.</span></span>
   * <span data-ttu-id="3a938-119">Swagger belgesinin bu gereksinimi karşılamıyorsa, kullanabileceğiniz [Azure Storage CORS'yi ile](#hosting-swagger-from-storage) belge depolamak için.</span><span class="sxs-lookup"><span data-stu-id="3a938-119">If the Swagger document doesn't meet this requirement, you can use [Azure Storage with CORS enabled](#hosting-swagger-from-storage) to store the document.</span></span>
5. <span data-ttu-id="3a938-120">Tıklatın **sonraki** okuyun ve Swagger belgeyi işlemek için.</span><span class="sxs-lookup"><span data-stu-id="3a938-120">Click **Next** to read and render from the Swagger document.</span></span>
6. <span data-ttu-id="3a938-121">HTTP çağrısı için gerekli olan parametreleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="3a938-121">Add in any parameters that are required for the HTTP call.</span></span>
   
    ![Tam HTTP eylemi](./media/connectors-native-http-swagger/using-action-2.png)
7. <span data-ttu-id="3a938-123">Kaydetmek ve mantıksal uygulamanızı yayımlamak için **kaydetmek** tasarımcı araç.</span><span class="sxs-lookup"><span data-stu-id="3a938-123">To save and publish your logic app, click **Save** on designer toolbar.</span></span>

### <a name="host-swagger-from-azure-storage"></a><span data-ttu-id="3a938-124">Azure depolama biriminden konak Swagger</span><span class="sxs-lookup"><span data-stu-id="3a938-124">Host Swagger from Azure Storage</span></span>
<span data-ttu-id="3a938-125">Değil barındırılan ya da, güvenlik ve tasarımcı çıkış noktaları arası gereksinimlerini karşılamıyor Swagger belgeye başvurmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3a938-125">You might want to reference a Swagger document that's not hosted, or that doesn't meet the security and cross-origin requirements for the designer.</span></span> <span data-ttu-id="3a938-126">Bu sorunu çözmek için Swagger belgesinin Azure depolama alanına depolar ve belgeye başvurmak CORS etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="3a938-126">To resolve this issue, you can store the Swagger document in Azure Storage and enable CORS to reference the document.</span></span>  

<span data-ttu-id="3a938-127">Oluşturma, yapılandırma ve Azure depolama alanında Swagger belgeleri depolamak için adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="3a938-127">Here are the steps to create, configure, and store Swagger documents in Azure Storage:</span></span>

1. <span data-ttu-id="3a938-128">[Azure Blob storage ile Azure depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="3a938-128">[Create an Azure storage account with Azure Blob storage](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="3a938-129">Bu adımı gerçekleştirmek için izinleri ayarla **genel erişim**.</span><span class="sxs-lookup"><span data-stu-id="3a938-129">To perform this step, set permissions to **Public Access**.</span></span>

2. <span data-ttu-id="3a938-130">CORS blob üzerindeki etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="3a938-130">Enable CORS on the blob.</span></span> 

   <span data-ttu-id="3a938-131">Bu ayarı otomatik olarak yapılandırmak için kullanabileceğiniz [bu PowerShell Betiği](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span><span class="sxs-lookup"><span data-stu-id="3a938-131">To automatically configure this setting, you can use [this PowerShell script](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span></span>

3. <span data-ttu-id="3a938-132">Swagger dosyası için blob karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3a938-132">Upload the Swagger file to the blob.</span></span> 

   <span data-ttu-id="3a938-133">Bu adımdaki gerçekleştirebilirsiniz [Azure portal](https://portal.azure.com) veya gibi bir araçtan [Azure Storage Gezgini](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="3a938-133">You can perform this step from the [Azure portal](https://portal.azure.com) or from a tool like [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

4. <span data-ttu-id="3a938-134">Bir HTTPS bağlantısı Azure Blob Depolama belgesine başvurun.</span><span class="sxs-lookup"><span data-stu-id="3a938-134">Reference an HTTPS link to the document in Azure Blob storage.</span></span> 

   <span data-ttu-id="3a938-135">Bağlantı bu biçimi kullanır:</span><span class="sxs-lookup"><span data-stu-id="3a938-135">The link uses this format:</span></span>

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a><span data-ttu-id="3a938-136">Teknik Ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="3a938-136">Technical details</span></span>
<span data-ttu-id="3a938-137">Tetikleyiciler ve Eylemler için Ayrıntılar verilmiştir, bu HTTP + Swagger bağlayıcısını destekler.</span><span class="sxs-lookup"><span data-stu-id="3a938-137">Following are the details for the triggers and actions that this HTTP + Swagger connector supports.</span></span>

## <a name="http--swagger-triggers"></a><span data-ttu-id="3a938-138">HTTP + Swagger Tetikleyicileri</span><span class="sxs-lookup"><span data-stu-id="3a938-138">HTTP + Swagger triggers</span></span>
<span data-ttu-id="3a938-139">Bir tetikleyici bir mantıksal uygulama tanımlı iş akışını başlatmak için kullanılan bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="3a938-139">A trigger is an event that can be used to start the workflow that's defined in a logic app.</span></span> [<span data-ttu-id="3a938-140">Tetikleyiciler hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="3a938-140">Learn more about triggers.</span></span>](connectors-overview.md) <span data-ttu-id="3a938-141">HTTP + Swagger Bağlayıcısı bir tetikleyici vardır.</span><span class="sxs-lookup"><span data-stu-id="3a938-141">The HTTP + Swagger connector has one trigger.</span></span>

| <span data-ttu-id="3a938-142">Tetikleyici</span><span class="sxs-lookup"><span data-stu-id="3a938-142">Trigger</span></span> | <span data-ttu-id="3a938-143">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3a938-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3a938-144">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="3a938-144">HTTP + Swagger</span></span> |<span data-ttu-id="3a938-145">Bir HTTP çağrısı yapmak ve yanıt içeriği döndürür</span><span class="sxs-lookup"><span data-stu-id="3a938-145">Make an HTTP call and return the response content</span></span> |

## <a name="http--swagger-actions"></a><span data-ttu-id="3a938-146">HTTP + Swagger Eylemler</span><span class="sxs-lookup"><span data-stu-id="3a938-146">HTTP + Swagger actions</span></span>
<span data-ttu-id="3a938-147">Bir eylem, bir mantıksal uygulama içinde tanımlanan iş akışı tarafından gerçekleştirilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="3a938-147">An action is an operation that's carried out by the workflow that's defined in a logic app.</span></span> [<span data-ttu-id="3a938-148">Eylemler hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="3a938-148">Learn more about actions.</span></span>](connectors-overview.md) <span data-ttu-id="3a938-149">HTTP + Swagger bağlayıcının bir olası eylem.</span><span class="sxs-lookup"><span data-stu-id="3a938-149">The HTTP + Swagger connector has one possible action.</span></span>

| <span data-ttu-id="3a938-150">Eylem</span><span class="sxs-lookup"><span data-stu-id="3a938-150">Action</span></span> | <span data-ttu-id="3a938-151">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3a938-151">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3a938-152">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="3a938-152">HTTP + Swagger</span></span> |<span data-ttu-id="3a938-153">Bir HTTP çağrısı yapmak ve yanıt içeriği döndürür</span><span class="sxs-lookup"><span data-stu-id="3a938-153">Make an HTTP call and return the response content</span></span> |

### <a name="action-details"></a><span data-ttu-id="3a938-154">Eylem ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="3a938-154">Action details</span></span>
<span data-ttu-id="3a938-155">HTTP + Swagger bağlayıcı olası bir eylem ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="3a938-155">The HTTP + Swagger connector comes with one possible action.</span></span> <span data-ttu-id="3a938-156">Aşağıda, her eylemleri, bunların gerekli ve isteğe bağlı giriş alanları ve kullanımı ile ilişkilendirilmiş ilgili çıkış ayrıntıları hakkında bilgi verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3a938-156">Following is information about each of the actions, their required and optional input fields, and the corresponding output details that are associated with their usage.</span></span>

#### <a name="http--swagger"></a><span data-ttu-id="3a938-157">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="3a938-157">HTTP + Swagger</span></span>
<span data-ttu-id="3a938-158">Giden HTTP isteğinden Swagger meta verileri Yardım olun.</span><span class="sxs-lookup"><span data-stu-id="3a938-158">Make an HTTP outbound request with assistance of Swagger metadata.</span></span>
<span data-ttu-id="3a938-159">Bir yıldız işareti (*) gerekli bir alan anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="3a938-159">An asterisk (*) means a required field.</span></span>

| <span data-ttu-id="3a938-160">Görünen ad</span><span class="sxs-lookup"><span data-stu-id="3a938-160">Display name</span></span> | <span data-ttu-id="3a938-161">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="3a938-161">Property name</span></span> | <span data-ttu-id="3a938-162">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3a938-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3a938-163">Yöntemi *</span><span class="sxs-lookup"><span data-stu-id="3a938-163">Method*</span></span> |<span data-ttu-id="3a938-164">Yöntemi</span><span class="sxs-lookup"><span data-stu-id="3a938-164">method</span></span> |<span data-ttu-id="3a938-165">HTTP fiili'kullanılacak.</span><span class="sxs-lookup"><span data-stu-id="3a938-165">HTTP verb to use.</span></span> |
| <span data-ttu-id="3a938-166">URI *</span><span class="sxs-lookup"><span data-stu-id="3a938-166">URI*</span></span> |<span data-ttu-id="3a938-167">URI</span><span class="sxs-lookup"><span data-stu-id="3a938-167">uri</span></span> |<span data-ttu-id="3a938-168">HTTP isteği için URI.</span><span class="sxs-lookup"><span data-stu-id="3a938-168">URI for the HTTP request.</span></span> |
| <span data-ttu-id="3a938-169">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="3a938-169">Headers</span></span> |<span data-ttu-id="3a938-170">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="3a938-170">headers</span></span> |<span data-ttu-id="3a938-171">Eklenecek HTTP üstbilgilerini JSON nesnesinin.</span><span class="sxs-lookup"><span data-stu-id="3a938-171">A JSON object of HTTP headers to include.</span></span> |
| <span data-ttu-id="3a938-172">Gövde</span><span class="sxs-lookup"><span data-stu-id="3a938-172">Body</span></span> |<span data-ttu-id="3a938-173">Gövde</span><span class="sxs-lookup"><span data-stu-id="3a938-173">body</span></span> |<span data-ttu-id="3a938-174">HTTP istek gövdesi.</span><span class="sxs-lookup"><span data-stu-id="3a938-174">The HTTP request body.</span></span> |
| <span data-ttu-id="3a938-175">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="3a938-175">Authentication</span></span> |<span data-ttu-id="3a938-176">Kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="3a938-176">authentication</span></span> |<span data-ttu-id="3a938-177">İstek için kullanılacak kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="3a938-177">Authentication to use for request.</span></span> <span data-ttu-id="3a938-178">Daha fazla bilgi için bkz: [HTTP Bağlayıcısı](connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="3a938-178">For more information, see the [HTTP connector](connectors-native-http.md#authentication).</span></span> |

<span data-ttu-id="3a938-179">**Çıkış Ayrıntıları**</span><span class="sxs-lookup"><span data-stu-id="3a938-179">**Output details**</span></span>

<span data-ttu-id="3a938-180">HTTP yanıtı</span><span class="sxs-lookup"><span data-stu-id="3a938-180">HTTP response</span></span>

| <span data-ttu-id="3a938-181">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="3a938-181">Property Name</span></span> | <span data-ttu-id="3a938-182">Veri türü</span><span class="sxs-lookup"><span data-stu-id="3a938-182">Data type</span></span> | <span data-ttu-id="3a938-183">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3a938-183">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3a938-184">Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="3a938-184">Headers</span></span> |<span data-ttu-id="3a938-185">Nesne</span><span class="sxs-lookup"><span data-stu-id="3a938-185">object</span></span> |<span data-ttu-id="3a938-186">Yanıt Üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="3a938-186">Response headers</span></span> |
| <span data-ttu-id="3a938-187">Gövde</span><span class="sxs-lookup"><span data-stu-id="3a938-187">Body</span></span> |<span data-ttu-id="3a938-188">Nesne</span><span class="sxs-lookup"><span data-stu-id="3a938-188">object</span></span> |<span data-ttu-id="3a938-189">Yanıt nesnesi</span><span class="sxs-lookup"><span data-stu-id="3a938-189">Response object</span></span> |
| <span data-ttu-id="3a938-190">Durum kodu</span><span class="sxs-lookup"><span data-stu-id="3a938-190">Status Code</span></span> |<span data-ttu-id="3a938-191">Int</span><span class="sxs-lookup"><span data-stu-id="3a938-191">int</span></span> |<span data-ttu-id="3a938-192">HTTP durum kodu</span><span class="sxs-lookup"><span data-stu-id="3a938-192">HTTP status code</span></span> |

### <a name="http-responses"></a><span data-ttu-id="3a938-193">HTTP yanıtları</span><span class="sxs-lookup"><span data-stu-id="3a938-193">HTTP responses</span></span>
<span data-ttu-id="3a938-194">Çeşitli eylemler için çağrıları yapılırken belirli yanıtları alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3a938-194">When making calls to various actions, you might get certain responses.</span></span> <span data-ttu-id="3a938-195">Karşılık gelen yanıtları ve açıklamaları özetleyen tablosu aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="3a938-195">Following is a table that outlines corresponding responses and descriptions.</span></span>

| <span data-ttu-id="3a938-196">Ad</span><span class="sxs-lookup"><span data-stu-id="3a938-196">Name</span></span> | <span data-ttu-id="3a938-197">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3a938-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3a938-198">200</span><span class="sxs-lookup"><span data-stu-id="3a938-198">200</span></span> |<span data-ttu-id="3a938-199">TAMAM</span><span class="sxs-lookup"><span data-stu-id="3a938-199">OK</span></span> |
| <span data-ttu-id="3a938-200">202</span><span class="sxs-lookup"><span data-stu-id="3a938-200">202</span></span> |<span data-ttu-id="3a938-201">Kabul edildi</span><span class="sxs-lookup"><span data-stu-id="3a938-201">Accepted</span></span> |
| <span data-ttu-id="3a938-202">400</span><span class="sxs-lookup"><span data-stu-id="3a938-202">400</span></span> |<span data-ttu-id="3a938-203">Hatalı istek</span><span class="sxs-lookup"><span data-stu-id="3a938-203">Bad request</span></span> |
| <span data-ttu-id="3a938-204">401</span><span class="sxs-lookup"><span data-stu-id="3a938-204">401</span></span> |<span data-ttu-id="3a938-205">Yetkilendirilmemiş</span><span class="sxs-lookup"><span data-stu-id="3a938-205">Unauthorized</span></span> |
| <span data-ttu-id="3a938-206">403</span><span class="sxs-lookup"><span data-stu-id="3a938-206">403</span></span> |<span data-ttu-id="3a938-207">Yasak</span><span class="sxs-lookup"><span data-stu-id="3a938-207">Forbidden</span></span> |
| <span data-ttu-id="3a938-208">404</span><span class="sxs-lookup"><span data-stu-id="3a938-208">404</span></span> |<span data-ttu-id="3a938-209">Bulunamadı</span><span class="sxs-lookup"><span data-stu-id="3a938-209">Not Found</span></span> |
| <span data-ttu-id="3a938-210">500</span><span class="sxs-lookup"><span data-stu-id="3a938-210">500</span></span> |<span data-ttu-id="3a938-211">İç sunucu hatası.</span><span class="sxs-lookup"><span data-stu-id="3a938-211">Internal server error.</span></span> <span data-ttu-id="3a938-212">Bilinmeyen bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="3a938-212">Unknown error occurred.</span></span> |

- - -
## <a name="next-steps"></a><span data-ttu-id="3a938-213">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3a938-213">Next steps</span></span>

* [<span data-ttu-id="3a938-214">Mantıksal uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3a938-214">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="3a938-215">Diğer bağlayıcıları Bul</span><span class="sxs-lookup"><span data-stu-id="3a938-215">Find other connectors</span></span>](apis-list.md)