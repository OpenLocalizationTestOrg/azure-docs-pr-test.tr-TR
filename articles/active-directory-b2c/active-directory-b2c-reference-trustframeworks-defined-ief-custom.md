---
title: "Azure Active Directory B2C: Başvuru - güven çerçeveleri | Microsoft Docs"
description: "Azure Active Directory B2C özel ilkeler ve hello kimlik deneyimi Framework hakkındaki bir konu"
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
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: d9634da72cb136ac165dd32e735622b5d0e22ec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="define-trust-frameworks-with-azure-ad-b2c-identity-experience-framework"></a>Azure AD B2C kimlik deneyimi Framework güven çerçeveleri tanımlayın

Azure Active Directory B2C hello kimlik deneyimi Framework kullanın (Azure AD B2C) özel ilkeler, merkezi bir hizmeti, kuruluşunuz sağlar. Bu hizmet ilgi büyük bir topluluk içinde Kimlik Federasyonu hello karmaşıklığını azaltır. Merhaba karmaşıklık azaltılmış tooa tek güven ilişkisi ve meta veri değişimi ' dir.

Merhaba kimlik deneyimi Framework tooenable kullanan azure AD B2C özel ilkeler aşağıdaki, tooanswer hello sorular:

- Merhaba yasal, güvenlik, gizlilik ve bağlı gereken veri koruma ilkeleri nelerdir?
- Kimin hello kişiler ve onaylanmış bir katılımcısı olma hello işlemler nelerdir?
- Kimlik bilgisi sağlayıcıları (olarak da bilinen "Talep Sağlayıcıları") accredited hello kim ve ne sunar?
- Hello kim bağlı olan taraflar accredited (ve isteğe bağlı olarak, ne duyarlar)?
- "Hello kablo" teknik hello nelerdir katılımcıları birlikte çalışabilirlik gereksinimlerini?
- Dijital kimlik bilgileri değişimi için zorlanan gerekir hello işletimsel "çalışma zamanı" kuralları nelerdir?

tooanswer tüm bu sorular, hello kimlik deneyimi Framework kullanımı hello güven Framework (TF) kullanan Azure AD B2C özel ilkeleri oluşturun. Şimdi ne sağlar ve bu yapıyı göz önünde bulundurun.

## <a name="understand-hello-trust-framework-and-federation-management-foundation"></a>Merhaba güven Framework ve Federasyon management foundation anlama

Merhaba güven Framework bir topluluk ilgi toowhich katılımcıları uymalıdır hello kimlik, güvenlik, gizlilik ve veri koruma ilkelerinin yazılmış bir özelliğidir.

Federe kimlik, son kullanıcı kimliğini güvence Internet ölçeğinde ulaşmak için bir temel sağlar. Kimlik Yönetimi toothird taraflar için temsilci seçme ile birden çok bağlı olan taraflar bir son kullanıcı için tek bir dijital kimliği yeniden kullanılabilir.  

Kimlik güvence kimlik sağlayıcısı (IdPs) ve öznitelik sağlayıcıları (AtPs) toospecific güvenlik, gizlilik ve işlem ilkeleri ve uygulamaları uyması gerekir.  Doğrudan incelemeleri gerçekleştirilemiyor, bağlı olan taraflar hello IdPs ve toowork ile tercih ettikleri AtPs güven ilişkileri (RPs) geliştirmelisiniz.  

Tüketicileri ve sağlayıcıları dijital kimlik bilgilerinin Hello sayısı arttıkça, bu güven ilişkileri pairwise yönetimi zor toocontinue veya ikili exchange ağ bağlantısı için gerekli olan hello teknik meta verilerin bile hello .  Federasyon hub'ları bu sorunları çözmek sırasında yalnızca sınırlı başarı elde.

### <a name="what-a-trust-framework-specification-defines"></a>Bir güven Framework belirtimi tanımlar
TFs hello linchpins ilgi her topluluk tarafından belirli bir TF belirtimi burada tabidir hello açık kimlik Exchange (OIX) güven Framework modelinin ' dir. Bu tür bir TF belirtimi tanımlar:

