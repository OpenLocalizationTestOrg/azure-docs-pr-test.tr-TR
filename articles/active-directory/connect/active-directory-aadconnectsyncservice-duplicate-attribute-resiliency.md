---
title: "aaaIdentity eşitleme ve yinelenen öznitelik dayanıklılık | Microsoft Docs"
description: "Nasıl toohandle Azure AD Connect'i kullanarak dizin eşitleme sırasında UPN veya ProxyAddress çakışıyor nesneleri yeni davranışı."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 537a92b7-7a84-4c89-88b0-9bce0eacd931
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.openlocfilehash: e27dcbf9d71f83fa9566cae2fd99350297d1cd9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="identity-synchronization-and-duplicate-attribute-resiliency"></a>Kimlik eşitleme ve yinelenen öznitelik dayanıklılığı
Yinelenen öznitelik dayanıklılık nedeni uyuşmazlık giderilecektir Azure Active Directory'de bir özelliktir **UserPrincipalName** ve **ProxyAddress** Microsoft'un eşitleme araçlardan birini çalıştırırken çakışıyor.

Bu iki genellikle gerekli toobe benzersiz tüm öznitelikleridir **kullanıcı**, **grup**, veya **kişi** nesneleri belirli bir Azure Active Directory kiracısı.

> [!NOTE]
> Yalnızca kullanıcıların UPN olabilir.
> 
> 

Bu özellik sağlar hello yeni davranış hello bulut bölümünde hello eşitleme ardışık, bu nedenle, istemci belirsiz ve Azure AD Connect, DirSync ve MIM + bağlayıcı dahil olmak üzere herhangi bir Microsoft Eşitleme ürünü için ilgili. Bu belge toorepresent bu ürünlerden birinin Hello genel terim "eşitleme istemcisi" kullanılır.

## <a name="current-behavior"></a>Şu anki davranışı
Bu benzersizlik kısıtlamasını ihlal eden bir UPN veya ProxyAddress değer ile yeni bir nesne bir girişim tooprovision ise, Azure Active Directory bu nesnesinin oluşturulmasını engeller. Benzer şekilde, bir nesne bir benzersiz olmayan UPN veya ProxyAddress ile güncelleştirdiyseniz hello güncelleştirme başarısız. denemesi veya güncelleştirme sağlama hello her dışarı aktarma döngüsü sırasında hello eşitleme istemcisi tarafından denenen ve hello çakışması çözülene kadar toofail devam eder. Bir hata raporu e-posta her denendiğinde oluşturulur ve bir hata hello eşitleme istemci tarafından kaydedilir.

## <a name="behavior-with-duplicate-attribute-resiliency"></a>Yinelenen öznitelik dayanıklılığına sahip davranışı
Yerine tamamen tooprovision başarısız veya yinelenen bir öznitelik ile Azure Active Directory "Merhaba benzersizlik kısıtlamasını ihlal ediyor hello yinelenen özniteliği karantinaya" nesne güncelleştirin. Bu öznitelik, UserPrincipalName gibi sağlama için gerekli değilse hello hizmeti bir yer tutucu değerini atar. Bu geçici değerleri Hello biçimi  
"***<OriginalPrefix>+ < 4DigitNumber > @<InitialTenantDomain>. onmicrosoft.com***".  
Merhaba özniteliği gerekli değilse, ister bir **ProxyAddress**, Azure Active Directory sadece hello çakışma özniteliği karantinaya ve hello nesne oluşturma veya güncelleştirme işlemi devam eder.

Merhaba özniteliği karantinaya alma sırasında hello çakışması hakkında bilgi aynı hata raporu e-posta kullanılan hello hello eski davranışı gönderilir. Hello karantina gerçekleştiğinde, ancak, bu bilgileri, hello hata raporu içinde yalnızca bir kez görüntülenir. Bu e-postalar ileride toobe oturum devam etmez. Ayrıca, bu nesne için hello dışarı aktarma başarılı olduktan sonra hello eşitleme istemcisi bir hata günlüğe kaydetmez ve mu olmayan yeniden deneme hello oluşturma / güncelleştirme işlemi sonraki eşitleme döngüsü sırasında.

