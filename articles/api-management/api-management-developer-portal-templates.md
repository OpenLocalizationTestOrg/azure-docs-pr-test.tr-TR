---
title: "şablonları kullanarak aaaCustomize hello API Management Geliştirici Portalı-Azure | Microsoft Docs"
description: "Nasıl toocustomize hello Azure API Management Geliştirici Portalı şablonları kullanma hakkında bilgi edinin."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: a195675b-f7d0-4fc9-90bf-860e6f17ccf7
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: b00d5f1534e9466f30ff3920e7aae048feb8b8c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-hello-azure-api-management-developer-portal-using-templates"></a>Nasıl toocustomize hello Azure API Management Geliştirici Portalı şablonlarını kullanma

Azure API Management'te üç temel şekilde toocustomize hello Geliştirici Portalı vardır:

* [Statik sayfaları ve sayfa düzeni öğelerini Hello içeriğini düzenleme][modify-content-layout]
* [Merhaba Geliştirici Portalı sayfası öğeleri için kullanılan güncelleştirme hello stilleri][customize-styles]
* [Merhaba portal tarafından oluşturulan sayfalar için kullanılan hello şablonları değiştirmek] [ portal-templates] (Bu kılavuzda açıklanan)

Sistem tarafından oluşturulan Geliştirici portal sayfalarına (örneğin API belgeleri, ürünler, kullanıcı kimlik doğrulaması, vb.) içerik kullanılan toocustomize hello şablonlarıdır. Kullanarak [DotLiquid](http://dotliquidmarkup.org/) sözdizimi ve yerelleştirilmiş dize kaynakları, simgeler ve sayfa denetimleri, sağlanan bir dizi uygun gördüğünüz şekilde hello sayfaların büyük esneklik tooconfigure hello içeriğe sahip.

## <a name="developer-portal-templates-overview"></a>Geliştirici Portalı şablonlarına genel bakış
Şablonları düzenleme hello yapılır **Geliştirici Portalı** yönetici olarak oturum açmış oluştu. tooget var. önce hello Azure Portal açın ve tıklatın **yayımcı portalına** , API Management örneğinin hello hizmet araç çubuğundan.

![Yayımcı portalı][api-management-management-console]

Tıklayın **Geliştirici Portalı** hello sağ üst üzerinde. 

![Geliştirici portal menüsü][api-management-developer-portal-menu]

tooaccess Geliştirici Portalı şablonları Merhaba, hello tıklatın hello sol toodisplay hello özelleştirme menüsündeki simgesini özelleştirmek ve tıklayın **şablonları**.

![Geliştirici Portalı şablonları][api-management-customize-menu]

Merhaba şablonları listesini hello Geliştirici Portalı farklı sayfalarında hello kapsayan şablonlarının çeşitli kategorileri görüntüler. Her şablon farklıdır ancak hello adımları tooedit bunları ve yayımlama hello değişiklikleri olan, hello aynı. tooedit bir şablon hello hello şablonunun adını tıklatın.

![Geliştirici Portalı şablonları][api-management-templates-menu]

Bir şablon tıklamak Bu şablon tarafından özelleştirilebilir toohello Geliştirici portal sayfası götürür. Bu örnek hello içinde **ürün listesi** şablonu görüntülenir. Merhaba **ürün listesi** şablonu denetimleri hello hello ekranının hello kırmızı dikdörtgeni tarafından belirtilen alan. 

![Ürün şablonu listesi][api-management-developer-portal-templates-overview]

Hello gibi bazı şablonlar **kullanıcı profili** şablonlarını özelleştirme hello farklı kısımlarını aynı sayfa. 

![Kullanıcı profil şablonları][api-management-user-profile-templates]

Her Geliştirici Portalı şablonu için başlangıç Düzenleyicisi hello sayfasının hello altında görüntülenen iki bölümü vardır. Merhaba taraftaki hello bölmesini hello şablonu için düzenleme ve hello sağ taraftaki hello veri modeli hello şablonu için görüntüler. 

Merhaba Şablon bölmesinde düzenleme hello görünümünü ve davranışını hello Geliştirici Portalı'nda hello karşılık gelen sayfasının denetimleri hello biçimlendirme içeriyor. hello şablon Hello biçimlendirmede kullanan hello [DotLiquid](http://dotliquidmarkup.org/) sözdizimi. Bir popüler düzenleyicisidir DotLiquid için [DotLiquid tasarımcıları için](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers). Düzenleme sırasında herhangi bir yapılan değişiklikler toohello şablonu görüntülenir, hello tarayıcıda, ancak görünür tooyour müşteriler dek gerçek zamanlı [kaydetmek](#to-save-a-template) ve [yayımlama](#to-publish-a-template) hello şablonu.

![Şablon biçimlendirme][api-management-template]

Merhaba **şablon verileri** bölmesi toohello veri bir kılavuz sağlar belirli bir şablon kullanmak için kullanılabilir hello varlıklar için model. Bu kılavuz, şu anda hello Geliştirici Portalı'nda görüntülenen hello canlı verileri görüntüleyerek sağlar. Merhaba dikdörtgen hello hello sağ üst köşesindeki tıklayarak hello şablon bölmeleri genişletebilirsiniz **şablon verileri** bölmesi.

![Şablon veri modeli][api-management-template-data]

Merhaba önceki örnekte hello görüntülenen hello veri alındı hello Geliştirici Portalı'nda görüntülenen iki ürün yok **şablon verileri** hello aşağıdaki örnekte gösterildiği gibi bölmesi.

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
            "Id": "56ec64c380ed850042060001",
            "Title": "Starter",
            "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",
            "Terms": "",
            "ProductState": 1,
            "AllowMultipleSubscriptions": false,
            "MultipleSubscriptionsCount": 1
        },
        {
            "Id": "56ec64c380ed850042060002",
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

Merhaba Hello biçimlendirmede **ürün listesi** şablon işlemleri ürünleri toodisplay bilgileri ve bağlantı tooeach bireysel ürün hello toplulukta yineleme tarafından veri tooprovide hello istenen çıkış hello. Not hello `<search-control>` ve `<page-control>` hello biçimlendirme öğeleri. Bu, arama ve disk belleği'hello sayfadaki denetimleri hello hello görünümünü denetler. `ProductsStrings|PageTitleProducts`Merhaba içeren bir yerelleştirilmiş dize başvuru `h2` hello sayfa için üstbilgi metni. Dize kaynakları, sayfa denetimleri ve simgeleri Geliştirici Portalı şablonlarındaki kullanıma listesi için bkz [API Management Geliştirici Portalı şablonları başvurusu](api-management-developer-portal-templates-reference.md).

```html
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

## <a name="toosave-a-template"></a>toosave bir şablonu
toosave bir şablon tıklatın kaydetme hello Şablon Düzenleyicisi'nde.

![Şablonu kaydetme][api-management-save-template]

Bunlar yayımlanan kadar değişiklikleri kaydedildi hello Geliştirici Portalı'nda Canlı değildir.

## <a name="toopublish-a-template"></a>toopublish bir şablonu
Tek tek veya birlikte kaydedilen şablonları yayımlanabilir. toopublish tek tek bir şablon, yayınla hello Şablon Düzenleyicisi'nde ' yı tıklatın.

![Yayın şablonu][api-management-publish-template]

Tıklatın **Evet** tooconfirm ve hello şablon hello Geliştirici portalında Canlı.

![Onayla yayımlama][api-management-publish-template-confirm]

toopublish olan tüm yayımlanmamış şablonu sürümleri, tıklatın **Yayımla** hello şablonları listesinde. Yayımdan şablonları hello şablonu adından bir yıldız işaretiyle belirtilir. Bu örnekte, hello **ürün listesi** ve **ürün** şablonları yayımlanır.

![Şablonlarını yayınlama][api-management-publish-templates]

Tıklatın **özelleştirmeleri yayımlamak** tooconfirm.

![Onayla yayımlama][api-management-publish-customizations]

Yeni yayımlanan şablonların hemen hello Geliştirici Portalı'nda etkili olur.

## <a name="toorevert-a-template-toohello-previous-version"></a>toorevert şablon toohello önceki bir sürümü
Şablon toohello önceki yayımlanmış bir sürüm toorevert, tıklatın hello Şablon Düzenleyicisi'nde geri dönün.

![Şablon geri][api-management-revert-template]

Tıklatın **Evet** tooconfirm.

![Onayla][api-management-revert-template-confirm]

daha önce yayımlanmış bir sürüm bir şablon hello geri sonra işlem hello Geliştirici Portalı'nda Canlı hello tamamlanır.

## <a name="toorestore-a-template-toohello-default-version"></a>toorestore şablon toohello varsayılan sürümü
Geri yükleme şablonları tootheir varsayılan sürüm iki adımlı bir işlemdir. İlk hello şablonları geri gerekir ve ardından geri hello sürümleri yayımlanması gerekir.

toorestore tek şablonu toohello varsayılan sürümü hello şablonu Düzenleyicisi'ni geri yükleme'yi tıklatın.

![Şablon geri][api-management-reset-template]

Tıklatın **Evet** tooconfirm.

![Onayla][api-management-reset-template-confirm]

Tüm Şablonları tootheir varsayılan sürümler, toorestore tıklatın **geri varsayılan şablonları** hello şablon listesinde.

![Şablonları geri yükleme][api-management-restore-templates]

Merhaba geri yüklenen şablonları sonra ayrı ayrı veya tümünü bir defada hello adımları izleyerek yayımlanmalıdır [toopublish bir şablon](#to-publish-a-template).

## <a name="next-steps"></a>Sonraki adımlar
Geliştirici Portalı şablonları, dize kaynaklarını, simgeler ve sayfa denetimleri için başvuru bilgileri için bkz: [API Management Geliştirici Portalı şablonları başvurusu](api-management-developer-portal-templates-reference.md).

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[api-management-customize-menu]: ./media/api-management-developer-portal-templates/api-management-customize-menu.png
[api-management-templates-menu]: ./media/api-management-developer-portal-templates/api-management-templates-menu.png
[api-management-developer-portal-templates-overview]: ./media/api-management-developer-portal-templates/api-management-developer-portal-templates-overview.png
[api-management-template]: ./media/api-management-developer-portal-templates/api-management-template.png
[api-management-template-data]: ./media/api-management-developer-portal-templates/api-management-template-data.png
[api-management-developer-portal-menu]: ./media/api-management-developer-portal-templates/api-management-developer-portal-menu.png
[api-management-management-console]: ./media/api-management-developer-portal-templates/api-management-management-console.png
[api-management-browse]: ./media/api-management-developer-portal-templates/api-management-browse.png
[api-management-user-profile-templates]: ./media/api-management-developer-portal-templates/api-management-user-profile-templates.png
[api-management-save-template]: ./media/api-management-developer-portal-templates/api-management-save-template.png
[api-management-publish-template]: ./media/api-management-developer-portal-templates/api-management-publish-template.png
[api-management-publish-template-confirm]: ./media/api-management-developer-portal-templates/api-management-publish-template-confirm.png
[api-management-publish-templates]: ./media/api-management-developer-portal-templates/api-management-publish-templates.png
[api-management-publish-customizations]: ./media/api-management-developer-portal-templates/api-management-publish-customizations.png
[api-management-revert-template]: ./media/api-management-developer-portal-templates/api-management-revert-template.png
[api-management-revert-template-confirm]: ./media/api-management-developer-portal-templates/api-management-revert-template-confirm.png
[api-management-reset-template]: ./media/api-management-developer-portal-templates/api-management-reset-template.png
[api-management-reset-template-confirm]: ./media/api-management-developer-portal-templates/api-management-reset-template-confirm.png
[api-management-restore-templates]: ./media/api-management-developer-portal-templates/api-management-restore-templates.png







