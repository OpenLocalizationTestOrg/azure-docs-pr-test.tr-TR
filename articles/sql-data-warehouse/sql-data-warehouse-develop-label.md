---
title: "SQL veri ambarı'nda gereç sorgular için etiketleri kullanma | Microsoft Docs"
description: "Çözümleri geliştirme için Azure SQL Data Warehouse'da gereç sorgulara etiketleri kullanma ipuçları."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 44988de8-04c1-4fed-92be-e1935661a4e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 9e75bbe528a427724a623305fbd45e2277e9d0af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-labels-to-instrument-queries-in-sql-data-warehouse"></a><span data-ttu-id="04184-103">SQL veri ambarı'nda gereç sorgular için etiketleri kullanma</span><span class="sxs-lookup"><span data-stu-id="04184-103">Use labels to instrument queries in SQL Data Warehouse</span></span>
<span data-ttu-id="04184-104">SQL veri ambarı sorgusu etiketleri adlı bir kavram destekler.</span><span class="sxs-lookup"><span data-stu-id="04184-104">SQL Data Warehouse supports a concept called query labels.</span></span> <span data-ttu-id="04184-105">Herhangi bir derinliğe şimdi geçmeden önce bir bir örneğe bakın:</span><span class="sxs-lookup"><span data-stu-id="04184-105">Before going into any depth let's look at an example of one:</span></span>

```sql
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query Label')
;
```

<span data-ttu-id="04184-106">Bu son satırında sorgu dizesine 'My sorgu etiketi' etiketler.</span><span class="sxs-lookup"><span data-stu-id="04184-106">This last line tags the string 'My Query Label' to the query.</span></span> <span data-ttu-id="04184-107">Etiket-Dmv'leri sorgulayabilir olduğu gibi bu seçenek özellikle yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="04184-107">This is particularly helpful as the label is query-able through the DMVs.</span></span> <span data-ttu-id="04184-108">Bu bize sorun sorguları izlemek ve ETL Çalıştır ilerlemeyi tanımlamaya yardımcı olmak için bir mekanizma sağlar.</span><span class="sxs-lookup"><span data-stu-id="04184-108">This provides us with a mechanism to track down problem queries and also to help identify progress through an ETL run.</span></span>

<span data-ttu-id="04184-109">İyi bir adlandırma kuralı gerçekten burada yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="04184-109">A good naming convention really helps here.</span></span> <span data-ttu-id="04184-110">Örneğin şuna benzer ' proje: yordamı: DEYİMİ: Açıklama ' sorguyu kaynak denetiminde tüm kod arasında benzersiz şekilde tanımlamak için yardımcı.</span><span class="sxs-lookup"><span data-stu-id="04184-110">For example something like ' PROJECT : PROCEDURE : STATEMENT : COMMENT' would help to uniquely identify the query in amongst all the code in source control.</span></span>

<span data-ttu-id="04184-111">Etikete göre aramak için dinamik yönetim görünümlerini kullanan aşağıdaki sorgu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="04184-111">To search by label you can use the following query that uses the dynamic management views:</span></span>

```sql
SELECT  *
FROM    sys.dm_pdw_exec_requests r
WHERE   r.[label] = 'My Query Label'
;
```

> [!NOTE]
> <span data-ttu-id="04184-112">Sorgulanırken köşeli veya çift tırnak word etiket kaydırma gereklidir.</span><span class="sxs-lookup"><span data-stu-id="04184-112">It is essential that you wrap square brackets or double quotes around the word label when querying.</span></span> <span data-ttu-id="04184-113">Etiket ayrılmış bir sözcük ve onu Sınırlanmamış bir hata neden olur.</span><span class="sxs-lookup"><span data-stu-id="04184-113">Label is a reserved word and will caused an error if it has not been delimited.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="04184-114">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="04184-114">Next steps</span></span>
<span data-ttu-id="04184-115">Daha fazla geliştirme ipuçları için bkz: [geliştirmeye genel bakış][development overview].</span><span class="sxs-lookup"><span data-stu-id="04184-115">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
