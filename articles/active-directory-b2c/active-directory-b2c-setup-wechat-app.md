---
title: "Azure Active Directory B2C: WeChat yapılandırma | Microsoft Docs"
description: "Uygulamalarınızda Azure Active Directory B2C tarafından güvenliği sağlanan WeChat hesaplarıyla kaydolma ve oturum açma tooconsumers sağlar."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d2424c66-ba68-4d82-847e-d137683527b0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 92cc3579d818d2379a503ccc695138b33a34466d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-wechat-accounts"></a>Azure Active Directory B2C: Kaydolma ve oturum açma tooconsumers WeChat hesaplarıyla sağlayın.

> [!NOTE]
> Bu özelliğin önizlemede değil.
> 

## <a name="create-a-wechat-application"></a>WeChat uygulaması oluşturma

toouse WeChat Azure Active Directory (Azure AD) B2C içinde kimlik sağlayıcısı, toocreate WeChat uygulama gerekir ve hello doğru parametrelerle sağlayın. Bu WeChat hesap toodo gerekir. Yoksa, bir mobil uygulamalarını biri aracılığıyla kaydolan veya h numaranızı kullanarak elde edebilirsiniz. Bundan sonra hesabınızı hello WeChat Geliştirici programla kayıtlı alın. Daha fazla bilgi bulabilirsiniz [burada](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).

### <a name="register-a-wechat-application"></a>WeChat uygulamayı Kaydet

1. Çok Git[https://open.weixin.qq.com/](https://open.weixin.qq.com/) ve oturum açın.
2. Tıklayın**管理中心**(Yönetim Merkezi).
3. Merhaba gerekli adımları tooregister yeni bir uygulama izleyin.
4. İçin**授权回调域**(geri çağırma URL'si) girin `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`. Örneğin, varsa, `tenant_name` contoso.onmicrosoft.com, kümesi hello URL toobe olan `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.
5. Bul ve kopyalama hello **uygulama kimliği** ve **uygulama anahtarı**. Bu bilgiler daha sonra ihtiyacınız olacaktır.

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a>Kimlik sağlayıcısı kiracınızda WeChat yapılandırın
1. Bu adımları çok[toohello B2C özellikleri dikey penceresine gidin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure portalı üzerinde.
2. Merhaba B2C özellikleri dikey penceresinde **kimlik sağlayıcıları**.
3. Tıklatın **+ Ekle** hello dikey penceresinde hello üstünde.
4. Kolay bir sağlamak **adı** hello kimlik sağlayıcı yapılandırması için. Örneğin, "WeChat" girin.
5. Tıklatın **kimlik sağlayıcısı türü**seçin **WeChat**, tıklatıp **Tamam**.
6. Tıklatın **bu kimlik sağlayıcısı'nı ayarlama**
7. Merhaba girin **uygulama anahtarı** hello daha önce kopyaladığınız **istemci kimliği**.
8. Merhaba girin **uygulama gizli anahtarı** hello daha önce kopyaladığınız **gizli**.
9. Tıklatın **Tamam** ve ardından **oluşturma** toosave WeChat yapılandırmanızı.

