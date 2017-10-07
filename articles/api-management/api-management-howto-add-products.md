---
title: "aaaHow toocreate ürün ve Azure API Management'te yayımlama"
description: "Bilgi nasıl toocreate ve ürünleri Azure API Management'te yayımlayın."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 31de55cb-9384-490b-a2f2-6dfcf83da764
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: f0a37f08b4e29ca68be9caec4c7604e3b4b6aaa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-publish-a-product-in-azure-api-management"></a>Nasıl toocreate ve Azure API Management'te bir ürün yayımlama
Azure API Management'te bir ürün, bir veya daha fazla API'leri ve bunun yanı sıra bir kullanım kotası ve hello kullanım koşulları içerir. Bir ürün yayımlandığında, geliştiricilerin toohello ürün abone ve toouse hello ürün API'lerine başlayın. Merhaba konu Kılavuzu toocreating bir ürüne API ekleme ve geliştiriciler için yayımlama sağlar.

## <a name="create-product"></a>Ürün oluşturma
Operations eklenir ve tooan API hello yayımcı portalında yapılandırılır. tooaccess hello yayımcı portalı, tıklatın **yayımcı portalına** API Management hizmetiniz için hello Azure Portalı'nda.

![Yayımcı portalı][api-management-management-console]

> Henüz bir API Management hizmeti örneği oluşturmadıysanız, bkz: [bir API Management hizmet örneği oluşturma] [ Create an API Management service instance] hello içinde [Azure API Management ile çalışmaya başlama] [ Get started with Azure API Management] Öğreticisi.
> 
> 

Tıklayın **ürünleri** hello sol toodisplay hello hello menüsünde **ürünleri** sayfasında ve tıklayın **Ürün Ekle**.

![Ürünler][api-management-products]

![Yeni ürün][api-management-add-new-product]

Hello hello ürün için açıklayıcı bir ad girin **adı** alan ve hello hello üründe açıklamasını **açıklama** alan.

API Management ürünleri olabilir **açık** veya **korumalı**. Korumalı ürünleri, bunlar kullanılabilir, açıkken abone toobefore olmalıdır ürünler abonelik olmadan kullanılabilir. Denetleme **abonelik iste** toocreate bir abonelik gerektiren korumalı ürün. Merhaba varsayılan ayar budur.

Denetleme **abonelik onayı iste** bir yönetici tooreview istediğiniz ve kabul edin veya reddedin abonelik toothis ürün çalışır. Merhaba kutusu işaretli değilse abonelik girişimleri otomatik onaylı olacaktır. Abonelikler hakkında daha fazla bilgi için bkz: [görünüm aboneleri tooa ürün][View subscribers tooa product].

tooallow Geliştirici hesaplarını toosubscribe birden çok kez toohello ürün denetleyin hello **birden çok abonelik izin** onay kutusu. Her geliştirici hesabını, bu kutu işaretli değilse, yalnızca bir kereliğine toohello ürün abone olabilirsiniz.

![Sınırsız birden çok abonelik][api-management-unlimited-multiple-subscriptions]

toolimit hello aynı anda birden fazla abonelik sayısını kontrol hello **aynı anda abonelik sayısını sınırlandır** onay kutusunu işaretleyin ve hello abonelik sınırı girin. Aşağıdaki örneğine hello, sınırlı toofour Geliştirici hesabı başına eşzamanlı abonelikler var.

![Dört birden çok abonelik][api-management-four-multiple-subscriptions]

Tüm yeni ürün seçenekleri yapılandırıldıktan sonra tıklatın **kaydetmek** toocreate hello yeni ürün.

![Ürünler][api-management-products-page]

> Varsayılan olarak yeni ürünler yayımdan olduğunda ve görünür yalnızca toohello **Yöneticiler** grubu.
> 
> 

Merhaba hello ürün adı tooconfigure bir ürün tıklayın **ürünleri** sekmesi.

## <a name="add-apis"></a>Ekleme API'leri tooa ürün
Merhaba **ürünleri** sayfa yapılandırması için dört bağlantılarını içerir: **Özet**, **ayarları**, **görünürlük**, ve  **Aboneler**. Merhaba **Özet** sekme, burada API'leri ekleyebilir ve yayımlama veya yayımdan bir ürün kullanılabilir.

![Özet][api-management-new-product-summary]

Ürünü yayımlamadan önce bir veya daha fazla API'leri tooadd gerekir. toodo bunu, **API Ekle tooproduct**.

![API ekleme][api-management-add-apis-to-product]

Select hello istenen API'ler ve tıklatın **kaydetmek**.

## <a name="add-description"></a>Ekle açıklayıcı bilgiler tooa ürün
Merhaba **ayarları** sekme sağlar, tooprovide amacı, hello API'leri erişim sağlar ve diğer yararlı bilgiler gibi hello ürün hakkında ayrıntılı bilgi. Merhaba içerik hello API çağırma ve düz metin veya HTML biçimlendirmesi yazılabilir hello geliştiriciler hedefleyen.

