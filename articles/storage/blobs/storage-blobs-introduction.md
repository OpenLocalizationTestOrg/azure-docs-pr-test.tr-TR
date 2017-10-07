---
title: Blob Depolama aaaIntroduction tooAzure | Microsoft Docs
description: "Giriş tooAzure Blob Depolama"
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
ms.date: 08/17/2017
ms.author: robinsh
ms.openlocfilehash: 3431f826ae51d42dbced084ee60f9ff70a8168d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooblob-storage"></a><span data-ttu-id="51a28-103">Giriş tooBlob depolama</span><span class="sxs-lookup"><span data-stu-id="51a28-103">Introduction tooBlob storage</span></span>

<span data-ttu-id="51a28-104">Azure Blob depolama alanından herhangi bir yere Merhaba Dünya HTTP veya HTTPS üzerinden erişilebilen metin veya ikili veriler gibi yapılandırılmamış nesne verilerini büyük miktarlarda depolamak için bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="51a28-104">Azure Blob storage is a service for storing large amounts of unstructured object data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="51a28-105">Blob Depolama tooexpose verileri kullanabileceğiniz genel olarak toohello world veya toostore uygulama verilerini özel olarak.</span><span class="sxs-lookup"><span data-stu-id="51a28-105">You can use Blob storage tooexpose data publicly toohello world, or toostore application data privately.</span></span>

<span data-ttu-id="51a28-106">Blob Storage’ın yaygın kullanımları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="51a28-106">Common uses of Blob storage include:</span></span>

* <span data-ttu-id="51a28-107">Hizmet görüntüleri veya doğrudan tooa tarayıcı belgeleri</span><span class="sxs-lookup"><span data-stu-id="51a28-107">Serving images or documents directly tooa browser</span></span>
* <span data-ttu-id="51a28-108">Dağıtılan erişim için dosyaların depolanması</span><span class="sxs-lookup"><span data-stu-id="51a28-108">Storing files for distributed access</span></span>
* <span data-ttu-id="51a28-109">Video ve ses akışları</span><span class="sxs-lookup"><span data-stu-id="51a28-109">Streaming video and audio</span></span>
* <span data-ttu-id="51a28-110">Yedekleme ve geri yükleme, olağanüstü durum kurtarma ve arşivleme için verilerin depolanması</span><span class="sxs-lookup"><span data-stu-id="51a28-110">Storing data for backup and restore, disaster recovery, and archiving</span></span>
* <span data-ttu-id="51a28-111">Şirket içi veya Azure barındırılan hizmetle analiz için verilerin depolanması</span><span class="sxs-lookup"><span data-stu-id="51a28-111">Storing data for analysis by an on-premises or Azure-hosted service</span></span>

## <a name="blob-service-concepts"></a><span data-ttu-id="51a28-112">Blob hizmeti kavramları</span><span class="sxs-lookup"><span data-stu-id="51a28-112">Blob service concepts</span></span>

<span data-ttu-id="51a28-113">Merhaba Blob hizmeti hello aşağıdaki bileşenleri içerir:</span><span class="sxs-lookup"><span data-stu-id="51a28-113">hello Blob service contains hello following components:</span></span>

![Blob mimarisi](./media/storage-blobs-introduction/blob1.png)

