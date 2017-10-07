---
title: "aaaAzure Active Directory karma kimlik tasarımı hakkında önemli noktalar - karma kimlik benimseme stratejinizi tanımlama | Microsoft Docs"
description: "Koşullu erişim denetimi ile Azure Active Directory hello belirli koşullar hello kullanıcı kimlik doğrulaması ve erişim toohello uygulama izin vermeden önce çekme denetler. Bu koşullar sağlandığında hello kullanıcı kimlik doğrulaması ve erişim toohello uygulama izin verilir."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: b92fa5a9-c04c-4692-b495-ff64d023792c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 9ffca675d0c714392adfcbbc4dcfad12fccbac78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="define-a-hybrid-identity-adoption-strategy"></a>Bir karma kimlik benimseme stratejinizi tanımlayın
Bu görevde, ele alınan karma kimlik çözümü toomeet hello iş gereksinimleriniz için hello karma kimlik benimseme stratejinizi tanımlayın:

* [İş gereksinimlerini belirleme](active-directory-hybrid-identity-design-considerations-business-needs.md)
* [Dizin eşitleme gereksinimlerini belirleyin](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)
* [Çok faktörlü kimlik doğrulama gereksinimlerini belirleyin](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)

## <a name="define-business-needs-strategy"></a>İş gereksinimlerini stratejisini tanımlayın
Hello ilk görev belirleme hello kuruluşlar iş gereksinimlerini karşılar.  Bu çok geniş olabilir ve kapsam yayılmasını dikkatli değilse ortaya çıkabilir.  Merhaba başına basit tutmak ancak her zaman uygun hale getirmek ve gelecekteki hello değişikliği kolaylaştırmak tasarım tooplan unutmayın.  Basit bir tasarım veya çok karmaşık bir olup bağımsız olarak, Azure Active Directory, Office 365, Microsoft Online Services ve bulut kullanan uygulamaları destekler hello Microsoft Identity platformudur.

## <a name="define-an-integration-strategy"></a>Bir tümleştirme stratejisini tanımlayın
Microsoft, bulut kimlikleri, eşitlenen kimlikler ve Federasyon kimlikleri olan üç ana tümleştirme senaryolarına sahiptir.  Bu tümleştirme stratejiler birini benimsenmesi planlamanız gerekir.  Merhaba farklı olabilir ve bir seçerken hello kararları içerebilir, ne tür seçtiğiniz stratejisi tooprovide istediğiniz kullanıcı deneyimi, bazı hello varolan altyapısının yerinde'zaten var ve en düşük maliyetli hello nedir.  

![](./media/hybrid-id-design-considerations/integration-scenarios.png)

Merhaba şekil yukarıda tanımlanan hello senaryolar şunlardır:

* **Bulut kimlikleri**: Bunlar yalnızca hello bulutta mevcut hesaplardır.  Azure AD Hello durumda özellikle Azure AD dizininizi bulunması.
* **Eşitlenen**: şirket içi mevcut kimlikleri bunlar ve hello bulutta.  Azure AD Connect'i kullanarak, bu kullanıcılar oluşturulan ya da var olan Azure AD hesapları ile birleştirilmiş.  Merhaba kullanıcının parola karmasını parola karması olarak adlandırılan hello şirket içi ortamına toohello bulutta eşitlenen.  Kullanarak eşitlendiğinde hello bir uyarı hello şirket içi ortamda kullanıcı devre dışı bırakılırsa, o hesap durumu tooshow için too3 saatlerini Azure AD'de yapabilmesidir.  Toohello eşitleme zaman aralığı budur.
* **Federasyon**: Bu kimlikleri hem şirket içinde bulunur ve hello bulutta.  Azure AD Connect'i kullanarak, bu kullanıcılar oluşturulan ya da var olan Azure AD hesapları ile birleştirilmiş.  

> [!NOTE]
> Merhaba eşitleme seçenekleri hakkında daha fazla bilgi için okumaya devam [şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](connect/active-directory-aadconnect.md).
> 
> 

Aşağıdaki tablonun hello hello olumlu ve olumsuz yönlerini her stratejileri aşağıdaki hello belirlemenize yardımcı olur:

| Stratejisi | Avantajları | Olumsuz yönleri |
| --- | --- | --- |
| **Bulut kimlikleri** |Küçük bir kuruluş için daha kolay toomanage. <br> Hiçbir şey tooinstall üzerinde-şirket içi-No ek bir donanım gerekli<br>Merhaba kullanıcı hello şirketten ayrılması durumunda kolayca devre dışı |Kullanıcıların toosign bileşenini hello bulut iş yüklerini erişirken gerekir <br> Parolalar olabilir veya aynı için bulut ve şirket içi kimlikleri hello olmayabilir |
| **Eşitlendi** |Şirket içi parola hem şirket içi kimlik doğrulaması ve bulut dizinlerinizin <br>Küçük, Orta veya büyük kuruluşlarda daha kolay toomanage <br>Kullanıcıların bazı kaynaklar için çoklu oturum açma (SSO) olabilir <br> Eşitleme için tercih edilen Microsoft yöntemi <br> Daha kolay toomanage |Bazı müşterilerin belirli şirketin Polis dizinlerine hello ile bulut isteksiz toosynchronize olabilir |
| **Federasyon** |Kullanıcılar, çoklu oturum açma (SSO) olabilir <br>Bir kullanıcı sonlandırılır veya bırakır, hello hesabı hemen devre dışı bırakılabilir ve erişimi iptal,<br> Destekler Gelişmiş senaryoları, ile elde olamaz eşitlendi |Daha fazla toosetup adımları ve yapılandırma <br> Daha yüksek bakım <br> Merhaba STS altyapınız için ek donanım gerektirebilir <br> Ek donanım tooinstall hello Federasyon sunucusu gerektirebilir. AD FS kullanılırsa, ek yazılım gereklidir <br> SSO için kapsamlı Kurulum gerektirir <br> Merhaba Federasyon sunucusu kapalı olduğunda hata noktası kritik, kullanıcıların edemez tooauthenticate |

### <a name="client-experience"></a>Müşteri deneyimi
kullandığınız hello stratejisi hello kullanıcı oturum açma deneyimini benimsendiği belirler.  Merhaba aşağıdaki tablolar hello kullanıcıların kendi oturum açma beklemelisiniz bilgi sizinle toobe deneyimi sağlar.  Tüm Federasyon kimlik sağlayıcıları tüm senaryolarda SSO desteklediğini unutmayın.

**Etki alanı ile birleşik ve özel ağ uygulamaları**:

|  | Eşitlenen kimliği | Federe kimlik |
| --- | --- | --- |
| Web tarayıcıları |Form tabanlı kimlik doğrulama |Çoklu oturum açma toosupply kuruluş kimliği üzerinde bazen gerekli |
| Outlook |Kimlik bilgisi istemi |Kimlik bilgisi istemi |
| Skype Kurumsal (Lync) |Kimlik bilgisi istemi |Çoklu oturum açma için Lync, Exchange için kimlik bilgileri istenir |
| SkyDrive Pro |Kimlik bilgisi istemi |Çoklu oturum açma |
| Office aboneliği artı Pro |Kimlik bilgisi istemi |Çoklu oturum açma |

**Dış veya güvenilmeyen kaynaklardan**:

|  | Eşitlenen kimliği | Federe kimlik |
| --- | --- | --- |
| Web tarayıcıları |Form tabanlı kimlik doğrulama |Form tabanlı kimlik doğrulama |
| Outlook, Skype Kurumsal (Lync) Skydrive Pro, Office Aboneliği |Kimlik bilgisi istemi |Kimlik bilgisi istemi |
| Exchange ActiveSync |Kimlik bilgisi istemi |Çoklu oturum açma için Lync, Exchange için kimlik bilgileri istenir |
| Mobil uygulamalar |Kimlik bilgisi istemi |Kimlik bilgisi istemi |

Azure AD ile bir tooprovide Federasyon IDP veya olan giderek toouse taraf 3 sahip 1 görevden karar verdiyseniz aşağıdaki hello kullanan, desteklenen toobe yetenekleri gerekir:

* Merhaba SP Lite profili uyumlu olan herhangi bir SAML 2.0 sağlayıcısına kimlik doğrulama tooAzure AD ve ilişkili uygulamaları destekler
* Kimlik doğrulama tooOWA, SPO, kolaylaştıran destekler pasif kimlik vs.
* Exchange Online istemcileri hello SAML 2.0 Gelişmiş istemci profili (ECP) desteklenebilir

Ayrıca hangi özellikleri kullanılamaz olarak haberdar olmanız gerekir:

* WS-Güven/Federasyon desteği olmadan, tüm etkin istemciler çalışmamasına neden olur
  * Hiçbir Lync istemcisi, OneDrive istemcisi, Office aboneliği, Office Mobile önceki tooOffice 2016 anlamına
