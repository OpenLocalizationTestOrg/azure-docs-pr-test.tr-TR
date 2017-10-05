---
title: "Bir Azure içeri/dışarı aktarma alma işi - v1 sabit sürücülerini prep için örnek iş akışı | Microsoft Docs"
description: "Sürücüleri Azure içeri/dışarı aktarma hizmetindeki bir içeri aktarma işi hazırlama tam işlemi için bkz."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 6eb1b1b7-c69f-4365-b5ef-3cd5e05eb72a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 179c6bac9a2d9509baa0007a7008d75d0874a25e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="sample-workflow-to-prepare-hard-drives-for-an-import-job"></a><span data-ttu-id="9a25f-103">Sabit sürücüleri içeri aktarma işine hazırlamak için örnek iş akışı</span><span class="sxs-lookup"><span data-stu-id="9a25f-103">Sample workflow to prepare hard drives for an import job</span></span>
<span data-ttu-id="9a25f-104">Bu konu, sürücüler için içeri aktarma işi hazırlama tam işlemi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9a25f-104">This topic walks you through the complete process of preparing drives for an import job.</span></span>  
  
<span data-ttu-id="9a25f-105">Bu örnek olarak aşağıdaki verileri adlı bir Windows Azure depolama hesabı alır `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="9a25f-105">This example imports the following data into a Window Azure storage account named `mystorageaccount`:</span></span>  
  
|<span data-ttu-id="9a25f-106">Konum</span><span class="sxs-lookup"><span data-stu-id="9a25f-106">Location</span></span>|<span data-ttu-id="9a25f-107">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9a25f-107">Description</span></span>|  
|--------------|-----------------|  
|<span data-ttu-id="9a25f-108">H:\Video</span><span class="sxs-lookup"><span data-stu-id="9a25f-108">H:\Video</span></span>|<span data-ttu-id="9a25f-109">Bir koleksiyonu videoları, 5 TB toplam.</span><span class="sxs-lookup"><span data-stu-id="9a25f-109">A collection of videos, 5 TB in total.</span></span>|  
|<span data-ttu-id="9a25f-110">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="9a25f-110">H:\Photo</span></span>|<span data-ttu-id="9a25f-111">Bir koleksiyonu fotoğrafları, toplam 30 GB.</span><span class="sxs-lookup"><span data-stu-id="9a25f-111">A collection of photos, 30 GB in total.</span></span>|  
|<span data-ttu-id="9a25f-112">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="9a25f-112">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="9a25f-113">A Blu-ray™ disk görüntüsü, 25 GB.</span><span class="sxs-lookup"><span data-stu-id="9a25f-113">A Blu-Ray™ disk image, 25 GB.</span></span>|  
|<span data-ttu-id="9a25f-114">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="9a25f-114">\\\bigshare\john\music</span></span>|<span data-ttu-id="9a25f-115">Müzik dosyalarının toplam 10 GB bir ağ paylaşımında koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="9a25f-115">A collection of music files on a network share, 10 GB in total.</span></span>|  
  
<span data-ttu-id="9a25f-116">İçe aktarma işi bu veri depolama hesabındaki aşağıdaki hedefleri aktarır:</span><span class="sxs-lookup"><span data-stu-id="9a25f-116">The import job imports this data into the following destinations in the storage account:</span></span>  
  
|<span data-ttu-id="9a25f-117">Kaynak</span><span class="sxs-lookup"><span data-stu-id="9a25f-117">Source</span></span>|<span data-ttu-id="9a25f-118">Hedef sanal dizin veya blob</span><span class="sxs-lookup"><span data-stu-id="9a25f-118">Destination virtual directory or blob</span></span>|  
|------------|-------------------------------------------|  
|<span data-ttu-id="9a25f-119">H:\Video</span><span class="sxs-lookup"><span data-stu-id="9a25f-119">H:\Video</span></span>|<span data-ttu-id="9a25f-120">https://mystorageaccount.BLOB.Core.Windows.NET/video</span><span class="sxs-lookup"><span data-stu-id="9a25f-120">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="9a25f-121">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="9a25f-121">H:\Photo</span></span>|<span data-ttu-id="9a25f-122">https://mystorageaccount.BLOB.Core.Windows.NET/Photo</span><span class="sxs-lookup"><span data-stu-id="9a25f-122">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="9a25f-123">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="9a25f-123">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="9a25f-124">https://mystorageaccount.BLOB.Core.Windows.NET/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="9a25f-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="9a25f-125">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="9a25f-125">\\\bigshare\john\music</span></span>|<span data-ttu-id="9a25f-126">https://mystorageaccount.BLOB.Core.Windows.NET/Music</span><span class="sxs-lookup"><span data-stu-id="9a25f-126">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
<span data-ttu-id="9a25f-127">Bu eşleme, dosya ile `H:\Video\Drama\GreatMovie.mov` blob içe `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="9a25f-127">With this mapping, the file `H:\Video\Drama\GreatMovie.mov` is imported to the blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>  
  
