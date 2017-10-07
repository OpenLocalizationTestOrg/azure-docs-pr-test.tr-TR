---
title: "Bildirim hub'ları için aaaSecurity"
description: "Bu konu Azure bildirim hub'ları için güvenlik açıklar."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: 6506177c-e25c-4af7-8508-a3ddca9dc07c
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: f59ad4594c2c0a2e2b22ab0b6d6bad53825a4dc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="security"></a>Güvenlik
## <a name="overview"></a>Genel Bakış
Bu konu Azure bildirim hub'larını hello güvenlik modeli açıklanır. Bildirim hub'ları Service Bus varlık olduğundan, hello uyguladıkları aynı güvenlik modeli olarak hizmet veri yolu. Daha fazla bilgi için bkz: Merhaba [hizmet veri yolu kimlik doğrulaması](https://msdn.microsoft.com/library/azure/dn155925.aspx) Konular.

## <a name="shared-access-signature-security-sas"></a>Paylaşılan erişim imzası güvenlik (SAS)
Bildirim hub'ları bir varlık düzeyinde güvenlik şeması uygulayan SAS (paylaşılan erişim imzası) olarak adlandırılır. Bu düzen, Mesajlaşma varlıkları toodeclare varlık hakları too12 yetkilendirme kuralları kendi açıklama sağlar.

"Güvenlik taleplerini." Merhaba bölümünde açıklandığı gibi her bir kural bir ad, bir anahtar değeri (paylaşılan gizliliği) ve hakları, bir dizi içeriyor Bildirim hub'ı oluştururken, iki kuralları otomatik olarak oluşturulur: istemci uygulama kullandığı hello) dinleme hakları (ve (uygulama arka uç kullanır hello) tüm haklarına sahip bir biriyle.

Kayıt Yönetimi aracılığıyla Hello bilgi gönderirse istemci uygulamalardan gerçekleştirirken bildirimleri (örneğin, hava durumu güncelleştirmelerini) duyarlı değil, yaygın bir şekilde tooaccess bir bildirim hub'ı toogive hello anahtar hello kural yalnızca dinleme erişimi toohello değeri istemci uygulama ve toogive hello anahtar değeri hello kural tam erişim toohello uygulama arka ucu.

Windows mağazası istemci uygulamalarında hello anahtar değeri katıştırmak önerilmez. Merhaba anahtar değeri katıştırma bir şekilde tooavoid olan toohave hello istemci uygulamasını almak, başlangıçta hello uygulama arka.

Önemli dinleme erişim anahtarıyla hello toounderstand uygulama tooregister herhangi bir etiket için bir istemci sağlar. Uygulamanızı kayıtlar toospecific etiketleri toospecific istemcileri (örneğin, kullanıcı kimliklerini etiketleri temsil ettiğinde) kısıtlamanız gerekiyorsa, uygulamanızın arka ucuna hello kayıtlar gerçekleştirmeniz gerekir. Daha fazla bilgi için bkz: kayıt yönetimi. Bu şekilde, doğrudan erişim tooNotification hub hello istemci uygulaması olmaz unutmayın.

## <a name="security-claims"></a>Güvenlik taleplerini
Benzer tooother varlıklar, bildirim hub'ı işlemleri için üç güvenlik taleplerini verilir: dinleme, Gönder ve Yönet.

| İste | Açıklama | İzin verilen işlemler |
| --- | --- | --- |
| Dinleme |Oluştur/güncelleştir, okuma ve tek kayıtları silme |Kayıt oluştur/güncelleştir<br><br>Kayıt okuma<br><br>Tüm kayıtlar için bir tanıtıcı okuma<br><br>Kayıt silme |
| Gönder |Toohello bildirim hub'ı iletileri gönder |İleti gönderme |
| Yönet |Bildirim hub'ları (PNS kimlik bilgileri ve güvenlik anahtarları güncelleştirme dahil) ve etiketlere göre okuma kayıtlar cRUDs |Oluşturma/güncelleştirme/okuma/silme bildirim hub'ları<br><br>Etikete göre kayıtları oku |

Bildirim hub'ları doğrudan hello bildirim Hub'üzerinde yapılandırılmış paylaşılan anahtarlar ile oluşturulan imza belirteçleri ve Microsoft Azure erişim denetimi belirteçleri tarafından verilen bir talep kabul edin.

