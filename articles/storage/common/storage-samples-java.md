---
title: "Java kullanarak aaaAzure depolama örnekleri | Microsoft Docs"
description: "Görüntülemek, indirin ve örnek kod ve uygulamaları için Azure Storage çalıştırın. BLOB, kuyruklar, tablolar ve dosyaları için örnek hello Java depolama istemcisi kitaplıklarını kullanarak Başlarken bulur."
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
ms.openlocfilehash: 6aec326cbfedc1166fc61037ac39d33c15d28d2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-samples-using-java"></a><span data-ttu-id="031f2-104">Java kullanarak azure depolama örnekleri</span><span class="sxs-lookup"><span data-stu-id="031f2-104">Azure Storage samples using Java</span></span>

## <a name="java-sample-index"></a><span data-ttu-id="031f2-105">Java örnek dizini</span><span class="sxs-lookup"><span data-stu-id="031f2-105">Java sample index</span></span>

<span data-ttu-id="031f2-106">Merhaba aşağıdaki tabloda örneklerimizi genel bir bakış depo ve hello senaryolar sağlar her örnek kapsamdaki.</span><span class="sxs-lookup"><span data-stu-id="031f2-106">hello following table provides an overview of our samples repository and hello scenarios covered in each sample.</span></span> <span data-ttu-id="031f2-107">Merhaba bağlantılar tooview hello karşılık gelen örnek kod github'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="031f2-107">Click on hello links tooview hello corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="031f2-108">Uç Nokta</span><span class="sxs-lookup"><span data-stu-id="031f2-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="031f2-109">Senaryo</span><span class="sxs-lookup"><span data-stu-id="031f2-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="031f2-110">Örnek kod</span><span class="sxs-lookup"><span data-stu-id="031f2-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="031f2-111"><b>BLOB</b></span><span class="sxs-lookup"><span data-stu-id="031f2-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="031f2-112">BLOB ekleme</span><span class="sxs-lookup"><span data-stu-id="031f2-112">Append Blob</span></span></td> 
<td><span data-ttu-id="031f2-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java'da Azure Blob hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="031f2-114">Blok blobu</span><span class="sxs-lookup"><span data-stu-id="031f2-114">Block Blob</span></span></td>
<td><span data-ttu-id="031f2-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java'da Azure Blob hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="031f2-116">İstemci Tarafında Şifreleme</span><span class="sxs-lookup"><span data-stu-id="031f2-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="031f2-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Java'da Azure istemci tarafı şifreleme ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Getting Started with Azure Client Side Encryption in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="031f2-118">BLOB kopyalama</span><span class="sxs-lookup"><span data-stu-id="031f2-118">Copy Blob</span></span></td>
<td><span data-ttu-id="031f2-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java'da Azure Blob hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="031f2-120">Kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="031f2-120">Create Container</span></span></td>
<td><span data-ttu-id="031f2-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java'da Azure Blob hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="031f2-122">BLOB Sil</span><span class="sxs-lookup"><span data-stu-id="031f2-122">Delete Blob</span></span></td>
<td><span data-ttu-id="031f2-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java'da Azure Blob hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="031f2-124">Kapsayıcısını silmek</span><span class="sxs-lookup"><span data-stu-id="031f2-124">Delete Container</span></span></td>
<td><span data-ttu-id="031f2-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java'da Azure Blob hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="031f2-126">BLOB meta verileri/özellikler/Stats</span><span class="sxs-lookup"><span data-stu-id="031f2-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="031f2-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Java'da Azure Blob hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="031f2-128">Kapsayıcı ACL/meta veri/özellikleri</span><span class="sxs-lookup"><span data-stu-id="031f2-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="031f2-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Java'da Azure Blob hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="031f2-130">Sayfa aralıklarını alma</span><span class="sxs-lookup"><span data-stu-id="031f2-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="031f2-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Örnek sayfa blobu testleri</a></span><span class="sxs-lookup"><span data-stu-id="031f2-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Page Blob Tests Sample</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="031f2-132">Kira Blob/kapsayıcısı</span><span class="sxs-lookup"><span data-stu-id="031f2-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="031f2-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java'da Azure Blob hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="031f2-134">Liste Blob/kapsayıcısı</span><span class="sxs-lookup"><span data-stu-id="031f2-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="031f2-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java'da Azure Blob hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="031f2-136">Sayfa blobu</span><span class="sxs-lookup"><span data-stu-id="031f2-136">Page Blob</span></span></td>
<td><span data-ttu-id="031f2-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java'da Azure Blob hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="031f2-138">SAS</span><span class="sxs-lookup"><span data-stu-id="031f2-138">SAS</span></span></td>
<td><span data-ttu-id="031f2-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">SAS testleri örnek</a></span><span class="sxs-lookup"><span data-stu-id="031f2-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">SAS Tests Sample</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="031f2-140">Hizmet Özellikleri</span><span class="sxs-lookup"><span data-stu-id="031f2-140">Service Properties</span></span></td>
<td><span data-ttu-id="031f2-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Java'da Azure Blob hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="031f2-142">Anlık görüntü Blob</span><span class="sxs-lookup"><span data-stu-id="031f2-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="031f2-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Java'da Azure Blob hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="031f2-144"><b>Dosya</b></span><span class="sxs-lookup"><span data-stu-id="031f2-144"><b>File</b></span></span></td>
<td><span data-ttu-id="031f2-145">Dizinleri/paylaşımları/dosyaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="031f2-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="031f2-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java'da Azure dosya hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="031f2-147">Dizinleri/paylaşımları/dosyaları silin</span><span class="sxs-lookup"><span data-stu-id="031f2-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="031f2-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java'da Azure dosya hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="031f2-149">Dizin özellikleri/meta veri</span><span class="sxs-lookup"><span data-stu-id="031f2-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="031f2-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Java'da Azure dosya hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="031f2-151">Dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="031f2-151">Download Files</span></span></td> 
<td><span data-ttu-id="031f2-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java'da Azure dosya hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="031f2-153">Dosya özellikleri/meta veri/ölçümleri</span><span class="sxs-lookup"><span data-stu-id="031f2-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="031f2-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Java'da Azure dosya hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="031f2-155">Dosya hizmeti özellikleri</span><span class="sxs-lookup"><span data-stu-id="031f2-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="031f2-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Java'da Azure dosya hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="031f2-157">Liste dizinler ve dosyalar</span><span class="sxs-lookup"><span data-stu-id="031f2-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="031f2-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java'da Azure dosya hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="031f2-159">Paylaşımları</span><span class="sxs-lookup"><span data-stu-id="031f2-159">List Shares</span></span></td> 
<td><span data-ttu-id="031f2-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Java'da Azure dosya hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="031f2-161">Meta veri/özellikler/Stats paylaşma</span><span class="sxs-lookup"><span data-stu-id="031f2-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="031f2-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Java'da Azure dosya hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="031f2-163"><b>Sırası</b></span><span class="sxs-lookup"><span data-stu-id="031f2-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="031f2-164">Mesaj ekleyin.</span><span class="sxs-lookup"><span data-stu-id="031f2-164">Add Message</span></span></td> 
<td><span data-ttu-id="031f2-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Depolama Java istemci kitaplığı örnekleri</a></span><span class="sxs-lookup"><span data-stu-id="031f2-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="031f2-166">İstemci Tarafında Şifreleme</span><span class="sxs-lookup"><span data-stu-id="031f2-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="031f2-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Depolama Java istemci kitaplığı örnekleri</a></span><span class="sxs-lookup"><span data-stu-id="031f2-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="031f2-168">Sıra oluşturma</span><span class="sxs-lookup"><span data-stu-id="031f2-168">Create Queues</span></span></td> 
<td><span data-ttu-id="031f2-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Java'da Azure kuyruk hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="031f2-170">İleti/kuyruk silme</span><span class="sxs-lookup"><span data-stu-id="031f2-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="031f2-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Java'da Azure kuyruk hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="031f2-172">İletiye Gözat</span><span class="sxs-lookup"><span data-stu-id="031f2-172">Peek Message</span></span></td> 
<td><span data-ttu-id="031f2-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Java'da Azure kuyruk hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="031f2-174">Sıra ACL/meta veri/Stats</span><span class="sxs-lookup"><span data-stu-id="031f2-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="031f2-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Java'da Azure kuyruk hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="031f2-176">Kuyruk hizmeti özellikleri</span><span class="sxs-lookup"><span data-stu-id="031f2-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="031f2-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Java'da Azure kuyruk hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="031f2-178">Güncelleştirme iletisi</span><span class="sxs-lookup"><span data-stu-id="031f2-178">Update Message</span></span></td> 
<td><span data-ttu-id="031f2-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Java'da Azure kuyruk hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="031f2-180"><b>Tablo</b></span><span class="sxs-lookup"><span data-stu-id="031f2-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="031f2-181">Tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="031f2-181">Create Table</span></span></td> 
<td><span data-ttu-id="031f2-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Java'da Azure tablo hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="031f2-183">Varlık/tablo silme</span><span class="sxs-lookup"><span data-stu-id="031f2-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="031f2-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Java'da Azure tablo hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="031f2-185">Birleştirme/Ekle/Değiştir varlık</span><span class="sxs-lookup"><span data-stu-id="031f2-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="031f2-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Depolama Java istemci kitaplığı örnekleri</a></span><span class="sxs-lookup"><span data-stu-id="031f2-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="031f2-187">Sorgu varlıklar</span><span class="sxs-lookup"><span data-stu-id="031f2-187">Query Entities</span></span></td> 
<td><span data-ttu-id="031f2-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Java'da Azure tablo hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="031f2-189">Sorgu tabloları</span><span class="sxs-lookup"><span data-stu-id="031f2-189">Query Tables</span></span></td> 
<td><span data-ttu-id="031f2-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Java'da Azure tablo hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="031f2-191">Tablo ACL/özellikleri</span><span class="sxs-lookup"><span data-stu-id="031f2-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="031f2-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Java'da Azure tablo hizmeti ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="031f2-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="031f2-193">Varlık güncelleştir</span><span class="sxs-lookup"><span data-stu-id="031f2-193">Update Entity</span></span></td> 
<td><span data-ttu-id="031f2-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Depolama Java istemci kitaplığı örnekleri</a></span><span class="sxs-lookup"><span data-stu-id="031f2-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="031f2-195">Azure Kod Örnekleri Kitaplığı</span><span class="sxs-lookup"><span data-stu-id="031f2-195">Azure Code Samples library</span></span>

