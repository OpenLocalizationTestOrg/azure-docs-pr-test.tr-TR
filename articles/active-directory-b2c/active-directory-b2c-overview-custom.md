---
title: "Azure Active Directory B2C: Özel ilke | Microsoft Docs"
description: "Bir konu Azure Active Directory B2C özel ilkeler hakkında"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1ff398a4-2079-4615-94f1-57de22c0aad6
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 04/04/2017
ms.author: parakhj
ms.openlocfilehash: bada9cf5f1a86f3dd047536f6fd9359c0231a384
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-custom-policies"></a>Azure Active Directory B2C: Özel ilkeler

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

## <a name="what-are-custom-policies"></a>Özel ilkeler nelerdir?

Özel ilkeler, Azure AD B2C kiracısı hello davranışını tanımlayan yapılandırma dosyalarıdır. Oysa **yerleşik ilkeleri** hello en yaygın kimlik görevleri, özel ilkeler gibi olabilir hello Azure AD B2C Portalı'nda önceden tanımlanmış görevleri yakın sınırsız sayıda tam olarak bir kimlik Geliştirici toocomplete tarafından düzenlenebilir. Özel ilkeler, sağa ve kimlik senaryonuz ise üzerinde toodetermine okuyun.

**Özel ilke düzenleme herkes için değil.** Merhaba öğrenme eğrisi yoğun, hello başlangıç zamanını uzun ve gelecekteki değişiklikler toocustom ilkeleri benzer uzmanlık toomaintain gerektirir. Yerleşik ilkeler dikkatlice ilk senaryonuz için özel ilkeler kullanmadan önce dikkate alınmalıdır.

## <a name="comparing-built-in-policies-and-custom-policies"></a>Yerleşik ilkeleri ve özel ilkeler karşılaştırma

| | Yerleşik ilkeleri | özel ilkeler |
|-|-------------------|-----------------|
|Hedef Kullanıcılar | Tüm uygulama geliştiriciler ile veya olmadan kimlik uzmanlığı | Kimlik uzmanları: sistemleri tümleştiricileri, danışmanlarımızı ve şirket içi kimlik ekipler. Openıdconnect akışları ile deneyimliyseniz ve kimlik sağlayıcısı ve talep tabanlı kimlik doğrulaması anlama |
|Yapılandırma yöntemi | Azure portalıyla kullanıcı dostu bir kullanıcı Arabirimi | Doğrudan, XML dosyalarını düzenlemek ve toohello Azure portalına karşıya yükleme |
|UI Özelleştirme | (Özel etki alanı gerektirir) HTML, CSS ve jscript desteği dahil olmak üzere, tam kullanıcı arabirimini özelleştirme<br><br>Özel dizeler ile birden çok dil desteği | Aynı |
| Öznitelik özelleştirme | Standart ve özel öznitelikler | Aynı |
|Belirteç ve oturum yönetimi | Özel belirteç ve birden çok oturum seçenekleri | Aynı |
|Kimlik sağlayıcılar| **Bugün**: önceden tanımlanmış yerel, sosyal sağlayıcısı<br><br>**Gelecekte**: OIDC, SAML, standartlara dayalı OAuth | **Bugün**: OIDC, OAUTH, standartlara dayalı SAML<br><br>**Gelecekte**: WsFed |
|Kimlik görevler (örnekler) | Kaydolma veya yerel ve birçok sosyal hesaplarıyla oturum açma<br><br>Self Servis Parola Sıfırlama<br><br>Profil düzenleme<br><br>Çok faktörlü kimlik doğrulama senaryoları<br><br>Belirteçleri ve oturumları özelleştirme<br><br>Erişim belirteci akışlar | Merhaba aynı özel kimlik sağlayıcılarını kullanarak yerleşik ilkeleri olarak görevleri tamamlamak veya özel kapsamları kullanma<br><br>Kayıt hello zaman başka bir sistem sağlama kullanıcı<br><br>Kendi e-posta hizmeti sağlayıcısını kullanarak bir Hoş Geldiniz e-posta Gönder<br><br>Bir kullanıcı deposunun B2C dışında kullanın<br><br>Kullanıcı tarafından sağlanan güvenilir bir sistem API'si aracılığıyla bilgilerle doğrula |

## <a name="policy-files"></a>İlke dosyaları

Özel bir ilke tooeach hiyerarşik zincirdeki diğer başvuran bir veya birkaç XML biçimli dosya olarak temsil edilir. Merhaba XML öğeleri tanımlayın: talep şema talep dönüşümleri, içerik tanımları, talep sağlayıcıları/teknik profilleri ve diğer öğeleri arasında Userjourney düzenleme adımlarının.

