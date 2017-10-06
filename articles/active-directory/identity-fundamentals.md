---
title: "Azure Kimlik Yönetimi aaaFundamentals | Microsoft Docs"
description: 
keywords: 
author: jeffgilb
manager: femila
ms.reviewr: jsnow
ms.author: jeffgilb
ms.date: 7/5/2017
ms.topic: article
ms.prod: 
ms.service: azure
ms.technology: 
ms.assetid: 
ms.custom: it-pro
ms.openlocfilehash: a9710b8e543cdbb2f78ea9e3f83b183e1983b31d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="fundamentals-of-azure-identity-management"></a>Azure Kimlik Yönetimi temelleri
Merhaba şirket ağına, hello bulutta ve cihazlarında dışında daha da fazla şirket dijital kaynakları dinamik olarak bir harika bulut tabanlı kimlik ve erişim yönetimi çözümü zorunlu durumundadır. Bulut tabanlı hesaplardır şimdi hello en iyi şekilde toomaintain denetim üzerinden ve içine nasıl ve ne zaman kullanıcıların Kurumsal uygulamalara ve verilere erişim görünürlük.

Microsoft güvenliğini sağlamak için bulut tabanlı kimlikleri bir on üzerinden ve şimdi ile [Azure Active Directory (AD)](https://docs.microsoft.com/azure/active-directory/active-directory-editions), bu aynı koruma kullanılabilir tooyou sistemleridir. Azure AD ile kurumsal yöneticiler kolaylıkla kullanıcı ve yönetici sorumluluk daha iyi güvenlik ve idare zamankinden emin olabilirsiniz.

Azure AD Premium olan tüm uygulamalar, kimlik koruması için bir güvenli kimlik sağlayan bir bulut tabanlı kimlik ve erişim yönetimi çözümüyle gelişmiş koruma özellikleri (Merhaba tarafından geliştirilmiş [Microsoft Intelligence güvenlik grafiği](https://www.microsoft.com/en-us/security/intelligence)) ve ayrıcalıklı kimlik yönetimi. Değil yalnızca başka bir izleme veya Raporlama Aracı, Azure AD Premium gerçek zamanlı kullanıcı kimlikleri korumak ve kuruluşunuzun veri, toocreate risk tabanlı, Uyarlamalı erişim ilkeleri tooprotect etkinleştirin.

Azure AD kimlik yönetimi ve koruması hızlı bir genel bakış için kısa bu videoyu izleyin:
<iframe width="560" height="315" src="https://www.youtube.com/embed/9LGIJ2-FKIM" frameborder="0" allowfullscreen></iframe>

Microsoft yalnızca her yerde alan kimlik sağlar, ancak ayrıca araçları tooautomate kümesi güvenli hale getirmek ve yönetmek BT kuruluşunuz içinde. Hatta hello geliştirilirken bulut bilgi işlem, hala toomanage talep ve Yardım Masası kullanıcı parolalarını tooreset çağırır gibi görevlerini kontrol sonra kullanıcı Grup Yönetim ve uygulama istekleri. Daha fazla şey karmaşıklaştırarak, çalışanlar artık kendi kişisel cihazlarını toowork getiren ve kullanıma hazır SaaS uygulamaları kullanarak. Bu uygulamalarını Bakımı denetime kurumsal veri merkezleri ve genel bulut platformda önemli zor hale getirir.

[!INCLUDE [identity](../../includes/azure-ad-licenses.md)]

## <a name="connect-on-premises-active-directory-with-azure-ad-and-office-365"></a>Azure AD ile şirket içi Active Directory connect ve Office 365
Şirket içi Active Directory'de büyük yatırımlar yapmış kuruluşlar, bu Yatırımlar toohello bulut Azure AD ile şirket içi dizinlerine tümleştirerek genişletebilir [karma Kimlik Yönetimi](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview). Bunun yapılması, kullanıcılarınızın daha üretken konum bağımsız olarak kaynaklara erişmek için ortak bir kimlik sağlayarak hale getirir. Kullanıcıların ve kuruluşların kullanım çoklu oturum açma (SSO) tooaccess hem şirket içi kaynakları seçebilir ve Office 365 gibi hizmetler bulut.

[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) hello tek araç bitti tooget hello tümleştirme gerekir. Azure AD Connect kimlik eşitlemesi gerekir ve DirSync ve Azure AD eşitleme gibi kimlik tümleştirme araçlarının eski sürümlerinin yerine geçer yetenekleri toosupport sağlar. Azure AD Connect ile şirket içi ve Azure AD arasındaki eşitleme ve kimlik yönetimi etkin aracılığıyla:

- Eşitleme - Bu bileşen; kullanıcı, grup ve diğer nesnelerin oluşturulmasından sorumludur. Şirket içi kullanıcılar ve gruplar için kimlik bilgilerini hello bulut ile eşleşmesini sağlamaktan sorumludur. Bir kullanıcı parolalarını Azure AD içinde güncelleştirdiğinde parola geri yazma etkinleştirilmiş tookeep şirket içi dizin eşitleme de olabilir.
- AD FS - federasyon kullanılan tooconfigure bir şirket içi kullanarak karma bir ortamınız olabilecek Azure AD Connect tarafından sağlanan isteğe bağlı bir özellik olan AD FS altyapısı. Federasyon, kuruluşların tooaddress karmaşık dağıtımlar, çoklu oturum açma, akıllı kart veya üçüncü taraf MFA ve AD oturum açma ilkesini zorlama gibi tarafından kullanılabilir.
- Sistem durumu izleme - [Azure AD Connect Health](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health) izleme olanağı sağlayarak ve bu etkinliği hello Azure portal tooview merkezi bir konumda sağlayın.

## <a name="increase-productivity-and-reduce-helpdesk-costs-with-self-service-and-single-sign-on-experiences"></a>Üretkenliği artırmak ve Self Servis ve çoklu oturum açma deneyimlerini ile Yardım Masası maliyetlerini azaltma

Tek bir kullanıcı adı ve parola tooremember ve tutarlı bir deneyim her aygıttan olduğunda daha üretken çalışanlardır. Bunlar aynı zamanda bunların ne zaman gerçekleştirebilir gibi Self Servis görevleri zamandan [Unutulan parolayı sıfırlama](https://docs.microsoft.com/azure/active-directory/active-directory-passwords) veya erişim tooan uygulama hello Yardım Masası Yardım beklemeden istiyor.

Azure AD [şirket içi Active Directory genişletir](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) hello bulutunu kullanıcılar toouse hem kendi etki alanına katılmış aygıtlar, şirket kaynaklarına ve tüm hello web ve SaaS uygulamaları için birincil kuruluş hesabını etkinleştirme bunlar işlerini toouse tooget gerekir. Ayrıca birden çok kullanıcı adları ve parolalar, kullanıcıların uygulama erişimi kümesini de otomatik olarak sağlanan (XML'deki sağlanan veya) tooremember sahip toonot olarak çalışan kuruluş grup üyeliklerini ve durumlarına göre. Ve galeri uygulamalar veya için geliştirilen ve hello yayımlanan kendi şirket içi uygulamalar bu erişimi denetleyebilir [Azure AD uygulama proxy'si](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).

## <a name="manage-and-control-access-toocorporate-resources"></a>Yönetmek ve denetlemek toocorporate kaynaklarına erişim
Microsoft kimlik ve erişim yönetimi çözümlerini Yardım BT erişim tooapplications ve kaynakları hello kurumsal veri merkezi genelinde ve hello buluta doğrulama ek düzeyleri gibi etkinleştirme korumaya [çok faktörlü kimlik doğrulaması](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next) ve [koşullu erişim ilkeleri](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). Raporlama, Denetim ve yardımcı olası güvenlik sorunlarını azaltmak uyarı Gelişmiş Güvenlik ile izleme şüpheli etkinlik.

Azure AD Premium koşullu erişim ilkelerini size, kuruluş yöneticisi Merhaba, hello özelliği toocreate ilke tabanlı uygulama için erişim kurallarının tüm Azure AD bağlı (SaaS uygulamaları, özel uygulamalar hello Bulut veya şirket içi web uygulamaları çalıştıran). Azure AD, bu ilkeler gerçek zamanlı değerlendirir ve bir kullanıcı tooaccess çalıştığında bunları uygulamaya zorlar. Şüpheli etkinlik bulunduğundan, azure kimlik koruma ilkeleri tooautomatically eylemi gerçekleştirin etkinleştirin. Kimlik bilgileri gibi görünüyorsa sıfırlama kullanıcı parolalarını tehlikede olduğunu ve bu eylemleri erişim toousers çok faktörlü kimlik doğrulamasını zorunlu yüksek risk engelleme içerebilir.


## <a name="azure-active-directory-privileged-identity-management"></a>Azure Active Directory Ayrıcalıklı Kimlik Yönetimi

[Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-getting-started)hello Azure Active Directory Premium P2 ile dahil sunumunun verir toodiscover, kısıtlayın ve izleyin yönetim hesapları ve Azure Active Directory ve diğer kullanıcıların erişim tooresources Microsoft Çevrimiçi Hizmetler. Ayrıca, isteğe bağlı yönetim erişimi hello tam süre ihtiyacınız yönetmenize yardımcı olur.

Böylece yöneticiler çok faktörlü kimlik doğrulamalı, geçici ayrıcalıkların kendi hesaplarına tooa normal döndürmeden önce önceden yapılandırılmış süreler için isteyebilir isteğe bağlı yönetici hakları privileged Identity Management zorlayabilir Kullanıcı durumu.

## <a name="benefits-of-azure-identity"></a>Azure kimlik yararları

Azure Kimlik Yönetimi ile şunları yapabilirsiniz:

-   Oluşturma ve kullanıcılara, gruplara ve cihazlara ile eşitlenmiş şekilde kalmasının tüm kuruluşunuz genelinde her kullanıcı için tek bir kimliği yönetme [Azure Active Directory Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

-   Önceden tümleştirilmiş SaaS uygulamaları binlerce dahil olmak üzere tooyour uygulamalar tek oturum açma erişim sağlamak veya hello kullanarak tooon içi SaaS uygulamaları güvenli uzaktan erişim sağlayan [Azure AD uygulama proxy'si](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started).

-   Uygulama erişimi güvenliğini kural tabanlı zorlayarak etkinleştirmek [çok faktörlü kimlik doğrulaması](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next) şirket içi ve bulut uygulamaları.

-   Kullanıcı verimliliğini artırmak [Self Servis parola sıfırlama](https://docs.microsoft.com/azure/active-directory/active-directory-passwords), Grup ve erişim isteklerini hello kullanarak uygulama ve [MyApps portal](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-user-help).

-   Merhaba yararlanmak [yüksek kullanılabilirlik ve güvenilirlik](https://docs.microsoft.com/azure/architecture/resiliency/high-availability-azure-applications) bir dünya çapında, kurumsal düzeyde, bulut tabanlı kimlik ve erişim yönetimi çözümü.

## <a name="next-steps"></a>Sonraki adımlar
[Azure kimlik çözümleri hakkında daha fazla bilgi edinin](https://docs.microsoft.com/azure/active-directory/understand-azure-identity-solutions)