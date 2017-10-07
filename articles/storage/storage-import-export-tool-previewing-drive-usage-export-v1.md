---
title: "bir Azure içeri/dışarı aktarma dışarı aktarma işinin - v1 için sürücü kullanımı aaaPreviewing | Microsoft Docs"
description: "Nasıl toopreview hello BLOB'ları listesi hello Azure içeri/dışarı aktarma hizmetinde dışa aktarma işi için seçtiğiniz öğrenin."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 7707d744-7ec7-4de8-ac9b-93a18608dc9a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 88495f921371458c0451da6878fd7cc9a45d20cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="previewing-drive-usage-for-an-export-job"></a>Dışarı aktarma işi için sürücü kullanımının önizlemesini yapma
Bir dışarı aktarma işinin oluşturmadan önce bir dizi BLOB toobe dışarı toochoose gerekir. Seçtiğiniz toorepresent hello BLOB'lar blob önekleri veya Hello Microsoft Azure içeri/dışarı aktarma hizmeti toouse blob yolların listesini sağlar.  
  
Ardından, kaç tane sürücülere toodetermine ihtiyaç toosend gerekir. Merhaba içeri/dışarı aktarma aracı sağlar hello `PreviewExport` seçtiğiniz hello BLOB'lar için komut toopreview sürücü kullanımı, hello hello sürücüleri boyutuna göre toouse adımıdır.

## <a name="command-line-parameters"></a>Komut satırı parametreleri

Merhaba kullanırken şu parametreler hello kullanabilirsiniz `PreviewExport` hello içeri/dışarı aktarma aracı komutu.

|Komut satırı parametresi|Açıklama|  
|--------------------------|-----------------|  
|**/ LOGDIR:**< LogDirectory\>|İsteğe bağlı. Merhaba günlük dosyası dizini. Ayrıntılı günlük dosyalarını toothis dizin yazılır. Günlük dizini belirtilirse, hello geçerli dizin hello günlük dizini kullanılır.|  
|**/sn:**< StorageAccountName\>|Gereklidir. Merhaba depolama hesabının adını Hello hello için iş verin.|  
|**/SK:**< StorageAccountKey\>|Bir kapsayıcı SAS varsa ve yalnızca belirtilmemişse gereklidir. Merhaba hesap anahtarı hello depolama hesabı hello için iş verin.|  
|**/csas:**< ContainerSas\>|Bir depolama hesabı anahtarı varsa ve yalnızca belirtilmemişse gerekli. Liste hello BLOB'lar toobe için Hello kapsayıcı SAS hello dışarı aktarma işinin dışarı.|  
|**/ ExportBlobListFile:**< ExportBlobListFile\>|Gereklidir. Yol toohello XML içeren blob yollar listesi dosya veya yol önekleri dışarı hello BLOB'lar toobe için blob. Hello kullanılan hello dosya biçimi `BlobListBlobPath` hello öğesinde [Put işlemini](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) hello içeri/dışarı aktarma hizmeti REST API'si işlemi.|  
|**/ DriveSize:**< DriveSize\>|Gereklidir. Merhaba bir dışa aktarma işi için sürücüleri toouse boyutunu *ör*, 500 GB, 1,5 TB.|  

## <a name="command-line-example"></a>Komut satırı örneği

Merhaba aşağıdaki örnekte gösterilmiştir hello `PreviewExport` komutu:  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
Merhaba ve dışa aktarma blob listesi dosyasının blob adları içeren önekleri, aşağıda gösterildiği gibi blob:  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

Hello Azure içeri/dışarı aktarma aracı dışarı aktarılan tüm BLOB'ları toobe listeler ve nasıl hello sürücülerin bunlara boyutu gerekli tüm ek yükü dikkate alarak, ardından sürücü hello sayısı tahminleri belirtilen toopack toohold hello BLOB'ları ve sürücü kullanımını gerekli hesaplar bilgi.  
  
Atlanmış bilgilendirme günlükleriyle hello çıktısı örneği şöyledir:  
  
```  
Number of unique blob paths/prefixes:   3  
Number of duplicate blob paths/prefixes:        0  
Number of nonexistent blob paths/prefixes:      1  
  
Drive size:     500.00 GB  
Number of blobs that can be exported:   6  
Number of blobs that cannot be exported:        2  
Number of drives needed:        3  
        Drive #1:       blobs = 1, occupied space = 454.74 GB  
        Drive #2:       blobs = 3, occupied space = 441.37 GB  
        Drive #3:       blobs = 2, occupied space = 131.28 GB    
```  
  
## <a name="next-steps"></a>Sonraki adımlar

* [Azure içeri/dışarı aktarma aracı başvurusu](storage-import-export-tool-how-to-v1.md)
