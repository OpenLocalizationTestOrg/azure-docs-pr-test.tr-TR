---
title: aaaConnect tooAzure SQL Data Warehouse - SSMS | Microsoft Docs
description: "SQL Server Management Studio (SSMS) tooconnect tooand sorgu Azure SQL Data Warehouse kullanın."
services: sql-data-warehouse
documentationcenter: 
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 299e50b3-e68a-471c-8aee-b0b9874781bd
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: bcbaf7139d2e5183b388b8d58c015cf5ad726722
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sql-server-management-studio-ssms"></a><span data-ttu-id="09ee7-103">SQL Server Management Studio (SSMS) ile tooSQL veri ambarına bağlanma</span><span class="sxs-lookup"><span data-stu-id="09ee7-103">Connect tooSQL Data Warehouse with SQL Server Management Studio (SSMS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="09ee7-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="09ee7-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="09ee7-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="09ee7-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="09ee7-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="09ee7-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="09ee7-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="09ee7-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="09ee7-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="09ee7-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="09ee7-109">SQL Server Management Studio (SSMS) tooconnect tooand sorgu Azure SQL Data Warehouse kullanın.</span><span class="sxs-lookup"><span data-stu-id="09ee7-109">Use SQL Server Management Studio (SSMS) tooconnect tooand query Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="09ee7-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="09ee7-110">Prerequisites</span></span>
<span data-ttu-id="09ee7-111">toouse Bu öğretici, gerekir:</span><span class="sxs-lookup"><span data-stu-id="09ee7-111">toouse this tutorial, you need:</span></span>

