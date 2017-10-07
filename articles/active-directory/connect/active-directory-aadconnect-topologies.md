---
title: 'Azure AD Connect: destekli topolojileri | Microsoft Docs'
description: "Bu konuda, Azure AD Connect için desteklenen ve desteklenmeyen topolojileri ayrıntıları"
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 1034c000-59f2-4fc8-8137-2416fa5e4bfe
ms.service: active-directory
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: identity
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 41632a54e8e85492fbf1a751ef4e618c8870abe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="topologies-for-azure-ad-connect"></a>Azure AD Connect için topolojiler
Bu makalede, çeşitli şirket içi ve Azure AD Connect eşitleme hello anahtar tümleştirme çözümü kullanan Azure Active Directory (Azure AD) topolojileri açıklanır. Bu makalede, desteklenen ve desteklenmeyen yapılandırmalar içerir.

Resim hello makalede hello gösterge şöyledir:

| Açıklama | Simgesi |
| --- | --- |
| Şirket içi Active Directory ormanı |![Şirket içi Active Directory ormanı](./media/active-directory-aadconnect-topologies/LegendAD1.png) |
| Şirket içi Active Directory ile filtrelenmiş alma |![Active Directory ile filtrelenmiş alma](./media/active-directory-aadconnect-topologies/LegendAD2.png) |
| Azure AD Connect eşitleme sunucusu |![Azure AD Connect eşitleme sunucusu](./media/active-directory-aadconnect-topologies/LegendSync1.png) |
| "Hazırlama modu" azure AD Connect eşitleme sunucusu |!["Hazırlama modu" azure AD Connect eşitleme sunucusu](./media/active-directory-aadconnect-topologies/LegendSync2.png) |
| Forefront Identity Manager (FIM) 2010 veya Microsoft Identity Manager (MIM) 2016 ile GALSync |![FIM 2010 veya MIM 2016 ile GALSync](./media/active-directory-aadconnect-topologies/LegendSync3.png) |
| Ayrıntılı azure AD Connect eşitleme sunucusu |![Ayrıntılı azure AD Connect eşitleme sunucusu](./media/active-directory-aadconnect-topologies/LegendSync4.png) |
| Azure AD |![Azure Active Directory](./media/active-directory-aadconnect-topologies/LegendAAD.png) |
| Desteklenmeyen senaryo |![Desteklenmeyen senaryo](./media/active-directory-aadconnect-topologies/LegendUnsupported.png) |

## <a name="single-forest-single-azure-ad-tenant"></a>Tek bir orman, tek bir Azure AD kiracısı
![Tek bir ormana ve tek bir kiracı için topoloji](./media/active-directory-aadconnect-topologies/SingleForestSingleDirectory.png)

Merhaba en yaygın tek bir orman, bir veya birden çok etki alanı ve tek bir Azure AD Kiracı şirket içi topolojidir. Azure AD kimlik doğrulaması için parola eşitleme kullanılır. Azure AD Connect Hello hızlı yükleme yalnızca bu topoloji destekler.

### <a name="single-forest-multiple-sync-servers-tooone-azure-ad-tenant"></a>Tek orman, birden çok eşitleme sunucuları tooone Azure AD Kiracı
![Desteklenmeyen, filtrelenmiş topolojisi tek orman](./media/active-directory-aadconnect-topologies/SingleForestFilteredUnsupported.png)

