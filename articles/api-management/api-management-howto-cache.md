---
title: "Azure API Management tooimprove performansını önbelleğe alma aaaAdd | Microsoft Docs"
description: "API Management hizmeti çağrıları için nasıl tooimprove hello gecikme, bant genişliği kullanımını ve web hizmeti yükleme hakkında bilgi edinin."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 740f6a27-8323-474d-ade2-828ae0c75e7a
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 056ab7cf788218327e30bd5c028b76e3b1977fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-caching-tooimprove-performance-in-azure-api-management"></a><span data-ttu-id="2b415-103">Azure API Management'te önbelleğe alma tooimprove performans ekleme</span><span class="sxs-lookup"><span data-stu-id="2b415-103">Add caching tooimprove performance in Azure API Management</span></span>
<span data-ttu-id="2b415-104">API Management işlemleri yanıt önbelleğe alma için yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="2b415-104">Operations in API Management can be configured for response caching.</span></span> <span data-ttu-id="2b415-105">Yanıt önbelleğe alma, çok sık değişmeyen veriler için API gecikmesi, bant genişliği kullanımı ve web hizmeti yükünü önemli ölçüde azaltabilir.</span><span class="sxs-lookup"><span data-stu-id="2b415-105">Response caching can significantly reduce API latency, bandwidth consumption, and web service load for data that does not change frequently.</span></span>

<span data-ttu-id="2b415-106">Bu kılavuz size nasıl gösterir tooadd yanıt API için önbelleğe alma ve hello örnek Echo API işlemleri için ilkeleri yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="2b415-106">This guide shows you how tooadd response caching for your API and configure policies for hello sample Echo API operations.</span></span> <span data-ttu-id="2b415-107">Merhaba işlemi hello Geliştirici Portalı tooverify önbelleğe alma eylemini öğesinden sonra çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b415-107">You can then call hello operation from hello developer portal tooverify caching in action.</span></span>

> [!NOTE]
> <span data-ttu-id="2b415-108">Anahtar kullanım ilkesi ifadeleri hakkında daha fazla bilgi için bkz. [Azure API Management’te özel önbelleğe alma](api-management-sample-cache-by-key.md).</span><span class="sxs-lookup"><span data-stu-id="2b415-108">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="2b415-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2b415-109">Prerequisites</span></span>
<span data-ttu-id="2b415-110">Bu kılavuzda aşağıdaki hello adımları önce bir API Management hizmeti örneği bir API ve yapılandırılmış bir ürününüz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2b415-110">Before following hello steps in this guide, you must have an API Management service instance with an API and a product configured.</span></span> <span data-ttu-id="2b415-111">Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [Azure API Management ile çalışmaya başlama] [ Get started with Azure API Management] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="2b415-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

## <span data-ttu-id="2b415-112"><a name="configure-caching"> </a>Önbelleğe almak için bir işlemi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="2b415-112"><a name="configure-caching"> </a>Configure an operation for caching</span></span>
<span data-ttu-id="2b415-113">Bu adımda, önbelleğe alma hello ayarları hello inceleyeceksiniz **GET kaynağı (önbelleğe alınmış)** hello örnek Echo API'SİNİN işlemi.</span><span class="sxs-lookup"><span data-stu-id="2b415-113">In this step, you will review hello caching settings of hello **GET Resource (cached)** operation of hello sample Echo API.</span></span>

