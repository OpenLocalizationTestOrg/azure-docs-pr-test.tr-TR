---
title: Azure API Management'te aaaHow tooadd operations tooan API | Microsoft Docs
description: "Bilgi nasıl Azure API Management'te tooadd işlemleri tooan API."
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
ms.openlocfilehash: d57fa59a2b0ceb392cde23150a0cbb326e52d27d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-operations-tooan-api-in-azure-api-management"></a><span data-ttu-id="8192a-103">Nasıl Azure API Management'te tooadd işlemleri tooan API</span><span class="sxs-lookup"><span data-stu-id="8192a-103">How tooadd operations tooan API in Azure API Management</span></span>
<span data-ttu-id="8192a-104">Bir API API Management kullanmadan önce operations eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8192a-104">Before an API in API Management can be used, operations must be added.</span></span> <span data-ttu-id="8192a-105">Bu kılavuzu gösterir nasıl tooadd ve API Management işlemleri tooan API farklı türlerde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8192a-105">This guide shows how tooadd and configure different types of operations tooan API in API Management.</span></span>

## <span data-ttu-id="8192a-106"><a name="add-operation"></a>Bir işlem ekleme</span><span class="sxs-lookup"><span data-stu-id="8192a-106"><a name="add-operation"> </a>Add an operation</span></span>
<span data-ttu-id="8192a-107">Operations eklenir ve tooan API hello yayımcı portalında yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="8192a-107">Operations are added and configured tooan API in hello publisher portal.</span></span> <span data-ttu-id="8192a-108">tooaccess hello yayımcı portalı, tıklatın **yayımcı portalına** API Management hizmetiniz için hello Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="8192a-108">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Yayımcı portalı][api-management-management-console]

> <span data-ttu-id="8192a-110">Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [Azure API Management ile çalışmaya başlama] [ Get started with Azure API Management] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="8192a-110">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="8192a-111">Select hello istenen API hello yayımcı portalı ve ardından hello **Operations** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="8192a-111">Select hello desired API in hello publisher portal and then select hello **Operations** tab.</span></span> 

![İşlemler][api-management-operations]

<span data-ttu-id="8192a-113">Tıklatın **ekleme işlemi** tooadd yeni işlem.</span><span class="sxs-lookup"><span data-stu-id="8192a-113">Click **Add Operation** tooadd a new operation.</span></span> <span data-ttu-id="8192a-114">Merhaba **yeni işlem** görüntülenir ve hello **imza** sekmesi varsayılan olarak seçilir.</span><span class="sxs-lookup"><span data-stu-id="8192a-114">hello **New operation** will be displayed and hello **Signature** tab will be selected by default.</span></span>

![Ekleme işlemi][api-management-add-operation]

<span data-ttu-id="8192a-116">Merhaba belirtin **HTTP fiili** hello aşağı açılan listeden seçerek.</span><span class="sxs-lookup"><span data-stu-id="8192a-116">Specify hello **HTTP verb** by choosing from hello drop-down list.</span></span>

![HTTP yöntemi][api-management-http-method]

<a name="url-template"></a>

<span data-ttu-id="8192a-118">Bir veya daha fazla URL yolu kesimleri ve sıfır veya daha fazla sorgu dizesi parametreleri oluşan bir URL parçadaki yazarak Hello URL şablon tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="8192a-118">Define hello URL template by typing in a URL fragment consisting of one or more URL path segments and zero or more query string parameters.</span></span> <span data-ttu-id="8192a-119">Merhaba URL şablonu, eklenmiş toohello temel URL'sini hello API, tek bir HTTP işlemi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="8192a-119">hello URL template, appended toohello base URL of hello API, identifies a single HTTP operation.</span></span> <span data-ttu-id="8192a-120">Daha fazla küme ayraçları tanımlanan değişken bölümleri adlı veya birini içerebilir.</span><span class="sxs-lookup"><span data-stu-id="8192a-120">It may contain one or more named variable parts that are identified by curly braces.</span></span> <span data-ttu-id="8192a-121">Bu değişken bölümleri şablon parametreleri olarak adlandırılır ve hello isteği hello API Yönetimi platformunuz tarafından işlendiğinde hello isteğin URL'den ayıklanan değerler dinamik olarak atanır.</span><span class="sxs-lookup"><span data-stu-id="8192a-121">These variable parts are called template parameters and are dynamically assigned values extracted from hello request's URL when hello request is being processed by hello API Management platform.</span></span>