- **Merhaba toplulukla ilgi hello tanımı için güvenlik ve gizlilik ölçümleri hello:**
    - Katılımcıları tarafından sunulan/gerekli olan hello güvence düzeyleri (LOA); Örneğin, dijital kimlik bilgileri hello özgünlüğünü güvenirlik derecelendirmesi sıralı bir dizi.
    - Katılımcıları tarafından sunulan/gerekli olan hello koruma düzeyleri (LOP); Örneğin, ilgi hello topluluk katılımcıları tarafından işlenen dijital kimlik bilgilerinin hello koruma güvenirlik derecelendirmesi sıralı bir dizi.

- **Merhaba sunulan gerekli / hello dijital kimlik bilgilerinin açıklaması katılımcılar tarafından**.

- **Merhaba teknik ilkeleri üretim ve dijital kimlik bilgilerinin kullanım için ve bu nedenle LOA ve LOP ölçme. Bu ilkeler genellikle yazılmış ilkeleri kategorilerini aşağıdaki hello şunlardır:**
    - İlkeleri, örneğin sağlama kimlik: *vetted kişinin kimlik bilgilerini'ne kadar güçlü olan?*
    - Güvenlik ilkeleri, örneğin: *ne kadar güçlü bilgi bütünlüğü ve gizliliği korumalı misiniz?*
    - Gizlilik ilkeleri, örneğin: *hangi denetim bir kullanıcı kişisel olarak tanımlanabilir bilgileri (PII) sahip*?
    - Survivability ilkeleri, örneğin: *bir sağlayıcı işlemleri başlamasıyla nasıl mu devamlılığı ve koruma PII işlevinin?*

- **Merhaba üretim ve dijital kimlik bilgilerinin kullanım için teknik profilleri. Bu profiller içerir:**
    - Kapsam arabirimler, dijital kimlik bilgileri belirtilen LOA kullanılabilir.
    - Teknik gereksinimleri üzerindeki hat birlikte çalışabilirlik.

- **Merhaba açıklamalarını hello topluluk katılımcıları gerçekleştirmek ve bu rolleri gereken toofulfill olan nitelikleri hello çeşitli rolleri hello.**

Böylece kimlik bilgileri hello topluluk ilgi hello katılımcılar nasıl değiştirilir TF belirtimi yönetir: bağlı olan taraflar, kimlik ve öznitelik sağlayıcıları ve öznitelik doğrulayıcıları.

Hello idare hello onaylama düzenler ilgi hello topluluk ve hello topluluk içinde dijital kimlik bilgilerinin tüketim için bir başvuru olarak hizmet bir veya birden çok belge TF belirtimidir. İlgi bir topluluk üyeleri arasındaki çevrimiçi işlemleri için kullanılan dijital kimlikleri hello tooestablish güvende yordamları tasarlanmış ve ilkeleri belgelenmiş bir dizi kitaplıktır.  

Diğer bir deyişle, TF belirtimi bir topluluk için uygun Federal Kimlik ekosistemi oluşturmak için hello kuralları tanımlar.

Şu anda bu tür bir yaklaşım hello avantajı üzerinde yaygın anlaşmayı yoktur. Yoktur Şüphesiz, framework belirtimleri dijital kimliği ekosistemlerini ilgi birden çok topluluğu arasında kullanılabilme, yani doğrulanabilen güvenlik güvencesi ve gizlilik özelliklere sahip hello geliştirmeyi kolaylaştırmak güven.

Bu nedenle, hello kimlik deneyimi Framework kullanan Azure AD B2C özel ilkelerini kullanan hello belirtimi kendi veri temsili hello temeli olarak TF toofacilitate birlikte çalışabilirlik için.  

