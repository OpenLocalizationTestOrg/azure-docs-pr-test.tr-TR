---
title: "Azure IOT kenar genel bakış | Microsoft Docs"
description: "Azure IOT kenar ağ geçitleri, modüller ve aracıları gibi anahtar mimari kavramlarını açıklar."
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
ms.openlocfilehash: ecdd56c91a8fc2011b3d7abe93b9d27c1e1e0bef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-edge-architectural-concepts"></a><span data-ttu-id="b8107-103">Azure IOT kenar mimari kavramları</span><span class="sxs-lookup"><span data-stu-id="b8107-103">Azure IoT Edge architectural concepts</span></span>

<span data-ttu-id="b8107-104">Tüm örnek kodu incelemeden veya IOT kenar kullanarak kendi alan ağ geçidi oluşturmadan önce IOT kenar mimarisini destekleyen temel kavramları anlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b8107-104">Before you examine any sample code or create your own field gateway using IoT Edge, you should understand the key concepts that underpin the architecture of IoT Edge.</span></span>

## <a name="iot-edge-modules"></a><span data-ttu-id="b8107-105">IOT kenar modülleri</span><span class="sxs-lookup"><span data-stu-id="b8107-105">IoT Edge modules</span></span>

<span data-ttu-id="b8107-106">Bir ağ geçidi ile Azure IOT sınır oluşturma ve Birleştirme yapı *IOT kenar modülleri*.</span><span class="sxs-lookup"><span data-stu-id="b8107-106">You build a gateway with Azure IoT Edge by creating and assembling *IoT Edge modules*.</span></span> <span data-ttu-id="b8107-107">Modüller birbirileriyle veri alışverişinde bulunmak için *iletileri* kullanır.</span><span class="sxs-lookup"><span data-stu-id="b8107-107">Modules use *messages* to exchange data with each other.</span></span> <span data-ttu-id="b8107-108">Modül bir ileti alır, üzerinde bir işlem yapar, isteğe bağlı olarak onu yeni bir iletiye dönüştürür ve ardından diğer modüllerin işlemesi için yayımlar.</span><span class="sxs-lookup"><span data-stu-id="b8107-108">A module receives a message, performs some action on it, optionally transforms it into a new message, and then publishes it for other modules to process.</span></span> <span data-ttu-id="b8107-109">Bazı modüller yalnızca yeni iletiler oluşturabilir ve hiçbir zaman gelen iletileri işlemez.</span><span class="sxs-lookup"><span data-stu-id="b8107-109">Some modules might only produce new messages and never process incoming messages.</span></span> <span data-ttu-id="b8107-110">Bir modül zinciri, her bir modülün bir noktadaki veriler üzerinde dönüştürme gerçekleştirdiği bir veri işleme işlem hattı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b8107-110">A chain of modules creates a data processing pipeline with each module performing a transformation on the data at one point in that pipeline.</span></span>

![Ağ geçidinde Azure IoT Edge ile oluşturulan modül zinciri][1]

<span data-ttu-id="b8107-112">IOT kenar aşağıdaki bileşenleri içerir:</span><span class="sxs-lookup"><span data-stu-id="b8107-112">IoT Edge contains the following components:</span></span>

* <span data-ttu-id="b8107-113">Ortak ağ geçidi işlevlerini yerine önceden yazılmış modüller.</span><span class="sxs-lookup"><span data-stu-id="b8107-113">Pre-written modules that perform common gateway functions.</span></span>
* <span data-ttu-id="b8107-114">Bir geliştiricinin özel modüller yazmak için kullanabileceği arabirimler.</span><span class="sxs-lookup"><span data-stu-id="b8107-114">The interfaces a developer can use to write custom modules.</span></span>
* <span data-ttu-id="b8107-115">Bir modül kümesini dağıtmak ve çalıştırmak için gereken altyapı.</span><span class="sxs-lookup"><span data-stu-id="b8107-115">The infrastructure necessary to deploy and run a set of modules.</span></span>

<span data-ttu-id="b8107-116">SDK çeşitli işletim sistemleri ve platformlar üzerinde çalışacak ağ geçitleri oluşturmanıza olanak sağlayan bir soyutlama katmanı sağlar.</span><span class="sxs-lookup"><span data-stu-id="b8107-116">The SDK provides an abstraction layer that enables you to build gateways to run on various operating systems and platforms.</span></span>

