---
title: "Ayrıca \"bir dizin (portalı - Azure Search) sorgu | Microsoft Docs\""
description: "Hello Azure Portal'ın arama Gezgini arama sorgusu gönderin."
services: search
manager: jhubbard
documentationcenter: 
author: ashmaka
ms.assetid: 8e524188-73a7-44db-9e64-ae8bf66b05d3
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 07/10/2017
ms.author: ashmaka
ms.openlocfilehash: 56bab3ef8a66eeb053fbbeb6d322acb6824fb34b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="query-an-azure-search-index-using-search-explorer-in-hello-azure-portal"></a>Arama Gezgini hello Azure Portal kullanarak Azure Search dizini sorgulama
> [!div class="op_single_selector"]
> * [Genel Bakış](search-query-overview.md)
> * [Portal](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

Bu makalede nasıl tooquery Azure Search dizini kullanarak gösterilmektedir **arama Gezgini** hello Azure Portalı'nda. Arama Gezgini toosubmit basit veya tam Lucene sorgu dizeleri tooany var olan dizini hizmetinizde kullanabilirsiniz.

## <a name="open-hello-service-dashboard"></a>Açık hello hizmet Panosu
1. Tıklatın **tüm kaynakları** sol hello tarafı hello hello atlama çubuğunda [Azure portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).
2. Azure Search hizmetinizi seçin.

## <a name="select-an-index"></a>Dizin seçme

Merhaba gelen toosearch istediğinizi seçin hello dizin **dizinleri** döşeme.

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a>Arama Gezgini’ni açma

Merhaba arama Gezgini döşeme tooslide açık hello arama çubuğunu tıklayın ve sonuçlar bölmesinde.

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a>Aramayı başlatma

Merhaba arama Gezgini kullanırken belirtebilirsiniz [sorgu parametreleri](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) tooformulate hello sorgu.

1. **Sorgu dizesi**’nde sorguyu yazın ve **Ara**’ya basın. 

   Merhaba sorgu dizesi, URL toosubmit hello Azure Search REST API'sini bir HTTP isteği hello uygun istek otomatik olarak ayrıştırılır.   
   
   Tüm geçerli basit veya tam Lucene sorgu söz dizimi toocreate hello isteği kullanabilirsiniz. Merhaba `*` belirli bir sırada tüm belgeleri döndüren eşdeğer tooan boş veya belirtilmemiş arama karakterdir.

2. İçinde **sonuçları**, sorgu sonuçları ham JSON'da sunulan, aynı toohello yükü döndürülen istekleri program aracılığıyla gönderirken HTTP yanıt gövdesi.

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a>Sonraki adımlar

Merhaba kaynakları aşağıdaki ek sorgu sözdizimi bilgi ve örnekler sağlar.

 + [Basit sorgu söz dizimi](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [Lucene sorgu söz dizimi](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [Lucene sorgu söz dizimi örnekleri](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + [OData Filtre ifadesinin söz dizimi](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) 