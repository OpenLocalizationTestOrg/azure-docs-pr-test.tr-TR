---
title: "Azure zaman serisi Öngörüler aaaData erişim ilkelerinde | Microsoft Docs"
description: "Bu öğreticide, toomanage veri erişimi ilkelerini zaman serisi bilgiler öğrenin"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/01/2017
ms.author: omravi
ms.openlocfilehash: f286d26c8c5c851c523e9384760dc4b10711fa3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="grant-data-access-tooa-time-series-insights-environment-using-azure-portal"></a>Azure portalı kullanarak veri erişim tooa zaman serisi Öngörüler ortamı verin

Zaman Serisi Görüşleri ortamlarının birbirinden bağımsız türde iki erişim ilkesi vardır:

* Yönetim erişimi ilkeleri
* Veri erişimi ilkeleri

Her iki ilke de Azure Active Directory asıl adlarına (kullanıcılar ve uygulamalar) belirli bir ortam üzerinde çeşitli izinler verir. Merhaba ilkelerini (kullanıcılar ve uygulamalar) toohello etkin ait olmalıdır hello ortamı içeren hello abonelikle ilişkili dizin (veya "Azure Kiracı").

Yönetim erişim ilkeleri hello ortamının izinleri ilgili toohello yapılandırması gibi verin
*   Oluşturma ve silme hello ortamının olay kaynakları başvuru veri kümelerini ve
*   Merhaba veri erişimi ilkelerini yönetimi.

Veri erişimi ilkelerini tooissue veri sorguları, izinleri hello ortamında başvuru verileri işlemek ve kaydedilmiş sorguları hello ortamı Perspektifler paylaşın.

iki tür ilkeleri Hello hello ortamının erişim toohello yönetimi ve erişimi toohello verileri hello ortamı içindeki arasında açıkça birbirinden izin verir. Örneğin, Hello sahibi/creator hello ortamının hello veri erişimden kaldırılır, olası toosetup bir ortam olur. Kullanıcılar ve tooread veri hello ortamından izin verilen hizmetler yanı sıra hello ortamının hiçbir erişim toohello yapılandırması verilebilir.

## <a name="grant-data-access"></a>Veri erişim izni verme
Merhaba aşağıdaki adımları toogrant veri için bir kullanıcı asıl nasıl erişim göster:

1.  İçinde toohello oturum [Azure portal](https://portal.azure.com).
2.  "Tüm kaynaklar" Merhaba menü hello sol tarafındaki hello Azure portal'ı tıklatın.
3.  Zaman Serisi Görüşleri ortamınızı seçin.

  ![Merhaba zaman serisi Öngörüler kaynak - yönetmek ortamı](media/data-access/getstarted-grant-data-access1.png)

4.  “Veri Düzlemi Erişimi” öğesini seçin, “Ekle” düğmesine tıklayın

  ![Merhaba zaman serisi Öngörüler kaynak yönetme - ekleme](media/data-access/getstarted-grant-data-access2.png)

5.  "Kullanıcı seç" öğesine tıklayın.
6.  Arama ve hello e-posta ile kullanıcı seçin.
7.  “Kullanıcı Seç” dikey penceresinde “Seç” düğmesine tıklayın.

  ![Merhaba zaman serisi Öngörüler kaynak - kullanıcı yönetme](media/data-access/getstarted-grant-data-access3.png)

8.  “Rol seç” öğesine tıklayın.
9.  Perspektif ve kaydedilmiş sorguları hello ortamının diğer kullanıcılarla paylaşmak ve tooallow kullanıcı toochange başvuru verileri isterseniz "Katılımcı" seçin. Aksi takdirde hello ortamında "Okuyucu" tooallow kullanıcı sorgu verileri seçin ve kişisel (paylaşılmayan) sorguları hello ortamında kaydedin.
10. "Tamam" hello "Rolü Seç" dikey penceresinde'ı tıklatın.

  ![Merhaba zaman serisi Öngörüler kaynak - select rolünü yönetme](media/data-access/getstarted-grant-data-access4.png)

11. "Tamam" hello "Kullanıcı rolü Seç" dikey penceresinde'ı tıklatın.
12. Şunu görmeniz gerekir:

  ![Merhaba zaman serisi Öngörüler kaynak - sonuçlarını yönetme](media/data-access/getstarted-grant-data-access5.png)

## <a name="next-steps"></a>Sonraki adımlar

* [Olay kaynağı oluşturma](time-series-insights-add-event-source.md)
* [Olayları göndermek](time-series-insights-send-events.md) toohello olay kaynağı
* [Zaman Serisi Görüşleri Portalı](https://insights.timeseries.azure.com)’nda ortamınızı görüntüleme
