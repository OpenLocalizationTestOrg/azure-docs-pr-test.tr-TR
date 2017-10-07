---
title: "aaaReceive etkinlik günlüğü Uyarıları hizmeti bildirimleri | Microsoft Docs"
description: "Azure hizmet ortaya çıktığında, SMS, e-posta veya Web kancası aracılığıyla bilgi edinin."
author: johnkemnetz
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
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: dd35e8f39d2a522efdae4dfed20779c992c1dd27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts-on-service-notifications"></a>Etkinlik günlüğü Uyarıları hizmeti bildirimlerinin oluşturun.
## <a name="overview"></a>Genel Bakış
Bu makale size nasıl hello Azure portal kullanarak tooset etkinlik günlüğü yedeklemek için hizmet durumu bildirimlerine uyarıları gösterir.  

Azure hizmet durumu bildirimleri tooyour Azure aboneliği gönderdiğinde bir uyarı alabilirsiniz. Temel hello uyarı yapılandırabilirsiniz:

- hizmeti sistem durumu bildirimi (olay, bakım, bilgi, vb.) Hello sınıfı.
- Etkilenen hello hizmetlere.
- Etkilenen hello bilgiler.
- Merhaba bildirim (karşılaştırması çözümlenen etkin) Hello durumu.
- Merhaba düzeyi hello bildirimler (bilgi, uyarı, hatası).

Kimin hello uyarı göndermesi gerektiğini de yapılandırabilirsiniz:

- Var olan bir eylem grubunu seçin.
- (Bu uyarılar için kullanılabilir) yeni bir eylem grubu oluşturun.

Eylem grupları hakkında daha fazla toolearn bkz [oluşturma ve eylem gruplarını yönetme](monitoring-action-groups.md).

Azure Resource Manager şablonları kullanarak nasıl uyarılar tooconfigure hizmet sistem durumu bildirimi hakkında daha fazla bilgi için bkz: [Resource Manager şablonları](monitoring-create-activity-log-alerts-with-resource-manager-template.md).

## <a name="create-an-alert-on-a-service-health-notification-for-a-new-action-group-by-using-hello-azure-portal"></a>Hello Azure portal kullanarak bir uyarı yeni bir eylem grubu için bir hizmet sistem durumu bildirimi oluşturma
1. Merhaba, [portal](https://portal.azure.com)seçin **İzleyici**.

    ![Merhaba "İzleme" hizmeti](./media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.png)

2. Merhaba, **etkinlik günlüğü** bölümünde, select **uyarıları**.

    ![Merhaba "Uyarılar" sekmesi](./media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.png)

3. Seçin **etkinlik günlüğü uyarı Ekle**ve hello alanları doldurun.

    ![Merhaba "Etkinlik günlüğü uyarı Ekle" komutu](./media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.png)

4. Hello bir ad girin **etkinlik günlüğü uyarı adı** kutusuna ve sağlayan bir **açıklama**.

    ![Merhaba "etkinlik günlüğü uyarı Ekle" iletişim kutusu](./media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-new-action-group.png)

5. Merhaba **abonelik** kutusuna geçerli aboneliğiniz ile autofills. Bu abonelik kullanılan toosave hello etkinlik günlüğü uyarı belirtir. Merhaba uyarı hello etkinlik günlüğü için bu dağıtılan toothis abonelik ve izleyiciler olayları kaynaktır.

6. Select hello **kaynak grubu** hangi hello Uyarı kaynağı oluşturulur. Merhaba uyarı tarafından izlenen hello kaynak grubu değil. Bunun yerine, hello uyarı kaynağın bulunduğu hello kaynak grubu değil.

7. Merhaba, **olay kategorisi** kutusunda **hizmet durumu**. İsteğe bağlı olarak, hello seçin **hizmet**, **bölge**, **türü**, **durum**, ve **düzeyi** hizmeti Sistem durumu bildirimleri tooreceive istiyor.

8. Altında **aracılığıyla uyarı**seçin hello **yeni** eylem Grup düğmesi. Hello bir ad girin **eylem grup adı** kutusunda ve hello bir ad girin **kısa ad** kutusu. Bu uyarı oluşturulduğunda, gönderilen hello bildirimleri Hello kısa ad başvuruluyor.

9. Alıcıları listesini hello alıcının sağlayarak tanımlayın:

    a. **Ad**: hello alıcının adını, diğer ad veya tanımlayıcı girin.

    b. **Eylem türü**: SMS seçin, e-posta veya Web kancası.

    c. **Ayrıntılar**: seçilen hello eylem türüne bağlı olarak, bir telefon numarası, e-posta adresi veya Web kancası URI girin.

10. Seçin **Tamam** toocreate hello uyarı.

Birkaç dakika içinde hello etkindir ve uyarı oluşturma sırasında belirtilen hello koşullarına göre tootrigger başlar.

Etkinlik günlüğü uyarıları için hello Web kancası şeması hakkında daha fazla bilgi için bkz: [Azure etkinlik için Web kancası oturum uyarıları](monitoring-activity-log-alerts-webhook.md).

>[!NOTE]
>Bu adımlarda tanımlanan hello eylem tüm gelecekteki uyarı tanımları için var olan bir eylem grubu olarak yeniden kullanılabilir grubudur.
>
>

## <a name="create-an-alert-on-a-service-health-notification-for-an-existing-action-group-by-using-hello-azure-portal"></a>Hello Azure portal kullanarak bir uyarı varolan bir eylem grup için bir hizmet sistem durumu bildirimi oluşturma

1. 1 ile 7'de hello önceki bölümde toocreate hizmeti sistem durumu bildirimi adımları. 

2. Altında **aracılığıyla uyarı**seçin hello **varolan** eylem Grup düğmesi. Merhaba uygun eylemi grubunu seçin.

3. Seçin **Tamam** toocreate hello uyarı.

Birkaç dakika içinde hello etkindir ve uyarı oluşturma sırasında belirtilen hello koşullarına göre tootrigger başlar.

## <a name="manage-your-alerts"></a>Uyarılarınızı yönetme

Bir uyarı oluşturduktan sonra hello görünür **uyarıları** hello bölümünü **İzleyici** dikey. Toomanage için istediğiniz hello uyarıyı seçin:

* Düzenleyin.
* Dosyayı silin.
* Tootemporarily durdurma veya hello uyarı bildirimleri almaya devam etmek istiyorsanız, etkinleştirmek veya devre dışı.

## <a name="next-steps"></a>Sonraki adımlar
- Hakkında bilgi edinin [hizmet durumu bildirimlerine](monitoring-service-notifications.md).
- Hakkında bilgi edinin [bildirim hız sınırlaması](monitoring-alerts-rate-limiting.md).
- Gözden geçirme hello [etkinlik günlüğü uyarı Web kancası şeması](monitoring-activity-log-alerts-webhook.md).
- Alma bir [etkinlik günlüğü uyarıları genel bakış](monitoring-overview-alerts.md)ve öğrenin nasıl tooreceive uyarıları. 
- Daha fazla bilgi edinmek [Eylem grupları](monitoring-action-groups.md).
