---
title: "Azure Blob Depolama giriş | Microsoft Docs"
description: "Azure Blob Depolama giriş"
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
ms.openlocfilehash: 051f1b37eab254d4ab4f806166ac8d0b8cab944d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-blob-storage"></a><span data-ttu-id="73a63-103">Blob Storage'a giriş</span><span class="sxs-lookup"><span data-stu-id="73a63-103">Introduction to Blob storage</span></span>

<span data-ttu-id="73a63-104">Azure Blob Storage; HTTP veya HTTPS aracılığıyla dünyanın her yerinde erişilebilen metin veya ikili veriler gibi büyük miktarda yapılandırılmamış nesne verilerinin depolanması için bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="73a63-104">Azure Blob storage is a service for storing large amounts of unstructured object data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="73a63-105">Verileri genel olarak herkese açık kullanıma sunmak veya uygulama verilerini özel olarak depolamak için Blob Storage’ı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="73a63-105">You can use Blob storage to expose data publicly to the world, or to store application data privately.</span></span>

<span data-ttu-id="73a63-106">Blob Storage’ın yaygın kullanımları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="73a63-106">Common uses of Blob storage include:</span></span>

* <span data-ttu-id="73a63-107">Görüntülerin veya belgelerin doğrudan bir tarayıcıya sunulması</span><span class="sxs-lookup"><span data-stu-id="73a63-107">Serving images or documents directly to a browser</span></span>
* <span data-ttu-id="73a63-108">Dağıtılan erişim için dosyaların depolanması</span><span class="sxs-lookup"><span data-stu-id="73a63-108">Storing files for distributed access</span></span>
* <span data-ttu-id="73a63-109">Video ve ses akışları</span><span class="sxs-lookup"><span data-stu-id="73a63-109">Streaming video and audio</span></span>
* <span data-ttu-id="73a63-110">Yedekleme ve geri yükleme, olağanüstü durum kurtarma ve arşivleme için verilerin depolanması</span><span class="sxs-lookup"><span data-stu-id="73a63-110">Storing data for backup and restore, disaster recovery, and archiving</span></span>
* <span data-ttu-id="73a63-111">Şirket içi veya Azure barındırılan hizmetle analiz için verilerin depolanması</span><span class="sxs-lookup"><span data-stu-id="73a63-111">Storing data for analysis by an on-premises or Azure-hosted service</span></span>

## <a name="blob-service-concepts"></a><span data-ttu-id="73a63-112">Blob hizmeti kavramları</span><span class="sxs-lookup"><span data-stu-id="73a63-112">Blob service concepts</span></span>

<span data-ttu-id="73a63-113">Blob hizmetinde şu bileşenler bulunur:</span><span class="sxs-lookup"><span data-stu-id="73a63-113">The Blob service contains the following components:</span></span>

![Blob mimarisi](./media/storage-blobs-introduction/blob1.png)

