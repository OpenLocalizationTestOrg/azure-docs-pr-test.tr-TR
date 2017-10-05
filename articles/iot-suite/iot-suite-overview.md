---
title: "Microsoft Azure IoT Paketi’ne genel bakış | Microsoft Docs"
description: "Azure IoT Paketi, verileri toplamak, çözümlemek ve depolamak, görselleştirmeler sağlamak ve diğer sistemlerle tümleştirmek için önceden yapılandırılmış nesnelerin internetini nasıl sağladığına genel bakış."
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
ms.openlocfilehash: bfa8dbbd0b1d943a9eb7a042df0bac25189d9ac9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-azure-iot-suite"></a><span data-ttu-id="bb636-103">Azure IoT Paketi’ne Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="bb636-103">Overview of Azure IoT Suite</span></span>

<span data-ttu-id="bb636-104">Azure nesnelerin interneti (IoT) hizmetleri çok çeşitli özellikler sunar.</span><span class="sxs-lookup"><span data-stu-id="bb636-104">The Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="bb636-105">Bu kurumsal sınıf hizmetler şunları yapmanızı sağlar:</span><span class="sxs-lookup"><span data-stu-id="bb636-105">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="bb636-106">Cihazlardan veri toplama</span><span class="sxs-lookup"><span data-stu-id="bb636-106">Collect data from devices</span></span>
* <span data-ttu-id="bb636-107">Hareket halinde veri akışı çözümleme</span><span class="sxs-lookup"><span data-stu-id="bb636-107">Analyze data streams in-motion</span></span>
* <span data-ttu-id="bb636-108">Büyük veri gruplarını depolama ve sorgulama</span><span class="sxs-lookup"><span data-stu-id="bb636-108">Store and query large data sets</span></span>
* <span data-ttu-id="bb636-109">Gerçek zamanlı ve geçmiş verileri görselleştirme</span><span class="sxs-lookup"><span data-stu-id="bb636-109">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="bb636-110">Arka ofis sistemleriyle tümleştirme</span><span class="sxs-lookup"><span data-stu-id="bb636-110">Integrate with back-office systems</span></span>
* <span data-ttu-id="bb636-111">Cihazlarınızı yönetme</span><span class="sxs-lookup"><span data-stu-id="bb636-111">Manage your devices</span></span>

<span data-ttu-id="bb636-112">Bu özellikleri sunmak için, Azure IoT Paketi birçok Azure hizmetini özel uzantılarla birlikte *önceden yapılandırılmış çözümler* olarak paketledi.</span><span class="sxs-lookup"><span data-stu-id="bb636-112">To deliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as *preconfigured solutions*.</span></span> <span data-ttu-id="bb636-113">Bu önceden yapılandırılmış çözümler, IoT çözümlerinizi sunmak için geçirmeniz gereken süreyi azaltmak üzere genel IoT çözümü düzenlerinin temel uygulamalarıdır.</span><span class="sxs-lookup"><span data-stu-id="bb636-113">These preconfigured solutions are base implementations of common IoT solution patterns that help to reduce the time you take to deliver your IoT solutions.</span></span> <span data-ttu-id="bb636-114">[IoT yazılım geliştirme setlerini][lnk-sdks] kullanarak, kendi gereksinimlerinizi karşılamak için bu çözümleri özelleştirebilir ve genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb636-114">Using the [IoT software development kits][lnk-sdks], you can customize and extend these solutions to meet your own requirements.</span></span> <span data-ttu-id="bb636-115">Ayrıca bu çözümleri, yeni IoT çözümleri geliştirirken örnekler ya da şablonlar olarak da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb636-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="bb636-116">Aşağıdaki video Azure IoT paketine giriş sağlar:</span><span class="sxs-lookup"><span data-stu-id="bb636-116">The following video provides an introduction to Azure IoT Suite:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON309/player]
> 
> 

