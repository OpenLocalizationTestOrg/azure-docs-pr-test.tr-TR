---
title: "Azure Active Directory ile Active Directory’yi bağlayın. | Microsoft Belgeleri"
description: "Azure AD Connect, şirket içi dizinlerinizi Azure Active Directory ile tümleştirir. Bu, Office 365, Azure ve SaaS uygulamaları için ortak bir kimlik Azure AD ile tümleşik tooprovide sağlar."
keywords: "Giriş tooAzure AD Connect, Azure AD Connect'e genel bakış, Azure AD Connect, yükleme active directory nedir"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 59bd209e-30d7-4a89-ae7a-e415969825ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e49f2af4b67e9ed3ad093888541da7c82af0e052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-on-premises-directories-with-azure-active-directory"></a>Şirket içi dizinlerinizi Azure Active Directory ile tümleştirme
Azure AD Connect, şirket içi dizinlerinizi Azure Active Directory ile tümleştirir. Bu, kullanıcıların Office 365, Azure ve SaaS uygulamaları için ortak bir kimlik Azure AD ile tümleşik tooprovide sağlar. Bu konuda hello planlama, dağıtım ve işlem adımları yol gösterecektir. Bağlantılar toohello konular ilgili toothis alanı koleksiyonudur.

> [!IMPORTANT]
> [Azure AD Connect şirket içi dizininizi Azure AD ile en iyi şekilde tooconnect hello ve Office 365. Çok fazla zaman tooupgrade tooAzure AD Connect Windows Azure Active Directory eşitleme (DirSync) veya Azure AD eşitleme olarak bu araçlar artık kullanım dışı ve destek 13 Nisan 2017 tarihinde sona ermesi ulaşabileceği bir budur.](active-directory-aadconnect-dirsync-deprecated.md)
> 
> 

![Azure AD Connect nedir?](media/active-directory-aadconnect/arch.png)

## <a name="why-use-azure-ad-connect"></a>Azure AD Connect neden kullanılır?
Şirket içi dizinlerinizin Azure AD ile tümleştirilmesi, kullanıcılarınızın hem bulut kaynaklarına hem de şirket içi kaynaklara erişmesi için ortak bir kimlik oluşturarak daha üretken olmalarını sağlar. Kullanıcıların ve kuruluşların hello aşağıdaki özelliklerden yararlanabilirsiniz:

* Kullanıcılar tek kimlik tooaccess şirket uygulamaları ve Office 365 gibi hizmetler bulut kullanabilirsiniz.
* Aracı tooprovide kolay bir dağıtım deneyimi eşitleme ve oturum açma tek.
* Senaryolarınız için Hello en yeni işlevleri sağlar. Azure AD Connect; DirSync ve Azure AD Eşitleme gibi kimlik tümleştirme araçlarının eski sürümlerinin yerine kullanılmaktadır. Daha fazla bilgi için bkz. [Karma Kimlik dizini tümleştirme araçları karşılaştırması](../active-directory-hybrid-identity-design-considerations-tools-comparison.md).

### <a name="how-azure-ad-connect-works"></a>Azure AD Connect nasıl çalışır?
Azure Active Directory Connect oluşur üç birincil bileşenlerini: hello Eşitleme Hizmetleri, hello isteğe bağlı Active Directory Federasyon Hizmetleri bileşeni ve adlı İzleme bileşeni hello [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health.md) .

<center>![Azure AD Connect Stack](./media/active-directory-aadconnect-how-it-works/AADConnectStack2.png)
</center>

* Eşitleme - Bu bileşen; kullanıcı, grup ve diğer nesnelerin oluşturulmasından sorumludur. Şirket içi kullanıcılar ve gruplar için kimlik bilgilerini hello bulut ile eşleşmesini sağlamaktan sorumludur.
* AD FS - federasyon Azure AD Connect, isteğe bağlı bir parçasıdır ve kullanılan tooconfigure bir şirket içi kullanarak karma bir ortamınız olabilir AD FS altyapısı. Bu kuruluşların tooaddress karmaşık dağıtımlar, etki alanına katılım SSO'su, akıllı kart veya 3. taraf MFA ve AD oturum açma ilkesini zorlama gibi tarafından kullanılabilir.
* Sistem durumu izleme - Azure AD Connect Health izleme olanağı sağlayarak ve bu etkinliği hello Azure portal tooview merkezi bir konumda sağlayın. Ek bilgi için bkz. [Azure Active Directory Connect Health](../connect-health/active-directory-aadconnect-health.md).

