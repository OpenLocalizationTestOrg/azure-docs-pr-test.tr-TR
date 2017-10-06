---
title: "Azure API Management'ta Geliştirici portalını hello aaaCustomize stillerde | Microsoft Docs"
description: "Toomodify hello stilleri'hello Azure API Management'ta Geliştirici portalını herhangi bir sayfa için nasıl kullanılacağını öğrenin."
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
ms.openlocfilehash: aaaa86527992ba43e64eab5fd35c7f57b573c812
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-styling-of-hello-developer-portal-in-azure-api-management"></a>Merhaba stilini hello Azure API Management'ta Geliştirici portalını özelleştirme
Azure API Management'te üç temel şekilde toocustomize hello Geliştirici Portalı vardır:

* [Statik sayfaları ve sayfa düzeni öğelerini Hello içeriğini düzenleme][modify-content-layout]
* [Merhaba Geliştirici Portalı sayfası öğeleri için kullanılan hello stilleri güncelleştirme] [ customize-styles] (Bu kılavuzda açıklanan)
* [Merhaba portal tarafından oluşturulan sayfalar için kullanılan hello şablonları değiştirmek] [ portal-templates] (örneğin API belgeleri, ürünler, kullanıcı kimlik doğrulaması, vb.)

## <a name="change-headers-styling"></a>Sayfası öğeleri hello stilini değiştirme

Merhaba renkleri, yazı tipi, boyutları, boşluklar ve hello portalındaki herhangi bir sayfanın diğer stil ilgili öğeler stil kuralları tarafından tanımlanır. 

Merhaba stil kurallarını düzenlemenin hello yapılır **Geliştirici Portalı** yönetici olarak oturum açmış oluştu. tooget var. önce hello Azure Portal açın ve tıklatın **yayımcı portalına** , API Management örneğinin hello hizmet araç çubuğundan.

![Yayımcı portalı][api-management-management-console]

Tıklayın **Geliştirici Portalı** hello sağ üst üzerinde. 

![Geliştirici Portalı bağlantıyı hello yayımcı portalı][api-management-pp-dp-link]

tooopen hello özelleştirme araç farenizi hello özelleştirme simgenin üzerine getirin (veya seçin) ve ardından tıklatın "Merhaba araç çubuğundan stilleri".

![Özelleştirme araç çubuğu düğmesi][api-management-customization-toolbar-button]

Stil kurallarını düzenlemenin iki ana yol vardır - varsayılan olarak görüntülenen hello herhangi bir yerde kullanılan tüm hello Stil kurallarının listesini göz ve stil gerektiği şekilde değiştirin veya seçebilirsiniz **hello sayfada bir öğe seçin** ve ardından Merhaba sayfa toosee yalnızca hello stilleri o öğeye ilişkin üzerinde herhangi bir yere tıklayın.

![Özelleştirme araç çubuğu][api-management-customization-toolbar]

Merhaba tıklatın **hello sayfada bir öğe seçin** bu örneğin seçeneği.  Hangi öğe stillerini tıkladıysanız düzenlemeye başlamak üzerlerine hello fare toosignify ile gezinirken öğeler vurgulanır. Taşıma hello fare üzerinden hello metin hello üstbilgi (genellikle hello şirket adını buraya olması) ve ardından onu. Adlandırılmış ve kategorilere ayrılmış stil kuralları kümesi hello stil düzenleyicisinde görüntülenir. Her kural hello seçili öğenin bir stil özelliğini temsil eder. Örneğin, yukarıda seçilen hello üstbilgi metni için hello hello metin olarak boyutudur @font-size-h1 Alternatiflerle birlikte yazı tipi hello hello adı olarak kullanılırken @headings-font-family.

> Hakkında bilginiz varsa [önyükleme][bootstrap], bu kurallar aslında olan [LESS değişkenleri] [ LESS variables] hello tarafından kullanılan önyükleme temasının hello içinde Geliştirici Portalı.
> 
> 

Merhaba hello başlık metninin rengini değiştirelim. Hello Hello girişi seçin  **@headings-color**  alanı ve türü **#000000**. Bu hello onaltılık hello rengi siyah kodudur. Bunu yaparken, bir kare renk göstergesi hello hello metin kutusunun sonunda görüntülenir. Bu göstergeye tıklarsanız, bir renk seçici renk toochoose olanak sağlar.

![Renk seçici][api-management-customization-toolbar-color-picker]

Bunları hale getirir, ancak yalnızca tooadministrators görünür olan gibi değişiklikler gerçek zamanlı olarak önizlemesi. toomake görünür tooeveryone bu değişiklikler, hello tıklatın **Yayımla** düğmesini hello stil Düzenleyicisi'nde ve hello değişiklikleri onaylayın.

![Yayımla menüsü][api-management-customization-toolbar-publish-form]

> toochange hello stil tooany uygulamak kuralı başka bir öğenin başlangıç sayfasında, izleme hello aynı yordamı siz hello üstbilgisi vermedi. Tıklatın **hello sayfada bir öğe seçin** hello stil düzenleyicisini, ilgilendiğiniz select hello öğesi ve başlangıç Merhaba ekranında görüntülenen hello Stil kurallarının hello değerlerini değiştirme.
> 
> 


## <a name="next-steps"> </a>Sonraki adımlar
* Geliştirici Portalı toocustomize Merhaba içeriğine kullanarak nasıl sayfaları öğrenin [Geliştirici Portalı şablonları](api-management-developer-portal-templates.md).

[Change hello styling of hello headers]: #change-headers-styling
[Next steps]: #next-steps

[Azure Classic Portal]: https://manage.windowsazure.com/

[api-management-management-console]: ./media/api-management-customize-styles/api-management-management-console.png
[api-management-pp-dp-link]: ./media/api-management-customize-styles/api-management-pp-dp-link.png
[api-management-customization-toolbar-button]: ./media/api-management-customize-styles/api-management-customization-toolbar-button.png
[api-management-customization-toolbar]: ./media/api-management-customize-styles/api-management-customization-toolbar.png
[api-management-customization-toolbar-color-picker]: ./media/api-management-customize-styles/api-management-customization-toolbar-color-picker.png
[api-management-customization-toolbar-publish-form]: ./media/api-management-customize-styles/api-management-customization-toolbar-publish-form.png

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[bootstrap]: http://getbootstrap.com/
[LESS variables]: http://getbootstrap.com/css/
