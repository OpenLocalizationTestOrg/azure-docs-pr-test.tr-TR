---
title: "aaaUsing Windows 10 cihazların çalışma alanınızda | Microsoft Docs"
description: "Kullanıcılar için bir anlık görüntü yeteneklerini sağlar ve BT, aygıt sağlanabilir ve Windows 10 ile bir kuruluşta kullanılan hello farklı yolları çakışan."
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
ms.openlocfilehash: 8767e1649ced8737d20875f425c24198dcaa7f6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-windows-10-devices-in-your-workplace"></a>Windows 10 cihazlarını çalışma alanınızda kullanma
Uygulandığı öğe: Windows 10 bilgisayarları

Windows 10 kullanıcıları tooaccess iş kaynaklarına güvenli ve kolay bir şekilde etkinleştiren kuruluşlar için üç modeli sunar.

* **Azure Active Directory katılım** (Azure AD katılımı), öncelikle hello bulutta Office 365 gibi kaynaklara çalışanları için. Azure AD birleştirme, Windows 10'da yeni deneyimi sağlama ve Self Servis iştir.
* **Etki alanına katılma**, şirket uygulamalarına ve kaynaklarına yatırım olan kuruluşlar için. Etki alanına katılmayı Windows bağlıyken 10 Gelişmiş bir deneyim sunar tooAzure AD.
* **Yeni bir Basitleştirilmiş KCG deneyimi**tooadd bir iş isteyen kullanıcıların hesabı veya Okul tooWindows ve kolayca kişisel cihazlarda kaynaklara erişmek için.

Merhaba aşağıdaki tabloda bir anlık görüntüsünü kullanıcılar ve BT yöneticileri, bir cihaz sağlanabilir ve Windows 10 ile bir kuruluşta kullanılan hello farklı yolları çakışan yetenekleri sunar:

|  | Etki alanına katılma | Azure AD birleştirme | Kişisel cihaz |
| --- | --- | --- | --- |
| Windows cihaz oturum açma için iş veya Okul hesapları. |Evet |Evet |Hayır |
| Kullanıcı çoklu oturum açma (SSO) tooOffice 365 ve Azure AD uygulamaları. SSO hello özelliği toosign yalnızca bir kez tooaccess Kuruluş Kaynakları'ndaki ' dir. |Evet |Evet |Evet |
| Kullanıcı SSO tooKerberos/NTLM uygulamalar. |Evet |Sınırlı |Evet, VPN aracılığıyla |
| Güçlü Yetkilendirme ve iş veya Okul hesaplarıyla Microsoft Passport ve Windows Hello için uygun oturum açın. |Evet |Evet |Evet |
| Bir iş veya Okul hesabı (Microsoft hesabı değil) ile tooenterprise Windows mağazası erişin. |Evet |Evet |Evet |
| Kurumsal uyumlu kullanıcı iş veya Okul hesaplarıyla aygıtlar arasında Dolaşım ayarları. |Evet |Evet |Evet |
| Kurumsal cihaz ilkeleri ile uyumlu olan hello özelliği toorestrict erişim tooorganizational uygulamaları toodevices. |Evet |Evet |Evet |
| Kullanıcı Self Servis "İş" yerden için aygıtların sağlama |Hayır |Evet |Evet |
| Özelliği toomanage cihazlar. |Evet, GP/SCCM |Evet |Evet |

## <a name="use-work-owned-devices-with-azure-ad-join-and-domain-join-in-windows-10"></a>Windows 10'da Azure AD birleştirme ve etki alanı ile kullanım iş şirkete ait cihazları katılma
Windows 10 iş şirkete ait cihazları tooaccess çalışma kaynakları için iki yol sunar:

* Azure AD birleştirme
* Etki alanına katılma
  
  Her ikisi de, bir kuruluşun ihtiyaçlarına ve gereksinimlerine bağlı olarak geçerli seçenekler olabilir. Bazı durumlarda, her iki dağıtım yöntemlerini etkinleştirme kuruluşlar yararlanabilir.

## <a name="when-toouse-azure-active-directory-join"></a>Ne zaman toouse Azure Active Directory'e katılmasını
Azure AD birleştirme Windows 10 deneyimi sağlama yeni bir Self Servis iş ' dir.  Öncelikle hello bulutta Office 365 gibi iş kaynaklarına erişim çalışanları adresindeki yöneliktir. Bilgisayarlar, tabletler, basit yol tooconfigure olduğundan ve hello kuruluş için telefonlar. Cihazları Windows platformlarında tutarlı denetimlerini kullanarak mobil cihaz Yönetimi yönetilen.

