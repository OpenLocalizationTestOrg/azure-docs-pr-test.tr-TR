---
title: "aaaRestore Azure SQL Data Warehouse'a (Azure portalı) | Microsoft Docs"
description: "Azure SQL Data Warehouse geri yüklemek için azure portal görevler."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: barbkess
editor: 
ms.assetid: b0aef539-7657-4b0e-9899-74098f5c21bc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 09/21/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cb225d2a21b61acab70a51b69c266f8d3ffacc9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-azure-sql-data-warehouse-portal"></a><span data-ttu-id="4a45f-103">Azure SQL Data Warehouse (portal) geri yükleme</span><span class="sxs-lookup"><span data-stu-id="4a45f-103">Restore Azure SQL Data Warehouse (portal)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="4a45f-104">[Genel bakış][Overview]</span><span class="sxs-lookup"><span data-stu-id="4a45f-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="4a45f-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="4a45f-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="4a45f-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="4a45f-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="4a45f-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="4a45f-107">[REST][REST]</span></span>
>
>
<span data-ttu-id="4a45f-108">Bu makalede, Azure portal kullanarak Azure SQL Data Warehouse toorestore hello nasıl öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="4a45f-108">In this article, you will learn how toorestore Azure SQL Data Warehouse by using hello Azure portal.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4a45f-109">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="4a45f-109">Before you begin</span></span>
<span data-ttu-id="4a45f-110">**DTU kapasitenizi doğrulayın.**</span><span class="sxs-lookup"><span data-stu-id="4a45f-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="4a45f-111">SQL veri ambarı her bir örneğini varsayılan veri işleme birimi (DTU) kota olan bir SQL server tarafından (örneğin, myserver.database.windows.net) barındırılıyor.</span><span class="sxs-lookup"><span data-stu-id="4a45f-111">Each instance of SQL Data Warehouse is hosted by a SQL server (for example, myserver.database.windows.net) which has a default data throughput unit (DTU) quota.</span></span> <span data-ttu-id="4a45f-112">SQL veri ambarı geri yüklemeden önce SQL server'ınızdaki geri yüklemekte hello veritabanı için yeterli kalan DTU kota sahip olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="4a45f-112">Before you can restore SQL Data Warehouse, verify that your SQL server has enough remaining DTU quota for hello database that you're restoring.</span></span> <span data-ttu-id="4a45f-113">toolearn toocalculate DTU kota veya toorequest daha fazla Dtu'lar nasıl görürüm [DTU kota değişiklik isteği][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="4a45f-113">toolearn how toocalculate DTU quota or toorequest more DTUs, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="4a45f-114">Etkin ya da duraklatılmış bir veritabanını geri yükle</span><span class="sxs-lookup"><span data-stu-id="4a45f-114">Restore an active or paused database</span></span>
<span data-ttu-id="4a45f-115">bir veritabanı toorestore:</span><span class="sxs-lookup"><span data-stu-id="4a45f-115">toorestore a database:</span></span>

