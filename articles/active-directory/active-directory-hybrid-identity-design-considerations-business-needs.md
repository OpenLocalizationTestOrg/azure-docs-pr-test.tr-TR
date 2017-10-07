---
title: "aaaAzure Active Directory karma kimlik tasarımı hakkında önemli noktalar - belirlemek kimlik gereksinimleri | Microsoft Docs"
description: "Merhaba karma kimlik tasarımı için toodefine hello gereksinimleri götürür hello şirketin işletme gereksinimlerini tanımlama."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: de690978-84ef-41ad-9dfe-785722d343a1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: b2f1cad923b0f08ededa0d8f9a4ea8e799956e54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-identity-requirements-for-your-hybrid-identity-solution"></a>Karma kimlik çözümünü kimlik gereklilikleri
karma kimlik çözümünü tasarlamanın ilk adımı hello toodetermine hello gereksinimleri Bu çözüm yararlanarak hello iş kuruluş için ' dir.  Karma kimlik (diğer tüm bulut çözümleri kimlik doğrulaması sağlayarak destekler) destekleyen bir rol olarak başlar ve kullanıcılar için yeni iş yüklerine kilidini tooprovide yeni ve ilginç özellikleri gider.  Bu iş yükleri veya tooadopt kullanıcılarınız için istediğiniz hizmetleri hello karma kimlik tasarımı için hello gereksinimleri benimsendiği belirler.  Bu hizmet ve iş yükleri hem şirket içi tooleverage karma kimlik gerekir ve hello bulutta.  

Toogo hello iş toounderstand bu önemli yönlerinin üzerinde ne ihtiyacınız bu gereksinim artık ve hangi hello şirket hello gelecekteki planları olur. Karma kimlik tasarımı için hello uzun vadeli stratejisi hello görünürlüğünü yoksa, işleriniz büyür ve değişirken hello iş gereksinimleri değişirken çözümünüzün ölçeklenebilir olmayacağını kalabilirsiniz.   T kullanıcılar için kilidi bir karma kimlik mimarisi ve hello iş yüklerini örneği kendisinin diyagram gösterilmektedir. Bu yalnızca kilidi ve düz karma kimlik stratejisi ile sunulan tüm hello yeni olanaklar örneğidir. 

Merhaba karma kimlik mimarisi parçası olan bazı bileşenleri![](./media/hybrid-id-design-considerations/hybrid-identity-architechture.png)

## <a name="determine-business-needs"></a>İş gereksinimlerini belirleme
Bu şirketler hello bir parçası olsa bile her şirketin farklı gereksinimleri vardır aynı sektörde hello gerçek iş gereksinimleri farklılık gösterir. Hello endüstri gelen en iyi yöntemlerinden yine yararlanabilirsiniz, ancak sonuç olarak toodefine hello gereksinimleri hello karma kimlik tasarımı için götürür hello şirketin iş ihtiyaçları olacaktır. 

İşinizi tooanswer hello aşağıdaki soruları tooidentify emin olmak gerekir:

* Şirketiniz toocut BT operasyon maliyet istiyorsunuz?
* Şirketiniz toosecure bulut varlıklar (SaaS uygulamaları, altyapı) istiyorsunuz?
* Olan toomodernize arayan, şirketinizin BT?
  * Kullanıcılarınızın daha fazla mobil ve zorlu BT toocreate özel durumları, DMZ tooallow farklı trafik tooaccess farklı kaynak türünü içine misiniz?
  * Şirketinizin yayımlanan toobe gereken eski uygulamalar var mı toothese modern kullanıcı ancak değil kolay toorewrite?
  * Şirketiniz tüm bu görevlerin tooaccomplish gerekir ve hello denetimi altına alın aynı anda?
* Şirketiniz toosecure kullanıcıların kimliklerini arayan ve Microsoft'un Azure güvenlik uzmanlık şirket içi hello uzmanlığını yararlanan yeni araçları getirerek riskini azaltmak?
* Merhaba RID tooget çalışırken, şirketinizin "dış" hesapları şirket içi dreaded ve şirket içi ortamınız içinde etkinliği olmayan bir tehdit artık nerede toohello bulut taşıma nedir?

## <a name="analyze-on-premises-identity-infrastructure"></a>Şirket içi kimlik altyapınızı Çözümle
Şirket iş gereksinimlerinizi bir fikir sahip olduğunuza göre şirket içi kimlik altyapınızı tooevaluate gerekir. Bu değerlendirme hello teknik gereksinimleri toointegrate, geçerli kimlik çözümü toohello bulut kimlik yönetimi sistemi tanımlaması için önemlidir. Aşağıdaki sorular emin tooanswer hello olun:

* Hangi kimlik doğrulama ve yetkilendirme çözümü şirketiniz tarafından sağlanan şirket içi kullanma? 
* Şirket içi eşitleme hizmetlerin şu anda var mı?
* Şirketiniz tüm üçüncü taraf kimlik sağlayıcıları (IDP) kullanıyor mu?

Ayrıca toobe şirketinizin olabilir hello bulut Hizmetleri farkında gerekir. Bir değerlendirme toounderstand hello geçerli ile tümleştirme SaaS gerçekleştirmeden, Iaas veya PaaS modelleri, ortamınızdaki çok önemlidir. Bu değerlendirme sırasında sorular aşağıdaki emin tooanswer hello olun:

* Şirketiniz herhangi bir bulut hizmeti sağlayıcısı ile tümleştirme var mı?
* Yanıt Evet ise, hangi hizmetlerin kullanılıyor?
* Bu tümleştirme şu anda üretimde olan yoksa bir pilot mı?

