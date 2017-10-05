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
ms.openlocfilehash: 313f8c1f3962a943b4c98c530c324ff28aa84c10
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="sample-workflow-to-prepare-hard-drives-for-an-import-job"></a><span data-ttu-id="c16aa-103">Sabit sürücüleri içeri aktarma işine hazırlamak için örnek iş akışı</span><span class="sxs-lookup"><span data-stu-id="c16aa-103">Sample workflow to prepare hard drives for an import job</span></span>
<span data-ttu-id="c16aa-104">Bu konu, sürücüler için içeri aktarma işi hazırlama tam işlemi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c16aa-104">This topic walks you through the complete process of preparing drives for an import job.</span></span>  
  
<span data-ttu-id="c16aa-105">Bu örnek olarak aşağıdaki verileri adlı bir Windows Azure depolama hesabı alır `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="c16aa-105">This example imports the following data into a Window Azure storage account named `mystorageaccount`:</span></span>  
  
|<span data-ttu-id="c16aa-106">Konum</span><span class="sxs-lookup"><span data-stu-id="c16aa-106">Location</span></span>|<span data-ttu-id="c16aa-107">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c16aa-107">Description</span></span>|  
|--------------|-----------------|  
|<span data-ttu-id="c16aa-108">H:\Video</span><span class="sxs-lookup"><span data-stu-id="c16aa-108">H:\Video</span></span>|<span data-ttu-id="c16aa-109">Bir koleksiyonu videoları, 5 TB toplam.</span><span class="sxs-lookup"><span data-stu-id="c16aa-109">A collection of videos, 5 TB in total.</span></span>|  
|<span data-ttu-id="c16aa-110">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="c16aa-110">H:\Photo</span></span>|<span data-ttu-id="c16aa-111">Bir koleksiyonu fotoğrafları, toplam 30 GB.</span><span class="sxs-lookup"><span data-stu-id="c16aa-111">A collection of photos, 30 GB in total.</span></span>|  
|<span data-ttu-id="c16aa-112">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="c16aa-112">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="c16aa-113">A Blu-ray™ disk görüntüsü, 25 GB.</span><span class="sxs-lookup"><span data-stu-id="c16aa-113">A Blu-Ray™ disk image, 25 GB.</span></span>|  
|<span data-ttu-id="c16aa-114">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="c16aa-114">\\\bigshare\john\music</span></span>|<span data-ttu-id="c16aa-115">Müzik dosyalarının toplam 10 GB bir ağ paylaşımında koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="c16aa-115">A collection of music files on a network share, 10 GB in total.</span></span>|  
  
<span data-ttu-id="c16aa-116">İçe aktarma işi bu veri depolama hesabındaki aşağıdaki hedefleri aktarmak:</span><span class="sxs-lookup"><span data-stu-id="c16aa-116">The import job will import this data into the following destinations in the storage account:</span></span>  
  
|<span data-ttu-id="c16aa-117">Kaynak</span><span class="sxs-lookup"><span data-stu-id="c16aa-117">Source</span></span>|<span data-ttu-id="c16aa-118">Hedef sanal dizin veya blob</span><span class="sxs-lookup"><span data-stu-id="c16aa-118">Destination virtual directory or blob</span></span>|  
|------------|-------------------------------------------|  
|<span data-ttu-id="c16aa-119">H:\Video</span><span class="sxs-lookup"><span data-stu-id="c16aa-119">H:\Video</span></span>|<span data-ttu-id="c16aa-120">https://mystorageaccount.BLOB.Core.Windows.NET/video</span><span class="sxs-lookup"><span data-stu-id="c16aa-120">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="c16aa-121">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="c16aa-121">H:\Photo</span></span>|<span data-ttu-id="c16aa-122">https://mystorageaccount.BLOB.Core.Windows.NET/Photo</span><span class="sxs-lookup"><span data-stu-id="c16aa-122">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="c16aa-123">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="c16aa-123">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="c16aa-124">https://mystorageaccount.BLOB.Core.Windows.NET/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="c16aa-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="c16aa-125">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="c16aa-125">\\\bigshare\john\music</span></span>|<span data-ttu-id="c16aa-126">https://mystorageaccount.BLOB.Core.Windows.NET/Music</span><span class="sxs-lookup"><span data-stu-id="c16aa-126">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
<span data-ttu-id="c16aa-127">Bu eşleme, dosya ile `H:\Video\Drama\GreatMovie.mov` blob içeri aktarılacak `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="c16aa-127">With this mapping, the file `H:\Video\Drama\GreatMovie.mov` will be imported to the blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>  
  
