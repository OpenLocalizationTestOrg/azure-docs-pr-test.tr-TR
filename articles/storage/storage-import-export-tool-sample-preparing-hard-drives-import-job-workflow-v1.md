---
title: "aaaSample iş akışı tooprep sabit sürücüler için bir Azure içeri/dışarı aktarma alma işi - v1 | Microsoft Docs"
description: "Sürücüleri hello Azure içeri/dışarı aktarma hizmeti, bir içeri aktarma işi hazırlama hello tam işlemi için bkz."
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
ms.openlocfilehash: f836fc6104d8b4ad5660cb110a62f61b40b0b7ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a><span data-ttu-id="a4133-103">Örnek iş akışı tooprepare sabit sürücüler içeri aktarma işi için</span><span class="sxs-lookup"><span data-stu-id="a4133-103">Sample workflow tooprepare hard drives for an import job</span></span>
<span data-ttu-id="a4133-104">Bu konu, sürücüler için içeri aktarma işi hazırlama hello tam işlemi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a4133-104">This topic walks you through hello complete process of preparing drives for an import job.</span></span>  
  
<span data-ttu-id="a4133-105">Bu örnek veri adlı bir Windows Azure depolama hesabı aşağıdaki hello alır `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="a4133-105">This example imports hello following data into a Window Azure storage account named `mystorageaccount`:</span></span>  
  
|<span data-ttu-id="a4133-106">Konum</span><span class="sxs-lookup"><span data-stu-id="a4133-106">Location</span></span>|<span data-ttu-id="a4133-107">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a4133-107">Description</span></span>|  
|--------------|-----------------|  
|<span data-ttu-id="a4133-108">H:\Video</span><span class="sxs-lookup"><span data-stu-id="a4133-108">H:\Video</span></span>|<span data-ttu-id="a4133-109">Bir koleksiyonu videoları, 5 TB toplam.</span><span class="sxs-lookup"><span data-stu-id="a4133-109">A collection of videos, 5 TB in total.</span></span>|  
|<span data-ttu-id="a4133-110">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="a4133-110">H:\Photo</span></span>|<span data-ttu-id="a4133-111">Bir koleksiyonu fotoğrafları, toplam 30 GB.</span><span class="sxs-lookup"><span data-stu-id="a4133-111">A collection of photos, 30 GB in total.</span></span>|  
|<span data-ttu-id="a4133-112">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="a4133-112">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="a4133-113">A Blu-ray™ disk görüntüsü, 25 GB.</span><span class="sxs-lookup"><span data-stu-id="a4133-113">A Blu-Ray™ disk image, 25 GB.</span></span>|  
|<span data-ttu-id="a4133-114">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="a4133-114">\\\bigshare\john\music</span></span>|<span data-ttu-id="a4133-115">Müzik dosyalarının toplam 10 GB bir ağ paylaşımında koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="a4133-115">A collection of music files on a network share, 10 GB in total.</span></span>|  
  
<span data-ttu-id="a4133-116">Merhaba alma işi hello hello depolama hesabındaki hedeflerini izleyerek bu veri aktarmak:</span><span class="sxs-lookup"><span data-stu-id="a4133-116">hello import job will import this data into hello following destinations in hello storage account:</span></span>  
  
|<span data-ttu-id="a4133-117">Kaynak</span><span class="sxs-lookup"><span data-stu-id="a4133-117">Source</span></span>|<span data-ttu-id="a4133-118">Hedef sanal dizin veya blob</span><span class="sxs-lookup"><span data-stu-id="a4133-118">Destination virtual directory or blob</span></span>|  
|------------|-------------------------------------------|  
|<span data-ttu-id="a4133-119">H:\Video</span><span class="sxs-lookup"><span data-stu-id="a4133-119">H:\Video</span></span>|<span data-ttu-id="a4133-120">https://mystorageaccount.BLOB.Core.Windows.NET/video</span><span class="sxs-lookup"><span data-stu-id="a4133-120">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="a4133-121">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="a4133-121">H:\Photo</span></span>|<span data-ttu-id="a4133-122">https://mystorageaccount.BLOB.Core.Windows.NET/Photo</span><span class="sxs-lookup"><span data-stu-id="a4133-122">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="a4133-123">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="a4133-123">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="a4133-124">https://mystorageaccount.BLOB.Core.Windows.NET/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="a4133-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="a4133-125">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="a4133-125">\\\bigshare\john\music</span></span>|<span data-ttu-id="a4133-126">https://mystorageaccount.BLOB.Core.Windows.NET/Music</span><span class="sxs-lookup"><span data-stu-id="a4133-126">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
<span data-ttu-id="a4133-127">Bu eşleme ile dosya hello `H:\Video\Drama\GreatMovie.mov` alınan toohello blob olacaktır `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="a4133-127">With this mapping, hello file `H:\Video\Drama\GreatMovie.mov` will be imported toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>  
  
