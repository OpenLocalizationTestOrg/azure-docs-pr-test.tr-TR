---
title: "Windows 10 cihazlarını çalışma alanınızda kullanma | Microsoft Docs"
description: "Kullanıcılar için bir anlık görüntü yeteneklerini sağlar ve BT, aygıt sağlanabilir ve Windows 10 ile bir kuruluşta kullanılan farklı yolları çakışan."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: 94ccc8fd-b17b-4fda-8d56-9d87aa37a9f9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 451842f764898af65dd7300e8b48442d256cea7b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="using-windows-10-devices-in-your-workplace"></a>Windows 10 cihazlarını çalışma alanınızda kullanma
Uygulandığı öğe: Windows 10 bilgisayarları

Windows 10 iş kaynaklarına güvenli ve kolay bir şekilde erişmesini sağlama kuruluşlar için üç modeli sunar.

* **Azure Active Directory katılım** (Azure AD katılımı), öncelikle bulutta Office 365 gibi kaynaklara çalışanları için. Azure AD birleştirme, Windows 10'da yeni deneyimi sağlama ve Self Servis iştir.
* **Etki alanına katılma**, şirket uygulamalarına ve kaynaklarına yatırım olan kuruluşlar için. Etki alanına katılmayı Windows Azure AD ile bağlıyken 10 Gelişmiş bir deneyim sunar.
* **Yeni bir Basitleştirilmiş KCG deneyimi**, bir iş hesabı veya Okul Windows ve kolayca eklemek istediğiniz kullanıcılar kişisel cihazlarda kaynaklara erişmek için.

Aşağıdaki tabloda bir anlık görüntüsünü kullanıcılar ve BT yöneticileri, bir cihaz sağlanabilir ve Windows 10 ile bir kuruluşta kullanılan farklı yolları çakışan yetenekleri sunar:

|  | Etki alanına katılma | Azure AD birleştirme | Kişisel cihaz |
| --- | --- | --- | --- |
| Windows cihaz oturum açma için iş veya Okul hesapları. |Evet |Evet |Hayır |
| Kullanıcı çoklu oturum açma (SSO) Office 365 ve Azure AD uygulamaları için. SSO kuruluş kaynaklarına erişmek yalnızca bir kez oturum açmak için yeteneğidir. |Evet |Evet |Evet |
| SSO kullanıcı Kerberos/NTLM uygulamalar için. |Evet |Sınırlı |Evet, VPN aracılığıyla |
| Güçlü Yetkilendirme ve iş veya Okul hesaplarıyla Microsoft Passport ve Windows Hello için uygun oturum açın. |Evet |Evet |Evet |
| Bir iş veya Okul hesabı (Microsoft hesabı değil) ile Kurumsal Windows mağazası erişimi. |Evet |Evet |Evet |
| Kurumsal uyumlu kullanıcı iş veya Okul hesaplarıyla aygıtlar arasında Dolaşım ayarları. |Evet |Evet |Evet |
| Kurumsal cihaz ilkeleriyle uyumlu cihazlara kuruluş uygulama erişimi kısıtlama yeteneği. |Evet |Evet |Evet |
| Kullanıcı Self Servis "İş" yerden için aygıtların sağlama |Hayır |Evet |Evet |
| Aygıtları yönetme yeteneği. |Evet, GP/SCCM |Evet |Evet |

## <a name="use-work-owned-devices-with-azure-ad-join-and-domain-join-in-windows-10"></a>Windows 10'da Azure AD birleştirme ve etki alanı ile kullanım iş şirkete ait cihazları katılma
Windows 10 iş kaynaklarına erişmek iş ait cihazlar için iki yol sunar:

* Azure AD birleştirme
* Etki alanına katılma
  
  Her ikisi de, bir kuruluşun ihtiyaçlarına ve gereksinimlerine bağlı olarak geçerli seçenekler olabilir. Bazı durumlarda, her iki dağıtım yöntemlerini etkinleştirme kuruluşlar yararlanabilir.

## <a name="when-to-use-azure-active-directory-join"></a>Azure Active Directory katılım kullanma zamanı
Azure AD birleştirme Windows 10 deneyimi sağlama yeni bir Self Servis iş ' dir.  Öncelikle bulutta Office 365 gibi iş kaynaklarına erişim çalışanları adresindeki yöneliktir. Bilgisayarlar, tabletler ve telefonlardan kuruluş için yapılandırmak için basit bir yoludur. Cihazları Windows platformlarında tutarlı denetimlerini kullanarak mobil cihaz Yönetimi yönetilen.

