---
title: "aaaAzure Privileged Identity Management onay iş akışları | Microsoft Docs"
description: "Onay iş akışları ayrıcalıklı Kimlik Yönetimi'nın (PIM) hakkında bilgi edinin"
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: 4afaf5c138798a803eb3d3b7905b9361d65792cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="approvals-preview"></a>Onaylar (Önizleme)

## <a name="overview"></a>Genel Bakış

Onaylarıyla Privileged Identity Management için rolleri toorequire onay etkinleştirme için yapılandırmak ve bir veya birden çok kullanıcı veya grup olarak yetkilendirilmiş onaylayanlar seçin. Toolearn nasıl okumaya devam edin tooconfigure roller ve onaylayanlar seçin.

>[!NOTE]
Lütfen bu özelliği geliştirilme aşamasındadır göz önünde bulundurun ve hatalar karşılaşabilirsiniz. Merhaba işlevselliği, metin dahil ve adlandırma kuralları değiştirilebilir ve son düşünülmemelidir.


## <a name="key-terminology"></a>Anahtar terminolojisi

*Uygun rol kullanıcı* – kuruluşunuzdaki tooan Azure AD rolü uygun olarak atanmış bir kullanıcı bir uygun rol olduğu (Rol etkinleştirmesi gerekir).

*Onaylayan temsilci* – bir temsilci onaylayan bir veya birden çok kişiler rol etkinleştirme isteklerini onaylama için sorumlu olan grupları, Azure AD içinde mi.

## <a name="scenarios"></a>Senaryolar

Merhaba özel Önizleme hello aşağıdaki senaryoları destekler:

**Bir ayrıcalıklı Rol Yöneticisi (PRA) olarak şunları yapabilirsiniz:**