Birden çok Azure AD Connect eşitleme sunucusu bağlı toohello aynı Azure AD Kiracı desteklenmiyor sahip, dışındaki bir [server hazırlama](#staging-server). Bu sunucular ile birbirini dışlayan bir nesneler kümesini yapılandırılmış toosynchronize olsa bile desteklenmeyen sahip. Tek bir sunucudan hello ormandaki tüm etki alanları erişemezse ya da birçok sunucuya toodistribute yük istiyorsanız bu topoloji kabul.

## <a name="multiple-forests-single-azure-ad-tenant"></a>Birden çok orman, tek bir Azure AD kiracısı
![Birden çok orman ve tek bir kiracı için topoloji](./media/active-directory-aadconnect-topologies/MultiForestSingleDirectory.png)

Çoğu kuruluş ortamları ile birden çok şirket içi Active Directory ormanı sahiptir. Birden fazla şirket içi Active Directory ormanına sahip olmak için çeşitli nedenleri vardır. Tasarımlar hesap-kaynak ormanına ve hello birleşme veya sonucu edinme ile tipik örnekleridir.

Birden çok orman, tüm ormanlardaki olduğunda tek bir tarafından erişilebilir olmalıdır Azure AD Connect eşitleme sunucusu. Toojoin hello server tooa etki alanına sahip değilsiniz. Varsa gerekli tooreach tüm ormanlarda hello sunucu bir çevre ağında (Ayrıca DMZ, sivil bölge bilinen ve Perdeli alt ağ) yerleştirebilirsiniz.

Hello Azure AD Connect Yükleme Sihirbazı'nı birden fazla ormanda temsil çeşitli seçenekler tooconsolidate kullanıcılar sunar. Merhaba bir kullanıcı, Azure AD içinde yalnızca bir kez temsil edilir hedeftir. Merhaba özel yükleme yolu hello Yükleme Sihirbazı'nda yapılandırabileceğiniz bazı ortak topolojileri vardır. Merhaba üzerinde **kullanıcılarınızı benzersiz olarak tanımlama** sayfası, topolojinizi temsil eden select hello ilgili seçeneği. Merhaba birleştirme yalnızca kullanıcılar için yapılandırılır. Yinelenen grupları hello varsayılan yapılandırmayla birleştirilmiş değil.

Ortak topolojileri hakkında hello bölümlerde açıklanan [ayrı topolojileri](#multiple-forests-separate-topologies), [tam mesh](#multiple-forests-full-mesh-with-optional-galsync), ve [hesap-kaynak topoloji hello](#multiple-forests-account-resource-forest).

Azure AD Connect eşitleme Hello Varsayılan yapılandırmada varsayılır:

* Her kullanıcının yalnızca bir etkin hesaba sahip ve bu hesabın bulunduğu hello orman kullanılan tooauthenticate hello kullanıcıdır. Bu, hem parola eşitleme hem de Federasyon için varsayılır. UserPrincipalName ve sourceAnchor/İmmutableıd bu ormandan gelir.
* Her kullanıcının yalnızca bir posta kutusu vardır.
* bir kullanıcının hello posta kutusunu barındıran hello ormanda hello en iyi veri kalitesini hello Exchange Genel adres listesi (GAL) görünür öznitelikler için vardır. Merhaba kullanıcı için hiçbir posta kutusu varsa, herhangi bir orman kullanılan toocontribute olabilir bu değerleri özniteliği.
* Bağlı bir posta kutusu varsa, yoktur da bir hesap oturum açma için kullanılan farklı bir ormanda.

Ortamınızı bu varsayımları eşleşmiyorsa hello aşağıdakiler gerçekleşir:

* Birden fazla etkin hesabı ya da birden fazla posta kutusu varsa, hello eşitleme altyapısı birini seçer ve diğer hello yok sayar.
* Başka bir etkin hesabı bağlı posta kutusu dışarı aktarılan tooAzure AD değil. Merhaba kullanıcı hesabı, herhangi bir grubu üye olarak gösterilmiyor. DirSync bağlı bir posta kutusu her zaman normal bir posta kutusu olarak temsil edilir. Bu kasıtlı olarak farklı davranışlar toobetter destek birden çok orman senaryoları değişikliktir.

Daha ayrıntılı bilgi bulabilirsiniz [anlama hello varsayılan yapılandırma](active-directory-aadconnectsync-understanding-default-configuration.md).

### <a name="multiple-forests-multiple-sync-servers-tooone-azure-ad-tenant"></a>Birden çok orman, birden çok eşitleme sunucuları tooone Azure AD Kiracı
![Birden fazla ormanına ve birden çok eşitleme sunucusu için desteklenmeyen topolojisi](./media/active-directory-aadconnect-topologies/MultiForestMultiSyncUnsupported.png)

Birden fazla Azure AD Connect eşitleme bağlı sunucu tooa Azure AD kiracısı tek sahip desteklenmiyor. Merhaba hello kullanımını istisnadır bir [server hazırlama](#staging-server).

### <a name="multiple-forests-separate-topologies"></a>Birden çok orman, ayrı topolojileri
![Kullanıcıların yalnızca bir kez temsil eden tüm dizinlerde seçeneği](./media/active-directory-aadconnect-topologies/MultiForestUsersOnce.png)

![Birden çok orman ve ayrı topolojileri gösterimi](./media/active-directory-aadconnect-topologies/MultiForestSeperateTopologies.png)

Bu ortamda, tüm şirket içi ormanları ayrı varlıklar olarak kabul edilir. Hiçbir kullanıcı, başka bir ormanda mevcuttur. Her ormanda kendi Exchange kuruluşu vardır ve hello ormanlar arasında hiçbir GALSync yoktur. Bu topoloji, burada her iş birimi bağımsız olarak çalışır hello durum birleşme/edinme sonra veya bir kuruluşta olabilir. Bu ormanlarda: içinde hello Azure AD aynı kuruluşta ve birleşik GAL ile görünür. Resim önceki hello her ormanda her nesne hello meta veri deposunda bir kez temsil ve hello hedef Azure AD kiracısında bir araya getirilir.

### <a name="multiple-forests-match-users"></a>Birden çok orman: eşleşen kullanıcıları
Ortak tooall bu senaryolar olduğundan, dağıtım ve güvenlik grupları, kullanıcıları, kişileri ve yabancı güvenlik sorumlusu (FSP) bir karışımını içerebilir. FSP Active Directory etki alanı Hizmetleri (AD DS) toorepresent üyeleri bir güvenlik grubundaki diğer ormanlardaki kullanılır. Tüm FSP Azure AD içinde çözümlenen toohello gerçek nesne var.

### <a name="multiple-forests-full-mesh-with-optional-galsync"></a>Birden çok orman: tam mesh isteğe bağlı GALSync ile
![Kullanıcı kimlikleri birden fazla dizinde bulunur zaman eşleştirme için hello posta özniteliğinin kullanma seçeneği](./media/active-directory-aadconnect-topologies/MultiForestUsersMail.png)

![Birden çok orman için tam ağ topolojisi](./media/active-directory-aadconnect-topologies/MultiForestFullMesh.png)

Tam ağ topolojisi, kullanıcılara ve tüm ormanda bulunan kaynaklar toobe sağlar. Genellikle, hello ormanlar arasında iki yönlü güven vardır.

Birden fazla ormanda Exchange varsa olabilir (isteğe bağlı) bir şirket içi GALSync çözümü. Her kullanıcı ardından diğer tüm ormanlarda kişi olarak temsil edilir. GALSync sık FIM 2010 veya MIM 2016 aracılığıyla uygulanır. Azure AD Connect, şirket içi GALSync için kullanılamaz.

Bu senaryoda, kimlik nesneleri hello posta özniteliği ile birleştirilir. Bir posta kutusunu bir ormanda olan bir kullanıcı hello hello kişilerle katılmışsa diğer ormanlardaki.

### <a name="multiple-forests-account-resource-forest"></a>Birden çok orman: hesap-kaynak ormanı
![Kimlikleri birden fazla dizinde bulunur zaman eşleştirme için hello objectSID ve msExchMasterAccountSID öznitelikleri kullanma seçeneği](./media/active-directory-aadconnect-topologies/MultiForestUsersObjectSID.png)

![Birden çok orman için hesap-kaynak ormanı topolojisi](./media/active-directory-aadconnect-topologies/MultiForestAccountResource.png)

Bir veya daha fazla sahip bir hesap-kaynak ormanı topolojisinde *hesap* etkin kullanıcı hesapları ile ormanlar. Bir veya daha fazla de sahip *kaynak* devre dışı bırakılan hesapları ormanlar.

Bu senaryoda, tüm hesap ormanları bir (veya daha fazla) kaynak orman güvenleri. Merhaba kaynak ormanda Exchange ve Lync ile genişletilmiş bir Active Directory şemasını genellikle vardır. Tüm Exchange ve Lync Hizmetleri, diğer paylaşılan hizmetler yanı sıra, bu ormanda yer alır. Kullanıcılar bu ormanda bir devre dışı bırakılmış kullanıcı hesabı varsa ve hello posta kutusu bağlı olduğu toohello hesap ormanı.

## <a name="office-365-and-topology-considerations"></a>Office 365 ve topolojisi hakkında önemli noktalar
Bazı Office 365 iş yükleri üzerinde desteklenen topolojiler bazı kısıtlamalar vardır:

| İş yükü | Kısıtlamaları |
--------- | ---------
| Exchange Online | Birden fazla şirket içi Exchange kuruluşu ise (diğer bir deyişle, Exchange bir orman daha dağıtılan toomore bırakıldı), Exchange 2013 SP1'i kullanın veya sonraki bir sürümü. Daha fazla bilgi için bkz: [birden çok Active Directory ormanına karma dağıtımlarında](https://technet.microsoft.com/library/jj873754.aspx). |
| Skype Kurumsal | Birden çok şirket içi ormanları kullanırken, yalnızca hello hesabına kaynak orman topolojisini desteklenir. Daha fazla bilgi için bkz: [Business Server 2015 için Skype ortam gereksinimleri](https://technet.microsoft.com/library/dn933910.aspx). |


## <a name="staging-server"></a>Hazırlama sunucusu
![Hazırlama sunucu topoloji](./media/active-directory-aadconnect-topologies/MultiForestStaging.png)

İkinci bir sunucu yüklemeyi azure AD Connect destekler *hazırlama modu*. Bu modundaki bir sunucu, tüm bağlı dizinlerden verileri okur ancak hiçbir şey tooconnected dizinleri yazmaz. Merhaba normal eşitleme döngüsü kullanır ve bu nedenle hello kimlik verilerini güncelleştirilmiş bir kopyasını sahiptir.

Burada hello birincil sunucu başarısız olağanüstü bir durumda sunucu hazırlama toohello başarısız olabilir. Bu hello Azure AD Connect Sihirbazı'nda yapın. Hiçbir altyapı hello birincil sunucusu ile paylaşıldığından bu ikinci sunucuyu farklı bir veri merkezinde yer alabilir. Merhaba birincil sunucu toohello ikinci sunucusunda yapılan herhangi bir yapılandırma değişikliği el ile kopyalamanız gerekir.

Hazırlama sunucu tootest verilerinizde sahip yeni bir özel yapılandırma ve hello efekt kullanabilirsiniz. Önizleme hello değişiklikleri ve hello yapılandırmasını ayarlayın. Merhaba yeni yapılandırmayla memnun kaldığınızda, sunucu hello active server hazırlama hello yapmak ve hello eski active server toostaging modunu ayarlayın.

Bu yöntem tooreplace hello active eşitleme sunucusu de kullanabilirsiniz. Merhaba yeni bir sunucu hazırlayın ve toostaging modunu ayarlayın. İyi durumda, hazırlama modu (etkin hale), devre dışı olduğundan emin olun ve hello şu anda etkin sunucuyu kapatın.

Farklı veri merkezlerinde bulunan birden çok yedekleme toohave istiyorsanız bir hazırlama sunucusunda birden çok olası toohave yarar.

## <a name="multiple-azure-ad-tenants"></a>Birden çok Azure AD kiracılarıyla
Bir kuruluş için Azure AD'de tek bir kiracı olması önerilir.
Birden çok Azure AD kiracılarıyla toouse planlama önce hello makalesine bakın [Azure AD'de idari Birim Yönetimi](../active-directory-administrative-units-management.md). Tek bir kiracı burada kullanabileceğiniz ortak senaryolar kapsar.

![Birden fazla ormanına ve birden çok Kiracı için topoloji](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectory.png)

Bir Azure AD Connect eşitleme sunucusu ve Azure AD kiracısı arasında 1:1 ilişkisi yoktur. Her bir Azure AD Kiracı için bir Azure AD Connect eşitleme sunucusu yüklemesi gerekir. Hello Azure AD Kiracı örnekleri tasarım gereği yalıtılır. Diğer bir deyişle, bir kiracı kullanıcılar hello kullanıcıların diğer Kiracı göremezsiniz. Bu ayrım istiyorsanız, desteklenen bir yapılandırmadır. Aksi takdirde hello kullanması gereken tek bir Azure AD Kiracı modeli.

### <a name="each-object-only-once-in-an-azure-ad-tenant"></a>Her nesne yalnızca bir kez Azure AD kiracısı
![Tek bir orman için filtrelenmiş topolojisi](./media/active-directory-aadconnect-topologies/SingleForestFiltered.png)

Bu topolojide, bir Azure AD Connect eşitleme bağlı tooeach Azure AD Kiracı sunucusudur. böylece her nesneleri toooperate birbirini dışlayan bir dizi sahip hello Azure AD Connect eşitleme sunucuları filtreleme için yapılandırılmalıdır. Örneğin, her sunucu tooa belirli etki alanı ya da kuruluş birimi kapsamını olabilir.

Bir DNS etki alanı yalnızca tek bir kaydedilebilir Azure AD kiracısı. Merhaba UPN'ler hello şirket içi Active Directory örneğinde hello kullanıcılarının ayrıca ayrı ad alanları kullanmanız gerekir. Örneğin, resim önceki hello, üç ayrı UPN soneki hello şirket içi Active Directory örneğinde kayıtlı: contoso.com, fabrikam.com ve wingtiptoys.com. Her şirket içi Active Directory etki alanındaki Hello kullanıcılar farklı bir ad kullanın.

Hello Azure AD Kiracı örnekleri arasında hiçbir GALSync yoktur. kullanıcılar aynı Kiracı hello yalnızca Exchange Online ve Skype iş gösterir için adres defteri hello.

Bu topoloji hello aşağıdaki sahip başka kısıtlamalar desteklenen senaryolar:

* Hello Azure AD kiracılar yalnızca bir Exchange karma hello şirket içi Active Directory örneğiyle etkinleştirebilirsiniz.
* Windows 10 cihazları tek bir Azure AD Kiracı ile ilişkilendirilebilir.
* Merhaba tek oturum açma (SSO) seçenek parola eşitleme ve geçişli kimlik doğrulaması için yalnızca bir Azure AD Kiracı ile kullanılabilir.

birbirini dışlayan bir nesneler kümesini Hello gereksinimini toowriteback de geçerlidir. Tek şirket içi yapılandırma varsayar çünkü geri yazma özelliklerinden bazıları bu topolojisi ile desteklenmez. Bu özellikler şunlardır:

* Grup geri yazma varsayılan yapılandırmaya sahip.
* Cihaz geri yazma.

### <a name="each-object-multiple-times-in-an-azure-ad-tenant"></a>Her nesne birden çok kez Azure AD kiracısı
![Tek bir ormanına ve birden çok Kiracı için desteklenmeyen topolojisi](./media/active-directory-aadconnect-topologies/SingleForestMultiDirectoryUnsupported.png) ![Tek bir ormanına ve birden çok bağlayıcı için desteklenmeyen topolojisi](./media/active-directory-aadconnect-topologies/SingleForestMultiConnectorsUnsupported.png)

Bu görevler desteklenmez:

* Eşitleme hello aynı kullanıcı toomultiple Azure AD kiracılar.
* Bir yapılandırma bir Azure AD Kiracı kullanıcılar başka bir Azure AD kiracısı ilgili kişi olarak görünmesini sağlayacak şekilde değişikliği yapın.
* Azure AD Connect eşitleme tooconnect toomultiple Azure AD kiracılar değiştirin.

### <a name="galsync-by-using-writeback"></a>Geri yazma kullanarak GALSync
![Birden çok orman ve üzerinde Azure AD odaklanan GALSync ile birden çok dizin için desteklenmeyen topolojisi](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync1Unsupported.png) ![Birden çok orman ve GALSync odaklanan ile birden çok dizin için desteklenmeyen topoloji üzerinde Active Directory şirket içi](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync2Unsupported.png)

Azure AD kiracılarıyla tasarım gereği yalıtılır. Bu görevler desteklenmez:

* Başka bir Azure AD kiracısı Azure AD Connect eşitleme tooread verilerini hello yapılandırmasını değiştirme.
* Kullanıcılar, Azure AD Connect eşitleme kullanarak kişiler tooanother şirket içi Active Directory örneği olarak dışarı aktarın.

### <a name="galsync-with-on-premises-sync-server"></a>Şirket içi eşitleme sunucusu ile GALSync
![Birden fazla ormanına ve birden çok dizin için topoloji GALSync](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync.png)

FIM 2010 veya MIM 2016 şirket içi toosync (üzerinden kullanıcılara GALSync) iki Exchange kuruluşlar arasında kullanabilirsiniz. Yabancı kullanıcıları/ilgili kişi olarak görünür hello diğer kuruluştaki bir kuruluştaki Hello kullanıcıların. Bu farklı şirket içi Active Directory örnekleri sonra kendi Azure AD kiracılar ile eşitlenebilir.

## <a name="next-steps"></a>Sonraki adımlar
tooinstall bu senaryoları için Azure AD Connect nasıl görürüm toolearn [Azure AD Connect özel yüklemesi](active-directory-aadconnect-get-started-custom.md).

Merhaba hakkında daha fazla bilgi [Azure AD Connect eşitleme](active-directory-aadconnectsync-whatis.md) yapılandırma.

Daha fazla bilgi edinmek [şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md).
