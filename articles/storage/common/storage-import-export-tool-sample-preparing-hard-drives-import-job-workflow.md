---
title: "Bir Azure içeri/dışarı aktarma alma işi sabit sürücülerini prep için örnek iş akışı | Microsoft Docs"
description: "Sürücüleri Azure içeri/dışarı aktarma hizmetindeki bir içeri aktarma işi hazırlama tam işlemi için bkz."
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
ms.openlocfilehash: 83cb82b9807718e7a509312d159eb766a5da1d2c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="sample-workflow-to-prepare-hard-drives-for-an-import-job"></a><span data-ttu-id="a8f3d-103">Sabit sürücüleri içeri aktarma işine hazırlamak için örnek iş akışı</span><span class="sxs-lookup"><span data-stu-id="a8f3d-103">Sample workflow to prepare hard drives for an import job</span></span>

<span data-ttu-id="a8f3d-104">Bu makalede, sürücüler için içeri aktarma işi hazırlama tam işlemi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a8f3d-104">This article walks you through the complete process of preparing drives for an import job.</span></span>

## <a name="sample-data"></a><span data-ttu-id="a8f3d-105">Örnek veriler</span><span class="sxs-lookup"><span data-stu-id="a8f3d-105">Sample data</span></span>

<span data-ttu-id="a8f3d-106">Bu örnek olarak aşağıdaki verileri adlı bir Azure storage hesabınıza aktarır `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="a8f3d-106">This example imports the following data into an Azure storage account named `mystorageaccount`:</span></span>

|<span data-ttu-id="a8f3d-107">Konum</span><span class="sxs-lookup"><span data-stu-id="a8f3d-107">Location</span></span>|<span data-ttu-id="a8f3d-108">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a8f3d-108">Description</span></span>|<span data-ttu-id="a8f3d-109">Veri boyutu</span><span class="sxs-lookup"><span data-stu-id="a8f3d-109">Data size</span></span>|
|--------------|-----------------|-----|
|<span data-ttu-id="a8f3d-110">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="a8f3d-110">H:\Video\\</span></span> |<span data-ttu-id="a8f3d-111">Videolar koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="a8f3d-111">A collection of videos</span></span>|<span data-ttu-id="a8f3d-112">12 TB</span><span class="sxs-lookup"><span data-stu-id="a8f3d-112">12 TB</span></span>|
|<span data-ttu-id="a8f3d-113">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="a8f3d-113">H:\Photo\\</span></span> |<span data-ttu-id="a8f3d-114">Fotoğraf koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="a8f3d-114">A collection of photos</span></span>|<span data-ttu-id="a8f3d-115">30 GB</span><span class="sxs-lookup"><span data-stu-id="a8f3d-115">30 GB</span></span>|
|<span data-ttu-id="a8f3d-116">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="a8f3d-116">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="a8f3d-117">A Blu-ray™ disk görüntüsü</span><span class="sxs-lookup"><span data-stu-id="a8f3d-117">A Blu-Ray™ disk image</span></span>|<span data-ttu-id="a8f3d-118">25 GB</span><span class="sxs-lookup"><span data-stu-id="a8f3d-118">25 GB</span></span>|
|<span data-ttu-id="a8f3d-119">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="a8f3d-119">\\\bigshare\john\music\\</span></span>|<span data-ttu-id="a8f3d-120">Müzik dosyalarını bir ağ paylaşımına koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="a8f3d-120">A collection of music files on a network share</span></span>|<span data-ttu-id="a8f3d-121">10 GB</span><span class="sxs-lookup"><span data-stu-id="a8f3d-121">10 GB</span></span>|

## <a name="storage-account-destinations"></a><span data-ttu-id="a8f3d-122">Depolama hesabı hedefleri</span><span class="sxs-lookup"><span data-stu-id="a8f3d-122">Storage account destinations</span></span>

<span data-ttu-id="a8f3d-123">İçe aktarma işi verileri depolama hesabındaki aşağıdaki hedefleri alın:</span><span class="sxs-lookup"><span data-stu-id="a8f3d-123">The import job will import the data into the following destinations in the storage account:</span></span>

|<span data-ttu-id="a8f3d-124">Kaynak</span><span class="sxs-lookup"><span data-stu-id="a8f3d-124">Source</span></span>|<span data-ttu-id="a8f3d-125">Hedef sanal dizin veya blob</span><span class="sxs-lookup"><span data-stu-id="a8f3d-125">Destination virtual directory or blob</span></span>|
|------------|-------------------------------------------|
|<span data-ttu-id="a8f3d-126">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="a8f3d-126">H:\Video\\</span></span> |<span data-ttu-id="a8f3d-127">Video /</span><span class="sxs-lookup"><span data-stu-id="a8f3d-127">video/</span></span>|
|<span data-ttu-id="a8f3d-128">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="a8f3d-128">H:\Photo\\</span></span> |<span data-ttu-id="a8f3d-129">Fotoğraf /</span><span class="sxs-lookup"><span data-stu-id="a8f3d-129">photo/</span></span>|
|<span data-ttu-id="a8f3d-130">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="a8f3d-130">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="a8f3d-131">favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="a8f3d-131">favorite/FavoriteMovies.ISO</span></span>|
|<span data-ttu-id="a8f3d-132">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="a8f3d-132">\\\bigshare\john\music\\</span></span> |<span data-ttu-id="a8f3d-133">Müzik</span><span class="sxs-lookup"><span data-stu-id="a8f3d-133">music</span></span>|

<span data-ttu-id="a8f3d-134">Bu eşleme, dosya ile `H:\Video\Drama\GreatMovie.mov` blob içeri aktarılacak `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="a8f3d-134">With this mapping, the file `H:\Video\Drama\GreatMovie.mov` will be imported to the blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>

