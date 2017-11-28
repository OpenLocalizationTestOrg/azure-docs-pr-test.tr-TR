---
title: "aaaMicrosoft Azure IOT Paketi'ne Genel Bakış | Microsoft Docs"
description: "Azure IOT paketi önceden yapılandırılmış çözümler toocollect şey, Internet nasıl sunar genel bakış çözümleme, verileri depolamak, görselleştirmeler sağlamak ve diğer sistemlerle tümleştirmek."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2d38d08a-4133-4e5c-8b28-f93cadb5df05
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 385025c5ec0d37c74689a928bc09e85b33439634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-iot-suite"></a><span data-ttu-id="53a38-103">Azure IoT Paketi’ne Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="53a38-103">Overview of Azure IoT Suite</span></span>

<span data-ttu-id="53a38-104">Hello Azure Internet interneti (IOT) Hizmetleri çok çeşitli özellikler sunar.</span><span class="sxs-lookup"><span data-stu-id="53a38-104">hello Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="53a38-105">Bu kurumsal sınıf hizmetler şunları yapmanızı sağlar:</span><span class="sxs-lookup"><span data-stu-id="53a38-105">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="53a38-106">Cihazlardan veri toplama</span><span class="sxs-lookup"><span data-stu-id="53a38-106">Collect data from devices</span></span>
* <span data-ttu-id="53a38-107">Hareket halinde veri akışı çözümleme</span><span class="sxs-lookup"><span data-stu-id="53a38-107">Analyze data streams in-motion</span></span>
* <span data-ttu-id="53a38-108">Büyük veri gruplarını depolama ve sorgulama</span><span class="sxs-lookup"><span data-stu-id="53a38-108">Store and query large data sets</span></span>
* <span data-ttu-id="53a38-109">Gerçek zamanlı ve geçmiş verileri görselleştirme</span><span class="sxs-lookup"><span data-stu-id="53a38-109">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="53a38-110">Arka ofis sistemleriyle tümleştirme</span><span class="sxs-lookup"><span data-stu-id="53a38-110">Integrate with back-office systems</span></span>
* <span data-ttu-id="53a38-111">Cihazlarınızı yönetme</span><span class="sxs-lookup"><span data-stu-id="53a38-111">Manage your devices</span></span>

<span data-ttu-id="53a38-112">toodeliver bu özellikler, Azure IOT paketi paketleri birlikte birden çok Azure hizmetini özel uzantılarla *önceden yapılandırılmış çözümleri*.</span><span class="sxs-lookup"><span data-stu-id="53a38-112">toodeliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as *preconfigured solutions*.</span></span> <span data-ttu-id="53a38-113">Bu önceden yapılandırılmış çözümler, IOT çözümlerinizi toodeliver ele tooreduce hello zaman yardımcı genel IOT çözümü düzenlerinin temel uygulamalarıdır.</span><span class="sxs-lookup"><span data-stu-id="53a38-113">These preconfigured solutions are base implementations of common IoT solution patterns that help tooreduce hello time you take toodeliver your IoT solutions.</span></span> <span data-ttu-id="53a38-114">Hello kullanarak [IOT yazılım geliştirme setleri][lnk-sdks], özelleştirebilir ve bu çözümler toomeet kendi gereksinimlerinizi genişletir.</span><span class="sxs-lookup"><span data-stu-id="53a38-114">Using hello [IoT software development kits][lnk-sdks], you can customize and extend these solutions toomeet your own requirements.</span></span> <span data-ttu-id="53a38-115">Ayrıca bu çözümleri, yeni IoT çözümleri geliştirirken örnekler ya da şablonlar olarak da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53a38-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="53a38-116">Merhaba aşağıdaki video giriş tooAzure IOT paketi sağlar:</span><span class="sxs-lookup"><span data-stu-id="53a38-116">hello following video provides an introduction tooAzure IoT Suite:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON309/player]
> 
> 

