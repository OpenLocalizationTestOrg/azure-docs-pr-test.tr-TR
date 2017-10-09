---
title: "aaaStream hello Azure etkinlik günlüğü tooEvent hub | Microsoft Docs"
description: "Nasıl toostream hello Azure etkinlik günlüğü tooEvent hub'ları hakkında bilgi edinin."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ec4c2d2c-8907-484f-a910-712403a06829
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/06/2017
ms.author: johnkem
ms.openlocfilehash: 336f92771b9d4379ad9dbcadc6997dfae7fae7bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-hello-azure-activity-log-tooevent-hubs"></a>Hello Azure etkinlik günlüğü tooEvent hub akışı
Merhaba [ **Azure etkinlik günlüğü** ](monitoring-overview-activity-logs.md) içinde hello Portalı'nda hello yerleşik "Verme" seçeneğini kullanarak gerçek zamanlı tooany uygulama yakın gönderilebilen ya da hizmet veri yolu kural kimliği hello aracılığıyla bir günlük profilinde hello etkinleştirerek Azure PowerShell cmdlet'lerini veya Azure CLI.

## <a name="what-you-can-do-with-hello-activity-log-and-event-hubs"></a>Merhaba etkinlik günlüğü ve olay hub'ları ile yapabilecekleriniz
Merhaba etkinlik günlüğü yeteneği akış hello kullanabilir birkaç yollar şunlardır:

* **Akış toothird taraf günlüğe kaydetme ve telemetri sistemlerde** – zaman içinde olay hub'ları akış hello mekanizması toopipe etkinlik günlüğü üçüncü taraf Sıem'lerden duruma ve oturum analiz çözümleri.
* **Bir özel telemetri ve günlüğe kaydetme platformu yapı** – özel olarak geliştirilmiş telemetri platform zaten varsa veya olan hello alma yalnızca biri, yüksek düzeyde ölçeklenebilir hello yayımlama-abone olma yapı hakkında olay hub'ları yapısını tooflexibly verir düşünüyorum Etkinlik günlüğü. [Bir küresel ölçekteki telemetri Platform dan Rosanova'nın Kılavuzu toousing Event Hubs bakın.](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)

## <a name="enable-streaming-of-hello-activity-log"></a>Merhaba etkinlik günlüğü akışı etkinleştir
Etkinlik günlüğü Merhaba program aracılığıyla veya hello Portalı aracılığıyla akış etkinleştirebilirsiniz. Her iki durumda da, bir hizmet veri yolu Namespace ve bu ad alanı için bir paylaşılan erişim ilkesi seçin ve hello ilk yeni etkinlik günlüğü olay gerçekleştiğinde bir olay hub'ı bu ad alanında oluşturulur. Bir hizmet veri yolu Namespace yoksa, öncelikle toocreate biri gerekir. Etkinlik günlüğü olaylarını toothis Service Bus Namespace önceden akışı değilse, daha önce oluşturulmuş bir Event Hub hello yeniden kullanılabilir. Merhaba paylaşılan erişim ilkesi hello akış mekanizması vardır hello izinleri tanımlar. Günümüzde, tooan olay hub'ları akış gerektirir **Yönet**, **Gönder**, ve **dinleme** izinleri. Oluşturun veya hello "Yapılandırma" sekmesi altında hello Klasik Portalı'nda hizmet veri yolu Namespace paylaşılan erişim ilkeleri, hizmet veri yolu Namespace için değiştirin. tooupdate etkinlik günlüğü günlük profili tooinclude akış Merhaba, hello kullanıcı hello değişiklik yapmadan bu hizmet veri yolu yetkilendirme kuralı hello ListKey izninizin olması gerekir.

Merhaba hizmet veri yolu veya olay hub'ad alanı toobe hello yok uygun RBAC erişim tooboth abonelikleri hello ayarı yapılandıran hello kullanıcının sahip olduğu sürece günlükleri yayma hello abonelik aynı abonelik.

### <a name="via-azure-portal"></a>Azure portalı üzerinden
1. Toohello gidin **etkinlik günlüğü** yan hello portalının sol hello üzerinde hello menüsünü kullanarak dikey.
   
    ![TooActivity günlük portalında gidin](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. Merhaba tıklatın **dışarı** hello dikey penceresinde hello üstündeki düğmesi.
   
    ![Portalında Dışarı Aktar](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. Görüntülenen hello dikey penceresinde hello bölgeler için toostream olaylar ve hello Service Bus bu olayları akış için oluşturulan bir olay hub'ı toobe istediğiniz Namespace istediğiniz seçebilirsiniz.
   
    ![Etkinlik günlüğü dikey dışarı aktarma](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. Tıklatın **kaydetmek** toosave bu ayarlar. Hello ayarları hemen uygulanan tooyour abonelik olabilir.

### <a name="via-powershell-cmdlets"></a>PowerShell cmdlet'leri
Bir günlük profili zaten varsa, bu profili ilk tooremove gerekir.

1. Kullanım `Get-AzureRmLogProfile` günlük profili varsa, tooidentify
2. Aksi takdirde kullanmak `Remove-AzureRmLogProfile` tooremove onu.
3. Kullanım `Set-AzureRmLogProfile` toocreate bir profili:

```
Add-AzureRmLogProfile -Name my_log_profile -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

Merhaba Service Bus kural kimliği olduğundan bu biçiminde bir dize: {hizmet veri yolu kaynak kimliği} /authorizationrules/ {anahtar adı}, örneğin 

### <a name="via-azure-cli"></a>Azure CLI
Bir günlük profili zaten varsa, bu profili ilk tooremove gerekir.

1. Kullanım `azure insights logprofile list` günlük profili varsa, tooidentify
2. Aksi takdirde kullanmak `azure insights logprofile delete` tooremove onu.
3. Kullanım `azure insights logprofile add` toocreate bir profili:

```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

Merhaba Service Bus kural kimliği olduğundan bu biçiminde bir dize: `{service bus resource ID}/authorizationrules/{key name}`.

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a>Olay hub'ları hello günlük verilerini nasıl kullanabilir?
[Merhaba şema hello etkinlik günlüğü için kullanılabilir burada](monitoring-overview-activity-logs.md). Her bir olaydır JSON BLOB'ları "kayıtlar." olarak adlandırılan bir dizi

## <a name="next-steps"></a>Sonraki Adımlar
* [Arşiv hello etkinlik günlüğü tooa depolama hesabı](monitoring-archive-activity-log.md)
* [Okuma hello hello Azure etkinlik günlüğü genel bakış](monitoring-overview-activity-logs.md)
* [Etkinlik günlüğü olaya dayanarak bir uyarı ayarlama](insights-auditlog-to-webhook-email.md)

