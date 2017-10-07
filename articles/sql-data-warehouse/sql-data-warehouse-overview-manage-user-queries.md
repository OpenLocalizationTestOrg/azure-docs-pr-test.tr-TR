---
title: "Azure SQL Data Warehouse aaaMonitor kullanıcı sorguları | Microsoft Docs"
description: "Merhaba konuları, en iyi yöntemler ve Azure SQL Data Warehouse kullanıcı sorgularda izleme görevleri genel bakış"
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 1d0960db-5dcf-4a08-b1dc-6c5d3d5a616d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 67639e81b04635452e1ed844fe2d7245aa96a4fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-user-queries-in-azure-sql-data-warehouse"></a><span data-ttu-id="d06e7-103">Azure SQL veri ambarı İzleyicisi kullanıcı sorguları</span><span class="sxs-lookup"><span data-stu-id="d06e7-103">Monitor user queries in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="d06e7-104">Merhaba konuları, en iyi yöntemler ve SQL Data Warehouse kullanıcı sorgularda izleme görevleri genel bakış.</span><span class="sxs-lookup"><span data-stu-id="d06e7-104">Overview of hello considerations, best practices, and tasks for monitoring user queries in SQL Data Warehouse.</span></span>

| <span data-ttu-id="d06e7-105">Kategori</span><span class="sxs-lookup"><span data-stu-id="d06e7-105">Category</span></span> | <span data-ttu-id="d06e7-106">Görev ya da göz önünde bulundurarak</span><span class="sxs-lookup"><span data-stu-id="d06e7-106">Task or consideration</span></span> | <span data-ttu-id="d06e7-107">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d06e7-107">Description</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="d06e7-108">Yavaş performans</span><span class="sxs-lookup"><span data-stu-id="d06e7-108">Slow performance</span></span> |<span data-ttu-id="d06e7-109">Uzun süre çalışan kullanıcı sorgu Bul</span><span class="sxs-lookup"><span data-stu-id="d06e7-109">Find a long-running user query</span></span> |<span data-ttu-id="d06e7-110">[Uzun süre çalışan sorgular Bul][Find long-running queries]</span><span class="sxs-lookup"><span data-stu-id="d06e7-110">[Find long-running queries][Find long-running queries]</span></span> |
| <span data-ttu-id="d06e7-111">Eşzamanlılık</span><span class="sxs-lookup"><span data-stu-id="d06e7-111">Concurrency</span></span> |<span data-ttu-id="d06e7-112">Toouser sorguları eşzamanlı kaynak atama</span><span class="sxs-lookup"><span data-stu-id="d06e7-112">Assign concurrent resources toouser queries</span></span> |<span data-ttu-id="d06e7-113">[Eşzamanlılık ve iş yükü yönetimi][Concurrency and workload management]</span><span class="sxs-lookup"><span data-stu-id="d06e7-113">[Concurrency and workload management][Concurrency and workload management]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d06e7-114">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d06e7-114">Next steps</span></span>
<span data-ttu-id="d06e7-115">Daha fazla yönetim ipuçları toohello head [yönetimine genel bakış][Management overview].</span><span class="sxs-lookup"><span data-stu-id="d06e7-115">For more management tips, head over toohello [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Find long-running queries]: sql-data-warehouse-manage-monitor.md
[Concurrency and workload management]: sql-data-warehouse-develop-concurrency.md
[Management overview]: sql-data-warehouse-overview-manage.md

<!--MSDN references-->


<!--Other Web references-->
