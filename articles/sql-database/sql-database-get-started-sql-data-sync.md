---
title: "aaaGetting başlatılan Azure SQL veri eşitleme (Önizleme) | Microsoft Docs"
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
ms.openlocfilehash: 666d09237e42acc23ae3c8c81e60734a413f5949
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-sql-data-sync-preview"></a><span data-ttu-id="8d0ea-103">Azure SQL veri eşitleme (Önizleme) ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="8d0ea-103">Getting Started with Azure SQL Data Sync (Preview)</span></span>
<span data-ttu-id="8d0ea-104">Bu öğreticide, bir karma eşitleme grubu oluşturarak Azure SQL veri eşitleme tooset Azure SQL Database ve SQL Server örneklerini içeren öğrenin.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-104">In this tutorial, you learn how tooset up Azure SQL Data Sync by creating a hybrid sync group that contains both Azure SQL Database and SQL Server instances.</span></span> <span data-ttu-id="8d0ea-105">Merhaba yeni eşitleme grubu tam olarak yapılandırılmamış ve ayarladığınız hello zamanlamada eşitler.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-105">hello new sync group is fully configured and synchronizes on hello schedule you set.</span></span>

<span data-ttu-id="8d0ea-106">Bu öğretici, SQL Database ve SQL Server ile en az bazı konusunda deneyim sahibi olduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-106">This tutorial assumes that you have at least some prior experience with SQL Database and with SQL Server.</span></span> 

<span data-ttu-id="8d0ea-107">SQL veri eşitleme genel bakış için bkz: [verilerini](sql-database-sync-data.md).</span><span class="sxs-lookup"><span data-stu-id="8d0ea-107">For an overview of SQL Data Sync, see [Sync data](sql-database-sync-data.md).</span></span>

<span data-ttu-id="8d0ea-108">Göster tam PowerShell örnekleri için nasıl tooconfigure SQL veri eşitleme makaleleri aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="8d0ea-108">For complete PowerShell examples that show how tooconfigure SQL Data Sync, see hello following articles:</span></span>
-   [<span data-ttu-id="8d0ea-109">Birden çok Azure SQL veritabanı arasında PowerShell toosync kullanın</span><span class="sxs-lookup"><span data-stu-id="8d0ea-109">Use PowerShell toosync between multiple Azure SQL databases</span></span>](scripts/sql-database-sync-data-between-sql-databases.md)
-   [<span data-ttu-id="8d0ea-110">Bir Azure SQL Database ve SQL Server içi veritabanı arasında PowerShell toosync kullanın</span><span class="sxs-lookup"><span data-stu-id="8d0ea-110">Use PowerShell toosync between an Azure SQL Database and a SQL Server on-premises database</span></span>](scripts/sql-database-sync-data-between-azure-onprem.md)

> [!NOTE]
> <span data-ttu-id="8d0ea-111">Merhaba tam teknik belgeler önceden, MSDN'de bulunan Azure SQL veri eşitleme için ayarlanmış olarak kullanılabilir bir. PDF belgesini.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-111">hello complete technical documentation set for Azure SQL Data Sync, formerly located on MSDN, is available as a .PDF document.</span></span> <span data-ttu-id="8d0ea-112">Karşıdan [burada](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).</span><span class="sxs-lookup"><span data-stu-id="8d0ea-112">Download it [here](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).</span></span>

## <a name="step-1---create-sync-group"></a><span data-ttu-id="8d0ea-113">1. adım - eşitleme grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="8d0ea-113">Step 1 - Create sync group</span></span>

### <a name="locate-hello-data-sync-settings"></a><span data-ttu-id="8d0ea-114">Merhaba veri eşitleme ayarlarını bulun</span><span class="sxs-lookup"><span data-stu-id="8d0ea-114">Locate hello Data Sync settings</span></span>

1.  <span data-ttu-id="8d0ea-115">Tarayıcınızda, toohello Azure portalına gidin.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-115">In your browser, navigate toohello Azure portal.</span></span>

