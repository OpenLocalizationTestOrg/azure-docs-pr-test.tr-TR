---
title: aaaAzure Active Directory raporlama bildirimleri
description: "Nasıl toouse hello şüpheli oturum için Azure Active Directory raporlama bildirimleri bileşenleri."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ae6d4b0e-5931-4cb3-98bf-9be91b381c92
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.custom: oldportal
ms.reviewer: dhanyahk
ms.openlocfilehash: 3843c45eaf9d68e671943bfdbc7ab68933f38fbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-notifications"></a>Azure Active Directory raporlama bildirimleri
## <a name="what-reports-generate-email-notifications"></a>E-posta bildirimleri hangi raporlar oluşturur
Şu anda yalnızca hello düzensiz oturum Etkinlik Raporu Tetikleyicileri e-posta bildirimleri.

## <a name="what-is-an-irregular-sign-in"></a>Bir "düzensiz oturum açma" nedir?
Düzensiz oturum açma işlemleri bizim machine learning algoritmaları, bir oturum açma anormal konum ve cihaz ile birlikte bir "mümkün olmayan seyahat" koşulun hello temelinde tarafından tanımlanmış izinlerdir. Bu, bir bilgisayar korsanının bu hesabı kullanarak toosign çalışıyor olduğunu gösteriyor olabilir.

## <a name="who-receives-hello-email-notifications"></a>Kimin hello e-posta bildirimleri alan?
bir Active Directory Premium lisansı atanmış olan tooall genel Yöneticiler Hello e-posta gönderilir. teslim tooensure, biz de toohello admins alternatif e-posta adresi göndermek. Yöneticileri içermelidir aad-alerts-noreply@mail.windowsazure.com hello e-posta kaçırmamak için kendi Güvenilir Gönderenler listesinde.

## <a name="how-often-are-these-emails-sent"></a>Gönderilen bu e-postaları ne sıklıkla misiniz?
Merhaba e-posta, 10 yeni düzensiz oturum açma etkinliklerini hello son 30 günde bir yapılır ya da hello son e-posta gönderilip gönderilmediğini olduğundan, hangisi daha az ise gönderilir.

## <a name="how-do-i-access-hello-report-mentioned-in-hello-email"></a>Merhaba e-postayla bahsedilen hello raporu nasıl erişirim?
Merhaba bağlantısına tıkladığınızda, yeniden yönlendirilen toohello rapor sayfasının hello Klasik Azure portalı içinde olacaktır. Sırayla tooaccess rapor Merhaba, toobe hem gerekir:

* Bir yönetici veya Azure aboneliğinizin ortak yönetici
* Merhaba dizininde genel yönetici ve bir Active Directory Premium lisansı atanmış. Daha fazla bilgi için bkz. [Azure Active Directory sürümleri](active-directory-editions.md).

## <a name="can-i-turn-off-these-emails"></a>Bu e-postaları kapatabilir miyim?
Evet, bildirimler devre dışı tooturn tooanomalous oturum açma işlemleri hello Klasik Azure portalı içinde ilgili, tıklatın **yapılandırma**ve ardından **devre dışı** hello altında **bildirimleri**bölümü.

## <a name="whats-next"></a>Sırada ne var?
* Hangi güvenlik, Denetim ve etkinlik raporları kullanılabilir merak ediyor? Kullanıma [Azure AD güvenlik, Denetim ve etkinlik raporları](active-directory-view-access-usage-reports.md)
* [Azure Active Directory Premium ile çalışmaya başlama](active-directory-get-started-premium.md)
* [Tooyour oturum aç ve erişim paneli sayfalarınıza şirket markası ekleme](active-directory-add-company-branding.md)