Merhaba kimlik deneyimi Framework yararlanan azure AD B2C özel ilkeler TF belirtimi İnsan ve makine tarafından okunabilir veri bileşimi olarak temsil eder. Bu modelin (genellikle doğru idare daha odaklı bölümleri) bazı bölümleri toopublished güvenlik ve Gizlilik İlkesi belgeleri hello birlikte başvuran olarak temsil edilir (varsa) ilgili yordamlar. Diğer bölümler işletimsel Otomasyon kolaylaştıran ayrıntı hello yapılandırma meta verilerini ve çalışma zamanı kuralları açıklamaktadır.

## <a name="understand-trust-framework-policies"></a>Güven Framework ilkelerini anlama

Uygulama bakımından kimlik davranışları ve deneyimleri üzerinde tam denetim ilkeleri kümesini hello TF belirtimi oluşur.  Merhaba kimlik deneyimi Framework yararlanan azure AD B2C özel ilkeler, tooauthor etkinleştirin ve kendi TF tanımlayın ve yapılandırma gibi bildirim temelli ilkeleri aracılığıyla oluşturun:

- Merhaba belge başvurusu veya hello Federal Kimlik toohello TF ilişkili hello topluluk ekosistemi tanımlamak başvuruları. Bağlantılar toohello TF belgelerine oldukları. (önceden tanımlanmış) işletimsel "çalışma zamanı" kurallarını veya otomatikleştirmek ve/veya hello exchange ve hello talep kullanımını kontrol hello kullanıcı Yolculuklar hello. Bu kullanıcı Yolculuklar bir LOA (ve bir LOP) ile ilişkilendirilir. Bir ilke, bu nedenle LOAs (ve LOPs) değişen ile kullanıcı Yolculuklar sahip olabilir.

- Merhaba kimlik ve öznitelik sağlayıcılar veya hello sağlayıcıları talepleri, ilgi ve hello teknik profillerinin hello topluluğuna destekledikleri toothem ilişkili hello (bant-) LOA/LOP eşitlik belgesi yanı sıra.

- öznitelik doğrulayıcılar veya talep sağlayıcıları ile Merhaba tümleştirme.

- Merhaba bağlı olan taraflar hello topluluğundaki (tarafından çıkarım).

- katılımcılar arasındaki ağ iletişim kurmak için hello meta veriler. Merhaba teknik profilleri yanı sıra bu meta veriler işlem tooplumb sırasında kullanılan "üzerinde hello kablo" Merhaba bağlı olan taraf ve diğer topluluk katılımcılar arasındaki birlikte çalışabilirlik.

- Merhaba Protokolü dönüştürme varsa (örneğin, SAML, OAuth2, WS-Federation ve Openıd Connect).

- Merhaba kimlik doğrulama gereksinimleri.

- Merhaba çok faktörlü orchestration varsa.

- Tüm kullanılabilir hello talepler ve ilgi topluluğunun eşlemeleri tooparticipants için paylaşılan bir şema.

- Tüm hello hello olası veri minimization bu içerik, toosustain hello exchange ve hello talep kullanımını birlikte dönüşümleri talepleri.

- Merhaba bağlama ve şifreleme.

- Merhaba depolama talepleri.

### <a name="understand-claims"></a>Talep anlama

> [!NOTE]
> Biz topluca "talep" olarak değiştirilen kimlik bilgilerinin tooall hello olası türlerini başvurun: kişisel olarak tanımlayan talep bir son kullanıcının kimlik doğrulama kimlik bilgileri, kimliği vetting, iletişim aygıtı, fiziksel konumu hakkında öznitelikler ve benzeri.  
>
> Çevrimiçi işlemlerde bu veri yapıları doğrudan bağlı olan taraf hello tarafından doğrulanabilen bulguları olduğundan hello terimi "talep"--yerine "öznitelikleri"--kullanın. Bunun yerine onaylar veya yeterli güvenirlik toogrant hello son kullanıcının istenen işlem bağlı olan taraf için hangi hello geliştirmelidir bulguları hakkında talepleri oldukları.  
>
> Ayrıca Azure AD B2C'hello kimlik deneyimi Framework kullanan özel ilkeler toosimplify hello exchange dijital kimlik bilgilerinin her türlü bağımsız olarak, tutarlı bir şekilde tasarlanmış nedeniyle "talep" olup olmadığını temel hello hello terim kullanırız protokol, kullanıcı kimlik doğrulaması veya öznitelik alımı için tanımlanır.  Benzer şekilde, "Talep Sağlayıcıları" toocollectively, tooidentity sağlayıcıları, öznitelik sağlayıcıları ve öznitelik doğrulayıcılar belirli işlevleri arasında toodistinguish istemiyorsanız başvurmak hello terim kullanın.   

