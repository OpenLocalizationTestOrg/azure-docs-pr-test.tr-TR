---
title: "aaaAzure kimlik ve erişim en iyi güvenlik uygulamaları | Microsoft Docs"
description: "Bu makalede kimlik yönetimi için en iyi yöntemler kümesi sağlar ve erişim denetimi Azure özellikleri kullanılarak."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 07d8e8a8-47e8-447c-9c06-3a88d2713bc1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/30/2017
ms.author: yurid
ms.openlocfilehash: af07dfda84758b9124641078ac8f696f725f2bf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-identity-management-and-access-control-security-best-practices"></a>En iyi güvenlik uygulamaları Azure kimlik yönetimi ve erişim denetimi
Birçok kimlik toobe hello yeni sınır katmanı hello geleneksel ağ merkezli açısından bu rolü ele güvenlik için göz önünde bulundurun. Bu güvenlik dikkat ve Yatırımlar hello birincil Özet evrimi gelen ağ çevreyi hale giderek porous ve bu çevre savunması kez öncekitoohelloPatlamasıolduklarıolabildiğinceetkiliolamazhelloolgu[KCG](http://aka.ms/byodcg) cihazlar ve bulut uygulamaları.

Bu makalede Azure kimlik yönetimi ve erişim denetimi en iyi güvenlik yöntemleri koleksiyonunu aşağıdakiler ele alınacaktır. Bu en iyi uygulamaları ile deneyimi bizim türetilmiş [Azure AD](../active-directory/active-directory-whatis.md) ve müşterilerin hello deneyimleri kendiniz ister.

En iyi her uygulama için açıklayacağız:

* Hangi hello en iyi uygulamadır
* Neden bu en iyi uygulama tooenable istiyor
* Tooenable hello en iyi yöntem başarısız olursa ne hello sonucu olabilir
* Olası alternatifler toohello en iyi uygulama
* Tooenable hello en iyi yöntem nasıl öğrenin

Bu makalenin yazıldığı hello zamanında oldukları gibi bu Azure kimlik yönetimi ve erişim en iyi yöntemler makalesi anlaşma fikir ve Azure platformu özellikleri ve özellik kümeleri dayalı güvenlik denetler. Bu makalede olacaktır ve görüşlerini ve teknolojileri değiştirmek zaman içinde bu değişiklikleri düzenli olarak tooreflect üzerinde güncelleştirildi.

Bu makalede ele alınan azure kimlik yönetimi ve erişim denetimi güvenlik en iyi uygulamalar şunlardır:

* Kimlik yönetimini merkezi hale getirin
* Çoklu oturum açma (SSO) etkinleştir
* Parola yönetimi dağıtma
* Kullanıcılar için çok faktörlü kimlik doğrulaması (MFA) zorunlu
* Kullanım rol tabanlı erişim denetimi (RBAC)
* Kaynakları Kaynak Yöneticisi'ni kullanarak oluşturulduğu denetim konumları
* Geliştiriciler tooleverage kimlik yeteneklerine SaaS uygulamaları için kılavuz
* Etkin olarak şüpheli etkinlikleri izleme

## <a name="centralize-your-identity-management"></a>Kimlik yönetimini merkezi hale getirin
Kimliğinizi güvenliğini sağlamaya yönelik bir önemli bir adımdır tooensure, BT'nin bu hesabın oluşturulduğu ile ilgili bir konumdan tek hesaplarını yönetebilir. Merhaba çoğunluğu hello işletmelerin BT kuruluşları, kendi birincil hesap şirket içi dizin olacaktır, karma bulut dağıtımları hello yükselişe ve, nasıl toointegrate şirket içi anlamak ve bulut dizinleri ve sunabileceğiniz önemlidir sırada bir deneyim toohello son kullanıcı.

tooaccomplish bu [karma kimlik](../active-directory/active-directory-hybrid-identity-design-considerations-overview.md) senaryo iki seçenek öneririz:

* Şirket içi dizininizi Azure AD Connect'i kullanarak, bulut dizini ile eşitleme
* Şirket içi kimlik bilgilerinizi kullanarak bulut dizini ile birleştirmek [Active Directory Federasyon Hizmetleri](https://msdn.microsoft.com/library/bb897402.aspx) (AD FS)

Şirket içi kimliklerini kendi bulut kimliği ile karşılaşırsınız toointegrate başarısız kuruluşlar yönetim ek yükü hesaplarını yönetme, hataları ve güvenlik ihlallerini hello arttırır çıkarılmıştır.

Azure AD eşitleme hakkında daha fazla bilgi için lütfen hello makaleyi okuyun [şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](../active-directory/active-directory-aadconnect.md).

## <a name="enable-single-sign-on-sso"></a>Çoklu oturum açma (SSO) etkinleştir
Birden çok dizin toomanage varsa, bu değil yalnızca yönetimsel bir sorun haline tooremember birden çok parola sahip son kullanıcılar için de BT. Kullanarak [SSO](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/) aynı toosign açma kimlik bilgilerini ayarlayın ve, ne olursa olsun bu kaynak şirket içinde olduğu veya hello bulutta ihtiyaç duydukları hello kaynaklarına erişim kullanım hello hello yeteneklerini kullanıcılarınızın sağlayacaktır.

SSO tooenable kullanıcılar tooaccess kullanmak kendi [SaaS uygulamaları](../active-directory/active-directory-appssoaccess-whatis.md) kuruluş hesaplarıyla Azure AD'de göre. Bu yalnızca Microsoft SaaS uygulamaları, ancak diğer uygulamalar için de geçerli olduğu gibi [Google Apps](../active-directory/active-directory-saas-google-apps-tutorial.md) ve [Salesforce](../active-directory/active-directory-saas-salesforce-tutorial.md). Uygulamanızı olarak yapılandırılmış toouse Azure AD olabilir bir [SAML tabanlı kimlik](../active-directory/fundamentals-identity.md) sağlayıcısı. Güvenlik denetimi olarak Azure AD, Azure AD kullanarak erişim verildi sürece hello uygulamasına toosign vermeden bir belirteç yayınlamayacaktır. Doğrudan veya bir grup üyesi oldukları erişim.

> [!NOTE]
> Merhaba karar toouse SSO nasıl şirket içi dizininizi bulut diziniyle tümleştirmek etkiler. SSO istiyorsanız, dizin eşitleme yalnızca sağlayacağından toouse Federasyon gerekir [aynı oturum açma deneyimi](../active-directory/active-directory-aadconnect.md).
>
>

SSO, kullanıcılar ve uygulamalar için zorlamaz kuruluşlar, kullanıcıların parolalarını yeniden kullanma veya Zayıf parolalar kullanılarak kullanıcı hello olasılığını doğrudan artıran birden çok parola burada gerekir daha gösterilen tooscenarios şunlardır.

Merhaba makale okuyarak Azure AD SSO hakkında daha fazla bilgiyi [AD FS yönetimi ve Azure AD Connect ile özelleştirme](../active-directory/active-directory-aadconnect-federation-management.md).

## <a name="deploy-password-management"></a>Parola yönetimi dağıtma
Birden çok kiracıya sahip veya tooenable kullanıcıların çok istediğiniz olduğu senaryolarda[kendi parolasını sıfırlama](../active-directory/active-directory-passwords-update-your-own-password.md), uygun güvenlik ilkeleri tooprevent kötüye kullanmak önemlidir. Azure'da hello Self Servis parola sıfırlama yeteneğinden yararlanabilir ve iş gereksinimlerinizi hello güvenlik seçenekleri toomeet özelleştirebilirsiniz.

Bu kullanıcılardan özellikle önemlidir tooobtain geribildirim ve adımları tooperform çalışırken deneyimlerini öğrenin. Bu deneyimler bağlı olarak, daha büyük bir grup hello dağıtımı sırasında oluşabilecek planı toomitigate olası sorunlar özenli. Ayrıca hello kullanmanız önerilir [parola sıfırlama kayıt Etkinlik Raporu](../active-directory/active-directory-passwords-get-insights.md) kaydediyorsunuz toomonitor hello kullanıcılar.

Tooavoid parola isteyen kuruluşların destek aramaları değiştirebilirsiniz ancak kullanıcıların tooreset etkinleştirmek kendi parolalarını daha açıktır. tooa daha yüksek çağrısı birim toohello hizmet Masası toopassword sorunları nedeniyle şunlardır. Birden çok kiracıya sahip kuruluşlarda, bu tür bir yetenek ve kullanıcıların tooperform parola hello Güvenlik İlkesi'nde oluşturulmuş olan güvenlik sınırları içinde sıfırlamayı etkinleştirmek zorunludur.

Parola hello makale okuyarak sıfırlama hakkında daha fazla bilgiyi [dağıtma parola yönetimi ve eğitim kullanıcılar toouse onu](../active-directory/active-directory-passwords-best-practices.md).

## <a name="enforce-multi-factor-authentication-mfa-for-users"></a>Kullanıcılar için çok faktörlü kimlik doğrulaması (MFA) zorunlu
Toobe gibi endüstri standartlarına uyması gereken kuruluşlar [PCI DSS sürüm 3.2](http://blog.pcisecuritystandards.org/preparing-for-pci-dss-32), çok faktörlü kimlik doğrulaması şart olduğu için kullanıcıların kimlik doğrulaması özelliğine sahip. Endüstri standartları ile uyumlu olmasını ötesinde MFA tooauthenticate kullanıcılar zorlamayı da saldırı, kuruluşların toomitigate kimlik bilgisi hırsızlığı türü gibi yardımcı olabilir [Pass--Hash (PtH)](http://aka.ms/PtHPaper).

Kullanıcılarınız için Azure MFA etkinleştirerek, güvenlik toouser oturum açmalarına ve işlemlerine ikinci bir katmanı ekliyorsunuz. Bu durumda, bir işlem bir dosya sunucusunda veya, SharePoint Online'da bulunan bir belge erişiyor. Azure MFA, güvenliği aşılmış bir kimlik bilgisi erişim tooorganization'ın veri olduğunu BT tooreduce hello olasılığı da yardımcı olur.

Örneğin: kullanıcılarınız için Azure MFA zorlamak ve toouse bir telefon araması veya kısa mesaj doğrulama yapılandırın. Merhaba kullanıcının kimlik bilgilerini aşılırsa hello saldırgan olmaz kendisine erişim toouser'ın telefon olmaz beri mümkün tooaccess herhangi bir kaynak olabilir. Ek kimlik koruma katmanları eklemeyin kuruluşlar toodata güvenliğinin aşılmasına neden olabilir kimlik bilgisi hırsızlığı saldırısına için daha açıktır.

Bir alternatif tookeep hello tüm kimlik doğrulama denetimi isteyen kuruluşların için şirket içi olan toouse [Azure çok faktörlü kimlik doğrulama sunucusu](../multi-factor-authentication/multi-factor-authentication-get-started-server.md), MFA şirket içi olarak da bilinir. Bu yöntemi kullanarak hello MFA sunucusu şirket içi korurken mümkün tooenforce çok faktörlü kimlik doğrulaması, devam edersiniz.

Azure MFA hakkında daha fazla bilgi için lütfen hello makaleyi okuyun [hello bulutta Azure multi Factor Authentication ile çalışmaya başlama](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).

## <a name="use-role-based-access-control-rbac"></a>Kullanım rol tabanlı erişim denetimi (RBAC)
Erişimi kısıtlama tabanlı hello üzerinde [tooknow gerek](https://en.wikipedia.org/wiki/Need_to_know) ve [en az ayrıcalık](https://en.wikipedia.org/wiki/Principle_of_least_privilege) güvenlik ilkeleri kesinlik temelli tooenforce güvenlik ilkeleri veri erişimi için istediğiniz kuruluşlar için. Azure rol tabanlı erişim denetimi (RBAC) kullanılan tooassign izinleri toousers, gruplar ve uygulamalar belirli bir kapsamda olabilir. bir rol ataması Hello kapsamını bir abonelik, bir kaynak grubu veya tek bir kaynak olabilir.

Yararlanabileceğiniz [RBAC yerleşik](../active-directory/role-based-access-built-in-roles.md) Azure tooassign ayrıcalıkları toousers rollerinde. Kullanmayı *depolama hesabı katkıda bulunan* toomanage depolama hesapları gereken bulut operatörleri için ve *Klasik depolama hesabı katkıda bulunan* rol toomanage Klasik depolama hesapları. Toomanage Vm'leri ve depolama hesabı gerekiyor bulut operatörleri için bunları çok eklemeyi düşünün*sanal makine Katılımcısı* rol.

Veri erişim denetimi RBAC gibi özellikler yararlanarak zorlamaz kuruluşlar gerekli tootheir kullanıcılar'den daha fazla ayrıcalık vermiş. Bu toodata güvenliğinin aşılmasına neden tarafından hello ilk yerinde olmamalıdır (örneğin, yüksek iş etkisi) veri türleri toocertain türlerini kullanıcılar erişime izin.

Merhaba makale okuyarak Azure RBAC hakkında daha fazla bilgiyi [Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md).

## <a name="control-locations-where-resources-are-created-using-resource-manager"></a>Kaynakları Kaynak Yöneticisi'ni kullanarak oluşturulduğu denetim konumları
Toomanage gerekli olan kuralları kesilmesini önleme durduğunda, kuruluşunuzun kaynakları bulut işleçleri tooperform görevleri etkinleştirmeyi çok önemlidir. Kaynakları oluşturulduğu toocontrol hello konumları isteyen kuruluşların sabit bu konumları kod.

tooachieve Bu, kuruluşların hello eylemler veya özellikle izin verilmeyen kaynaklara açıklamak tanımları olan güvenlik ilkeleri oluşturabilir. Bu ilke tanımları hello abonelik, kaynak grubu veya tek başına bir kaynak gibi istenen hello kapsamda atayın.

> [!NOTE]
> Bu olduğu değil Merhaba aynı RBAC, aslında bu kaynakları ayrıcalık toocreate sahip RBAC tooauthenticate hello kullanıcılar yararlanır.
>
>

Dengeleme [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) toocreate özel ilkeler de burada hello kuruluş istediği tooallow işlemleri yalnızca zaman hello uygun maliyet merkezi senaryoları için ilişkili; Aksi takdirde hello isteği reddeder.

Kaynakları nasıl oluşturulduğunu denetlediğiniz olmayan kuruluşlar hello hizmet ihtiyaç duydukları olandan daha fazla kaynak oluşturarak kötüye daha açıktır. toousers şunlardır. Merhaba kaynağı oluşturma işlemi sağlamlaştırma önemli adım toosecure çok kiracılı senaryo olur.

Merhaba makale okuyarak Azure Resource Manager ile ilkeleri oluşturma hakkında daha fazla bilgi edinebilirsiniz [kullanım ilkesi toomanage kaynakları ve erişimi denetleme](../azure-resource-manager/resource-manager-policy.md).

## <a name="guide-developers-tooleverage-identity-capabilities-for-saas-apps"></a>Geliştiriciler tooleverage kimlik yeteneklerine SaaS uygulamaları için kılavuz
Kullanıcı Kimliği işlevden birçok senaryoda kullanıcılar eriştiğinde [SaaS uygulamaları](https://azure.microsoft.com/marketplace/active-directory/all/) ile şirket içi tümleştirilebilir veya Bulut dizini. Öncelikle, geliştiricilerin güvenli Metodoloji toodevelop bu uygulamaları gibi kullanmanızı öneririz [Microsoft Security Development Lifecycle (SDL)](https://www.microsoft.com/sdl/default.aspx). Azure AD ile bir hizmet olarak kimlik sağlayarak geliştiriciler için endüstri standardı protokolleri gibi desteği için kimlik doğrulama basitleştirir [OAuth 2.0](http://oauth.net/2/) ve [Openıd Connect](http://openid.net/connect/), de olarak açık kaynak kitaplıkları farklı platformlar için.

Bu zorunlu bir yordamdır, kimlik doğrulama tooAzure AD outsources herhangi bir uygulama tooregister emin olun. oturum açma (SSO) işleme veya değişimi belirteçler, Azure AD hello uygulamayla toocoordinate hello iletişim gerektiğinden bu arkasında hello nedenidir. Azure AD tarafından hello belirteç Hello süresi dolduğunda hello kullanıcının oturum sona erer. Her zaman bu süre, uygulamanızın kullanması gerekiyorsa veya bu süresini azaltabilir, değerlendirin. Azalan hello ömrü kullanıcılar toosign çıkışı bir süre işlem yapılmadığında dayalı zorlayacağı bir güvenlik önlemi olarak çalışabilir.

Kimlik denetimi tooaccess uygulamaları uygulamaz ve bunların Geliştirici nasıl toosecurely tümleştirmek uygulamaları kendi kimlik yönetimi sistemiyle üzerinde Kılavuzu değil kuruluşlar olabilir saldırı, daha açıktır. toocredential hırsızlığı türü gibi [zayıf Açık Web uygulaması güvenlik proje (OWASP) ilk 10 açıklanan kimlik doğrulama ve oturum yönetimi](https://www.owasp.org/index.php/OWASP_Top_Ten_Cheat_Sheet).

SaaS uygulamaları için kimlik doğrulama senaryoları hakkında daha fazla okuyarak bilgi [Azure AD için kimlik doğrulama senaryoları](../active-directory/active-directory-authentication-scenarios.md).

## <a name="actively-monitor-for-suspicious-activities"></a>Etkin olarak şüpheli etkinlikleri izleme
Çok göre[Verizon 2016 veri ihlali rapor](http://www.verizonenterprise.com/verizon-insights-lab/dbir/2016/), kimlik bilgilerinin tehlikeye atılması olduğundan hala hello yükseklik ve hello En Karlı işletmeler birini siber suçlular olma. Bu nedenle, önemli toohave bir etkin kimlik izleme sistemi, hızlı bir şekilde kuşkulu davranış etkinliği algılayabilir ve daha fazla araştırma için bir uyarı tetiklemesi yerde değil. Azure AD'de kuruluşların kimliklerini izlemenize yardımcı olacak iki önemli özellikleri vardır: Azure AD Premium [anomali raporları](../active-directory/active-directory-view-access-usage-reports.md) ve Azure AD [kimlik koruması](../active-directory/active-directory-identityprotection.md) yeteneği.

Emin toouse hello anomali raporları tooidentify denemeleri toosign olun [izlenen olmadan](../active-directory/active-directory-reporting-sign-ins-from-unknown-sources.md), [yanılma](../active-directory/active-directory-reporting-sign-ins-after-multiple-failures.md) saldırılarına karşı birden fazla konumdan denemeleri toosign içinde belirli bir hesap oturum açın gelen [etkilenen cihazlar](../active-directory/active-directory-reporting-sign-ins-from-possibly-infected-devices.md) ve kuşkulu IP adreslerini. Bu raporlar olduğunu aklınızda bulundurun. Diğer bir deyişle, işlemler ve yordamlar, BT yöneticileri toorun için bu raporları hello günlük olarak veya isteğe bağlı olarak (genellikle bir olay yanıtlama senaryosunda) koyun olması gerekir.

Buna karşılık, Azure AD kimlik koruması etkin bir izleme sistemi ve kendi Panoda hello geçerli riskleri işaretleyecektir. Yanı sıra da e-posta yoluyla günlük özet bildirim alırsınız. Merhaba risk düzeyi tooyour iş gereksinimlerinize göre ayarlamanız önerilir. Hello risk düzeyi risk olayı (yüksek, Orta veya düşük) hello risk olayın hello önem derecesi göstergesidir. Merhaba risk düzeyi tooreduce hello risk tootheir kuruluş almalıdır hello Eylemler öncelik kimlik koruması kullanıcıların yardımcı olur.

Etkin kimlik sistemlerini izlemeyecek kuruluşların, kullanıcı kimlik bilgilerini tehlikeye sahip olmanın risk altındadır. Bu kimlik bilgileri kullanılarak kuşkulu etkinlikleri kaplayan bilginiz dışında yerleştirin, kuruluşlar, bu tür mümkün toomitigate olmayacak tehdit.
Okuyarak Azure kimlik koruması hakkında daha fazla bilgiyi [Azure Active Directory kimlik koruması](../active-directory/active-directory-identityprotection.md).
