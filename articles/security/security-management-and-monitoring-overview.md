---
title: "aaaAzure güvenlik yönetimi ve izlemeye genel bakış | Microsoft Docs"
description: " Azure güvenlik mekanizmaları tooaid hello yönetimi ve izlenmesi Azure bulut Hizmetleri ve sanal makineleri sağlar.  Bu makalede bu temel güvenlik özellikleri ve Hizmetleri genel bakış sağlar. "
services: security
documentationcenter: na
author: TerryLanfear
manager: StevenPo
editor: TomSh
ms.assetid: 5cf2827b-6cd3-434d-9100-d7411f7ed424
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: terrylan
ms.openlocfilehash: 0026fa97bab7e15c9f8de6856b5075abe2288f61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-management-and-monitoring-overview"></a>Azure güvenlik yönetimi ve izlemeye genel bakış
Azure güvenlik mekanizmaları tooaid hello yönetimi ve izlenmesi Azure bulut Hizmetleri ve sanal makineleri sağlar. Bu makalede bu temel güvenlik özellikleri ve Hizmetleri genel bakış sağlar. Daha fazla bilgi için her ayrıntılarını veren tooarticles bağlantılar sağlanmaktadır.

Microsoft bulut hizmetlerinin başlangıç güvenlik ortaklığı ve Microsoft arasında paylaşılan sorumluluk ' dir. Paylaşılan sorumluluk (kilitli rozet giriş kapıları, dilimleri ve koruyucuları gibi güvenlik korumaları kullanarak) Microsoft hello Microsoft Azure ve veri merkezleri, fiziksel güvenlik için sorumlu olduğu anlamına gelir. Ayrıca, Azure bulut güvenlik hello güvenlik, gizlilik ve zorlu müşterilerine uyumluluk gereksinimlerini karşılayan hello yazılım katmanında güçlü düzeyleri sağlar.

Sahip olduğunuz veriler ve kimlikleri, bunları, şirket içi kaynaklarınızın hello güvenlik ve bulut bileşenleri üzerinde denetim sahibi hello güvenliğini koruma sorumluluğunu hello. Microsoft sağlar, güvenlik denetimleri ve yetenekleri toohelp ile verileriniz ve uygulamalarınız koruma. Güvenlik sorumluluğunu, derecesini bulut hizmeti başlangıç türünü temel alır.

Grafik aşağıdaki hello hem Microsoft hem de hello müşteri sorumluluğunu hello bakiyesini özetler.

![Paylaşılan sorumluluk][1]

