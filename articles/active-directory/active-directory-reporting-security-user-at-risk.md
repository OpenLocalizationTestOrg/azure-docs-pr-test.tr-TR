---
title: "aaaUsers bayrağı risk güvenlik raporu hello Azure Active Directory portalında için | Microsoft Docs"
description: "Risk güvenlik raporu hello Azure Active Directory portalında için işaretlenen hello kullanıcılar hakkında bilgi edinin"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5077cd61d6119745a85ed712623904633a151331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="users-flagged-for-risk-security-report-in-hello-azure-active-directory-portal"></a>Risk güvenlik raporu hello Azure Active Directory portalında için bayrak eklenen kullanıcılar

Hello Azure Active Directory (Azure AD) içinde Hello güvenlik raporları ile ortamınızda ele geçirilen kullanıcı hesapları hello olasılığını Öngörüler elde edebilirsiniz. 

Azure Active Directory, ilgili tooyour kullanıcı hesapları olan şüpheli eylemleri algılar. Algılanan her eylem için *risk olayı* adlı bir kayıt oluşturulur. Daha fazla bilgi için bkz. [Azure Active Directory risk olayları](active-directory-identity-protection-risk-events.md). 

Merhaba risk olaylarını kullanılan toocalculate algıladı:

- **Riskli oturum açma işlemleri** -bir riskli oturum açma bir hello meşru bir kullanıcı hesabının sahibi olmayan kişi tarafından gerçekleştirilmiş olabilecek bir oturum açma girişimi için göstergesidir. Daha fazla bilgi için bkz. [Riskli oturum açma işlemleri](active-directory-identityprotection.md#risky-sign-ins). 

- **Riskli oldukları belirlenen kullanıcılar** - Riskli kullanıcı, güvenliği tehlikeye girmiş olabilecek bir kullanıcı hesabının göstergesidir. Daha fazla bilgi için bkz. [Risk için işaretlenen kullanıcılar](active-directory-identityprotection.md#users-flagged-for-risk).  

Hello Azure portal, hello güvenlik raporları hello üzerinde bulabilirsiniz **Azure Active Directory** dikey penceresinde hello **güvenlik** bölümü.  

![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-user-at-risk/10.png)



## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a>Hangi Azure AD lisans tooaccess bir güvenlik raporu gerekiyor mu?  

Azure Active Directory'nin tüm sürümlerinde size riskli oldukları belirlenen kullanıcılar ve risk raporları sağlanır.  
Bununla birlikte, rapor ayrıntı düzeyini hello hello sürümleri arasında farklılık gösterir: 

- Merhaba, **Azure Active Directory ücretsiz ve Basic sürümleri**, zaten risk bayrak eklenen kullanıcılar listesini alın. 

- Merhaba **Azure Active Directory Premium 1** edition'ı genişletir bu modeli de tooexamine sağlayarak her rapor için algılanan risk olayı temel hello bazıları. 

- Merhaba **Azure Active Directory Premium 2** edition ile sağlar hello tüm temel alınan risk olaylar hakkında en ayrıntılı bilgi ve otomatik olarak tooconfigured risk yanıt tooconfigure güvenlik ilkeleri sağlar düzeyleri.



## <a name="azure-active-directory-free-and-basic-edition"></a>Azure Active Directory ücretsiz ve temel sürümleri

risk raporda hello Azure Active Directory ücretsiz ve temel sürümleri için işaretlenen hello kullanıcılar tehlikede olduğunu kullanıcı hesaplarının bir listesini sağlar. 


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-user-at-risk/03.png)

Bir kullanıcı seçilmesi hello ilgili kullanıcı veri dikey penceresi açılır.
Risk altında olan kullanıcı için hello kullanıcının oturum açma geçmişini gözden geçirin ve gerekirse hello parola sıfırlama.

![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-user-at-risk/46.png)


Bu iletişim kutusu size şu seçeneği sunar:

- Merhaba raporu yükleyin

- Kullanıcılarda arama

![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-user-at-risk/16.png)


## <a name="azure-active-directory-premium-editions"></a>Azure Active Directory premium sürümleri

risk rapor hello Azure Active Directory premium sürümlerinde için işaretlenen hello kullanıcılar ile sağlar:

- Tehlikeye girmiş olabilecek [kullanıcı hesaplarının listesi](active-directory-identityprotection.md#users-flagged-for-risk) 

- Merhaba hakkında bilgiler birleştirilir [risk olayı türleri](active-directory-identity-protection-risk-events.md) , algılandı

- Bir seçenek toodownload hello raporu

- Bir seçenek tooconfigure bir [kullanıcı risk düzeltme İlkesi](active-directory-identityprotection.md#user-risk-security-policy)  


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-user-at-risk/71.png)

Bir kullanıcıyı seçtiğinizde bu kullanıcıya ilişkin, aşağıdakileri gerçekleştirmenize olanak tanıyan ayrıntılı bir rapor görünümü açılır:

- Tüm oturum açma işlemleri görüntülemek hello açın

- Merhaba kullanıcı parolasını sıfırlama

- Tüm olayları kapatabilirsiniz.

- Merhaba kullanıcı için bildirilen risk olaylarını araştırın. 


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-user-at-risk/324.png)


tooinvestigate bir risk olayı seçin hello listesi tooopen hello birinden **ayrıntıları** dikey penceresinde bu risk olay. Merhaba üzerinde **ayrıntıları** dikey penceresinde hello seçeneği tooeither sahip [el ile bir risk olayı kapatmak](active-directory-identityprotection.md#closing-risk-events-manually) veya el ile kapatılmış risk olayı yeniden etkinleştirme. 


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-user-at-risk/325.png)



## <a name="next-steps"></a>Sonraki adımlar

- Azure Active Directory Kimlik Koruması hakkında daha fazla bilgi için bkz. [Azure Active Directory Kimlik Koruması](active-directory-identityprotection.md).