## <a name="azure-iot-services-in-azure-iot-suite"></a><span data-ttu-id="53a38-117">Azure IoT Paketindeki Azure IoT Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="53a38-117">Azure IoT services in Azure IoT Suite</span></span>
<span data-ttu-id="53a38-118">Merhaba önceden yapılandırılmış çözümler genellikle aşağıdaki hizmetleri hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="53a38-118">hello preconfigured solutions typically use hello following services:</span></span>

* <span data-ttu-id="53a38-119">Çekirdek tooAzure IOT paketi olan hello [Azure IOT Hub] [ lnk-iot-hub] hizmet.</span><span class="sxs-lookup"><span data-stu-id="53a38-119">Core tooAzure IoT Suite is hello [Azure IoT Hub][lnk-iot-hub] service.</span></span> <span data-ttu-id="53a38-120">Bu hizmet hello cihaz-bulut sağlar ve bulut-cihaz Mesajlaşma işlevlerini ve ağ geçidi toohello hello gibi davranır Bulut ve diğer önemli IOT paketi hizmetlerini hello.</span><span class="sxs-lookup"><span data-stu-id="53a38-120">This service provides hello device-to-cloud and cloud-to-device messaging capabilities and acts as hello gateway toohello cloud and hello other key IoT Suite services.</span></span> <span data-ttu-id="53a38-121">Merhaba hizmet cihazınızdan ölçekte tooreceive iletilerden sağlar ve komutları tooyour aygıtları gönderin.</span><span class="sxs-lookup"><span data-stu-id="53a38-121">hello service enables you tooreceive messages from your devices at scale, and send commands tooyour devices.</span></span> <span data-ttu-id="53a38-122">Merhaba hizmeti de sağlar, çok[cihazlarınızı yönetmek][lnk-device-management].</span><span class="sxs-lookup"><span data-stu-id="53a38-122">hello service also enables you too[manage your devices][lnk-device-management].</span></span> <span data-ttu-id="53a38-123">Örneğin, yapılandırma, yeniden başlatma veya bir veya daha fazla aygıtları bağlı toohello hub bir Fabrika gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="53a38-123">For example, you can configure, reboot, or perform a factory reset on one or more devices connected toohello hub.</span></span>
* <span data-ttu-id="53a38-124">[Azure Stream Analytics][lnk-asa] hareket halinde veri çözümleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="53a38-124">[Azure Stream Analytics][lnk-asa] provides in-motion data analysis.</span></span> <span data-ttu-id="53a38-125">Bu hizmet tooprocess gelen telemetri IOT paketi kullanır, toplama gerçekleştirmek ve olayları algılamak.</span><span class="sxs-lookup"><span data-stu-id="53a38-125">IoT Suite uses this service tooprocess incoming telemetry, perform aggregation, and detect events.</span></span> <span data-ttu-id="53a38-126">Merhaba önceden yapılandırılmış çözümleri ayrıca aygıtlardan meta veri ya da komut yanıtları gibi verileri içeren stream analytics tooprocess bilgilendirici iletileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="53a38-126">hello preconfigured solutions also use stream analytics tooprocess informational messages that contain data such as metadata or command responses from devices.</span></span> <span data-ttu-id="53a38-127">Hello çözümler cihazlarınızdan gelen akış analizi tooprocess hello iletileri kullanın ve bu iletileri tooother Hizmetleri sunmak.</span><span class="sxs-lookup"><span data-stu-id="53a38-127">hello solutions use Stream Analytics tooprocess hello messages from your devices and deliver those messages tooother services.</span></span>
* <span data-ttu-id="53a38-128">[Azure depolama] [ lnk-azure-storage] ve [Azure Cosmos DB] [ lnk-document-db] hello veri depolama özellikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="53a38-128">[Azure Storage][lnk-azure-storage] and [Azure Cosmos DB][lnk-document-db] provide hello data storage capabilities.</span></span> <span data-ttu-id="53a38-129">Merhaba önceden yapılandırılmış çözümler blob depolama toostore telemetri ve toomake kullanır, çözümleme için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="53a38-129">hello preconfigured solutions use blob storage toostore telemetry and toomake it available for analysis.</span></span> <span data-ttu-id="53a38-130">Merhaba çözümleri hello çözümlerinin hello cihaz Yönetimi işlevlerini etkinleştirmek ve Cosmos DB toostore cihaz meta verilerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="53a38-130">hello solutions use Cosmos DB toostore device metadata and enable hello device management capabilities of hello solutions.</span></span>
* <span data-ttu-id="53a38-131">[Azure Web Apps] [ lnk-web-apps] ve [Microsoft Power BI] [ lnk-power-bi] hello veri görselleştirme özellikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="53a38-131">[Azure Web Apps][lnk-web-apps] and [Microsoft Power BI][lnk-power-bi] provide hello data visualization capabilities.</span></span> <span data-ttu-id="53a38-132">Power BI Hello esnekliğini sağlar tooquickly IOT paketi verilerini kullanan kendi etkileşimli panolar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="53a38-132">hello flexibility of Power BI enables you tooquickly build your own interactive dashboards that use IoT Suite data.</span></span>

