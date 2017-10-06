---
title: "Azure AD Connect: Tasarım kavramları | Microsoft Docs"
description: "Bu konuda belirli uygulama tasarım alanları ayrıntıları"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 4114a6c0-f96a-493c-be74-1153666ce6c9
ms.service: active-directory
ms.custom: azure-ad-connect
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1e5d5c6a716ca653fb14fc059e8155124b433732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-design-concepts"></a>Azure AD Connect: Tasarım kavramları
Bu konunun amacı Hello Azure AD Connect hello uygulama tasarımı sırasında zorlayıcı toodescribe alanlar'dır. Bu konuda derinlemesine belirli alanlara ise ve bu kavramları diğer konularında kısaca açıklanmıştır.

## <a name="sourceanchor"></a>sourceAnchor
Merhaba sourceAnchor özniteliği olarak tanımlanır *bir nesne hello ömrü boyunca sabit bir öznitelik*. Bir nesneyi benzersiz şekilde tanımlayan hello olduğu aynı şirket içi nesne ve Azure AD. Merhaba özniteliği olarak da adlandırılır **İmmutableıd** ve hello iki adları birbirinin yerine kullanılır.

Merhaba sözcüğünü değişmez, "değiştirilemez", önemli toothis konudur. Bu özniteliğin değeri ayarlandıktan sonra değiştirilemez olduğundan, önemli toopick senaryonuz destekleyen bir tasarım kalır.

Merhaba öznitelik hello senaryolar için kullanılır:

* Yeni bir eşitleme altyapısı sunucusu yerleşik veya bir olağanüstü durum kurtarma senaryosunda sonra yeniden, bu öznitelik varolan nesneleri nesneleri şirket içi Azure AD'de bağlar.
* Bir yalnızca bulut kimlik tooa eşitlenmiş kimlik modelden taşıyın ve sonra bu öznitelik nesneleri çok sağlar, şirket içi nesnelerle "sabit match" var olan nesneleri Azure AD'de.
* Federasyon ve ardından bu özniteliği hello ile birlikte kullanıyorsanız, **userPrincipalName** hello kullanılan toouniquely tanımlamak bir kullanıcı talebi.

Toousers ilgili olarak bu konu hakkında sourceAnchor yalnızca alınmaktadır. Merhaba aynı kuralları uygula tooall nesne türleri, ancak bunu yalnızca kullanıcılar için bu sorun genellikle bir konudur.

### <a name="selecting-a-good-sourceanchor-attribute"></a>İyi sourceAnchor özniteliği seçme
Merhaba öznitelik değeri hello kurallara uymalıdır:

* Daha az 60 karakter uzunluğunda olabilir
  * Karakter olmaması, a-z, A-Z veya 0-9 kodlanmış ve 3 karakter olarak sayılır
* Bir özel karakter içeremez: &#92;! # $ % & * + / = ? ^ &#96; { } | ~ < > ( ) ' ; : , [ ] " @ _
* Genel olarak benzersiz olmalıdır
* Bir dize, tamsayı veya ikili olmalıdır
* Kullanıcı adı, bu değişiklikleri dayanmalıdır değil
* Değil büyük küçük harfe duyarlı ve örneğe göre farklılık gösterebilir değerleri kaçının
* Merhaba nesnesi oluşturulduğunda atanmalıdır

Merhaba sourceAnchor seçtiyseniz, Azure AD Connect Base64Encode hello öznitelik değeri tooensure hiçbir özel karakter görünür sonra türü dize değil. ADFS değerinden başka bir federasyon sunucusu kullanıyorsanız, ayrıca Base64Encode hello özniteliği için sunucunuzun emin olun.

Merhaba sourceAnchor özniteliği büyük/küçük harf duyarlıdır. "JohnDoe" değerini olduğu değil hello "johndoe" ile aynı. Ancak, iki farklı nesneler arasındaki fark durumda yalnızca sahip olmamalıdır.

