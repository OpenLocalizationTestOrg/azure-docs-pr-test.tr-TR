---
title: "aaaAzure olay kılavuz teslim ve yeniden deneyin"
description: "Azure olay kılavuz olayları nasıl sunar ve teslim edilmeyen iletilerini nasıl işlediğini açıklar."
services: event-grid
author: djrosanova
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/11/2017
ms.author: darosa
ms.openlocfilehash: 874b3bf8892fbf803ef40f29d0ec10eb50150916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-message-delivery-and-retry"></a>Olay kılavuz ileti teslimi ve yeniden deneyin 

Bu makalede, Azure olay kılavuz teslim edilmedi olduğunda olayları nasıl işlediğini açıklar.

Olay kılavuz dayanıklı teslim sağlar. Her ileti en az bir kez her abonelik için sunar. Olayları hemen her abonelik kayıtlı toohello Web kancası gönderilir. Bir Web kancası olaya alınmasını kabul değil hello ilk teslimat 60 saniye içinde çalışır, olay kılavuz hello olay teslimini yeniden dener.

## <a name="message-delivery-status"></a>İleti teslimat durumu

Olay kılavuz HTTP yanıt kodları tooacknowledge giriş olayların kullanır. 

### <a name="success-codes"></a>Başarı kodları

Merhaba aşağıdaki HTTP yanıt kodları olaya tooyour Web kancası başarıyla teslim olduğunu gösterir. Olay kılavuz teslim tam olarak değerlendirir.

- 200 TAMAM
- 202 kabul edilen

### <a name="failure-codes"></a>Hata kodları

HTTP yanıt kodları aşağıdaki hello olay teslim girişimi başarısız olduğunu gösterir. Olay kılavuz toosend hello olay yeniden dener. 

- 400 Hatalı istek
- 401 Yetkisiz
- 404 Bulunamadı
- 408 isteği zaman aşımı
- 414 URI çok uzun
- 500 İç sunucu hatası
- 503 Hizmet kullanılamıyor
- 504 ağ geçidi zaman aşımı

Diğer bir yanıt kodu veya bir yanıt eksikliği hata gösterir. Olay kılavuz teslim yeniden dener. 

## <a name="retry-intervals"></a>Aralıkları yeniden deneyin

Olay kılavuz üstel geri alma yeniden deneme ilkesi olay teslimi için kullanır. Web kancası yanıt vermiyor veya bir hata kodu döndürüyor, zamanlama uyarınca hello Teslimde olay kılavuz yeniden deneme sayısı:

1. 10 saniye
2. 30 saniye
3. 1 dakika
4. 5 dakika
5. 10 dakika
6. 30 dakika
7. 1 saat

Olay kılavuz, küçük rasgele tooall yeniden deneme aralıkları ekler.

## <a name="retry-duration"></a>Süre yeniden deneyin

Merhaba Önizleme sırasında Azure olay kılavuz iki saat içinde teslim edilmedi tüm olayları süresi dolar. Genel kullanılabilirlik önce bu kez artan too24 saatleri olacaktır. 

## <a name="next-steps"></a>Sonraki adımlar

* Bir giriş tooEvent kılavuz için bkz: [hakkında olay kılavuz](overview.md).
* tooquickly olay kılavuz kullanımına başlamanıza bkz [Azure olay kılavuz oluşturma ve rota özel olaylarla](custom-event-quickstart.md).
