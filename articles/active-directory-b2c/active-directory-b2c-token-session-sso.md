---
title: "Azure Active Directory B2C: Belirteci, oturum ve tek oturum açma yapılandırması | Microsoft Docs"
description: "Belirteç, oturum ve Azure Active Directory B2C, tek oturum açma yapılandırması"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: e78e6344-0089-49bf-8c7b-5f634326f58c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: swkrish
ms.openlocfilehash: 63325ed97a7363723c97ee3a992046ebb5592662
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-token-session-and-single-sign-on-configuration"></a>Azure Active Directory B2C: Belirteci, oturum ve tek oturum açma yapılandırması
Bu özellik, hassas bir denetim üzerinde sunar bir [ilke başına temel](active-directory-b2c-reference-policies.md), biri:

1. Azure Active Directory (Azure AD) B2C tarafından gösterilen güvenlik belirteçlerinin yaşam süresi.
2. Azure AD B2C tarafından yönetilen web uygulama oturumları ömürleri.
3. Azure AD B2C tarafından gösterilen hello güvenlik belirteçleri önemli Taleplerde biçimleri.
4. Çoklu oturum açma (SSO) davranışı birden çok uygulamalar ve ilkeler B2C kiracınızda arasında.

Bu özellik, B2C kiracınızda gibi kullanabilirsiniz:

1. Bu adımları çok[toohello B2C özellikleri dikey penceresine gidin](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) hello Azure portalı üzerinde.
2. Tıklatın **oturum açma ilkeleri**. *Not: Bu özellik tüm ilke türüne açık değil yalnızca kullanabileceğiniz **oturum açma ilkeleri***.
3. Bir ilke tıklatarak açın. Örneğin, tıklayın **B2C_1_SiIn**.
4. Tıklatın **Düzenle** hello dikey penceresinde hello üstünde.
5. Tıklatın **belirteci, oturum ve çoklu oturum açma config**.
6. İstediğiniz değişiklikleri yapın. Sonraki bölümlerde kullanılabilir özellikler hakkında bilgi edinin.
7. **Tamam** düğmesine tıklayın.
8. Tıklatın **kaydetmek** hello dikey hello üstte.

## <a name="token-lifetimes-configuration"></a>Belirteç yaşam süreleri yapılandırma
Azure AD B2C destekleyen hello [OAuth 2.0 yetkilendirme protokolünü](active-directory-b2c-reference-protocols.md) tooprotected kaynaklarına güvenli erişim etkinleştirmek için. tooimplement Bu destek, Azure AD B2C çeşitli yayar [güvenlik belirteçleri](active-directory-b2c-reference-tokens.md). Azure AD B2C tarafından gösterilen güvenlik belirteçlerinin toomanage yaşam süreleri bir hello özellikleri şunlardır:

* **Erişim & kimliği belirteci yaşam süresi (dakika)**: hello OAuth 2.0 taşıyıcı belirteci kullanılan toogain erişim tooa hello ömrü korumalı kaynak. Azure AD B2C şu anda yalnızca kimliği belirteçleri verir. Biz bunları desteği eklediğinizde, bu değer tooaccess belirteçleri de geçerli olur.
  * Varsayılan = 60 dakika.
  * Minimum (dahil) = 5 dakika.
  * Maksimum (dahil) = 1440 dakika.
* **Belirteç ömrü Yenile (gün)**: en fazla süre önce bir yenileme belirteci olabilen kullanılan tooacquire yeni erişim veya kimliği belirteci hello (ve uygulamanızı hello yeterliyse isteğe bağlı olarak, yeni bir yenileme belirteci, `offline_access` kapsam).
  * Varsayılan = 14 gün.
  * (Dahil) en az 1 gün =.
  * Maksimum (dahil) = 90 gün.