<span data-ttu-id="c16aa-128">Ardından, kaç tane sabit sürücüler gerekli belirlemek için verilerin boyutunu hesaplama:</span><span class="sxs-lookup"><span data-stu-id="c16aa-128">Next, to determine how many hard drives are needed, compute the size of the data:</span></span>  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
<span data-ttu-id="c16aa-129">Bu örnekte, iki 3TB sabit sürücü yeterli olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c16aa-129">For this example, two 3TB hard drives should be sufficient.</span></span> <span data-ttu-id="c16aa-130">Ancak, kaynak dizin itibaren `H:\Video` 5 TB'lık veriyi varsa ve yalnızca 3 TB, tek sabit diskin kapasitesini ayırmak gerekli olan `H:\Video` Microsoft Azure içeri/dışarı aktarma Aracı'nı çalıştırmadan önce iki küçük dizini içine: `H:\Video1` ve `H:\Video2`.</span><span class="sxs-lookup"><span data-stu-id="c16aa-130">However, since the source directory `H:\Video` has 5TB of data and your single hard drive's capacity is only 3TB, it's necessary to break `H:\Video` into two smaller directories before running the Microsoft Azure Import/Export Tool: `H:\Video1` and `H:\Video2`.</span></span> <span data-ttu-id="c16aa-131">Bu adımı şu kaynak dizinlerini verir:</span><span class="sxs-lookup"><span data-stu-id="c16aa-131">This step yields the following source directories:</span></span>  
  
|<span data-ttu-id="c16aa-132">Konum</span><span class="sxs-lookup"><span data-stu-id="c16aa-132">Location</span></span>|<span data-ttu-id="c16aa-133">Boyut</span><span class="sxs-lookup"><span data-stu-id="c16aa-133">Size</span></span>|<span data-ttu-id="c16aa-134">Hedef sanal dizin veya blob</span><span class="sxs-lookup"><span data-stu-id="c16aa-134">Destination virtual directory or blob</span></span>|  
|--------------|----------|-------------------------------------------|  
|<span data-ttu-id="c16aa-135">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="c16aa-135">H:\Video1</span></span>|<span data-ttu-id="c16aa-136">2.5 TB</span><span class="sxs-lookup"><span data-stu-id="c16aa-136">2.5TB</span></span>|<span data-ttu-id="c16aa-137">https://mystorageaccount.BLOB.Core.Windows.NET/video</span><span class="sxs-lookup"><span data-stu-id="c16aa-137">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="c16aa-138">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="c16aa-138">H:\Video2</span></span>|<span data-ttu-id="c16aa-139">2.5 TB</span><span class="sxs-lookup"><span data-stu-id="c16aa-139">2.5TB</span></span>|<span data-ttu-id="c16aa-140">https://mystorageaccount.BLOB.Core.Windows.NET/video</span><span class="sxs-lookup"><span data-stu-id="c16aa-140">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="c16aa-141">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="c16aa-141">H:\Photo</span></span>|<span data-ttu-id="c16aa-142">30 GB</span><span class="sxs-lookup"><span data-stu-id="c16aa-142">30GB</span></span>|<span data-ttu-id="c16aa-143">https://mystorageaccount.BLOB.Core.Windows.NET/Photo</span><span class="sxs-lookup"><span data-stu-id="c16aa-143">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="c16aa-144">K:\Temp\FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="c16aa-144">K:\Temp\FavoriteMovies.ISO</span></span>|<span data-ttu-id="c16aa-145">25 GB</span><span class="sxs-lookup"><span data-stu-id="c16aa-145">25GB</span></span>|<span data-ttu-id="c16aa-146">https://mystorageaccount.BLOB.Core.Windows.NET/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="c16aa-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="c16aa-147">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="c16aa-147">\\\bigshare\john\music</span></span>|<span data-ttu-id="c16aa-148">10GB</span><span class="sxs-lookup"><span data-stu-id="c16aa-148">10GB</span></span>|<span data-ttu-id="c16aa-149">https://mystorageaccount.BLOB.Core.Windows.NET/Music</span><span class="sxs-lookup"><span data-stu-id="c16aa-149">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
 <span data-ttu-id="c16aa-150">Unutmayın `H:\Video`dizin bölme iki dizini için depolama hesabı aynı hedef sanal dizine gidin.</span><span class="sxs-lookup"><span data-stu-id="c16aa-150">Note that even though the `H:\Video`directory has been split to two directories, they point to the same destination virtual directory in the storage account.</span></span> <span data-ttu-id="c16aa-151">Bu şekilde tüm video dosyaları altında tek bir korunur `video` depolama hesabındaki kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="c16aa-151">This way, all video files are maintained under a single `video` container in the storage account.</span></span>  
  
 <span data-ttu-id="c16aa-152">Ardından, yukarıdaki kaynak dizinleri iki sabit sürücü olacak şekilde eşit dağıtılır:</span><span class="sxs-lookup"><span data-stu-id="c16aa-152">Next, the above source directories are evenly distributed to the two hard drives:</span></span>  
  
