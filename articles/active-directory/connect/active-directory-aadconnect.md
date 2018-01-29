---
title: "Azure Active Directory ile Active Directory’yi bağlayın. | Microsoft Docs"
description: "Azure AD Connect, şirket içi dizinlerinizi Azure Active Directory ile tümleştirir. Bu sayede Azure AD ile tümleşik Office 365, Azure ve SaaS uygulamaları için ortak bir kimlik oluşturabilirsiniz."
keywords: "Azure AD Connect’e giriş, Azure AD Connect’e genel bakış, Azure AD Connect nedir, active directory yükleme"
services: active-directory
documentationcenter: 
author: billmath
manager: mtillman
editor: 
ms.assetid: 59bd209e-30d7-4a89-ae7a-e415969825ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/02/2017
ms.author: billmath
ms.openlocfilehash: 83654a406019c4ac3837a3e961a6de640c98f31c
ms.sourcegitcommit: 3f33787645e890ff3b73c4b3a28d90d5f814e46c
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/03/2018
---
# <a name="integrate-your-on-premises-directories-with-azure-active-directory"></a>Şirket içi dizinlerinizi Azure Active Directory ile tümleştirme
Azure AD Connect, şirket içi dizinlerinizi Azure Active Directory ile tümleştirir. Bu sayede kullanıcılarınıza Azure AD ile tümleşik Office 365, Azure ve SaaS uygulamaları için ortak bir kimlik sağlayabilirsiniz. Planlama, dağıtım ve işlem adımları sırasında sizi yönlendirmesi için bu konu başlığından faydalanabilirsiniz. Bu alanla ilgili konu başlıklarına yönelik bağlantılar mevcuttur.

> [!IMPORTANT]
> [Azure AD Connect, şirket içi dizininizi Azure AD'ye ve Office 365'e bağlamanın en iyi yoludur. Microsoft Azure Active Directory Eşitleme (DirSync) ve Azure AD Eşitleme araçları artık kullanım dışı olduğundan ve 13 Nisan 2017’den itibaren desteklenmediğinden şimdi Azure AD Connect’e yükseltmenin tam zamanı.](active-directory-aadconnect-dirsync-deprecated.md)
> 
> 

![Azure AD Connect nedir?](media/active-directory-aadconnect/arch.png)

## <a name="why-use-azure-ad-connect"></a>Azure AD Connect neden kullanılır?
Şirket içi dizinlerinizin Azure AD ile tümleştirilmesi, kullanıcılarınızın hem bulut kaynaklarına hem de şirket içi kaynaklara erişmesi için ortak bir kimlik oluşturarak daha üretken olmalarını sağlar. Kullanıcılar ve kuruluşlar aşağıdaki avantajlardan faydalanabilir:

* Kullanıcılar, Office 365 gibi bulut hizmetlerine ve şirket içi uygulamalara erişmek için tek bir kimlik kullanabilir.
* Eşitleme ve oturum açmaya yönelik kolay bir dağıtım deneyimi sağlamak için tek araç.
* Senaryolarınız için en yeni işlevleri sağlar. Azure AD Connect; DirSync ve Azure AD Eşitleme gibi kimlik tümleştirme araçlarının eski sürümlerinin yerine kullanılmaktadır. Daha fazla bilgi için bkz. [Karma Kimlik dizini tümleştirme araçları karşılaştırması](../active-directory-hybrid-identity-design-considerations-tools-comparison.md).

### <a name="how-azure-ad-connect-works"></a>Azure AD Connect nasıl çalışır?
Azure Active Directory Connect üç birincil bileşenden oluşur: eşitleme hizmetleri, isteğe bağlı Active Directory Federasyon Hizmetleri bileşeni ve [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health.md) adlı izleme bileşeni.

<center>![Azure AD Connect Stack](./media/active-directory-aadconnect-how-it-works/AADConnectStack2.png)
</center>

