---
title: "aaaCreate etkinlik günlüğü uyarıları | Microsoft Docs"
description: "Merhaba etkinlik günlüğünde belirli olaylar meydana geldiğinde, SMS, Web kancası ve e-posta bildirilmesi."
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
ms.date: 08/03/2017
ms.author: johnkem
ms.openlocfilehash: ba0716cc12a0b3a0024ee5562a025f3f153f8982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts"></a>Etkinlik günlüğü uyarı oluşturma

## <a name="overview"></a>Genel Bakış
Etkinlik günlüğü yeni bir etkinlik günlüğü olay oluştuğunda etkinleştirme uyarılar eşleşen hello uyarıda belirtilen hello koşullarına uyarılar. Bunlar Azure kaynaklarını; dolayısıyla bir Azure Resource Manager şablonu kullanılarak oluşturulabilir. Bunlar ayrıca oluşturulabilir, güncelleştirilmiş veya hello Azure portal silindi. Bu makalede, etkinlik günlüğü uyarıları hello kavramları tanıtır. Ardından size nasıl toouse hello etkinlik günlüğü olaylarını üzerinde bir uyarı oluşturan Azure portal tooset gösterir.

Etkinlik günlüğü uyarıları tooreceive bildirimleri normalde, oluşturduğunuz zaman:

* Azure aboneliği, genellikle kapsamlı tooparticular kaynak grupları veya kaynakları kaynaklardaki belirli değişiklikler gerçekleşir. Örneğin, myProductionResourceGroup herhangi bir sanal makine silindiğinde bildirim toobe isteyebilirsiniz. Veya herhangi bir yeni rol tooa kullanıcı aboneliğinizde atanmışsa bildirim toobe isteyebilirsiniz.
* Hizmet sistem durumu olayı oluşur. Hizmet sistem durumu olayları olaylar ve aboneliğinizde tooresources uygulamak bakım olayları bildirimi içerir.

Her iki durumda da, hello abonelik hangi hello uyarı oluşturulan olaylar için yalnızca bir etkinlik günlüğü uyarı izler.

Hello JSON nesnesinde bir etkinlik günlüğü olayı için herhangi bir üst düzey özelliği bağlı bir etkinlik günlüğü uyarı yapılandırabilirsiniz. Ancak, hello portal hello en yaygın seçenekler gösterilmektedir:

- **Kategori**: yönetici, hizmet sistem durumu, otomatik ölçeklendirme ve öneri. Daha fazla bilgi için bkz: [hello Azure etkinlik günlüğü'ne genel bakış](./monitoring-overview-activity-logs.md#categories-in-the-activity-log). Hizmet sistem durumu olayları hakkında daha fazla toolearn bkz [etkinlik günlüğü Uyarıları hizmeti bildirimleri almak](./monitoring-activity-log-alerts-on-service-notifications.md).
- **Kaynak grubu**
- **Kaynak**
- **Kaynak türü**
- **İşlem adı**: hello kaynak yöneticisi rol tabanlı erişim denetimi işlem adı.
- **Düzey**: Merhaba (ayrıntılı bilgi, uyarı, hata veya kritik) hello olay önem derecesi.
- **Durum**: hello durum hello olayın genellikle başlatıldı, başarısız veya başarılı oldu.
- **Olayı başlatan tarafından**: olarak da bilinen hello "çağırıcı." Merhaba e-posta adresi veya hello işlemi gerçekleştiren hello kullanıcının Azure Active Directory tanıtıcısı.

>[!NOTE]
>En az iki bir olan ile uyarıdaki ölçütleri önceki hello belirtmelisiniz hello kategorisi. Merhaba etkinlik günlükleri her bir olay oluşturulduğunda etkinleştiren bir uyarı oluşturamazsınız.
>
>

Bir etkinlik günlüğü uyarı etkinleştirildiğinde, bir eylem kullanan Grup toogenerate eylemler veya bildirimleri. Bir eylem grubu yeniden kullanılabilir e-posta adresleri gibi bildirim alıcıları Web kancası URL'leri ya da SMS telefon numaralarının kümesidir. Merhaba alıcıları birden çok uyarıları toocentralize başvurulabilir ve bildirim kanallarını gruplayın. Etkinlik günlüğü Uyarınız tanımlamak için iki seçeneğiniz vardır. Şunları yapabilirsiniz:

* Varolan bir eylem Grup etkinlik günlüğü Uyarınız kullanın. 
* Yeni bir eylem grubu oluşturun. 

Eylem grupları hakkında daha fazla toolearn bkz [oluşturma ve eylem gruplarında hello Azure portalında yönetmek](monitoring-action-groups.md).

Hizmet durumu bildirimlerine hakkında daha fazla toolearn bkz [hizmet durumu bildirimlerine etkinlik günlüğü uyarılar alırsınız](monitoring-activity-log-alerts-on-service-notifications.md).

## <a name="create-an-alert-on-an-activity-log-event-with-a-new-action-group-by-using-hello-azure-portal"></a>Hello Azure portal kullanarak yeni bir eylem grubu ile etkinlik günlüğü olay bir uyarı oluştur
1. Merhaba, [portal](https://portal.azure.com)seçin **İzleyici**.

    ![Merhaba "İzleme" hizmeti](./media/monitoring-activity-log-alerts/home-monitor.png)
2. Merhaba, **etkinlik günlüğü** bölümünde, select **uyarıları**.

    ![Merhaba "Uyarılar" sekmesi](./media/monitoring-activity-log-alerts/alerts-blades.png)
3. Seçin **etkinlik günlüğü uyarı Ekle**ve hello alanları doldurun.

4. Hello bir ad girin **etkinlik günlüğü uyarı adı** kutusunda ve seçin bir **açıklama**.

    ![Merhaba "Etkinlik günlüğü uyarı Ekle" komutu](./media/monitoring-activity-log-alerts/add-activity-log-alert.png)

5. Merhaba **abonelik** kutusuna geçerli aboneliğiniz ile autofills. Bu abonelik, hangi hello eylem grubu kaydedildi hello bir olur. Merhaba uyarı dışarı dağıtılan toothis abonelik ve izleyiciler etkinlik günlüğü olaylarını kaynaktır.

    ![Merhaba "etkinlik günlüğü uyarı Ekle" iletişim kutusu](./media/monitoring-activity-log-alerts/activity-log-alert-new-action-group.png)

6. Select hello **kaynak grubu** hangi hello Uyarı kaynağı oluşturulur. Bu hello uyarı tarafından izlenen hello kaynak grubu değil. Bunun yerine, hello uyarı kaynağın bulunduğu hello kaynak grubu değil.

7. İsteğe bağlı olarak, seçin bir **olay kategorisi** toomodify hello gösterilen ek filtreler. Yönetim olaylar için hello filtreleri içeren **kaynak grubu**, **kaynak**, **kaynak türü**, **işlem adı**, **Düzeyi**, **durum**, ve **olayı başlatan tarafından**. Bu değerleri bu uyarı izlemelidir hangi olayların tanımlayın.

    >[!NOTE]
    >Merhaba, Uyarı ölçütleri önceki en az birini belirtmeniz gerekir. Merhaba etkinlik günlükleri her bir olay oluşturulduğunda etkinleştiren bir uyarı oluşturamazsınız.
    >
    >

8. Hello bir ad girin **eylem grup adı** kutusunda ve hello bir ad girin **kısa ad** kutusu. Bu grubun kullanarak bildirimler gönderildiğinde hello kısa adı yerine bir tam eylem grup adı kullanılır.

9.  Eylemin hello sağlayarak eylemlerin bir listesini tanımlar:

    a. **Ad**: hello eylemin adı, diğer ad veya tanımlayıcı girin.

    b. **Eylem türü**: SMS seçin, e-posta veya Web kancası.

    c. **Ayrıntılar**: hello eylem türüne bağlı olarak, bir telefon numarası, e-posta adresi veya Web kancası URI girin.

10. Seçin **Tamam** toocreate hello uyarı.

Merhaba uyarı toofully yaymak ve etkin hale birkaç dakika sürer. Yeni olaylar hello uyarının ölçütleri eşleştiğinde tetikler.

Daha fazla bilgi için bkz: [etkinlik günlüğü uyarıları kullanılan anlayın hello Web kancası şema](monitoring-activity-log-alerts-webhook.md).

>[!NOTE]
>Bu adımlarda tanımlanan hello eylem tüm gelecekteki uyarı tanımları için var olan bir eylem grubu olarak yeniden kullanılabilir grubudur.
>
>

## <a name="create-an-alert-on-an-activity-log-event-for-an-existing-action-group-by-using-hello-azure-portal"></a>Hello Azure portal kullanarak bir uyarı varolan bir eylem grup için bir etkinlik günlüğü olay oluşturma
1. 1 ile 7'de hello önceki bölümde toocreate etkinlik günlüğü Uyarınız adımları.

2. Altında **aracılığıyla bildir**seçin hello **varolan** eylem Grup düğmesi. Var olan bir eylem grubunu hello listeden seçin.

3. Seçin **Tamam** toocreate hello uyarı.

Merhaba uyarı toofully yaymak ve etkin hale birkaç dakika sürer. Yeni olaylar hello uyarının ölçütleri eşleştiğinde tetikler.

## <a name="manage-your-alerts"></a>Uyarılarınızı yönetme

Bir uyarı oluşturduktan sonra hello uyarıları bölümünde hello İzleyici dikey penceresinde görünür olur. Toomanage için istediğiniz hello uyarıyı seçin:

* Düzenleyin.
* Dosyayı silin.
* Tootemporarily durdurma veya hello uyarı bildirimleri almaya devam etmek istiyorsanız, etkinleştirmek veya devre dışı.

## <a name="next-steps"></a>Sonraki adımlar
- Alma bir [uyarılar genel bakış](monitoring-overview-alerts.md).
- Hakkında bilgi edinin [bildirim hız sınırlaması](monitoring-alerts-rate-limiting.md).
- Gözden geçirme hello [etkinlik günlüğü uyarı Web kancası şeması](monitoring-activity-log-alerts-webhook.md).
- Daha fazla bilgi edinmek [Eylem grupları](monitoring-action-groups.md).  
- Hakkında bilgi edinin [hizmet durumu bildirimlerine](monitoring-service-notifications.md).
- Oluşturma bir [etkinliğini günlüğe uyarı toomonitor aboneliğinizi tüm otomatik ölçeklendirme altyapısı işlemler](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).
- Oluşturma bir [etkinliğini günlüğe uyarı toomonitor aboneliğinizi tüm başarısız otomatik ölçeklendirme ölçek/genişletme işlemler](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).
