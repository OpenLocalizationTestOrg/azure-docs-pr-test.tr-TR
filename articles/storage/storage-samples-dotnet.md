---
title: ".NET kullanarak azure depolama örnekleri | Microsoft Docs"
description: "Görüntülemek, indirin ve örnek kod ve uygulamaları için Azure Storage çalıştırın. BLOB, kuyruklar, tablolar ve dosyaları için .NET depolama istemcisi kitaplıklarını kullanarak örnek Başlarken bulur."
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 01/12/2017
ms.author: seguler
ms.openlocfilehash: d2b6b3d9483f230ad25ae47255a4f28c1a67e064
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-storage-samples-using-net"></a><span data-ttu-id="b789e-104">.NET kullanarak azure depolama örnekleri</span><span class="sxs-lookup"><span data-stu-id="b789e-104">Azure Storage samples using .NET</span></span>

## <a name="net-sample-index"></a><span data-ttu-id="b789e-105">.NET örnek dizini</span><span class="sxs-lookup"><span data-stu-id="b789e-105">.NET sample index</span></span>

<span data-ttu-id="b789e-106">Aşağıdaki tabloda bizim örnek depo ve her örnek kapsamdaki senaryolar genel bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="b789e-106">The following table provides an overview of our samples repository and the scenarios covered in each sample.</span></span> <span data-ttu-id="b789e-107">Github'da karşılık gelen örnek kod görüntülemek için bağlantıları tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b789e-107">Click on the links to view the corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="b789e-108">Uç Nokta</span><span class="sxs-lookup"><span data-stu-id="b789e-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="b789e-109">Senaryo</span><span class="sxs-lookup"><span data-stu-id="b789e-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="b789e-110">Örnek kod</span><span class="sxs-lookup"><span data-stu-id="b789e-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="b789e-111"><b>BLOB</b></span><span class="sxs-lookup"><span data-stu-id="b789e-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="b789e-112">BLOB ekleme</span><span class="sxs-lookup"><span data-stu-id="b789e-112">Append Blob</span></span></td> 
<td><span data-ttu-id="b789e-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">CloudBlobContainer.GetAppendBlobReference yöntemi örneği</a></span><span class="sxs-lookup"><span data-stu-id="b789e-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">CloudBlobContainer.GetAppendBlobReference Method Example</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b789e-114">Blok blobu</span><span class="sxs-lookup"><span data-stu-id="b789e-114">Block Blob</span></span></td>
<td><span data-ttu-id="b789e-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Depolama Fotoğraf Galerisi Web uygulaması</a></span><span class="sxs-lookup"><span data-stu-id="b789e-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="b789e-116">İstemci Tarafında Şifreleme</span><span class="sxs-lookup"><span data-stu-id="b789e-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="b789e-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">BLOB şifreleme örnekleri</a></span><span class="sxs-lookup"><span data-stu-id="b789e-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Blob Encryption Samples</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="b789e-118">BLOB kopyalama</span><span class="sxs-lookup"><span data-stu-id="b789e-118">Copy Blob</span></span></td>
<td><span data-ttu-id="b789e-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">BLOB'lar ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="b789e-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="b789e-120">Kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b789e-120">Create Container</span></span></td>
<td><span data-ttu-id="b789e-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Depolama Fotoğraf Galerisi Web uygulaması</a></span><span class="sxs-lookup"><span data-stu-id="b789e-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="b789e-122">BLOB Sil</span><span class="sxs-lookup"><span data-stu-id="b789e-122">Delete Blob</span></span></td>
<td><span data-ttu-id="b789e-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Depolama Fotoğraf Galerisi Web uygulaması</a></span><span class="sxs-lookup"><span data-stu-id="b789e-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="b789e-124">Kapsayıcısını silmek</span><span class="sxs-lookup"><span data-stu-id="b789e-124">Delete Container</span></span></td>
<td><span data-ttu-id="b789e-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">BLOB'lar ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="b789e-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="b789e-126">BLOB meta verileri/özellikler/Stats</span><span class="sxs-lookup"><span data-stu-id="b789e-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="b789e-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">BLOB'lar ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="b789e-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="b789e-128">Kapsayıcı ACL/meta veri/özellikleri</span><span class="sxs-lookup"><span data-stu-id="b789e-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="b789e-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Depolama Fotoğraf Galerisi Web uygulaması</a></span><span class="sxs-lookup"><span data-stu-id="b789e-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="b789e-130">Sayfa aralıklarını alma</span><span class="sxs-lookup"><span data-stu-id="b789e-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="b789e-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">BLOB'lar ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="b789e-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="b789e-132">Kira Blob/kapsayıcısı</span><span class="sxs-lookup"><span data-stu-id="b789e-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="b789e-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">BLOB'lar ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="b789e-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="b789e-134">Liste Blob/kapsayıcısı</span><span class="sxs-lookup"><span data-stu-id="b789e-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="b789e-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">BLOB'lar ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="b789e-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="b789e-136">Sayfa blobu</span><span class="sxs-lookup"><span data-stu-id="b789e-136">Page Blob</span></span></td>
<td><span data-ttu-id="b789e-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">BLOB'lar ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="b789e-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="b789e-138">SAS</span><span class="sxs-lookup"><span data-stu-id="b789e-138">SAS</span></span></td>
<td><span data-ttu-id="b789e-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">BLOB'lar ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="b789e-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="b789e-140">Hizmet Özellikleri</span><span class="sxs-lookup"><span data-stu-id="b789e-140">Service Properties</span></span></td>
<td><span data-ttu-id="b789e-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">BLOB'lar ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="b789e-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="b789e-142">Anlık görüntü Blob</span><span class="sxs-lookup"><span data-stu-id="b789e-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="b789e-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Artımlı anlık görüntüleri yedekleme Azure sanal makine diskleriyle</a></span><span class="sxs-lookup"><span data-stu-id="b789e-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Backup Azure Virtual Machine Disks with Incremental Snapshots</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="b789e-144"><b>Dosya</b></span><span class="sxs-lookup"><span data-stu-id="b789e-144"><b>File</b></span></span></td>
<td><span data-ttu-id="b789e-145">Dizinleri/paylaşımları/dosyaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="b789e-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="b789e-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure depolama .NET dosya depolama örnek</a></span><span class="sxs-lookup"><span data-stu-id="b789e-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="b789e-147">Dizinleri/paylaşımları/dosyaları silin</span><span class="sxs-lookup"><span data-stu-id="b789e-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="b789e-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Azure dosya hizmeti .NET kullanmaya Başlarken</a></span><span class="sxs-lookup"><span data-stu-id="b789e-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Getting Started with Azure File Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b789e-149">Dizin özellikleri/meta veri</span><span class="sxs-lookup"><span data-stu-id="b789e-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="b789e-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure depolama .NET dosya depolama örnek</a></span><span class="sxs-lookup"><span data-stu-id="b789e-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b789e-151">Dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="b789e-151">Download Files</span></span></td> 
<td><span data-ttu-id="b789e-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure depolama .NET dosya depolama örnek</a></span><span class="sxs-lookup"><span data-stu-id="b789e-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b789e-153">Dosya özellikleri/meta veri/ölçümleri</span><span class="sxs-lookup"><span data-stu-id="b789e-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="b789e-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure depolama .NET dosya depolama örnek</a></span><span class="sxs-lookup"><span data-stu-id="b789e-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b789e-155">Dosya hizmeti özellikleri</span><span class="sxs-lookup"><span data-stu-id="b789e-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="b789e-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure depolama .NET dosya depolama örnek</a></span><span class="sxs-lookup"><span data-stu-id="b789e-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b789e-157">Liste dizinler ve dosyalar</span><span class="sxs-lookup"><span data-stu-id="b789e-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="b789e-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure depolama .NET dosya depolama örnek</a></span><span class="sxs-lookup"><span data-stu-id="b789e-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="b789e-159">Paylaşımları</span><span class="sxs-lookup"><span data-stu-id="b789e-159">List Shares</span></span></td> 
<td><span data-ttu-id="b789e-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure depolama .NET dosya depolama örnek</a></span><span class="sxs-lookup"><span data-stu-id="b789e-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="b789e-161">Meta veri/özellikler/Stats paylaşma</span><span class="sxs-lookup"><span data-stu-id="b789e-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="b789e-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure depolama .NET dosya depolama örnek</a></span><span class="sxs-lookup"><span data-stu-id="b789e-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="b789e-163"><b>Sırası</b></span><span class="sxs-lookup"><span data-stu-id="b789e-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="b789e-164">Mesaj ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b789e-164">Add Message</span></span></td> 
<td><span data-ttu-id="b789e-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Azure kuyruk hizmetinde .NET kullanmaya Başlarken</a></span><span class="sxs-lookup"><span data-stu-id="b789e-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b789e-166">İstemci Tarafında Şifreleme</span><span class="sxs-lookup"><span data-stu-id="b789e-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="b789e-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Azure depolama .NET sıra istemci tarafı şifreleme</a></span><span class="sxs-lookup"><span data-stu-id="b789e-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Azure Storage .NET Queue Client-Side Encryption</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b789e-168">Sıra oluşturma</span><span class="sxs-lookup"><span data-stu-id="b789e-168">Create Queues</span></span></td> 
<td><span data-ttu-id="b789e-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Azure kuyruk hizmetinde .NET kullanmaya Başlarken</a></span><span class="sxs-lookup"><span data-stu-id="b789e-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b789e-170">İleti/kuyruk silme</span><span class="sxs-lookup"><span data-stu-id="b789e-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="b789e-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Azure kuyruk hizmetinde .NET kullanmaya Başlarken</a></span><span class="sxs-lookup"><span data-stu-id="b789e-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b789e-172">İletiye Gözat</span><span class="sxs-lookup"><span data-stu-id="b789e-172">Peek Message</span></span></td> 
<td><span data-ttu-id="b789e-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Azure kuyruk hizmetinde .NET kullanmaya Başlarken</a></span><span class="sxs-lookup"><span data-stu-id="b789e-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b789e-174">Sıra ACL/meta veri/Stats</span><span class="sxs-lookup"><span data-stu-id="b789e-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="b789e-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Azure kuyruk hizmetinde .NET kullanmaya Başlarken</a></span><span class="sxs-lookup"><span data-stu-id="b789e-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b789e-176">Kuyruk hizmeti özellikleri</span><span class="sxs-lookup"><span data-stu-id="b789e-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="b789e-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Azure kuyruk hizmetinde .NET kullanmaya Başlarken</a></span><span class="sxs-lookup"><span data-stu-id="b789e-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b789e-178">Güncelleştirme iletisi</span><span class="sxs-lookup"><span data-stu-id="b789e-178">Update Message</span></span></td> 
<td><span data-ttu-id="b789e-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Azure kuyruk hizmetinde .NET kullanmaya Başlarken</a></span><span class="sxs-lookup"><span data-stu-id="b789e-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="b789e-180"><b>Tablo</b></span><span class="sxs-lookup"><span data-stu-id="b789e-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="b789e-181">Tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="b789e-181">Create Table</span></span></td> 
<td><span data-ttu-id="b789e-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Azure Storage - örnek uygulaması kullanarak eşzamanlılık yönetme</a></span><span class="sxs-lookup"><span data-stu-id="b789e-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b789e-183">Varlık/tablo silme</span><span class="sxs-lookup"><span data-stu-id="b789e-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="b789e-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">.NET’te Azure Tablo Depolama Kullanmaya Başlama</a></span><span class="sxs-lookup"><span data-stu-id="b789e-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b789e-185">Birleştirme/Ekle/Değiştir varlık</span><span class="sxs-lookup"><span data-stu-id="b789e-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="b789e-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Azure Storage - örnek uygulaması kullanarak eşzamanlılık yönetme</a></span><span class="sxs-lookup"><span data-stu-id="b789e-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b789e-187">Sorgu varlıklar</span><span class="sxs-lookup"><span data-stu-id="b789e-187">Query Entities</span></span></td> 
<td><span data-ttu-id="b789e-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">.NET’te Azure Tablo Depolama Kullanmaya Başlama</a></span><span class="sxs-lookup"><span data-stu-id="b789e-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b789e-189">Sorgu tabloları</span><span class="sxs-lookup"><span data-stu-id="b789e-189">Query Tables</span></span></td> 
<td><span data-ttu-id="b789e-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">.NET’te Azure Tablo Depolama Kullanmaya Başlama</a></span><span class="sxs-lookup"><span data-stu-id="b789e-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b789e-191">Tablo ACL/özellikleri</span><span class="sxs-lookup"><span data-stu-id="b789e-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="b789e-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">.NET’te Azure Tablo Depolama Kullanmaya Başlama</a></span><span class="sxs-lookup"><span data-stu-id="b789e-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="b789e-193">Varlık güncelleştir</span><span class="sxs-lookup"><span data-stu-id="b789e-193">Update Entity</span></span></td> 
<td><span data-ttu-id="b789e-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Azure Storage - örnek uygulaması kullanarak eşzamanlılık yönetme</a></span><span class="sxs-lookup"><span data-stu-id="b789e-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="b789e-195">Azure Kod Örnekleri Kitaplığı</span><span class="sxs-lookup"><span data-stu-id="b789e-195">Azure Code Samples library</span></span>

