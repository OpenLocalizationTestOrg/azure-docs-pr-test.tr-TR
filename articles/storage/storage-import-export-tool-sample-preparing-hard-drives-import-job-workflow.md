---
title: "aaaSample iş akışı tooprep sabit sürücüler için bir Azure içeri/dışarı aktarma alma işi | Microsoft Docs"
description: "Sürücüleri hello Azure içeri/dışarı aktarma hizmeti, bir içeri aktarma işi hazırlama hello tam işlemi için bkz."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: muralikk
ms.openlocfilehash: 560220b7dc9f87416f1fec1ff30fa5cd65812ce5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a><span data-ttu-id="11039-103">Örnek iş akışı tooprepare sabit sürücüler içeri aktarma işi için</span><span class="sxs-lookup"><span data-stu-id="11039-103">Sample workflow tooprepare hard drives for an import job</span></span>

<span data-ttu-id="11039-104">Bu makalede, sürücüler için içeri aktarma işi hazırlama hello tam işlemi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="11039-104">This article walks you through hello complete process of preparing drives for an import job.</span></span>

## <a name="sample-data"></a><span data-ttu-id="11039-105">Örnek veriler</span><span class="sxs-lookup"><span data-stu-id="11039-105">Sample data</span></span>

<span data-ttu-id="11039-106">Bu örnek veri adlı bir Azure storage hesabınıza aşağıdaki hello alır `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="11039-106">This example imports hello following data into an Azure storage account named `mystorageaccount`:</span></span>

|<span data-ttu-id="11039-107">Konum</span><span class="sxs-lookup"><span data-stu-id="11039-107">Location</span></span>|<span data-ttu-id="11039-108">Açıklama</span><span class="sxs-lookup"><span data-stu-id="11039-108">Description</span></span>|<span data-ttu-id="11039-109">Veri boyutu</span><span class="sxs-lookup"><span data-stu-id="11039-109">Data size</span></span>|
|--------------|-----------------|-----|
|<span data-ttu-id="11039-110">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="11039-110">H:\Video\\</span></span> |<span data-ttu-id="11039-111">Videolar koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="11039-111">A collection of videos</span></span>|<span data-ttu-id="11039-112">12 TB</span><span class="sxs-lookup"><span data-stu-id="11039-112">12 TB</span></span>|
|<span data-ttu-id="11039-113">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="11039-113">H:\Photo\\</span></span> |<span data-ttu-id="11039-114">Fotoğraf koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="11039-114">A collection of photos</span></span>|<span data-ttu-id="11039-115">30 GB</span><span class="sxs-lookup"><span data-stu-id="11039-115">30 GB</span></span>|
|<span data-ttu-id="11039-116">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="11039-116">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="11039-117">A Blu-ray™ disk görüntüsü</span><span class="sxs-lookup"><span data-stu-id="11039-117">A Blu-Ray™ disk image</span></span>|<span data-ttu-id="11039-118">25 GB</span><span class="sxs-lookup"><span data-stu-id="11039-118">25 GB</span></span>|
|<span data-ttu-id="11039-119">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="11039-119">\\\bigshare\john\music\\</span></span>|<span data-ttu-id="11039-120">Müzik dosyalarını bir ağ paylaşımına koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="11039-120">A collection of music files on a network share</span></span>|<span data-ttu-id="11039-121">10 GB</span><span class="sxs-lookup"><span data-stu-id="11039-121">10 GB</span></span>|

## <a name="storage-account-destinations"></a><span data-ttu-id="11039-122">Depolama hesabı hedefleri</span><span class="sxs-lookup"><span data-stu-id="11039-122">Storage account destinations</span></span>

<span data-ttu-id="11039-123">Merhaba alma işi hello depolama hesabındaki hedeflerini izleyerek hello hello veri aktarmak:</span><span class="sxs-lookup"><span data-stu-id="11039-123">hello import job will import hello data into hello following destinations in hello storage account:</span></span>

|<span data-ttu-id="11039-124">Kaynak</span><span class="sxs-lookup"><span data-stu-id="11039-124">Source</span></span>|<span data-ttu-id="11039-125">Hedef sanal dizin veya blob</span><span class="sxs-lookup"><span data-stu-id="11039-125">Destination virtual directory or blob</span></span>|
|------------|-------------------------------------------|
|<span data-ttu-id="11039-126">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="11039-126">H:\Video\\</span></span> |<span data-ttu-id="11039-127">Video /</span><span class="sxs-lookup"><span data-stu-id="11039-127">video/</span></span>|
|<span data-ttu-id="11039-128">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="11039-128">H:\Photo\\</span></span> |<span data-ttu-id="11039-129">Fotoğraf /</span><span class="sxs-lookup"><span data-stu-id="11039-129">photo/</span></span>|
|<span data-ttu-id="11039-130">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="11039-130">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="11039-131">favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="11039-131">favorite/FavoriteMovies.ISO</span></span>|
|<span data-ttu-id="11039-132">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="11039-132">\\\bigshare\john\music\\</span></span> |<span data-ttu-id="11039-133">Müzik</span><span class="sxs-lookup"><span data-stu-id="11039-133">music</span></span>|

<span data-ttu-id="11039-134">Bu eşleme ile dosya hello `H:\Video\Drama\GreatMovie.mov` alınan toohello blob olacaktır `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="11039-134">With this mapping, hello file `H:\Video\Drama\GreatMovie.mov` will be imported toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>