<span data-ttu-id="a4133-128">Ardından, toodetermine işlem hello hello verilerin boyutunu kaç sabit sürücüler gerekli değildir:</span><span class="sxs-lookup"><span data-stu-id="a4133-128">Next, toodetermine how many hard drives are needed, compute hello size of hello data:</span></span>  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
<span data-ttu-id="a4133-129">Bu örnekte, iki 3TB sabit sürücü yeterli olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a4133-129">For this example, two 3TB hard drives should be sufficient.</span></span> <span data-ttu-id="a4133-130">Ancak, hello kaynak dizin itibaren `H:\Video` 5 TB'lık veriyi varsa ve yalnızca 3 TB, tek sabit diskin kapasitesini gerekli toobreak olan `H:\Video` çalıştırmadan önce iki küçük dizini halinde Microsoft Azure içeri/dışarı aktarma aracı hello: `H:\Video1` ve `H:\Video2`.</span><span class="sxs-lookup"><span data-stu-id="a4133-130">However, since hello source directory `H:\Video` has 5TB of data and your single hard drive's capacity is only 3TB, it's necessary toobreak `H:\Video` into two smaller directories before running hello Microsoft Azure Import/Export Tool: `H:\Video1` and `H:\Video2`.</span></span> <span data-ttu-id="a4133-131">Bu adım, kaynak dizinleri izleyen hello verir:</span><span class="sxs-lookup"><span data-stu-id="a4133-131">This step yields hello following source directories:</span></span>  
  
|<span data-ttu-id="a4133-132">Konum</span><span class="sxs-lookup"><span data-stu-id="a4133-132">Location</span></span>|<span data-ttu-id="a4133-133">Boyut</span><span class="sxs-lookup"><span data-stu-id="a4133-133">Size</span></span>|<span data-ttu-id="a4133-134">Hedef sanal dizin veya blob</span><span class="sxs-lookup"><span data-stu-id="a4133-134">Destination virtual directory or blob</span></span>|  
|--------------|----------|-------------------------------------------|  
|<span data-ttu-id="a4133-135">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="a4133-135">H:\Video1</span></span>|<span data-ttu-id="a4133-136">2.5 TB</span><span class="sxs-lookup"><span data-stu-id="a4133-136">2.5TB</span></span>|<span data-ttu-id="a4133-137">https://mystorageaccount.BLOB.Core.Windows.NET/video</span><span class="sxs-lookup"><span data-stu-id="a4133-137">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="a4133-138">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="a4133-138">H:\Video2</span></span>|<span data-ttu-id="a4133-139">2.5 TB</span><span class="sxs-lookup"><span data-stu-id="a4133-139">2.5TB</span></span>|<span data-ttu-id="a4133-140">https://mystorageaccount.BLOB.Core.Windows.NET/video</span><span class="sxs-lookup"><span data-stu-id="a4133-140">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="a4133-141">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="a4133-141">H:\Photo</span></span>|<span data-ttu-id="a4133-142">30 GB</span><span class="sxs-lookup"><span data-stu-id="a4133-142">30GB</span></span>|<span data-ttu-id="a4133-143">https://mystorageaccount.BLOB.Core.Windows.NET/Photo</span><span class="sxs-lookup"><span data-stu-id="a4133-143">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="a4133-144">K:\Temp\FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="a4133-144">K:\Temp\FavoriteMovies.ISO</span></span>|<span data-ttu-id="a4133-145">25 GB</span><span class="sxs-lookup"><span data-stu-id="a4133-145">25GB</span></span>|<span data-ttu-id="a4133-146">https://mystorageaccount.BLOB.Core.Windows.NET/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="a4133-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="a4133-147">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="a4133-147">\\\bigshare\john\music</span></span>|<span data-ttu-id="a4133-148">10GB</span><span class="sxs-lookup"><span data-stu-id="a4133-148">10GB</span></span>|<span data-ttu-id="a4133-149">https://mystorageaccount.BLOB.Core.Windows.NET/Music</span><span class="sxs-lookup"><span data-stu-id="a4133-149">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
 <span data-ttu-id="a4133-150">Rağmen hello Not `H:\Video`dizin, tootwo dizinleri bölme, toohello noktası aynı hedef sanal dizinde hello depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="a4133-150">Note that even though hello `H:\Video`directory has been split tootwo directories, they point toohello same destination virtual directory in hello storage account.</span></span> <span data-ttu-id="a4133-151">Bu şekilde tüm video dosyaları altında tek bir korunur `video` hello depolama hesabındaki kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="a4133-151">This way, all video files are maintained under a single `video` container in hello storage account.</span></span>  
  
 <span data-ttu-id="a4133-152">Ardından, dizinleri eşit olan kaynak yukarıda hello toohello iki sabit sürücü dağıtılmış:</span><span class="sxs-lookup"><span data-stu-id="a4133-152">Next, hello above source directories are evenly distributed toohello two hard drives:</span></span>  
  
