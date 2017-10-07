---
title: "Azure Search'te aaaData karşıya yükleme | Microsoft Docs"
description: "Nasıl tooupload veri tooan dizin Azure Search'te öğrenin."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
editor: 
tags: 
ms.assetid: aa8d47c1-4ae6-4209-a8ce-48d5a9474707
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: ashmaka
ms.openlocfilehash: a95eae94f72c1d0926804ff7e1152f21773fcabf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search"></a>Veri tooAzure arama karşıya yükle
> [!div class="op_single_selector"]
> * [Genel Bakış](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
> 
> 

Dizin verilerinizi ile iki şekilde toopopulate vardır. Merhaba ilk seçenek olan el ile Ftp'den verilerinizi hello Azure Search kullanarak hello dizine [REST API](search-import-data-rest-api.md) veya [.NET SDK'sı](search-import-data-dotnet.md). Merhaba ikinci seçenek olan çok[desteklenen veri kaynağı](search-indexer-overview.md) tooyour dizini oluşturmak ve Azure hello verileri otomatik olarak çekmesini sağlamaktır.

## <a name="push-data-tooan-index"></a>Anında iletme veri tooan dizini
Bu yaklaşım, veri tooAzure arama toomake gönderme tooprogrammatically başvuruyor, arama için kullanılabilir. (Örneğin, dinamik stok veritabanlarıyla eşitlenmiş işlemleri toobe arama) çok düşük gecikme gereksinimlerine sahip uygulamalar için hello gönderme modeli, tek seçenektir.

Merhaba kullanabilirsiniz [REST API](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents) veya [.NET SDK'sı](search-import-data-dotnet.md) toopush veri tooan dizini. Şu anda hello portal aracılığıyla veri gönderme için hiçbir araç desteği.

Bu yaklaşım, belgeleri tek tek veya toplu işlemle karşıya yükleyebileceğinizden hello çekme modelinden daha esnektir (toplu işlem veya 16 MB başına too1000 sınırlarından hangisi önce gelirse). Merhaba gönderme modeli, verilerinizin nerede olduğuna bakılmaksızın tooupload belgeleri tooAzure arama sağlar.

Azure Search tarafından anlaşılan hello verileri JSON biçimidir ve hello kümesindeki tüm belgeleri, dizin şeması'nda tanımlanan toofields harita alanları olması gerekir. 

## <a name="pull-data-into-an-index"></a>Bir dizine veri çekme
Merhaba çekme modeli, desteklenen veri kaynağında gezinir ve hello veri dizininize otomatik olarak yükler. Azure Search'te bu işlev, şu anda [Blob depolama](search-howto-indexing-azure-blob-storage.md), [Tablo depolama](search-howto-indexing-azure-tables.md), [Azure Cosmos DB](http://aka.ms/documentdb-search-indexer), [Azure SQL Veritabanı ve Azure VM'lerdeki SQL Server](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)'da kullanılabilen *dizin oluşturucular* aracılığıyla uygulanır. 

Dizin oluşturucular bir dizin tooa veri kaynağı (genellikle bir tablo, görünüm veya eşdeğeri yapısı) bağlantı ve kaynak alanlar tooequivalent alanları hello dizindeki eşleyin. Yürütme sırasında hello satır kümesi otomatik olarak dönüştürülmüş tooJSON olan ve hello belirtilen dizine yüklenir. Tüm Dizin oluşturucuların ne sıklıkta hello veri toobe yenilenmiş olduğunu belirtebilirsiniz, böylece zamanlama destekler. Çoğu dizin oluşturucular değişiklik hello veri kaynağı destekliyorsa izleme sağlar. İzleme değişiklikleri ve silmeleri tarafından tooexisting ayrıca toorecognizing yeni belgeler belgeleri, dizin oluşturucular hello gereksinimini kaldırmak tooactively dizininizdeki hello verileri yönetin. 

Dizin oluşturucu işlevi hello açığa [Azure portal](search-import-data-portal.md), hello [REST API](/rest/api/searchservice/Indexer-operations)ve hello [.NET SDK'sı](/dotnet/api/microsoft.azure.search.indexersoperations). 

Bir avantajı toousing hello Portal'da Azure Search genellikle varsayılan dizin şemasını sizin için hello kaynak dataset hello meta verilerini okuyarak oluşturabilecek olmasıdır. Hangi hello sonra yalnızca şema düzenlemeleri yeniden dizin oluşturmaya gerektirmeyen olanlar izin verilen Hello dizin işlenir kadar hello oluşturulan dizini değiştirebilirsiniz. Toomake etkisi istediğiniz hello değişiklikleri şema doğrudan hello toorebuild hello dizin gereksiniminiz olacaktır. 

Merhaba dizin doldurulduktan sonra kullanabileceğiniz **arama Gezgini** hello portal komut çubuğunda bir doğrulama adımı olarak.

## <a name="query-an-index-using-search-explorer"></a>Arama Gezgini kullanarak dizin sorgulama

Bir hızlı yol tooperform hello belge karşıya yükleme sırasında Ön onay toouse olan **arama Gezgini** hello Portalı'nda. Merhaba Gezgini herhangi bir kod toowrite gerek kalmadan bir dizini sorgulama izin verir. Merhaba arama deneyimi hello gibi varsayılan ayarları dayanır [basit sözdizimi](/rest/api/searchservice/simple-query-syntax-in-azure-search) ve varsayılan [searchMode sorgu parametresi](/rest/api/searchservice/search-documents). Böylece hello tüm belgeyi inceleyebilirsiniz sonuçları JSON döndürülür.

> [!TIP]
> Çok sayıda [Azure Search kod örnekleri](https://github.com/Azure-Samples/?utf8=%E2%9C%93&query=search) kolay bir yolu tooget başlatılan sunumu katıştırılmış veya kullanıma hazır veri kümeleri, içerir. Merhaba portal, örnek dizin oluşturucu ve veri kaynağı ("realestate-us-sample" olarak adlandırılır) bir küçük Gayrimenkul veri kümesi oluşan de sağlar. Hello örnek veri kaynağında hello önceden yapılandırılmış dizin oluşturucu çalıştırdığınızda, bir dizin oluşturulur ve ardından arama Gezgini veya yazdığınız kodu tarafından sorgulanabilir belgelerle yüklendi.
