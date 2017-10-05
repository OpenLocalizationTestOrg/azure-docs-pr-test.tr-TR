---
title: "Azure SQL veri eşitleme (Önizleme) ile çalışmaya başlama | Microsoft Docs"
description: "Bu öğreticide Azure SQL veri eşitleme (Önizleme) ile çalışmaya başlamanıza yardımcı olur."
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: a295a768-7ff2-4a86-a253-0090281c8efa
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: douglasl
ms.openlocfilehash: 2d0f9d7f32ad79f49d58165d734b9df4af862835
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="getting-started-with-azure-sql-data-sync-preview"></a><span data-ttu-id="5ab47-103">Azure SQL veri eşitleme (Önizleme) ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="5ab47-103">Getting Started with Azure SQL Data Sync (Preview)</span></span>
<span data-ttu-id="5ab47-104">Bu öğreticide, Azure SQL Database ve SQL Server örneklerini içeren bir karma eşitleme grubu oluşturarak Azure SQL veri eşitlemeyi ayarlamak nasıl öğrenin.</span><span class="sxs-lookup"><span data-stu-id="5ab47-104">In this tutorial, you learn how to set up Azure SQL Data Sync by creating a hybrid sync group that contains both Azure SQL Database and SQL Server instances.</span></span> <span data-ttu-id="5ab47-105">Yeni eşitleme grubunu tam olarak yapılandırılmamış ve belirlediğiniz bir zamanlamaya göre eşitler.</span><span class="sxs-lookup"><span data-stu-id="5ab47-105">The new sync group is fully configured and synchronizes on the schedule you set.</span></span>

<span data-ttu-id="5ab47-106">Bu öğretici, SQL Database ve SQL Server ile en az bazı konusunda deneyim sahibi olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="5ab47-106">This tutorial assumes that you have at least some prior experience with SQL Database and with SQL Server.</span></span> 

<span data-ttu-id="5ab47-107">SQL veri eşitleme genel bakış için bkz: [verilerini](sql-database-sync-data.md).</span><span class="sxs-lookup"><span data-stu-id="5ab47-107">For an overview of SQL Data Sync, see [Sync data](sql-database-sync-data.md).</span></span>

<span data-ttu-id="5ab47-108">SQL veri eşitleme yapılandırmayı gösterir tam PowerShell örnekler için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="5ab47-108">For complete PowerShell examples that show how to configure SQL Data Sync, see the following articles:</span></span>
-   [<span data-ttu-id="5ab47-109">Birden çok Azure SQL veritabanları arasında eşitlemek için PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="5ab47-109">Use PowerShell to sync between multiple Azure SQL databases</span></span>](scripts/sql-database-sync-data-between-sql-databases.md)
-   [<span data-ttu-id="5ab47-110">Bir Azure SQL Database ve SQL Server içi veritabanı arasında eşitlemek için PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="5ab47-110">Use PowerShell to sync between an Azure SQL Database and a SQL Server on-premises database</span></span>](scripts/sql-database-sync-data-between-azure-onprem.md)

> [!NOTE]
> <span data-ttu-id="5ab47-111">Önceden, MSDN'de bulunan Azure SQL veri eşitleme için ayarlama tam teknik belgeler olarak kullanılabilir bir. PDF belgesini.</span><span class="sxs-lookup"><span data-stu-id="5ab47-111">The complete technical documentation set for Azure SQL Data Sync, formerly located on MSDN, is available as a .PDF document.</span></span> <span data-ttu-id="5ab47-112">Karşıdan [burada](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).</span><span class="sxs-lookup"><span data-stu-id="5ab47-112">Download it [here](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).</span></span>

## <a name="step-1---create-sync-group"></a><span data-ttu-id="5ab47-113">1. adım - eşitleme grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="5ab47-113">Step 1 - Create sync group</span></span>

### <a name="locate-the-data-sync-settings"></a><span data-ttu-id="5ab47-114">Veri Eşitleme ayarlarını bulun</span><span class="sxs-lookup"><span data-stu-id="5ab47-114">Locate the Data Sync settings</span></span>