> [!NOTE]
> Tüm uygulamalarınızın doğru bir eşleme varsa ve bulut Hizmetleri yok, hello Cloud App Discovery aracını kullanabilirsiniz. Bu araç, BT departmanınızın tüm kuruluşunuzun iş ve tüketici bulut uygulamalarını görünürlük sağlayabilirsiniz. Herhangi bir zamanda toodiscover gölge BT daha ayrıntıları kullanım modelleri ve bulut uygulamalarınız erişen tüm kullanıcılar dahil olmak üzere kuruluşunuzdaki kolaylaştırır. başlatılan tooget bkz [Cloud app discovery](active-directory-cloudappdiscovery-whatis.md).
> 
> 

## <a name="evaluate-identity-integration-requirements"></a>Kimlik Tümleştirme gereksinimlerini değerlendirin
Ardından, tooevaluate hello Kimlik Tümleştirme gereksinimlerini gerekir. Bu değerlendirme nasıl kullanıcılar kimlik doğrulaması, hello kuruluşunuzun varlığı hello bulutta nasıl görüneceğine, hello kuruluşunuzun yetkilendirme nasıl izin verecek ve devam eden toobe hangi hello kullanıcı deneyimi olan için önemli toodefine hello teknik gereksinimleri ' dir. Aşağıdaki sorular emin tooanswer hello olun:

* Kuruluşunuz, Federasyon, standart kimlik doğrulama veya her ikisini kullanacaksınız?
* Federasyon bir gereksinimdir?  Merhaba aşağıdaki nedeniyle:
  * Kerberos tabanlı SSO
  * Şirketiniz SAML veya benzer Federasyon yeteneklerini kullanır (ya da şirket içi veya 3 taraf yerleşik) bir şirket içi uygulamalara sahiptir.
  * Akıllı kartlar ile MFA. RSA Securıd, vb.
  * Merhaba soruları aşağıdaki istemci erişim kuralları:
    1. Tüm dış erişim tooOffice hello istemcisinin hello IP adresine göre 365 engelleyebilir miyim?
    2. Tüm dış erişim tooOffice 365, Exchange ActiveSync dışında engelleyebilir miyim?
    3. (OWA, SPO) tarayıcı tabanlı uygulamalar dışındaki tüm dış erişim tooOffice, 365 engelleyebilir miyim
    4. Belirtilen AD gruplarının üyeleri için tüm dış erişim tooOffice 365 engelleyebilir miyim
* Güvenlik ve denetim konuları
* Federe kimlik doğrulaması yatırım zaten var
* Hangi ad hello bulut bizim etki alanı için kuruluşunuzun kullanacak mısınız?
* Merhaba kuruluş özel bir etki alanı var mı?
  1. Bu etki alanı, ortak ve DNS aracılığıyla kolayca doğrulanabilen nedir?
  2. Değilse, AD içinde kullanılan tooregister bir alternatif UPN olan genel etki alanı var mı?
* Merhaba kullanıcı tanımlayıcıları için bulut gösterimi tutarlı misiniz? 
* Merhaba kuruluş, bulut Hizmetleri ile tümleştirme gerektiren uygulamalar var mı?
* Hello kuruluş birden çok etki alanına sahip ve tüm standart ya da federe kimlik doğrulamasını kullanır?

## <a name="evaluate-applications-that-run-in-your-environment"></a>Ortamınızda çalışan uygulamaları değerlendir
Şirket içi bir fikir sahip ve altyapı bulut göre bu ortamlarda çalışan tooevaluate hello uygulamaları gerekir. Bu değerlendirme toodefine hello teknik gereksinimleri toointegrate bu uygulamaları toohello bulut kimlik yönetimi sistemi önemlidir. Aşağıdaki sorular emin tooanswer hello olun:

* Burada bizim uygulamaları Canlı?
* Kullanıcıların şirket içi uygulamalara erişecek?  Merhaba bulutta? Veya her ikisini birden mi?
* Planları tootake hello varolan uygulama iş yükleri vardır ve toohello bulut taşıma?
* Hem şirket içinde bulunan veya hello bulut toodevelop yeni uygulamalar bulut kimlik doğrulamasını kullanır planları var mı?

## <a name="evaluate-user-requirements"></a>Kullanıcı gereksinimlerini değerlendirin
Ayrıca tooevaluate hello kullanıcı gereksinimleri vardır. Bu değerlendirme devreye alma ve toohello bulut geçiş olarak kullanıcılara yardım için gereken önemli toodefine hello adımları ' dir. Aşağıdaki sorular emin tooanswer hello olun:

* Kullanıcılar uygulamaları şirket içi erişecek?
* Kullanıcıların hello bulut uygulamalarında erişecek?
* Kullanıcıların nasıl yerine genellikle oturum açma tootheir şirket içi ortamına?
* Kullanıcıların oturum açma toohello bulut ne?

> [!NOTE]
> Her yanıtı tootake Not emin olun ve hello yanıtın hello yanıt arkasındaki mantığı anladığınızdan emin olun. [Olay yanıtlama gereksinimlerini belirlemek](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) hello seçenekleri ve her seçeneğin olumlu/eksilerini üzerinden geçer.  Seçeneği, iş gereksinimlerinize en uygun belirleyeceksiniz bu soruları yanıtladığınızda gerekir.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
[Dizin eşitleme gereksinimlerini belirleyin](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)

## <a name="see-also"></a>Ayrıca bkz.
[Tasarım konularına genel bakış](active-directory-hybrid-identity-design-considerations-overview.md)

