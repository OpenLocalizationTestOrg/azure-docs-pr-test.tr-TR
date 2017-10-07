---
title: "aaaAzure Active Directory kimlik koruması bildirimleri | Microsoft Docs"
description: "Bildirimleri araştırma etkinliklerinizi'ı nasıl desteklediğini öğrenin."
services: active-directory
keywords: "Azure active directory kimlik koruması, cloud app discovery'yi, uygulamalar, güvenlik, risk, risk düzeyi, güvenlik açığı, güvenlik ilkesi yönetme"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 65ca79b9-4da1-4d5b-bebd-eda776cc32c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 19e62374873f034591c658a779f97d935766c612
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-notifications"></a>Azure Active Directory kimlik koruması bildirimleri
Azure AD kimlik koruması iki tür otomatik bildirim e-postalar yönettiğiniz toohelp kullanıcı risk ve risk olaylarını gönderir:

* Kullanıcı uyarı e-posta güvenliği
* Haftalık Özet e-posta

## <a name="user-compromised-alert-email"></a>Kullanıcı uyarı e-posta güvenliği
Azure AD Identity Protection tehlikeye gibi bir hesap belirlediğinde kullanıcı güvenliği aşılmış bir e-posta uyarısı oluşturulur. Merhaba e-posta bayrak eklenen kullanıcılar hello Identity Protection panosunda risk rapor için bir bağlantı toohello içerir. Güvenliği aşılmış hesapları bildirimleri hemen araştırın öneririz.

## <a name="weekly-digest-email"></a>Haftalık Özet e-posta
Merhaba Haftalık Özet e-posta yeni risk olaylarını özetini içerir.<br>
Aşağıdakileri içerir:

* Risk altındaki kullanıcılar
* Kuşkulu etkinlikler
* Algılanan güvenlik açıkları
* Kimlik koruması raporlarda bağlantılar toohello ilgili

<br>
![Düzeltme](./media/active-directory-identityprotection-notifications/400.png "düzeltme")
<br>

Haftalık Özet e-posta gönderme devre dışı geçiş yapabilirsiniz.
<br><br>
![Kullanıcı riskleri](./media/active-directory-identityprotection-notifications/62.png "kullanıcı riskleri")
<br>

**tooopen hello ilgili yapılandırma iletişim**:

1. Merhaba üzerinde **Azure AD Identity Protection** dikey penceresinde tıklatın **ayarları**.
   <br><br>
   ![Kullanıcı risk ilkesine](./media/active-directory-identityprotection-notifications/401.png "kullanıcı risk İlkesi")
   <br>
2. Merhaba, **genel** 'yi tıklatın **bildirimleri**.
   <br><br>
   ![Kullanıcı risk ilkesine](./media/active-directory-identityprotection-notifications/405.png "kullanıcı risk İlkesi")
   <br>

## <a name="see-also"></a>Ayrıca bkz.
* [Azure Active Directory kimlik koruması](active-directory-identityprotection.md)
