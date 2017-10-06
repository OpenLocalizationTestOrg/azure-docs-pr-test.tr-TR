---
title: "Azure API Management'te aaaProduct şablonları | Microsoft Docs"
description: "Merhaba ürün toocustomize Merhaba içeriğine hello Azure API Management Geliştirici Portalı'nda nasıl sayfaları hakkında bilgi edinin."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 49f9254c-4c5f-4ed4-9c8d-798f44e805ee
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 60600299287aad87f9b621782ab5ceb866601d03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="product-templates-in-azure-api-management"></a><span data-ttu-id="20c90-103">Azure API Management'te ürün şablonları</span><span class="sxs-lookup"><span data-stu-id="20c90-103">Product templates in Azure API Management</span></span>
<span data-ttu-id="20c90-104">Azure API Management yeteneği toocustomize hello Geliştirici portal sayfalarına içeriklerini yapılandırma şablonları kümesini kullanarak içeriğini hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="20c90-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="20c90-105">Kullanarak [DotLiquid](http://dotliquidmarkup.org/) sözdizimi ve hello düzenleyiciyi, gibi [tasarımcıları için DotLiquid](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), ve sağlanan bir dizi yerelleştirilmiş [dize kaynakları](api-management-template-resources.md#strings), [ Karakter kaynakları](api-management-template-resources.md#glyphs), ve [sayfasında denetimleri](api-management-page-controls.md), bu şablonları kullanarak uygun gördüğünüz şekilde hello sayfaların büyük esneklik tooconfigure hello içeriğe sahip.</span><span class="sxs-lookup"><span data-stu-id="20c90-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="20c90-106">Bu bölümdeki Hello şablonları hello Geliştirici Portalı'nda hello ürün sayfaları toocustomize hello içeriği sağlar.</span><span class="sxs-lookup"><span data-stu-id="20c90-106">hello templates in this section allow you toocustomize hello content of hello product pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="20c90-107">Ürün Listesi</span><span class="sxs-lookup"><span data-stu-id="20c90-107">Product list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="20c90-108">Ürün</span><span class="sxs-lookup"><span data-stu-id="20c90-108">Product</span></span>](#Product)  
  