1.  <span data-ttu-id="5ab47-115">Tarayıcınızda, Azure portalına gidin.</span><span class="sxs-lookup"><span data-stu-id="5ab47-115">In your browser, navigate to the Azure portal.</span></span>

2.  <span data-ttu-id="5ab47-116">Portalda, SQL veritabanlarınızın Panonuzda veya SQL veritabanları simgesi araç çubuğunda bulun.</span><span class="sxs-lookup"><span data-stu-id="5ab47-116">In the portal, locate your SQL databases from your Dashboard or from the SQL Databases icon on the toolbar.</span></span>

    ![Azure SQL veritabanı listesi](media/sql-database-get-started-sql-data-sync/datasync-preview-sqldbs.png)

3.  <span data-ttu-id="5ab47-118">Üzerinde **SQL veritabanları** dikey penceresinde hub veritabanı olarak veri eşitleme için kullanmak istediğiniz varolan bir SQL veritabanını seçin. SQL veritabanı dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="5ab47-118">On the **SQL databases** blade, select the existing SQL database that you want to use as the hub database for Data Sync. The SQL database blade opens.</span></span>

4.  <span data-ttu-id="5ab47-119">SQL veritabanı dikey penceresinde seçili veritabanı, seçin **diğer veritabanlarına eşitleme**.</span><span class="sxs-lookup"><span data-stu-id="5ab47-119">On the SQL database blade for the selected database, select **Sync to other databases**.</span></span> <span data-ttu-id="5ab47-120">Veri Eşitleme dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="5ab47-120">The Data Sync blade opens.</span></span>

    ![Diğer veritabanlarını seçeneğine eşitleme](media/sql-database-get-started-sql-data-sync/datasync-preview-newsyncgroup.png)

### <a name="create-a-new-sync-group"></a><span data-ttu-id="5ab47-122">Yeni bir eşitleme grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="5ab47-122">Create a new Sync Group</span></span>

1.  <span data-ttu-id="5ab47-123">Veri Eşitleme dikey penceresinde, seçin **yeni eşitleme grubu**.</span><span class="sxs-lookup"><span data-stu-id="5ab47-123">On the Data Sync blade, select **New Sync Group**.</span></span> <span data-ttu-id="5ab47-124">**Yeni eşitleme grubu** dikey pencere açılır adım 1 ile **eşitleme Grup Oluştur**, vurgulanan.</span><span class="sxs-lookup"><span data-stu-id="5ab47-124">The **New sync group** blade opens with Step 1, **Create sync group**, highlighted.</span></span> <span data-ttu-id="5ab47-125">**Veri eşitleme grubu oluşturma** dikey penceresi de açılır.</span><span class="sxs-lookup"><span data-stu-id="5ab47-125">The **Create Data Sync Group** blade also opens.</span></span>