2.  <span data-ttu-id="8d0ea-116">Merhaba Portalı'nda, SQL veritabanlarınızın panonuz veya hello SQL veritabanları simgesi hello araç çubuğunda bulun.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-116">In hello portal, locate your SQL databases from your Dashboard or from hello SQL Databases icon on hello toolbar.</span></span>

    ![Azure SQL veritabanı listesi](media/sql-database-get-started-sql-data-sync/datasync-preview-sqldbs.png)

3.  <span data-ttu-id="8d0ea-118">Merhaba üzerinde **SQL veritabanları** dikey penceresinde, select hello hello hub veritabanı için veri eşitleme hello SQL veritabanı dikey penceresini açar gibi toouse istediğiniz var olan SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-118">On hello **SQL databases** blade, select hello existing SQL database that you want toouse as hello hub database for Data Sync. hello SQL database blade opens.</span></span>

4.  <span data-ttu-id="8d0ea-119">Merhaba SQL veritabanı dikey penceresinde hello seçili veritabanı, seçin **eşitleme tooother veritabanları**.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-119">On hello SQL database blade for hello selected database, select **Sync tooother databases**.</span></span> <span data-ttu-id="8d0ea-120">Merhaba veri eşitleme dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-120">hello Data Sync blade opens.</span></span>

    ![Eşitleme tooother veritabanları seçeneği](media/sql-database-get-started-sql-data-sync/datasync-preview-newsyncgroup.png)

### <a name="create-a-new-sync-group"></a><span data-ttu-id="8d0ea-122">Yeni bir eşitleme grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="8d0ea-122">Create a new Sync Group</span></span>

1.  <span data-ttu-id="8d0ea-123">Merhaba veri eşitleme dikey penceresinde, seçin **yeni eşitleme grubu**.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-123">On hello Data Sync blade, select **New Sync Group**.</span></span> <span data-ttu-id="8d0ea-124">Merhaba **yeni eşitleme grubu** dikey pencere açılır adım 1 ile **eşitleme Grup Oluştur**, vurgulanan.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-124">hello **New sync group** blade opens with Step 1, **Create sync group**, highlighted.</span></span> <span data-ttu-id="8d0ea-125">Merhaba **veri eşitleme grubu oluşturma** dikey penceresi de açılır.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-125">hello **Create Data Sync Group** blade also opens.</span></span>