## <a name="azure-iot-services-in-azure-iot-suite"></a><span data-ttu-id="bb636-117">Azure IoT Paketindeki Azure IoT Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="bb636-117">Azure IoT services in Azure IoT Suite</span></span>
<span data-ttu-id="bb636-118">Önceden yapılandırılmış çözümler genellikle aşağıdaki hizmetleri kullanır:</span><span class="sxs-lookup"><span data-stu-id="bb636-118">The preconfigured solutions typically use the following services:</span></span>

* <span data-ttu-id="bb636-119">Azure IoT paketinin çekirdeği [Azure IoT Hub][lnk-iot-hub] hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="bb636-119">Core to Azure IoT Suite is the [Azure IoT Hub][lnk-iot-hub] service.</span></span> <span data-ttu-id="bb636-120">Bu hizmet cihaz-bulut arası ve bulut-cihaz arası ileti gönderme özellikleri sağlar ve buluta ve diğer temel IoT Paketi hizmetlerine ağ geçidi görevi görür.</span><span class="sxs-lookup"><span data-stu-id="bb636-120">This service provides the device-to-cloud and cloud-to-device messaging capabilities and acts as the gateway to the cloud and the other key IoT Suite services.</span></span> <span data-ttu-id="bb636-121">Hizmet cihazınızdan ölçekte mesajlar almanızı ve cihazlarınıza komutlar göndermenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="bb636-121">The service enables you to receive messages from your devices at scale, and send commands to your devices.</span></span> <span data-ttu-id="bb636-122">Hizmet ayrıca [cihazlarınızı yönetmenizi][lnk-device-management] de sağlar.</span><span class="sxs-lookup"><span data-stu-id="bb636-122">The service also enables you to [manage your devices][lnk-device-management].</span></span> <span data-ttu-id="bb636-123">Örneğin hub'a bağlı bir veya daha fazla cihazı yapılandırabilir, yeniden başlatabilir veya fabrika ayarlarına döndürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb636-123">For example, you can configure, reboot, or perform a factory reset on one or more devices connected to the hub.</span></span>
* <span data-ttu-id="bb636-124">[Azure Stream Analytics][lnk-asa] hareket halinde veri çözümleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="bb636-124">[Azure Stream Analytics][lnk-asa] provides in-motion data analysis.</span></span> <span data-ttu-id="bb636-125">IoT Paketi, gelen telemetri işlemek, toplama gerçekleştirmek ve olayları algılamak için bu hizmeti kullanır.</span><span class="sxs-lookup"><span data-stu-id="bb636-125">IoT Suite uses this service to process incoming telemetry, perform aggregation, and detect events.</span></span> <span data-ttu-id="bb636-126">Önceden yapılandırılmış çözümler, meta veriler ya da cihazlardan alınan komut yanıtları gibi verileri içeren bilgi iletilerini işlemek için de akış analizini kullanır.</span><span class="sxs-lookup"><span data-stu-id="bb636-126">The preconfigured solutions also use stream analytics to process informational messages that contain data such as metadata or command responses from devices.</span></span> <span data-ttu-id="bb636-127">Çözümler cihazlarınızdan gelen iletileri işlemek ve bu iletileri diğer cihazlara göndermek için Stream Analytics kullanır.</span><span class="sxs-lookup"><span data-stu-id="bb636-127">The solutions use Stream Analytics to process the messages from your devices and deliver those messages to other services.</span></span>
* <span data-ttu-id="bb636-128">[Azure Depolama][lnk-azure-storage] ve [Azure Cosmos DB][lnk-document-db] veri depolama özellikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="bb636-128">[Azure Storage][lnk-azure-storage] and [Azure Cosmos DB][lnk-document-db] provide the data storage capabilities.</span></span> <span data-ttu-id="bb636-129">Önceden yapılandırılmış çözümler, telemetri depolamak ve çözümleme için kullanılabilir hale getirmek üzere blob depolamayı kullanır.</span><span class="sxs-lookup"><span data-stu-id="bb636-129">The preconfigured solutions use blob storage to store telemetry and to make it available for analysis.</span></span> <span data-ttu-id="bb636-130">Çözümler cihaz meta verilerini depolamak ve çözümlerin cihaz yönetimi özelliklerini etkinleştirmek için Cosmos DB kullanır.</span><span class="sxs-lookup"><span data-stu-id="bb636-130">The solutions use Cosmos DB to store device metadata and enable the device management capabilities of the solutions.</span></span>
* <span data-ttu-id="bb636-131">[Azure Web Apps][lnk-web-apps] ve [Microsoft Power BI][lnk-power-bi] veri görselleştirme özellikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="bb636-131">[Azure Web Apps][lnk-web-apps] and [Microsoft Power BI][lnk-power-bi] provide the data visualization capabilities.</span></span> <span data-ttu-id="bb636-132">Power BI esnekliği, IoT Paketi verilerini kullanan kendi etkileşimli panolarınızı hızlı bir şekilde oluşturmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="bb636-132">The flexibility of Power BI enables you to quickly build your own interactive dashboards that use IoT Suite data.</span></span>