* Office toopassive kimlik doğrulamasının geçiş izni verdiği bunları toosupport saf SAML 2.0 IdPs ancak destek bir istemci istemci temelinde çıkarılsın

> [!NOTE]
> Merhaba en güncel listesi hello makale http://aka.ms/ssoproviders okuyun.
> 
> 

## <a name="define-synchronization-strategy"></a>Eşitleme stratejisini tanımlayın
Bu görevde, kullanılan toosynchronize hello kuruluşun şirket içi veri toohello Bulutu ile ne olacağını hello araçları tanımlayacaksınız topoloji kullanması gerekir.  Çoğu kuruluş Active Directory'yi kullanmak için bazı ayrıntılı olarak Azure AD Connect tooaddress hello soruları yukarıdaki kullanma hakkında bilgi sağlanır.  Active Directory olmayan ortamlarda, FIM 2010 R2 kullanma hakkında bilgi yok veya MIM 2016 toohelp bu strateji planlayın.  Ancak, Azure AD Connect gelecek sürümlerde LDAP dizinleri, bu nedenle, zaman çizelgesinde bağlı olarak destekler, bu bilgileri mümkün tooassist olabilir.

### <a name="synchronization-tools"></a>Eşitleme araçları
Hello yıllar içinde birkaç eşitleme araçları sahip ve mevcut olan çeşitli senaryoları için kullanılır.  Şu anda Azure AD Connect olduğu hello tüm desteklenen senaryolar tercih edin tootool.  AAD eşitleme ve DirSync yine de geçici ve hatta şimdi ortamınızda mevcut olabilir. 

> [!NOTE]
> Merhaba son her aracı hakkında bilgi için desteklenen hello özellikleri okuma [dizin tümleştirme araçları karşılaştırması](active-directory-hybrid-identity-design-considerations-tools-comparison.md) makalesi.  
> 
> 

### <a name="supported-topologies"></a>Desteklenen topolojiler
Bir eşitleme stratejinizi tanımlarken kullanılır hello topoloji belirlenmesi gerekir. Merhaba bağlı olarak, hangi topoloji belirleyebilirsiniz 2. adımda belirlendi hello uygun bir toouse bilgilerdir. Merhaba tek orman, tek Azure AD topoloji hello en yaygın olan ve tek bir Active Directory ormanı ve Azure AD tek bir örneğini oluşur.  Bu hello senaryoları çoğunu içinde kullanılan toobe geçiyor ve beklenen hello topoloji Azure AD Connect Express yüklemesi hello aşağıdaki çizimde gösterildiği gibi kullanırken.

![](./media/hybrid-id-design-considerations/single-forest.png)Tek orman senaryo olduğu için daha küçük ve büyük kuruluşların toohave yaygın birden çok orman, Şekil 5'te gösterildiği gibi.

> [!NOTE]
> Hakkında daha fazla bilgi içi farklı hello ve Azure AD topolojileri Azure AD Connect eşitleme ile Merhaba makalesini okuyun [Azure AD Connect için topolojiler](connect/active-directory-aadconnect-topologies.md).
> 
> 

![](./media/hybrid-id-design-considerations/multi-forest.png) 

Çoklu orman senaryosu

Bu hello durumda sonra çok forest tek hello hello aşağıdaki öğeleri doğruysa, Azure AD topoloji düşünülmesi gereken:

* Tüm ormanlarda yalnızca 1 kimlik kullanıcınız – kullanıcılar bölümü aşağıdaki tanıtan hello bu daha ayrıntılı olarak açıklanmaktadır.
* Merhaba kullanıcı kimliklerini bulunduğu toohello orman doğrular
* UPN ve kaynak bağlantısı (değişmez kimliği) bu ormandan gelir
* Tüm ormanlarda Azure AD Connect tarafından erişilebilir – bu toobe etki alanına katılmış gerekli değildir ve bu bu kolaylaştırır, çevre ağınızda yerleştirilebilir anlamına gelir.
* Kullanıcıların yalnızca bir posta kutusuna sahip
* bir kullanıcının posta barındıran hello ormanda hello Exchange Genel adres listesi (GAL) görünür öznitelikler için en iyi veri kalitesini hello vardır
* Merhaba kullanıcı hiçbir posta kutusu olduğu sonra herhangi bir orman olabilir kullanılan toocontribute bu değerleri olabilir
* Bağlı bir posta kutusu varsa, sonra bulunmaktadır de başka bir hesap kullanılan farklı orman toosign.