2.  <span data-ttu-id="8d0ea-126">Merhaba üzerinde **veri eşitleme grubu oluşturma** dikey penceresinde, öğeleri hello:</span><span class="sxs-lookup"><span data-stu-id="8d0ea-126">On hello **Create Data Sync Group** blade, do hello following things:</span></span>

    1.  <span data-ttu-id="8d0ea-127">Merhaba, **eşitleme grubu adı** alanında, hello yeni eşitleme grubu için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-127">In hello **Sync Group Name** field, enter a name for hello new sync group.</span></span>

    2.  <span data-ttu-id="8d0ea-128">Merhaba, **eşitleme meta veri veritabanı** bölümünde, toocreate (önerilen) yeni bir veritabanı veya toouse var olan veritabanı olup olmadığını seçin.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-128">In hello **Sync Metadata Database** section, choose whether toocreate a new database (recommended) or toouse an existing database.</span></span>

        > [!NOTE]
        > <span data-ttu-id="8d0ea-129">Microsoft, eşitleme meta veri veritabanı hello gibi bir yeni, boş bir veritabanı toouse oluşturduğunuz önerir.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-129">Microsoft recommends that you create a new, empty database toouse as hello Sync Metadata Database.</span></span> <span data-ttu-id="8d0ea-130">Veri Eşitleme bu veritabanında tablolar oluşturur ve sık kullanılan bir iş yükü çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-130">Data Sync creates tables in this database and runs a frequent workload.</span></span> <span data-ttu-id="8d0ea-131">Bu veritabanı, otomatik olarak hello tüm eşitleme gruplarınızı hello seçili bölgede için eşitleme meta veri veritabanı olarak paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-131">This database is automatically shared as hello Sync Metadata Database for all of your Sync groups in hello selected region.</span></span> <span data-ttu-id="8d0ea-132">Bırakma olmadan hello eşitleme meta veri veritabanı, adını ya da kendi hizmet düzeyi değiştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-132">You can't change hello Sync Metadata Database, its name, or its service level without dropping it.</span></span>

        <span data-ttu-id="8d0ea-133">Seçerseniz **yeni veritabanı**seçin **yeni veritabanı oluştur.**</span><span class="sxs-lookup"><span data-stu-id="8d0ea-133">If you chose **New database**, select **Create new database.**</span></span> <span data-ttu-id="8d0ea-134">Merhaba **SQL veritabanı** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-134">hello **SQL Database** blade opens.</span></span> <span data-ttu-id="8d0ea-135">Merhaba üzerinde **SQL veritabanı** dikey penceresinde, adı ve hello yeni veritabanını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-135">On hello **SQL Database** blade, name and configure hello new database.</span></span> <span data-ttu-id="8d0ea-136">Ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-136">Then select **OK**.</span></span>

        <span data-ttu-id="8d0ea-137">Seçerseniz **varolan veritabanını kullan**seçin hello veritabanından hello listesi.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-137">If you chose **Use existing database**, select hello database from hello list.</span></span>

    3.  <span data-ttu-id="8d0ea-138">Merhaba, **otomatik eşitleme** bölümünde, ilk seçin **üzerinde** veya **devre dışı**.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-138">In hello **Automatic Sync** section, first select **On** or **Off**.</span></span>

        <span data-ttu-id="8d0ea-139">Seçerseniz **üzerinde**, hello içinde **eşitleme sıklığı** bölümünde, bir sayı girin ve saniye, dakika, saat veya gün seçin.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-139">If you chose **On**, in hello **Sync Frequency** section, enter a number and select Seconds, Minutes, Hours, or Days.</span></span>

        ![Eşitleme sıklığı belirtin](media/sql-database-get-started-sql-data-sync/datasync-preview-syncfreq.png)

    4.  <span data-ttu-id="8d0ea-141">Merhaba, **çakışma çözümü** bölümünde, "Hub wins" veya "Üye WINS." seçin</span><span class="sxs-lookup"><span data-stu-id="8d0ea-141">In hello **Conflict Resolution** section, select "Hub wins" or "Member wins."</span></span>

        ![Çakışmalar nasıl çözümlenir belirtin](media/sql-database-get-started-sql-data-sync/datasync-preview-conflictres.png)

    5.  <span data-ttu-id="8d0ea-143">Seçin **Tamam** ve oluşturulan ve dağıtılan hello yeni eşitleme grubu toobe için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-143">Select **OK** and wait for hello new sync group toobe created and deployed.</span></span>

## <a name="step-2---add-sync-members"></a><span data-ttu-id="8d0ea-144">2. adım - eşitleme üyeleri Ekle</span><span class="sxs-lookup"><span data-stu-id="8d0ea-144">Step 2 - Add sync members</span></span>

<span data-ttu-id="8d0ea-145">Hello yeni eşitleme grubu oluşturup, adım 2 ' yi dağıttıktan sonra **eşitleme üye eklemek**, hello vurgulanmış **yeni eşitleme grubu** dikey.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-145">After hello new sync group is created and deployed, Step 2, **Add sync members**, is highlighted in hello **New sync group** blade.</span></span>

<span data-ttu-id="8d0ea-146">Merhaba, **Hub veritabanı** bölümünde, için hello SQL veritabanı sunucusu hangi hello hub veritabanı bulunduğu hello varolan kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-146">In hello **Hub Database** section, enter hello existing credentials for hello SQL Database server on which hello hub database is located.</span></span> <span data-ttu-id="8d0ea-147">Girmeyin *yeni* Bu bölümde kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-147">Don't enter *new* credentials in this section.</span></span>