Bu davranış yeni bir öznitelik bırakıldı toosupport toohello kullanıcı, Grup ve iletişim nesne sınıfları eklendi:  
**DirSyncProvisioningErrors**

Normal olarak eklenmelidir hello benzersizlik kısıtlamasını ihlal ediyor kullanılan toostore hello çakışan özniteliği birden çok değerli bir özniteliktir. Bir arka plan Zamanlayıcı görevi, her saat toolook çözümlendi ve söz konusu hello öznitelikleri karantinadan otomatik olarak kaldırır yinelenen öznitelik çakışmaları çalıştıran Azure Active Directory'de etkin.

### <a name="enabling-duplicate-attribute-resiliency"></a>Yinelenen öznitelik dayanıklılık etkinleştirme
Yinelenen öznitelik dayanıklılık hello yeni varsayılan davranış tüm Azure Active Directory kiracılar arasında olacaktır. Bu üzerinde ilk kez 22 Ağustos 2016 veya sonraki sürümlerde eşitleme hello için etkinleştirilmiş tüm kiracılar için varsayılan olarak olacaktır. Eşitleme önceki toothis tarih etkin kiracılar hello özelliğinin toplu olarak etkin olacaktır. Bu sunum Eylül 2016'da başlayacak ve tooeach kiracının Teknik Bildirim kişi hello özelliği etkin olduğunda hello belirli bir tarih ile bir e-posta bildirimi gönderilir.

> [!NOTE]
> Yinelenen öznitelik dayanıklılık açık durumda sonra devre dışı bırakılamaz.

kiracınız için Hello özelliği etkinleştirilmişse toocheck hello hello Azure Active Directory PowerShell modülü en son sürümünü indirme ve çalıştırma yapabilirsiniz:

`Get-MsolDirSyncFeatures -Feature DuplicateUPNResiliency`

`Get-MsolDirSyncFeatures -Feature DuplicateProxyAddressResiliency`

> [!NOTE]
> Kiracınız için açık önce artık kümesi MsolDirSyncFeature cmdlet tooproactively etkinleştir hello yinelenen öznitelik dayanıklılık özelliğini kullanabilirsiniz. toobe mümkün tootest hello özelliği, toocreate yeni bir Azure Active Directory kiracısı gerekir.

## <a name="identifying-objects-with-dirsyncprovisioningerrors"></a>DirSyncProvisioningErrors nesneleriyle tanımlama
Bu hatalar son tooduplicate özelliği çakışmaları, Azure Active Directory PowerShell ve hello Office 365 Yönetici portalı tooidentify nesneleri şu anda iki yöntem vardır. Merhaba gelecekteki raporlama dayalı planları tooextend tooadditional portal vardır.

### <a name="azure-active-directory-powershell"></a>Azure Active Directory PowerShell
Hello için PowerShell cmdlet'leri bu konuda, doğru hello aşağıda verilmiştir:

* Cmdlet aşağıdaki hello büyük küçük harfe duyarlı değildir.
* Merhaba **– ErrorCategory PropertyConflict** her zaman dahil edilmelidir. Şu anda başka tür olan **ErrorCategory**, ancak bu hello gelecekteki genişletilmiş.

İlk olarak, çalıştırarak kullanmaya başlama **Bağlan MsolService** ve için Kiracı Yöneticisi kimlik bilgilerini girme.

Ardından, aşağıdaki cmdlet'leri ve işleçleri tooview hatalar farklı şekillerde hello kullanın:

1. [Tüm bakın](#see-all)
2. [Özellik türü tarafından](#by-property-type)
3. [Çakışan değerine göre](#by-conflicting-value)
4. [Bir dize arama kullanma](#using-a-string-search)
5. [Sıralanmış](#sorted)
6. [Sınırlı bir miktar veya tümü](#in-a-limited-quantity-or-all)

#### <a name="see-all"></a>Tümünü incele
Bağlantı kurulduktan sonra toosee genel hello Kiracı hataları sağlama öznitelik listesini çalıştırın:

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict`

Bu hello aşağıdaki gibi bir sonuç oluşturur:  
 ![Get-MsolDirSyncProvisioningError](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1.png "Get-MsolDirSyncProvisioningError")  

#### <a name="by-property-type"></a>Özellik türü tarafından
özellik türü tarafından toosee hataları eklemek hello **- PropertyName** hello bayrağıyla **UserPrincipalName** veya **ProxyAddresses** bağımsız değişkeni:

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyName UserPrincipalName`

Veya

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyName ProxyAddresses`

#### <a name="by-conflicting-value"></a>Çakışan değerine göre
tooa belirli özellik ilgili toosee hataları eklemek hello **- PropertyValue** bayrağı (**- PropertyName** de bu bayrak eklerken kullanılması gerekir):

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -PropertyValue User@domain.com -PropertyName UserPrincipalName`

#### <a name="using-a-string-search"></a>Bir dize arama kullanma
toodo geniş dize arama kullanmak hello **- AramaDizesi** bayrağı. Bu tüm hello özel bayrakları yukarıda hello bağımsız olarak kullanılabilir **- ErrorCategory PropertyConflict**, olduğu her zaman gerekli:

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -SearchString User`

#### <a name="in-a-limited-quantity-or-all"></a>Sınırlı bir miktar veya tümü
1. **MaxResults <Int>**  olabilir toolimit hello sorgu tooa belirli sayıda değerler kullanılır.
2. **Tüm** tüm sonuçları, çok sayıda hataları var. hello durumda alınır kullanılan tooensure olabilir.

`Get-MsolDirSyncProvisioningError -ErrorCategory PropertyConflict -MaxResults 5`

## <a name="office-365-admin-portal"></a>Office 365 Yönetici portalı
Dizin eşitleme hatalarına hello Office 365 Yönetim Merkezi'nde görüntüleyebilirsiniz. Merhaba hello Office 365 portalı yalnızca görüntüler raporda **kullanıcı** bu hataları olan nesne. Arasındaki çakışmaları hakkında bilgi göstermez **grupları** ve **kişiler**.

![Etkin kullanıcılar](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/1234.png "etkin kullanıcılar")

Nasıl tooview dizin eşitleme hatalarının hello Office 365 Yönetim Merkezi ile ilgili yönergeler için bkz: [Office 365'te dizin eşitleme hatalarına tanımlamak](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067).

### <a name="identity-synchronization-error-report"></a>Kimlik eşitleme hata raporu
Yinelenen öznitelik çakışma sahip bir nesne için bir bildirim yer aldığı bu yeni davranış işlendiğinde kimlik eşitleme hata raporu e-posta, hello standart toohello Teknik Bildirim kişi hello Kiracı için gönderilir. Ancak, bu davranış önemli bir değişiklik yoktur. Merhaba çakışma çözüldü kadar her sonraki hata raporunda hello geçmiş, yinelenen öznitelik çakışma hakkında bilgi dahil edilir. Bu yeni davranış ile belirli bir çakışma hello hata bildirimi yalnızca bir kez - hello çakışan öznitelik karantinaya hello zaman gibi görünüyor.

Aşağıda, hangi hello e-posta bildirimi için ProxyAddress çakışması benzer bir örnek verilmiştir:  
    ![Etkin kullanıcılar](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "etkin kullanıcılar")  

## <a name="resolving-conflicts"></a>Çakışmalarını çözme
Strateji ve çözüm taktiği bu hataları için sorun giderme yinelenen öznitelik hataları hello son işlenen hello biçimi farklı. Merhaba tek fark hello çakışma giderildikten sonra hello Zamanlayıcı görevi dağılımlarında hello Kiracı hello Hizmet tarafı tooautomatically'aracılığıyla hello özniteliği soru toohello uygun nesnesinde eklemek olacaktır.

Merhaba aşağıdaki makalede özetlenmektedir çeşitli sorun giderme ve çözümleme stratejileri: [yinelenen ya da geçersiz öznitelikler önlemek Office 365'te dizin eşitleme](https://support.microsoft.com/kb/2647098).

## <a name="known-issues"></a>Bilinen sorunlar
Bu bilinen sorunlar hiçbiri veri kaybı veya hizmet düşüşüne neden olur. Birkaç estetik, diğerleri standart neden "*öncesi dayanıklılık*" Merhaba çakışma özniteliği ve başka karantinaya alma yerine durum yinelenen öznitelik hataları toobe belirli hataları toorequire fazladan el ile düzeltme yukarı neden olur.

**Çekirdek davranışı:**

1. Karşılıklı toohello yinelenen karantinaya alınmış öznitelikleri gibi belirli özniteliği yapılandırmaları nesneleriyle tooreceive verme hataları devam eder.  
   Örneğin:
   
    a. Yeni kullanıcı AD UPN ile oluşturulur  **Joe@contoso.com**  ve ProxyAddress**smtp:Joe@contoso.com**
   
    b. Merhaba, bu nesnenin özellikleri çakışma ProxyAddress olduğu varolan bir grupla  **SMTP:Joe@contoso.com** .
   
    c. Dışa aktarma, üzerine bir **ProxyAddress çakışma** hata karantinaya hello çakışma özniteliklere sahip yerine oluşur. Merhaba dayanıklılık özellik etkinleştirilmeden önce olabilirdi gibi hello işlemi her sonraki eşitleme döngüsü sırasında denenir.
2. İki grup oluşturduysanız hello ile aynı içi SMTP adresi, yinelenen bir standart hello ilk denemede bir başarısız tooprovision **ProxyAddress** hata. Ancak, hello yinelenen değer düzgün şekilde hello sonraki eşitleme döngüsü karantinaya alındı.

**Office portalı rapor**:

1. Merhaba ayrıntılı hata iletisi UPN çakışma kümesinde iki nesneler için aynı hello ' dir. Bu, bunların her ikisi de değiştirilmiş / karantinaya gerçekte yalnızca bir tanesi değiştirilen veri varken UPN Değerlerinin beklendiğinden gösterir.
2. Merhaba yanlış displayName değişti ve karantinaya UPN Değerlerinin oluşmuş bir kullanıcı için UPN çakışması Hello ayrıntılı hata iletisi gösterir. Örneğin:
   
    a. **Kullanıcı A** eşitlenir ilk yukarı **UPN = User@contoso.com** .
   
    b. **Kullanıcı B** sonraki ile ayarlama girişimi toobe eşitlenen **UPN = User@contoso.com** .
   
    c. **B kullanıcısının** UPN çok değiştirilen **User1234@contoso.onmicrosoft.com**  ve  **User@contoso.com**  çok eklenen**DirSyncProvisioningErrors**.
   
    d. Merhaba hata iletisi için **kullanıcı B** bildiren **kullanıcısı** zaten  **User@contoso.com**  UPN, ancak gösterildiği gibi **kullanıcı B'nin** kendi görünen adı.

**Kimlik eşitleme hata raporu**:

Merhaba bağlantısını *adımları tooresolve bu sorunu* yanlış:  
    ![Etkin kullanıcılar](./media/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency/6.png "etkin kullanıcılar")  

Çok işaret etmelidir[https://aka.ms/duplicateattributeresiliency](https://aka.ms/duplicateattributeresiliency).

## <a name="see-also"></a>Ayrıca bkz.
* [Azure AD Connect eşitleme](active-directory-aadconnectsync-whatis.md)
* [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md)
* [Office 365'te dizin eşitleme hataları tanımlar](https://support.office.com/en-us/article/Identify-directory-synchronization-errors-in-Office-365-b4fc07a5-97ea-4ca6-9692-108acab74067)