## <a name="determine-hard-drive-requirements"></a><span data-ttu-id="a8f3d-135">Sabit sürücü gereksinimlerini belirleyin</span><span class="sxs-lookup"><span data-stu-id="a8f3d-135">Determine hard drive requirements</span></span>

<span data-ttu-id="a8f3d-136">Ardından, kaç tane sabit sürücüler gerekli belirlemek için verilerin boyutunu hesaplama:</span><span class="sxs-lookup"><span data-stu-id="a8f3d-136">Next, to determine how many hard drives are needed, compute the size of the data:</span></span>

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

<span data-ttu-id="a8f3d-137">Bu örnekte, iki 8TB sabit sürücü yeterli olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a8f3d-137">For this example, two 8TB hard drives should be sufficient.</span></span> <span data-ttu-id="a8f3d-138">Ancak, kaynak dizin itibaren `H:\Video` yalnızca 8 TB, tek sabit diskin kapasitesini 12 TB'lık veriyi sahipse ve bu yolla da aşağıdakileri belirtin kuramaz **driveset.csv** dosyası:</span><span class="sxs-lookup"><span data-stu-id="a8f3d-138">However, since the source directory `H:\Video` has 12TB of data and your single hard drive's capacity is only 8TB, you will be able to specify this in the following way in the **driveset.csv** file:</span></span>

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
<span data-ttu-id="a8f3d-139">Aracın en iyi duruma getirilmiş bir şekilde iki sabit sürücüde veri dağıtın.</span><span class="sxs-lookup"><span data-stu-id="a8f3d-139">The tool will distribute data across two hard drives in an optimized way.</span></span>

## <a name="attach-drives-and-configure-the-job"></a><span data-ttu-id="a8f3d-140">Sürücüleri bağlayın ve iş yapılandırın</span><span class="sxs-lookup"><span data-stu-id="a8f3d-140">Attach drives and configure the job</span></span>
<span data-ttu-id="a8f3d-141">Her iki diskin makineye ekleyebilir ve birimler oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="a8f3d-141">You will attach both disks to the machine and create volumes.</span></span> <span data-ttu-id="a8f3d-142">Ardından Yazar **dataset.csv** dosyası:</span><span class="sxs-lookup"><span data-stu-id="a8f3d-142">Then author **dataset.csv** file:</span></span>
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

<span data-ttu-id="a8f3d-143">Ayrıca, aşağıdaki meta verileri tüm dosyalar için ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a8f3d-143">In addition, you can set the following metadata for all files:</span></span>

* <span data-ttu-id="a8f3d-144">**UploadMethod:** Windows Azure içeri/dışarı aktarma hizmeti</span><span class="sxs-lookup"><span data-stu-id="a8f3d-144">**UploadMethod:** Windows Azure Import/Export service</span></span>
* <span data-ttu-id="a8f3d-145">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="a8f3d-145">**DataSetName:** SampleData</span></span>
* <span data-ttu-id="a8f3d-146">**CreationDate:** 1/10/2013</span><span class="sxs-lookup"><span data-stu-id="a8f3d-146">**CreationDate:** 10/1/2013</span></span>