Tek bir ormana sahibim şirket içi, kullanmanız gereken sonra hello özniteliği ise **objectGUID**. Bu ayrıca Azure AD Connect'i hızlı ayarları kullanın ve aynı zamanda DirSync tarafından kullanılan öznitelik hello kullanılan hello özniteliğidir.

Birden çok ormanınız varsa ve kullanıcı etki alanları ve ormanlar arasında sonra taşımayın **objectGUID** iyi özniteliği toouse olsa bile bu durumda.

Kullanıcıların etki alanları ve ormanlar arasında taşırsanız, hello taşıma işlemi sırasında hello kullanıcılarla değişmeyen veya taşınabilir bir özniteliği bulmalıdır. Toointroduce yapay bir öznitelik bir önerilen yaklaşımdır. Bir GUID gibi görünen bir şey tutan bir öznitelik uygun olacaktır. Nesne oluşturma sırasında yeni bir GUID oluşturulur ve hello kullanıcı damgalı. Özel eşitleme kuralı üzerinde hello göre bu değer hello eşitleme altyapısı sunucusu toocreate oluşturulabilir **objectGUID** ve güncelleştirme hello seçili özniteliği EKLER. Merhaba nesneyi taşıdığınızda, bu değer emin tooalso kopyalama hello içeriği olun.

Toopick değişmeyen bildiğiniz varolan bir özniteliğe başka bir çözümdür. Yaygın olarak kullanılan öznitelikler içerir **EmployeeID**. Harfleri içeren bir öznitelik düşünüyorsanız, hiçbir fırsat hello çalışması (küçük harf ve büyük harflerle) hello özniteliğin değerini değiştirebilirsiniz olduğundan emin olun. Kullanılmaması gereken hatalı öznitelikler bu özniteliklerle hello hello kullanıcı adını içerir. Marriage veya divorce hello bu öznitelik için izin verilmiyor beklenen toochange adıdır. Bu ayrıca nedenlerinden biri neden olduğu gibi öznitelikleri **userPrincipalName**, **posta**, ve **targetAddress** hello Azure AD Connect yükleme bile olası tooselect değildir Sihirbazı. Bu öznitelikler de hello içerir "@" Merhaba sourceAnchor izin verilmeyen bir karakter.

### <a name="changing-hello-sourceanchor-attribute"></a>Merhaba sourceAnchor özniteliği değiştirme
Azure AD'de hello nesne oluşturulduktan sonra hello kimlik eşitlenir Hello sourceAnchor özniteliği değeri değiştirilemez.

Bu nedenle, aşağıdaki kısıtlamaları hello uygulamak tooAzure AD Connect:

* Merhaba sourceAnchor özniteliği yalnızca ilk yükleme sırasında ayarlanabilir. Merhaba Yükleme Sihirbazı'nı yeniden çalıştırın, bu seçenek salt okunurdur. Sonra da kaldırmanız ve yeniden yüklemeniz gerekir, bu ayar toochange gerekiyorsa.
* Başka bir Azure AD Connect sunucusu, sonra yüklerseniz seçin, daha önce kullanılan aynı sourceAnchor özniteliği hello gerekir. Daha önce DirSync kullanarak ve tooAzure AD taşıma bağlanma kullanmanız gerekir, **objectGUID** , DirSync tarafından kullanılan hello öznitelik olduğundan.
* SourceAnchor için hello değeri Hello nesne dışarı aktarılan tooAzure AD, ardından Azure AD Connect eşitleme bir hata oluşturur ve daha fazla değişiklik nesnede hello sorun düzeltilmiştir ve hello sourceAnchor geri hello değiştirilir önce izin vermiyor sonra değiştirilirse Kaynak dizini.

## <a name="using-msds-consistencyguid-as-sourceanchor"></a>MsDS-ConsistencyGuid sourceAnchor kullanma
Varsayılan olarak, Azure AD Connect (sürüm 1.1.486.0 ve daha eski) objectGUID hello sourceAnchor özniteliği olarak kullanır. Sistem tarafından oluşturulan objectguıd'dir. Değerini oluştururken AD nesnelerini şirket içi belirtemezsiniz. Bölümünde açıklandığı gibi [sourceAnchor](#sourceanchor), toospecify hello sourceAnchor değerine ihtiyacınız olduğu senaryolar da vardır. Merhaba senaryoları geçerli tooyou varsa, hello sourceAnchor özniteliği olarak yapılandırılabilir bir AD özniteliği (örneğin, msDS-ConsistencyGuid) kullanmanız gerekir.