<span data-ttu-id="53a38-133">Tipik bir IOT çözüm mimarisini hello genel bakış için bkz: [Microsoft Azure ve nesnelerin interneti (IOT) hello][iot-suite-what-is-azure-iot].</span><span class="sxs-lookup"><span data-stu-id="53a38-133">For an overview of hello architecture of a typical IoT solution, see [Microsoft Azure and hello Internet of Things (IoT)][iot-suite-what-is-azure-iot].</span></span>

## <a name="preconfigured-solutions"></a><span data-ttu-id="53a38-134">Önceden yapılandırılmış çözümler</span><span class="sxs-lookup"><span data-stu-id="53a38-134">Preconfigured solutions</span></span>

<span data-ttu-id="53a38-135">IOT paketi önceden yapılandırılmış çözümler içerir, etkinleştirme, tooquickly ile çalışmaya başlama ve tooexplore gibi yaygın IOT senaryolarını hello:</span><span class="sxs-lookup"><span data-stu-id="53a38-135">IoT Suite includes preconfigured solutions that enable you tooquickly get started with and tooexplore hello common IoT scenarios, such as:</span></span>

* <span data-ttu-id="53a38-136">Uzaktan izleme</span><span class="sxs-lookup"><span data-stu-id="53a38-136">Remote monitoring</span></span>
* <span data-ttu-id="53a38-137">Tahmine dayalı bakım</span><span class="sxs-lookup"><span data-stu-id="53a38-137">Predictive maintenance</span></span>
* <span data-ttu-id="53a38-138">Bağlı fabrika</span><span class="sxs-lookup"><span data-stu-id="53a38-138">Connected factory</span></span>

<span data-ttu-id="53a38-139">Bu çözümleri tooyour Azure aboneliği dağıtın ve ardından tam, uçtan uca bir IOT senaryosu çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53a38-139">You can deploy these solutions tooyour Azure subscription and then run a complete, end-to-end IoT scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53a38-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="53a38-140">Next steps</span></span>

<span data-ttu-id="53a38-141">IOT paketi yapabileceklerine ve temel bileşenlerine nelerdir genel bakış sahip olduğunuza göre IOT paketi önceden yapılandırılmış hello çözümleri hakkında daha fazla bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53a38-141">Now that you have an overview of what IoT Suite can do and what are its main components, you can learn more about hello preconfigured solutions in IoT Suite.</span></span> <span data-ttu-id="53a38-142">Daha fazla bilgi için bkz: [ne hello Azure IOT önceden yapılandırılmış çözümleri?][lnk-what-are-preconfig]</span><span class="sxs-lookup"><span data-stu-id="53a38-142">For more information, see [What are hello Azure IoT preconfigured solutions?][lnk-what-are-preconfig]</span></span>

[lnk-sdks]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-azure-storage]: https://azure.microsoft.com/documentation/services/storage/
[lnk-document-db]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-power-bi]: https://powerbi.microsoft.com/
[lnk-web-apps]: https://azure.microsoft.com/documentation/services/app-service/web/
[iot-suite-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-what-are-preconfig]: iot-suite-what-are-preconfigured-solutions.md
[lnk-device-management]: ../iot-hub/iot-hub-device-management-overview.md