<span data-ttu-id="a8f3d-147">İçeri aktarılan dosyalar için meta veri ayarlamak için bir metin dosyası oluşturun `c:\WAImportExport\SampleMetadata.txt`, aşağıdaki içeriğe sahip:</span><span class="sxs-lookup"><span data-stu-id="a8f3d-147">To set metadata for the imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with the following content:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="a8f3d-148">Bazı özellikler için de ayarlayabilirsiniz `FavoriteMovie.ISO` blob:</span><span class="sxs-lookup"><span data-stu-id="a8f3d-148">You can also set some properties for the `FavoriteMovie.ISO` blob:</span></span>

* <span data-ttu-id="a8f3d-149">**Content-Type:** application/octet-stream,</span><span class="sxs-lookup"><span data-stu-id="a8f3d-149">**Content-Type:** application/octet-stream</span></span>
* <span data-ttu-id="a8f3d-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ ==</span><span class="sxs-lookup"><span data-stu-id="a8f3d-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>
* <span data-ttu-id="a8f3d-151">**Cache-Control:** no cache</span><span class="sxs-lookup"><span data-stu-id="a8f3d-151">**Cache-Control:** no-cache</span></span>

<span data-ttu-id="a8f3d-152">Bu özellikleri ayarlamak için bir metin dosyası oluşturun `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="a8f3d-152">To set these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-the-azure-importexport-tool-waimportexportexe"></a><span data-ttu-id="a8f3d-153">Azure içeri/dışarı aktarma Aracı (WAImportExport.exe) çalıştırın</span><span class="sxs-lookup"><span data-stu-id="a8f3d-153">Run the Azure Import/Export Tool (WAImportExport.exe)</span></span>

<span data-ttu-id="a8f3d-154">Şimdi iki sabit sürücü hazırlamak için Azure içeri/dışarı aktarma aracını çalıştırmak hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="a8f3d-154">Now you are ready to run the Azure Import/Export Tool to prepare the two hard drives.</span></span>

<span data-ttu-id="a8f3d-155">**İlk oturum için:**</span><span class="sxs-lookup"><span data-stu-id="a8f3d-155">**For the first session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

<span data-ttu-id="a8f3d-156">Daha fazla veri eklenmesi gerekiyorsa, başka bir veri kümesi dosyasını (Initialdataset ile aynı biçimi) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a8f3d-156">If any more data needs to be added, create another dataset file (same format as Initialdataset).</span></span>

<span data-ttu-id="a8f3d-157">**İkinci oturum için:**</span><span class="sxs-lookup"><span data-stu-id="a8f3d-157">**For the second session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

<span data-ttu-id="a8f3d-158">Kopyalama oturumları tamamladıktan sonra iki sürücü kopyalama bilgisayardan bağlantısını kesmek ve uygun Azure veri merkezine sevk.</span><span class="sxs-lookup"><span data-stu-id="a8f3d-158">Once the copy sessions have completed, you can disconnect the two drives from the copy computer and ship them to the appropriate Azure data center.</span></span> <span data-ttu-id="a8f3d-159">İki günlük dosyalarını yükleyeceğiniz `<FirstDriveSerialNumber>.xml` ve `<SecondDriveSerialNumber>.xml`, Azure portalında alma işi oluşturduğunuzda.</span><span class="sxs-lookup"><span data-stu-id="a8f3d-159">You'll upload the two journal files, `<FirstDriveSerialNumber>.xml` and `<SecondDriveSerialNumber>.xml`, when you create the import job in the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8f3d-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a8f3d-160">Next steps</span></span>

* [<span data-ttu-id="a8f3d-161">Sabit sürücüleri içeri aktarma işine hazırlama</span><span class="sxs-lookup"><span data-stu-id="a8f3d-161">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import.md)
* [<span data-ttu-id="a8f3d-162">Sık kullanılan komutlar için hızlı başvuru</span><span class="sxs-lookup"><span data-stu-id="a8f3d-162">Quick reference for frequently used commands</span></span>](../storage-import-export-tool-quick-reference.md)