<span data-ttu-id="9a25f-128">Ardından, kaç tane sabit sürücüler gerekli belirlemek için verilerin boyutunu hesaplama:</span><span class="sxs-lookup"><span data-stu-id="9a25f-128">Next, to determine how many hard drives are needed, compute the size of the data:</span></span>  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
<span data-ttu-id="9a25f-129">Bu örnekte, iki 3 TB sabit sürücü yeterli olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9a25f-129">For this example, two 3-TB hard drives should be sufficient.</span></span> <span data-ttu-id="9a25f-130">Ancak, kaynak dizin itibaren `H:\Video` 5 TB'lık veriyi varsa ve yalnızca 3 TB, tek sabit diskin kapasitesini ayırmak gerekli olan `H:\Video` iki küçük dizini içine: `H:\Video1` ve `H:\Video2`, Microsoft Azure çalıştırmadan önce İçeri/dışarı aktarma aracı.</span><span class="sxs-lookup"><span data-stu-id="9a25f-130">However, since the source directory `H:\Video` has 5 TB of data and your single hard drive's capacity is only 3 TB, it's necessary to break `H:\Video` into two smaller directories: `H:\Video1` and `H:\Video2`, before running the Microsoft Azure Import/Export Tool.</span></span> <span data-ttu-id="9a25f-131">Bu adımı şu kaynak dizinlerini verir:</span><span class="sxs-lookup"><span data-stu-id="9a25f-131">This step yields the following source directories:</span></span>  
  
|<span data-ttu-id="9a25f-132">Konum</span><span class="sxs-lookup"><span data-stu-id="9a25f-132">Location</span></span>|<span data-ttu-id="9a25f-133">Boyut</span><span class="sxs-lookup"><span data-stu-id="9a25f-133">Size</span></span>|<span data-ttu-id="9a25f-134">Hedef sanal dizin veya blob</span><span class="sxs-lookup"><span data-stu-id="9a25f-134">Destination virtual directory or blob</span></span>|  
|--------------|----------|-------------------------------------------|  
|<span data-ttu-id="9a25f-135">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="9a25f-135">H:\Video1</span></span>|<span data-ttu-id="9a25f-136">2,5 TB</span><span class="sxs-lookup"><span data-stu-id="9a25f-136">2.5 TB</span></span>|<span data-ttu-id="9a25f-137">https://mystorageaccount.BLOB.Core.Windows.NET/video</span><span class="sxs-lookup"><span data-stu-id="9a25f-137">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="9a25f-138">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="9a25f-138">H:\Video2</span></span>|<span data-ttu-id="9a25f-139">2,5 TB</span><span class="sxs-lookup"><span data-stu-id="9a25f-139">2.5 TB</span></span>|<span data-ttu-id="9a25f-140">https://mystorageaccount.BLOB.Core.Windows.NET/video</span><span class="sxs-lookup"><span data-stu-id="9a25f-140">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="9a25f-141">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="9a25f-141">H:\Photo</span></span>|<span data-ttu-id="9a25f-142">30 GB</span><span class="sxs-lookup"><span data-stu-id="9a25f-142">30 GB</span></span>|<span data-ttu-id="9a25f-143">https://mystorageaccount.BLOB.Core.Windows.NET/Photo</span><span class="sxs-lookup"><span data-stu-id="9a25f-143">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="9a25f-144">K:\Temp\FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="9a25f-144">K:\Temp\FavoriteMovies.ISO</span></span>|<span data-ttu-id="9a25f-145">25 GB</span><span class="sxs-lookup"><span data-stu-id="9a25f-145">25 GB</span></span>|<span data-ttu-id="9a25f-146">https://mystorageaccount.BLOB.Core.Windows.NET/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="9a25f-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="9a25f-147">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="9a25f-147">\\\bigshare\john\music</span></span>|<span data-ttu-id="9a25f-148">10 GB</span><span class="sxs-lookup"><span data-stu-id="9a25f-148">10 GB</span></span>|<span data-ttu-id="9a25f-149">https://mystorageaccount.BLOB.Core.Windows.NET/Music</span><span class="sxs-lookup"><span data-stu-id="9a25f-149">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
 <span data-ttu-id="9a25f-150">Olsa bile `H:\Video`dizin bölme iki dizini için depolama hesabı aynı hedef sanal dizine gidin.</span><span class="sxs-lookup"><span data-stu-id="9a25f-150">Even though the `H:\Video`directory has been split to two directories, they point to the same destination virtual directory in the storage account.</span></span> <span data-ttu-id="9a25f-151">Bu şekilde tüm video dosyaları altında tek bir korunur `video` depolama hesabındaki kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="9a25f-151">This way, all video files are maintained under a single `video` container in the storage account.</span></span>  
  
 <span data-ttu-id="9a25f-152">Ardından, önceki kaynak dizinleri iki sabit sürücü olacak şekilde eşit dağıtılır:</span><span class="sxs-lookup"><span data-stu-id="9a25f-152">Next, the previous source directories are evenly distributed to the two hard drives:</span></span>  
  
