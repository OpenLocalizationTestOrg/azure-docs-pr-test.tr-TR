---
title: "aaaTranslate bağlantıları ve URL'leri Azure AD uygulaması Proxy | Microsoft Docs"
description: "Merhaba temel Azure AD uygulama proxy'si bağlayıcılar hakkında bilgiler yer almaktadır."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7ec2b9fb01617067cf5d676037877bf72c19217b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="redirect-hardcoded-links-for-apps-published-with-azure-ad-application-proxy"></a>Azure AD uygulama ara sunucusu ile yayımlanan uygulamalar için sabit kodlanmış bağlantı yeniden yönlendirme

Azure AD uygulama proxy'si uzak veya kendi cihazlarını olan, şirket içi uygulamalar kullanılabilir toousers yapar. Bazı uygulamalar, ancak hello HTML katıştırılmış yerel bağlantılar ile geliştirilmiştir. Merhaba uygulama uzaktan kullanıldığında, bu bağlantıları doğru çalışmaz. Çeşitli şirket içi uygulamalar noktası tooeach diğer sahip olduğunuzda, kullanıcılarınızın hello ofiste olmadıklarını çalışma hello bağlantılar tookeep bekler. 

Merhaba en iyi şekilde toomake bağlantılar iş aynı hem içinde hem de hello ve şirket ağının dışından tooconfigure hello dış uygulamaları toobe URL'lerini olduğundan emin hello aynı kendi iç URL olarak. Kullanım [özel etki alanlarını](active-directory-application-proxy-custom-domains.md) tooconfigure şirket etki alanınızı yerine hello varsayılan uygulama proxy etki alanı adı, dış URL'ler toohave.

Özel etki alanlarını kiracınızda kullanamıyorsanız, uygulama proxy'sinin hello bağlantı çeviri özelliği, kullanıcılarınızın nerede olursa olsun çalışma bağlantılarınızı tutar. Toointernal uç noktaları veya bağlantı noktaları, eşleyebilirsiniz doğrudan işaret eden uygulamalar varsa bu dahili URL'leri toohello uygulama Proxy URL'lere yayımladı. Bağlantı çeviri etkinleştirildiğinde ve HTML, CSS ve JavaScript etiketlerin select yayımlanan iç bağlantılar için uygulama proxy'si arar. Böylece kullanıcılarınızın kesintisiz bir deneyim almak hello uygulama proxy'si hizmeti bunları çevirir.

