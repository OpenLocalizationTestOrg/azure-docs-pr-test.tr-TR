---
title: "aaaCreate ve hello Azure portal'ın eylem gruplarını yönetme | Microsoft Docs"
description: "Bilgi nasıl toocreate hello Azure portal'ın Eylem grupları ve yönetin."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: ancav
ms.openlocfilehash: 97e0b22bea7787fff6856f895a7e6256c177efd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-action-groups-in-hello-azure-portal"></a>Hello Azure portal'ın eylem gruplarını oluşturma ve yönetme
## <a name="overview"></a>Genel Bakış ##
Bu makale size nasıl gösterir toocreate hello Azure portal'ın Eylem grupları ve yönetin.

Eylem gruplarıyla eylemlerin bir listesini yapılandırabilirsiniz. Etkinlik günlüğü uyarıları tanımlarken bu gruplar daha sonra kullanılabilir. Bu gruplar daha sonra aynı eylemleri hello etkinlik günlüğü uyarısı her tetiklenişinde alınır, hello sağlama tanımlamak her etkinlik günlüğü uyarı tarafından yeniden kullanılabilir.

Bir eylem grubu, her eylem türü too10 olabilir. Her eylem aşağıdaki özelliklere hello oluşur:

* **Ad**: hello eylem grubu içinde benzersiz bir tanımlayıcı.  
* **Eylem türü**: bir SMS gönder, bir e-posta gönderme veya bir Web kancası çağırın.  
* **Ayrıntılar**: karşılık gelen telefon numarası, e-posta adresi veya Web kancası URI hello.

Hakkında bilgi için bkz: toouse Azure Resource Manager şablonları tooconfigure Eylem grupları, [eylem Grup Resource Manager şablonları](monitoring-create-action-group-with-resource-manager-template.md).

## <a name="create-an-action-group-by-using-hello-azure-portal"></a>Hello Azure portal kullanarak bir eylem grubu oluşturma ##
1. Merhaba, [portal](https://portal.azure.com)seçin **İzleyici**. Merhaba **İzleyici** dikey penceresinde, izleme ayarları ve verileri tek bir görünümde birleştirir.

    ![Merhaba "İzleme" hizmeti](./media/monitoring-action-groups/home-monitor.png)
2. Merhaba, **etkinlik günlüğü** bölümünde, select **Eylem grupları**.

    ![Merhaba "Eylem grupları" sekmesi](./media/monitoring-action-groups/action-groups-blade.png)
3. Seçin **eylem Grup Ekle**ve hello alanları doldurun.

    ![Merhaba "Eylem Grup Ekle" komutu](./media/monitoring-action-groups/add-action-group.png)
4. Hello bir ad girin **eylem grup adı** kutusunda ve hello bir ad girin **kısa ad** kutusu. Bu grubun kullanarak bildirimler gönderildiğinde hello kısa adı yerine bir tam eylem grup adı kullanılır.

      ![Merhaba eylem Grup Ekle"iletişim kutusu](./media/monitoring-action-groups/action-group-define.png)

5. Merhaba **abonelik** kutusuna geçerli aboneliğiniz ile autofills. Bu abonelik, hangi hello eylem grubu kaydedildi hello bir olur.

6. Select hello **kaynak grubu** hangi hello eylemde Grup kaydedilir.

7. Eylemlerin bir listesini, her eylemin sağlayarak tanımlayın:

    a. **Ad**: Bu eylem için benzersiz bir tanımlayıcı girin.

    b. **Eylem türü**: SMS seçin, e-posta veya Web kancası.

    c. **Ayrıntılar**: hello eylem türüne bağlı olarak, bir telefon numarası, e-posta adresi veya Web kancası URI girin.

8. Seçin **Tamam** toocreate hello eylem grubu.

## <a name="manage-your-action-groups"></a>Eylem gruplarınızı yönetme ##
Bir eylem grubu oluşturduktan sonra hello görünür **Eylem grupları** hello bölümünü **İzleyici** dikey. Toomanage için istediğiniz hello eylem grubunu seçin:

* Ekleme, düzenleme veya Eylemler kaldırma.
* Merhaba eylem grubunu silin.

## <a name="next-steps"></a>Sonraki adımlar ##
* Daha fazla bilgi edinmek [SMS uyarı davranış](monitoring-sms-alert-behavior.md).  
* Geçirmesine bir [hello etkinlik günlüğü uyarı Web kancası şeması anlama](monitoring-activity-log-alerts-webhook.md).  
* Daha fazla bilgi edinmek [hız sınırlaması](monitoring-alerts-rate-limiting.md) uyarılar hakkında. 
* Alma bir [etkinlik günlüğü uyarıları genel bakış](monitoring-overview-alerts.md)ve öğrenin nasıl tooreceive uyarıları.  
* Nasıl çok öğrenin[hizmeti sistem durumu bildirimi gönderilen her uyarıları yapılandırmak](monitoring-activity-log-alerts-on-service-notifications.md).
