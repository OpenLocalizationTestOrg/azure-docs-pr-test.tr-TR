---
title: "Azure AD Connect: Özel yükleme | Microsoft Belgeleri"
description: "Bu belge hello Azure AD Connect için özel yükleme seçenekleri ayrıntılı olarak açıklanmaktadır. Bu yönergeler tooinstall Active Directory aracılığıyla Azure AD Connect kullanın."
services: active-directory
keywords: "Azure AD Connect nedir, Active Directory yükleme, Azure AD için gerekli bileşenler"
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 6d42fb79-d9cf-48da-8445-f482c4c536af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: c49724fab78c5a1688662043f69506fff6f82104
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-installation-of-azure-ad-connect"></a>Azure AD Connect özel yüklemesi
Azure AD Connect **özel ayarları** hello yükleme için daha fazla seçenek istediğinizde kullanılır. Birden çok ormanınız varsa veya hello hızlı yükleme kapsamında olmayan tooconfigure isteğe bağlı özellikler istiyorsanız kullanılır. Merhaba burada tüm durumlarda kullanılan [ **hızlı yükleme** ](active-directory-aadconnect-get-started-express.md) seçeneğinin dağıtımınız veya topolojiniz uygun olmadığı.

Azure AD Connect'i yüklemeye başlamadan önce emin olun çok[Azure AD Connect indirin](http://go.microsoft.com/fwlink/?LinkId=615771) ve tam hello önkoşul adımlarını [Azure AD Connect: donanım ve Önkoşullar](active-directory-aadconnect-prerequisites.md). Ayrıca [Azure AD Connect hesapları ve izinleri](active-directory-aadconnect-accounts-permissions.md) bölümünde açıklandığı üzere, gerekli hesaplara sahip olduğunuzdan olduğundan emin olun .

