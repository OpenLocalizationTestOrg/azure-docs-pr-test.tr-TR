---
title: "aaaIndexing CSV BLOB'ların Azure Search blob oluşturucusuyla | Microsoft Docs"
description: "Azure Search ile nasıl tooindex CSV BLOB bilgi edinin"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: ed3c9cff-1946-4af2-a05a-5e0b3d61eb25
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 12/15/2016
ms.author: eugenesh
ms.openlocfilehash: f2b1ce824e62c5b3f6155c6e88887897cf1a8eae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-csv-blobs-with-azure-search-blob-indexer"></a>Dizin oluşturma CSV BLOB'lar ile Azure Search blob dizin oluşturucu
Varsayılan olarak, [Azure Search blob dizin oluşturucu](search-howto-indexing-azure-blob-storage.md) ayrıştırıyor sınırlandırılmış metin BLOB'ları tek bir metin öbek. Ancak, CSV verileri içeren BLOB'lar ile genellikle tootreat hello blob her satır ayrı bir belge olarak istiyor. Örneğin, hello aşağıdaki sınırlandırılmış metin: 

    id, datePublished, tags
    1, 2016-01-12, "azure-search,azure,cloud" 
    2, 2016-07-07, "cloud,mobile" 

tooparse isteyebilirsiniz, "id", "datePublished" ve "etiketler" alanları 2 belgelere her içeren.

Bu makalede nasıl tooparse CSV ile bir Azure Search blob dizinleyici BLOB'ların öğreneceksiniz. 

> [!IMPORTANT]
> Bu işlevsellik şu anda önizlemede değil. Sürüm kullanarak yalnızca hello REST API kullanılabilir **2015-02-28-Önizleme**. Lütfen unutmayın, Önizleme API'leri sınama ve değerlendirme için tasarlanmıştır ve üretim ortamlarında kullanılmamalıdır. 
> 
> 

## <a name="setting-up-csv-indexing"></a>CSV Dizin oluşturmayı ayarlama
tooindex CSV BLOB'lar, oluşturma veya bir dizin oluşturucu tanımı ile Merhaba güncelleştirme `delimitedText` ayrıştırma modu:  

    {
      "name" : "my-csv-indexer",
      ... other indexer properties
      "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "firstLineContainsHeaders" : true } }
    }

Merhaba dizin oluşturucu API oluşturma hakkında daha fazla ayrıntı için kullanıma [oluşturma dizin oluşturucu](search-api-indexers-2015-02-28-preview.md#create-indexer).

`firstLineContainsHeaders`Her bir blob Hello ilk (boş olmayan) satırının üstbilgileri içerdiğini gösterir.
BLOB'ları ilk başlık satırı içermiyorsa, hello üstbilgileri hello dizin oluşturucu yapılandırmasında belirtilen: 

    "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "delimitedTextHeaders" : "id,datePublished,tags" } } 

Şu anda yalnızca hello UTF-8 kodlaması desteklenir. Ayrıca, yalnızca virgülle hello `','` karakter ayırıcısı hello olarak desteklenir. Diğer Kodlamalar veya sınırlayıcıları için destek gerekiyorsa, lütfen bize bilmeniz [UserVoice sitemizi](https://feedback.azure.com/forums/263029-azure-search).

> [!IMPORTANT]
> Modu, Azure Search ayrıştırma hello sınırlandırılmış metin kullandığınızda, veri kaynağındaki tüm BLOB'lar CSV olacağını varsayar. Toosupport CSV bir karışımını gerekir ve CSV olmayan BLOB'hello aynı veri kaynağı, lütfen izin bize bilmeniz [UserVoice sitemizi](https://feedback.azure.com/forums/263029-azure-search).
> 
> 

## <a name="request-examples"></a>İstek örnekleri
Bu tüm koyma birlikte hello tam yükü örnekler şunlardır. 

Veri kaynağı: 

    POST https://[service name].search.windows.net/datasources?api-version=2015-02-28-Preview
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "<optional, my-folder>" }
    }   

Dizin Oluşturucu:

    POST https://[service name].search.windows.net/indexers?api-version=2015-02-28-Preview
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-csv-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "delimitedTextHeaders" : "id,datePublished,tags" } }
    }

## <a name="help-us-make-azure-search-better"></a>Azure Search iyileştirmemize yardımcı olun
Özellik istekleri veya fikir geliştirmeleri için varsa, lütfen üzerinde toous ulaşmak bizim [UserVoice sitesinde](https://feedback.azure.com/forums/263029-azure-search/).

