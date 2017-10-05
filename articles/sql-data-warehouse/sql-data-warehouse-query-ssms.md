---
title: "Azure SQL veri ambarı - SSMS bağlanma | Microsoft Docs"
description: "SQL Server Management Studio (SSMS) bağlanmak ve Azure SQL Data Warehouse sorgulamak için kullanın."
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
ms.openlocfilehash: 207fb9fd861c66039fbde89681aed3df3a2f4021
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-sql-data-warehouse-with-sql-server-management-studio-ssms"></a><span data-ttu-id="b6afa-103">SQL Server Management Studio (SSMS) ile SQL Data Warehouse'a bağlanma</span><span class="sxs-lookup"><span data-stu-id="b6afa-103">Connect to SQL Data Warehouse with SQL Server Management Studio (SSMS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b6afa-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="b6afa-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="b6afa-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="b6afa-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="b6afa-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b6afa-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="b6afa-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="b6afa-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="b6afa-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="b6afa-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="b6afa-109">SQL Server Management Studio (SSMS) bağlanmak ve Azure SQL Data Warehouse sorgulamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="b6afa-109">Use SQL Server Management Studio (SSMS) to connect to and query Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b6afa-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b6afa-110">Prerequisites</span></span>
<span data-ttu-id="b6afa-111">Bu öğreticiyi kullanmak için şunlar gerekir:</span><span class="sxs-lookup"><span data-stu-id="b6afa-111">To use this tutorial, you need:</span></span>

