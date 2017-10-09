---
title: "Azure Active Directory B2C: Facebook yapılandırma | Microsoft Docs"
description: "Uygulamalarınızda Azure Active Directory B2C tarafından güvenliği sağlanan Facebook hesaplarıyla kaydolma ve oturum açma tooconsumers sağlar."
services: active-directory-b2c
documentationcenter: 
author: sromeroz
manager: krassk
editor: sromeroz
ms.assetid: b875f235-a1d2-4abb-b9f0-b89beac38a32
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/7/2017
ms.author: sromeroz
ms.openlocfilehash: 4c3b79c7248bd1e789bf33fc467abb27d0170edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-facebook-accounts"></a>Azure Active Directory B2C: Kaydolma ve oturum açma tooconsumers Facebook hesabıyla sağlayın.
## <a name="create-a-facebook-application"></a>Bir Facebook uygulaması oluşturma
toouse Facebook kimlik sağlayıcısı Azure Active Directory (Azure AD) B2C içinde toocreate bir Facebook uygulaması gerekir ve hello doğru parametrelerle sağlayın. Bu bir Facebook hesap toodo gerekir. Bir sahip değilseniz, yerinde edinebilirsiniz [https://www.facebook.com/](https://www.facebook.com/).

1. Toohello Git [geliştiriciler için Facebook](https://developers.facebook.com/) hesap kimlik bilgileri Web sitesi ve, Facebook ile oturum açın.
2. Zaten yapmadıysanız, Facebook geliştirici olarak tooregister gerekir. toodo bunu, **kaydetmek** (Merhaba sağ üst köşesinde hello sayfasının), Facebook'ın ilkeleri kabul etmek ve hello kayıt adımları tamamlayın.
3. Tıklatın **My uygulamaları** ve ardından **yeni bir uygulama eklemek**. 
4. Hello formunda sağlayan bir **görünen adı** ve geçerli bir **ilgili kişi e-posta**.
5. Tıklatın **uygulama kimliği oluşturma**. Bu tooaccept Facebook platform ilkeleri gerektirir ve bir çevrimiçi güvenlik denetimi tamamlandı.
6. Merhaba sol sütunda tıklatın **ayarları** ve ardından **temel** zaten seçilmemişse.
7. Seçin bir **kategori**. 
8. Tıklatın **+ Platform eklemek** seçip **Web sitesi**.
   
    ![Facebook - ayarlar](./media/active-directory-b2c-setup-fb-app/fb-settings.png)
   
    ![Facebook - ayarları - Web sitesi](./media/active-directory-b2c-setup-fb-app/fb-website.png)
9. Girin `https://login.microsoftonline.com/` hello içinde **Site URL'si** alan ve ardından **Değişiklikleri Kaydet** hello sayfanın hello sonundaki.
   
    ![Facebook - Site URL'si](./media/active-directory-b2c-setup-fb-app/fb-site-url.png)

10. Merhaba değerini kopyalayın **uygulama kimliği**. Tıklatın **Göster** ve kopyalama hello değerini **uygulama gizli anahtarı**. Bunların her ikisi gerekir tooconfigure Facebook kiracınızda kimlik sağlayıcısı. **Uygulama gizli anahtarı** önemli güvenlik kimlik bilgileri.
   
    ![Facebook - uygulama kimliği & uygulama gizli anahtarı](./media/active-directory-b2c-setup-fb-app/fb-app-id-app-secret.png)
11. Tıklatın **+ ürün ekleme** hello sol gezinti ve ardından hello **Ayarla** için düğmesini **Facebook oturum açma**.
   
    ![Facebook - Facebook oturum açma](./media/active-directory-b2c-setup-fb-app/fb-login.png)
12. Tıklatın **ayarları** hello sağ nav altında üzerinde **Facebook oturum açma**

    ![Facebook - Facebook oturum açma ayarları](./media/active-directory-b2c-setup-fb-app/fb-login-settings.png)
13. Girin `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` hello içinde **geçerli OAuth yeniden yönlendirme URI'ler** hello alanındaki **istemci OAuth ayarları** bölümü. Değiştir **{tenant}** , kiracının adlı (örneğin, contosob2c.onmicrosoft.com). Tıklatın **Değişiklikleri Kaydet** hello sayfanın hello sonundaki.
    
    ![Facebook - OAuth yeniden yönlendirme URI'si](./media/active-directory-b2c-setup-fb-app/fb-oauth-redirect-uri.png)
14. toomake Facebook uygulamanız toomake ihtiyacınız Azure AD B2C tarafından kullanılabilir, genel olarak kullanılabilir. Tıklayarak bunu yapabilirsiniz **uygulama İnceleme** sol gezinti hello ve kapatma hello geçiş hello hello sayfanın başında çok**Evet** tıklatıp **Onayla**.
    
    ![Facebook - uygulama genel](./media/active-directory-b2c-setup-fb-app/fb-app-public.png)

## <a name="configure-facebook-as-an-identity-provider-in-your-tenant"></a>Facebook kimlik sağlayıcısı kiracınızda yapılandırın
1. Bu adımları çok[toohello B2C özellikleri dikey penceresine gidin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure portalı üzerinde.
2. Merhaba B2C özellikleri dikey penceresinde **kimlik sağlayıcıları**.
3. Tıklatın **+ Ekle** hello dikey penceresinde hello üstünde.
4. Kolay bir sağlamak **adı** hello kimlik sağlayıcı yapılandırması için. Örneğin, "Facebook" girin.
5. Tıklatın **kimlik sağlayıcısı türü**seçin **Facebook**, tıklatıp **Tamam**.
6. Tıklatın **bu kimlik sağlayıcısı'nı ayarlama** ve hello uygulama kimliği ve uygulama gizli anahtarı (Merhaba daha önce oluşturduğunuz Facebook uygulaması) girin hello içinde **istemci kimliği** ve **gizli**sırasıyla alanları.
7. Tıklatın **Tamam**ve ardından **oluşturma** toosave Facebook yapılandırmanızı.

> [!NOTE]
> Ekleme bir **kimlik sağlayıcısı** tooyour Kiracı varolan ilkelerinizi değiştirilmez. Tooupdate, az önce oluşturduğunuz hello kimlik sağlayıcısı dahil ederek ilkelerinizi unutmayın.
>