---
title: "Azure API Management'te bir API'ye işlem ekleme | Microsoft Docs"
description: "Azure API Management'te bir API işlemleri eklemeyi öğrenin."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 1158a023-1913-4e9c-93de-9164b672f9b3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 105fc51c2d1152a40a5757985da47330e0b7b8cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-add-operations-to-an-api-in-azure-api-management"></a><span data-ttu-id="a425d-103">Azure API Management'te bir API'ye işlem ekleme</span><span class="sxs-lookup"><span data-stu-id="a425d-103">How to add operations to an API in Azure API Management</span></span>
<span data-ttu-id="a425d-104">Bir API API Management kullanmadan önce operations eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="a425d-104">Before an API in API Management can be used, operations must be added.</span></span> <span data-ttu-id="a425d-105">Bu kılavuz, ekleme ve farklı bir API işlemlerinin API Management'te yapılandırma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a425d-105">This guide shows how to add and configure different types of operations to an API in API Management.</span></span>

## <span data-ttu-id="a425d-106"><a name="add-operation"></a>Bir işlem ekleme</span><span class="sxs-lookup"><span data-stu-id="a425d-106"><a name="add-operation"> </a>Add an operation</span></span>
<span data-ttu-id="a425d-107">Operations eklenir ve bir API yayımcı portalında yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="a425d-107">Operations are added and configured to an API in the publisher portal.</span></span> <span data-ttu-id="a425d-108">Yayımcı portalına erişmek için tıklatın **yayımcı portalına** API Management hizmetiniz için Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="a425d-108">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Yayımcı portalı][api-management-management-console]

