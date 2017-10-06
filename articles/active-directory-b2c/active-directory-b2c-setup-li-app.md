---
title: "Azure Active Directory B2C: LinkedIn yapılandırma | Microsoft Docs"
description: "Uygulamalarınızda Azure Active Directory B2C tarafından güvenliği sağlanan LinkedIn hesaplarıyla kaydolma ve oturum açma tooconsumers sağlayın"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: fa51a16b-9ce9-4e27-9eff-0869b4c4f0ef
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6c5233ef48b24968fd6383f470b5d8a969a78ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-linkedin-accounts"></a>Azure Active Directory B2C: Kaydolma ve oturum açma tooconsumers LinkedIn hesaplarıyla sağlayın.
## <a name="create-a-linkedin-application"></a>Bir LinkedIn uygulaması oluşturma
toouse LinkedIn Azure Active Directory (Azure AD) B2C içinde kimlik sağlayıcısı, toocreate LinkedIn uygulama gerekir ve hello doğru parametrelerle sağlayın. Bu bir LinkedIn hesap toodo gerekir. Bir sahip değilseniz, yerinde edinebilirsiniz [https://www.linkedin.com/](https://www.linkedin.com/).

1. Toohello Git [LinkedIn geliştiricilerin Web sitesi](https://www.developer.linkedin.com/) ve LinkedIn hesabı kimlik bilgilerinizle oturum açın.
2. Tıklatın **My uygulamaları** hello üst menü çubuğu ve ardından **uygulama oluştur**.
   
    ![LinkedIn - yeni uygulama](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. Merhaba, **yeni bir uygulama oluşturmak** formunda, hello ilgili bilgileri doldurun (**şirket adı**, **adı**, **açıklama**, **Uygulama Logo URL'si**, **uygulama kullanımı**, **Web sitesi URL'si**, **iş e-posta** ve **iş telefonu**).
4. Toohello kabul **LinkedIn API Kullanım Koşulları'nı** tıklatıp **gönderme**.
   
    ![LinkedIn - kayıt uygulama](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. Merhaba değerlerini kopyalamayı **istemci kimliği** ve **gizli**. (Bunları altında bulabilirsiniz **kimlik doğrulaması anahtarları**.) Bunların her ikisi gerekir tooconfigure LinkedIn kiracınızda kimlik sağlayıcısı.
   
   > [!NOTE]
   > **İstemci parolası** önemli güvenlik kimlik bilgileri.
   > 
   > 
6. Girin `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` hello içinde **yönlendirme URL'si yetkili** alan (altında **OAuth 2.0**). Değiştir **{tenant}** , kiracının adlı (örneğin, contoso.onmicrosoft.com). Tıklatın **Ekle**ve ardından **güncelleştirme**. Merhaba **{tenant}** duyarlıdır.
   
    ![LinkedIn - Kurulum uygulama](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a>Kimlik sağlayıcısı kiracınızda LinkedIn yapılandırın
1. Bu adımları çok[toohello B2C özellikleri dikey penceresine gidin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure portalı üzerinde.
2. Merhaba B2C özellikleri dikey penceresinde **kimlik sağlayıcıları**.
3. Tıklatın **+ Ekle** hello dikey penceresinde hello üstünde.
4. Kolay bir sağlamak **adı** hello kimlik sağlayıcı yapılandırması için. Örneğin, "LI" girin.
5. Tıklatın **kimlik sağlayıcısı türü**seçin **LinkedIn**, tıklatıp **Tamam**.
6. Tıklatın **bu kimlik sağlayıcısı'nı ayarlama** ve hello daha önce oluşturduğunuz LinkedIn uygulama, hello istemci kimliği ve istemci parolasını girin.
7. Tıklatın **Tamam** ve ardından **oluşturma** toosave LinkedIn yapılandırmanızı.

