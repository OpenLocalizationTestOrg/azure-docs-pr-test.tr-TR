---
title: "SQL Server DB Azure SQL veritabanına geçirme | Microsoft Docs"
description: "SQL Server veritabanını Azure SQL veritabanına geçirme öğrenin."
services: sql-database
documentationcenter: 
author: janeng
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,load & move data
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/27/2017
ms.author: janeng
ms.openlocfilehash: 375d3ea0230e7d3fd0fc02ca7e0b8a7a76c24a27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-sql-server-database-to-azure-sql-database"></a><span data-ttu-id="2c7c3-103">SQL Server veritabanını Azure SQL veritabanına geçirme</span><span class="sxs-lookup"><span data-stu-id="2c7c3-103">Migrate your SQL Server database to Azure SQL Database</span></span>

<span data-ttu-id="2c7c3-104">Azure SQL veritabanı, SQL Server veritabanınızın üç bölümden oluşan bir işlemdir - ilk hazırlama taşıma, ardından dışarı aktarın ve veritabanı içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-104">Moving your SQL Server database to Azure SQL Database is a three part process - you first prepare, then export, and then import the database.</span></span> <span data-ttu-id="2c7c3-105">Bu öğreticide, öğrenin:</span><span class="sxs-lookup"><span data-stu-id="2c7c3-105">In this tutorial, you learn to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2c7c3-106">Azure SQL veritabanı kullanarak geçiş için bir SQL Server veritabanında hazırlama [veri geçiş Yardımcısı](https://www.microsoft.com/download/details.aspx?id=53595) (DMA)</span><span class="sxs-lookup"><span data-stu-id="2c7c3-106">Prepare a database in a SQL Server for migration to Azure SQL Database using the [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) (DMA)</span></span>
> * <span data-ttu-id="2c7c3-107">Veritabanını bir BACPAC dosyasına dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="2c7c3-107">Export the database to a BACPAC file</span></span>
> * <span data-ttu-id="2c7c3-108">Bir Azure SQL veritabanına BACPAC dosyasını içeri aktar</span><span class="sxs-lookup"><span data-stu-id="2c7c3-108">Import the BACPAC file into an Azure SQL Database</span></span>

<span data-ttu-id="2c7c3-109">Bir Azure aboneliğiniz yoksa [ücretsiz bir hesap oluşturma](https://azure.microsoft.com/free/) başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-109">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c7c3-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2c7c3-110">Prerequisites</span></span>

<span data-ttu-id="2c7c3-111">Bu öğreticiyi tamamlamak için aşağıdaki ön koşulların karşılandığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="2c7c3-111">To complete this tutorial, make sure the following prerequisites are completed:</span></span>

- <span data-ttu-id="2c7c3-112">En son sürümü yüklü [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="2c7c3-112">Installed the newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS).</span></span> <span data-ttu-id="2c7c3-113">SSMS yükleme SQLPackage, bir dizi veritabanı geliştirme görevlerini otomatikleştirmek için kullanılan bir komut satırı yardımcı programı en yeni sürümünü yükler.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-113">Installing SSMS also installs the newest version of SQLPackage, a command-line utility that can be used to automate a range of database development tasks.</span></span> 
- <span data-ttu-id="2c7c3-114">Yüklü [veri geçiş Yardımcısı](https://www.microsoft.com/download/details.aspx?id=53595) (DMA).</span><span class="sxs-lookup"><span data-stu-id="2c7c3-114">Installed the [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) (DMA).</span></span>
- <span data-ttu-id="2c7c3-115">Tanımladınız ve geçirmek için bir veritabanı erişimi.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-115">You have identified and have access to a database to migrate.</span></span> <span data-ttu-id="2c7c3-116">Bu öğretici kullanır [SQL Server 2008R2 AdventureWorks OLTP veritabanını](https://msftdbprodsamples.codeplex.com/releases/view/59211) örneğindeki SQL Server 2008R2 ya da daha yeni, ancak siz tercih ettiğiniz herhangi bir veritabanını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-116">This tutorial uses the [SQL Server 2008R2 AdventureWorks OLTP database](https://msftdbprodsamples.codeplex.com/releases/view/59211) on an instance of SQL Server 2008R2 or newer, but you can use any database of your choice.</span></span> <span data-ttu-id="2c7c3-117">Uyumluluk sorunlarını gidermek için kullanmak [SQL Server veri araçları](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)</span><span class="sxs-lookup"><span data-stu-id="2c7c3-117">To fix compatibility issues, use [SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)</span></span>

## <a name="prepare-for-migration"></a><span data-ttu-id="2c7c3-118">Geçiş için hazırlama</span><span class="sxs-lookup"><span data-stu-id="2c7c3-118">Prepare for migration</span></span>

<span data-ttu-id="2c7c3-119">Geçişe hazırlanmak hazır olursunuz.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-119">You are ready to prepare for migration.</span></span> <span data-ttu-id="2c7c3-120">Kullanmak için aşağıdaki adımları izleyin  **[veri geçiş Yardımcısı](https://www.microsoft.com/download/details.aspx?id=53595)**  veritabanınız Azure SQL veritabanı geçiş için hazır olup olmadığını değerlendirmek için.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-120">Follow these steps to use the **[Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595)** to assess the readiness of your database for migration to Azure SQL Database.</span></span>

1. <span data-ttu-id="2c7c3-121">Açık **veri geçiş Yardımcısı**.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-121">Open the **Data Migration Assistant**.</span></span> <span data-ttu-id="2c7c3-122">Herhangi bir bilgisayarda, geçirmeyi planladığınız veritabanını içeren SQL Server örneği ile bağlantı DMA çalıştırabilir, SQL Server örneğini barındıran bilgisayara yüklemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-122">You can run DMA on any computer with connectivity to the SQL Server instance containing the database that you plan to migrate, you do not need to install it on the computer hosting the SQL Server instance.</span></span>

     ![açık veri geçiş Yardımcısı](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-open.png)

2. <span data-ttu-id="2c7c3-124">Sol menüde tıklatın **+ yeni** oluşturmak için bir **değerlendirme** projesi.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-124">In the left-hand menu, click **+ New** to create an **Assessment** project.</span></span> <span data-ttu-id="2c7c3-125">Formu doldurun bir **proje adı** (diğer tüm değerler varsayılan değerlerinde bırakılmalıdır) tıklatıp **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-125">Fill in the form with a **Project name** (all other values should be left at their default values) and click **Create**.</span></span> <span data-ttu-id="2c7c3-126">**Seçenekleri** sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-126">The **Options** page opens.</span></span>

     ![Yeni veri geçiş Yardımcısı projesi](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-new-project.png)

3. <span data-ttu-id="2c7c3-128">Üzerinde **seçenekleri** sayfasında, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-128">On the **Options** page, click **Next**.</span></span> <span data-ttu-id="2c7c3-129">**Seçin kaynakları** sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-129">The **Select sources** page opens.</span></span>

     ![Yeni veri geçiş seçenekleri](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-options.png) 

4. <span data-ttu-id="2c7c3-131">Üzerinde **seçin kaynakları** sayfasında, geçirmeyi planladığınız sunucunun içeren SQL Server örneğinin adını girin.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-131">On the **Select sources** page, enter the name of SQL Server instance containing the server you plan to migrate.</span></span> <span data-ttu-id="2c7c3-132">Bu sayfadaki diğer değerler, gerekirse değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-132">Change the other values on this page if necessary.</span></span> <span data-ttu-id="2c7c3-133">**Bağlan**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-133">Click **Connect**.</span></span>

     ![Yeni veri geçiş select kaynakları](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources.png)

5. <span data-ttu-id="2c7c3-135">İçinde **ekleme kaynakları** kısmı **seçin kaynakları** sayfasında, uyumluluk için sınanacak veritabanları için onay kutularını seçin.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-135">In the **Add sources** portion of the **Select sources** page, select the checkboxes for the databases to be tested for compatibility.</span></span> <span data-ttu-id="2c7c3-136">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-136">Click **Add**.</span></span>

     ![Yeni veri geçiş select kaynakları](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources-add.png)

6. <span data-ttu-id="2c7c3-138">Tıklatın **Başlat değerlendirme**.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-138">Click **Start Assessment**.</span></span>

     ![Yeni veri geçiş başlangıç değerlendirme](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-start-assessment.png)

7. <span data-ttu-id="2c7c3-140">Değerlendirme tamamlandığında veritabanı geçirmek için yeterince uyumlu olup olmadığını görmek için ilk bakın.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-140">When the assessment completes, first look to see if the database is sufficiently compatible to migrate.</span></span> <span data-ttu-id="2c7c3-141">Yeşil bir daire onay işaretine arayın.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-141">Look for the checkmark in a green circle.</span></span>

     ![Yeni veri geçiş değerlendirme sonuçlarını uyumlu](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-compatible.png)

8. <span data-ttu-id="2c7c3-143">Sonuçları gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-143">Review the results.</span></span> <span data-ttu-id="2c7c3-144">**SQL Server özellik eşliği** gösterilen sonucu olan varsayılan sonuçlarını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-144">The **SQL Server feature parity** results shown are the default results to review.</span></span> <span data-ttu-id="2c7c3-145">Özellikle desteklenmeyen ve kısmen desteklenen özellikler hakkında bilgi ve önerilen eylemler hakkında sağlanan bilgileri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-145">Specifically review the information about unsupported and partially supported features, and the provided information about recommended actions.</span></span> 

     ![Yeni veri geçiş değerlendirme eşlik](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-parity.png)

9. <span data-ttu-id="2c7c3-147">Gözden geçirme **uyumluluk sorunları** bu seçeneği sol üst köşedeki tıklatarak.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-147">Review the **Compatibility issues** by clicking that option in the upper left.</span></span> <span data-ttu-id="2c7c3-148">Özellikle geçiş blockers, davranış değişiklikleri ve her uyumluluk düzeyi için kullanım dışı özellikler hakkındaki bilgileri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-148">Specifically review the information about migration blockers, behavior changes, and deprecated features for each compatibility level.</span></span> <span data-ttu-id="2c7c3-149">AdventureWorks2008R2 veritabanı için SQL Server 2000'den itibaren SQL Server 2008 ve SERVERPROPERTY('LCID') değişiklikleri itibaren tam metin araması değişiklikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-149">For the AdventureWorks2008R2 database, review the changes to Full-Text Search since SQL Server 2008 and the changes to SERVERPROPERTY('LCID') since SQL Server 2000.</span></span> <span data-ttu-id="2c7c3-150">Bu değişiklikler hakkında daha fazla bilgi için daha fazla bilgi için bağlantılar sağlanır.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-150">For details on these changes, links for more information is provided.</span></span> <span data-ttu-id="2c7c3-151">Birçok seçenekleri arayın ve tam metin araması için ayarları değiştirdiniz</span><span class="sxs-lookup"><span data-stu-id="2c7c3-151">Many search options and settings for Full-Text Search have changed</span></span> 

   > [!IMPORTANT] 
   > <span data-ttu-id="2c7c3-152">Azure SQL veritabanına veritabanınızı geçirdikten sonra veritabanını geçerli uyumluluk düzeyinde (düzey 100 AdventureWorks2008R2 veritabanı için) veya daha yüksek düzeyde çalışmaya seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-152">After you migrate your database to Azure SQL Database, you can choose to operate the database at its current compatibility level (level 100 for the AdventureWorks2008R2 database) or at a higher level.</span></span> <span data-ttu-id="2c7c3-153">Uygulamaları ve belirli bir uyumluluk düzeyinde bir veritabanı işletim seçenekleri hakkında daha fazla bilgi için bkz: [ALTER veritabanı uyumluluk düzeyi](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span><span class="sxs-lookup"><span data-stu-id="2c7c3-153">For more information on the implications and options for operating a database at a specific compatibility level, see [ALTER DATABASE Compatibility Level](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level).</span></span> <span data-ttu-id="2c7c3-154">Ayrıca bkz. [ALTER veritabanı kapsamlı yapılandırma](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) Uyumluluk Düzeyleri ilgili ek veritabanı düzeyi ayarları hakkında bilgi için.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-154">See also [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) for information about additional database-level settings related to compatibility levels.</span></span>
   >

10. <span data-ttu-id="2c7c3-155">İsteğe bağlı olarak, tıklayın **verme rapor** raporu bir JSON dosyası olarak kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-155">Optionally, click **Export report** to save the report as a JSON file.</span></span>
11. <span data-ttu-id="2c7c3-156">Veri geçiş Yardımcısı'nı kapatın.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-156">Close the Data Migration Assistant.</span></span>

## <a name="export-to-bacpac-file"></a><span data-ttu-id="2c7c3-157">BACPAC dosyasına dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="2c7c3-157">Export to BACPAC file</span></span> 

<span data-ttu-id="2c7c3-158">ZIP dosyası meta verileri ve SQL Server veritabanından veri içeren BACPAC uzantılı bir BACPAC dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-158">A BACPAC file is a ZIP file with an extension of BACPAC containing the metadata and data from a SQL Server database.</span></span> <span data-ttu-id="2c7c3-159">Bir BACPAC dosyayı Azure blob depolama veya geçiş - veya arşivleme için yerel depolama gibi SQL Server'dan Azure SQL veritabanına depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-159">A BACPAC file can be stored in Azure blob storage or in local storage for archiving or for migration - such as from SQL Server to Azure SQL Database.</span></span> <span data-ttu-id="2c7c3-160">Bir verme işlemsel olarak tutarlı olmasını ya da hiçbir yazma emin olmalısınız etkinlik dışa aktarma sırasında gerçekleşen.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-160">For an export to be transactionally consistent, you must ensure either that no write activity is occurring during the export.</span></span>

<span data-ttu-id="2c7c3-161">Yerel depolama alanına AdventureWorks2008R2 veritabanını dışarı aktarma SQLPackage komut satırı yardımcı programını kullanmak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-161">Follow these steps to use the SQLPackage command-line utility to export the AdventureWorks2008R2 database to local storage.</span></span>

1. <span data-ttu-id="2c7c3-162">Bir Windows komut istemi açın ve sahip olduğunuz bir klasöre dizininize değiştirin **130** sürüm SQLPackage, - gibi **C:\Program Files (x86) \Microsoft SQL Server\130\DAC\bin**.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-162">Open a Windows command prompt and change your directory to a folder in which you have the **130** version of SQLPackage - such as **C:\Program Files (x86)\Microsoft SQL Server\130\DAC\bin**.</span></span>

2. <span data-ttu-id="2c7c3-163">Dışarı aktarmak için komut isteminde aşağıdaki SQLPackage komutu yürütün **AdventureWorks2008R2** veritabanını **localhost** için **AdventureWorks2008R2.bacpac**.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-163">Execute the following SQLPackage command at the command prompt to export the **AdventureWorks2008R2** database from **localhost** to **AdventureWorks2008R2.bacpac**.</span></span> <span data-ttu-id="2c7c3-164">Bu değerleri ortamınıza uygun şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-164">Change any of these values as appropriate to your environment.</span></span>

    ```SQLPackage
    sqlpackage.exe /Action:Export /ssn:localhost /sdn:AdventureWorks2008R2 /tf:AdventureWorks2008R2.bacpac
    ```

    ![sqlpackage dışarı aktarma](./media/sql-database-migrate-your-sql-server-database/sqlpackage-export.png)

<span data-ttu-id="2c7c3-166">Yürütme tamamlandıktan sonra oluşturulan BACPAC dosyası yürütülebilir sqlpackage bulunduğu dizinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-166">Once the execution is complete the generated BACPAC file is stored in the directory where the sqlpackage executable is located.</span></span> <span data-ttu-id="2c7c3-167">Bu örnekte, C:\Program Files (x86) \Microsoft SQL Server\130\DAC\bin.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-167">In this example C:\Program Files (x86)\Microsoft SQL Server\130\DAC\bin.</span></span> 

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="2c7c3-168">Azure portalında oturum açma</span><span class="sxs-lookup"><span data-stu-id="2c7c3-168">Log in to the Azure portal</span></span>

<span data-ttu-id="2c7c3-169">[Azure Portal](https://portal.azure.com/)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-169">Log in to the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="2c7c3-170">SQLPackage komut satırı yardımcı programını çalıştırdığınız bilgisayarda oturum açma güvenlik duvarı kuralı oluşturma 5. adımda kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-170">Logging on from the computer from which you are running the SQLPackage command-line utility eases the creation of the firewall rule in step 5.</span></span>

## <a name="create-a-sql-server-logical-server"></a><span data-ttu-id="2c7c3-171">Bir SQL server mantıksal sunucusu oluşturma</span><span class="sxs-lookup"><span data-stu-id="2c7c3-171">Create a SQL server logical server</span></span>

<span data-ttu-id="2c7c3-172">A [SQL server mantıksal sunucu](sql-database-features.md) birden fazla veritabanı için merkezi bir yönetim noktası işlevi görür.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-172">A [SQL server logical server](sql-database-features.md) acts as a central administrative point for multiple databases.</span></span> <span data-ttu-id="2c7c3-173">Geçirilen Adventure Works OLTP SQL Server veritabanını içeren bir SQL server mantıksal sunucu oluşturmak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-173">Follow these steps to create a SQL server logical server to contain the migrated Adventure Works OLTP SQL Server database.</span></span> 

1. <span data-ttu-id="2c7c3-174">Azure portalının sol üst köşesinde bulunan **Yeni** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-174">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="2c7c3-175">Tür **sql server** arama penceresinde **yeni** sayfasında ve seçin **SQL veritabanı (mantıksal sunucu)** filtre uygulanmış listeden.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-175">Type **sql server** in the search window on the **New** page, and select **SQL database (logical server)** from the filtered list.</span></span>

    ![mantıksal sunucu seçme](./media/sql-database-migrate-your-sql-server-database/logical-server.png)

3. <span data-ttu-id="2c7c3-177">Üzerinde **her şeyi** sayfasında, **SQL server (mantıksal sunucu)** ve ardından **oluşturma** üzerinde **SQL Server (mantıksal sunucu)** sayfası.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-177">On the **Everything** page, click **SQL server (logical server)** and then click **Create** on the **SQL Server (logical server)** page.</span></span>

    ![mantıksal sunucusu oluşturma](./media/sql-database-migrate-your-sql-server-database/logical-server-create.png)

4. <span data-ttu-id="2c7c3-179">SQL sunucusu (mantıksal sunucu) formunu, önceki görüntüde gösterildiği gibi aşağıdaki bilgilerle doldurun:</span><span class="sxs-lookup"><span data-stu-id="2c7c3-179">Fill out the SQL server (logical server) form with the following information, as shown on the preceding image:</span></span>     

   | <span data-ttu-id="2c7c3-180">Ayar</span><span class="sxs-lookup"><span data-stu-id="2c7c3-180">Setting</span></span>       | <span data-ttu-id="2c7c3-181">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="2c7c3-181">Suggested value</span></span> | <span data-ttu-id="2c7c3-182">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2c7c3-182">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="2c7c3-183">**Sunucu adı**</span><span class="sxs-lookup"><span data-stu-id="2c7c3-183">**Server name**</span></span> | <span data-ttu-id="2c7c3-184">Genel olarak benzersiz bir ad girin</span><span class="sxs-lookup"><span data-stu-id="2c7c3-184">Enter any globally unique name</span></span> | <span data-ttu-id="2c7c3-185">Geçerli sunucu adları için bkz. [Adlandırma kuralları ve kısıtlamalar](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span><span class="sxs-lookup"><span data-stu-id="2c7c3-185">For valid server names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> | 
   | <span data-ttu-id="2c7c3-186">**Sunucu yöneticisi oturum açma bilgileri**</span><span class="sxs-lookup"><span data-stu-id="2c7c3-186">**Server admin login**</span></span> | <span data-ttu-id="2c7c3-187">Geçerli bir ad girin</span><span class="sxs-lookup"><span data-stu-id="2c7c3-187">Enter any valid name</span></span> | <span data-ttu-id="2c7c3-188">Geçerli oturum açma adları için bkz. [Veritabanı Tanımlayıcıları](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).</span><span class="sxs-lookup"><span data-stu-id="2c7c3-188">For valid login names, see [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).</span></span> |
   | <span data-ttu-id="2c7c3-189">**Parola**</span><span class="sxs-lookup"><span data-stu-id="2c7c3-189">**Password**</span></span> | <span data-ttu-id="2c7c3-190">Geçerli bir parola girin</span><span class="sxs-lookup"><span data-stu-id="2c7c3-190">Enter any valid password</span></span> | <span data-ttu-id="2c7c3-191">Parolanız en az 8 karakter olmalı ve aşağıdaki kategoriden üçünden karakterler içermelidir: büyük harf karakterler, küçük harfler, sayılar ve alfasayısal olmayan karakter.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-191">Your password must have at least 8 characters and must contain characters from three of the following categories: upper case characters, lower case characters, numbers, and non-alphanumeric characters.</span></span> |
   | <span data-ttu-id="2c7c3-192">**Abonelik**</span><span class="sxs-lookup"><span data-stu-id="2c7c3-192">**Subscription**</span></span> | <span data-ttu-id="2c7c3-193">Abonelik seçin</span><span class="sxs-lookup"><span data-stu-id="2c7c3-193">Select a subscription</span></span> | <span data-ttu-id="2c7c3-194">Abonelikleriniz hakkında daha ayrıntılı bilgi için bkz. [Abonelikler](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="2c7c3-194">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="2c7c3-195">**Kaynak grubu**</span><span class="sxs-lookup"><span data-stu-id="2c7c3-195">**Resource group**</span></span> | <span data-ttu-id="2c7c3-196">Varolan bir kaynak grubu seçin veya yeni bir grup oluşturun **myResourceGroup**</span><span class="sxs-lookup"><span data-stu-id="2c7c3-196">Choose an existing resource group or create a new group, such as **myResourceGroup**</span></span> |  <span data-ttu-id="2c7c3-197">Geçerli kaynak grubu adları için bkz. [Adlandırma kuralları ve kısıtlamalar](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span><span class="sxs-lookup"><span data-stu-id="2c7c3-197">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="2c7c3-198">**Konum**</span><span class="sxs-lookup"><span data-stu-id="2c7c3-198">**Location**</span></span> | <span data-ttu-id="2c7c3-199">Yeni sunucu için geçerli bir konum girin</span><span class="sxs-lookup"><span data-stu-id="2c7c3-199">Enter any valid location for the new server</span></span> | <span data-ttu-id="2c7c3-200">Bölgeler hakkında bilgi için bkz. [Azure Bölgeleri](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="2c7c3-200">For information about regions, see [Azure Regions](https://azure.microsoft.com/regions/).</span></span> |

   ![mantıksal sunucu tamamlandı formu oluşturma](./media/sql-database-migrate-your-sql-server-database/logical-server-create-completed.png)

5. <span data-ttu-id="2c7c3-202">Tıklatın **oluşturma** mantıksal sunucusu sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-202">Click **Create** to provision the logical server.</span></span> <span data-ttu-id="2c7c3-203">Sağlama birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-203">Provisioning takes a few minutes.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="2c7c3-204">Sunucu adı, Sunucu Yöneticisi oturum açma adı ve parola unutmayın.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-204">Remember your server name, server admin login name, and password.</span></span> <span data-ttu-id="2c7c3-205">Bu öğreticide daha sonra bu değerler gerekir.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-205">You need these values later in this tutorial.</span></span>
>

## <a name="create-a-server-level-firewall-rule"></a><span data-ttu-id="2c7c3-206">Sunucu düzeyinde bir güvenlik duvarı kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2c7c3-206">Create a server-level firewall rule</span></span>

<span data-ttu-id="2c7c3-207">SQL veritabanı hizmetinin oluşturur bir [sunucu düzeyinde güvenlik duvarı](sql-database-firewall-configure.md) engelleyen harici uygulamalar ve araçlar için Güvenlik Duvarı'nı açmak için bir güvenlik duvarı kuralı yapılandırılmadığı sürece sunucu veya sunucu üzerindeki herhangi bir veritabanına bağlanmasını Belirli IP adresleri.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-207">The SQL Database service creates a [firewall at the server-level](sql-database-firewall-configure.md) that prevents external applications and tools from connecting to the server or any databases on the server unless a firewall rule is created to open the firewall for specific IP addresses.</span></span> <span data-ttu-id="2c7c3-208">SQLPackage komut satırı yardımcı programını çalıştırdığınız bilgisayarın IP adresi için bir SQL veritabanı sunucu düzeyinde güvenlik duvarı kuralı oluşturmak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-208">Follow these steps to create a SQL Database server-level firewall rule for the IP address of the computer from which you are running the SQLPackage command-line utility.</span></span> <span data-ttu-id="2c7c3-209">Bu, Azure SQL veritabanı güvenlik duvarı üzerinden SQL serverDatabase mantıksal sunucusuna bağlanmak SQLPackage sağlar.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-209">This enables SQLPackage to connect to the SQL serverDatabase logical server through the Azure SQL Database firewall.</span></span> 

1. <span data-ttu-id="2c7c3-210">Tıklatın **tüm kaynakları** sol menüden ve yeni sunucunuzu tıklayın **tüm kaynakları** sayfa.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-210">Click **All resources** from the left-hand menu and click your new server on the **All resources** page.</span></span> <span data-ttu-id="2c7c3-211">Sunucunuz için genel bakış sayfası açılır ve ek yapılandırma seçeneklerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-211">The overview page for your server opens and provides options for further configuration.</span></span>

     ![mantıksal sunucusuna genel bakış](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

2. <span data-ttu-id="2c7c3-213">Tıklatın **Güvenlik Duvarı** altında sol menüde **ayarları** genel bakış sayfasında.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-213">Click **Firewall** in the left-hand menu under **Settings** on the overview page.</span></span> <span data-ttu-id="2c7c3-214">SQL Veritabanı sunucusu için **Güvenlik duvarı ayarları** sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-214">The **Firewall settings** page for the SQL Database server opens.</span></span> 

3. <span data-ttu-id="2c7c3-215">Tıklatın **istemci IP'si Ekle** bilgisayarın IP adresi eklemek için araç çubuğundaki kullanmakta olduğunuz ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-215">Click **Add client IP** on the toolbar to add the IP address of the computer you are currently using and then click **Save**.</span></span> <span data-ttu-id="2c7c3-216">Bu IP adresi için bir sunucu düzeyinde güvenlik duvarı kuralı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-216">A server-level firewall rule is created for this IP address.</span></span>

     ![sunucu güvenlik duvarı kuralı ayarla](./media/sql-database-migrate-your-sql-server-database/server-firewall-rule-set.png)

4. <span data-ttu-id="2c7c3-218">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-218">Click **OK**.</span></span>

<span data-ttu-id="2c7c3-219">SQL Server Management Studio veya önceden oluşturulmuş sunucu yönetici hesabı kullanarak bu IP adresinden tercih ettiğiniz başka bir araç kullanarak bu sunucudaki tüm veritabanları artık bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-219">You can now connect to all databases on this server using SQL Server Management Studio or another tool of your choice from this IP address using the server admin account created previously.</span></span>

> [!NOTE]
> <span data-ttu-id="2c7c3-220">SQL Veritabanı 1433 numaralı bağlantı noktası üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-220">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="2c7c3-221">Bir kurumsal ağ içerisinden bağlanmaya çalışıyorsanız, ağınızın güvenlik duvarı tarafından 1433 numaralı bağlantı noktası üzerinden giden trafiğe izin verilmiyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-221">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="2c7c3-222">Bu durumda BT departmanınız 1433 numaralı bağlantı noktasını açmadığı sürece Azure SQL Veritabanı sunucunuza bağlanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-222">If so, you cannot connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="import-a-bacpac-file-to-azure-sql-database"></a><span data-ttu-id="2c7c3-223">Azure SQL veritabanı için bir BACPAC dosyasını içeri aktarın</span><span class="sxs-lookup"><span data-stu-id="2c7c3-223">Import a BACPAC file to Azure SQL Database</span></span> 

<span data-ttu-id="2c7c3-224">Azure SQL veritabanını belirtilen bir oluşturmak için en yeni sürümlerin SQLPackage komut satırı yardımcı programının desteği sağlamak [Hizmet katmanını ve performans düzeyini](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="2c7c3-224">The newest versions of the SQLPackage command-line utility provide support for creating an Azure SQL database at a specified [service tier and performance level](sql-database-service-tiers.md).</span></span> <span data-ttu-id="2c7c3-225">En iyi performans için içeri aktarma işlemi sırasında yüksek Hizmet katmanını ve performans düzeyini seçin ve Hizmet katmanını ve performans düzeyini hemen gerekenden daha yüksek olması durumunda içeri aktarma işleminden sonra ölçeklendirmeyi azaltın.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-225">For best performance during import, select a high service tier and performance level and then scale down after import if the service tier and performance level is higher than you need immediately.</span></span>

<span data-ttu-id="2c7c3-226">Bu adımları kullanma AdventureWorks2008R2 veritabanını Azure SQL veritabanı için içeri aktarma SQLPackage komut satırı yardımcı programını izleyin.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-226">Follow these steps use the SQLPackage command-line utility to import the AdventureWorks2008R2 database to Azure SQL Database.</span></span> <span data-ttu-id="2c7c3-227">Bu görev için SQL Server Management Studio'yu kullanabilirsiniz, ancak SQLPackage en fazla esneklik ve en iyi performans için birçok üretim ortamları için tercih edilen yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-227">While you can use SQL Server Management Studio for this task, SQLPackage is the preferred method for most production environments for maximum flexibility and best performance.</span></span> <span data-ttu-id="2c7c3-228">Bkz: [BACPAC dosyalarını kullanarak Azure SQL veritabanı için SQL Server'dan geçirme](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span><span class="sxs-lookup"><span data-stu-id="2c7c3-228">See [Migrating from SQL Server to Azure SQL Database using BACPAC Files](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).</span></span>

- <span data-ttu-id="2c7c3-229">İçeri aktarmak için komut isteminde aşağıdaki SQLPackage komutu yürütme **AdventureWorks2008R2** yerel depolama veritabanına yeni bir veritabanı, bir hizmet katmanı ,dahaönceoluşturduğunuzSQLservermantıksalsunucu **Premium**ve bir hizmet amacını **P6**.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-229">Execute the following SQLPackage command at the command prompt to import the **AdventureWorks2008R2** database from local storage to the SQL server logical server that you previously created to a new database, a service tier of **Premium**, and a Service Objective of **P6**.</span></span> <span data-ttu-id="2c7c3-230">SQL server mantıksal sunucunuz için uygun değerlerle köşeli değerleri değiştirin ve yeni veritabanı için bir ad belirtin (Ayrıca köşeli değiştirin).</span><span class="sxs-lookup"><span data-stu-id="2c7c3-230">Replace the values in angle brackets with appropriate values for your SQL server logical server and specify a name for the new database (also replace the angle brackets).</span></span> <span data-ttu-id="2c7c3-231">Veritabanı sürümü ve hizmet objectgive ortamınıza uygun şekilde değerlerini değiştirmek seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-231">You can also choose to change the values for database edition and service objectgive as appropriate to your environment.</span></span> <span data-ttu-id="2c7c3-232">Bu öğreticinin amaçları doğrultusunda, yükseltilen veritabanının adı **myMigratedDatabase**.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-232">For the purpose of this tutorial, the migrated database is called **myMigratedDatabase**.</span></span>

    ```
    SqlPackage.exe /a:import /tcs:"Data Source=<your_server_name>.database.windows.net;Initial Catalog=<your_new_database_name>;User Id=<change_to_your_admin_user_account>;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
    ```

   ![sqlpackage alma](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> <span data-ttu-id="2c7c3-234">Bir SQL server mantıksal sunucusu 1433 bağlantı noktasını dinler.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-234">A SQL server logical server listens on port 1433.</span></span> <span data-ttu-id="2c7c3-235">Bir SQL server mantıksal Sunucusu'ndan kurumsal bir güvenlik duvarı içinde bağlanmaya çalışıyorsanız, bu bağlantı noktası, başarılı bir şekilde bağlanmak Kurumsal Güvenlik Duvarı'nda açık olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-235">If you are attempting to connect to a SQL server logical server from within a corporate firewall, this port must be open in the corporate firewall for you to successfully connect.</span></span>
>

## <a name="connect-using-sql-server-management-studio-ssms"></a><span data-ttu-id="2c7c3-236">SQL Server Management Studio (SSMS) kullanarak bağlan</span><span class="sxs-lookup"><span data-stu-id="2c7c3-236">Connect using SQL Server Management Studio (SSMS)</span></span>

<span data-ttu-id="2c7c3-237">Geçirilen adlı veritabanı, Azure SQL veritabanı sunucunuzun ve yeni bir bağlantı kurmak için SQL Server Management Studio kullanın **myMigratedDatabase** bu öğreticideki.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-237">Use SQL Server Management Studio to establish a connection to your Azure SQL Database server and newly migrated database, called **myMigratedDatabase** in this tutorial.</span></span> <span data-ttu-id="2c7c3-238">SQL Server Management Studio SQLPackage çalıştırıldığı farklı bir bilgisayarda çalıştırıyorsanız, önceki yordamdaki adımları kullanarak bu bilgisayar için bir güvenlik duvarı kuralı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-238">If you are running SQL Server Management Studio on a different computer from which you ran SQLPackage, create a firewall rule for this computer using the steps in the previous procedure.</span></span>

1. <span data-ttu-id="2c7c3-239">SQL Server Management Studio’yu açın.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-239">Open SQL Server Management Studio.</span></span>

2. <span data-ttu-id="2c7c3-240">**Sunucuya Bağlan** iletişim kutusuna şu bilgileri girin:</span><span class="sxs-lookup"><span data-stu-id="2c7c3-240">In the **Connect to Server** dialog box, enter the following information:</span></span>
   - <span data-ttu-id="2c7c3-241">**Sunucu türü**: Veritabanı altyapısını belirtin</span><span class="sxs-lookup"><span data-stu-id="2c7c3-241">**Server type**: Specify Database engine</span></span>
   - <span data-ttu-id="2c7c3-242">**Sunucu adı**: tam sunucu adınızı girin **mynewserver20170403.database.windows.net**</span><span class="sxs-lookup"><span data-stu-id="2c7c3-242">**Server name**: Enter your fully qualified server name, such as **mynewserver20170403.database.windows.net**</span></span>
   - <span data-ttu-id="2c7c3-243">**Kimlik doğrulama**: SQL Server Kimlik Doğrulaması belirtin</span><span class="sxs-lookup"><span data-stu-id="2c7c3-243">**Authentication**: Specify SQL Server Authentication</span></span>
   - <span data-ttu-id="2c7c3-244">**Kullanıcı adı**: Sunucu yöneticisi hesabınızı girin</span><span class="sxs-lookup"><span data-stu-id="2c7c3-244">**Login**: Enter your server admin account</span></span>
   - <span data-ttu-id="2c7c3-245">**Parola**: Sunucu yöneticisi hesabınızın parolasını girin</span><span class="sxs-lookup"><span data-stu-id="2c7c3-245">**Password**: Enter the password for your server admin account</span></span>
 
    ![SSMS ile bağlanma](./media/sql-database-migrate-your-sql-server-database/connect-ssms.png)

3. <span data-ttu-id="2c7c3-247">**Bağlan**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-247">Click **Connect**.</span></span> <span data-ttu-id="2c7c3-248">Nesne Gezgini penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-248">The Object Explorer window opens.</span></span> 

4. <span data-ttu-id="2c7c3-249">Nesne Gezgini'nde genişletin **veritabanları** genişletin ve ardından **myMigratedDatabase** örnek veritabanında nesneleri görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-249">In Object Explorer, expand **Databases** and then expand **myMigratedDatabase** to view the objects in the sample database.</span></span>

## <a name="change-database-properties"></a><span data-ttu-id="2c7c3-250">Veritabanı özelliklerini değiştir</span><span class="sxs-lookup"><span data-stu-id="2c7c3-250">Change database properties</span></span>

<span data-ttu-id="2c7c3-251">Hizmet katmanı, performans düzeyi ve SQL Server Management Studio'yu kullanarak uyumluluk düzeyini değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-251">You can change the service tier, performance level, and compatibility level using SQL Server Management Studio.</span></span> <span data-ttu-id="2c7c3-252">İçeri aktarma aşaması sırasında en iyi performans için daha yüksek bir performans katmanı veritabanına aktarmak, ancak içeri aktarılan veritabanını etkin olarak kullanmaya hazır olana kadar tasarruf için alma işlemi tamamlandıktan sonra ölçeklendirmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-252">During the import phase, we recommend that you import to a higher performance tier database for best performance, but that you scale down after the import completes to save money until you are ready to actively use the imported database.</span></span> <span data-ttu-id="2c7c3-253">Uyumluluk düzeyinin değiştirilmesi, daha iyi performans ve Azure SQL veritabanı hizmetinin en yeni özelliklere erişim elde etmek.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-253">Changing the compatibility level may yield better performance and access to the newest capabilities of the Azure SQL Database service.</span></span> <span data-ttu-id="2c7c3-254">Eski bir veritabanını geçirdiğinizde, veritabanı uyumluluk düzeyi düzeyinde içeri aktarılmakta olan veritabanı ile uyumlu olan en düşük desteklenen korunur.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-254">When you migrate an older database, its database compatibility level is maintained at the lowest supported level that is compatible with the database being imported.</span></span> <span data-ttu-id="2c7c3-255">Daha fazla bilgi için bkz: [iyileştirilmiş sorgu performansı ile Azure SQL veritabanı uyumluluk düzeyi 130](sql-database-compatibility-level-query-performance-130.md).</span><span class="sxs-lookup"><span data-stu-id="2c7c3-255">For more information, see [Improved query performance with compatibility Level 130 in Azure SQL Database](sql-database-compatibility-level-query-performance-130.md).</span></span>

1. <span data-ttu-id="2c7c3-256">Nesne Gezgini'nde sağ **myMigratedDatabase** tıklatıp **yeni sorgu**.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-256">In Object Explorer, right-click **myMigratedDatabase** and click **New Query**.</span></span> <span data-ttu-id="2c7c3-257">Veritabanına bağlı bir sorgu penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-257">A query window opens connected to your database.</span></span>

2. <span data-ttu-id="2c7c3-258">Hizmet katmanı ayarlamak için aşağıdaki komutu yürütün **standart** ve performans düzeyine **S1**.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-258">Execute the following command to set the service tier to **Standard** and the performance level to **S1**.</span></span>

    ```
    ALTER DATABASE myMigratedDatabase 
    MODIFY 
        (
        EDITION = 'Standard'
        , MAXSIZE = 250 GB
        , SERVICE_OBJECTIVE = 'S1'
    );
    ```

    ![Hizmet katmanını değiştirebilirsiniz](./media/sql-database-migrate-your-sql-server-database/service-tier.png)

3. <span data-ttu-id="2c7c3-260">Veritabanı uyumluluk düzeyini değiştirmek için aşağıdaki komutu yürütün **130**.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-260">Execute the following command to change the database compatibility level to **130**.</span></span>

    ```
    ALTER DATABASE myMigratedDatabase  
    SET COMPATIBILITY_LEVEL = 130;
    ```

   ![uyumluluk düzeyini değiştirme](./media/sql-database-migrate-your-sql-server-database/compat-level.png)

## <a name="next-steps"></a><span data-ttu-id="2c7c3-262">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2c7c3-262">Next steps</span></span> 
<span data-ttu-id="2c7c3-263">Bu öğreticide dışarı ve veritabanınızı içe hazır.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-263">In this tutorial you prepared, exported and imported your database.</span></span> <span data-ttu-id="2c7c3-264">İçin öğrenilen:</span><span class="sxs-lookup"><span data-stu-id="2c7c3-264">You learned to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2c7c3-265">Bir SQL Server veritabanında Azure SQL veritabanı geçiş için hazırlama</span><span class="sxs-lookup"><span data-stu-id="2c7c3-265">Prepare a database in a SQL Server for migration to Azure SQL Database</span></span>
> * <span data-ttu-id="2c7c3-266">Veritabanını bir BACPAC dosyasına dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="2c7c3-266">Export the database to a BACPAC file</span></span>
> * <span data-ttu-id="2c7c3-267">Bir Azure SQL veritabanına BACPAC dosyasını içeri aktar</span><span class="sxs-lookup"><span data-stu-id="2c7c3-267">Import the BACPAC file into an Azure SQL Database</span></span>

<span data-ttu-id="2c7c3-268">Veritabanınızın güvenliğini sağlamak öğrenmek için sonraki öğretici ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="2c7c3-268">Advance to the next tutorial to learn how to secure your database.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="2c7c3-269">[Azure SQL veritabanınızı güvenli](sql-database-security-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="2c7c3-269">[Secure your Azure SQL Database](sql-database-security-tutorial.md).</span></span>