**Azure AD katılım şu nedenlerden biriyle kullanmak**:

* Merhaba çalışanları gidin tooenable hello Self Servis aygıtların sağlama istiyor.
* Kullanıcılar iş şirkete ait mobil cihazları tabletler ve telefonlar gibi sağlar.
* Toomanage kullanıcı Active Directory yerine Azure AD'de Mevsimlik çalışanları, Yükleniciler veya Öğrenciler gibi istiyor.
* Tooprovide katılma yetenekleri tooworkers sınırlı şirket içi altyapı ile uzak şube ofislerinde istiyor.
* Bir şirket içi Active Directory sahip değil.

Özellikle bunların çoğu veya tüm kaynakları toohello bulut geçirmek gibi bazı kuruluşlar Azure AD katılım hello birincil yolu toodeploy iş şirkete ait cihaz kullanır. Active Directory ve Azure AD karma kuruluşlarla de toodeploy bir yöntemi veya başka bir hello kullanıcı ya da departman bağlı olarak seçebilirsiniz.

Okul bölgeleri ve üniversiteler, örneğin, Active Directory'de personel ve öğrenciler Azure AD'de yönetebilir. Bazı şirketler, Azure AD'de toomanage şubelere veya satış Departmanlar isteyebilirsiniz. Azure AD birleştirme ve etki alanı katılma yöntemleri karma kuruluş içinde kullanılabilir. Azure AD birleştirme aygıtları bir iş ortamında dağıtmak için harika tamamlama toodomain birleştirme olabilir.

**Merhaba en sık kullanılan erişim tooenterprise kaynakları hello bulut ise, kuruluşunuzun ek varsa avantajlarından**:

* Şirket içi kimlik altyapınızı bağımlılıkları kaldırabilirsiniz.
* Self Servis yapılandırma vererek uzağa doğru görüntüleme çözümleri alma, cihazları dağıtım modelini basitleştirebilir.
* Mobil cihaz Yönetimi toomanage farklı platformlarda tüm cihazlarınızda kullanabilirsiniz.

Azure AD katılım hakkında daha fazla bilgi için bkz: [bulut özellikleri tooWindows 10 cihazların Azure Active Directory katılım aracılığıyla genişletme](active-directory-azureadjoin-overview.md).

## <a name="when-toouse-domain-join-or-keep-using-it"></a>Ne zaman toouse etki alanına (veya kullanmaya devam)
Merhaba son 15 yıldan, birçok kuruluş etki alanı katılma tooconnect iş aygıtları kullandınız. Kullanıcıların toosign sağlar, Active Directory ile tootheir aygıtlarında iş veya Okul hesapları. Etki alanına katılma BT toocentrally de sağlar ve bu aygıtların tam olarak yönetin. Kuruluşlar genellikle görüntüleme yöntemleri tooprovision aygıtları kullanır ve System Center Configuration Manager (SCCM) ya da Grup İlkesi (GP) toomanage sık kullandığınız bunları.

**Kuruluşunuzun etki alanı katılma (veya onu kullanmaya devam etmek) şu nedenlerden biriyle kullanmalısınız**:

* NTLM/Kerberos kullanan Win32 uygulamaları dağıtılan toothese cihazları var.
* GP veya SCCM/DCM toomanage cihazları gerektirir.
* Çalışanlarınız için toocontinue toouse görüntüleme çözümleri tooconfigure cihazların istediğiniz.

**Windows 10 etki alanına katılma de size avantaj hello aşağıdaki bağlı tooAzure AD**:

* Güçlü aygıt bağlı kimlik doğrulaması ve güvenli oturum açma için iş veya Okul hesaplarıyla Microsoft Passport ve Windows Hello.
* İş veya Okul hesapları (Microsoft hesabı gereklidir) cihazlar için Windows mağazası toohello Kurumsal erişin.
* İş veya Okul hesaplarını (Microsoft hesabı gereklidir) kullanan aygıtlarda gezici kullanıcı ayarlarını Kurumsal uyumlu.
* Kurumsal cihaz ilkeleri ile uyumlu olan hello özelliği toorestrict erişim tooorganizational uygulamaları toodevices.

Azure AD katılım hakkında daha fazla bilgi için bkz: [bulut özellikleri tooWindows 10 cihazların Azure Active Directory katılım aracılığıyla genişletme](active-directory-azureadjoin-overview.md).

