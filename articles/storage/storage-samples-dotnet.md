---
title: ".NET kullanarak aaaAzure depolama örnekleri | Microsoft Docs"
description: "Görüntülemek, indirin ve örnek kod ve uygulamaları için Azure Storage çalıştırın. BLOB, kuyruklar, tablolar ve dosyaları için örnek hello .NET depolama istemcisi kitaplıklarını kullanarak Başlarken bulur."
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
ms.openlocfilehash: 9a7055645b0f0658b850f024b8b19ab19840330e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-samples-using-net"></a><span data-ttu-id="539e6-104">.NET kullanarak azure depolama örnekleri</span><span class="sxs-lookup"><span data-stu-id="539e6-104">Azure Storage samples using .NET</span></span>

## <a name="net-sample-index"></a><span data-ttu-id="539e6-105">.NET örnek dizini</span><span class="sxs-lookup"><span data-stu-id="539e6-105">.NET sample index</span></span>

<span data-ttu-id="539e6-106">Merhaba aşağıdaki tabloda örneklerimizi genel bir bakış depo ve hello senaryolar sağlar her örnek kapsamdaki.</span><span class="sxs-lookup"><span data-stu-id="539e6-106">hello following table provides an overview of our samples repository and hello scenarios covered in each sample.</span></span> <span data-ttu-id="539e6-107">Merhaba bağlantılar tooview hello karşılık gelen örnek kod github'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="539e6-107">Click on hello links tooview hello corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="539e6-108">Uç Nokta</span><span class="sxs-lookup"><span data-stu-id="539e6-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="539e6-109">Senaryo</span><span class="sxs-lookup"><span data-stu-id="539e6-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="539e6-110">Örnek kod</span><span class="sxs-lookup"><span data-stu-id="539e6-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="539e6-111"><b>BLOB</b></span><span class="sxs-lookup"><span data-stu-id="539e6-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="539e6-112">BLOB ekleme</span><span class="sxs-lookup"><span data-stu-id="539e6-112">Append Blob</span></span></td> 
<td><span data-ttu-id="539e6-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">CloudBlobContainer.GetAppendBlobReference yöntemi örneği</a></span><span class="sxs-lookup"><span data-stu-id="539e6-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">CloudBlobContainer.GetAppendBlobReference Method Example</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="539e6-114">Blok blobu</span><span class="sxs-lookup"><span data-stu-id="539e6-114">Block Blob</span></span></td>
<td><span data-ttu-id="539e6-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Depolama Fotoğraf Galerisi Web uygulaması</a></span><span class="sxs-lookup"><span data-stu-id="539e6-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="539e6-116">İstemci Tarafında Şifreleme</span><span class="sxs-lookup"><span data-stu-id="539e6-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="539e6-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">BLOB şifreleme örnekleri</a></span><span class="sxs-lookup"><span data-stu-id="539e6-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Blob Encryption Samples</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="539e6-118">BLOB kopyalama</span><span class="sxs-lookup"><span data-stu-id="539e6-118">Copy Blob</span></span></td>
<td><span data-ttu-id="539e6-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">BLOB'lar ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="539e6-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="539e6-120">Kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="539e6-120">Create Container</span></span></td>
<td><span data-ttu-id="539e6-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Depolama Fotoğraf Galerisi Web uygulaması</a></span><span class="sxs-lookup"><span data-stu-id="539e6-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="539e6-122">BLOB Sil</span><span class="sxs-lookup"><span data-stu-id="539e6-122">Delete Blob</span></span></td>
<td><span data-ttu-id="539e6-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Depolama Fotoğraf Galerisi Web uygulaması</a></span><span class="sxs-lookup"><span data-stu-id="539e6-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="539e6-124">Kapsayıcısını silmek</span><span class="sxs-lookup"><span data-stu-id="539e6-124">Delete Container</span></span></td>
<td><span data-ttu-id="539e6-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">BLOB'lar ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="539e6-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="539e6-126">BLOB meta verileri/özellikler/Stats</span><span class="sxs-lookup"><span data-stu-id="539e6-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="539e6-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">BLOB'lar ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="539e6-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="539e6-128">Kapsayıcı ACL/meta veri/özellikleri</span><span class="sxs-lookup"><span data-stu-id="539e6-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="539e6-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Depolama Fotoğraf Galerisi Web uygulaması</a></span><span class="sxs-lookup"><span data-stu-id="539e6-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="539e6-130">Sayfa aralıklarını alma</span><span class="sxs-lookup"><span data-stu-id="539e6-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="539e6-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">BLOB'lar ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="539e6-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="539e6-132">Kira Blob/kapsayıcısı</span><span class="sxs-lookup"><span data-stu-id="539e6-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="539e6-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">BLOB'lar ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="539e6-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="539e6-134">Liste Blob/kapsayıcısı</span><span class="sxs-lookup"><span data-stu-id="539e6-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="539e6-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">BLOB'lar ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="539e6-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="539e6-136">Sayfa blobu</span><span class="sxs-lookup"><span data-stu-id="539e6-136">Page Blob</span></span></td>
<td><span data-ttu-id="539e6-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">BLOB'lar ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="539e6-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="539e6-138">SAS</span><span class="sxs-lookup"><span data-stu-id="539e6-138">SAS</span></span></td>
<td><span data-ttu-id="539e6-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">BLOB'lar ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="539e6-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="539e6-140">Hizmet Özellikleri</span><span class="sxs-lookup"><span data-stu-id="539e6-140">Service Properties</span></span></td>
<td><span data-ttu-id="539e6-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">BLOB'lar ile çalışmaya başlama</a></span><span class="sxs-lookup"><span data-stu-id="539e6-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="539e6-142">Anlık görüntü Blob</span><span class="sxs-lookup"><span data-stu-id="539e6-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="539e6-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Artımlı anlık görüntüleri yedekleme Azure sanal makine diskleriyle</a></span><span class="sxs-lookup"><span data-stu-id="539e6-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Backup Azure Virtual Machine Disks with Incremental Snapshots</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="539e6-144"><b>Dosya</b></span><span class="sxs-lookup"><span data-stu-id="539e6-144"><b>File</b></span></span></td>
<td><span data-ttu-id="539e6-145">Dizinleri/paylaşımları/dosyaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="539e6-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="539e6-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure depolama .NET dosya depolama örnek</a></span><span class="sxs-lookup"><span data-stu-id="539e6-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="539e6-147">Dizinleri/paylaşımları/dosyaları silin</span><span class="sxs-lookup"><span data-stu-id="539e6-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="539e6-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Azure dosya hizmeti .NET kullanmaya Başlarken</a></span><span class="sxs-lookup"><span data-stu-id="539e6-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Getting Started with Azure File Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="539e6-149">Dizin özellikleri/meta veri</span><span class="sxs-lookup"><span data-stu-id="539e6-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="539e6-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure depolama .NET dosya depolama örnek</a></span><span class="sxs-lookup"><span data-stu-id="539e6-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="539e6-151">Dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="539e6-151">Download Files</span></span></td> 
<td><span data-ttu-id="539e6-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure depolama .NET dosya depolama örnek</a></span><span class="sxs-lookup"><span data-stu-id="539e6-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="539e6-153">Dosya özellikleri/meta veri/ölçümleri</span><span class="sxs-lookup"><span data-stu-id="539e6-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="539e6-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure depolama .NET dosya depolama örnek</a></span><span class="sxs-lookup"><span data-stu-id="539e6-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="539e6-155">Dosya hizmeti özellikleri</span><span class="sxs-lookup"><span data-stu-id="539e6-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="539e6-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure depolama .NET dosya depolama örnek</a></span><span class="sxs-lookup"><span data-stu-id="539e6-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="539e6-157">Liste dizinler ve dosyalar</span><span class="sxs-lookup"><span data-stu-id="539e6-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="539e6-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure depolama .NET dosya depolama örnek</a></span><span class="sxs-lookup"><span data-stu-id="539e6-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="539e6-159">Paylaşımları</span><span class="sxs-lookup"><span data-stu-id="539e6-159">List Shares</span></span></td> 
<td><span data-ttu-id="539e6-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure depolama .NET dosya depolama örnek</a></span><span class="sxs-lookup"><span data-stu-id="539e6-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="539e6-161">Meta veri/özellikler/Stats paylaşma</span><span class="sxs-lookup"><span data-stu-id="539e6-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="539e6-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure depolama .NET dosya depolama örnek</a></span><span class="sxs-lookup"><span data-stu-id="539e6-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="539e6-163"><b>Sırası</b></span><span class="sxs-lookup"><span data-stu-id="539e6-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="539e6-164">Mesaj ekleyin.</span><span class="sxs-lookup"><span data-stu-id="539e6-164">Add Message</span></span></td> 
<td><span data-ttu-id="539e6-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Azure kuyruk hizmetinde .NET kullanmaya Başlarken</a></span><span class="sxs-lookup"><span data-stu-id="539e6-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="539e6-166">İstemci Tarafında Şifreleme</span><span class="sxs-lookup"><span data-stu-id="539e6-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="539e6-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Azure depolama .NET sıra istemci tarafı şifreleme</a></span><span class="sxs-lookup"><span data-stu-id="539e6-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Azure Storage .NET Queue Client-Side Encryption</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="539e6-168">Sıra oluşturma</span><span class="sxs-lookup"><span data-stu-id="539e6-168">Create Queues</span></span></td> 
<td><span data-ttu-id="539e6-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Azure kuyruk hizmetinde .NET kullanmaya Başlarken</a></span><span class="sxs-lookup"><span data-stu-id="539e6-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="539e6-170">İleti/kuyruk silme</span><span class="sxs-lookup"><span data-stu-id="539e6-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="539e6-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Azure kuyruk hizmetinde .NET kullanmaya Başlarken</a></span><span class="sxs-lookup"><span data-stu-id="539e6-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="539e6-172">İletiye Gözat</span><span class="sxs-lookup"><span data-stu-id="539e6-172">Peek Message</span></span></td> 
<td><span data-ttu-id="539e6-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Azure kuyruk hizmetinde .NET kullanmaya Başlarken</a></span><span class="sxs-lookup"><span data-stu-id="539e6-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="539e6-174">Sıra ACL/meta veri/Stats</span><span class="sxs-lookup"><span data-stu-id="539e6-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="539e6-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Azure kuyruk hizmetinde .NET kullanmaya Başlarken</a></span><span class="sxs-lookup"><span data-stu-id="539e6-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="539e6-176">Kuyruk hizmeti özellikleri</span><span class="sxs-lookup"><span data-stu-id="539e6-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="539e6-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Azure kuyruk hizmetinde .NET kullanmaya Başlarken</a></span><span class="sxs-lookup"><span data-stu-id="539e6-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="539e6-178">Güncelleştirme iletisi</span><span class="sxs-lookup"><span data-stu-id="539e6-178">Update Message</span></span></td> 
<td><span data-ttu-id="539e6-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Azure kuyruk hizmetinde .NET kullanmaya Başlarken</a></span><span class="sxs-lookup"><span data-stu-id="539e6-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="539e6-180"><b>Tablo</b></span><span class="sxs-lookup"><span data-stu-id="539e6-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="539e6-181">Tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="539e6-181">Create Table</span></span></td> 
<td><span data-ttu-id="539e6-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Azure Storage - örnek uygulaması kullanarak eşzamanlılık yönetme</a></span><span class="sxs-lookup"><span data-stu-id="539e6-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="539e6-183">Varlık/tablo silme</span><span class="sxs-lookup"><span data-stu-id="539e6-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="539e6-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">.NET’te Azure Tablo Depolama Kullanmaya Başlama</a></span><span class="sxs-lookup"><span data-stu-id="539e6-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="539e6-185">Birleştirme/Ekle/Değiştir varlık</span><span class="sxs-lookup"><span data-stu-id="539e6-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="539e6-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Azure Storage - örnek uygulaması kullanarak eşzamanlılık yönetme</a></span><span class="sxs-lookup"><span data-stu-id="539e6-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="539e6-187">Sorgu varlıklar</span><span class="sxs-lookup"><span data-stu-id="539e6-187">Query Entities</span></span></td> 
<td><span data-ttu-id="539e6-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">.NET’te Azure Tablo Depolama Kullanmaya Başlama</a></span><span class="sxs-lookup"><span data-stu-id="539e6-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="539e6-189">Sorgu tabloları</span><span class="sxs-lookup"><span data-stu-id="539e6-189">Query Tables</span></span></td> 
<td><span data-ttu-id="539e6-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">.NET’te Azure Tablo Depolama Kullanmaya Başlama</a></span><span class="sxs-lookup"><span data-stu-id="539e6-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="539e6-191">Tablo ACL/özellikleri</span><span class="sxs-lookup"><span data-stu-id="539e6-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="539e6-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">.NET’te Azure Tablo Depolama Kullanmaya Başlama</a></span><span class="sxs-lookup"><span data-stu-id="539e6-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="539e6-193">Varlık güncelleştir</span><span class="sxs-lookup"><span data-stu-id="539e6-193">Update Entity</span></span></td> 
<td><span data-ttu-id="539e6-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Azure Storage - örnek uygulaması kullanarak eşzamanlılık yönetme</a></span><span class="sxs-lookup"><span data-stu-id="539e6-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="539e6-195">Azure Kod Örnekleri Kitaplığı</span><span class="sxs-lookup"><span data-stu-id="539e6-195">Azure Code Samples library</span></span>