## <a name="install-azure-ad-connect"></a>Azure AD Connect'i yükleme
Azure AD Connect'i hello indirme bulabilirsiniz [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=615771).

| Çözüm | Senaryo |
| --- | --- |
| Başlamadan önce - [Donanım ve önkoşullar](active-directory-aadconnect-prerequisites.md) |<li>Azure AD Connect tooinstall başlamadan önce adımları toocomplete.</li> |
| [Hızlı ayarlar](active-directory-aadconnect-get-started-express.md) |<li>Tek bir orman AD sonra bu varsa hello seçeneği toouse önerilir.</li> <li>Kullanıcı oturum oturum hello aynı parola eşitleme kullanarak parola.</li> |
| [Özelleştirilmiş ayarlar](active-directory-aadconnect-get-started-custom.md) |<li>Birden çok ormanınız olduğunda kullanılır. Birçok şirket içi [topolojiyi](active-directory-aadconnect-topologies.md) destekler.</li> <li>Oturum açma seçeneğinizi özelleştirin (örneğin, federasyon için ADFS) veya 3. taraf bir kimlik sağlayıcısı kullanın.</li> <li>Eşitleme özelliklerini özelleştirin (örneğin, filtreleme ve geri yazma).</li> |
| [DirSync’ten yükseltme](active-directory-aadconnect-dirsync-upgrade-get-started.md) |<li>Zaten çalışmakta olan bir DirSync sunucunuz varsa kullanılır.</li> |
| [Azure AD Eşitleme veya Azure AD Connect’ten yükseltme](active-directory-aadconnect-upgrade-previous-version.md) |<li>Tercihinize bağlı olarak birkaç farklı yöntem vardır.</li> |

[Yükleme sonrasında](active-directory-aadconnect-whats-next.md) beklendiği gibi çalıştığını ve toohello kullanıcı lisansları atama doğrulamanız gerekir.

### <a name="next-steps-tooinstall-azure-ad-connect"></a>Azure AD Connect tooInstall sonraki adımlar
|Konu |Bağlantı|  
| --- | --- |
|Azure AD Connect'i indirme | [Azure AD Connect’i indirme](http://go.microsoft.com/fwlink/?LinkId=615771)|
|Hızlı ayarları kullanarak yükleme | [Azure AD Connect’i hızlı yükleme](./active-directory-aadconnect-get-started-express.md)|
|Özelleştirilmiş ayarları kullanarak yükleme | [Azure AD Connect özel yüklemesi](./active-directory-aadconnect-get-started-custom.md)|
|DirSync'ten yükseltme | [Azure AD eşitleme aracından (DirSync) yükseltme](./active-directory-aadconnect-dirsync-upgrade-get-started.md)|
|Yükleme işleminden sonra | [Merhaba yüklemeyi doğrulayın ve lisansları atama](active-directory-aadconnect-whats-next.md)|