Azure AD Connect (sürüm 1.1.524.0 ve sonra) şimdi msDS-ConsistencyGuid sourceAnchor özniteliği olarak hello kullanımını kolaylaştırır. Bu özelliği kullanıldığında, Azure AD Connect hello eşitleme kuralları otomatik olarak yapılandırır:

1. MsDS-ConsistencyGuid hello sourceAnchor özniteliği olarak kullanıcı nesneleri için kullanın. ObjectGUID diğer nesne türleri için kullanılır.

2. Verilen herhangi için şirket içi AD kullanıcısının, msDS-ConsistencyGuid özniteliği değil doldurulmuş, Azure AD Connect, şirket içi Active Directory'de, objectGUID değer geri toohello msDS-ConsistencyGuid öznitelik yazan nesnesi. Merhaba msDS-ConsistencyGuid özniteliği doldurulduktan sonra Azure AD Connect sonra hello nesne tooAzure AD dışa aktarır.

>[!NOTE]
> Bir kez bir şirket içi AD nesne (yani AD bağlayıcı alanı hello içeri aktarılıp, meta veri deposu hello öngörülen) Azure AD Connect içine aktarılır, sourceAnchor değerini artık değiştiremezsiniz. toospecify hello sourceAnchor değeri için bir şirket içi verilen AD nesne, Azure AD Connect içeri aktarılmadan önce kendi msDS-ConsistencyGuid özniteliği yapılandırın.

### <a name="permission-required"></a>İzin gerekiyor
Bu özellik toowork için hello AD DS kullanılan hesap toosynchronize şirket içi Active Directory ile şirket içi Active Directory'de yazma izni toohello msDS-ConsistencyGuid öznitelik verilmesi gerekir.

### <a name="how-tooenable-hello-consistencyguid-feature---new-installation"></a>Nasıl tooenable hello ConsistencyGuid özellik - yeni yükleme
Yeni yükleme sırasında ConsistencyGuid sourceAnchor olarak hello kullanımını etkinleştirebilirsiniz. Bu bölümde, hızlı ve özel yükleme ayrıntıları ele alınmaktadır.

  >[!NOTE]
  > Azure AD Connect yalnızca yeni sürümlerini (1.1.524.0 ve sonra) destekler, yeni yükleme sırasında sourceAnchor olarak ConsistencyGuid kullanımını hello.

### <a name="how-tooenable-hello-consistencyguid-feature"></a>Nasıl tooenable hello ConsistencyGuid özelliği
Şu anda hello özelliği yalnızca yeni Azure AD Connect yüklemesi sırasında yalnızca etkinleştirilebilir.

#### <a name="express-installation"></a>Hızlı yükleme
Azure AD Connect ile hızlı mod yüklerken hello Azure AD Connect Sihirbazı hello en uygun AD özniteliği toouse mantığı aşağıdaki hello kullanarak hello sourceAnchor özniteliği otomatik olarak belirler:

* İlk olarak, Azure AD Kiracı tooretrieve hello AD özniteliği olarak kullanılan hello Azure AD Connect Sihirbazı sorguları hello önceki Azure AD Connect yükleme sourceAnchor özniteliği (varsa) hello. Bu bilgiler varsa, Azure AD Connect hello aynı AD özniteliğini kullanır.

  >[!NOTE]
  > Azure AD Connect yalnızca yeni sürümlerini (1.1.524.0 ve sonra) hello sourceAnchor özniteliği hakkında bilgileri depolar Azure AD kiracınızda yükleme sırasında kullanılır. Azure AD Connect eski sürümlerinde yoktur.

