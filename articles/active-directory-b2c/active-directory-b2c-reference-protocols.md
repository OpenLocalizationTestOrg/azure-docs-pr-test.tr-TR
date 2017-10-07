---
title: "Azure Active Directory B2C: Kimlik doğrulama protokolleri | Microsoft Docs"
description: "Azure Active Directory B2C tarafından desteklenen protokolleri kullanarak doğrudan toobuild uygulamaları nasıl hello"
services: active-directory-b2c
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5e407d0a-73a2-4d74-ac81-3aa6c31ddcee
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: 8fa4cbebe711841d410b3ae43b78f893c06d9b63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# Azure AD B2C: Kimlik doğrulama protokolleri
Azure Active Directory B2C (Azure AD B2C) sağlayan kimlik uygulamalarınız için bir hizmet olarak iki endüstri standardı protokoller destekleyerek: Openıd Connect ve OAuth 2.0. Merhaba hizmet standartlarıyla uyumlu, ancak iki belirtilmesinden bu protokollerin küçük farklılıklar olabilir. 

Bu kılavuzdaki Hello bilgilerini doğrudan göndererek ve HTTP isteklerini işlemek yerine bir açık kaynak kitaplığı kullanarak kodunuzu yazma yararlıdır. Bu sayfayı her belirli Protokolü hello ayrıntılarını hemen önce okumanızı öneririz. Ancak, zaten Azure AD B2C ile konusunda bilginiz varsa, doğrudan çok geçebilir[hello Protokolü Başvuru Kılavuzu](#protocols).

<!-- TODO: Need link toolibraries above -->

## Merhaba temelleri
Azure AD B2C kullanan her uygulamanın B2C dizininizde hello kayıtlı toobe ihtiyacı [Azure portal](https://portal.azure.com). Merhaba uygulama kayıt işlemi toplar ve birkaç değerleri tooyour uygulama atar:

* Uygulamanızı benzersiz olarak tanımlayan bir **Uygulama Kimliği**.
* A **yeniden yönlendirme URI'si** veya **tanımlayıcısı paketini** kullanılan toodirect yanıtları geri tooyour uygulama olabilir.
* Diğer birkaç senaryoya özel değerler. Daha fazla bilgi için bilgi [nasıl tooregister uygulamanız](active-directory-b2c-app-registration.md).

Uygulamanızı kaydettikten sonra Azure Active Directory (Azure AD) ile istekleri toohello endpoint göndererek iletişim kurar:

```
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/authorize
https://login.microsoftonline.com/{tenant}/oauth2/v2.0/token
```

Neredeyse tüm OAuth ve Openıd Connect akışlarında, dört tarafların hello Exchange'de söz konusu şunlardır:

![OAuth 2.0 rolleri](./media/active-directory-b2c-reference-protocols/protocols_roles.png)

* Merhaba **yetkilendirme sunucusu** hello Azure AD uç noktadır. Güvenli bir şekilde herhangi bir şey ilgili toouser bilgi ve erişim işler. Ayrıca, akış içindeki hello taraflar arasındaki güven ilişkilerinin hello işler. Merhaba kullanıcının kimliğini doğrulamak, verme ve erişim tooresources iptal etme ve belirteç için sorumlu değildir. Bunu olarak da bilinen hello kimlik sağlayıcısı'dır.

* Merhaba **kaynak sahibi** genellikle hello son kullanıcısıdır. Merhaba verilerin sahibi hello taraf olduğu ve bu verileri veya kaynak hello güç tooallow üçüncü tarafların tooaccess vardır.

* Merhaba **OAuth istemcisi** uygulamanızın. Kendi uygulama kimliği tarafından tanımlanır Genellikle, son kullanıcıların etkileşimde hello taraf olur. Ayrıca belirteçleri hello yetkilendirme sunucusundan gelen istekleri. Merhaba kaynak sahibi hello istemci izni tooaccess kaynak hello vermeniz gerekir.

* Merhaba **kaynak sunucusu** hello kaynak veya veri bulunduğu değil. Merhaba yetkilendirme güvenilen sunucu toosecurely kimlik doğrulaması ve hello OAuth istemci yetkilendirme. Ayrıca, taşıyıcı erişim tooa kaynağa erişim belirteçleri tooensure verilebilir kullanır.

## İlkeler
Tartışmaya açık bir şekilde, Azure AD B2C ilkeleri hello hizmet hello en önemli özellikleri verilmiştir. Azure AD B2C ilkelerini tanımlayarak hello standart OAuth 2.0 ve Openıd Connect protokollerini genişletir. Bu Azure AD B2C tooperform daha basit kimlik doğrulama ve yetkilendirme fazlasını sağlar. 

İlkeleri tam olarak tüketici kimlik deneyimi kaydolma, oturum açma dahil olmak üzere,'ı açıklamakta ve profil düzenleme. İlkeleri, bir yönetici kullanıcı Arabiriminde tanımlanabilir. HTTP kimlik doğrulama isteklerinin özel sorgu parametresi kullanılarak çalıştırılabilir. 

İlkeleri olmayan OAuth 2.0 ve Openıd Connect, standart özelliklerini hello zaman toounderstand almanız gereken şekilde bunları. Daha fazla bilgi için bkz: Merhaba [Azure AD B2C İlkesi Başvuru Kılavuzu](active-directory-b2c-reference-policies.md).

## Belirteçler
OAuth 2.0 ve Openıd Connect Hello Azure AD B2C uygulaması JSON web belirteçleri (Jwt'ler) temsil edilir taşıyıcı belirteçlerini dahil olmak üzere, taşıyıcı belirteçlerini kapsamlı kullanımını sağlar. Bir basit güvenlik belirteci verir "bearer" erişim tooa hello korumalı kaynak bir taşıyıcı belirtecidir.

Merhaba taşıyıcı hello belirteci sunabilir herhangi bir tarafa ' dir. Bir taşıyıcı belirteci almak için önce azure AD önce bir taraf kimlik doğrulaması gerekir. Ancak adımları toosecure hello belirteçte iletim ve depolama katılmaz hello gerekli olursa, kullanılabilir engelledik ve istenmeyen bir şirket tarafından kullanılan.

Bazı güvenlik belirteçleri yetkisiz tarafların onları kullanmasına engel olmak yerleşik mekanizmalar sahip, ancak taşıyıcı belirteçlerini bu düzenek sahip değil. Bunlar bir Aktarım Katmanı Güvenliği (HTTPS) gibi güvenli bir kanal taşınan gerekir. 

Bir taşıyıcı belirteci dışında güvenli bir kanal iletilirse, kötü amaçlı bir taraf man-in--middle saldırı tooacquire hello belirteci kullanın ve toogain yetkisiz erişim korumalı tooa kaynak kullanın. Merhaba depolanan ya da daha sonra kullanmak üzere önbelleğe taşıyıcı belirteçlerini aynı güvenlik ilkeleri uygulayın. Her zaman uygulamanızı aktarır ve güvenli bir şekilde taşıyıcı belirteçleri depolar emin olun.

Ek taşıyıcı belirteci güvenlik konuları için bkz: [RFC 6750 bölüm 5](http://tools.ietf.org/html/rfc6750).

Azure AD B2C'de kullanılan belirteçleri hello farklı türleri hakkında daha fazla bilgi edinilebilir [Azure AD belirteç başvurusu hello](active-directory-b2c-reference-tokens.md).

## Protokoller
Hazır olduğunuzda tooreview bazı örnek istekleri, öğreticiler aşağıdaki hello biriyle başlatabilirsiniz. Her tooa belirli kimlik doğrulama senaryosu karşılık gelir. Hangi akış sizin için uygun olan saptarken yardıma gerek duyarsanız kullanıma [hello Azure AD B2C kullanarak oluşturabilir uygulama türleri](active-directory-b2c-apps.md).

* [OAuth 2.0 kullanarak mobil ve yerel uygulamalar oluşturma](active-directory-b2c-reference-oauth-code.md)
* [Openıd Connect kullanarak Web uygulamaları oluşturma](active-directory-b2c-reference-oidc.md)
* [Merhaba OAuth 2.0 örtük akışını kullanarak tek sayfalı uygulamalar oluşturma](active-directory-b2c-reference-spa.md)