||||  
|-|-|-|  
|<span data-ttu-id="c16aa-153">Sabit sürücü</span><span class="sxs-lookup"><span data-stu-id="c16aa-153">Hard drive</span></span>|<span data-ttu-id="c16aa-154">Kaynak dizinler</span><span class="sxs-lookup"><span data-stu-id="c16aa-154">Source directories</span></span>|<span data-ttu-id="c16aa-155">Toplam boyutu</span><span class="sxs-lookup"><span data-stu-id="c16aa-155">Total size</span></span>|  
|<span data-ttu-id="c16aa-156">İlk sürücü</span><span class="sxs-lookup"><span data-stu-id="c16aa-156">First Drive</span></span>|<span data-ttu-id="c16aa-157">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="c16aa-157">H:\Video1</span></span>|<span data-ttu-id="c16aa-158">2.5 TB + 30 GB</span><span class="sxs-lookup"><span data-stu-id="c16aa-158">2.5TB + 30GB</span></span>|  
||<span data-ttu-id="c16aa-159">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="c16aa-159">H:\Photo</span></span>||  
|<span data-ttu-id="c16aa-160">İkinci sürücü</span><span class="sxs-lookup"><span data-stu-id="c16aa-160">Second Drive</span></span>|<span data-ttu-id="c16aa-161">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="c16aa-161">H:\Video2</span></span>|<span data-ttu-id="c16aa-162">2.5 TB + 35 GB</span><span class="sxs-lookup"><span data-stu-id="c16aa-162">2.5TB + 35GB</span></span>|  
||<span data-ttu-id="c16aa-163">K:\Temp\BlueRay.ISO</span><span class="sxs-lookup"><span data-stu-id="c16aa-163">K:\Temp\BlueRay.ISO</span></span>||  
||<span data-ttu-id="c16aa-164">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="c16aa-164">\\\bigshare\john\music</span></span>||  
  
<span data-ttu-id="c16aa-165">Ayrıca, aşağıdaki meta verileri tüm dosyalar için ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c16aa-165">In addition, you can set the following metadata for all files:</span></span>  
  
-   <span data-ttu-id="c16aa-166">**UploadMethod:** Windows Azure içeri/dışarı aktarma hizmeti</span><span class="sxs-lookup"><span data-stu-id="c16aa-166">**UploadMethod:** Windows Azure Import/Export service</span></span>  
  
-   <span data-ttu-id="c16aa-167">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="c16aa-167">**DataSetName:** SampleData</span></span>  
  
-   <span data-ttu-id="c16aa-168">**CreationDate:** 1/10/2013</span><span class="sxs-lookup"><span data-stu-id="c16aa-168">**CreationDate:** 10/1/2013</span></span>  
  
