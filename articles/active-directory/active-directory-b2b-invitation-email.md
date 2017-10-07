---
title: "hello Azure Active Directory B2B işbirliği davet e-posta aaaThe öğeleri | Microsoft Docs"
description: "Azure Active Directory B2B işbirliği davet e-posta şablonu"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: f4908014d71a63442bbdca2182f54c7a79675a82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-elements-of-hello-b2b-collaboration-invitation-email"></a>Merhaba B2B işbirliği davet e-posta Hello öğeleri

Davet e-postaların bir kritik bileşeni toobring karttaki B2B işbirliği kullanıcılar olarak Azure AD içinde ortaklarıdır. Bunları tooincrease hello alıcının güven kullanabilirsiniz. yasallığı ve sosyal kanıtını toohello e-posta ekleyebilirsiniz, toomake emin hello alıcı hissi hello seçme ile rahat **Get Started** düğmesini tooaccept hello davet. Bu güven dir bir anahtar uyuşmazlık paylaşımı tooreduce anlamına gelir. Ve ayrıca toomake hello e-posta görünüm harika!

![Azure AD B2b davet e-postası](media/active-directory-b2b-invitation-email/invitation-email.png)

## <a name="explaining-hello-email"></a>Merhaba e-posta açıklayan
En iyi nasıl toouse yeteneklerini bilmesi hello e-postanın birkaç öğeler bakalım.

### <a name="subject"></a>Konu
Merhaba hello e-postanın konu izleyen desen aşağıdaki hello: sizi davet toohello &lt;tenantname&gt; kuruluş

### <a name="from-address"></a>Adresinden
Bir LinkedIn desen adresinden hello için kullanırız.  Merhaba davet eden olduğu ve hangi şirket ve ayrıca açıklamak hello e-posta bir Microsoft e-posta adresinden gelen açık olmalıdır. Merhaba biçimi: &lt;davet eden görünen adını&gt; gelen &lt;tenantname&gt; (aracılığıyla Microsoft) <invites@microsoft.com&gt;

### <a name="reply-to"></a>Yanıtla
Merhaba yanıt-tooemail toohello davet ın eden eposta kullanılabilir olduğunda, bir e-posta geri toohello davet eden toohello e-posta gönderir yanıtlama şekilde ayarlanır.

### <a name="branding"></a>Markalama
hello şirket, markası, Kiracı gelen e-postaları kullanmak hello davet kiracınız için ayarladığınız. Bu özellik tootake avantajlarından istiyorsanız [burada](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) hello ayrıntıları nasıl tooconfigure onu. Merhaba başlık logosu hello e-postayla görüntülenir. Merhaba görüntü boyutu izleyin ve kalite yönergeleri [burada](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) en iyi sonuçlar için. Ayrıca, hello şirket adı da hello çağrısı tooaction görüntülenir.

### <a name="call-tooaction"></a>Çağrı tooaction
Merhaba çağrısı tooaction iki bölümden oluşur: hello alıcı hello posta neden aldı ve hangi hello alıcı toodo hakkında isteniyor açıklayan.
- "neden" bölüm düzeni aşağıdaki hello kullanarak çözülebilir hello: hello davet edilen tooaccess uygulamalarda verilmiş &lt;tenantname&gt; kuruluş

- Ve "ne, toodo isteniyor" bölümü hello hello varlığını tarafından gösterilen hello **Get Started** düğmesi. Merhaba alıcı davetleri hello gerek kalmadan eklendiğinde bu düğme göstermez.

### <a name="inviters-information"></a>Davet eden'ın bilgi
Merhaba davet ın eden görünen adı hello e-postayla dahil edilir. Ve Azure AD hesabınız için bir profil resmi oluşturmadıysanız, ayrıca, e-posta davet hello o resmi de içerir. Her iki hedeflenen tooincrease hello e-posta alıcının güveni olan.

Profil resminizi henüz ayarlamadıysanız hello resim yerine hello davet ın eden baş harflerini içeren bir simge gösterilir:

  ![görüntüleme hello davet eden'ın baş harfleri](media/active-directory-b2b-invitation-email/inviters-initials.png)

### <a name="body"></a>Gövde
Merhaba gövdesinde selamlama iletisine bu hello davet eden oluşturur veya hello davet API geçirilir. Güvenlik nedenleriyle HTML etiketlerini işlemek için bir metin alanı var.

### <a name="footer-section"></a>Altbilgi bölümü
Merhaba altbilgi hello Microsoft şirketinizin markasını içeren ve hello e-posta izlenmeyen bir diğer ad tarafından gönderildiyse bilmeniz hello alıcı olanak tanır. Özel durumlar:

- Merhaba davet eden bir e-posta adresi kiralama davet hello sahip değil

  ![davet eden resmi bir e-posta adresi kiralama davet hello sahip değil](media/active-directory-b2b-invitation-email/inviter-no-email.png)


- Merhaba alıcı tooredeem hello davet gerek yoktur

  ![Alıcı tooredeem davet gerektiğinde değil](media/active-directory-b2b-invitation-email/when-recipient-doesnt-redeem.png)


## <a name="next-steps"></a>Sonraki adımlar

Azure AD B2B işbirliği ile ilgili diğer makalelerimize göz atın:

* [Azure AD B2B işbirliği nedir](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Azure Active Directory yöneticileri B2B işbirliği kullanıcıların nasıl eklenir?](active-directory-b2b-admin-add-users.md)
* [Bilgi çalışanları B2B işbirliği kullanıcıların nasıl eklenir?](active-directory-b2b-iw-add-users.md)
* [B2B işbirliği davet kullanım](active-directory-b2b-redemption-experience.md)
* [Azure AD B2B işbirliği lisanslama](active-directory-b2b-licensing.md)
* [Azure Active Directory B2B işbirliği sorunlarını giderme](active-directory-b2b-troubleshooting.md)
* [Azure Active Directory B2B işbirliği sık sorulan sorular (SSS)](active-directory-b2b-faq.md)
* [Azure Active Directory B2B işbirliği API ve özelleştirme](active-directory-b2b-api.md)
* [B2B işbirliği kullanıcıları için çok faktörlü kimlik doğrulaması](active-directory-b2b-mfa-instructions.md)
* [B2B işbirliği kullanıcıları davet olmadan ekleme](active-directory-b2b-add-user-without-invite.md)
* [Azure Active Directory'de Uygulama Yönetimi için Makale Dizini](active-directory-apps-index.md)
