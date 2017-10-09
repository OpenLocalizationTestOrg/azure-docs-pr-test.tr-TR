---
title: Azure Search'te aaaIndexers | Microsoft Docs
description: "Azure SQL veritabanı, Azure Cosmos DB veya Azure depolama tooextract aranabilir verileri gezinme ve Azure Search dizini doldurabilirsiniz."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 34a7694c-8fd9-46b1-8900-cefdd7236323
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: 6a816252ec5d6032491a12651c05cb1fe77d3d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="indexers-in-azure-search"></a>Azure Search'te dizin oluşturucular
> [!div class="op_single_selector"]
>
> * [Genel Bakış](search-indexer-overview.md)
> * [Portal](search-import-data-portal.md)
> * [Azure SQL](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
> * [Azure Cosmos DB](search-howto-index-documentdb.md)
> * [Azure Blob Depolama](search-howto-indexing-azure-blob-storage.md)
> * [Azure Table Storage](search-howto-indexing-azure-tables.md)
>
>

Bir **dizin oluşturucu** Azure Search'te bir dış veri kaynağından aranabilir verileri ve meta verileri ayıklar ve bir dizini dolduran bir Gezgin alan alan eşlemelerini hello dizini ile veri kaynağınız arasında temel alır. Merhaba hizmet verileri toowrite kalmadan veri tooan dizini iter herhangi bir kod çeker çünkü bu yaklaşım bazen başvurulan tooas 'çekme modeli' olur.

Veri alımı amacıyla hello tek bir dizin oluşturucuyu kullanın veya dizininizdeki hello alanların yalnızca bazılarını yüklemek için bir dizin oluşturucu hello kullanımı dahil teknikler birleşimini kullanın.

Dizin oluşturucuları isteğe bağlı olarak veya her on beş dakikada bir çalıştırılan bir yinelenen veri yenileme zamanlamasıyla çalıştırabilirsiniz. Daha sık güncelleştirmeler için hem Azure Search'te hem de dış veri kaynağınızda verileri aynı anda güncelleştiren bir gönderme modeli gerekir.

## <a name="approaches-for-creating-and-managing-indexers"></a>Dizin oluşturucular oluşturma ve yönetme yaklaşımları
Azure SQL veya Azure Cosmos DB gibi genel kullanıma açık dizin oluşturucular için bu yaklaşımları kullanarak dizin oluşturucular oluşturabilir ve bunları yönetebilirsiniz:

* [Portal > Veri Alma Sihirbazı](search-get-started-portal.md)
* [Hizmet REST API'si](https://msdn.microsoft.com/library/azure/dn946891.aspx)
* [.NET SDK](https://msdn.microsoft.com/library/azure/microsoft.azure.search.iindexersoperations.aspx)

## <a name="basic-configuration-steps"></a>Temel yapılandırma adımları
Dizin oluşturucular benzersiz toohello veri kaynağı özellikleri sunabilir. Bu bakımdan, dizin oluşturucu veya veri kaynağı yapılandırmasının bazı boyutları dizin oluşturucu türüne göre farklılık gösterir. Ancak, tüm dizin oluşturucuların hello paylaşır aynı temel birleşim ve gereksinimleri. Dizin oluşturucular aşağıda ele alınmıştır ortak tooall adımları.

### <a name="step-1-create-an-index"></a>1. Adım: Dizin oluşturma
Bir dizin oluşturucu bazı görevler ilgili toodata alım otomatik olarak güncelleştirir, ancak dizin oluşturma bunlardan biri değil. Bir önkoşul olarak dış veri kaynağınızdaki alanlarla eşleşen alanlara sahip önceden tanımlı bir dizininiz olmalıdır. Bir dizini yapılandırma konusunda daha fazla bilgi için bkz. [Dizin oluşturma (Azure Search REST API’si)](https://msdn.microsoft.com/library/azure/dn798941.aspx).

### <a name="step-2-create-a-data-source"></a>2. Adım: Veri kaynağı oluşturma
Dizin oluşturucu, bağlantı dizesi gibi bilgileri içeren bir **veri kaynağından** veri çeker. Şu anda aşağıdaki veri kaynaklar hello desteklenir:

* [Bir Azure sanal makinesinde Azure SQL Veritabanı veya SQL Server](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [Azure Cosmos DB](search-howto-index-documentdb.md)
* [Azure Blob Depolama](search-howto-indexing-azure-blob-storage.md), PDF, Office belgeleri, HTML veya XML tooextract metinden kullanılan
* [Azure Table Storage](search-howto-indexing-azure-tables.md)

Veri kaynakları yapılandırılmış ve bir veri kaynağı tarafından birden çok dizin oluşturucular tooload kullanılabilir anlamına gelir, birden fazla dizine aynı anda bunları kullanan hello dizin oluşturucular bağımsız olarak yönetilir.

### <a name="step-3create-and-schedule-hello-indexer"></a>3. adım: oluşturma ve zamanlama hello dizin oluşturucu
Merhaba dizin oluşturucu tanımı hello dizin, veri kaynağı ve bir zamanlama belirten bir yapıdır. Bu veri kaynağı hello olduğu sürece bir dizin oluşturucu başka bir hizmet, bir veri kaynağı başvurusu yapabilir aynı abonelik. Bir dizin oluşturucuyu yapılandırma konusunda daha fazla bilgi için bkz. [Dizin Oluşturucu Oluşturma (Azure Search REST API’si)](https://msdn.microsoft.com/library/azure/dn946899.aspx).

## <a name="next-steps"></a>Sonraki adımlar
Merhaba temel düşünce sahip olduğunuza göre hello sonraki tooreview gereksinimleri ve görevleri belirli tooeach veri kaynağı türü adımdır.

* [Bir Azure sanal makinesinde Azure SQL Veritabanı veya SQL Server](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [Azure Cosmos DB](search-howto-index-documentdb.md)
* [Azure Blob Storage](search-howto-indexing-azure-blob-storage.md), PDF, Office belgeleri, HTML veya XML tooextract metinden kullanılan
* [Azure Table Storage](search-howto-indexing-azure-tables.md)
* [CSV BLOB'lar Hello Azure arama Blob Dizin Oluşturucu kullanarak dizin oluşturma](search-howto-index-csv-blobs.md)
* [Azure Search Blob dizin oluşturucu ile JSON bloblarını dizine ekleme](search-howto-index-json-blobs.md)
