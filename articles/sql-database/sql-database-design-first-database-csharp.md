---
title: "İlk Azure SQL veritabanınızı - C# tasarlama | Microsoft Docs"
description: "İlk Azure SQL veritabanınızı tasarım ve ADO.NET kullanarak C# programı ile bağlanma hakkında bilgi edinme."
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
ms.openlocfilehash: d9731cf5399cce6f103129ccda521f2867bd8da6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="design-an-azure-sql-database-and-connect-with-cx23-and-adonet"></a><span data-ttu-id="aa6f9-103">Bir Azure SQL veritabanı tasarlamak ve C & #x23 bağlanın; ve ADO.NET</span><span class="sxs-lookup"><span data-stu-id="aa6f9-103">Design an Azure SQL database and connect with C&#x23; and ADO.NET</span></span>

<span data-ttu-id="aa6f9-104">Azure SQL veritabanı bir ilişkisel veritabanı-olarak-a (DBaaS) ("Azure") Microsoft Cloud hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="aa6f9-104">Azure SQL Database is a relational database-as-a service (DBaaS) in the Microsoft Cloud ("Azure").</span></span> <span data-ttu-id="aa6f9-105">Bu öğreticide, Azure portal ve ADO.NET için Visual Studio ile nasıl kullanılacağını öğrenin:</span><span class="sxs-lookup"><span data-stu-id="aa6f9-105">In this tutorial, you learn how to use the Azure portal and ADO.NET with Visual Studio to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="aa6f9-106">Azure portalında bir veritabanı oluşturun</span><span class="sxs-lookup"><span data-stu-id="aa6f9-106">Create a database in the Azure portal</span></span>
> * <span data-ttu-id="aa6f9-107">Azure portalında bir sunucu düzeyinde güvenlik duvarı kuralı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="aa6f9-107">Set up a server-level firewall rule in the Azure portal</span></span>
> * <span data-ttu-id="aa6f9-108">ADO.NET ve Visual Studio ile veritabanına bağlan</span><span class="sxs-lookup"><span data-stu-id="aa6f9-108">Connect to the database with ADO.NET and Visual Studio</span></span>
> * <span data-ttu-id="aa6f9-109">ADO.NET ile tabloları oluşturma</span><span class="sxs-lookup"><span data-stu-id="aa6f9-109">Create tables with ADO.NET</span></span>
> * <span data-ttu-id="aa6f9-110">Ekle, Güncelleştir ve ADO.NET verilerle silme</span><span class="sxs-lookup"><span data-stu-id="aa6f9-110">Insert, update, and delete data with ADO.NET</span></span> 
> * <span data-ttu-id="aa6f9-111">ADO.NET veri sorgulama</span><span class="sxs-lookup"><span data-stu-id="aa6f9-111">Query data ADO.NET</span></span>

<span data-ttu-id="aa6f9-112">Bir Azure aboneliğiniz yoksa [ücretsiz bir hesap oluşturma](https://azure.microsoft.com/free/) başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="aa6f9-112">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa6f9-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="aa6f9-113">Prerequisites</span></span>

<span data-ttu-id="aa6f9-114">[Visual Studio Community 2017, Visual Studio Professional 2017 veya Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/) yüklemesi.</span><span class="sxs-lookup"><span data-stu-id="aa6f9-114">An installation of [Visual Studio Community 2017, Visual Studio Professional 2017, or Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span></span>

<!-- The following included .md, sql-database-tutorial-portal-create-firewall-connection-1.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-tutorial-portal-create-firewall-connection-1](../../includes/sql-database-tutorial-portal-create-firewall-connection-1.md)]


<!-- The following included .md, sql-database-csharp-adonet-create-query-2.md, is long.
And it starts with a ## H2.
-->

[!INCLUDE [sql-database-csharp-adonet-create-query-2](../../includes/sql-database-csharp-adonet-create-query-2.md)]


## <a name="next-steps"></a><span data-ttu-id="aa6f9-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="aa6f9-115">Next steps</span></span>

<span data-ttu-id="aa6f9-116">Bu öğreticide, temel veritabanı görevlerini gibi bir veritabanı ve tablo oluşturma hakkında bilgi edindiniz, yükleme ve verileri sorgulamak ve veritabanını zaman içinde daha önceki bir noktaya geri.</span><span class="sxs-lookup"><span data-stu-id="aa6f9-116">In this tutorial, you learned basic database tasks such as create a database and tables, load and query data, and restore the database to a previous point in time.</span></span> <span data-ttu-id="aa6f9-117">Size nasıl öğrenilen için:</span><span class="sxs-lookup"><span data-stu-id="aa6f9-117">You learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="aa6f9-118">Veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="aa6f9-118">Create a database</span></span>
> * <span data-ttu-id="aa6f9-119">Bir güvenlik duvarı kuralı ayarlamak</span><span class="sxs-lookup"><span data-stu-id="aa6f9-119">Set up a firewall rule</span></span>
> * <span data-ttu-id="aa6f9-120">Veritabanı ile bağlanmak [Visual Studio ve C#](sql-database-connect-query-dotnet-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="aa6f9-120">Connect to the database with [Visual Studio and C#](sql-database-connect-query-dotnet-visual-studio.md)</span></span>
> * <span data-ttu-id="aa6f9-121">Tabloları oluşturma</span><span class="sxs-lookup"><span data-stu-id="aa6f9-121">Create tables</span></span>
> * <span data-ttu-id="aa6f9-122">Ekle, Güncelleştir ve verilerini sil</span><span class="sxs-lookup"><span data-stu-id="aa6f9-122">Insert, update, and delete data</span></span>
> * <span data-ttu-id="aa6f9-123">Verileri sorgulama</span><span class="sxs-lookup"><span data-stu-id="aa6f9-123">Query data</span></span>

<span data-ttu-id="aa6f9-124">Verilerinizi geçirme hakkında bilgi edinmek için sonraki öğretici ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="aa6f9-124">Advance to the next tutorial to learn about migrating your data.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="aa6f9-125">SQL Server veritabanını Azure SQL veritabanına geçirme</span><span class="sxs-lookup"><span data-stu-id="aa6f9-125">Migrate your SQL Server database to Azure SQL Database</span></span>](sql-database-migrate-your-sql-server-database.md)