* Kullanılan hello sourceAnchor özniteliği hakkında bilgi kullanılabilir değilse, Başlangıç Sihirbazı'nı şirket içi Active Directory'de hello msDS-ConsistencyGuid özniteliği hello durumunu denetler. Merhaba özniteliği hello dizinde herhangi bir nesne üzerinde yapılandırılmazsa hello Sihirbazı hello msDS-ConsistencyGuid hello sourceAnchor özniteliği olarak kullanır. Merhaba dizininde bir veya daha fazla nesnelerde Hello özniteliği yapılandırdıysanız, Başlangıç Sihirbazı'nı hello özniteliği diğer uygulamalar tarafından kullanılıyor ve sourceAnchor özniteliği olarak uygun değil sonucuna...

* Bu durumda hello Sihirbazı hello sourceAnchor özniteliği olarak toousing objectGUID geri döner.

* Merhaba sourceAnchor özniteliği karar sonra Başlangıç Sihirbazı, Azure AD kiracınızda hello bilgileri depolar. Merhaba bilgiler gelecekteki Azure AD Connect yüklemesi tarafından kullanılır.

Hızlı yükleme işlemi tamamlandıktan sonra hello Sihirbazı hangi öznitelik hello kaynak bağlantısı özniteliği olarak çekilen bildirir.

![SourceAnchor için çekildi AD özniteliği Sihirbazı sizi bilgilendirir](./media/active-directory-aadconnect-design-concepts/consistencyGuid-01.png)

#### <a name="custom-installation"></a>Özel yükleme
Azure AD Connect özel moduyla yüklerken hello Azure AD Connect Sihirbazı sourceAnchor özniteliği yapılandırırken iki seçenek sunar:

![Özel yükleme - sourceAnchor yapılandırma](./media/active-directory-aadconnect-design-concepts/consistencyGuid-02.png)

