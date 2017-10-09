---
title: "aaaAzure IOT Hub IP bağlantı filtrelerini | Microsoft Docs"
description: "Nasıl tooyour Azure IOT hub için belirli IP tooblock bağlantılarından filtreleme toouse IP adresleri. Tek tek bağlantılarından veya IP adres aralıklarını engelleyebilirsiniz."
services: iot-hub
documentationcenter: 
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: f833eac3-5b5f-46a7-a47b-f4f6fc927f3f
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: boltean
ms.openlocfilehash: 45e5906a494561b6108895d86d6a04fc3b52b8fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-ip-filters"></a>IP filtreleri kullanın

Güvenlik Azure IOT hub'ına bağlı herhangi bir IOT çözümü önemli bir yönüdür. Bazen tooexplicitly gereken güvenlik yapılandırmanızın bir parçası, cihazları bağlanabilir hello IP adreslerini belirtin. Merhaba _IP Filtresi_ özelliği tooconfigure kurallarını reddetme veya belirli IPv4 adresleri gelen trafiği kabul etmesini sağlar.

## <a name="when-toouse"></a>Zaman toouse

Belirli IP adresleri için yararlı tooblock hello IOT Hub uç noktaları olduğunda iki belirli kullanım örnekleri şunlardır:

- IOT hub'ınızı trafiği yalnızca belirtilen IP adreslerinden almak ve şey Reddet gerekir. Örneğin, IOT hub'ınıza kullanarak [Azure Express rota] toocreate IOT hub'ı ve şirket içi altyapınızı arasında özel bağlantılar.
- Kuşkulu olarak hello IOT hub'ı yönetici tarafından belirlenen IP adreslerinden gelen tooreject trafiğine gerekir.

## <a name="how-filter-rules-are-applied"></a>Filtre kuralları nasıl uygulanır

Hello IP Filtresi kuralları IOT hub'ı hizmet düzeyi hello sırasında uygulanır. Bu nedenle cihazları ve herhangi bir desteklenen protokolünü kullanarak arka uç uygulamaları tooall bağlantılarını hello IP filtresi kurallarını uygulayın.

IOT hub'ınızdaki rejecting IP kuralıyla eşleşen bir IP adresinden gelen bağlantı girişimleri yetkisiz 401 durum kodu ve açıklama alır. Merhaba yanıt iletisi hello IP kural Bahsediyor değil.

## <a name="default-setting"></a>Varsayılan ayar

Varsayılan olarak, hello **IP Filtresi** hello portalında bir IOT hub'ına yönelik kılavuz boştur. Bu varsayılan ayarı hub'ınızı herhangi bir IP adresi bağlantılarını kabul anlamına gelir. Bu varsayılan ayarı hello 0.0.0.0/0 IP adresi aralığı kabul eşdeğer tooa kuralıdır.

![IOT hub'ı varsayılan IP Filtresi Ayarları][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a>IP filtre kuralı Ekle veya Düzenle

IP filtre kuralı eklediğinizde, aşağıdaki değerleri Merhaba istenir:

- Bir **IP filtre kuralı adı** too128 karakter uzunluğunda yukarı benzersiz, büyük küçük harf duyarsız, alfasayısal bir dize olmalıdır. Yalnızca ASCII 7 bit hello alfasayısal karakterler artı `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` kabul edilir.
- Seçin bir **Reddet** veya **kabul** hello olarak **eylem** hello IP filtre kuralı için.
- Tek bir IPv4 adresi veya IP adreslerinin CIDR gösteriminde sağlar. Örneğin, içinde CIDR gösterimi 192.168.100.0/22 hello 1024 IPv4 adresleri 192.168.100.0 temsil eden too192.168.103.255.

![IP filtre kuralı tooan IOT hub'ı ekleme][img-ip-filter-add-rule]

Hello kural kaydettikten sonra o hello güncelleştirme devam ediyor bildiren bir uyarı görürsünüz.

![IP filtre kuralı kaydetme hakkında bildirim][img-ip-filter-save-new-rule]

Merhaba **Ekle** hello en fazla 10 IP filtresi kurallarını ulaştığında seçeneği devre dışıdır.

Mevcut bir kuralı hello kuralı içeren hello satır çift tıklayarak düzenleyebilirsiniz.

> [!NOTE]
> Reddetme IP adresleri hello IOT hub ile etkileşim diğer Azure Hizmetleri (örneğin, Azure akış analizi, Azure sanal makineleri veya hello aygıt Explorer hello Portalı'nda) engelleyebilirsiniz.

> [!WARNING]
> IP Filtresi etkinleştirilmiş bir IOT hub'ı Azure akış analizi (ASA) tooread iletileri kullanıyorsanız hello Event Hub ile uyumlu ada ve IOT hub'ınızın uç hello ASA bağlantı dizesi kullanın.

## <a name="delete-an-ip-filter-rule"></a>IP filtre kuralını Sil

toodelete bir IP filtre kuralı seçin bir veya daha fazla kural hello kılavuz ve tıklatın **silmek**.

![Bir IOT Hub IP Filtresi kuralını silmek][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a>IP filtre kural değerlendirmesi

IP filtresi kurallarını sırayla uygulanır ve hello ilk kural eşleşen hello IP adresi hello belirler veya eylem reddedebilirsiniz.

Örneğin, hello aralığı 192.168.100.0/22 tooaccept adresleri istiyorsanız ve şey Reddet hello ilk kural hello kılavuzunda hello adres aralığı 192.168.100.0/22 kabul etmelidir. Merhaba sonraki kural hello aralığı 0.0.0.0/0 kullanarak tüm adresleri reddedecek.

Merhaba üç dikey noktalar hello başlangıç satır tıklayarak ve sürükleme kullanarak IP Filtresi kurallarınızı hello kılavuzunda hello sırasını değiştirmek ve bırakın.

Yeni IP toosave filtre kuralı sipariş, tıklatın **kaydetmek**.

![IOT Hub IP Filtresi kurallarınızı Hello sırasını değiştirme][img-ip-filter-rule-order]

## <a name="next-steps"></a>Sonraki adımlar

toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:

- [İzleme işlemleri][lnk-monitor]
- [IOT hub'ı ölçümleri][lnk-metrics]

<!-- Images -->
[img-ip-filter-default]: ./media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: ./media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: ./media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: ./media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: ./media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
[Azure Express rota]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md