* <span data-ttu-id="51a28-115">**Depolama hesabı:** üzerinden depolama hesabı tüm erişim tooAzure depolama yapılır.</span><span class="sxs-lookup"><span data-stu-id="51a28-115">**Storage Account:** All access tooAzure Storage is done through a storage account.</span></span> <span data-ttu-id="51a28-116">Bu depolama hesabı olabilir bir **genel amaçlı depolama hesabı** veya **Blob storage hesabı** nesnelerin/blobların depolanması için özelleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="51a28-116">This storage account can be a **General-purpose storage account** or a **Blob storage account** that is specialized for storing objects/blobs.</span></span> <span data-ttu-id="51a28-117">Daha fazla bilgi için bkz. [Azure depolama hesapları hakkında](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="51a28-117">See [About Azure storage accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span>

* <span data-ttu-id="51a28-118">**Kapsayıcı:** Kapsayıcı, bir dizi blobun gruplandırılmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="51a28-118">**Container:** A container provides a grouping of a set of blobs.</span></span> <span data-ttu-id="51a28-119">Tüm bloblar bir kapsayıcıda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="51a28-119">All blobs must be in a container.</span></span> <span data-ttu-id="51a28-120">Bir hesapta sınırsız sayıda kapsayıcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="51a28-120">An account can contain an unlimited number of containers.</span></span> <span data-ttu-id="51a28-121">Kapsayıcıda sınırsız sayıda blob depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="51a28-121">A container can store an unlimited number of blobs.</span></span> <span data-ttu-id="51a28-122">Merhaba kapsayıcı adının küçük harfli olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="51a28-122">Note that hello container name must be lowercase.</span></span>

* <span data-ttu-id="51a28-123">**Blob:** Herhangi bir türde ve boyutta bir dosya.</span><span class="sxs-lookup"><span data-stu-id="51a28-123">**Blob:** A file of any type and size.</span></span> <span data-ttu-id="51a28-124">Azure Storage üç tür blob sunar: blok blobları, sayfa blobları ve ekleme blobları.</span><span class="sxs-lookup"><span data-stu-id="51a28-124">Azure Storage offers three types of blobs: block blobs, page blobs, and append blobs.</span></span>
  
    <span data-ttu-id="51a28-125">*Blok blobları*, belgeler ve medya dosyaları gibi metin veya ikili dosyaların depolanması için idealdir.</span><span class="sxs-lookup"><span data-stu-id="51a28-125">*Block blobs* are ideal for storing text or binary files, such as documents and media files.</span></span> <span data-ttu-id="51a28-126">*Ekleme blobları* olan benzer tooblock BLOB'lar bunlar bloklardan oluşur ancak için iyileştirilmiş da ekleme işlemleri, günlük kaydı senaryoları için yararlı olacak şekilde.</span><span class="sxs-lookup"><span data-stu-id="51a28-126">*Append blobs* are similar tooblock blobs in that they are made up of blocks, but they are optimized for append operations, so they are useful for logging scenarios.</span></span> <span data-ttu-id="51a28-127">Tek bir blok blobu too50, her too100 MB yukarı 000 bloklarını yukarı içerebilir, biraz daha fazladır 4.75 TB (100 MB X 50.000) toplam boyut.</span><span class="sxs-lookup"><span data-stu-id="51a28-127">A single block blob can contain up too50,000 blocks of up too100 MB each, for a total size of slightly more than 4.75 TB (100 MB X 50,000).</span></span> <span data-ttu-id="51a28-128">Tek ek blob too50, her too4 MB yukarı 000 bloklarını yukarı içerebilir toplam boyut 195 GB'den biraz daha büyük (4 MB X 50.000).</span><span class="sxs-lookup"><span data-stu-id="51a28-128">A single append blob can contain up too50,000 blocks of up too4 MB each, for a total size of slightly more than 195 GB (4 MB X 50,000).</span></span>
  
    <span data-ttu-id="51a28-129">*Sayfa blobları* yukarı too1 TB boyutunda olabilir ve sık sık okuma/yazma işlemleri için daha verimlidir.</span><span class="sxs-lookup"><span data-stu-id="51a28-129">*Page blobs* can be up too1 TB in size, and are more efficient for frequent read/write operations.</span></span> <span data-ttu-id="51a28-130">Azure Virtual Machines sayfa bloblarını işletim sistemi ve veri diskleri olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="51a28-130">Azure Virtual Machines uses page blobs as OS and data disks.</span></span>
  
    <span data-ttu-id="51a28-131">Kapsayıcıları ve blobları adlandırma hakkında ayrıntılı bilgi için bkz. [Kapsayıcıları, Blobları ve Meta Verileri Adlandırma ve Bunlara Başvurma](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).</span><span class="sxs-lookup"><span data-stu-id="51a28-131">For details about naming containers and blobs, see [Naming and Referencing Containers, Blobs, and Metadata](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).</span></span>

## <a name="next-steps"></a><span data-ttu-id="51a28-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="51a28-132">Next steps</span></span>

* [<span data-ttu-id="51a28-133">Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="51a28-133">Create a storage account</span></span>](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="51a28-134">.NET kullanarak Blob storage'ı kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="51a28-134">Getting started with Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)