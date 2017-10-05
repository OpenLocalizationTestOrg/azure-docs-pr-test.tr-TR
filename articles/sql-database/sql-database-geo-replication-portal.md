---
title: "Azure portal: SQL Database coğrafi çoğaltma | Microsoft Docs"
description: "Azure portalı ve başlatma yük devretme Azure SQL veritabanı için coğrafi çoğaltma yapılandırma"
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d0b29822-714f-4633-a5ab-fb1a09d43ced
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/06/2016
ms.author: carlrab
ms.openlocfilehash: db90fad2fe397f0c8466db6bdc1bd8c8d1cf8f15
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-the-azure-portal-and-initiate-failover"></a><span data-ttu-id="a334a-103">Aktif coğrafi çoğaltma Azure portal ve başlatma yük devretme Azure SQL veritabanı için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a334a-103">Configure active geo-replication for Azure SQL Database in the Azure portal and initiate failover</span></span>

<span data-ttu-id="a334a-104">Bu makalede, SQL veritabanında için etkin coğrafi çoğaltma yapılandırma gösterilmektedir [Azure portal](http://portal.azure.com) ve yük devretme başlatın.</span><span class="sxs-lookup"><span data-stu-id="a334a-104">This article shows you how to configure active geo-replication for SQL Database in the [Azure portal](http://portal.azure.com) and to initiate failover.</span></span>

<span data-ttu-id="a334a-105">Azure portal ile yük devretme başlatmak için bkz: [planlanmış veya planlanmamış bir yük devretme, Azure portalı ile Azure SQL veritabanı için başlatmak](sql-database-geo-replication-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a334a-105">To initiate failover with the Azure portal, see [Initiate a planned or unplanned failover for Azure SQL Database with the Azure portal](sql-database-geo-replication-portal.md).</span></span>

<span data-ttu-id="a334a-106">Aktif coğrafi çoğaltma Azure portalını kullanarak yapılandırmak için aşağıdaki kaynak gerekir:</span><span class="sxs-lookup"><span data-stu-id="a334a-106">To configure active geo-replication by using the Azure portal, you need the following resource:</span></span>

* <span data-ttu-id="a334a-107">Azure SQL veritabanını: farklı bir coğrafi bölgeye çoğaltmak istediğiniz birincil veritabanı.</span><span class="sxs-lookup"><span data-stu-id="a334a-107">An Azure SQL database: The primary database that you want to replicate to a different geographical region.</span></span>

> [!Note]
<span data-ttu-id="a334a-108">Aktif coğrafi çoğaltma veritabanları aynı abonelikte arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a334a-108">Active geo-replication must be between databases in the same subscription.</span></span>

## <a name="add-a-secondary-database"></a><span data-ttu-id="a334a-109">İkincil bir veritabanı ekleyin</span><span class="sxs-lookup"><span data-stu-id="a334a-109">Add a secondary database</span></span>
<span data-ttu-id="a334a-110">Aşağıdaki adımlar bir coğrafi çoğaltma ortaklığı yeni ikincil bir veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a334a-110">The following steps create a new secondary database in a geo-replication partnership.</span></span>  

<span data-ttu-id="a334a-111">İkincil bir veritabanı eklemek için abonelik sahibi veya ortak sahibi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a334a-111">To add a secondary database, you must be the subscription owner or co-owner.</span></span>

<span data-ttu-id="a334a-112">İkincil veritabanını birincil veritabanı ile aynı ada ve varsayılan olarak, aynı hizmet düzeyinde sahiptir.</span><span class="sxs-lookup"><span data-stu-id="a334a-112">The secondary database has the same name as the primary database and has, by default, the same service level.</span></span> <span data-ttu-id="a334a-113">İkincil veritabanı tek bir veritabanı veya veritabanı esnek havuzdaki olabilir.</span><span class="sxs-lookup"><span data-stu-id="a334a-113">The secondary database can be a single database or a database in an elastic pool.</span></span> <span data-ttu-id="a334a-114">Daha fazla bilgi için bkz: [hizmet katmanları](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="a334a-114">For more information, see [Service tiers](sql-database-service-tiers.md).</span></span>
<span data-ttu-id="a334a-115">İkincil oluşturulan ve dağıtılan sonra verileri yeni ikincil veritabanına birincil veritabanından çoğaltmaya başlar.</span><span class="sxs-lookup"><span data-stu-id="a334a-115">After the secondary is created and seeded, data begins replicating from the primary database to the new secondary database.</span></span>

> [!NOTE]
> <span data-ttu-id="a334a-116">(Örneğin, bir önceki coğrafi çoğaltma ilişkisi sonlandırma sonucunda) ortak veritabanı zaten var. komutu başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="a334a-116">If the partner database already exists (for example, as a result of terminating a previous geo-replication relationship) the command fails.</span></span>
> 

1. <span data-ttu-id="a334a-117">İçinde [Azure portal](http://portal.azure.com), coğrafi çoğaltma için ayarlamak istediğiniz veritabanına gözatın.</span><span class="sxs-lookup"><span data-stu-id="a334a-117">In the [Azure portal](http://portal.azure.com), browse to the database that you want to set up for geo-replication.</span></span>
2. <span data-ttu-id="a334a-118">SQL veritabanı sayfasında seçin **coğrafi çoğaltma**ve ardından ikincil veritabanını oluşturmak için bölge seçin.</span><span class="sxs-lookup"><span data-stu-id="a334a-118">On the SQL database page, select **geo-replication**, and then select the region to create the secondary database.</span></span> <span data-ttu-id="a334a-119">Birincil veritabanını barındıran bölgesi dışında herhangi bir bölgeyi seçebilirsiniz, ancak öneririz [eşleştirilmiş bölge](../best-practices-availability-paired-regions.md).</span><span class="sxs-lookup"><span data-stu-id="a334a-119">You can select any region other than the region hosting the primary database, but we recommend the [paired region](../best-practices-availability-paired-regions.md).</span></span>
   
    ![Coğrafi çoğaltmayı yapılandırma](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. <span data-ttu-id="a334a-121">Seçin veya sunucuyu ve fiyatlandırma katmanı ikincil veritabanı için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="a334a-121">Select or configure the server and pricing tier for the secondary database.</span></span>
   
    ![İkincil yapılandırın](./media/sql-database-geo-replication-portal/create-secondary.png)
4. <span data-ttu-id="a334a-123">İsteğe bağlı olarak, ikincil bir veritabanını bir esnek havuz ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a334a-123">Optionally, you can add a secondary database to an elastic pool.</span></span> <span data-ttu-id="a334a-124">Bir havuzda ikincil veritabanını oluşturmak için tıklatın **esnek havuz** ve hedef sunucudaki bir havuz seçin.</span><span class="sxs-lookup"><span data-stu-id="a334a-124">To create the secondary database in a pool, click **elastic pool** and select a pool on the target server.</span></span> <span data-ttu-id="a334a-125">Bir havuzu hedef sunucuda zaten mevcut olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a334a-125">A pool must already exist on the target server.</span></span> <span data-ttu-id="a334a-126">Bu iş akışı bir havuzu oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="a334a-126">This workflow does not create a pool.</span></span>
5. <span data-ttu-id="a334a-127">Tıklatın **oluşturma** ikincil kopya eklemek için.</span><span class="sxs-lookup"><span data-stu-id="a334a-127">Click **Create** to add the secondary.</span></span>
6. <span data-ttu-id="a334a-128">İkincil veritabanı oluşturulur ve dengeli dağıtım işlemi başlar.</span><span class="sxs-lookup"><span data-stu-id="a334a-128">The secondary database is created and the seeding process begins.</span></span>
   
    ![İkincil yapılandırın](./media/sql-database-geo-replication-portal/seeding0.png)
7. <span data-ttu-id="a334a-130">Dengeli dağıtım işlemi tamamlandığında, ikincil veritabanı durumunu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="a334a-130">When the seeding process is complete, the secondary database displays its status.</span></span>
   
    ![Tam üretme](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a><span data-ttu-id="a334a-132">Bir yük devretme başlatın</span><span class="sxs-lookup"><span data-stu-id="a334a-132">Initiate a failover</span></span>

<span data-ttu-id="a334a-133">İkincil veritabanının birincil olmasını değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="a334a-133">The secondary database can be switched to become the primary.</span></span>  

1. <span data-ttu-id="a334a-134">İçinde [Azure portal](http://portal.azure.com), coğrafi çoğaltma ortaklığı birincil veritabanında konumuna göz atın.</span><span class="sxs-lookup"><span data-stu-id="a334a-134">In the [Azure portal](http://portal.azure.com), browse to the primary database in the geo-replication partnership.</span></span>
2. <span data-ttu-id="a334a-135">SQL veritabanı dikey seçin **tüm ayarları** > **coğrafi çoğaltma**.</span><span class="sxs-lookup"><span data-stu-id="a334a-135">On the SQL Database blade, select **All settings** > **geo-replication**.</span></span>
3. <span data-ttu-id="a334a-136">İçinde **İKİNCİLLER** listesinde, yeni birincil hale tıklatıp istediğiniz veritabanını seçin **yük devretme**.</span><span class="sxs-lookup"><span data-stu-id="a334a-136">In the **SECONDARIES** list, select the database you want to become the new primary and click **Failover**.</span></span>
   
    ![Yük devretme](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. <span data-ttu-id="a334a-138">Tıklatın **Evet** yük devretmeyi başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="a334a-138">Click **Yes** to begin the failover.</span></span>

<span data-ttu-id="a334a-139">Komut, ikincil veritabanı birincil rolde hemen geçirir.</span><span class="sxs-lookup"><span data-stu-id="a334a-139">The command immediately switches the secondary database into the primary role.</span></span> 

<span data-ttu-id="a334a-140">Rolleri geçiş sırasında hangi sırasında her iki veritabanı (0-25 saniye terabayt) kullanılamaz kısa bir süre yoktur.</span><span class="sxs-lookup"><span data-stu-id="a334a-140">There is a short period during which both databases are unavailable (on the order of 0 to 25 seconds) while the roles are switched.</span></span> <span data-ttu-id="a334a-141">Birincil veritabanında birden fazla ikincil veritabanı varsa, komut yeni birincil bağlanmak için diğer ikincil kopya otomatik olarak yeniden yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="a334a-141">If the primary database has multiple secondary databases, the command automatically reconfigures the other secondaries to connect to the new primary.</span></span> <span data-ttu-id="a334a-142">Tüm işlemi normal koşullarda tamamlanması bir dakikadan az zamanınızı.</span><span class="sxs-lookup"><span data-stu-id="a334a-142">The entire operation should take less than a minute to complete under normal circumstances.</span></span> 

> [!NOTE]
> <span data-ttu-id="a334a-143">Bu komut, bir kesinti durumunda veritabanının Hızlı Kurtarma için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a334a-143">This command is designed for quick recovery of the database in case of an outage.</span></span> <span data-ttu-id="a334a-144">Yük devretme (yük devretme zorlanır) veri eşitleme tetikler.</span><span class="sxs-lookup"><span data-stu-id="a334a-144">It triggers failover without data synchronization (forced failover).</span></span>  <span data-ttu-id="a334a-145">Varsa birincil çevrimiçi olduğunu ve bazı veri kaybı komutu verildiğinde işlem yürüten ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="a334a-145">If the primary is online and committing transactions when the command is issued some data loss may occur.</span></span> 
> 
> 

## <a name="remove-secondary-database"></a><span data-ttu-id="a334a-146">İkincil veritabanını Kaldır</span><span class="sxs-lookup"><span data-stu-id="a334a-146">Remove secondary database</span></span>
<span data-ttu-id="a334a-147">Bu işlem kalıcı olarak ikincil veritabanı için çoğaltma sonlandırır ve normal bir okuma-yazma veritabanı rolü ikincil değiştirir.</span><span class="sxs-lookup"><span data-stu-id="a334a-147">This operation permanently terminates the replication to the secondary database, and changes the role of the secondary to a regular read-write database.</span></span> <span data-ttu-id="a334a-148">İkincil veritabanı bağlantısını bozuksa, komut başarılı olur, ancak ikincil mu bağlantı kadar sonra okuma-yazma olmayan bir duruma geri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="a334a-148">If the connectivity to the secondary database is broken, the command succeeds but the secondary does not become read-write until after connectivity is restored.</span></span>  

1. <span data-ttu-id="a334a-149">İçinde [Azure portal](http://portal.azure.com), coğrafi çoğaltma ortaklığı birincil veritabanında konumuna göz atın.</span><span class="sxs-lookup"><span data-stu-id="a334a-149">In the [Azure portal](http://portal.azure.com), browse to the primary database in the geo-replication partnership.</span></span>
2. <span data-ttu-id="a334a-150">SQL veritabanı sayfasında seçin **coğrafi çoğaltma**.</span><span class="sxs-lookup"><span data-stu-id="a334a-150">On the SQL database page, select **geo-replication**.</span></span>
3. <span data-ttu-id="a334a-151">İçinde **İKİNCİLLER** listesinde, coğrafi çoğaltma ortaklığı kaldırmak istediğiniz veritabanını seçin.</span><span class="sxs-lookup"><span data-stu-id="a334a-151">In the **SECONDARIES** list, select the database you want to remove from the geo-replication partnership.</span></span>
4. <span data-ttu-id="a334a-152">Tıklatın **çoğaltmayı durdurma**.</span><span class="sxs-lookup"><span data-stu-id="a334a-152">Click **Stop Replication**.</span></span>
   
    ![İkincil Kaldır](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. <span data-ttu-id="a334a-154">Bir onay penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="a334a-154">A confirmation window opens.</span></span> <span data-ttu-id="a334a-155">Tıklatın **Evet** coğrafi çoğaltma ortaklığı veritabanını kaldırmak için.</span><span class="sxs-lookup"><span data-stu-id="a334a-155">Click **Yes** to remove the database from the geo-replication partnership.</span></span> <span data-ttu-id="a334a-156">(Bu bir okuma-yazma veritabanına herhangi çoğaltma'nın parçası olmayan ayarlanır.)</span><span class="sxs-lookup"><span data-stu-id="a334a-156">(Set it to a read-write database not part of any replication.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="a334a-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a334a-157">Next steps</span></span>
* <span data-ttu-id="a334a-158">Aktif coğrafi çoğaltma hakkında daha fazla bilgi için bkz: [aktif coğrafi çoğaltma](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a334a-158">To learn more about active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md).</span></span>
* <span data-ttu-id="a334a-159">İş sürekliliğine genel bakış ve senaryolar için bkz: [iş sürekliliğine genel bakış](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="a334a-159">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md).</span></span>

