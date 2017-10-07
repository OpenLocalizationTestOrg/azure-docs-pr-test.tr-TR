---
title: "IOT hub'ı aaaUse hello Azure portal toocreate | Microsoft Docs"
description: "Nasıl toocreate, yönetin ve hello Azure Portalı aracılığıyla Azure IOT hub'ları silin. Fiyatlandırma katmanlarına, ölçeklendirme, güvenlik ve yapılandırma Mesajlaşma hakkında bilgi içerir."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0909cd2b-4c1e-49e0-b68a-75532caf0a6a
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: 383968c90ee7ef3bff85a6c90efbf5f0e8fbb208
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-portal"></a>Hello Azure portal kullanarak IOT hub oluşturma

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

Bu makalede açıklanır:

* Nasıl toofind, IOT Hub'hello Azure portal hizmetinde hello.
* Nasıl toocreate ve IOT hub'ları yönetin.

## <a name="where-toofind-hello-iot-hub-service"></a>Burada toofind hello IOT Hub hizmeti

Merhaba IOT Hub hizmeti aşağıdaki konumlardan hello portalında hello bulabilirsiniz:

* Seçin **+ yeni**, ardından **nesnelerin interneti**.
* Hello Market, seçin **nesnelerin interneti**.

## <a name="create-an-iot-hub"></a>IoT hub oluşturma

Bir IOT hub'hello aşağıdaki yöntemleri kullanarak oluşturabilirsiniz:

* Merhaba **+ yeni** seçeneği ekran görüntüsü aşağıdaki hello gösterilen hello dikey penceresini açar. Merhaba marketplace ve bu yöntem aracılığıyla hello IOT hub oluşturma hello adımları aynıdır.
* Hello Market, seçin **oluşturma** tooopen hello dikey ekran görüntüsü aşağıdaki hello gösterilmektedir.

Merhaba aşağıdaki bölümlerde açıklanmaktadır hello çeşitli adımları toocreate bir IOT hub:

### <a name="choose-hello-name-of-hello-iot-hub"></a>Merhaba IOT hub'ı Hello adını seçin

toocreate IOT hub'ı, hello IOT hub'ı adı olmalıdır. Bu ad, tüm IOT hub'ları arasında benzersiz olması gerekir.

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

### <a name="choose-hello-pricing-tier"></a>Merhaba fiyatlandırma katmanı seçin

Dört katmanları seçebilirsiniz: **serbest**, **standart 1** ve **standart 2**, ve **standart S3**. Hello ücretsiz katmanı 500 aygıtları toobe toohello IOT hub'ı bağlı yalnızca ve too8, günde 000 iletileri yedekleme sağlar.

**Standart S1**: çok sayıda her küçük miktarda veri oluşturur aygıtları çözümlere için kullanım hello S1 sürümü. Too400, tüm bağlı aygıtlar arasında günde 000 iletileri yukarı hello S1 edition her ölçü sağlar.

**Standart S2**: IOT çözümleri cihazları büyük miktarlarda verinin oluşturmak için kullanım hello S2 sürümü. Merhaba S2 edition her ölçü too6 tüm bağlı aygıtlar arasında günde milyon iletilerine izin verir.

**Standart S3**: büyük miktarlarda verinin oluşturmak IOT çözümleri için kullanım hello S3 sürümü. Merhaba S3 edition her ölçü too300 tüm bağlı aygıtlar arasında günde milyon iletilerine izin verir.

![][4]

> [!NOTE]
> IOT Hub, yalnızca bir ücretsiz hub Azure abonelik başına izin verir.

### <a name="iot-hub-units"></a>IOT hub'ı birimleri

gün başına birim başına izin verilen ileti Hello sayısı, hub'ın fiyatlandırma katmanında bağlıdır. Örneğin, IOT hub toosupport giriş 700.000 iletilerinin hello isterseniz, iki S1 katmanı birimleri seçin.

### <a name="device-toocloud-partitions-and-resource-group"></a>Aygıt toocloud bölümler ve kaynak grubu

IOT hub'ı için bölümlerin sayısı hello değiştirebilirsiniz. Merhaba varsayılan bölüm sayısı 4, farklı bir numara hello aşağı açılan listeden seçebilirsiniz.

İhtiyacınız olmayan tooexplicitly boş bir kaynak grubu oluşturun. Bir kaynak oluşturduğunuzda, yeni bir ya da toocreate seçin veya varolan bir kaynak grubunu kullanın.

![][5]

### <a name="choose-subscription"></a>Abonelik seçin