![Hub veritabanı toosync Grup eklendi](media/sql-database-get-started-sql-data-sync/datasync-preview-hubadded.png)

## <a name="add-an-azure-sql-database"></a><span data-ttu-id="8d0ea-149">Bir Azure SQL veritabanı Ekle</span><span class="sxs-lookup"><span data-stu-id="8d0ea-149">Add an Azure SQL Database</span></span>

<span data-ttu-id="8d0ea-150">Merhaba, **üye veritabanı** bölümünde, isteğe bağlı olarak bir Azure SQL veritabanı toohello eşitleme grubu seçerek eklemek **Azure veritabanı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-150">In hello **Member Database** section, optionally add an Azure SQL Database toohello sync group by selecting **Add an Azure Database**.</span></span> <span data-ttu-id="8d0ea-151">Merhaba **Azure veritabanını yapılandırma** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-151">hello **Configure Azure Database** blade opens.</span></span>

<span data-ttu-id="8d0ea-152">Merhaba üzerinde **Azure veritabanını yapılandırma** dikey penceresinde, öğeleri hello:</span><span class="sxs-lookup"><span data-stu-id="8d0ea-152">On hello **Configure Azure Database** blade, do hello following things:</span></span>

1.  <span data-ttu-id="8d0ea-153">Merhaba, **eşitleme üye adı** alanında, hello yeni eşitleme üyesi için bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-153">In hello **Sync Member Name** field, provide a name for hello new sync member.</span></span> <span data-ttu-id="8d0ea-154">Bu ad hello veritabanının kendisi hello adından farklıdır.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-154">This name is distinct from hello name of hello database itself.</span></span>

2.  <span data-ttu-id="8d0ea-155">Merhaba, **abonelik** alanında, select hello ilişkili faturalandırma için Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-155">In hello **Subscription** field, select hello associated Azure subscription for billing purposes.</span></span>

3.  <span data-ttu-id="8d0ea-156">Merhaba, **Azure SQL Server** alanında, select hello varolan SQL veritabanı sunucusu.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-156">In hello **Azure SQL Server** field, select hello existing SQL database server.</span></span>

4.  <span data-ttu-id="8d0ea-157">Merhaba, **Azure SQL veritabanı** alanında, select hello varolan bir SQL veritabanının.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-157">In hello **Azure SQL Database** field, select hello existing SQL database.</span></span>

5.  <span data-ttu-id="8d0ea-158">Merhaba, **eşitleme yönergeleri** alanında, çift yönlü eşitleme, toohello Hub'ı seçin veya hello Hub.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-158">In hello **Sync Directions** field, select Bi-directional Sync, toohello Hub, or From hello Hub.</span></span>

    ![Yeni bir SQL veritabanı eşitleme üye ekleme](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadding.png)

6.  <span data-ttu-id="8d0ea-160">Merhaba, **kullanıcıadı** ve **parola** alanlar için hello SQL veritabanı sunucusu hangi hello üye veritabanı bulunduğu hello varolan kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-160">In hello **Username** and **Password** fields, enter hello existing credentials for hello SQL Database server on which hello member database is located.</span></span> <span data-ttu-id="8d0ea-161">Girmeyin *yeni* Bu bölümde kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-161">Don't enter *new* credentials in this section.</span></span>

7.  <span data-ttu-id="8d0ea-162">Seçin **Tamam** ve oluşturulan ve dağıtılan hello yeni eşitleme üye toobe için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-162">Select **OK** and wait for hello new sync member toobe created and deployed.</span></span>

    ![Yeni SQL veritabanı eşitleme üye eklendi](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadded.png)

## <a name="add-an-on-premises-sql-server-database"></a><span data-ttu-id="8d0ea-164">Bir şirket içi SQL Server veritabanı ekleyin</span><span class="sxs-lookup"><span data-stu-id="8d0ea-164">Add an on-premises SQL Server database</span></span>