> [!NOTE]
>  <span data-ttu-id="20c90-109">Örnek varsayılan şablonları belgelerine aşağıdaki hello dahil olan, ancak konu toochange toocontinuous geliştirmeler nedeniyle.</span><span class="sxs-lookup"><span data-stu-id="20c90-109">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="20c90-110">İstenen toohello tek tek şablonları giderek hello Canlı varsayılan şablonları hello Geliştirici Portalı'nda görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="20c90-110">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="20c90-111">Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [nasıl toocustomize hello şablonları kullanarak API Management Geliştirici Portalı](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="20c90-111">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="20c90-112"><a name="ProductList"></a>Ürün Listesi</span><span class="sxs-lookup"><span data-stu-id="20c90-112"><a name="ProductList"></a> Product list</span></span>  
 <span data-ttu-id="20c90-113">Merhaba **ürün listesi** şablonu verir hello ürün listesi sayfasının toocustomize hello gövdesi hello Geliştirici Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="20c90-113">hello **Product list** template allows you toocustomize hello body of hello product list page in hello developer portal.</span></span>  
  
 <span data-ttu-id="20c90-114">![Ürün listesini](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span><span class="sxs-lookup"><span data-stu-id="20c90-114">![Products list](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="20c90-115">Varsayılan şablonu</span><span class="sxs-lookup"><span data-stu-id="20c90-115">Default template</span></span>  
  
```xml  
<search-control></search-control>  
<div class="row">  
    <div class="col-md-9">  
        <h2>{% localized "ProductsStrings|PageTitleProducts" %}</h2>  
    </div>  
</div>  
<div class="row">  
    <div class="col-md-12">  
    {% if products.size > 0 %}  
    <ul class="list-unstyled">  
    {% for product in products %}  
        <li>  
            <h3><a href="/products/{{product.id}}">{{product.title}}</a></h3>  
            {{product.description}}  
        </li>     
    {% endfor %}  
    </ul>  
    <paging-control></paging-control>  
    {% else %}  
    {% localized "CommonResources|NoItemsToDisplay" %}  
    {% endif %}  
    </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="20c90-116">Denetimler</span><span class="sxs-lookup"><span data-stu-id="20c90-116">Controls</span></span>  
 <span data-ttu-id="20c90-117">Merhaba `Product list` şablonu hello aşağıdaki kullanabilir [sayfasında denetimleri](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="20c90-117">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="20c90-118">disk belleği denetimi</span><span class="sxs-lookup"><span data-stu-id="20c90-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
-   [<span data-ttu-id="20c90-119">arama denetimi</span><span class="sxs-lookup"><span data-stu-id="20c90-119">search-control</span></span>](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a><span data-ttu-id="20c90-120">Veri modeli</span><span class="sxs-lookup"><span data-stu-id="20c90-120">Data model</span></span>  
  
|<span data-ttu-id="20c90-121">Özellik</span><span class="sxs-lookup"><span data-stu-id="20c90-121">Property</span></span>|<span data-ttu-id="20c90-122">Tür</span><span class="sxs-lookup"><span data-stu-id="20c90-122">Type</span></span>|<span data-ttu-id="20c90-123">Açıklama</span><span class="sxs-lookup"><span data-stu-id="20c90-123">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="20c90-124">Sayfalama</span><span class="sxs-lookup"><span data-stu-id="20c90-124">Paging</span></span>|<span data-ttu-id="20c90-125">[Disk belleği](api-management-template-data-model-reference.md#Paging) varlık.</span><span class="sxs-lookup"><span data-stu-id="20c90-125">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="20c90-126">Merhaba ürünleri koleksiyonu için başlangıç disk belleği bilgilerini.</span><span class="sxs-lookup"><span data-stu-id="20c90-126">hello paging information for hello products collection.</span></span>|  
|<span data-ttu-id="20c90-127">Filtreleme</span><span class="sxs-lookup"><span data-stu-id="20c90-127">Filtering</span></span>|<span data-ttu-id="20c90-128">[Filtreleme](api-management-template-data-model-reference.md#Filtering) varlık.</span><span class="sxs-lookup"><span data-stu-id="20c90-128">[Filtering](api-management-template-data-model-reference.md#Filtering) entity.</span></span>|<span data-ttu-id="20c90-129">Merhaba ürün listesi sayfası için filtre bilgilerini hello.</span><span class="sxs-lookup"><span data-stu-id="20c90-129">hello filtering information for hello products list page.</span></span>|  
|<span data-ttu-id="20c90-130">Ürünler</span><span class="sxs-lookup"><span data-stu-id="20c90-130">Products</span></span>|<span data-ttu-id="20c90-131">Koleksiyonu [ürün](api-management-template-data-model-reference.md#Product) varlıklar.</span><span class="sxs-lookup"><span data-stu-id="20c90-131">Collection of [Product](api-management-template-data-model-reference.md#Product) entities.</span></span>|<span data-ttu-id="20c90-132">Merhaba ürünleri görünür toohello geçerli kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="20c90-132">hello products visible toohello current user.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="20c90-133">Örnek şablon verileri</span><span class="sxs-lookup"><span data-stu-id="20c90-133">Sample template data</span></span>  
  
```json  
{  
    "Paging": {  
        "Page": 1,  
        "PageSize": 10,  
        "TotalItemCount": 2,  
        "ShowAll": false,  
        "PageCount": 1  
    },  
    "Filtering": {  
        "Pattern": null,  
        "Placeholder": "Search products"  
    },  
    "Products": [  
        {  
            "Id": "56f9445ffaf7560049060001",  
            "Title": "Starter",  
            "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
            "Terms": "",  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        },  
        {  
            "Id": "56f9445ffaf7560049060002",  
            "Title": "Unlimited",  
            "Description": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",  
            "Terms": null,  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="20c90-134"><a name="Product"></a>Ürün</span><span class="sxs-lookup"><span data-stu-id="20c90-134"><a name="Product"></a> Product</span></span>  
 <span data-ttu-id="20c90-135">Merhaba **ürün** şablonu verir toocustomize hello hello ürün sayfası gövdesi hello Geliştirici Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="20c90-135">hello **Product** template allows you toocustomize hello body of hello product page in hello developer portal.</span></span>  
  
 <span data-ttu-id="20c90-136">![Geliştirici Portalı ürün sayfası](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span><span class="sxs-lookup"><span data-stu-id="20c90-136">![Developer portal product page](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="20c90-137">Varsayılan şablonu</span><span class="sxs-lookup"><span data-stu-id="20c90-137">Default template</span></span>  
  
```xml  
<h2>{{Product.Title}}</h2>  
<p>{{Product.Description}}</p>  
  
{% assign replaceString0 = '{0}' %}  
  
{% if Limits and Limits.size > 0 %}  
<h3>{% localized "ProductDetailsStrings|WebProductsUsageLimitsHeader"%}</h3>  
<ul>  
  {% for limit in Limits %}  
  <li>{{limit.DisplayName}}</li>  
  {% endfor %}  
</ul>  
{% endif %}  
  
{% if apis.size > 0 %}  
<p>  
  <b>  
    {% if apis.size == 1 %}  
    {% capture apisCountText %}{% localized "ProductDetailsStrings|TextblockSingleApisCount" %}{% endcapture %}  
    {% else %}  
    {% capture apisCountText %}{% localized "ProductDetailsStrings|TextblockMultipleApisCount" %}{% endcapture %}  
    {% endif %}  
  
    {% capture apisCount %}{{apis.size}}{% endcapture %}  
    {{ apisCountText | replace : replaceString0, apisCount }}  
  </b>  
</p>  
  
<ul>  
  {% for api in Apis %}  
  <li>  
    <a href="/docs/services/{{api.Id}}">{{api.Name}}</a>  
  </li>  
  {% endfor %}  
</ul>  
{% endif %}  
  
{% if subscriptions.size > 0 %}  
<p>  
  <b>  
    {% if subscriptions.size == 1 %}  
    {% capture subscriptionsCountText %}{% localized "ProductDetailsStrings|TextblockSingleSubscriptionsCount" %}{% endcapture %}  
    {% else %}  
    {% capture subscriptionsCountText %}{% localized "ProductDetailsStrings|TextblockMultipleSubscriptionsCount" %}{% endcapture %}  
    {% endif %}  
  
    {% capture subscriptionsCount %}{{subscriptions.size}}{% endcapture %}  
    {{ subscriptionsCountText | replace : replaceString0, subscriptionsCount }}  
  </b>  
</p>  
  
<ul>  
  {% for subscription in subscriptions %}  
  <li>  
    <a href="/developer#{{subscription.Id}}">{{subscription.DisplayName}}</a>  
  </li>  
  {% endfor %}  
</ul>  
{% endif %}  
{% if CannotAddBecauseSubscriptionNumberLimitReached %}  
<b>{% localized "ProductDetailsStrings|TextblockSubscriptionLimitReached" %}</b>  
{% elsif CannotAddBecauseMultipleSubscriptionsNotAllowed == false %}  
<subscribe-button></subscribe-button>  
{% endif %}  
```  
  
### <a name="controls"></a><span data-ttu-id="20c90-138">Denetimler</span><span class="sxs-lookup"><span data-stu-id="20c90-138">Controls</span></span>  
 <span data-ttu-id="20c90-139">Merhaba `Product list` şablonu hello aşağıdaki kullanabilir [sayfasında denetimleri](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="20c90-139">hello `Product list` template may use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="20c90-140">Abone düğmesi</span><span class="sxs-lookup"><span data-stu-id="20c90-140">subscribe-button</span></span>](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a><span data-ttu-id="20c90-141">Veri modeli</span><span class="sxs-lookup"><span data-stu-id="20c90-141">Data model</span></span>  
  
|<span data-ttu-id="20c90-142">Özellik</span><span class="sxs-lookup"><span data-stu-id="20c90-142">Property</span></span>|<span data-ttu-id="20c90-143">Tür</span><span class="sxs-lookup"><span data-stu-id="20c90-143">Type</span></span>|<span data-ttu-id="20c90-144">Açıklama</span><span class="sxs-lookup"><span data-stu-id="20c90-144">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="20c90-145">Ürün</span><span class="sxs-lookup"><span data-stu-id="20c90-145">Product</span></span>|[<span data-ttu-id="20c90-146">Ürün</span><span class="sxs-lookup"><span data-stu-id="20c90-146">Product</span></span>](api-management-template-data-model-reference.md#Product)|<span data-ttu-id="20c90-147">Belirtilen ürün Hello.</span><span class="sxs-lookup"><span data-stu-id="20c90-147">hello specified product.</span></span>|  
|<span data-ttu-id="20c90-148">IsDeveloperSubscribed</span><span class="sxs-lookup"><span data-stu-id="20c90-148">IsDeveloperSubscribed</span></span>|<span data-ttu-id="20c90-149">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="20c90-149">boolean</span></span>|<span data-ttu-id="20c90-150">Merhaba geçerli kullanıcının abone toothis ürün olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="20c90-150">Whether hello current user is subscribed toothis product.</span></span>|  
|<span data-ttu-id="20c90-151">SubscriptionState</span><span class="sxs-lookup"><span data-stu-id="20c90-151">SubscriptionState</span></span>|<span data-ttu-id="20c90-152">Sayı</span><span class="sxs-lookup"><span data-stu-id="20c90-152">number</span></span>|<span data-ttu-id="20c90-153">Merhaba abonelik Hello durumu.</span><span class="sxs-lookup"><span data-stu-id="20c90-153">hello state of hello subscription.</span></span> <span data-ttu-id="20c90-154">Olası durumlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="20c90-154">Possible states are:</span></span><br /><br /> <span data-ttu-id="20c90-155">-   `0 - suspended`– hello abonelik engellenir ve hello abone hello ürünün herhangi bir API çağrılamıyor.</span><span class="sxs-lookup"><span data-stu-id="20c90-155">-   `0 - suspended` – hello subscription is blocked, and hello subscriber cannot call any APIs of hello product.</span></span><br /><span data-ttu-id="20c90-156">-   `1 - active`– hello abonelik etkin olduğunu.</span><span class="sxs-lookup"><span data-stu-id="20c90-156">-   `1 - active` – hello subscription is active.</span></span><br /><span data-ttu-id="20c90-157">-   `2 - expired`– hello abonelik sona erme tarihini ulaştı ve devre dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="20c90-157">-   `2 - expired` – hello subscription reached its expiration date and was deactivated.</span></span><br /><span data-ttu-id="20c90-158">-   `3 - submitted`– hello abonelik isteği hello geliştirici tarafından yapılan ancak henüz onaylanamıyor veya reddedilemiyor.</span><span class="sxs-lookup"><span data-stu-id="20c90-158">-   `3 - submitted` – hello subscription request has been made by hello developer, but has not yet been approved or rejected.</span></span><br /><span data-ttu-id="20c90-159">-   `4 - rejected`– bir yönetici tarafından hello abonelik isteği reddedildi.</span><span class="sxs-lookup"><span data-stu-id="20c90-159">-   `4 - rejected` – hello subscription request has been denied by an administrator.</span></span><br /><span data-ttu-id="20c90-160">-   `5 - cancelled`– hello geliştirici veya yönetici tarafından hello aboneliği iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="20c90-160">-   `5 - cancelled` – hello subscription has been cancelled by hello developer or administrator.</span></span>|  
|<span data-ttu-id="20c90-161">Sınırlar</span><span class="sxs-lookup"><span data-stu-id="20c90-161">Limits</span></span>|<span data-ttu-id="20c90-162">Dizi</span><span class="sxs-lookup"><span data-stu-id="20c90-162">array</span></span>|<span data-ttu-id="20c90-163">Bu özellik kullanım dışıdır ve kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="20c90-163">This property is deprecated and should not be used.</span></span>|  
|<span data-ttu-id="20c90-164">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="20c90-164">DelegatedSubscriptionEnabled</span></span>|<span data-ttu-id="20c90-165">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="20c90-165">boolean</span></span>|<span data-ttu-id="20c90-166">Olup olmadığını [temsilci](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) Bu abonelik için etkin.</span><span class="sxs-lookup"><span data-stu-id="20c90-166">Whether [delegation](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) is enabled for this subscription.</span></span>|  
|<span data-ttu-id="20c90-167">DelegatedSubscriptionUrl</span><span class="sxs-lookup"><span data-stu-id="20c90-167">DelegatedSubscriptionUrl</span></span>|<span data-ttu-id="20c90-168">Dize</span><span class="sxs-lookup"><span data-stu-id="20c90-168">string</span></span>|<span data-ttu-id="20c90-169">Temsilci etkinleştirilirse, hello abonelik URL temsilci.</span><span class="sxs-lookup"><span data-stu-id="20c90-169">If delegation is enabled, hello delegated subscription URL.</span></span>|  
|<span data-ttu-id="20c90-170">IsAgreed</span><span class="sxs-lookup"><span data-stu-id="20c90-170">IsAgreed</span></span>|<span data-ttu-id="20c90-171">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="20c90-171">boolean</span></span>|<span data-ttu-id="20c90-172">Merhaba ürün koşulları varsa, olup hello geçerli kullanıcının anlaşılan toohello koşulları.</span><span class="sxs-lookup"><span data-stu-id="20c90-172">If hello product has terms, whether hello current user has agreed toohello terms.</span></span>|  
|<span data-ttu-id="20c90-173">Abonelikler</span><span class="sxs-lookup"><span data-stu-id="20c90-173">Subscriptions</span></span>|<span data-ttu-id="20c90-174">Koleksiyonu [abonelik özeti](api-management-template-data-model-reference.md#SubscriptionSummary) varlıklar.</span><span class="sxs-lookup"><span data-stu-id="20c90-174">Collection of [Subscription summary](api-management-template-data-model-reference.md#SubscriptionSummary) entities.</span></span>|<span data-ttu-id="20c90-175">Merhaba abonelikleri toohello ürün.</span><span class="sxs-lookup"><span data-stu-id="20c90-175">hello subscriptions toohello product.</span></span>|  
|<span data-ttu-id="20c90-176">API'leri</span><span class="sxs-lookup"><span data-stu-id="20c90-176">Apis</span></span>|<span data-ttu-id="20c90-177">Koleksiyonu [API](api-management-template-data-model-reference.md#API) varlıklar.</span><span class="sxs-lookup"><span data-stu-id="20c90-177">Collection of [API](api-management-template-data-model-reference.md#API) entities.</span></span>|<span data-ttu-id="20c90-178">Bu üründe Hello API'leri.</span><span class="sxs-lookup"><span data-stu-id="20c90-178">hello APIs in this product.</span></span>|  
|<span data-ttu-id="20c90-179">CannotAddBecauseSubscriptionNumberLimitReached</span><span class="sxs-lookup"><span data-stu-id="20c90-179">CannotAddBecauseSubscriptionNumberLimitReached</span></span>|<span data-ttu-id="20c90-180">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="20c90-180">boolean</span></span>|<span data-ttu-id="20c90-181">Merhaba geçerli kullanıcı uygun toosubscribe toothis ürün şekilde toohello abonelik sınırına sahip olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="20c90-181">Whether hello current user is eligible toosubscribe toothis product with regard toohello subscription limit.</span></span>|  
|<span data-ttu-id="20c90-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span><span class="sxs-lookup"><span data-stu-id="20c90-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span></span>|<span data-ttu-id="20c90-183">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="20c90-183">boolean</span></span>|<span data-ttu-id="20c90-184">Merhaba geçerli kullanıcı uygun toosubscribe toothis şekilde toomultiple abonelikleri veya izin verilmeden ürünle olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="20c90-184">Whether hello current user is eligible toosubscribe toothis product with regard toomultiple subscriptions being allowed or not.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="20c90-185">Örnek şablon verileri</span><span class="sxs-lookup"><span data-stu-id="20c90-185">Sample template data</span></span>  
  
```json  
{  
    "Product": {  
        "Id": "56f9445ffaf7560049060001",  
        "Title": "Starter",  
        "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",  
        "Terms": "",  
        "ProductState": 1,  
        "AllowMultipleSubscriptions": false,  
        "MultipleSubscriptionsCount": 1  
    },  
    "IsDeveloperSubscribed": true,  
    "SubscriptionState": 1,  
    "Limits": [],  
    "DelegatedSubscriptionEnabled": false,  
    "DelegatedSubscriptionUrl": null,  
    "IsAgreed": false,  
    "Subscriptions": [  
        {  
            "Id": "56f9445ffaf7560049070001",  
            "DisplayName": "Starter  (default)"  
        }  
    ],  
    "Apis": [  
        {  
            "id": "56f9445ffaf7560049040001",  
            "name": "Echo API",  
            "description": null,  
            "serviceUrl": "http://echoapi.cloudapp.net/api",  
            "path": "echo",  
            "protocols": [  
                2  
            ],  
            "authenticationSettings": null,  
            "subscriptionKeyParameterNames": null  
        }  
    ],  
    "CannotAddBecauseSubscriptionNumberLimitReached": false,  
    "CannotAddBecauseMultipleSubscriptionsNotAllowed": true  
}  
```

## <a name="next-steps"></a><span data-ttu-id="20c90-186">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="20c90-186">Next steps</span></span>
<span data-ttu-id="20c90-187">Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [nasıl toocustomize hello şablonları kullanarak API Management Geliştirici Portalı](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="20c90-187">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