* <span data-ttu-id="73a63-115">**Depolama Hesabı:** Tüm Azure Storage erişimi bir depolama hesabıyla yapılır.</span><span class="sxs-lookup"><span data-stu-id="73a63-115">**Storage Account:** All access to Azure Storage is done through a storage account.</span></span> <span data-ttu-id="73a63-116">Bu depolama hesabı olabilir bir **genel amaçlı depolama hesabı** veya **Blob storage hesabı** nesnelerin/blobların depolanması için özelleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="73a63-116">This storage account can be a **General-purpose storage account** or a **Blob storage account** that is specialized for storing objects/blobs.</span></span> <span data-ttu-id="73a63-117">Daha fazla bilgi için bkz. [Azure depolama hesapları hakkında](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="73a63-117">See [About Azure storage accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span>

* <span data-ttu-id="73a63-118">**Kapsayıcı:** Kapsayıcı, bir dizi blobun gruplandırılmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="73a63-118">**Container:** A container provides a grouping of a set of blobs.</span></span> <span data-ttu-id="73a63-119">Tüm bloblar bir kapsayıcıda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="73a63-119">All blobs must be in a container.</span></span> <span data-ttu-id="73a63-120">Bir hesapta sınırsız sayıda kapsayıcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="73a63-120">An account can contain an unlimited number of containers.</span></span> <span data-ttu-id="73a63-121">Kapsayıcıda sınırsız sayıda blob depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="73a63-121">A container can store an unlimited number of blobs.</span></span> <span data-ttu-id="73a63-122">Kapsayıcı adındaki harflerin küçük harf olması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="73a63-122">Note that the container name must be lowercase.</span></span>

* <span data-ttu-id="73a63-123">**Blob:** Herhangi bir türde ve boyutta bir dosya.</span><span class="sxs-lookup"><span data-stu-id="73a63-123">**Blob:** A file of any type and size.</span></span> <span data-ttu-id="73a63-124">Azure Storage üç tür blob sunar: blok blobları, sayfa blobları ve ekleme blobları.</span><span class="sxs-lookup"><span data-stu-id="73a63-124">Azure Storage offers three types of blobs: block blobs, page blobs, and append blobs.</span></span>
  
    <span data-ttu-id="73a63-125">*Blok blobları*, belgeler ve medya dosyaları gibi metin veya ikili dosyaların depolanması için idealdir.</span><span class="sxs-lookup"><span data-stu-id="73a63-125">*Block blobs* are ideal for storing text or binary files, such as documents and media files.</span></span> <span data-ttu-id="73a63-126">*Ekleme blobları* blok bloblarına benzer; bloklardan oluşturulmuş olsalar da ekleme işlemleri için iyileştirilmişlerdir; bu nedenle, günlük kaydı senaryoları için kullanışlıdırlar.</span><span class="sxs-lookup"><span data-stu-id="73a63-126">*Append blobs* are similar to block blobs in that they are made up of blocks, but they are optimized for append operations, so they are useful for logging scenarios.</span></span> <span data-ttu-id="73a63-127">Tek bir blok blobu, her birinin büyüklüğü 100 MB’a kadar olabilen 50.000 blok içerebilir; toplam boyut 4,75 TB'tan biraz fazladır (100 MB X 50.000).</span><span class="sxs-lookup"><span data-stu-id="73a63-127">A single block blob can contain up to 50,000 blocks of up to 100 MB each, for a total size of slightly more than 4.75 TB (100 MB X 50,000).</span></span> <span data-ttu-id="73a63-128">Tek bir ekleme blobu, her birinin büyüklüğü 4 MB’a kadar olabilen 50.000 blok içerebilir; toplam boyut 195 GB'tan biraz fazladır (4 MB X 50.000).</span><span class="sxs-lookup"><span data-stu-id="73a63-128">A single append blob can contain up to 50,000 blocks of up to 4 MB each, for a total size of slightly more than 195 GB (4 MB X 50,000).</span></span>
  
    <span data-ttu-id="73a63-129">*Sayfa blobları* boyut olarak 1 TB'ye kadar olabilir; sık gerçekleştirilen okuma/yazma işlemleri için daha verimlidir.</span><span class="sxs-lookup"><span data-stu-id="73a63-129">*Page blobs* can be up to 1 TB in size, and are more efficient for frequent read/write operations.</span></span> <span data-ttu-id="73a63-130">Azure Virtual Machines sayfa bloblarını işletim sistemi ve veri diskleri olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="73a63-130">Azure Virtual Machines uses page blobs as OS and data disks.</span></span>
  
    <span data-ttu-id="73a63-131">Kapsayıcıları ve blobları adlandırma hakkında ayrıntılı bilgi için bkz. [Kapsayıcıları, Blobları ve Meta Verileri Adlandırma ve Bunlara Başvurma](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).</span><span class="sxs-lookup"><span data-stu-id="73a63-131">For details about naming containers and blobs, see [Naming and Referencing Containers, Blobs, and Metadata](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).</span></span>

## <a name="next-steps"></a><span data-ttu-id="73a63-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="73a63-132">Next steps</span></span>

* [<span data-ttu-id="73a63-133">Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="73a63-133">Create a storage account</span></span>](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="73a63-134">.NET kullanarak Blob storage'ı kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="73a63-134">Getting started with Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)