---
title: "Azure Active Directory B2C: Weibo yapılandırma | Microsoft Docs"
description: "Uygulamalarınızda Azure Active Directory B2C tarafından güvenliği sağlanan Weibo hesaplarıyla kaydolma ve oturum açma tooconsumers sağlar."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1860de34-94cb-4ceb-851e-102f930f7230
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: c0648620f318046c1d9d24feb92a0c5f19c6a91a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-weibo-accounts"></a>Azure Active Directory B2C: Kaydolma ve oturum açma tooconsumers Weibo hesaplarıyla sağlayın.

> [!NOTE]
> Bu özelliğin önizlemede değil. Bu kimlik sağlayıcısı, üretim ortamınızda kullanmayın.
> 

## <a name="create-a-weibo-application"></a>Weibo uygulaması oluşturma

toouse Weibo Azure Active Directory (Azure AD) B2C içinde kimlik sağlayıcısı, toocreate Weibo uygulama gerekir ve hello doğru parametrelerle sağlayın. Bu Weibo hesap toodo gerekir. Yoksa, her seferde alabilirsiniz [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).

### <a name="register-for-hello-weibo-developer-program"></a>Merhaba Weibo developer program kaydolun

1. Toohello Git [Weibo Geliştirici Portalı](http://open.weibo.com/) ve Weibo hesabı kimlik bilgilerinizle oturum açın.
2. Oturum açtıktan sonra görünen adınızı hello sağ üst köşedeki tıklayın.
3. Merhaba açılır menüde seçin**编辑开发者信息**(Geliştirici bilgilerini Düzenle).
4. Merhaba forma hello gerekli bilgileri girin ve tıklatın**提交**(Gönder).
5. Merhaba e-posta doğrulama işlemini tamamlayın.
6. Toohello Git [kimlik doğrulama sayfasında](http://open.weibo.com/developers/identity/edit).
7. Merhaba forma hello gerekli bilgileri girin ve tıklatın**提交**(Gönder).

### <a name="register-a-weibo-application"></a>Weibo uygulamayı Kaydet

1. Toohello Git [yeni Weibo uygulama kayıt sayfasına](http://open.weibo.com/apps/new).
2. Merhaba gerekli uygulama bilgilerini girin.
3. Tıklatın**创建**(Oluştur).
4. Merhaba değerlerini kopyalamayı **uygulama anahtarı** ve **uygulama gizli anahtarı**. Bu daha sonra ihtiyacınız olacak.
5. Gerekli hello fotoğrafı karşıya ve hello gerekli bilgileri girin.
6. Tıklatın**保存以上信息**(Kaydet).
7. Tıklatın**高级信息**(Gelişmiş).
8. Tıklatın**编辑**(düzenleme) sonraki toohello alanı OAuth2.0 için**授权设置**(yeniden yönlendirme URL'si).
9. Girin `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` OAuth2.0 için**授权设置**(yeniden yönlendirme URL'si). Örneğin, varsa, `tenant_name` contoso.onmicrosoft.com, kümesi hello URL toobe olan `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.
10. Tıklatın**提交**(Gönder).  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a>Kimlik sağlayıcısı kiracınızda Weibo yapılandırın
1. Bu adımları çok[toohello B2C özellikleri dikey penceresine gidin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure portalı üzerinde.
2. Merhaba B2C özellikleri dikey penceresinde **kimlik sağlayıcıları**.
3. Tıklatın **+ Ekle** hello dikey penceresinde hello üstünde.
4. Kolay bir sağlamak **adı** hello kimlik sağlayıcı yapılandırması için. Örneğin, "Weibo" girin.
5. Tıklatın **kimlik sağlayıcısı türü**seçin **Weibo**, tıklatıp **Tamam**.
6. Tıklatın **bu kimlik sağlayıcısı'nı ayarlama**
7. Merhaba girin **uygulama anahtarı** hello daha önce kopyaladığınız **istemci kimliği**.
8. Merhaba girin **uygulama gizli anahtarı** hello daha önce kopyaladığınız **gizli**.
9. Tıklatın **Tamam** ve ardından **oluşturma** toosave Weibo yapılandırmanızı.

