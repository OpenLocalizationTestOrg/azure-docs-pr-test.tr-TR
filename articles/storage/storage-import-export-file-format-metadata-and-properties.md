---
title: "aaaAzure içeri/dışarı aktarma meta verileri ve özellikleri dosya biçimi | Microsoft Docs"
description: "Bilgi nasıl toospecify meta verileri ve bir veya daha fazla özellikleri BLOB, bir içeri aktarma parçası olan veya iş dışarı aktarma."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 840364c6-d9a8-4b43-a9f3-f7441c625069
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: bb13c1f1a27baea77298cb224970cd521d02d8c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a>Azure içeri/dışarı aktarma hizmeti meta verileri ve özellikleri dosya biçimi
Meta veri ve bir veya daha fazla BLOB özelliklerini alma işi veya bir dışarı aktarma işinin parçası olarak belirtebilirsiniz. tooset meta verileri veya bir alma işinin bir parçası olarak oluşturulan BLOB'lar için özellikleri, bir meta veri ya da özellikler dosyası içeri hello veri toobe içeren hello sabit sürücüsünde sağlayın. Bir dışarı aktarma işi için meta verileri ve özellikler dahil tooa meta verileri veya özellikleri dosya tooyou döndürülen hello sabit sürücüde yazılır.  
  
## <a name="metadata-file-format"></a>Meta veri dosyası biçimi  
meta veri dosyasının Hello biçimi aşağıdaki gibidir:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|XML öğesi|Tür|Açıklama|  
|-----------------|----------|-----------------|  
|`Metadata`|Kök öğesi|Merhaba meta veri dosyasının kök öğesinin Hello.|  
|`metadata-name`|Dize|İsteğe bağlı. Merhaba XML öğesi hello blob hello meta verilerin hello adını belirtir ve değerini hello hello meta verileri ayarın değerini belirtir.|  
  
## <a name="properties-file-format"></a>Özellikler dosya biçimi  
Özellikler dosyasının Hello biçimi aşağıdaki gibidir:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
[<Last-Modified>date-time-value</Last-Modified>]  
[<Etag>etag</Etag>]  
[<Content-Length>size-in-bytes<Content-Length>]  
[<Content-Type>content-type</Content-Type>]  
[<Content-MD5>content-md5</Content-MD5>]  
[<Content-Encoding>content-encoding</Content-Encoding>]  
[<Content-Language>content-language</Content-Language>]  
[<Cache-Control>cache-control</Cache-Control>]  
</Properties>  
```
  
|XML öğesi|Tür|Açıklama|  
|-----------------|----------|-----------------|  
|`Properties`|Kök öğesi|Merhaba özellikleri dosyasının kök öğesinin Hello.|  
|`Last-Modified`|Dize|İsteğe bağlı. Merhaba son değişiklik zamanı hello blob için. Dışarı aktarma işleri yalnızca.|  
|`Etag`|Dize|İsteğe bağlı. blob'un ETag değeri hello. Dışarı aktarma işleri yalnızca.|  
|`Content-Length`|Dize|İsteğe bağlı. Merhaba blob bayt cinsinden boyutu Hello. Dışarı aktarma işleri yalnızca.|  
|`Content-Type`|Dize|İsteğe bağlı. Merhaba hello BLOB içerik türü.|  
|`Content-MD5`|Dize|İsteğe bağlı. Merhaba blob'un MD5 karma değeri.|  
|`Content-Encoding`|Dize|İsteğe bağlı. Merhaba blob'un içerik kodlaması.|  
|`Content-Language`|Dize|İsteğe bağlı. blob'un içerik dil hello.|  
|`Cache-Control`|Dize|İsteğe bağlı. Merhaba önbellek denetimi dizesi hello blob.|  

## <a name="next-steps"></a>Sonraki adımlar

Bkz: [blob özelliklerini ayarlama](/rest/api/storageservices/set-blob-properties), [Blob meta verileri ayarlama](/rest/api/storageservices/set-blob-metadata), ve [ayarı ve alınırken özelliklerini ve meta verileri için blob kaynakları](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) için blob meta verileri ve özellikleri ayarlama hakkında ayrıntılı kurallar.