> <span data-ttu-id="8192a-122">Merhaba URL şablon joker karakter düzenleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="8192a-122">hello URL template can include wildcard patterns.</span></span> <span data-ttu-id="8192a-123">Örneğin, belirten `/*` tüm istekler bu HTTP yöntemini toohello için hizmet İleri sona erer.</span><span class="sxs-lookup"><span data-stu-id="8192a-123">For example, specifying `/*` will forward all requests for that HTTP method toohello back end service.</span></span>

![URL şablonu][api-management-url-template]

<a name="rewrite-url-template"></a>

<span data-ttu-id="8192a-125">İsterseniz, hello belirtin **URL yeniden yazma şablon**.</span><span class="sxs-lookup"><span data-stu-id="8192a-125">If desired, specify hello **Rewrite URL template**.</span></span> <span data-ttu-id="8192a-126">Bu, toouse hello standart URL şablon hello ön uç üzerinde gelen istekleri işlemek için sayesinde, hello arka uç toohello göre dönüştürülen bir URL aracılığıyla çağrılırken şablonu yeniden yazın.</span><span class="sxs-lookup"><span data-stu-id="8192a-126">This allows you toouse hello standard URL template for processing incoming requests on hello front-end, while calling hello back-end via a converted URL according toohello rewrite template.</span></span> <span data-ttu-id="8192a-127">Şablon parametreleri hello URL şablondan hello yeniden yazma şablonunda kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8192a-127">Template parameters from hello URL template should be used in hello rewrite template.</span></span> <span data-ttu-id="8192a-128">Merhaba aşağıdaki örnek hello önceki örnekteki hello web hizmeti yol kesimi hello bir sorgu parametresi olarak API hello hello URL şablonları kullanarak API Management platform yayımlanan sağlanabilir olarak kodlanmış nasıl içerik türünü gösterir.</span><span class="sxs-lookup"><span data-stu-id="8192a-128">hello following example shows how content type encoded as path segment in hello web service from hello previous example can be provided as a query parameter in hello API published via hello API Management platform using hello URL templates.</span></span>

![URL şablonu yeniden yazma][api-management-url-template-rewrite]

<span data-ttu-id="8192a-130">Arayanlar toohello işlemi hello biçimi kullanın `/customers?customerid=ALFKI` ve bu çok eşlenecek`/Customers('ALFKI')` hello arka uç hizmetine zaman çağrılır.</span><span class="sxs-lookup"><span data-stu-id="8192a-130">Callers toohello operation will use hello format `/customers?customerid=ALFKI` and this will be mapped too`/Customers('ALFKI')` when hello back-end service is invoked.</span></span>

<span data-ttu-id="8192a-131">**Görüntü** adı ve **açıklama** hello işlemi bir açıklama belirtin ve kullanılan tooprovide belgelerine hello Geliştirici Portalı'nda bu API'yi kullanarak toohello geliştiricilerin önerilir.</span><span class="sxs-lookup"><span data-stu-id="8192a-131">**Display** name and **Description** provide a description of hello operation and are used tooprovide documentation toohello developers using this API in hello developer portal.</span></span>

![Açıklama][api-management-description]

<span data-ttu-id="8192a-133">Merhaba işlemi açıklama belirtilebilir düz metin veya HTML hello **açıklama** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="8192a-133">hello operation description can be specified as plain text or HTML in hello **Description** text box.</span></span>