2.  <span data-ttu-id="5ab47-126">Üzerinde **veri eşitleme grubu oluşturma** dikey penceresinde, şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="5ab47-126">On the **Create Data Sync Group** blade, do the following things:</span></span>

    1.  <span data-ttu-id="5ab47-127">İçinde **eşitleme grubu adı** alan, yeni eşitleme grubu için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="5ab47-127">In the **Sync Group Name** field, enter a name for the new sync group.</span></span>

    2.  <span data-ttu-id="5ab47-128">İçinde **eşitleme meta veri veritabanı** bölümünde, (önerilen) yeni bir veritabanı oluşturun veya varolan bir veritabanını kullanmak için seçin.</span><span class="sxs-lookup"><span data-stu-id="5ab47-128">In the **Sync Metadata Database** section, choose whether to create a new database (recommended) or to use an existing database.</span></span>

        > [!NOTE]
        > <span data-ttu-id="5ab47-129">Microsoft Eşitleme meta veri veritabanı olarak kullanmak için yeni, boş bir veritabanı oluşturmak önerir.</span><span class="sxs-lookup"><span data-stu-id="5ab47-129">Microsoft recommends that you create a new, empty database to use as the Sync Metadata Database.</span></span> <span data-ttu-id="5ab47-130">Veri Eşitleme bu veritabanında tablolar oluşturur ve sık kullanılan bir iş yükü çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="5ab47-130">Data Sync creates tables in this database and runs a frequent workload.</span></span> <span data-ttu-id="5ab47-131">Bu veritabanı, tüm seçili bölgede eşitleme gruplarınızın için eşitleme meta veri veritabanı olarak otomatik olarak paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="5ab47-131">This database is automatically shared as the Sync Metadata Database for all of your Sync groups in the selected region.</span></span> <span data-ttu-id="5ab47-132">Eşitleme meta veri veritabanı, adını ya da kendi hizmet düzeyi bırakmadan olmadan değiştirilemiyor.</span><span class="sxs-lookup"><span data-stu-id="5ab47-132">You can't change the Sync Metadata Database, its name, or its service level without dropping it.</span></span>

        <span data-ttu-id="5ab47-133">Seçerseniz **yeni veritabanı**seçin **yeni veritabanı oluştur.**</span><span class="sxs-lookup"><span data-stu-id="5ab47-133">If you chose **New database**, select **Create new database.**</span></span> <span data-ttu-id="5ab47-134">**SQL veritabanı** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="5ab47-134">The **SQL Database** blade opens.</span></span> <span data-ttu-id="5ab47-135">Üzerinde **SQL veritabanı** dikey penceresinde, adı ve yeni veritabanını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5ab47-135">On the **SQL Database** blade, name and configure the new database.</span></span> <span data-ttu-id="5ab47-136">Ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="5ab47-136">Then select **OK**.</span></span>

        <span data-ttu-id="5ab47-137">Seçerseniz **varolan veritabanını kullan**, veritabanını listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="5ab47-137">If you chose **Use existing database**, select the database from the list.</span></span>

    3.  <span data-ttu-id="5ab47-138">İçinde **otomatik eşitleme** bölümünde, ilk seçin **üzerinde** veya **devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="5ab47-138">In the **Automatic Sync** section, first select **On** or **Off**.</span></span>

        <span data-ttu-id="5ab47-139">Seçerseniz **üzerinde**, **eşitleme sıklığı** bölümünde, bir sayı girin ve saniye, dakika, saat veya gün seçin.</span><span class="sxs-lookup"><span data-stu-id="5ab47-139">If you chose **On**, in the **Sync Frequency** section, enter a number and select Seconds, Minutes, Hours, or Days.</span></span>

        ![Eşitleme sıklığı belirtin](media/sql-database-get-started-sql-data-sync/datasync-preview-syncfreq.png)

    4.  <span data-ttu-id="5ab47-141">İçinde **çakışma çözümü** bölümünde, "Hub wins" veya "Üye WINS." seçin</span><span class="sxs-lookup"><span data-stu-id="5ab47-141">In the **Conflict Resolution** section, select "Hub wins" or "Member wins."</span></span>

        ![Çakışmalar nasıl çözümlenir belirtin](media/sql-database-get-started-sql-data-sync/datasync-preview-conflictres.png)

    5.  <span data-ttu-id="5ab47-143">Seçin **Tamam** ve oluşturulan ve dağıtılan için yeni eşitleme grubu bekleyin.</span><span class="sxs-lookup"><span data-stu-id="5ab47-143">Select **OK** and wait for the new sync group to be created and deployed.</span></span>

## <a name="step-2---add-sync-members"></a><span data-ttu-id="5ab47-144">2. adım - eşitleme üyeleri Ekle</span><span class="sxs-lookup"><span data-stu-id="5ab47-144">Step 2 - Add sync members</span></span>

<span data-ttu-id="5ab47-145">Yeni eşitleme grubu oluşturup, adım 2 ' yi dağıttıktan sonra **eşitleme üye eklemek**, vurgulanan **yeni eşitleme grubu** dikey.</span><span class="sxs-lookup"><span data-stu-id="5ab47-145">After the new sync group is created and deployed, Step 2, **Add sync members**, is highlighted in the **New sync group** blade.</span></span>

<span data-ttu-id="5ab47-146">İçinde **Hub veritabanı** bölümünde, hangi hub veritabanının bulunduğu SQL veritabanı sunucusu için varolan kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="5ab47-146">In the **Hub Database** section, enter the existing credentials for the SQL Database server on which the hub database is located.</span></span> <span data-ttu-id="5ab47-147">Girmeyin *yeni* Bu bölümde kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="5ab47-147">Don't enter *new* credentials in this section.</span></span>