## <a name="determine-hard-drive-requirements"></a><span data-ttu-id="11039-135">Sabit sürücü gereksinimlerini belirleyin</span><span class="sxs-lookup"><span data-stu-id="11039-135">Determine hard drive requirements</span></span>

<span data-ttu-id="11039-136">Ardından, toodetermine işlem hello hello verilerin boyutunu kaç sabit sürücüler gerekli değildir:</span><span class="sxs-lookup"><span data-stu-id="11039-136">Next, toodetermine how many hard drives are needed, compute hello size of hello data:</span></span>

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

<span data-ttu-id="11039-137">Bu örnekte, iki 8TB sabit sürücü yeterli olacaktır.</span><span class="sxs-lookup"><span data-stu-id="11039-137">For this example, two 8TB hard drives should be sufficient.</span></span> <span data-ttu-id="11039-138">Ancak, hello kaynak dizin itibaren `H:\Video` 12 TB'lık veriyi varsa ve yalnızca 8 TB, tek sabit diskin kapasitesini mümkün toospecify bu olacaktır hello hello şekilde aşağıdaki **driveset.csv** dosya:</span><span class="sxs-lookup"><span data-stu-id="11039-138">However, since hello source directory `H:\Video` has 12TB of data and your single hard drive's capacity is only 8TB, you will be able toospecify this in hello following way in hello **driveset.csv** file:</span></span>

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
<span data-ttu-id="11039-139">Merhaba aracı en iyi duruma getirilmiş bir şekilde iki sabit sürücüde veri dağıtın.</span><span class="sxs-lookup"><span data-stu-id="11039-139">hello tool will distribute data across two hard drives in an optimized way.</span></span>

## <a name="attach-drives-and-configure-hello-job"></a><span data-ttu-id="11039-140">Sürücüleri bağlayın ve hello iş yapılandırın</span><span class="sxs-lookup"><span data-stu-id="11039-140">Attach drives and configure hello job</span></span>
<span data-ttu-id="11039-141">Her iki diskleri toohello makine ekleme ve birimler oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="11039-141">You will attach both disks toohello machine and create volumes.</span></span> <span data-ttu-id="11039-142">Ardından Yazar **dataset.csv** dosyası:</span><span class="sxs-lookup"><span data-stu-id="11039-142">Then author **dataset.csv** file:</span></span>
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

<span data-ttu-id="11039-143">Ayrıca, tüm dosyalar için meta veriler aşağıdaki hello ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="11039-143">In addition, you can set hello following metadata for all files:</span></span>

