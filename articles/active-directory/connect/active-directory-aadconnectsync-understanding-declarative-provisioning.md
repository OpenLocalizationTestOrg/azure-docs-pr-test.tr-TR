---
title: "Azure AD Connect: Bildirim temelli hazırlama anlama | Microsoft Docs"
description: "Merhaba bildirim temelli hazırlama yapılandırma modeli Azure AD CONNECT'te açıklanmaktadır."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: cfbb870d-be7d-47b3-ba01-9e78121f0067
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: f11e078f0aafacf94d69f0726ae41629a8470336
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-declarative-provisioning"></a>Azure AD Connect eşitleme: bildirim temelli hazırlama anlama
Bu konuda, Azure AD CONNECT'te hello yapılandırma modeli açıklanmaktadır. bildirim temelli hazırlama Hello modeli adı verilir ve bir yapılandırma değişikliği kolayca toomake izin verir. Bu konuda açıklanan pek çok gelişmiş ve çoğu müşteri senaryoları için gerekli değildir.

## <a name="overview"></a>Genel Bakış
Bildirim temelli hazırlama bağlı kaynak dizinden gelen nesneleri işleme ve nasıl hello nesne ve özniteliklerin bir kaynak tooa hedeften dönüştürülmesi gereken belirler. Bir nesne eşitleme ardışık düzeninde işlenir ve hello ardışık düzen olduğu hello aynı için gelen ve giden kuralları. Bir gelen kuralı bağlayıcı alanı toohello meta veri ve giden kuralı hello meta veri deposu tooa bağlayıcı alanından.

![Eşitleme ardışık düzen](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/sync1.png)  

Merhaba ardışık düzen birkaç farklı modülü vardır. Her biri bir kavram nesne eşitleme olarak sorumludur.

![Eşitleme ardışık düzen](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/pipeline.png)  

