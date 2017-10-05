---
title: "Özellikleri ve Azure içeri/dışarı aktarma - v1 kullanarak meta verileri ayarlama | Microsoft Docs"
description: "Özellikler ve hedef BLOB'ları üzerinde Azure içeri/dışarı aktarma Aracı çalıştırırken sürücülerinizin hazırlamak için ayarlanacak meta veri belirtin öğrenin. İçeri/Dışarı Aktarma Aracı'nın v1 başvuruyor."
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
ms.openlocfilehash: 77bdaa5559de86cd1de9f30e70656e47fd5719e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="setting-properties-and-metadata-during-the-import-process"></a><span data-ttu-id="9d0da-104">İçeri aktarma işlemi sırasında özellikleri ve meta verileri ayarlama</span><span class="sxs-lookup"><span data-stu-id="9d0da-104">Setting properties and metadata during the import process</span></span>
<span data-ttu-id="9d0da-105">Sürücülerinizin hazırlamak üzere Microsoft Azure içeri/dışarı aktarma aracı çalıştırdığınızda, özellikleri ve hedef BLOB'ları üzerinde ayarlamak için meta veriler belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9d0da-105">When you run the Microsoft Azure Import/Export Tool to prepare your drives, you can specify properties and metadata to be set on the destination blobs.</span></span> <span data-ttu-id="9d0da-106">Şu adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="9d0da-106">Follow these steps:</span></span>  
  
1.  <span data-ttu-id="9d0da-107">BLOB özelliklerini ayarlamak için özellik adları ve değerleri belirtir, yerel bilgisayarınızda bir metin dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9d0da-107">To set blob properties, create a text file on your local computer that specifies property names and values.</span></span>  
  
2.  <span data-ttu-id="9d0da-108">BLOB meta verileri ayarlamak için yerel bilgisayarınızda meta verileri adları ve değerleri bir metin dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9d0da-108">To set blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>  
  
3.  <span data-ttu-id="9d0da-109">Bir parçası olarak geçişi birini veya her ikisini Azure içeri/dışarı aktarma aracı için bu dosyalar için tam yolu `PrepImport` işlemi.</span><span class="sxs-lookup"><span data-stu-id="9d0da-109">Pass the full path to one or both of these files to the Azure Import/Export Tool as part of the `PrepImport` operation.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="9d0da-110">Özellikler veya meta veri dosya kopyalama oturumun bir parçası belirttiğinizde, bu kopya oturumu bir parçası olarak alınan her blob için bu özellikleri veya meta veriler ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="9d0da-110">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="9d0da-111">İçeri aktarılan BLOB'ları bazıları için özellikleri veya meta veriler farklı bir kümesini belirtmek istiyorsanız, farklı özellikleri veya meta veri dosyaları ile ayrı kopya oturumu oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9d0da-111">If you want to specify a different set of properties or metadata for some of the blobs being imported, you'll need to create a separate copy session with different properties or metadata files.</span></span>  
  
## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="9d0da-112">Bir metin dosyasına BLOB özellikleri belirtin</span><span class="sxs-lookup"><span data-stu-id="9d0da-112">Specify Blob Properties in a Text File</span></span>  
<span data-ttu-id="9d0da-113">BLOB özelliklerini belirtmek için bir yerel metin dosyası oluşturun ve öğeleri ve değerleri olarak özellik değerleri olarak özellik adlarını belirtir XML içerir.</span><span class="sxs-lookup"><span data-stu-id="9d0da-113">To specify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="9d0da-114">Bazı özellik değerleri belirten örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="9d0da-114">Here's an example that specifies some property values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="9d0da-115">Dosya gibi yerel bir konuma kaydetmeniz `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="9d0da-115">Save the file to a local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>  
  
## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="9d0da-116">Bir metin dosyasına BLOB meta verileri belirtin</span><span class="sxs-lookup"><span data-stu-id="9d0da-116">Specify Blob Metadata in a Text File</span></span>  
<span data-ttu-id="9d0da-117">Benzer şekilde, blob meta verileri belirtmek için meta veri adlarının öğeleri ve meta veri değerlerinin değerler olarak olarak belirten bir yerel metin dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9d0da-117">Similarly, to specify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="9d0da-118">Bazı meta veri değerleri belirten örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="9d0da-118">Here's an example that specifies some metadata values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="9d0da-119">Dosya gibi yerel bir konuma kaydetmeniz `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="9d0da-119">Save the file to a local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>  
  
## <a name="create-a-copy-session-including-the-properties-or-metadata-files"></a><span data-ttu-id="9d0da-120">Özellikler veya meta veri dosyaları dahil olmak üzere bir kopya oturum oluşturma</span><span class="sxs-lookup"><span data-stu-id="9d0da-120">Create a Copy Session Including the Properties or Metadata Files</span></span>  
<span data-ttu-id="9d0da-121">İçeri aktarma işi hazırlama Azure içeri/dışarı aktarma aracı çalıştırdığınızda, komut satırını kullanarak üzerinde özellikleri dosyası belirtin `PropertyFile` parametresi.</span><span class="sxs-lookup"><span data-stu-id="9d0da-121">When you run the Azure Import/Export Tool to prepare the import job, specify the properties file on the command line using the `PropertyFile` parameter.</span></span> <span data-ttu-id="9d0da-122">Komut satırını kullanarak üzerinde meta veri dosyası belirtin `/MetadataFile` parametresi.</span><span class="sxs-lookup"><span data-stu-id="9d0da-122">Specify the metadata file on the command line using the `/MetadataFile` parameter.</span></span> <span data-ttu-id="9d0da-123">Her iki dosya belirten örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="9d0da-123">Here's an example that specifies both files:</span></span>  
  
```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```
  
## <a name="next-steps"></a><span data-ttu-id="9d0da-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9d0da-124">Next steps</span></span>

* [<span data-ttu-id="9d0da-125">İçeri/Dışarı Aktarma hizmeti meta veriler ve özellikler dosyası biçimi</span><span class="sxs-lookup"><span data-stu-id="9d0da-125">Import/Export service metadata and properties file format</span></span>](../storage-import-export-file-format-metadata-and-properties.md)