Güvenlik yönetimi içine daha ayrıntılı bilgi edinmek için bkz: [azure'da güvenlik yönetimi](azure-security-management.md).

Bu makalede ele alınan hello çekirdek özellikler toobe şunlardır:

* Rol Tabanlı Access Control
* Kötü Amaçlı Yazılımdan Koruma
* Multi-Factor Authentication
* ExpressRoute
* Sanal ağ geçitleri
* Ayrıcalıklı Kimlik Yönetimi
* Kimlik koruması
* Güvenlik Merkezi

## <a name="role-based-access-control"></a>Rol Tabanlı Access Control
Rol tabanlı erişim denetimi (RBAC) Azure kaynakları için ayrıntılı erişim yönetimi sağlar. RBAC kullanarak, kişiler yalnızca hello tooperform işlerini gereken erişim miktarını verebilirsiniz.  RBAC da kişiler hello kuruluştan ayrılan bunlar erişim tooresources hello bulutta kaybetmek olmanıza yardımcı olabilir.

Daha fazla bilgi edinin:

* [RBAC üzerinde Active Directory ekip blogu](http://i1.blogs.technet.com/b/ad/archive/2015/10/12/azure-rbac-is-ga.aspx)
* [Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md)

## <a name="antimalware"></a>Kötü Amaçlı Yazılımdan Koruma
Azure ile Microsoft, Symantec, eğilim mikro, McAfee gibi önemli güvenlik satıcılardan kötü amaçlı yazılımdan koruma yazılımını kullanabilirsiniz ve Kaspersky toohelp kötü amaçlı dosyalar, reklam ve diğer tehditlerden sanal makinelerinizi koruyun.

Microsoft Antimalware özelliği tooinstall PaaS rol ve sanal makineler için bir kötü amaçlı yazılımdan koruma Aracısı hello sunar. System Center Endpoint Protection'ı bağlı olarak, bu özellik kanıtlanmış şirket içi güvenlik teknolojisi toohello bulut getirir.

Ayrıca eğilimi'nın için derin tümleştirme sunuyoruz [derin güvenlik](http://www.trendmicro.com/us/enterprise/cloud-solutions/deep-security/)™ ve [SecureCloud](http://www.trendmicro.com/us/enterprise/cloud-solutions/secure-cloud/)™ hello Azure platformu ürünlerinde. DeepSecurity virüsten koruma çözümüdür ve SecureCloud bir şifreleme çözümüdür. DeepSecurity bir uzantı modeli kullanarak VM'ler içinde dağıtılır. Merhaba portal UI ve PowerShell kullanarak, toouse DeepSecurity çalışmaya başlar yeni VM'ler veya zaten dağıtılmış varolan VM'ler içinde seçebilirsiniz.

Symantec uç nokta koruma (Eylül) de Azure üzerinde desteklenir. Portal tümleştirme sayesinde, müşteriler toouse Eylül bir VM içinde düşündüğünüz belirtebilirsiniz. Eylül hello Azure portal aracılığıyla yepyeni bir VM yüklenebilir veya PowerShell kullanarak var olan bir VM üzerinde yüklenebilir.

Daha fazla bilgi edinin:

* [Azure Sanal Makinelerinde Kötü Amaçlı Yazılıma Karşı Koruma Çözümleri Dağıtma](https://azure.microsoft.com/blog/deploying-antimalware-solutions-on-azure-virtual-machines/)
* [Azure bulut Hizmetleri ve sanal makineleri için Microsoft kötü amaçlı yazılımdan koruma](azure-security-antimalware.md)
* [Nasıl tooinstall ve bir Windows VM bir hizmet olarak eğilimi mikro derin güvenliği yapılandırma](../virtual-machines/windows/classic/install-trend.md)
* [Nasıl tooinstall ve Symantec Endpoint Protection bir Windows VM yapılandırma](../virtual-machines/windows/classic/install-symantec.md)
* [Azure sanal makineleri – McAfee Endpoint Protection korunması için yeni kötü amaçlı yazılımdan koruma seçenekleri](https://azure.microsoft.com/blog/new-antimalware-options-for-protecting-azure-virtual-machines/)

## <a name="multi-factor-authentication"></a>Multi-Factor Authentication
Azure çok faktörlü kimlik doğrulaması (MFA) hello birden fazla doğrulama yöntemi kullanılmasını gerektiren ve güvenlik toouser oturum açmalarına ve işlemlerine önemli bir ikinci katmanı ekleyen kimlik doğrulama yöntemidir. MFA basit bir oturum açma işlemi için kullanıcı talebine buluştururken koruma erişim toodata ve uygulamaları yardımcı olur. Güçlü kimlik doğrulama seçeneklerini çeşitli aracılığıyla sunar — telefon araması, SMS mesajı veya mobil uygulama bildirimi veya doğrulama kodu ve üçüncü taraf OATH belirteçleri.

Daha fazla bilgi edinin:

* [Multi-Factor Authentication](https://azure.microsoft.com/documentation/services/multi-factor-authentication/)
* [Azure Multi-Factor Authentication nedir?](../multi-factor-authentication/multi-factor-authentication.md)
* [Azure multi-Factor Authentication nasıl çalışır](../multi-factor-authentication/multi-factor-authentication-how-it-works.md)

## <a name="expressroute"></a>ExpressRoute
Microsoft Azure ExpressRoute bağlantı sağlayıcı tarafından kolaylaştırılan adanmış özel bağlantı üzerinden şirket içi ağlarınızı Microsoft bulut hello genişletmenizi sağlar. ExpressRoute ile Microsoft Azure, Office 365 ve CRM Online gibi bağlantıları tooMicrosoft bulut Hizmetleri kurabilirsiniz. Ortak yerleşim tesisinde bağlantı sağlayıcısı üzerinden herhangi bir ağdan herhangi bir ağa (IP VP), noktadan noktaya Ethernet ağı veya sanal çapraz bağlantısından bağlantı olabilir.  ExpressRoute bağlantıları hello Git değil genel Internet. Bu ExpressRoute bağlantıları toooffer daha fazla güvenilirlik, yüksek hız, düşük gecikme ve normal bağlantıları daha yüksek güvenlik hello Internet sağlar.

Daha fazla bilgi edinin:

* [ExpressRoute teknik genel bakış](../expressroute/expressroute-introduction.md)

## <a name="virtual-network-gateways"></a>Sanal ağ geçitleri
Azure sanal ağ geçitleri olarak da adlandırılan, VPN ağ geçitleri kullanılan sanal ağlar ve şirket içi konumlara arasında ağ trafiğini toosend. Bunlar ayrıca azure'da (VNet-VNet) birden çok sanal ağlar arasında kullanılan toosend trafiği değildir.  VPN ağ geçitleri altyapınız ile Azure arasında güvenli şirket içi bağlantısı sağlar.

Daha fazla bilgi edinin:

* [VPN ağ geçitleri hakkında](../vpn-gateway/vpn-gateway-about-vpngateways.md)
* [Azure ağ güvenliğine genel bakış](security-network-overview.md)

## <a name="privileged-identity-management"></a>Privileged Identity Management
Bazen kullanıcıların Azure kaynakları veya diğer SaaS uygulamalarında ayrıcalıklı işlemleri çıkışı toocarry gerekir. Bu, genellikle kuruluşlar sahip toogive anlamına bunları kalıcı ayrıcalıklı erişim Azure Active Directory (Azure AD). Kuruluşlar, yeteri kadar ayrıcalıklı erişim ile bu kullanıcıların ne yaptıklarını izleyemez bulutta barındırılan kaynaklar için büyüyen bir güvenlik riski olmasıdır.
Ayrıca, ayrıcalıklı erişimi olan bir kullanıcı hesabı ihlal edilmesi durumunda, bir ihlali genel bulut güvenliğinizi etkileyebilir. Azure AD Privileged Identity Management tooresolve bu riski hello Etkilenme ayrıcalıkları süresini azaltarak ve kullanım görünürlük artırma tarafından yardımcı olur.  

Privileged Identity Management geçici bir yönetici rol ya da bir etkinleştirme işlemi, rolü atanmış toocomplete gereksinim duyan bir kullanıcı "tam zamanında" Yönetici erişimi için hello kavramını sunmaktadır. Merhaba etkinleştirme süreci değişiklikleri etkin olmayan tooactive, Azure AD'den belirli bir süre sekiz saat gibi hello kullanıcı tooa rolünün atamasını hello.

Daha fazla bilgi edinin:

* [Azure AD Privileged Identity Management](../active-directory/active-directory-privileged-identity-management-configure.md)
* [Azure AD Privileged Identity Management ile çalışmaya başlama](../active-directory/active-directory-privileged-identity-management-getting-started.md)

## <a name="identity-protection"></a>Kimlik Koruması
Azure Active Directory (AD) kimlik koruması oturum açma kuşkulu etkinlikleri birleştirilmiş bir görünümünü sağlar ve olası güvenlik açıklarını toohelp işletmenizin koruyun. Kimlik koruması kullanıcılar için kuşkulu etkinlikleri algılar ve ayrıcalıklı (Yönetici) kimlikleri, kaba kuvvet saldırıları gibi sinyalleri dayalı kimlik bilgilerini ve oturum açma işlemleri tanınmayan konumlardan sızmasını ve aygıtları virüs bulaşmış.

Kimlik koruması bildirimleri ve önerilen düzeltme sağlayarak, gerçek zamanlı toomitigate riskleri yardımcı olur. Kullanıcı risk önem hesaplar ve risk tabanlı ilkeleri tooautomatically Yardım uygulama erişimi korumaya gelecekteki tehditlere karşı yapılandırabilirsiniz.

Daha fazla bilgi edinin:

* [Azure Active Directory kimlik koruması](../active-directory/active-directory-identityprotection.md)
* [Kanal 9: Azure AD ve kimlik göster: kimlik koruması Önizleme](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

## <a name="security-center"></a>Güvenlik Merkezi
Azure Güvenlik Merkezi, engellemenize, algılamanıza ve toothreats yanıt yardımcı olur ve artan, görünürlük ve denetim üzerinden, Azure kaynaklarınızın hello güvenlik sağlar. Aboneliklerinizde, tümleşik güvenlik izleme ve ilke yönetimi sağlar; normal koşullarda gözden kaçabilecek tehditleri algılamaya yardımcı olur ve güvenlik çözümlerinin geniş ekosistemiyle çalışır.

Güvenlik Merkezi en iyi duruma getirme ve Azure kaynaklarınızı tarafından hello güvenliğini izlemenize yardımcı olur:

* Azure aboneliği kaynaklarınızın tooyour göre toodefine ilkelerini etkinleştirme şirketin güvenlik gerektiriyor ve uygulamaların türü veya hello her Abonelikteki verilerin duyarlılığına hello.
* Azure sanal makineleri, ağ ve uygulamaları Hello durumunu izleme.
* Öncelikli güvenlik uyarıları, tümleşik iş ortağı çözümleri tooquickly ihtiyacınız hello bilgilerle birlikte araştırmak ve öneriler nasıl gelen uyarılar dahil olmak üzere bir listesini sağlayan bir saldırı tooremediate.

Daha fazla bilgi edinin:

* [Giriş tooAzure Güvenlik Merkezi](../security-center/security-center-intro.md)

<!--Image references-->
[1]: ./media/security-management-and-monitoring-overview/shared-responsibility.png
