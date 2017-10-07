---
title: "Azure AD Connect Eşitleme Hizmeti Yöneticisi'ni işlemleri | Microsoft Docs"
description: "Merhaba işlemleri sekmesinde hello Synchronization Service Manager için Azure AD Connect anlayın."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 97a26565-618f-4313-8711-5925eeb47cdc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: decbc53613d456a71cd116c40c5e1fd761efd4af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-sync-service-manager-operations-tab"></a>Merhaba Eşitleme Hizmeti Yöneticisi'ni işlemler sekmesini kullanarak

![Eşitleme Hizmeti Yöneticisi](./media/active-directory-aadconnectsync-service-manager-ui/operations.png)

Hello işlemleri sekmesinde hello en son işlemleri hello sonuçlarını gösterir. Bu sekme, anahtar toounderstand olduğu ve sorunlarını giderme.

## <a name="understand-hello-information-visible-in-hello-operations-tab"></a>Merhaba bilgi hello işlemleri sekmesinde görünür anlama
Merhaba üst yarı tüm metinler kronolojik sırada gösterir. Varsayılan olarak, hello işlemleri günlük hello hakkında bilgi son yedi gün korur, ancak bu ayar ile Merhaba değiştirilebilir [Zamanlayıcı](active-directory-aadconnectsync-feature-scheduler.md). Başarı durumunu göstermez herhangi çalıştırmak için toolook istiyor. Merhaba üstbilgilerini tıklatarak sıralama hello değiştirebilirsiniz.

Merhaba **durum** hello en önemli bilgileri bir sütundur ve hello bir çalıştırma için en önemli bir sorun gösterir. Merhaba en yaygın durumları tooinvestigate öncelik sırasına göre hızlı bir özeti aşağıda verilmiştir (burada * birkaç olası hata dizeleri gösterir).

| Durum | Açıklama |
| --- | --- |
| durdurulmuş-* |çalıştırma hello tamamlanamadı. Örneğin, hello uzak sistem kapalı ve bağlantı kurulamıyor. |
| durduruldu-hata-sınırı |5. 000'den fazla hataları vardır. çalıştırma hello otomatik olarak toohello çok sayıda hata durduruldu. |
| Tamamlanan -\*-hataları |Merhaba tamamlanmış çalıştırın, ancak araştırılması gereken bir hata (daha az 5.000). |
| Tamamlanan -\*-uyarıları |Merhaba çalıştırma tamamlandı, ancak bazı verileri beklenen hello durumda değil. Hatalar varsa, bu ileti genellikle yalnızca bir belirti içindir. Hataları ele kadar uyarıları araştırmanız gereken değil. |
| başarılı |Sorunu yok. |

Bir satır seçtiğinizde, hello alt tooshow hello ayrıntılarını çalıştıran güncelleştirir. toohello hello sonuna kadar sol, liste bildiren olabilir **adım #**. Burada her etki alanı adımı tarafından temsil edilen ormanınızdaki birden çok etki alanı varsa, bu listede yalnızca görünür. Merhaba etki alanı adı hello başlığı altında bulunabilir **bölüm**. Altında **eşitleme istatistikleri**, hello işlenen değişikliklerin sayısı hakkında daha fazla bilgi bulabilirsiniz. Merhaba bağlantılar tooget değiştirilen hello nesnelerin bir listesini tıklatabilirsiniz. Hatalarla nesneniz varsa, bu hataları altında görünmesini **eşitleme hatalarını**.

Daha fazla bilgi için bkz: [not synchronızıng bir nesne sorun giderme](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)

## <a name="next-steps"></a>Sonraki adımlar
Merhaba hakkında daha fazla bilgi [Azure AD Connect eşitleme](active-directory-aadconnectsync-whatis.md) yapılandırma.

[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.