Azure IOT Hub, listeleri hello Azure abonelikleri hello kullanıcı hesabı için otomatik olarak bağlanır. Hello Azure aboneliği tooassociate hello IOT hub'ına seçebilirsiniz.

### <a name="choose-hello-location"></a>Başlangıç konumu seçin

IOT hub'ı kullanılabilir olduğu hello bölgelerin bir listesi Hello konum seçeneği sağlar.

### <a name="create-hello-iot-hub"></a>Merhaba IOT hub oluşturma

Önceki adımların tümünü tamamlandığı zaman hello IOT hub'ı oluşturabilirsiniz. Tıklatın **oluşturma** toostart arka uç işlem toocreate hello ve seçtiğiniz hello seçeneklerle hello IOT hub'ı dağıtın.

Merhaba uygun konuma sunucularda hello arka uç dağıtım toorun süredir yararlanırken birkaç dakika toocreate hello IOT hub alabilir.

## <a name="change-hello-settings-of-hello-iot-hub"></a>Merhaba IOT hub'ının Hello ayarlarını değiştirme

IOT Hub dikey penceresinde hello oluşturulduktan sonra var olan IOT hub'ı hello ayarlarını değiştirebilirsiniz.

![][8]

**Paylaşılan erişim ilkeleri**: cihazları ve Hizmetleri tooconnect tooIoT Hub hello izinlerini bu ilkeleri tanımlar. Bu ilkeler tıklatarak erişebilirsiniz **paylaşılan erişim ilkeleri** altında **genel**. Bu dikey pencerede, varolan ilkeleri değiştirmek veya yeni bir ilke ekleme.

### <a name="create-a-policy"></a>Bir ilke oluşturun

* Tıklatın **Ekle** tooopen bir dikey pencere. Merhaba yeni ilke adı buraya girin ve hello aşağıda gösterildiği gibi bu ilke ile tooassociate istediğiniz hello izinleri şekil:

    Bu paylaşılan ilkeleriyle ilişkilendirilebilir birkaç izinleri vardır. Merhaba **okuma kayıt defteri** ve **kayıt defteri yazma** ilkeleri okuma ve yazma erişimi hakları toohello kimlik kayıt defteri verin. Merhaba yazma seçeneği otomatik olarak seçme seçeneği hello okuma seçer.

    Merhaba **Service bağlanma** İlkesi izni tooaccess gibi hizmet uç noktaları verir **alma cihaz bulut**. Merhaba **aygıtı bağlayın** İlkesi hello IOT Hub cihaz tarafındaki uç noktalarını kullanarak ileti gönderme ve alma için izinler verir.

* Tıklatın **oluşturma** tooadd bu yeni oluşturulmuş İlkesi toohello varolan listesi.

![][10]

## <a name="endpoints"></a>Uç Noktalar

Tıklatın **uç noktaları** toodisplay değiştirdiğiniz hello IOT hub için uç nokta listesi. Uç noktaları iki tür vardır: Merhaba IOT hub'ına yerleşik uç noktaları ve uç noktaları toohello IOT hub'ı oluşturulduktan sonra ekleyin.

![][11]

### <a name="built-in-endpoints"></a>Yerleşik uç noktaları

İki yerleşik uç noktalar vardır: **bulut toodevice geri bildirim** ve **olayları**.

* **Bulut toodevice geri bildirim** ayarları: Bu ayar iki subsettings sahiptir: **tooDevice TTL bulut** (time-to-live) ve **bekletme süresini** (saat) içindeki Merhaba iletileri için. İlk oluşturduğunuzda, IOT hub'ı hem de bu ayarları bir saat hello varsayılan değere sahip. tooadjust bu ayarları hello kaydırma çubuklarını kullanın veya hello değerler girin.
* **Olayları** ayarları: Bu ayar salt okunur bazıları aşağıda verilen birkaç subsettings sahiptir. liste aşağıdaki hello bu ayarları açıklanmaktadır:

  * **Bölümler**: Merhaba IOT hub'ı oluşturduğunuzda varsayılan bir değer ayarlanır. Bu ayar aracılığıyla bölüm sayısı hello değiştirebilirsiniz.

  * **Olay Hub ile uyumlu ada ve uç nokta**: Merhaba IOT hub'ı oluşturduğunuzda olay hub'ı dahili olarak, toounder belirli koşullar erişim oluşturulur. Merhaba Event Hub ile uyumlu adı ve uç nokta değerleri özelleştiremezsiniz ancak tıklayarak kopyalayabilirsiniz **kopya**.

  * **Saklama süresi**: tooone günlük varsayılan olarak ayarlanmış ancak hello açılan listeyi kullanarak değiştirebilirsiniz. Bu değer hello cihaz bulut ayarı için gün olur.

  * **Tüketici grupları**: tüketici grupları birden çok okuyucular tooread iletilerden bağımsız olarak hello IOT hub'ı etkinleştirin. Her IOT hub ile varsayılan bir tüketici grubu oluşturulur. Ancak, eklemek veya bu ayarı kullanarak tüketici grupları tooyour IOT hub'ları silin.

  > [!NOTE]
  > Merhaba varsayılan bir tüketici grubu silinmiş veya düzenlenemez.

