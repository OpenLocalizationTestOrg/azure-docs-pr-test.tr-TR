---
title: Azure AD Privileged Identity Management aaaConfigure | Microsoft Docs
description: "Azure AD Privileged Identity Management nedir açıklayan bir konu ve nasıl toouse PIM tooimprove bulut güvenliğinizi."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: c548ed2e-06e3-4eaf-a63d-0f02ee72da25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: dbe49fe4a0f6e5b46ed5a17fc7e8dcdacafe3846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-ad-privileged-identity-management"></a>Azure AD Privileged Identity Management nedir?
Azure Active Directory (AD) Privileged Identity Management sayesinde kuruluşunuz içindeki erişimi yönetebilir, denetleyebilir ve izleyebilirsiniz. Bu erişim tooresources Azure AD'de ve Office 365 veya Microsoft Intune gibi diğer Microsoft online services içerir.  

> [!NOTE]
> Privileged Identity Management yöneticilerinizi hello Premium P2 edition Azure Active Directory ile lisans kullanılabilir tooyour tüm kuruluş durumdur. Daha fazla bilgi için bkz. [Azure Active Directory sürümleri](active-directory-editions.md).

Çünkü, bu erişim alma kötü niyetli bir kullanıcının hello olasılığını azaltır kuruluşlar toominimize hello toosecure bilgilere erişmek veya kaynaklarını olan kişiler sayısı istiyor. Ancak, kullanıcılar yine de Azure, Office 365 ya da SaaS uygulamalarında ayrıcalıklı işlemleri çıkışı toocarry gerekir. Kuruluşlar, yönetici ayrıcalıklarını bu kullanıcıların ne yaptıklarını izleme olmadan, Azure AD'de kullanıcılar ayrıcalıklı erişim verin. Azure AD Privileged Identity Management tooresolve bu riski yardımcı olur.  

Azure AD Privileged Identity Management yardımcı olur:  

* Hangi kullanıcıların Azure AD yöneticilerdir bakın
* İsteğe bağlı, "Office 365 ve Intune yönetim erişimi tooMicrosoft çevrimiçi hizmetler gibi tam zamanında" etkinleştirme
* Yönetici erişim geçmişine ve değişiklikler hakkında raporlar yönetici atamaları alma
* Erişim tooa ayrıcalıklı rol hakkında uyarı alın
* Onay tooactivate (Önizleme) gerektirir

Azure AD Privileged Identity Management (ancak bunlarla sınırlı değil) hello yerleşik Azure AD kuruluş rolleri yönetebilir:  

* Genel yönetici
* Faturalama Yöneticisi
* Hizmet Yöneticisi  
* Kullanıcı Yöneticisi
* Parola Yöneticisi

## <a name="just-in-time-administrator-access"></a>Yalnızca süresi yönetici erişimi
Tarihsel olarak, bir kullanıcı tooan Yönetici rolü hello Klasik Azure portalı üzerinden veya Windows PowerShell atayabilirsiniz. Sonuç olarak, bu kullanıcının hale bir **kalıcı yönetici**, atanan hello rolündeki her zaman etkin. Azure AD Privileged Identity Management hello kavramını sunmaktadır bir **uygun yönetici**. Uygun admins şimdi yapıp ancak her gün ayrıcalıklı erişimi olması gereken kullanıcılar olmalıdır. bir etkinleştirme işlemini tamamlamak ve önceden belirlenen bir süre için etkin bir yönetim hale hello kullanıcının erişim, gerektiği kadar hello rolü etkin değil.

## <a name="enable-privileged-identity-management-for-your-directory"></a>Privileged Identity Management dizininiz için etkinleştirme
Azure AD Privileged Identity Management hello kullanmaya başlayabilmeniz için [Azure portal](https://portal.azure.com/).

> [!NOTE]
> Bir kurumsal hesap ile genel yönetici olmanız gerekir (örneğin, @yourdomain.com), bir Microsoft hesabı (örneğin, @outlook.com), bir dizin için Azure AD Privileged Identity Management tooenable.

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/) dizininizin genel Yöneticisi olarak.
2. Kuruluşunuz birden fazla dizine sahipse, kullanıcı adınızı hello sağ üst köşesinde hello Azure portalı içinde seçin. Burada, Azure AD Privileged Identity Management kullanacağınız hello dizini seçin.
3. Seçin **daha fazla hizmet** ve hello filtre textbox toosearch **Azure AD Privileged Identity Management**.
4. Denetleme **PIN toodashboard** ve ardından **oluşturma**. Merhaba Privileged Identity Management uygulaması açılır.

Dizininizde Azure AD Privileged Identity Management ilk kişinin toouse olduğunuz hello varsa, ardından hello [Güvenlik Sihirbazı](active-directory-privileged-identity-management-security-wizard.md) hello ilk atama deneyimi boyunca size yardımcı olur. Bundan sonra otomatik olarak hale hello ilk **Güvenlik Yöneticisi** ve **ayrıcalıklı Rol Yöneticisi** hello dizininin.

Yalnızca ayrıcalıklı Rol Yöneticisi, diğer yöneticiler için erişimi yönetebilirsiniz. Yapabilecekleriniz [PIM diğer kullanıcıların hello özelliği toomanage vermek](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).