* <span data-ttu-id="11039-144">**UploadMethod:** Windows Azure içeri/dışarı aktarma hizmeti</span><span class="sxs-lookup"><span data-stu-id="11039-144">**UploadMethod:** Windows Azure Import/Export service</span></span>
* <span data-ttu-id="11039-145">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="11039-145">**DataSetName:** SampleData</span></span>
* <span data-ttu-id="11039-146">**CreationDate:** 1/10/2013</span><span class="sxs-lookup"><span data-stu-id="11039-146">**CreationDate:** 10/1/2013</span></span>

<span data-ttu-id="11039-147">tooset meta verileri içe hello dosyaları için bir metin dosyası oluşturma `c:\WAImportExport\SampleMetadata.txt`, içeriği aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="11039-147">tooset metadata for hello imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with hello following content:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="11039-148">Başlangıç için bazı özellikler de ayarlayabilirsiniz `FavoriteMovie.ISO` blob:</span><span class="sxs-lookup"><span data-stu-id="11039-148">You can also set some properties for hello `FavoriteMovie.ISO` blob:</span></span>

* <span data-ttu-id="11039-149">**Content-Type:** application/octet-stream,</span><span class="sxs-lookup"><span data-stu-id="11039-149">**Content-Type:** application/octet-stream</span></span>
* <span data-ttu-id="11039-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ ==</span><span class="sxs-lookup"><span data-stu-id="11039-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>
* <span data-ttu-id="11039-151">**Cache-Control:** no cache</span><span class="sxs-lookup"><span data-stu-id="11039-151">**Cache-Control:** no-cache</span></span>

<span data-ttu-id="11039-152">tooset bu özellikler bir metin dosyası oluşturma `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="11039-152">tooset these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-hello-azure-importexport-tool-waimportexportexe"></a><span data-ttu-id="11039-153">Çalışma hello Azure içeri/dışarı aktarma Aracı (WAImportExport.exe)</span><span class="sxs-lookup"><span data-stu-id="11039-153">Run hello Azure Import/Export Tool (WAImportExport.exe)</span></span>

<span data-ttu-id="11039-154">Hazır toorun hello Azure içeri/dışarı aktarma aracı tooprepare hello iki sabit sürücü sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="11039-154">Now you are ready toorun hello Azure Import/Export Tool tooprepare hello two hard drives.</span></span>

<span data-ttu-id="11039-155">**Merhaba ilk oturum için:**</span><span class="sxs-lookup"><span data-stu-id="11039-155">**For hello first session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

<span data-ttu-id="11039-156">Daha fazla veri eklenen toobe gerekirse, başka bir veri kümesi dosyasını (Initialdataset ile aynı biçimi) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="11039-156">If any more data needs toobe added, create another dataset file (same format as Initialdataset).</span></span>

<span data-ttu-id="11039-157">**Merhaba ikinci oturumu için:**</span><span class="sxs-lookup"><span data-stu-id="11039-157">**For hello second session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

<span data-ttu-id="11039-158">Merhaba kopyalama oturumları tamamladıktan sonra hello iki sürücüsü hello kopyalama bilgisayardan çıkarın ve toohello uygun Azure veri merkezi sevk.</span><span class="sxs-lookup"><span data-stu-id="11039-158">Once hello copy sessions have completed, you can disconnect hello two drives from hello copy computer and ship them toohello appropriate Azure data center.</span></span> <span data-ttu-id="11039-159">Merhaba iki günlük dosyaları, yükleyeceğiniz `<FirstDriveSerialNumber>.xml` ve `<SecondDriveSerialNumber>.xml`, hello Azure portal hello alma işi oluşturduğunuzda.</span><span class="sxs-lookup"><span data-stu-id="11039-159">You'll upload hello two journal files, `<FirstDriveSerialNumber>.xml` and `<SecondDriveSerialNumber>.xml`, when you create hello import job in hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11039-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="11039-160">Next steps</span></span>

* [<span data-ttu-id="11039-161">Sabit sürücüleri içeri aktarma işine hazırlama</span><span class="sxs-lookup"><span data-stu-id="11039-161">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import.md)
* [<span data-ttu-id="11039-162">Sık kullanılan komutlar için hızlı başvuru</span><span class="sxs-lookup"><span data-stu-id="11039-162">Quick reference for frequently used commands</span></span>](storage-import-export-tool-quick-reference.md)
