---
title: "Azure Active Directory B2C: Google + yapılandırma | Microsoft Docs"
description: "Uygulamalarınızda Azure Active Directory B2C tarafından güvence altına alınan Google + hesapları ile kaydolma ve oturum açma tooconsumers sağlar."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 4dcca66f-29e4-4b4d-8840-50baad736bd7
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6ef66eb17777acd95b5f4745ed6097c77e37663b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-google-accounts"></a>Azure Active Directory B2C: Kaydolma ve oturum açma tooconsumers Google + hesaplarıyla sağlayın.
## <a name="create-a-google-application"></a>Bir Google + uygulama oluşturma
toouse Google + Azure Active Directory (Azure AD) B2C içinde kimlik sağlayıcısı, toocreate Google + uygulama gerekir ve hello doğru parametrelerle sağlayın. Bu bir Google + hesap toodo gerekir. Bir sahip değilseniz, yerinde edinebilirsiniz [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).

1. Toohello Git [Google geliştiriciler konsol](https://console.developers.google.com/) ve Google + hesabı kimlik bilgilerinizle oturum açın.
2. Tıklatın **proje oluştur**, girin bir **proje adı**ve ardından **oluşturma**.
   
    ![Google + - kullanmaya başlama](./media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google + - yeni proje](./media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. Tıklatın **API Yöneticisi** ve ardından **kimlik bilgileri** sol gezinti hello içinde.
4. Merhaba tıklatın **OAuth izni ekran** sekmesini hello üstünde.
   
    ![Google + - kimlik bilgileri](./media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. Seçin veya geçerli bir belirtin **e-posta adresi**, sağlayan bir **ürün adı**, tıklatıp **kaydetmek**.
   
    ![Google + - OAuth onay ekranı](./media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. Tıklatın **yeni kimlik bilgileri** ve ardından **OAuth istemci kimliği**.
   
    ![Google + - OAuth onay ekranı](./media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. Altında **uygulama türü**seçin **Web uygulaması**.
   
    ![Google + - OAuth onay ekranı](./media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. Sağlamak bir **adı** , uygulamanız için girin `https://login.microsoftonline.com` hello içinde **yetkili JavaScript çıkış** alan, ve `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` hello içinde **yetkili URI'leryenidenyönlendirme**alan. Değiştir **{tenant}** , kiracının adlı (örneğin, contosob2c.onmicrosoft.com). Merhaba **{tenant}** duyarlıdır. **Oluştur**'a tıklayın.
   
    ![Google + - istemci kodu oluştur](./media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. Merhaba değerlerini kopyalamayı **istemci kimliği** ve **gizli**. Bunların her ikisi gerekir tooconfigure Google + kiracınızda kimlik sağlayıcısı. **İstemci parolası** önemli güvenlik kimlik bilgileri.
   
    ![Google + - gizli](./media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a>Google + kiracınızda kimlik sağlayıcısı yapılandırma
1. Bu adımları çok[toohello B2C özellikleri dikey penceresine gidin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure portalı üzerinde.
2. Merhaba B2C özellikleri dikey penceresinde **kimlik sağlayıcıları**.
3. Tıklatın **+ Ekle** hello dikey penceresinde hello üstünde.
4. Kolay bir sağlamak **adı** hello kimlik sağlayıcı yapılandırması için. Örneğin, "G +" girin.
5. Tıklatın **kimlik sağlayıcısı türü**seçin **Google**, tıklatıp **Tamam**.
6. Tıklatın **bu kimlik sağlayıcısı'nı ayarlama** ve hello daha önce oluşturduğunuz Google + uygulama, hello istemci kimliği ve istemci parolasını girin.
7. Tıklatın **Tamam** ve ardından **oluşturma** toosave Google + yapılandırmanızı.