## <span data-ttu-id="8192a-134"><a name="operation-caching"></a>İşlemi önbelleğe alma</span><span class="sxs-lookup"><span data-stu-id="8192a-134"><a name="operation-caching"> </a>Operation caching</span></span>
<span data-ttu-id="8192a-135">Yanıt önbelleğe alma düşürmeye bant genişliği tüketimi hello API tüketiciler tarafından algılanan gecikmesini azaltır ve hello HTTP web hizmeti uygulama düşüşleri hello yükle hello API.</span><span class="sxs-lookup"><span data-stu-id="8192a-135">Response caching reduces latency perceived by hello API consumers, lowers bandwidth consumption and decreases hello load on hello HTTP web service implementing hello API.</span></span> 

<span data-ttu-id="8192a-136">tooeasily ve hızlı bir şekilde select hello hello işlem için önbelleğe almayı etkinleştir **önbelleğe alma** sekmesinde ve hello denetleyin **etkinleştirmek** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="8192a-136">tooeasily and quickly enable caching for hello operation, select hello **Caching** tab and check hello **Enable** checkbox.</span></span>

![Önbelleğe alma][api-management-caching-tab]

<span data-ttu-id="8192a-138">**Süre** hello sırasında hangi hello işlemi yanıt hello önbellekte kalır süreyi belirtir.</span><span class="sxs-lookup"><span data-stu-id="8192a-138">**Duration** specifies hello time period during which hello operation response remains in hello cache.</span></span> <span data-ttu-id="8192a-139">Merhaba varsayılan değer 3600 saniye veya 1 saat olur.</span><span class="sxs-lookup"><span data-stu-id="8192a-139">hello default value is 3600 seconds or 1 hour.</span></span>

<span data-ttu-id="8192a-140">Önbellek anahtarlarını yanıtları arasında kullanılan toodifferentiate içindir tooeach farklı önbellek anahtarını karşılık gelen hello yanıt kendi ayrı önbelleğe alınan değeri alır.</span><span class="sxs-lookup"><span data-stu-id="8192a-140">Cache keys are used toodifferentiate between responses so that hello response corresponding tooeach different cache key will get its own separate cached value.</span></span> <span data-ttu-id="8192a-141">İsteğe bağlı olarak, özel bir sorgu dizesi parametreleri ve/veya HTTP üstbilgileri toobe hello önbellek anahtar değerlerini bilgisayar kullanılan girin **sorgu dizesi parametrelerine göre değişiklik gösterebilir** ve **üstbilgileri göre değişiklik gösterebilir** metin kutuları sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="8192a-141">Optionally, enter specific query string parameters and/or HTTP headers toobe used in computing cache key values in hello **Vary by query string parameters** and **Vary by headers** text boxes respectively.</span></span> <span data-ttu-id="8192a-142">Ne zaman belirtilen, tam istek URL'si yok ve HTTP üstbilgi değerlerini aşağıdaki hello önbellek anahtar oluşturma kullanılır: **kabul** ve **Accept-Charset**.</span><span class="sxs-lookup"><span data-stu-id="8192a-142">When none are specified, full request URL and hello following HTTP header values are used in cache key generation: **Accept** and **Accept-Charset**.</span></span>