<span data-ttu-id="8d0ea-165">Merhaba, **üye veritabanı** bölümünde, isteğe bağlı olarak bir şirket içi SQL Server toohello eşitleme grubu seçerek eklemek **bir şirket içi veritabanı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-165">In hello **Member Database** section, optionally add an on-premises SQL Server toohello sync group by selecting **Add an On-Premises Database**.</span></span> <span data-ttu-id="8d0ea-166">Merhaba **yapılandırma şirket içi** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-166">hello **Configure On-Premises** blade opens.</span></span>

<span data-ttu-id="8d0ea-167">Merhaba üzerinde **yapılandırma şirket içi** dikey penceresinde, öğeleri hello:</span><span class="sxs-lookup"><span data-stu-id="8d0ea-167">On hello **Configure On-Premises** blade, do hello following things:</span></span>

1.  <span data-ttu-id="8d0ea-168">Seçin **Seç hello eşitleme Aracısı ağ geçidi**.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-168">Select **Choose hello Sync Agent Gateway**.</span></span> <span data-ttu-id="8d0ea-169">Merhaba **seçin eşitleme Aracısı** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-169">hello **Select Sync Agent** blade opens.</span></span>

    ![Merhaba eşitleme Aracısı ağ geçidi seçin](media/sql-database-get-started-sql-data-sync/datasync-preview-choosegateway.png)

