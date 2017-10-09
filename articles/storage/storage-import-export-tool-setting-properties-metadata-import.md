---
title: "aaaSetting özellikleri ve Azure içeri/dışarı aktarma kullanarak meta verilerini | Microsoft Docs"
description: "Hello Azure içeri/dışarı aktarma aracı tooprepare sürücülerinizin çalıştırırken toospecify özellikleri ve meta veriler toobe hello hedef BLOB'ları üzerinde nasıl ayarlanacağını öğrenin."
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
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 05c2b13bead793c8ab5aac6ce25816be97fffb14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-properties-and-metadata-during-hello-import-process"></a><span data-ttu-id="4cc19-103">Özellikleri ayarlama ve hello sırasında meta veri alma işlemi</span><span class="sxs-lookup"><span data-stu-id="4cc19-103">Setting properties and metadata during hello import process</span></span>

<span data-ttu-id="4cc19-104">Merhaba Microsoft Azure içeri/dışarı aktarma aracı tooprepare sürücülerinizin çalıştırdığınızda, özellikleri ve meta veri toobe hello hedef BLOB'ları üzerinde ayarlamak belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4cc19-104">When you run hello Microsoft Azure Import/Export Tool tooprepare your drives, you can specify properties and metadata toobe set on hello destination blobs.</span></span> <span data-ttu-id="4cc19-105">Şu adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="4cc19-105">Follow these steps:</span></span>

1.  <span data-ttu-id="4cc19-106">tooset blob özellikleri, özellik adları ve değerleri belirtir, yerel bilgisayarınızda bir metin dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4cc19-106">tooset blob properties, create a text file on your local computer that specifies property names and values.</span></span>
2.  <span data-ttu-id="4cc19-107">tooset meta verileri blob, meta veri adları ve değerleri belirtir, yerel bilgisayarınızda bir metin dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4cc19-107">tooset blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>
3.  <span data-ttu-id="4cc19-108">Merhaba tam yolu tooone veya bu dosyaları toohello Azure içeri/dışarı aktarma aracı her ikisi de hello bir parçası olarak geçirin `PrepImport` işlemi.</span><span class="sxs-lookup"><span data-stu-id="4cc19-108">Pass hello full path tooone or both of these files toohello Azure Import/Export Tool as part of hello `PrepImport` operation.</span></span>

> [!NOTE]
>  <span data-ttu-id="4cc19-109">Özellikler veya meta veri dosya kopyalama oturumun bir parçası belirttiğinizde, bu kopya oturumu bir parçası olarak alınan her blob için bu özellikleri veya meta veriler ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="4cc19-109">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="4cc19-110">İçeri aktarılan hello BLOB'ları bazıları için toospecify özellikleri veya meta veriler farklı bir kümesini istiyorsanız, ayrı bir kopyalama farklı özellikleri veya meta veri dosyaları oturumla toocreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="4cc19-110">If you want toospecify a different set of properties or metadata for some of hello blobs being imported, you'll need toocreate a separate copy session with different properties or metadata files.</span></span>

## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="4cc19-111">Bir metin dosyasına BLOB özellikleri belirtin</span><span class="sxs-lookup"><span data-stu-id="4cc19-111">Specify blob properties in a text file</span></span>

<span data-ttu-id="4cc19-112">toospecify blob özellikleri, bir yerel metin dosyası oluşturun ve öğeleri ve değerleri olarak özellik değerleri olarak özellik adlarını belirtir XML içerir.</span><span class="sxs-lookup"><span data-stu-id="4cc19-112">toospecify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="4cc19-113">Bazı özellik değerleri belirten örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="4cc19-113">Here's an example that specifies some property values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

<span data-ttu-id="4cc19-114">Merhaba dosya tooa yerel bir konum gibi kaydetmek `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="4cc19-114">Save hello file tooa local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>

## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="4cc19-115">Bir metin dosyasına BLOB meta verileri belirtin</span><span class="sxs-lookup"><span data-stu-id="4cc19-115">Specify blob metadata in a text file</span></span>

<span data-ttu-id="4cc19-116">Benzer şekilde, toospecify meta verileri blob, meta veri adlarının öğeleri ve meta veri değerlerinin değerler olarak olarak belirten bir yerel metin dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4cc19-116">Similarly, toospecify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="4cc19-117">Bazı meta veri değerleri belirten örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="4cc19-117">Here's an example that specifies some metadata values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="4cc19-118">Merhaba dosya tooa yerel bir konum gibi kaydetmek `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="4cc19-118">Save hello file tooa local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>

## <a name="add-hello-path-tooproperties-and-metadata-files-in-datasetcsv"></a><span data-ttu-id="4cc19-119">İçinde dataset.csv Hello yolu tooproperties ve meta veri dosyaları Ekle</span><span class="sxs-lookup"><span data-stu-id="4cc19-119">Add hello path tooproperties and metadata files in dataset.csv</span></span>

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,https://mystorageaccount.blob.core.windows.net/video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,https://mystorageaccount.blob.core.windows.net/photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,https://mystorageaccount.blob.core.windows.net/music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

## <a name="next-steps"></a><span data-ttu-id="4cc19-120">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4cc19-120">Next steps</span></span>

* [<span data-ttu-id="4cc19-121">İçeri/Dışarı Aktarma hizmeti meta veriler ve özellikler dosyası biçimi</span><span class="sxs-lookup"><span data-stu-id="4cc19-121">Import/Export service metadata and properties file format</span></span>](storage-import-export-file-format-metadata-and-properties.md)
