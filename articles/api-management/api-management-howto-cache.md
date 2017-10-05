---
title: "Azure API Management performansını artırmak için önbelleğe alma ekleme | Microsoft Belgeleri"
description: "API Management hizmeti çağrıları için gecikme, bant genişliği kullanımı ve web hizmeti yüklerini geliştirmeyi öğrenin."
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
ms.openlocfilehash: 59c595f0d5ce849f44c46fdb6cab0b44d35fffa0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="add-caching-to-improve-performance-in-azure-api-management"></a><span data-ttu-id="fb059-103">Azure API Management performansını artırmak için önbelleğe alma ekleme</span><span class="sxs-lookup"><span data-stu-id="fb059-103">Add caching to improve performance in Azure API Management</span></span>
<span data-ttu-id="fb059-104">API Management işlemleri yanıt önbelleğe alma için yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="fb059-104">Operations in API Management can be configured for response caching.</span></span> <span data-ttu-id="fb059-105">Yanıt önbelleğe alma, çok sık değişmeyen veriler için API gecikmesi, bant genişliği kullanımı ve web hizmeti yükünü önemli ölçüde azaltabilir.</span><span class="sxs-lookup"><span data-stu-id="fb059-105">Response caching can significantly reduce API latency, bandwidth consumption, and web service load for data that does not change frequently.</span></span>

<span data-ttu-id="fb059-106">Bu kılavuz size API’nize yanıt önbelleğe alma eklemeyi ve örnek Echo API işlemleri için ilkeleri yapılandırmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="fb059-106">This guide shows you how to add response caching for your API and configure policies for the sample Echo API operations.</span></span> <span data-ttu-id="fb059-107">Böylece önbelleğe alma eylemini doğrulamak için işlemi geliştirici portalından çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fb059-107">You can then call the operation from the developer portal to verify caching in action.</span></span>

