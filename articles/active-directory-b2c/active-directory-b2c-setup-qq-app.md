---
title: "Azure Active Directory B2C: H yapılandırma | Microsoft Docs"
description: "Uygulamalarınızda Azure Active Directory B2C tarafından güvenliği sağlanan h hesaplarıyla kaydolma ve oturum açma tooconsumers sağlar."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 18c2cf94-8004-4de1-81c2-e45be65ce12d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 896d6221e01d15de1652a5717cf1f65619101e0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-qq-accounts"></a>Azure Active Directory B2C: Kaydolma ve oturum açma tooconsumers h hesaplarıyla sağlayın.

> [!NOTE]
> Bu özelliğin önizlemede değil.
> 

## <a name="create-a-qq-application"></a>H uygulaması oluşturma

toouse h Azure Active Directory (Azure AD) B2C içinde kimlik sağlayıcısı, toocreate h uygulama gerekir ve hello doğru parametrelerle sağlayın. Bu h hesap toodo gerekir. Yoksa, her seferde alabilirsiniz [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).

### <a name="register-for-hello-qq-developer-program"></a>Merhaba h developer program kaydolun

1. Toohello Git [h Geliştirici Portalı](http://open.qq.com) ve h hesabı kimlik bilgilerinizle oturum açın.
2. Oturum açtıktan sonra çok Git[http://open.qq.com/reg](http://open.qq.com/reg) tooregister kendiniz bir geliştirici olarak.
3. Merhaba menüde seçin**个人**(bireysel Geliştirici).
4. Merhaba forma hello gerekli bilgileri girin ve tıklatın**下一步**(sonraki adım).
5. Merhaba e-posta doğrulama işlemini tamamlayın.

> [!NOTE]
> Geliştirici olarak kaydolduktan sonra onaylanmış birkaç gün toobe toowait gerekir. 

### <a name="register-a-qq-application"></a>H uygulamayı Kaydet

1. Çok Git[https://connect.qq.com/index.html](https://connect.qq.com/index.html).
2. Tıklayın**应用管理**(Uygulama Yönetimi).
3. Tıklayın**创建应用**(Uygulama Oluştur).
4. Merhaba gerekli uygulama bilgileri girin.
5. Tıklayın**创建应用**(Uygulama Oluştur).
6. Merhaba gerekli bilgileri girin.
7. Hello için**授权回调域**(geri çağırma URL'si) alanına, `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`. Örneğin, varsa, `tenant_name` contoso.onmicrosoft.com, kümesi hello URL toobe olan `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.
8. Tıklayın**创建应用**(Uygulama Oluştur).
9. Merhaba onay sayfasında tıklayın**应用管理**(Uygulama Yönetimi) tooreturn toohello Uygulama Yönetimi sayfasında.
10. Tıklayın**查看**(Görünüm), yeni oluşturduğunuz sonraki toohello uygulama.
11. Tıklayın**修改**(Düzenle).
12. Merhaba sayfa Hello üstten hello kopyalama **uygulama kimliği** ve **uygulama anahtarı**.

## <a name="configure-qq-as-an-identity-provider-in-your-tenant"></a>Kimlik sağlayıcısı kiracınızda h yapılandırın
1. Bu adımları çok[toohello B2C özellikleri dikey penceresine gidin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure portalı üzerinde.
2. Merhaba B2C özellikleri dikey penceresinde **kimlik sağlayıcıları**.
3. Tıklatın **+ Ekle** hello dikey penceresinde hello üstünde.
4. Kolay bir sağlamak **adı** hello kimlik sağlayıcı yapılandırması için. Örneğin, "H" girin.
5. Tıklatın **kimlik sağlayıcısı türü**seçin **h**, tıklatıp **Tamam**.
6. Tıklatın **bu kimlik sağlayıcısı'nı ayarlama**
7. Merhaba girin **uygulama anahtarı** hello daha önce kopyaladığınız **istemci kimliği**.
8. Merhaba girin **uygulama gizli anahtarı** hello daha önce kopyaladığınız **gizli**.
9. Tıklatın **Tamam** ve ardından **oluşturma** toosave h yapılandırmanızı.