2.  <span data-ttu-id="8d0ea-171">Merhaba üzerinde **Seç hello eşitleme Aracısı ağ geçidi** dikey penceresinde, seçin olup olmadığını toouse var olan bir aracıyı veya yeni bir aracı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-171">On hello **Choose hello Sync Agent Gateway** blade, choose whether toouse an existing agent or create a new agent.</span></span>

    <span data-ttu-id="8d0ea-172">Seçerseniz **varolan aracıları**, hello hello listeden var olan aracıyı seçin.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-172">If you chose **Existing agents**, select hello existing agent from hello list.</span></span>

    <span data-ttu-id="8d0ea-173">Seçerseniz **yeni bir aracı oluşturma**, öğeleri hello:</span><span class="sxs-lookup"><span data-stu-id="8d0ea-173">If you chose **Create a new agent**, do hello following things:</span></span>

    1.  <span data-ttu-id="8d0ea-174">Sağlanan hello bağlantısından Hello istemci eşitleme Aracısı yazılımını indirin ve hello SQL Server bulunduğu hello bilgisayara yükleyin.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-174">Download hello client sync agent software from hello link provided and install it on hello computer where hello SQL Server is located.</span></span>
 
        > [!IMPORTANT]
        > <span data-ttu-id="8d0ea-175">Merhaba sunucusuyla iletişim tooopen giden TCP bağlantı noktası 1433 hello güvenlik duvarı toolet hello istemci aracısında var.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-175">You have tooopen outbound TCP port 1433 in hello firewall toolet hello client agent communicate with hello server.</span></span>


    2.  <span data-ttu-id="8d0ea-176">Merhaba aracısı için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-176">Enter a name for hello agent.</span></span>

    3.  <span data-ttu-id="8d0ea-177">Seçin **oluşturun ve anahtarı oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-177">Select **Create and Generate Key**.</span></span>

    4.  <span data-ttu-id="8d0ea-178">Merhaba Aracısı anahtar toohello panoya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-178">Copy hello agent key toohello clipboard.</span></span>
        
        ![Yeni bir eşitleme aracı oluşturma](media/sql-database-get-started-sql-data-sync/datasync-preview-selectsyncagent.png)

    5.  <span data-ttu-id="8d0ea-180">Seçin **Tamam** tooclose hello **seçin eşitleme Aracısı** dikey.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-180">Select **OK** tooclose hello **Select Sync Agent** blade.</span></span>

    6.  <span data-ttu-id="8d0ea-181">Merhaba SQL Server bilgisayarında, bulun ve hello istemci eşitleme Aracısı uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-181">On hello SQL Server computer, locate and run hello Client Sync Agent app.</span></span>

        ![İstemci Aracısı uygulama Hello veri eşitleme](media/sql-database-get-started-sql-data-sync/datasync-preview-clientagent.png)

    7.  <span data-ttu-id="8d0ea-183">Merhaba eşitleme Aracısı uygulamada seçin **aracı anahtarını Gönder**.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-183">In hello sync agent app, select **Submit Agent Key**.</span></span> <span data-ttu-id="8d0ea-184">Merhaba **eşitleme meta veri veritabanı yapılandırması** iletişim kutusu açılır.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-184">hello **Sync Metadata Database Configuration** dialog box opens.</span></span>

    8.  <span data-ttu-id="8d0ea-185">Merhaba, **eşitleme meta veri veritabanı yapılandırması** iletişim kutusu, Azure portal hello kopyalanan hello aracı anahtarını yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-185">In hello **Sync Metadata Database Configuration** dialog box, paste in hello agent key copied from hello Azure portal.</span></span> <span data-ttu-id="8d0ea-186">Ayrıca hello hello Azure SQL veritabanı sunucusu hangi hello meta veri veritabanının bulunduğu için var olan kimlik bilgilerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-186">Also provide hello existing credentials for hello Azure SQL Database server on which hello metadata database is located.</span></span> <span data-ttu-id="8d0ea-187">(Yeni bir meta veri veritabanı oluşturduysanız, bu üzerinde hello veritabanıdır hello hub veritabanı aynı sunucuya.) Seçin **Tamam** ve hello yapılandırma toofinish için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-187">(If you created a new metadata database, this database is on hello same server as hello hub database.) Select **OK** and wait for hello configuration toofinish.</span></span>

        ![Merhaba aracı anahtarını ve sunucu kimlik bilgilerini girin](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-enterkey.png)

        >   [!NOTE] 
        >   <span data-ttu-id="8d0ea-189">Bu noktada bir güvenlik duvarı hatası alırsanız, toocreate bir güvenlik duvarı kuralı hello SQL Server bilgisayardan gelen trafiği Azure tooallow sahip.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-189">If you get a firewall error at this point, you have toocreate a firewall rule on Azure tooallow incoming traffic from hello SQL Server computer.</span></span> <span data-ttu-id="8d0ea-190">Merhaba kural hello Portalı'nda el ile oluşturabilirsiniz, ancak daha kolay toocreate bulabilirsiniz, SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="8d0ea-190">You can create hello rule manually in hello portal, but you may find it easier toocreate it in SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="8d0ea-191">SSMS, Azure üzerinde tooconnect toohello hub veritabanı deneyin.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-191">In SSMS, try tooconnect toohello hub database on Azure.</span></span> <span data-ttu-id="8d0ea-192">Adı olarak girin \<hub_database_name\>. database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-192">Enter its name as \<hub_database_name\>.database.windows.net.</span></span> <span data-ttu-id="8d0ea-193">Merhaba iletişim kutusu tooconfigure hello Azure güvenlik duvarı kuralı Hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-193">Follow hello steps in hello dialog box tooconfigure hello Azure firewall rule.</span></span> <span data-ttu-id="8d0ea-194">Ardından toohello istemci eşitleme Aracısı uygulamaya dönün.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-194">Then return toohello Client Sync Agent app.</span></span>

    9.  <span data-ttu-id="8d0ea-195">Merhaba istemci eşitleme Aracısı uygulamanın tıklayın **kaydetmek** tooregister hello Aracısı ile bir SQL Server veritabanı.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-195">In hello Client Sync Agent app, click **Register** tooregister a SQL Server database with hello agent.</span></span> <span data-ttu-id="8d0ea-196">Merhaba **SQL Server yapılandırma** iletişim kutusu açılır.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-196">hello **SQL Server Configuration** dialog box opens.</span></span>

        ![Ekleme ve bir SQL Server veritabanı yapılandırma](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-adddb.png)

    10. <span data-ttu-id="8d0ea-198">Merhaba, **SQL Server yapılandırma** iletişim kutusunda, seçin olup olmadığını tooconnect SQL Server kimlik doğrulaması veya Windows kimlik doğrulaması kullanarak.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-198">In hello **SQL Server Configuration** dialog box, choose whether tooconnect by using SQL Server authentication or Windows authentication.</span></span> <span data-ttu-id="8d0ea-199">SQL Server kimlik doğrulamasını seçerseniz, hello varolan kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-199">If you chose SQL Server authentication, enter hello existing credentials.</span></span> <span data-ttu-id="8d0ea-200">Merhaba SQL Server adı ve hello hello veritabanının adını toosync istediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-200">Provide hello SQL Server name and hello name of hello database that you want toosync.</span></span> <span data-ttu-id="8d0ea-201">Seçin **Bağlantıyı Sına** tootest ayarlarınızı.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-201">Select **Test connection** tootest your settings.</span></span> <span data-ttu-id="8d0ea-202">Ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-202">Then select **Save**.</span></span> <span data-ttu-id="8d0ea-203">Merhaba kayıtlı veritabanı hello listesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-203">hello registered database appears in hello list.</span></span>

        ![SQL Server veritabanı artık kayıtlı](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-dbadded.png)

    11. <span data-ttu-id="8d0ea-205">Merhaba istemci eşitleme Aracısı uygulama artık kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-205">You can now close hello Client Sync Agent app.</span></span>

    12. <span data-ttu-id="8d0ea-206">Hello portalında, hello **yapılandırma şirket içi** dikey penceresinde, select **hello veritabanı seçin.**</span><span class="sxs-lookup"><span data-stu-id="8d0ea-206">In hello portal, on hello **Configure On-Premises** blade, select **Select hello Database.**</span></span> <span data-ttu-id="8d0ea-207">Merhaba **Veritabanı Seç** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-207">hello **Select Database** blade opens.</span></span>

    13. <span data-ttu-id="8d0ea-208">Merhaba üzerinde **Veritabanı Seç** dikey penceresinde hello **eşitleme üye adı** alanında, hello yeni eşitleme üyesi için bir ad sağlayın.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-208">On hello **Select Database** blade, in hello **Sync Member Name** field, provide a name for hello new sync member.</span></span> <span data-ttu-id="8d0ea-209">Bu ad hello veritabanının kendisi hello adından farklıdır.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-209">This name is distinct from hello name of hello database itself.</span></span> <span data-ttu-id="8d0ea-210">Merhaba veritabanı hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-210">Select hello database from hello list.</span></span> <span data-ttu-id="8d0ea-211">Merhaba, **eşitleme yönergeleri** alanında, çift yönlü eşitleme, toohello Hub'ı seçin veya hello Hub.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-211">In hello **Sync Directions** field, select Bi-directional Sync, toohello Hub, or From hello Hub.</span></span>

        ![Şirket içi veritabanında Hello seçin](media/sql-database-get-started-sql-data-sync/datasync-preview-selectdb.png)

    14. <span data-ttu-id="8d0ea-213">Seçin **Tamam** tooclose hello **Veritabanı Seç** dikey.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-213">Select **OK** tooclose hello **Select Database** blade.</span></span> <span data-ttu-id="8d0ea-214">Ardından **Tamam** tooclose hello **yapılandırma şirket içi** dikey ve hello bekle yeni oluşturulan ve dağıtılan üye toobe eşitleme.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-214">Then select **OK** tooclose hello **Configure On-Premises** blade and wait for hello new sync member toobe created and deployed.</span></span> <span data-ttu-id="8d0ea-215">Son olarak, tıklatın **Tamam** tooclose hello **eşitleme üyeleri seçin** dikey.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-215">Finally, click **OK** tooclose hello **Select sync members** blade.</span></span>

        ![Şirket içi veritabanında toosync Grup eklendi](media/sql-database-get-started-sql-data-sync/datasync-preview-onpremadded.png)