>[!NOTE]
>Merhaba bağlantı çeviri ne olursa olsun nedeni için özel etki alanlarını kullanamazsınız, kiracılar için özelliktir toohave hello uygulamalarını aynı iç ve dış URL. Bu özelliği etkinleştirmek için önce olup [Azure AD uygulama proxy'si özel etki alanlarında](active-directory-application-proxy-custom-domains.md) sizin için çalışabilir.
>
>Veya, SharePoint Merhaba uygulaması ile bağlantı çeviri tooconfigure ihtiyacınız olup olmadığını [SharePoint 2013 için diğer erişim eşleşmeleri yapılandırma](https://technet.microsoft.com/library/cc263208.aspx) başka bir yaklaşım toomapping bağlantılar için.

## <a name="how-link-translation-works"></a>Çeviri works nasıl bağlantı

Bir kimlik doğrulamasından sonra hello proxy sunucusu hello uygulama veri toohello kullanıcı, başarılı olduğunda uygulama proxy'si Merhaba uygulaması sabit kodlanmış bağlantılar için tarar ve dış URL'ler yayımlanan kendi ilgili ile değiştirir.

Uygulama proxy'si uygulamaları UTF-8'de kodlandığını varsayar. Merhaba durum bu değilse, hello kodlama türü bir http yanıt üstbilgisi gibi belirtin `Content-Type:text/html;charset=utf-8`.

### <a name="which-links-are-affected"></a>Hangi bağlantıların etkilenen?

Merhaba bağlantı çeviri özelliği yalnızca kod etiketler, bir uygulamanın hello gövdesinde yer alan bağlantıları arar. Uygulama proxy'si tanımlama bilgilerini veya URL'leri üstbilgilerinde çevirme için ayrı bir özellik vardır. 

Şirket içi uygulamalara iç bağlantıları iki genel türleri şunlardır:

- **Göreli iç bağlantıları** bu noktası tooa paylaşılan kaynak gibi bir yerel dosya yapısında `/claims/claims.html`. Uygulama proxy'si aracılığıyla yayımlanır ve toowork ile veya olmadan bağlantı çeviri devam uygulamalarında bu bağlantıları otomatik olarak çalışır. 
- **Sabit kodlanmış iç bağlantılar** tooother şirket içi uygulamalar gibi `http://expenses` ya da dosyalar gibi yayımlanan `http://expenses/logo.jpg`. Merhaba bağlantı çeviri özelliğini sabit kodlanmış iç bağlantıları çalışır ve uzak kullanıcılar toogo aracılığıyla gereken toopoint toohello dış URL'ler değiştirir.

### <a name="how-do-apps-link-tooeach-other"></a>Uygulamaları tooeach diğer nasıl bağlanır?

Merhaba uygulama başına düzeyinde hello kullanıcı deneyimi üzerinde denetiminiz bağlantı çeviri her uygulama için etkinleştirilir. Bir uygulama için bağlantı çeviri hello bağlantılar istediğinizde Aç *gelen* o uygulama toobe çevrilmiş, olmayan bağlantıları *için* bu uygulama. 

Örneğin, uygulama tüm tooeach diğer bağlantı Proxy üzerinden yayımlanan üç uygulama olduğunu varsayalım: avantajları, gider ve seyahat. Dördüncü bir uygulama, uygulama proxy'si aracılığıyla yayımlanan değil geri bildirim yoktur.

Bağlantı çevirisi hello avantajları uygulama için etkinleştirdiğinizde, hello bağlantılar tooExpenses ve seyahat yeniden yönlendirilen toohello dış URL'ler bu uygulamalarda, ancak hiçbir dış URL olduğundan hello bağlantı tooFeedback yeniden yönlendirilen değil. Bağlantılar giderleri ve seyahat bağlantı çeviri iki uygulamalarla için etkin değil çünkü müşteri geri tooBenefits çalışmıyor.

![Bağlantı çeviri etkinleştirildiğinde avantajları tooother uygulamalardan bağlantılar](./media/application-proxy-link-translation/one_app.png)

### <a name="which-links-arent-translated"></a>Hangi bağlantıların çevrilen değil mi?

tooimprove performans ve güvenlik, bazı bağlantılar olmayan çevrilen:

- Bağlantılar kod etiketleri içinde değil. 
- Bağlantılar HTML, CSS ve JavaScript içinde değil. 
- İç bağlantılar diğer programlardan açıldı. Gönderilen e-posta veya anlık ileti veya diğer belgelerde bulunan bağlantılar çevrilmiş olmaz. Merhaba kullanıcıların tooknow toogo toohello dış URL gerekir.

Şu iki senaryodan biri toosupport gerekiyorsa, kullanım hello aynı bağlantı çeviri yerine iç ve dış URL.  

## <a name="enable-link-translation"></a>Bağlantı çeviri etkinleştir

Bağlantı çevirisi ile çalışmaya başlama düğmesi olarak kadar kolaydır:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com) yönetici olarak.
2. Çok Git**Azure Active Directory** > **kurumsal uygulamalar** > **tüm uygulamaları** > select hello uygulamayı toomanage > **Uygulama proxy'si**.
3. Kapatma **Çevir URL'leri uygulama gövdesindeki** çok**Evet**.

   ![Evet tootranslate URL'leri uygulama gövdesinde seçin](./media/application-proxy-link-translation/select_yes.png).
4. Seçin **kaydetmek** tooapply değişikliklerinizi.

Kullanıcıların bu uygulamayı eriştiğinizde, şimdi hello proxy otomatik olarak uygulama proxy'si aracılığıyla Kiracı'yayımlandı iç URL'ler için tarar.

## <a name="send-feedback"></a>Geri bildirim gönderin

Yardım toomake bu özellik iş tüm uygulamalar istiyoruz. Biz 30 etiketleri HTML ve CSS arayın ve hangi JavaScript durumlarda toosupport dikkate. Çevrildiğini olmayan oluşturulan bağlantıları örneği varsa, bir kod parçacığı çok göndermeniz[uygulama Proxy geri bildirim](mailto:aadapfeedback@microsoft.com). 

## <a name="next-steps"></a>Sonraki adımlar
[Azure AD uygulama proxy'si ile özel etki alanları kullanabilirsiniz](active-directory-application-proxy-custom-domains.md) toohave hello aynı iç ve dış URL

[SharePoint 2013 için diğer erişim eşleşmeleri yapılandırın](https://technet.microsoft.com/library/cc263208.aspx)
