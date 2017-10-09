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

## <a name="add-hello-path-tooproperties-and-metadata-files-in-datasetcsv"></a>İçinde dataset.csv Hello yolu tooproperties ve meta veri dosyaları Ekle

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,https://mystorageaccount.blob.core.windows.net/video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,https://mystorageaccount.blob.core.windows.net/photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,https://mystorageaccount.blob.core.windows.net/music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

## <a name="next-steps"></a>Sonraki adımlar

* [İçeri/Dışarı Aktarma hizmeti meta veriler ve özellikler dosyası biçimi](storage-import-export-file-format-metadata-and-properties.md)
