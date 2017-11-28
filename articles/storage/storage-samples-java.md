---
title: "Java kullanarak azure depolama örnekleri | Microsoft Docs"
description: "Görüntülemek, indirin ve örnek kod ve uygulamaları için Azure Storage çalıştırın. BLOB, kuyruklar, tablolar ve dosyaları için Java depolama istemcisi kitaplıklarını kullanarak örnek Başlarken bulur."
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 01/12/2017
ms.author: seguler
ms.openlocfilehash: 98e6022062b4ef5b5c71b54a0e94775b925d216b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-storage-samples-using-java"></a><span data-ttu-id="c0416-104">Java kullanarak azure depolama örnekleri</span><span class="sxs-lookup"><span data-stu-id="c0416-104">Azure Storage samples using Java</span></span>

## <a name="java-sample-index"></a><span data-ttu-id="c0416-105">Java örnek dizini</span><span class="sxs-lookup"><span data-stu-id="c0416-105">Java sample index</span></span>

<span data-ttu-id="c0416-106">Aşağıdaki tabloda bizim örnek depo ve her örnek kapsamdaki senaryolar genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="c0416-106">The following table provides an overview of our samples repository and the scenarios covered in each sample.</span></span> <span data-ttu-id="c0416-107">Github'da karşılık gelen örnek kod görüntülemek için bağlantıları tıklatın.</span><span class="sxs-lookup"><span data-stu-id="c0416-107">Click on the links to view the corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="c0416-108">Uç Nokta</span><span class="sxs-lookup"><span data-stu-id="c0416-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="c0416-109">Senaryo</span><span class="sxs-lookup"><span data-stu-id="c0416-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="c0416-110">Örnek kod</span><span class="sxs-lookup"><span data-stu-id="c0416-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="c0416-111"><b>BLOB</b></span><span class="sxs-lookup"><span data-stu-id="c0416-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="c0416-112">BLOB ekleme</span><span class="sxs-lookup"><span data-stu-id="c0416-112">Append Blob</span></span></td> 
<td><span data-ttu-id="c0416-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java'da Azure Blob hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c0416-114">Blok blobu</span><span class="sxs-lookup"><span data-stu-id="c0416-114">Block Blob</span></span></td>
<td><span data-ttu-id="c0416-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java'da Azure Blob hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="c0416-116">İstemci Tarafında Şifreleme</span><span class="sxs-lookup"><span data-stu-id="c0416-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="c0416-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Java'da Azure istemci tarafı şifreleme ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Getting Started with Azure Client Side Encryption in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="c0416-118">BLOB kopyalama</span><span class="sxs-lookup"><span data-stu-id="c0416-118">Copy Blob</span></span></td>
<td><span data-ttu-id="c0416-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java'da Azure Blob hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="c0416-120">Kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c0416-120">Create Container</span></span></td>
<td><span data-ttu-id="c0416-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java'da Azure Blob hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="c0416-122">BLOB Sil</span><span class="sxs-lookup"><span data-stu-id="c0416-122">Delete Blob</span></span></td>
<td><span data-ttu-id="c0416-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java'da Azure Blob hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="c0416-124">Kapsayıcısını silmek</span><span class="sxs-lookup"><span data-stu-id="c0416-124">Delete Container</span></span></td>
<td><span data-ttu-id="c0416-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java'da Azure Blob hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="c0416-126">BLOB meta verileri/özellikler/Stats</span><span class="sxs-lookup"><span data-stu-id="c0416-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="c0416-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Java'da Azure Blob hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="c0416-128">Kapsayıcı ACL/meta veri/özellikleri</span><span class="sxs-lookup"><span data-stu-id="c0416-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="c0416-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Java'da Azure Blob hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="c0416-130">Sayfa aralıklarını alma</span><span class="sxs-lookup"><span data-stu-id="c0416-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="c0416-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Örnek sayfa blobu testleri</a></span><span class="sxs-lookup"><span data-stu-id="c0416-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Page Blob Tests Sample</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="c0416-132">Kira Blob/kapsayıcısı</span><span class="sxs-lookup"><span data-stu-id="c0416-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="c0416-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java'da Azure Blob hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="c0416-134">Liste Blob/kapsayıcısı</span><span class="sxs-lookup"><span data-stu-id="c0416-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="c0416-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java'da Azure Blob hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="c0416-136">Sayfa blobu</span><span class="sxs-lookup"><span data-stu-id="c0416-136">Page Blob</span></span></td>
<td><span data-ttu-id="c0416-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java'da Azure Blob hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="c0416-138">SAS</span><span class="sxs-lookup"><span data-stu-id="c0416-138">SAS</span></span></td>
<td><span data-ttu-id="c0416-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">SAS testleri örnek</a></span><span class="sxs-lookup"><span data-stu-id="c0416-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">SAS Tests Sample</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="c0416-140">Hizmet Özellikleri</span><span class="sxs-lookup"><span data-stu-id="c0416-140">Service Properties</span></span></td>
<td><span data-ttu-id="c0416-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Java'da Azure Blob hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="c0416-142">Anlık görüntü Blob</span><span class="sxs-lookup"><span data-stu-id="c0416-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="c0416-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java'da Azure Blob hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="c0416-144"><b>Dosya</b></span><span class="sxs-lookup"><span data-stu-id="c0416-144"><b>File</b></span></span></td>
<td><span data-ttu-id="c0416-145">Dizinleri/paylaşımları/dosyaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="c0416-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="c0416-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java'da Azure dosya hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="c0416-147">Dizinleri/paylaşımları/dosyaları silin</span><span class="sxs-lookup"><span data-stu-id="c0416-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="c0416-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java'da Azure dosya hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c0416-149">Dizin özellikleri/meta veri</span><span class="sxs-lookup"><span data-stu-id="c0416-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="c0416-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Java'da Azure dosya hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c0416-151">Dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="c0416-151">Download Files</span></span></td> 
<td><span data-ttu-id="c0416-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java'da Azure dosya hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c0416-153">Dosya özellikleri/meta veri/ölçümleri</span><span class="sxs-lookup"><span data-stu-id="c0416-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="c0416-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Java'da Azure dosya hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c0416-155">Dosya hizmeti özellikleri</span><span class="sxs-lookup"><span data-stu-id="c0416-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="c0416-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Java'da Azure dosya hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c0416-157">Liste dizinler ve dosyalar</span><span class="sxs-lookup"><span data-stu-id="c0416-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="c0416-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java'da Azure dosya hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="c0416-159">Paylaşımları</span><span class="sxs-lookup"><span data-stu-id="c0416-159">List Shares</span></span></td> 
<td><span data-ttu-id="c0416-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java'da Azure dosya hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="c0416-161">Meta veri/özellikler/Stats paylaşma</span><span class="sxs-lookup"><span data-stu-id="c0416-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="c0416-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Java'da Azure dosya hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="c0416-163"><b>Sırası</b></span><span class="sxs-lookup"><span data-stu-id="c0416-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="c0416-164">Mesaj ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c0416-164">Add Message</span></span></td> 
<td><span data-ttu-id="c0416-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Depolama Java istemci kitaplığı örnekleri</a></span><span class="sxs-lookup"><span data-stu-id="c0416-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c0416-166">İstemci Tarafında Şifreleme</span><span class="sxs-lookup"><span data-stu-id="c0416-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="c0416-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Depolama Java istemci kitaplığı örnekleri</a></span><span class="sxs-lookup"><span data-stu-id="c0416-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c0416-168">Sıra oluşturma</span><span class="sxs-lookup"><span data-stu-id="c0416-168">Create Queues</span></span></td> 
<td><span data-ttu-id="c0416-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Java'da Azure kuyruk hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c0416-170">İleti/kuyruk silme</span><span class="sxs-lookup"><span data-stu-id="c0416-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="c0416-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Java'da Azure kuyruk hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c0416-172">İletiye Gözat</span><span class="sxs-lookup"><span data-stu-id="c0416-172">Peek Message</span></span></td> 
<td><span data-ttu-id="c0416-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Java'da Azure kuyruk hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c0416-174">Sıra ACL/meta veri/Stats</span><span class="sxs-lookup"><span data-stu-id="c0416-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="c0416-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Java'da Azure kuyruk hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c0416-176">Kuyruk hizmeti özellikleri</span><span class="sxs-lookup"><span data-stu-id="c0416-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="c0416-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Java'da Azure kuyruk hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c0416-178">Güncelleştirme iletisi</span><span class="sxs-lookup"><span data-stu-id="c0416-178">Update Message</span></span></td> 
<td><span data-ttu-id="c0416-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Java'da Azure kuyruk hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="c0416-180"><b>Tablo</b></span><span class="sxs-lookup"><span data-stu-id="c0416-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="c0416-181">Tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="c0416-181">Create Table</span></span></td> 
<td><span data-ttu-id="c0416-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Java'da Azure tablo hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c0416-183">Varlık/tablo silme</span><span class="sxs-lookup"><span data-stu-id="c0416-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="c0416-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Java'da Azure tablo hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c0416-185">Birleştirme/Ekle/Değiştir varlık</span><span class="sxs-lookup"><span data-stu-id="c0416-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="c0416-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Depolama Java istemci kitaplığı örnekleri</a></span><span class="sxs-lookup"><span data-stu-id="c0416-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c0416-187">Sorgu varlıklar</span><span class="sxs-lookup"><span data-stu-id="c0416-187">Query Entities</span></span></td> 
<td><span data-ttu-id="c0416-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Java'da Azure tablo hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c0416-189">Sorgu tabloları</span><span class="sxs-lookup"><span data-stu-id="c0416-189">Query Tables</span></span></td> 
<td><span data-ttu-id="c0416-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Java'da Azure tablo hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c0416-191">Tablo ACL/özellikleri</span><span class="sxs-lookup"><span data-stu-id="c0416-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="c0416-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Java'da Azure tablo hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="c0416-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="c0416-193">Varlık güncelleştir</span><span class="sxs-lookup"><span data-stu-id="c0416-193">Update Entity</span></span></td> 
<td><span data-ttu-id="c0416-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Depolama Java istemci kitaplığı örnekleri</a></span><span class="sxs-lookup"><span data-stu-id="c0416-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="c0416-195">Azure Kod Örnekleri Kitaplığı</span><span class="sxs-lookup"><span data-stu-id="c0416-195">Azure Code Samples library</span></span>