> <span data-ttu-id="a425d-110">Henüz bir API Management hizmeti örneği oluşturmadıysanız, [Azure API Management'i kullanmaya başlama][Get started with Azure API Management] öğreticisinde [API Management hizmet örneği oluşturma][Create an API Management service instance]'ya bakın.</span><span class="sxs-lookup"><span data-stu-id="a425d-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="a425d-111">İstenen API yayımcı Portalı'nda seçin ve ardından **Operations** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="a425d-111">Select the desired API in the publisher portal and then select the **Operations** tab.</span></span> 

![İşlemler][api-management-operations]

<span data-ttu-id="a425d-113">Tıklatın **ekleme işlemi** yeni bir işlem eklemek için.</span><span class="sxs-lookup"><span data-stu-id="a425d-113">Click **Add Operation** to add a new operation.</span></span> <span data-ttu-id="a425d-114">**Yeni işlem** görüntülenir ve **imza** sekmesi varsayılan olarak seçilir.</span><span class="sxs-lookup"><span data-stu-id="a425d-114">The **New operation** will be displayed and the **Signature** tab will be selected by default.</span></span>

![Ekleme işlemi][api-management-add-operation]

<span data-ttu-id="a425d-116">Belirtin **HTTP fiili** aşağı açılan listeden seçerek.</span><span class="sxs-lookup"><span data-stu-id="a425d-116">Specify the **HTTP verb** by choosing from the drop-down list.</span></span>

![HTTP yöntemi][api-management-http-method]

<a name="url-template"></a>

<span data-ttu-id="a425d-118">URL şablonu, bir veya daha fazla URL yolu kesimleri ve sıfır veya daha fazla sorgu dizesi parametreleri oluşan bir URL parçadaki yazarak tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="a425d-118">Define the URL template by typing in a URL fragment consisting of one or more URL path segments and zero or more query string parameters.</span></span> <span data-ttu-id="a425d-119">API temel URL'sini eklenmiş URL şablon, tek bir HTTP işlemi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a425d-119">The URL template, appended to the base URL of the API, identifies a single HTTP operation.</span></span> <span data-ttu-id="a425d-120">Daha fazla küme ayraçları tanımlanan değişken bölümleri adlı veya birini içerebilir.</span><span class="sxs-lookup"><span data-stu-id="a425d-120">It may contain one or more named variable parts that are identified by curly braces.</span></span> <span data-ttu-id="a425d-121">Bu değişken bölümleri şablon parametreleri olarak adlandırılır ve istek API Yönetimi platformunuz tarafından işlendiğinde isteğin URL'den ayıklanan değerler dinamik olarak atanır.</span><span class="sxs-lookup"><span data-stu-id="a425d-121">These variable parts are called template parameters and are dynamically assigned values extracted from the request's URL when the request is being processed by the API Management platform.</span></span>

> <span data-ttu-id="a425d-122">URL şablon joker karakter düzenleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="a425d-122">The URL template can include wildcard patterns.</span></span> <span data-ttu-id="a425d-123">Örneğin, belirten `/*` geri, HTTP yöntemine yönelik tüm istekleri hizmet İleri sona erer.</span><span class="sxs-lookup"><span data-stu-id="a425d-123">For example, specifying `/*` will forward all requests for that HTTP method to the back end service.</span></span>

![URL şablonu][api-management-url-template]

<a name="rewrite-url-template"></a>

<span data-ttu-id="a425d-125">İsterseniz, belirtin **URL yeniden yazma şablon**.</span><span class="sxs-lookup"><span data-stu-id="a425d-125">If desired, specify the **Rewrite URL template**.</span></span> <span data-ttu-id="a425d-126">Bu, dönüştürülmüş bir URL yeniden yazma şablon göre aracılığıyla arka uç çağrılırken ön uç üzerinde gelen istekleri işlemek için standart URL şablonu kullanmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="a425d-126">This allows you to use the standard URL template for processing incoming requests on the front-end, while calling the back-end via a converted URL according to the rewrite template.</span></span> <span data-ttu-id="a425d-127">Şablon parametreleri URL şablondan yeniden yazma şablonunda kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a425d-127">Template parameters from the URL template should be used in the rewrite template.</span></span> <span data-ttu-id="a425d-128">Aşağıdaki örnek, önceki örnekten web hizmeti yol kesimi, URL şablonları kullanarak API Management platform yayımlanan API bir sorgu parametresi olarak sağlanabilir olarak kodlanmış nasıl içerik türünü gösterir.</span><span class="sxs-lookup"><span data-stu-id="a425d-128">The following example shows how content type encoded as path segment in the web service from the previous example can be provided as a query parameter in the API published via the API Management platform using the URL templates.</span></span>

![URL şablonu yeniden yazma][api-management-url-template-rewrite]

<span data-ttu-id="a425d-130">İşlemi arayanlara biçimini kullanacak `/customers?customerid=ALFKI` ve bu öğesine eşlenecek `/Customers('ALFKI')` arka uç hizmetine zaman çağrılır.</span><span class="sxs-lookup"><span data-stu-id="a425d-130">Callers to the operation will use the format `/customers?customerid=ALFKI` and this will be mapped to `/Customers('ALFKI')` when the back-end service is invoked.</span></span>

<span data-ttu-id="a425d-131">**Görüntü** adı ve **açıklama** işlemi bir açıklama belirtin ve Geliştirici Portalı'nda bu API kullanan geliştiriciler için belgeleri sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a425d-131">**Display** name and **Description** provide a description of the operation and are used to provide documentation to the developers using this API in the developer portal.</span></span>

![Açıklama][api-management-description]

<span data-ttu-id="a425d-133">Düz metin veya HTML olarak işlemi açıklama belirtilen **açıklama** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="a425d-133">The operation description can be specified as plain text or HTML in the **Description** text box.</span></span>

## <span data-ttu-id="a425d-134"><a name="operation-caching"></a>İşlemi önbelleğe alma</span><span class="sxs-lookup"><span data-stu-id="a425d-134"><a name="operation-caching"> </a>Operation caching</span></span>
<span data-ttu-id="a425d-135">Yanıt önbelleğe alma API Tüketiciler, düşürmeye bant genişliği kullanımını ve HTTP web üzerindeki yükü hizmet API uygulama düşüşleri tarafından algılanan gecikmesini azaltır.</span><span class="sxs-lookup"><span data-stu-id="a425d-135">Response caching reduces latency perceived by the API consumers, lowers bandwidth consumption and decreases the load on the HTTP web service implementing the API.</span></span> 

<span data-ttu-id="a425d-136">Hızla ve kolayca işlem için önbelleğe almayı etkinleştirmek için seçin **önbelleğe alma** sekmesinde ve denetleme **etkinleştirmek** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="a425d-136">To easily and quickly enable caching for the operation, select the **Caching** tab and check the **Enable** checkbox.</span></span>

![Önbelleğe alma][api-management-caching-tab]

<span data-ttu-id="a425d-138">**Süre** işlemi yanıt sırasında önbellekte kalan süreyi belirtir.</span><span class="sxs-lookup"><span data-stu-id="a425d-138">**Duration** specifies the time period during which the operation response remains in the cache.</span></span> <span data-ttu-id="a425d-139">Varsayılan değer 3600 saniye veya 1 saat olur.</span><span class="sxs-lookup"><span data-stu-id="a425d-139">The default value is 3600 seconds or 1 hour.</span></span>

<span data-ttu-id="a425d-140">Önbellek anahtarlar, böylece her farklı önbellek anahtarına karşılık gelen yanıt kendi ayrı önbelleğe alınan değeri alır yanıtlar arasında ayırt etmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a425d-140">Cache keys are used to differentiate between responses so that the response corresponding to each different cache key will get its own separate cached value.</span></span> <span data-ttu-id="a425d-141">İsteğe bağlı olarak, özel bir sorgu dizesi parametreleri ve/veya önbellek anahtar değerlerini bilgisayar kullanılacak HTTP üstbilgileri girin **sorgu dizesi parametrelerine göre değişiklik gösterebilir** ve **üstbilgileri göre değişiklik gösterebilir** metin kutuları sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="a425d-141">Optionally, enter specific query string parameters and/or HTTP headers to be used in computing cache key values in the **Vary by query string parameters** and **Vary by headers** text boxes respectively.</span></span> <span data-ttu-id="a425d-142">Ne zaman belirtilen, tam istek URL'si yok ve önbellek anahtar oluşturma aşağıdaki HTTP üst bilgisi değerler kullanılır: **kabul** ve **Accept-Charset**.</span><span class="sxs-lookup"><span data-stu-id="a425d-142">When none are specified, full request URL and the following HTTP header values are used in cache key generation: **Accept** and **Accept-Charset**.</span></span>

> <span data-ttu-id="a425d-143">Önbelleğe alma ve önbelleğe alma ilkeleri hakkında daha fazla bilgi için bkz: [sonuçları işlemi önbelleğe almak nasıl Azure API Management'te][How to cache operation results in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="a425d-143">For more information on caching and caching policies, see [How to cache operation results in Azure API Management][How to cache operation results in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="a425d-144"><a name="request-parameters"></a>Parametreleri</span><span class="sxs-lookup"><span data-stu-id="a425d-144"><a name="request-parameters"> </a>Request parameters</span></span>
<span data-ttu-id="a425d-145">İşlem parametrelerini parametreleri sekmesinde yönetilir.</span><span class="sxs-lookup"><span data-stu-id="a425d-145">Operation parameters are managed on the Parameters tab.</span></span> <span data-ttu-id="a425d-146">Belirtilen parametreleri **URL şablonu** üzerinde **imza** sekmesinde otomatik olarak eklenir ve yalnızca URL şablonu düzenleyerek değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="a425d-146">Parameters specified in the **URL Template** on the **Signature** tab are added automatically and can be changed only by editing the URL template.</span></span> <span data-ttu-id="a425d-147">Ek parametreler el ile girilebilir.</span><span class="sxs-lookup"><span data-stu-id="a425d-147">Additional parameters can be entered manually.</span></span>

<span data-ttu-id="a425d-148">Yeni bir sorgu parametresi eklemek için tıklatın **sorgu parametresi Ekle** ve aşağıdaki bilgileri girin:</span><span class="sxs-lookup"><span data-stu-id="a425d-148">To add a new query parameter, click **Add Query Parameter** and enter the following information:</span></span>

* <span data-ttu-id="a425d-149">**Ad** -parametre adı.</span><span class="sxs-lookup"><span data-stu-id="a425d-149">**Name** - parameter name.</span></span>
* <span data-ttu-id="a425d-150">**Açıklama** -(isteğe bağlı) parametre kısa bir açıklaması.</span><span class="sxs-lookup"><span data-stu-id="a425d-150">**Description** - a brief description of the parameter (optional).</span></span>
* <span data-ttu-id="a425d-151">**Tür** -aşağı açılan seçilen parametre türü.</span><span class="sxs-lookup"><span data-stu-id="a425d-151">**Type** - parameter type, selected in the drop down.</span></span>
* <span data-ttu-id="a425d-152">**Değerleri** -bu parametresine atanan değer.</span><span class="sxs-lookup"><span data-stu-id="a425d-152">**Values** - values that can be assigned to this parameter.</span></span> <span data-ttu-id="a425d-153">Değerlerden biri varsayılan olarak (isteğe bağlı) işaretlenebilir.</span><span class="sxs-lookup"><span data-stu-id="a425d-153">One of the values can be marked as default (optional).</span></span>
* <span data-ttu-id="a425d-154">**Gerekli** -onay kutusunu işaretleyerek parametresi zorunlu kılabilir.</span><span class="sxs-lookup"><span data-stu-id="a425d-154">**Required** - make the parameter mandatory by checking the checkbox.</span></span> 

![İstek parametreleri][api-management-request-parameters]

## <span data-ttu-id="a425d-156"><a name="request-body"></a>İstek gövdesinde</span><span class="sxs-lookup"><span data-stu-id="a425d-156"><a name="request-body"> </a>Request body</span></span>
<span data-ttu-id="a425d-157">İşlem izin veriyorsa (örneğin, PUT, POST) ve tüm desteklenen gösterimi biçimlerinin (örneğin json, XML) içinde örneği sağlayabilir gövde gerektirir.</span><span class="sxs-lookup"><span data-stu-id="a425d-157">If the operation allows (e.g. PUT, POST) and requires a body you may provide an example of it in all of the supported representation formats (e.g. json, XML).</span></span> 

> <span data-ttu-id="a425d-158">İstek gövdesi doğrulanmazsa ve yalnızca belgeleri amacıyla kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a425d-158">The request body is used for documentation purposes only and is not validated.</span></span>
> 
> 

<span data-ttu-id="a425d-159">Bir istek gövdesi girmek için geçiş **gövde** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="a425d-159">To enter a request body, switch to the **Body** tab.</span></span>

<span data-ttu-id="a425d-160">Tıklatın **eklemek gösterimi**, istenen içerik türü adı (örn. uygulama/json) yazmaya başlayın, açılan seçin ve istenen istek gövdesi örnek seçili biçiminde metin kutusuna yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="a425d-160">Click **Add Representation**, start typing desired content type name (e.g. application/json), select it in the drop-down, and paste the desired request body example in the selected format into the text box.</span></span> 

![İstek gövdesi][api-management-request-body]

<span data-ttu-id="a425d-162">Ek gösterimler için ayrıca bir isteğe bağlı metin açıklaması belirtebilirsiniz **açıklama** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="a425d-162">In additional to representations, you can also specify an optional text description in the **Description** text box.</span></span>

## <span data-ttu-id="a425d-163"><a name="responses"></a>Yanıtları</span><span class="sxs-lookup"><span data-stu-id="a425d-163"><a name="responses"> </a>Responses</span></span>
<span data-ttu-id="a425d-164">İşlemi üretebilir için tüm durum kodları örnekleri yanıtların sağlamak için iyi bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="a425d-164">It is a good practice to provide examples of responses for all status codes that the operation may produce.</span></span> <span data-ttu-id="a425d-165">Her durum kodu birden fazla yanıt gövdesi örnek, desteklenen içerik türlerinin her biri için bir tane olabilir.</span><span class="sxs-lookup"><span data-stu-id="a425d-165">Each status code may have more than one response body example, one for each of the supported content types.</span></span> 

<span data-ttu-id="a425d-166">Bir yanıt eklemek için tıklatın **Ekle** ve istenen durum kodu yazmaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="a425d-166">To add a response, click **Add** and start typing the desired status code.</span></span> <span data-ttu-id="a425d-167">Bu örnekte durum kodudur **200 Tamam**.</span><span class="sxs-lookup"><span data-stu-id="a425d-167">In this example the status code is **200 OK**.</span></span> <span data-ttu-id="a425d-168">Kod açılan görüntülendikten sonra seçmek ve yanıt kodu oluşturulur ve işleminiz için eklendi.</span><span class="sxs-lookup"><span data-stu-id="a425d-168">Once the code is displayed in the drop-down, select it, and the response code is created and added to your operation.</span></span>

![Yanıt kodu][api-management-response-code]

<span data-ttu-id="a425d-170">Tıklatın **eklemek gösterimi**, istenen içerik türü adı (örn. uygulama/json) yazmaya başlayın ve ardından aşağı açılan seçin.</span><span class="sxs-lookup"><span data-stu-id="a425d-170">Click **Add Representation**, start typing the desired content type name (e.g. application/json) and then select it in the drop down.</span></span>

![Gövde içerik türü][api-management-response-body-content-type]

<span data-ttu-id="a425d-172">Yanıt gövdesi örnek seçili biçiminde metin kutusuna yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="a425d-172">Paste the response body example in the selected format into the text box.</span></span> 

![Yanıt gövdesi][api-management-response-body]

<span data-ttu-id="a425d-174">İsterseniz, isteğe bağlı bir açıklama ekleyin **açıklama** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="a425d-174">If desired, add an optional description into the **Description** text box.</span></span>

<span data-ttu-id="a425d-175">İşlemi yapılandırıldıktan sonra tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="a425d-175">Once the operation is configured, click **Save**.</span></span>

## <span data-ttu-id="a425d-176"><a name="next-steps"> </a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a425d-176"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="a425d-177">Operations API'ye eklendikten sonra sonraki API bir ürünle ilişkilendirin ve böylece geliştiriciler işlemlerini çağırabilirsiniz yayımlamak için adımdır.</span><span class="sxs-lookup"><span data-stu-id="a425d-177">Once the operations are added to an API, the next step is to associate the API with a product and publish it so that developers can call its operations.</span></span>

* <span data-ttu-id="a425d-178">[Oluşturma ve bir ürün yayımlama][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="a425d-178">[How to create and publish a product][How to create and publish a product]</span></span>

[api-management-management-console]: ./media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: ./media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: ./media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: ./media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: ./media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: ./media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: ./media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: ./media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: ./media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: ./media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: ./media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: ./media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: ./media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to cache operation results in Azure API Management]: api-management-howto-cache.md