<span data-ttu-id="c16aa-169">İçeri aktarılan dosyalar için meta veri ayarlamak için bir metin dosyası oluşturun `c:\WAImportExport\SampleMetadata.txt`, aşağıdaki içeriğe sahip:</span><span class="sxs-lookup"><span data-stu-id="c16aa-169">To set metadata for the imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with the following content:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="c16aa-170">Bazı özellikler için de ayarlayabilirsiniz `FavoriteMovie.ISO` blob:</span><span class="sxs-lookup"><span data-stu-id="c16aa-170">You can also set some properties for the `FavoriteMovie.ISO` blob:</span></span>  
  
-   <span data-ttu-id="c16aa-171">**Content-Type:** application/octet-stream,</span><span class="sxs-lookup"><span data-stu-id="c16aa-171">**Content-Type:** application/octet-stream</span></span>  
  
-   <span data-ttu-id="c16aa-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ ==</span><span class="sxs-lookup"><span data-stu-id="c16aa-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>  
  
-   <span data-ttu-id="c16aa-173">**Cache-Control:** no cache</span><span class="sxs-lookup"><span data-stu-id="c16aa-173">**Cache-Control:** no-cache</span></span>  
  
<span data-ttu-id="c16aa-174">Bu özellikleri ayarlamak için bir metin dosyası oluşturun `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="c16aa-174">To set these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="c16aa-175">Şimdi iki sabit sürücü hazırlamak için Azure içeri/dışarı aktarma aracını çalıştırmak hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="c16aa-175">Now you are ready to run the Azure Import/Export Tool to prepare the two hard drives.</span></span> <span data-ttu-id="c16aa-176">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="c16aa-176">Note that:</span></span>  
  
-   <span data-ttu-id="c16aa-177">İlk sürücü X sürücü olarak bağlı.</span><span class="sxs-lookup"><span data-stu-id="c16aa-177">The first drive is mounted as drive X.</span></span>  
  
-   <span data-ttu-id="c16aa-178">İkinci sürücüyü Y sürücü olarak bağlı.</span><span class="sxs-lookup"><span data-stu-id="c16aa-178">The second drive is mounted as drive Y.</span></span>  
  
-   <span data-ttu-id="c16aa-179">Depolama hesabı anahtarı `mystorageaccount` olan `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span><span class="sxs-lookup"><span data-stu-id="c16aa-179">The key for the storage account `mystorageaccount` is `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span></span>  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a><span data-ttu-id="c16aa-180">Veri önceden yüklendiğinde disk alma işlemi için hazırlanıyor</span><span class="sxs-lookup"><span data-stu-id="c16aa-180">Preparing disk for import when data is pre-loaded</span></span>
 
 <span data-ttu-id="c16aa-181">İçeri aktarılacak veri disk üzerinde zaten bayrağı /skipwrite kullanın.</span><span class="sxs-lookup"><span data-stu-id="c16aa-181">If the data to be imported is already present on the disk, use the flag /skipwrite.</span></span> <span data-ttu-id="c16aa-182">Değeri /t ve /srcdir her ikisi de alma için hazırlanan diske işaret etmelidir.</span><span class="sxs-lookup"><span data-stu-id="c16aa-182">Value of /t and /srcdir both should point to the disk being prepared for import.</span></span> <span data-ttu-id="c16aa-183">Tüm disk üzerindeki verileri gereken aynı hedef sanal dizin veya depolama hesabı kökündeki gitmek için çalıştırırsanız, aynı komut /ID değerini ayrı ayrı tutma her dizin için tüm çalıştırmaları arasında aynı.</span><span class="sxs-lookup"><span data-stu-id="c16aa-183">If not all the data on the disk needs to go to the same destination virtual directory or root of the storage account, run the same command for each directory separately keeping the value of /id same across all runs.</span></span>

>[!NOTE] 
><span data-ttu-id="c16aa-184">Bu diskte verileri silme şekilde Format belirtmeyin.</span><span class="sxs-lookup"><span data-stu-id="c16aa-184">Do not specify /format as it will wipe the data on the disk.</span></span> <span data-ttu-id="c16aa-185">Belirtin / şifrelemek veya olup disk zaten veya şifrelenmiş bağlı olarak /bk.</span><span class="sxs-lookup"><span data-stu-id="c16aa-185">You can specify /encrypt or /bk depending on whether the disk is already encrypted or not.</span></span> 
>

```
    When data is already present on the disk for each drive run the following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a><span data-ttu-id="c16aa-186">Oturumlarını - Kopyala ilk sürücü</span><span class="sxs-lookup"><span data-stu-id="c16aa-186">Copy sessions - first drive</span></span>

