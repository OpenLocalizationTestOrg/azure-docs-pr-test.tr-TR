---
title: aaaConnect tooAzure SQL Data Warehouse - VSTS | Microsoft Docs
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
ms.openlocfilehash: 55eef4dff3e0647be5a735295bc89b43eb456079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-visual-studio-and-ssdt"></a><span data-ttu-id="2ecaa-103">Visual Studio ve SSDT ile tooSQL veri ambarına bağlanma</span><span class="sxs-lookup"><span data-stu-id="2ecaa-103">Connect tooSQL Data Warehouse with Visual Studio and SSDT</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2ecaa-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="2ecaa-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="2ecaa-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="2ecaa-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="2ecaa-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2ecaa-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="2ecaa-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="2ecaa-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="2ecaa-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="2ecaa-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="2ecaa-109">Visual Studio tooquery Azure SQL Data Warehouse yalnızca birkaç dakika içinde kullanın.</span><span class="sxs-lookup"><span data-stu-id="2ecaa-109">Use Visual Studio tooquery Azure SQL Data Warehouse in just a few minutes.</span></span> <span data-ttu-id="2ecaa-110">Bu yöntem, Visual Studio'da hello SQL Server veri Araçları (SSDT) uzantısını kullanır.</span><span class="sxs-lookup"><span data-stu-id="2ecaa-110">This method uses hello SQL Server Data Tools (SSDT) extension in Visual Studio.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2ecaa-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2ecaa-111">Prerequisites</span></span>
<span data-ttu-id="2ecaa-112">toouse Bu öğretici, gerekir:</span><span class="sxs-lookup"><span data-stu-id="2ecaa-112">toouse this tutorial, you need:</span></span>

