---
title: "Azure AD için aaaDevelop uygulamalar | Microsoft Docs"
description: "Hello BT Uzmanı yazılmış, Azure uygulamalarını Active Directory ile tümleştirme için bu makaleyi kılavuz bilgiler verilmektedir."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: dd69f2bc-37c5-457c-857d-27acb84267fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2924be752af0be2843b1d9b74d9ec446d3fe1ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a>Azure Active Directory için satır iş kolu uygulamaları geliştirme
Bu kılavuz, Azure Active Directory (AD) .hello için satır iş kolu (LoB) uygulamaları geliştirme genel bir bakış İzleyici Active Directory/Office 365 genel Yöneticiler amaçlanmıştır sağlar.

## <a name="overview"></a>Genel Bakış
Azure AD ile tümleşik uygulamaları oluşturmak, kuruluş çoklu oturum açma Office 365 ile kullanıcılara sağlar. Merhaba uygulaması hello Merhaba uygulaması için kimlik doğrulama ilkesini üzerinden denetim Azure AD sağlar bulundurmak. koşullu erişim ve çok faktörlü kimlik doğrulaması (MFA) tooprotect uygulamalarla nasıl görürüm hakkında daha fazla toolearn [yapılandırma erişim kuralları](active-directory-conditional-access-azuread-connected-apps.md).

Uygulama toouse Azure Active Directory'ye kaydedin. Merhaba Uygulaması kaydettirilirken, geliştiricilerin Azure AD tooauthenticate kullanıcıları kullanın ve e-posta, Takvim ve belgeler gibi erişim toouser kaynakları isteği anlamına gelir.

Aksi takdirde olarak bilinen bir uygulama dizininize (Konuklar değil) herhangi bir üyenin kaydedebilirsiniz *uygulama nesnesi oluşturma*.

Uygulama kaydetme hiçbir kullanıcı toodo hello aşağıdakileri sağlar:

* Azure AD tanıdığı kendi uygulama için bir kimlik alma
* Edinebileceğinizi veya daha fazla gizli/uygulama hello anahtarları tooAD tooauthenticate kendisini kullanabilirsiniz
* Merhaba uygulamada hello Azure portalı özel adı, logosu, vb. ile marka.
* Azure AD yetkilendirme özellikleri tootheir uygulama geçerli dahil olmak üzere:

  * Rol Tabanlı Erişim Denetimi (RBAC)
  * OAuth yetkilendirme sunucusu olarak Azure Active Directory (Merhaba uygulaması tarafından sunulan bir API güvenli)
* Gerekli izinleri hello uygulama toofunction için gerekli dahil olmak üzere, beklendiği gibi bildirin:

      - Uygulama izinleri (yalnızca genel Yöneticiler). Örneğin: başka bir Azure AD uygulama veya rol üyeliğini göreli tooan Azure kaynak, kaynak grubu, rol üyeliğini veya abonelik
      - Temsilci izinleri (herhangi bir kullanıcı). Örneğin: Azure AD oturum açma ve okuma profili

> [!NOTE]
> Varsayılan olarak, bir uygulama herhangi bir üyenin kaydedebilirsiniz. uygulamaları toospecific üyeleri kaydettirmek için toorestrict izinleri nasıl görürüm toolearn [tooAzure AD uygulamaları nasıl eklenir](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).
>
>

Burada hangi, hello genel yönetici, kendi uygulama toodo toohelp geliştiriciler üretime hazır olun:

* Erişim kuralları (erişim ilkesi/MFA) yapılandırma
* Merhaba uygulama toorequire kullanıcı ataması yapılandırın ve kullanıcılar atayın
* Merhaba varsayılan kullanıcı onayı deneyimi gösterme

## <a name="configure-access-rules"></a>Erişim kuralları yapılandırın
Uygulama başına erişim kuralları tooyour SaaS uygulamalarını yapılandırın. Örneğin, MFA gerektirecek veya yalnızca güvenilen ağlarda erişim toousers izin verebilirsiniz. Bu Hello ayrıntılarını hello belgede kullanılabilir [yapılandırma erişim kuralları](active-directory-conditional-access-azuread-connected-apps.md).

## <a name="configure-hello-app-toorequire-user-assignment-and-assign-users"></a>Merhaba uygulama toorequire kullanıcı ataması yapılandırın ve kullanıcılar atayın
Varsayılan olarak, kullanıcılar atanmadan uygulamalarına erişebilir. Ancak, hello uygulama rolleri gösterir veya bir kullanıcının erişim panelinde hello uygulama tooappear istiyorsanız, kullanıcı ataması istemeniz gerekir.

[Kullanıcı ataması gerektirme](active-directory-applications-guiding-developers-requiring-user-assignment.md)

Bir Azure AD Premium veya Enterprise Mobility Suite (EMS) abone değilseniz, grupları kullanmanızı öneririz. Toohello uygulama grupları atama toodelegate sürekli erişim yönetimi toohello hello grubun sahibi sağlar. Merhaba grubu oluşturun veya Grup Yönetimi özelliğini kullanarak kuruluş toocreate hello grubunuzdaki hello sorumlu taraf isteyin.

[Kullanıcıları tooan uygulama atama](active-directory-applications-guiding-developers-assigning-users.md)  
[Tooan uygulama grupları atama](active-directory-applications-guiding-developers-assigning-groups.md)

## <a name="suppress-user-consent"></a>Kullanıcı izni gösterme
Varsayılan olarak, her kullanıcı onayı deneyimi toosign geçer. tooan uygulaması, kullanıcıların toogrant izinleri isteyen hello onayı deneyimi böyle kararları ile ilgili bilginiz kullanıcılar için disconcerting olabilir.

Güvendiğiniz uygulamalar için kuruluşunuz adına onaylıyorsunuz toohello uygulama tarafından hello kullanıcı deneyimi basitleştirebilirsiniz.

Kullanıcı izni ve hello izin hakkında daha fazla bilgi için Azure'da deneyimi, bkz: [Azure Active Directory Tümleştirme uygulamalarla](active-directory-integrating-applications.md).

## <a name="related-articles"></a>İlgili makaleler
* [Azure AD uygulama proxy'si tooon içi uygulamalara güvenli uzaktan erişim etkinleştir](active-directory-application-proxy-get-started.md)
* [SaaS uygulamaları için Azure koşullu erişim önizlemesi](active-directory-conditional-access-azuread-connected-apps.md)
* [Azure AD ile erişim tooapps yönetme](active-directory-managing-access-to-apps.md)
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)