![Ürün ayarları][api-management-product-settings]

Denetleme **abonelik iste** toocreate abonelik toobe kullanılan ya da Temizle gerektiren korumalı ürün hello onay kutusunu toocreate abonelik olmadan çağrılabilen bir ürünü aç.

Seçin **abonelik onayı iste** toomanually istiyorsanız, tüm ürün abonelik istekleri onaylayabilir. Varsayılan olarak tüm ürün abonelikler otomatik olarak verilir.

tooallow Geliştirici hesaplarını toosubscribe birden çok kez toohello ürün denetleyin hello **birden çok abonelik izin** onay kutusunu işaretleyin ve isteğe bağlı olarak bir sınırı belirtin. Her geliştirici hesabını, bu kutu işaretli değilse, yalnızca bir kereliğine toohello ürün abone olabilirsiniz.

İsteğe bağlı olarak hello dolgu **kullanım koşulları** hello kullanım koşullarına aboneleri sipariş toouse hello üründe kabul etmelisiniz hello ürün açıklayan alan.

## <a name="publish-product"></a>Bir ürün yayımlama
Bir ürün Hello API'leri çağrılabilir önce hello ürünün yayımlanması gerekir. Merhaba üzerinde **Özet** hello ürün sekmesini tıklatın, **Yayımla**ve ardından **Evet, Yayımla** tooconfirm. toomake önceden yayımlanmış ürün özel tıklatın **yayımdan**.

![Ürünü yayımlama][api-management-publish-product]

## <a name="make-visible"></a>Ürün görünür toodevelopers olun
Merhaba **görünürlük** sekme hangi roller mümkün toosee hello ürün hello Geliştirici Portalı üzerinde ve toohello ürün abone toochoose sağlar.

![Ürün görünürlüğü][api-management-product-visiblity]

bir grup halinde hello geliştiriciler için bir ürün tooenable veya devre dışı bırakma görünürlüğünü denetleme veya hello hello grubunun yanındaki onay kutusunun işaretini kaldırın ve ardından **kaydetmek**.

> Daha fazla bilgi için bkz: [nasıl toocreate ve kullanım grupları toomanage Geliştirici Azure API Management'te hesapları][How toocreate and use groups toomanage developer accounts in Azure API Management].
> 
> 

## <a name="view-subscribers"></a>Görünüm aboneleri tooa ürün
Merhaba **aboneleri** sekmesi toohello ürün abone olduğunuz hello geliştiriciler listeler. Merhaba ayrıntılarını ve ayarlar her geliştirici hello geliştiricinin adına tıklayarak görüntülenebilir. Bu örnekte hiçbir geliştiriciler henüz toohello ürün abone oldunuz.

![Geliştiriciler][api-management-developer-list]

## <a name="next-steps"> </a>Sonraki adımlar
Bir kez hello API'ler eklenmiştir ve hello ürün yayımlanan, geliştiriciler toohello ürün abone ve toocall hello API'leri başlamak istenen. Bu öğeleri yanı sıra Gelişmiş Ürün yapılandırma gösteren bir öğretici için bkz: [oluşturma ve Gelişmiş Ürün ayarları Azure API Management'te yapılandırma][How create and configure advanced product settings in Azure API Management].

Ürünleri ile çalışma hakkında daha fazla bilgi için video aşağıdaki hello bakın.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

[Create a product]: #create-product
[Add APIs tooa product]: #add-apis
[Add descriptive information tooa product]: #add-description
[Publish a product]: #publish-product
[Make a product visible toodevelopers]: #make-visible
[View subscribers tooa product]: #view-subscribers
[Next steps]: #next-steps

[api-management-management-console]: ./media/api-management-howto-add-products/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-add-products/api-management-add-product.png
[api-management-add-new-product]: ./media/api-management-howto-add-products/api-management-add-new-product.png
[api-management-unlimited-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-unlimited-multiple-subscriptions.png
[api-management-four-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-four-multiple-subscriptions.png
[api-management-products-page]: ./media/api-management-howto-add-products/api-management-products-page.png
[api-management-new-product-summary]: ./media/api-management-howto-add-products/api-management-new-product-summary.png
[api-management-add-apis-to-product]: ./media/api-management-howto-add-products/api-management-add-apis-to-product.png
[api-management-product-settings]: ./media/api-management-howto-add-products/api-management-product-settings.png
[api-management-publish-product]: ./media/api-management-howto-add-products/api-management-publish-product.png
[api-management-product-visiblity]: ./media/api-management-howto-add-products/api-management-product-visibility.png
[api-management-developer-list]: ./media/api-management-howto-add-products/api-management-developer-list.png



[api-management-products]: ./media/api-management-howto-add-products/api-management-products.png
[api-management-]: ./media/api-management-howto-add-products/
[api-management-]: ./media/api-management-howto-add-products/


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps
[How toocreate and use groups toomanage developer accounts in Azure API Management]: api-management-howto-create-groups.md
[How create and configure advanced product settings in Azure API Management]: api-management-howto-product-with-rules.md 
