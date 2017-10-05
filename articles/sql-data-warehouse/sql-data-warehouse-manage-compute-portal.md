---
title: "Azure SQL Data warehouse'da (Azure portalı) işlem güç yönetimi | Microsoft Docs"
description: "İşlem gücüne yönetmek için azure portal görevleri. Dwu ayarlayarak işlem kaynaklarını ölçeklendirme. Veya, duraklatma ve sürdürme işlem kaynaklarını maliyet tasarrufu sağlamak."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 233b0da5-4abd-4d1d-9586-4ccc5f50b071
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 63888d5dd103b585cf18e4787d3e779810163e3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-azure-portal"></a><span data-ttu-id="b4035-105">Azure SQL Data warehouse'da (Azure portalı) işlem güç yönetimi</span><span class="sxs-lookup"><span data-stu-id="b4035-105">Manage compute power in Azure SQL Data Warehouse (Azure portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b4035-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="b4035-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="b4035-107">Portal</span><span class="sxs-lookup"><span data-stu-id="b4035-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="b4035-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b4035-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="b4035-109">REST</span><span class="sxs-lookup"><span data-stu-id="b4035-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="b4035-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="b4035-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>


## <a name="scale-compute-power"></a><span data-ttu-id="b4035-111">Ölçek işlem gücü</span><span class="sxs-lookup"><span data-stu-id="b4035-111">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="b4035-112">İşlem kaynakları değiştirmek için:</span><span class="sxs-lookup"><span data-stu-id="b4035-112">To change compute resources:</span></span>

1. <span data-ttu-id="b4035-113">Açık [Azure portal][Azure portal], veritabanınızı açın ve'ı tıklatın **ölçek**.</span><span class="sxs-lookup"><span data-stu-id="b4035-113">Open the [Azure portal][Azure portal], open your database, and click **Scale**.</span></span>

    ![Ölçek'ı tıklatın][1]
2. <span data-ttu-id="b4035-115">Ölçek dikey penceresinde, kaydırıcıyı sola veya sağa DWU ayarını değiştirmek taşıyın.</span><span class="sxs-lookup"><span data-stu-id="b4035-115">In the Scale blade, move the slider left or right to change the DWU setting.</span></span>

    ![Kaydırıcıyı taşıyın][2]
3. <span data-ttu-id="b4035-117">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b4035-117">Click **Save**.</span></span> <span data-ttu-id="b4035-118">Bir onay iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b4035-118">A confirmation message appears.</span></span> <span data-ttu-id="b4035-119">Tıklatın **Evet** onaylamak için veya **hiçbir** iptal etmek için.</span><span class="sxs-lookup"><span data-stu-id="b4035-119">Click **yes** to confirm or **no** to cancel.</span></span>

    ![Kaydet’e tıklayın.][3]

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="b4035-121">Duraklatma işlem</span><span class="sxs-lookup"><span data-stu-id="b4035-121">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="b4035-122">Bir veritabanı duraklatmak için:</span><span class="sxs-lookup"><span data-stu-id="b4035-122">To pause a database:</span></span>

1. <span data-ttu-id="b4035-123">Açık [Azure portal] [ Azure portal] ve veritabanınızı açın.</span><span class="sxs-lookup"><span data-stu-id="b4035-123">Open the [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="b4035-124">Durum olduğuna dikkat edin **çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="b4035-124">Notice that the Status is **Online**.</span></span>

    ![Çevrimiçi durumu][6]
2. <span data-ttu-id="b4035-126">İşlem ve bellek kaynakları askıya almak için tıklayın **duraklatma**, ve ardından bir onay iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b4035-126">To suspend compute and memory resources, click **Pause**, and then a confirmation message appears.</span></span> <span data-ttu-id="b4035-127">Tıklatın **Evet** onaylamak için veya **hiçbir** iptal etmek için.</span><span class="sxs-lookup"><span data-stu-id="b4035-127">Click **yes** to confirm or **no** to cancel.</span></span>

    ![Duraklatma onaylayın][7]
3. <span data-ttu-id="b4035-129">SQL veri ambarı veritabanı başlatılırken durumudur **duraklatma**.</span><span class="sxs-lookup"><span data-stu-id="b4035-129">While SQL Data Warehouse is starting the database, the status is **Pausing**.</span></span>
4. <span data-ttu-id="b4035-130">Durum olduğunda **duraklatıldı**, duraklatma işlemi yapılır ve, artık Dwu için ücretlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4035-130">When the status is **Paused**, the pause operation is done and you are no longer being charged for DWUs.</span></span>

    ![Duraklatma durumu][4]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="b4035-132">Resume işlem</span><span class="sxs-lookup"><span data-stu-id="b4035-132">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="b4035-133">Bir veritabanı devam ettirmek için:</span><span class="sxs-lookup"><span data-stu-id="b4035-133">To resume a database:</span></span>

1. <span data-ttu-id="b4035-134">Açık [Azure portal] [ Azure portal] ve veritabanınızı açın.</span><span class="sxs-lookup"><span data-stu-id="b4035-134">Open the [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="b4035-135">Durum olduğuna dikkat edin **duraklatıldı**.</span><span class="sxs-lookup"><span data-stu-id="b4035-135">Notice that the Status is **Paused**.</span></span>

    ![Duraklatma veritabanı][4]
2. <span data-ttu-id="b4035-137">Veritabanı sürdürmek için **Başlat**, ve ardından bir onay iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b4035-137">To resume the database click **Start**, and then a confirmation message appears.</span></span> <span data-ttu-id="b4035-138">Tıklatın **Evet** onaylamak için veya **hiçbir** iptal etmek için.</span><span class="sxs-lookup"><span data-stu-id="b4035-138">Click **yes** to confirm or **no** to cancel.</span></span>

    ![Resume onaylayın][5]
3. <span data-ttu-id="b4035-140">SQL veri ambarı veritabanı başlatılırken durum "Sürdürülüyor" olur.</span><span class="sxs-lookup"><span data-stu-id="b4035-140">While SQL Data Warehouse is starting the database, the status is "Resuming".</span></span>
4. <span data-ttu-id="b4035-141">Durum olduğunda **çevrimiçi**, hazır bir veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="b4035-141">When the status is **online**, the database is ready.</span></span>

    ![Çevrimiçi durumu][6]

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="b4035-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b4035-143">Next steps</span></span>
<span data-ttu-id="b4035-144">Daha fazla bilgi için bkz: [yönetimine genel bakış][Management overview].</span><span class="sxs-lookup"><span data-stu-id="b4035-144">For more information, see [Management overview][Management overview].</span></span>

<!--Image references-->
[1]: ./media/sql-data-warehouse-manage-compute-portal/click-scale.png
[2]: ./media/sql-data-warehouse-manage-compute-portal/move-slider.png
[3]: ./media/sql-data-warehouse-manage-compute-portal/click-save.png
[4]: ./media/sql-data-warehouse-manage-compute-portal/resume-database.png
[5]: ./media/sql-data-warehouse-manage-compute-portal/resume-confirm.png
[6]: ./media/sql-data-warehouse-manage-compute-portal/pause-database.png
[7]: ./media/sql-data-warehouse-manage-compute-portal/pause-confirm.png

<!--Article references-->
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
