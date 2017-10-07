---
title: "Azure AD Connect eşitleme: Kullanıcıları ve kişileri anlama | Microsoft Docs"
description: "Kullanıcılar ve kişiler Azure AD Connect Eşitleme'de açıklanmaktadır."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8d204647-213a-4519-bd62-49563c421602
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi;andkjell
ms.openlocfilehash: 4d80648c53a2981eb2626338913ed2282423f183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-users-and-contacts"></a>Azure AD Connect Eşitleme: Kullanıcıları ve Kişileri Anlama
Neden birden çok Active Directory ormanına gerekir ve birçok farklı dağıtım topolojileri vardır birkaç farklı nedenleri vardır. Ortak modelleri birleşme & edinme sonra bir hesap-kaynak dağıtımı ve GAL sync'ed ormanları içerir. Ancak karma modeller de olsa bile saf modelleri, yaygındır. Azure AD Connect eşitleme Hello Varsayılan yapılandırmada herhangi belirli bir modeli varsaymaz ancak nasıl kullanıcı eşleştirme hello Yükleme Kılavuzu'nda seçilen bağlı olarak, farklı davranışlar gösterilebilir.

Bu konuda, hello varsayılan yapılandırması bazı topolojide nasıl davranacağını aracılığıyla ele alacağız. Merhaba yapılandırma aracılığıyla ele alacağız ve eşitleme kuralları Düzenleyicisi hello hello yapılandırma sırasında kullanılan toolook olabilir.

Merhaba yapılandırma varsayar birkaç genel kurallar şunlardır:

* Biz etkin dizinleri hello kaynağından almak sıra bağımsız olarak, hello sonuç her zaman olması hello aynı.
* Etkin bir hesap oturum açma bilgileri, her zaman katkıda dahil olmak üzere **userPrincipalName** ve **sourceAnchor**.
* Bulunan hiçbir active hesabı toobe ise bağlı bir posta kutusu olmadığı sürece devre dışı bırakılmış bir hesaba userPrincipalName ve sourceAnchor, katkıda bulunur.
* Bağlantılı bir posta kutusuna sahip bir hesap hiçbir zaman userPrincipalName ve sourceAnchor için kullanılır. Etkin bir hesabı daha sonra bulunamadı varsayılır.
* Bir kişi nesnesi, bir kişi veya bir kullanıcı olarak sağlanan tooAzure AD olabilir. Tüm kaynak Active Directory ormanları işlenen kadar gerçekten tanımadığınız.

## <a name="contacts"></a>Kişiler
Farklı bir ormanda bir kullanıcıyı temsil eden kişiler sahip bir birleşme & edinme sonra GALSync çözüm iki veya daha fazla ormanlarında Exchange burada köprüleme yaygındır. Merhaba kişi nesnesi, her zaman hello posta özniteliği kullanılarak hello bağlayıcı alanı toohello meta veri deposu katılıyor. Zaten varsa bir kişi nesnesi veya kullanıcı nesnesi hello ile aynı Adres posta, hello nesneleri birleştirilir. Bu hello kuralında yapılandırılmış **içinde AD'den – kişi katılma**. Adlı bir kural bulunmaktadır **içinde AD'den – kişi ortak** bir öznitelik akışı toohello meta veri deposu özniteliği olan **sourceObjectType** hello sabiti ile **kişi**. Bu kural çok düşük önceliğe sahip bunu herhangi bir kullanıcı nesnesi birleştirilmiş toohello ise aynı meta veri deposu nesne sonra hello kural **içinde AD'den – kullanıcı ortak** hello değeri kullanıcı toothis özniteliği katkıda bulunur. Bu kural, bu öznitelik hiçbir kullanıcı birleştirdiğinizde başvurun ve en az bir kullanıcı bulunamazsa, kullanıcı değeri hello hello değerine sahip olacaktır.

