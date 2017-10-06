---
title: "Azure AD Connect: Kullanıcı oturum açma | Microsoft Docs"
description: "Azure AD Connect kullanıcı oturum açma için özel ayarlar."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 547b118e-7282-4c7f-be87-c035561001df
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 7848b419f3855b25cfa074a46779d258bd534bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-user-sign-in-options"></a>Azure AD Connect kullanıcı oturum açma seçenekleri
Aynı parolayı kullanarak şirket içi kaynakları hello ve Azure Active Directory (Azure AD) bağlanma, kullanıcıların toosign tooboth bulutta izin verir. Bu makalede her kimlik modeli toohelp için anahtar kavramlar tooAzure AD imzalamak için toouse istediğiniz hello kimlik seçin.

Zaten hello Azure AD kimlik modeliyle tanıdık ve toolearn belirli bir yöntemi hakkında daha fazla bilgi istiyorsanız hello uygun bağlantıya bakın:

* [Parola Eşitleme](#password-synchronization) ile [çoklu oturum açma (SSO)](active-directory-aadconnect-sso.md)
* [Doğrudan kimlik doğrulama](active-directory-aadconnect-pass-through-authentication.md)
* [Federasyon SSO (ile Active Directory Federasyon Hizmetleri (AD FS))](#federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2)

## <a name="choosing-hello-user-sign-in-method-for-your-organization"></a>Kuruluşunuz için Hello kullanıcı oturum yöntemini seçme
Yalnızca tooenable kullanıcı oturum açma tooOffice 365, SaaS uygulamaları ve diğer Azure AD tabanlı kaynakları istediğiniz çoğu kuruluş için hello varsayılan parola eşitleme seçeneğini öneririz. Bazı kuruluşlar ancak, mümkün toouse olmayan özel bir nedeniniz yoksa bu seçenek. Bunlar ya da bir federe oturum açma seçeneği, AD FS veya doğrudan kimlik doğrulama gibi seçebilirsiniz. Tablo toohelp hello doğru seçim yapmanıza aşağıdaki hello kullanabilirsiniz.

Çok gerekir| PS SSO| PA SSO| AD FS |
 --- | --- | --- | --- |
Yeni kullanıcı, kişi ve grup hesapları şirket içi Active Directory toohello bulutta otomatik olarak eşitle.|x|x|x|
My Kiracı Office 365 karma senaryolar için ayarlayın.|x|x|x|
My kullanıcılar toosign ve erişim bulut Hizmetleri, şirket içi parolalarını kullanarak etkinleştirin.|x|x|x|
Çoklu oturum açma şirket kimlik bilgilerini kullanarak uygular.|x|x|x|
Hiçbir parolaları hello bulutta depolandığından emin olun.||x *|x|
Şirket içi çok faktörlü kimlik doğrulaması çözümleri etkinleştirin.|||x|

* Aracılığıyla basit bir bağlayıcı.

>[!NOTE]
> Doğrudan kimlik doğrulama şu anda Zengin istemci ile bazı sınırlamalar vardır. Bkz: [doğrudan kimlik doğrulama](active-directory-aadconnect-pass-through-authentication.md) daha fazla ayrıntı için.

### <a name="password-synchronization"></a>Parola eşitleme
Parola Eşitleme ile şirket içi Active Directory tooAzure AD kullanıcı parolalarını karmalarını eşitlenir. Parolalar değiştirilir veya şirket içi sıfırlama, kullanıcılarınızın her zaman böylece kullanım hello hemen aynı hello yeni parolalar eşitlenmiş tooAzure AD olan Bulut ve şirket kaynaklarının parolası. Merhaba parolalar hiçbir zaman tooAzure AD gönderilen veya düz metin Azure AD'de depolanabilir. Parola Eşitleme parola geri yazma tooenable Self Servis parola sıfırlama Azure AD ile birlikte kullanabilirsiniz.

Ayrıca, etkinleştirebilirsiniz [SSO](active-directory-aadconnect-sso.md) hello kurumsal ağ üzerindeki etki alanına katılmış makinede kullanıcılar için. Çoklu oturum açma, etkin kullanıcılar ile yalnızca tooenter bulut kaynaklarına güvenle erişmesini bir kullanıcı adı toohelp gerekir.

![Parola eşitleme](./media/active-directory-aadconnect-user-signin/passwordhash.png)

Daha fazla bilgi için bkz: Merhaba [parola eşitleme](active-directory-aadconnectsync-implement-password-synchronization.md) makalesi.

### <a name="pass-through-authentication"></a>Doğrudan kimlik doğrulama
Doğrudan kimlik doğrulama ile Merhaba kullanıcının parolasını hello şirket içi Active Directory denetleyicisine karşı doğrulanır. Merhaba parola toobe herhangi bir biçimde Azure AD'de mevcut gerekmez. Bu oturum açma saatleri kısıtlaması gibi şirket içi ilkeleri için kimlik doğrulama toocloud Hizmetleri sırasında değerlendirilen toobe sağlar.

Doğrudan kimlik doğrulaması, bir Windows Server 2012 R2 etki alanına katılmış makinede hello şirket içi ortamda basit bir aracı kullanır. Bu aracı parola doğrulama isteklerini dinler. Tüm gelen bağlantı noktalarının toobe açık toohello Internet gerektirmez.

Buna ek olarak, çoklu oturum açma hello kurumsal ağ üzerindeki etki alanına katılmış makinede kullanıcılar için de etkinleştirebilirsiniz. Çoklu oturum açma, etkin kullanıcılar ile yalnızca tooenter bulut kaynaklarına güvenle erişmesini bir kullanıcı adı toohelp gerekir.
![Doğrudan kimlik doğrulama](./media/active-directory-aadconnect-user-signin/pta.png)

Daha fazla bilgi için bkz.
- [Doğrudan kimlik doğrulama](active-directory-aadconnect-pass-through-authentication.md)
- [Çoklu oturum açma](active-directory-aadconnect-sso.md)

### <a name="federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2"></a>Windows Server 2012 R2'de AD FS ile yeni veya varolan bir grubu kullanan Federasyon
Federasyon ile oturum açma, kullanıcılarınızın şirket içi parolalarını AD tabanlı hizmetlerle tooAzure imzalayabilirsiniz. Merhaba Kurumsal ağda olup olmadıklarını olsa da, bunlar tooenter bile parolalarını yok. AD FS ile Merhaba Federasyon seçeneğini kullanarak, Windows Server 2012 R2'de AD FS ile yeni veya varolan bir grubu dağıtabilirsiniz. Varolan bir grubu toospecify seçerseniz, Azure AD Connect kullanıcılarınız oturum açarak grubu ve Azure AD arasında güven hello yapılandırır.

<center>![Windows Server 2012 R2 AD FS ile Federasyon](./media/active-directory-aadconnect-user-signin/federatedsignin.png)</center>

#### <a name="deploy-federation-with-ad-fs-in-windows-server-2012-r2"></a>Windows Server 2012 R2'de AD FS ile Federasyon dağıtma

Yeni bir grubu dağıtıyorsanız, gerekir:

* Merhaba Federasyon sunucusu için Windows Server 2012 R2 sunucusu.
* Merhaba Web uygulaması proxy'si için Windows Server 2012 R2 sunucusu.
* Hedeflenen Federasyon Hizmeti adı için bir .pfx dosyası bir SSL sertifikası ile. Örneğin: fs.contoso.com.

Yeni grubu dağıtma ya da varolan bir grubu kullanarak, gerekir:

* Federasyon sunucularınız üzerinde yerel yönetici kimlik bilgileri.
* Bir çalışma grubu sunucuları (olmayan etki alanına katılmış) üzerinde yerel yönetici kimlik bilgilerinin toodeploy amaçladığınız Web Uygulaması Proxy'si rol üzerinde hello.
* Merhaba makine Windows Uzaktan Yönetimi'ni kullanarak AD FS veya Web uygulaması proxy'si tooinstall istediğiniz diğer makinelere toobe mümkün tooconnect tooany üzerinde hello Sihirbazı'nı çalıştırın.

Daha fazla bilgi için bkz: [AD FS yapılandırma SSO'su](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs).

#### <a name="sign-in-by-using-an-earlier-version-of-ad-fs-or-a-third-party-solution"></a>AD FS veya bir üçüncü taraf çözümü önceki bir sürümünü kullanarak oturum açın
Zaten bulut oturum açma (örneğin, AD FS 2.0) AD FS veya üçüncü taraf Federasyon sağlayıcısı önceki bir sürümünü kullanarak yapılandırdıysanız, oturum açma tooskip kullanıcı yapılandırması Azure AD Connect aracılığı seçebilirsiniz. Bu, tooget hello son eşitleme ve diğer özelliklerini Azure AD Connect oturum açma için hala var olan çözümünüzü kullanırken olanak tanır.

Daha fazla bilgi için bkz: Merhaba [Azure AD üçüncü taraf Federasyon Uyumluluğu Listesi](active-directory-aadconnect-federation-compatibility.md).


## <a name="user-sign-in-and-user-principal-name"></a>Kullanıcı oturum açma ve kullanıcı asıl adı
### <a name="understanding-user-principal-name"></a>Anlama kullanıcı asıl adı
Active Directory'de hello varsayılan kullanıcı asıl adı (UPN) sonekini hello DNS hello kullanıcı hesabının oluşturulduğu hello etki alanı adıdır. Çoğu durumda bu hello Internet üzerinde hello kuruluş etki alanı olarak kayıtlı hello etki alanı adıdır. Ancak, Active Directory etki alanları ve Güvenleri'ni kullanarak daha fazla UPN soneki ekleyebilirsiniz.

Merhaba hello kullanıcının UPN'sini sahip hello biçimi username@domain. Örneğin, "contoso.com" adlı bir Active Directory etki alanı için John adlı bir kullanıcı hello UPN olabilir "john@contoso.com". Merhaba hello kullanıcının UPN'sini RFC 822 temel alır. Merhaba UPN ve e-posta paylaşımı ile aynı biçimi hello rağmen bir kullanıcı için UPN hello hello değerini olabilir veya aynı hello e-posta adresi hello kullanıcı olarak hello olmayabilir.

### <a name="user-principal-name-in-azure-ad"></a>Azure AD'de kullanıcı asıl adı
Şirket içi hello kullanıcı asıl adı olarak Azure AD içinde kullanılan özniteliğinde (özel bir yükleme) toobe belirtmenizi sağlar hello veya hello userPrincipalName özniteliği Hello Azure AD Connect Sihirbazı'nı kullanır. Bu tooAzure AD imzalama için kullanılan hello değerdir. Merhaba userPrincipalName özniteliğinin Hello değeri karşılık gelmiyor varsa Azure AD ile bir varsayılan yerini sonra tooa etki alanı Azure AD'de doğrulandı.. onmicrosoft.com değeri.

Azure Active Directory'de her dizin hello biçimi contoso.onmicrosoft.com, Azure veya diğer Microsoft hizmetlerini kullanmaya başlamanıza olanak tanıyan bir yerleşik etki alanı adıyla birlikte gönderilir. Geliştirmek ve özel etki alanlarını kullanarak hello oturum açma deneyimini basitleştirin. Azure AD'de özel etki alanı adları hakkında bilgi için ve nasıl tooverify bir etki alanı bkz [özel etki alanı adı tooAzure Active Directory eklemek](../add-custom-domain.md#add-your-custom-domain).

## <a name="azure-ad-sign-in-configuration"></a>Azure AD oturum açma yapılandırması
### <a name="azure-ad-sign-in-configuration-with-azure-ad-connect"></a>Azure AD oturum açma yapılandırması Azure AD Connect ile
Azure AD hello hello Azure AD dizininde doğrulanır hello özel etki alanlarının eşitlenmiş tooone yüklenmekte olan bir kullanıcının kullanıcı asıl adı soneki olup eşleştirebilirsiniz Hello Azure AD oturum açma deneyimini bağlıdır. Azure AD oturum açma ayarları yapılandırması sırasında azure AD Connect hello kullanıcı oturum açma deneyimi hello bulut benzer toohello şirket içi deneyimidir Yardım sağlar.

Azure AD Connect listeleri hello hello etki alanları ve çalıştığında toomatch için tanımlanan UPN soneki bunları Azure AD'de özel bir etki alanı ile. Ardından gerçekleştirilecek toobe gereken hello uygun eylemiyle yardımcı olur.
Hello Azure AD oturum açma sayfası şirket içi Active Directory için tanımlanan hello UPN soneki listeler ve her sonek karşı hello karşılık gelen durumunu görüntüler. Merhaba durum değerleri hello aşağıdakilerden biri olabilir:

| Durum | Açıklama | Eylem gerekli |
|:--- |:--- |:--- |
| Doğrulandı |Azure AD Connect, eşleşen bir etki alanı Azure AD'de doğrulanmış bulundu. Bu etki alanı için tüm kullanıcıların şirket içi kimlik bilgilerini kullanarak oturum açabilir. |Eylem gerekmiyor. |
| Doğrulanmadı |Azure AD Connect özel eşleşen bir etki alanı Azure AD içinde bulundu, ancak doğrulandı değil. Bu etki alanının hello kullanıcılarının Hello UPN soneki olacaktır değiştirilen toohello varsayılan. onmicrosoft.com sonekini hello etki alanını doğruladıysanız değil, eşitlemeden sonra. | [Merhaba özel etki alanı Azure AD'de doğrulayın.](../add-custom-domain.md#verify-the-domain-name-with-azure-ad) |
| Eklenmedi |Azure AD Connect özel bir etki alanı corresponded toohello UPN soneki bulamadı. Merhaba UPN soneki hello kullanıcılarının bu etki alanı olacaktır değiştirilen toohello varsayılan. onmicrosoft.com sonekini hello etki alanı eklediyseniz değilse ve Azure'da doğrulandı. | [Ekleyin ve toohello UPN soneki karşılık gelen özel bir etki alanını doğrulayın.](../add-custom-domain.md) |

Hello Azure AD oturum açma sayfasında, şirket içi Active Directory için tanımlanır ve Azure AD ile Merhaba geçerli doğrulama durumunu içinde karşılık gelen özel etki alanı hello hello UPN soneki listeler. Özel bir yükleme şimdi hello özniteliği hello hello kullanıcı asıl adı için seçebileceğiniz **Azure AD oturum açma** sayfası.

![Azure AD oturum açma sayfası](./media/active-directory-aadconnect-user-signin/custom_azure_sign_in.png)

Merhaba Yenile düğmesini toore fetch hello son durumunu hello Azure AD'den özel etki alanlarını tıklatabilirsiniz.

### <a name="selecting-hello-attribute-for-hello-user-principal-name-in-azure-ad"></a>Azure AD'de Hello özniteliği hello kullanıcı asıl adı için seçme
Merhaba özniteliği userPrincipalName tooAzure AD ve Office 365 oturum açtığınızda, kullanıcıların kullanan hello özniteliğidir. Merhaba kullanıcılar eşitlenmeden önce Azure AD içinde kullanılan hello etki alanları (UPN soneki olarak da bilinir) doğrulamanız gerekir.

Merhaba varsayılan özniteliği userPrincipalName tutmanızı öneririz. Bu öznitelik nonroutable ise ve olası tooselect ise, doğrulanamıyor oturum açma kimliği hello tutan hello özniteliği olarak başka bir öznitelik (örneğin, eposta) Bu hello alternatif kimliği bilinir Merhaba alternatif kimlik öznitelik değeri hello RFC 822 standart izlemeniz gerekir. Alternatif kimlik, hem parola SSO hem de Federasyon SSO hello oturum açma çözümü olarak kullanabilirsiniz.

> [!NOTE]
> Alternatif kimlik kullanımı tüm Office 365 iş yükü ile uyumlu değil. Daha fazla bilgi için bkz: [alternatif oturum açma Kimliğini yapılandırma](https://technet.microsoft.com/library/dn659436.aspx).
>
>

#### <a name="different-custom-domain-states-and-their-effect-on-hello-azure-sign-in-experience"></a>Farklı bir özel etki alanı durumları ve etkilerini hello Azure oturum açma deneyimi
Merhaba olan UPN soneki tanımlanan şirket içi ve bu çok önemli toounderstand hello Azure AD dizininizdeki hello özel etki alanı durumlar arasındaki ilişkidir. Merhaba farklı olası Azure oturum açma deneyimlerini Azure AD Connect kullanarak eşitleme ayarlama zaman edelim.

Biz hello şirket içi dizininde örneğin UPN--bir parçası olarak kullanılan hello UPN soneki contoso.com ile ilgili aşağıdaki bilgilerle Merhaba varsayalım user@contoso.com.

###### <a name="express-settingspassword-synchronization"></a>Ayarları/parola eşitleme express
| Durum | Azure oturum açma kullanıcı deneyimi üzerinde etkisi |
|:---:|:--- |
| Eklenmedi |Bu durumda, hiçbir özel etki alanı contoso.com hello Azure AD dizininde eklendi. UPN şirket içi hello sonekine sahip kullanıcılar @contoso.com mümkün toouse kendi şirket içi UPN toosign tooAzure içinde olmayacaktır. Bunlar bunun yerine toouse toothem hello varsayılan Azure AD dizini için hello sonek ekleyerek Azure AD tarafından sağlanan yeni bir UPN sahip olacaksınız. Örneğin, kullanıcılar toohello Azure AD directory azurecontoso.onmicrosoft.com eşitleniyor, ardından hello kullanıcı şirket içi user@contoso.com UPN verilen user@azurecontoso.onmicrosoft.com. |
| Doğrulanmadı |Bu durumda, hello Azure AD dizininde eklenen bir özel etki alanı contoso.com sahip. Ancak, henüz doğrulanır. Merhaba etki alanı doğrulamadan kullanıcılar eşitleniyor ile devam edin, ardından hello kullanıcıların yeni UPN Azure AD tarafından atanır, hello senaryo "Eklenmedi" olduğu gibi. |
| Doğrulandı |Bu durumda, zaten eklenmiş olan ve hello için Azure AD'de UPN soneki doğrulanmış bir özel etki alanı contoso.com sahip. Kullanıcıların mümkün toouse şirket içi kullanıcı asıl adına, örneğin olacaktır user@contoso.com, eşitlenen sonra tooAzure toosign tooAzure AD. |

###### <a name="ad-fs-federation"></a>AD FS federasyon
Merhaba varsayılan ile bir Federasyon oluşturulamıyor. onmicrosoft.com etki alanı Azure AD'de veya doğrulanmamış özel etki alanı Azure AD'de. Doğrulanmamış etki alanı toocreate seçerseniz zaman hello Azure AD Connect Sihirbazı, bir Federasyon ile çalıştırdığınız ardından Azure AD Connect ister hello gerekli sizinle hello etki alanı için DNS sunucunuzun barındırıldığı oluşturulan toobe kaydeder. Daha fazla bilgi için bkz: [Federasyon için seçili hello Azure AD etki alanını doğrula](active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation).

Merhaba kullanıcı oturum açma seçeneğini seçtiyseniz, **AD FS ile Federasyon**, sonra da Azure AD'de bir Federasyon oluşturma bir özel etki alanı toocontinue olması gerekir. Bizim hakkında bilgi için bu hello Azure AD dizininde eklenen bir özel etki alanı contoso.com olmalıdır anlamına gelir.

| Durum | Hello Azure oturum açma kullanıcı deneyimi üzerinde etkisi |
|:---:|:--- |
| Eklenmedi |Bu durumda, Azure AD Connect hello UPN soneki contoso.com hello Azure AD dizini için eşleşen bir özel etki alanı bulunamadı. Kendi şirket içi UPN ile AD FS kullanarak kullanıcıların toosign gerekiyorsa tooadd özel etki alanı contoso.com gerekir (gibi user@contoso.com). |
| Doğrulanmadı |Bu durumda, Azure AD Connect, daha sonraki bir aşamada etki alanınızın nasıl doğrulayabilirsiniz üzerinde uygun ayrıntılarla ister. |
| Doğrulandı |Bu durumda, başka bir eylem olmadan hello yapılandırmasıyla devam gidebilirsiniz. |

## <a name="changing-hello-user-sign-in-method"></a>Değişen hello kullanıcı oturum açma yöntemi
Merhaba hello Sihirbazı'nı kullanarak Azure AD Connect ilk yapılandırmadan sonra Azure AD Connect içinde kullanılabilir hello görevlerini kullanarak, Federasyon, parola eşitleme ya da doğrudan kimlik doğrulama hello kullanıcı oturum açma yöntemi değiştirebilirsiniz. Hello Azure AD Connect Sihirbazı'nı yeniden çalıştırın ve gerçekleştirebileceğiniz görevlerin bir listesi görürsünüz. Seçin **değiştirme kullanıcı oturum açma** görevleri hello listesinden.

![Kullanıcı oturum açma değiştirme](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

Merhaba sonraki sayfada, Azure AD için tooprovide hello kimlik bilgileri sorulur.

![TooAzure AD connect](./media/active-directory-aadconnect-user-signin/changeusersignin2.png)

Merhaba üzerinde **kullanıcı oturum açma** sayfasında, istenen hello kullanıcı oturum açma seçin.

![TooAzure AD connect](./media/active-directory-aadconnect-user-signin/changeusersignin2a.png)

> [!NOTE]
> Bir geçici geçiş toopassword eşitleme yalnızca yapıyorsanız hello seçin **kullanıcı hesapları dönüştürmez** onay kutusu. Merhaba seçenek işaretlendiğinde değil her kullanıcı toofederated dönüştürür ve birkaç saat sürebilir.
>
>

## <a name="next-steps"></a>Sonraki adımlar
- Daha fazla bilgi edinmek [şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md).
- Daha fazla bilgi edinmek [Azure AD Connect tasarım kavramları](active-directory-aadconnect-design-concepts.md).