![Hub veritabanı grubunu eşitlemek için eklenen](media/sql-database-get-started-sql-data-sync/datasync-preview-hubadded.png)

## <a name="add-an-azure-sql-database"></a><span data-ttu-id="5ab47-149">Bir Azure SQL veritabanı Ekle</span><span class="sxs-lookup"><span data-stu-id="5ab47-149">Add an Azure SQL Database</span></span>

<span data-ttu-id="5ab47-150">İçinde **üye veritabanı** bölümünde, isteğe bağlı olarak bir Azure SQL veritabanı seçerek eşitleme grubuna ekleyin **Azure veritabanı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="5ab47-150">In the **Member Database** section, optionally add an Azure SQL Database to the sync group by selecting **Add an Azure Database**.</span></span> <span data-ttu-id="5ab47-151">**Azure veritabanını yapılandırma** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="5ab47-151">The **Configure Azure Database** blade opens.</span></span>

<span data-ttu-id="5ab47-152">Üzerinde **Azure veritabanını yapılandırma** dikey penceresinde, şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="5ab47-152">On the **Configure Azure Database** blade, do the following things:</span></span>

1.  <span data-ttu-id="5ab47-153">İçinde **eşitleme üye adı** alanında, yeni eşitleme üyesi için bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="5ab47-153">In the **Sync Member Name** field, provide a name for the new sync member.</span></span> <span data-ttu-id="5ab47-154">Bu ad, veritabanı adından farklıdır.</span><span class="sxs-lookup"><span data-stu-id="5ab47-154">This name is distinct from the name of the database itself.</span></span>

2.  <span data-ttu-id="5ab47-155">İçinde **abonelik** alan, faturalandırma için ilişkili Azure aboneliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="5ab47-155">In the **Subscription** field, select the associated Azure subscription for billing purposes.</span></span>

3.  <span data-ttu-id="5ab47-156">İçinde **Azure SQL Server** alanında, varolan bir SQL veritabanı sunucusuna seçin.</span><span class="sxs-lookup"><span data-stu-id="5ab47-156">In the **Azure SQL Server** field, select the existing SQL database server.</span></span>

4.  <span data-ttu-id="5ab47-157">İçinde **Azure SQL veritabanı** alanında, varolan bir SQL veritabanını seçin.</span><span class="sxs-lookup"><span data-stu-id="5ab47-157">In the **Azure SQL Database** field, select the existing SQL database.</span></span>

5.  <span data-ttu-id="5ab47-158">İçinde **eşitleme yönergeleri** alan, select çift yönlü eşitleme, için Hub veya gelen Hub.</span><span class="sxs-lookup"><span data-stu-id="5ab47-158">In the **Sync Directions** field, select Bi-directional Sync, To the Hub, or From the Hub.</span></span>

    ![Yeni bir SQL veritabanı eşitleme üye ekleme](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadding.png)

6.  <span data-ttu-id="5ab47-160">İçinde **kullanıcıadı** ve **parola** alanları üye veritabanının bulunduğu SQL veritabanı sunucusu için var olan kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="5ab47-160">In the **Username** and **Password** fields, enter the existing credentials for the SQL Database server on which the member database is located.</span></span> <span data-ttu-id="5ab47-161">Girmeyin *yeni* Bu bölümde kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="5ab47-161">Don't enter *new* credentials in this section.</span></span>

7.  <span data-ttu-id="5ab47-162">Seçin **Tamam** ve oluşturulan ve dağıtılan yeni eşitleme üyesi için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="5ab47-162">Select **OK** and wait for the new sync member to be created and deployed.</span></span>

    ![Yeni SQL veritabanı eşitleme üye eklendi](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadded.png)

## <a name="add-an-on-premises-sql-server-database"></a><span data-ttu-id="5ab47-164">Bir şirket içi SQL Server veritabanı ekleyin</span><span class="sxs-lookup"><span data-stu-id="5ab47-164">Add an on-premises SQL Server database</span></span>