Özelleştirilmiş ayarlar, topolojinizle eşleşmiyorsa, tooupgrade DirSync, örneğin bkz [ilgili belgelere](#related-documentation) diğer senaryolar için.

## <a name="custom-settings-installation-of-azure-ad-connect"></a>Azure AD Connect özel ayarlarını yükleme
### <a name="express-settings"></a>Hızlı Ayarlar
Bu sayfada tıklatın **Özelleştir** toostart özelleştirilmiş ayarları yüklemeyi.

### <a name="install-required-components"></a>Gerekli bileşenleri yükleme
Merhaba Eşitleme hizmetlerini yüklerken, hello isteğe bağlı yapılandırma bölümünü işaretlenmemiş olarak bırakabilirsiniz ve Azure AD Connect her şeyi otomatik olarak ayarlar. Bir SQL Server 2012 Express LocalDB örneği ayarlar, hello uygun grupları oluşturun ve izinleri atayın. Toochange hello Varsayılanları isterseniz, kullanılabilir tablo toounderstand hello isteğe bağlı yapılandırma seçenekleri aşağıdaki hello kullanabilirsiniz.

![Gerekli Bileşenler](./media/active-directory-aadconnect-get-started-custom/requiredcomponents.png)

| İsteğe Bağlı Yapılandırma | Açıklama |
| --- | --- |
| Mevcut bir SQL Server'ı kullanma |Toospecify hello SQL Server adı ve hello örnek adı sağlar. Toouse istediğiniz bir veritabanı sunucusu zaten varsa bu seçeneği belirleyin. Bir virgül ve bağlantı noktası numarası ve ardından hello örnek adını girin **örnek adı** SQL Server'ınızdaki gözatma özelliği etkin yoksa. |
| Mevcut bir hizmet hesabını kullanma |Varsayılan olarak Azure AD Connect hello Eşitleme Hizmetleri toouse için bir sanal hizmet hesabı kullanır. Uzak bir SQL server kullanmak veya kimlik doğrulama gerektiren bir proxy kullanıyorsanız, toouse gereken bir **yönetilen hizmet hesabı** veya hello etki alanında bir hizmet hesabı kullanın ve hello parolayı biliyor. Bu gibi durumlarda hello hesap toouse girin. Merhaba hizmet hesabı için bir oturum oluşturulabilmesi hello yükleme çalıştıran hello kullanıcının SQL'de bir olduğundan emin olun. Bkz. [Azure AD Connect hesapları ve izinleri](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) |
| Özel eşitleme grubu belirtme |Merhaba Eşitleme Hizmetleri yüklendiğinde varsayılan olarak Azure AD Connect dört grupları yerel toohello server oluşturur. Bu gruplar: Administrators grubunun, işleçler grubu, gözatma grubu ve hello parola sıfırlama grubudur. Kendi gruplarınızı burada belirtebilirsiniz. Merhaba gruplar hello sunucuda yerel olmalıdır ve hello etki alanında yer alamaz. |

### <a name="user-sign-in"></a>Kullanıcı oturumu açma
Tooselect sorulur hello gerekli bileşenleri yükledikten sonra kullanıcılarınız oturum açma yöntemi tek. Aşağıdaki tablonun hello hello kullanılabilir seçenekler kısa bir açıklamasını sağlar. Merhaba oturum açma yöntemleri tam bir açıklaması için bkz: [kullanıcı oturum açma](active-directory-aadconnect-user-signin.md).

![Kullanıcı Oturumu açma](./media/active-directory-aadconnect-get-started-custom/usersignin2.png)

| Çoklu Oturum Açma Seçeneği | Açıklama |
| --- | --- |
| Parola Eşitleme |Kullanıcılardır mümkün toosign tooMicrosoft bulut Hizmetleri'nde, Office 365 gibi kullanarak hello şirket içi ağlarında kullandıkları aynı parolayı. Parola karması olarak eşitlenmiş tooAzure AD Hello kullanıcı parolaları olan ve hello bulutta kimlik doğrulaması gerçekleşir. Daha fazla bilgi için bkz. [Parola eşitleme](active-directory-aadconnectsync-implement-password-synchronization.md). |
|Doğrudan kimlik doğrulama (Önizleme)|Kullanıcılardır mümkün toosign tooMicrosoft bulut Hizmetleri'nde, Office 365 gibi kullanarak hello şirket içi ağlarında kullandıkları aynı parolayı.  Merhaba kullanıcılar parola toohello şirket içi Active Directory denetleyicisi toobe doğrulanmış geçirilir.
| AD FS ile Federasyon |Kullanıcılardır mümkün toosign tooMicrosoft bulut Hizmetleri'nde, Office 365 gibi kullanarak hello şirket içi ağlarında kullandıkları aynı parolayı.  Merhaba kullanıcılar yönlendirilir tootheir şirket içi AD FS örneği toosign ve şirket içi kimlik doğrulaması gerçekleşir. |
| Yapılandırmayın |Özellik yüklenmez ve yapılandırılmaz. Zaten 3. taraf bir federasyon sunucunuz varsa veya başka bir çözümden faydalanıyorsanız bu seçeneği belirleyin. |
|Çoklu Oturum Açmayı Etkinleştir|Bu seçenekler hem parola eşitleme hem de doğrudan kimlik doğrulama ile kullanılabilir ve çoklu oturum açma hello şirket ağındaki Masaüstü kullanıcılar için deneyimi sağlar.  Daha fazla bilgi için bkz. [Çoklu oturum açma](active-directory-aadconnect-sso.md). </br>Not Çoklu oturum açmanın AD FS teklifleri hello aynı düzeyde zaten AD FS müşteriler için bu seçenek kullanılamaz.</br>(PTA hello yayımlanmamış varsa aynı anda)
|Oturum Açma Seçeneği|Bu seçenekler parola eşitleme müşterileri için kullanılabilir ve çoklu oturum açma hello şirket ağındaki Masaüstü kullanıcılar için deneyimi sağlar.  </br>Daha fazla bilgi için bkz. [Çoklu oturum açma](active-directory-aadconnect-sso.md). </br>Not Çoklu oturum açmanın AD FS teklifleri hello aynı düzeyde zaten AD FS müşteriler için bu seçenek kullanılamaz.


### <a name="connect-tooazure-ad"></a>TooAzure AD connect
Merhaba Bağlan tooAzure AD ekranında bir genel yönetici hesabı ve parolası girin. Seçtiyseniz **AD FS ile Federasyon** hello önceki sayfada oturumu bir etki alanındaki bir hesapla Federasyon tooenable planlayın. Toouse hello varsayılan hesap önerilir **onmicrosoft.com** Azure AD dizini ile birlikte gelen etki alanı.

Bu hesap yalnızca kullanılan toocreate bir Azure AD içinde service hesabıdır ve hello Sihirbaz tamamlandıktan sonra kullanılmaz.  
![Kullanıcı Oturumu açma](./media/active-directory-aadconnect-get-started-custom/connectaad.png)

Genel yönetici hesabınızda MFA etkinse varsa tooprovide hello parolayı tekrar oturum açma hello açılır ve tam hello MFA testini gerekir. bir doğrulama kodu veya bir telefon araması sağlama Hello Çekişme olabilir.  
![MFA’da kullanıcı Oturumu açma](./media/active-directory-aadconnect-get-started-custom/connectaadmfa.png)

Merhaba genel yönetici hesabı da olabilir [Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md) etkin.

Bir hatayla karşılaştıysanız ve bağlantı sorunlarınız varsa bkz. [Bağlantı sorunlarını giderme](active-directory-aadconnect-troubleshoot-connectivity.md).

## <a name="pages-under-hello-section-sync"></a>Eşitleme başlangıç bölümünde sayfaları

### <a name="connect-your-directories"></a>Dizinlerinizi bağlama
tooconnect tooyour Active Directory etki alanı hizmeti, Azure AD Connect hello orman adı ve yeterli izinlere sahip bir hesabın kimlik bilgilerini gerekir.

![Connect Dizini](./media/active-directory-aadconnect-get-started-custom/connectdir01.png)

Merhaba orman adı girerek ve tıkladıktan sonra **Dizin Ekle**, bir açılır iletişim kutusu görüntülenir ve aşağıdaki seçenekleri şu hello ile istenir:

| Seçenek | Açıklama |
| --- | --- |
| Mevcut hesabı kullan | Toobe Azure AD Connect dizin eşitlemesi sırasında toohello AD ormanı bağlanmak için kullanılan tooprovide var olan bir AD DS hesap istiyorsanız bu seçeneği seçin. Merhaba etki alanı bölümünü NetBIOS veya FQDN biçiminde, diğer bir deyişle, FABRIKAM\syncuser veya fabrikam.com\syncuser girebilirsiniz. Bu hesap yalnızca hello varsayılan Okuma izinleri gerektiğinden normal bir kullanıcı hesabı olabilir. Ancak senaryonuza bağlı olarak daha fazla izin gerekebilir. Daha fazla bilgi için bkz. [Azure AD Connect Hesapları ve izinleri](active-directory-aadconnect-accounts-permissions.md#create-the-ad-ds-account). |
| Yeni hesap oluştur | Azure AD Connect Sihirbazı toocreate hello AD DS hesap tarafından Azure AD Connect dizin eşitlemesi sırasında toohello AD ormanı bağlanmak için gerekli istiyorsanız bu seçeneği seçin. Bu seçenek belirlendiğinde, bir kuruluş yöneticisi hesabı için hello kullanıcı adı ve parola girin. Merhaba sağlanan kuruluş yöneticisi hesabı kullanılacak Azure AD Connect tarafından Sihirbazı toocreate hello AD DS hesabı gerekiyor. Merhaba etki alanı bölümünü NetBIOS veya FQDN biçiminde, diğer bir deyişle, ör. fabrıkam\yönetici veya fabrikam.com\administrator girebilirsiniz. |

![Connect Dizini](./media/active-directory-aadconnect-get-started-custom/connectdir02.png)


### <a name="azure-ad-sign-in-configuration"></a>Azure AD oturum açma yapılandırması
Bu sayfa tooreview hello UPN etki alanlarını şirket içi mevcut verir AD DS'de doğrulanmış olup Azure AD içinde. Bu sayfa ayrıca tooconfigure hello özniteliği toouse hello userPrincipalName için sağlar.

![Doğrulanmamış etki alanları](./media/active-directory-aadconnect-get-started-custom/aadsigninconfig.png)  
**Eklenmedi** ve **Doğrulanmadı** olarak işaretlenen tüm etki alanlarını gözden geçirin. Kullandığınız etki alanlarının Azure AD'de doğrulanmış olduğundan emin olun. Etki alanlarınızı doğruladıktan hello Yenile simgesine tıklayın. Daha fazla bilgi için bkz: [hello etki ekleyin ve doğrulayın](../active-directory-add-domain.md)

**UserPrincipalName** -hello özniteliği userPrincipalName özelliği hello özniteliği, kullanıcıların tooAzure AD ve Office 365 oturum açtığınızda kullanın. Merhaba etki alanları kullanıldığında, olarak da bilinen hello UPN soneki, hello kullanıcılar eşitlenmeden önce Azure AD'de doğrulanması gerekir. Microsoft, tookeep hello varsayılan özniteliği userPrincipalName önerir. Bu öznitelik yönlendirilemeyen ve doğrulanamıyor durumunda olası tooselect olan başka bir öznitelik. Merhaba oturum açma kimliğinin bulunduğu hello öznitelik olarak e-posta örneğin seçebilirsiniz userPrincipalName dışında başka bir özniteliğin kullanılmasına **Alternatif kimlik** adı verilir. Merhaba alternatif kimlik öznitelik değeri, RFC822 standart hello izlemeniz gerekir. Alternatif kimlik, hem parola eşitleme ile hem de federasyon ile kullanılabilir.

>[!NOTE]
> Doğrudan kimlik doğrulama etkinleştirdiğinizde, sipariş toocontinue hello Sihirbazı aracılığıyla en az bir doğrulanmış etki alanı olması gerekir.

> [!WARNING]
> Alternatif kimlik kullanımı, hiçbir Office 365 iş yükü ile uyumlu değildir. Daha fazla bilgi için çok başvurun[alternatif oturum açma Kimliğini yapılandırma](https://technet.microsoft.com/library/dn659436.aspx).
>
>

### <a name="domain-and-ou-filtering"></a>Etki alanı ve OU filtreleme
Varsayılan olarak tüm etki alanları ve OU'lar eşitlenir. Bazı etki alanları veya OU'lar toosynchronize tooAzure AD istemediğiniz varsa, bu etki alanları ve OU'lar işaretini kaldırabilirsiniz.  
![DomainOU filtreleme](./media/active-directory-aadconnect-get-started-custom/domainoufiltering.png)  
Bu sayfayı hello Sihirbazı'nda, etki alanı ve OU tabanlı filtreleme yapılandırıyor. Toomake değişiklikleri düşünüyorsanız, daha sonra bkz [etki alanı tabanlı filtreleme](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) ve [ou tabanlı filtreleme](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) bu değişiklikleri yapmadan önce. Bazı kuruluş birimleri hello işlevselliği için gerekli olan ve seçili olmamalıdır.

Azure AD Connect’in 1.1.524.0’dan önceki bir sürümü ile OU tabanlı filtreleme kullanıyorsanız, daha sonra eklenen yeni OU’lar varsayılan olarak eşitlenir. Bu yeni hello davranışı isterseniz OU'lar değil eşitlenmesi gerektiğini sonra ile Merhaba Sihirbaz tamamlandıktan sonra yapılandırabilirsiniz [ou tabanlı filtreleme](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering). Azure AD Connect'i sürüm 1.1.524.0 ya da sonra eşitlenen veya olmayan yeni OU'lar toobe isteyip istemediğinizi belirtebilirsiniz.

Toouse düşünüyorsanız [grup tabanlı filtreleme](#sync-filtering-based-on-groups), hello OU hello grubuyla dahil ve OU filtreleme ile filtrelenmiş değil emin olun. OU filtreleme, grup tabanlı filtrelemeden önce değerlendirilir.

Bazı etki alanlarına toofirewall kısıtlamaları erişilebilir olmayan mümkündür. Bu etki alanları varsayılan olarak seçili değildir ve uyarı içerir.  
![Erişilemeyen etki alanları](./media/active-directory-aadconnect-get-started-custom/unreachable.png)  
Bu uyarıyı görürseniz bu etki alanlarına gerçekten erişilemediğinden ve hello uyarının beklendiğinden emin olun.

### <a name="uniquely-identifying-your-users"></a>Kullanıcılarınızı benzersiz olarak tanımlama

#### <a name="select-how-users-should-be-identified-in-your-on-premises-directories"></a>Şirket içi dizinlerinizde kullanıcıların nasıl tanımlanması gerektiğini seçin
Merhaba ormanlar arasında eşleştirme özelliği, AD DS ormanlardaki kullanıcıların Azure AD'de nasıl temsil edildiğini toodefine sağlar. Bir kullanıcı ya tüm ormanlarda yalnızca bir kez temsil edilebilir ya da etkin ve devre dışı hesapların birleşimine sahip olabilir. Merhaba kullanıcı bazı ormanlarda kişi olarak da temsil edilebilir.

![Benzersiz](./media/active-directory-aadconnect-get-started-custom/unique.png)

| Ayar | Açıklama |
| --- | --- |
| [Kullanıcılar tüm ormanlarda yalnızca bir kez temsil edilir](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |Tüm kullanıcılar Azure AD'de bireysel nesne olarak oluşturulur. Merhaba nesneleri hello meta veri deposunda birleştirilmez. |
| [Posta özniteliği](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |Merhaba posta özniteliğinin farklı ormanlarda aynı değeri hello varsa bu seçeneği kullanıcıları ve kişileri birleştirir. Kişileriniz GALSync kullanılarak oluşturulduysa bu seçeneği kullanın. Bu seçeneği seçilirse, kullanıcı nesnelerini değil, posta özniteliğinin doldurulmuş eşitlenmiş tooAzure AD olmaz. |
| [ObjectSID ve msExchangeMasterAccountSID/ msRTCSIP-OriginatorSid](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |Bu seçenek, hesap ormanındaki etkin bir kullanıcıyla kaynak ormandaki devre dışı bırakılmış bir kullanıcıyı birleştirir. Bu yapılandırma, Exchange'de bağlı posta kutusu olarak bilinir. Bu seçenek, yalnızca Lync'i kullanıyor ve Exchange hello kaynak ormanında değilse kullanılabilir. |
| sAMAccountName ve MailNickName |Bu seçenek hello kullanıcı bulunabilir beklenen hello oturum açma kimliği olduğu özniteliklerinde birleştirir. |
| Belirli bir öznitelik |Bu seçenek, tooselect tanır kendi özniteliği. Bu seçeneği seçilirse, kullanıcı nesnelerini değil (Seçili), öznitelik doldurulmuş eşitlenmiş tooAzure AD olmaz. **Sınırlama:** zaten hello meta veri deposunda bulunan bir öznitelik emin toopick olun. Özel bir öznitelik (değil hello meta veri deposunda) seçerseniz hello sihirbaz tamamlanamaz. |

#### <a name="select-how-users-should-be-identified-with-azure-ad---source-anchor"></a>Azure AD - Kaynak Bağlantısı ile kullanıcıların nasıl tanımlanması gerektiğini seçin
Merhaba özniteliği sourceAnchor hello bir kullanıcı nesnesinin ömrü boyunca sabit olan bir özniteliktir. Bunu Azure AD içinde hello şirket içi kullanıcı hello kullanıcıyla bağlama hello birincil anahtardır.

| Ayar | Açıklama |
| --- | --- |
| Benim için Hello kaynak bağlantısı yönetmek Azure sağlar | Sizin için Azure AD toopick hello özniteliği istiyorsanız bu seçeneği seçin. Bu seçeneği belirlerseniz, Azure AD Connect Sihirbazı makale bölümünde açıklanan hello sourceAnchor özniteliği seçim mantığı uygular [Azure AD Connect: tasarım kavramları - sourceAnchor msDS-ConsistencyGuid kullanarak](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor). Başlangıç Sihirbazı'nı özel yükleme tamamlandıktan sonra hangi öznitelik hello kaynak bağlantısı özniteliği olarak çekilen bildirir. |
| Belirli bir öznitelik | Varolan bir AD özniteliği hello sourceAnchor özniteliği olarak toospecify istiyorsanız bu seçeneği belirleyin. |

Merhaba öznitelik değiştirilemeyeceği için iyi özniteliği toouse planlamanız gerekir. ObjectGUID iyi bir seçenektir. Merhaba kullanıcı hesabı ormanlar/etki alanları arasında taşınmadığı sürece bu öznitelik değiştirilmez. Burada hesapları ormanlar arasında taşıdığınız Çoklu orman ortamında başka bir öznitelik, bir öznitelik hello EmployeeID ile gibi kullanılmalıdır. Bir kişi evlendiğinde değişecek olan veya atamaları değiştirecek olan öznitelikleri kullanmaktan kaçının. @-sign içeren nitelikleri kullanamazsınız. Bu nedenle e-posta ve userPrincipalName seçeneği kullanılamaz. Merhaba özniteliktir ayrıca büyük küçük harfe duyarlı bir nesneyi ormanlar arasında taşıdığınızda, bu nedenle emin toopreserve hello büyük/küçük harfleri olun. İkili öznitelikler base64 kodludur ancak diğer öznitelik türleri kodlanmamış durumda kalır. Federasyon senaryolarında ve bazı Azure AD arabirimlerinde, bu öznitelik immutableID özniteliği olarak da bilinir. Hello hello kaynak bağlantısı hakkında daha fazla bilgi bulunabilir [tasarım kavramları](active-directory-aadconnect-design-concepts.md#sourceanchor).

### <a name="sync-filtering-based-on-groups"></a>Grup tabanlı eşitleme filtrelemesi
Grup filtreleme özelliği hello bir pilot için yalnızca küçük bir alt nesnelerin toosync sağlar. toouse bu özelliği, şirket içi Active Directory'de bu amaç için bir grup oluşturun. Ardından kullanıcıların ve grupların doğrudan üyeleri olarak eşitlenmiş tooAzure AD olmalıdır ekleyin. Daha sonra Ekle ve kullanıcıların toothis Grup toomaintain hello Azure AD'de mevcut olması gereken nesnelerin listesini kaldırın. Toosynchronize istediğiniz tüm nesnelerin doğrudan hello grubunun üyesi olması gerekir. Tüm kullanıcılar, gruplar, kişiler ve bilgisayarlar/cihazlar doğrudan üye olmalıdır. İç içe geçmiş grup üyelikleri çözümlenmez. Yalnızca hello grup kendi üyesi eklendiği bir grup eklediğinizde ve; üyeleri eklenmez.

![Eşitleme Filtreleme](./media/active-directory-aadconnect-get-started-custom/filter2.png)

> [!WARNING]
> Bu özellik yalnızca hedeflenen toosupport pilot dağıtımı olur. Bu özelliği tam gelişmiş üretim dağıtımında kullanmayın.
>
>

Bir özelliği tam gelişmiş üretim dağıtımında, toobe sabit toomaintain tüm nesneleri toosynchronize ile tek bir grup geçiyor. Merhaba yöntemlerden birini kullanmalısınız [filtreleme yapılandırma](active-directory-aadconnectsync-configure-filtering.md).

### <a name="optional-features"></a>İsteğe Bağlı Özellikler
Bu ekran, belirli senaryolarınız için tooselect hello isteğe bağlı özellikler sağlar.

![İsteğe bağlı özellikler](./media/active-directory-aadconnect-get-started-custom/optional.png)

> [!WARNING]
> Şu anda DirSync veya Azure AD eşitleme etkinse varsa, Azure AD CONNECT'te hello geri yazma özelliklerinden herhangi birini etkinleştirmeyin.
>
>

| İsteğe Bağlı Özellikler | Açıklama |
| --- | --- |
| Exchange Karma Dağıtımı |Merhaba Exchange karma dağıtımı özelliği hello arada çalışmasını Exchange posta kutuları için her iki şirket içi sağlar ve Office 365'te. Azure AD Connect, Azure AD'den belirli bir [öznitelikler](active-directory-aadconnectsync-attributes-synchronized.md#exchange-hybrid-writeback) kümesini şirket içi dizininize geri eşitler. |
| Exchange Posta Ortak Klasörleri | Merhaba Exchange posta ortak klasörleri özelliği toosynchronize posta özellikli şirket içi Active Directory tooAzure AD ortak klasör nesnelerden sağlar. |
| Azure AD uygulaması ve öznitelik filtreleme |Azure AD uygulaması ve öznitelik filtrelemesini etkinleştirerek hello eşitlenen öznitelikler kümesi uyarlanabilir. Bu seçenek iki daha fazla yapılandırma sayfaları toohello Sihirbazı ekler. Daha fazla bilgi için bkz. [Azure AD uygulaması ve öznitelik filtreleme](#azure-ad-app-and-attribute-filtering). |
| Parola eşitleme |Ardından federasyon hello oturum açma çözümü olarak seçtiyseniz, bu seçeneği etkinleştirebilirsiniz. Bu durumda parola eşitleme, bir yedekleme seçeneği olarak kullanılabilir. Ek bilgi için bkz. [Parola eşitleme](active-directory-aadconnectsync-implement-password-synchronization.md). </br></br>Doğrudan kimlik doğrulama seçtiyseniz bu seçeneği eski istemcileri ve yedekleme seçeneği olarak tooensure destek varsayılan olarak etkindir. Ek bilgi için bkz. [Parola eşitleme](active-directory-aadconnectsync-implement-password-synchronization.md).|
| Parola geri yazma |Parola geri yazmayı etkinleştirerek Azure AD'de gerçekleşen parola değişiklikleri geri yazılır tooyour şirket içi dizin. Daha fazla bilgi için bkz. [Parola yönetimine başlarken](../active-directory-passwords-getting-started.md). |
| Grup geri yazma |Merhaba kullanırsanız **Office 365 grupları** özelliği, şirket içi Active Directory'de temsil bu gruplara sahip. Bu seçenek yalnızca şirket içi Active Directory'nizde Exchange varsa kullanılır. Daha fazla bilgi için bkz. [Grup geri yazma](active-directory-aadconnect-feature-preview.md#group-writeback). |
| Cihaz geri yazma |Azure AD tooyour şirket içi koşullu erişim senaryoları için Active Directory toowriteback aygıt nesneleri sağlar. Daha fazla bilgi için bkz. [Azure AD Connect'te cihaz geri yazma özelliğini etkinleştirme](active-directory-aadconnect-feature-device-writeback.md). |
| Dizin genişletme öznitelik eşitlemesi |Dizin genişletme öznitelik eşitlemesi etkinleştirerek belirtilen öznitelikler eşitlenen tooAzure AD bağlıdır. Daha fazla bilgi için bkz. [Dizin genişletmeleri](active-directory-aadconnectsync-feature-directory-extensions.md). |

### <a name="azure-ad-app-and-attribute-filtering"></a>Azure AD uygulaması ve öznitelik filtreleme
Hangi özniteliklerin toosynchronize tooAzure AD, ardından başlatmak, kullanmakta olduğunuz hizmetleri seçerek toolimit istiyorsanız. Bu sayfada yapılandırma değişiklikleri yaparsanız, yeni bir hizmet açıkça hello yükleme sihirbazını yeniden çalıştırarak seçilen toobe sahiptir.

![İsteğe bağlı özellikler Uygulamalar](./media/active-directory-aadconnect-get-started-custom/azureadapps2.png)

Merhaba önceki adımda seçtiğiniz hello Hizmetleri bağlı olarak, bu sayfayı eşitlenen tüm öznitelikleri gösterir. Bu liste, eşitlenmekte olan tüm nesne türlerinin birleşimidir. Varsa toonot gereken bazı öznitelikler eşitleme özniteliklerle işaretini kaldırabilirsiniz.

![İsteğe bağlı özellikler Öznitelikler](./media/active-directory-aadconnect-get-started-custom/azureadattributes2.png)

> [!WARNING]
> Özniteliklerin kaldırılması, işlevselliği etkileyebilir. En iyi yöntemler ve öneriler için bkz. [eşitlenen öznitelikler](active-directory-aadconnectsync-attributes-synchronized.md#attributes-to-synchronize).
>
>

### <a name="directory-extension-attribute-sync"></a>Dizin Genişletme öznitelik eşitlemesi
Kuruluşunuz veya Active Directory'deki diğer özniteliklerle tarafından eklenen özel özniteliklere sahip Azure AD'de hello şemasını genişletebilirsiniz. toouse bu özellik, select **dizin genişletme öznitelik eşitlemesi** hello üzerinde **isteğe bağlı özellikler** sayfası. Bu sayfada daha fazla öznitelikleri toosync seçebilirsiniz.

![Dizin genişletmeleri](./media/active-directory-aadconnect-get-started-custom/extension2.png)

Daha fazla bilgi için bkz. [Dizin genişletmeleri](active-directory-aadconnectsync-feature-directory-extensions.md).

### <a name="enabling-single-sign-on-sso"></a>Çoklu oturum açmayı (SSO) etkinleştirme
Çoklu oturum açma kullanmak için parola eşitleme ya da doğrudan kimlik doğrulaması ile yapılandırma, yalnızca toocomplete kez eşitlenmiş tooAzure AD yüklenmekte olan her bir orman için gerektiği basit bir işlemdir. Yapılandırma aşağıdaki iki adımdan oluşur:

1.  Şirket içi Active Directory Hello gerekli bilgisayar hesabı oluşturun.
2.  Merhaba intranet bölgesine toosupport tek oturum açma hello istemci makinelerin yapılandırın.

#### <a name="create-hello-computer-account-in-active-directory"></a>Active Directory'de Hello bilgisayar hesabı oluşturma
Azure AD Connect eklenen her bir orman için böylece her ormanda Hello bilgisayar hesabı oluşturulabilir toosupply etki alanı yönetici kimlik bilgileri gerekir. Hello kimlik bilgileri yalnızca kullanılan toocreate hello hesabı olan ve olmayan depolanan veya başka bir işlem için kullanılan. Merhaba kimlik bilgileri hello eklemeniz yeterlidir **etkinleştirmek tek oturum açma** gösterildiği gibi hello Azure AD Connect Sihirbazı sayfasında:

![Çoklu oturum açmayı etkinleştirme](./media/active-directory-aadconnect-get-started-custom/enablesso.png)

>[!NOTE]
>Bu orman ile toouse çoklu oturum açma istemiyorsanız, belirli bir ormandaki atlayabilirsiniz.

#### <a name="configure-hello-intranet-zone-for-client-machines"></a>Merhaba Intranet istemci makineleri için yapılandırma
Merhaba istemci oturum açma işlemleri hello intranet otomatik olarak, bölge tooensure iki URL'leri hello intranet bölgesinin bir parçası olduğunu tooensure gerekir. Bu, o hello etki alanına katılmış bilgisayara otomatik olarak Kerberos bileti tooAzure bağlı toohello kurumsal ağ olduğunda AD gönderir sağlar.
Bir bilgisayarda, hello Grup İlkesi yönetim araçlarına sahiptir.

1.  Açık hello Grup İlkesi Yönetimi Araçları
2.  Uygulanan tooall kullanıcılar hello Grup İlkesi düzenleyin. Örneğin, varsayılan etki alanı ilkesi hello.
3.  Çok gidin**Kullanıcı Yapılandırması\Yönetim Şablonları\Windows Bileşenleri\Internet Explorer\Internet Denetim Panel\Security sayfası** seçip **tooZone ataması listesi Site** hello görüntü başına Aşağıda.
4.  Merhaba ilkesini etkinleştirmek ve iki öğe hello iletişim kutusunda aşağıdaki hello girin.

        Value: `https://autologon.microsoftazuread-sso.com`  
        Data: 1  
        Value: `https://aadg.windows.net.nsatc.net`  
        Data: 1

5.  Benzer toohello aşağıdaki gibi görünmelidir:  
![Intranet Bölgeleri](./media/active-directory-aadconnect-get-started-custom/sitezone.png)

6.  İki kez **Tamam**'a tıklayın.

## <a name="configuring-federation-with-ad-fs"></a>AD FS ile federasyonu yapılandırma
Azure AD Connect ile AD FS'yi yalnızca birkaç tıklama ile kolayca yapılandırabilirsiniz. Merhaba aşağıdaki önce hello yapılandırma gerekli değildir.

* Merhaba Federasyon sunucusu uzaktan yönetimi etkinleştirilmiş bir Windows Server 2012 R2 sunucusu
* Uzaktan Yönetimi etkinleştirilmiş hello Web uygulaması Ara sunucusu için bir Windows Server 2012 R2 sunucusu
* Bir SSL sertifikası hello Federasyon hizmet adı (örneğin sts.contoso.com) toouse düşündüğünüz

### <a name="ad-fs-configuration-pre-requisites"></a>AD FS yapılandırması önkoşulları
tooconfigure AD FS Azure AD Connect'i kullanarak grubu, WinRM hello uzak sunucularda etkin emin olun. Ayrıca, listelenen hello bağlantı noktaları gereksinimlerini Git [Tablo 3 - Azure AD Connect ve Federasyon sunucuları/WAP](active-directory-aadconnect-ports.md#table-3---azure-ad-connect-and-ad-fs-federation-serverswap).

### <a name="create-a-new-ad-fs-farm-or-use-an-existing-ad-fs-farm"></a>Yeni bir AD FS grubu oluşturma veya var olan bir AD FS grubunu kullanma
Mevcut bir AD FS grubunu kullanabilir veya yeni bir AD FS grubunu toocreate seçebilirsiniz. Yeni bir tane toocreate seçerseniz, gerekli tooprovide hello SSL sertifikasıdır. Merhaba SSL sertifikası bir parolayla korunuyorsa hello parolası istenir.

![AD FS Grubu](./media/active-directory-aadconnect-get-started-custom/adfs1.png)

Mevcut bir AD FS grubunu toouse seçerseniz, doğrudan Merhaba ekranında AD FS ile Azure AD arasında güven ilişkisi yapılandırma toohello alınır.

### <a name="specify-hello-ad-fs-servers"></a>Merhaba AD FS sunucularını belirtme
AD FS tooinstall istediğiniz hello sunucuları girin. Kapasite planlama gereksinimlerinize göre bir veya daha fazla sunucu ekleyebilirsiniz. Bu yapılandırmayı gerçekleştirmeden önce tüm sunucuları tooActive dizin ekleyin. Microsoft, test ve pilot dağıtımlar için tek bir AD FS sunucusunun yüklenmesini önerir. Ardından ekleyin ve yeniden ilk yapılandırmadan sonra Azure AD Connect çalıştırarak, ölçeklendirme gereksinimlerinizi daha fazla sunucuları toomeet dağıtın.

> [!NOTE]
> Bu yapılandırmayı geçekleştirmeden önce tüm sunucularınızın etki alanına katılmış tooan AD alanı olduğundan emin olun.
>
>

![AD FS Sunucuları](./media/active-directory-aadconnect-get-started-custom/adfs2.png)

### <a name="specify-hello-web-application-proxy-servers"></a>Merhaba Web uygulaması Proxy sunucuları belirtin
Web uygulaması Ara sunucusu olarak istediğiniz hello sunucuları girin. Merhaba web uygulaması Ara sunucusu, çevre ağınızda (extranete yönelik) dağıtılır ve hello extranet kimlik doğrulama isteklerini destekler. Kapasite planlama gereksinimlerinize göre bir veya daha fazla sunucu ekleyebilirsiniz. Microsoft, test ve pilot dağıtımlar için tek bir Web uygulaması ara sunucusunun yüklenmesini önerir. Ardından ekleyin ve yeniden ilk yapılandırmadan sonra Azure AD Connect çalıştırarak, ölçeklendirme gereksinimlerinizi daha fazla sunucuları toomeet dağıtın. Merhaba intranet proxy sunucular toosatisfy kimlik, aynı sayıda olması önerilir.

> [!NOTE]
> <li> Sonra kullandığınız hello hesabı hello AD FS sunucularında yerel yönetici değilse yönetici kimlik bilgileri istenir.</li>
> <li> Bu adımı gerçekleştirmeden önce hello Azure AD Connect sunucusu ve hello Web uygulaması Ara sunucusu arasında HTTP/HTTPS bağlantısının olduğundan olun.</li>
> <li> Merhaba AD FS sunucu tooallow kimlik doğrulama isteklerini tooflow aracılığıyla hello Web uygulama sunucusu arasında HTTP/HTTPS bağlantısı olduğundan emin olun.</li>
>

![Web Uygulaması](./media/active-directory-aadconnect-get-started-custom/adfs3.png)

Merhaba web uygulama sunucusu güvenli bağlantı toohello AD FS sunucu belirleyebilmesi için istendiğinde tooenter kimlik bilgileridir. Bu kimlik bilgileri toobe hello AD FS sunucusunda yerel yönetici gerekir.

![Ara sunucu](./media/active-directory-aadconnect-get-started-custom/adfs4.png)

### <a name="specify-hello-service-account-for-hello-ad-fs-service"></a>Merhaba hello AD FS hizmeti için hizmet hesabı belirtin
Merhaba AD FS hizmeti gerektiren bir etki alanı hizmet hesabı tooauthenticate kullanıcılar ve kullanıcı bilgilerini Active Directory'de. AD FS hizmeti, iki hizmet hesabı türünü destekler:

* **Grup Tarafından Yönetilen Hizmet Hesabı** - Windows Server 2012'de Active Directory Etki Alanı Hizmetleri ile birlikte kullanıma sunuldu. Bu hesap türü, AD FS, düzenli olarak tooupdate hello hesap parolaya gerek kalmadan tek bir hesap gibi hizmetleri sağlar. AD FS sunucularınızın ait hello etki alanında Windows Server 2012 etki alanı denetleyicileri zaten varsa bu seçeneği kullanın.
* **Etki alanı kullanıcı hesabı** -hello parola değiştiğinde veya süresi dolduğunda bu hesap türü, tooprovide bir parola ve düzenli olarak güncelleştirmeyi hello parola gerektirir. Yalnızca, Windows Server 2012 etki alanı denetleyicileri AD FS sunucularınızın ait hello etki alanında olmadığında bu seçeneği kullanın.

Grup Tarafından Yönetilen Hizmet Hesabı'nı seçtiyseniz ve bu özellik Active Directory'de hiç kullanılmadıysa Kuruluş Yöneticisi kimlik bilgilerini girmeniz istenir. Bu kimlik bilgileri kullanılan tooinitiate hello anahtar deposu ve Active Directory'de hello özelliğini etkinleştirin.

> [!NOTE]
> Merhaba AD FS hizmeti zaten hello etki alanındaki bir SPN kaydedilmişse azure AD Connect onay toodetect gerçekleştirir.  AD DS aynı anda kayıtlı yinelenen SPN'ın toobe izin vermez.  Yinelenen SPN bulunursa, hello SPN kaldırılana kadar daha fazla mümkün tooproceed olmaz.

![AD FS Hizmet Hesabı](./media/active-directory-aadconnect-get-started-custom/adfs5.png)

### <a name="select-hello-azure-ad-domain-that-you-wish-toofederate"></a>Toofederate istediğiniz hello Azure AD etki alanını seçin
Bu yapılandırma kullanılan toosetup hello Federasyon AD FS ile Azure AD arasındaki ilişkidir. AD FS tooissue güvenlik belirteçleri tooAzure AD yapılandırır ve bu belirli AD FS örneğinden Azure AD tootrust hello belirteçleri yapılandırır. Bu sayfa yalnızca tooconfigure hello ilk yüklemede tek bir etki alanı sağlar. Daha sonra Azure AD Connect'i tekrar çalıştırarak daha fazla etki alanını yapılandırabilirsiniz.

![Azure AD Etki Alanı](./media/active-directory-aadconnect-get-started-custom/adfs6.png)

### <a name="verify-hello-azure-ad-domain-selected-for-federation"></a>Federasyon için seçili hello Azure AD etki alanını doğrulayın
Federe hello etki alanı toobe seçtiğinizde, Azure AD Connect, gerekli bilgileri tooverify ile doğrulanmamış bir etki alanını sağlar. Bkz: [Ekle ve hello etki alanını doğrulayın](../active-directory-add-domain.md) nasıl toouse bu bilgileri.

![Azure AD Etki Alanı](./media/active-directory-aadconnect-get-started-custom/verifyfeddomain.png)

> [!NOTE]
> AD Connect çalıştığında tooverify hello etki hello sırasında aşama yapılandırın. Tooconfigure hello gerekli DNS kayıtlarını eklemeden devam ederseniz, Başlangıç Sihirbazı'nı mümkün toocomplete hello yapılandırma değil.
>
>

## <a name="configure-and-verify-pages"></a>Yapılandırma ve doğrulama sayfaları
Merhaba yapılandırma bu sayfada gerçekleşir.

> [!NOTE]
> Federasyonu yapılandırdıysanız ve yüklemeye devam etmek istiyorsanız [Federasyon sunucuları için ad çözümlemesi](active-directory-aadconnect-prerequisites.md#name-resolution-for-federation-servers) yapılandırmasını tamamladığınızdan emin olun.
>
>

![Hazır tooconfigure](./media/active-directory-aadconnect-get-started-custom/readytoconfigure2.png)

### <a name="staging-mode"></a>Hazırlama modu
Bu, olası toosetup hazırlama modu ile paralel olarak yeni bir eşitleme sunucusu olur. Merhaba bulut tooone dizininde dışa aktarma yalnızca desteklenen toohave bir eşitleme sunucusu var. Ancak başka bir sunucudan, örneğin, çalışan bir Dirsync'ten toomove istiyorsanız, Azure AD Connect'i hazırlama modunda etkinleştirebilirsiniz. Etkinleştirildiğinde, hello eşitleme altyapısı alma ve verileri normal olarak eşitleme, ancak hiçbir şey vermez tooAzure AD veya AD. Merhaba, özellikleri parola eşitleme ve parola geri yazma devre dışı bırakılır hazırlama modunda.

![Hazırlama modu](./media/active-directory-aadconnect-get-started-custom/stagingmode.png)

Hazırlama modundayken bu olası toomake gerekli değişiklikleri toohello eşitleme altyapısı ve dışarı toobe hakkında nedir gözden geçirin. Hello yapılandırma iyi göründüğünde, hello Yükleme Sihirbazı'nı yeniden çalıştırın ve hazırlama modunu devre dışı bırakın. Şimdi bu sunucudan dışarı aktarılan tooAzure AD verilerdir. Diğer hello aynı zaman bu nedenle tek bir sunucu etkin olarak dışarı aktarma sunucusunda hello emin toodisable olun.

Daha fazla bilgi için bkz. [Hazırlama modu](active-directory-aadconnectsync-operations.md#staging-mode).

### <a name="verify-your-federation-configuration"></a>Federasyon yapılandırmanızı doğrulama
Merhaba doğrula düğmesine tıkladığınızda azure AD Connect, hello DNS ayarlarını doğrular.

**İntranet bağlantısı denetimleri**

* Federasyon FQDN'yi çözümlemek: hello Federasyon FQDN DNS tooensure bağlantısı tarafından çözülebilir varsa Azure AD Connect denetler. Azure AD Connect hello FQDN'yi çözümleyemiyorsa, hello doğrulama başarısız olur. Bir DNS kaydı hello Federasyon Hizmeti'nde FQDN sipariş toosuccessfully tam hello doğrulama için mevcut olduğundan emin olun.
* DNS A kaydı: Azure AD Connect, federasyon hizmetiniz için bir A kaydı olup olmadığını denetler. Bir A kaydı Hello olmaması durumunda hello doğrulama başarısız olur. Bir Oluştur kaydı ve hello doğrulamayı tamamlamak değil için CNAME kaydı, ' % s'federasyon FQDN sipariş toosuccessfully içinde.

**Extranet bağlantısı denetimleri**

* Federasyon FQDN'yi çözümlemek: hello Federasyon FQDN DNS tooensure bağlantısı tarafından çözülebilir varsa Azure AD Connect denetler.

![Tamamlama](./media/active-directory-aadconnect-get-started-custom/completed.png)

![Doğrulama](./media/active-directory-aadconnect-get-started-custom/adfs7.png)

Ayrıca, hello aşağıdaki doğrulama adımları gerçekleştirin:

* Hello intranet etki alanına katılmış makinede bir tarayıcıdan oturum açabildiğinizi doğrulayın: toohttps://myapps.microsoft.com bağlanmak ve hello oturum açma açtığınız hesabınız ile doğrulayın. Merhaba yerleşik AD DS yönetici hesabı eşitlenmemiş ve doğrulama için kullanılamaz.
* Hello extranet bir CİHAZDAN oturum açabildiğinizi doğrulayın. Bir ana makine veya bir mobil cihaz, toohttps://myapps.microsoft.com bağlanmak ve kimlik bilgilerinizi sağlayın.
* Zengin istemci oturumu açma işlemini doğrulayın. Toohttps://testconnectivity.microsoft.com bağlanma, hello seçin **Office 365** sekmesini ve hello **Office 365 çoklu oturum açma testi**.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba yükleme tamamlandıktan sonra oturumu kapatın ve Eşitleme Hizmeti Yöneticisi'ni veya Synchronization Rule Editor'ı kullanmadan önce tooWindows içinde yeniden oturum açın.

Azure AD Connect'i sahip olduğunuza göre şunları yapabilirsiniz [hello yüklemeyi doğrulayın ve lisansları atama](active-directory-aadconnect-whats-next.md).

Merhaba yüklemeyle etkinleştirilen özellikler hakkında daha fazla bilgi edinin: [yanlışlıkla silmeleri engelleme](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) ve [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).

Bu genel konular hakkında daha fazla bilgi edinin: [Zamanlayıcı ve nasıl tootrigger eşitleme](active-directory-aadconnectsync-feature-scheduler.md).

[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.