**Azure AD katılım şu nedenlerden biriyle kullanmak**:

* Self Servis aygıtların hareket halindeyken çalışanları sağlamayı etkinleştirmek istiyor.
* Kullanıcılar iş şirkete ait mobil cihazları tabletler ve telefonlar gibi sağlar.
* Mevsimlik çalışanları, Yükleniciler veya Öğrenciler gibi Azure AD'de yerine Active Directory'de bir kullanıcı kümesini yönetmek istiyorsunuz.
* Sınırlı şirket içi altyapı ile uzak şube ofislerinde çalışanları katılma yetenekleri sağlamak istiyorsunuz.
* Bir şirket içi Active Directory sahip değil.

Özellikle bunların çoğu ya da kendi kaynakların tümünü buluta taşımasına gibi bazı kuruluşlar Azure AD katılım iş şirkete ait cihaz dağıtmak için birincil şekilde kullanır. Active Directory ve Azure AD karma kuruluşlarla bir yöntemi veya başka bir kullanıcı ya da departman bağlı olarak dağıtmak de seçebilirsiniz.

Okul bölgeleri ve üniversiteler, örneğin, Active Directory'de personel ve öğrenciler Azure AD'de yönetebilir. Bazı şirketler, uzak ofislerdeki ya da satış Departmanlar Azure AD'de yönetmek isteyebilirsiniz. Azure AD birleştirme ve etki alanı katılma yöntemleri karma kuruluş içinde kullanılabilir. Azure AD birleştirme aygıtları bir iş ortamında dağıtmak için etki alanına katılma için harika bir tamamlama olabilir.

**En sık kullanılan kurumsal kaynaklara erişimi bulut ise, kuruluşunuzun ek varsa avantajlarından**:

* Şirket içi kimlik altyapınızı bağımlılıkları kaldırabilirsiniz.
* Self Servis yapılandırma vererek uzağa doğru görüntüleme çözümleri alma, cihazları dağıtım modelini basitleştirebilir.
* Farklı platformlarda cihazlarınızın tümünü yönetmek için mobil cihaz Yönetimi'ni kullanabilirsiniz.

Azure AD katılım hakkında daha fazla bilgi için bkz: [geniletmek bulut özelliklerini Azure Active Directory katılım aracılığıyla Windows 10 cihazlarına](active-directory-azureadjoin-overview.md).

## <a name="when-to-use-domain-join-or-keep-using-it"></a>Etki alanı katılma (veya onu kullanmaya devam etmek) kullanmak ne zaman
Son 15 yıldır birçok kuruluş, iş cihazları bağlamak için etki alanına katılma kullanılan. Kullanıcıların cihazlarını kullanıcıların Active Directory iş için oturum açın veya Okul hesapları olanak tanır. Etki alanına katılma de sağlar merkezi olarak ve tam olarak bu cihazları yönetmek için BT. Kuruluşlar, cihazları sağlamak için görüntü oluşturma yöntemleri genellikle kullanır ve genellikle bunları yönetmek için System Center Configuration Manager (SCCM) veya Grup İlkesi (GP) kullanın.

**Kuruluşunuzun etki alanı katılma (veya onu kullanmaya devam etmek) şu nedenlerden biriyle kullanmalısınız**:

* Win32 uygulamaları NTLM/Kerberos kullanan bu cihazlara dağıttığınız var.
* GP veya SCCM/DCM cihazları yönetmek için gerektirir.
* Çalışanlarınız için cihazları yapılandırmak için görüntüleme çözümlerini kullanmaya devam etmek istiyor.

**Windows 10 etki alanına katılma de size Azure AD ile bağlandığında aşağıdaki faydaları**:

* Güçlü aygıt bağlı kimlik doğrulaması ve güvenli oturum açma için iş veya Okul hesaplarıyla Microsoft Passport ve Windows Hello.
* İş veya Okul hesapları (Microsoft hesabı gereklidir) cihazlar için Windows mağazası Kurumsal erişim.
* İş veya Okul hesaplarını (Microsoft hesabı gereklidir) kullanan aygıtlarda gezici kullanıcı ayarlarını Kurumsal uyumlu.
* Kurumsal cihaz ilkeleriyle uyumlu cihazlara kuruluş uygulama erişimi kısıtlama yeteneği.

Azure AD katılım hakkında daha fazla bilgi için bkz: [geniletmek bulut özelliklerini Azure Active Directory katılım aracılığıyla Windows 10 cihazlarına](active-directory-azureadjoin-overview.md).

