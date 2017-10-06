---
title: "Azure AD Connect: Eşitleme sırasında sorun giderme | Microsoft Docs"
description: "Azure AD Connect ile eşitleme sırasında nasıl tootroubleshoot hatalarla karşılaştı açıklanmaktadır."
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 2209d5ce-0a64-447b-be3a-6f06d47995f8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: af262dfe95d686e34697454c0dfe8b4a6d8693c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-errors-during-synchronization"></a>Eşitleme sırasında sorun giderme
Windows Server Active Directory (AD DS) tooAzure Active Directory (Azure AD) kimlik verilerini eşitlendiğinde hataları oluşabilir. Bu makalede, farklı türdeki eşitleme hatalar, bu hataları ve olası yolları toofix hello hatalarına neden hello olası senaryolardan bazıları genel bakış sağlar. Bu makalede hello karşılaşılan hata içerir ve tüm hello olası hatalar kapak değil.

 Bu makalede hello okuyucu hello temel ile hakkında bilgi sahibi olduğunu varsayar [tasarım kavramları Azure AD ve Azure AD Connect](active-directory-aadconnect-design-concepts.md).

Azure AD Connect'in en son sürümünü hello ile \(Ağustos 2016 veya daha yüksek\), eşitleme hatalarını raporunu hello kullanılabilir [Azure Portal](https://aka.ms/aadconnecthealth) Azure AD Connect Health eşitleme için bir parçası olarak.

1 Eylül 2016'dan başlayarak [Azure Active Directory yinelenen öznitelik dayanıklılık](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) özellik, varsayılan olarak tüm hello için etkinleştirilecek *yeni* Azure Active Directory kiracılar. Bu özellik, hello gelecek aylarda var olan kiracılar için otomatik olarak etkinleştirilir.

Azure AD Connect eşitleme sürdürür hello dizinlerden 3 tür işlemler gerçekleştiren: alma, eşitleme ve dışarı aktarma. Tüm hello işlemlerinde hatalar gerçekleşebilir. Bu makalede, verme tooAzure AD sırasında hataları çoğunlukla ele alınmaktadır.

## <a name="errors-during-export-tooazure-ad"></a>Dışarı aktarma tooAzure AD sırasında hatalar
Bölümden farklı türleri açıklanmaktadır eşitlenmesi hello verme işlemi tooAzure AD kullanılarak sırasında oluşan hataları Azure AD Bağlayıcısı hello. Bu bağlayıcı "contoso. olan hello adı biçimi tarafından belirlenebilir. *onmicrosoft.com*".
Dışarı aktarma tooAzure AD sırasında hatalar belirtmek bu hello işlemi \(Ekle, Güncelleştir, Sil vb.\) Azure AD Connect tarafından çalıştı \(eşitleme altyapısı\) Azure Active Directory'ye başarısız oldu.

![Dışarı Aktarma hataları genel bakış](./media/active-directory-aadconnect-troubleshoot-sync-errors/Export_Errors_Overview_01.png)