3.  <span data-ttu-id="8d0ea-217">tooconnect tooSQL veri eşitleme ve hello yerel aracı, ekleme, kullanıcı adı toohello rolünüz `DataSync_Executor`.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-217">tooconnect tooSQL Data Sync and hello local agent, add your user name toohello role `DataSync_Executor`.</span></span> <span data-ttu-id="8d0ea-218">Veri Eşitleme hello SQL Server örneğinde bu rol oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-218">Data Sync creates this role on hello SQL Server instance.</span></span>

## <a name="step-3---configure-sync-group"></a><span data-ttu-id="8d0ea-219">3. adım - eşitleme grubunu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8d0ea-219">Step 3 - Configure sync group</span></span>

<span data-ttu-id="8d0ea-220">Merhaba yeni eşitleme grubu üyeleri oluşturulan ve dağıtılan, adım 3, sonra **yapılandırma eşitleme grubu**, hello vurgulanmış **yeni eşitleme grubu** dikey.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-220">After hello new sync group members are created and deployed, Step 3, **Configure sync group**, is highlighted in hello **New sync group** blade.</span></span>

1.  <span data-ttu-id="8d0ea-221">Merhaba üzerinde **tabloları** eşitleme hello listesinden bir veritabanı grubu üyeleri ve ardından dikey penceresinde, select **yenileme şema**.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-221">On hello **Tables** blade, select a database from hello list of sync group members, and then select **Refresh schema**.</span></span>

