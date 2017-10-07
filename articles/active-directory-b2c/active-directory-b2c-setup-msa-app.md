---
title: "Azure Active Directory B2C: Microsoft hesabı yapılandırması | Microsoft Docs"
description: "Uygulamalarınızda Azure Active Directory B2C tarafından güvence altına alınan Microsoft hesaplarıyla kaydolma ve oturum açma tooconsumers sağlar."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 06407322-142c-4cb3-9106-a8d752c4c853
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: bec4777f003c459030f68c35b24f0e4bcddf84ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-microsoft-accounts"></a>Azure Active Directory B2C: Kaydolma ve oturum açma tooconsumers Microsoft hesaplarıyla sağlayın.
## <a name="create-a-microsoft-account-application"></a>Bir Microsoft hesabı uygulaması oluşturma
toouse Microsoft hesabı kimlik sağlayıcısı Azure Active Directory (Azure AD) B2C içinde hello doğru parametrelerle tedarik ve toocreate bir Microsoft hesabı uygulaması gerekir. Bu Microsoft hesabı toodo gerekir. Bir sahip değilseniz, yerinde edinebilirsiniz [https://www.live.com/](https://www.live.com/).

1. Toohello Git [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) ve Microsoft hesabı kimlik bilgilerinizle oturum açın.
2. Tıklatın **bir uygulama ekleyin**.
   
    ![Microsoft hesabı - yeni bir uygulama ekleme](./media/active-directory-b2c-setup-msa-app/msa-add-new-app.png)
3. Sağlayan bir **adı** tıklatın ve uygulama için **uygulaması oluşturma**.
   
    ![Microsoft hesabı - uygulama adı](./media/active-directory-b2c-setup-msa-app/msa-app-name.png)
4. Merhaba değerini kopyalayın **uygulama kimliği**. Tooconfigure Microsoft hesabı kimlik sağlayıcısı olarak kiracınızda ihtiyacınız.
   
    ![Microsoft hesabı - uygulama kimliği](./media/active-directory-b2c-setup-msa-app/msa-app-id.png)
5. Tıklayın **Ekle platform** ve **Web**.
   
    ![Microsoft hesabı - platform ekleme](./media/active-directory-b2c-setup-msa-app/msa-add-platform.png)
   
    ![Microsoft hesabı - Web](./media/active-directory-b2c-setup-msa-app/msa-web.png)
6. Girin `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` hello içinde **yeniden yönlendirme URI'ler** alan. Değiştir **{tenant}** , kiracının adlı (örneğin, contosob2c.onmicrosoft.com).
   
    ![Microsoft hesabı - yeniden yönlendirme URL'si](./media/active-directory-b2c-setup-msa-app/msa-redirect-url.png)
7. Tıklayın **yeni bir parola oluşturmak** hello altında **uygulama parolaları** bölümü. Ekranda görüntülenen hello yeni parolayı kopyalayın. Tooconfigure Microsoft hesabı kimlik sağlayıcısı olarak kiracınızda ihtiyacınız. Bu parolayı bir önemli güvenlik kimlik bilgisidir.
   
    ![Microsoft hesabı - yeni bir parola oluştur](./media/active-directory-b2c-setup-msa-app/msa-generate-new-password.png)
   
    ![Microsoft hesabı - yeni parola](./media/active-directory-b2c-setup-msa-app/msa-new-password.png)
8. Bildiren hello kutuyu **Live SDK'sı desteği** hello altında **Gelişmiş Seçenekler** bölümü. **Kaydet** düğmesine tıklayın.
   
    ![Microsoft hesabı - Live SDK'sı desteği](./media/active-directory-b2c-setup-msa-app/msa-live-sdk-support.png)

## <a name="configure-microsoft-account-as-an-identity-provider-in-your-tenant"></a>Microsoft hesabı kimlik sağlayıcısı kiracınızda yapılandırın
1. Bu adımları çok[toohello B2C özellikleri dikey penceresine gidin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure portalı üzerinde.
2. Merhaba B2C özellikleri dikey penceresinde **kimlik sağlayıcıları**.
3. Tıklatın **+ Ekle** hello dikey penceresinde hello üstünde.
4. Kolay bir sağlamak **adı** hello kimlik sağlayıcı yapılandırması için. Örneğin, "MSA" girin.
5. Tıklatın **kimlik sağlayıcısı türü**seçin **Microsoft hesabı**, tıklatıp **Tamam**.
6. Tıklatın **bu kimlik sağlayıcısı'nı ayarlama** hello uygulama kimliği ve hello daha önce oluşturduğunuz Microsoft hesabı uygulama parolasını girin.
7. Tıklatın **Tamam** ve ardından **oluşturma** toosave Microsoft hesabı yapılandırma.