## <a name="data-mismatch-errors"></a>Veri uyuşmazlığı hataları
### <a name="invalidsoftmatch"></a>InvalidSoftMatch
#### <a name="description"></a>Açıklama
* Ne zaman Azure AD Connect \(eşitleme altyapısı\) Azure Active Directory tooadd veya güncelleştirme nesneleri, Azure AD bildirir eşleşmeleri hello hello kullanarak gelen nesnesi **sourceAnchor** toohello özniteliği  **İmmutableıd** Azure AD'de nesnelerin öznitelik. Bu eşleşme olarak adlandırılan bir **sabit eşleşen**.
* Zaman Azure AD **bulamadı** hello eşleşen herhangi bir nesne **İmmutableıd** hello özniteliğiyle **sourceAnchor** sağlamadan önce gelen nesnesinin Merhaba, özniteliği bir Yeni nesne, toouse hello ProxyAddresses geri döner ve UserPrincipalName öznitelikleri toofind bir eşleşme. Bu eşleşme olarak adlandırılan bir **yumuşak eşleşen**. Merhaba yumuşak eşleşme tasarlanmış toomatch nesneleri (yani Azure AD'de elde edilir) Azure AD içinde zaten mevcut nesnelerle hello temsil eden eşitleme sırasında eklenen/güncellenen olan hello yeni olan şirket içi aynı varlık (kullanıcılar, gruplar).
* **InvalidSoftMatch** hata oluşuyor hello sabit eşleşme eşleşen hiçbir nesne bulamadı **ve** yumuşak eşleşme eşleşen bir nesne bulur, ancak bu nesne farklı değerine sahip *İmmutableıd* gelen nesnenin hello daha *SourceAnchor*, nesne eşleşen bu hello öneren eşitlenmiş başka bir nesneden şirket içi Active Directory ile.

Diğer bir deyişle, hello yumuşak eşleşme toowork için sırayla soft-eşleşen ile Merhaba nesne toobe hello için herhangi bir değer olmamalıdır *İmmutableıd*. Herhangi bir nesnesi ile varsa *İmmutableıd* bir değer kümesiyle hello eşleşme sabit ancak çağıran hello yumuşak eşleşme ölçütlerini başarısız, hello işlemi InvalidSoftMatch eşitleme hatayla sonuçlanacak.

Şema toohave hello aşağıdaki hello aynı değerini iki veya daha fazla nesne izin verme Azure Active Directory öznitelikleri. \(Bu kapsamlı bir liste değildir.\)

* ProxyAddresses
* userPrincipalName
* onPremisesSecurityIdentifier
* objectID

> [!NOTE]
> [Azure AD özniteliği yinelenen öznitelik dayanıklılık](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) özelliği ayrıca alınıyor Azure Active Directory hello varsayılan davranış olarak.  Azure AD daha esnektir, yinelenen ProxyAddresses ve UserPrincipalName öznitelikleri mevcut şirket içi AD işleme hello şekilde yaparak bu hello Azure AD Connect (yanı sıra diğer eşitleme istemciler) görülen eşitleme hatalarının sayısını azaltır ortamlar. Bu özellik hello çoğaltma hataları düzeltmez. Bu nedenle hello veri hala sabit toobe gerekiyor. Ancak Azure AD'de tooduplicated değerleri sağlanan Aksi takdirde engellenir yeni nesnelerin sağlanmasına olanak tanır. Bu ayrıca toohello eşitleme istemci döndürülen Eşitleme hataları hello sayısını azaltır.
> Bu özellik Kiracınız için etkinleştirilirse, yeni nesnelerin sağlama sırasında görülen hello InvalidSoftMatch eşitleme hatalarını görmezsiniz.
>
>

#### <a name="example-scenarios-for-invalidsoftmatch"></a>InvalidSoftMatch için örnek senaryolar
1. İki veya daha fazla şirket içinde Active Directory ProxyAddresses özniteliğinin aynı değeri bulunmaktadır hello nesneleriyle. Tek bir Azure AD içinde sağlanır.
2. İki veya daha fazla şirket içinde Active Directory userPrincipalName aynı değeri bulunmaktadır hello nesneleriyle. Tek bir Azure AD içinde sağlanır.
3. Bir nesne hello şirket içi Active Directory hello ile aynı eklendi, Azure Active Directory'de mevcut nesnesinin olarak ProxyAddresses özniteliğinin değeri. Şirket içinde eklenen hello nesne Azure Active Directory'de sağlanmamış.
4. Bir nesne ile şirket içi Active Directory hello ile aynı eklenmiştir, Azure Active Directory'de bir hesap olarak userPrincipalName özniteliğinin değeri. Merhaba nesne Azure Active Directory'de sağlanmamış.
5. Eşitlenen bir hesabı B. Azure AD Connect (eşitleme altyapısı) objectGUID özniteliği toocompute hello SourceAnchor kullanarak orman A tooForest taşındı. Merhaba orman taşıma sonrasında hello SourceAnchor hello değerini farklıdır. Merhaba yeni nesnesinden (orman B) Azure AD içinde toosync hello varolan nesne ile başarısız oluyor.
6. Eşitlenen nesne yanlışlıkla uygulamasından şirket içinde Active Directory silinen ve yeni bir nesne Active Directory'de Merhaba aynı oluşturuldu Azure Active Directory'de hello hesabı silme olmadan varlık (örneğin, kullanıcı). Merhaba yeni hesabı toosync hello nesnelerinden Azure AD ile başarısız olur.
7. Azure AD Connect kaldırılır ve yeniden yüklendi. Merhaba yeniden yükleme sırasında farklı bir öznitelik SourceAnchor hello seçildi. Önceden eşitlenmiş tüm hello nesneleri InvalidSoftMatch hata ile eşitleniyor durduruldu.

#### <a name="example-case"></a>Örnek durum:
1. **Bob Smith** eşitlenen kullanıcının Azure Active Directory'de üzerinde şirket içi Active Directory olduğu *contoso.com*
2. Bob Smith'in **UserPrincipalName** olarak ayarlanmış olan  **bobs@contoso.com** .
3. **"abcdefghijklmnopqrstuv =="** hello olan **SourceAnchor** Bob Smith'in kullanarak Azure AD Connect tarafından hesaplanan **objectGUID** gelen Active Directory, şirket içinde olduğu hello **İmmutableıd** Azure Active Directory'de Bob Smith için.
4. Bob de sahip hello için değerleri aşağıdaki **proxyAddresses** özniteliği:
   * smtp:bobs@contoso.com
   * smtp:bob.smith@contoso.com
   * **smtp:bob@contoso.com**
5. Yeni bir kullanıcı **Bob Taylor**, şirket içinde Active Directory toohello eklenir.
6. Bob Taylor'ın **UserPrincipalName** olarak ayarlanmış olan  **bobt@contoso.com** .
7. **"abcdefghijkl0123456789 ==" "** hello olan **sourceAnchor** Bob Taylor'ın kullanarak Azure AD Connect tarafından hesaplanan **objectGUID** gelen üzerinde Active Directory şirket içi. Bob Taylor'ın nesne tooAzure Active Directory henüz eşitlenmedi.
8. Bob Taylor hello proxyAddresses özniteliği için değerleri aşağıdaki hello sahip
   * smtp:bobt@contoso.com
   * smtp:bob.taylor@contoso.com
   * **smtp:bob@contoso.com**
9. Eşitleme sırasında Azure AD Connect şirket içi Active Directory içinde Bob Taylor hello eklenmesi algılar ve Azure isteyin AD toomake hello aynı değiştirin.
10. Azure AD ilk sabit eşleşme gerçekleştirir. Diğer bir deyişle, yoksa herhangi bir nesne hello İmmutableıd ile eşit çok arayacaktır "abcdefghijkl0123456789 ==". Azure AD'de başka bir nesneyi o İmmutableıd olacağından sabit eşleşme başarısız olur.
11. Azure AD toosoft-match sonra deneyecek Bob Taylor. Dahil olmak üzere üç değerden proxyAddresses eşit toohello ile herhangi bir nesne ise başka bir deyişle, ararsmtp:bob@contoso.com
12. Azure AD Bob Smith'in nesne toomatch hello yumuşak eşleşme ölçütlerini bulur. Ancak bu nesne İmmutableıd hello değerine sahip = "abcdefghijklmnopqrstuv ==". Bu nesne belirten nesnesinden başka bir şirket içi Active Directory eşitlenen. Bu nedenle, Azure AD yumuşak bu nesneler ve sonuçları eşleştirme olamaz bir **InvalidSoftMatch** eşitleme hatası.

#### <a name="how-toofix-invalidsoftmatch-error"></a>Nasıl toofix InvalidSoftMatch hata
Merhaba hello InvalidSoftMatch hata en yaygın nedeni olan iki farklı SourceAnchor nesneleriyle \(İmmutableıd\) hello sırasında kullanılan hello ProxyAddresses ve/veya UserPrincipalName öznitelikleri için aynı değeri hello sahip soft-işlem üzerinde Azure AD eşleşmiyor. Sipariş toofix hello geçersiz yazılım eşleştirme

1. Yinelenen hello proxyAddresses, userPrincipalName veya hello hataya neden olan başka bir öznitelik değer belirleyin. Ayrıca, iki tanımlamak \(veya daha fazla\) nesneleri söz konusu hello çakışıyor. Merhaba tarafından oluşturulan rapor [Azure AD Connect Health eşitleme](https://aka.ms/aadchsyncerrors) hello iki nesneleri belirlemenize yardımcı olabilir.
2. Hangi nesne toohave hello yinelenen değer devam etmesi gerektiğini ve hangi nesne vermemelisiniz belirleyin.
3. Yinelenen hello değeri bu değere sahip olmaması gereken hello nesnesinden kaldırın. Gelen hello nesne burada kaynaklanan hello dizininde değiştirmek hello yapmak unutmayın. Bazı durumlarda, çakışan hello nesnelerden birini toodelete gerekebilir.
4. Şirket içi AD hello değiştirmek hello yaptıysanız, Azure AD Connect eşitleme hello değiştirmek olanak tanır.

Eşitleme hata raporu içinde Azure AD Connect Health eşitleme için 30 dakikada bir güncellenir ve hello en son eşitleme girişimi hello hatalarını içeren unutmayın.

> [!NOTE]
> İmmutableıd, hello yaşam süresi hello nesnesinin tanımı tarafından değiştirmemelisiniz. Azure AD Connect ile Merhaba listesinin gelen aklınızda hello senaryolardan bazıları yapılandırılmadıysa, burada Azure AD Connect hesaplar hello SourceAnchor temsil aynı varlık hello hello AD nesne için farklı bir değer durumda şunun (aynı kullanıcı / grup/kişisi vb.) Azure AD toocontinue kullanarak istediğiniz var olan bir nesne içeriyor.
>
>

#### <a name="related-articles"></a>İlgili makaleler
* [Office 365'te dizin eşitleme yinelenen ya da geçersiz öznitelikler engelle](https://support.microsoft.com/en-us/kb/2647098)

### <a name="objecttypemismatch"></a>ObjectTypeMismatch
#### <a name="description"></a>Açıklama
Azure AD toosoft eşleşme iki nesne çalıştığında, farklı iki nesnelerin "nesne türü," (gibi kullanıcı, Grup, ilgili kişi vb.) mümkündür tooperform hello yumuşak eşleşme kullanılan hello öznitelikler için değerlerini aynı hello sahip. Çoğaltma bu özniteliklerin Azure AD içinde izin verilmiyor gibi hello işlemi "ObjectTypeMismatch" eşitleme hatası neden olabilir.

#### <a name="example-scenarios-for-objecttypemismatch-error"></a>ObjectTypeMismatch hata için örnek senaryolar
* Office 365'te posta etkin güvenlik grubu oluşturulur. Yönetici, yeni bir kullanıcı veya kişi ekler (yani tooAzure AD henüz eşitlemedi) yerinde AD ile aynı değer olarak, Office 365 hello hello ProxyAddresses özniteliği için hello gruplandırma.

#### <a name="example-case"></a>Örnek durumu
1. Yönetici hello vergi departmanı için Office 365'te yeni bir posta etkin güvenlik grubu oluşturur ve bir e-posta adresi olarak sağlar tax@contoso.com. Bu hello ProxyAddresses özniteliği bu grup, hello değeriyle atar**smtp:tax@contoso.com**
2. Yeni bir kullanıcı Contoso.com ve şirket içi hello proxyAddress ile Merhaba kullanıcı için bir hesap oluşturulur**smtp:tax@contoso.com**
3. Azure AD Connect hello yeni kullanıcı hesabı eşitlenecek zaman hello "ObjectTypeMismatch" hata iletisi alır.

#### <a name="how-toofix-objecttypemismatch-error"></a>Nasıl toofix ObjectTypeMismatch hata
hello ObjectTypeMismatch hatanın en yaygın nedeni Hello (kullanıcı, Grup, ilgili kişi vb.) farklı türde iki nesne aynı hello ProxyAddresses özniteliği için değer hello sahip olabilir. Sipariş toofix hello ObjectTypeMismatch:

1. Yinelenen hello tanımlamak proxyAddresses (veya başka bir öznitelik) değeri bu neden hello hata. Ayrıca, iki tanımlamak \(veya daha fazla\) nesneleri söz konusu hello çakışıyor. Merhaba tarafından oluşturulan rapor [Azure AD Connect Health eşitleme](https://aka.ms/aadchsyncerrors) hello iki nesneleri belirlemenize yardımcı olabilir.
2. Hangi nesne toohave hello yinelenen değer devam etmesi gerektiğini ve hangi nesne vermemelisiniz belirleyin.
3. Yinelenen hello değeri bu değere sahip olmaması gereken hello nesnesinden kaldırın. Gelen hello nesne burada kaynaklanan hello dizininde değiştirmek hello yapmak unutmayın. Bazı durumlarda, çakışan hello nesnelerden birini toodelete gerekebilir.
4. Şirket içi AD hello değiştirmek hello yaptıysanız, Azure AD Connect eşitleme hello değiştirmek olanak tanır. Eşitleme hata raporu içinde Azure AD Connect Health eşitleme için 30 dakikada bir güncelleştirilir ve hello en son eşitleme girişimi hello hataları içerir.

## <a name="duplicate-attributes"></a>Yinelenen öznitelikler
### <a name="attributevaluemustbeunique"></a>AttributeValueMustBeUnique
#### <a name="description"></a>Açıklama
Şema toohave hello aşağıdaki hello aynı değerini iki veya daha fazla nesne izin verme Azure Active Directory öznitelikleri. Her Azure AD zorlanmış toohave anda bu özniteliklerin benzersiz bir değer nesnesidir olmasıdır.

* ProxyAddresses
* userPrincipalName

Azure AD Connect tooadd yeni bir nesne çalışır veya varolan bir nesne öznitelikleri yukarıda tooanother nesne Azure Active Directory'de zaten atanmış hello için bir değer güncelleştirmek, hello işlemi hello "AttributeValueMustBeUnique" eşitleme hatası oluşur.

#### <a name="possible-scenarios"></a>Olası senaryolar:
1. Yinelenen değer eşitlenmiş başka bir nesneyle çakışıyor atanan tooan zaten eşitlenmiş nesnesidir.

#### <a name="example-case"></a>Örnek durum:
1. **Bob Smith** eşitlenen kullanıcının Azure Active Directory'de üzerinde şirket içi Active Directory contoso.com olan
2. Bob Smith'in **UserPrincipalName** şirket içinde olarak ayarlanmış olan  **bobs@contoso.com** .
3. Bob de sahip hello için değerleri aşağıdaki **proxyAddresses** özniteliği:
   * smtp:bobs@contoso.com
   * smtp:bob.smith@contoso.com
   * **smtp:bob@contoso.com**
4. Yeni bir kullanıcı **Bob Taylor**, şirket içinde Active Directory toohello eklenir.
5. Bob Taylor'ın **UserPrincipalName** olarak ayarlanmış olan  **bobt@contoso.com** .
6. **Bob Taylor** hello için değerleri aşağıdaki hello sahip **ProxyAddresses** özniteliği i. smtp:bobt@contoso.comII. smtp:bob.taylor@contoso.com
7. Bob Taylor'ın nesnesi başarıyla Azure AD ile eşitlenir.
8. Yönetici karar tooupdate Bob Taylor'ın **ProxyAddresses** aşağıdaki değeri hello özniteliğiyle: ediyorum. **smtp:bob@contoso.com**
9. Azure AD ile Merhaba değerin üzerinde Azure AD'de tooupdate Bob Taylor'ın nesne deneyecek, ancak ProxyAddresses değeri tooBob Smith, zaten atanmış işlemi olarak yapamaz oluşan "AttributeValueMustBeUnique" hata.

#### <a name="how-toofix-attributevaluemustbeunique-error"></a>Nasıl toofix AttributeValueMustBeUnique hata
Merhaba hello AttributeValueMustBeUnique hata en yaygın nedeni olan iki farklı SourceAnchor nesneleriyle \(İmmutableıd\) hello ProxyAddresses ve/veya UserPrincipalName öznitelikleri için aynı değeri hello sahip. Sipariş toofix AttributeValueMustBeUnique hata

1. Yinelenen hello proxyAddresses, userPrincipalName veya hello hataya neden olan başka bir öznitelik değer belirleyin. Ayrıca, iki tanımlamak \(veya daha fazla\) nesneleri söz konusu hello çakışıyor. Merhaba tarafından oluşturulan rapor [Azure AD Connect Health eşitleme](https://aka.ms/aadchsyncerrors) hello iki nesneleri belirlemenize yardımcı olabilir.
2. Hangi nesne toohave hello yinelenen değer devam etmesi gerektiğini ve hangi nesne vermemelisiniz belirleyin.
3. Yinelenen hello değeri bu değere sahip olmaması gereken hello nesnesinden kaldırın. Gelen hello nesne burada kaynaklanan hello dizininde değiştirmek hello yapmak unutmayın. Bazı durumlarda, çakışan hello nesnelerden birini toodelete gerekebilir.
4. Şirket içi AD hello değiştirmek hello yaptıysanız, Azure AD Connect eşitleme hello sabit hello hata tooget için değiştirme olanak tanır.

#### <a name="related-articles"></a>İlgili makaleler
-[Office 365'te dizin eşitleme yinelenen ya da geçersiz öznitelikler engelle](https://support.microsoft.com/en-us/kb/2647098)

## <a name="data-validation-failures"></a>Veri doğrulama hataları
### <a name="identitydatavalidationfailed"></a>IdentityDataValidationFailed
#### <a name="description"></a>Açıklama
Azure Active Directory hello Directory'ye yazılır, veri toobe izin vermeden önce hello verilerin kendisi çeşitli kısıtlamalar zorlar. Son kullanıcılar bu veriler üzerinde bağlı hello uygulamalar kullanırken hello en iyi olası deneyimleri elde tooensure budur.

#### <a name="scenarios"></a>Senaryolar
a. Merhaba UserPrincipalName öznitelik değeri geçersiz karakterler içeriyor.
b. Merhaba UserPrincipalName özniteliği hello gerekli biçime izlemez.

#### <a name="how-toofix-identitydatavalidationfailed-error"></a>Nasıl toofix IdentityDataValidationFailed hata
a. Bu hello userPrincipalName özniteliği karakterler ve gerekli biçime desteklenen olduğundan emin olun.

#### <a name="related-articles"></a>İlgili makaleler
* [Dizin eşitleme tooOffice 365 tooprovision kullanıcılara hazırlama](https://support.office.com/en-us/article/Prepare-to-provision-users-through-directory-synchronization-to-Office-365-01920974-9e6f-4331-a370-13aea4e82b3e)

### <a name="federateddomainchangeerror"></a>FederatedDomainChangeError
#### <a name="description"></a>Açıklama
Bu sonuçlanan, belirli bir durumdur bir **"FederatedDomainChangeError"** kullanıcının UserPrincipalName hello soneki bir Federasyon etki alanını tooanother Federasyon etki alanından diğerine değiştirildiğinde, eşitleme hatası.

#### <a name="scenarios"></a>Senaryolar
Eşitlenen bir kullanıcı için şirket içi bir Federasyon etki alanını tooanother Federasyon etki alanından hello UserPrincipalName soneki değiştirildi. Örneğin, *UserPrincipalName = bob@contoso.com*  çok değiştirildi*UserPrincipalName = bob@fabrikam.com* .

#### <a name="example"></a>Örnek
1. Bob Smith, Contoso.com için bir hesap hello UserPrincipalName Active Directory'de yeni bir kullanıcı olarak eklenmişbob@contoso.com
2. Bob tooa farklı bölme Fabrikam.com ve kendi UserPrincipalName adlı contoso.com değiştirilir taşırtoobob@fabrikam.com
3. Azure Active Directory ile Federasyon etki alanı contoso.com ve fabrikam.com etki alanlarıdır.
4. Bob'un userPrincipalName güncelleştirilmemiş ve bir "FederatedDomainChangeError" eşitleme hatayla sonuçlanır.

#### <a name="how-toofix"></a>Nasıl toofix
Bir kullanıcının UserPrincipalName soneki @ bob gelen güncelleştirildi,**contoso.com** @ toobob**fabrikam.com**, burada her ikisi de **contoso.com** ve **fabrikam.com** olan **Federasyon etki alanları**, bu adımları toofix hello eşitleme hatası izleyin

1. Azure AD'den Hello kullanıcının UserPrincipalName güncelleştirmek bob@contoso.com toobob@contoso.onmicrosoft.com. Hello Azure AD PowerShell modülü PowerShell komutuyla aşağıdaki hello kullanabilirsiniz:`Set-MsolUserPrincipalName -UserPrincipalName bob@contoso.com -NewUserPrincipalName bob@contoso.onmicrosoft.com`
2. Merhaba sonraki eşitleme döngüsü tooattempt eşitleme izin verin. Bu zaman eşitleme başarılı olur ve hello UserPrincipalName, Bob güncelleştirecektir toobob@fabrikam.com beklendiği gibi.

#### <a name="related-articles"></a>İlgili makaleler
* [Bir kullanıcı hesabı toouse farklı bir Federasyon etki alanına UPN hello değiştirdikten sonra değişiklikleri hello Azure Active Directory eşitleme aracı tarafından eşitlenen değil](https://support.microsoft.com/en-us/help/2669550/changes-aren-t-synced-by-the-azure-active-directory-sync-tool-after-you-change-the-upn-of-a-user-account-to-use-a-different-federated-domain)

## <a name="largeobject"></a>LargeObject
### <a name="description"></a>Açıklama
Bir öznitelik hello boyut sınırı, uzunluk sınırı veya Azure Active Directory şemasına göre sayısı sınırını izin aştığında hello eşitleme işlemi hello sonuçları **LargeObject** veya **ExceededAllowedLength** eşitleme hatası. Genellikle bu hata için öznitelikler aşağıdaki hello oluşur.

* userCertificate
* userSMIMECertificate
* thumbnailPhoto
* proxyAddresses

### <a name="possible-scenarios"></a>Olası senaryolar
1. Bob'un userCertificate özniteliği çok fazla sertifikalar atanması tooBob depolama. Bunlar daha eski, süresi dolan sertifikaları olabilir. Merhaba sabit sınırı 15 sertifikaları olur. Nasıl toohandle LargeObject userCertificate hatalarla, lütfen öznitelik hakkında daha fazla bilgi için tooarticle başvuran [userCertificate özniteliği tarafından işleme LargeObject hatalardır](active-directory-aadconnectsync-largeobjecterror-usercertificate.md).
2. Bob'un userSMIMECertificate özniteliği çok fazla sertifikalar atanması tooBob depolama. Bunlar daha eski, süresi dolan sertifikaları olabilir. Merhaba sabit sınırı 15 sertifikaları olur.
3. Active Directory'de ayarlanan Bob'un thumbnailPhoto Azure AD'ye eşitlenen çok büyük toobe ' dir.
4. Active Directory'de hello ProxyAddresses öznitelik otomatik doldurma sırasında bir nesne atanan çok fazla ProxyAddresses sahiptir.

### <a name="how-toofix"></a>Nasıl toofix
1. Merhaba hatasına neden bu hello öznitelik sınırlaması izin hello içinde olduğundan emin olun.

## <a name="related-links"></a>İlgili bağlantılar
* [Active Directory Yönetim Merkezi'nde Active Directory nesneleri bulun](https://technet.microsoft.com/library/dd560661.aspx)
* [Nasıl bir nesne için Azure Active Directory PowerShell kullanarak Azure Active Directory tooquery](https://msdn.microsoft.com/library/azure/jj151815.aspx)