||||  
|-|-|-|  
|<span data-ttu-id="a4133-153">Sabit sürücü</span><span class="sxs-lookup"><span data-stu-id="a4133-153">Hard drive</span></span>|<span data-ttu-id="a4133-154">Kaynak dizinler</span><span class="sxs-lookup"><span data-stu-id="a4133-154">Source directories</span></span>|<span data-ttu-id="a4133-155">Toplam boyutu</span><span class="sxs-lookup"><span data-stu-id="a4133-155">Total size</span></span>|  
|<span data-ttu-id="a4133-156">İlk sürücü</span><span class="sxs-lookup"><span data-stu-id="a4133-156">First Drive</span></span>|<span data-ttu-id="a4133-157">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="a4133-157">H:\Video1</span></span>|<span data-ttu-id="a4133-158">2.5 TB + 30 GB</span><span class="sxs-lookup"><span data-stu-id="a4133-158">2.5TB + 30GB</span></span>|  
||<span data-ttu-id="a4133-159">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="a4133-159">H:\Photo</span></span>||  
|<span data-ttu-id="a4133-160">İkinci sürücü</span><span class="sxs-lookup"><span data-stu-id="a4133-160">Second Drive</span></span>|<span data-ttu-id="a4133-161">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="a4133-161">H:\Video2</span></span>|<span data-ttu-id="a4133-162">2.5 TB + 35 GB</span><span class="sxs-lookup"><span data-stu-id="a4133-162">2.5TB + 35GB</span></span>|  
||<span data-ttu-id="a4133-163">K:\Temp\BlueRay.ISO</span><span class="sxs-lookup"><span data-stu-id="a4133-163">K:\Temp\BlueRay.ISO</span></span>||  
||<span data-ttu-id="a4133-164">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="a4133-164">\\\bigshare\john\music</span></span>||  
  
<span data-ttu-id="a4133-165">Ayrıca, tüm dosyalar için meta veriler aşağıdaki hello ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a4133-165">In addition, you can set hello following metadata for all files:</span></span>  
  
-   <span data-ttu-id="a4133-166">**UploadMethod:** Windows Azure içeri/dışarı aktarma hizmeti</span><span class="sxs-lookup"><span data-stu-id="a4133-166">**UploadMethod:** Windows Azure Import/Export service</span></span>  
  
-   <span data-ttu-id="a4133-167">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="a4133-167">**DataSetName:** SampleData</span></span>  
  
