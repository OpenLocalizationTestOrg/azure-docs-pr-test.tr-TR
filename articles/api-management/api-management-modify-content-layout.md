---
title: "Azure API Management'ta Geliştirici portalını hello aaaModify sayfası içeriğini | Microsoft Docs"
description: "Nasıl hello Geliştirici portalındaki Azure API Management'te tooedit sayfa içeriğini öğrenin."
services: api-management
documentationcenter: 
author: antonba
manager: vlvinogr
editor: 
ms.assetid: 186128fe-41c0-4efb-9efe-2478ad4d103f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/09/2017
ms.author: antonba
ms.openlocfilehash: fd5a854e900d9512518643e593b1b59a0952621f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-content-and-layout-of-pages-on-hello-developer-portal-in-azure-api-management"></a>Merhaba içeriğini ve Azure API Management'ta Geliştirici portalını hello sayfalarında düzenini değiştirme
Azure API Management'te üç temel şekilde toocustomize hello Geliştirici Portalı vardır:

* [Statik sayfaları ve sayfa düzeni öğelerini Merhaba içeriğine Düzenle] [ modify-content-layout] (Bu kılavuzda açıklanan)
* [Merhaba Geliştirici Portalı sayfası öğeleri için kullanılan güncelleştirme hello stilleri][customize-styles]
* [Merhaba portal tarafından oluşturulan sayfalar için kullanılan hello şablonları değiştirmek] [ portal-templates] (örneğin API belgeleri, ürünler, kullanıcı kimlik doğrulaması, vb.)

## <a name="page-structure"> </a>Geliştirici portalı sayfalarının yapısı

Merhaba Geliştirici Portalı bir içerik yönetimi sistemini temel alır. her sayfasının Hello düzenini pencere öğeleri bilinen küçük sayfa öğelerin dayanır:

![Geliştirici portalı sayfa yapısı][api-management-customization-widget-structure]

Tüm pencere öğeleri düzenlenebilir. 
* Merhaba çekirdek içeriği belirli tooeach tek tek sayfa hello "İçerik" Pencere öğesinde bulunur. Bir sayfa düzenleme Bu pencere öğesi Merhaba içeriğine düzenleme anlamına gelir.
* Tüm sayfa düzeni öğeleri ile Merhaba kalan pencere öğeleri bulunur. Toothese pencere öğeleri yapılan değişiklikler tooall sayfaları uygulanır. Bunlar, başvurulan tooas "düzeni pencere öğeleri" olacaktır.

Günlük sayfasında bir genellikle düzenleme her sayfa için farklı içeriğe sahip olacak hello içerik pencere yalnızca değiştirir.

## <a name="modify-layout-widget"></a>Düzeni pencere öğesi hello içeriğini değiştirme

Merhaba Geliştirici portalındaki içerik hello Azure Portalı ' erişilebilen hello yayımcı Portalı aracılığıyla değiştirilir. tooreach, tıklatın **yayımcı portalına** , API Management örneğinin hello hizmet araç çubuğundan.

![Yayımcı portalı][api-management-management-console]

Bu pencere öğesi tooedit Merhaba içeriğine tıklatın **pencere öğeleri** hello gelen **Geliştirici Portalı** hello sol menüsünde. Bu örnek sağlayan için hello üstbilgi pencere öğesi hello içeriğini değiştirin. Select hello **üstbilgi** hello listeden pencere öğesi.

![Pencere öğeleri üst bilgisi][api-management-widgets-header]

hello üstbilgi Merhaba içeriğine hello içinde düzenlenebilir **gövde** alan. Değiştirmek istediğiniz gibi hello metin ve ardından **kaydetmek** hello sayfanın hello sonundaki.

Artık mümkün toosee hello yeni üstbilgi hello Geliştirici portalındaki her sayfada olması gerekir.

> tooopen hello Geliştirici Portalı hello yayımcı portalında karşın, tıklatın **Geliştirici Portalı** hello üst çubuğunda.
> 
> 

## <a name="edit-page-contents"></a>Hello bir sayfanın içeriğini düzenleme

toosee hello tüm var olan içerik sayfalarının listesini tıklatın **içerik** hello gelen **Geliştirici Portalı** hello yayımcı portalı menüsünde.

![İçeriği yönetme][api-management-customization-manage-content]

Merhaba tıklatın **Hoş Geldiniz** tooedit hello Geliştirici Portalı hello giriş sayfasında görüntülenen sayfa. İstediğiniz, gerekirse Önizleme ve ardından hello değişiklik **Şimdi Yayımla** toomake onları görünür tooeveryone.

> Merhaba giriş sayfası hello üstünde toodisplay bir başlık sağlayan özel bir düzen kullanır. Bu başlık hello düzenlenebilir değil **içerik** bölümü. tooedit Bu başlık tıklatın **pencere öğeleri** hello gelen **Geliştirici Portalı** menüsünde, select **giriş sayfası** hello gelen **geçerli katman** açılır Liste ve hello açın **başlık** öğesi hello altında **öne çıkan bölüm**. Bu pencere öğesi Hello içeriği diğer sayfalar gibi düzenlenebilir.
> 
> 

## <a name="next-steps"> </a>Sonraki adımlar
* [Merhaba Geliştirici Portalı sayfası öğeleri için kullanılan güncelleştirme hello stilleri][customize-styles]
* [Merhaba portal tarafından oluşturulan sayfalar için kullanılan hello şablonları değiştirmek] [ portal-templates] (örneğin API belgeleri, ürünler, kullanıcı kimlik doğrulaması, vb.)

[Structure of developer portal pages]: #page-structure
[Modifying hello contents of a layout widget]: #modify-layout-widget
[Edit hello contents of a page]: #edit-page-contents
[Next steps]: #next-steps

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[api-management-customization-widget-structure]: ./media/api-management-modify-content-layout/portal-widget-structure.png
[api-management-management-console]: ./media/api-management-modify-content-layout/api-management-management-console.png
[api-management-widgets-header]: ./media/api-management-modify-content-layout/api-management-widgets-header.png
[api-management-customization-manage-content]: ./media/api-management-modify-content-layout/api-management-customization-manage-content.png
