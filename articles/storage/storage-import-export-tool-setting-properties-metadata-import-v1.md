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
ms.openlocfilehash: 66e55c2076fbcda9b78302f17b5ff2cf96bb24e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-properties-and-metadata-during-hello-import-process"></a>Özellikleri ayarlama ve hello sırasında meta veri alma işlemi
Merhaba Microsoft Azure içeri/dışarı aktarma aracı tooprepare sürücülerinizin çalıştırdığınızda, özellikleri ve meta veri toobe hello hedef BLOB'ları üzerinde ayarlamak belirtebilirsiniz. Şu adımları uygulayın:  
  
1.  tooset blob özellikleri, özellik adları ve değerleri belirtir, yerel bilgisayarınızda bir metin dosyası oluşturun.  
  
2.  tooset meta verileri blob, meta veri adları ve değerleri belirtir, yerel bilgisayarınızda bir metin dosyası oluşturun.  
  
3.  Merhaba tam yolu tooone veya bu dosyaları toohello Azure içeri/dışarı aktarma aracı her ikisi de hello bir parçası olarak geçirin `PrepImport` işlemi.  
  
> [!NOTE]
>  Özellikler veya meta veri dosya kopyalama oturumun bir parçası belirttiğinizde, bu kopya oturumu bir parçası olarak alınan her blob için bu özellikleri veya meta veriler ayarlanır. İçeri aktarılan hello BLOB'ları bazıları için toospecify özellikleri veya meta veriler farklı bir kümesini istiyorsanız, ayrı bir kopyalama farklı özellikleri veya meta veri dosyaları oturumla toocreate gerekir.  
  
## <a name="specify-blob-properties-in-a-text-file"></a>Bir metin dosyasına BLOB özellikleri belirtin  
toospecify blob özellikleri, bir yerel metin dosyası oluşturun ve öğeleri ve değerleri olarak özellik değerleri olarak özellik adlarını belirtir XML içerir. Bazı özellik değerleri belirten örnek aşağıda verilmiştir:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
Merhaba dosya tooa yerel bir konum gibi kaydetmek `C:\WAImportExport\ImportProperties.txt`.  
  
## <a name="specify-blob-metadata-in-a-text-file"></a>Bir metin dosyasına BLOB meta verileri belirtin  
Benzer şekilde, toospecify meta verileri blob, meta veri adlarının öğeleri ve meta veri değerlerinin değerler olarak olarak belirten bir yerel metin dosyası oluşturun. Bazı meta veri değerleri belirten örnek aşağıda verilmiştir:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
Merhaba dosya tooa yerel bir konum gibi kaydetmek `C:\WAImportExport\ImportMetadata.txt`.  
  
## <a name="create-a-copy-session-including-hello-properties-or-metadata-files"></a>Oturum kopyalama dahil olmak üzere hello özellikleri veya meta veri dosyaları oluşturma  
Hello Azure içeri/dışarı aktarma aracı tooprepare hello alma işi çalıştırdığınızda, hello komut satırında hello kullanarak hello özellikleri dosya belirtin `PropertyFile` parametresi. Merhaba meta veri dosyası hello komut satırında hello kullanarak belirtin `/MetadataFile` parametresi. Her iki dosya belirten örnek aşağıda verilmiştir:  
  
```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```
  
## <a name="next-steps"></a>Sonraki adımlar

* [İçeri/Dışarı Aktarma hizmeti meta veriler ve özellikler dosyası biçimi](storage-import-export-file-format-metadata-and-properties.md)
