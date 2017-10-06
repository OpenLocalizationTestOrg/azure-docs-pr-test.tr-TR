---
title: "Azure AD Connect eşitleme: hello varsayılan yapılandırmayı anlama | Microsoft Docs"
description: "Bu makalede, Azure AD Connect eşitleme hello Varsayılan yapılandırmada açıklanmaktadır."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: ed876f22-6892-4b9d-acbe-6a2d112f1cd1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1cf95759af913cad8a1393839d3a836434e7c9bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-hello-default-configuration"></a>Azure AD Connect eşitleme: hello varsayılan yapılandırmayı anlama
Bu makalede hello out-of-box yapılandırma kuralları açıklanır. Merhaba kuralları ve bu kuralları hello yapılandırma nasıl etkiler belgeler. Bu ayrıca, Azure AD Connect eşitleme hello varsayılan yapılandırmasını açıklanmaktadır. Merhaba hello okuyucu bildirim temelli hazırlama, adlı hello yapılandırma modeli gerçek örnekte nasıl çalıştığını algıladığını hedeftir. Bu makale, zaten yüklemiş olduğunuz ve Azure AD Connect eşitleme hello Yükleme Sihirbazı'nı kullanarak yapılandırma varsayar.

Okuma hello yapılandırma modeli toounderstand hello ayrıntılarını [anlama bildirim temelli hazırlama](active-directory-aadconnectsync-understanding-declarative-provisioning.md).

## <a name="out-of-box-rules-from-on-premises-tooazure-ad"></a>Şirket içi tooAzure AD Out-of-box kuralları
Merhaba aşağıdaki ifadeleri hello out-of-box yapılandırmada bulunamadı.

### <a name="user-out-of-box-rules"></a>Kullanıcı out-of-box kuralları
Bu kurallar toohello iNetOrgPerson nesne türü de geçerlidir.

Bir kullanıcı nesnesi eşitlenen toobe aşağıdaki hello karşılaması gerekir:

* Bir sourceAnchor olması gerekir.
* Merhaba sonra Azure AD içinde nesne oluşturulduktan sonra sourceAnchor değiştiremezsiniz. Merhaba değer değiştirilen şirket içi ise, hello sourceAnchor geri tooits önceki değeri değiştirilene kadar hello nesne eşitleme durdurur.
* Merhaba accountEnabled (userAccountControl) öznitelik doldurulmuş gerekir. Bir şirket içi Active Directory ile bu öznitelik her zaman mevcut ve doldurulan durumda.

kullanıcı nesneleri aşağıdaki hello olan **değil** tooAzure AD eşitlenir:

* `IsPresent([isCriticalSystemObject])`. Merhaba yerleşik yönetici hesabı gibi birçok out-of-box nesneleri, Active Directory içinde emin olun, eşitlenmez.
* `IsPresent([sAMAccountName]) = False`. Kullanıcı nesneleri sAMAccountName özniteliği ile eşitlenmemiş emin olun. Bu durumda yalnızca pratikte NT4 yükseltilmiş bir etki alanında gerçekleşir.
* `Left([sAMAccountName], 4) = "AAD_"`, `Left([sAMAccountName], 5) = "MSOL_"`. Azure AD Connect eşitleme ve önceki sürümleri tarafından kullanılan hello hizmet hesabı eşitlemez.
* Exchange Online çalışmayan Exchange hesaplarına eşitlemez.
  * `[sAMAccountName] = "SUPPORT_388945a0"`
  * `Left([mailNickname], 14) = "SystemMailbox{"`
  * `(Left([mailNickname], 4) = "CAS_" && (InStr([mailNickname], "}") > 0))`
  * `(Left([sAMAccountName], 4) = "CAS_" && (InStr([sAMAccountName], "}")> 0))`
* Exchange Online çalışmayan nesneleri eşitlemez.
  `CBool(IIF(IsPresent([msExchRecipientTypeDetails]),BitAnd([msExchRecipientTypeDetails],&H21C07000) > 0,NULL))`  
  Bu bit maskesi (& H21C07000) nesneleri aşağıdaki hello filtreler:
  * Posta etkinleştirilmiş ortak klasör
  * Sistem Katılımcısı posta kutusu
  * Posta kutusu veritabanı posta kutusu (sistem posta)
  * Evrensel güvenlik grubu (bir kullanıcı için geçerli olmayacaktır, ancak eski nedenlerle varsa)
  * Olmayan Evrensel Grup (bir kullanıcı için geçerli olmayacaktır, ancak eski nedenlerle varsa)
  * Posta kutusu planı
  * Bulma posta kutusu