* Eşitleme - Bu bileşen; kullanıcı, grup ve diğer nesnelerin oluşturulmasından sorumludur. Aynı zamanda şirket içi kullanıcılarınıza ve gruplarınıza ilişkin kimlik bilgilerinin bulut ile eşleşmesini sağlamaktan da sorumludur.
* AD FS - Federasyon, Azure AD Connect'in isteğe bağlı bir parçası olup şirket içi bir AD FS altyapısını kullanarak karma bir ortamı yapılandırabilir. Bu, etki alanına katılım SSO'su, AD oturum açma ilkesini zorlama ve akıllı kart veya 3. taraf MFA gibi karmaşık dağıtımlar gerçekleştiren kuruluşlar tarafından kullanılabilir.
* Sistem Durumu İzleme - Azure AD Connect Health, iyi bir izleme olanağı sağlayarak bu etkinliğin Azure portalında görüntülenmesi için merkezi bir konum oluşturur. Ek bilgi için bkz. [Azure Active Directory Connect Health](../connect-health/active-directory-aadconnect-health.md).

## <a name="install-azure-ad-connect"></a>Azure AD Connect'i yükleme
Azure AD Connect'i [Microsoft İndirme Merkezi](http://go.microsoft.com/fwlink/?LinkId=615771)'nden indirebilirsiniz.

| Çözüm | Senaryo |
| --- | --- |
| Başlamadan önce - [Donanım ve önkoşullar](active-directory-aadconnect-prerequisites.md) |<li>Azure AD Connect'i yüklemeye başlamadan önce tamamlamanız gereken adımlar.</li> |
| [Hızlı ayarlar](active-directory-aadconnect-get-started-express.md) |<li>Tek bir AD ormanınız varsa bu seçeneği kullanmanız önerilir. </li> <li>Parola eşitleme özelliğini kullanarak aynı parola ile kullanıcı oturumu açma.</li> |
| [Özelleştirilmiş ayarlar](active-directory-aadconnect-get-started-custom.md) |<li>Birden çok ormanınız olduğunda kullanılır. Birçok şirket içi [topolojiyi](active-directory-aadconnect-topologies.md) destekler.</li> <li>Oturum açma seçeneğinizi özelleştirin (örneğin, federasyon için ADFS) veya 3. taraf bir kimlik sağlayıcısı kullanın.</li> <li>Eşitleme özelliklerini özelleştirin (örneğin, filtreleme ve geri yazma).</li> |
| [DirSync’ten yükseltme](active-directory-aadconnect-dirsync-upgrade-get-started.md) |<li>Zaten çalışmakta olan bir DirSync sunucunuz varsa kullanılır.</li> |
| [Azure AD Eşitleme veya Azure AD Connect’ten yükseltme](active-directory-aadconnect-upgrade-previous-version.md) |<li>Tercihinize bağlı olarak birkaç farklı yöntem vardır.</li> |

[Yüklemeden sonra](active-directory-aadconnect-whats-next.md), programın beklendiği gibi çalıştığını doğrulamanız ve kullanıcılara lisans atamanız gerekir.

### <a name="next-steps-to-install-azure-ad-connect"></a>Azure AD Connect'i Yüklemek için sonraki adımlar
|Konu |Bağlantı|  
| --- | --- |
|Azure AD Connect'i indirme | [Azure AD Connect’i indirme](http://go.microsoft.com/fwlink/?LinkId=615771)|
|Hızlı ayarları kullanarak yükleme | [Azure AD Connect’i hızlı yükleme](./active-directory-aadconnect-get-started-express.md)|
|Özelleştirilmiş ayarları kullanarak yükleme | [Azure AD Connect özel yüklemesi](./active-directory-aadconnect-get-started-custom.md)|
|DirSync'ten yükseltme | [Azure AD eşitleme aracından (DirSync) yükseltme](./active-directory-aadconnect-dirsync-upgrade-get-started.md)|
|Yükleme işleminden sonra | [Yüklemeyi doğrulama ve lisansları atama](active-directory-aadconnect-whats-next.md)|