<span data-ttu-id="b789e-196">Tam örnek kitaplığını görüntülemek için Git [Azure Kod örnekleri](https://azure.microsoft.com/resources/samples/?service=storage) Azure Storage için karşıdan yükle ve yerel olarak çalıştırılan örnekleri içeren kitaplık.</span><span class="sxs-lookup"><span data-stu-id="b789e-196">To view the complete sample library, go to the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="b789e-197">Kod örneği kitaplığı .zip biçimi örnek kodda sağlar.</span><span class="sxs-lookup"><span data-stu-id="b789e-197">The Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="b789e-198">Alternatif olarak, bulun ve her bir örnek için GitHub deposunu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="b789e-198">Alternatively, you can browse and clone the GitHub repository for each sample.</span></span>

[!INCLUDE [storage-dotnet-samples-include](../../includes/storage-dotnet-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="b789e-199">Başlarken kılavuzları alma</span><span class="sxs-lookup"><span data-stu-id="b789e-199">Getting started guides</span></span>

<span data-ttu-id="b789e-200">Yükleyin ve Azure Storage istemcisi kitaplıklarını ile çalışmaya başlama hakkında yönergeler arıyorsanız aşağıdaki kılavuzlara denetleyin.</span><span class="sxs-lookup"><span data-stu-id="b789e-200">Check out the following guides if you are looking for instructions on how to install and get started with the Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="b789e-201">Azure Blob hizmetine .NET kullanmaya Başlarken</span><span class="sxs-lookup"><span data-stu-id="b789e-201">Getting Started with Azure Blob Service in .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="b789e-202">Azure kuyruk hizmetinde .NET kullanmaya Başlarken</span><span class="sxs-lookup"><span data-stu-id="b789e-202">Getting Started with Azure Queue Service in .NET</span></span>](storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="b789e-203">Azure tablo hizmetinde .NET kullanmaya Başlarken</span><span class="sxs-lookup"><span data-stu-id="b789e-203">Getting Started with Azure Table Service in .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="b789e-204">Azure dosya hizmeti .NET kullanmaya Başlarken</span><span class="sxs-lookup"><span data-stu-id="b789e-204">Getting Started with Azure File Service in .NET</span></span>](storage-dotnet-how-to-use-files.md)

## <a name="next-steps"></a><span data-ttu-id="b789e-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b789e-205">Next steps</span></span>

<span data-ttu-id="b789e-206">Diğer diller için örnekleri hakkında daha fazla bilgi için:</span><span class="sxs-lookup"><span data-stu-id="b789e-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="b789e-207">Java: [Java kullanarak Azure Storage örnekleri](storage-samples-java.md)</span><span class="sxs-lookup"><span data-stu-id="b789e-207">Java: [Azure Storage samples using Java](storage-samples-java.md)</span></span>
* <span data-ttu-id="b789e-208">Tüm diğer dillere: [Azure Storage örnekleri](storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="b789e-208">All other languages: [Azure Storage samples](storage-samples.md)</span></span>
