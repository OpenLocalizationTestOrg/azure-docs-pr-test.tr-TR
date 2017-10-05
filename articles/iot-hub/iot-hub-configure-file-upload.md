---
title: "Karşıya dosya yükleme yapılandırmak için Azure portalını kullanma | Microsoft Docs"
description: "Azure portalı bağlı dosya yüklemelerini etkinleştirmek için IOT hub'ınızı yapılandırma için nasıl kullanılacağını. Hedef Azure depolama hesabı yapılandırma hakkında bilgi içerir."
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
ms.openlocfilehash: 149dd84d7d8f4ff9cd30f9fc649ced3cb364cfb7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-iot-hub-file-uploads-using-the-azure-portal"></a><span data-ttu-id="d90a6-104">IOT Hub'ın Azure Portalı'nı kullanarak dosya yüklemeleri yapılandırın</span><span class="sxs-lookup"><span data-stu-id="d90a6-104">Configure IoT Hub file uploads using the Azure portal</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a><span data-ttu-id="d90a6-105">Karşıya dosya yükleme</span><span class="sxs-lookup"><span data-stu-id="d90a6-105">File upload</span></span>

<span data-ttu-id="d90a6-106">Kullanılacak [dosya karşıya yükleme işlevselliği IOT hub'da][lnk-upload], bir Azure Storage hesabı hub'ınıza ilk ilişkilendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d90a6-106">To use the [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your hub.</span></span> <span data-ttu-id="d90a6-107">Seçin **karşıya dosya yükleme** karşıya dosya yükleme özellikleri değiştirilmekte olan IOT hub'ına yönelik bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="d90a6-107">Select **File upload** to display a list of file upload properties for the IoT hub that is being modified.</span></span>

![Görünüm IOT hub'ı dosyayı karşıya portalındaki ayarları][13]

<span data-ttu-id="d90a6-109">**Depolama kapsayıcısı**: IOT Hub ile ilişkilendirmek için geçerli Azure aboneliğinizde bir Azure depolama hesabındaki bir blob kapsayıcısını seçmek için Azure portalını kullanın.</span><span class="sxs-lookup"><span data-stu-id="d90a6-109">**Storage container**: Use the Azure portal to select a blob container in an Azure Storage account in your current Azure subscription to associate with your IoT Hub.</span></span> <span data-ttu-id="d90a6-110">Gerekirse, bir Azure Storage hesabı oluşturabilirsiniz, **depolama hesapları** dikey ve blob kapsayıcısında **kapsayıcıları** dikey.</span><span class="sxs-lookup"><span data-stu-id="d90a6-110">If necessary, you can create an Azure Storage account on the **Storage accounts** blade and blob container on the **Containers** blade.</span></span> <span data-ttu-id="d90a6-111">IOT hub'ı SAS URI'ler dosyaları karşıya yükleme sırasında kullanmak cihazlar için bu blob kapsayıcısına yazma izinlerine sahip otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d90a6-111">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span></span>

![Karşıya dosya yükleme için depolama kapsayıcıları portalında görüntüleyin][14]

<span data-ttu-id="d90a6-113">**Karşıya yüklenen dosyalar için bildirimlerin**: etkinleştirmek veya dosya karşıya yükleme bildirimlerini geçiş aracılığıyla devre dışı.</span><span class="sxs-lookup"><span data-stu-id="d90a6-113">**Receive notifications for uploaded files**: Enable or disable file upload notifications via the toggle.</span></span>

<span data-ttu-id="d90a6-114">**SAS TTL**: saat yaşam IOT Hub tarafından cihaza döndürülen SAS URI, bu ayar değildir.</span><span class="sxs-lookup"><span data-stu-id="d90a6-114">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span></span> <span data-ttu-id="d90a6-115">Varsayılan olarak bir saat için ayarlanmış ancak kaydırıcıyı kullanarak diğer değerleri için özelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="d90a6-115">Set to one hour by default but can be customized to other values using the slider.</span></span>

<span data-ttu-id="d90a6-116">**Dosya bildirim ayarları varsayılan TTL**: süresi doldu önce bildirim zaman yaşam dosyasının karşıya.</span><span class="sxs-lookup"><span data-stu-id="d90a6-116">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="d90a6-117">Varsayılan olarak bir gün için ayarlanmış ancak kaydırıcıyı kullanarak diğer değerleri için özelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="d90a6-117">Set to one day by default but can be customized to other values using the slider.</span></span>

<span data-ttu-id="d90a6-118">**Dosya bildirim maksimum teslimat sayısı**: IOT hub'ı bir dosya teslim etmek için kaç deneme sayısı bildirim karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d90a6-118">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span></span> <span data-ttu-id="d90a6-119">Varsayılan olarak 10 olarak ayarlandı ancak kaydırıcıyı kullanarak diğer değerleri için özelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="d90a6-119">Set to 10 by default but can be customized to other values using the slider.</span></span>

![IOT hub'ı dosya karşıya yükleme portalında yapılandırın][15]

## <a name="next-steps"></a><span data-ttu-id="d90a6-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d90a6-121">Next steps</span></span>

<span data-ttu-id="d90a6-122">IOT hub'ı dosya karşıya yükleme özellikleri hakkında daha fazla bilgi için bkz: [karşıya bir aygıtı dosyalarından] [ lnk-upload] IOT Hub Geliştirici Kılavuzu'nda.</span><span class="sxs-lookup"><span data-stu-id="d90a6-122">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload] in the IoT Hub developer guide.</span></span>

<span data-ttu-id="d90a6-123">Azure IOT hub'ı yönetme hakkında daha fazla bilgi için bu bağlantıları izleyin:</span><span class="sxs-lookup"><span data-stu-id="d90a6-123">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="d90a6-124">[Toplu IOT cihazları yönetme][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="d90a6-124">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="d90a6-125">[IOT hub'ı ölçümleri][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="d90a6-125">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="d90a6-126">[İzleme işlemleri][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="d90a6-126">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="d90a6-127">Daha fazla IOT hub'ı özelliklerini keşfetmek için bkz:</span><span class="sxs-lookup"><span data-stu-id="d90a6-127">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="d90a6-128">[IOT Hub Geliştirici Kılavuzu][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="d90a6-128">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="d90a6-129">[Bir cihaz IOT Edge benzetimini yapma][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="d90a6-129">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="d90a6-130">[IOT çözümünüzden zemin oluşturan güvenli][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="d90a6-130">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

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
