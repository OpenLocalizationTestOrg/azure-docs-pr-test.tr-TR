---
title: "aaaHow toorequire çok faktörlü kimlik doğrulaması | Microsoft Docs"
description: "Hello Azure Active Directory Privileged Identity Management uzantısı kimliklerle toorequire çok faktörlü kimlik doğrulaması (MFA) nasıl ayrıcalıklı öğrenin."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 1e3dc4ad-3a6a-4a52-8417-3ca4f84ae05c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: c08fad9dc80c09a14a4bd7497da4942fa227c3ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorequire-mfa-in-azure-ad-privileged-identity-management"></a>Nasıl toorequire Azure AD Privileged Identity Management MFA
Çok faktörlü kimlik doğrulaması (MFA) tüm yöneticilerinizi için ihtiyaç duyduğunuz öneririz. Merhaba tehlikeye tooa parola nedeniyle bir saldırı riskini azaltır.

Kullanıcılar oturum açtığında kullanıcılar bir MFA testini tamamlamanız gerekli kılabilirsiniz. Merhaba blog gönderisi [MFA Office 365 ve Azure MFA için](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/) Office ve Azure abonelikleri hello Microsoft Azure multi-Factor Authentication Sunumda bulunan hello özelliklerle içereceği karşılaştırır.

Ayrıca, Azure AD PIM rolünde etkinleştirdiğinizde kullanıcılar bir MFA testini tamamlamanız isteyebilirsiniz. Bu şekilde hello kullanıcı oturum açıp MFA testini tamamlanmadı, bunlar istendiğinde toodo olacaktır PIM tarafından bunu.

## <a name="requiring-mfa-in-azure-ad-privileged-identity-management"></a>Azure AD Privileged Identity Management MFA gerektirme
Ayrıcalıklı rol yöneticisi olarak PIM kimlikleri yönetirken, ayrıcalıklı hesaplar için MFA önerilir uyarıları görebilirsiniz. Merhaba güvenliği hello PIM Pano ve yeni bir dikey pencere uyarıda MFA gerektirmelidir hello yönetici hesapları bir listesi açılır.  Birden çok rolü seçerek ve ardından hello tıklatarak MFA'ya gerek duyabilirsiniz **düzeltme** düğmesini veya hello elipsler sonraki tooindividual roller'i tıklatın ve ardından hello **düzeltme** düğmesi.

> [!IMPORTANT]
> Şimdi, sağa Azure MFA yalnızca works iş veya Okul hesapları, değil Microsoft hesapları (Skype, Xbox, Outlook.com, vb. gibi tooMicrosoft Hizmetleri'ndeki toosign kullandığı genellikle bir kişisel hesap.). Rollerine MFA tooactivate kullanamadığından bu nedenle, herhangi bir Microsoft hesabı kullanarak uygun yönetim olamaz. Bu kullanıcılar bir Microsoft hesabı kullanarak iş yükleri yönetme toocontinue gerekiyorsa, şu an için toopermanent Yöneticiler Yükselt.
> 
> 

Ayrıca, hello hello PIM Pano rolleri bölümünü tıklayarak hello MFA gereksinimi belirli bir rol için değiştirebilirsiniz. Ardından, tıklatın **ayarları** hello rol dikey ve ardından seçerek **etkinleştirmek** çok faktörlü kimlik doğrulaması altında.

## <a name="how-azure-ad-pim-validates-mfa"></a>Azure AD PIM MFA nasıl doğrular
Bir kullanıcı bir rolünü etkinleştirirken MFA doğrulamak için iki seçenek vardır.

Merhaba basit bir ayrıcalıklı rolü etkinleştirme kullanıcılar için Azure MFA üzerinde toorely seçenektir. toodo kullanıcılarla gerekirse lisanslanır ve Azure MFA için kayıtlı Bu, ilk denetleyin. Nasıl toodo bu bulunduğu hakkında daha fazla bilgi [hello bulutta Azure multi Factor Authentication ile çalışmaya başlama](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md). Bu önerilir, ancak gerekli değildir, bunlar oturum açtığında bu kullanıcılar için Azure AD tooenforce MFA yapılandırın. Azure AD PIM tarafından kendisini Hello MFA denetimleri yapılacağından budur.

Alternatif olarak, kullanıcıların şirket içi kimlik doğrulaması, MFA için sorumlu kimlik sağlayıcınız olabilir. Örneğin, Azure AD erişmeden önce AD Federasyon Hizmetleri toorequire akıllı kart tabanlı kimlik doğrulaması yapılandırılmışsa [güvenliğini sağlama bulut kaynakları Azure multi-Factor Authentication ve AD FS ile](../multi-factor-authentication/multi-factor-authentication-get-started-adfs-cloud.md) yönergeleri içerir AD FS toosend talep tooAzure AD yapılandırmak için. Bir kullanıcı tooactivate rol çalıştığında, Azure AD PIM hello uygun talep aldıktan sonra MFA zaten hello kullanıcıdan doğrulandı olduğunu kabul eder.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

