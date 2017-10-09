---
title: "aaaDesign ilk Azure SQL veritabanınızı - C# | Microsoft Docs"
description: "İlk Azure SQL veritabanınızı toodesign öğrenin ve ADO.NET kullanarak C# programı ile tooit bağlanın."
services: sql-database
documentationcenter: 
author: MightyPen
manager: craigg-msft
editor: CarlRabeler
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: develop databases
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 07/31/2017
ms.author: genemi;carlrab
ms.openlocfilehash: 8161de24bff1ec2fa307efa93adab2bd1b761fd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="design-an-azure-sql-database-and-connect-with-cx23-and-adonet"></a><span data-ttu-id="ba01a-103">Bir Azure SQL veritabanı tasarlamak ve C & #x23 bağlanın; ve ADO.NET</span><span class="sxs-lookup"><span data-stu-id="ba01a-103">Design an Azure SQL database and connect with C&#x23; and ADO.NET</span></span>

<span data-ttu-id="ba01a-104">Azure SQL veritabanı bir ilişkisel veritabanı-olarak-a (DBaaS) hello Microsoft Cloud ("Azure") hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="ba01a-104">Azure SQL Database is a relational database-as-a service (DBaaS) in hello Microsoft Cloud ("Azure").</span></span> <span data-ttu-id="ba01a-105">Bu öğreticide, toouse nasıl hello Azure portalı ve Visual Studio ile ADO.NET öğrenin:</span><span class="sxs-lookup"><span data-stu-id="ba01a-105">In this tutorial, you learn how toouse hello Azure portal and ADO.NET with Visual Studio to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="ba01a-106">Hello Azure portalında bir veritabanı oluşturun</span><span class="sxs-lookup"><span data-stu-id="ba01a-106">Create a database in hello Azure portal</span></span>
> * <span data-ttu-id="ba01a-107">Hello Azure portal sunucu düzeyinde güvenlik duvarı kuralında ayarlama</span><span class="sxs-lookup"><span data-stu-id="ba01a-107">Set up a server-level firewall rule in hello Azure portal</span></span>
> * <span data-ttu-id="ba01a-108">ADO.NET ve Visual Studio ile toohello veritabanına bağlanın</span><span class="sxs-lookup"><span data-stu-id="ba01a-108">Connect toohello database with ADO.NET and Visual Studio</span></span>
> * <span data-ttu-id="ba01a-109">ADO.NET ile tabloları oluşturma</span><span class="sxs-lookup"><span data-stu-id="ba01a-109">Create tables with ADO.NET</span></span>
> * <span data-ttu-id="ba01a-110">Ekle, Güncelleştir ve ADO.NET verilerle silme</span><span class="sxs-lookup"><span data-stu-id="ba01a-110">Insert, update, and delete data with ADO.NET</span></span> 
> * <span data-ttu-id="ba01a-111">ADO.NET veri sorgulama</span><span class="sxs-lookup"><span data-stu-id="ba01a-111">Query data ADO.NET</span></span>

<span data-ttu-id="ba01a-112">Bir Azure aboneliğiniz yoksa [ücretsiz bir hesap oluşturma](https://azure.microsoft.com/free/) başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="ba01a-112">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba01a-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ba01a-113">Prerequisites</span></span>

<span data-ttu-id="ba01a-114">[Visual Studio Community 2017, Visual Studio Professional 2017 veya Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/) yüklemesi.</span><span class="sxs-lookup"><span data-stu-id="ba01a-114">An installation of [Visual Studio Community 2017, Visual Studio Professional 2017, or Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span></span>

<!-- hello following included .md, sql-database-tutorial-portal-create-firewall-connection-1.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-tutorial-portal-create-firewall-connection-1](../../includes/sql-database-tutorial-portal-create-firewall-connection-1.md)]


<!-- hello following included .md, sql-database-csharp-adonet-create-query-2.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-csharp-adonet-create-query-2](../../includes/sql-database-csharp-adonet-create-query-2.md)]


## <a name="next-steps"></a><span data-ttu-id="ba01a-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ba01a-115">Next steps</span></span>

<span data-ttu-id="ba01a-116">Bu öğreticide temel veritabanı görevlerini gibi bir veritabanı ve tablo oluşturma hakkında bilgi edindiniz, yükleme ve verileri sorgulamak ve zaman içinde hello veritabanı tooa önceki noktası geri.</span><span class="sxs-lookup"><span data-stu-id="ba01a-116">In this tutorial, you learned basic database tasks such as create a database and tables, load and query data, and restore hello database tooa previous point in time.</span></span> <span data-ttu-id="ba01a-117">Şunları öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="ba01a-117">You learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="ba01a-118">Veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ba01a-118">Create a database</span></span>
> * <span data-ttu-id="ba01a-119">Bir güvenlik duvarı kuralı ayarlamak</span><span class="sxs-lookup"><span data-stu-id="ba01a-119">Set up a firewall rule</span></span>
> * <span data-ttu-id="ba01a-120">Toohello veritabanı ile bağlantı [Visual Studio ve C#](sql-database-connect-query-dotnet-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="ba01a-120">Connect toohello database with [Visual Studio and C#](sql-database-connect-query-dotnet-visual-studio.md)</span></span>
> * <span data-ttu-id="ba01a-121">Tabloları oluşturma</span><span class="sxs-lookup"><span data-stu-id="ba01a-121">Create tables</span></span>
> * <span data-ttu-id="ba01a-122">Ekle, Güncelleştir ve verilerini sil</span><span class="sxs-lookup"><span data-stu-id="ba01a-122">Insert, update, and delete data</span></span>
> * <span data-ttu-id="ba01a-123">Verileri sorgulama</span><span class="sxs-lookup"><span data-stu-id="ba01a-123">Query data</span></span>

<span data-ttu-id="ba01a-124">Verilerinizi geçirme hakkında toohello sonraki öğretici toolearn ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="ba01a-124">Advance toohello next tutorial toolearn about migrating your data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="ba01a-125">SQL Server veritabanı tooAzure SQL veritabanına geçirme</span><span class="sxs-lookup"><span data-stu-id="ba01a-125">Migrate your SQL Server database tooAzure SQL Database</span></span>](sql-database-migrate-your-sql-server-database.md)