<span data-ttu-id="031f2-196">tooview hello tam örnek kitaplığı, Git toohello [Azure Kod örnekleri](https://azure.microsoft.com/resources/samples/?service=storage) Azure Storage için karşıdan yükle ve yerel olarak çalıştırılan örnekleri içeren kitaplık.</span><span class="sxs-lookup"><span data-stu-id="031f2-196">tooview hello complete sample library, go toohello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="031f2-197">Merhaba kod örnek kitaplığı .zip biçimi örnek kodda sağlar.</span><span class="sxs-lookup"><span data-stu-id="031f2-197">hello Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="031f2-198">Alternatif olarak, bulun ve her bir örnek için hello GitHub deposunu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="031f2-198">Alternatively, you can browse and clone hello GitHub repository for each sample.</span></span>

[!INCLUDE [storage-java-samples-include](../../../includes/storage-java-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="031f2-199">Başlarken kılavuzları alma</span><span class="sxs-lookup"><span data-stu-id="031f2-199">Getting started guides</span></span>

<span data-ttu-id="031f2-200">Kılavuzları hakkında yönergeler arıyorsanız aşağıdaki hello kullanıma tooinstall ve Azure Storage istemcisi kitaplıklarını hello ile çalışmaya başlama.</span><span class="sxs-lookup"><span data-stu-id="031f2-200">Check out hello following guides if you are looking for instructions on how tooinstall and get started with hello Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="031f2-201">Java'da Azure Blob hizmeti ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="031f2-201">Getting Started with Azure Blob Service in Java</span></span>](../blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="031f2-202">Java'da Azure kuyruk hizmeti ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="031f2-202">Getting Started with Azure Queue Service in Java</span></span>](../storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="031f2-203">Java'da Azure tablo hizmeti ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="031f2-203">Getting Started with Azure Table Service in Java</span></span>](../../cosmos-db/table-storage-how-to-use-java.md)
* [<span data-ttu-id="031f2-204">Java'da Azure dosya hizmeti ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="031f2-204">Getting Started with Azure File Service in Java</span></span>](../storage-java-how-to-use-file-storage.md)

## <a name="next-steps"></a><span data-ttu-id="031f2-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="031f2-205">Next steps</span></span>

<span data-ttu-id="031f2-206">Diğer diller için örnekleri hakkında daha fazla bilgi için:</span><span class="sxs-lookup"><span data-stu-id="031f2-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="031f2-207">.NET: [.NET kullanarak azure Storage örnekleri](../storage-samples-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="031f2-207">.NET: [Azure Storage samples using .NET](../storage-samples-dotnet.md)</span></span>
* <span data-ttu-id="031f2-208">Tüm diğer dillere: [Azure Storage örnekleri](../storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="031f2-208">All other languages: [Azure Storage samples](../storage-samples.md)</span></span>
