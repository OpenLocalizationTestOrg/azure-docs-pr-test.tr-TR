---
title: "Bir erişim gözden geçirme tamamlama | Microsoft Docs"
description: "Azure AD Privileged Identity Management erişim gözden geçirme başlatıldıktan sonra tamamlamak ve sonuçları görüntüleme hakkında bilgi edinin"
services: active-directory
documentationcenter: 
author: billmath
manager: mtillman
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
ms.openlocfilehash: 3866438de8fba7a6c42777bbb57746eadf1158eb
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/11/2017
---
# <a name="how-to-complete-an-access-review-in-azure-ad-privileged-identity-management"></a>Azure AD Privileged Identity Management erişim incelemede tamamlama
Ayrıcalıklı rol Yöneticiler gözden geçirebileceğiniz ayrıcalıklı erişim kez bir [güvenlik incelemesi başlatıldıysa](active-directory-privileged-identity-management-how-to-start-security-review.md). Azure AD Privileged Identity Management (PIM) otomatik olarak erişimleri gözden geçirmek için kullanıcıların isteyen bir e-posta gönderir. Bir kullanıcı bir e-posta almadığını varsa, bunları yönergeleri gönderebilirsiniz [güvenlik incelemesi gerçekleştirme](active-directory-privileged-identity-management-how-to-perform-security-review.md).

Güvenlik değerlendirme süresi sona erer veya tüm kullanıcılar kendi kendini gözden tamamladıktan sonra gözden geçirme yönetmek ve sonuçları görmek için bu makaledeki adımları izleyin.

## <a name="manage-security-reviews"></a>Güvenlik değerlendirmeleri yönetme
1. Git [Azure portal](https://portal.azure.com/) seçip **Azure AD Privileged Identity Management** Panonuzda uygulama.
2. Seçin **erişim incelemeler** bölümü.
3. Yönetmek istediğiniz erişim gözden geçirme seçin.

Erişim gözden geçirme 's ayrıntı dikey penceresinde bu gözden geçirme yönetmek için bir numara seçenekleri mevcuttur.

![PIM erişim gözden geçirme düğmeleri - ekran görüntüsü][1]

### <a name="remind"></a>Anımsat
Böylece kullanıcılar kendileri gözden erişim gözden geçirme ayarlanıp ayarlanmadığını **Anımsat** düğmesi bir bildirim gönderir. 

### <a name="stop"></a>Durdur
Bitiş tarihi tüm erişim değerlendirmeleri sahip, ancak kullanabileceğiniz **durdurmak** erken bitirme düğmesi. Tüm kullanıcılar bu zamana kadar gözden yapmadıysanız, gözden geçirme durdurduktan sonra için değiştiremezler. Durdurulmuş sonra bir gözden geçirme yeniden başlatılamıyor.

### <a name="apply"></a>Başvurun
Bir erişim gözden geçirme tamamlandıktan sonra da bitiş tarihi ulaşıldı veya el ile durduruldu çünkü **Uygula** düğmesi gözden sonucunu uygular. Bir kullanıcının erişimi incelemede reddedildiyse, kendi rol atamasını kaldıracak adım budur.  

### <a name="export"></a>Dışarı Aktarma
Güvenlik incelemesi sonuçlarını el ile uygulamak istiyorsanız, gözden geçirme dışarı aktarabilirsiniz. **Verme** düğmesi, bir CSV dosyası yükleme başlayacak. Excel veya CSV dosyalarını açma diğer programları sonuçlarını yönetebilirsiniz.

### <a name="delete"></a>Sil
Başka incelemede değil ilgileniyorsanız, dosyayı silin. **Silmek** düğmesini gözden geçirme PIM uygulamasını kaldırır.

> [!IMPORTANT]
> Değil silme oluşmadan önce bir uyarı almak, böylece bu gözden geçirme silmek istediğinizden emin olun. 

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
