---
title: "Azure portal: SQL Database coğrafi çoğaltma | Microsoft Docs"
description: "Coğrafi çoğaltma hello Azure portal ve başlatma yük devretme Azure SQL veritabanı için yapılandırma"
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
ms.openlocfilehash: 09cbbdb040f36c42593e3be87ce6db2238f36656
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-hello-azure-portal-and-initiate-failover"></a><span data-ttu-id="118e5-103">Aktif coğrafi çoğaltma hello Azure portal ve başlatma yük devretme Azure SQL veritabanı için yapılandırma</span><span class="sxs-lookup"><span data-stu-id="118e5-103">Configure active geo-replication for Azure SQL Database in hello Azure portal and initiate failover</span></span>

<span data-ttu-id="118e5-104">Bu makale size nasıl gösterir tooconfigure aktif coğrafi çoğaltma SQL veritabanı için hello içinde [Azure portal](http://portal.azure.com) ve tooinitiate yük devretme.</span><span class="sxs-lookup"><span data-stu-id="118e5-104">This article shows you how tooconfigure active geo-replication for SQL Database in hello [Azure portal](http://portal.azure.com) and tooinitiate failover.</span></span>

<span data-ttu-id="118e5-105">hello Azure portal ile tooinitiate yük devretme bkz [planlanmış veya planlanmamış bir yük devretme hello Azure portal ile Azure SQL veritabanı için başlatmak](sql-database-geo-replication-portal.md).</span><span class="sxs-lookup"><span data-stu-id="118e5-105">tooinitiate failover with hello Azure portal, see [Initiate a planned or unplanned failover for Azure SQL Database with hello Azure portal](sql-database-geo-replication-portal.md).</span></span>

<span data-ttu-id="118e5-106">tooconfigure aktif coğrafi hello Azure portal kullanarak çoğaltma, kaynak aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="118e5-106">tooconfigure active geo-replication by using hello Azure portal, you need hello following resource:</span></span>

* <span data-ttu-id="118e5-107">Azure SQL veritabanını: hello birincil veritabanı tooreplicate tooa farklı coğrafi bölge istiyor.</span><span class="sxs-lookup"><span data-stu-id="118e5-107">An Azure SQL database: hello primary database that you want tooreplicate tooa different geographical region.</span></span>

> [!Note]
<span data-ttu-id="118e5-108">Aktif coğrafi çoğaltma hello veritabanları arasında olmalıdır aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="118e5-108">Active geo-replication must be between databases in hello same subscription.</span></span>

## <a name="add-a-secondary-database"></a><span data-ttu-id="118e5-109">İkincil bir veritabanı ekleyin</span><span class="sxs-lookup"><span data-stu-id="118e5-109">Add a secondary database</span></span>
<span data-ttu-id="118e5-110">Merhaba aşağıdaki adımları yeni bir ikincil veritabanı bir coğrafi çoğaltma ortaklığı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="118e5-110">hello following steps create a new secondary database in a geo-replication partnership.</span></span>  

<span data-ttu-id="118e5-111">ikincil bir veritabanı tooadd hello abonelik sahibi veya ortak sahibi olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="118e5-111">tooadd a secondary database, you must be hello subscription owner or co-owner.</span></span>

<span data-ttu-id="118e5-112">Merhaba ikincil veritabanı aynı hello birincil veritabanı olarak ad hello sahiptir ve varsa varsayılan olarak, hello aynı hizmet düzeyi.</span><span class="sxs-lookup"><span data-stu-id="118e5-112">hello secondary database has hello same name as hello primary database and has, by default, hello same service level.</span></span> <span data-ttu-id="118e5-113">Merhaba ikincil veritabanı tek bir veritabanı veya veritabanı esnek havuzdaki olabilir.</span><span class="sxs-lookup"><span data-stu-id="118e5-113">hello secondary database can be a single database or a database in an elastic pool.</span></span> <span data-ttu-id="118e5-114">Daha fazla bilgi için bkz: [hizmet katmanları](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="118e5-114">For more information, see [Service tiers](sql-database-service-tiers.md).</span></span>
<span data-ttu-id="118e5-115">Merhaba ikincil oluşturulan ve dağıtılan sonra veri hello birincil veritabanı toohello yeni ikincil veritabanından çoğaltmaya başlar.</span><span class="sxs-lookup"><span data-stu-id="118e5-115">After hello secondary is created and seeded, data begins replicating from hello primary database toohello new secondary database.</span></span>

> [!NOTE]
> <span data-ttu-id="118e5-116">(Örneğin, bir önceki coğrafi çoğaltma ilişkisi sonlandırma sonucunda) Hello ortak veritabanı zaten var. hello komutu başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="118e5-116">If hello partner database already exists (for example, as a result of terminating a previous geo-replication relationship) hello command fails.</span></span>
> 

1. <span data-ttu-id="118e5-117">Merhaba, [Azure portal](http://portal.azure.com), tooset coğrafi çoğaltma için istediğiniz toohello veritabanı göz atın.</span><span class="sxs-lookup"><span data-stu-id="118e5-117">In hello [Azure portal](http://portal.azure.com), browse toohello database that you want tooset up for geo-replication.</span></span>
2. <span data-ttu-id="118e5-118">Merhaba SQL veritabanı sayfasında seçin **coğrafi çoğaltma**, sonra hello bölge toocreate hello ikincil veritabanını seçin.</span><span class="sxs-lookup"><span data-stu-id="118e5-118">On hello SQL database page, select **geo-replication**, and then select hello region toocreate hello secondary database.</span></span> <span data-ttu-id="118e5-119">Merhaba birincil veritabanı barındırma hello bölgesi dışında herhangi bir bölgeyi seçebilirsiniz, ancak hello öneririz [eşleştirilmiş bölge](../best-practices-availability-paired-regions.md).</span><span class="sxs-lookup"><span data-stu-id="118e5-119">You can select any region other than hello region hosting hello primary database, but we recommend hello [paired region](../best-practices-availability-paired-regions.md).</span></span>
   
    ![Coğrafi çoğaltmayı yapılandırma](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. <span data-ttu-id="118e5-121">Seçin veya hello sunucuyu ve fiyatlandırma katmanı hello ikincil veritabanı için yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="118e5-121">Select or configure hello server and pricing tier for hello secondary database.</span></span>
   
    ![İkincil yapılandırın](./media/sql-database-geo-replication-portal/create-secondary.png)
4. <span data-ttu-id="118e5-123">İsteğe bağlı olarak, ikincil veritabanı tooan esnek havuz ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="118e5-123">Optionally, you can add a secondary database tooan elastic pool.</span></span> <span data-ttu-id="118e5-124">bir havuzdaki toocreate hello ikincil veritabanını tıklatın **esnek havuz** ve hello hedef sunucu üzerindeki bir havuz seçin.</span><span class="sxs-lookup"><span data-stu-id="118e5-124">toocreate hello secondary database in a pool, click **elastic pool** and select a pool on hello target server.</span></span> <span data-ttu-id="118e5-125">Bir havuzu hello hedef sunucuda zaten mevcut olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="118e5-125">A pool must already exist on hello target server.</span></span> <span data-ttu-id="118e5-126">Bu iş akışı bir havuzu oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="118e5-126">This workflow does not create a pool.</span></span>
5. <span data-ttu-id="118e5-127">Tıklatın **oluşturma** tooadd hello ikincil.</span><span class="sxs-lookup"><span data-stu-id="118e5-127">Click **Create** tooadd hello secondary.</span></span>
6. <span data-ttu-id="118e5-128">Merhaba ikincil veritabanı oluşturulur ve işlem dengeli hello başlar.</span><span class="sxs-lookup"><span data-stu-id="118e5-128">hello secondary database is created and hello seeding process begins.</span></span>
   
    ![İkincil yapılandırın](./media/sql-database-geo-replication-portal/seeding0.png)
7. <span data-ttu-id="118e5-130">İşlem dengeli hello tamamlandığında hello ikincil veritabanı durumunu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="118e5-130">When hello seeding process is complete, hello secondary database displays its status.</span></span>
   
    ![Tam üretme](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a><span data-ttu-id="118e5-132">Bir yük devretme başlatın</span><span class="sxs-lookup"><span data-stu-id="118e5-132">Initiate a failover</span></span>

<span data-ttu-id="118e5-133">Merhaba ikincil veritabanının birincil anahtarlı toobecome hello olabilir.</span><span class="sxs-lookup"><span data-stu-id="118e5-133">hello secondary database can be switched toobecome hello primary.</span></span>  

1. <span data-ttu-id="118e5-134">Merhaba, [Azure portal](http://portal.azure.com), birincil veritabanı hello coğrafi çoğaltma ortaklığı toohello göz atın.</span><span class="sxs-lookup"><span data-stu-id="118e5-134">In hello [Azure portal](http://portal.azure.com), browse toohello primary database in hello geo-replication partnership.</span></span>
2. <span data-ttu-id="118e5-135">Merhaba SQL veritabanı dikey penceresinde, seçin **tüm ayarları** > **coğrafi çoğaltma**.</span><span class="sxs-lookup"><span data-stu-id="118e5-135">On hello SQL Database blade, select **All settings** > **geo-replication**.</span></span>
3. <span data-ttu-id="118e5-136">Merhaba, **İKİNCİLLER** listesi, toobecome istediğiniz select hello veritabanı hello yeni birincil ve tıklayın **yük devretme**.</span><span class="sxs-lookup"><span data-stu-id="118e5-136">In hello **SECONDARIES** list, select hello database you want toobecome hello new primary and click **Failover**.</span></span>
   
    ![Yük devretme](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. <span data-ttu-id="118e5-138">Tıklatın **Evet** toobegin hello yük devretme.</span><span class="sxs-lookup"><span data-stu-id="118e5-138">Click **Yes** toobegin hello failover.</span></span>

<span data-ttu-id="118e5-139">Merhaba komutu hello ikincil veritabanı hello birincil rolünde hemen geçer.</span><span class="sxs-lookup"><span data-stu-id="118e5-139">hello command immediately switches hello secondary database into hello primary role.</span></span> 

<span data-ttu-id="118e5-140">Merhaba rolleri geçiş sırasında hangi sırasında her iki veritabanı (Merhaba 0 too25 saniye üzerinde sırasını) kullanılamaz kısa bir süre yoktur.</span><span class="sxs-lookup"><span data-stu-id="118e5-140">There is a short period during which both databases are unavailable (on hello order of 0 too25 seconds) while hello roles are switched.</span></span> <span data-ttu-id="118e5-141">Birden fazla ikincil veritabanları, hello komutu Hello birincil veritabanı otomatik olarak varsa, yeniden yapılandırır diğer ikincil tooconnect toohello yeni birincil hello.</span><span class="sxs-lookup"><span data-stu-id="118e5-141">If hello primary database has multiple secondary databases, hello command automatically reconfigures hello other secondaries tooconnect toohello new primary.</span></span> <span data-ttu-id="118e5-142">Merhaba tüm işlemi normal koşullarda dakika toocomplete değerinden almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="118e5-142">hello entire operation should take less than a minute toocomplete under normal circumstances.</span></span> 

> [!NOTE]
> <span data-ttu-id="118e5-143">Bu komut, bir kesinti durumunda hello veritabanının Hızlı Kurtarma için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="118e5-143">This command is designed for quick recovery of hello database in case of an outage.</span></span> <span data-ttu-id="118e5-144">Yük devretme (yük devretme zorlanır) veri eşitleme tetikler.</span><span class="sxs-lookup"><span data-stu-id="118e5-144">It triggers failover without data synchronization (forced failover).</span></span>  <span data-ttu-id="118e5-145">Varsa Hello birincil çevrimiçi olduğunu ve bazı veri kaybı hello komut verildiğinde işlem yürüten ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="118e5-145">If hello primary is online and committing transactions when hello command is issued some data loss may occur.</span></span> 
> 
> 

## <a name="remove-secondary-database"></a><span data-ttu-id="118e5-146">İkincil veritabanını Kaldır</span><span class="sxs-lookup"><span data-stu-id="118e5-146">Remove secondary database</span></span>
<span data-ttu-id="118e5-147">Bu işlem kalıcı olarak hello çoğaltma toohello ikincil veritabanı sonlandırır ve değişiklikleri hello ikincil tooa normal okuma-yazma veritabanının rolü hello.</span><span class="sxs-lookup"><span data-stu-id="118e5-147">This operation permanently terminates hello replication toohello secondary database, and changes hello role of hello secondary tooa regular read-write database.</span></span> <span data-ttu-id="118e5-148">Merhaba bağlantı toohello ikincil veritabanının bozuk olması durumunda, hello komutu başarılı olur, ancak bağlantı geri yüklendikten sonra ikincil mu değil duruma okuma-yazma kadar hello.</span><span class="sxs-lookup"><span data-stu-id="118e5-148">If hello connectivity toohello secondary database is broken, hello command succeeds but hello secondary does not become read-write until after connectivity is restored.</span></span>  

1. <span data-ttu-id="118e5-149">Merhaba, [Azure portal](http://portal.azure.com), birincil veritabanı hello coğrafi çoğaltma ortaklığı toohello göz atın.</span><span class="sxs-lookup"><span data-stu-id="118e5-149">In hello [Azure portal](http://portal.azure.com), browse toohello primary database in hello geo-replication partnership.</span></span>
2. <span data-ttu-id="118e5-150">Merhaba SQL veritabanı sayfasında seçin **coğrafi çoğaltma**.</span><span class="sxs-lookup"><span data-stu-id="118e5-150">On hello SQL database page, select **geo-replication**.</span></span>
3. <span data-ttu-id="118e5-151">Merhaba, **İKİNCİLLER** listesi, hello coğrafi çoğaltma ortaklığı gelen tooremove istediğiniz select hello veritabanı.</span><span class="sxs-lookup"><span data-stu-id="118e5-151">In hello **SECONDARIES** list, select hello database you want tooremove from hello geo-replication partnership.</span></span>
4. <span data-ttu-id="118e5-152">Tıklatın **çoğaltmayı durdurma**.</span><span class="sxs-lookup"><span data-stu-id="118e5-152">Click **Stop Replication**.</span></span>
   
    ![İkincil Kaldır](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. <span data-ttu-id="118e5-154">Bir onay penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="118e5-154">A confirmation window opens.</span></span> <span data-ttu-id="118e5-155">Tıklatın **Evet** tooremove hello hello coğrafi çoğaltma ortaklığı veritabanından.</span><span class="sxs-lookup"><span data-stu-id="118e5-155">Click **Yes** tooremove hello database from hello geo-replication partnership.</span></span> <span data-ttu-id="118e5-156">(Tooa okuma-yazma veritabanı tüm çoğaltma'nın parçası olmayan ayarlayın.)</span><span class="sxs-lookup"><span data-stu-id="118e5-156">(Set it tooa read-write database not part of any replication.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="118e5-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="118e5-157">Next steps</span></span>
* <span data-ttu-id="118e5-158">Aktif coğrafi çoğaltma hakkında daha fazla toolearn bkz [aktif coğrafi çoğaltma](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="118e5-158">toolearn more about active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md).</span></span>
* <span data-ttu-id="118e5-159">İş sürekliliğine genel bakış ve senaryolar için bkz: [iş sürekliliğine genel bakış](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="118e5-159">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md).</span></span>