* `CBool(InStr(DNComponent(CRef([dn]),1),"\\0ACNF:")>0)`. Herhangi bir çoğaltma kurban nesne eşitlemez.

öznitelik kuralları aşağıdaki hello Uygula:

* `sourceAnchor <- IIF([msExchRecipientTypeDetails]=2,NULL,..)`. bağlantılı bir posta kutusundan Hello sourceAnchor özniteliği katkıda değil. Bağlı bir posta kutusu bulunursa hello gerçek hesap daha sonra katılmışsa varsayılır.
* Exchange ilgili öznitelikleri yalnızca Merhaba, eşitlenen öznitelik **mailNickName** bir değere sahip.
* Birden çok ormanınız olduğunda öznitelikleri sırasının hello kullanılır:
  1. Öznitelikleri ilgili toosign bileşenini hello ormanındaki etkin bir hesapla katkıda (örnek userPrincipalName için).
  2. Bir Exchange GAL (genel adres listesi) bulunabilir öznitelikleri, bir Exchange posta kutusu ile Merhaba ormandan katkıda.
  3. Posta kutusu bulunabilir, bu öznitelikler herhangi bir orman gelebilir.
  4. Exchange ilgili öznitelikleri (Merhaba GAL görünür teknik öznitelikler) hello ormandan katkıda bulunan burada `mailNickname ISNOTNULL`.
  5. Bu kurallardan biri karşılamak ve ardından hello birden çok orman varsa oluşturma (tarih) hello bağlayıcılar (orman) hangi ormanın hello öznitelikleri katkı kullanılan toodetermine sırasıdır.

### <a name="contact-out-of-box-rules"></a>Out-of-box kuralları başvurun
Bir kişi nesnesi eşitlenen toobe aşağıdaki hello karşılaması gerekir:

* Merhaba kişi, posta etkinleştirilmiş olması gerekir. Kuralları aşağıdaki hello ile doğrulanır:
  * `IsPresent([proxyAddresses]) = True)`. Merhaba proxyAddresses özniteliği doldurulmalıdır.
  * Bir birincil e-posta adresi hello proxyAddresses özniteliği veya hello posta özniteliği içinde bulunabilir. Merhaba varlığını bir @ hello içerik bir e-posta adresi olduğunu kullanılan tooverify değil. Bu iki kuralın değerlendirilen tooTrue biri olmalıdır.
    * `(Contains([proxyAddresses], "SMTP:") > 0) && (InStr(Item([proxyAddresses], Contains([proxyAddresses], "SMTP:")), "@") > 0))`. Olan bir giriş yok "SMTP:" ve varsa, bir hello dizesinde bulunan @ olabilir?
    * `(IsPresent([mail]) = True && (InStr([mail], "@") > 0)`. Merhaba doldurulmuş posta özniteliğinin ve değilse, bir hello dizesinde bulunan @ olabilir?

Kişi nesneleri aşağıdaki hello olan **değil** tooAzure AD eşitlenir:

* `IsPresent([isCriticalSystemObject])`. Kritik olarak işaretlenmelidir herhangi bir kişi nesnenin eşitlenir emin olun. Herhangi bir varsayılan yapılandırmaya sahip olmamalıdır.
* `((InStr([displayName], "(MSOL)") > 0) && (CBool([msExchHideFromAddressLists])))`.
* `(Left([mailNickname], 4) = "CAS_" && (InStr([mailNickname], "}") > 0))`. Bu nesneler Exchange Online iş olmayacaktır.
* `CBool(InStr(DNComponent(CRef([dn]),1),"\\0ACNF:")>0)`. Herhangi bir çoğaltma kurban nesne eşitlemez.

### <a name="group-out-of-box-rules"></a>Grup out-of-box kuralları
Bir grup nesnesi, eşitlenen toobe aşağıdaki hello karşılaması gerekir:

* 50. 000'den az üyeleri olmalıdır. Bu sayı, hello şirket içi grubun üyeleri, hello sayısıdır.
  * Eşitleme hello ilk kez başlamadan önce daha fazla üye varsa hello Grup eşitlenmemiş.
  * Merhaba üyelik sayısı yeniden 50. 000 ' daha düşük olana kadar eşitleme durdurur 50.000 üyeleri ulaştığında başlangıçta, ardından oluşturulduğunda gelen hello üye sayısı büyümesine durumunda.
  * Not: hello 50.000 üyelik sayısı ayrıca Azure AD tarafından zorlanır. Değiştirdiğinizde ya da bu kuralı kaldırmak olsa bile daha fazla üyesi olan mümkün toosynchronize gruplar olmayan.
* Merhaba grubu ise bir **dağıtım grubu**, posta etkinleştirilmiş olmalıdır. Bkz: [başvurun out-of-box kuralları](#contact-out-of-box-rules) için bu kural zorlanır.

Grup nesneleri aşağıdaki hello olan **değil** tooAzure AD eşitlenir:

* `IsPresent([isCriticalSystemObject])`. Merhaba yerleşik Yöneticiler grubunun gibi birçok out-of-box nesneleri, Active Directory içinde emin olun, eşitlenmez.
* `[sAMAccountName] = "MSOL_AD_Sync_RichCoexistence"`. DirSync tarafından kullanılan eski grubu.
* `BitAnd([msExchRecipientTypeDetails],&amp;H40000000)`. Rol grubu.
* `CBool(InStr(DNComponent(CRef([dn]),1),"\\0ACNF:")>0)`. Herhangi bir çoğaltma kurban nesne eşitlemez.

### <a name="foreignsecurityprincipal-out-of-box-rules"></a>ForeignSecurityPrincipal out-of-box kuralları
FSP çok "herhangi" birleştirilir (\*) hello meta veri deposu nesne. Gerçekte, bu birleştirme yalnızca kullanıcılar ve güvenlik grupları için gerçekleşir. Bu yapılandırma, ormanlar arası üyeliklerini çözümlendi ve Azure AD içinde doğru şekilde temsil sağlar.

### <a name="computer-out-of-box-rules"></a>Bilgisayar out-of-box kuralları
Bir bilgisayar nesnesi eşitlenen toobe aşağıdaki hello karşılaması gerekir:

* `userCertificate ISNOTNULL`. Yalnızca Windows 10 bilgisayarlar, bu öznitelik doldurun. Bu öznitelik alanında bir değere sahip tüm bilgisayar nesneleri eşitlenir.

## <a name="understanding-hello-out-of-box-rules-scenario"></a>Merhaba out-of-box kurallar senaryo anlama
Bu örnekte, bir hesap ormanı (A) olan bir dağıtım, bir kaynak ormanı (R) ve bir Azure AD dizini kullanıyoruz.

![Senaryo açıklaması ile resim](./media/active-directory-aadconnectsync-understanding-default-configuration/scenario.png)

Bu yapılandırmada, hello hesap ormanındaki etkin bir hesap ve hello kaynak ormanında bağlı bir posta kutusu ile devre dışı bırakılmış bir hesabı varsayılır.

Amacımız hello varsayılan yapılandırmayla şöyledir:

* Öznitelikleri ilgili toosign bileşenini hello ormanındaki etkin hello hesabıyla eşitlenir.
* Merhaba GAL (genel adres listesi) bulunabilir öznitelikleri hello ormandaki hello posta kutusu ile eşitlenir. Posta kutusu bulunabilir, başka bir ormana kullanılır.
* Bağlı bir posta kutusu bulunursa, hello bağlantılı etkinleştirilmiş hesabı hello nesne dışarı toobe tooAzure AD bulunması gerekir.

### <a name="synchronization-rule-editor"></a>Eşitleme kuralı Düzenleyicisi
Merhaba yapılandırma görüntülenebilir ve eşitleme kuralları Düzenleyicisi'ni (SRE) hello aracıyla değişti ve bir kısayol tooit hello Başlat menüsünde bulunabilir.

![Eşitleme kuralları Düzenleyicisi simgesi](./media/active-directory-aadconnectsync-understanding-default-configuration/sre.png)

Merhaba SRE bir Kaynak Seti aracıdır ve Azure AD Connect eşitleme ile yüklenir. toobe mümkün toostart, hello ADSyncAdmins grubunun bir üyesi olması gerekir. Başlatıldığında, aşağıdakine benzer bakın:

![Gelen eşitleme kuralları](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulesinbound.png)

Bu bölümde, tüm eşitleme yapılandırmanız için oluşturulan kuralların bakın. Merhaba tablodaki her satır bir eşitleme kuralıdır. toohello sol altında kural türleri, iki farklı tür listelenen hello: gelen ve giden. Gelen ve giden hello meta veri deposu hello görünümünden olur. Çoğunlukla hello üzerinde devam eden toofocus olduğunuz gelen kuralları bu genel bakış. Hello gerçek eşitleme kuralları listesi AD içinde algılanan hello şemasına göre değişir. Yukarıdaki Hello resim içinde hello hesabında orman (fabrikamonline.com) Exchange ve Lync ve eşitleme kuralları gibi hizmetlerin yok oluşturulmuş bu hizmetler için. Ancak, hello kaynak ormandaki (res.fabrikamonline.com), eşitleme kuralları bu hizmetler için bulun. Merhaba kuralları Merhaba içeriğine bağlı olarak hello sürümü algılandı farklıdır. Örneğin, Exchange 2013 ile bir dağıtımda vardır yapılandırılmış Exchange 2010/2007'den daha fazla öznitelik akışları.

### <a name="synchronization-rule"></a>Eşitleme kuralı
Bir koşul yerine getirdiğinizde akan öznitelikleri kümesi içeren bir yapılandırma nesnesi bir eşitleme kuralıdır. Aynı zamanda nasıl bir bağlayıcı alanı nesnedir hello meta veri deposu, olarak bilinen ilgili tooan nesnesinde kullanılan toodescribe olan **birleştirme** veya **eşleşen**. Merhaba eşitleme kuralları ne tooeach diğer ilişkili oldukları belirten bir öncelik değerine sahip. Daha yüksek bir önceliği daha düşük bir sayısal değer ile bir eşitleme kuralı varsa ve bir öznitelik akışı çakışması çakışma çözümü daha yüksek öncelik WINS hello.

Örnek olarak, eşitleme kuralı hello Ara **içinde AD'den – kullanıcı AccountEnabled**. Bu satırda hello SRE işaretleyin ve seçin **Düzenle**.

Bu kural bir out-of-box kuralı olduğundan, hello kural açtığınızda bir uyarı alırsınız. Herhangi bir yapmamalısınız [kutusunu tooout kuralları değişiklikleri](active-directory-aadconnectsync-best-practices-changing-default-configuration.md), bu nedenle, amaçları nelerdir sorulur. Bu durumda, yalnızca tooview hello kural istiyor. Seçin **Hayır**.

![Eşitleme kuralları uyarı](./media/active-directory-aadconnectsync-understanding-default-configuration/warningeditrule.png)

Bir eşitleme kuralı dört yapılandırma bölümü vardır: filtresi, birleştirme kuralları ve dönüştürmeler kapsamlar açıklaması.

#### <a name="description"></a>Açıklama
Merhaba ilk bölümü, bir ad ve açıklama gibi temel bilgiler sağlar.

![Açıklama sekmesinde eşitleme kural Düzenleyicisi ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncruledescription.png)

Ayrıca hangi hakkında hello türünde nesne bu kural, ilgili bağlı sistemi uygulandığı sistem bağlı ve meta veri deposu nesne türü hello bilgiler bulunur. Merhaba kaynak nesne türü kullanıcı, iNetOrgPerson veya kişi olduğunda hello meta veri deposu nesne türü kişi bakılmaksızın her zaman olur. Genel bir tür oluşmasını hello meta veri deposu nesne türü hiçbir zaman değiştirmeniz gerekir. Merhaba bağlantı türü tooJoin, StickyJoin veya sağlama ayarlayabilirsiniz. Bu ayar hello katılma kurallar bölümü ile birlikte çalışır ve daha sonra ele alınmıştır.

Bu eşitleme kuralı için parola eşitlemesi kullanıldığını da görebilirsiniz. Bir kullanıcı bu eşitleme kuralı kapsamına ise, şirket içi toocloud (Merhaba parola eşitleme özelliği etkinleştirilmiş varsayarak) hello parola eşitlenir.

#### <a name="scoping-filter"></a>Kapsamı filtresi
hello filtre kapsamı bölümünde kullanılan tooconfigure olduğunda eşitleme kuralı uygulamalıdır. Merhaba kapsam, yalnızca uygulanması için etkin kullanıcılar hello eşitleme sırasında arayan kuralı Hello adını gösterir olduğundan, yapılandırılmış bunu hello AD özniteliği **userAccountControl** hello 2 biti ayarlanmış olması gerekir değil. Merhaba eşitleme altyapısı AD içinde bir kullanıcı bulduğunda, bu eşitleme geçerlidir kural **userAccountControl** toohello ondalık değer 512 (etkin normal kullanıcı) ayarlayın. Merhaba kullanıcının olduğunda hello kural uygulanmaz **userAccountControl** too514 ayarlayın (devre dışı bırakılmış normal kullanıcı).

![Kapsam sekmesinde eşitleme kural Düzenleyicisi ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulescopingfilter.png)

Merhaba kapsam filtresi grupları ve iç içe olabilir tümceler var. Bir grup içindeki tüm yan tümceleri eşitleme kuralı tooapply için karşılanması gerekir. Birden çok grubu tanımlandığında, en az bir grup hello kural tooapply için karşılanması gerekir. Diğer bir deyişle, mantıksal veya grupları ve bir mantıksal arasında değerlendirilir ve bir grup içinde değerlendirilir. Bu yapılandırma örneği hello bulunabilir giden eşitleme kuralı **tooAAD – gruba katılma çıkışı**. Birkaç eşitleme filtre grubu vardır, örneğin bir güvenlik grupları (`securityEnabled EQUAL True`) ve dağıtım grupları için bir tane (`securityEnabled EQUAL False`).

![Kapsam sekmesinde eşitleme kural Düzenleyicisi ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulescopingfilterout.png)

Sağlanan tooAzure AD grupları olması gereken kullanılan toodefine kuralıdır. Dağıtım grupları için etkin posta toobe Azure AD ile eşitlenmiş olması gerekir, ancak güvenlik grupları için bir e-posta gerekli değildir.

#### <a name="join-rules"></a>Kuralları katılma
Merhaba üçüncü bölümdür kullanılan tooconfigure hello bağlayıcı alanı nesne hello meta dizesinde tooobjects nasıl ilişkilidir. Merhaba, arama sırasında önceki kural herhangi bir yapılandırma kuralları, katılmak için bunun yerine, devam eden toolook olduğunuz yok **içinde AD'den – kullanıcı katılma**.

![Kurallar sekmesi eşitleme kuralı Düzenleyicisi'nde katılma ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulejoinrules.png)

Merhaba Yükleme Sihirbazı'nda seçeneğe eşleşen hello hello birleştirme kuralı Merhaba içeriğine bağlıdır. Bir gelen kuralı için bir nesnenin hello kaynak bağlayıcı alanı hello değerlendirme başlatır ve hello birleştirme kuralları her grupta sırayla değerlendirilir. Kaynak nesne varsa olduğu değerlendirilen toomatch tam olarak bir nesnesi hello birleştirme kuralları birini kullanarak meta veri deposu Merhaba, hello nesneleri birleştirilir. Tüm kuralları değerlendirilemiyor ve eşleşmesi yok hello açıklama ekleyin sayfasında hello bağlantı türü kullanılır. Bu yapılandırma çok ayarlarsanız**sağlama**, yeni bir nesne hello meta veri deposu, hello hedef oluşturulur. olarak da bilinen yeni bir nesne toohello meta veri olan çok tooprovision**proje** bir nesne toohello meta veri deposu.

Merhaba birleştirme kuralları yalnızca bir kez değerlendirilir. Bağlayıcı alanı nesne ve meta veri deposu nesnesinin katıldığında, hello eşitleme kuralı hello kapsamını hala memnun olduğu sürece birleştirilmiş kalırlar.

Eşitleme kuralları değerlendirilirken tanımlanan birleştirme kurallar ile yalnızca bir eşitleme kuralı kapsamında olması gerekir. Bir nesne için birden çok eşitleme kuralları birleştirme kurallarla bulunursa, bir hata oluşturulur. Bu nedenle, hello en iyi kapsamında bir nesne için birden çok eşitleme kuralları olduğunda birleşim ile yalnızca bir eşitleme kuralı tanımlanan toohave uygulamadır. Hello out-of-box yapılandırması Azure AD Connect eşitleme için bu kurallar hello adına bakarak bulunamadı ve hello word olanlar Bul **katılma** hello sonunda hello adı. Başka bir eşitleme kuralı hello nesneleri birleştirilen veya hello hedef yeni bir nesne sağlanan bir eşitleme kuralı tanımlanan herhangi bir birleştirme kuralı olmadan hello öznitelik akışları uygulanır.

Resmi hello yukarıdaki bakarsanız, hello kural toojoin çalışıyor görebilirsiniz **objectSID** ile **msExchMasterAccountSid** (Exchange) ve **Msrtcsıp-OriginatorSid** () Lync) olan bir hesap-kaynak ormanı topolojisinde ne bekliyoruz. Merhaba bulduğunuz tüm ormanlarda aynı kuralı. Merhaba her ormanda bir hesabı veya kaynak ormanı olabilir varsayılır. Tek bir ormanda canlı ve birleştirilmiş toobe olmayan hesapları varsa, bu yapılandırma ayrıca çalışır.

#### <a name="transformations"></a>Dönüşümleri
Merhaba dönüştürme bölümü hello nesneleri birleştirilir ve hello kapsam filtresi sağlanıyorsa toohello hedef nesnesi geçerli tüm öznitelik akışları tanımlar. Toohello geri dönerseniz **içinde AD'den – kullanıcı AccountEnabled** eşitleme kuralı dönüşümleri aşağıdaki hello bulun:

![Eşitleme kuralı Düzenleyicisi dönüşümleri sekmesi ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncruletransformations.png)

tooput bu bağlamda bir hesap-kaynak orman dağıtımı, hello hesap ormanındaki etkin bir hesap ve devre dışı bırakılmış bir hesaba hello kaynak orman Exchange ve Lync ayarlarla beklenen toofind yapılandırmadır. Merhaba eşitleme sırasında arayan kuralı oturum açmak için gereken hello öznitelikleri içerir ve bu öznitelikler hello ormandan akış etkinleştirilmiş bir hesabı olduğu. Bu öznitelik akışları birlikte bir eşitleme kuralı yerleştirilir.

Bir dönüşüm farklı olabilir: sabiti, doğrudan ve ifade.

* Sürekli akışı, her zaman bir sabit kodlanmış değer akar. Yukarıdaki Hello durumda da, her zaman hello değeri ayarlar **True** adlı hello meta veri deposu öznitelikte **accountEnabled**.
* Doğrudan bir akış hello kaynak toohello Hedef öznitelik hello özniteliğinin hello değeri her zaman akar-değil.
* Merhaba üçüncü akış türü ifadesidir ve daha gelişmiş yapılandırmalarını sağlar.

Merhaba ifade VBA (Visual Basic for Applications), bu nedenle Microsoft Office deneyimiyle kişiler veya VBScript hello biçimi tanıyacağı bir dildir. Öznitelikler [attributeName] köşeli parantez içine alınır. Öznitelik adları ve işlev adları büyük küçük harfe duyarlıdır, ancak hello eşitleme kuralları Düzenleyicisi hello ifadeleri değerlendirir ve hello ifadesi geçerli değilse bir uyarı sağlayın. Tüm ifadeler, iç içe geçmiş işlevler ile tek bir satırda belirtilmiştir. tooshow hello güç hello yapılandırma dilinin hello akış pwdLastSet, ancak eklenen ek açıklamaları olan şöyledir:

```
// If-then-else
IIF(
// (hello evaluation for IIF) Is hello attribute pwdLastSet present in AD?
IsPresent([pwdLastSet]),
// (hello True part of IIF) If it is, then from right tooleft, convert hello AD time format tooa .Net datetime, change it toohello time format used by Azure AD, and finally convert it tooa string.
CStr(FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")),
// (hello False part of IIF) Nothing toocontribute
NULL
)
```

Bkz: [anlama bildirim temelli hazırlama ifadelerini](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) öznitelik akışları için hello ifade dili hakkında daha fazla bilgi için.

### <a name="precedence"></a>Önceliği
Bazı bireysel eşitleme kurallarında şimdi attıktan ancak hello kuralları hello yapılandırmada birlikte çalışır. Bazı durumlarda, birden çok eşitleme kuralları toohello bir öznitelik değeri katkıda aynı hedef özniteliği. Bu durumda, öznitelik önceliği hangi öznitelik WINS kullanılan toodetermine ' dir. Örnek olarak, hello özniteliği sourceAnchor arayın. Önemli özniteliğinin bir toobe mümkün toosign tooAzure AD içinde özniteliğidir. İki farklı eşitleme kuralları, bu öznitelik için bir öznitelik akışı bulabilirsiniz **içinde AD'den – kullanıcı AccountEnabled** ve **içinde AD'den – kullanıcı ortak**. Birkaç nesneleri birleştirilmiş toohello meta veri deposu nesne olduğunda tooSynchronization kural önceliği hello sourceAnchor özniteliği hello ormanındaki etkin bir hesapla ilk katkısı. Hiçbir etkin hesapları sonra hello eşitleme altyapısı kullanır hello catch tüm eşitleme kuralı **içinde AD'den – kullanıcı ortak**. Bu yapılandırma, devre dışı bırakılmış bile hesapları için olduğunu hala bir sourceAnchor sağlar.

![Gelen eşitleme kuralları](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulesinbound.png)

Eşitleme kuralları için Hello önceliğini gruplarında hello Yükleme Sihirbazı tarafından ayarlanır. Bir gruptaki tüm kurallar hello sahip aynı adlı ancak olan bağlı bağlı toodifferent dizinleri. Merhaba Yükleme Sihirbazı'nı verir hello kural **içinde AD'den – kullanıcı katılma** en yüksek öncelik ve onu tekrarlanan üzerinden tüm bağlı AD dizinleri. Önceden tanımlanmış bir sırada kurallarının hello sonraki gruplarla sonra sürdürür. Bir grup içinde bağlayıcılar hello sihirbazında eklenmiş hello sipariş hello hello kurallar eklenir. Başka bir bağlayıcı hello sihirbazda eklediyseniz, hello eşitleme kuralları kaldırılmasında ve hello yeni bağlayıcı kuralları son her gruba eklenir.

### <a name="putting-it-all-together"></a>Tüm bir araya getirme
Şimdi yeterli eşitleme kuralları toobe mümkün toounderstand hello yapılandırma hello ile nasıl çalıştığı hakkında biliyoruz farklı eşitleme kuralları. Bakarsanız, bir kullanıcı ve hello öznitelikleri toohello meta veri deposu katkıda bulunan, hello kuralları sırasının hello uygulanır:

| Ad | Açıklama |
|:--- |:--- |
| İçinde AD'den – kullanıcı birleştirme |Bağlayıcı alanı nesneler meta veri deposu ile birleştirme kuralı. |
| İçinde kullanıcı hesabı AD – etkin |Oturum açma tooAzure AD ve Office 365 için gerekli öznitelikler. Bu öznitelikler etkin hello hesabından istiyoruz. |
| İçinde AD'den – kullanıcı ortak Exchange'den |Merhaba genel adres listesinde bulunan öznitelikler. Merhaba veri kalitesini hello kullanıcının posta bulduk olduğu hello ormandaki en iyisidir varsayalım. |
| İçinde AD'den – kullanıcı ortak |Merhaba genel adres listesinde bulunan öznitelikler. Bir posta kutusu bulamadık durumda alanına katılmış herhangi bir nesne hello öznitelik değeri katkıda bulunabilir. |
| İçinde AD'den – kullanıcı Exchange |Yalnızca Exchange algıladıysa bulunmaktadır. Tüm altyapı Exchange özniteliklerini akar. |
| İçinde AD'den – kullanıcı Lync |Lync algıladıysa yalnızca bulunmaktadır. Tüm altyapı Lync öznitelikleri akar. |

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba yapılandırma modeli hakkında daha fazla bilgiyi [anlama bildirim temelli hazırlama](active-directory-aadconnectsync-understanding-declarative-provisioning.md).
* Merhaba ifade dili hakkında daha fazla bilgiyi [anlama bildirim temelli hazırlama ifadelerini](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md).
* Merhaba out-of-box yapılandırma şeklini okunurken devam [kullanıcıları ve kişileri anlama](active-directory-aadconnectsync-understanding-users-and-contacts.md)
* Toomake bir pratik nasıl değiştiğini içinde bildirim temelli hazırlama kullanarak görmek [nasıl toomake değişiklik toohello varsayılan yapılandırması](active-directory-aadconnectsync-change-the-configuration.md).

**Genel bakış konuları**

* [Azure AD Connect eşitleme: anlamak ve eşitleme özelleştirme](active-directory-aadconnectsync-whatis.md)
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)