### <a name="learn-more-about-install-azure-ad-connect"></a>Azure AD Connect'i yükleme hakkında daha fazla bilgi edinin
Ayrıca tooprepare için istediğiniz [işletimsel](active-directory-aadconnectsync-operations.md) sorunları. Varsa, kolayca üstesinden toohave beklemeyi sunucu isteyebilirsiniz bir [olağanüstü durum](active-directory-aadconnectsync-operations.md#disaster-recovery). Toomake sık yapılandırma değişiklikleri planlıyorsanız, planlamanız bir [hazırlama modu](active-directory-aadconnectsync-operations.md#staging-mode) sunucu.

|Konu |Bağlantı|  
| --- | --- |
|Desteklenen topolojiler | [Azure AD Connect için topolojiler](active-directory-aadconnect-topologies.md)|
|Tasarım kavramları | [Azure AD Connect tasarım kavramları](active-directory-aadconnect-design-concepts.md)|
|Yükleme için kullanılan hesaplar | [Azure AD Connect kimlik bilgileri ve izinleri hakkında daha fazla bilgi](./active-directory-aadconnect-accounts-permissions.md)|
|İşletimsel planlama | [Azure AD Connect Eşitleme: İşletimsel görevler ve önemli noktalar](active-directory-aadconnectsync-operations.md)|
|Kullanıcı oturumu açma seçenekleri | [Azure AD Connect kullanıcı oturumu açma seçenekleri](active-directory-aadconnect-user-signin.md)|

## <a name="configure-sync-features"></a>Eşitleme özelliklerini yapılandırma
Azure AD Connect, isteğe bağlı olarak açabileceğiniz veya varsayılan olarak etkin olan çeşitli özellikler sunar. Bazı özellikler için bazen belirli senaryo ve topolojilerde daha fazla yapılandırma gerekebilir.

[Filtreleme](active-directory-aadconnectsync-configure-filtering.md) hangi nesneleri toolimit eşitlenen tooAzure AD istediğinizde kullanılır. Varsayılan olarak tüm kullanıcılar, kişiler, gruplar ve Windows 10 yüklü bilgisayarlar eşitlenir. Merhaba etki alanları, OU veya özniteliklere göre filtrelemeyi değiştirebilirsiniz.

[Parola Eşitleme](active-directory-aadconnectsync-implement-password-synchronization.md) hello parola karması Active Directory tooAzure AD içinde eşitler. Merhaba son kullanıcı aynı parolayı şirket içi ve tek bir konumda yönetebilirsiniz ancak hello bulutta hello kullanabilirsiniz. Merhaba yetkilisi olarak şirket içi Active Directory'nizi kullandığından, kendi parola ilkenizi de kullanabilirsiniz.

[Parola geri yazma](../active-directory-passwords-getting-started.md) , kullanıcıların toochange izin ve parolalarını hello bulutta ve uygulanan şirket içi parola ilkenizi sahiptir.

[Cihaz geri yazma](active-directory-aadconnect-feature-device-writeback.md) için koşullu erişim kullanılabilmesi için tooon içi Active Directory geri yazılan Azure AD toobe kayıtlı bir cihaz izin verir.

Merhaba [yanlışlıkla silmeleri engelleme](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) özelliği varsayılan olarak açıktır ve bulut dizininizi hello adresindeki Çoklu silme korur aynı anda. Varsayılan olarak, her çalıştırma sırasında 500 silme işlemine izin verir. Kuruluşunuzun büyüklüğüne bağlı olarak bu ayarı değiştirebilirsiniz.

[Otomatik yükseltmeyi](active-directory-aadconnect-feature-automatic-upgrade.md) hızlı ayar yüklemeleri için varsayılan olarak etkindir ve Azure AD Connect'in her zaman toodate hello en son sürümle yukarı sağlar.

### <a name="next-steps-tooconfigure-sync-features"></a>Sonraki adımlar tooconfigure eşitleme özellikleri
|Konu |Bağlantı|  
| --- | --- |
|Filtrelemeyi yapılandırma | [Azure AD Connect eşitleme: Filtrelemeyi yapılandırma](active-directory-aadconnectsync-configure-filtering.md)|
|Parola eşitleme | [Azure AD Connect eşitleme: Parola eşitlemesi uygulama](active-directory-aadconnectsync-implement-password-synchronization.md)|
|Parola geri yazma | [Parola yönetimine başlarken](../active-directory-passwords-getting-started.md)|
|Cihaz geri yazma | [Azure AD Connect’te cihaz geri yazma özelliğini etkinleştirme](active-directory-aadconnect-feature-device-writeback.md)|
|Yanlışlıkla silmeleri engelleme | [Azure AD Connect eşitleme: Yanlışlıkla Silmeleri Engelleme](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)|
|Otomatik yükseltme | [Azure AD Connect: Otomatik yükseltme](active-directory-aadconnect-feature-automatic-upgrade.md)|

## <a name="customize-azure-ad-connect-sync"></a>Azure AD Connect Eşitleme'yi özelleştirme
Azure AD Connect eşitleme, çoğu müşteriler ve Topolojileri için hedeflenen toowork olan varsayılan yapılandırma ile birlikte gelir. Ancak her zaman burada hello varsayılan yapılandırması çalışmaz ve ayarlanması gereken durumlar vardır. Bu bölümde ve bağlantılı konu belgelenen olarak desteklenen toomake değişiklikler var.

Toostart toounderstand hello temelleri istediğiniz ve hello hello açıklandığı şekilde kullanılan terimler için önce bir eşitleme topolojisi ile çalışmadıysanız [teknik kavramlar](active-directory-aadconnectsync-technical-concepts.md). Azure AD Connect hello evrimi MIIS2003, ILM2007 ve fım2010 ' dir. Bazı özellikleri aynı olsa da bir çok şey değişti.

Merhaba [varsayılan yapılandırması](active-directory-aadconnectsync-understanding-default-configuration.md) hello yapılandırmasında birden çok orman olabileceğini varsayar. Bu topolojilerde bir kullanıcı nesnesi, başka ormandaki bir kişi olarak gösterilebilir. Merhaba kullanıcı başka bir kaynak ormanında bağlı bir posta kutusu sahip olabilir. Merhaba varsayılan yapılandırması Hello davranışını açıklanan [kullanıcıları ve kişileri](active-directory-aadconnectsync-understanding-users-and-contacts.md).

Merhaba yapılandırma modeli çağrılır [bildirim temelli hazırlama](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md). Merhaba Gelişmiş öznitelik akışları kullanıyorsanız [işlevleri](active-directory-aadconnectsync-functions-reference.md) tooexpress dönüşümleri özniteliği. Görebilir ve hangi Azure AD Connect ile birlikte sunulan araçları kullanarak hello tüm yapılandırmayı inceleyebilirsiniz. Toomake yapılandırma değişiklikleri gerekiyorsa, hello izlediğinizden emin olun [en iyi uygulamalar](active-directory-aadconnectsync-best-practices-changing-default-configuration.md) daha kolay tooadopt yeni sürümler gelir.

### <a name="next-steps-toocustomize-azure-ad-connect-sync"></a>Toocustomize Azure AD Connect eşitleme sonraki adımlar
|Konu |Bağlantı|  
| --- | --- |
|Tüm Azure AD Connect Eşitleme makaleleri | [Azure AD Connect eşitleme](active-directory-aadconnectsync-whatis.md)|
|Teknik kavramlar | [Azure AD Connect eşitleme: Teknik Kavramlar](active-directory-aadconnectsync-technical-concepts.md)|
|Merhaba varsayılan yapılandırmayı anlama | [Azure AD Connect eşitleme: hello varsayılan yapılandırmayı anlama](active-directory-aadconnectsync-understanding-default-configuration.md)|
|Kullanıcıları ve kişileri anlama | [Azure AD Connect eşitleme: Kullanıcıları ve Kişileri Anlama](active-directory-aadconnectsync-understanding-users-and-contacts.md)|
|Bildirim temelli hazırlama | [Azure AD Connect eşitleme: Bildirim Temelli Sağlama İfadelerini Anlama](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)|
|Merhaba varsayılan yapılandırmayı değiştirme | [Merhaba varsayılan yapılandırmasını değiştirmek için en iyi uygulamalar](active-directory-aadconnectsync-best-practices-changing-default-configuration.md)|

## <a name="configure-federation-features"></a>Federasyon özelliklerini yapılandırma
ADFS, yapılandırılmış toosupport olabilir [birden çok etki alanı](active-directory-aadconnect-multiple-domains.md). Örneğin toouse Federasyon için gereken birden çok üst etki alanınız olabilir.

ADFS sunucunuz sertifikaları Azure AD'den yapılandırılmış tooautomatically güncelleştir ayarlanmadı veya ADFS dışı çözümü kullanıyorsanız, çok olduğunda sonra size bildirilecek[sertifikaları güncelleştirmeniz](active-directory-aadconnect-o365-certs.md).

### <a name="next-steps-tooconfigure-federation-features"></a>Sonraki adımlar tooconfigure Federasyon özellikleri
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

Şirket içi dizinleri toohello bulut genişletme üzerinde 2015 sunumuna göz atın.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3862/player]
> 
> 