> [!NOTE]
> <span data-ttu-id="2b415-114">Her API Management hizmet örneği ile kullanılan tooexperiment ve API Management hakkında bilgi edinin bir Echo API'si ile önceden yapılandırılmış olarak gelir.</span><span class="sxs-lookup"><span data-stu-id="2b415-114">Each API Management service instance comes preconfigured with an Echo API that can be used tooexperiment with and learn about API Management.</span></span> <span data-ttu-id="2b415-115">Daha fazla bilgi için bkz. [Azure API Management'i kullanmaya başlama][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="2b415-115">For more information, see [Get started with Azure API Management][Get started with Azure API Management].</span></span>
> 
> 

<span data-ttu-id="2b415-116">başlatıldı, tooget tıklatın **yayımcı portalına** API Management hizmetiniz için hello Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="2b415-116">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="2b415-117">Bu toohello API Management yayımcı portalına götürür.</span><span class="sxs-lookup"><span data-stu-id="2b415-117">This takes you toohello API Management publisher portal.</span></span>

![Yayımcı portalı][api-management-management-console]

<span data-ttu-id="2b415-119">Tıklatın **API'leri** hello gelen **API Management** sol hello ve ardından menüsünde **Echo API'si**.</span><span class="sxs-lookup"><span data-stu-id="2b415-119">Click **APIs** from hello **API Management** menu on hello left, and then click **Echo API**.</span></span>

![Echo API’si][api-management-echo-api]

<span data-ttu-id="2b415-121">Merhaba tıklatın **Operations** sekmesini ve sonra hello **GET kaynağı (önbelleğe alınmış)** hello işleminden **Operations** listesi.</span><span class="sxs-lookup"><span data-stu-id="2b415-121">Click hello **Operations** tab, and then click hello **GET Resource (cached)** operation from hello **Operations** list.</span></span>

![Echo API’si işlemleri][api-management-echo-api-operations]

<span data-ttu-id="2b415-123">Merhaba tıklatın **önbelleğe alma** sekmesini tooview hello ayarları bu işlem için önbelleğe alma.</span><span class="sxs-lookup"><span data-stu-id="2b415-123">Click hello **Caching** tab tooview hello caching settings for this operation.</span></span>

![Önbelleğe alma sekmesi][api-management-caching-tab]

<span data-ttu-id="2b415-125">tooenable select hello bir işlem için önbelleğe alma **etkinleştirmek** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="2b415-125">tooenable caching for an operation, select hello **Enable** check box.</span></span> <span data-ttu-id="2b415-126">Bu örnekte, önbelleğe alma etkindir.</span><span class="sxs-lookup"><span data-stu-id="2b415-126">In this example, caching is enabled.</span></span>

<span data-ttu-id="2b415-127">Her işlem yanıtı, hello içinde hello değerlere göre anahtarlanır **sorgu dizesi parametrelerine göre değişiklik gösterebilir** ve **üstbilgileri göre değişiklik gösterebilir** alanları.</span><span class="sxs-lookup"><span data-stu-id="2b415-127">Each operation response is keyed, based on hello values in hello **Vary by query string parameters** and **Vary by headers** fields.</span></span> <span data-ttu-id="2b415-128">Sorgu dizesi parametreleri veya üst bilgileri temel alarak birden çok yanıtlarını toocache istiyorsanız, bunları bu iki alanda yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b415-128">If you want toocache multiple responses based on query string parameters or headers, you can configure them in these two fields.</span></span>

<span data-ttu-id="2b415-129">**Süre** hello hello önbelleğe alınan yanıtların sona erme aralığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="2b415-129">**Duration** specifies hello expiration interval of hello cached responses.</span></span> <span data-ttu-id="2b415-130">Bu örnekte, hello aralığıdır **3600** eşdeğer tooone saattir saniye.</span><span class="sxs-lookup"><span data-stu-id="2b415-130">In this example, hello interval is **3600** seconds, which is equivalent tooone hour.</span></span>

<span data-ttu-id="2b415-131">Bu örnekte yapılandırma önbelleği hello kullanarak, ilk isteği toohello hello **GET kaynağı (önbelleğe alınmış)** işlemi hello arka uç hizmetinden bir yanıt döndürür.</span><span class="sxs-lookup"><span data-stu-id="2b415-131">Using hello caching configuration in this example, hello first request toohello **GET Resource (cached)** operation returns a response from hello backend service.</span></span> <span data-ttu-id="2b415-132">Bu yanıt, belirtilen hello tarafından önbelleğe alınır ve anahtarlanır üst bilgilerinin ve sorgu dize parametreleri.</span><span class="sxs-lookup"><span data-stu-id="2b415-132">This response will be cached, keyed by hello specified headers and query string parameters.</span></span> <span data-ttu-id="2b415-133">Parametreler, eşleşen toohello işlemi hello olacaktır sonraki çağrılar hello önbellek süresi aralığı sona erinceye kadar döndürülen yanıt önbelleğe alınmış.</span><span class="sxs-lookup"><span data-stu-id="2b415-133">Subsequent calls toohello operation, with matching parameters, will have hello cached response returned, until hello cache duration interval has expired.</span></span>

## <span data-ttu-id="2b415-134"><a name="caching-policies"></a>Gözden geçirme hello önbelleğe alma ilkeleri</span><span class="sxs-lookup"><span data-stu-id="2b415-134"><a name="caching-policies"> </a>Review hello caching policies</span></span>
<span data-ttu-id="2b415-135">Bu adımda, hello ayarlarını önbelleğe alma hello gözden **GET kaynağı (önbelleğe alınmış)** hello örnek Echo API'SİNİN işlemi.</span><span class="sxs-lookup"><span data-stu-id="2b415-135">In this step, you review hello caching settings for hello **GET Resource (cached)** operation of hello sample Echo API.</span></span>

<span data-ttu-id="2b415-136">Ne zaman önbelleğe alma ayarları yapılandırıldığında hello üzerinde bir işlemi için **önbelleğe alma** sekmesinde, önbelleğe alma ilkeleri hello işlemi için eklenir.</span><span class="sxs-lookup"><span data-stu-id="2b415-136">When caching settings are configured for an operation on hello **Caching** tab, caching policies are added for hello operation.</span></span> <span data-ttu-id="2b415-137">Bu ilkeler görüntülenebilir ve hello İlkesi Düzenleyicisi'nde düzenlenebilir.</span><span class="sxs-lookup"><span data-stu-id="2b415-137">These policies can be viewed and edited in hello policy editor.</span></span>

<span data-ttu-id="2b415-138">Tıklatın **ilkeleri** hello gelen **API Management** hello sol ve ardından menüsünde **Echo API'si / GET kaynağı (önbelleğe alınmış)** hello gelen **işlemi**aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="2b415-138">Click **Policies** from hello **API Management** menu on hello left, and then select **Echo API / GET Resource (cached)** from hello **Operation** drop-down list.</span></span>

![İlke kapsamı işlemi][api-management-operation-dropdown]

<span data-ttu-id="2b415-140">Bu, hello İlkesi Düzenleyicisi'nde hello ilkeleri bu işlem için görüntüler.</span><span class="sxs-lookup"><span data-stu-id="2b415-140">This displays hello policies for this operation in hello policy editor.</span></span>

![API Management ilkesi düzenleyicisi][api-management-policy-editor]

<span data-ttu-id="2b415-142">Bu işlem için Hello ilke tanımı hello kullanılarak gözden geçirilen yapılandırma önbelleği hello tanımlayan hello ilkelerini içerir **önbelleğe alma** hello önceki adımda sekmesi.</span><span class="sxs-lookup"><span data-stu-id="2b415-142">hello policy definition for this operation includes hello policies that define hello caching configuration that were reviewed using hello **Caching** tab in hello previous step.</span></span>

```xml
<policies>
    <inbound>
        <base />
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false">
            <vary-by-header>Accept</vary-by-header>
            <vary-by-header>Accept-Charset</vary-by-header>
        </cache-lookup>
        <rewrite-uri template="/resource" />
    </inbound>
    <outbound>
        <base />
        <cache-store caching-mode="cache-on" duration="3600" />
    </outbound>
</policies>
```

> [!NOTE]
> <span data-ttu-id="2b415-143">Yapılan değişiklikler toohello önbelleğe alma ilkeleri hello İlkesi Düzenleyicisi'nde hello üzerinde yansıtılır **önbelleğe alma** bir işlemi ve tam tersini sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="2b415-143">Changes made toohello caching policies in hello policy editor will be reflected on hello **Caching** tab of an operation, and vice-versa.</span></span>
> 
> 

## <span data-ttu-id="2b415-144"><a name="test-operation"></a>Bir işlem çağırma ve hello önbelleğe almayı test etme</span><span class="sxs-lookup"><span data-stu-id="2b415-144"><a name="test-operation"> </a>Call an operation and test hello caching</span></span>
<span data-ttu-id="2b415-145">toosee hello önbelleğe alma eylemini, biz hello işlemi hello Geliştirici portalından çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b415-145">toosee hello caching in action, we can call hello operation from hello developer portal.</span></span> <span data-ttu-id="2b415-146">Tıklatın **Geliştirici Portalı** hello sağ üst menüsündeki içinde.</span><span class="sxs-lookup"><span data-stu-id="2b415-146">Click **Developer portal** in hello top right menu.</span></span>

![Geliştirici portalı][api-management-developer-portal-menu]

<span data-ttu-id="2b415-148">Tıklatın **API'leri** hello üst menü ve ardından **Echo API'si**.</span><span class="sxs-lookup"><span data-stu-id="2b415-148">Click **APIs** in hello top menu, and then select **Echo API**.</span></span>

![Echo API’si][api-management-apis-echo-api]

> <span data-ttu-id="2b415-150">Yapılandırılmış tek bir API veya görünür tooyour hesabı, API'lere tıklamak sizi doğrudan bu API'nin toohello işlemlerine götürür varsa.</span><span class="sxs-lookup"><span data-stu-id="2b415-150">If you have only one API configured or visible tooyour account, then clicking APIs takes you directly toohello operations for that API.</span></span>
> 
> 

<span data-ttu-id="2b415-151">Select hello **GET kaynağı (önbelleğe alınmış)** işlemi ve ardından **açık Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="2b415-151">Select hello **GET Resource (cached)** operation, and then click **Open Console**.</span></span>

![Konsolu açma][api-management-open-console]

<span data-ttu-id="2b415-153">Merhaba konsol hello Geliştirici portalından doğrudan tooinvoke işlemlere izin verir.</span><span class="sxs-lookup"><span data-stu-id="2b415-153">hello console allows you tooinvoke operations directly from hello developer portal.</span></span>

![Konsol][api-management-console]

<span data-ttu-id="2b415-155">Merhaba varsayılan değerleri tutun **param1** ve **param2**.</span><span class="sxs-lookup"><span data-stu-id="2b415-155">Keep hello default values for **param1** and **param2**.</span></span>

<span data-ttu-id="2b415-156">Select hello hello istediğiniz anahtarı **abonelik anahtarı** aşağı açılan liste.</span><span class="sxs-lookup"><span data-stu-id="2b415-156">Select hello desired key from hello **subscription-key** drop-down list.</span></span> <span data-ttu-id="2b415-157">Hesabınızda yalnızca bir abonelik varsa, bu zaten seçilir.</span><span class="sxs-lookup"><span data-stu-id="2b415-157">If your account has only one subscription, it will already be selected.</span></span>

<span data-ttu-id="2b415-158">Girin **sampleheader:value1** hello içinde **istek üst** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="2b415-158">Enter **sampleheader:value1** in hello **Request headers** text box.</span></span>

<span data-ttu-id="2b415-159">Tıklatın **HTTP Get** ve yanıt üstbilgileri hello not edin.</span><span class="sxs-lookup"><span data-stu-id="2b415-159">Click **HTTP Get** and make a note of hello response headers.</span></span>

<span data-ttu-id="2b415-160">Girin **sampleheader:value2** hello içinde **istek üst** metin kutusuna ve ardından **HTTP Get**.</span><span class="sxs-lookup"><span data-stu-id="2b415-160">Enter **sampleheader:value2** in hello **Request headers** text box, and then click **HTTP Get**.</span></span>

<span data-ttu-id="2b415-161">Bu hello değeri Not **sampleheader** hala **value1** hello yanıt.</span><span class="sxs-lookup"><span data-stu-id="2b415-161">Note that hello value of **sampleheader** is still **value1** in hello response.</span></span> <span data-ttu-id="2b415-162">Bazı farklı değerler deneyin ve önbelleğe alınan yanıt hello ilk çağrısından hello Not döndürülür.</span><span class="sxs-lookup"><span data-stu-id="2b415-162">Try some different values and note that hello cached response from hello first call is returned.</span></span>

<span data-ttu-id="2b415-163">Girin **25** hello içine **param2** alan ve ardından **HTTP Get**.</span><span class="sxs-lookup"><span data-stu-id="2b415-163">Enter **25** into hello **param2** field, and then click **HTTP Get**.</span></span>

<span data-ttu-id="2b415-164">Bu hello değeri Not **sampleheader** hello yanıt sunulmuştur **value2**.</span><span class="sxs-lookup"><span data-stu-id="2b415-164">Note that hello value of **sampleheader** in hello response is now **value2**.</span></span> <span data-ttu-id="2b415-165">Merhaba işlem sonuçları sorgu dizesi tarafından anahtarlandığından hello önceki önbelleğe alınan yanıt döndürülmedi.</span><span class="sxs-lookup"><span data-stu-id="2b415-165">Because hello operation results are keyed by query string, hello previous cached response was not returned.</span></span>

## <span data-ttu-id="2b415-166"><a name="next-steps"> </a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2b415-166"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="2b415-167">Önbelleğe alma ilkeleri hakkında daha fazla bilgi için bkz: [önbelleğe alma ilkeleri] [ Caching policies] hello içinde [API Management ilke başvurusu][API Management policy reference].</span><span class="sxs-lookup"><span data-stu-id="2b415-167">For more information about caching policies, see [Caching policies][Caching policies] in hello [API Management policy reference][API Management policy reference].</span></span>
* <span data-ttu-id="2b415-168">Anahtar kullanım ilkesi ifadeleri hakkında daha fazla bilgi için bkz. [Azure API Management’te özel önbelleğe alma](api-management-sample-cache-by-key.md).</span><span class="sxs-lookup"><span data-stu-id="2b415-168">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>

[api-management-management-console]: ./media/api-management-howto-cache/api-management-management-console.png
[api-management-echo-api]: ./media/api-management-howto-cache/api-management-echo-api.png
[api-management-echo-api-operations]: ./media/api-management-howto-cache/api-management-echo-api-operations.png
[api-management-caching-tab]: ./media/api-management-howto-cache/api-management-caching-tab.png
[api-management-operation-dropdown]: ./media/api-management-howto-cache/api-management-operation-dropdown.png
[api-management-policy-editor]: ./media/api-management-howto-cache/api-management-policy-editor.png
[api-management-developer-portal-menu]: ./media/api-management-howto-cache/api-management-developer-portal-menu.png
[api-management-apis-echo-api]: ./media/api-management-howto-cache/api-management-apis-echo-api.png
[api-management-open-console]: ./media/api-management-howto-cache/api-management-open-console.png
[api-management-console]: ./media/api-management-howto-cache/api-management-console.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review hello caching policies]: #caching-policies
[Call an operation and test hello caching]: #test-operation
[Next steps]: #next-steps