<span data-ttu-id="539e6-196">tooview hello tam örnek kitaplığı, Git toohello [Azure Kod örnekleri](https://azure.microsoft.com/resources/samples/?service=storage) Azure Storage için karşıdan yükle ve yerel olarak çalıştırılan örnekleri içeren kitaplık.</span><span class="sxs-lookup"><span data-stu-id="539e6-196">tooview hello complete sample library, go toohello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="539e6-197">Merhaba kod örnek kitaplığı .zip biçimi örnek kodda sağlar.</span><span class="sxs-lookup"><span data-stu-id="539e6-197">hello Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="539e6-198">Alternatif olarak, bulun ve her bir örnek için hello GitHub deposunu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="539e6-198">Alternatively, you can browse and clone hello GitHub repository for each sample.</span></span>

[!INCLUDE [storage-dotnet-samples-include](../../includes/storage-dotnet-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="539e6-199">Başlarken kılavuzları alma</span><span class="sxs-lookup"><span data-stu-id="539e6-199">Getting started guides</span></span>

<span data-ttu-id="539e6-200">Kılavuzları hakkında yönergeler arıyorsanız aşağıdaki hello kullanıma tooinstall ve Azure Storage istemcisi kitaplıklarını hello ile çalışmaya başlama.</span><span class="sxs-lookup"><span data-stu-id="539e6-200">Check out hello following guides if you are looking for instructions on how tooinstall and get started with hello Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="539e6-201">Azure Blob hizmetine .NET kullanmaya Başlarken</span><span class="sxs-lookup"><span data-stu-id="539e6-201">Getting Started with Azure Blob Service in .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="539e6-202">Azure kuyruk hizmetinde .NET kullanmaya Başlarken</span><span class="sxs-lookup"><span data-stu-id="539e6-202">Getting Started with Azure Queue Service in .NET</span></span>](storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="539e6-203">Azure tablo hizmetinde .NET kullanmaya Başlarken</span><span class="sxs-lookup"><span data-stu-id="539e6-203">Getting Started with Azure Table Service in .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="539e6-204">Azure dosya hizmeti .NET kullanmaya Başlarken</span><span class="sxs-lookup"><span data-stu-id="539e6-204">Getting Started with Azure File Service in .NET</span></span>](storage-dotnet-how-to-use-files.md)

## <a name="next-steps"></a><span data-ttu-id="539e6-205">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="539e6-205">Next steps</span></span>

<span data-ttu-id="539e6-206">Diğer diller için örnekleri hakkında daha fazla bilgi için:</span><span class="sxs-lookup"><span data-stu-id="539e6-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="539e6-207">Java: [Java kullanarak Azure Storage örnekleri](storage-samples-java.md)</span><span class="sxs-lookup"><span data-stu-id="539e6-207">Java: [Azure Storage samples using Java](storage-samples-java.md)</span></span>
* <span data-ttu-id="539e6-208">Tüm diğer dillere: [Azure Storage örnekleri](storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="539e6-208">All other languages: [Azure Storage samples](storage-samples.md)</span></span>
