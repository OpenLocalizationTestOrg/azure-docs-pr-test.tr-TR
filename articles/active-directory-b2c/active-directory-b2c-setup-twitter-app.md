---
title: "Azure Active Directory B2C: Twitter yapılandırma | Microsoft Docs"
description: "Uygulamalarınızda Azure Active Directory B2C tarafından güvenliği sağlanan Twitter hesaplarıyla kaydolma ve oturum açma tooconsumers sağlar."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 579a6841-9329-45b8-a351-da4315a6634e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/06/2017
ms.author: parakhj
ms.openlocfilehash: 275c5c73fd5e8e5075e77fee942cbc1b5e1586cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-twitter-accounts"></a>Azure Active Directory B2C: Kaydolma ve oturum açma tooconsumers Twitter hesaplarıyla sağlayın.

> [!NOTE]
> Bu özelliğin önizlemede değil.
> 

## <a name="create-a-twitter-application"></a>Bir Twitter uygulaması oluşturma
toouse Twitter kimlik sağlayıcısı Azure Active Directory (Azure AD) B2C içinde hello doğru parametrelerle sağlayın ve toocreate bir Twitter uygulaması gerekir. Bu bir Twitter Geliştirici hesabı toodo gerekir. Bir sahip değilseniz, yerinde edinebilirsiniz [https://dev.twitter.com/](https://dev.twitter.com/).

1. Toohello Git [Geliştirici Web sitesi Twitter](https://dev.twitter.com/) ve kimlik bilgilerinizle oturum açın.
2. Tıklatın **uygulamalarım** altında **araçları ve Destek** ve ardından **yeni uygulama oluşturma**. 
3. Merhaba biçiminde hello için bir değer sağlayın **adı**, **açıklama**, ve **Web sitesi**.
4. Hello için **geri çağırma URL'si**, girin `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`. Emin tooreplace olun **{tenant}** , kiracının adlı (örneğin, contosob2c.onmicrosoft.com).
5. Merhaba kutusunu tooagree toohello denetleyin **Geliştirici anlaşma** tıklatıp **Twitter uygulamanızı oluşturma**.
6. Merhaba uygulama oluşturulduktan sonra tıklatın **anahtarları ve erişim belirteçleri**.
7. Merhaba değerini kopyalayın **tüketici anahtarı** ve **tüketici gizli**. Bunların her ikisi gerekir tooconfigure Twitter kiracınızda kimlik sağlayıcısı.

## <a name="configure-twitter-as-an-identity-provider-in-your-tenant"></a>Twitter kimlik sağlayıcısı kiracınızda yapılandırın
1. Bu adımları çok[toohello B2C özellikleri dikey penceresine gidin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure portalı üzerinde.
2. Merhaba B2C özellikleri dikey penceresinde **kimlik sağlayıcıları**.
3. Tıklatın **+ Ekle** hello dikey penceresinde hello üstünde.
4. Kolay bir sağlamak **adı** hello kimlik sağlayıcı yapılandırması için. Örneğin, "Twitter" girin.
5. Tıklatın **kimlik sağlayıcısı türü**seçin **Twitter**, tıklatıp **Tamam**.
6. Tıklatın **bu kimlik sağlayıcısı'nı ayarlama** ve hello Twitter girin **tüketici anahtarı** hello için **istemci kimliği** ve Twitter hello **tüketici gizli**hello için **gizli**.
7. Tıklatın **Tamam**ve ardından **oluşturma** toosave Twitter yapılandırmanızı.