* Kaynak, hello kaynak nesnesi
* [Kapsam](#scope), kapsamındaki tüm eşitleme kuralları bulur
* [Katılma](#join), bağlayıcı alanı ve meta veri deposu arasındaki ilişki belirler
* [Dönüştürme](#transform), nasıl öznitelikleri dönüştürülmüş hesaplar ve akış
* [Öncelik](#precedence), öznitelik Katkıları çakışan çözümler
* Hedef, hello hedef nesnesi

## <a name="scope"></a>Kapsam
Merhaba kapsam modülü bir nesne değerlendirmek ve kapsamda ve hello işleme dahil edilmesi gereken hello kuralları belirler. Merhaba nesnesinde Hello öznitelik değerlerini bağlı olarak farklı eşitleme kapsamında değerlendirilen toobe kurallardır. Örneğin, Exchange posta kutusu devre dışı bırakılmış bir kullanıcıyla bir posta etkin bir kullanıcıyla daha farklı kuralları vardır.  
![Kapsam](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/scope1.png)  

Merhaba Kapsam grupları ve yan tümceleri tanımlanır. Merhaba yan tümceleri içinde bir grubudur. Mantıksal AND bir gruptaki tüm yan tümceleri arasında kullanılır. Örneğin, (departman BT ve ülke = = Danimarka). Mantıksal OR grupları arasında kullanılır.

![Kapsam](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/scope2.png)  
Bu resmi Hello kapsamında kimler olarak (departman BT ve ülke = = Danimarka) veya (ülke İsveç =). Grup 1 veya 2 grubu değerlendirilen tootrue ise, ardından hello kapsamda kuralıdır.

Merhaba kapsam modül işlemleri aşağıdaki hello destekler.

| İşlem | Açıklama |
| --- | --- |
| EŞİTTİR, EŞİT DEĞİLDİR |Değer eşit toohello değeriyse hello özniteliğinde, veren bir dize karşılaştırın. Birden çok değerli öznitelikler için ISIN ve ISNOTIN bakın. |
| LESSTHAN, LESSTHAN_OR_EQUAL |Değer veren bir dize karşılaştırma satıcısı hello özniteliğinde hello değerin. |
| İÇEREN NOTCONTAINS |Değer bir yerde içindeki değeri hello özniteliğinde bulunabiliyorsa veren bir dize karşılaştırma. |
| STARTSWITH, NOTSTARTSWITH |Hello başına hello özniteliğinde hello değer, değer ise veren bir dize karşılaştırın. |
| ENDSWITH, NOTENDSWITH |Değer hello uçtaki hello özniteliğinde hello değerin ise veren bir dize karşılaştırma. |
| GREATERTHAN, GREATERTHAN_OR_EQUAL |Değer hello özniteliğinde hello değerin büyükse veren bir dize karşılaştırın. |
| ISNULL, ISNOTNULL |Merhaba özniteliği mevcut olup olmadığını değerlendirir hello nesnesinden. Merhaba özniteliği mevcut değil ve bu nedenle null, hello kural kapsamda olur. |
| ISIN, ISNOTIN |Merhaba değer tanımlı hello özniteliğinde mevcut olup olmadığını değerlendirir. Bu işlem hello birden çok değerli eşittir ve NOTEQUAL çeşididir. Hello özniteliği toobe birden çok değerli bir öznitelik olması ve hello öznitelik değerleri hiçbirinde hello değeri bulunabilir, hello kural kapsamda olur. |
| ISBITSET, ISNOTBITSET |Belirli bir biti ayarlanmışsa değerlendirir. Örneğin, bir kullanıcı etkinleştirilmiş veya devre dışı bırakılmışsa kullanılan tooevaluate userAccountControl toosee hello bit olabilir. |
| ISMEMBEROF, ISNOTMEMBEROF |Merhaba değeri hello bağlayıcı alanı DN tooa grubunda içermelidir. Merhaba nesne belirtilen hello grubunun bir üyesi ise, hello kapsamda kuralıdır. |

## <a name="join"></a>Birleştir
Merhaba birleştirme modülü hello eşitleme ardışık düzeninde hello kaynak hello nesnesinde ve bir nesne arasındaki ilişkiyi hello hello hedef bulmak için sorumludur. Bir gelen kuralı, bu ilişki hello meta veri deposunda bir ilişki tooan nesne bulma bağlayıcı alanı içindeki bir nesneyi olacaktır.  
![Mv ile cs arasında katılma](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join1.png)  
varsa bir nesne zaten başka bir bağlayıcı tarafından oluşturulan hello meta dizesinde hello hedef toosee, ile ilişkili. Örneğin, bir hesap-kaynak ormanı hello hello hesap ormanı kullanıcıdan hello kaynak ormandaki hello kullanıcıyla alanına eklenmelidir.

Birleştirmeler çoğunlukla gelen kuralları toojoin bağlayıcı alanı nesne birlikte toohello üzerinde kullanılan aynı meta veri deposu nesnesi.

Merhaba birleştirmeler bir veya daha fazla grupları olarak tanımlanır. Bir grup yan tümceleri sahip. Mantıksal AND bir gruptaki tüm yan tümceleri arasında kullanılır. Mantıksal OR grupları arasında kullanılır. Başlangıç gruplarını, üst toobottom ile sırada işlenir. Bir grubu hello hedef nesne ile tam olarak bir eşleşme buldu, diğer bir birleşim kuralları değerlendirilir. Sıfır veya bir nesne bulunandan daha fazla işleme toohello sonraki grubu kurallarının devam eder. Bu nedenle, hello kuralları hello sırasına göre en açık ilk ve hello sonunda daha belirsiz oluşturulmalıdır.  
![Tanımı katılma](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join2.png)  
Bu resmi Hello birleşimlerde üst toobottom işlenir. İlk hello eşitleme ardışık düzen EmployeeID bir eşleşme olup olmadığını görür. Aksi durumda, hello hesap adı kullanılan toojoin hello nesnelerin araya olabiliyorsa hello ikinci kural görür. Bu bir eşleşme ya da değilse, hello üçüncü ve son daha benzer eşleştirme hello kullanıcı adını kullanarak kuralıdır.

Tüm birleşim kuralları değerlendirilir ve tam bir eşleşme ise, hello **bağlantı türü** hello üzerinde **açıklama** sayfa kullanılır. Bu seçeneği çok ayarlarsanız**sağlama**, hello hedef yeni bir nesne oluşturulduktan sonra.  
![Sağlama veya birleştirme](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join3.png)  

Bir nesne, yalnızca birleştirme kurallarla bir tek eşitleme kuralı kapsamında olmalıdır. Varsa birden çok eşitleme kuralları birleştirme tanımlandığı, bir hata oluşur. Öncelik kullanılan tooresolve birleştirme çakışmaları değil. Bir nesne öznitelikleri tooflow hello ile kapsamında bir birleşim kuralına sahip olmalıdır aynı gelen/giden yön. Gelen ve giden toohello tooflow gerekiyorsa öznitelikleri aynı nesne, bir gelen ve giden eşitleme kuralı birleştirme ile olması gerekir.

Bir nesne tooa hedef bağlayıcı alanı tooprovision çalıştığında giden birleşim özel bir davranışı vardır. Merhaba DN, kullanılan toofirst deneyin Ters Birleştirme özniteliğidir. Zaten bir nesne içinde olmadığında hello hedef bağlayıcı alanı ile aynı DN, nesneleri katılan hello hello.

ne zaman yeni bir eşitleme kuralı kapsamına olduğunda hello birleştirme modülü yalnızca değerlendirilir. Bir nesne katıldı, hello birleştirme ölçütlerini artık karşılamadı olsa bile, ayrılma değil. Bir nesne toodisjoin istiyorsanız, hello nesneleri birleştirilmiş hello eşitleme kuralı kapsamının dışına gitmeniz gerekir.

### <a name="metaverse-delete"></a>Meta veri deposu Sil
Meta veri deposu nesne kapsamlı bir eşitleme kuralı olduğu kadar uzun kalır **bağlantı türü** çok ayarlamak**sağlama** veya **StickyJoin**. Bir bağlayıcı tooprovision yeni bir izin verilmiyor bir StickyJoin kullanıldığında toohello meta veri deposu nesnesi, ancak bunu katıldı, hello meta veri deposu nesnesi silinmeden önce hello kaynağında silinmesi gerekir.

Bir meta veri deposu nesnesi silindiğinde, bir giden eşitleme kuralı ile ilişkili tüm nesneler için işaretlenmiş **sağlama** silinmek üzere işaretlenmiş.

## <a name="transformations"></a>Dönüşümleri
Merhaba dönüşümleri öznitelikleri hello kaynak toohello hedeften nasıl gerçekleştiğini kullanılan toodefine ' dir. Merhaba akışları hello aşağıdakilerden biri olabilir **akış türleri**: doğrudan, sabit değer veya ifade. Doğrudan bir akış akar öznitelik değeri olarak-ile hiçbir ek dönüştürmeler değil. Bir sabit değer kümeleri hello değer belirtildi. Bir ifade hello dönüştürme nasıl olmalıdır hello bildirim temelli hazırlama ifade dil tooexpress kullanır. Merhaba ifade dili hello bulunabilir ayrıntıları Hello [bildirim temelli hazırlama ifade dili anlama](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) konu.

![Sağlama veya birleştirme](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/transformations1.png)  

Merhaba **bir kez Uygula** onay kutusunu tanımlar, hello özniteliği, yalnızca hello nesnesi ilk oluşturulduğunda ayarlanmalıdır. Örneğin, bu yapılandırma kullanılan tooset yeni bir kullanıcı nesnesi için bir başlangıç parolası olabilir.

### <a name="merging-attribute-values"></a>Öznitelik değerlerini birleştirme
Merhaba öznitelik akışları içinde olup olmadığını ayarı toodetermine birden çok değerli öznitelikleri birkaç farklı bağlayıcılardan birleştirilemez. Merhaba varsayılan değer **güncelleştirme**, en yüksek önceliğe sahip o hello eşitleme kuralı belirten win.

![Türleri birleştirme](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/mergetype.png)  

Ayrıca **birleştirme** ve **MergeCaseInsensitive**. Bu seçenekler toomerge değerlerinden farklı kaynaklar sağlar. Örneğin, birkaç farklı ormanlardaki kullanılan toomerge hello üyesi veya proxyAddresses öznitelik olabilir. Bu seçeneği kullandığınızda, bir nesne hello kullanmalıdır tüm kuralları kapsamında eşitleme aynı birleştirme türü. Tanımlayamazsınız **güncelleştirme** bir bağlayıcısından alınan ve **birleştirme** başka bir. Çalışırsanız, bir hata alırsınız.

Merhaba arasındaki farkı **birleştirme** ve **MergeCaseInsensitive** tooprocess yinelenen öznitelik değerleri nasıl olduğu. Merhaba eşitleme altyapısı yinelenen değerler hello target özniteliği eklenmiyor emin olur. İle **MergeCaseInsensitive**, toobe mevcut yapmayacağınız durumda yalnızca bir fark değerlerle yinelenen. Örneğin, her ikisi de görülmemelidir "SMTP:bob@contoso.com"ve"smtp:bob@contoso.com" Merhaba Hedef öznitelik. **Birleştirme** değerleri tam hello ve birden çok değer yalnızca arıyor yalnızca olması durumunda bir fark çalışması mevcut olabilir.

Merhaba seçeneği **Değiştir** olduğundan, hello aynı **güncelleştirme**, ancak değil kullanılır.

### <a name="control-hello-attribute-flow-process"></a>Denetim hello öznitelik akışı işlemi
Birden çok gelen eşitleme kuralı yapılandırılmış toocontribute toohello olduğunda aynı meta veri deposu özniteliği öncelik olduğundan kullanılan toodetermine hello kazanan. en yüksek öncelik (en düşük sayısal değer) ile Merhaba eşitleme kuralı toocontribute hello değerini geçiyor. Merhaba giden kuralları için aynı olur. en yüksek önceliğe sahip Hello eşitleme kuralı WINS ve hello değeri toohello bağlı dizin katkıda.

Bazı durumlarda, bir değer katkıda yerine hello eşitleme kuralı diğer kuralların nasıl hareket etmesi gerektiğini belirlemeniz gerekir. Bu örnekte kullanılan bazı özel değişmez değerler vardır.

Gelen eşitleme kuralları için değişmez değer hello **NULL** kullanılan tooindicate hello akış hiçbir değer toocontribute sahip olabilir. Daha düşük önceliğe sahip başka bir kural, bir değer katkıda bulunabilir. Hiçbir kural katkıda bulunan bir değer varsa, hello meta veri deposu özniteliği kaldırılır. Bir giden kuralı için **NULL** tüm eşitleme kuralları işlendikten sonra hello değer hello bağlı dizininde kaldırılır sonra hello son değerdir.

değişmez değer Hello **AuthoritativeNull** çok benzer**NULL** ancak hello arasındaki fark daha düşük bir öncelik kuralları bir değer katkıda bulunabilir.

Bir öznitelik akışı da kullanabilirsiniz **IgnoreThisFlow**. Merhaba herkese açık bir şey yok olduğuna benzer tooNULL olan toocontribute. Merhaba, zaten varolan bir değerle hello hedef kaldırmadığını farktır. Merhaba öznitelik akışı hiç var. olmamıştı gibidir.

Örnek aşağıda verilmiştir:

İçinde *tooAD - kullanıcı Exchange karma çıkışı* akış aşağıdaki hello bulunabilir:  
`IIF([cloudSOAExchMailbox] = True,[cloudMSExchSafeSendersHash],IgnoreThisFlow)`  
Bu ifade olarak okumalısınız: hello kullanıcı posta kutusuna Azure AD içinde yer alıyorsa, Azure AD tooAD hello özniteliğinden akış. Herhangi bir şey geri tooActive dizin akan değilse. Bu durumda, onu hello mevcut değeri AD içinde tutmak.

### <a name="importedvalue"></a>ImportedValue
Merhaba işlevi ImportedValue diğer işlevleri farklı olduğu Hello öznitelik adı köşeli ayraç yerine tırnak içine alınması gerekir:  
`ImportedValue("proxyAddresses")`.

Genellikle eşitleme sırasında hello beklenen değer ("üst") hello kule, dışa aktarma sırasında bir hata alındı veya henüz dışarı kurmadı olsa bile bir özniteliğini kullanır. Gelen eşitleme henüz bağlı bir dizin sonunda üst sınırına kurmadı bir öznitelik bu ulaştığında varsayar. Bazı durumlarda, tooonly eşitleme hello bağlı dizin ("hologramı ve delta kule alma") tarafından onaylanan bir değer önemlidir.

Bu işlev örneği hello out-of-box içinde bulunabilir eşitleme kuralı *içinde AD'den – kullanıcı ortak Exchange'den*. Merhaba değeri başarıyla dışarı aktarıldı onaylandıktan olduğunda karma Exchange'de çevrimiçi Exchange tarafından eklenen hello değeri yalnızca eşitlenmesi gereken:  
`proxyAddresses` <- `RemoveDuplicates(Trim(ImportedValue("proxyAddresses")))`

## <a name="precedence"></a>Önceliği
Birkaç eşitleme kuralları çalıştığınızda toocontribute aynı öznitelik değeri toohello hedef Merhaba, hello öncelik değeri kullanılan toodetermine hello kazanır. en yüksek öncelik, en düşük sayısal değer Hello kuralıyla bir çakışma toocontribute hello özniteliğinde geçiyor.

![Türleri birleştirme](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/precedence1.png)  

Bu sıralama kullanılan toodefine daha kesin olabilir öznitelik akışları küçük bir alt nesne için. Örneğin, hello çıkış-in-kutusu-kuralları etkinleştirilmiş bir hesaptan öznitelikleri emin olun (**kullanıcı AccountEnabled**) diğer hesaplarından önceliğe sahiptir.

Öncelik arasında bağlayıcılar tanımlanabilir. Bağlayıcılar daha iyi veri toocontribute değerlerle ilk sağlar.

### <a name="multiple-objects-from-hello-same-connector-space"></a>Birden çok nesneden aynı bağlayıcı alanı hello
Birden fazla nesneniz varsa hello aynı bağlayıcı alanı birleştirilmiş toohello aynı meta veri deposu nesnesi, öncelik ayarlanmış. Bazı nesneler kapsamında olması durumunda hello aynı kural eşitleme sonra hello eşitleme altyapısı mümkün toodetermine öncelik değil. Hangi kaynak nesnesi hello değeri toohello meta veri deposu katkıda bulunmalıdır, belirsiz. Merhaba kaynak Hello öznitelikleri hello olsa bile bu yapılandırmayı belirsiz olarak bildirilen aynı değeri.  
![Birden çok nesne toohello birleştirilmiş aynı mv nesnesi](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/multiple1.png)  

Merhaba kaynak nesneleri farklı eşitleme kuralları kapsamında olması için bu senaryo için toochange hello hello eşitleme kuralların kapsamını olması gerekir. Toodefine farklı öncelik verir.  
![Birden çok nesne toohello birleştirilmiş aynı mv nesnesi](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/multiple2.png)  

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba ifade dili hakkında daha fazla bilgiyi [anlama bildirim temelli hazırlama ifadelerini](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md).
* Bkz: nasıl bildirim temelli sağlama kullanılan out-of-box içinde olduğu [anlama hello varsayılan yapılandırma](active-directory-aadconnectsync-understanding-default-configuration.md).
* Toomake bir pratik nasıl değiştiğini içinde bildirim temelli hazırlama kullanarak görmek [nasıl toomake değişiklik toohello varsayılan yapılandırması](active-directory-aadconnectsync-change-the-configuration.md).
* Kullanıcıları ve kişileri nasıl birlikte içinde tooread devam [kullanıcıları ve kişileri anlama](active-directory-aadconnectsync-understanding-users-and-contacts.md).

**Genel bakış konuları**

* [Azure AD Connect eşitleme: anlamak ve eşitleme özelleştirme](active-directory-aadconnectsync-whatis.md)
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)

**Başvuru konuları**

* [Azure AD Connect eşitleme: işlevleri başvurusu](active-directory-aadconnectsync-functions-reference.md)
