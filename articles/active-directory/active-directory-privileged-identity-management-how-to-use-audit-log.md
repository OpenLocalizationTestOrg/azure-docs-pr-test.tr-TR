---
title: "Azure AD Privileged Identity Management aaaHow toouse hello Denetim günlüğüne | Microsoft Docs"
description: "Nasıl toouse hello denetim günlüğünü hello Azure Privileged Identity Management uzantısı'nda öğrenin."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 5d13a6dd-1fcb-4e76-82fb-cb2f4f0e4357
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 36987eaab9fe02c5dd7b4f4705e487299430745d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-audit-log-in-pim"></a>PIM içinde Hello denetim günlüğünü kullanma
Belirli bir süre içinde tüm hello kullanıcısı atamalarını ve etkinleştirmeler hello ayrıcalıklı Kimlik Yönetimi (PIM) denetim günlüğü toosee'yı kullanabilirsiniz. Yönetici, son kullanıcı ve eşitleme etkinliği de dahil olmak üzere, kiracınızda etkinliğinin toosee hello tam denetim geçmişi istiyorsanız hello kullanabilirsiniz [Azure Active Directory'ye erişim ve kullanım raporları.](active-directory-view-access-usage-reports.md)

## <a name="navigate-toohello-audit-log"></a>Toohello denetim günlüğü gidin
Merhaba gelen [Azure portal](https://portal.azure.com) Pano, select hello **Azure AD Privileged Identity Management** uygulama. Tıklayarak hello denetim günlüğü buradan, erişim **yönetmek ayrıcalıklı rolleri** > **denetim geçmişi** hello PIM panosunda.

## <a name="hello-audit-log-graph"></a>Merhaba denetim günlüğü grafiği
Bir çizgi grafiğinde hello denetim günlüğü tooview hello toplam etkinleştirmeler, günde en çok etkinleştirmeleri ve gün başına ortalama etkinleştirmeleri kullanabilirsiniz.  Merhaba denetim geçmişi birden fazla rol varsa hello veri role göre filtre uygulayabilirsiniz.

Kullanım hello **zaman**, **eylem**, ve **rol** düğmeleri toosort hello günlük.

## <a name="hello-audit-log-list"></a>Merhaba denetim günlüğü listesi
Merhaba denetim günlüğü listesinde Hello sütunlar şunlardır:

* **İstek sahibi** -hello rol etkinleştirme veya değiştirme isteyen hello kullanıcı.  Merhaba değer "Azure sistemi" ise, daha fazla bilgi için hello Azure denetim günlüğünü denetleyin.
* **Kullanıcı** -etkinleştiriyor veya tooa rolü atanmış hello kullanıcı.
* **Rol** -hello rolü atanmış veya hello kullanıcı tarafından etkinleştirilmiş.
* **Eylem** - hello istek sahibi tarafından yapılan hello eylemler. Bu atama, atamayı kaldırma konusunda, etkinleştirme veya devre dışı bırakma içerebilir.
* **Zaman** - hello eylem oluştuğunda.
* **Akıl** -herhangi bir metin hello neden alanına etkinleştirme sırasında girilen varsa, burada gösterir.
* **Sona erme** - rol etkinleştirmesi için yalnızca ilgili.

## <a name="filter-hello-audit-log"></a>Filtre hello denetim günlüğü
Merhaba tıklayarak hello Denetim günlüğüne görüntülenir hello bilgileri filtreleyebilirsiniz **filtre** düğmesi.  Merhaba **güncelleştirme Grafik Parametreler dikey** görünür.

Merhaba filtreleri ayarladıktan sonra tıklayın **güncelleştirme** hello günlük toofilter hello verileri.  Merhaba veri hemen görünmüyorsa, hello sayfayı yenileyin.

### <a name="change-hello-date-range"></a>Merhaba tarih aralığını Değiştir
Kullanım hello **Bugün**, **geçen hafta**, **geçen ay**, veya **özel** hello denetim günlüğü toochange hello zaman aralığını düğmeler.

Merhaba seçtiğinizde **özel** düğmesi, size sunulur bir **gelen** tarih alanı ve bir **için** alan toospecify hello günlüğü için tarih aralığını tarih.  AA/GG/YYYY biçiminde hello tarihleri girin veya üzerinde hello tıklatın **Takvim** simgesini ve bir takvimden hello tarih seçin.

### <a name="change-hello-roles-included-in-hello-log"></a>Merhaba günlüğüne dahil hello rollerini değiştirme
İşaretleyin veya işaretini kaldırın hello **rol** onay kutusunu sonraki tooeach rol tooinclude veya hariç tutma hello oturumunuzu.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

