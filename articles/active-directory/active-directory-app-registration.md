---
title: "aaaAzure Active Directory Uygulama kaydı | Microsoft Docs"
description: "Bu makalede nasıl toouse hello Azure portal tooregister uygulama Azure Active Directory ile açıklanır"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 7dc7b89f-653f-405a-b5f4-2c1288720c15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: priyamo
ms.reviewer: elisol
ms.openlocfilehash: 0134e299dcc53919a6f789a0878a1cf64a8e244d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="register-your-application-with-your-azure-active-directory-tenant"></a>Azure Active Directory kiracınızın ile uygulamanızı kaydetme

Uygulamanız Azure Active Directory (Azure AD) Kiracı ile hello Azure portal tooregister kullanabilirsiniz. Bu hello uygulama için bir uygulama kimliği oluşturur ve tooreceive belirteçleri sağlar.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Azure AD kiracınıza hello sağ üst köşedeki hello sayfasının hesabınızı seçerek belirleyin.
3. Merhaba sol gezinti bölmesinde seçin **daha Hizmetleri**, tıklatın **uygulama kayıtlar**, tıklatıp **Ekle**.
4. Merhaba komut istemlerini izleyin ve yeni bir uygulama oluşturun. Belirli örnekler web uygulamaları veya yerel uygulamaları için isterseniz, kullanıma bizim [quickstarts](active-directory-developers-guide.md).
  * Web uygulamaları için hello sağlamak **oturum açma URL'si**, kullanıcılar, örneğin,'burada oturum açabilir, uygulamanızın hello temel URL olduğu `http://localhost:12345`.
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * Yerel uygulamalar için sağlayan bir **yeniden yönlendirme URI'si**, tooreturn belirteci yanıtları hangi Azure AD kullanır. Bir değer belirli tooyour uygulama girin. Örneğin`http://MyFirstAADApp`
5. Kayıt tamamladıktan sonra Azure AD, uygulamanızın hello uygulama kimliği bir benzersiz istemci tanımlayıcı atar.

## <a name="update-application-settings-from-hello-azure-portal"></a>Hello Azure portalında uygulama ayarlarını güncelleştirme

Kolayca hello Azure portal kullanarak var olan bir uygulamanın ayarlarını değiştirebilirsiniz. Örneğin, burada Azure AD belirteci yanıtları sorunları olan bir yanıt URL'si tooconfigure isteyebilirsiniz. Tooconfigure izinleri tooother uygulamalar da isteyebilirsiniz, örnek tooallow için Microsoft Graph API uygulaması tooaccess hello. Tüm hello uygulama ayarları sayfası üzerinden bunu yapabilirsiniz.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Azure AD kiracınıza hello sağ üst köşedeki hello sayfasının hesabınızı seçerek belirleyin.
3. Merhaba sol gezinti bölmesinde seçin **daha Hizmetleri**, tıklatın **uygulama kayıtlar**ve uygulamanızı hello listeden seçin.
4. Tıklatın **ayarları** tooopen hello ayarları sayfasını Merhaba uygulaması için.
  * Merhaba **özellikleri** sayfa hello uygulaması hello genel bilgilerini değiştirmenize olanak sağlar. Bu, hello uygulama adı, hello oturum açma URL'si ve hello oturum kapatma URL'sini içerir.
  * Merhaba **yanıt URL'leri** sayfası tooadd burada Azure AD belirteci yanıtları gönderir olan bir yanıt URL'si sağlar.
  * Merhaba **sahipleri** sayfası tooadd uygulama sahipleri sağlar.
  * Merhaba **izinleri** sayfası hello uygulama tooconfigure izinlerini verir. Örneğin, tooaccess hello Microsoft Graph API tıklayın **Ekle** seçip **Microsoft Graph** hello API seçicide hello izin gerekiyor, örneğin seçin **dizin verilerini okuma** .
  * Merhaba **anahtarları** sayfası tooadd uygulama parolaları sağlar. Hello gizli yalnızca bir kez görüntülenir hemen oluşturulduktan sonra bu nedenle emin toocopy yapmak için daha fazla kullanılmasını.

## <a name="use-hello-inline-manifest-editor"></a>Merhaba satır içi bildirim Düzenleyicisi'ni kullanın

Merhaba satır içi bildirim Düzenleyicisi toomodify doğrudan gösterilmeyen uygulama özelliklerini Azure portal hello belirli kullanabilirsiniz. Örneğin, toomodify hello uygulamanın uygulama kimliği URI'sini kullanın veya tooenable hello OAuth2.0 örtük akış hello varsayılan yetkilendirme yerine izin kodu akışı.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Azure AD kiracınıza hello sağ üst köşedeki hello sayfasının hesabınızı seçerek belirleyin.
3. Merhaba sol gezinti bölmesinde seçin **daha Hizmetleri**, tıklatın **uygulama kayıtlar**ve uygulamanızı hello listeden seçin.
4. Tıklatın **bildirim** düzenleyicisinden hello uygulama sayfası tooopen hello satır içi bildirim.
5. Bildirim ve hazır olduğunuzda kaydedin değişiklikleri toohello doğrudan yapabilirsiniz. Alternatif olarak, hello bildirim tooopen indirebilirsiniz bildirimi sık kullanılan Düzenleyicisi ve karşıya yükleme hello içinde güncelleştirildi.

## <a name="next-steps"></a>Sonraki Adımlar

1. Merhaba denetleyin [Quickstarts](active-directory-developers-guide.md) ayrıntılı talimatları uygulamaları Azure AD kullanarak kimlik doğrulaması gerçekleştirmek için.
2. Tam kod örnekleri listemiz kullanıma [GitHub](https://github.com/azure-samples).
