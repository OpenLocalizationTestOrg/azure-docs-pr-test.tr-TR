---
title: "Azure SQL Data Warehouse'a (Azure portalı) geri | Microsoft Docs"
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
ms.openlocfilehash: f6bc8671410dc7015a8d2a4bea1ba11f9ae526c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="restore-azure-sql-data-warehouse-portal"></a><span data-ttu-id="21241-103">Azure SQL Data Warehouse (portal) geri yükleme</span><span class="sxs-lookup"><span data-stu-id="21241-103">Restore Azure SQL Data Warehouse (portal)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="21241-104">[Genel bakış][Overview]</span><span class="sxs-lookup"><span data-stu-id="21241-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="21241-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="21241-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="21241-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="21241-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="21241-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="21241-107">[REST][REST]</span></span>
>
>
<span data-ttu-id="21241-108">Bu makalede, Azure portalını kullanarak Azure SQL Data Warehouse geri öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="21241-108">In this article, you will learn how to restore Azure SQL Data Warehouse by using the Azure portal.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="21241-109">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="21241-109">Before you begin</span></span>
<span data-ttu-id="21241-110">**DTU kapasitenizi doğrulayın.**</span><span class="sxs-lookup"><span data-stu-id="21241-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="21241-111">SQL veri ambarı her bir örneğini varsayılan veri işleme birimi (DTU) kota olan bir SQL server tarafından (örneğin, myserver.database.windows.net) barındırılıyor.</span><span class="sxs-lookup"><span data-stu-id="21241-111">Each instance of SQL Data Warehouse is hosted by a SQL server (for example, myserver.database.windows.net) which has a default data throughput unit (DTU) quota.</span></span> <span data-ttu-id="21241-112">SQL veri ambarı geri yüklemeden önce SQL server'ınızdaki geri yüklemekte veritabanı için yeterli kalan DTU kota sahip olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="21241-112">Before you can restore SQL Data Warehouse, verify that your SQL server has enough remaining DTU quota for the database that you're restoring.</span></span> <span data-ttu-id="21241-113">DTU kota hesaplamak için ya da daha fazla Dtu'lar istemek için öğrenmek için bkz: [DTU kota değişiklik isteği][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="21241-113">To learn how to calculate DTU quota or to request more DTUs, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="21241-114">Etkin ya da duraklatılmış bir veritabanını geri yükle</span><span class="sxs-lookup"><span data-stu-id="21241-114">Restore an active or paused database</span></span>
<span data-ttu-id="21241-115">Bir veritabanını geri yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="21241-115">To restore a database:</span></span>

