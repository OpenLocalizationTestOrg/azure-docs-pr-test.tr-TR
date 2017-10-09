---
title: "aaaHow toocomplete erişim gözden geçirme | Microsoft Docs"
description: "Azure AD Privileged Identity Management erişim gözden geçirme başlatıldıktan sonra öğrenin nasıl toocomplete ve görünüm hello sonuçları"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: abc2d3dd-afd5-42cf-8a17-6c11f5674c35
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: f99ddf3ebcf80b51110326064d584f33d8e1679a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocomplete-an-access-review-in-azure-ad-privileged-identity-management"></a>Nasıl toocomplete access gözden Azure AD Privileged Identity Management
Ayrıcalıklı rol Yöneticiler gözden geçirebileceğiniz ayrıcalıklı erişim kez bir [güvenlik incelemesi başlatıldıysa](active-directory-privileged-identity-management-how-to-start-security-review.md). Azure AD Privileged Identity Management (PIM) otomatik olarak kullanıcılar tooreview bunların erişim isteyen bir e-posta gönderir. Bir kullanıcı bir e-posta almadığını varsa, bunları hello yönergeleri gönderebilirsiniz [nasıl tooperform güvenlik gözden](active-directory-privileged-identity-management-how-to-perform-security-review.md).

Merhaba güvenlik değerlendirme süresi sona erer veya tüm hello kullanıcılar kendi kendini gözden tamamladıktan sonra bu makale toomanage hello gözden hello adımları izleyin ve hello sonuçlarını görebilirsiniz.

## <a name="manage-security-reviews"></a>Güvenlik değerlendirmeleri yönetme
1. Toohello Git [Azure portal](https://portal.azure.com/) ve select hello **Azure AD Privileged Identity Management** Panonuzda uygulama.
2. Select hello **erişim incelemeler** başlangıç Panosu bölümü.
3. Merhaba erişim gözden geçirme toomanage istediğinizi seçin.

Merhaba erişim gözden geçirme 's ayrıntı dikey penceresinde bu gözden geçirme yönetmek için bir numara seçenekleri mevcuttur.

![PIM erişim gözden geçirme düğmeleri - ekran görüntüsü][1]

### <a name="remind"></a>Şu aralıklarla uyar
Böylece Hello kullanıcıların kendilerini gözden erişim gözden geçirme ayarlanıp ayarlanmadığını hello **Anımsat** düğmesi bir bildirim gönderir. 

### <a name="stop"></a>Durdur
Bitiş tarihi tüm erişim değerlendirmeleri sahip, ancak hello kullanabilirsiniz **durdurmak** düğmesini toofinish, erken. Tüm kullanıcılar bu zamana kadar gözden yapmadıysanız, bunlar hello gözden geçirme durdurmak mümkün tooafter olmayacaktır. Durdurulmuş sonra bir gözden geçirme yeniden başlatılamıyor.

### <a name="apply"></a>Başvurun
Bir erişim gözden geçirme tamamlandıktan sonra hello bitiş tarihi ulaşıldı veya el ile durduruldu çünkü ya da hello **Uygula** düğmesi uygulayan hello sonucu hello gözden geçirin. Bir kullanıcının erişimi hello incelemede reddedildiyse, kendi rol atamasını kaldıracak hello adım budur.  

### <a name="export"></a>Dışarı Aktarma
Tooapply hello hello güvenlik incelemesi sonuçlarını el ile istiyorsanız hello gözden geçirme dışarı aktarabilirsiniz. Merhaba **verme** düğmesi, bir CSV dosyası yükleme başlayacak. Excel veya CSV dosyalarını açma diğer programları hello sonuçlarını yönetebilirsiniz.

### <a name="delete"></a>Sil
Hello ilgilenen değilseniz daha fazla gözden, silin. Merhaba **silmek** düğmesini hello gözden geçirme hello PIM uygulama ' kaldırır.

> [!IMPORTANT]
> Değil silme oluşmadan önce bir uyarı almak, böylece gözden toodelete istediğiniz emin olun. 

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