<span data-ttu-id="5ab47-165">İçinde **üye veritabanı** bölümünde, isteğe bağlı olarak seçerek bir şirket içi SQL Server eşitleme grubuna ekleyin **bir şirket içi veritabanı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="5ab47-165">In the **Member Database** section, optionally add an on-premises SQL Server to the sync group by selecting **Add an On-Premises Database**.</span></span> <span data-ttu-id="5ab47-166">**Yapılandırma şirket içi** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="5ab47-166">The **Configure On-Premises** blade opens.</span></span>

<span data-ttu-id="5ab47-167">Üzerinde **yapılandırma şirket içi** dikey penceresinde, şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="5ab47-167">On the **Configure On-Premises** blade, do the following things:</span></span>

1.  <span data-ttu-id="5ab47-168">Seçin **eşitleme Aracısı ağ geçidi seçin**.</span><span class="sxs-lookup"><span data-stu-id="5ab47-168">Select **Choose the Sync Agent Gateway**.</span></span> <span data-ttu-id="5ab47-169">**Seçin eşitleme Aracısı** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="5ab47-169">The **Select Sync Agent** blade opens.</span></span>

    ![Eşitleme Aracısı ağ geçidi seçin](media/sql-database-get-started-sql-data-sync/datasync-preview-choosegateway.png)

