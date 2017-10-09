---
title: "aaaHow toostart erişim gözden geçirme | Microsoft Docs"
description: "Toocreate erişimini nasıl gözden hello Azure Privileged Identity Management uygulaması ile ayrıcalıklı kimlikleri için öğrenin."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 3e52b731-55f4-4c8a-ba87-9fd34033f52f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 24feac307f77c69b5d68d6ae0623dbcb52416b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostart-an-access-review-in-azure-ad-privileged-identity-management"></a>Nasıl toostart access gözden Azure AD Privileged Identity Management
Kullanıcılar ayrıcalıklı artık gerekmeyen erişimi olan, rol atamaları "eski" olur. Bu eski rol atamaları ile ilişkili sipariş tooreduce hello riskine ayrıcalıklı rol Yöneticiler düzenli olarak kullanıcılara verilen hello rolleri gözden geçirmelidir. Bu belge, Azure AD Privileged Identity Management (PIM) erişim gözden geçirme başlatmak için hello adımlar kapsanmaktadır.

## <a name="start-an-access-review"></a>Bir erişim incelemesi başlatma
> [!NOTE]
> Hello Azure portal hello PIM uygulama tooyour Panosu eklemediyseniz, hello adımlara bakın [Azure Privileged Identity Management ile çalışmaya başlama](active-directory-privileged-identity-management-getting-started.md)
> 
> 

Merhaba PIM uygulama ana sayfası, bir erişim gözden geçirme üç yolu toostart vardır:

* **Erişim incelemeler** > **Ekle**
* **Rolleri** > **gözden geçirme** düğmesi
* Select hello belirli rol toobe gözden hello rollerinin listesinden > **gözden geçirme** düğmesi

Merhaba üzerinde tıkladığınızda **gözden** hello düğmesi, **erişim incelemesi başlatma** dikey penceresi görünür. Bu dikey giderek tooconfigure hello gözden bir ada sahip olduğunuz ve sınırı süresi, bir rol tooreview seçin ve hello gözden geçirme işlemini gerçekleştirecek karar verin.

![-Ekran görüntüsü bir erişim incelemesi başlatma][1]

### <a name="configure-hello-review"></a>Merhaba gözden geçirme yapılandırın
access toocreate gözden geçirin, tooname ve bir başlangıç ve bitiş tarihi kümesi gerekir.

![Gözden geçirme - ekran görüntüsü yapılandırma][2]

Merhaba uzunluğu yeteri kadar kullanıcılar toocomplete için gözden hello olun. Merhaba bitiş tarihinden önce son varsa, her zaman hello gözden geçirme erken durdurabilirsiniz.

### <a name="choose-a-role-tooreview"></a>Bir rol tooreview seçin
Her gözden geçirme sadece tek bir rol üzerinde odaklanmıştır. Belirli bir rol dikey penceresinden hello erişim gözden geçirme başlattığınız sürece toochoose rol artık gerekir.

1. Çok gidin**rol üyeliğini gözden geçirin**
   
    ![Gözden geçirme rol üyeliğini - ekran görüntüsü][3]
2. Bir rol hello listeden seçin.

### <a name="decide-who-will-perform-hello-review"></a>Merhaba gözden geçirme işlemini gerçekleştirecek karar verin
Bir gözden geçirme gerçekleştirmek için üç seçenek vardır. Merhaba gözden geçirme toosomeone atayabilirsiniz başka toocomplete kendiniz yapabileceğiniz ya da kendi access gözden her kullanıcının olabilir.

1. Çok gidin**gözden geçirenler seçin**
   
    ![Gözden geçirenler - ekran görüntüsü seçin][4]
2. Merhaba seçeneklerden birini seçin:
   
   * **Select İnceleme**: erişim gerek duyan bilmiyorsanız bu seçeneği kullanın. Bu seçenek ile Merhaba gözden geçirme tooa kaynak sahibi veya grup yöneticisi toocomplete atayabilirsiniz.
   * **Bana**: toopreview nasıl istiyorsanız yararlı olamaz kişilerin adına tooreview istediğiniz veya erişim iş gözden geçirir.
   * **Üyeleri kendilerini gözden**: Bu seçenek toohave hello kullanıcılar gözden kendi rol atamalarını kullanın.

### <a name="start-hello-review"></a>Merhaba incelemesi başlatma
Son olarak, kullanıcılar erişimleri onaylıyorsanız bir gerekçe sağlamasını hello seçeneği toorequire sahip. Merhaba gözden geçirme açıklamasını isterseniz ekleyin ve seçin **Başlat**.

Kullanıcılarınız kendileri için bekleyen bir erişim gözden geçirme olduğunu biliyor ve bunları Göster izin emin olun [tooperform erişimini nasıl gözden](active-directory-privileged-identity-management-how-to-perform-security-review.md).

## <a name="manage-hello-access-review"></a>Merhaba erişim gözden geçirme yönetme
Merhaba gözden geçirenler hello Azure AD PIM Pano içinde kendi incelemeler tamamlarken hello ilerleme durumunu izleyebilirsiniz, hello erişim bölümü gözden geçirir. Erişim hakları yok kadar hello dizininde değiştirilecek [hello İnceleme tamamlandıktan](active-directory-privileged-identity-management-how-to-complete-review.md).

Merhaba gözden geçirme süresi bitene kadar kullanıcılar toocomplete gözden anımsatmak veya Dur hello gözden geçirme, hello erişimden erken bölümü gözden geçirir..

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="pim-table-of-contents"></a>PIM İçindekiler
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
