---
title: "İçerik Paketi hataları günlüğe Azure Active Directory etkinliği sorunlarını giderme | Microsoft Docs"
description: "Hello Azure Active Directory etkinliği İçerik Paketi ve adımları toofix hata iletilerinin bir listesini sağlar bunları."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 325de65ff1572a2f8f8319c0a52350bda03af3de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a>İçerik Paketi hataları günlüklerini Azure Active Directory etkinliği sorunlarını giderme 


Azure Active Directory Önizleme için Hello Power BI içerik paketi ile çalışırken, aşağıdaki hatalar hello çalıştırmak mümkündür: 

- [Yenileme başarısız oldu](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [Başarısız tooupdate veri kaynağı kimlik bilgileri](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [Veri alma çok uzun sürüyor](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) 
 
Bu konu, hello olası nedenleri hakkında bilgi sağlar ve nasıl toofix bu hatalar.
 
## <a name="refresh-failed"></a>Yenileme başarısız oldu 
 
**Bu hatanın nasıl ortaya**: e-posta Power BI veya hello yenileme geçmişi başarısız durumda. 


| Nedeni | Nasıl toofix |
| ---   | ---        |
| Toohello içerik paketi bağlanan hello kullanıcıları Hello kimlik bilgilerini sıfırlama ancak hello hello içerik paketi, bağlantı ayarlarını hello güncelleştirilmemiş hataları nedeniyle başarısız oldu yenileyin. | Power bı'da hello dataset karşılık gelen toohello Azure Active Directory etkinliği günlükleri Pano (Azure Active Directory etkinliği günlükleri) bulun, yenileme zamanlaması seçin ve ardından Azure AD kimlik bilgilerinizi girin. |
| Bir yenileme içerik paketi temel hello toodata sorunları nedeniyle başarısız olabilir. | Bir destek bileti dosya. Daha fazla ayrıntı için bkz: [nasıl tooget desteklemek için Azure Active Directory](active-directory-troubleshooting-support-howto.md).|
 
 
## <a name="failed-tooupdate-data-source-credentials"></a>Başarısız tooupdate veri kaynağı kimlik bilgileri 
 
**Bu hatanın nasıl ortaya**: Power toohello Azure Active Directory etkinliği günlükleri (Önizleme) İçerik Paketi bağlanırken BI'da. 

| Nedeni | Nasıl toofix |
| ---   | ---        |
| Genel yönetici veya bir güvenlik okuyucu veya bir güvenlik yöneticisine Hello bağlanan kullanıcının olduğu | Genel yönetici veya bir güvenlik okuyucu veya bir güvenlik yönetici tooaccess hello içerik paketleri olan bir hesap kullanın. |
| Kiracı Premium Kiracı değil veya Premium lisansı dosya en az bir kullanıcı yok. | Bir destek bileti dosya. Daha fazla ayrıntı için bkz: [nasıl tooget desteklemek için Azure Active Directory](active-directory-troubleshooting-support-howto.md).|
 

 

## <a name="importing-of-data-is-taking-too-long"></a>Veri alma çok uzun sürüyor 
 
**Bu hatanın nasıl ortaya**: içerik paketiniz bağlandıktan sonra Power BI'da tooprepare hello veri içeri aktarma işlemi panonuz için Azure Active Directory etkinlik günlüğü başlatır. Merhaba iletisini görürsünüz: "*... veri alma* "  

| Nedeni | Nasıl toofix |
| ---   | ---        |
| Kiracı Hello boyutuna bağlı olarak, bu adım birkaç dakika too30 dakika arasında herhangi bir yere ele geçirebilir. | Yalnızca endişelenmeyin. Merhaba ileti, bir saat içinde panonuz tooshowing değişmezse, Lütfen bir destek bileti dosya. Daha fazla ayrıntı için bkz: [nasıl tooget desteklemek için Azure Active Directory](active-directory-troubleshooting-support-howto.md).|

## <a name="next-steps"></a>Sonraki adımlar

tooinstall hello Azure Active Directory Önizleme için Power BI içerik paketi tıklatın [burada](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).