1. <span data-ttu-id="21241-116">[Azure portalında][Azure portal] oturum açın.</span><span class="sxs-lookup"><span data-stu-id="21241-116">Sign in to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="21241-117">Sol bölmede seçin **Gözat**ve ardından **SQL sunucuları**.</span><span class="sxs-lookup"><span data-stu-id="21241-117">In the left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Gözat seçin > SQL Server'lar](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="21241-119">Sunucunuz bulun ve seçin.</span><span class="sxs-lookup"><span data-stu-id="21241-119">Find your server, and then select it.</span></span>

    ![Sunucunuzu seçin](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. <span data-ttu-id="21241-121">Geri yüklemek istediğiniz bir SQL Data Warehouse örneğini bulun ve seçin.</span><span class="sxs-lookup"><span data-stu-id="21241-121">Find the instance of SQL Data Warehouse that you want to restore from, and then select it.</span></span>

    ![Geri yüklemek için SQL veri ambarı örneği seçin](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. <span data-ttu-id="21241-123">Veri ambarı dikey pencerenin en üstünde seçin **geri**.</span><span class="sxs-lookup"><span data-stu-id="21241-123">At the top of the Data Warehouse blade, select **Restore**.</span></span>

    ![Geri yükleme seçin](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. <span data-ttu-id="21241-125">Yeni bir belirtin **veritabanı adı**.</span><span class="sxs-lookup"><span data-stu-id="21241-125">Specify a new **Database name**.</span></span>
7. <span data-ttu-id="21241-126">En son seçin **geri yükleme noktası**.</span><span class="sxs-lookup"><span data-stu-id="21241-126">Select the latest **Restore point**.</span></span>

   <span data-ttu-id="21241-127">En son geri yükleme noktası seçtiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="21241-127">Make sure you choose the latest restore point.</span></span> <span data-ttu-id="21241-128">Geri yükleme noktaları Eşgüdümlü Evrensel Saat (UTC) gösterilir çünkü varsayılan seçeneği en son geri yükleme noktası olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="21241-128">Because restore points are shown in Coordinated Universal Time (UTC), the default option might not be the latest restore point.</span></span>

      ![Bir geri yükleme noktası seçin](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. <span data-ttu-id="21241-130">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="21241-130">Select **OK**.</span></span>
9. <span data-ttu-id="21241-131">Veritabanı geri yükleme işlemi başlar ve kullanabileceğiniz **bildirimleri** işlemi izlemek üzere.</span><span class="sxs-lookup"><span data-stu-id="21241-131">The database restore process will begin, and you can use **NOTIFICATIONS** to monitor the process.</span></span>

> [!NOTE]
> <span data-ttu-id="21241-132">Geri yükleme tamamlandıktan sonra kurtarılan veritabanının izleyerek yapılandırabileceğiniz [kurtarma işleminden sonra veritabanını yapılandırma][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="21241-132">After the restore has finished, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="restore-a-deleted-database"></a><span data-ttu-id="21241-133">Silinen veritabanını geri yükleme</span><span class="sxs-lookup"><span data-stu-id="21241-133">Restore a deleted database</span></span>
<span data-ttu-id="21241-134">Silinen bir veritabanını geri yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="21241-134">To restore a deleted database:</span></span>

1. <span data-ttu-id="21241-135">[Azure portalında][Azure portal] oturum açın.</span><span class="sxs-lookup"><span data-stu-id="21241-135">Sign in to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="21241-136">Sol bölmede seçin **Gözat**ve ardından **SQL sunucuları**.</span><span class="sxs-lookup"><span data-stu-id="21241-136">In the left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Gözat seçin > SQL Server'lar](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="21241-138">Sunucunuz bulun ve seçin.</span><span class="sxs-lookup"><span data-stu-id="21241-138">Find your server, and then select it.</span></span>

    ![Sunucunuzu seçin](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. <span data-ttu-id="21241-140">Ekranı aşağı kaydırarak **Operations** sunucunuzun dikey bölüm.</span><span class="sxs-lookup"><span data-stu-id="21241-140">Scroll down to the **Operations** section on your server's blade.</span></span>
5. <span data-ttu-id="21241-141">Seçin **veritabanlarını sildi** döşeme.</span><span class="sxs-lookup"><span data-stu-id="21241-141">Select the **Deleted databases** tile.</span></span>

    ![Silinen veritabanları kutucuk seçin](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. <span data-ttu-id="21241-143">Geri yüklemek istediğiniz silinen bir veritabanını seçin.</span><span class="sxs-lookup"><span data-stu-id="21241-143">Select the deleted database that you want to restore.</span></span>

    ![Geri yüklemek için bir veritabanı seçin](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. <span data-ttu-id="21241-145">Yeni bir belirtin **veritabanı adı**.</span><span class="sxs-lookup"><span data-stu-id="21241-145">Specify a new **Database name**.</span></span>

    ![Veritabanı için bir ad ekleyin](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. <span data-ttu-id="21241-147">**Tamam**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="21241-147">Select **OK**.</span></span>
9. <span data-ttu-id="21241-148">Veritabanı geri yükleme işlemi başlar ve kullanabileceğiniz **bildirimleri** işlemi izlemek üzere.</span><span class="sxs-lookup"><span data-stu-id="21241-148">The database restore process will begin, and you can use **NOTIFICATIONS** to monitor the process.</span></span>

> [!NOTE]
> <span data-ttu-id="21241-149">Geri yükleme tamamlandıktan sonra veritabanını yapılandırmak için bkz: [kurtarma işleminden sonra veritabanını yapılandırma][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="21241-149">To configure your database after the restore has finished, see [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="21241-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="21241-150">Next steps</span></span>
<span data-ttu-id="21241-151">Azure SQL veritabanı sürümlerini iş sürekliliği özellikleri hakkında bilgi edinmek için okuma [Azure SQL Database iş sürekliliğine genel bakış][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="21241-151">To learn about the business continuity features of Azure SQL Database editions, read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

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
