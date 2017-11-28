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
# <a name="configure-iot-hub-file-uploads-using-hello-azure-portal"></a><span data-ttu-id="37e17-104">IOT hub'ı dosya yüklemeleriyle Hello Azure portal kullanarak yapılandırma</span><span class="sxs-lookup"><span data-stu-id="37e17-104">Configure IoT Hub file uploads using hello Azure portal</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a><span data-ttu-id="37e17-105">Karşıya dosya yükleme</span><span class="sxs-lookup"><span data-stu-id="37e17-105">File upload</span></span>

<span data-ttu-id="37e17-106">toouse hello [dosya karşıya yükleme işlevselliği IOT hub'da][lnk-upload], bir Azure Storage hesabı hub'ınıza ilk ilişkilendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="37e17-106">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your hub.</span></span> <span data-ttu-id="37e17-107">Seçin **karşıya dosya yükleme** toodisplay değiştiriliyor hello IOT hub için dosya karşıya yükleme özelliklerinin bir listesi.</span><span class="sxs-lookup"><span data-stu-id="37e17-107">Select **File upload** toodisplay a list of file upload properties for hello IoT hub that is being modified.</span></span>

![Görünüm IOT hub'ı dosyayı karşıya hello portalındaki ayarları][13]

<span data-ttu-id="37e17-109">**Depolama kapsayıcısı**: kullanım hello Azure portal tooselect, geçerli bir Azure aboneliği tooassociate IOT Hub'ınızı ile Azure depolama hesabında blob kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="37e17-109">**Storage container**: Use hello Azure portal tooselect a blob container in an Azure Storage account in your current Azure subscription tooassociate with your IoT Hub.</span></span> <span data-ttu-id="37e17-110">Gerekirse, bir Azure depolama hesabı üzerinde hello oluşturabileceğiniz, **depolama hesapları** hello dikey ve blob kapsayıcısında **kapsayıcıları** dikey.</span><span class="sxs-lookup"><span data-stu-id="37e17-110">If necessary, you can create an Azure Storage account on hello **Storage accounts** blade and blob container on hello **Containers** blade.</span></span> <span data-ttu-id="37e17-111">Dosyaları karşıya yüklediğinizde IOT Hub cihazları toouse için yazma izinleri toothis blob kapsayıcısı ile SAS URI'ler otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="37e17-111">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

![Karşıya dosya yükleme için depolama kapsayıcılarına hello portalında görüntüleyin][14]

<span data-ttu-id="37e17-113">**Karşıya yüklenen dosyalar için bildirimlerin**: etkinleştirmek veya dosya karşıya yükleme bildirimlerini hello geçiş aracılığıyla devre dışı.</span><span class="sxs-lookup"><span data-stu-id="37e17-113">**Receive notifications for uploaded files**: Enable or disable file upload notifications via hello toggle.</span></span>

<span data-ttu-id="37e17-114">**SAS TTL**: hello zaman yaşam SAS URI'ler toohello cihaz IOT Hub tarafından döndürülen Merhaba, bu bir ayardır.</span><span class="sxs-lookup"><span data-stu-id="37e17-114">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="37e17-115">Varsayılan olarak tooone saat ayarlanmış ancak özelleştirilmiş tooother değerleri hello kaydırıcıyı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="37e17-115">Set tooone hour by default but can be customized tooother values using hello slider.</span></span>

<span data-ttu-id="37e17-116">**Dosya bildirim ayarları varsayılan TTL**: hello zaman süresi doldu önce dosya karşıya yükleme bildirimi yaşam.</span><span class="sxs-lookup"><span data-stu-id="37e17-116">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="37e17-117">Tooone günlük varsayılan olarak ayarlanmış, ancak özelleştirilmiş tooother değerleri hello kaydırıcıyı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="37e17-117">Set tooone day by default but can be customized tooother values using hello slider.</span></span>

<span data-ttu-id="37e17-118">**Dosya bildirim maksimum teslimat sayısı**: hello sayısı zaman hello IOT hub'ı denemeleri toodeliver dosya karşıya yükleme bildirimi.</span><span class="sxs-lookup"><span data-stu-id="37e17-118">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="37e17-119">Too10 varsayılan olarak ayarlanmış, ancak özelleştirilmiş tooother değerleri hello kaydırıcıyı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="37e17-119">Set too10 by default but can be customized tooother values using hello slider.</span></span>

![IOT hub'ı dosya karşıya yükleme hello portalında yapılandırın][15]

## <a name="next-steps"></a><span data-ttu-id="37e17-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="37e17-121">Next steps</span></span>

<span data-ttu-id="37e17-122">IOT hub'ı hello dosya karşıya yükleme özellikleri hakkında daha fazla bilgi için bkz: [karşıya bir aygıtı dosyalarından] [ lnk-upload] hello IOT Hub Geliştirici Kılavuzu'nda.</span><span class="sxs-lookup"><span data-stu-id="37e17-122">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload] in hello IoT Hub developer guide.</span></span>

<span data-ttu-id="37e17-123">Azure IOT hub'ı yönetme hakkında daha fazla bu bağlantılar toolearn izleyin:</span><span class="sxs-lookup"><span data-stu-id="37e17-123">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="37e17-124">[Toplu IOT cihazları yönetme][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="37e17-124">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="37e17-125">[IOT hub'ı ölçümleri][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="37e17-125">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="37e17-126">[İzleme işlemleri][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="37e17-126">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="37e17-127">toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:</span><span class="sxs-lookup"><span data-stu-id="37e17-127">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="37e17-128">[IOT Hub Geliştirici Kılavuzu][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="37e17-128">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="37e17-129">[Bir cihaz IOT Edge benzetimini yapma][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="37e17-129">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="37e17-130">[IOT çözümünüzden plan hello güvenli][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="37e17-130">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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
