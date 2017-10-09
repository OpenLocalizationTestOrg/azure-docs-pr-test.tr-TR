---
title: "aaaLog Analytics HTTP veri toplayıcı API | Microsoft Docs"
description: "Merhaba günlük analizi HTTP veri toplayıcı API tooadd POST JSON veri toohello günlük analizi deposu hello REST API'si çağırabilirsiniz herhangi bir istemciden kullanabilirsiniz. Bu makalede nasıl toouse API hello ve örnekleri sahip farklı programlama dillerini kullanarak toopublish veri."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: c2921082831c49da764d946ac9c4fab975a38185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="send-data-toolog-analytics-with-hello-http-data-collector-api"></a><span data-ttu-id="72d94-104">Merhaba HTTP veri toplayıcı API ile veri tooLog Analytics Gönder</span><span class="sxs-lookup"><span data-stu-id="72d94-104">Send data tooLog Analytics with hello HTTP Data Collector API</span></span>
<span data-ttu-id="72d94-105">Bu makalede nasıl toouse hello REST API istemciden gelen HTTP veri toplayıcı API toosend veri tooLog Analytics gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="72d94-105">This article shows you how toouse hello HTTP Data Collector API toosend data tooLog Analytics from a REST API client.</span></span>  <span data-ttu-id="72d94-106">Komut dosyası veya uygulama tarafından toplanan tooformat verileri bir istekte içerir ve nasıl günlük analizi tarafından yetkili bu istekte açıklar.</span><span class="sxs-lookup"><span data-stu-id="72d94-106">It describes how tooformat data collected by your script or application, include it in a request, and have that request authorized by Log Analytics.</span></span>  <span data-ttu-id="72d94-107">PowerShell, C# ve Python için örnekler verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="72d94-107">Examples are provided for PowerShell, C#, and Python.</span></span>

## <a name="concepts"></a><span data-ttu-id="72d94-108">Kavramlar</span><span class="sxs-lookup"><span data-stu-id="72d94-108">Concepts</span></span>
<span data-ttu-id="72d94-109">Bir REST API'si çağırabilirsiniz herhangi bir istemciden hello HTTP veri toplayıcı API toosend veri tooLog Analytics kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72d94-109">You can use hello HTTP Data Collector API toosend data tooLog Analytics from any client that can call a REST API.</span></span>  <span data-ttu-id="72d94-110">Bu runbook olabilir Azure Otomasyonu'nda yönetim toplar Azure veya başka bir bulut ya da verileri günlük analizi tooconsolidate kullanan bir alternatif yönetim sisteminin ve verileri analiz etmek.</span><span class="sxs-lookup"><span data-stu-id="72d94-110">This might be a runbook in Azure Automation that collects management data from Azure or another cloud, or it might be an alternate management system that uses Log Analytics tooconsolidate and analyze data.</span></span>

<span data-ttu-id="72d94-111">Merhaba günlük analizi deposundaki tüm verileri belirli bir kayıt türü içeren bir kayıt olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="72d94-111">All data in hello Log Analytics repository is stored as a record with a particular record type.</span></span>  <span data-ttu-id="72d94-112">Veri toosend toohello HTTP veri toplayıcı API JSON içinde birden çok kayıt olarak biçimlendirin.</span><span class="sxs-lookup"><span data-stu-id="72d94-112">You format your data toosend toohello HTTP Data Collector API as multiple records in JSON.</span></span>  <span data-ttu-id="72d94-113">Merhaba veri gönderdiğinde, tek bir kaydın hello depo hello isteği yükü her kayıt için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="72d94-113">When you submit hello data, an individual record is created in hello repository for each record in hello request payload.</span></span>