2.  <span data-ttu-id="5ab47-171">Üzerinde **eşitleme Aracısı ağ geçidi seçin** dikey penceresinde, var olan bir aracıyı kullanın veya yeni bir aracı oluşturmak isteyip istemediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="5ab47-171">On the **Choose the Sync Agent Gateway** blade, choose whether to use an existing agent or create a new agent.</span></span>

    <span data-ttu-id="5ab47-172">Seçerseniz **varolan aracıları**, var olan aracıyı listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="5ab47-172">If you chose **Existing agents**, select the existing agent from the list.</span></span>

    <span data-ttu-id="5ab47-173">Seçerseniz **yeni bir aracı oluşturma**, şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="5ab47-173">If you chose **Create a new agent**, do the following things:</span></span>

    1.  <span data-ttu-id="5ab47-174">İstemci eşitleme Aracısı yazılımı sağlanan bağlantısından yükleyin ve SQL Server bulunduğu bilgisayara yükleyin.</span><span class="sxs-lookup"><span data-stu-id="5ab47-174">Download the client sync agent software from the link provided and install it on the computer where the SQL Server is located.</span></span>
 
        > [!IMPORTANT]
        > <span data-ttu-id="5ab47-175">Sunucuyla iletişim istemci Aracısı izin vermek için Güvenlik Duvarı'nda giden TCP bağlantı noktası 1433 açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ab47-175">You have to open outbound TCP port 1433 in the firewall to let the client agent communicate with the server.</span></span>


    2.  <span data-ttu-id="5ab47-176">Aracı için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="5ab47-176">Enter a name for the agent.</span></span>

    3.  <span data-ttu-id="5ab47-177">Seçin **oluşturun ve anahtarı oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="5ab47-177">Select **Create and Generate Key**.</span></span>

    4.  <span data-ttu-id="5ab47-178">Aracı anahtarını panoya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="5ab47-178">Copy the agent key to the clipboard.</span></span>
        
        ![Yeni bir eşitleme aracı oluşturma](media/sql-database-get-started-sql-data-sync/datasync-preview-selectsyncagent.png)

    5.  <span data-ttu-id="5ab47-180">Seçin **Tamam** kapatmak için **seçin eşitleme Aracısı** dikey.</span><span class="sxs-lookup"><span data-stu-id="5ab47-180">Select **OK** to close the **Select Sync Agent** blade.</span></span>

    6.  <span data-ttu-id="5ab47-181">SQL Server bilgisayarında, bulun ve istemci eşitleme Aracısı uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5ab47-181">On the SQL Server computer, locate and run the Client Sync Agent app.</span></span>

        ![İstemci Aracısı uygulama verilerini eşitleme](media/sql-database-get-started-sql-data-sync/datasync-preview-clientagent.png)

    7.  <span data-ttu-id="5ab47-183">Eşitleme Aracısı uygulamayı seçin **aracı anahtarını Gönder**.</span><span class="sxs-lookup"><span data-stu-id="5ab47-183">In the sync agent app, select **Submit Agent Key**.</span></span> <span data-ttu-id="5ab47-184">**Eşitleme meta veri veritabanı yapılandırması** iletişim kutusu açılır.</span><span class="sxs-lookup"><span data-stu-id="5ab47-184">The **Sync Metadata Database Configuration** dialog box opens.</span></span>

    8.  <span data-ttu-id="5ab47-185">İçinde **eşitleme meta veri veritabanı yapılandırması** iletişim kutusu, Azure portalından kopyalandığından aracı anahtarını yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="5ab47-185">In the **Sync Metadata Database Configuration** dialog box, paste in the agent key copied from the Azure portal.</span></span> <span data-ttu-id="5ab47-186">Ayrıca meta veri veritabanının bulunduğu için Azure SQL veritabanı sunucusu varolan kimlik bilgilerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="5ab47-186">Also provide the existing credentials for the Azure SQL Database server on which the metadata database is located.</span></span> <span data-ttu-id="5ab47-187">(Yeni bir meta veri veritabanı oluşturduysanız, bu hub veritabanı ile aynı sunucuda veritabanıdır.) Seçin **Tamam** ve yapılandırmayı tamamlamak bekleyin.</span><span class="sxs-lookup"><span data-stu-id="5ab47-187">(If you created a new metadata database, this database is on the same server as the hub database.) Select **OK** and wait for the configuration to finish.</span></span>

        ![Aracı anahtarını ve sunucu kimlik bilgilerini girin](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-enterkey.png)

        >   [!NOTE] 
        >   <span data-ttu-id="5ab47-189">Bu noktada bir güvenlik duvarı hata alırsanız, SQL Server bilgisayardan gelen trafiğe izin vermek için Azure üzerinde bir güvenlik duvarı kuralı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5ab47-189">If you get a firewall error at this point, you have to create a firewall rule on Azure to allow incoming traffic from the SQL Server computer.</span></span> <span data-ttu-id="5ab47-190">Kural Portalı'nda el ile oluşturabilirsiniz, ancak SQL Server Management Studio (SSMS) oluşturmak daha kolay bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ab47-190">You can create the rule manually in the portal, but you may find it easier to create it in SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="5ab47-191">SSMS, Azure hub veritabanına bağlanmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="5ab47-191">In SSMS, try to connect to the hub database on Azure.</span></span> <span data-ttu-id="5ab47-192">Adı olarak girin \<hub_database_name\>. database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="5ab47-192">Enter its name as \<hub_database_name\>.database.windows.net.</span></span> <span data-ttu-id="5ab47-193">Azure güvenlik duvarı kuralı yapılandırmak için iletişim kutusu'ndaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="5ab47-193">Follow the steps in the dialog box to configure the Azure firewall rule.</span></span> <span data-ttu-id="5ab47-194">Ardından istemci eşitleme Aracısı uygulamaya geri dönün.</span><span class="sxs-lookup"><span data-stu-id="5ab47-194">Then return to the Client Sync Agent app.</span></span>

    9.  <span data-ttu-id="5ab47-195">İstemci eşitleme Aracısı uygulamanın tıklayın **kaydetmek** aracı ile bir SQL Server veritabanına kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="5ab47-195">In the Client Sync Agent app, click **Register** to register a SQL Server database with the agent.</span></span> <span data-ttu-id="5ab47-196">**SQL Server yapılandırma** iletişim kutusu açılır.</span><span class="sxs-lookup"><span data-stu-id="5ab47-196">The **SQL Server Configuration** dialog box opens.</span></span>

        ![Ekleme ve bir SQL Server veritabanı yapılandırma](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-adddb.png)

    10. <span data-ttu-id="5ab47-198">İçinde **SQL Server yapılandırma** iletişim kutusu, SQL Server kimlik doğrulaması veya Windows kimlik doğrulaması kullanarak bağlanmak üzere seçim yapın.</span><span class="sxs-lookup"><span data-stu-id="5ab47-198">In the **SQL Server Configuration** dialog box, choose whether to connect by using SQL Server authentication or Windows authentication.</span></span> <span data-ttu-id="5ab47-199">SQL Server kimlik doğrulamasını seçerseniz, var olan kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="5ab47-199">If you chose SQL Server authentication, enter the existing credentials.</span></span> <span data-ttu-id="5ab47-200">SQL Server adı ve eşitlemek istediğiniz veritabanının adını belirtin. Seçin **Bağlantıyı Sına** ayarlarınızı sınamak için.</span><span class="sxs-lookup"><span data-stu-id="5ab47-200">Provide the SQL Server name and the name of the database that you want to sync. Select **Test connection** to test your settings.</span></span> <span data-ttu-id="5ab47-201">Ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="5ab47-201">Then select **Save**.</span></span> <span data-ttu-id="5ab47-202">Kayıtlı veritabanı listede görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="5ab47-202">The registered database appears in the list.</span></span>

        ![SQL Server veritabanı artık kayıtlı](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-dbadded.png)

    11. <span data-ttu-id="5ab47-204">İstemci eşitleme Aracısı uygulama artık kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ab47-204">You can now close the Client Sync Agent app.</span></span>

    12. <span data-ttu-id="5ab47-205">Portalda, üzerinde **yapılandırma şirket içi** dikey penceresinde, select **veritabanını seçin.**</span><span class="sxs-lookup"><span data-stu-id="5ab47-205">In the portal, on the **Configure On-Premises** blade, select **Select the Database.**</span></span> <span data-ttu-id="5ab47-206">**Veritabanı Seç** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="5ab47-206">The **Select Database** blade opens.</span></span>

    13. <span data-ttu-id="5ab47-207">Üzerinde **Veritabanı Seç** dikey penceresindeki **eşitleme üye adı** alanında, yeni eşitleme üyesi için bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="5ab47-207">On the **Select Database** blade, in the **Sync Member Name** field, provide a name for the new sync member.</span></span> <span data-ttu-id="5ab47-208">Bu ad, veritabanı adından farklıdır.</span><span class="sxs-lookup"><span data-stu-id="5ab47-208">This name is distinct from the name of the database itself.</span></span> <span data-ttu-id="5ab47-209">Veritabanını listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="5ab47-209">Select the database from the list.</span></span> <span data-ttu-id="5ab47-210">İçinde **eşitleme yönergeleri** alan, select çift yönlü eşitleme, için Hub veya gelen Hub.</span><span class="sxs-lookup"><span data-stu-id="5ab47-210">In the **Sync Directions** field, select Bi-directional Sync, To the Hub, or From the Hub.</span></span>

        ![Şirket içi veritabanını seçin](media/sql-database-get-started-sql-data-sync/datasync-preview-selectdb.png)

    14. <span data-ttu-id="5ab47-212">Seçin **Tamam** kapatmak için **Veritabanı Seç** dikey.</span><span class="sxs-lookup"><span data-stu-id="5ab47-212">Select **OK** to close the **Select Database** blade.</span></span> <span data-ttu-id="5ab47-213">Ardından **Tamam** kapatmak için **yapılandırma şirket içi** dikey penceresinde ve oluşturulan ve dağıtılan yeni eşitleme üye tamamlanmasını bekleyin.</span><span class="sxs-lookup"><span data-stu-id="5ab47-213">Then select **OK** to close the **Configure On-Premises** blade and wait for the new sync member to be created and deployed.</span></span> <span data-ttu-id="5ab47-214">Son olarak, tıklatın **Tamam** kapatmak için **eşitleme üyeleri seçin** dikey.</span><span class="sxs-lookup"><span data-stu-id="5ab47-214">Finally, click **OK** to close the **Select sync members** blade.</span></span>

        ![Şirket içi veritabanında eşitleme grubuna eklendi](media/sql-database-get-started-sql-data-sync/datasync-preview-onpremadded.png)

