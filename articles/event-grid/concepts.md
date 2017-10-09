---
title: "aaaAzure olay kılavuz kavramları"
description: "Azure olay kılavuz ve onun kavramlarını açıklar. Olay kılavuzunun birkaç anahtar bileşenleri tanımlar."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/10/2017
ms.author: babanisa
ms.openlocfilehash: bb86381330fd2d6d2769167ec1953f0d5c28af85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="concepts-in-azure-event-grid"></a>Azure Event kılavuzunda kavramları

Merhaba kavramlarla Azure olay kılavuzunda şunlardır:

## <a name="events"></a>Olaylar

Bir olay hello en küçük hello sistemde gerçekleşen tam olarak bir şey açıklayan bilgileri miktarıdır.  Her olay gibi genel bilgiler vardır: hello olayın zaman hello olay kaynağını sürdü yerinde ve benzersiz tanımlayıcı.  Her olay yalnızca ilgili toohello belirli olay belirli bilgileri de vardır. Örneğin, Azure depolama alanında oluşturulan yeni bir dosya ile ilgili bir olay hello lastTimeModified değeri gibi hello dosyası ayrıntılarını içerir. Veya bir sanal makine yeniden başlatılıyor hakkında bir olay hello sanal makine ve yeniden başlatma hello nedeni hello adını içerir.

## <a name="event-sourcespublishers"></a>Olay kaynakları/yayımcıları

Burada hello olay gerçekleştiğinde bir olay kaynağıdır. Örneğin, Azure Storage hello olay olaylar oluşturulup blob kaynağıdır. Azure VM doku hello olay için sanal makine olayları kaynağıdır. Olay kaynakları olayları tooEvent kılavuz yayımlamak için sorumludur.

## <a name="topics"></a>Konu başlıkları

Yayımcıları olayları konulara kategorilere ayırma. Merhaba konu burada hello yayımcı olaylar gönderir bir uç nokta içerir. Olay toorespond toocertain türleri, hangi konuları toosubscribe aboneleri karar verin. Böylece aboneleri nasıl tooconsume hello olayları uygun şekilde bulabilir konular da bir olay şeması sağlar.

Sistem konular, Azure Hizmetleri tarafından sağlanan yerleşik konulardır. Uygulama ve üçüncü taraf konuları bunun özel konulardır.

## <a name="event-subscriptions"></a>Olay abonelikleri

Bir abonelik olay hangi olayların bir konuda üzerinde bir abone olarak alma ilgilenmektedir kılavuz bildirir.  Bir abonelik de olayları toohello abone nasıl teslim hakkında bilgi içerir.

## <a name="event-handlers"></a>Olay işleyicileri

Bir olay kılavuz açısından bakıldığında, olay işleyici burada hello olayı gönderilir hello yerdir. Merhaba işleyici bazı başka eylem tooprocess hello olayı alır.  Olay kılavuz birden çok abone türlerini destekler. Abone Hello türüne bağlı olarak farklı mekanizmaları tooguarantee hello teslim hello olayın olay kılavuz izler.  Durum kodu Hello işleyici dönene kadar HTTP Web kancası olay işleyicileri için hello olay denenir `200 – OK`. Merhaba sıra hizmeti mümkün toosuccessfully işlem hello ileti gönderme hello kuyruğuna olana kadar Azure depolama kuyruğu için hello olayları denenir.

## <a name="filters"></a>Filtreler

Tooa konu abone olurken toohello endpoint gönderilen hello olayları filtreleyebilirsiniz. Olay türü ya da konu düzeni göre filtreleyebilirsiniz. Daha fazla bilgi için bkz: [olay kılavuz abonelik şema](subscription-creation-schema.md).

## <a name="security"></a>Güvenlik

Olay tootopics abone olma ve konuları yayımlamak için güvenlik sağlar. Abone olurken hello kaynak ya da konu yeterli izinleriniz olmalıdır. Yayımlama sırasında hello konu için anahtar kimlik doğrulaması ya da SAS belirteci olması gerekir. Daha fazla bilgi için bkz: [olay kılavuz güvenlik ve kimlik doğrulama](security-authentication.md).

## <a name="failed-delivery"></a>Başarısız teslim

Olay kılavuz bulunamıyor doğrulayın olaya hello abonenin bitiş noktası tarafından alındı, hello olay redelivers. Daha fazla bilgi için bkz: [olay kılavuz ileti teslimi ve Yeniden Dene'yi](delivery-and-retry.md).

## <a name="next-steps"></a>Sonraki adımlar

* Bir giriş tooEvent kılavuz için bkz: [hakkında olay kılavuz](overview.md).
* tooquickly olay kılavuz kullanımına başlamanıza bkz [Azure olay kılavuz oluşturma ve rota özel olaylarla](custom-event-quickstart.md).