### <a name="custom-endpoints"></a>Özel uç noktaları

Merhaba portal kullanarak IOT hub'da özel uç noktalar ekleyebilirsiniz. Hello gelen **uç noktaları** dikey penceresinde tıklatın **Ekle** hello üst tooopen hello adresindeki **uç nokta ekleyin** dikey. Merhaba gerekli bilgileri girin ve ardından **Tamam**. Özel uç noktanızı şimdi hello ana listelenen **uç noktaları** dikey.

![][13]

Daha fazla bilgiyi özel uç noktalarını hakkında [başvuru - IOT hub uç noktaları][lnk-devguide-endpoints].

## <a name="routes"></a>Yollar

Tıklatın **yollar** toomanage nasıl IOT Hub, cihaz-bulut iletileri gönderir.

![][14]

Yollar tooyour IOT hub'ı tıklatarak ekleyebileceğiniz **Ekle** hello hello üstündeki **yollar*** hello gerekli bilgileri girerek ve tıklayarak dikey **Tamam**. Rota hello ana sonra listelenen **yollar** dikey. Bir rota hello yollar listesinde tıklayarak düzenleyebilirsiniz. tooenable bir rota yolların hello listeyi tıklatın ve ayarlama hello **etkin** çok geçiş**devre dışı**. toosave hello Değiştir'i tıklatın **Tamam** hello dikey penceresinde hello sonundaki.

![][15]

## <a name="pricing-and-scale"></a>Fiyatlandırma ve ölçek

var olan bir IOT hub ' Hello fiyatlandırma hello değiştirilebilir **fiyatlandırma** ayarlarla hello aşağıdaki özel durumlar:

* Hello geçerli uygulamasında katmanları tooone SKU'ları, ücretli Merhaba, bir IOT hub ile boş bir SKU değiştirilemiyor veya tam tersi.
* Yalnızca olabilir bir ücretsiz katmanı IOT hub'hello Azure aboneliği.

![][12]

Yalnızca o gün gönderilen ileti sayısını hello hello hello alt katmanı için kotasına zaman daha yüksek bir toolower katmanından taşıyabilirsiniz. Örneğin, günde iletilerinin Hello sayısı 400.000 aşarsa, ardından hello IOT hub değiştirilebilir katmanını hello. Ancak, toohello S1 katmanı değiştirirseniz hello IOT hub'ı o gün için kısıtlanır.

## <a name="delete-hello-iot-hub"></a>Merhaba IOT hub'ını silmek

Toohello IOT hub'ı tıklatarak toodelete istediğiniz göz atabilirsiniz **Gözat**, ve ardından uygun hub toodelete hello. toodelete IOT hub'ı Merhaba, hello tıklatın **silmek** hello IOT hub'ı adı altındaki düğme.

## <a name="next-steps"></a>Sonraki adımlar

Azure IOT hub'ı yönetme hakkında daha fazla bu bağlantılar toolearn izleyin:

* [Toplu IOT cihazları yönetme][lnk-bulk]
* [IOT hub'ı ölçümleri][lnk-metrics]
* [İzleme işlemleri][lnk-monitor]

toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:

* [IOT Hub Geliştirici Kılavuzu][lnk-devguide]
* [Bir cihaz IOT Edge benzetimini yapma][lnk-iotedge]
* [IOT çözümünüzden plan hello güvenli][lnk-securing]

[4]: ./media/iot-hub-create-through-portal/create-iothub.png
[5]: ./media/iot-hub-create-through-portal/location1.png
[8]: ./media/iot-hub-create-through-portal/portal-settings.png
[10]: ./media/iot-hub-create-through-portal/shared-access-policies.png
[11]: ./media/iot-hub-create-through-portal/messaging-settings.png
[12]: ./media/iot-hub-create-through-portal/pricing-error.png
[13]: ./media/iot-hub-create-through-portal/endpoint-creation.png
[14]: ./media/iot-hub-create-through-portal/routes-list.png
[15]: ./media/iot-hub-create-through-portal/route-edit.png

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