||||  
|-|-|-|  
|<span data-ttu-id="9a25f-153">Sabit sürücü</span><span class="sxs-lookup"><span data-stu-id="9a25f-153">Hard drive</span></span>|<span data-ttu-id="9a25f-154">Kaynak dizinler</span><span class="sxs-lookup"><span data-stu-id="9a25f-154">Source directories</span></span>|<span data-ttu-id="9a25f-155">Toplam boyutu</span><span class="sxs-lookup"><span data-stu-id="9a25f-155">Total size</span></span>|  
|<span data-ttu-id="9a25f-156">İlk sürücü</span><span class="sxs-lookup"><span data-stu-id="9a25f-156">First Drive</span></span>|<span data-ttu-id="9a25f-157">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="9a25f-157">H:\Video1</span></span>|<span data-ttu-id="9a25f-158">2.5 TB + 30 GB</span><span class="sxs-lookup"><span data-stu-id="9a25f-158">2.5 TB + 30 GB</span></span>|  
||<span data-ttu-id="9a25f-159">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="9a25f-159">H:\Photo</span></span>||  
|<span data-ttu-id="9a25f-160">İkinci sürücü</span><span class="sxs-lookup"><span data-stu-id="9a25f-160">Second Drive</span></span>|<span data-ttu-id="9a25f-161">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="9a25f-161">H:\Video2</span></span>|<span data-ttu-id="9a25f-162">2.5 TB + 35 GB</span><span class="sxs-lookup"><span data-stu-id="9a25f-162">2.5 TB + 35 GB</span></span>|  
||<span data-ttu-id="9a25f-163">K:\Temp\BlueRay.ISO</span><span class="sxs-lookup"><span data-stu-id="9a25f-163">K:\Temp\BlueRay.ISO</span></span>||  
||<span data-ttu-id="9a25f-164">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="9a25f-164">\\\bigshare\john\music</span></span>||  
  
<span data-ttu-id="9a25f-165">Ayrıca, aşağıdaki meta verileri tüm dosyalar için ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9a25f-165">In addition, you can set the following metadata for all files:</span></span>  
  
-   <span data-ttu-id="9a25f-166">**UploadMethod:** Windows Azure içeri/dışarı aktarma hizmeti</span><span class="sxs-lookup"><span data-stu-id="9a25f-166">**UploadMethod:** Windows Azure Import/Export service</span></span>  
  
