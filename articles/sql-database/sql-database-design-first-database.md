---
title: "aaaDesign ilk Azure SQL veritabanınızı | Microsoft Docs"
description: "İlk Azure SQL veritabanınızı toodesign öğrenin."
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop databases
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/03/2017
ms.author: carlrab
ms.openlocfilehash: 65f0a1594cbdda7480abf32a847266a073e7560d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-sql-database"></a><span data-ttu-id="0ad9e-103">İlk Azure SQL veritabanınızı tasarlama</span><span class="sxs-lookup"><span data-stu-id="0ad9e-103">Design your first Azure SQL database</span></span>

<span data-ttu-id="0ad9e-104">Azure SQL veritabanı bir ilişkisel veritabanı-olarak-a (DBaaS) hello Microsoft Cloud ("Azure") hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-104">Azure SQL Database is a relational database-as-a service (DBaaS) in hello Microsoft Cloud ("Azure").</span></span> <span data-ttu-id="0ad9e-105">Bu öğreticide, nasıl toouse hello Azure portal öğrenin ve [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) için:</span><span class="sxs-lookup"><span data-stu-id="0ad9e-105">In this tutorial, you learn how toouse hello Azure portal and [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="0ad9e-106">Hello Azure portalında bir veritabanı oluşturun</span><span class="sxs-lookup"><span data-stu-id="0ad9e-106">Create a database in hello Azure portal</span></span>
> * <span data-ttu-id="0ad9e-107">Hello Azure portal sunucu düzeyinde güvenlik duvarı kuralında ayarlama</span><span class="sxs-lookup"><span data-stu-id="0ad9e-107">Set up a server-level firewall rule in hello Azure portal</span></span>
> * <span data-ttu-id="0ad9e-108">SSMS ile toohello veritabanına bağlanın</span><span class="sxs-lookup"><span data-stu-id="0ad9e-108">Connect toohello database with SSMS</span></span>
> * <span data-ttu-id="0ad9e-109">SSMS ile tabloları oluşturma</span><span class="sxs-lookup"><span data-stu-id="0ad9e-109">Create tables with SSMS</span></span>
> * <span data-ttu-id="0ad9e-110">Yığın BCP ile veri yükleme</span><span class="sxs-lookup"><span data-stu-id="0ad9e-110">Bulk load data with BCP</span></span>
> * <span data-ttu-id="0ad9e-111">SSMS ile bu verileri Sorgulama</span><span class="sxs-lookup"><span data-stu-id="0ad9e-111">Query that data with SSMS</span></span>
> * <span data-ttu-id="0ad9e-112">Merhaba veritabanı tooa önceki geri [geri yükleme noktası](sql-database-recovery-using-backups.md#point-in-time-restore) hello Azure portal'ın</span><span class="sxs-lookup"><span data-stu-id="0ad9e-112">Restore hello database tooa previous [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore) in hello Azure portal</span></span>

<span data-ttu-id="0ad9e-113">Bir Azure aboneliğiniz yoksa [ücretsiz bir hesap oluşturma](https://azure.microsoft.com/free/) başlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-113">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ad9e-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0ad9e-114">Prerequisites</span></span>

<span data-ttu-id="0ad9e-115">toocomplete Bu öğretici, yapma emin yüklediğiniz:</span><span class="sxs-lookup"><span data-stu-id="0ad9e-115">toocomplete this tutorial, make sure you have installed:</span></span>
- <span data-ttu-id="0ad9e-116">Merhaba en yeni sürümünü [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="0ad9e-116">hello newest version of [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS).</span></span>
- <span data-ttu-id="0ad9e-117">Merhaba en yeni sürümünü [BCP ve SQLCMD](https://www.microsoft.com/download/details.aspx?id=36433).</span><span class="sxs-lookup"><span data-stu-id="0ad9e-117">hello newest version of [BCP and SQLCMD](https://www.microsoft.com/download/details.aspx?id=36433).</span></span>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="0ad9e-118">Toohello Azure portalında oturum açın</span><span class="sxs-lookup"><span data-stu-id="0ad9e-118">Log in toohello Azure portal</span></span>

<span data-ttu-id="0ad9e-119">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0ad9e-119">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-blank-sql-database"></a><span data-ttu-id="0ad9e-120">Boş bir SQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0ad9e-120">Create a blank SQL database</span></span>

<span data-ttu-id="0ad9e-121">Azure SQL veritabanı bir dizi [işlem ve depolama kaynağı](sql-database-service-tiers.md) ile oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-121">An Azure SQL database is created with a defined set of [compute and storage resources](sql-database-service-tiers.md).</span></span> <span data-ttu-id="0ad9e-122">Merhaba veritabanı içinde oluşturulur bir [Azure kaynak grubu](../azure-resource-manager/resource-group-overview.md) ve bir [Azure SQL Database mantıksal sunucusu](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="0ad9e-122">hello database is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md) and in an [Azure SQL Database logical server](sql-database-features.md).</span></span> 

<span data-ttu-id="0ad9e-123">Bu adımları toocreate boş bir SQL veritabanı izleyin.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-123">Follow these steps toocreate a blank SQL database.</span></span> 

1. <span data-ttu-id="0ad9e-124">Merhaba tıklatın **yeni** düğmesi hello sol üst köşesinin hello Azure portalı üzerinde bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-124">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="0ad9e-125">Seçin **veritabanları** hello gelen **yeni** sayfasında ve seçin **SQL veritabanı** hello gelen **veritabanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-125">Select **Databases** from hello **New** page, and select **SQL Database** from hello **Databases** page.</span></span> 

   ![Boş veritabanı oluşturma](./media/sql-database-design-first-database/create-empty-database.png)

3. <span data-ttu-id="0ad9e-127">Hello SQL veritabanı formu görüntü önceki hello üzerinde gösterildiği gibi bilgileri, aşağıdaki hello ile doldurun:</span><span class="sxs-lookup"><span data-stu-id="0ad9e-127">Fill out hello SQL Database form with hello following information, as shown on hello preceding image:</span></span>   

   | <span data-ttu-id="0ad9e-128">Ayar</span><span class="sxs-lookup"><span data-stu-id="0ad9e-128">Setting</span></span>       | <span data-ttu-id="0ad9e-129">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="0ad9e-129">Suggested value</span></span> | <span data-ttu-id="0ad9e-130">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0ad9e-130">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="0ad9e-131">**Veritabanı adı**</span><span class="sxs-lookup"><span data-stu-id="0ad9e-131">**Database name**</span></span> | <span data-ttu-id="0ad9e-132">mySampleDatabase</span><span class="sxs-lookup"><span data-stu-id="0ad9e-132">mySampleDatabase</span></span> | <span data-ttu-id="0ad9e-133">Geçerli veritabanı adları için bkz. [Veritabanı Tanımlayıcıları](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).</span><span class="sxs-lookup"><span data-stu-id="0ad9e-133">For valid database names, see [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).</span></span> | 
   | <span data-ttu-id="0ad9e-134">**Abonelik**</span><span class="sxs-lookup"><span data-stu-id="0ad9e-134">**Subscription**</span></span> | <span data-ttu-id="0ad9e-135">Aboneliğiniz</span><span class="sxs-lookup"><span data-stu-id="0ad9e-135">Your subscription</span></span>  | <span data-ttu-id="0ad9e-136">Abonelikleriniz hakkında daha ayrıntılı bilgi için bkz. [Abonelikler](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="0ad9e-136">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="0ad9e-137">**Kaynak grubu**</span><span class="sxs-lookup"><span data-stu-id="0ad9e-137">**Resource group**</span></span> | <span data-ttu-id="0ad9e-138">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0ad9e-138">myResourceGroup</span></span> | <span data-ttu-id="0ad9e-139">Geçerli kaynak grubu adları için bkz. [Adlandırma kuralları ve kısıtlamalar](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span><span class="sxs-lookup"><span data-stu-id="0ad9e-139">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="0ad9e-140">**Kaynak seçin**</span><span class="sxs-lookup"><span data-stu-id="0ad9e-140">**Select source**</span></span> | <span data-ttu-id="0ad9e-141">Boş veritabanı</span><span class="sxs-lookup"><span data-stu-id="0ad9e-141">Blank database</span></span> | <span data-ttu-id="0ad9e-142">Boş bir veritabanı oluşturulması gerektiğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-142">Specifies that a blank database should be created.</span></span> |

4. <span data-ttu-id="0ad9e-143">Tıklatın **Server** toocreate ve yeni veritabanı için yeni bir sunucu yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-143">Click **Server** toocreate and configure a new server for your new database.</span></span> <span data-ttu-id="0ad9e-144">Merhaba dolgu **yeni sunucu form** bilgisinden hello ile:</span><span class="sxs-lookup"><span data-stu-id="0ad9e-144">Fill out hello **New server form** with hello following information:</span></span> 

   | <span data-ttu-id="0ad9e-145">Ayar</span><span class="sxs-lookup"><span data-stu-id="0ad9e-145">Setting</span></span>       | <span data-ttu-id="0ad9e-146">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="0ad9e-146">Suggested value</span></span> | <span data-ttu-id="0ad9e-147">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0ad9e-147">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="0ad9e-148">**Sunucu adı**</span><span class="sxs-lookup"><span data-stu-id="0ad9e-148">**Server name**</span></span> | <span data-ttu-id="0ad9e-149">Genel olarak benzersiz bir ad</span><span class="sxs-lookup"><span data-stu-id="0ad9e-149">Any globally unique name</span></span> | <span data-ttu-id="0ad9e-150">Geçerli sunucu adları için bkz. [Adlandırma kuralları ve kısıtlamalar](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span><span class="sxs-lookup"><span data-stu-id="0ad9e-150">For valid server names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> | 
   | <span data-ttu-id="0ad9e-151">**Sunucu yöneticisi oturum açma bilgileri**</span><span class="sxs-lookup"><span data-stu-id="0ad9e-151">**Server admin login**</span></span> | <span data-ttu-id="0ad9e-152">Geçerli bir ad</span><span class="sxs-lookup"><span data-stu-id="0ad9e-152">Any valid name</span></span> | <span data-ttu-id="0ad9e-153">Geçerli oturum açma adları için bkz. [Veritabanı Tanımlayıcıları](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).</span><span class="sxs-lookup"><span data-stu-id="0ad9e-153">For valid login names, see [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).</span></span>|
   | <span data-ttu-id="0ad9e-154">**Parola**</span><span class="sxs-lookup"><span data-stu-id="0ad9e-154">**Password**</span></span> | <span data-ttu-id="0ad9e-155">Geçerli bir parola</span><span class="sxs-lookup"><span data-stu-id="0ad9e-155">Any valid password</span></span> | <span data-ttu-id="0ad9e-156">Parolanız en az 8 karakter olmalı ve kategorileri aşağıdaki hello üçünden karakterler içermelidir: büyük harf karakterler, küçük harfler, sayılar ve alfasayısal olmayan karakter.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-156">Your password must have at least 8 characters and must contain characters from three of hello following categories: upper case characters, lower case characters, numbers, and non-alphanumeric characters.</span></span> |
   | <span data-ttu-id="0ad9e-157">**Konum**</span><span class="sxs-lookup"><span data-stu-id="0ad9e-157">**Location**</span></span> | <span data-ttu-id="0ad9e-158">Geçerli bir konum</span><span class="sxs-lookup"><span data-stu-id="0ad9e-158">Any valid location</span></span> | <span data-ttu-id="0ad9e-159">Bölgeler hakkında bilgi için bkz. [Azure Bölgeleri](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="0ad9e-159">For information about regions, see [Azure Regions](https://azure.microsoft.com/regions/).</span></span> |

   ![create database-server](./media//sql-database-design-first-database/create-database-server.png)

5. <span data-ttu-id="0ad9e-161">**Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-161">Click **Select**.</span></span>

6. <span data-ttu-id="0ad9e-162">Tıklatın **fiyatlandırma katmanı** toospecify hello hizmeti katmanını ve performans düzeyini yeni veritabanı.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-162">Click **Pricing tier** toospecify hello service tier and performance level for your new database.</span></span> <span data-ttu-id="0ad9e-163">Bu öğretici için seçin **20 Dtu'lar** ve **250** GB depolama alanı.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-163">For this tutorial, select **20 DTUs** and **250** GB of storage.</span></span>

   ![create database-s1](./media/sql-database-design-first-database/create-empty-database-pricing-tier.png)

7. <span data-ttu-id="0ad9e-165">**Uygula**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-165">Click **Apply**.</span></span>  

8. <span data-ttu-id="0ad9e-166">Seçin bir **harmanlama** hello boş veritabanı (Bu öğretici için kullanım hello varsayılan değer).</span><span class="sxs-lookup"><span data-stu-id="0ad9e-166">Select a **collation** for hello blank database (for this tutorial, use hello default value).</span></span> <span data-ttu-id="0ad9e-167">Harmanlamaları hakkında daha fazla bilgi için bkz: [harmanlamaları](https://docs.microsoft.com/sql/t-sql/statements/collations)</span><span class="sxs-lookup"><span data-stu-id="0ad9e-167">For more information about collations, see [Collations](https://docs.microsoft.com/sql/t-sql/statements/collations)</span></span>

9. <span data-ttu-id="0ad9e-168">Tıklatın **oluşturma** tooprovision hello veritabanı.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-168">Click **Create** tooprovision hello database.</span></span> <span data-ttu-id="0ad9e-169">Bir dakika ve bir yarı toocomplete hakkında alır sağlama.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-169">Provisioning takes about a minute and a half toocomplete.</span></span> 

10. <span data-ttu-id="0ad9e-170">Merhaba araç çubuğundan, **bildirimleri** toomonitor hello dağıtım işlemi.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-170">On hello toolbar, click **Notifications** toomonitor hello deployment process.</span></span>

   ![bildirim](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a><span data-ttu-id="0ad9e-172">Sunucu düzeyinde bir güvenlik duvarı kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0ad9e-172">Create a server-level firewall rule</span></span>

<span data-ttu-id="0ad9e-173">Hello SQL veritabanı hizmetinin hello sunucusu düzeyinde-harici uygulamalar ve Araçlar tooopen hello Güvenlik Duvarı'nı belirli IP adresleri için bir güvenlik duvarı kuralı yapılandırılmadığı sürece toohello sunucu veya hello sunucudaki tüm veritabanları bağlanmasını engelleyen bir güvenlik duvarı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-173">hello SQL Database service creates a firewall at hello server-level that prevents external applications and tools from connecting toohello server or any databases on hello server unless a firewall rule is created tooopen hello firewall for specific IP addresses.</span></span> <span data-ttu-id="0ad9e-174">Bu adımları toocreate izleyin bir [SQL veritabanı sunucu düzeyinde güvenlik duvarı kuralı](sql-database-firewall-configure.md) için istemcinin IP adresi ve IP adresiniz yalnızca hello SQL veritabanı güvenlik duvarı üzerinden dış bağlantısı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-174">Follow these steps toocreate a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your client's IP address and enable external connectivity through hello SQL Database firewall for your IP address only.</span></span> 

> [!NOTE]
> <span data-ttu-id="0ad9e-175">SQL Veritabanı 1433 numaralı bağlantı noktası üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-175">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="0ad9e-176">Bir şirket ağından gelen tooconnect çalışıyorsanız, bağlantı noktası 1433 üzerinden giden trafik, ağınızın güvenlik duvarı tarafından izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-176">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="0ad9e-177">BT departmanınız 1433 numaralı bağlantı noktasını açar sürece bu durumda, tooyour Azure SQL veritabanı sunucusuna bağlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-177">If so, you cannot connect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

1. <span data-ttu-id="0ad9e-178">Merhaba dağıtım tamamlandıktan sonra **SQL veritabanları** hello sol menüsünden ve ardından **mySampleDatabase** hello üzerinde **SQL veritabanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-178">After hello deployment completes, click **SQL databases** from hello left-hand menu and then click **mySampleDatabase** on hello **SQL databases** page.</span></span> <span data-ttu-id="0ad9e-179">Merhaba hello tam olarak gösteren, veritabanı açılır genel bakış sayfasında tam sunucu adını (gibi **mynewserver20170313.database.windows.net**) ve diğer yapılandırmalar için seçenekler sağlar.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-179">hello overview page for your database opens, showing you hello fully qualified server name (such as **mynewserver20170313.database.windows.net**) and provides options for further configuration.</span></span> <span data-ttu-id="0ad9e-180">Daha sonra kullanmak üzere bu tam sunucu adını kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-180">Copy this fully qualified server name for use later.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="0ad9e-181">Sonraki hızlı başlatır, veritabanlarını ve bu tam sunucu adı tooconnect tooyour sunucu gerekir.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-181">You need this fully qualified server name tooconnect tooyour server and its databases in subsequent quick starts.</span></span>
   > 

   ![sunucu adı](./media/sql-database-connect-query-dotnet/server-name.png) 

2. <span data-ttu-id="0ad9e-183">Tıklatın **ayarlayın sunucu Güvenlik Duvarı** hello önceki görüntüde gösterildiği gibi hello araç.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-183">Click **Set server firewall** on hello toolbar as shown in hello previous image.</span></span> <span data-ttu-id="0ad9e-184">Merhaba **Güvenlik Duvarı ayarları** hello SQL veritabanı sunucusu sayfasını açar.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-184">hello **Firewall settings** page for hello SQL Database server opens.</span></span> 

   ![sunucu güvenlik duvarı kuralı](./media/sql-database-get-started-portal/server-firewall-rule.png) 


3. <span data-ttu-id="0ad9e-186">Tıklatın **istemci IP'si Ekle** hello araç tooadd üzerinde geçerli IP adresi tooa yeni güvenlik duvarı kuralı.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-186">Click **Add client IP** on hello toolbar tooadd your current IP address tooa new firewall rule.</span></span> <span data-ttu-id="0ad9e-187">Güvenlik duvarı kuralı, 1433 numaralı bağlantı noktasını tek bir IP adresi veya bir IP adresi aralığı için açabilir.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-187">A firewall rule can open port 1433 for a single IP address or a range of IP addresses.</span></span>

4. <span data-ttu-id="0ad9e-188">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-188">Click **Save**.</span></span> <span data-ttu-id="0ad9e-189">Geçerli IP adresiniz hello mantıksal sunucuda bağlantı noktası 1433'ü açmak için bir sunucu düzeyinde güvenlik duvarı kuralı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-189">A server-level firewall rule is created for your current IP address opening port 1433 on hello logical server.</span></span>

   ![sunucu güvenlik duvarı kuralı ayarla](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. <span data-ttu-id="0ad9e-191">Tıklatın **Tamam** ve hello kapatın **Güvenlik Duvarı ayarları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-191">Click **OK** and then close hello **Firewall settings** page.</span></span>

<span data-ttu-id="0ad9e-192">Şimdi toohello SQL veritabanı sunucusunu ve veritabanlarını SQL Server Management Studio veya bu IP adresinden daha önce oluşturulmuş hello server yönetici hesabı kullanarak tercih ettiğiniz başka bir araç kullanarak bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-192">You can now connect toohello SQL Database server and its databases using SQL Server Management Studio or another tool of your choice from this IP address using hello server admin account created previously.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0ad9e-193">Varsayılan olarak, tüm Azure hizmetlerini hello SQL veritabanı güvenlik duvarı üzerinden erişim etkin.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-193">By default, access through hello SQL Database firewall is enabled for all Azure services.</span></span> <span data-ttu-id="0ad9e-194">Tıklatın **OFF** tüm Azure Hizmetleri için bu sayfayı toodisable üzerinde.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-194">Click **OFF** on this page toodisable for all Azure services.</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="0ad9e-195">SQL Server bağlantı bilgileri</span><span class="sxs-lookup"><span data-stu-id="0ad9e-195">SQL server connection information</span></span>

<span data-ttu-id="0ad9e-196">Azure SQL veritabanı sunucunuz için Hello tam sunucu adını hello Azure portal alın.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-196">Get hello fully qualified server name for your Azure SQL Database server in hello Azure portal.</span></span> <span data-ttu-id="0ad9e-197">SQL Server Management Studio'yu kullanarak hello tam adı tooconnect tooyour sunucusu kullanın.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-197">You use hello fully qualified server name tooconnect tooyour server using SQL Server Management Studio.</span></span>

1. <span data-ttu-id="0ad9e-198">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0ad9e-198">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0ad9e-199">Seçin **SQL veritabanları** hello sol taraftaki menüden veritabanınızda hello tıklatıp **SQL veritabanları** sayfası.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-199">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="0ad9e-200">Merhaba, **Essentials** Merhaba, veritabanı için Azure portal sayfası bölmesinde bulun ve ardından hello kopyalayın **sunucu adı**.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-200">In hello **Essentials** pane in hello Azure portal page for your database, locate and then copy hello **Server name**.</span></span>

   ![bağlantı bilgileri](./media/sql-database-connect-query-dotnet/server-name.png)

## <a name="connect-toohello-database-with-ssms"></a><span data-ttu-id="0ad9e-202">SSMS ile toohello veritabanına bağlanın</span><span class="sxs-lookup"><span data-stu-id="0ad9e-202">Connect toohello database with SSMS</span></span>

<span data-ttu-id="0ad9e-203">Kullanım [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) tooestablish bağlantı tooyour Azure SQL veritabanı sunucusu.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-203">Use [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) tooestablish a connection tooyour Azure SQL Database server.</span></span>

1. <span data-ttu-id="0ad9e-204">SQL Server Management Studio’yu açın.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-204">Open SQL Server Management Studio.</span></span>

2. <span data-ttu-id="0ad9e-205">Merhaba, **tooServer bağlanmak** iletişim kutusunda, aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="0ad9e-205">In hello **Connect tooServer** dialog box, enter hello following information:</span></span>

   | <span data-ttu-id="0ad9e-206">Ayar</span><span class="sxs-lookup"><span data-stu-id="0ad9e-206">Setting</span></span>       | <span data-ttu-id="0ad9e-207">Önerilen değer</span><span class="sxs-lookup"><span data-stu-id="0ad9e-207">Suggested value</span></span> | <span data-ttu-id="0ad9e-208">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0ad9e-208">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="0ad9e-209">Sunucu türü</span><span class="sxs-lookup"><span data-stu-id="0ad9e-209">Server type</span></span> | <span data-ttu-id="0ad9e-210">Veritabanı altyapısı</span><span class="sxs-lookup"><span data-stu-id="0ad9e-210">Database engine</span></span> | <span data-ttu-id="0ad9e-211">Bu değer gereklidir</span><span class="sxs-lookup"><span data-stu-id="0ad9e-211">This value is required</span></span> |
   | <span data-ttu-id="0ad9e-212">Sunucu adı</span><span class="sxs-lookup"><span data-stu-id="0ad9e-212">Server name</span></span> | <span data-ttu-id="0ad9e-213">Merhaba tam sunucu adı</span><span class="sxs-lookup"><span data-stu-id="0ad9e-213">hello fully qualified server name</span></span> | <span data-ttu-id="0ad9e-214">Merhaba adı şöyle olmalıdır: **mynewserver20170313.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-214">hello name should be something like this: **mynewserver20170313.database.windows.net**.</span></span> |
   | <span data-ttu-id="0ad9e-215">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="0ad9e-215">Authentication</span></span> | <span data-ttu-id="0ad9e-216">SQL Server Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="0ad9e-216">SQL Server Authentication</span></span> | <span data-ttu-id="0ad9e-217">SQL kimlik doğrulaması biz Bu öğreticide yapılandırdığınız hello yalnızca kimlik doğrulaması türüdür.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-217">SQL Authentication is hello only authentication type that we have configured in this tutorial.</span></span> |
   | <span data-ttu-id="0ad9e-218">Oturum Aç</span><span class="sxs-lookup"><span data-stu-id="0ad9e-218">Login</span></span> | <span data-ttu-id="0ad9e-219">Merhaba server yönetici hesabı</span><span class="sxs-lookup"><span data-stu-id="0ad9e-219">hello server admin account</span></span> | <span data-ttu-id="0ad9e-220">Bu hello sunucu oluşturduğunuzda, belirttiğiniz hello hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-220">This is hello account that you specified when you created hello server.</span></span> |
   | <span data-ttu-id="0ad9e-221">Parola</span><span class="sxs-lookup"><span data-stu-id="0ad9e-221">Password</span></span> | <span data-ttu-id="0ad9e-222">Sunucu yönetici hesabınız için Hello parola</span><span class="sxs-lookup"><span data-stu-id="0ad9e-222">hello password for your server admin account</span></span> | <span data-ttu-id="0ad9e-223">Bu hello sunucu oluşturduğunuzda, belirttiğiniz hello paroladır.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-223">This is hello password that you specified when you created hello server.</span></span> |

   ![tooserver Bağlan](./media/sql-database-connect-query-ssms/connect.png)

3. <span data-ttu-id="0ad9e-225">Tıklatın **seçenekleri** hello içinde **tooserver bağlanmak** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-225">Click **Options** in hello **Connect tooserver** dialog box.</span></span> <span data-ttu-id="0ad9e-226">Merhaba, **toodatabase bağlanmak** bölümünde, girin **mySampleDatabase** tooconnect toothis veritabanı.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-226">In hello **Connect toodatabase** section, enter **mySampleDatabase** tooconnect toothis database.</span></span>

   ![sunucuda toodb Bağlan](./media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. <span data-ttu-id="0ad9e-228">**Bağlan**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-228">Click **Connect**.</span></span> <span data-ttu-id="0ad9e-229">SSMS Hello Nesne Gezgini penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-229">hello Object Explorer window opens in SSMS.</span></span> 

5. <span data-ttu-id="0ad9e-230">Nesne Gezgini'nde genişletin **veritabanları** genişletin ve ardından **mySampleDatabase** hello örnek veritabanındaki tooview hello nesneleri.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-230">In Object Explorer, expand **Databases** and then expand **mySampleDatabase** tooview hello objects in hello sample database.</span></span>

   ![Veritabanı nesneleri](./media/sql-database-connect-query-ssms/connected.png)  

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="0ad9e-232">Merhaba veritabanında tabloları oluşturma</span><span class="sxs-lookup"><span data-stu-id="0ad9e-232">Create tables in hello database</span></span> 

<span data-ttu-id="0ad9e-233">Bir öğrenci yönetimi sistemi kullanarak üniversiteler için model dört tablolar ile bir veritabanı şeması oluşturma [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference):</span><span class="sxs-lookup"><span data-stu-id="0ad9e-233">Create a database schema with four tables that model a student management system for universities using [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference):</span></span>

- <span data-ttu-id="0ad9e-234">Kişi</span><span class="sxs-lookup"><span data-stu-id="0ad9e-234">Person</span></span>
- <span data-ttu-id="0ad9e-235">İndirmelere</span><span class="sxs-lookup"><span data-stu-id="0ad9e-235">Course</span></span>
- <span data-ttu-id="0ad9e-236">Öğrenci</span><span class="sxs-lookup"><span data-stu-id="0ad9e-236">Student</span></span>
- <span data-ttu-id="0ad9e-237">Bu model bir öğrenci yönetim sistemi üniversiteler için kredi</span><span class="sxs-lookup"><span data-stu-id="0ad9e-237">Credit that model a student management system for universities</span></span>

<span data-ttu-id="0ad9e-238">Merhaba Aşağıdaki diyagramda nasıl bu tablolar diğer ilgili tooeach gösterir.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-238">hello following diagram shows how these tables are related tooeach other.</span></span> <span data-ttu-id="0ad9e-239">Bu tablolar bazıları diğer tablolardaki sütunlara başvuru.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-239">Some of these tables reference columns in other tables.</span></span> <span data-ttu-id="0ad9e-240">Örneğin, hello hello Öğrenci tabloya başvuruyorsa **PersonId** hello sütunu **kişi** tablo.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-240">For example, hello Student table references hello **PersonId** column of hello **Person** table.</span></span> <span data-ttu-id="0ad9e-241">Olay İncelemesi hello diyagramı toounderstand nasıl hello tabloları Bu öğreticide ilgili tooone olan başka bir.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-241">Study hello diagram toounderstand how hello tables in this tutorial are related tooone another.</span></span> <span data-ttu-id="0ad9e-242">Nasıl ilişkin ayrıntılı bir bakış için toocreate etkili veritabanı tabloları, bkz: [etkili veritabanı tabloları oluşturma](https://msdn.microsoft.com/library/cc505842.aspx).</span><span class="sxs-lookup"><span data-stu-id="0ad9e-242">For an in-depth look at how toocreate effective database tables, see [Create effective database tables](https://msdn.microsoft.com/library/cc505842.aspx).</span></span> <span data-ttu-id="0ad9e-243">Veri türleri seçme hakkında daha fazla bilgi için bkz: [veri türleri](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="0ad9e-243">For information about choosing data types, see [Data types](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql).</span></span>

> [!NOTE]
> <span data-ttu-id="0ad9e-244">Merhaba de kullanabilirsiniz [Tablo Tasarımcısı'nda SQL Server Management Studio](https://msdn.microsoft.com/library/hh272695.aspx) toocreate ve tabloları tasarlayın.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-244">You can also use hello [table designer in SQL Server Management Studio](https://msdn.microsoft.com/library/hh272695.aspx) toocreate and design your tables.</span></span> 

![Tablo ilişkileri](./media/sql-database-design-first-database/tutorial-database-tables.png)

1. <span data-ttu-id="0ad9e-246">Nesne Gezgini’nde **mySampleDatabase** öğesine sağ tıklayıp **Yeni Sorgu**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-246">In Object Explorer, right-click **mySampleDatabase** and click **New Query**.</span></span> <span data-ttu-id="0ad9e-247">Boş sorgu penceresi bağlı tooyour veritabanını başka bir deyişle açar.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-247">A blank query window opens that is connected tooyour database.</span></span>

2. <span data-ttu-id="0ad9e-248">Merhaba sorgu penceresinde, veritabanınızda query toocreate dört tablonun aşağıdaki hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="0ad9e-248">In hello query window, execute hello following query toocreate four tables in your database:</span></span> 

   ```sql 
   -- Create Person table

   CREATE TABLE Person
   (
   PersonId   INT IDENTITY PRIMARY KEY,
   FirstName   NVARCHAR(128) NOT NULL,
   MiddelInitial NVARCHAR(10),
   LastName   NVARCHAR(128) NOT NULL,
   DateOfBirth   DATE NOT NULL
   )
   
   -- Create Student table
 
   CREATE TABLE Student
   (
   StudentId INT IDENTITY PRIMARY KEY,
   PersonId  INT REFERENCES Person (PersonId),
   Email   NVARCHAR(256)
   )
   
   -- Create Course table
 
   CREATE TABLE Course
   (
   CourseId  INT IDENTITY PRIMARY KEY,
   Name   NVARCHAR(50) NOT NULL,
   Teacher   NVARCHAR(256) NOT NULL
   ) 

   -- Create Credit table
 
   CREATE TABLE Credit
   (
   StudentId   INT REFERENCES Student (StudentId),
   CourseId   INT REFERENCES Course (CourseId),
   Grade   DECIMAL(5,2) CHECK (Grade <= 100.00),
   Attempt   TINYINT,
   CONSTRAINT  [UQ_studentgrades] UNIQUE CLUSTERED
   (
   StudentId, CourseId, Grade, Attempt
   )
   )
   ```

   ![Tabloları oluşturma](./media/sql-database-design-first-database/create-tables.png)

3. <span data-ttu-id="0ad9e-250">Oluşturduğunuz hello SQL Server Management Studio Nesne Gezgini toosee hello tabloları Hello 'tablo' düğümünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-250">Expand hello 'tables' node in hello SQL Server Management Studio Object explorer toosee hello tables you created.</span></span>

   ![SSMS tablolarının oluşturulması](./media/sql-database-design-first-database/ssms-tables-created.png)

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="0ad9e-252">Merhaba tablolara veri yükleme</span><span class="sxs-lookup"><span data-stu-id="0ad9e-252">Load data into hello tables</span></span>

1. <span data-ttu-id="0ad9e-253">Adlı bir klasör oluşturun **SampleTableData** indirmeler klasörüne toostore örnek verilerinizde veritabanınız için.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-253">Create a folder called **SampleTableData** in your Downloads folder toostore sample data for your database.</span></span> 

2. <span data-ttu-id="0ad9e-254">Sağ hello aşağıdaki bağlar ve bunları hello kaydetmek **SampleTableData** klasör.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-254">Right-click hello following links and save them into hello **SampleTableData** folder.</span></span> 

   - [<span data-ttu-id="0ad9e-255">SampleCourseData</span><span class="sxs-lookup"><span data-stu-id="0ad9e-255">SampleCourseData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCourseData)
   - [<span data-ttu-id="0ad9e-256">SamplePersonData</span><span class="sxs-lookup"><span data-stu-id="0ad9e-256">SamplePersonData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SamplePersonData)
   - [<span data-ttu-id="0ad9e-257">SampleStudentData</span><span class="sxs-lookup"><span data-stu-id="0ad9e-257">SampleStudentData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleStudentData)
   - [<span data-ttu-id="0ad9e-258">SampleCreditData</span><span class="sxs-lookup"><span data-stu-id="0ad9e-258">SampleCreditData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCreditData)

3. <span data-ttu-id="0ad9e-259">Bir komut istemi penceresi açın ve toohello SampleTableData klasörüne gidin.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-259">Open a command prompt window and navigate toohello SampleTableData folder.</span></span>

4. <span data-ttu-id="0ad9e-260">Merhaba değerlerini değiştirme hello tablolara komutları tooinsert örnek verileri aşağıdaki hello yürütme **ServerName**, **DatabaseName**, **kullanıcıadı**ve **Parola** ortamınız için hello değerlere sahip.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-260">Execute hello following commands tooinsert sample data into hello tables replacing hello values for **ServerName**, **DatabaseName**, **UserName**, and **Password** with hello values for your environment.</span></span>
  
   ```bcp
   bcp Course in SampleCourseData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Person in SamplePersonData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Student in SampleStudentData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Credit in SampleCreditData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   ```

<span data-ttu-id="0ad9e-261">Ayrıca, daha önce oluşturduğunuz hello tablolara şimdi örnek veri yüklemiş olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-261">You have now loaded sample data into hello tables you created earlier.</span></span>

## <a name="query-data"></a><span data-ttu-id="0ad9e-262">Verileri sorgulama</span><span class="sxs-lookup"><span data-stu-id="0ad9e-262">Query data</span></span>

<span data-ttu-id="0ad9e-263">Sorguları tooretrieve bilgisinden hello veritabanı tablolarından hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-263">Execute hello following queries tooretrieve information from hello database tables.</span></span> <span data-ttu-id="0ad9e-264">Bkz: [SQL sorguları yazma](https://technet.microsoft.com/library/bb264565.aspx) toolearn SQL sorguları yazma hakkında daha fazla.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-264">See [Writing SQL Queries](https://technet.microsoft.com/library/bb264565.aspx) toolearn more about writing SQL queries.</span></span> <span data-ttu-id="0ad9e-265">Tüm hello Öğrenciler öğrettin tüm dört tablonun toofind tarafından ' Dominick kendi sınıfında 75 %'den daha yüksek bir düzeyde olan Pope' Hello ilk sorgu birleştirir.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-265">hello first query joins all four tables toofind all hello students taught by 'Dominick Pope' who have a grade higher than 75% in his class.</span></span> <span data-ttu-id="0ad9e-266">Merhaba ikinci sorgu dört tablonun tamamını birleştirir ve 'Barış Coleman' herhangi bir zamanda kaydolduğu tüm kursları bulur.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-266">hello second query joins all four tables and finds all courses in which 'Noe Coleman' has ever enrolled.</span></span>

1. <span data-ttu-id="0ad9e-267">Bir SQL Server Management Studio sorgu penceresinde hello sorgu aşağıdaki yürütün:</span><span class="sxs-lookup"><span data-stu-id="0ad9e-267">In a SQL Server Management Studio query window, execute hello following query:</span></span>

   ```sql 
   -- Find hello students taught by Dominick Pope who have a grade higher than 75%

   SELECT  person.FirstName,
   person.LastName,
   course.Name,
   credit.Grade
   FROM  Person AS person
   INNER JOIN Student AS student ON person.PersonId = student.PersonId
   INNER JOIN Credit AS credit ON student.StudentId = credit.StudentId
   INNER JOIN Course AS course ON credit.CourseId = course.courseId
   WHERE course.Teacher = 'Dominick Pope' 
   AND Grade > 75
   ```

2. <span data-ttu-id="0ad9e-268">Bir SQL Server Management Studio sorgu penceresinde, sorguyu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="0ad9e-268">In a SQL Server Management Studio query window, execute following query:</span></span>

   ```sql
   -- Find all hello courses in which Noe Coleman has ever enrolled

   SELECT  course.Name,
   course.Teacher,
   credit.Grade
   FROM  Course AS course
   INNER JOIN Credit AS credit ON credit.CourseId = course.CourseId
   INNER JOIN Student AS student ON student.StudentId = credit.StudentId
   INNER JOIN Person AS person ON person.PersonId = student.PersonId
   WHERE person.FirstName = 'Noe'
   AND person.LastName = 'Coleman'
   ```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="0ad9e-269">Zaman içinde veritabanı tooa önceki bir noktaya geri</span><span class="sxs-lookup"><span data-stu-id="0ad9e-269">Restore a database tooa previous point in time</span></span>

<span data-ttu-id="0ad9e-270">Yanlışlıkla bir tabloyu sildiniz düşünün.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-270">Imagine you have accidentally deleted a table.</span></span> <span data-ttu-id="0ad9e-271">Bu, kolayca kurtaramazsınız şeydir.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-271">This is something you cannot easily recover from.</span></span> <span data-ttu-id="0ad9e-272">Azure SQL veritabanı toogo geri tooany noktası hello zamanda son too35 günleri sağlar ve bu noktaya zaman tooa yeni veritabanı geri yükleme.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-272">Azure SQL Database allows you toogo back tooany point in time in hello last up too35 days and restore this point in time tooa new database.</span></span> <span data-ttu-id="0ad9e-273">Bu veritabanı toorecover silinmiş verilerinizi gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-273">You can you this database toorecover your deleted data.</span></span> <span data-ttu-id="0ad9e-274">Merhaba tabloları eklenmeden önce hello aşağıdaki adımları hello örnek veritabanı tooa geri yükleme noktası.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-274">hello following steps restore hello sample database tooa point before hello tables were added.</span></span>

1. <span data-ttu-id="0ad9e-275">Merhaba SQL veritabanı sayfasında veritabanınız için tıklayın **geri** hello araç.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-275">On hello SQL Database page for your database, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="0ad9e-276">Merhaba **geri** sayfası açılır.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-276">hello **Restore** page opens.</span></span>

   ![Geri yükleme](./media/sql-database-design-first-database/restore.png)

2. <span data-ttu-id="0ad9e-278">Merhaba dolgu **geri** form hello gerekli bilgilerle:</span><span class="sxs-lookup"><span data-stu-id="0ad9e-278">Fill out hello **Restore** form with hello required information:</span></span>
    * <span data-ttu-id="0ad9e-279">Veritabanı adı: Bir veritabanı adı sağlayın</span><span class="sxs-lookup"><span data-stu-id="0ad9e-279">Database name: Provide a database name</span></span> 
    * <span data-ttu-id="0ad9e-280">Noktası zamanında: Select hello **noktası zaman** hello geri yükleme formundaki sekmesi</span><span class="sxs-lookup"><span data-stu-id="0ad9e-280">Point-in-time: Select hello **Point-in-time** tab on hello Restore form</span></span> 
    * <span data-ttu-id="0ad9e-281">Geri yükleme noktası: hello veritabanı değiştirilmeden önce oluşan bir süre seçin</span><span class="sxs-lookup"><span data-stu-id="0ad9e-281">Restore point: Select a time that occurs before hello database was changed</span></span>
    * <span data-ttu-id="0ad9e-282">Hedef sunucu: bir veritabanı geri yüklenirken bu değeri değiştirilemiyor</span><span class="sxs-lookup"><span data-stu-id="0ad9e-282">Target server: You cannot change this value when restoring a database</span></span> 
    * <span data-ttu-id="0ad9e-283">Esnek veritabanı havuzu: seçin **yok**</span><span class="sxs-lookup"><span data-stu-id="0ad9e-283">Elastic database pool: Select **None**</span></span>  
    * <span data-ttu-id="0ad9e-284">Fiyatlandırma katmanı: seçin **20 Dtu'lar** ve **250 GB** depolama.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-284">Pricing tier: Select **20 DTUs** and **250 GB** of storage.</span></span>

   ![geri yükleme noktası](./media/sql-database-design-first-database/restore-point.png)

3. <span data-ttu-id="0ad9e-286">Tıklatın **Tamam** toorestore hello veritabanı çok[tooa noktası zaman içinde geri](sql-database-recovery-using-backups.md#point-in-time-restore) hello tabloları eklenmeden önce.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-286">Click **OK** toorestore hello database too[restore tooa point in time](sql-database-recovery-using-backups.md#point-in-time-restore) before hello tables were added.</span></span> <span data-ttu-id="0ad9e-287">Veritabanı tooa farklı bir noktaya geri yükleme zamanında, hello yinelenen bir veritabanı oluşturur hello özgün veritabanı hello noktaya itibariyle aynı sunucuya belirttiğiniz hello saklama süresi içinde olduğu sürece, [hizmet katmanı](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="0ad9e-287">Restoring a database tooa different point in time creates a duplicate database in hello same server as hello original database as of hello point in time you specify, as long as it is within hello retention period for your [service tier](sql-database-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ad9e-288">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="0ad9e-288">Next Steps</span></span> 
<span data-ttu-id="0ad9e-289">Bu öğreticide temel veritabanı görevlerini gibi bir veritabanı ve tablo oluşturma hakkında bilgi edindiniz, yükleme ve verileri sorgulamak ve zaman içinde hello veritabanı tooa önceki noktası geri.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-289">In this tutorial, you learned basic database tasks such as create a database and tables, load and query data, and restore hello database tooa previous point in time.</span></span> <span data-ttu-id="0ad9e-290">Şunları öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="0ad9e-290">You learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="0ad9e-291">Veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0ad9e-291">Create a database</span></span>
> * <span data-ttu-id="0ad9e-292">Bir güvenlik duvarı kuralı ayarlamak</span><span class="sxs-lookup"><span data-stu-id="0ad9e-292">Set up a firewall rule</span></span>
> * <span data-ttu-id="0ad9e-293">Toohello veritabanı ile bağlantı [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS)</span><span class="sxs-lookup"><span data-stu-id="0ad9e-293">Connect toohello database with [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS)</span></span>
> * <span data-ttu-id="0ad9e-294">Tabloları oluşturma</span><span class="sxs-lookup"><span data-stu-id="0ad9e-294">Create tables</span></span>
> * <span data-ttu-id="0ad9e-295">Yığın veri yükleme</span><span class="sxs-lookup"><span data-stu-id="0ad9e-295">Bulk load data</span></span>
> * <span data-ttu-id="0ad9e-296">Bu verileri Sorgulama</span><span class="sxs-lookup"><span data-stu-id="0ad9e-296">Query that data</span></span>
> * <span data-ttu-id="0ad9e-297">SQL veritabanı kullanarak zamanında Hello veritabanı tooa önceki noktası geri [geri yükleme noktası](sql-database-recovery-using-backups.md#point-in-time-restore) özellikleri</span><span class="sxs-lookup"><span data-stu-id="0ad9e-297">Restore hello database tooa previous point in time using SQL Database [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore) capabilities</span></span>

<span data-ttu-id="0ad9e-298">Visual Studio ve C# kullanarak veritabanı tasarlama hakkında toohello sonraki öğretici toolearn ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="0ad9e-298">Advance toohello next tutorial toolearn about designing a database using Visual Studio and C#.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="0ad9e-299">Bir Azure SQL veritabanı tasarlama ve C# ve ADO.NET bağlantı</span><span class="sxs-lookup"><span data-stu-id="0ad9e-299">Design an Azure SQL database and connect with C# and ADO.NET</span></span>](sql-database-design-first-database-csharp.md)