## <a name="enable-joining-of-personally-owned-devices-for-work-or-school"></a>İş veya Okul için kişisel aygıtların birleştirme etkinleştir
Kuruluş içinde KCG desteklemek için Windows 10 kullanıcı, bilgisayar, tablet veya telefon bir iş veya Okul hesabı ekleyin olanağı sağlar. Kullanıcı bir iş veya Okul hesabı ekler sonra cihaz Azure AD ile kayıtlı ve isteğe bağlı olarak kuruluş yapılandırmış mobil cihaz yönetim sisteminde kayıtlı. Dizin bu cihazların 'Kayıtlı' vs gösterilir. 'Azure AD alanına'. BT yöneticileri, isterseniz iş ait cihazlarda kişisel cihazlarda daha açık bir touch sağlayarak bu bilgilere göre farklı ilkeleri uygulayabilirsiniz.

Kullanıcılar, bir iş veya Okul hesabı için kişisel cihazlarını oldukça rahat. Bu bir iş uygulaması ilk kez erişirken yapabileceklerini veya bunlar el ile ayarları menüsü üzerinden bunu yapabilirsiniz. Bu hesap kuruluş kaynaklarına SSO sağlar.

Azure AD katılım hakkında daha fazla bilgi için bkz: [Windows 10 deneyimleri için etki alanına katılmış cihazlar için Azure AD Connect](active-directory-azureadjoin-devices-group-policy.md).

## <a name="enable-domain-join-or-azure-ad-join"></a>Etki alanına katılma veya Azure AD birleştirme etkinleştirme
Daha önce açıklanan tüm yöntemleri (etki alanına katılma, Azure AD birleştirme ve ekleme iş veya Okul hesabı) Windows 10 kullanıcı deneyimi giriş noktaları vardır. Ancak, tüm bir BT yöneticisi deneyimi çalışmadan önce altyapısında işlevselliğini etkinleştirmek gerektirir.

## <a name="requirements-for-deploying-azure-ad-join"></a>Azure AD katılım dağıtma gereksinimleri
Azure AD katılım herhangi bir kullanıcılar kümesi dağıtmak için aşağıdakiler gerekir:

* Bir Azure AD abonelik.
* Mobil cihaz Yönetimi otomatik daha fazla yetenekleri Gerekiyorsa kayıt gibi bir Azure AD Premium aboneliği.
* Mobil cihaz Yönetimi--örnek, bir Microsoft Intune aboneliği, Office 365 için mobil cihaz Yönetimi veya herhangi bir Azure AD ile tümleştirmek ortak mobil cihaz Yönetimi satıcılar için. (Bkz [SSS bölümüne](#frequently-asked-questions) daha fazla bilgi için bu makalenin sonuna).

Karma, tesis varsa Azure AD ile şirket içi dizin genişletmek için Azure AD Connect dağıtmak kesinlikle önerilir.

## <a name="requirements-for-using-domain-join-with-azure-ad"></a>Azure AD ile etki alanına katılma kullanma gereksinimleri
Etki alanına katılma, her zaman olduğu gibi çalışmaya devam eder. Ancak, Azure AD avantajlarından yararlanabilmek için aşağıdakiler gerekir:

* Bir Azure AD abonelik.
* Azure AD ile şirket içi dizin genişletmek için Azure AD Connect dağıtımı.
* Etki alanına katılmış cihazları Azure AD koşullu erişimi veren bir ilke.
* Bazı cihazlar için erişimi kısıtlamak istiyorsanız, "etki alanına katılmış" cihazlara erişim veren bir ilke.
* System Center Configuration Manager sürüm 1509 Technical uyumlu cihazların gerektirme kurallarını etkinleştirmek için Önizleme için. (Bkz. TechNet belgeleri ve blog gönderisi).

Windows 10 etki alanına katılma hakkında daha fazla bilgi için bkz: [Windows 10 deneyimleri için etki alanına katılmış cihazları Azure AD'ye bağlanma](active-directory-azureadjoin-devices-group-policy.md)

## <a name="requirements-for-using-byod-and-add-a-work-or-school-account"></a>KCG ve "iş veya Okul hesabı ekle" kullanma gereksinimleri
"Kendi cihazını getir" etkinleştirmek için (KCG) iş veya Okul hesaplarıyla, aşağıdakiler gerekir:

* Bir Azure AD abonelik.
* Mobil cihaz Yönetimi otomatik daha fazla yetenekleri Gerekiyorsa kayıt gibi bir Azure AD Premium aboneliği.

## <a name="requirements-for-using-microsoft-passport"></a>Microsoft Passport kullanma gereksinimleri
Microsoft Passport etkinleştirmek için aşağıdakiler gerekir:

* Microsoft Passport kullandığı sertifika tabanlı kimlik doğrulama desteği için ortak anahtar altyapısı (PKI).
* Intune aboneliğine Azure AD katılım için Microsoft Passport ve iş veya Okul hesapları kullanan sertifika tabanlı kimlik doğrulama desteği.
* System Center Configuration Manager Technical Preview için sürüm 1509 (bkz: TechNet belgeleri ve blog gönderisi) etki alanına katılma için Microsoft Passport kullandığı sertifika tabanlı kimlik doğrulama desteği.
* Kuruluşunuzda Microsoft Passport etkinleştirmek için bir ilke.

Bir PKI kullanarak alternatif olarak, aşağıdakileri yaparak anahtar tabanlı Microsoft Passport etkinleştirebilirsiniz:

* Windows Server 2016 "Üretim Önizleme 1" DC'leri (etki alanı veya orman işlev düzeyleri gerek yoktur; her Active Directory sitesi yeterli artıklık hizmet için birkaç DC'ler) dağıtın.
* Kuruluşunuzda Microsoft Passport etkinleştirmek için ilke ayarlayın.

Microsoft Passport ve Windows Hello Windows 10 hakkında daha fazla bilgi için < link-to-MS-Passport-and-Windows-Hello-document > bakın.

## <a name="frequently-asked-questions"></a>Sık sorulan sorular
### <a name="which-partner-mobile-device-management-products-integrate-with-azure-ad"></a>Hangi iş ortağı mobil cihaz yönetim ürünleri Azure AD ile tümleşik mu?
Aşağıdaki Satıcı ürünleri birleştirilmiş kayıt ve Windows 10 koşullu erişim için Azure AD ile tümleştirme:

* VMware tarafından AirWatch
* Citrix Xenmobile
* Lightspeed mobil Yöneticisi
* SOTI şirket içi mobil cihaz Yönetimi
* MobileIron

### <a name="what-about-workplace-join-in-windows-10"></a>Çalışma alanı hakkında Windows 10 katılacak mısınız?
Çalışma alanına katılma KCG'yi etkinleştirmek için Windows 8.1 kullanıldı. Windows 10'da KCG "Bir iş veya Okul hesabı" Bu belgenin önceki bölümlerinde açıklandığı gibi etkinleştirilir. Mobil cihaz yönetimleri Azure AD ile tümleştirmek olmayan kuruluşlar için el ile aracılığıyla yönetime, cihaz kullanıcılar kaydedebilir **ayarları** > **hesapları**  >  **İş yeri erişimi**.

### <a name="can-users-connect-their-microsoft-account-to-their-domain-account-in-windows-10"></a>Kullanıcılar kendi etki alanı hesabı Windows 10 için Microsoft hesabını bağlanabilir miyim?
Değil 10 Windows. Windows 8.1 etki alanına katılmış cihazların kullanıcılarının, "Microsoft hesabını (örneğin, Hotmail, canlı, Outlook, Xbox, vb.) SSO gibi belirli deneyimleri Live services, Windows mağazası kullanımını ve gezici kullanıcı etkinleştirmek için kendi etki alanı hesabı için bağlantı kurulamadı" aygıtlar arasında ayarları. Windows 10'da "işlevselliği Bağlan" Microsoft hesabı devre dışı bırakılmış. Kullanıcı bir veya daha fazla Microsoft hesabı tüketici hizmetlerine Windows mağazası gibi SSO'yu etkinleştirmek için ek hesaplar ekleyebilirsiniz. Bu yapılır **ayarları** > **hesapları** > **hesabınızı**.

Windows 8.1 etki alanına katılmış aygıtlardan yükseltme yapıyorsanız ve kimlerin kendi Microsoft hesabına sahip kullanıcıların bağlı, kullandıkları ek hesaplar listesine eklenen bağlı Microsoft hesabını otomatik olarak sahip olacaktır.

## <a name="additional-information"></a>Ek bilgiler
* [Kurumlar için Windows 10: Cihazları iş için kullanmanın yolları](active-directory-azureadjoin-windows10-devices-overview.md)
* [Azure Active Directory Join ile bulut işlevlerini Windows 10 cihazlarına genişletme](active-directory-azureadjoin-user-upgrade.md)
* [Azure AD Katılımı kullanım senaryoları hakkında bilgi edinin](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Windows 10 deneyiminden faydalanmak için etki alanına katılan cihazları Azure AD'ye bağlama](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD'ye Katılım ayarlama](active-directory-azureadjoin-setup.md)