-   <span data-ttu-id="a4133-168">**CreationDate:** 1/10/2013</span><span class="sxs-lookup"><span data-stu-id="a4133-168">**CreationDate:** 10/1/2013</span></span>  
  
<span data-ttu-id="a4133-169">tooset meta verileri içe hello dosyaları için bir metin dosyası oluşturma `c:\WAImportExport\SampleMetadata.txt`, içeriği aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="a4133-169">tooset metadata for hello imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with hello following content:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="a4133-170">Başlangıç için bazı özellikler de ayarlayabilirsiniz `FavoriteMovie.ISO` blob:</span><span class="sxs-lookup"><span data-stu-id="a4133-170">You can also set some properties for hello `FavoriteMovie.ISO` blob:</span></span>  
  
-   <span data-ttu-id="a4133-171">**Content-Type:** application/octet-stream,</span><span class="sxs-lookup"><span data-stu-id="a4133-171">**Content-Type:** application/octet-stream</span></span>  
  
-   <span data-ttu-id="a4133-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ ==</span><span class="sxs-lookup"><span data-stu-id="a4133-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>  
  
-   <span data-ttu-id="a4133-173">**Cache-Control:** no cache</span><span class="sxs-lookup"><span data-stu-id="a4133-173">**Cache-Control:** no-cache</span></span>  
  
<span data-ttu-id="a4133-174">tooset bu özellikler bir metin dosyası oluşturma `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="a4133-174">tooset these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="a4133-175">Hazır toorun hello Azure içeri/dışarı aktarma aracı tooprepare hello iki sabit sürücü sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="a4133-175">Now you are ready toorun hello Azure Import/Export Tool tooprepare hello two hard drives.</span></span> <span data-ttu-id="a4133-176">Şunlara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="a4133-176">Note that:</span></span>  
  
-   <span data-ttu-id="a4133-177">Merhaba ilk sürücü X sürücü olarak bağlı.</span><span class="sxs-lookup"><span data-stu-id="a4133-177">hello first drive is mounted as drive X.</span></span>  
  
-   <span data-ttu-id="a4133-178">Merhaba ikinci sürücü Y sürücü olarak bağlı.</span><span class="sxs-lookup"><span data-stu-id="a4133-178">hello second drive is mounted as drive Y.</span></span>  
  
-   <span data-ttu-id="a4133-179">Merhaba depolama hesabının Hello anahtarı `mystorageaccount` olan `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span><span class="sxs-lookup"><span data-stu-id="a4133-179">hello key for hello storage account `mystorageaccount` is `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span></span>  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a><span data-ttu-id="a4133-180">Veri önceden yüklendiğinde disk alma işlemi için hazırlanıyor</span><span class="sxs-lookup"><span data-stu-id="a4133-180">Preparing disk for import when data is pre-loaded</span></span>
 
 <span data-ttu-id="a4133-181">İçeri aktarılan hello veri toobe hello diskte zaten hello bayrağı /skipwrite kullanın.</span><span class="sxs-lookup"><span data-stu-id="a4133-181">If hello data toobe imported is already present on hello disk, use hello flag /skipwrite.</span></span> <span data-ttu-id="a4133-182">/T ve /srcdir değerini alma için hazırlanan toohello disk işaret etmelidir.</span><span class="sxs-lookup"><span data-stu-id="a4133-182">Value of /t and /srcdir both should point toohello disk being prepared for import.</span></span> <span data-ttu-id="a4133-183">Tüm veri hello toogo toohello hello disk gerekir veya aynı hedef sanal dizin hello depolama hesabı, aynı komut /ID hello değerini ayrı ayrı tutma her dizin için çalışma hello kökündeki tüm çalıştırmaları arasında aynı.</span><span class="sxs-lookup"><span data-stu-id="a4133-183">If not all hello data on hello disk needs toogo toohello same destination virtual directory or root of hello storage account, run hello same command for each directory separately keeping hello value of /id same across all runs.</span></span>

>[!NOTE] 
><span data-ttu-id="a4133-184">Bunu hello diskte hello verileri silme şekilde Format belirtmeyin.</span><span class="sxs-lookup"><span data-stu-id="a4133-184">Do not specify /format as it will wipe hello data on hello disk.</span></span> <span data-ttu-id="a4133-185">Belirtin / şifrelemek veya olup hello disk zaten veya şifrelenmiş bağlı olarak /bk.</span><span class="sxs-lookup"><span data-stu-id="a4133-185">You can specify /encrypt or /bk depending on whether hello disk is already encrypted or not.</span></span> 
>

```
    When data is already present on hello disk for each drive run hello following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a><span data-ttu-id="a4133-186">Oturumlarını - Kopyala ilk sürücü</span><span class="sxs-lookup"><span data-stu-id="a4133-186">Copy sessions - first drive</span></span>