## <a name="enable-joining-of-personally-owned-devices-for-work-or-school"></a>İş veya Okul için kişisel aygıtların birleştirme etkinleştir
bir iş veya Okul hesabı tootheir bilgisayar, tablet veya telefon toosupport KCG hello kuruluşta Windows 10 hello kullanıcı hello özelliği tooadd sağlar. Merhaba sonra kullanıcı bir iş ekler veya Okul hesabı, hello aygıt Azure AD ile kayıtlı ve isteğe bağlı olarak hello kuruluş yapılandırılmış hello mobil cihaz yönetim sisteminde kayıtlı. Merhaba directory bu cihazların 'Kayıtlı' vs gösterilir. 'Azure AD alanına'. BT yöneticileri, isterseniz iş ait cihazlarda kişisel cihazlarda daha açık bir touch sağlayarak bu bilgilere göre farklı ilkeleri uygulayabilirsiniz.

Kullanıcılar bir iş ekleyebilir veya hesap tootheir kişisel cihaz oldukça rahat Okul. Bu bir iş uygulaması ilk kez hello için erişirken yapabileceklerini veya bunlar el ile hello ayarları menüsü üzerinden bunu yapabilirsiniz. Bu hesap SSO tooorganizational kaynaklar sağlar.

Azure AD katılım hakkında daha fazla bilgi için bkz: [Windows 10 deneyimleri için etki alanına katılmış aygıtlar tooAzure AD Connect](active-directory-azureadjoin-devices-group-policy.md).

## <a name="enable-domain-join-or-azure-ad-join"></a>Etki alanına katılma veya Azure AD birleştirme etkinleştirme
Daha önce açıklanan tüm yöntemleri (etki alanına katılma, Azure AD birleştirme ve ekleme iş veya Okul hesabı) hello Windows 10 kullanıcı deneyimi giriş noktaları vardır. Ancak, Hello deneyimi çalışmadan önce tüm bir BT yöneticisi tooenable hello işlevindeki hello altyapı gerektirir.

## <a name="requirements-for-deploying-azure-ad-join"></a>Azure AD katılım dağıtma gereksinimleri
toodeploy Azure AD katılım herhangi bir kullanıcı kümesi için aşağıdaki hello gerekir:

* Bir Azure AD abonelik.
* Mobil cihaz Yönetimi otomatik daha fazla yetenekleri Gerekiyorsa kayıt gibi bir Azure AD Premium aboneliği.
* Mobil cihaz Yönetimi--örnek, bir Microsoft Intune aboneliği, Office 365 için mobil cihaz Yönetimi veya herhangi bir Azure AD ile tümleştirmek hello ortak mobil cihaz Yönetimi satıcıları için. (Merhaba bkz [SSS bölümüne](#frequently-asked-questions) daha fazla bilgi için bu makalenin hello sona).

Karma, tesis varsa Azure AD Connect tooextend hello şirket içi dizin tooAzure AD dağıtmak kesinlikle önerilir.

## <a name="requirements-for-using-domain-join-with-azure-ad"></a>Azure AD ile etki alanına katılma kullanma gereksinimleri
Her zaman olduğu gibi etki alanına katılma toowork devam eder. Ancak, tooget hello Azure AD avantajları aşağıdaki hello gerekir:

* Bir Azure AD abonelik.
* Azure AD Connect tooextend hello şirket içi dizin tooAzure AD dağıtımı.
* Etki alanına katılmış aygıtlar toohave koşullu erişim tooAzure AD veren bir ilke.
* Bazı aygıtlar toobe mümkün toorestrict erişmek istiyorsanız, çok "etki alanına katılmış" aygıtları erişim veren bir ilke.
* System Center Configuration Manager Technical Preview, uyumlu cihazların gerektirme tooenable kuralları için sürüm 1509. (Merhaba TechNet belgeleri ve blog gönderisine bakın).

Windows 10 etki alanına katılma hakkında daha fazla bilgi için bkz: [Windows 10 deneyimleri için etki alanına katılmış aygıtlar tooAzure AD Connect](active-directory-azureadjoin-devices-group-policy.md)

## <a name="requirements-for-using-byod-and-add-a-work-or-school-account"></a>KCG ve "iş veya Okul hesabı ekle" kullanma gereksinimleri
tooenable "kendi cihazını getir" (BYOD) iş veya Okul hesaplarıyla hello aşağıdaki gerekir:

* Bir Azure AD abonelik.
* Mobil cihaz Yönetimi otomatik daha fazla yetenekleri Gerekiyorsa kayıt gibi bir Azure AD Premium aboneliği.

## <a name="requirements-for-using-microsoft-passport"></a>Microsoft Passport kullanma gereksinimleri
Microsoft Passport tooenable hello aşağıdaki gerekir:

* Microsoft Passport kullandığı sertifika tabanlı kimlik doğrulama desteği için ortak anahtar altyapısı (PKI).
* Intune aboneliğine Azure AD katılım için Microsoft Passport ve iş veya Okul hesapları kullanan sertifika tabanlı kimlik doğrulama desteği.
* System Center Configuration Manager Technical Preview için sürüm 1509 (Merhaba TechNet belgeleri ve blog gönderisine bakın) etki alanına katılma için Microsoft Passport kullandığı sertifika tabanlı kimlik doğrulama desteği.
* Microsoft Passport hello kuruluşta etkinleştirmek için bir ilke.

Bir alternatif toousing bir PKI'sı, Microsoft Passport anahtar tabanlı hello aşağıdakileri yaparak etkinleştirebilirsiniz:

* Windows Server 2016 "Üretim Önizleme 1" DC'leri (etki alanı veya orman işlev düzeyleri gerek yoktur; her Active Directory sitesi yeterli artıklık hizmet için birkaç DC'ler) dağıtın.
* İlke tooenable Microsoft Passport hello kuruluşta ayarlayın.

Microsoft Passport ve Windows Hello Windows 10 hakkında daha fazla bilgi için < link-to-MS-Passport-and-Windows-Hello-document > bakın.

## <a name="frequently-asked-questions"></a>Sık sorulan sorular
### <a name="which-partner-mobile-device-management-products-integrate-with-azure-ad"></a>Hangi iş ortağı mobil cihaz yönetim ürünleri Azure AD ile tümleşik mu?
Merhaba aşağıdaki Satıcı ürünleri birleştirilmiş kayıt ve Windows 10 koşullu erişim için Azure AD ile tümleştirme:

* VMware tarafından AirWatch
* Citrix Xenmobile
* Lightspeed mobil Yöneticisi
* SOTI şirket içi mobil cihaz Yönetimi
* MobileIron

### <a name="what-about-workplace-join-in-windows-10"></a>Çalışma alanı hakkında Windows 10 katılacak mısınız?
Çalışma alanına katılma, Windows 8.1 tooenable KCG kullanıldı. Windows 10'da KCG "Bir iş veya Okul hesabı" Bu belgenin önceki bölümlerinde açıklandığı gibi etkinleştirilir. Mobil cihaz yönetimleri Azure AD ile tümleştirmek olmayan kuruluşlar için el ile aracılığıyla yönetime, hello aygıt kullanıcılar kaydedebilir **ayarları** > **hesapları**  >  **İş yeri erişimi**.

### <a name="can-users-connect-their-microsoft-account-tootheir-domain-account-in-windows-10"></a>Kullanıcılar, Windows 10'daki Microsoft hesabı tootheir etki alanı hesabını bağlanabilir miyim?
Değil 10 Windows. Windows 8.1 etki alanına katılmış cihazların kullanıcılarının, "kendi Microsoft hesabı (örneğin, Hotmail, canlı, Outlook, Xbox, vb.) tootheir etki alanı hesabı tooenable SSO tooLive Hizmetleri, Windows mağazası hello kullanımını ve, dolaşım gibi belirli deneyimleri bağlantı kurulamadı" cihazlar arasında kullanıcı ayarları. Windows 10'da hello "işlevselliği Bağlan" Microsoft hesabı devre dışı bırakılmış. Merhaba kullanıcı hello Windows mağazası gibi ek hesapları tooenable SSO tooconsumer Hizmetleri olarak bir veya daha fazla Microsoft hesapları ekleyebilirsiniz. Bu yapılır **ayarları** > **hesapları** > **hesabınızı**.

Windows 8.1 etki alanına katılmış aygıtlardan yükseltme yapıyorsanız ve kimlerin Microsoft hesabını bağlı kullanıcılar, otomatik olarak bağlı Microsoft hesabını kullanırlar ek hesapları toohello listesi eklemiş.

## <a name="additional-information"></a>Ek bilgiler
* [Merhaba kuruluş için Windows 10: yolları toouse cihazlar iş için](active-directory-azureadjoin-windows10-devices-overview.md)
* [Bulut özellikleri tooWindows 10 cihazların Azure Active Directory katılım aracılığıyla genişletme](active-directory-azureadjoin-user-upgrade.md)
* [Azure AD Katılımı kullanım senaryoları hakkında bilgi edinin](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Etki alanına katılmış aygıtlar tooAzure Windows 10 deneyimleri için AD Bağlan](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD'ye Katılım ayarlama](active-directory-azureadjoin-setup.md)

