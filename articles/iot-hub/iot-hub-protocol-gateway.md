---
title: "aaaAzure IOT protokolü ağ geçidini | Microsoft Docs"
description: "Nasıl toouse bir Azure IOT ağ geçidi tooextend IOT hub'ı yetenekleri ve protokol desteği tooenable aygıtları tooconnect tooyour hub IOT Hub tarafından yerel olarak desteklenmeyen protokolleri kullanarak protokol."
services: iot-hub
documentationcenter: 
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 555e59ae-3136-4533-8ba8-f3a3b6acf648
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.openlocfilehash: 9cfed30149672d8f7e021a9899192105bbcdd400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# IOT hub'ına yönelik destek ek protokoller
Azure IOT hub'ı yerel olarak hello MQTT, AMQP ve HTTP protokolleri iletişimi destekler. Bazı durumlarda, aygıtları veya alan ağ geçitleri mümkün toouse bu standart protokollerden birini olmayabilir ve protokolü uyarlama gerektirir. Böyle durumlarda, özel bir ağ geçidi kullanabilirsiniz. Özel bir ağ geçidi Protokolü uyarlama IOT Hub uç noktaları için hello trafiği tooand IOT hub'dan köprüleme tarafından etkinleştirebilirsiniz. Merhaba kullanabilirsiniz [Azure IOT protokolü ağ geçidini](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md) bir özel ağ geçidi tooenable Protokolü uyarlama IOT hub'ına yönelik olarak.

## Azure IOT protokolü ağ geçidi
Hello Azure IOT protokolü ağ geçidini, büyük ölçekli, IOT Hub ile çift yönlü aygıt iletişim için tasarlanmış Protokolü uyarlama için bir çerçevedir. Merhaba protokol ağ geçidi, belirli bir protokolü üzerinden cihaz bağlantılarını kabul doğrudan bir bileşenidir. Merhaba trafik tooIoT Hub AMQP 1.0 arasında köprü. Hello Azure IOT protokolü ağ geçidini çeşitli protokolleri ve protokol sürümleri için destek eklemek için bir açık kaynaklı yazılım proje tooprovide esneklik olarak kullanılabilir.

Azure Service Fabric, Azure Cloud Services çalışan roller ya da Windows sanal makineleri kullanarak azure'da hello protokol ağ geçidi yüksek düzeyde ölçeklenebilir bir şekilde dağıtabilirsiniz. Ayrıca, şirket içi ortamlarda, alan ağ geçitleri gibi hello protokol ağ geçidi dağıtılabilir.

Hello Azure IOT protokolü ağ geçidi, MQTT protokol davranışı gerekirse toocustomize hello sağlayan MQTT Protokolü bağdaştırıcıyı içerir. IOT hub'ı hello MQTT v3.1.1 protokolü için yerleşik destek sağlayan bu yana yalnızca Protokolü özelleştirmeleri veya ek işlevsellik için belirli gereksinimler gerekirse hello MQTT Protokolü bağdaştırıcısını kullanmayı düşünmeniz gerekir.

Merhaba MQTT bağdaştırıcısı de diğer protokolleri için iletişim kuralı bağdaştırıcıları oluşturmak için programlama modelini hello gösterir. Ayrıca, hello Azure IOT protokolü ağ geçidi programlama modeli, tooplug özel bileşenleri için özelleştirilmiş işlem özel kimlik doğrulama, ileti dönüşümleri, sıkıştırma/açma veya trafiği şifreleme/şifre çözme gibi sağlar Merhaba cihazlar ve IOT hub'ı arasında.

Esneklik için açık kaynaklı yazılım projesinde hello protokol ağ geçidi ve MQTT uygulama sağlanır. Bu, gerektiği gibi toocustomize hello uygulaması sağlar.

## Sonraki adımlar
toolearn hello Azure IOT protokolü ağ geçidi hakkında daha fazla bilgi ve nasıl toouse ve IOT çözümünüzün bir parçası olarak dağıtmak için bkz:

* [Github'daki Azure IOT protokolü ağ geçidi deposu](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md)
* [Azure IOT protokolü ağ geçidi Geliştirici Kılavuzu](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/docs/DeveloperGuide.md)

IOT hub'ı dağıtımınızı planlama hakkında daha fazla toolearn bakın:

* [Event Hubs ile karşılaştırın][lnk-compare]
* [Ölçeklendirme, HA ve DR][lnk-scaling]
* [IOT Hub Geliştirici Kılavuzu][lnk-devguide]

[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