* <span data-ttu-id="09ee7-112">Var olan bir SQL veri ambarı.</span><span class="sxs-lookup"><span data-stu-id="09ee7-112">An existing SQL data warehouse.</span></span> <span data-ttu-id="09ee7-113">toocreate biri bkz [SQL Data Warehouse oluşturma][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="09ee7-113">toocreate one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="09ee7-114">SQL Server Management Studio (yüklü SSMS).</span><span class="sxs-lookup"><span data-stu-id="09ee7-114">SQL Server Management Studio (SSMS) installed.</span></span> <span data-ttu-id="09ee7-115">[SSMS yükleme] [ Install SSMS] ücretsiz, zaten yoksa.</span><span class="sxs-lookup"><span data-stu-id="09ee7-115">[Install SSMS][Install SSMS] for free if you don't already have it.</span></span>
* <span data-ttu-id="09ee7-116">Merhaba SQL server tam adı.</span><span class="sxs-lookup"><span data-stu-id="09ee7-116">hello fully qualified SQL server name.</span></span> <span data-ttu-id="09ee7-117">toofind Bu, bkz: [tooSQL veri ambarına bağlanmak][Connect tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="09ee7-117">toofind this, see [Connect tooSQL Data Warehouse][Connect tooSQL Data Warehouse].</span></span>

## <a name="1-connect-tooyour-sql-data-warehouse"></a><span data-ttu-id="09ee7-118">1. SQL veri ambarı tooyour Bağlan</span><span class="sxs-lookup"><span data-stu-id="09ee7-118">1. Connect tooyour SQL Data Warehouse</span></span>
1. <span data-ttu-id="09ee7-119">SSMS açın.</span><span class="sxs-lookup"><span data-stu-id="09ee7-119">Open SSMS.</span></span>
2. <span data-ttu-id="09ee7-120">Nesne Gezgini'ni açın.</span><span class="sxs-lookup"><span data-stu-id="09ee7-120">Open Object Explorer.</span></span> <span data-ttu-id="09ee7-121">toodo Bu, select **dosya** > **bağlanmak Nesne Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="09ee7-121">toodo this, select **File** > **Connect Object Explorer**.</span></span>
   
    ![SQL Server Nesne Gezgini][1]
3. <span data-ttu-id="09ee7-123">Merhaba Bağlan tooServer penceresinde hello alanları doldurun.</span><span class="sxs-lookup"><span data-stu-id="09ee7-123">Fill in hello fields in hello Connect tooServer window.</span></span>
   
    ![TooServer Bağlan][2]
   
   * <span data-ttu-id="09ee7-125">**Sunucu adı**</span><span class="sxs-lookup"><span data-stu-id="09ee7-125">**Server name**.</span></span> <span data-ttu-id="09ee7-126">Merhaba girin **sunucu adı** önceden tanımlanmış.</span><span class="sxs-lookup"><span data-stu-id="09ee7-126">Enter hello **server name** previously identified.</span></span>
   * <span data-ttu-id="09ee7-127">**Kimlik Doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="09ee7-127">**Authentication**.</span></span> <span data-ttu-id="09ee7-128">**SQL Server Kimlik Doğrulaması**'nı veya **Active Directory Tümleşik Kimlik Doğrulaması**'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="09ee7-128">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="09ee7-129">**Kullanıcı Adı** ve **Parola**.</span><span class="sxs-lookup"><span data-stu-id="09ee7-129">**User Name** and **Password**.</span></span> <span data-ttu-id="09ee7-130">Yukarıda SQL Server Kimlik Doğrulaması seçiliyse kullanıcı adını ve parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="09ee7-130">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="09ee7-131">**Bağlan**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="09ee7-131">Click **Connect**.</span></span>
4. <span data-ttu-id="09ee7-132">tooexplore, Azure SQL sunucunuzu genişletin.</span><span class="sxs-lookup"><span data-stu-id="09ee7-132">tooexplore, expand your Azure SQL server.</span></span> <span data-ttu-id="09ee7-133">Merhaba sunucuyla ilişkili hello veritabanlarını görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="09ee7-133">You can view hello databases associated with hello server.</span></span> <span data-ttu-id="09ee7-134">Örnek veritabanınızdaki AdventureWorksDW toosee hello tabloları genişletin.</span><span class="sxs-lookup"><span data-stu-id="09ee7-134">Expand AdventureWorksDW toosee hello tables in your sample database.</span></span>
   
    ![AdventureWorksDW'yi araştırma][3]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="09ee7-136">2. Örnek sorgu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="09ee7-136">2. Run a sample query</span></span>
<span data-ttu-id="09ee7-137">Bir bağlantı kurulan tooyour veritabanı kaldırıldı, bir sorgu yazalım.</span><span class="sxs-lookup"><span data-stu-id="09ee7-137">Now that a connection has been established tooyour database, let's write a query.</span></span>

1. <span data-ttu-id="09ee7-138">SQL Server Nesne Gezgini'nde veritabanınıza sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="09ee7-138">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="09ee7-139">**Yeni Sorgu**'yu seçin.</span><span class="sxs-lookup"><span data-stu-id="09ee7-139">Select **New Query**.</span></span> <span data-ttu-id="09ee7-140">Yeni bir sorgu penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="09ee7-140">A new query window opens.</span></span>
   
    ![Yeni sorgu][4]
3. <span data-ttu-id="09ee7-142">Şu TSQL sorgusunu hello sorgu penceresine kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="09ee7-142">Copy this TSQL query into hello query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="09ee7-143">Merhaba sorgu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="09ee7-143">Run hello query.</span></span> <span data-ttu-id="09ee7-144">toodo bunu, `Execute` veya kullanım hello aşağıdaki kısayol: `F5`.</span><span class="sxs-lookup"><span data-stu-id="09ee7-144">toodo this, click `Execute` or use hello following shortcut: `F5`.</span></span>
   
    ![Sorgu çalıştırma][5]
5. <span data-ttu-id="09ee7-146">Merhaba sorgu sonuçlarına bakın.</span><span class="sxs-lookup"><span data-stu-id="09ee7-146">Look at hello query results.</span></span> <span data-ttu-id="09ee7-147">Bu örnekte, hello Factınternetsales tablosunda 60398 satır var.</span><span class="sxs-lookup"><span data-stu-id="09ee7-147">In this example, hello FactInternetSales table has 60398 rows.</span></span>
   
    ![Sorgu sonuçları][6]

## <a name="next-steps"></a><span data-ttu-id="09ee7-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="09ee7-149">Next steps</span></span>
<span data-ttu-id="09ee7-150">Bağlanma ve sorgulama şimdi deneyin [hello Powerbı ile verileri görselleştirmeyi][visualizing hello data with PowerBI].</span><span class="sxs-lookup"><span data-stu-id="09ee7-150">Now that you can connect and query, try [visualizing hello data with PowerBI][visualizing hello data with PowerBI].</span></span>

<span data-ttu-id="09ee7-151">ortamınız için Azure Active Directory kimlik doğrulaması, tooconfigure bkz [tooSQL veri ambarı kimlik doğrulaması][Authenticate tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="09ee7-151">tooconfigure your environment for Azure Active Directory authentication, see [Authenticate tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md 

<!--Other-->
[Azure portal]: https://portal.azure.com
[Install SSMS]: https://msdn.microsoft.com/en-US/library/hh213248.aspx


<!--Image references-->

[1]: media/sql-data-warehouse-query-ssms/connect-object-explorer.png
[2]: media/sql-data-warehouse-query-ssms/connect-object-explorer1.png
[3]: media/sql-data-warehouse-query-ssms/explore-tables.png
[4]: media/sql-data-warehouse-query-ssms/new-query.png
[5]: media/sql-data-warehouse-query-ssms/execute-query.png
[6]: media/sql-data-warehouse-query-ssms/results.png