-   <span data-ttu-id="9a25f-167">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="9a25f-167">**DataSetName:** SampleData</span></span>  
  
-   <span data-ttu-id="9a25f-168">**CreationDate:** 1/10/2013</span><span class="sxs-lookup"><span data-stu-id="9a25f-168">**CreationDate:** 10/1/2013</span></span>  
  
<span data-ttu-id="9a25f-169">İçeri aktarılan dosyalar için meta veri ayarlamak için bir metin dosyası oluşturun `c:\WAImportExport\SampleMetadata.txt`, aşağıdaki içeriğe sahip:</span><span class="sxs-lookup"><span data-stu-id="9a25f-169">To set metadata for the imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with the following content:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="9a25f-170">Bazı özellikler için de ayarlayabilirsiniz `FavoriteMovie.ISO` blob:</span><span class="sxs-lookup"><span data-stu-id="9a25f-170">You can also set some properties for the `FavoriteMovie.ISO` blob:</span></span>  
  
-   <span data-ttu-id="9a25f-171">**Content-Type:** application/octet-stream,</span><span class="sxs-lookup"><span data-stu-id="9a25f-171">**Content-Type:** application/octet-stream</span></span>  
  
-   <span data-ttu-id="9a25f-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ ==</span><span class="sxs-lookup"><span data-stu-id="9a25f-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>  
  
-   <span data-ttu-id="9a25f-173">**Cache-Control:** no cache</span><span class="sxs-lookup"><span data-stu-id="9a25f-173">**Cache-Control:** no-cache</span></span>  
  
<span data-ttu-id="9a25f-174">Bu özellikleri ayarlamak için bir metin dosyası oluşturun `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="9a25f-174">To set these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="9a25f-175">Şimdi iki sabit sürücü hazırlamak için Azure içeri/dışarı aktarma aracını çalıştırmak hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="9a25f-175">Now you are ready to run the Azure Import/Export Tool to prepare the two hard drives.</span></span> <span data-ttu-id="9a25f-176">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="9a25f-176">Note that:</span></span>  
  
-   <span data-ttu-id="9a25f-177">İlk sürücü X sürücü olarak bağlı.</span><span class="sxs-lookup"><span data-stu-id="9a25f-177">The first drive is mounted as drive X.</span></span>  
  
-   <span data-ttu-id="9a25f-178">İkinci sürücüyü Y sürücü olarak bağlı.</span><span class="sxs-lookup"><span data-stu-id="9a25f-178">The second drive is mounted as drive Y.</span></span>  
  
-   <span data-ttu-id="9a25f-179">Depolama hesabı anahtarı `mystorageaccount` olan `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span><span class="sxs-lookup"><span data-stu-id="9a25f-179">The key for the storage account `mystorageaccount` is `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span></span>  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a><span data-ttu-id="9a25f-180">Veri önceden yüklendiğinde disk alma işlemi için hazırlanıyor</span><span class="sxs-lookup"><span data-stu-id="9a25f-180">Preparing disk for import when data is pre-loaded</span></span>
 
 <span data-ttu-id="9a25f-181">İçeri aktarılacak veri disk üzerinde zaten bayrağı /skipwrite kullanın.</span><span class="sxs-lookup"><span data-stu-id="9a25f-181">If the data to be imported is already present on the disk, use the flag /skipwrite.</span></span> <span data-ttu-id="9a25f-182">/T ve /srcdir değerini alma için hazırlanan diske hem noktası gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a25f-182">The value of /t and /srcdir should both point to the disk being prepared for import.</span></span> <span data-ttu-id="9a25f-183">İçeri aktarılacak verilerin tümünü yok olduğuna aynı hedef sanal dizin veya kök depolama hesabının, her hedef dizini için aynı komutu ayrı ayrı /ID değerini tüm çalıştırmaları arasında aynı kalmasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9a25f-183">If all of the data to be imported is not going to the same destination virtual directory or root of the storage account, run the same command for each destination directory separately, keeping the value of /id the same across all runs.</span></span>

>[!NOTE] 
><span data-ttu-id="9a25f-184">Bu diskte verileri silme şekilde Format belirtmeyin.</span><span class="sxs-lookup"><span data-stu-id="9a25f-184">Do not specify /format as it will wipe the data on the disk.</span></span> <span data-ttu-id="9a25f-185">Belirtin / şifrelemek veya olup disk zaten veya şifrelenmiş bağlı olarak /bk.</span><span class="sxs-lookup"><span data-stu-id="9a25f-185">You can specify /encrypt or /bk depending on whether the disk is already encrypted or not.</span></span> 
>

```
    When data is already present on the disk for each drive run the following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a><span data-ttu-id="9a25f-186">Oturumlarını - Kopyala ilk sürücü</span><span class="sxs-lookup"><span data-stu-id="9a25f-186">Copy sessions - first drive</span></span>