* <span data-ttu-id="b6afa-112">Var olan bir SQL veri ambarı.</span><span class="sxs-lookup"><span data-stu-id="b6afa-112">An existing SQL data warehouse.</span></span> <span data-ttu-id="b6afa-113">Bir tane oluşturmak için bkz. [SQL Veri Ambarı oluşturma][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="b6afa-113">To create one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="b6afa-114">SQL Server Management Studio (yüklü SSMS).</span><span class="sxs-lookup"><span data-stu-id="b6afa-114">SQL Server Management Studio (SSMS) installed.</span></span> <span data-ttu-id="b6afa-115">[SSMS yükleme] [ Install SSMS] ücretsiz, zaten yoksa.</span><span class="sxs-lookup"><span data-stu-id="b6afa-115">[Install SSMS][Install SSMS] for free if you don't already have it.</span></span>
* <span data-ttu-id="b6afa-116">Tam SQL server adı.</span><span class="sxs-lookup"><span data-stu-id="b6afa-116">The fully qualified SQL server name.</span></span> <span data-ttu-id="b6afa-117">Bunu bulmak için bkz. [SQL Veri Ambarı'na bağlanma][Connect to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="b6afa-117">To find this, see [Connect to SQL Data Warehouse][Connect to SQL Data Warehouse].</span></span>

## <a name="1-connect-to-your-sql-data-warehouse"></a><span data-ttu-id="b6afa-118">1. SQL Data Warehouse'unuza bağlanma</span><span class="sxs-lookup"><span data-stu-id="b6afa-118">1. Connect to your SQL Data Warehouse</span></span>
1. <span data-ttu-id="b6afa-119">SSMS açın.</span><span class="sxs-lookup"><span data-stu-id="b6afa-119">Open SSMS.</span></span>
2. <span data-ttu-id="b6afa-120">Nesne Gezgini'ni açın.</span><span class="sxs-lookup"><span data-stu-id="b6afa-120">Open Object Explorer.</span></span> <span data-ttu-id="b6afa-121">Bunu yapmak için seçin **dosya** > **bağlanmak Nesne Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="b6afa-121">To do this, select **File** > **Connect Object Explorer**.</span></span>
   
    ![SQL Server Nesne Gezgini][1]
3. <span data-ttu-id="b6afa-123">Sunucuya Bağlan penceresindeki alanları doldurun.</span><span class="sxs-lookup"><span data-stu-id="b6afa-123">Fill in the fields in the Connect to Server window.</span></span>
   
    ![Sunucuya bağlanma][2]
   
   * <span data-ttu-id="b6afa-125">**Sunucu adı**</span><span class="sxs-lookup"><span data-stu-id="b6afa-125">**Server name**.</span></span> <span data-ttu-id="b6afa-126">Önceden tanımlanmış olan **sunucu adını** girin.</span><span class="sxs-lookup"><span data-stu-id="b6afa-126">Enter the **server name** previously identified.</span></span>
   * <span data-ttu-id="b6afa-127">**Kimlik Doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="b6afa-127">**Authentication**.</span></span> <span data-ttu-id="b6afa-128">**SQL Server Kimlik Doğrulaması**'nı veya **Active Directory Tümleşik Kimlik Doğrulaması**'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="b6afa-128">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="b6afa-129">**Kullanıcı Adı** ve **Parola**.</span><span class="sxs-lookup"><span data-stu-id="b6afa-129">**User Name** and **Password**.</span></span> <span data-ttu-id="b6afa-130">Yukarıda SQL Server Kimlik Doğrulaması seçiliyse kullanıcı adını ve parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="b6afa-130">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="b6afa-131">**Bağlan**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b6afa-131">Click **Connect**.</span></span>
4. <span data-ttu-id="b6afa-132">Araştırmak için Azure SQL sunucunuzu genişletin.</span><span class="sxs-lookup"><span data-stu-id="b6afa-132">To explore, expand your Azure SQL server.</span></span> <span data-ttu-id="b6afa-133">Sunucuyla ilişkili veritabanlarını görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6afa-133">You can view the databases associated with the server.</span></span> <span data-ttu-id="b6afa-134">Örnek veritabanınızdaki tabolaları görmek için AdventureWorksDW'yi genişletin.</span><span class="sxs-lookup"><span data-stu-id="b6afa-134">Expand AdventureWorksDW to see the tables in your sample database.</span></span>
   
    ![AdventureWorksDW'yi araştırma][3]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="b6afa-136">2. Örnek sorgu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b6afa-136">2. Run a sample query</span></span>
<span data-ttu-id="b6afa-137">Artık veritabanınızla bağlantı kurulduğuna göre bir sorgu yazalım.</span><span class="sxs-lookup"><span data-stu-id="b6afa-137">Now that a connection has been established to your database, let's write a query.</span></span>

1. <span data-ttu-id="b6afa-138">SQL Server Nesne Gezgini'nde veritabanınıza sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b6afa-138">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="b6afa-139">**Yeni Sorgu**'yu seçin.</span><span class="sxs-lookup"><span data-stu-id="b6afa-139">Select **New Query**.</span></span> <span data-ttu-id="b6afa-140">Yeni bir sorgu penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="b6afa-140">A new query window opens.</span></span>
   
    ![Yeni sorgu][4]
3. <span data-ttu-id="b6afa-142">Şu TSQL sorgusunu sorgu penceresine kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="b6afa-142">Copy this TSQL query into the query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="b6afa-143">Sorguyu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b6afa-143">Run the query.</span></span> <span data-ttu-id="b6afa-144">Bunu yapmak için tıklatın `Execute` veya şu kısayolu kullanın: `F5`.</span><span class="sxs-lookup"><span data-stu-id="b6afa-144">To do this, click `Execute` or use the following shortcut: `F5`.</span></span>
   
    ![Sorgu çalıştırma][5]
5. <span data-ttu-id="b6afa-146">Sorgu sonuçlarına bakın.</span><span class="sxs-lookup"><span data-stu-id="b6afa-146">Look at the query results.</span></span> <span data-ttu-id="b6afa-147">Bu örnekte FactInternetSales tablosunda 60398 satır var.</span><span class="sxs-lookup"><span data-stu-id="b6afa-147">In this example, the FactInternetSales table has 60398 rows.</span></span>
   
    ![Sorgu sonuçları][6]

## <a name="next-steps"></a><span data-ttu-id="b6afa-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b6afa-149">Next steps</span></span>
<span data-ttu-id="b6afa-150">Artık bağlanıp sorgulama yapabildiğinize göre [PowerBI ile verileri görselleştirmeyi][visualizing the data with PowerBI] deneyin.</span><span class="sxs-lookup"><span data-stu-id="b6afa-150">Now that you can connect and query, try [visualizing the data with PowerBI][visualizing the data with PowerBI].</span></span>

<span data-ttu-id="b6afa-151">Ortamınızı Azure Active Directory kimlik doğrulaması için yapılandırmak üzere bkz. [SQL Veri Ambarı’nda kimlik doğrulama][Authenticate to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="b6afa-151">To configure your environment for Azure Active Directory authentication, see [Authenticate to SQL Data Warehouse][Authenticate to SQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect to SQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Authenticate to SQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing the data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md 

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