> <span data-ttu-id="8192a-143">Önbelleğe alma ve önbelleğe alma ilkeleri hakkında daha fazla bilgi için bkz: [nasıl toocache işlemi Azure API Management'te sonuçları][How toocache operation results in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="8192a-143">For more information on caching and caching policies, see [How toocache operation results in Azure API Management][How toocache operation results in Azure API Management].</span></span>
> 
> 

## <span data-ttu-id="8192a-144"><a name="request-parameters"></a>Parametreleri</span><span class="sxs-lookup"><span data-stu-id="8192a-144"><a name="request-parameters"> </a>Request parameters</span></span>
<span data-ttu-id="8192a-145">İşlem parametrelerini hello parametreleri sekmesinde yönetilir. Hello belirtilen parametreleri **URL şablonu** hello üzerinde **imza** sekmesinde otomatik olarak eklenir ve yalnızca hello URL şablonu düzenleyerek değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="8192a-145">Operation parameters are managed on hello Parameters tab. Parameters specified in hello **URL Template** on hello **Signature** tab are added automatically and can be changed only by editing hello URL template.</span></span> <span data-ttu-id="8192a-146">Ek parametreler el ile girilebilir.</span><span class="sxs-lookup"><span data-stu-id="8192a-146">Additional parameters can be entered manually.</span></span>

<span data-ttu-id="8192a-147">Yeni bir sorgu parametresi tooadd tıklatın **sorgu parametresi Ekle** ve aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="8192a-147">tooadd a new query parameter, click **Add Query Parameter** and enter hello following information:</span></span>

* <span data-ttu-id="8192a-148">**Ad** -parametre adı.</span><span class="sxs-lookup"><span data-stu-id="8192a-148">**Name** - parameter name.</span></span>
* <span data-ttu-id="8192a-149">**Açıklama** -hello parametre (isteğe bağlı) kısa bir açıklaması.</span><span class="sxs-lookup"><span data-stu-id="8192a-149">**Description** - a brief description of hello parameter (optional).</span></span>
* <span data-ttu-id="8192a-150">**Tür** -hello açılan seçilen parametre türü.</span><span class="sxs-lookup"><span data-stu-id="8192a-150">**Type** - parameter type, selected in hello drop down.</span></span>
* <span data-ttu-id="8192a-151">**Değerleri** -toothis parametresi atanabilir değerleri.</span><span class="sxs-lookup"><span data-stu-id="8192a-151">**Values** - values that can be assigned toothis parameter.</span></span> <span data-ttu-id="8192a-152">Merhaba değerlerden birini varsayılan olarak (isteğe bağlı) işaretlenebilir.</span><span class="sxs-lookup"><span data-stu-id="8192a-152">One of hello values can be marked as default (optional).</span></span>
* <span data-ttu-id="8192a-153">**Gerekli** -hello onay kutusunu işaretleyerek hello parametre zorunlu kılabilir.</span><span class="sxs-lookup"><span data-stu-id="8192a-153">**Required** - make hello parameter mandatory by checking hello checkbox.</span></span> 

![İstek parametreleri][api-management-request-parameters]

## <span data-ttu-id="8192a-155"><a name="request-body"></a>İstek gövdesinde</span><span class="sxs-lookup"><span data-stu-id="8192a-155"><a name="request-body"> </a>Request body</span></span>
<span data-ttu-id="8192a-156">Merhaba işlemi izin veriyorsa (örneğin, PUT, POST) ve onu hello tümünde örneği sağlayabilir gövde desteklenen gösterimi biçimleri (örneğin json, XML) gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8192a-156">If hello operation allows (e.g. PUT, POST) and requires a body you may provide an example of it in all of hello supported representation formats (e.g. json, XML).</span></span> 

> <span data-ttu-id="8192a-157">Merhaba istek gövdesi yalnızca belgeleri amaçlar için kullanılır ve doğrulanmazsa.</span><span class="sxs-lookup"><span data-stu-id="8192a-157">hello request body is used for documentation purposes only and is not validated.</span></span>
> 
> 

<span data-ttu-id="8192a-158">bir istek gövdesi tooenter geçiş toohello **gövde** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="8192a-158">tooenter a request body, switch toohello **Body** tab.</span></span>

<span data-ttu-id="8192a-159">Tıklatın **eklemek gösterimi**, istenen içerik türü (örn. uygulama/json), adını yazarak Başlat'ı seçin, hello açılır ve Yapıştır hello istenen istek gövdesi örnek hello seçilen biçiminde hello metin kutusuna.</span><span class="sxs-lookup"><span data-stu-id="8192a-159">Click **Add Representation**, start typing desired content type name (e.g. application/json), select it in hello drop-down, and paste hello desired request body example in hello selected format into hello text box.</span></span> 

![İstek gövdesi][api-management-request-body]

<span data-ttu-id="8192a-161">Ek toorepresentations içinde hello isteğe bağlı metnini açıklamada da belirtebilirsiniz **açıklama** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="8192a-161">In additional toorepresentations, you can also specify an optional text description in hello **Description** text box.</span></span>

## <span data-ttu-id="8192a-162"><a name="responses"></a>Yanıtları</span><span class="sxs-lookup"><span data-stu-id="8192a-162"><a name="responses"> </a>Responses</span></span>
<span data-ttu-id="8192a-163">Yanıtlar hello işlemi üretebilir tüm durum kodları için iyi bir uygulama tooprovide örnekleri olur.</span><span class="sxs-lookup"><span data-stu-id="8192a-163">It is a good practice tooprovide examples of responses for all status codes that hello operation may produce.</span></span> <span data-ttu-id="8192a-164">Birden fazla yanıt gövdesi örnek her durum koduna sahip olabilir, her hello desteklenen içerik türleri.</span><span class="sxs-lookup"><span data-stu-id="8192a-164">Each status code may have more than one response body example, one for each of hello supported content types.</span></span> 

<span data-ttu-id="8192a-165">tooadd bir yanıt tıklatın **Ekle** ve istenen hello durum kodu yazmaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="8192a-165">tooadd a response, click **Add** and start typing hello desired status code.</span></span> <span data-ttu-id="8192a-166">Bu örnek hello durum kodudur **200 Tamam**.</span><span class="sxs-lookup"><span data-stu-id="8192a-166">In this example hello status code is **200 OK**.</span></span> <span data-ttu-id="8192a-167">Merhaba kod hello açılan listesinde görüntülendikten sonra seçin ve hello yanıt kodu oluşturulan ve eklenen tooyour işlemdir.</span><span class="sxs-lookup"><span data-stu-id="8192a-167">Once hello code is displayed in hello drop-down, select it, and hello response code is created and added tooyour operation.</span></span>

![Yanıt kodu][api-management-response-code]

<span data-ttu-id="8192a-169">Tıklatın **eklemek gösterimi**hello istediğiniz içerik türü adı (örn. uygulama/json) yazmaya başlayın ve ardından hello içinde açılır.</span><span class="sxs-lookup"><span data-stu-id="8192a-169">Click **Add Representation**, start typing hello desired content type name (e.g. application/json) and then select it in hello drop down.</span></span>

![Gövde içerik türü][api-management-response-body-content-type]

<span data-ttu-id="8192a-171">Merhaba yanıt gövdesi örneği hello seçili biçiminde hello metin kutusuna yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="8192a-171">Paste hello response body example in hello selected format into hello text box.</span></span> 

![Yanıt gövdesi][api-management-response-body]

<span data-ttu-id="8192a-173">İsterseniz, isteğe bağlı bir açıklama hello içine ekleme **açıklama** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="8192a-173">If desired, add an optional description into hello **Description** text box.</span></span>

<span data-ttu-id="8192a-174">Merhaba işlemi yapılandırıldıktan sonra tıklatın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="8192a-174">Once hello operation is configured, click **Save**.</span></span>

## <span data-ttu-id="8192a-175"><a name="next-steps"> </a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8192a-175"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="8192a-176">Merhaba işlemleri tooan API eklendikten sonra hello sonraki adıma tooassociate hello API bir ürüne sahip olan ve böylece geliştiriciler işlemlerini çağırabilirsiniz yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="8192a-176">Once hello operations are added tooan API, hello next step is tooassociate hello API with a product and publish it so that developers can call its operations.</span></span>

* <span data-ttu-id="8192a-177">[Nasıl toocreate ürün ve yayımlama][How toocreate and publish a product]</span><span class="sxs-lookup"><span data-stu-id="8192a-177">[How toocreate and publish a product][How toocreate and publish a product]</span></span>

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

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocache operation results in Azure API Management]: api-management-howto-cache.md
