---
title: Kuyruk depolama aaaIntroduction tooAzure | Microsoft Docs
description: "Giriş tooAzure kuyruk depolama"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: robinsh
ms.openlocfilehash: 669effedff7beedde8a119c350a2a70edafedcf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooqueues"></a><span data-ttu-id="dc7c6-103">Giriş tooQueues</span><span class="sxs-lookup"><span data-stu-id="dc7c6-103">Introduction tooQueues</span></span>

<span data-ttu-id="dc7c6-104">Azure kuyruk depolama alanından herhangi bir yere Merhaba Dünya HTTP veya HTTPS kullanarak kimlik doğrulaması yapılmış çağrılar aracılığıyla erişilebilen iletileri çok sayıda depolamak için bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="dc7c6-104">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="dc7c6-105">Tek bir kuyruk iletisinin boyutu too64 KB yukarı olabilir ve bir kuyruk iletileri, bir depolama hesabı toohello toplam kapasite sınırına milyonlarca içerebilir.</span><span class="sxs-lookup"><span data-stu-id="dc7c6-105">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span>

## <a name="common-uses"></a><span data-ttu-id="dc7c6-106">Ortak kullanımlar</span><span class="sxs-lookup"><span data-stu-id="dc7c6-106">Common uses</span></span>

<span data-ttu-id="dc7c6-107">Kuyruk depolamanın yaygın kullanımları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="dc7c6-107">Common uses of Queue storage include:</span></span>

* <span data-ttu-id="dc7c6-108">Zaman uyumsuz olarak biriktirme çalışma tooprocess listesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="dc7c6-108">Creating a backlog of work tooprocess asynchronously</span></span>
* <span data-ttu-id="dc7c6-109">İletileri Azure web rolü tooan Azure çalışan rolüne geçirme</span><span class="sxs-lookup"><span data-stu-id="dc7c6-109">Passing messages from an Azure web role tooan Azure worker role</span></span>

## <a name="queue-service-concepts"></a><span data-ttu-id="dc7c6-110">Kuyruk hizmeti kavramları</span><span class="sxs-lookup"><span data-stu-id="dc7c6-110">Queue service concepts</span></span>

<span data-ttu-id="dc7c6-111">Merhaba sıra hizmeti hello aşağıdaki bileşenleri içerir:</span><span class="sxs-lookup"><span data-stu-id="dc7c6-111">hello Queue service contains hello following components:</span></span>

![Sıra kavramları](./media/storage-queues-introduction/queue1.png)

* <span data-ttu-id="dc7c6-113">**URL biçimi:** sıraları hello şu URL biçimi kullanılarak adreslenebilir:</span><span class="sxs-lookup"><span data-stu-id="dc7c6-113">**URL format:** Queues are addressable using hello following URL format:</span></span>   
    <span data-ttu-id="dc7c6-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span><span class="sxs-lookup"><span data-stu-id="dc7c6-114">http://`<storage account>`.queue.core.windows.net/`<queue>`</span></span> 
  
    <span data-ttu-id="dc7c6-115">URL aşağıdaki hello hello diyagramı kuyrukta ele alır:</span><span class="sxs-lookup"><span data-stu-id="dc7c6-115">hello following URL addresses a queue in hello diagram:</span></span>  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* <span data-ttu-id="dc7c6-116">**Depolama hesabı:** üzerinden depolama hesabı tüm erişim tooAzure depolama yapılır.</span><span class="sxs-lookup"><span data-stu-id="dc7c6-116">**Storage account:** All access tooAzure Storage is done through a storage account.</span></span> <span data-ttu-id="dc7c6-117">Depolama hesabı kapasitesi hakkında ayrıntılı bilgi için bkz. [Azure Storage Ölçeklenebilirlik ve Performans Hedefleri](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dc7c6-117">See [Azure Storage Scalability and Performance Targets](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) for details about storage account capacity.</span></span>

* <span data-ttu-id="dc7c6-118">**Kuyruk:** Kuyrukta bir dizi ileti vardır.</span><span class="sxs-lookup"><span data-stu-id="dc7c6-118">**Queue:** A queue contains a set of messages.</span></span> <span data-ttu-id="dc7c6-119">Tüm iletiler bir kuyrukta olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="dc7c6-119">All messages must be in a queue.</span></span> <span data-ttu-id="dc7c6-120">Bu hello sıra adı tüm küçük harfli olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="dc7c6-120">Note that hello queue name must be all lowercase.</span></span> <span data-ttu-id="dc7c6-121">Kuyrukların adlandırılması hakkında daha fazla bilgi için bkz. [Kuyrukları ve Meta Verileri Adlandırma](https://msdn.microsoft.com/library/azure/dd179349.aspx).</span><span class="sxs-lookup"><span data-stu-id="dc7c6-121">For information on naming queues, see [Naming Queues and Metadata](https://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

* <span data-ttu-id="dc7c6-122">**İleti:** bir ileti görüntülenirse, herhangi bir biçimde too64 KB.</span><span class="sxs-lookup"><span data-stu-id="dc7c6-122">**Message:** A message, in any format, of up too64 KB.</span></span> <span data-ttu-id="dc7c6-123">bir ileti hello kuyrukta kalabileceği en uzun süre hello yedi gündür.</span><span class="sxs-lookup"><span data-stu-id="dc7c6-123">hello maximum time that a message can remain in hello queue is seven days.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc7c6-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dc7c6-124">Next steps</span></span>

* [<span data-ttu-id="dc7c6-125">Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="dc7c6-125">Create a storage account</span></span>](../storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [<span data-ttu-id="dc7c6-126">.NET kullanarak kuyruklarla çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="dc7c6-126">Getting started with Queues using .NET</span></span>](storage-dotnet-how-to-use-queues.md)