3.  <span data-ttu-id="5ab47-216">SQL veri eşitleme ve yerel aracı bağlanmak için kullanıcı adınızı role ekleyin `DataSync_Executor`.</span><span class="sxs-lookup"><span data-stu-id="5ab47-216">To connect to SQL Data Sync and the local agent, add your user name to the role `DataSync_Executor`.</span></span> <span data-ttu-id="5ab47-217">Veri Eşitleme SQL Server örneğinde bu rol oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5ab47-217">Data Sync creates this role on the SQL Server instance.</span></span>

## <a name="step-3---configure-sync-group"></a><span data-ttu-id="5ab47-218">3. adım - eşitleme grubunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5ab47-218">Step 3 - Configure sync group</span></span>

<span data-ttu-id="5ab47-219">Yeni eşitleme Grup üyeleri oluşturulan ve dağıtılan, adım 3, sonra **yapılandırma eşitleme grubu**, vurgulanan **yeni eşitleme grubu** dikey.</span><span class="sxs-lookup"><span data-stu-id="5ab47-219">After the new sync group members are created and deployed, Step 3, **Configure sync group**, is highlighted in the **New sync group** blade.</span></span>

1.  <span data-ttu-id="5ab47-220">Üzerinde **tabloları** eşitleme listesinden bir veritabanı grubu üyeleri ve ardından dikey penceresinde, select **yenileme şema**.</span><span class="sxs-lookup"><span data-stu-id="5ab47-220">On the **Tables** blade, select a database from the list of sync group members, and then select **Refresh schema**.</span></span>