Bu nedenle bunlar kimlik bilgilerini bir bağlı olan taraf, kimlik ve öznitelik sağlayıcıları ve öznitelik doğrulayıcılar arasında nasıl alınıp yönetir. Hangi kimlik denetlemek ve özniteliği sağlayıcıları için bir bağlı olan tarafın kimlik doğrulaması gerekir. Bunlar bir etki alanına özgü dil (DSL) başka bir deyişle, belirli uygulama etki alanı devralmayla, için özelleştirilmiş bir bilgisayar dil düşünülmesi gereken *varsa* deyimleri, çok biçimlilik.

Bu ilkeler hello makine tarafından okunabilir TF oluşturmak hello kimlik deneyimi Framework yararlanarak Azure AD B2C özel ilkelerinde hello bölümünü oluşturur. Talep sağlayıcısı meta verileri ve teknik profilleri, talep şema tanımları, talep dönüştürme işlevleri ve doldurulur kullanıcı Yolculuklar toofacilitate işletimsel düzenleme dahil olmak üzere tüm hello işletimsel ayrıntıları içerir ve Otomasyon.  

Toobe varsayılır *yaşam belgeleri* içeriklerini hello aktif katılımcılara hello ilkelerinde bildirilen ilgili zamanla değiştirecek şansı olduğundan. Merhaba hüküm ve koşullar Katılımcısı olması için değişebilir hello olası yoktur.  

Federasyon Kurulum ve Bakım çok Basitleştirilmiş farklı talep sağlayıcıları/doğrulayıcılar katılma veya (Merhaba topluluk tarafından temsil edilen) ayrılma gibi devam eden güven ve bağlantı yeniden yapılandırmaların bağlı olan tarafların koruma hello ilkeleri kümesi.

Birlikte çalışabilirlik başka bir önemli bir iştir. Ek talep sağlayıcıları/doğrulayıcılar tümleşik, bağlı olan taraflar olası toosupport olduğundan tüm gerekli protokolleri hello. Azure AD B2C özel ilkeler, endüstri standardı protokolleri destekleyerek bu sorunu çözmek ve belirli bir kullanıcı Yolculuklar uygulayarak bağlı olan taraflar ve öznitelik sağlayıcıları desteklemediği zaman tootranspose istekleri aynı protokol hello.  

Kullanıcı Yolculuklar dahil Protokolü profilleri ve kullanılan tooplumb olan meta veri "üzerinde hello kablo" Merhaba bağlı olan taraf ve diğer katılımcılar arasındaki birlikte çalışabilirlik. Merhaba TF belirtiminin bir parçası olarak yayımlanan ilkeleriyle uyumluluğunu zorlama uygulanan tooidentity bilgileri exchange istek/yanıt iletilerini işletimsel çalışma zamanı kurallar vardır. Kullanıcı Yolculuklar Hello fikri anahtar toohello hello müşteri deneyimini özelleştirmesini değildir. Ayrıca, hello sistem hello protokol düzeyinde nasıl çalıştığı ışık sheds.

Bu temelinde bağlı olan taraf uygulamaları ve portalları bağlamları bağlı olarak Dengeleme kimlik deneyimi belirli bir ilke hello adını geçirerek Framework hello ve tam olarak hello davranışı ve bilgi alın Azure AD B2C özel ilkeler çağırabileceği herhangi bir muss fuss veya riski olmadan istedikleri exchange.