![Azure IoT Edge özet düzeyi][2]

## <a name="messages"></a><span data-ttu-id="b8107-118">İletiler</span><span class="sxs-lookup"><span data-stu-id="b8107-118">Messages</span></span>

<span data-ttu-id="b8107-119">Birbirlerine ileti gönderen modüllerin düşünülmesi bir ağ geçidinin nasıl çalıştığını kavramsallaştırmanın kolay bir yolu olsa da neler olduğunu doğru şekilde yansıtmaz.</span><span class="sxs-lookup"><span data-stu-id="b8107-119">Although thinking about modules passing messages to each other is a convenient way to conceptualize how a gateway functions, it does not accurately reflect what happens.</span></span> <span data-ttu-id="b8107-120">IOT kenar modüller birbirleri ile iletişim kurmak için bir aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="b8107-120">IoT Edge modules use a broker to communicate with each other.</span></span> <span data-ttu-id="b8107-121">Modüller (veri yolu veya Yayınla/Abone ol gibi Mesajlaşma modelleri kullanarak) aracısı iletileri yayımlamak ve iletiyi kendisine bağlı modülleri yönlendirmek Aracısı olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="b8107-121">Modules publish messages to the broker (using messaging patterns such as bus, or publish/subscribe) and then let the broker route the message to the modules connected to it.</span></span>

<span data-ttu-id="b8107-122">Bir modül, aracıya ileti yayımlamak için **Broker_Publish** işlevini kullanır.</span><span class="sxs-lookup"><span data-stu-id="b8107-122">A module uses the **Broker_Publish** function to publish a message to the broker.</span></span> <span data-ttu-id="b8107-123">Aracı bir geri çağırma işlevini çağırarak iletileri bir modüle teslim eder.</span><span class="sxs-lookup"><span data-stu-id="b8107-123">The broker delivers messages to a module by invoking a callback function.</span></span> <span data-ttu-id="b8107-124">İleti bir dizi anahtar/değer özelliklerinden ve bir bellek bloğu olarak geçirilen içeriklerden oluşur.</span><span class="sxs-lookup"><span data-stu-id="b8107-124">A message consists of a set of key/value properties and content passed as a block of memory.</span></span>

![Azure IoT Edge’de Aracı’nın rolü][3]

## <a name="message-routing-and-filtering"></a><span data-ttu-id="b8107-126">İleti yönlendirme ve filtreleme</span><span class="sxs-lookup"><span data-stu-id="b8107-126">Message routing and filtering</span></span>

<span data-ttu-id="b8107-127">Doğru IOT kenar modülleri iletilerini yönlendirmek için iki yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="b8107-127">There are two ways to direct messages to the correct IoT Edge modules:</span></span>

* <span data-ttu-id="b8107-128">Bağlantılar kümesi geçirebilirsiniz aracı kaynak ve havuz her modül için bilmesi için Aracısı geçirilebilir.</span><span class="sxs-lookup"><span data-stu-id="b8107-128">You can pass a set of links can be passed to the broker so the broker knows the source and sink for each module.</span></span>
* <span data-ttu-id="b8107-129">Bir modül, ileti özelliklerini filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8107-129">A module can filter on the properties of the message.</span></span>

<span data-ttu-id="b8107-130">İleti bu amaca yönelikse modül yalnızca iletiye göre davranmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b8107-130">A module should only act upon a message if the message is intended for it.</span></span> <span data-ttu-id="b8107-131">Bağlantılar ve etkili bir şekilde filtreleme ileti ileti işlem hattını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b8107-131">Links and message filtering effectively create a message pipeline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b8107-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b8107-132">Next steps</span></span>

<span data-ttu-id="b8107-133">Çalıştırabileceğiniz bir örnek uygulanan Bu kavramlar görmek için bkz: [keşfedin Azure IOT kenar mimarisi][lnk-hello-world].</span><span class="sxs-lookup"><span data-stu-id="b8107-133">To see these concepts applied in a sample you can run, see [Explore Azure IoT Edge architecture][lnk-hello-world].</span></span>

<!-- Images -->
[1]: media/iot-hub-iot-edge-overview/modules.png
[2]: media/iot-hub-iot-edge-overview/modules_2.png
[3]: media/iot-hub-iot-edge-overview/messages_1.png

<!-- Links -->
[lnk-hello-world]: ./iot-hub-linux-iot-edge-get-started.md