> [!NOTE]
> Her iki şirket içi ve hello cloud mevcut nesneleri "benzersiz bir tanımlayıcıya bağlı". Dizin eşitleme Hello bağlamında, başvuruda bulunulan tooas hello SourceAnchor bu benzersiz tanımlayıcısı değil. Çoklu oturum açma Hello bağlamda başvurulan tooas hello İmmutableıd budur. [İçin Azure AD Connect tasarım kavramları](connect/active-directory-aadconnect-design-concepts.md#sourceanchor) SourceAnchor hello kullanımıyla ilgili daha fazla hususlara için.
> 
> 

Yukarıdaki Hello doğru değildir ve birden fazla etkin hesabı ya da birden fazla posta kutusu varsa, Azure AD Connect birini seçin ve hello diğer yoksay.  Posta kutularını ancak başka bir hesap bağladıysanız, bu hesapları dışarı aktarılan tooAzure AD olmayacak ve bu kullanıcı herhangi bir grup üyesi olmayacaktır.  Bu nasıl içindeydi alanından farklıdır DirSync ile Merhaba geçmiş ve bu çok ormanlı senaryolar kasıtlı toobetter desteği. Çoklu orman senaryosu hello aşağıdaki çizimde gösterilmektedir.

![](./media/hybrid-id-design-considerations/multiforest-multipleAzureAD.png) 

**Çoklu orman birden çok Azure AD senaryosu**

1:1 ilişki bir Azure AD Connect eşitleme sunucusu ve Azure AD dizini arasında tutulur, ancak bir kuruluş için Azure AD yalnızca tek bir dizinde toohave desteklenir önerilir.  Azure AD her örneği için Azure AD Connect yüklemesi gerekir.  Ayrıca, Azure AD tasarım gereği yalıtılır ve bir Azure AD örneğini kullanıcılar mümkün toosee kullanıcılar başka bir örnekte olmayacaktır.

Mümkündür ve desteklenen tooconnect bir içi hello aşağıdaki çizimde gösterildiği gibi Active Directory toomultiple Azure AD dizinlerinden örneği:

![](./media/hybrid-id-design-considerations/single-forest-flitering.png) 

**Tek orman filtreleme senaryosu**

Sipariş toodo bu hello aşağıdakilerin doğru olması gerekir:

* Azure AD Connect eşitleme sunucusu birbirini dışlayan bir nesneler kümesini sahip oldukları her şekilde filtreleme için yapılandırılmış olması gerekir.  Bu her sunucu tooa belirli etki alanı ya da OU'yu kapsamı tarafından yapılır.
* Bir DNS etki alanı yalnızca tek bir kaydedilebilir hello hello hello kullanıcıların UPN içi bağlı AD ayrı ad alanları kullanmanız gerekir böylece Azure AD dizini
* Bir Azure AD örneğini kullanıcılar yalnızca kendi örneği mümkün toosee kullanıcılardan olacaktır.  Bunlar almayacak hello mümkün toosee kullanıcıların diğer örnekleri yer
* Hello Azure AD dizinlerden biri Exchange etkinleştirebilirsiniz yalnızca karma hello ile şirket içi AD
* Karşılıklı exclusivity toowrite geri de geçerlidir.  Bu, bu tek şirket içi yapılandırma varsayın beri bu topolojisi ile desteklenmeyen bazı geri yazma özellikleri sağlar.  Buna aşağıdakiler dahildir:
  * Grup geri yazma varsayılan yapılandırmaya sahip
  * Cihaz geri yazma

Merhaba aşağıdaki desteklenmez ve bir uygulama seçilmelidir değil dikkat edin:

* Nesne yapılandırılmış toosynchronize birbirini dışlayan olsa bile toohello aynı Azure AD directory bağlanan birden çok Azure AD Connect eşitleme sunucusu ayarlayın desteklenen toohave değil
* Desteklenmeyen toosync hello aynı kullanıcı toomultiple Azure AD dizinleri. 
* Ayrıca, bir yapılandırma değişikliği toomake kullanıcıların bir Azure AD tooappear olarak başka bir Azure AD dizininde kişiler desteklenmeyen toomake unutulmamalıdır. 
* Desteklenmeyen toomodify Azure AD Connect eşitleme tooconnect toomultiple Azure AD dizinler de olabilir.
* Azure AD dizinleri yalıtılmış tasarım gereği ' dir. Bunu desteklenmeyen toochange hello Azure AD Connect eşitleme tooread verilerini hello dizinler arasındaki girişimi toobuild ortak ve birleşik GAL başka bir Azure AD dizininde bir yapılandırmadır. Aynı zamanda tooanother kişiler gibi desteklenmeyen tooexport kullanıcıları olan şirket içi Azure AD Connect eşitleme kullanarak AD.

> [!NOTE]
> Kuruluşunuz, ağınızdaki bilgisayarlar toohello Internet bağlanmasını kısıtladığında, hello uç noktaları (FQDN'ler, IPv4 ve IPv6 adres aralıklarını) Bu makalede listelenmektedir içeren listeler ve Internet Explorer Güvenilen siteler bölgesinde, Gidene izin ver istemci bilgisayarları tooensure bilgisayarlarınızı başarıyla Office 365 kullanabilirsiniz. Daha fazla bilgi için okuma [Office 365 URL'leri ve IP adresi aralıkları](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US).
> 
> 

## <a name="define-multi-factor-authentication-strategy"></a>Çok faktörlü kimlik doğrulaması stratejisini tanımlayın
Bu görevde hello çok faktörlü kimlik doğrulama stratejisi toouse tanımlayacaksınız.  Azure multi-Factor Authentication iki farklı sürümde gelir.  Bir bulut tabanlı ve diğer hello şirket hello Azure MFA sunucusu kullanarak tabanlı.  Size, belirleyebilirsiniz hello değerlendirme hangi çözümün stratejinizi için doğru bir hello temel.  Tasarım seçeneği, şirketinizin güvenlik gereksinimi karşılamak toodetermine aşağıdaki Hello tabloyu kullanın:

Çok faktörlü tasarım seçenekleri:

| Varlık toosecure | Merhaba bulutta MFA | Şirket içi MFA |
| --- | --- | --- |
| Microsoft uygulamaları |Evet |Evet |
| Merhaba uygulama galerisinde SaaS uygulamaları |Evet |Evet |
| Azure AD Uygulaması Proxy üzerinden yayımlanan IIS uygulamaları |Evet |Evet |
| Hello Azure AD uygulaması Proxy yayımlanmayan IIS uygulamaları |Yok |Evet |
| Uzaktan erişim VPN, RDG olarak |Yok |Evet |

Stratejinizi için bir çözüm üzerinde kapatılan olsa bile, yine, kullanıcılarınızın nerede olduğunuza toouse hello değerlendirme üstten gerekir.  Bu hello çözüm toochange neden olabilir.  Tooassist Hello tabloda, bu belirleme kullanın:

| Kullanıcı konumu | Tercih edilen tasarım seçeneği |
| --- | --- |
| Azure Active Directory |Multi-FactorAuthentication hello bulutta |
| AD FS ile federasyon kullanana Azure AD ve şirket içi AD |Her ikisi |
| Azure AD ve şirket içi AD kullanarak Azure AD Connect parola eşitleme yok |Her ikisi |
| Azure AD ve parola eşitleme ile Azure AD Connect kullanarak şirket içi |Her ikisi |
| Şirket içi AD |Multi-Factor Authentication Sunucusu |

> [!NOTE]
> Ayrıca, seçtiğiniz hello çok faktörlü kimlik doğrulaması tasarım seçeneği tasarımınız için gerekli olan hello özellikleri desteklediğini de emin olmalısınız.  Daha fazla bilgi için okuma [hello multi-Factor güvenlik çözümünü seçtiğiniz](../multi-factor-authentication/multi-factor-authentication-get-started.md#what-am-i-trying-to-secure).
> 
> 

## <a name="multi-factor-auth-provider"></a>Multi-Factor Auth sağlayıcısı
Çok faktörlü kimlik doğrulaması varsayılan olarak, bir Azure Active Directory kiracısı olan küresel yöneticiler tarafından kullanılabilir. Kullanıcılarınızın tooextend çok faktörlü kimlik doğrulaması tooall istiyor ve/veya tooyour genel Yöneticiler toobe mümkün tootake avantajı özellikler hello Yönetim Portalı, özel Karşılama ve raporlar gibi istiyorsanız, ancak daha sonra satın alın ve yapılandırmanız gerekir Çok faktörlü kimlik doğrulama sağlayıcısı.

> [!NOTE]
> Ayrıca, seçtiğiniz hello çok faktörlü kimlik doğrulaması tasarım seçeneği tasarımınız için gerekli olan hello özellikleri desteklediğini de emin olmalısınız. 
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
[Veri koruma gereksinimlerini belirleme](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md)

## <a name="see-also"></a>Ayrıca bkz.
[Tasarım konularına genel bakış](active-directory-hybrid-identity-design-considerations-overview.md)

