---
title: "Azure Active Directory B2C: Amazon yapılandırma | Microsoft Docs"
description: "Uygulamalarınızda Azure Active Directory B2C tarafından güvenliği sağlanan Amazon hesaplarıyla kaydolma ve oturum açma tooconsumers sağlar."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 77c099bb-a005-4d75-87f9-f61e3de48725
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 60d7c4b76d9d3e86ed535765329abed07f1e5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-amazon-accounts"></a>Azure Active Directory B2C: Kaydolma ve oturum açma tooconsumers Amazon hesabıyla sağlayın.
## <a name="create-an-amazon-application"></a>Amazon uygulama oluşturma
toouse Amazon Azure Active Directory (Azure AD) B2C içinde kimlik sağlayıcısı, toocreate Amazon uygulamanın gereksinim ve hello doğru parametrelerle sağlayın. Bu bir Amazon hesap toodo gerekir. Bir sahip değilseniz, yerinde edinebilirsiniz [http://www.amazon.com/](http://www.amazon.com/).

1. Toohello Git [Amazon Geliştirici Merkezi](https://login.amazon.com/) ve Amazon hesabı kimlik bilgilerinizle oturum açın.
2. Zaten yapmadıysanız, tıklatın **kaydolun**hello Geliştirici kayıt adımları izleyin ve hello İlkesi kabul edin.
3. Tıklatın **kaydetmek yeni uygulama**.
   
    ![Yeni bir uygulama hello Amazon Web sitesindeki kaydetme](./media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. Uygulama bilgilerini sağlayın (**adı**, **açıklama**, ve **gizlilik bildirimi URL'si**) tıklatıp **kaydetmek**.
   
    ![Amazon en yeni bir uygulama kaydetmeye yönelik uygulama bilgileri sağlama](./media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. Merhaba, **Web ayarları** bölümünde, kopyalama hello değerlerini **istemci kimliği** ve **gizli**. (Tooclick hello ihtiyacınız **Göster gizli** toosee bu düğmesine tıklayın.) Her ikisine de ihtiyacınız tooconfigure Amazon kiracınızda kimlik sağlayıcısı. Tıklatın **Düzenle** hello bölümünün hello altındaki. **İstemci parolası** önemli güvenlik kimlik bilgileri.
   
    ![Yeni uygulamanızı Amazon için istemci kimliği ve istemci parolası sağlama](./media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. Girin `https://login.microsoftonline.com` hello içinde **izin JavaScript çıkış** alan ve `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` hello içinde **dönüş URL'leri izin** alan. Değiştir **{tenant}** , kiracının adlı (örneğin, contoso.onmicrosoft.com). **Kaydet** düğmesine tıklayın. Merhaba **{tenant}** duyarlıdır.
   
    ![Yeni uygulamanızı Amazon için JavaScript kaynakları ve dönüş URL'leri sağlama](./media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a>Kimlik sağlayıcısı kiracınızda Amazon yapılandırın
1. Bu adımları çok[toohello B2C özellikleri dikey penceresine gidin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure portalı üzerinde.
2. Merhaba B2C özellikleri dikey penceresinde **kimlik sağlayıcıları**.
3. Tıklatın **+ Ekle** hello dikey penceresinde hello üstünde.
4. Kolay bir sağlamak **adı** hello kimlik sağlayıcı yapılandırması için. Örneğin, "Amzn" girin.
5. Tıklatın **kimlik sağlayıcısı türü**seçin **Amazon**, tıklatıp **Tamam**.
6. Tıklatın **bu kimlik sağlayıcısı'nı ayarlama** ve hello daha önce oluşturduğunuz Amazon uygulama, hello istemci kimliği ve istemci parolasını girin.
7. Tıklatın **Tamam** ve ardından **oluşturma** toosave Amazon yapılandırmanızı.

