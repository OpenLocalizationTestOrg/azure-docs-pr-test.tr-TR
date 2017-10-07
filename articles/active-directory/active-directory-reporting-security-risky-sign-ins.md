---
title: "aaaRisky oturum açma işlemleri raporu hello Azure Active Directory portalında | Microsoft Docs"
description: "Merhaba riskli oturum açma işlemleri raporu hello Azure Active Directory portalında hakkında bilgi edinin"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: 7728fcd7-3dd5-4b99-a0e4-949c69788c0f
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d8df5cafea6b38f3e364c24a6aff599abe088e88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="risky-sign-ins-report-in-hello-azure-active-directory-portal"></a>Hello Azure Active Directory portalında riskli oturum açma işlemleri raporu

Merhaba güvenlik raporları Azure Active Directory'de (Azure AD) ile ortamınızda ele geçirilen kullanıcı hesapları hello olasılığını Öngörüler elde edebilirsiniz. 

Azure AD, ilgili tooyour kullanıcı hesapları olan şüpheli eylemleri algılar. Algılanan her eylem için *risk olayı* adlı bir kayıt oluşturulur. Daha ayrıntılı bilgi için bkz. [Azure Active Directory risk olayları](active-directory-identity-protection-risk-events.md). 

Merhaba risk olaylarını kullanılan toocalculate algıladı:

- **Riskli oturum açma işlemleri** -bir riskli oturum açma bir hello meşru bir kullanıcı hesabının sahibi olmayan kişi tarafından gerçekleştirilmiş olabilecek bir oturum açma girişimi için göstergesidir. Daha fazla bilgi için bkz. [Riskli oturum açma işlemleri](active-directory-identityprotection.md#risky-sign-ins). 

- **Riskli oldukları belirlenen kullanıcılar** - Riskli kullanıcı, güvenliği tehlikeye girmiş olabilecek bir kullanıcı hesabının göstergesidir. Daha fazla bilgi için bkz. [Riskli oldukları belirlenen kullanıcılar](active-directory-identityprotection.md#users-flagged-for-risk).  

İçinde [Azure portal hello](https://portal.azure.com), hello güvenlik raporları hello üzerinde bulabilirsiniz **Azure Active Directory** dikey penceresinde hello **güvenlik** bölümü. 

![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-risky-sign-ins/10.png)


## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a>Hangi Azure AD lisans tooaccess bir güvenlik raporu gerekiyor mu?  

Azure Active Directory'nin tüm sürümlerinde size riskli oturum açma işlemleri raporları sağlanır.  
Bununla birlikte, rapor ayrıntı düzeyini hello hello sürümleri arasında farklılık gösterir: 

- Merhaba, **Azure Active Directory ücretsiz ve Basic sürümleri**, zaten riskli oturum açma işlemleri listesini alın. 

- Merhaba **Azure Active Directory Premium 1** edition'ı genişletir bu modeli de tooexamine sağlayarak her rapor için algılanan risk olayı temel hello bazıları. 

- Merhaba **Azure Active Directory Premium 2** edition, ayrıca, otomatik olarak tooconfigured yanıt tooconfigure güvenlik ilkeleri sağlar ve tüm temel alınan risk olaylar hakkında bilgi en ayrıntılı hello ile sağlar risk düzeyleri.



## <a name="azure-active-directory-free-and-basic-edition"></a>Azure Active Directory ücretsiz ve temel sürümleri

Hello Azure Active Directory ücretsiz ve basic sürümleri, kullanıcılarınız için riskli oturum açma, algılanmış olan işlemleri, bir listesi sağlanmaktadır. Bu raporda şunlar listelenmiştir:

- **Kullanıcı** - hello hello oturum açma işlemi sırasında kullanılan hello kullanıcı adı
- **IP** -hello kullanılan tooconnect tooAzure Active Directory olduğu hello aygıtın IP adresi
- **Konum** -başlangıç konumu kullanılan tooconnect tooAzure Active Directory
- **Oturum açma saatini** -hello zaman zaman hello oturum açma gerçekleştirilir
- **Durum** -hello hello oturum açma durumu


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-risky-sign-ins/01.png)

Araştırmanızı hello riskli oturum açma, bağlı olarak, geri bildirim tooAzure biçiminde hello eylemleri aşağıdaki Active Directory sağlayabilirsiniz:

- Çözümleme
- Yanlış pozitif olarak işaretleme
- Yoksayma
- Yeniden etkinleştirme

![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-risky-sign-ins/21.png)

Daha fazla ayrıntı için bkz. [Risk olaylarını elle kapatma](active-directory-identityprotection.md#closing-risk-events-manually).

Bu rapor size şu seçeneği sağlar:

- Kaynaklarda ara
- Merhaba rapor verilerini indirme


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-risky-sign-ins/93.png)


## <a name="azure-active-directory-premium-editions"></a>Azure Active Directory premium sürümleri

Merhaba riskli oturum açma işlemleri raporu hello Azure Active Directory premium sürümlerinde ile sağlar:

- Merhaba hakkında bilgiler birleştirilir [risk olayı türleri](active-directory-identity-protection-risk-events.md) , algılandı

- Bir seçenek toodownload hello raporu


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-risky-sign-ins/456.png)


Bir risk olayını seçtiğinizde bu risk olayına ilişkin, aşağıdakileri gerçekleştirmenize olanak tanıyan ayrıntılı bir rapor görünümü açılır:

- Bir seçenek tooconfigure bir [kullanıcı risk düzeltme İlkesi](active-directory-identityprotection.md#user-risk-security-policy)  

- Gözden geçirme hello algılama hello risk olayı için zaman çizelgesi  

- Bu risk olayının hangi kullanıcılarla ilgili olarak algılandığının listesini gözden geçirebilirsiniz.

- [Risk olayını elle kapatabilir](active-directory-identityprotection.md#closing-risk-events-manually) ya da elle kapatılmış bir risk olayını yeniden etkinleştirebilirsiniz. 


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-risky-sign-ins/457.png)

Bir kullanıcıyı seçtiğinizde bu kullanıcıya ilişkin, aşağıdakileri gerçekleştirmenize olanak tanıyan ayrıntılı bir rapor görünümü açılır:

- Tüm oturum açma işlemleri görüntülemek hello açın

- Merhaba kullanıcı parolasını sıfırlama

- Tüm olayları kapatabilirsiniz.

- Merhaba kullanıcı için bildirilen risk olaylarını araştırın. 


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-risky-sign-ins/324.png)


tooinvestigate bir risk olayı hello listeden birini seçin.  
Merhaba açılır **ayrıntıları** dikey penceresinde bu risk olay. Merhaba üzerinde **ayrıntıları** dikey penceresinde hello seçeneği tooeither sahip [el ile bir risk olayı kapatmak](active-directory-identityprotection.md#closing-risk-events-manually) veya el ile kapatılmış risk olayı yeniden etkinleştirme. 


![Riskli Oturum Açma İşlemleri](./media/active-directory-reporting-security-risky-sign-ins/325.png)





## <a name="next-steps"></a>Sonraki adımlar

- Azure Active Directory Kimlik Koruması hakkında daha fazla bilgi için bkz. [Azure Active Directory Kimlik Koruması](active-directory-identityprotection.md).