| Ayar | Açıklama |
| --- | --- |
| Benim için Hello kaynak bağlantısı yönetmek Azure sağlar | Sizin için Azure AD toopick hello özniteliği istiyorsanız bu seçeneği seçin. Bu seçeneği belirlerseniz, Azure AD Connect Sihirbazı uygular hello aynı [sourceAnchor özniteliği seçme mantığı Express yüklemesi sırasında kullanılan](#express-installation). Benzer tooExpress yükleme, Başlangıç Sihirbazı'nı özel yükleme tamamlandıktan sonra hangi öznitelik hello kaynak bağlantısı özniteliği çekilen sizi bilgilendirir. |
| Belirli bir öznitelik | Varolan bir AD özniteliği hello sourceAnchor özniteliği olarak toospecify istiyorsanız bu seçeneği belirleyin. |

### <a name="how-tooenable-hello-consistencyguid-feature---existing-deployment"></a>Nasıl tooenable hello ConsistencyGuid özellik - var olan dağıtım
ObjectGUID hello kaynak bağlantısı özniteliği olarak kullanan mevcut bir Azure AD Connect dağıtımınız varsa, toousing ConsistencyGuid yerine geçebilirsiniz.

>[!NOTE]
> Azure AD Connect yalnızca yeni sürümlerini (1.1.552.0 ve sonra) objectGUID tooConsistencyGuid hello kaynak bağlantısı özniteliği olarak gelen geçişi destekler.

objectGUID tooConsistencyGuid hello kaynak bağlantısı özniteliği olarak gelen tooswitch:

1. Hello Azure AD Connect Sihirbazı başlatın ve tıklatın **yapılandırma** toogo toohello görevleri ekran.

2. Select hello **yapılandırma kaynak bağlantısı** görev seçeneğini ve tıklayın **sonraki**.

   ![Var olan dağıtım - adım 2 ConsistencyGuid etkinleştir](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment01.png)

3. Azure AD yönetici kimlik bilgilerinizi girin ve tıklayın **sonraki**.

4. Azure AD Connect Sihirbazı hello msDS-ConsistencyGuid özniteliği şirket içi Active Directory'de hello durumunu inceler. Dizin, Azure AD Connect'i başka bir uygulama hello özniteliği kullanmakta olduğu ve güvenli toouse olduğu sonucuna hello Hello özniteliği herhangi yapılandırılmazsa hello kaynak bağlantısı özniteliği olarak nesne. Tıklatın **sonraki** toocontinue.

   ![Var olan dağıtım - 4. adım ConsistencyGuid etkinleştir](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment02.png)

5. Merhaba, **hazır tooConfigure** ekranında **yapılandırma** toomake hello yapılandırma değişikliği.

   ![Var olan dağıtım - 5. adım ConsistencyGuid etkinleştir](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment03.png)

6. Hello Yapılandırma tamamlandıktan sonra o msDS-ConsistencyGuid şimdi hello kaynak bağlantısı özniteliği olarak kullanılan hello Sihirbazı'nı gösterir.

   ![Var olan dağıtım - adım 6 ConsistencyGuid etkinleştir](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeployment04.png)

Hello özniteliği hello dizininde bir veya daha fazla nesnelerde yapılandırılmışsa (4. adım) hello Çözümleme sırasında Başlangıç Sihirbazı'nı hello özniteliği başka bir uygulama tarafından kullanılıyor ve hello diyagramda gösterildiği gibi bir hata döndürür sonlanır. Bu hello özniteliği var olan uygulamalar tarafından kullanılmaz, nasıl toosuppress hata hello hakkında bilgi için destek toocontact gerekir.

![Var olan dağıtım - hata ConsistencyGuid etkinleştir](./media/active-directory-aadconnect-design-concepts/consistencyguidexistingdeploymenterror.png)

### <a name="impact-on-ad-fs-or-third-party-federation-configuration"></a>AD FS veya üçüncü taraf Federasyon yapılandırma üzerinde etkisi
Azure kullanıyorsanız, AD Connect toomanage şirket içi AD FS dağıtımı, hello Azure AD Connect hello talep kuralları toouse hello aynı AD özniteliği sourceAnchor olarak otomatik olarak güncelleştirir. Bu, ADFS tarafından oluşturulan hello İmmutableıd talebi hello sourceAnchor değerleri dışarı aktarılan tooAzure ile AD tutarlı olmasını sağlar.

AD FS Azure AD Connect dışında yönettiğiniz veya üçüncü taraf federasyon sunucuları için kimlik doğrulaması kullanıyorsanız, el ile Merhaba talep kuralları talep toobe hello sourceAnchor değerleri ile tutarlı olarak tooAzure AD dışarı İmmutableıd için güncelleştirmeniz gerekir makale bölümünde açıklanan [Değiştir AD FS talep kuralları](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-federation-management#modclaims). Başlangıç Sihirbazı'nı yükleme tamamlandıktan sonra uyarı aşağıdaki hello döndürür:

![Üçüncü taraf Federasyon yapılandırma](./media/active-directory-aadconnect-design-concepts/consistencyGuid-03.png)

### <a name="adding-new-directories-tooexisting-deployment"></a>Yeni dizinleri tooexisting dağıtım ekleme
Azure AD Connect hello ConsistencyGuid özelliği etkinleştirilmiş ve tooadd istediğiniz artık başka bir dizin toohello dağıtım dağıttığınız varsayalım. Tooadd hello dizin çalıştığınızda, Azure AD Connect Sihirbazı hello mSDS-ConsistencyGuid özniteliği hello Directory'de hello durumunu denetler. Merhaba dizininde bir veya daha fazla nesnelerde Hello özniteliği yapılandırdıysanız, Başlangıç Sihirbazı'nı hello özniteliği diğer uygulamalar tarafından kullanılıyor ve hello diyagramda gösterildiği gibi bir hata döndürür sonlanır. Bu hello özniteliği var olan uygulamalar tarafından kullanılmaz, nasıl toosuppress hata hello hakkında bilgi için destek toocontact gerekir.

![Yeni dizinleri tooexisting dağıtım ekleme](./media/active-directory-aadconnect-design-concepts/consistencyGuid-04.png)

## <a name="azure-ad-sign-in"></a>Azure AD oturum açma
Şirket içi dizininizi Azure AD ile tümleştirme sırasında önemli toounderstand olan hello eşitleme ayarlarını hello şekilde kullanıcı nasıl etkileyebileceğini kimliğini doğrular. Azure AD userPrincipalName (UPN) tooauthenticate hello kullanıcı kullanır. Ancak, kullanıcılarınızın eşitlediğinizde, userPrincipalName değeri için dikkatli bir şekilde kullanılan hello özniteliği toobe seçmeniz gerekir.

### <a name="choosing-hello-attribute-for-userprincipalname"></a>Merhaba özniteliği userPrincipalName için seçme
Ne zaman Azure birinde kullanılan UPN toobe hello değeri sağlamak için hello özniteliği seçerek emin olmanız gerekir

* Merhaba öznitelik değerleri hello biçimi olması gereken toohello UPN sözdizimi (RFC 822) uygunusername@domain
* Merhaba, hello değerleri eşleşmeleri tooone Hello soneki özel etki alanlarını Azure AD'de doğrulandı.

Express ayarlarında hello hello özniteliği için seçim userPrincipalName kabul edilir. Merhaba userPrincipalName özniteliği hello değer içermiyorsa, kullanıcılar toosign tooAzure içinde istediğiniz sonra seçmeniz gerekir **özel yükleme**.

### <a name="custom-domain-state-and-upn"></a>Özel etki alanı durumu ve UPN
Önemli tooensure hello UPN soneki doğrulanmış bir etki alanı olduğundan emin olur.

John, contoso.com ormanındaki bir kullanıcıdır. John istediğiniz toouse hello şirket içi UPN john@contoso.com çalıştırdıktan sonra tooAzure toosign eşitlenen kullanıcılar tooyour Azure AD directory contoso.onmicrosoft.com. toodo bu nedenle, tooadd gerekir ve contoso.com özel bir etki alanı başlatmak için önce Azure AD'de doğrulayın. Merhaba kullanıcılar eşitleniyor. John, örneğin contoso.com Hello UPN soneki Azure AD'de doğrulanmış bir etki alanı eşleşmiyorsa, Azure AD ile contoso.onmicrosoft.com hello UPN soneki değiştirir.

### <a name="non-routable-on-premises-domains-and-upn-for-azure-ad"></a>Yönlendirilebilir olmayan şirket içi etki alanları ve Azure AD için UPN
Bazı kuruluşlar contoso.local veya contoso gibi basit tek etiketli etki alanları gibi yönlendirilebilir olmayan etki alanları sahiptir. Mümkün tooverify yönlendirilemeyen bir etki alanı Azure AD içinde değildir. Azure AD Connect tooonly doğrulanmış bir etki alanı Azure AD'ye eşitleyebilirsiniz. Azure AD dizini oluşturduğunuzda, örneğin, contoso.onmicrosoft.com Azure AD için varsayılan etki alanı haline gelir yönlendirilebilir bir etki alanı oluşturur. Toosync toohello varsayılan onmicrosoft.com etki alanı istemediğiniz durumda bu nedenle, bu gerekli tooverify diğer yönlendirilebilir etki alanında böyle bir senaryo olur.

Okuma [özel etki alanı adı tooAzure Active Directory eklemek](../active-directory-add-domain.md) ekleme ve etki alanı doğrulama hakkında daha fazla bilgi için.

Azure AD Connect yönlendirilebilir olmayan etki alanı ortamında çalıştırıyorsanız ve uygun şekilde express ayarlarla devam giderek uyar algılar. Büyük olasılıkla bu hello hello kullanıcıların UPN sonra yönlendirilemeyen bir etki alanında çalışıyorsanız yönlendirilemeyen sonekleri da içerir. Örneğin, contoso.local altında çalıştırıyorsanız, Azure AD Connect'i hızlı ayarları kullanmak yerine, toouse özel ayarları önerir. Özel ayarlarını kullanarak hello kullanıcılar eşitlenmiş tooAzure AD sonra UPN toosign tooAzure içinde olarak kullanılması gereken mümkün toospecify hello özniteliği olan.

## <a name="next-steps"></a>Sonraki adımlar
[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.
