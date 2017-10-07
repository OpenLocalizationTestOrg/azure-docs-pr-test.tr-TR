---
title: "aaaSetting özellikleri ve Azure içeri/dışarı aktarma - v1 kullanarak meta verilerini | Microsoft Docs"
description: "Hello Azure içeri/dışarı aktarma aracı tooprepare sürücülerinizin çalıştırırken toospecify özellikleri ve meta veriler toobe hello hedef BLOB'ları üzerinde nasıl ayarlanacağını öğrenin. Merhaba içeri/dışarı aktarma aracı toov1 başvuruyor."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: e8541695-bcfb-4bf0-84d9-72c9de32a0a8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 5b7b1c346ecde8a26d985bd5de7efcf7d86eb9e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-properties-and-metadata-during-hello-import-process"></a><span data-ttu-id="d1b10-104">Özellikleri ayarlama ve hello sırasında meta veri alma işlemi</span><span class="sxs-lookup"><span data-stu-id="d1b10-104">Setting properties and metadata during hello import process</span></span>
<span data-ttu-id="d1b10-105">Merhaba Microsoft Azure içeri/dışarı aktarma aracı tooprepare sürücülerinizin çalıştırdığınızda, özellikleri ve meta veri toobe hello hedef BLOB'ları üzerinde ayarlamak belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1b10-105">When you run hello Microsoft Azure Import/Export Tool tooprepare your drives, you can specify properties and metadata toobe set on hello destination blobs.</span></span> <span data-ttu-id="d1b10-106">Şu adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="d1b10-106">Follow these steps:</span></span>  
  
1.  <span data-ttu-id="d1b10-107">tooset blob özellikleri, özellik adları ve değerleri belirtir, yerel bilgisayarınızda bir metin dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d1b10-107">tooset blob properties, create a text file on your local computer that specifies property names and values.</span></span>  
  
2.  <span data-ttu-id="d1b10-108">tooset meta verileri blob, meta veri adları ve değerleri belirtir, yerel bilgisayarınızda bir metin dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d1b10-108">tooset blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>  
  
3.  <span data-ttu-id="d1b10-109">Merhaba tam yolu tooone veya bu dosyaları toohello Azure içeri/dışarı aktarma aracı her ikisi de hello bir parçası olarak geçirin `PrepImport` işlemi.</span><span class="sxs-lookup"><span data-stu-id="d1b10-109">Pass hello full path tooone or both of these files toohello Azure Import/Export Tool as part of hello `PrepImport` operation.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="d1b10-110">Özellikler veya meta veri dosya kopyalama oturumun bir parçası belirttiğinizde, bu kopya oturumu bir parçası olarak alınan her blob için bu özellikleri veya meta veriler ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="d1b10-110">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="d1b10-111">İçeri aktarılan hello BLOB'ları bazıları için toospecify özellikleri veya meta veriler farklı bir kümesini istiyorsanız, ayrı bir kopyalama farklı özellikleri veya meta veri dosyaları oturumla toocreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="d1b10-111">If you want toospecify a different set of properties or metadata for some of hello blobs being imported, you'll need toocreate a separate copy session with different properties or metadata files.</span></span>  
  
## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="d1b10-112">Bir metin dosyasına BLOB özellikleri belirtin</span><span class="sxs-lookup"><span data-stu-id="d1b10-112">Specify Blob Properties in a Text File</span></span>  
<span data-ttu-id="d1b10-113">toospecify blob özellikleri, bir yerel metin dosyası oluşturun ve öğeleri ve değerleri olarak özellik değerleri olarak özellik adlarını belirtir XML içerir.</span><span class="sxs-lookup"><span data-stu-id="d1b10-113">toospecify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="d1b10-114">Bazı özellik değerleri belirten örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d1b10-114">Here's an example that specifies some property values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="d1b10-115">Merhaba dosya tooa yerel bir konum gibi kaydetmek `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="d1b10-115">Save hello file tooa local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>  
  
## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="d1b10-116">Bir metin dosyasına BLOB meta verileri belirtin</span><span class="sxs-lookup"><span data-stu-id="d1b10-116">Specify Blob Metadata in a Text File</span></span>  
<span data-ttu-id="d1b10-117">Benzer şekilde, toospecify meta verileri blob, meta veri adlarının öğeleri ve meta veri değerlerinin değerler olarak olarak belirten bir yerel metin dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d1b10-117">Similarly, toospecify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="d1b10-118">Bazı meta veri değerleri belirten örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d1b10-118">Here's an example that specifies some metadata values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="d1b10-119">Merhaba dosya tooa yerel bir konum gibi kaydetmek `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="d1b10-119">Save hello file tooa local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>  
  
## <a name="create-a-copy-session-including-hello-properties-or-metadata-files"></a><span data-ttu-id="d1b10-120">Oturum kopyalama dahil olmak üzere hello özellikleri veya meta veri dosyaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="d1b10-120">Create a Copy Session Including hello Properties or Metadata Files</span></span>  
<span data-ttu-id="d1b10-121">Hello Azure içeri/dışarı aktarma aracı tooprepare hello alma işi çalıştırdığınızda, hello komut satırında hello kullanarak hello özellikleri dosya belirtin `PropertyFile` parametresi.</span><span class="sxs-lookup"><span data-stu-id="d1b10-121">When you run hello Azure Import/Export Tool tooprepare hello import job, specify hello properties file on hello command line using hello `PropertyFile` parameter.</span></span> <span data-ttu-id="d1b10-122">Merhaba meta veri dosyası hello komut satırında hello kullanarak belirtin `/MetadataFile` parametresi.</span><span class="sxs-lookup"><span data-stu-id="d1b10-122">Specify hello metadata file on hello command line using hello `/MetadataFile` parameter.</span></span> <span data-ttu-id="d1b10-123">Her iki dosya belirten örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d1b10-123">Here's an example that specifies both files:</span></span>  
  
```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```
  
## <a name="next-steps"></a><span data-ttu-id="d1b10-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d1b10-124">Next steps</span></span>

* [<span data-ttu-id="d1b10-125">İçeri/Dışarı Aktarma hizmeti meta veriler ve özellikler dosyası biçimi</span><span class="sxs-lookup"><span data-stu-id="d1b10-125">Import/Export service metadata and properties file format</span></span>](../storage-import-export-file-format-metadata-and-properties.md)