## <a name="privileged-identity-management-admin-dashboard"></a>Privileged Identity Management Yönetim Panosu
Azure AD Privileged Identity Manager gibi önemli bilgiler sağlayan bir Yönetim Panosu sağlar:

* Fırsatları tooimprove güvenlik noktası uyarıları
* Merhaba tooeach ayrıcalıklı role atanmış kullanıcıların sayısını  
* uygun ve kalıcı admins Hello sayısı
* Ayrıcalıklı rolü etkinleştirme dizininizde grafiği

![PIM Pano - ekran görüntüsü][2]

## <a name="privileged-role-management"></a>Ayrıcalıklı rol yönetimi
Azure AD Privileged Identity Management'ı ekleyerek veya kaldırarak kalıcı veya uygun Yöneticiler tooeach rolünün hello Yöneticiler yönetebilir.

![PIM Ekle/Kaldır yöneticileri - ekran görüntüsü][3]

## <a name="configure-hello-role-activation-settings"></a>Merhaba rol etkinleştirme ayarlarını yapılandırma
Hello kullanarak [rol ayarlarını](active-directory-privileged-identity-management-how-to-change-default-settings.md) hello uygun rol etkinleştirme özellikleri dahil olmak üzere yapılandırabilirsiniz:

* Merhaba rol etkinleştirme süresi başlangıç süresi
* Merhaba rol etkinleştirme bildirimi
* Merhaba bilgi kullanıcı tooprovide hello rol etkinleştirme işlemi sırasında gerekiyor.
* Hizmet bileti veya olay numarası
* [Onay iş akışı gereksinimleri - Önizleme](./privileged-identity-management/azure-ad-pim-approval-workflow.md)

![PIM ayarları - yönetici etkinleştirme - ekran görüntüsü][4]

Merhaba görüntüde için hello düğmeleri Not **çok faktörlü kimlik doğrulaması** devre dışı bırakılır. Belirli, yüksek ayrıcalıklı rolleri, size daha fazla koruma için MFA gerekir.

## <a name="role-activation"></a>Rol etkinleştirme
çok[bir rolü etkinleştirmesi](active-directory-privileged-identity-management-how-to-activate-role.md), bir zaman sınırlı "etkinleştirme" Merhaba rolü için uygun yönetici ister. Merhaba etkinleştirme hello kullanarak istenebilir **my rolünü etkinleştirmek** Azure AD Privileged Identity Management seçeneği.

Bir rolü tooactivate isteyen bir yönetici tooinitialize hello Azure portalında Azure AD Privileged Identity Management gerekir.

Rol etkinleştirme özelleştirilebilir. Merhaba PIM ayarlarında hello etkinleştirme ve hangi bilgi hello Yöneticisi tooprovide tooactivate hello rolüne ihtiyacı hello uzunluğu belirleyebilirsiniz.

![PIM yönetici isteği rol etkinleştirme - ekran görüntüsü][5]

## <a name="review-role-activity"></a>Gözden geçirme rol etkinliği
İki yolu tootrack vardır, çalışanlarınızın ve admins nasıl kullandığını ayrıcalıklı rolleri. Merhaba ilk seçenek kullanıyor [Directory rolleri denetim geçmişi](active-directory-privileged-identity-management-how-to-use-audit-log.md). Merhaba denetim geçmişi Değişiklikleri İzle ayrıcalıklı rol atamaları ve rol etkinleştirme geçmişini kaydeder.

![PIM etkinleştirme geçmişi - ekran görüntüsü][6]

Merhaba ikinci tooset normal yedekleme seçenektir [erişim incelemeler](active-directory-privileged-identity-management-how-to-start-security-review.md). Bu erişim incelemeler tarafından gerçekleştirilen ve İnceleme (örneğin, bir takım Yöneticisi) atanmış veya hello çalışanlar kendilerini gözden geçirebilirsiniz. Kimin hala erişim gerektirir ve artık kilitlenmiyor hello en iyi şekilde toomonitor budur.

## <a name="azure-ad-pim-at-subscription-expiration"></a>Abonelik sona erme adresindeki Azure AD PIM
Önceki tooreaching kullanılabilirlik Azure AD PIM önizlemede oldu ve lisans vardı genel bir kiracı toopreview Azure AD PIM denetler.  Azure AD PIM genel kullanılabilirlik ulaştı, deneme aboneliği veya Ücretli lisans PIM kullanarak hello Kiracı toocontinue toohello yöneticileri atanması gerekir.  Kuruluşunuz Azure AD Premium P2 satın değil veya deneme süresi, genellikle tüm hello Azure AD PIM özellikler artık kiracınızda kullanılabilir.  Daha fazla bilgiyi hello içinde [Azure AD PIM abonelik gereksinimleri](./privileged-identity-management/subscription-requirements.md)

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-configure/PIM_Admin_Overview.png
[3]: ./media/active-directory-privileged-identity-management-configure/PIM_AddRemove.png
[4]: ./media/active-directory-privileged-identity-management-configure/PIM_Settings_w_Approval_Disabled.png
[5]: ./media/active-directory-privileged-identity-management-configure/PIM_RequestActivation.png
[6]: ./media/active-directory-privileged-identity-management-configure/PIM_ActivationHistory.png
