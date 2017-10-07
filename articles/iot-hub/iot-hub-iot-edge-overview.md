---
title: Azure IOT ucunun aaaOverview | Microsoft Docs
description: "Merhaba anahtar mimari kavramlarını Azure IOT edge'de ağ geçitleri, modüller ve aracıları gibi açıklar."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dobett
ms.openlocfilehash: 32debc0d4f40cfd7f2cce7cf8c76b12ec18ee2dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-edge-architectural-concepts"></a>Azure IOT kenar mimari kavramları

Tüm örnek kodu incelemeden veya IOT kenar kullanarak kendi alan ağ geçidi oluşturmadan önce hello IOT kenar hello mimarisini destekleyen temel kavramları anlamanız gerekir.

## <a name="iot-edge-modules"></a>IOT kenar modülleri

Bir ağ geçidi ile Azure IOT sınır oluşturma ve Birleştirme yapı *IOT kenar modülleri*. Modüllerini *iletileri* birbirleriyle tooexchange veri. Bir modül bir ileti alır, üzerinde bazı eylemleri gerçekleştirir, isteğe bağlı olarak yeni bir iletiye dönüştürür ve sonra diğer modüller tooprocess için yayımlar. Bazı modüller yalnızca yeni iletiler oluşturabilir ve hiçbir zaman gelen iletileri işlemez. Bir modül zinciri, o ardışık düzeninde bir noktada hello veri dönüştürme gerçekleştiriliyor her modül bir veri işleme işlem hattı oluşturur.

![Ağ geçidinde Azure IoT Edge ile oluşturulan modül zinciri][1]

IOT kenar hello aşağıdaki bileşenleri içerir:

* Ortak ağ geçidi işlevlerini yerine önceden yazılmış modüller.
* Geliştirici bir Hello arabirimleri toowrite özel modüller kullanabilirsiniz.
* Altyapı gerekli toodeploy hello ve bir modül kümesini çalıştırın.

Merhaba SDK çeşitli işletim sistemleri ve platformlar üzerinde toobuild ağ geçitleri toorun sağlayan bir soyutlama katmanı sağlar.

![Azure IoT Edge özet düzeyi][2]

## <a name="messages"></a>İletiler

Bir ağ geçidinin nasıl tooeach iletileri diğer uygun şekilde tooconceptualize olan geçirme modüllerine düşünüyorum rağmen bunu doğru şekilde ne olur yansıtmaz. IOT kenar modüller birbirleri ile Aracısı toocommunicate kullanın. Modüller (veri yolu veya Yayınla/Abone ol gibi Mesajlaşma modelleri kullanarak) iletileri toohello Aracısı yayımlayın ve hello Aracısı rota hello ileti toohello modülleri bağlı tooit olanak tanır.

Bir modül hello kullanan **Broker_Publish** toopublish bir ileti toohello Aracısı işlev. Merhaba Aracısı, bir geri çağırma işlevini çağırarak iletileri tooa modülü sunar. İleti bir dizi anahtar/değer özelliklerinden ve bir bellek bloğu olarak geçirilen içeriklerden oluşur.

![hello Azure IOT kenar Aracısı Hello rolü][3]

## <a name="message-routing-and-filtering"></a>İleti yönlendirme ve filtreleme

Toodirect iletileri toohello doğru IOT kenar modülleri iki yolu vardır:

* Bağlantılar kümesi geçirebilirsiniz hello Aracısı hello kaynak ve havuz her modül için bilmesi için toohello Aracısı geçirilebilir.
* Bir modül selamlama iletisine hello özelliklerini filtreleyebilirsiniz.

Selamlama iletisine için amaçlanıyorsa bir modülü yalnızca bir ileti üzerinde işlem yapmalıdır. Bağlantılar ve etkili bir şekilde filtreleme ileti ileti işlem hattını oluşturun.

## <a name="next-steps"></a>Sonraki adımlar

toosee çalıştırabilirsiniz, bir örnek uygulanan bu bkz [keşfedin Azure IOT kenar mimarisi][lnk-hello-world].

<!-- Images -->
[1]: media/iot-hub-iot-edge-overview/modules.png
[2]: media/iot-hub-iot-edge-overview/modules_2.png
[3]: media/iot-hub-iot-edge-overview/messages_1.png

<!-- Links -->
[lnk-hello-world]: ./iot-hub-linux-iot-edge-get-started.md