<span data-ttu-id="9a25f-187">İlk sürücüsü için iki kez iki kaynak dizinleri kopyalamak için Azure içeri/dışarı aktarma aracını çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9a25f-187">For the first drive, run the Azure Import/Export Tool twice to copy the two source directories:</span></span>  

<span data-ttu-id="9a25f-188">**İlk kopya oturumu**</span><span class="sxs-lookup"><span data-stu-id="9a25f-188">**First copy session**</span></span>
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

<span data-ttu-id="9a25f-189">**İkinci kopya oturumu**</span><span class="sxs-lookup"><span data-stu-id="9a25f-189">**Second copy session**</span></span>

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a><span data-ttu-id="9a25f-190">Oturumlarını - Kopyala ikinci sürücü</span><span class="sxs-lookup"><span data-stu-id="9a25f-190">Copy sessions - second drive</span></span>
 
<span data-ttu-id="9a25f-191">İkinci sürücüsü için Azure içeri/dışarı aktarma aracı üç kez, bir kez her kaynak dizinler için ve bir kez tek başına Blu-Ray™ görüntü dosyası için):</span><span class="sxs-lookup"><span data-stu-id="9a25f-191">For the second drive, run the Azure Import/Export Tool three times, once each for the source directories, and once for the standalone Blu-Ray™ image file):</span></span>  
  
<span data-ttu-id="9a25f-192">**İlk kopya oturumu**</span><span class="sxs-lookup"><span data-stu-id="9a25f-192">**First copy session**</span></span> 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
<span data-ttu-id="9a25f-193">**İkinci kopya oturumu**</span><span class="sxs-lookup"><span data-stu-id="9a25f-193">**Second copy session**</span></span>

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
<span data-ttu-id="9a25f-194">**Üçüncü kopya oturumu**</span><span class="sxs-lookup"><span data-stu-id="9a25f-194">**Third copy session**</span></span>  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a><span data-ttu-id="9a25f-195">Kopya oturum tamamlama</span><span class="sxs-lookup"><span data-stu-id="9a25f-195">Copy session completion</span></span>

<span data-ttu-id="9a25f-196">Kopyalama oturumları tamamladıktan sonra iki sürücüsü kopyalama bilgisayardan bağlantısını kesmek ve uygun Windows Azure veri merkezine sevk.</span><span class="sxs-lookup"><span data-stu-id="9a25f-196">Once the copy sessions have completed, you can disconnect the two drives from the copy computer and ship them to the appropriate Windows Azure data center.</span></span> <span data-ttu-id="9a25f-197">İki günlük dosyalarını karşıya `FirstDrive.jrn` ve `SecondDrive.jrn`, içeri aktarma işi oluşturduğunuzda [Windows Azure portalında](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="9a25f-197">Upload the two journal files, `FirstDrive.jrn` and `SecondDrive.jrn`, when you create the import job in the [Windows Azure portal](https://manage.windowsazure.com/).</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="9a25f-198">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9a25f-198">Next steps</span></span>

* [<span data-ttu-id="9a25f-199">Sabit sürücüleri içeri aktarma işine hazırlama</span><span class="sxs-lookup"><span data-stu-id="9a25f-199">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="9a25f-200">Sık kullanılan komutlar için hızlı başvuru</span><span class="sxs-lookup"><span data-stu-id="9a25f-200">Quick reference for frequently used commands</span></span>](../storage-import-export-tool-quick-reference-v1.md) 