<span data-ttu-id="bb636-133">Tipik bir IoT çözüm mimarisine genel bakış için bkz. [Microsoft Azure ve Nesnelerin İnterneti (IoT)][iot-suite-what-is-azure-iot].</span><span class="sxs-lookup"><span data-stu-id="bb636-133">For an overview of the architecture of a typical IoT solution, see [Microsoft Azure and the Internet of Things (IoT)][iot-suite-what-is-azure-iot].</span></span>

## <a name="preconfigured-solutions"></a><span data-ttu-id="bb636-134">Önceden yapılandırılmış çözümler</span><span class="sxs-lookup"><span data-stu-id="bb636-134">Preconfigured solutions</span></span>

<span data-ttu-id="bb636-135">IoT paketi, yaygın IoT senaryolarını hızlı şekilde kullanmaya başlamanızı ve keşfetmenizi sağlayan aşağıdaki gibi önceden yapılandırılmış çözümler sunar:</span><span class="sxs-lookup"><span data-stu-id="bb636-135">IoT Suite includes preconfigured solutions that enable you to quickly get started with and to explore the common IoT scenarios, such as:</span></span>

* <span data-ttu-id="bb636-136">Uzaktan izleme</span><span class="sxs-lookup"><span data-stu-id="bb636-136">Remote monitoring</span></span>
* <span data-ttu-id="bb636-137">Tahmine dayalı bakım</span><span class="sxs-lookup"><span data-stu-id="bb636-137">Predictive maintenance</span></span>
* <span data-ttu-id="bb636-138">Bağlı fabrika</span><span class="sxs-lookup"><span data-stu-id="bb636-138">Connected factory</span></span>

<span data-ttu-id="bb636-139">Bu çözümleri Azure aboneliğinize dağıtabilir ve ardından tam, uçtan uca bir IoT senaryosu çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb636-139">You can deploy these solutions to your Azure subscription and then run a complete, end-to-end IoT scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb636-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bb636-140">Next steps</span></span>

<span data-ttu-id="bb636-141">IoT Paketi'nin yapabileceklerini ve ana bileşenlerini genel hatlarıyla gördüğünüze göre IoT Paketi'ndeki önceden yapılandırılmış çözümler hakkında daha fazla bilgi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb636-141">Now that you have an overview of what IoT Suite can do and what are its main components, you can learn more about the preconfigured solutions in IoT Suite.</span></span> <span data-ttu-id="bb636-142">Daha fazla bilgi için bkz. [Önceden yapılandırılmış Azure IoT çözümleri nelerdir?][lnk-what-are-preconfig]</span><span class="sxs-lookup"><span data-stu-id="bb636-142">For more information, see [What are the Azure IoT preconfigured solutions?][lnk-what-are-preconfig]</span></span>

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