-   [belirli roller onayını etkinleştir](#enable-approval-for-specific-roles)

-   [Onaylayan kullanıcılara ve/veya grupları tooapprove istekleri belirtin](#specify-approver-users-and/or-groups-to-approve-requests)

-   [tüm ayrıcalıklı rolleri için istek ve onay geçmişini görüntüleme](#view-request-and-approval-history-for-all-privileged-roles)

**Belirlenen onaylayıcı olarak, şunları yapabilirsiniz:**

-   [Bekleyen onaylar (istek) görüntüleme](#view-pending-approvals-requests)

-   [onaylama veya reddetme rol yükseltme (tek ve/veya toplu) istekleri](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk)

-   [my onay/reddetme için gerekçe](#provide-justification-for-my-approval/rejection) 

**Uygun bir Role kullanıcı olarak şunları yapabilirsiniz:**

-   [onay gerektiren bir rolü etkinleştirme isteği](#request-activation-of-a-role-that-requires-approval)

-   [İstek tooactivate hello durumunu görüntüleme](#view-the-status-of-your-request-to-activate)

-   [etkinleştirme onaylanırsa Azure AD'de Görevinizi tamamlamak](#complete-your-task-in-azure-ad-if-activation-was-approved)

### <a name="navigation"></a>Gezinme

Biz hello Gezinti toosupport onayları güncelleştirdikten

![](media/azure-ad-pim-approval-workflow/image001.png)

Merhaba varsayılan giriş sayfası PIM ve hello yeni onayları belgeler hakkında uygun erişim tooinformation sağlar.

![](media/azure-ad-pim-approval-workflow/image002.png)

PIM, 'My denetim Geçmişi' tüm kullanıcılar için yeni bir bölüm de ekledik. Burada tüm hello bilgi ilgili tooyour kimlik bulabilirsiniz. Bu seçenek, tüm bekleyen ve tamamlanmış istekleri, çözümlemeniz hello istekleri hakkında yaptığınız kararları ve tüm son rol etkinleştirme tek bir konumda içerir.

![](media/azure-ad-pim-approval-workflow/image003.png)

### <a name="enable-approval-for-specific-roles"></a>Belirli roller onayını etkinleştir

belirli bir rol tooenable onaya hello sol gezinti bölmesinden ilk dizin rol seçin.

![](media/azure-ad-pim-approval-workflow/image004.png)

Bulma ve hello Directory rolleri sol gezinti ayarlarını seçin

![](media/azure-ad-pim-approval-workflow/image006.png)

Ayrıcalıklı rolleri seçin:

![](media/azure-ad-pim-approval-workflow/image009.png)

Hello seçin "Etkinleştir" onay bölümüne gerektirir:

![](media/azure-ad-pim-approval-workflow/image011.png)

Bir kez etkinleştirildikten sonra hello dikey penceresinde aşağıdaki ayrıntılara tooshow hello genişletin:

![](media/azure-ad-pim-approval-workflow/image013.png)

>[!NOTE]
VERMEYİN herhangi onaylayanlar belirtirseniz, hello PRA(s) hello varsayılan approver(s) haline gelir. Bu rol için tüm etkinleştirme istekleri gerekli tooapprove pra(s) olacaktır.

### <a name="specify-approver-users-andor-groups-tooapprove-requests"></a>Onaylayan kullanıcılara ve/veya grupları tooapprove istekleri belirtin

toodelegate onay hello seçeneğini çok onaylayanlar "Seç":

![](media/azure-ad-pim-approval-workflow/image015.png)

Merhaba Select onaylayanlar dikey yüklediğinde, belirli bir kullanıcı veya grup hello üst veya hello önceden doldurulmuş haldedir listeden seçerek hello arama çubuğunu kullanarak arayın ve sonra "bittiğinde," Seç:

![](media/azure-ad-pim-approval-workflow/image017.png)

Not: Bir defada birden çok kullanıcı veya grup seçebilirsiniz.

Seçiminiz hello seçili onaylayanlar listesinde aşağıda görüldüğü gibi görünür:

![](media/azure-ad-pim-approval-workflow/image019.png)

tooremove onaylayıcı, yalnızca hello Kaldır düğmesini sonraki tootheir adını tıklatın.

tooadd ek onaylayanlar, yineleme hello işlemi.

## <a name="view-request-and-approval-history-for-all-privileged-roles"></a>Tüm ayrıcalıklı rolleri için istek ve onay geçmişini görüntüleme

tüm ayrıcalıklı rolleri için tooview istek ve onay geçmişini hello panodan denetim geçmişi seçin:

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
Eylem tarafından hello verileri sıralamak ve "Etkinleştirme onaylanmış" bakın

### <a name="view-pending-approvals-requests"></a>Bekleyen onaylar (istek) görüntüleme

Onayınızı bekleyen istek olduğunda, bir temsilci onaylayan e-posta bildirimleri alırsınız. tooview bu istekleri hello panosunda (Merhaba yeni gezinti) select hello "beklemedeki onay istekleri" sekmesinden hello PIM portalında gezinti çubuğu kalmadı.

![](media/azure-ad-pim-approval-workflow/image023.png)

Burada, onay bekleyen isteklerin listesini görürsünüz:

![](media/azure-ad-pim-approval-workflow/image024.png)

### <a name="approve-or-reject-requests-for-role-elevation-single-andor-bulk"></a>Onaylama veya reddetme rol yükseltme (tek ve/veya toplu) istekleri

Tooapprove istediğiniz ya da reddetme hello isteklerini seçin ve kararınızı ile karşılık gelen eylem çubuğunda hello düğmesini tıklatın:

![](media/azure-ad-pim-approval-workflow/image025.png)

### <a name="provide-justification-for-my-approvalrejection"></a>My onay/reddetme için gerekçe

Bu yeni bir dikey tooapprove açın veya birden çok isteği aynı anda reddedin. Kararınızı için bir gerekçe girin ve Onayla (veya reddetme) hello alt veya hello dikey:

![](media/azure-ad-pim-approval-workflow/image029.png)

Merhaba isteği işlemi tamamlandığında, hello durum simgesinde yaptığınız karar yansıtılacaktır (Bu örnekte, hello onaylama karardır):

![](media/azure-ad-pim-approval-workflow/image031.png)

### <a name="request-activation-of-a-role-that-requires-approval"></a>Onay gerektiren bir rolü etkinleştirme isteği

Etkinleştirme ya da hello eski PIM hello yeni gezinti veya onay başlatılabilir gerektiren bir rolün isteyen, rol etkinleştirme kalır hello işlem olarak aynı hello. Yalnızca bir rolü etkinleştirmek için roller hello listeden seçin:

![](media/azure-ad-pim-approval-workflow/image033.png)

Ayrıcalıklı rol çok faktörlü kimlik doğrulaması gerektiriyorsa, önce bu görevi tamamlamak için istenir:

![](media/azure-ad-pim-approval-workflow/image035.png)

Tamamlandıktan sonra Etkinleştir'i tıklatın ve bir gerekçe (gerekliyse):

![](media/azure-ad-pim-approval-workflow/image037.png)

Merhaba istek sahibi onay bekleyen istek hello bir bildirim olduğunu görürsünüz:

![](media/azure-ad-pim-approval-workflow/image039.png)

### <a name="view-hello-status-of-your-request-tooactivate"></a>İstek tooactivate hello durumunu görüntüleme

Bekleyen isteği tooactivate Hello durumunu görüntüleme yeni gezinti bölmesinden erişilmesi gerekir. Merhaba sol gezinti çubuğu'ndan hello "İsteklerim" sekmesini seçin:

![](media/azure-ad-pim-approval-workflow/image041.png)

Merhaba istek durumu varsayılan olarak çok "Bekliyor", ancak tüm toosee geçiş yapabilir veya reddedilen istek sayısı.

### <a name="complete-your-task-in-azure-ad-if-activation-was-approved"></a>Etkinleştirme onaylanırsa Azure AD'de Görevinizi tamamlamak

Merhaba istek onaylandıktan sonra hello rolü etkin ve bu rol gerektiren herhangi bir iş ile devam edebilirsiniz.

![](media/azure-ad-pim-approval-workflow/image043.png)

## <a name="next-steps"></a>Sonraki adımlar

Geri bildiriminiz değerlidir toous. Lütfen ücretsiz tooshare açıklamaları veya Geri bildiriminiz bizim için burada eşitleyerek!
