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
# <a name="query-an-azure-search-index-using-search-explorer-in-hello-azure-portal"></a><span data-ttu-id="40ebc-103">Arama Gezgini hello Azure Portal kullanarak Azure Search dizini sorgulama</span><span class="sxs-lookup"><span data-stu-id="40ebc-103">Query an Azure Search index using Search Explorer in hello Azure Portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="40ebc-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="40ebc-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="40ebc-105">Portal</span><span class="sxs-lookup"><span data-stu-id="40ebc-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="40ebc-106">.NET</span><span class="sxs-lookup"><span data-stu-id="40ebc-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="40ebc-107">REST</span><span class="sxs-lookup"><span data-stu-id="40ebc-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="40ebc-108">Bu makalede nasıl tooquery Azure Search dizini kullanarak gösterilmektedir **arama Gezgini** hello Azure Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="40ebc-108">This article shows you how tooquery an Azure Search index using **Search Explorer** in hello Azure portal.</span></span> <span data-ttu-id="40ebc-109">Arama Gezgini toosubmit basit veya tam Lucene sorgu dizeleri tooany var olan dizini hizmetinizde kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40ebc-109">You can use Search Explorer toosubmit simple or full Lucene query strings tooany existing index in your service.</span></span>

## <a name="open-hello-service-dashboard"></a><span data-ttu-id="40ebc-110">Açık hello hizmet Panosu</span><span class="sxs-lookup"><span data-stu-id="40ebc-110">Open hello service dashboard</span></span>
1. <span data-ttu-id="40ebc-111">Tıklatın **tüm kaynakları** sol hello tarafı hello hello atlama çubuğunda [Azure portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).</span><span class="sxs-lookup"><span data-stu-id="40ebc-111">Click **All resources** in hello jump bar on hello left side of hello [Azure portal](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).</span></span>
2. <span data-ttu-id="40ebc-112">Azure Search hizmetinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="40ebc-112">Select your Azure Search service.</span></span>

## <a name="select-an-index"></a><span data-ttu-id="40ebc-113">Dizin seçme</span><span class="sxs-lookup"><span data-stu-id="40ebc-113">Select an index</span></span>

<span data-ttu-id="40ebc-114">Merhaba gelen toosearch istediğinizi seçin hello dizin **dizinleri** döşeme.</span><span class="sxs-lookup"><span data-stu-id="40ebc-114">Select hello index you would like toosearch from hello **Indexes** tile.</span></span>

   ![](./media/search-explorer/pick-index.png)

## <a name="open-search-explorer"></a><span data-ttu-id="40ebc-115">Arama Gezgini’ni açma</span><span class="sxs-lookup"><span data-stu-id="40ebc-115">Open Search Explorer</span></span>

<span data-ttu-id="40ebc-116">Merhaba arama Gezgini döşeme tooslide açık hello arama çubuğunu tıklayın ve sonuçlar bölmesinde.</span><span class="sxs-lookup"><span data-stu-id="40ebc-116">Click on hello Search Explorer tile tooslide open hello search bar and results pane.</span></span>

   ![](./media/search-explorer/search-explorer-tile.png)

## <a name="start-searching"></a><span data-ttu-id="40ebc-117">Aramayı başlatma</span><span class="sxs-lookup"><span data-stu-id="40ebc-117">Start searching</span></span>

<span data-ttu-id="40ebc-118">Merhaba arama Gezgini kullanırken belirtebilirsiniz [sorgu parametreleri](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) tooformulate hello sorgu.</span><span class="sxs-lookup"><span data-stu-id="40ebc-118">When using hello Search Explorer, you can specify [query parameters](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) tooformulate hello query.</span></span>

1. <span data-ttu-id="40ebc-119">**Sorgu dizesi**’nde sorguyu yazın ve **Ara**’ya basın.</span><span class="sxs-lookup"><span data-stu-id="40ebc-119">In **Query string**, type a query and then press **Search**.</span></span> 

   <span data-ttu-id="40ebc-120">Merhaba sorgu dizesi, URL toosubmit hello Azure Search REST API'sini bir HTTP isteği hello uygun istek otomatik olarak ayrıştırılır.</span><span class="sxs-lookup"><span data-stu-id="40ebc-120">hello query string is automatically parsed into hello proper request URL toosubmit a HTTP request against hello Azure Search REST API.</span></span>   
   
   <span data-ttu-id="40ebc-121">Tüm geçerli basit veya tam Lucene sorgu söz dizimi toocreate hello isteği kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40ebc-121">You can use any valid simple or full Lucene query syntax toocreate hello request.</span></span> <span data-ttu-id="40ebc-122">Merhaba `*` belirli bir sırada tüm belgeleri döndüren eşdeğer tooan boş veya belirtilmemiş arama karakterdir.</span><span class="sxs-lookup"><span data-stu-id="40ebc-122">hello `*` character is equivalent tooan empty or unspecified search that returns all documents in no particular order.</span></span>

2. <span data-ttu-id="40ebc-123">İçinde **sonuçları**, sorgu sonuçları ham JSON'da sunulan, aynı toohello yükü döndürülen istekleri program aracılığıyla gönderirken HTTP yanıt gövdesi.</span><span class="sxs-lookup"><span data-stu-id="40ebc-123">In  **Results**, query results are presented in raw JSON, identical toohello payload returned in an HTTP Response Body when issuing requests programmatically.</span></span>

   ![](./media/search-explorer/search-bar.png)

## <a name="next-steps"></a><span data-ttu-id="40ebc-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="40ebc-124">Next steps</span></span>

<span data-ttu-id="40ebc-125">Merhaba kaynakları aşağıdaki ek sorgu sözdizimi bilgi ve örnekler sağlar.</span><span class="sxs-lookup"><span data-stu-id="40ebc-125">hello following resources provide additional query syntax information and examples.</span></span>

 + [<span data-ttu-id="40ebc-126">Basit sorgu söz dizimi</span><span class="sxs-lookup"><span data-stu-id="40ebc-126">Simple query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) 
 + [<span data-ttu-id="40ebc-127">Lucene sorgu söz dizimi</span><span class="sxs-lookup"><span data-stu-id="40ebc-127">Lucene query syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) 
 + [<span data-ttu-id="40ebc-128">Lucene sorgu söz dizimi örnekleri</span><span class="sxs-lookup"><span data-stu-id="40ebc-128">Lucene query syntax examples</span></span>](https://docs.microsoft.com/azure/search/search-query-lucene-examples) 
 + [<span data-ttu-id="40ebc-129">OData Filtre ifadesinin söz dizimi</span><span class="sxs-lookup"><span data-stu-id="40ebc-129">OData Filter expression syntax</span></span>](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) 