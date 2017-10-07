---
title: "aaaUse hello Azure portal tooconfigure karşıya dosya yükleme | Microsoft Docs"
description: "Toouse hello nasıl Azure portal tooconfigure bağlı aygıtlardan IOT hub tooenable dosyanızı karşıya yükleme. Merhaba hedef Azure depolama hesabı yapılandırma hakkında bilgi içerir."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 915f1597-272d-4fd4-8c5b-a0ccb1df0d91
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: dobett
ms.openlocfilehash: b90c3fbed47b4eb144d3cb7480068b7cfc776ba6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-hello-azure-portal"></a>IOT hub'ı dosya yüklemeleriyle Hello Azure portal kullanarak yapılandırma

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a>Karşıya dosya yükleme

toouse hello [dosya karşıya yükleme işlevselliği IOT hub'da][lnk-upload], bir Azure Storage hesabı hub'ınıza ilk ilişkilendirmeniz gerekir. Seçin **karşıya dosya yükleme** toodisplay değiştiriliyor hello IOT hub için dosya karşıya yükleme özelliklerinin bir listesi.

![Görünüm IOT hub'ı dosyayı karşıya hello portalındaki ayarları][13]

**Depolama kapsayıcısı**: kullanım hello Azure portal tooselect, geçerli bir Azure aboneliği tooassociate IOT Hub'ınızı ile Azure depolama hesabında blob kapsayıcısı. Gerekirse, bir Azure depolama hesabı üzerinde hello oluşturabileceğiniz, **depolama hesapları** hello dikey ve blob kapsayıcısında **kapsayıcıları** dikey. Dosyaları karşıya yüklediğinizde IOT Hub cihazları toouse için yazma izinleri toothis blob kapsayıcısı ile SAS URI'ler otomatik olarak oluşturur.

![Karşıya dosya yükleme için depolama kapsayıcılarına hello portalında görüntüleyin][14]

**Karşıya yüklenen dosyalar için bildirimlerin**: etkinleştirmek veya dosya karşıya yükleme bildirimlerini hello geçiş aracılığıyla devre dışı.

**SAS TTL**: hello zaman yaşam SAS URI'ler toohello cihaz IOT Hub tarafından döndürülen Merhaba, bu bir ayardır. Varsayılan olarak tooone saat ayarlanmış ancak özelleştirilmiş tooother değerleri hello kaydırıcıyı kullanarak.

**Dosya bildirim ayarları varsayılan TTL**: hello zaman süresi doldu önce dosya karşıya yükleme bildirimi yaşam. Tooone günlük varsayılan olarak ayarlanmış, ancak özelleştirilmiş tooother değerleri hello kaydırıcıyı kullanarak.

**Dosya bildirim maksimum teslimat sayısı**: hello sayısı zaman hello IOT hub'ı denemeleri toodeliver dosya karşıya yükleme bildirimi. Too10 varsayılan olarak ayarlanmış, ancak özelleştirilmiş tooother değerleri hello kaydırıcıyı kullanarak.

![IOT hub'ı dosya karşıya yükleme hello portalında yapılandırın][15]

## <a name="next-steps"></a>Sonraki adımlar

IOT hub'ı hello dosya karşıya yükleme özellikleri hakkında daha fazla bilgi için bkz: [karşıya bir aygıtı dosyalarından] [ lnk-upload] hello IOT Hub Geliştirici Kılavuzu'nda.

Azure IOT hub'ı yönetme hakkında daha fazla bu bağlantılar toolearn izleyin:

* [Toplu IOT cihazları yönetme][lnk-bulk]
* [IOT hub'ı ölçümleri][lnk-metrics]
* [İzleme işlemleri][lnk-monitor]

toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:

* [IOT Hub Geliştirici Kılavuzu][lnk-devguide]
* [Bir cihaz IOT Edge benzetimini yapma][lnk-iotedge]
* [IOT çözümünüzden plan hello güvenli][lnk-securing]

[13]: ./media/iot-hub-configure-file-upload/file-upload-settings.png
[14]: ./media/iot-hub-configure-file-upload/file-upload-container-selection.png
[15]: ./media/iot-hub-configure-file-upload/file-upload-selected-container.png

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