Bir nesne tooAzure AD sağlamak için giden kuralı hello **tooAAD – başvurun katılma çıkışı** Merhaba, bir kişi nesnesi oluşturacak meta veri deposu özniteliği **sourceObjectType** çok ayarlanır**başvurun** . Bu öznitelik çok ayarlanırsa**kullanıcı**, ardından hello kural **tooAAD – kullanıcı katılma çıkışı** bunun yerine bir kullanıcı nesnesi oluşturacak.
Daha fazla kaynak etkin dizinler aktarılması ve eşitlenmiş bir nesnenin kişi tooUser yükseltilir mümkündür.

Biz hello ilk ormanı içeri aktardığınızda Örneğin, bir GALSync topolojisinde biz kişi nesneleri herkes için hello ikinci ormanda bulur. Bu yeni iletişim nesneler hello AAD bağlayıcı aşama. Biz daha sonra almak ve hello ikinci ormanın eşitlemek, biz hello gerçek kullanıcıları bulmak ve toohello var olan meta veri deposu nesneleri ekleyin. Biz ardından hello kişi nesnesi, AAD silin ve yeni bir kullanıcı nesnesi oluşturun.

Kullanıcılar, kişiler olarak burada sunulur bir topoloji varsa, hello Yükleme Kılavuzu'nda toomatch kullanıcıları hello posta özniteliği seçtiğinizden emin olun. Başka bir seçeneği belirlerseniz, bir siparişi bağımlı yapılandırmaya sahip olur. Kişi nesneler her zaman hello posta özniteliği katılacak ancak hello Yükleme Kılavuzu'nda bu seçenek seçildiyse kullanıcı nesneleri yalnızca hello posta özniteliği katılın. Ardından hello meta veri deposu hello ile iki farklı nesneleri aynı şunun hello kişi nesnesi hello kullanıcı nesnesi önce aldıysanız posta özniteliği. Dışarı aktarma tooAzure AD sırasında bir hata oluşturulur. Bu davranış tasarım gereğidir ve hatalı veri gösterir ya da bu hello topoloji hello yükleme sırasında doğru tanımlanmadı.

## <a name="disabled-accounts"></a>Devre dışı bırakılan hesapları
Devre dışı bırakılan hesapları da tooAzure AD eşitlenir. Exchange, örneğin konferans odaları ortak toorepresent kaynakları devre dışı hesaplarıdır. Merhaba, bağlı bir posta kutusu kullanıcılarla istisnadır; daha önce belirtildiği gibi bunlar hiç bir hesap tooAzure AD hazırlayacağınız.

Merhaba, devre dışı bırakılmış kullanıcı hesabı bulunamadı, daha sonra başka bir etkin hesabı sizi bir sonraki bulamaz hello nesnesi hello userPrincipalName ve bulunan sourceAnchor ile sağlanan tooAzure AD ise varsayılır. Durumda başka bir etkin hesabı, ardından userPrincipalName ve sourceAnchor aynı meta veri deposu nesnesi kullanılacak toohello katılır.

## <a name="changing-sourceanchor"></a>SourceAnchor değiştirme
Bir nesne verildiğinde tooAzure AD sonra onu değil izin verilen toochange hello sourceAnchor artık. Merhaba nesne dışarı aktarılan hello meta veri deposu özniteliği süredir zaman **cloudSourceAnchor** hello ile ayarlanır **sourceAnchor** Azure AD tarafından kabul edilen değer. Varsa **sourceAnchor** değiştirilir ve eşleşmiyor **cloudSourceAnchor**, hello kural **tooAAD – kullanıcı katılma çıkışı** hello hata atar **sourceAnchor özniteliği değişti**. Bu durumda, hello yapılandırma veya veri düzeltilmesi gerekir böylece aynı hello sourceAnchor hello nesnesi yeniden eşitlenebilmesi yeniden hello meta veri deposunda mevcut.

## <a name="additional-resources"></a>Ek Kaynaklar
* [Azure AD Connect eşitleme: Eşitleme seçeneklerini özelleştirme](active-directory-aadconnectsync-whatis.md)
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)