<span data-ttu-id="c16aa-187">İlk sürücüsü için iki kez iki kaynak dizinleri kopyalamak için Azure içeri/dışarı aktarma aracını çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c16aa-187">For the first drive, run the Azure Import/Export Tool twice to copy the two source directories:</span></span>  

<span data-ttu-id="c16aa-188">**İlk kopya oturumu**</span><span class="sxs-lookup"><span data-stu-id="c16aa-188">**First copy session**</span></span>
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

<span data-ttu-id="c16aa-189">**İkinci kopya oturumu**</span><span class="sxs-lookup"><span data-stu-id="c16aa-189">**Second copy session**</span></span>

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a><span data-ttu-id="c16aa-190">Oturumlarını - Kopyala ikinci sürücü</span><span class="sxs-lookup"><span data-stu-id="c16aa-190">Copy sessions - second drive</span></span>
 
<span data-ttu-id="c16aa-191">İkinci sürücüsü için Azure içeri/dışarı aktarma aracı üç kez, bir kez her kaynak dizinler için ve bir kez tek başına Blu-Ray™ görüntü dosyası için):</span><span class="sxs-lookup"><span data-stu-id="c16aa-191">For the second drive, run the Azure Import/Export Tool three times, once each for the source directories, and once for the standalone Blu-Ray™ image file):</span></span>  
  
<span data-ttu-id="c16aa-192">**İlk kopya oturumu**</span><span class="sxs-lookup"><span data-stu-id="c16aa-192">**First copy session**</span></span> 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
<span data-ttu-id="c16aa-193">**İkinci kopya oturumu**</span><span class="sxs-lookup"><span data-stu-id="c16aa-193">**Second copy session**</span></span>

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
<span data-ttu-id="c16aa-194">**Üçüncü kopya oturumu**</span><span class="sxs-lookup"><span data-stu-id="c16aa-194">**Third copy session**</span></span>  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a><span data-ttu-id="c16aa-195">Kopya oturum tamamlama</span><span class="sxs-lookup"><span data-stu-id="c16aa-195">Copy session completion</span></span>

<span data-ttu-id="c16aa-196">Kopyalama oturumları tamamladıktan sonra iki sürücüsü kopyalama bilgisayardan bağlantısını kesmek ve uygun Windows Azure veri merkezine sevk.</span><span class="sxs-lookup"><span data-stu-id="c16aa-196">Once the copy sessions have completed, you can disconnect the two drives from the copy computer and ship them to the appropriate Windows Azure data center.</span></span> <span data-ttu-id="c16aa-197">İki günlük dosyalarını yükleyeceğiniz `FirstDrive.jrn` ve `SecondDrive.jrn`, içeri aktarma işi oluşturduğunuzda [Windows Azure Yönetim Portalı](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="c16aa-197">You'll upload the two journal files, `FirstDrive.jrn` and `SecondDrive.jrn`, when you create the import job in the [Windows Azure Management Portal](https://manage.windowsazure.com/).</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="c16aa-198">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c16aa-198">Next steps</span></span>

* [<span data-ttu-id="c16aa-199">Sabit sürücüleri içeri aktarma işine hazırlama</span><span class="sxs-lookup"><span data-stu-id="c16aa-199">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="c16aa-200">Sık kullanılan komutlar için hızlı başvuru</span><span class="sxs-lookup"><span data-stu-id="c16aa-200">Quick reference for frequently used commands</span></span>](storage-import-export-tool-quick-reference-v1.md) 