<span data-ttu-id="a4133-187">Merhaba ilk sürücü dizinleri hello Azure içeri/dışarı aktarma iki kez toocopy hello iki kaynak aracı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a4133-187">For hello first drive, run hello Azure Import/Export Tool twice toocopy hello two source directories:</span></span>  

<span data-ttu-id="a4133-188">**İlk kopya oturumu**</span><span class="sxs-lookup"><span data-stu-id="a4133-188">**First copy session**</span></span>
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

<span data-ttu-id="a4133-189">**İkinci kopya oturumu**</span><span class="sxs-lookup"><span data-stu-id="a4133-189">**Second copy session**</span></span>

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a><span data-ttu-id="a4133-190">Oturumlarını - Kopyala ikinci sürücü</span><span class="sxs-lookup"><span data-stu-id="a4133-190">Copy sessions - second drive</span></span>
 
<span data-ttu-id="a4133-191">Merhaba çalıştırmak ikinci sürücü hello Azure içeri/dışarı aktarma aracı üç kez, her hello için dizinler kaynağı ve bir kez hello tek başına Blu-Ray™ dosya görüntü bir kez):</span><span class="sxs-lookup"><span data-stu-id="a4133-191">For hello second drive, run hello Azure Import/Export Tool three times, once each for hello source directories, and once for hello standalone Blu-Ray™ image file):</span></span>  
  
<span data-ttu-id="a4133-192">**İlk kopya oturumu**</span><span class="sxs-lookup"><span data-stu-id="a4133-192">**First copy session**</span></span> 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
<span data-ttu-id="a4133-193">**İkinci kopya oturumu**</span><span class="sxs-lookup"><span data-stu-id="a4133-193">**Second copy session**</span></span>

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
<span data-ttu-id="a4133-194">**Üçüncü kopya oturumu**</span><span class="sxs-lookup"><span data-stu-id="a4133-194">**Third copy session**</span></span>  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a><span data-ttu-id="a4133-195">Kopya oturum tamamlama</span><span class="sxs-lookup"><span data-stu-id="a4133-195">Copy session completion</span></span>

<span data-ttu-id="a4133-196">Hello kopyalama oturumları tamamladıktan sonra hello iki sürücüsü hello kopyalama bilgisayardan bağlantısını kesmek ve toohello uygun Windows Azure veri merkezi sevk.</span><span class="sxs-lookup"><span data-stu-id="a4133-196">Once hello copy sessions have completed, you can disconnect hello two drives from hello copy computer and ship them toohello appropriate Windows Azure data center.</span></span> <span data-ttu-id="a4133-197">Merhaba iki günlük dosyaları, yükleyeceğiniz `FirstDrive.jrn` ve `SecondDrive.jrn`, hello hello alma işi oluşturduğunuzda [Windows Azure Yönetim Portalı](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="a4133-197">You'll upload hello two journal files, `FirstDrive.jrn` and `SecondDrive.jrn`, when you create hello import job in hello [Windows Azure Management Portal](https://manage.windowsazure.com/).</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="a4133-198">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a4133-198">Next steps</span></span>

* [<span data-ttu-id="a4133-199">Sabit sürücüleri içeri aktarma işine hazırlama</span><span class="sxs-lookup"><span data-stu-id="a4133-199">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="a4133-200">Sık kullanılan komutlar için hızlı başvuru</span><span class="sxs-lookup"><span data-stu-id="a4133-200">Quick reference for frequently used commands</span></span>](storage-import-export-tool-quick-reference-v1.md) 
