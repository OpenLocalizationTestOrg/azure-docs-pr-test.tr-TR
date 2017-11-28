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
# <a name="azure-iot-edge-architectural-concepts"></a><span data-ttu-id="a4327-103">Azure IOT kenar mimari kavramları</span><span class="sxs-lookup"><span data-stu-id="a4327-103">Azure IoT Edge architectural concepts</span></span>

<span data-ttu-id="a4327-104">Tüm örnek kodu incelemeden veya IOT kenar kullanarak kendi alan ağ geçidi oluşturmadan önce hello IOT kenar hello mimarisini destekleyen temel kavramları anlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a4327-104">Before you examine any sample code or create your own field gateway using IoT Edge, you should understand hello key concepts that underpin hello architecture of IoT Edge.</span></span>

## <a name="iot-edge-modules"></a><span data-ttu-id="a4327-105">IOT kenar modülleri</span><span class="sxs-lookup"><span data-stu-id="a4327-105">IoT Edge modules</span></span>

<span data-ttu-id="a4327-106">Bir ağ geçidi ile Azure IOT sınır oluşturma ve Birleştirme yapı *IOT kenar modülleri*.</span><span class="sxs-lookup"><span data-stu-id="a4327-106">You build a gateway with Azure IoT Edge by creating and assembling *IoT Edge modules*.</span></span> <span data-ttu-id="a4327-107">Modüllerini *iletileri* birbirleriyle tooexchange veri.</span><span class="sxs-lookup"><span data-stu-id="a4327-107">Modules use *messages* tooexchange data with each other.</span></span> <span data-ttu-id="a4327-108">Bir modül bir ileti alır, üzerinde bazı eylemleri gerçekleştirir, isteğe bağlı olarak yeni bir iletiye dönüştürür ve sonra diğer modüller tooprocess için yayımlar.</span><span class="sxs-lookup"><span data-stu-id="a4327-108">A module receives a message, performs some action on it, optionally transforms it into a new message, and then publishes it for other modules tooprocess.</span></span> <span data-ttu-id="a4327-109">Bazı modüller yalnızca yeni iletiler oluşturabilir ve hiçbir zaman gelen iletileri işlemez.</span><span class="sxs-lookup"><span data-stu-id="a4327-109">Some modules might only produce new messages and never process incoming messages.</span></span> <span data-ttu-id="a4327-110">Bir modül zinciri, o ardışık düzeninde bir noktada hello veri dönüştürme gerçekleştiriliyor her modül bir veri işleme işlem hattı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a4327-110">A chain of modules creates a data processing pipeline with each module performing a transformation on hello data at one point in that pipeline.</span></span>

![Ağ geçidinde Azure IoT Edge ile oluşturulan modül zinciri][1]

<span data-ttu-id="a4327-112">IOT kenar hello aşağıdaki bileşenleri içerir:</span><span class="sxs-lookup"><span data-stu-id="a4327-112">IoT Edge contains hello following components:</span></span>

* <span data-ttu-id="a4327-113">Ortak ağ geçidi işlevlerini yerine önceden yazılmış modüller.</span><span class="sxs-lookup"><span data-stu-id="a4327-113">Pre-written modules that perform common gateway functions.</span></span>
* <span data-ttu-id="a4327-114">Geliştirici bir Hello arabirimleri toowrite özel modüller kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4327-114">hello interfaces a developer can use toowrite custom modules.</span></span>
* <span data-ttu-id="a4327-115">Altyapı gerekli toodeploy hello ve bir modül kümesini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a4327-115">hello infrastructure necessary toodeploy and run a set of modules.</span></span>

<span data-ttu-id="a4327-116">Merhaba SDK çeşitli işletim sistemleri ve platformlar üzerinde toobuild ağ geçitleri toorun sağlayan bir soyutlama katmanı sağlar.</span><span class="sxs-lookup"><span data-stu-id="a4327-116">hello SDK provides an abstraction layer that enables you toobuild gateways toorun on various operating systems and platforms.</span></span>

![Azure IoT Edge özet düzeyi][2]

## <a name="messages"></a><span data-ttu-id="a4327-118">İletiler</span><span class="sxs-lookup"><span data-stu-id="a4327-118">Messages</span></span>