1. <span data-ttu-id="4a45f-116">İçinde toohello oturum [Azure portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="4a45f-116">Sign in toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="4a45f-117">Merhaba sol bölmesinde seçin **Gözat**ve ardından **SQL sunucuları**.</span><span class="sxs-lookup"><span data-stu-id="4a45f-117">In hello left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Gözat seçin > SQL Server'lar](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="4a45f-119">Sunucunuz bulun ve seçin.</span><span class="sxs-lookup"><span data-stu-id="4a45f-119">Find your server, and then select it.</span></span>

    ![Sunucunuzu seçin](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. <span data-ttu-id="4a45f-121">SQL veri ambarı Hello örneğini toorestore gelen istediğiniz ve seçin bulun.</span><span class="sxs-lookup"><span data-stu-id="4a45f-121">Find hello instance of SQL Data Warehouse that you want toorestore from, and then select it.</span></span>

    ![SQL veri ambarı toorestore Hello örneğini seçin](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. <span data-ttu-id="4a45f-123">Merhaba veri ambarı dikey penceresinde Hello üstünde seçin **geri**.</span><span class="sxs-lookup"><span data-stu-id="4a45f-123">At hello top of hello Data Warehouse blade, select **Restore**.</span></span>

    ![Geri yükleme seçin](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. <span data-ttu-id="4a45f-125">Yeni bir belirtin **veritabanı adı**.</span><span class="sxs-lookup"><span data-stu-id="4a45f-125">Specify a new **Database name**.</span></span>
7. <span data-ttu-id="4a45f-126">Son SELECT hello **geri yükleme noktası**.</span><span class="sxs-lookup"><span data-stu-id="4a45f-126">Select hello latest **Restore point**.</span></span>

   <span data-ttu-id="4a45f-127">Merhaba en son geri yükleme noktası seçtiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="4a45f-127">Make sure you choose hello latest restore point.</span></span> <span data-ttu-id="4a45f-128">Geri yükleme noktaları Eşgüdümlü Evrensel Saat (UTC) gösterilir çünkü hello varsayılan seçeneği hello en son geri yükleme noktası olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="4a45f-128">Because restore points are shown in Coordinated Universal Time (UTC), hello default option might not be hello latest restore point.</span></span>

      ![Bir geri yükleme noktası seçin](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. <span data-ttu-id="4a45f-130">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="4a45f-130">Select **OK**.</span></span>
9. <span data-ttu-id="4a45f-131">Merhaba veritabanı geri yükleme işlemi başlayacak ve kullanabileceğiniz **bildirimleri** toomonitor hello işlemi.</span><span class="sxs-lookup"><span data-stu-id="4a45f-131">hello database restore process will begin, and you can use **NOTIFICATIONS** toomonitor hello process.</span></span>

> [!NOTE]
> <span data-ttu-id="4a45f-132">Merhaba geri yükleme tamamlandıktan sonra izleyerek, kurtarılan veritabanının yapılandırabilirsiniz [kurtarma işleminden sonra veritabanını yapılandırma][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="4a45f-132">After hello restore has finished, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="restore-a-deleted-database"></a><span data-ttu-id="4a45f-133">Silinen veritabanını geri yükleme</span><span class="sxs-lookup"><span data-stu-id="4a45f-133">Restore a deleted database</span></span>
<span data-ttu-id="4a45f-134">Silinen bir veritabanını toorestore:</span><span class="sxs-lookup"><span data-stu-id="4a45f-134">toorestore a deleted database:</span></span>

1. <span data-ttu-id="4a45f-135">İçinde toohello oturum [Azure portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="4a45f-135">Sign in toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="4a45f-136">Merhaba sol bölmesinde seçin **Gözat**ve ardından **SQL sunucuları**.</span><span class="sxs-lookup"><span data-stu-id="4a45f-136">In hello left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Gözat seçin > SQL Server'lar](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="4a45f-138">Sunucunuz bulun ve seçin.</span><span class="sxs-lookup"><span data-stu-id="4a45f-138">Find your server, and then select it.</span></span>

    ![Sunucunuzu seçin](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. <span data-ttu-id="4a45f-140">Toohello aşağı **Operations** sunucunuzun dikey bölüm.</span><span class="sxs-lookup"><span data-stu-id="4a45f-140">Scroll down toohello **Operations** section on your server's blade.</span></span>
5. <span data-ttu-id="4a45f-141">Select hello **veritabanlarını sildi** döşeme.</span><span class="sxs-lookup"><span data-stu-id="4a45f-141">Select hello **Deleted databases** tile.</span></span>

    ![Merhaba silinen veritabanları kutucuk seçin](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. <span data-ttu-id="4a45f-143">Silinen hello veritabanını toorestore istediğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="4a45f-143">Select hello deleted database that you want toorestore.</span></span>

    ![Bir veritabanı toorestore seçin](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. <span data-ttu-id="4a45f-145">Yeni bir belirtin **veritabanı adı**.</span><span class="sxs-lookup"><span data-stu-id="4a45f-145">Specify a new **Database name**.</span></span>

    ![Merhaba veritabanı için bir ad ekleyin](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. <span data-ttu-id="4a45f-147">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="4a45f-147">Select **OK**.</span></span>
9. <span data-ttu-id="4a45f-148">Merhaba veritabanı geri yükleme işlemi başlayacak ve kullanabileceğiniz **bildirimleri** toomonitor hello işlemi.</span><span class="sxs-lookup"><span data-stu-id="4a45f-148">hello database restore process will begin, and you can use **NOTIFICATIONS** toomonitor hello process.</span></span>

> [!NOTE]
> <span data-ttu-id="4a45f-149">Merhaba geri yükleme tamamlandıktan sonra veritabanınızı tooconfigure bkz [kurtarma işleminden sonra veritabanını yapılandırma][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="4a45f-149">tooconfigure your database after hello restore has finished, see [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="4a45f-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4a45f-150">Next steps</span></span>
<span data-ttu-id="4a45f-151">Merhaba okuma Azure SQL veritabanı sürümlerinin hello iş sürekliliği özellikleri hakkında toolearn [Azure SQL Database iş sürekliliğine genel bakış][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="4a45f-151">toolearn about hello business continuity features of Azure SQL Database editions, read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change

<!--MSDN references-->

<!--Blog references-->

<!--Other Web references-->
[Azure portal]: https://portal.azure.com/