2.  <span data-ttu-id="8d0ea-222">Kullanılabilir tabloların Hello listeden toosync istediğiniz hello tabloları seçin.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-222">From hello list of available tables, select hello tables that you want toosync.</span></span>

    ![Tablolar toosync seçin](media/sql-database-get-started-sql-data-sync/datasync-preview-tables.png)

3.  <span data-ttu-id="8d0ea-224">Varsayılan olarak, hello tablodaki tüm sütunları seçilir.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-224">By default, all columns in hello table are selected.</span></span> <span data-ttu-id="8d0ea-225">Tüm hello sütunları toosync istemiyorsanız, toosync istemediğiniz hello sütunları hello onay kutusunu devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-225">If you don't want toosync all hello columns, disable hello checkbox for hello columns that you don't want toosync.</span></span> <span data-ttu-id="8d0ea-226">Tooleave hello birincil anahtar sütunu seçili olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-226">Be sure tooleave hello primary key column selected.</span></span>

    ![Alanları toosync seçin](media/sql-database-get-started-sql-data-sync/datasync-preview-tables2.png)

4.  <span data-ttu-id="8d0ea-228">Son olarak, seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-228">Finally, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8d0ea-229">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8d0ea-229">Next steps</span></span>
<span data-ttu-id="8d0ea-230">Tebrikler.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-230">Congratulations.</span></span> <span data-ttu-id="8d0ea-231">Bir SQL veritabanı örneğini ve SQL Server veritabanı içeren bir eşitleme grubu oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="8d0ea-231">You have created a sync group that includes both a SQL Database instance and a SQL Server database.</span></span>

<span data-ttu-id="8d0ea-232">SQL Database ve SQL veri eşitleme hakkında daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="8d0ea-232">For more info about SQL Database and SQL Data Sync, see:</span></span>

-   [<span data-ttu-id="8d0ea-233">Merhaba tam SQL veri eşitleme teknik belgeler indirin</span><span class="sxs-lookup"><span data-stu-id="8d0ea-233">Download hello complete SQL Data Sync technical documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)
-   [<span data-ttu-id="8d0ea-234">Merhaba SQL veri eşitleme REST API belgelerini indirebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="8d0ea-234">Download hello SQL Data Sync REST API documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)
-   [<span data-ttu-id="8d0ea-235">SQL veritabanı genel bakış</span><span class="sxs-lookup"><span data-stu-id="8d0ea-235">SQL Database Overview</span></span>](sql-database-technical-overview.md)
-   [<span data-ttu-id="8d0ea-236">Veritabanı yaşam döngüsü yönetimi</span><span class="sxs-lookup"><span data-stu-id="8d0ea-236">Database Lifecycle Management</span></span>](https://msdn.microsoft.com/library/jj907294.aspx)