İlke dosyaları üç tür hello kullanılmasını öneririz:

- **TEMEL dosya**, çoğu hello tanımları ve tam bir örnek Azure sağlayan içerir.  Sorun giderme toohelp toothis dosya değişiklikleri en az sayıda ve uzun süreli bakım, ilkelerinizin yaptığınız öneririz
- **Uzantılar dosya** kiracınız için hello benzersiz yapılandırma değişikliklerini tutan
- **bir bağlı olan taraf (RP) dosyası** doğrudan hello uygulama veya hizmet (diğer adıyla bağlı olan taraf) tarafından çağrılan hello tek görev odaklı dosyası değil.  Daha fazla bilgi için ilke dosya tanımları Hello makalesini okuyun.  Benzersiz her görev kendi RP gerektirir ve gereksinimleri markalama bağlı olarak hello numarası "kullanım örnekleri toplam sayısı x uygulamalarının toplam" olabilir.


Azure AD B2C yerleşik ilkelerinde yukarıdaki hello portal hello arka plan toohello EXTenstions dosyasında değişiklik yaparken görür bağlı olan taraf (RP) dosya hello yalnızca hello Geliştirici gösterilen hello 3 dosya düzeni izleyin.

## <a name="core-concepts-you-should-know-when-using-custom-policies"></a>Özel ilkeler kullanırken bilmeniz gereken temel kavramlar

### <a name="azure-active-directory-b2c"></a>Azure Active Directory B2C

Azure'nın müşteri kimlik ve erişim yönetimi (CIAM) hizmeti. Merhaba hizmet içerir:

1. Bir özel amaçlı Azure Active Directory erişilebilir Microsoft Graph ve yerel hesaplar ve Federasyon hesapları için kullanıcı verilerini tutan aracılığıyla hello biçiminde bir kullanıcı dizini 
2. Erişim toohello **kimlik deneyimi Framework** hangi kullanıcıların ve varlıklar arasındaki güven düzenler ve talep aralarında toocomplete kimlik/erişim yönetim görevi geçirir 
3. Kimliği belirteçleri, yenileme belirteçleri, erişim belirteçleri (ve eşdeğer SAML onaylar) verme ve bunları tooprotect kaynaklar doğrulanıyor bir güvenlik belirteci hizmeti (STS).

Azure AD B2C, bir kimlik görev kimlik sağlayıcıları, kullanıcıların, diğer sistemler ile hello yerel kullanıcı dizisi tooachieve dizininde ile etkileşim (örn. bir kullanıcı oturum açma yeni bir kullanıcı kaydı, bir parola sıfırlama). Merhaba, çok kişili güven oluşturur ve bu adımları yürütür temel platform olarak adlandırılır kimlik deneyimi Framework ve (bir kullanıcı gezisine veya güven framework ilkesi olarak da bilinir) bir ilke hello açıkça hello aktörler, hello Eylemler hello tanımlar protokoller ve adımları toocomplete hello dizisi.

### <a name="identity-experience-framework"></a>Kimlik Deneyimi Altyapısı

Openıdconnect, OAuth, SAML, WSFed ve birkaç standart olmayan yorumlar gibi standart protokol varlıkları (geniş çapta talep sağlayıcıları) arasında güven düzenler bir tam olarak yapılandırılabilir, ilke temelli, bulut tabanlı Azure platformu biçimleri (örneğin REST API tabanlı Sistem için alışverişleri talepleri). Merhaba I2E kullanıcı dostu oluşturur, whitelabelled karşılaştığında HTML, CSS ve jscript destekler.  Bugün, hello kimlik deneyimi Framework yalnızca hello bağlamında hello Azure AD B2C hizmetinde kullanılabilir ve görevler için ilgili tooCIAM öncelik.

### <a name="built-in-policies"></a>Yerleşik ilkeleri

Azure AD B2C tooperform en yaygın olarak kullanılan hello kimlik doğrudan hello davranışını görevler (örn. kullanıcı kaydı, oturum açma, parola sıfırlama) ve ilişkilerini de önceden tanımlanmış Azure AD B2C (güvenilir taraflar etkileşimde yapılandırma dosyalarını önceden tanımlanmış Örneğin Facebook kimlik sağlayıcısı, LinkedIn, Microsoft Account, Google hesapları).  Hello gelecekteki, özelleştirme, genellikle Azure Active Directory Premium, Active Directory/ADFS, Salesforce kimlik sağlayıcısı vb. gibi hello Kurumsal bölgedeki olan kimlik sağlayıcıları için yerleşik ilkeleri sağlayabilir.


### <a name="custom-policies"></a>özel ilkeler

