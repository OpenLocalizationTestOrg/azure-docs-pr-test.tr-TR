---
title: aaaAzure Active Directory ile ilgili SSS | Microsoft Docs
description: "Azure Active Directory ile ilgili SSS tooaccess Azure ve Azure Active Directory, parola yönetimi ve uygulama nasıl erişim sorular yanıtlanmaktadır."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: b8207760-9714-4871-93d5-f9893de31c8f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/16/2017
ms.author: markvi
ms.openlocfilehash: 63c30c4aeda4551bf02c6b968f98cded5a3b2c16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-faq"></a>Azure Active Directory ile ilgili SSS
Azure Active Directory (Azure AD), kimlik, erişim yönetimi ve güvenliği tüm yönleriyle kapsayan bir hizmet olarak kimlik (IDaaS) çözümüdür.

Daha fazla bilgi için bkz. [Azure Active Directory nedir?](active-directory-whatis.md).


## <a name="access-azure-and-azure-active-directory"></a>Azure ve Azure Active Directory erişimi
**Merhaba Klasik Azure portalı, Azure AD tooaccess çalıştığımda neden "abonelik bulunamadı" sağlarım?**

**Y:** tooaccess Merhaba Klasik Azure portalı, her bir kullanıcı Azure aboneliği ile izinleri olması gerekir. Ücretli bir Azure AD ve Office 365 aboneliği varsa, çok gidin[http://aka.ms/accessAAD](http://aka.ms/accessAAD) bir kerelik etkinleştirme adımı için. Aksi durumda, tooactivate ücretsiz gerekir [Azure hesabı](https://azure.microsoft.com/pricing/free-trial/) veya Ücretli abonelik.

Daha fazla bilgi için bkz.

* [Azure aboneliklerinin Azure Active Directory ile ilişkisi](active-directory-how-subscriptions-associated-directory.md)
* [Azure'da Office 365 aboneliğinize Hello dizini yönetme](active-directory-manage-o365-subscription.md)

- - -
**S: Azure AD arasındaki hello ilişki nedir Office 365 ve Azure?**

**Y:** Azure AD, ortak kimlik ve erişim yetenekleri ile tooall web hizmetleri sağlar. Office 365, Microsoft Azure, Intune veya diğer, size, kullanıp kullanmadığınızı olduğunuz zaten Azure AD toohelp kullanarak aç Bu hizmetler için oturum açma ve erişim yönetimi.

Toouse web hizmetlerini ayarlama tüm kullanıcılar, bir veya daha fazla Azure AD örneğinde kullanıcı hesapları olarak tanımlanır. Bulut uygulama erişimi gibi ücretsiz Azure AD özellikleri için bu hesapları ayarlayabilirsiniz.

Enterprise Mobility + Security gibi ücretli Azure AD hizmetleri, kurumsal ölçekte kapsamlı yönetim ve güvenlik çözümleriyle Office 365 ve Microsoft Azure gibi diğer web hizmetlerini tamamlar.
- - -
**Neden ı toohello Azure portalında oturum ancak klasik Azure portalı hello değil mi?**

**Y:** hello Azure portal geçerli bir abonelik gerektirmez ve hello Klasik portal geçerli bir abonelik gerektirir.  Bir abonelik yoksa da toohello Klasik Portalı'nda oturum açamazsınız.
- - -
**S: hello farklarını Abonelik Yöneticisi ve dizin Yöneticisi nelerdir?**

**Y:** varsayılan olarak, Azure için kaydolduğunuzda hello Abonelik Yöneticisi rolü atanır. Abonelik Yöneticisi bir Microsoft hesabı ya da bir iş kullanabilir veya Okul hesabı Azure aboneliği hello hello dizininden ile ilişkilidir.  Bu rol hello Azure portal yetkili toomanage Hizmetleri'nde değildir.

Diğerleri de toosign gerekir ve Hizmetleri tarafından erişirseniz, Merhaba aynı aboneliği kullanarak, ortak yöneticileri ekleyebilirsiniz. Bu rol hello sahip aynı erişim ayrıcalıkları hello Hizmet Yöneticisi, ancak abonelikleri tooAzure dizinleri hello ilişkisini değiştiremezsiniz.  Abonelik yöneticileri hakkında ek bilgi için bkz: [nasıl tooadd ya da değişiklik Azure yönetici rolleri](../billing-add-change-azure-subscription-administrator.md) ve [Azure aboneliklerinin Azure Active Directory ile ilişkili](active-directory-how-subscriptions-associated-directory.md).


Azure AD'de yönetici rolleri toomanage hello dizin ve kimlik güvenlikle ilgili özellikler farklı kümesi vardır.  Bu yöneticileri erişim toovarious özelliğiniz hello Azure portalında veya Klasik Azure portalı hello. Hello Yöneticisi'nin rol, oluşturmak veya kullanıcıları Düzenle, yönetici rollerini tooothers ata, kullanıcı parolalarını sıfırlama, kullanıcı lisanslarını yönetme veya etki alanlarını yönetme gibi yapabileceklerini belirler.  Azure AD dizin yöneticileri ve rolleri hakkında daha fazla bilgi için bkz. [Azure Active Directory’de yönetici rolü atama](active-directory-assign-admin-roles.md).

Ayrıca, Enterprise Mobility + Security gibi ücretli Azure AD hizmetleri, kurumsal ölçekte kapsamlı yönetim ve güvenlik çözümleriyle Office 365 ve Microsoft Azure gibi diğer web hizmetlerini tamamlar.

- - -
**S: Azure AD kullanıcı lisanslarımın ne zaman sona ereceğini gösteren bir rapor var mı?**

**C:** Hayır.  Bu özellik şu an kullanılamıyor.

- - -

## <a name="get-started-with-hybrid-azure-ad"></a>Karma Azure AD ile çalışmaya başlama


**S: Ortak çalışan olarak eklendiğimde kiracıdan nasıl ayrılabilirim?**

**Y:** tooanother kuruluşunuzun Kiracı ortak çalışanı eklendiğinde, hello "Kiracı değiştirici" Merhaba üst sağ tooswitch, kiracılar arasında kullanabilirsiniz.  Şu anda, kuruluş davet hiçbir şekilde tooleave hello yoktur ve Microsoft bu işlevselliği sağlayan üzerinde çalışmaktadır.  Bu özellik kullanılabilir oluncaya kadar kuruluş tooremove davet hello sorabileceğiniz kendi Kiracı sizden.
- - -
**S: my şirket içi dizin tooAzure AD nasıl bağlanabilir miyim?**

**Y:** Azure AD Connect kullanarak şirket içi dizin tooAzure AD bağlanabilirsiniz.

Daha fazla bilgi için bkz. [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md).

- - -
**S: Şirket içi dizinim ve bulut uygulamalarım arasında SSO'yu nasıl ayarlarım?**

**Y:** çoklu oturum açma (SSO) şirket içi dizin ve Azure AD arasındaki yukarı tooset yeterlidir. Bulut uygulamalarınıza Azure AD üzerinden eriştiğiniz sürece hello hizmet toocorrectly kendi şirket içi kimlik bilgileriyle kimlik doğrulaması, kullanıcıların otomatik olarak yürütür.

Şirket içi konumdan SSO uygulama işlemi, Active Directory Federation Services (ADFS) gibi federasyon çözümleri veya parola karma eşitlemesini yapılandırma işlemi ile kolayca gerçekleştirilebilir. Hello Azure AD Connect yapılandırma sihirbazını kullanarak her iki seçeneği de kolayca dağıtabilirsiniz.

Daha fazla bilgi için bkz. [Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md).

- - -
**S: Azure AD, kuruluşumdaki kullanıcılar için bir self servis portal sağlar mı?**

**Y:** Evet, Azure AD, ile Merhaba sağlar [Azure AD erişim paneli](http://myapps.microsoft.com) kullanıcı Self Servis ve uygulama erişimi. Bir Office 365 müşterisiyseniz, birçok hello aynı yetenekleri hello Office 365 Portalı'nda bulabilirsiniz.

Daha fazla bilgi için bkz: [giriş toohello erişim paneli](active-directory-saas-access-panel-introduction.md).

- - -
**S: Azure AD, şirket içi altyapımı yönetmeme yardımcı olur mu?**

**Y:** Evet. Hello Azure AD Premium edition Azure AD Connect Health ile sağlar. Azure AD Connect Health, izleme ve altyapı ve hello Eşitleme Hizmetleri, şirket içi kimlik kavramanıza yardımcı olur.  

Daha fazla bilgi için bkz: [hello bulutta, şirket içi kimlik altyapınızı ve Eşitleme hizmetlerini izlemek](active-directory-aadconnect-health.md).  

- - -
## <a name="password-management"></a>Parola yönetimi
**S: Azure AD parola geri yazma özelliğini parola eşitleme olmadan kullanabilir miyim? (Bu senaryoda, olası toouse Azure AD Self Servis parola sıfırlama (SSPR) parola geri yazma ve değil deposu parolaları hello bulutta olduğu?)**

**Y:** , Active Directory parolaları tooAzure AD tooenable sonradan yazma toosynchronize gerekmez. Federasyon ortamında, Azure AD çoklu oturum açma (SSO) hello şirket içi dizin tooauthenticate hello kullanıcı kullanır. Bu senaryo, Azure AD'de izlenen hello şirket içi parola toobe gerektirmez.

- - -
**S: ne kadar süreyle tooActive şirket içi dizin geri yazılmış bir parola toobe için sürer?**

**Y:** Parola geri yazma işlemi gerçek zamanlı olarak gerçekleşir.

Daha fazla bilgi için bkz. [Parola yönetimine başlarken](active-directory-passwords-getting-started.md).

- - -
**S: Parola geri yazma özelliğini bir yönetici tarafından yönetilen parolalarla kullanabilir miyim?**

**Y:** parola geri yazma özelliğini etkinleştirdiyseniz varsa, Evet, bir yönetici tarafından gerçekleştirilen parola işlemleri hello geri tooyour şirket içi ortamına yazılır.  

Toopassword ilgili sorular ve yanıtları için bkz [parola yönetimi sık sorulan sorular](active-directory-passwords-faq.md).
- - -
**S: ı mevcut Office 365/Azure AD parolamı parolamı toochange çalışırken anımsamıyorsanız ne yapabilirim?**

**Y:** Bu tür bir durum için birkaç seçenek vardır.  Varsa, self servis parola sıfırlama (SSPR) özelliğini kullanın.  SSPR’nin çalışıp çalışmaması nasıl yapılandırıldığına bağlıdır.  Daha fazla bilgi için bkz: [nasıl hello parola sıfırlama portalı iş](active-directory-passwords-best-practices.md).

Office 365 kullanıcıları için yöneticinize hello parola özetlenen hello adımları kullanarak sıfırlayabilirsiniz [kullanıcı parolalarını sıfırlama](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US).

Azure AD hesapları için admins hello aşağıdakilerden birini kullanarak parolaları sıfırlayabilirsiniz:

- [Hello Azure portal hesapları sıfırla](active-directory-users-reset-password-azure-portal.md)
- [Merhaba Klasik Portalı'nda hesapları sıfırla](active-directory-create-users-reset-password.md)
- [PowerShell’i kullanma](/powershell/module/msonline/set-msoluserpassword?view=azureadps-1.0)


- - -
## <a name="security"></a>Güvenlik
**S: Hesaplar belirli sayıda girişim başarısız olduktan sonra kilitleniyor mu, yoksa kullanılan daha karmaşık bir strateji mi var?**</br>
Daha karmaşık bir strateji toolock hesapları kullanırız.  Bu hello istek ve girilen hello parolalar hello IP temel alır. Merhaba hello kilitleme süresini aynı zamanda bir saldırı olduğunu hello olasılığını göre artırır.  

**'Bu parolayı kullanılan toomany kez denendi' s: (ortak) parolaları ile Merhaba reddedilen belirli iletileri, bu hello geçerli active directory içinde kullanılan toopasswords bakın mu?**</br>
Bu, tüm çeşitlemelerini "Parola" ve "123456" gibi genel olarak ortak toopasswords ifade eder.

**S: Güvenilmez kaynaklardan (botnet, tor uç noktası) gelen oturum açma istekleri bir B2C kiracısında engellenir mi veya bir Temel ya da Premium sürüm kiracı gerekir mi?**</br>
İstekleri filtreleyen ve botnetlere karşı koruma sağlayıp tüm B2C kiracılarına uygulanan bir ağ geçidine sahibiz.

## <a name="application-access"></a>Uygulama erişimi
**S: Azure AD ile önceden tümleştirilmiş olan uygulamaların ve özelliklerinin listesini nereden bulabilirim?**

**Y:** Azure AD, Microsoft'a, uygulama hizmeti sağlayıcılarına ve iş ortaklarına ait 2.600'ü aşkın önceden tümleştirilmiş uygulama içerir. Önceden tümleştirilmiş tüm uygulamalar çoklu oturum açmayı (SSO) destekler. SSO, kuruluş kimlik bilgilerini tooaccess uygulamalarınızı kullanmanıza olanak sağlar. Bazı hello uygulamalar aynı zamanda otomatik hazırlama ve sağlamayı kaldırma özelliklerini destekler.

Merhaba hello önceden tümleştirilmiş uygulamaların tam listesi için bkz: [Active Directory Marketi](https://azure.microsoft.com/marketplace/active-directory/).

- - -
**S: Peki hello ihtiyacım uygulama hello Azure AD marketinde değil misiniz?**

**Y:** Azure AD Premium ile istediğiniz uygulamayı ekleyip yapılandırabilirsiniz. Uygulamanızın özelliklerine ve tercihlerinize bağlı olarak, SSO'yu ve otomatik hazırlamayı yapılandırabilirsiniz.  

Daha fazla bilgi için bkz.

* [Hello Azure Active Directory Uygulama galerisinde olmayan tek oturum açma tooapplications yapılandırma](active-directory-saas-custom-apps.md)
* [SCIM'yi tooenable otomatik kullanıcıların ve grupların Azure Active Directory tooapplications sağlama kullanma](active-directory-scim-provisioning.md)

- - -
**S: nasıl kullanıcılar Azure AD kullanarak tooapplications içinde oturum?**

**Y:** Azure AD kullanıcıların tooview için çeşitli yollar sağlar ve erişim gibi kendi uygulamalarında:

* Hello Azure AD erişim paneli
* Merhaba Office 365 uygulama Başlatıcı
* Oturum açma doğrudan toofederated uygulamalar
* Ayrıntılı bağlantılar toofederated, parola tabanlı veya var olan uygulamalar

Daha fazla bilgi için bkz: [dağıtma Azure AD tümleşik uygulamalarını toousers](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).

- - -
**S: hello farklı şekillerde Azure AD nelerdir kimlik doğrulaması ve çoklu oturum açma tooapplications sağlar?**

**Y:** Azure AD; SAML 2.0, OpenID Connect, OAuth 2.0 ve WS-Federasyon gibi birçok standartlaştırılmış kimlik doğrulaması ve yetkilendirme protokolünü destekler. Azure AD aynı zamanda, yalnızca form tabanlı kimlik doğrulamasını destekleyen uygulamalar için parola kasası oluşturma ve otomatik oturum açma işlevlerini de destekler.  

Daha fazla bilgi için bkz.

* [Azure AD için Kimlik Doğrulama Senaryoları](active-directory-authentication-scenarios.md)
* [Active Directory kimlik doğrulama protokolleri](https://msdn.microsoft.com/library/azure/dn151124.aspx)
* [Çoklu oturum açma özelliği, Azure Active Directory ile nasıl kullanılır?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)

- - -
**S: Şirket içi olarak çalıştırdığım uygulamaları ekleyebilir miyim?**

**Y:** Azure AD uygulama proxy'si, kolay ve güvenli erişim ile seçtiğiniz tooon içi web uygulamaları sağlar. Bu uygulamaların hello erişmek için aynı şekilde Azure AD'de hizmet (SaaS) uygulamaları olarak yazılımınızı erişim. Ağ altyapınızın bir VPN veya toochange gerek yoktur.  

Daha fazla bilgi için bkz: [nasıl tooprovide güvenli uzaktan erişim tooon içi uygulamaları](active-directory-application-proxy-get-started.md).

- - -
**S: Belirli bir uygulamaya erişen kullanıcılar için çok faktörlü kimlik doğrulamasını nasıl isteyebilirim?**

**Y:** Azure AD koşullu erişimi ile her bir uygulama için benzersiz bir erişim ilkesi atayabilirsiniz. İlkenizde, her zaman çok faktörlü kimlik doğrulamasını zorunlu kılabilir veya ne zaman kullanıcılar yerel ağa bağlı toohello olup olmadığı.  

Daha fazla bilgi için bkz: [tooOffice 365 ve diğer uygulamalar erişim güvenliği bağlı tooAzure Active Directory](active-directory-conditional-access.md).

- - -
**S: SaaS uygulamaları için otomatik kullanıcı hazırlama nedir?**

**Y:** kullanım Azure AD tooautomate hello oluşturulması, Bakım ve birçok popüler bulut SaaS uygulamalarına kullanıcı kimliklerini kaldırılması.

Daha fazla bilgi için bkz: [otomatikleştirmek kullanıcı sağlama ve Azure Active Directory ile tooSaaS uygulamaları etkinleştirmektir](active-directory-saas-app-provisioning.md).

- - -
**S:  Azure AD ile güvenli bir LDAP bağlantısı oluşturabilir miyim?**

**Y:** Hayır. Azure AD hello LDAP protokolünü desteklemiyor.
