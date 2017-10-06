---
title: "Azure Active Directory B2C: özel ilkelerini kullanma Geliştirici Notları | Microsoft Docs"
description: "Yapılandırma ve Azure AD B2C ile özel ilkeler koruma geliştiriciler için Notlar"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: rojasja
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 05/05/2017
ms.author: joroja
ms.openlocfilehash: 979b8a264eb819ee4a208b9171a53a5ffbf062c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-azure-active-directory-b2c-custom-policy-public-preview"></a>Azure Active Directory B2C özel ilke genel Önizleme için sürüm notları
Merhaba özel İlkesi özellik kümesini artık genel Önizleme için tüm Azure Active Directory B2C altında değerlendirme için kullanılabilir (Azure AD B2C) müşteriler. Bu özellik kümesi hello en karmaşık kimlik çözümleri oluşturma Gelişmiş kimlik geliştiricileri yöneliktir.  

Günümüzde, bu özellik kümesi geliştiriciler tooconfigure hello kimlik deneyimi Framework XML dosyasını düzenleyerek aracılığıyla doğrudan gerektirir. Bu yapılandırma, güçlü ve karmaşık yöntemidir. Merhaba kullanan kimlik geliştiriciler Gelişmiş kimlik deneyimi Framework tooinvest kılavuzlarına tamamladıktan ve başvuru belgeleri okuma biraz zaman planlamanız gerekir. 

## <a name="features-included-in-this-public-preview"></a>Bu genel önizlemede bulunan özellikler
Hello genel Önizleme'de sunulan hello yeni özelliklerle, geliştiriciler hello aşağıdaki görevleri gerçekleştirebilirsiniz:<br>

* Özel ilkeler kullanarak yazar ve karşıya yükleme özel kimlik doğrulama kullanıcı Yolculuklar. 
   * Kullanıcı Yolculuklar alışverişleri adım adım talep sağlayıcıları arasında açıklanmaktadır. 
   * Koşullu kullanıcı Yolculuklar dallanma tanımlayın. 
* Özel kimlik doğrulama kullanıcı Yolculuklar REST API etkin Hizmetleri'nde tümleştirin.  
* Openıdconnect standart hello ile uyumlu olan kimlik sağlayıcıları ile Federasyon ekleyin. <br>
* Federasyon toohello SAML 2.0 protokolü uyması kimlik sağlayıcıları ile ekleyin. 

## <a name="terms-of-hello-public-preview"></a>Merhaba genel Önizleme koşulları

* Toouse hello yeni özellikler yalnızca değerlendirme amacıyla öneririz.<br>
* Yeni özellikler, bir üretim ortamında kullanılması amaçlanmamıştır.<br>
* Hizmet düzeyi sözleşmelerine (SLA) toohello yeni özellikleri geçerli değildir. <br>
* Destek istekleri normal destek kanallarını Dosyalanan. <br>
* Genel kullanılabilirlik taahhüt edilen tarih yoktur.<br>
* Bizim tedbirli ve herhangi bir nedenle, Microsoft bayrak ve reddetme veya senaryoları ve hello Azure AD B2C ürün kurucu tooserve müşteri kimlik ve erişim yönetimi (CIAM) platformu olarak hello kapsamını aşan kullanıcı Yolculuklar kısıtlama.

## <a name="responsibilities-of-custom-policy-feature-set-developers"></a>Özel ilke özellik kümesi geliştiricilerin sorumlulukları
El ile ilke yapılandırması Azure AD B2C platformu temel düşük düzeyli erişim toohello verir ve benzersiz, tam olarak özelleştirilebilir güven framework hello oluşturulmasında sonuçlanır. Olası alternatifler özel kimlik sağlayıcıları, güven ilişkileri dış hizmetler ve adım adım iş akışları ile tümleştirmeleri bunları kullanan geliştiriciler Gelişmiş hello üzerinde büyük taleplerini yerleştirin.

toofully avantajı hello genel Önizlemesi'nden, geliştiricilerin hello özel İlkesi özellik kümesini kullanma yönergeleri izleyerek toohello uygun olan öneririz:
* Merhaba kimlik deneyimi altyapısı Hello yapılandırma dilini ve anahtar/parolalar yönetimi konusunda bilgi sahibi olur.
* Senaryolar ve özel tümleştirmeler sahipliğini alın.
* Sistemli senaryo test gerçekleştirin.
* Yazılım geliştirme ve en iyi yöntemlerle en az bir geliştirme ve test ortamı ve bir üretim ortamında hazırlama izleyin.
* Merhaba kimlik sağlayıcıları ve Hizmetleri ile tümleştirme yeni gelişmeler hakkında bilgi sahibi olma. Örneğin, gizli ve zamanlanmış ve zamanlanmamış değişiklikleri toohello hizmetinin değişiklikleri takip edin.
* Etkin izleme işlevini ayarlama ve üretim ortamlarında hello yeteneğini izleyin.
* İletişim e-posta adresleri güncel tutun ve esnek toohello Microsoft live site takım e-postaları kalır.
* Tavsiye edilir toodo giderek hello durumlarda Microsoft live site ekibi zamanında eyleme. 


>[!NOTE]
>Bu özellikler sonunda daha erişilebilir tooall geliştiriciler yaparak Azure AD yerleşik İlkeleri'nde bulunabilir.

## <a name="next-steps"></a>Sonraki adımlar
[Özel ilkelerini kullanmaya başlama](active-directory-b2c-get-started-custom.md).