![HTTP veri toplayıcı genel bakış](media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a><span data-ttu-id="72d94-115">Bir isteği oluşturun</span><span class="sxs-lookup"><span data-stu-id="72d94-115">Create a request</span></span>
<span data-ttu-id="72d94-116">toouse hello HTTP veri toplayıcı API hello veri toosend JavaScript nesne gösterimi (JSON) içeren bir POST isteği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="72d94-116">toouse hello HTTP Data Collector API, you create a POST request that includes hello data toosend in JavaScript Object Notation (JSON).</span></span>  <span data-ttu-id="72d94-117">her istek için gerekli olan sonraki üç tablolar listesi hello öznitelikler hello.</span><span class="sxs-lookup"><span data-stu-id="72d94-117">hello next three tables list hello attributes that are required for each request.</span></span> <span data-ttu-id="72d94-118">Biz her özniteliği hello makalenin sonraki bölümlerinde daha ayrıntılı açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="72d94-118">We describe each attribute in more detail later in hello article.</span></span>

### <a name="request-uri"></a><span data-ttu-id="72d94-119">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="72d94-119">Request URI</span></span>
| <span data-ttu-id="72d94-120">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="72d94-120">Attribute</span></span> | <span data-ttu-id="72d94-121">Özellik</span><span class="sxs-lookup"><span data-stu-id="72d94-121">Property</span></span> |
|:--- |:--- |
| <span data-ttu-id="72d94-122">Yöntem</span><span class="sxs-lookup"><span data-stu-id="72d94-122">Method</span></span> |<span data-ttu-id="72d94-123">YAYINLA</span><span class="sxs-lookup"><span data-stu-id="72d94-123">POST</span></span> |
| <span data-ttu-id="72d94-124">URI</span><span class="sxs-lookup"><span data-stu-id="72d94-124">URI</span></span> |<span data-ttu-id="72d94-125">https://\<CustomerID\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span><span class="sxs-lookup"><span data-stu-id="72d94-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span></span> |
| <span data-ttu-id="72d94-126">İçerik türü</span><span class="sxs-lookup"><span data-stu-id="72d94-126">Content type</span></span> |<span data-ttu-id="72d94-127">uygulama/json</span><span class="sxs-lookup"><span data-stu-id="72d94-127">application/json</span></span> |

### <a name="request-uri-parameters"></a><span data-ttu-id="72d94-128">İstek URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="72d94-128">Request URI parameters</span></span>
| <span data-ttu-id="72d94-129">Parametre</span><span class="sxs-lookup"><span data-stu-id="72d94-129">Parameter</span></span> | <span data-ttu-id="72d94-130">Açıklama</span><span class="sxs-lookup"><span data-stu-id="72d94-130">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="72d94-131">CustomerID</span><span class="sxs-lookup"><span data-stu-id="72d94-131">CustomerID</span></span> |<span data-ttu-id="72d94-132">Merhaba hello Microsoft Operations Management Suite çalışma alanı için benzersiz tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="72d94-132">hello unique identifier for hello Microsoft Operations Management Suite workspace.</span></span> |
| <span data-ttu-id="72d94-133">Kaynak</span><span class="sxs-lookup"><span data-stu-id="72d94-133">Resource</span></span> |<span data-ttu-id="72d94-134">Merhaba API kaynak adı: / api/günlükleri.</span><span class="sxs-lookup"><span data-stu-id="72d94-134">hello API resource name: /api/logs.</span></span> |
| <span data-ttu-id="72d94-135">API sürümü</span><span class="sxs-lookup"><span data-stu-id="72d94-135">API Version</span></span> |<span data-ttu-id="72d94-136">Bu istek ile Merhaba API toouse Hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="72d94-136">hello version of hello API toouse with this request.</span></span> <span data-ttu-id="72d94-137">Şu anda, 2016-04-01 değil.</span><span class="sxs-lookup"><span data-stu-id="72d94-137">Currently, it's 2016-04-01.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="72d94-138">İstek üstbilgileri</span><span class="sxs-lookup"><span data-stu-id="72d94-138">Request headers</span></span>
| <span data-ttu-id="72d94-139">Üstbilgi</span><span class="sxs-lookup"><span data-stu-id="72d94-139">Header</span></span> | <span data-ttu-id="72d94-140">Açıklama</span><span class="sxs-lookup"><span data-stu-id="72d94-140">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="72d94-141">Yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="72d94-141">Authorization</span></span> |<span data-ttu-id="72d94-142">Merhaba yetkilendirme imzası.</span><span class="sxs-lookup"><span data-stu-id="72d94-142">hello authorization signature.</span></span> <span data-ttu-id="72d94-143">Merhaba makalenin sonraki bölümlerinde, hakkında bilgi edinebilirsiniz toocreate HMAC SHA256 üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="72d94-143">Later in hello article, you can read about how toocreate an HMAC-SHA256 header.</span></span> |
| <span data-ttu-id="72d94-144">Günlük türü</span><span class="sxs-lookup"><span data-stu-id="72d94-144">Log-Type</span></span> |<span data-ttu-id="72d94-145">Merhaba kayıt gönderiliyor hello veri türünü belirtin.</span><span class="sxs-lookup"><span data-stu-id="72d94-145">Specify hello record type of hello data that is being submitted.</span></span> <span data-ttu-id="72d94-146">Şu anda, yalnızca alfasayısal karakterler hello günlük türünü destekler.</span><span class="sxs-lookup"><span data-stu-id="72d94-146">Currently, hello log type supports only alpha characters.</span></span> <span data-ttu-id="72d94-147">Sayısal türler veya özel karakterler desteklemez.</span><span class="sxs-lookup"><span data-stu-id="72d94-147">It does not support numerics or special characters.</span></span> |
| <span data-ttu-id="72d94-148">x-ms-date</span><span class="sxs-lookup"><span data-stu-id="72d94-148">x-ms-date</span></span> |<span data-ttu-id="72d94-149">Başlangıç tarihi, Başlangıç isteği işlendi, RFC 1123 biçiminde.</span><span class="sxs-lookup"><span data-stu-id="72d94-149">hello date that hello request was processed, in RFC 1123 format.</span></span> |
| <span data-ttu-id="72d94-150">saat oluşturulan alanı</span><span class="sxs-lookup"><span data-stu-id="72d94-150">time-generated-field</span></span> |<span data-ttu-id="72d94-151">Merhaba veri öğesinin hello zaman damgası içeren hello veri alanına Hello adı.</span><span class="sxs-lookup"><span data-stu-id="72d94-151">hello name of a field in hello data that contains hello timestamp of hello data item.</span></span> <span data-ttu-id="72d94-152">Bir alan belirtin sonra içeriği için kullanılan **TimeGenerated**.</span><span class="sxs-lookup"><span data-stu-id="72d94-152">If you specify a field then its contents are used for **TimeGenerated**.</span></span> <span data-ttu-id="72d94-153">Bu alan belirtilmezse, varsayılan hello **TimeGenerated** bu hello hello zamandır ileti alınan.</span><span class="sxs-lookup"><span data-stu-id="72d94-153">If this field isn’t specified, hello default for **TimeGenerated** is hello time that hello message is ingested.</span></span> <span data-ttu-id="72d94-154">Merhaba ileti alanının Merhaba içeriğine hello ISO 8601 biçimi YYYY izlemelidir-aa-: ssZ.</span><span class="sxs-lookup"><span data-stu-id="72d94-154">hello contents of hello message field should follow hello ISO 8601 format YYYY-MM-DDThh:mm:ssZ.</span></span> |

## <a name="authorization"></a><span data-ttu-id="72d94-155">Yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="72d94-155">Authorization</span></span>
<span data-ttu-id="72d94-156">Tüm istek toohello günlük analizi HTTP veri toplayıcı API bir authorization üstbilgisi eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="72d94-156">Any request toohello Log Analytics HTTP Data Collector API must include an authorization header.</span></span> <span data-ttu-id="72d94-157">bir istek tooauthenticate hello istekle hello birincil ya da hello isteği yapan hello çalışma alanı için ikincil anahtar hello oturum açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="72d94-157">tooauthenticate a request, you must sign hello request with either hello primary or hello secondary key for hello workspace that is making hello request.</span></span> <span data-ttu-id="72d94-158">Daha sonra bu imza hello isteğin bir parçası geçirin.</span><span class="sxs-lookup"><span data-stu-id="72d94-158">Then, pass that signature as part of hello request.</span></span>   

<span data-ttu-id="72d94-159">Merhaba authorization üstbilgisi için hello biçimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="72d94-159">Here's hello format for hello authorization header:</span></span>

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

<span data-ttu-id="72d94-160">*Workspaceıd* hello Operations Management Suite çalışma hello benzersiz tanımlayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="72d94-160">*WorkspaceID* is hello unique identifier for hello Operations Management Suite workspace.</span></span> <span data-ttu-id="72d94-161">*İmza* olan bir [karma tabanlı ileti kimlik doğrulama kodu (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) hello isteğinden oluşturulan ve hello kullanarak hesaplanan [SHA256 algoritmasını](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span><span class="sxs-lookup"><span data-stu-id="72d94-161">*Signature* is a [Hash-based Message Authentication Code (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) that is constructed from hello request and then computed by using hello [SHA256 algorithm](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span></span> <span data-ttu-id="72d94-162">Ardından, onu Base64 kodlaması kullanarak kodlayın.</span><span class="sxs-lookup"><span data-stu-id="72d94-162">Then, you encode it by using Base64 encoding.</span></span>

<span data-ttu-id="72d94-163">Bu biçim tooencode hello kullan **SharedKey** imza dizesi:</span><span class="sxs-lookup"><span data-stu-id="72d94-163">Use this format tooencode hello **SharedKey** signature string:</span></span>

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

<span data-ttu-id="72d94-164">İmza dize örneği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="72d94-164">Here's an example of a signature string:</span></span>

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

<span data-ttu-id="72d94-165">Kullanarak kodlayın hello imza dize olduğunda HMAC SHA256 algoritmasını hello UTF-8 kodlu dize üzerinde hello ve hello sonucu Base64 olarak kodlayın.</span><span class="sxs-lookup"><span data-stu-id="72d94-165">When you have hello signature string, encode it by using hello HMAC-SHA256 algorithm on hello UTF-8-encoded string, and then encode hello result as Base64.</span></span> <span data-ttu-id="72d94-166">Şu biçimi kullanın:</span><span class="sxs-lookup"><span data-stu-id="72d94-166">Use this format:</span></span>

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

<span data-ttu-id="72d94-167">Merhaba sonraki bölümlerde Hello örnekleri bir authorization üstbilgisi oluşturduğunuz örnek kod toohelp sahip.</span><span class="sxs-lookup"><span data-stu-id="72d94-167">hello samples in hello next sections have sample code toohelp you create an authorization header.</span></span>

## <a name="request-body"></a><span data-ttu-id="72d94-168">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="72d94-168">Request body</span></span>
<span data-ttu-id="72d94-169">Merhaba ileti gövdesi Hello JSON'de olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="72d94-169">hello body of hello message must be in JSON.</span></span> <span data-ttu-id="72d94-170">Bu biçimde hello özelliği ad ve değer çiftleri ile bir veya daha fazla kayıt içermesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="72d94-170">It must include one or more records with hello property name and value pairs in this format:</span></span>

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

<span data-ttu-id="72d94-171">Biçim aşağıdaki hello kullanarak tek bir istekte birden çok kayıt toplu.</span><span class="sxs-lookup"><span data-stu-id="72d94-171">You can batch multiple records together in a single request by using hello following format.</span></span> <span data-ttu-id="72d94-172">Tüm hello kayıtları hello olmalıdır aynı kayıt türü.</span><span class="sxs-lookup"><span data-stu-id="72d94-172">All hello records must be hello same record type.</span></span>

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
},
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

## <a name="record-type-and-properties"></a><span data-ttu-id="72d94-173">Kayıt türü ve özellikleri</span><span class="sxs-lookup"><span data-stu-id="72d94-173">Record type and properties</span></span>
<span data-ttu-id="72d94-174">Merhaba günlük analizi HTTP veri toplayıcı API aracılığıyla veri gönderdiğinde, özel bir kayıt türü tanımlarsınız.</span><span class="sxs-lookup"><span data-stu-id="72d94-174">You define a custom record type when you submit data through hello Log Analytics HTTP Data Collector API.</span></span> <span data-ttu-id="72d94-175">Şu anda, oluşturulan kayıt türleri diğer veri türleri ve çözümleri tarafından veri tooexisting yazamıyor.</span><span class="sxs-lookup"><span data-stu-id="72d94-175">Currently, you can't write data tooexisting record types that were created by other data types and solutions.</span></span> <span data-ttu-id="72d94-176">Günlük analizi hello gelen verileri okur ve girdiğiniz hello değerlerin hello veri türüyle eşleşen özelliklerini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="72d94-176">Log Analytics reads hello incoming data and then creates properties that match hello data types of hello values that you enter.</span></span>

<span data-ttu-id="72d94-177">Günlük analizi API içermelidir her isteği toohello bir **günlük türü** hello kayıt türünün hello ada sahip üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="72d94-177">Each request toohello Log Analytics API must include a **Log-Type** header with hello name for hello record type.</span></span> <span data-ttu-id="72d94-178">Merhaba soneki **_CL** otomatik olarak eklenen toohello addır, diğer günlüğünden türleri özel bir günlük toodistinguish girin.</span><span class="sxs-lookup"><span data-stu-id="72d94-178">hello suffix **_CL** is automatically appended toohello name you enter toodistinguish it from other log types as a custom log.</span></span> <span data-ttu-id="72d94-179">Örneğin, hello adı girerseniz **MyNewRecordType**, günlük analizi hello türündeki bir kayıt oluşturur **MyNewRecordType_CL**.</span><span class="sxs-lookup"><span data-stu-id="72d94-179">For example, if you enter hello name **MyNewRecordType**, Log Analytics creates a record with hello type **MyNewRecordType_CL**.</span></span> <span data-ttu-id="72d94-180">Bu, kullanıcı tarafından oluşturulan tür adları ve bunlar geçerli veya gelecek Microsoft çözümlerinde sevk arasında çakışmalar olduğundan emin olun yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="72d94-180">This helps ensure that there are no conflicts between user-created type names and those shipped in current or future Microsoft solutions.</span></span>

<span data-ttu-id="72d94-181">tooidentify bir özelliğin veri türü, günlük analizi soneki toohello özellik adı ekler.</span><span class="sxs-lookup"><span data-stu-id="72d94-181">tooidentify a property's data type, Log Analytics adds a suffix toohello property name.</span></span> <span data-ttu-id="72d94-182">Bir özellik boş bir değer içeriyorsa, hello özelliği bulunan ve bu kaydı bulunmaz.</span><span class="sxs-lookup"><span data-stu-id="72d94-182">If a property contains a null value, hello property is not included in that record.</span></span> <span data-ttu-id="72d94-183">Bu tabloda hello özellik veri türünü ve karşılık gelen sonekinin listelenmektedir:</span><span class="sxs-lookup"><span data-stu-id="72d94-183">This table lists hello property data type and corresponding suffix:</span></span>

| <span data-ttu-id="72d94-184">Özellik veri türü</span><span class="sxs-lookup"><span data-stu-id="72d94-184">Property data type</span></span> | <span data-ttu-id="72d94-185">Son eki</span><span class="sxs-lookup"><span data-stu-id="72d94-185">Suffix</span></span> |
|:--- |:--- |
| <span data-ttu-id="72d94-186">Dize</span><span class="sxs-lookup"><span data-stu-id="72d94-186">String</span></span> |<span data-ttu-id="72d94-187">_Yanları</span><span class="sxs-lookup"><span data-stu-id="72d94-187">_s</span></span> |
| <span data-ttu-id="72d94-188">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="72d94-188">Boolean</span></span> |<span data-ttu-id="72d94-189">_B</span><span class="sxs-lookup"><span data-stu-id="72d94-189">_b</span></span> |
| <span data-ttu-id="72d94-190">Çift</span><span class="sxs-lookup"><span data-stu-id="72d94-190">Double</span></span> |<span data-ttu-id="72d94-191">_D</span><span class="sxs-lookup"><span data-stu-id="72d94-191">_d</span></span> |
| <span data-ttu-id="72d94-192">Tarih/saat</span><span class="sxs-lookup"><span data-stu-id="72d94-192">Date/time</span></span> |<span data-ttu-id="72d94-193">_T</span><span class="sxs-lookup"><span data-stu-id="72d94-193">_t</span></span> |
| <span data-ttu-id="72d94-194">GUID</span><span class="sxs-lookup"><span data-stu-id="72d94-194">GUID</span></span> |<span data-ttu-id="72d94-195">_g</span><span class="sxs-lookup"><span data-stu-id="72d94-195">_g</span></span> |

<span data-ttu-id="72d94-196">Merhaba kayıt türü hello yeni kayıt için zaten var olup üzerinde her özelliği için günlük analizi kullanan hello veri türüne bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="72d94-196">hello data type that Log Analytics uses for each property depends on whether hello record type for hello new record already exists.</span></span>

* <span data-ttu-id="72d94-197">Günlük analizi Hello kayıt türü mevcut değilse yeni bir tane oluşturur.</span><span class="sxs-lookup"><span data-stu-id="72d94-197">If hello record type does not exist, Log Analytics creates a new one.</span></span> <span data-ttu-id="72d94-198">Günlük analizi hello JSON türü çıkarımı toodetermine hello veri türü hello yeni kayıt için her bir özellik için kullanır.</span><span class="sxs-lookup"><span data-stu-id="72d94-198">Log Analytics uses hello JSON type inference toodetermine hello data type for each property for hello new record.</span></span>
* <span data-ttu-id="72d94-199">Merhaba kayıt türü mevcut değilse, günlük analizi toocreate varolan özelliğe göre yeni bir kayıt çalışır.</span><span class="sxs-lookup"><span data-stu-id="72d94-199">If hello record type does exist, Log Analytics attempts toocreate a new record based on existing properties.</span></span> <span data-ttu-id="72d94-200">Merhaba hello yeni kayıttaki bir özellik için veri türü değil eşleşen ve olamaz dönüştürülmüş toohello türü mevcut olması veya hello kaydı varolmayan bir özellik içerir, günlük analizi yeni bir özellik oluşturur, hello ilgili soneki olmaz.</span><span class="sxs-lookup"><span data-stu-id="72d94-200">If hello data type for a property in hello new record doesn’t match and can’t be converted toohello existing type, or if hello record includes a property that doesn’t exist, Log Analytics creates a new property that has hello relevant suffix.</span></span>

<span data-ttu-id="72d94-201">Örneğin, bir kayıt üç özellik ile bu gönderimi giriş oluşturursunuz **number_d**, **boolean_b**, ve **string_s**:</span><span class="sxs-lookup"><span data-stu-id="72d94-201">For example, this submission entry would create a record with three properties, **number_d**, **boolean_b**, and **string_s**:</span></span>

![Kayıt örneği 1](media/log-analytics-data-collector-api/record-01.png)

<span data-ttu-id="72d94-203">Ardından tüm değerleri dize olarak biçimlendirilmiş bu sonraki giriş gönderdiyseniz hello özellikleri değişmediği.</span><span class="sxs-lookup"><span data-stu-id="72d94-203">If you then submitted this next entry, with all values formatted as strings, hello properties would not change.</span></span> <span data-ttu-id="72d94-204">Bu değerler dönüştürülmüş tooexisting veri türleri olabilir:</span><span class="sxs-lookup"><span data-stu-id="72d94-204">These values can be converted tooexisting data types:</span></span>

![Örnek kaydı 2](media/log-analytics-data-collector-api/record-02.png)

<span data-ttu-id="72d94-206">Ancak, daha sonra bu sonraki gönderme yaptıysanız, günlük analizi yeni özellikleri hello oluşturacak **boolean_d** ve **string_d**.</span><span class="sxs-lookup"><span data-stu-id="72d94-206">But, if you then made this next submission, Log Analytics would create hello new properties **boolean_d** and **string_d**.</span></span> <span data-ttu-id="72d94-207">Bu değerleri dönüştürülemiyor:</span><span class="sxs-lookup"><span data-stu-id="72d94-207">These values can't be converted:</span></span>

![Örnek kayıt 3](media/log-analytics-data-collector-api/record-03.png)

<span data-ttu-id="72d94-209">Ardından hello kayıt türü oluşturulmadan önce girişi, aşağıdaki hello gönderdiyseniz, günlük analizi üç özellik ile bir kayıt oluşturacak **başarı sayısı**, **boolean_s**, ve **string_s**.</span><span class="sxs-lookup"><span data-stu-id="72d94-209">If you then submitted hello following entry, before hello record type was created, Log Analytics would create a record with three properties, **number_s**, **boolean_s**, and **string_s**.</span></span> <span data-ttu-id="72d94-210">Bu girdiye hello ilk değerlerin her birini bir dize olarak biçimlendirilmiş:</span><span class="sxs-lookup"><span data-stu-id="72d94-210">In this entry, each of hello initial values is formatted as a string:</span></span>

![Örnek kayıt 4](media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a><span data-ttu-id="72d94-212">Veri sınırları</span><span class="sxs-lookup"><span data-stu-id="72d94-212">Data limits</span></span>
<span data-ttu-id="72d94-213">Merhaba veri toohello Log Analytics verisi toplama API gönderilen geçici bazı kısıtlamalar vardır.</span><span class="sxs-lookup"><span data-stu-id="72d94-213">There are some constraints around hello data posted toohello Log Analytics Data collection API.</span></span>

* <span data-ttu-id="72d94-214">Post tooLog Analytics Veri Toplayıcı API başına en fazla 30 MB.</span><span class="sxs-lookup"><span data-stu-id="72d94-214">Maximum of 30 MB per post tooLog Analytics Data Collector API.</span></span> <span data-ttu-id="72d94-215">Tek bir posta için boyut sınırı budur.</span><span class="sxs-lookup"><span data-stu-id="72d94-215">This is a size limit for a single post.</span></span> <span data-ttu-id="72d94-216">30 MB aşıyor tek bir post verilerden Merhaba, toosmaller boyuta sahip verileri öbekleri ve eş zamanlı gönderme hello bölme durumunda.</span><span class="sxs-lookup"><span data-stu-id="72d94-216">If hello data from a single post that exceeds 30 MB, you should split hello data up toosmaller sized chunks and send them concurrently.</span></span>
* <span data-ttu-id="72d94-217">En fazla 32 KB sınırını alan değerleri için.</span><span class="sxs-lookup"><span data-stu-id="72d94-217">Maximum of 32 KB limit for field values.</span></span> <span data-ttu-id="72d94-218">Merhaba alan değeri 32 KB'den büyükse hello verileri kesilecek.</span><span class="sxs-lookup"><span data-stu-id="72d94-218">If hello field value is greater than 32 KB, hello data will be truncated.</span></span>
* <span data-ttu-id="72d94-219">Önerilen alanı sayısı için belirli bir türde 50'dir.</span><span class="sxs-lookup"><span data-stu-id="72d94-219">Recommended maximum number of fields for a given type is 50.</span></span> <span data-ttu-id="72d94-220">Kullanılabilirlik ve arama deneyimi perspektifinden pratik sınır budur.</span><span class="sxs-lookup"><span data-stu-id="72d94-220">This is a practical limit from a usability and search experience perspective.</span></span>  

## <a name="return-codes"></a><span data-ttu-id="72d94-221">Dönüş kodları</span><span class="sxs-lookup"><span data-stu-id="72d94-221">Return codes</span></span>
<span data-ttu-id="72d94-222">HTTP durum kodu 200 Hello bu hello istek işleme için alınan anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="72d94-222">hello HTTP status code 200 means that hello request has been received for processing.</span></span> <span data-ttu-id="72d94-223">Bu, o hello işlemi başarıyla tamamlandı gösterir.</span><span class="sxs-lookup"><span data-stu-id="72d94-223">This indicates that hello operation completed successfully.</span></span>

<span data-ttu-id="72d94-224">Bu tabloda hello eksiksiz hello hizmet döndürebilir durum kodları listelenmektedir:</span><span class="sxs-lookup"><span data-stu-id="72d94-224">This table lists hello complete set of status codes that hello service might return:</span></span>

| <span data-ttu-id="72d94-225">Kod</span><span class="sxs-lookup"><span data-stu-id="72d94-225">Code</span></span> | <span data-ttu-id="72d94-226">Durum</span><span class="sxs-lookup"><span data-stu-id="72d94-226">Status</span></span> | <span data-ttu-id="72d94-227">Hata kodu</span><span class="sxs-lookup"><span data-stu-id="72d94-227">Error code</span></span> | <span data-ttu-id="72d94-228">Açıklama</span><span class="sxs-lookup"><span data-stu-id="72d94-228">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="72d94-229">200</span><span class="sxs-lookup"><span data-stu-id="72d94-229">200</span></span> |<span data-ttu-id="72d94-230">TAMAM</span><span class="sxs-lookup"><span data-stu-id="72d94-230">OK</span></span> | |<span data-ttu-id="72d94-231">Merhaba isteği başarıyla kabul edildi.</span><span class="sxs-lookup"><span data-stu-id="72d94-231">hello request was successfully accepted.</span></span> |
| <span data-ttu-id="72d94-232">400</span><span class="sxs-lookup"><span data-stu-id="72d94-232">400</span></span> |<span data-ttu-id="72d94-233">Hatalı istek</span><span class="sxs-lookup"><span data-stu-id="72d94-233">Bad request</span></span> |<span data-ttu-id="72d94-234">InactiveCustomer</span><span class="sxs-lookup"><span data-stu-id="72d94-234">InactiveCustomer</span></span> |<span data-ttu-id="72d94-235">Merhaba çalışma kapatıldı.</span><span class="sxs-lookup"><span data-stu-id="72d94-235">hello workspace has been closed.</span></span> |
| <span data-ttu-id="72d94-236">400</span><span class="sxs-lookup"><span data-stu-id="72d94-236">400</span></span> |<span data-ttu-id="72d94-237">Hatalı istek</span><span class="sxs-lookup"><span data-stu-id="72d94-237">Bad request</span></span> |<span data-ttu-id="72d94-238">InvalidApiVersion</span><span class="sxs-lookup"><span data-stu-id="72d94-238">InvalidApiVersion</span></span> |<span data-ttu-id="72d94-239">Belirttiğiniz hello API sürümü hello hizmeti tarafından tanınmadı.</span><span class="sxs-lookup"><span data-stu-id="72d94-239">hello API version that you specified was not recognized by hello service.</span></span> |
| <span data-ttu-id="72d94-240">400</span><span class="sxs-lookup"><span data-stu-id="72d94-240">400</span></span> |<span data-ttu-id="72d94-241">Hatalı istek</span><span class="sxs-lookup"><span data-stu-id="72d94-241">Bad request</span></span> |<span data-ttu-id="72d94-242">InvalidCustomerId</span><span class="sxs-lookup"><span data-stu-id="72d94-242">InvalidCustomerId</span></span> |<span data-ttu-id="72d94-243">Belirtilen hello çalışma alanı kimliği geçersiz.</span><span class="sxs-lookup"><span data-stu-id="72d94-243">hello workspace ID specified is invalid.</span></span> |
| <span data-ttu-id="72d94-244">400</span><span class="sxs-lookup"><span data-stu-id="72d94-244">400</span></span> |<span data-ttu-id="72d94-245">Hatalı istek</span><span class="sxs-lookup"><span data-stu-id="72d94-245">Bad request</span></span> |<span data-ttu-id="72d94-246">InvalidDataFormat</span><span class="sxs-lookup"><span data-stu-id="72d94-246">InvalidDataFormat</span></span> |<span data-ttu-id="72d94-247">Geçersiz JSON gönderildi.</span><span class="sxs-lookup"><span data-stu-id="72d94-247">Invalid JSON was submitted.</span></span> <span data-ttu-id="72d94-248">Merhaba yanıt gövdesi nasıl tooresolve hello hata hakkında daha fazla bilgi içerebilir.</span><span class="sxs-lookup"><span data-stu-id="72d94-248">hello response body might contain more information about how tooresolve hello error.</span></span> |
| <span data-ttu-id="72d94-249">400</span><span class="sxs-lookup"><span data-stu-id="72d94-249">400</span></span> |<span data-ttu-id="72d94-250">Hatalı istek</span><span class="sxs-lookup"><span data-stu-id="72d94-250">Bad request</span></span> |<span data-ttu-id="72d94-251">InvalidLogType</span><span class="sxs-lookup"><span data-stu-id="72d94-251">InvalidLogType</span></span> |<span data-ttu-id="72d94-252">Kapsanan özel karakter veya sayı belirtilen Hello günlük türü.</span><span class="sxs-lookup"><span data-stu-id="72d94-252">hello log type specified contained special characters or numerics.</span></span> |
| <span data-ttu-id="72d94-253">400</span><span class="sxs-lookup"><span data-stu-id="72d94-253">400</span></span> |<span data-ttu-id="72d94-254">Hatalı istek</span><span class="sxs-lookup"><span data-stu-id="72d94-254">Bad request</span></span> |<span data-ttu-id="72d94-255">MissingApiVersion</span><span class="sxs-lookup"><span data-stu-id="72d94-255">MissingApiVersion</span></span> |<span data-ttu-id="72d94-256">Merhaba API sürümü belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="72d94-256">hello API version wasn’t specified.</span></span> |
| <span data-ttu-id="72d94-257">400</span><span class="sxs-lookup"><span data-stu-id="72d94-257">400</span></span> |<span data-ttu-id="72d94-258">Hatalı istek</span><span class="sxs-lookup"><span data-stu-id="72d94-258">Bad request</span></span> |<span data-ttu-id="72d94-259">MissingContentType</span><span class="sxs-lookup"><span data-stu-id="72d94-259">MissingContentType</span></span> |<span data-ttu-id="72d94-260">Merhaba içerik türü belirtilmedi.</span><span class="sxs-lookup"><span data-stu-id="72d94-260">hello content type wasn’t specified.</span></span> |
| <span data-ttu-id="72d94-261">400</span><span class="sxs-lookup"><span data-stu-id="72d94-261">400</span></span> |<span data-ttu-id="72d94-262">Hatalı istek</span><span class="sxs-lookup"><span data-stu-id="72d94-262">Bad request</span></span> |<span data-ttu-id="72d94-263">MissingLogType</span><span class="sxs-lookup"><span data-stu-id="72d94-263">MissingLogType</span></span> |<span data-ttu-id="72d94-264">Merhaba, değer günlük türü belirtilmedi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="72d94-264">hello required value log type wasn’t specified.</span></span> |
| <span data-ttu-id="72d94-265">400</span><span class="sxs-lookup"><span data-stu-id="72d94-265">400</span></span> |<span data-ttu-id="72d94-266">Hatalı istek</span><span class="sxs-lookup"><span data-stu-id="72d94-266">Bad request</span></span> |<span data-ttu-id="72d94-267">UnsupportedContentType</span><span class="sxs-lookup"><span data-stu-id="72d94-267">UnsupportedContentType</span></span> |<span data-ttu-id="72d94-268">Merhaba içerik türü çok ayarlanmamış**uygulama/json**.</span><span class="sxs-lookup"><span data-stu-id="72d94-268">hello content type was not set too**application/json**.</span></span> |
| <span data-ttu-id="72d94-269">403</span><span class="sxs-lookup"><span data-stu-id="72d94-269">403</span></span> |<span data-ttu-id="72d94-270">Yasak</span><span class="sxs-lookup"><span data-stu-id="72d94-270">Forbidden</span></span> |<span data-ttu-id="72d94-271">InvalidAuthorization</span><span class="sxs-lookup"><span data-stu-id="72d94-271">InvalidAuthorization</span></span> |<span data-ttu-id="72d94-272">Merhaba hizmet tooauthenticate hello isteği başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="72d94-272">hello service failed tooauthenticate hello request.</span></span> <span data-ttu-id="72d94-273">Bu hello çalışma alanı kimliği ve bağlantı anahtarı geçerli olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="72d94-273">Verify that hello workspace ID and connection key are valid.</span></span> |
| <span data-ttu-id="72d94-274">404</span><span class="sxs-lookup"><span data-stu-id="72d94-274">404</span></span> |<span data-ttu-id="72d94-275">Bulunamadı</span><span class="sxs-lookup"><span data-stu-id="72d94-275">Not Found</span></span> | | <span data-ttu-id="72d94-276">Sağlanan hello URL yanlış ya da hello isteği çok büyük.</span><span class="sxs-lookup"><span data-stu-id="72d94-276">Either hello URL provided is incorrect, or hello request is too large.</span></span> |
| <span data-ttu-id="72d94-277">429</span><span class="sxs-lookup"><span data-stu-id="72d94-277">429</span></span> |<span data-ttu-id="72d94-278">Çok fazla istek</span><span class="sxs-lookup"><span data-stu-id="72d94-278">Too Many Requests</span></span> | | <span data-ttu-id="72d94-279">Merhaba hizmet hesabınızdan veri hacmi yüksek yaşıyor.</span><span class="sxs-lookup"><span data-stu-id="72d94-279">hello service is experiencing a high volume of data from your account.</span></span> <span data-ttu-id="72d94-280">Lütfen hello isteği daha sonra yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="72d94-280">Please retry hello request later.</span></span> |
| <span data-ttu-id="72d94-281">500</span><span class="sxs-lookup"><span data-stu-id="72d94-281">500</span></span> |<span data-ttu-id="72d94-282">İç sunucu hatası</span><span class="sxs-lookup"><span data-stu-id="72d94-282">Internal Server Error</span></span> |<span data-ttu-id="72d94-283">UnspecifiedError</span><span class="sxs-lookup"><span data-stu-id="72d94-283">UnspecifiedError</span></span> |<span data-ttu-id="72d94-284">Merhaba hizmeti bir iç hatayla karşılaştı.</span><span class="sxs-lookup"><span data-stu-id="72d94-284">hello service encountered an internal error.</span></span> <span data-ttu-id="72d94-285">Lütfen hello isteği yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="72d94-285">Please retry hello request.</span></span> |
| <span data-ttu-id="72d94-286">503</span><span class="sxs-lookup"><span data-stu-id="72d94-286">503</span></span> |<span data-ttu-id="72d94-287">Hizmet kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="72d94-287">Service Unavailable</span></span> |<span data-ttu-id="72d94-288">ServiceUnavailable</span><span class="sxs-lookup"><span data-stu-id="72d94-288">ServiceUnavailable</span></span> |<span data-ttu-id="72d94-289">Merhaba Hizmet şu anda kullanılamıyor tooreceive isteği sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="72d94-289">hello service currently is unavailable tooreceive requests.</span></span> <span data-ttu-id="72d94-290">Lütfen isteğinizi yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="72d94-290">Please retry your request.</span></span> |

## <a name="query-data"></a><span data-ttu-id="72d94-291">Verileri sorgulama</span><span class="sxs-lookup"><span data-stu-id="72d94-291">Query data</span></span>
<span data-ttu-id="72d94-292">Merhaba günlük analizi HTTP veri toplayıcı API, arama ile kayıt tarafından gönderilen tooquery veri **türü** diğer bir deyişle eşit toohello **LogType** , belirttiğiniz değer eklenmiş olan **_CL**.</span><span class="sxs-lookup"><span data-stu-id="72d94-292">tooquery data submitted by hello Log Analytics HTTP Data Collector API, search for records with **Type** that is equal toohello **LogType** value that you specified, appended with **_CL**.</span></span> <span data-ttu-id="72d94-293">Örneğin, kullandığınız **MyCustomLog**, tüm kayıtları döndürecekti sonra **türü MyCustomLog_CL =**.</span><span class="sxs-lookup"><span data-stu-id="72d94-293">For example, if you used **MyCustomLog**, then you'd return all records with **Type=MyCustomLog_CL**.</span></span>

>[!NOTE]
> <span data-ttu-id="72d94-294">Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), sorgu yukarıda hello toohello aşağıdaki değişeceğinden sonra.</span><span class="sxs-lookup"><span data-stu-id="72d94-294">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above query would change toohello following.</span></span>

> `MyCustomLog_CL`

## <a name="sample-requests"></a><span data-ttu-id="72d94-295">Örnek istek</span><span class="sxs-lookup"><span data-stu-id="72d94-295">Sample requests</span></span>
<span data-ttu-id="72d94-296">Merhaba sonraki bölümlerde, nasıl örnekleri bulabilirsiniz toosubmit veri toohello günlük analizi HTTP veri toplayıcı API farklı programlama dillerini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="72d94-296">In hello next sections, you'll find samples of how toosubmit data toohello Log Analytics HTTP Data Collector API by using different programming languages.</span></span>

<span data-ttu-id="72d94-297">Her bir örnek için tooset hello değişkenleri hello authorization üstbilgisi için bu adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="72d94-297">For each sample, do these steps tooset hello variables for hello authorization header:</span></span>

1. <span data-ttu-id="72d94-298">Merhaba Hello Operations Management Suite Portalı'nda seçin **ayarları** döşeme ve hello ardından **bağlı kaynakları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="72d94-298">In hello Operations Management Suite portal, select hello **Settings** tile, and then select hello **Connected Sources** tab.</span></span>
2. <span data-ttu-id="72d94-299">sağ toohello **çalışma alanı kimliği**hello Kopyala simgesini seçin ve hello kimliği hello hello değeri olarak yapıştırın **Müşteri Kimliği** değişkeni.</span><span class="sxs-lookup"><span data-stu-id="72d94-299">toohello right of **Workspace ID**, select hello copy icon, and then paste hello ID as hello value of hello **Customer ID** variable.</span></span>
3. <span data-ttu-id="72d94-300">sağ toohello **birincil anahtar**hello Kopyala simgesini seçin ve hello kimliği hello hello değeri olarak yapıştırın **paylaşılan anahtar** değişkeni.</span><span class="sxs-lookup"><span data-stu-id="72d94-300">toohello right of **Primary Key**, select hello copy icon, and then paste hello ID as hello value of hello **Shared Key** variable.</span></span>

<span data-ttu-id="72d94-301">Alternatif olarak, hello değişkenleri hello günlük türü ve JSON verileri için değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72d94-301">Alternatively, you can change hello variables for hello log type and JSON data.</span></span>

### <a name="powershell-sample"></a><span data-ttu-id="72d94-302">PowerShell örnek</span><span class="sxs-lookup"><span data-stu-id="72d94-302">PowerShell sample</span></span>
```
# Replace with your Workspace ID
$CustomerId = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"  

# Replace with your Primary Key
$SharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# Specify hello name of hello record type that you'll be creating
$LogType = "MyRecordType"

# Specify a field with hello created time for hello records
$TimeStampField = "DateValue"


# Create two records with hello same set of properties toocreate
$json = @"
[{  "StringValue": "MyString1",
    "NumberValue": 42,
    "BooleanValue": true,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "9909ED01-A74C-4874-8ABF-D2678E3AE23D"
},
{   "StringValue": "MyString2",
    "NumberValue": 43,
    "BooleanValue": false,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "8809ED01-A74C-4874-8ABF-D2678E3AE23D"
}]
"@

# Create hello function toocreate hello authorization signature
Function Build-Signature ($customerId, $sharedKey, $date, $contentLength, $method, $contentType, $resource)
{
    $xHeaders = "x-ms-date:" + $date
    $stringToHash = $method + "`n" + $contentLength + "`n" + $contentType + "`n" + $xHeaders + "`n" + $resource

    $bytesToHash = [Text.Encoding]::UTF8.GetBytes($stringToHash)
    $keyBytes = [Convert]::FromBase64String($sharedKey)

    $sha256 = New-Object System.Security.Cryptography.HMACSHA256
    $sha256.Key = $keyBytes
    $calculatedHash = $sha256.ComputeHash($bytesToHash)
    $encodedHash = [Convert]::ToBase64String($calculatedHash)
    $authorization = 'SharedKey {0}:{1}' -f $customerId,$encodedHash
    return $authorization
}


# Create hello function toocreate and post hello request
Function Post-OMSData($customerId, $sharedKey, $body, $logType)
{
    $method = "POST"
    $contentType = "application/json"
    $resource = "/api/logs"
    $rfc1123date = [DateTime]::UtcNow.ToString("r")
    $contentLength = $body.Length
    $signature = Build-Signature `
        -customerId $customerId `
        -sharedKey $sharedKey `
        -date $rfc1123date `
        -contentLength $contentLength `
        -fileName $fileName `
        -method $method `
        -contentType $contentType `
        -resource $resource
    $uri = "https://" + $customerId + ".ods.opinsights.azure.com" + $resource + "?api-version=2016-04-01"

    $headers = @{
        "Authorization" = $signature;
        "Log-Type" = $logType;
        "x-ms-date" = $rfc1123date;
        "time-generated-field" = $TimeStampField;
    }

    $response = Invoke-WebRequest -Uri $uri -Method $method -ContentType $contentType -Headers $headers -Body $body -UseBasicParsing
    return $response.StatusCode

}

# Submit hello data toohello API endpoint
Post-OMSData -customerId $customerId -sharedKey $sharedKey -body ([System.Text.Encoding]::UTF8.GetBytes($json)) -logType $logType  
```

### <a name="c-sample"></a><span data-ttu-id="72d94-303">C# örneği</span><span class="sxs-lookup"><span data-stu-id="72d94-303">C# sample</span></span>
```
using System;
using System.Net;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Security.Cryptography;
using System.Text;
using System.Threading.Tasks;

namespace OIAPIExample
{
    class ApiExample
    {
        // An example JSON object, with key/value pairs
        static string json = @"[{""DemoField1"":""DemoValue1"",""DemoField2"":""DemoValue2""},{""DemoField3"":""DemoValue3"",""DemoField4"":""DemoValue4""}]";

        // Update customerId tooyour Operations Management Suite workspace ID
        static string customerId = "xxxxxxxx-xxx-xxx-xxx-xxxxxxxxxxxx";

        // For sharedKey, use either hello primary or hello secondary Connected Sources client authentication key   
        static string sharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";

        // LogName is name of hello event type that is being submitted tooLog Analytics
        static string LogName = "DemoExample";

        // You can use an optional field toospecify hello timestamp from hello data. If hello time field is not specified, Log Analytics assumes hello time is hello message ingestion time
        static string TimeStampField = "";

        static void Main()
        {
            // Create a hash for hello API signature
            var datestring = DateTime.UtcNow.ToString("r");
            string stringToHash = "POST\n" + json.Length + "\napplication/json\n" + "x-ms-date:" + datestring + "\n/api/logs";
            string hashedString = BuildSignature(stringToHash, sharedKey);
            string signature = "SharedKey " + customerId + ":" + hashedString;

            PostData(signature, datestring, json);
        }

        // Build hello API signature
        public static string BuildSignature(string message, string secret)
        {
            var encoding = new System.Text.ASCIIEncoding();
            byte[] keyByte = Convert.FromBase64String(secret);
            byte[] messageBytes = encoding.GetBytes(message);
            using (var hmacsha256 = new HMACSHA256(keyByte))
            {
                byte[] hash = hmacsha256.ComputeHash(messageBytes);
                return Convert.ToBase64String(hash);
            }
        }

        // Send a request toohello POST API endpoint
        public static void PostData(string signature, string date, string json)
        {
            try
            {
                string url = "https://" + customerId + ".ods.opinsights.azure.com/api/logs?api-version=2016-04-01";

                System.Net.Http.HttpClient client = new System.Net.Http.HttpClient();
                client.DefaultRequestHeaders.Add("Accept", "application/json");
                client.DefaultRequestHeaders.Add("Log-Type", LogName);
                client.DefaultRequestHeaders.Add("Authorization", signature);
                client.DefaultRequestHeaders.Add("x-ms-date", date);
                client.DefaultRequestHeaders.Add("time-generated-field", TimeStampField);

                System.Net.Http.HttpContent httpContent = new StringContent(json, Encoding.UTF8);
                httpContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");
                Task<System.Net.Http.HttpResponseMessage> response = client.PostAsync(new Uri(url), httpContent);

                System.Net.Http.HttpContent responseContent = response.Result.Content;
                string result = responseContent.ReadAsStringAsync().Result;
                Console.WriteLine("Return Result: " + result);
            }
            catch (Exception excep)
            {
                Console.WriteLine("API Post Exception: " + excep.Message);
            }
        }
    }
}

```

### <a name="python-sample"></a><span data-ttu-id="72d94-304">Python örneği</span><span class="sxs-lookup"><span data-stu-id="72d94-304">Python sample</span></span>
```
import json
import requests
import datetime
import hashlib
import hmac
import base64

# Update hello customer ID tooyour Operations Management Suite workspace ID
customer_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

# For hello shared key, use either hello primary or hello secondary Connected Sources client authentication key   
shared_key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# hello log type is hello name of hello event that is being submitted
log_type = 'WebMonitorTest'

# An example JSON web monitor object
json_data = [{
   "slot_ID": 12345,
    "ID": "5cdad72f-c848-4df0-8aaa-ffe033e75d57",
    "availability_Value": 100,
    "performance_Value": 6.954,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "true"
},
{   
    "slot_ID": 67890,
    "ID": "b6bee458-fb65-492e-996d-61c4d7fbb942",
    "availability_Value": 100,
    "performance_Value": 3.379,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "false"
}]
body = json.dumps(json_data)

#####################
######Functions######  
#####################

# Build hello API signature
def build_signature(customer_id, shared_key, date, content_length, method, content_type, resource):
    x_headers = 'x-ms-date:' + date
    string_to_hash = method + "\n" + str(content_length) + "\n" + content_type + "\n" + x_headers + "\n" + resource
    bytes_to_hash = bytes(string_to_hash).encode('utf-8')  
    decoded_key = base64.b64decode(shared_key)
    encoded_hash = base64.b64encode(hmac.new(decoded_key, bytes_to_hash, digestmod=hashlib.sha256).digest())
    authorization = "SharedKey {}:{}".format(customer_id,encoded_hash)
    return authorization

# Build and send a request toohello POST API
def post_data(customer_id, shared_key, body, log_type):
    method = 'POST'
    content_type = 'application/json'
    resource = '/api/logs'
    rfc1123date = datetime.datetime.utcnow().strftime('%a, %d %b %Y %H:%M:%S GMT')
    content_length = len(body)
    signature = build_signature(customer_id, shared_key, rfc1123date, content_length, method, content_type, resource)
    uri = 'https://' + customer_id + '.ods.opinsights.azure.com' + resource + '?api-version=2016-04-01'

    headers = {
        'content-type': content_type,
        'Authorization': signature,
        'Log-Type': log_type,
        'x-ms-date': rfc1123date
    }

    response = requests.post(uri,data=body, headers=headers)
    if (response.status_code >= 200 and response.status_code <= 299):
        print 'Accepted'
    else:
        print "Response code: {}".format(response.status_code)

post_data(customer_id, shared_key, body, log_type)
```

## <a name="next-steps"></a><span data-ttu-id="72d94-305">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="72d94-305">Next steps</span></span>
- <span data-ttu-id="72d94-306">Kullanım hello [günlük arama API](log-analytics-log-search-api.md) hello günlük analizi depodan tooretrieve veri.</span><span class="sxs-lookup"><span data-stu-id="72d94-306">Use hello [Log Search API](log-analytics-log-search-api.md) tooretrieve data from hello Log Analytics repository.</span></span>