Azure AD B2C kiracınızda kimlik deneyimi Framework hello davranışını tanımlamak yapılandırma dosyaları. Özel bir ilke hello kimlik deneyimi bağlı olan taraf (örneğin bir uygulama) tarafından çağrıldığında Framework tarafından yürütülen (ilke dosyaları tanımları bakın) bir veya birkaç XML dosyalarını olarak erişilebilir. Özel ilkeler olabilir doğrudan görevleri yakın sınırsız sayıda kimlik Geliştirici toocomplete tarafından düzenlenebilir. Yapılandırma özel ilkeler tanımlamalısınız geliştiriciler dikkatli ayrıntı tooinclude meta veri uç noktalarını güvenilen ilişkilerde Merhaba, tam talep tanımları exchange ve gizli anahtarları, anahtarlar ve sertifikalar her kimlik sağlayıcısı tarafından gerektiği gibi yapılandırın.

## <a name="policy-file-definitions-for-identity-experience-framework-trustframeworks"></a>Kimlik deneyimi Framework Trustframeworks ilke dosyası tanımları

### <a name="policy-files"></a>İlke dosyaları

Özel bir ilke tooeach hiyerarşik zincirdeki diğer başvuran bir veya birkaç XML biçimli dosya olarak temsil edilir. Merhaba XML öğeleri tanımlayın: talep şema talep dönüşümleri, içerik tanımları, talep sağlayıcıları/teknik profilleri ve diğer öğeleri arasında Userjourney düzenleme adımlarının.  İlke dosyaları üç tür hello kullanılmasını öneririz:

- **TEMEL dosya**, çoğu hello tanımları ve tam bir örnek Azure sağlayan içerir.  Sorun giderme toohelp toothis dosya değişiklikleri en az sayıda ve uzun süreli bakım, ilkelerinizin yaptığınız öneririz
- **Uzantılar dosya** kiracınız için hello benzersiz yapılandırma değişikliklerini tutan
- **bir bağlı olan taraf (RP) dosyası** doğrudan hello uygulama veya hizmet (diğer adıyla bağlı olan taraf) tarafından çağrılan hello tek görev odaklı dosyası değil.  Daha fazla bilgi için ilke dosya tanımları Hello makalesini okuyun.  Benzersiz her görev kendi RP gerektirir ve gereksinimleri markalama bağlı olarak hello numarası "kullanım örnekleri toplam sayısı x uygulamalarının toplam" olabilir.

![İlke dosya türleri](media/active-directory-b2c-overview-custom/active-directory-b2c-overview-custom-policy-files.png)

| İlke dosya türü | Örnek dosya adı | Önerilen kullanın | Öğesinden devralınan |
|---------------------|--------------------|-----------------|---------------|
| TEMEL |TrustFrameworkBase.xml<br><br>Mytenant.onmicrosoft.com B2C 1A_BASE1.xml | Merhaba çekirdek talep şeması, talep dönüştürmeleri, talep sağlayıcıları ve Microsoft tarafından yapılandırılan kullanıcı Yolculuklar içerir<br><br>Küçük değişiklikler toothis dosya olun | None |
| Uzantı (EXT) | TrustFrameworkExtensions.xml<br><br>Mytenant.onmicrosoft.com B2C 1A_EXT.xml | Değişiklikleri toohello temel dosyanızı burada birleştirin<br><br>Değiştirilen talep sağlayıcıları<br><br>Değiştirilen kullanıcı Yolculuklar<br><br>Kendi özel şema tanımları | TEMEL dosya |
| Bağlı olan taraf (RP) | B2C_1A_sign_up_sign_in.XML| Belirteci şekli ve oturum burada ayarlarını değiştirme| Extensions(ext) dosyası |

### <a name="inheritance-model"></a>Devralma modeli

Uygulamanın hello RP ilke dosyasını aradığında, hello B2C kimlik deneyimi Framework tüm hello öğeleri temel sonra uzantılardan ekleyin ve son olarak hello RP ilke dosyası tooassemble geçerli ilke etkili hello.  Aynı yazın ve hello RP dosyadaki adı hello öğelerinin hello UZANTILARI ve UZANTILARI geçersiz kılmaları temel geçersiz kılar.

**Yerleşik ilkeleri** Azure AD B2C'de, yukarıda hello portal hello arka plan toohello EXTenstions dosyasında değişiklik yaparken görür bağlı olan taraf (RP) dosya hello yalnızca hello Geliştirici gösterilen hello 3 dosya düzeni izleyin.  Tüm Azure AD B2C'hello Azure B2C takım hello denetiminde ve sık sık güncelleştirilen bir temel ilke dosyası paylaşır.
