---
title: aaaUse etiketler SQL Data Warehouse tooinstrument sorgularda | Microsoft Docs
description: "Kullanımı hakkında ipuçları çözümleri geliştirmek için Azure SQL Data Warehouse tooinstrument sorgularda etiketler."
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
ms.openlocfilehash: 82e7ea98e1417134227f1d7c529fdaf2f1df3853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-labels-tooinstrument-queries-in-sql-data-warehouse"></a><span data-ttu-id="a025b-103">SQL veri ambarı'nda etiketleri tooinstrument sorgularını kullan</span><span class="sxs-lookup"><span data-stu-id="a025b-103">Use labels tooinstrument queries in SQL Data Warehouse</span></span>
<span data-ttu-id="a025b-104">SQL veri ambarı sorgusu etiketleri adlı bir kavram destekler.</span><span class="sxs-lookup"><span data-stu-id="a025b-104">SQL Data Warehouse supports a concept called query labels.</span></span> <span data-ttu-id="a025b-105">Herhangi bir derinliğe şimdi geçmeden önce bir bir örneğe bakın:</span><span class="sxs-lookup"><span data-stu-id="a025b-105">Before going into any depth let's look at an example of one:</span></span>

```sql
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query Label')
;
```

<span data-ttu-id="a025b-106">Bu son satırında hello dize 'My sorgu etiketi' toohello sorgu etiketler.</span><span class="sxs-lookup"><span data-stu-id="a025b-106">This last line tags hello string 'My Query Label' toohello query.</span></span> <span data-ttu-id="a025b-107">Merhaba etiket-Dmv'leri hello sorgulayabilir olduğu gibi bu seçenek özellikle yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="a025b-107">This is particularly helpful as hello label is query-able through hello DMVs.</span></span> <span data-ttu-id="a025b-108">Bu bize mekanizması tootrack sorun sorguları aşağı sağlar ve ayrıca toohelp ETL Çalıştır ilerlemeyi tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="a025b-108">This provides us with a mechanism tootrack down problem queries and also toohelp identify progress through an ETL run.</span></span>

<span data-ttu-id="a025b-109">İyi bir adlandırma kuralı gerçekten burada yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="a025b-109">A good naming convention really helps here.</span></span> <span data-ttu-id="a025b-110">Örneğin şuna benzer ' proje: yordamı: DEYİMİ: Açıklama ' hello sorgu kaynak denetiminde tüm hello kodu arasında tanımlamak toouniquely yardımcı.</span><span class="sxs-lookup"><span data-stu-id="a025b-110">For example something like ' PROJECT : PROCEDURE : STATEMENT : COMMENT' would help toouniquely identify hello query in amongst all hello code in source control.</span></span>

<span data-ttu-id="a025b-111">toosearch kullanan sorgu aşağıdaki hello kullanabileceğiniz etiketine göre dinamik yönetim görünümlerini hello:</span><span class="sxs-lookup"><span data-stu-id="a025b-111">toosearch by label you can use hello following query that uses hello dynamic management views:</span></span>

```sql
SELECT  *
FROM    sys.dm_pdw_exec_requests r
WHERE   r.[label] = 'My Query Label'
;
```

> [!NOTE]
> <span data-ttu-id="a025b-112">Sorgulanırken köşeli veya çift tırnak hello word etiket kaydırma gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a025b-112">It is essential that you wrap square brackets or double quotes around hello word label when querying.</span></span> <span data-ttu-id="a025b-113">Etiket ayrılmış bir sözcük ve onu Sınırlanmamış bir hata neden olur.</span><span class="sxs-lookup"><span data-stu-id="a025b-113">Label is a reserved word and will caused an error if it has not been delimited.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a025b-114">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a025b-114">Next steps</span></span>
<span data-ttu-id="a025b-115">Daha fazla geliştirme ipuçları için bkz: [geliştirmeye genel bakış][development overview].</span><span class="sxs-lookup"><span data-stu-id="a025b-115">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
