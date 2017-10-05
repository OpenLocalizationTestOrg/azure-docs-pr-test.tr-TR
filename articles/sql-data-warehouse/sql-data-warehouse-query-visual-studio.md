---
title: "Azure SQL Veri Ambarı'na Bağlanma - VSTS | Microsoft Belgeleri"
description: "Visual Studio ile SQL Data Warehouse'u sorgulayın."
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: daace889-95e5-4826-b2fc-047eac9d6d95
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 1e44c6c3c47034a892753c69c5ef22a5eac18c0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-sql-data-warehouse-with-visual-studio-and-ssdt"></a><span data-ttu-id="daf77-103">Visual Studio ve SSDT ile SQL Veri Ambarı'na bağlanma</span><span class="sxs-lookup"><span data-stu-id="daf77-103">Connect to SQL Data Warehouse with Visual Studio and SSDT</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="daf77-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="daf77-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="daf77-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="daf77-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="daf77-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="daf77-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="daf77-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="daf77-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="daf77-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="daf77-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="daf77-109">Azure SQL Data Warehouse’u yalnızca birkaç dakika içinde sorgulamak için Visual Studio kullanın.</span><span class="sxs-lookup"><span data-stu-id="daf77-109">Use Visual Studio to query Azure SQL Data Warehouse in just a few minutes.</span></span> <span data-ttu-id="daf77-110">Bu yöntem Visual Studio’daki SQL Server Veri Araçları (SSDT) uzantısını kullanır.</span><span class="sxs-lookup"><span data-stu-id="daf77-110">This method uses the SQL Server Data Tools (SSDT) extension in Visual Studio.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="daf77-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="daf77-111">Prerequisites</span></span>
<span data-ttu-id="daf77-112">Bu öğreticiyi kullanmak için şunlar gerekir:</span><span class="sxs-lookup"><span data-stu-id="daf77-112">To use this tutorial, you need:</span></span>