2.  <span data-ttu-id="5ab47-221">Kullanılabilir tabloların listeden eşitlemek istediğiniz tabloları seçin.</span><span class="sxs-lookup"><span data-stu-id="5ab47-221">From the list of available tables, select the tables that you want to sync.</span></span>

    ![Eşitlenecek tabloları seçin](media/sql-database-get-started-sql-data-sync/datasync-preview-tables.png)

3.  <span data-ttu-id="5ab47-223">Varsayılan olarak, tablodaki tüm sütunların seçilir.</span><span class="sxs-lookup"><span data-stu-id="5ab47-223">By default, all columns in the table are selected.</span></span> <span data-ttu-id="5ab47-224">Tüm sütunları eşitlemek istemiyorsanız eşitlemek istemediğiniz sütunlar için onay kutusunu devre dışı bırakın. Seçili birincil anahtar sütunu olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="5ab47-224">If you don't want to sync all the columns, disable the checkbox for the columns that you don't want to sync. Be sure to leave the primary key column selected.</span></span>

    ![Eşitlemek için alanları seçin](media/sql-database-get-started-sql-data-sync/datasync-preview-tables2.png)

4.  <span data-ttu-id="5ab47-226">Son olarak, seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="5ab47-226">Finally, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ab47-227">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5ab47-227">Next steps</span></span>
<span data-ttu-id="5ab47-228">Tebrikler.</span><span class="sxs-lookup"><span data-stu-id="5ab47-228">Congratulations.</span></span> <span data-ttu-id="5ab47-229">Bir SQL veritabanı örneğini ve SQL Server veritabanı içeren bir eşitleme grubu oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="5ab47-229">You have created a sync group that includes both a SQL Database instance and a SQL Server database.</span></span>

<span data-ttu-id="5ab47-230">SQL Database ve SQL veri eşitleme hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="5ab47-230">For more info about SQL Database and SQL Data Sync, see:</span></span>

-   [<span data-ttu-id="5ab47-231">Tam SQL veri eşitleme teknik belgeler indirin</span><span class="sxs-lookup"><span data-stu-id="5ab47-231">Download the complete SQL Data Sync technical documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)
-   [<span data-ttu-id="5ab47-232">SQL veri eşitleme REST API belgelerini indirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="5ab47-232">Download the SQL Data Sync REST API documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)
-   [<span data-ttu-id="5ab47-233">SQL veritabanı genel bakış</span><span class="sxs-lookup"><span data-stu-id="5ab47-233">SQL Database Overview</span></span>](sql-database-technical-overview.md)
-   [<span data-ttu-id="5ab47-234">Veritabanı yaşam döngüsü yönetimi</span><span class="sxs-lookup"><span data-stu-id="5ab47-234">Database Lifecycle Management</span></span>](https://msdn.microsoft.com/library/jj907294.aspx)