### <a name="learn-more-about-install-azure-ad-connect"></a>Azure AD Connect'i yükleme hakkında daha fazla bilgi edinin
[İşletimsel](active-directory-aadconnectsync-operations.md) sorunlara karşı hazırlıksız olmak istemezsiniz. [Olağanüstü bir durumla](active-directory-aadconnectsync-operations.md#disaster-recovery) karşılaştığınızda kolayca üstesinden gelebilmek için yedekte bir sunucu bulundurmak isteyebilirsiniz. Sık sık yapılandırma değişiklikleri yapmayı düşünüyorsanız [hazırlama modu](active-directory-aadconnectsync-operations.md#staging-mode) sunucusunu göz önünde bulundurmanız gerekir.

|Konu |Bağlantı|  
| --- | --- |
|Desteklenen topolojiler | [Azure AD Connect için topolojiler](active-directory-aadconnect-topologies.md)|
|Tasarım kavramları | [Azure AD Connect tasarım kavramları](active-directory-aadconnect-design-concepts.md)|
|Yükleme için kullanılan hesaplar | [Azure AD Connect kimlik bilgileri ve izinleri hakkında daha fazla bilgi](./active-directory-aadconnect-accounts-permissions.md)|
|İşletimsel planlama | [Azure AD Connect Eşitleme: İşletimsel görevler ve önemli noktalar](active-directory-aadconnectsync-operations.md)|
|Kullanıcı oturumu açma seçenekleri | [Azure AD Connect kullanıcı oturumu açma seçenekleri](active-directory-aadconnect-user-signin.md)|

## <a name="configure-sync-features"></a>Eşitleme özelliklerini yapılandırma
Azure AD Connect, isteğe bağlı olarak açabileceğiniz veya varsayılan olarak etkin olan çeşitli özellikler sunar. Bazı özellikler için bazen belirli senaryo ve topolojilerde daha fazla yapılandırma gerekebilir.

[Filtreleme](active-directory-aadconnectsync-configure-filtering.md), hangi nesnelerin Azure AD ile eşitleneceğine yönelik bir sınırlama getirmek istediğinizde kullanılır. Varsayılan olarak tüm kullanıcılar, kişiler, gruplar ve Windows 10 yüklü bilgisayarlar eşitlenir. Etki alanlarına, kuruluş birimlerine veya özniteliklere göre filtrelemeyi değiştirebilirsiniz.

[Parola eşitleme](active-directory-aadconnectsync-implement-password-synchronization.md), Active Directory'deki parola karmasını Azure AD ile eşitler. Son kullanıcı, şirket içinde ve bulutta aynı parolayı kullanabilir ancak parolayı yalnızca tek bir konumda yönetebilir. Yetkili olarak şirket içi Active Directory'nizi kullandığından, kendi parola ilkenizi de kullanabilirsiniz.

[Parola geri yazma](../active-directory-passwords-getting-started.md) özelliği, kullanıcılarınızın buluttaki parolalarını değiştirmelerine ve sıfırlamalarına olanak sağlamanın yanı sıra şirket içi parola ilkenizi uygular.

[Cihaz geri yazma](active-directory-aadconnect-feature-device-writeback.md) Azure AD'de kayıtlı cihazın şirket içi Active Directory'ye geri yazılmasına izin verir, bu sayede koşullu erişim için kullanılabilir.

[Yanlışlıkla silmeleri engelle](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) özelliği, varsayılan olarak açıktır ve bulut dizininizi aynı anda gerçekleştirilen çoklu silme işlemlerine karşı korur. Varsayılan olarak, her çalıştırma sırasında 500 silme işlemine izin verir. Kuruluşunuzun büyüklüğüne bağlı olarak bu ayarı değiştirebilirsiniz.

[Otomatik yükseltme](active-directory-aadconnect-feature-automatic-upgrade.md), hızlı ayar yüklemeleri için varsayılan olarak etkindir ve her zaman Azure AD Connect'in güncel olan en son sürümüne sahip olmanızı sağlar.

### <a name="next-steps-to-configure-sync-features"></a>Eşitleme özelliklerini yapılandırmak için sonraki adımlar
|Konu |Bağlantı|  
| --- | --- |
|Filtrelemeyi yapılandırma | [Azure AD Connect eşitleme: Filtrelemeyi yapılandırma](active-directory-aadconnectsync-configure-filtering.md)|
|Parola eşitleme | [Azure AD Connect eşitleme: Parola eşitlemesi uygulama](active-directory-aadconnectsync-implement-password-synchronization.md)|
|Parola geri yazma | [Parola yönetimine başlarken](../active-directory-passwords-getting-started.md)|
|Cihaz geri yazma | [Azure AD Connect’te cihaz geri yazma özelliğini etkinleştirme](active-directory-aadconnect-feature-device-writeback.md)|
|Yanlışlıkla silmeleri engelleme | [Azure AD Connect eşitleme: Yanlışlıkla Silmeleri Engelleme](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)|
|Otomatik yükseltme | [Azure AD Connect: Otomatik yükseltme](active-directory-aadconnect-feature-automatic-upgrade.md)|

## <a name="customize-azure-ad-connect-sync"></a>Azure AD Connect Eşitleme'yi özelleştirme
Azure AD Connect Eşitleme, çoğu müşteri tarafından birçok topoloji ile kullanılmak üzere tasarlanmış varsayılan bir yapılandırmaya sahiptir. Ancak her zaman varsayılan yapılandırmanın işe yaramadığı ve ayarlanması gereken durumlarla karşılaşırsınız. Bu bölümde ve bağlantılı konu başlıklarında açıklandığı üzere, bu gibi değişiklikler desteklenmektedir.

Daha önce bir eşitleme topolojisi kullanmadıysanız [teknik kavramlarda](active-directory-aadconnectsync-technical-concepts.md) açıklanan terimleri ve temel kavramları öğrenmeniz gerekir. Azure AD Connect, MIIS2003, ILM2007 ve FIM2010'un gelişmiş sürümüdür. Bazı özellikleri aynı olsa da bir çok şey değişti.

[Varsayılan yapılandırma](active-directory-aadconnectsync-understanding-default-configuration.md), yapılandırmada birden çok orman olabileceğini varsayar. Bu topolojilerde bir kullanıcı nesnesi, başka ormandaki bir kişi olarak gösterilebilir. Ayrıca kullanıcının, başka bir kaynak ormanında bağlı bir posta kutusu da olabilir. Varsayılan yapılandırma davranışı, [kullanıcılar ve kişiler](active-directory-aadconnectsync-understanding-users-and-contacts.md) bölümünde açıklanmaktadır.

Eşitlemedeki yapılandırma modeli, [bildirim temelli hazırlama](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) olarak adlandırılır. Gelişmiş öznitelik akışları, öznitelik dönüşümlerini ifade etmek için [işlevleri](active-directory-aadconnectsync-functions-reference.md) kullanır. Azure AD Connect ile birlikte sunulan araçları kullanarak tüm yapılandırmayı inceleyebilirsiniz. Yapılandırma değişiklikleri yapmanız gerekirse [en iyi yöntemleri](active-directory-aadconnectsync-best-practices-changing-default-configuration.md) uyguladığınızdan emin olun , böylece yeni sürümleri daha kolay şekilde benimseyebilirsiniz.

### <a name="next-steps-to-customize-azure-ad-connect-sync"></a>Azure AD Connect Eşitleme'yi özelleştirmek için sonraki adımlar
|Konu |Bağlantı|  
| --- | --- |
|Tüm Azure AD Connect Eşitleme makaleleri | [Azure AD Connect eşitleme](active-directory-aadconnectsync-whatis.md)|
|Teknik kavramlar | [Azure AD Connect eşitleme: Teknik Kavramlar](active-directory-aadconnectsync-technical-concepts.md)|
|Varsayılan yapılandırmayı anlama | [Azure AD Connect eşitleme: Varsayılan yapılandırmayı anlama](active-directory-aadconnectsync-understanding-default-configuration.md)|
|Kullanıcıları ve kişileri anlama | [Azure AD Connect eşitleme: Kullanıcıları ve Kişileri Anlama](active-directory-aadconnectsync-understanding-users-and-contacts.md)|
|Bildirim temelli hazırlama | [Azure AD Connect eşitleme: Bildirim Temelli Sağlama İfadelerini Anlama](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)|
|Varsayılan yapılandırmayı değiştirme | [Varsayılan yapılandırmanın değiştirilmesine ilişkin önerilen yöntemler](active-directory-aadconnectsync-best-practices-changing-default-configuration.md)|

## <a name="configure-federation-features"></a>Federasyon özelliklerini yapılandırma

Azure AD Connect, AD FS kullanarak Azure AD federasyonu yapılandırmayı ve federasyon güveninizi yönetmeyi kolaylaştıran birçok özellik sunar. Azure AD Connect, Windows Server 2012R2 veya üzeri için AD FS desteği sunar.

Azure AD Connect'i federasyon güveninizi yönetmek için kullanmıyor olsanız dahi [AD FS grubunun SSL sertifikasını güncelleştirin](active-directory-aadconnectfed-ssl-update.md).

Grubu gereken şekilde genişletmek için grubunuza [AD FS sunucusu](active-directory-aadconnect-federation-management.md#addadfsserver) ekleyin.

Birkaç tıklamayla Azure AD ile [güveni onarın](active-directory-aadconnect-federation-management.md#repairthetrust).

ADFS, [birden çok etki alanını](active-directory-aadconnect-multiple-domains.md) destekleyecek şekilde yapılandırılabilir. Örneğin, federasyon için kullanmanız gereken birden çok üst etki alanınız olabilir.

ADFS sunucunuz sertifikaları Azure AD'den otomatik olarak güncelleştirecek şekilde yapılandırılmadıysa veya ADFS dışında bir çözüm kullanıyorsanız [sertifikaları güncelleştirmeniz](active-directory-aadconnect-o365-certs.md) gerektiğinde size bildirilir.

### <a name="next-steps-to-configure-federation-features"></a>Federasyon özelliklerini yapılandırmak için sonraki adımlar
|Konu |Bağlantı|  
| --- | --- |
|Tüm AD FS makaleleri | [Azure AD Connect ve federasyon](active-directory-aadconnectfed-whatis.md)|
|Alt etki alanları bulunan ADFS'yi yapılandırma | [Azure AD ile Federasyon için Çoklu Etki Alanı Desteği](active-directory-aadconnect-multiple-domains.md)|
|AD FS grubunu yönetme | [Azure AD Connect ile AD FS yönetimi ve özelleştirmesi](active-directory-aadconnect-federation-management.md)|
|Federasyon sertifikalarını el ile güncelleştirme | [Office 365 ve Azure AD için Federasyon Sertifikalarını Yenileme](active-directory-aadconnect-o365-certs.md)|

## <a name="more-information-and-references"></a>Daha fazla bilgi ve referans
|Konu |Bağlantı|  
| --- | --- |
|Sürüm geçmişi | [Sürüm geçmişi](active-directory-aadconnect-version-history.md)|
|DirSync, Azure AD Eşitleme ve Azure AD Connect Karşılaştırması | [Dizin tümleştirmesi araçlarının karşılaştırılması](../active-directory-hybrid-identity-design-considerations-tools-comparison.md)|
|Azure AD için ADFS dışı uyumluluk listesi | [Azure AD federasyonu uyumluluk listesi](active-directory-aadconnect-federation-compatibility.md)|
|SAML 2.0 IdP'yi yapılandırma|[Çoklu Oturum Açma için SAML 2.0 Kimlik Sağlayıcısı (IdP) Kullanma](active-directory-aadconnect-federation-saml-idp.md)|
|Eşitlenen öznitelikler | [Eşitlenen öznitelikler](active-directory-aadconnectsync-attributes-synchronized.md)|
|Azure AD Connect Health'i kullanarak izleme | [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health.md)|
|Sık Sorulan Sorular | [Azure AD Connect ile ilgili SSS](active-directory-aadconnect-faq.md)|

**Ek Kaynaklar**

Şirket içi dizinlerinizi buluta taşıyıp genişletme ile ilgili 2015 sunumuna göz atın.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3862/player]
> 
> 