* <span data-ttu-id="daf77-113">Var olan bir SQL veri ambarı.</span><span class="sxs-lookup"><span data-stu-id="daf77-113">An existing SQL data warehouse.</span></span> <span data-ttu-id="daf77-114">Bir tane oluşturmak için bkz. [SQL Veri Ambarı oluşturma][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="daf77-114">To create one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="daf77-115">Visual Studio için SSDT.</span><span class="sxs-lookup"><span data-stu-id="daf77-115">SSDT for Visual Studio.</span></span> <span data-ttu-id="daf77-116">Visual Studio varsa büyük olasılıkla buna da sahip olursunuz.</span><span class="sxs-lookup"><span data-stu-id="daf77-116">If you have Visual Studio, you probably already have this.</span></span> <span data-ttu-id="daf77-117">Yükleme yönergeleri ve seçenekleri için bkz. [Visual Studio’yu ve SSDT’yi yükleme][Installing Visual Studio and SSDT].</span><span class="sxs-lookup"><span data-stu-id="daf77-117">For installation instructions and options, see [Installing Visual Studio and SSDT][Installing Visual Studio and SSDT].</span></span>
* <span data-ttu-id="daf77-118">Tam SQL server adı.</span><span class="sxs-lookup"><span data-stu-id="daf77-118">The fully qualified SQL server name.</span></span> <span data-ttu-id="daf77-119">Bunu bulmak için bkz. [SQL Veri Ambarı'na bağlanma][Connect to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="daf77-119">To find this, see [Connect to SQL Data Warehouse][Connect to SQL Data Warehouse].</span></span>

## <a name="1-connect-to-your-sql-data-warehouse"></a><span data-ttu-id="daf77-120">1. SQL Data Warehouse'unuza bağlanma</span><span class="sxs-lookup"><span data-stu-id="daf77-120">1. Connect to your SQL Data Warehouse</span></span>
1. <span data-ttu-id="daf77-121">Visual Studio 2013 veya Visual Studio 2015'i açın.</span><span class="sxs-lookup"><span data-stu-id="daf77-121">Open Visual Studio 2013 or 2015.</span></span>
2. <span data-ttu-id="daf77-122">SQL Server Nesne Gezgini'ni açın.</span><span class="sxs-lookup"><span data-stu-id="daf77-122">Open SQL Server Object Explorer.</span></span> <span data-ttu-id="daf77-123">Bunu gerçekleştirmek için **Görünüm** > **SQL Server Nesne Gezgini**'ni seçin.</span><span class="sxs-lookup"><span data-stu-id="daf77-123">To do this, select **View** > **SQL Server Object Explorer**.</span></span>
   
    ![SQL Server Nesne Gezgini][1]
3. <span data-ttu-id="daf77-125">**SQL Server ekle** simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="daf77-125">Click the **Add SQL Server** icon.</span></span>
   
    ![SQL Server ekleme][2]
4. <span data-ttu-id="daf77-127">Sunucuya Bağlan penceresindeki alanları doldurun.</span><span class="sxs-lookup"><span data-stu-id="daf77-127">Fill in the fields in the Connect to Server window.</span></span>
   
    ![Sunucuya bağlanma][3]
   
   * <span data-ttu-id="daf77-129">**Sunucu adı**</span><span class="sxs-lookup"><span data-stu-id="daf77-129">**Server name**.</span></span> <span data-ttu-id="daf77-130">Önceden tanımlanmış olan **sunucu adını** girin.</span><span class="sxs-lookup"><span data-stu-id="daf77-130">Enter the **server name** previously identified.</span></span>
   * <span data-ttu-id="daf77-131">**Kimlik Doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="daf77-131">**Authentication**.</span></span> <span data-ttu-id="daf77-132">**SQL Server Kimlik Doğrulaması**'nı veya **Active Directory Tümleşik Kimlik Doğrulaması**'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="daf77-132">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="daf77-133">**Kullanıcı Adı** ve **Parola**.</span><span class="sxs-lookup"><span data-stu-id="daf77-133">**User Name** and **Password**.</span></span> <span data-ttu-id="daf77-134">Yukarıda SQL Server Kimlik Doğrulaması seçiliyse kullanıcı adını ve parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="daf77-134">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="daf77-135">**Bağlan**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="daf77-135">Click **Connect**.</span></span>
5. <span data-ttu-id="daf77-136">Araştırmak için Azure SQL sunucunuzu genişletin.</span><span class="sxs-lookup"><span data-stu-id="daf77-136">To explore, expand your Azure SQL server.</span></span> <span data-ttu-id="daf77-137">Sunucuyla ilişkili veritabanlarını görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="daf77-137">You can view the databases associated with the server.</span></span> <span data-ttu-id="daf77-138">Örnek veritabanınızdaki tabolaları görmek için AdventureWorksDW'yi genişletin.</span><span class="sxs-lookup"><span data-stu-id="daf77-138">Expand AdventureWorksDW to see the tables in your sample database.</span></span>
   
    ![AdventureWorksDW'yi araştırma][4]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="daf77-140">2. Örnek sorgu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="daf77-140">2. Run a sample query</span></span>
<span data-ttu-id="daf77-141">Artık veritabanınızla bağlantı kurulduğuna göre bir sorgu yazalım.</span><span class="sxs-lookup"><span data-stu-id="daf77-141">Now that a connection has been established to your database, let's write a query.</span></span>

1. <span data-ttu-id="daf77-142">SQL Server Nesne Gezgini'nde veritabanınıza sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="daf77-142">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="daf77-143">**Yeni Sorgu**'yu seçin.</span><span class="sxs-lookup"><span data-stu-id="daf77-143">Select **New Query**.</span></span> <span data-ttu-id="daf77-144">Yeni bir sorgu penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="daf77-144">A new query window opens.</span></span>
   
    ![Yeni sorgu][5]
3. <span data-ttu-id="daf77-146">Şu TSQL sorgusunu sorgu penceresine kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="daf77-146">Copy this TSQL query into the query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="daf77-147">Sorguyu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="daf77-147">Run the query.</span></span> <span data-ttu-id="daf77-148">Bunu gerçekleştirmek için yeşil ok simgesine tıklayın veya şu kısayolu kullanın: `CTRL`+`SHIFT`+`E`.</span><span class="sxs-lookup"><span data-stu-id="daf77-148">To do this, click the green arrow or use the following shortcut: `CTRL`+`SHIFT`+`E`.</span></span>
   
    ![Sorgu çalıştırma][6]
5. <span data-ttu-id="daf77-150">Sorgu sonuçlarına bakın.</span><span class="sxs-lookup"><span data-stu-id="daf77-150">Look at the query results.</span></span> <span data-ttu-id="daf77-151">Bu örnekte FactInternetSales tablosunda 60398 satır var.</span><span class="sxs-lookup"><span data-stu-id="daf77-151">In this example, the FactInternetSales table has 60398 rows.</span></span>
   
    ![Sorgu sonuçları][7]

## <a name="next-steps"></a><span data-ttu-id="daf77-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="daf77-153">Next steps</span></span>
<span data-ttu-id="daf77-154">Artık bağlanıp sorgulama yapabildiğinize göre [PowerBI ile verileri görselleştirmeyi][visualizing the data with PowerBI] deneyin.</span><span class="sxs-lookup"><span data-stu-id="daf77-154">Now that you can connect and query, try [visualizing the data with PowerBI][visualizing the data with PowerBI].</span></span>

<span data-ttu-id="daf77-155">Ortamınızı Azure Active Directory kimlik doğrulaması için yapılandırmak üzere bkz. [SQL Veri Ambarı’nda kimlik doğrulama][Authenticate to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="daf77-155">To configure your environment for Azure Active Directory authentication, see [Authenticate to SQL Data Warehouse][Authenticate to SQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect to SQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate to SQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing the data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->

[1]: media/sql-data-warehouse-query-visual-studio/open-ssdt.png
[2]: media/sql-data-warehouse-query-visual-studio/add-server.png
[3]: media/sql-data-warehouse-query-visual-studio/connection-dialog.png
[4]: media/sql-data-warehouse-query-visual-studio/explore-sample.png
[5]: media/sql-data-warehouse-query-visual-studio/new-query2.png
[6]: media/sql-data-warehouse-query-visual-studio/run-query.png
[7]: media/sql-data-warehouse-query-visual-studio/query-results.png
