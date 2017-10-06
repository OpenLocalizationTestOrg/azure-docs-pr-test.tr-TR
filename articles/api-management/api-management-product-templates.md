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
# <a name="product-templates-in-azure-api-management"></a>Azure API Management'te ürün şablonları
Azure API Management yeteneği toocustomize hello Geliştirici portal sayfalarına içeriklerini yapılandırma şablonları kümesini kullanarak içeriğini hello sağlar. Kullanarak [DotLiquid](http://dotliquidmarkup.org/) sözdizimi ve hello düzenleyiciyi, gibi [tasarımcıları için DotLiquid](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), ve sağlanan bir dizi yerelleştirilmiş [dize kaynakları](api-management-template-resources.md#strings), [ Karakter kaynakları](api-management-template-resources.md#glyphs), ve [sayfasında denetimleri](api-management-page-controls.md), bu şablonları kullanarak uygun gördüğünüz şekilde hello sayfaların büyük esneklik tooconfigure hello içeriğe sahip.  
  
 Bu bölümdeki Hello şablonları hello Geliştirici Portalı'nda hello ürün sayfaları toocustomize hello içeriği sağlar.  
  
-   [Ürün Listesi](#ProductList)  
  
-   [Ürün](#Product)  
  
> [!NOTE]
>  Örnek varsayılan şablonları belgelerine aşağıdaki hello dahil olan, ancak konu toochange toocontinuous geliştirmeler nedeniyle. İstenen toohello tek tek şablonları giderek hello Canlı varsayılan şablonları hello Geliştirici Portalı'nda görüntüleyebilirsiniz. Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [nasıl toocustomize hello şablonları kullanarak API Management Geliştirici Portalı](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).  
  
##  <a name="ProductList"></a>Ürün Listesi  
 Merhaba **ürün listesi** şablonu verir hello ürün listesi sayfasının toocustomize hello gövdesi hello Geliştirici Portalı'nda.  
  
 ![Ürün listesini](./media/api-management-product-templates/APIM_ProductsListTemplatePage.png "APIM_ProductsListTemplatePage")  
  
### <a name="default-template"></a>Varsayılan şablonu  
  
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
  
### <a name="controls"></a>Denetimler  
 Merhaba `Product list` şablonu hello aşağıdaki kullanabilir [sayfasında denetimleri](api-management-page-controls.md).  
  
-   [disk belleği denetimi](api-management-page-controls.md#paging-control)  
  
-   [arama denetimi](api-management-page-controls.md#search-control)  
  
### <a name="data-model"></a>Veri modeli  
  
|Özellik|Tür|Açıklama|  
|--------------|----------|-----------------|  
|Sayfalama|[Disk belleği](api-management-template-data-model-reference.md#Paging) varlık.|Merhaba ürünleri koleksiyonu için başlangıç disk belleği bilgilerini.|  
|Filtreleme|[Filtreleme](api-management-template-data-model-reference.md#Filtering) varlık.|Merhaba ürün listesi sayfası için filtre bilgilerini hello.|  
|Ürünler|Koleksiyonu [ürün](api-management-template-data-model-reference.md#Product) varlıklar.|Merhaba ürünleri görünür toohello geçerli kullanıcı.|  
  
### <a name="sample-template-data"></a>Örnek şablon verileri  
  
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
  
##  <a name="Product"></a>Ürün  
 Merhaba **ürün** şablonu verir toocustomize hello hello ürün sayfası gövdesi hello Geliştirici Portalı'nda.  
  
 ![Geliştirici Portalı ürün sayfası](./media/api-management-product-templates/APIM_ProductPage.png "APIM_ProductPage")  
  
### <a name="default-template"></a>Varsayılan şablonu  
  
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
  
### <a name="controls"></a>Denetimler  
 Merhaba `Product list` şablonu hello aşağıdaki kullanabilir [sayfasında denetimleri](api-management-page-controls.md).  
  
-   [Abone düğmesi](api-management-page-controls.md#subscribe-button)  
  
### <a name="data-model"></a>Veri modeli  
  
|Özellik|Tür|Açıklama|  
|--------------|----------|-----------------|  
|Ürün|[Ürün](api-management-template-data-model-reference.md#Product)|Belirtilen ürün Hello.|  
|IsDeveloperSubscribed|Boole değeri|Merhaba geçerli kullanıcının abone toothis ürün olup olmadığı.|  
|SubscriptionState|Sayı|Merhaba abonelik Hello durumu. Olası durumlar şunlardır:<br /><br /> -   `0 - suspended`– hello abonelik engellenir ve hello abone hello ürünün herhangi bir API çağrılamıyor.<br />-   `1 - active`– hello abonelik etkin olduğunu.<br />-   `2 - expired`– hello abonelik sona erme tarihini ulaştı ve devre dışı bırakıldı.<br />-   `3 - submitted`– hello abonelik isteği hello geliştirici tarafından yapılan ancak henüz onaylanamıyor veya reddedilemiyor.<br />-   `4 - rejected`– bir yönetici tarafından hello abonelik isteği reddedildi.<br />-   `5 - cancelled`– hello geliştirici veya yönetici tarafından hello aboneliği iptal edildi.|  
|Sınırlar|Dizi|Bu özellik kullanım dışıdır ve kullanılmamalıdır.|  
|DelegatedSubscriptionEnabled|Boole değeri|Olup olmadığını [temsilci](https://azure.microsoft.com/documentation/articles/api-management-howto-setup-delegation/) Bu abonelik için etkin.|  
|DelegatedSubscriptionUrl|Dize|Temsilci etkinleştirilirse, hello abonelik URL temsilci.|  
|IsAgreed|Boole değeri|Merhaba ürün koşulları varsa, olup hello geçerli kullanıcının anlaşılan toohello koşulları.|  
|Abonelikler|Koleksiyonu [abonelik özeti](api-management-template-data-model-reference.md#SubscriptionSummary) varlıklar.|Merhaba abonelikleri toohello ürün.|  
|API'leri|Koleksiyonu [API](api-management-template-data-model-reference.md#API) varlıklar.|Bu üründe Hello API'leri.|  
|CannotAddBecauseSubscriptionNumberLimitReached|Boole değeri|Merhaba geçerli kullanıcı uygun toosubscribe toothis ürün şekilde toohello abonelik sınırına sahip olup olmadığı.|  
|CannotAddBecauseMultipleSubscriptionsNotAllowed|Boole değeri|Merhaba geçerli kullanıcı uygun toosubscribe toothis şekilde toomultiple abonelikleri veya izin verilmeden ürünle olup olmadığı.|  
  
### <a name="sample-template-data"></a>Örnek şablon verileri  
  
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

## <a name="next-steps"></a>Sonraki adımlar
Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [nasıl toocustomize hello şablonları kullanarak API Management Geliştirici Portalı](api-management-developer-portal-templates.md).