<span data-ttu-id="a4327-119">Bir ağ geçidinin nasıl tooeach iletileri diğer uygun şekilde tooconceptualize olan geçirme modüllerine düşünüyorum rağmen bunu doğru şekilde ne olur yansıtmaz.</span><span class="sxs-lookup"><span data-stu-id="a4327-119">Although thinking about modules passing messages tooeach other is a convenient way tooconceptualize how a gateway functions, it does not accurately reflect what happens.</span></span> <span data-ttu-id="a4327-120">IOT kenar modüller birbirleri ile Aracısı toocommunicate kullanın.</span><span class="sxs-lookup"><span data-stu-id="a4327-120">IoT Edge modules use a broker toocommunicate with each other.</span></span> <span data-ttu-id="a4327-121">Modüller (veri yolu veya Yayınla/Abone ol gibi Mesajlaşma modelleri kullanarak) iletileri toohello Aracısı yayımlayın ve hello Aracısı rota hello ileti toohello modülleri bağlı tooit olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="a4327-121">Modules publish messages toohello broker (using messaging patterns such as bus, or publish/subscribe) and then let hello broker route hello message toohello modules connected tooit.</span></span>

<span data-ttu-id="a4327-122">Bir modül hello kullanan **Broker_Publish** toopublish bir ileti toohello Aracısı işlev.</span><span class="sxs-lookup"><span data-stu-id="a4327-122">A module uses hello **Broker_Publish** function toopublish a message toohello broker.</span></span> <span data-ttu-id="a4327-123">Merhaba Aracısı, bir geri çağırma işlevini çağırarak iletileri tooa modülü sunar.</span><span class="sxs-lookup"><span data-stu-id="a4327-123">hello broker delivers messages tooa module by invoking a callback function.</span></span> <span data-ttu-id="a4327-124">İleti bir dizi anahtar/değer özelliklerinden ve bir bellek bloğu olarak geçirilen içeriklerden oluşur.</span><span class="sxs-lookup"><span data-stu-id="a4327-124">A message consists of a set of key/value properties and content passed as a block of memory.</span></span>

![hello Azure IOT kenar Aracısı Hello rolü][3]

## <a name="message-routing-and-filtering"></a><span data-ttu-id="a4327-126">İleti yönlendirme ve filtreleme</span><span class="sxs-lookup"><span data-stu-id="a4327-126">Message routing and filtering</span></span>

<span data-ttu-id="a4327-127">Toodirect iletileri toohello doğru IOT kenar modülleri iki yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="a4327-127">There are two ways toodirect messages toohello correct IoT Edge modules:</span></span>

* <span data-ttu-id="a4327-128">Bağlantılar kümesi geçirebilirsiniz hello Aracısı hello kaynak ve havuz her modül için bilmesi için toohello Aracısı geçirilebilir.</span><span class="sxs-lookup"><span data-stu-id="a4327-128">You can pass a set of links can be passed toohello broker so hello broker knows hello source and sink for each module.</span></span>
* <span data-ttu-id="a4327-129">Bir modül selamlama iletisine hello özelliklerini filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4327-129">A module can filter on hello properties of hello message.</span></span>

<span data-ttu-id="a4327-130">Selamlama iletisine için amaçlanıyorsa bir modülü yalnızca bir ileti üzerinde işlem yapmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a4327-130">A module should only act upon a message if hello message is intended for it.</span></span> <span data-ttu-id="a4327-131">Bağlantılar ve etkili bir şekilde filtreleme ileti ileti işlem hattını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a4327-131">Links and message filtering effectively create a message pipeline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4327-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a4327-132">Next steps</span></span>

<span data-ttu-id="a4327-133">toosee çalıştırabilirsiniz, bir örnek uygulanan bu bkz [keşfedin Azure IOT kenar mimarisi][lnk-hello-world].</span><span class="sxs-lookup"><span data-stu-id="a4327-133">toosee these concepts applied in a sample you can run, see [Explore Azure IoT Edge architecture][lnk-hello-world].</span></span>

<!-- Images -->
[1]: media/iot-hub-iot-edge-overview/modules.png
[2]: media/iot-hub-iot-edge-overview/modules_2.png
[3]: media/iot-hub-iot-edge-overview/messages_1.png

<!-- Links -->
[lnk-hello-world]: ./iot-hub-linux-iot-edge-get-started.md