<span data-ttu-id="c0416-196">Tam örnek kitaplığını görüntülemek için Git [Azure Kod örnekleri](https://azure.microsoft.com/resources/samples/?service=storage) Azure Storage için karşıdan yükle ve yerel olarak çalıştırılan örnekleri içeren kitaplık.</span><span class="sxs-lookup"><span data-stu-id="c0416-196">To view the complete sample library, go to the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="c0416-197">Kod örneği kitaplığı .zip biçimi örnek kodda sağlar.</span><span class="sxs-lookup"><span data-stu-id="c0416-197">The Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="c0416-198">Alternatif olarak, bulun ve her bir örnek için GitHub deposunu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="c0416-198">Alternatively, you can browse and clone the GitHub repository for each sample.</span></span>

[!INCLUDE [storage-java-samples-include](../../includes/storage-java-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="c0416-199">Başlarken kılavuzları alma</span><span class="sxs-lookup"><span data-stu-id="c0416-199">Getting started guides</span></span>

<span data-ttu-id="c0416-200">Yükleyin ve Azure Storage istemcisi kitaplıklarını ile çalışmaya başlama hakkında yönergeler arıyorsanız aşağıdaki kılavuzlara denetleyin.</span><span class="sxs-lookup"><span data-stu-id="c0416-200">Check out the following guides if you are looking for instructions on how to install and get started with the Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="c0416-201">Java'da Azure Blob hizmeti ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="c0416-201">Getting Started with Azure Blob Service in Java</span></span>](storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="c0416-202">Java'da Azure kuyruk hizmeti ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="c0416-202">Getting Started with Azure Queue Service in Java</span></span>](storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="c0416-203">Java'da Azure tablo hizmeti ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="c0416-203">Getting Started with Azure Table Service in Java</span></span>](storage-java-how-to-use-table-storage.md)
* [<span data-ttu-id="c0416-204">Java'da Azure dosya hizmeti ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="c0416-204">Getting Started with Azure File Service in Java</span></span>](storage-java-how-to-use-file-storage.md)

## <a name="next-steps"></a><span data-ttu-id="c0416-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c0416-205">Next steps</span></span>

<span data-ttu-id="c0416-206">Diğer diller için örnekleri hakkında daha fazla bilgi için:</span><span class="sxs-lookup"><span data-stu-id="c0416-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="c0416-207">.NET: [.NET kullanarak azure Storage örnekleri](storage-samples-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="c0416-207">.NET: [Azure Storage samples using .NET](storage-samples-dotnet.md)</span></span>
* <span data-ttu-id="c0416-208">Tüm diğer dillere: [Azure Storage örnekleri](storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="c0416-208">All other languages: [Azure Storage samples](storage-samples.md)</span></span>