* **Yenileme belirteci kayan pencere ömrü (gün)**: Bu süre geçtikten hello kullanıcı zorlanmış toore sonra-hello hello uygulama tarafından alınan en son yenileme belirteci hello geçerlilik süresini bağımsız olarak kimlik doğrulaması. Başlangıç anahtarı çok ayarlanırsa yalnızca sağlanabilir**Bounded**. Toobe daha büyük veya eşit toohello gereken **yenileme belirteci yaşam süresi (gün)** değeri. Başlangıç anahtarı çok ayarlanırsa**Unbounded**, belirli bir değer sağlayamaz.
  * Varsayılan = 90 gün.
  * (Dahil) en az 1 gün =.
  * Maksimum (dahil) = 365 gün.

Bu, birkaç bu özellikleri kullanarak etkinleştirebilirsiniz kullanım örnekleri şunlardır:

* Çözemiyorsa Merhaba uygulaması sürekli olarak etkin olduğu sürece bir mobil uygulamasına süresiz olarak, imzalanmış bir kullanıcı toostay izin verir. Bu ayarı hello tarafından yapabilirsiniz **yenileme belirteci kayan pencere yaşam süresi (gün)** çok geçiş**Unbounded** ilkenizde oturum açma.
* Merhaba uygun erişim belirteci yaşam süresi ayarlayarak, sektörün güvenlik ve uyumluluk gereksinimlerini karşılar.

    > [!NOTE]
    > Bu ayarları ilkeleri parola sıfırlama için kullanılabilir değil.
    > 
    > 

## <a name="token-compatibility-settings"></a>Belirteç uyumluluk ayarları
Azure AD B2C tarafından gösterilen güvenlik belirteçlerinde biçimlendirme değişiklikleri tooimportant talep yapılan. Bu bizim standart protokol desteği tooimprove yapılır ve üçüncü taraf kimlik kitaplıkları ile daha iyi birlikte çalışabilirlik. Ancak, tooavoid sonu var olan uygulamalar, Özellikler tooallow müşteriler tooopt-gerektiği gibi aşağıdaki hello oluşturduk:

* **Veren (ISS) talep**: Bu hello belirteç hello Azure AD B2C Kiracı tanımlar.
  * `https://login.microsoftonline.com/{B2C tenant GUID}/v2.0/`: Bu hello varsayılan değerdir.
  * `https://login.microsoftonline.com/tfp/{B2C tenant GUID}/{Policy ID}/v2.0/`: Bu değer kimlikleri hello B2C Kiracı ve hello belirteci istekte kullanılan hello İlkesi içerir. Uygulama veya kitaplık Azure AD B2C toobe hello uyumlu gerekip gerekmediğini [Openıd Connect bulma 1.0 belirtimi](http://openid.net/specs/openid-connect-discovery-1_0.html), bu değeri kullanın.
* **Konu (alt) talep**: Bu hello varlık, yani, hangi Merhaba belirteci onaylar bilgi hello kullanıcı tanımlar.
  * **ObjectID**: hello varsayılan değer budur. Merhaba hello nesne hello dizininde hello kullanıcı Kimliğini doldurur `sub` hello belirteçte talep.
  * **Desteklenmeyen**: Bu, yalnızca geriye dönük uyumluluk için sağlanır ve çok geçiş öneririz**objectID** yapabileceksiniz hemen sonra.
* **İlke kimliği temsil eden talep**: Bu hangi hello hello belirteci istekte kullanılan ilke kimliği doldurulur hello talep türü tanımlar.
  * **tfp**: hello varsayılan değer budur.
  * **ACR**: Bu, yalnızca geriye dönük uyumluluk için sağlanır ve çok geçiş öneririz`tfp` yapabileceksiniz hemen sonra.

## <a name="session-behavior"></a>Oturum davranışı
Azure AD B2C destekleyen hello [Openıd Connect kimlik doğrulama protokolü](active-directory-b2c-reference-oidc.md) güvenli oturum açma tooweb uygulamaları etkinleştirme. Toomanage web uygulama oturumları bir hello özellikleri şunlardır:

* **Web uygulaması oturum yaşam süresi (dakika)**: Azure AD B2C'ın oturum tanımlama bilgisi hello kullanıcının tarayıcısının başarılı bir kimlik doğrulaması sırasında depolanan hello ömrü.
  * Varsayılan = 1440 dakika.
  * Minimum (dahil) = 15 dakika.
  * Maksimum (dahil) = 1440 dakika.
* **Web uygulaması oturum zaman aşımı**: Bu anahtarı çok ayarlanırsa**mutlak**, hello kullanıcıdır zorlanmış toore-hello tarafından belirtilen bir süre sonra kimlik doğrulaması **Web uygulaması oturum yaşam süresi (dakika)** sona erdiğinde. Bu anahtarı çok ayarlanırsa**çalışırken** (varsayılan ayar hello) hello kullanıcı web uygulamanızda sürekli etkin olduğu sürece hello kullanıcı oturum açmış durumda kalır.

Bu, birkaç bu özellikleri kullanarak etkinleştirebilirsiniz kullanım örnekleri şunlardır:

* Merhaba uygun web uygulaması oturum ayarlayarak, sektörün güvenlik ve uyumluluk gereksinimlerini karşılayan yaşam süresi yok.
* Yeniden kimlik doğrulama işleminden sonra ayarlanmış bir süre içinde web uygulamanızı yüksek güvenlikli bir parçası olan bir kullanıcı etkileşimi zorlar. 

    > [!NOTE]
    > Bu ayarları ilkeleri parola sıfırlama için kullanılabilir değil.
    > 
    > 

## <a name="single-sign-on-sso-configuration"></a>Çoklu oturum açma (SSO) yapılandırma
B2C kiracınızda birden çok uygulama ve ilkeleri varsa, kullanıcı etkileşimleri arasında gezinmek yönetebileceğiniz hello kullanarak **tek oturum açma yapılandırması** özelliği. Merhaba özelliği tooone ayarları aşağıdaki Merhaba, ayarlayabilirsiniz:

* **Kiracı**: hello varsayılan ayar budur. Bu ayarı kullanarak sağlayan birden çok uygulama ve ilkeleri B2C kiracınızda tooshare hello aynı kullanıcı oturumu. Bir uygulamaya bir kullanıcı oturum açtığında sonra Örneğin, Contoso alışveriş buldukça, aynı zamanda sorunsuz bir şekilde başka bir, Contoso erişmekte bağlı ilaç, içine oturum açabilirsiniz.
* **Uygulama**: Bu, bir kullanıcı oturumunu diğer uygulamaları bağımsız bir uygulama için özel olarak toomaintain sağlar. Merhaba kullanıcı toosign tooContoso ilaç içinde isterseniz, örneğin, (Merhaba ile aynı kimlik bilgileri), isterse zaten Contoso alışveriş, hello üzerinde başka bir uygulama içinde imzalansa bile aynı B2C Kiracı. 
* **İlke**: Bu, bir kullanıcı oturumunu hello uygulamaları kullanmaya bağımsız bir ilke için özel olarak toomaintain sağlar. Merhaba kullanıcı daha önce açtığınız ve çok faktörlü kimlik doğrulama (MFA) adımını tamamlamış, hello bağlı oturum toohello İlkesi kullanım süresi sona ermiyor sürece Örneğin, isterse erişim toohigher güvenlik birden çok uygulama bölümlerini verilebilir.
* **Devre dışı**: Bu hello kullanıcı toorun hello tüm kullanıcı gezisine aracılığıyla hello İlkesi her yürütülmesini zorlar. Örneğin, bu tooyour uygulamasının (bir senaryoda paylaşılan Masaüstü), birden çok kullanıcı toosign hello tüm süre boyunca tek bir kullanıcı oturum açmış durumda devam ederken bile izin verir.

    > [!NOTE]
    > Bu ayarları ilkeleri parola sıfırlama için kullanılabilir değil.
    > 
    > 