> [!NOTE]
> <span data-ttu-id="fb059-108">Anahtar kullanım ilkesi ifadeleri hakkında daha fazla bilgi için bkz. [Azure API Management’te özel önbelleğe alma](api-management-sample-cache-by-key.md).</span><span class="sxs-lookup"><span data-stu-id="fb059-108">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="fb059-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="fb059-109">Prerequisites</span></span>
<span data-ttu-id="fb059-110">Bu kılavuzdaki adımları izlemeden önce, API ve ürün yapılandırılmış bir API Management hizmeti örneğine sahip olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="fb059-110">Before following the steps in this guide, you must have an API Management service instance with an API and a product configured.</span></span> <span data-ttu-id="fb059-111">Henüz bir API Management hizmeti örneği oluşturmadıysanız, [Azure API Management'i kullanmaya başlama][Get started with Azure API Management] öğreticisinde [API Management hizmet örneği oluşturma][Create an API Management service instance]'ya bakın.</span><span class="sxs-lookup"><span data-stu-id="fb059-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

## <span data-ttu-id="fb059-112"><a name="configure-caching"> </a>Önbelleğe almak için bir işlemi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fb059-112"><a name="configure-caching"> </a>Configure an operation for caching</span></span>
<span data-ttu-id="fb059-113">Bu adımda, örnek Echo API’sinin **GET Kaynağı (önbelleğe alınmış)** işleminin önbelleğe alma ayarlarını inceleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="fb059-113">In this step, you will review the caching settings of the **GET Resource (cached)** operation of the sample Echo API.</span></span>

> [!NOTE]
> <span data-ttu-id="fb059-114">Her API Management hizmeti örneği, API Management’i denemek ve hakkında bilgi almak için kullanılabilecek bir Echo API’si ile önceden yapılandırılmış olarak gelir.</span><span class="sxs-lookup"><span data-stu-id="fb059-114">Each API Management service instance comes preconfigured with an Echo API that can be used to experiment with and learn about API Management.</span></span> <span data-ttu-id="fb059-115">Daha fazla bilgi için bkz. [Azure API Management'i kullanmaya başlama][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="fb059-115">For more information, see [Get started with Azure API Management][Get started with Azure API Management].</span></span>
> 
> 

<span data-ttu-id="fb059-116">Kullanmaya başlamak için API Management hizmetiniz için Azure Portal'da **Yayımcı portalı**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fb059-116">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="fb059-117">Bu sizi API Management yayımcı portalına götürür.</span><span class="sxs-lookup"><span data-stu-id="fb059-117">This takes you to the API Management publisher portal.</span></span>

![Yayımcı portalı][api-management-management-console]

<span data-ttu-id="fb059-119">Soldaki **API Management** menüsünde **API'ler**’e ve ardından **Echo API’si**’ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fb059-119">Click **APIs** from the **API Management** menu on the left, and then click **Echo API**.</span></span>

![Echo API’si][api-management-echo-api]

<span data-ttu-id="fb059-121">**İşlemler** sekmesine tıklayın ve ardından **İşlemler** listesinde **GET Kaynağı (önbelleğe alınmış)** işlemine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fb059-121">Click the **Operations** tab, and then click the **GET Resource (cached)** operation from the **Operations** list.</span></span>

![Echo API’si işlemleri][api-management-echo-api-operations]

<span data-ttu-id="fb059-123">Bu işlemin önbelleğe alma ayarlarını görüntülemek için **Önbelleğe alma**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fb059-123">Click the **Caching** tab to view the caching settings for this operation.</span></span>

![Önbelleğe alma sekmesi][api-management-caching-tab]

<span data-ttu-id="fb059-125">Bir işlem için önbelleğe almayı etkinleştirmek üzere **Etkinleştir** onay kutusunu seçin.</span><span class="sxs-lookup"><span data-stu-id="fb059-125">To enable caching for an operation, select the **Enable** check box.</span></span> <span data-ttu-id="fb059-126">Bu örnekte, önbelleğe alma etkindir.</span><span class="sxs-lookup"><span data-stu-id="fb059-126">In this example, caching is enabled.</span></span>

<span data-ttu-id="fb059-127">Her işlem, **Sorgu dizesi parametrelerine göre değişiklik gösterebilir** ve **Üst bilgilere göre değişiklik gösterebilir** alanlarındaki değerlere göre anahtarlanır ve bunları temel alır.</span><span class="sxs-lookup"><span data-stu-id="fb059-127">Each operation response is keyed, based on the values in the **Vary by query string parameters** and **Vary by headers** fields.</span></span> <span data-ttu-id="fb059-128">Sorgu dizesi parametreleri veya üst bilgileri temel alan birden çok yanıtı önbelleğe almak istiyorsanız, bunları bu iki alanda yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fb059-128">If you want to cache multiple responses based on query string parameters or headers, you can configure them in these two fields.</span></span>

<span data-ttu-id="fb059-129">**Süre** önbelleğe alınan yanıtların sona erme aralığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="fb059-129">**Duration** specifies the expiration interval of the cached responses.</span></span> <span data-ttu-id="fb059-130">Bu örnekte, aralık bir saate eşit olan **3600** saniyedir.</span><span class="sxs-lookup"><span data-stu-id="fb059-130">In this example, the interval is **3600** seconds, which is equivalent to one hour.</span></span>

<span data-ttu-id="fb059-131">Bu örnekte önbelleğe alma yapılandırması kullanılarak, **GET Kaynağı (önbelleğe alınmış)** işlemine yapılan ilk istek işlemi arka uç hizmetinden bir yanıt döndürür.</span><span class="sxs-lookup"><span data-stu-id="fb059-131">Using the caching configuration in this example, the first request to the **GET Resource (cached)** operation returns a response from the backend service.</span></span> <span data-ttu-id="fb059-132">Bu yanıt, belirtilen üst bilgiler ve sorgu dizesi parametreleri tarafından önbelleğe alınır ve anahtarlanır.</span><span class="sxs-lookup"><span data-stu-id="fb059-132">This response will be cached, keyed by the specified headers and query string parameters.</span></span> <span data-ttu-id="fb059-133">Eşleşen parametrelerle, işleme yapılan sonraki çağrılar, önbelleğe alma süresi aralığı sona erinceye kadar, önbelleğe alınan yanıtın döndürülmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="fb059-133">Subsequent calls to the operation, with matching parameters, will have the cached response returned, until the cache duration interval has expired.</span></span>

## <span data-ttu-id="fb059-134"><a name="caching-policies"> </a>Önbelleğe alma ilkelerini gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="fb059-134"><a name="caching-policies"> </a>Review the caching policies</span></span>
<span data-ttu-id="fb059-135">Bu adımda, örnek Echo API’sinin **GET Kaynağı (önbelleğe alınmış)** işleminin önbelleğe alma ayarlarını incelersiniz.</span><span class="sxs-lookup"><span data-stu-id="fb059-135">In this step, you review the caching settings for the **GET Resource (cached)** operation of the sample Echo API.</span></span>

<span data-ttu-id="fb059-136">Bir işlem için **Önbelleğe alma** sekmesinde önbelleğe alma ayarları yapılandırıldığında, işlem için önbelleğe alma ilkeleri eklenir.</span><span class="sxs-lookup"><span data-stu-id="fb059-136">When caching settings are configured for an operation on the **Caching** tab, caching policies are added for the operation.</span></span> <span data-ttu-id="fb059-137">Bu ilkeler ilke düzenleyicisinde görüntülenip düzenlenebilir.</span><span class="sxs-lookup"><span data-stu-id="fb059-137">These policies can be viewed and edited in the policy editor.</span></span>

<span data-ttu-id="fb059-138">Soldaki **API Management** menüsünde **İlkeler**’e tıklayın ve ardından **İşlem** açılır listesinde **Echo API’si / GET Kaynağı (önbelleğe alınmış)** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="fb059-138">Click **Policies** from the **API Management** menu on the left, and then select **Echo API / GET Resource (cached)** from the **Operation** drop-down list.</span></span>

![İlke kapsamı işlemi][api-management-operation-dropdown]

<span data-ttu-id="fb059-140">Bu, bu işlemin ilkelerini ilke düzenleyicisinde görüntüler.</span><span class="sxs-lookup"><span data-stu-id="fb059-140">This displays the policies for this operation in the policy editor.</span></span>

![API Management ilkesi düzenleyicisi][api-management-policy-editor]

<span data-ttu-id="fb059-142">Bu işlem için ilke tanımı, önceki adımda **Önbelleğe alma** sekmesi kullanılarak gözden geçirilen önbelleğe alma yapılandırmasını tanımlayan ilkeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="fb059-142">The policy definition for this operation includes the policies that define the caching configuration that were reviewed using the **Caching** tab in the previous step.</span></span>

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
> <span data-ttu-id="fb059-143">İlk düzenleyicisinde önbelleğe alma ilkelerinde yapılan değişiklikler işlemin **Önbelleğe alma** sekmesinde yansıtılır ve bu durumun tersi de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="fb059-143">Changes made to the caching policies in the policy editor will be reflected on the **Caching** tab of an operation, and vice-versa.</span></span>
> 
> 

## <span data-ttu-id="fb059-144"><a name="test-operation"> </a>İşlem çağırma ve önbelleğe almayı test etme</span><span class="sxs-lookup"><span data-stu-id="fb059-144"><a name="test-operation"> </a>Call an operation and test the caching</span></span>
<span data-ttu-id="fb059-145">Önbelleğe alma eylemini görmek için, işlemi geliştirici portalından çağırabiliriz.</span><span class="sxs-lookup"><span data-stu-id="fb059-145">To see the caching in action, we can call the operation from the developer portal.</span></span> <span data-ttu-id="fb059-146">Sağ üstteki menüde **Geliştirici Portalı**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fb059-146">Click **Developer portal** in the top right menu.</span></span>

![Geliştirici portalı][api-management-developer-portal-menu]

<span data-ttu-id="fb059-148">Üstteki menüde **API'ler**’e tıklayıp **Echo API’si**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="fb059-148">Click **APIs** in the top menu, and then select **Echo API**.</span></span>

![Echo API’si][api-management-apis-echo-api]

> <span data-ttu-id="fb059-150">Yapılandırılmış ya da hesabınıza görünen yalnızca bir API’niz varsa, API’lere tıklamak sizi doğrudan bu API’nin işlemlerine götürür.</span><span class="sxs-lookup"><span data-stu-id="fb059-150">If you have only one API configured or visible to your account, then clicking APIs takes you directly to the operations for that API.</span></span>
> 
> 

<span data-ttu-id="fb059-151">**GET Kaynağı (önbelleğe alınmış)** işlemini seçin ve ardından **Konsolu Aç**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fb059-151">Select the **GET Resource (cached)** operation, and then click **Open Console**.</span></span>

![Konsolu açma][api-management-open-console]

<span data-ttu-id="fb059-153">Konsol, işlemleri doğrudan geliştirici portalından çağırmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="fb059-153">The console allows you to invoke operations directly from the developer portal.</span></span>

![Konsol][api-management-console]

<span data-ttu-id="fb059-155">**param1** ve **param2** için varsayılan değerleri tutun.</span><span class="sxs-lookup"><span data-stu-id="fb059-155">Keep the default values for **param1** and **param2**.</span></span>

<span data-ttu-id="fb059-156">**subscription-key** açılır listesinde istediğiniz anahtarı seçin.</span><span class="sxs-lookup"><span data-stu-id="fb059-156">Select the desired key from the **subscription-key** drop-down list.</span></span> <span data-ttu-id="fb059-157">Hesabınızda yalnızca bir abonelik varsa, bu zaten seçilir.</span><span class="sxs-lookup"><span data-stu-id="fb059-157">If your account has only one subscription, it will already be selected.</span></span>

<span data-ttu-id="fb059-158">**İstek üst bilgileri** metin kutusuna **sampleheader:value1** değerini girin.</span><span class="sxs-lookup"><span data-stu-id="fb059-158">Enter **sampleheader:value1** in the **Request headers** text box.</span></span>

<span data-ttu-id="fb059-159">**HTTP Al**’a tıklayın ve yanıt üst bilgilerini not edin.</span><span class="sxs-lookup"><span data-stu-id="fb059-159">Click **HTTP Get** and make a note of the response headers.</span></span>

<span data-ttu-id="fb059-160">**İstek üst bilgileri** metin kutusuna **sampleheader:value2** değerini girin ve ardından **HTTP Get**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fb059-160">Enter **sampleheader:value2** in the **Request headers** text box, and then click **HTTP Get**.</span></span>

<span data-ttu-id="fb059-161">**sampleheader** değerinin hala yanıttaki **value1** olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="fb059-161">Note that the value of **sampleheader** is still **value1** in the response.</span></span> <span data-ttu-id="fb059-162">Bazı farklı değerler deneyin ve ilk çağrıya gelen önbelleğe alınan yanıtın döndürüldüğüne dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="fb059-162">Try some different values and note that the cached response from the first call is returned.</span></span>

<span data-ttu-id="fb059-163">**param2** alanına **25** değerini girin ve ardından **HTTP Get**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fb059-163">Enter **25** into the **param2** field, and then click **HTTP Get**.</span></span>

<span data-ttu-id="fb059-164">Yanıttaki **sampleheader** değerinin artık **value2** olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="fb059-164">Note that the value of **sampleheader** in the response is now **value2**.</span></span> <span data-ttu-id="fb059-165">İşlem sonuçları sorgu dizesi tarafından anahtarlandığından, önceki önbelleğe alınan yanıt döndürülmedi.</span><span class="sxs-lookup"><span data-stu-id="fb059-165">Because the operation results are keyed by query string, the previous cached response was not returned.</span></span>

## <span data-ttu-id="fb059-166"><a name="next-steps"> </a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fb059-166"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="fb059-167">Önbelleğe alma ilkeleri hakkında daha fazla bilgi için bkz. [API Management ilke başvurusunda][API Management policy reference] [Önbelleğe alma ilkeleri][Caching policies].</span><span class="sxs-lookup"><span data-stu-id="fb059-167">For more information about caching policies, see [Caching policies][Caching policies] in the [API Management policy reference][API Management policy reference].</span></span>
* <span data-ttu-id="fb059-168">Anahtar kullanım ilkesi ifadeleri hakkında daha fazla bilgi için bkz. [Azure API Management’te özel önbelleğe alma](api-management-sample-cache-by-key.md).</span><span class="sxs-lookup"><span data-stu-id="fb059-168">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>

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


[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review the caching policies]: #caching-policies
[Call an operation and test the caching]: #test-operation
[Next steps]: #next-steps