* <span data-ttu-id="2ecaa-113">Var olan bir SQL veri ambarı.</span><span class="sxs-lookup"><span data-stu-id="2ecaa-113">An existing SQL data warehouse.</span></span> <span data-ttu-id="2ecaa-114">toocreate biri bkz [SQL Data Warehouse oluşturma][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="2ecaa-114">toocreate one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="2ecaa-115">Visual Studio için SSDT.</span><span class="sxs-lookup"><span data-stu-id="2ecaa-115">SSDT for Visual Studio.</span></span> <span data-ttu-id="2ecaa-116">Visual Studio varsa büyük olasılıkla buna da sahip olursunuz.</span><span class="sxs-lookup"><span data-stu-id="2ecaa-116">If you have Visual Studio, you probably already have this.</span></span> <span data-ttu-id="2ecaa-117">Yükleme yönergeleri ve seçenekleri için bkz. [Visual Studio’yu ve SSDT’yi yükleme][Installing Visual Studio and SSDT].</span><span class="sxs-lookup"><span data-stu-id="2ecaa-117">For installation instructions and options, see [Installing Visual Studio and SSDT][Installing Visual Studio and SSDT].</span></span>
* <span data-ttu-id="2ecaa-118">Merhaba SQL server tam adı.</span><span class="sxs-lookup"><span data-stu-id="2ecaa-118">hello fully qualified SQL server name.</span></span> <span data-ttu-id="2ecaa-119">toofind Bu, bkz: [tooSQL veri ambarına bağlanmak][Connect tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="2ecaa-119">toofind this, see [Connect tooSQL Data Warehouse][Connect tooSQL Data Warehouse].</span></span>

## <a name="1-connect-tooyour-sql-data-warehouse"></a><span data-ttu-id="2ecaa-120">1. SQL veri ambarı tooyour Bağlan</span><span class="sxs-lookup"><span data-stu-id="2ecaa-120">1. Connect tooyour SQL Data Warehouse</span></span>
1. <span data-ttu-id="2ecaa-121">Visual Studio 2013 veya Visual Studio 2015'i açın.</span><span class="sxs-lookup"><span data-stu-id="2ecaa-121">Open Visual Studio 2013 or 2015.</span></span>
2. <span data-ttu-id="2ecaa-122">SQL Server Nesne Gezgini'ni açın.</span><span class="sxs-lookup"><span data-stu-id="2ecaa-122">Open SQL Server Object Explorer.</span></span> <span data-ttu-id="2ecaa-123">toodo Bu, select **Görünüm** > **SQL Server Nesne Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="2ecaa-123">toodo this, select **View** > **SQL Server Object Explorer**.</span></span>
   
    ![SQL Server Nesne Gezgini][1]
3. <span data-ttu-id="2ecaa-125">Merhaba tıklatın **SQL Server Ekle** simgesi.</span><span class="sxs-lookup"><span data-stu-id="2ecaa-125">Click hello **Add SQL Server** icon.</span></span>
   
    ![SQL Server ekleme][2]
4. <span data-ttu-id="2ecaa-127">Merhaba Bağlan tooServer penceresinde hello alanları doldurun.</span><span class="sxs-lookup"><span data-stu-id="2ecaa-127">Fill in hello fields in hello Connect tooServer window.</span></span>
   
    ![TooServer Bağlan][3]
   
   * <span data-ttu-id="2ecaa-129">**Sunucu adı**</span><span class="sxs-lookup"><span data-stu-id="2ecaa-129">**Server name**.</span></span> <span data-ttu-id="2ecaa-130">Merhaba girin **sunucu adı** önceden tanımlanmış.</span><span class="sxs-lookup"><span data-stu-id="2ecaa-130">Enter hello **server name** previously identified.</span></span>
   * <span data-ttu-id="2ecaa-131">**Kimlik Doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="2ecaa-131">**Authentication**.</span></span> <span data-ttu-id="2ecaa-132">**SQL Server Kimlik Doğrulaması**'nı veya **Active Directory Tümleşik Kimlik Doğrulaması**'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="2ecaa-132">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="2ecaa-133">**Kullanıcı Adı** ve **Parola**.</span><span class="sxs-lookup"><span data-stu-id="2ecaa-133">**User Name** and **Password**.</span></span> <span data-ttu-id="2ecaa-134">Yukarıda SQL Server Kimlik Doğrulaması seçiliyse kullanıcı adını ve parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="2ecaa-134">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="2ecaa-135">**Bağlan**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2ecaa-135">Click **Connect**.</span></span>
5. <span data-ttu-id="2ecaa-136">tooexplore, Azure SQL sunucunuzu genişletin.</span><span class="sxs-lookup"><span data-stu-id="2ecaa-136">tooexplore, expand your Azure SQL server.</span></span> <span data-ttu-id="2ecaa-137">Merhaba sunucuyla ilişkili hello veritabanlarını görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2ecaa-137">You can view hello databases associated with hello server.</span></span> <span data-ttu-id="2ecaa-138">Örnek veritabanınızdaki AdventureWorksDW toosee hello tabloları genişletin.</span><span class="sxs-lookup"><span data-stu-id="2ecaa-138">Expand AdventureWorksDW toosee hello tables in your sample database.</span></span>
   
    ![AdventureWorksDW'yi araştırma][4]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="2ecaa-140">2. Örnek sorgu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="2ecaa-140">2. Run a sample query</span></span>
<span data-ttu-id="2ecaa-141">Bir bağlantı kurulan tooyour veritabanı kaldırıldı, bir sorgu yazalım.</span><span class="sxs-lookup"><span data-stu-id="2ecaa-141">Now that a connection has been established tooyour database, let's write a query.</span></span>

1. <span data-ttu-id="2ecaa-142">SQL Server Nesne Gezgini'nde veritabanınıza sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2ecaa-142">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="2ecaa-143">**Yeni Sorgu**'yu seçin.</span><span class="sxs-lookup"><span data-stu-id="2ecaa-143">Select **New Query**.</span></span> <span data-ttu-id="2ecaa-144">Yeni bir sorgu penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="2ecaa-144">A new query window opens.</span></span>
   
    ![Yeni sorgu][5]
3. <span data-ttu-id="2ecaa-146">Şu TSQL sorgusunu hello sorgu penceresine kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="2ecaa-146">Copy this TSQL query into hello query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="2ecaa-147">Merhaba sorgu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2ecaa-147">Run hello query.</span></span> <span data-ttu-id="2ecaa-148">toodo Bu, hello yeşil ok simgesine tıklayın veya kısayol aşağıdaki hello kullanın: `CTRL` + `SHIFT` + `E`.</span><span class="sxs-lookup"><span data-stu-id="2ecaa-148">toodo this, click hello green arrow or use hello following shortcut: `CTRL`+`SHIFT`+`E`.</span></span>
   
    ![Sorgu çalıştırma][6]
5. <span data-ttu-id="2ecaa-150">Merhaba sorgu sonuçlarına bakın.</span><span class="sxs-lookup"><span data-stu-id="2ecaa-150">Look at hello query results.</span></span> <span data-ttu-id="2ecaa-151">Bu örnekte, hello Factınternetsales tablosunda 60398 satır var.</span><span class="sxs-lookup"><span data-stu-id="2ecaa-151">In this example, hello FactInternetSales table has 60398 rows.</span></span>
   
    ![Sorgu sonuçları][7]

## <a name="next-steps"></a><span data-ttu-id="2ecaa-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2ecaa-153">Next steps</span></span>
<span data-ttu-id="2ecaa-154">Bağlanma ve sorgulama şimdi deneyin [hello Powerbı ile verileri görselleştirmeyi][visualizing hello data with PowerBI].</span><span class="sxs-lookup"><span data-stu-id="2ecaa-154">Now that you can connect and query, try [visualizing hello data with PowerBI][visualizing hello data with PowerBI].</span></span>

<span data-ttu-id="2ecaa-155">ortamınız için Azure Active Directory kimlik doğrulaması, tooconfigure bkz [tooSQL veri ambarı kimlik doğrulaması][Authenticate tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="2ecaa-155">tooconfigure your environment for Azure Active Directory authentication, see [Authenticate tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

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
