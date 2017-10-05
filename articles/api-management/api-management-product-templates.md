---
title: "Azure API Management'te ürün şablonları | Microsoft Docs"
description: "Azure API Management Geliştirici Portalı ürün sayfalarında içeriğini özelleştirmeyi öğrenin."
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
ms.openlocfilehash: 9ddbb9860b437cb3e7334bdf5891f2fba1cffb76
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="product-templates-in-azure-api-management"></a><span data-ttu-id="7a03e-103">Azure API Management'te ürün şablonları</span><span class="sxs-lookup"><span data-stu-id="7a03e-103">Product templates in Azure API Management</span></span>
<span data-ttu-id="7a03e-104">Azure API Management Geliştirici portal sayfalarına içeriklerini yapılandırma şablonları kümesini kullanarak içeriği özelleştirme yeteneği sağlar.</span><span class="sxs-lookup"><span data-stu-id="7a03e-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="7a03e-105">Kullanarak [DotLiquid](http://dotliquidmarkup.org/) sözdizimi ve düzenleyiciyi, gibi [DotLiquid tasarımcıları için](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), ve sağlanan bir dizi yerelleştirilmiş [dize kaynakları](api-management-template-resources.md#strings), [karakter kaynakları](api-management-template-resources.md#glyphs), ve [sayfa denetimleri](api-management-page-controls.md), bu şablonları kullanarak uygun gördüğünüz şekilde sayfaların yapılandırmak için büyük esneklik vardır.</span><span class="sxs-lookup"><span data-stu-id="7a03e-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="7a03e-106">Bu bölümdeki şablonları Geliştirici Portalı ürün sayfalarında içeriğini özelleştirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="7a03e-106">The templates in this section allow you to customize the content of the product pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="7a03e-107">Ürün Listesi</span><span class="sxs-lookup"><span data-stu-id="7a03e-107">Product list</span></span>](#ProductList)  
  
-   [<span data-ttu-id="7a03e-108">Ürün</span><span class="sxs-lookup"><span data-stu-id="7a03e-108">Product</span></span>](#Product)  
  
> [!NOTE]
>  <span data-ttu-id="7a03e-109">Örnek varsayılan şablonları aşağıdaki belgelerde yer alır ancak değişikliği sürekli geliştirmeler nedeniyle tabidir.</span><span class="sxs-lookup"><span data-stu-id="7a03e-109">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="7a03e-110">İstenen tek tek şablonları giderek Geliştirici Portalı'nda Canlı varsayılan şablonları görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a03e-110">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="7a03e-111">Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [şablonları kullanarak API Management Geliştirici Portalı nasıl özelleştireceğinizi](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="7a03e-111">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="7a03e-112"><a name="ProductList"></a>Ürün Listesi</span><span class="sxs-lookup"><span data-stu-id="7a03e-112"><a name="ProductList"></a> Product list</span></span>  
 <span data-ttu-id="7a03e-113">**Ürün listesi** şablonu Geliştirici portalında ürün listesi sayfasının gövdesi özelleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7a03e-113">The **Product list** template allows you to customize the body of the product list page in the developer portal.</span></span>  
  
 <span data-ttu-id="7a03e-114">![Ürün listesini](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span><span class="sxs-lookup"><span data-stu-id="7a03e-114">![Products list](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="7a03e-115">Varsayılan şablonu</span><span class="sxs-lookup"><span data-stu-id="7a03e-115">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="7a03e-116">Denetimler</span><span class="sxs-lookup"><span data-stu-id="7a03e-116">Controls</span></span>  
 <span data-ttu-id="7a03e-117">`Product list` Şablonu, aşağıdaki kullanabilir [sayfasında denetimleri](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="7a03e-117">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="7a03e-118">disk belleği denetimi</span><span class="sxs-lookup"><span data-stu-id="7a03e-118">paging-control</span></span>](api-management-page-controls.md#paging-control)  
  
-   [<span data-ttu-id="7a03e-119">arama denetimi</span><span class="sxs-lookup"><span data-stu-id="7a03e-119">search-control</span></span>](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a><span data-ttu-id="7a03e-120">Veri modeli</span><span class="sxs-lookup"><span data-stu-id="7a03e-120">Data model</span></span>  
  
|<span data-ttu-id="7a03e-121">Özellik</span><span class="sxs-lookup"><span data-stu-id="7a03e-121">Property</span></span>|<span data-ttu-id="7a03e-122">Tür</span><span class="sxs-lookup"><span data-stu-id="7a03e-122">Type</span></span>|<span data-ttu-id="7a03e-123">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7a03e-123">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="7a03e-124">Sayfalama</span><span class="sxs-lookup"><span data-stu-id="7a03e-124">Paging</span></span>|<span data-ttu-id="7a03e-125">[Disk belleği](api-management-template-data-model-reference.md#Paging) varlık.</span><span class="sxs-lookup"><span data-stu-id="7a03e-125">[Paging](api-management-template-data-model-reference.md#Paging) entity.</span></span>|<span data-ttu-id="7a03e-126">Ürünler koleksiyonu için disk belleği bilgileri.</span><span class="sxs-lookup"><span data-stu-id="7a03e-126">The paging information for the products collection.</span></span>|  
|<span data-ttu-id="7a03e-127">Filtreleme</span><span class="sxs-lookup"><span data-stu-id="7a03e-127">Filtering</span></span>|<span data-ttu-id="7a03e-128">[Filtreleme](api-management-template-data-model-reference.md#Filtering) varlık.</span><span class="sxs-lookup"><span data-stu-id="7a03e-128">[Filtering](api-management-template-data-model-reference.md#Filtering) entity.</span></span>|<span data-ttu-id="7a03e-129">Ürün Listesi Sayfası için filtre bilgileri.</span><span class="sxs-lookup"><span data-stu-id="7a03e-129">The filtering information for the products list page.</span></span>|  
|<span data-ttu-id="7a03e-130">Ürünler</span><span class="sxs-lookup"><span data-stu-id="7a03e-130">Products</span></span>|<span data-ttu-id="7a03e-131">Koleksiyonu [ürün](api-management-template-data-model-reference.md#Product) varlıklar.</span><span class="sxs-lookup"><span data-stu-id="7a03e-131">Collection of [Product](api-management-template-data-model-reference.md#Product) entities.</span></span>|<span data-ttu-id="7a03e-132">Geçerli kullanıcı için görünür olan ürünleri.</span><span class="sxs-lookup"><span data-stu-id="7a03e-132">The products visible to the current user.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="7a03e-133">Örnek şablon verileri</span><span class="sxs-lookup"><span data-stu-id="7a03e-133">Sample template data</span></span>  
  
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
            "Description": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
            "Terms": "",  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        },  
        {  
            "Id": "56f9445ffaf7560049060002",  
            "Title": "Unlimited",  
            "Description": "Subscribers have completely unlimited access to the API. Administrator approval is required.",  
            "Terms": null,  
            "ProductState": 1,  
            "AllowMultipleSubscriptions": false,  
            "MultipleSubscriptionsCount": 1  
        }  
    ]  
}  
```  
  
##  <span data-ttu-id="7a03e-134"><a name="Product"></a>Ürün</span><span class="sxs-lookup"><span data-stu-id="7a03e-134"><a name="Product"></a> Product</span></span>  
 <span data-ttu-id="7a03e-135">**Ürün** şablonu Geliştirici portalında ürün sayfasının gövdesi özelleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7a03e-135">The **Product** template allows you to customize the body of the product page in the developer portal.</span></span>  
  
 <span data-ttu-id="7a03e-136">![Geliştirici Portalı ürün sayfası](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span><span class="sxs-lookup"><span data-stu-id="7a03e-136">![Developer portal product page](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="7a03e-137">Varsayılan şablonu</span><span class="sxs-lookup"><span data-stu-id="7a03e-137">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="7a03e-138">Denetimler</span><span class="sxs-lookup"><span data-stu-id="7a03e-138">Controls</span></span>  
 <span data-ttu-id="7a03e-139">`Product list` Şablonu, aşağıdaki kullanabilir [sayfasında denetimleri](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="7a03e-139">The `Product list` template may use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="7a03e-140">Abone düğmesi</span><span class="sxs-lookup"><span data-stu-id="7a03e-140">subscribe-button</span></span>](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a><span data-ttu-id="7a03e-141">Veri modeli</span><span class="sxs-lookup"><span data-stu-id="7a03e-141">Data model</span></span>  
  
|<span data-ttu-id="7a03e-142">Özellik</span><span class="sxs-lookup"><span data-stu-id="7a03e-142">Property</span></span>|<span data-ttu-id="7a03e-143">Tür</span><span class="sxs-lookup"><span data-stu-id="7a03e-143">Type</span></span>|<span data-ttu-id="7a03e-144">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7a03e-144">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="7a03e-145">Ürün</span><span class="sxs-lookup"><span data-stu-id="7a03e-145">Product</span></span>|[<span data-ttu-id="7a03e-146">Ürün</span><span class="sxs-lookup"><span data-stu-id="7a03e-146">Product</span></span>](api-management-template-data-model-reference.md#Product)|<span data-ttu-id="7a03e-147">Belirtilen ürün.</span><span class="sxs-lookup"><span data-stu-id="7a03e-147">The specified product.</span></span>|  
|<span data-ttu-id="7a03e-148">IsDeveloperSubscribed</span><span class="sxs-lookup"><span data-stu-id="7a03e-148">IsDeveloperSubscribed</span></span>|<span data-ttu-id="7a03e-149">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="7a03e-149">boolean</span></span>|<span data-ttu-id="7a03e-150">Olup geçerli kullanıcının bu ürüne abone olur.</span><span class="sxs-lookup"><span data-stu-id="7a03e-150">Whether the current user is subscribed to this product.</span></span>|  
|<span data-ttu-id="7a03e-151">SubscriptionState</span><span class="sxs-lookup"><span data-stu-id="7a03e-151">SubscriptionState</span></span>|<span data-ttu-id="7a03e-152">Sayı</span><span class="sxs-lookup"><span data-stu-id="7a03e-152">number</span></span>|<span data-ttu-id="7a03e-153">Abonelik durumu.</span><span class="sxs-lookup"><span data-stu-id="7a03e-153">The state of the subscription.</span></span> <span data-ttu-id="7a03e-154">Olası durumlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="7a03e-154">Possible states are:</span></span><br /><br /> <span data-ttu-id="7a03e-155">-   `0 - suspended`– Abonelik engellenir ve abone ürünün herhangi bir API çağrılamaz.</span><span class="sxs-lookup"><span data-stu-id="7a03e-155">-   `0 - suspended` – the subscription is blocked, and the subscriber cannot call any APIs of the product.</span></span><br /><span data-ttu-id="7a03e-156">-   `1 - active`– Aboneliğinizin etkin olduğunu.</span><span class="sxs-lookup"><span data-stu-id="7a03e-156">-   `1 - active` – the subscription is active.</span></span><br /><span data-ttu-id="7a03e-157">-   `2 - expired`– Abonelik sona erme tarihini ulaştı ve devre dışı bırakıldı.</span><span class="sxs-lookup"><span data-stu-id="7a03e-157">-   `2 - expired` – the subscription reached its expiration date and was deactivated.</span></span><br /><span data-ttu-id="7a03e-158">-   `3 - submitted`– Abonelik isteğinin geliştirici tarafından yapılan ancak henüz onaylanamıyor veya reddedilemiyor.</span><span class="sxs-lookup"><span data-stu-id="7a03e-158">-   `3 - submitted` – the subscription request has been made by the developer, but has not yet been approved or rejected.</span></span><br /><span data-ttu-id="7a03e-159">-   `4 - rejected`– Abonelik isteğinin bir yönetici tarafından reddedildi.</span><span class="sxs-lookup"><span data-stu-id="7a03e-159">-   `4 - rejected` – the subscription request has been denied by an administrator.</span></span><br /><span data-ttu-id="7a03e-160">-   `5 - cancelled`– Abonelik geliştirici veya yönetici tarafından iptal edildi.</span><span class="sxs-lookup"><span data-stu-id="7a03e-160">-   `5 - cancelled` – the subscription has been cancelled by the developer or administrator.</span></span>|  
|<span data-ttu-id="7a03e-161">Sınırlar</span><span class="sxs-lookup"><span data-stu-id="7a03e-161">Limits</span></span>|<span data-ttu-id="7a03e-162">Dizi</span><span class="sxs-lookup"><span data-stu-id="7a03e-162">array</span></span>|<span data-ttu-id="7a03e-163">Bu özellik kullanım dışıdır ve kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="7a03e-163">This property is deprecated and should not be used.</span></span>|  
|<span data-ttu-id="7a03e-164">DelegatedSubscriptionEnabled</span><span class="sxs-lookup"><span data-stu-id="7a03e-164">DelegatedSubscriptionEnabled</span></span>|<span data-ttu-id="7a03e-165">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="7a03e-165">boolean</span></span>|<span data-ttu-id="7a03e-166">Olup olmadığını [temsilci](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) Bu abonelik için etkin.</span><span class="sxs-lookup"><span data-stu-id="7a03e-166">Whether [delegation](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) is enabled for this subscription.</span></span>|  
|<span data-ttu-id="7a03e-167">DelegatedSubscriptionUrl</span><span class="sxs-lookup"><span data-stu-id="7a03e-167">DelegatedSubscriptionUrl</span></span>|<span data-ttu-id="7a03e-168">Dize</span><span class="sxs-lookup"><span data-stu-id="7a03e-168">string</span></span>|<span data-ttu-id="7a03e-169">Temsilci etkinleştirilirse, yetkilendirilmiş abonelik URL.</span><span class="sxs-lookup"><span data-stu-id="7a03e-169">If delegation is enabled, the delegated subscription URL.</span></span>|  
|<span data-ttu-id="7a03e-170">IsAgreed</span><span class="sxs-lookup"><span data-stu-id="7a03e-170">IsAgreed</span></span>|<span data-ttu-id="7a03e-171">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="7a03e-171">boolean</span></span>|<span data-ttu-id="7a03e-172">Olup ürün koşulları varsa, geçerli kullanıcının koşullarını kabul etmiştir.</span><span class="sxs-lookup"><span data-stu-id="7a03e-172">If the product has terms, whether the current user has agreed to the terms.</span></span>|  
|<span data-ttu-id="7a03e-173">Abonelikler</span><span class="sxs-lookup"><span data-stu-id="7a03e-173">Subscriptions</span></span>|<span data-ttu-id="7a03e-174">Koleksiyonu [abonelik özeti](api-management-template-data-model-reference.md#SubscriptionSummary) varlıklar.</span><span class="sxs-lookup"><span data-stu-id="7a03e-174">Collection of [Subscription summary](api-management-template-data-model-reference.md#SubscriptionSummary) entities.</span></span>|<span data-ttu-id="7a03e-175">Ürün abonelikleri.</span><span class="sxs-lookup"><span data-stu-id="7a03e-175">The subscriptions to the product.</span></span>|  
|<span data-ttu-id="7a03e-176">API'leri</span><span class="sxs-lookup"><span data-stu-id="7a03e-176">Apis</span></span>|<span data-ttu-id="7a03e-177">Koleksiyonu [API](api-management-template-data-model-reference.md#API) varlıklar.</span><span class="sxs-lookup"><span data-stu-id="7a03e-177">Collection of [API](api-management-template-data-model-reference.md#API) entities.</span></span>|<span data-ttu-id="7a03e-178">Bu ürüne API.</span><span class="sxs-lookup"><span data-stu-id="7a03e-178">The APIs in this product.</span></span>|  
|<span data-ttu-id="7a03e-179">CannotAddBecauseSubscriptionNumberLimitReached</span><span class="sxs-lookup"><span data-stu-id="7a03e-179">CannotAddBecauseSubscriptionNumberLimitReached</span></span>|<span data-ttu-id="7a03e-180">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="7a03e-180">boolean</span></span>|<span data-ttu-id="7a03e-181">Geçerli kullanıcının abonelik sınırı açısından bu ürüne abone olmak uygun olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="7a03e-181">Whether the current user is eligible to subscribe to this product with regard to the subscription limit.</span></span>|  
|<span data-ttu-id="7a03e-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span><span class="sxs-lookup"><span data-stu-id="7a03e-182">CannotAddBecauseMultipleSubscriptionsNotAllowed</span></span>|<span data-ttu-id="7a03e-183">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="7a03e-183">boolean</span></span>|<span data-ttu-id="7a03e-184">Geçerli kullanıcının bu ürünü veya izin verilmeden birden çok abonelik ile abone olmak uygun olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="7a03e-184">Whether the current user is eligible to subscribe to this product with regard to multiple subscriptions being allowed or not.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="7a03e-185">Örnek şablon verileri</span><span class="sxs-lookup"><span data-stu-id="7a03e-185">Sample template data</span></span>  
  
```json  
{  
    "Product": {  
        "Id": "56f9445ffaf7560049060001",  
        "Title": "Starter",  
        "Description": "Subscribers will be able to run 5 calls/minute up to a maximum of 100 calls/week.",  
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

## <a name="next-steps"></a><span data-ttu-id="7a03e-186">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7a03e-186">Next steps</span></span>
<span data-ttu-id="7a03e-187">Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [şablonları kullanarak API Management Geliştirici Portalı nasıl özelleştireceğinizi](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7a03e-187">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>