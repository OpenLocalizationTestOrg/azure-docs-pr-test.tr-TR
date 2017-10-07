---
title: "aaaManage işlem güç Azure SQL Data warehouse'da (Azure portalı) | Microsoft Docs"
description: "Azure portal görevleri toomanage güç işlem. Dwu ayarlayarak işlem kaynaklarını ölçeklendirme. Veya, duraklatma ve sürdürme kaynakları toosave maliyetlerini işlem."
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
ms.openlocfilehash: b2e84b3763e97ce88c190eecfb64b2d06f727229
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-azure-portal"></a><span data-ttu-id="7947a-105">Azure SQL Data warehouse'da (Azure portalı) işlem güç yönetimi</span><span class="sxs-lookup"><span data-stu-id="7947a-105">Manage compute power in Azure SQL Data Warehouse (Azure portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7947a-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="7947a-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="7947a-107">Portal</span><span class="sxs-lookup"><span data-stu-id="7947a-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="7947a-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7947a-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="7947a-109">REST</span><span class="sxs-lookup"><span data-stu-id="7947a-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="7947a-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="7947a-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>


## <a name="scale-compute-power"></a><span data-ttu-id="7947a-111">Ölçek işlem gücü</span><span class="sxs-lookup"><span data-stu-id="7947a-111">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="7947a-112">toochange işlem kaynakları:</span><span class="sxs-lookup"><span data-stu-id="7947a-112">toochange compute resources:</span></span>

1. <span data-ttu-id="7947a-113">Açık hello [Azure portal][Azure portal], veritabanınızı açın ve tıklayın **ölçek**.</span><span class="sxs-lookup"><span data-stu-id="7947a-113">Open hello [Azure portal][Azure portal], open your database, and click **Scale**.</span></span>

    ![Ölçek'ı tıklatın][1]
2. <span data-ttu-id="7947a-115">Merhaba ölçek dikey penceresinde hello kaydırıcıyı sola veya toochange hello DWU ayarını sağ.</span><span class="sxs-lookup"><span data-stu-id="7947a-115">In hello Scale blade, move hello slider left or right toochange hello DWU setting.</span></span>

    ![Kaydırıcıyı taşıyın][2]
3. <span data-ttu-id="7947a-117">**Kaydet** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7947a-117">Click **Save**.</span></span> <span data-ttu-id="7947a-118">Bir onay iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="7947a-118">A confirmation message appears.</span></span> <span data-ttu-id="7947a-119">Tıklatın **Evet** tooconfirm veya **hiçbir** toocancel.</span><span class="sxs-lookup"><span data-stu-id="7947a-119">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![Kaydet’e tıklayın.][3]

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="7947a-121">Duraklatma işlem</span><span class="sxs-lookup"><span data-stu-id="7947a-121">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="7947a-122">bir veritabanı toopause:</span><span class="sxs-lookup"><span data-stu-id="7947a-122">toopause a database:</span></span>

1. <span data-ttu-id="7947a-123">Açık hello [Azure portal] [ Azure portal] ve veritabanınızı açın.</span><span class="sxs-lookup"><span data-stu-id="7947a-123">Open hello [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="7947a-124">Durum bu hello fark **çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="7947a-124">Notice that hello Status is **Online**.</span></span>

    ![Çevrimiçi durumu][6]
2. <span data-ttu-id="7947a-126">toosuspend işlem ve bellek kaynakları tıklatın **duraklatma**, ve ardından bir onay iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="7947a-126">toosuspend compute and memory resources, click **Pause**, and then a confirmation message appears.</span></span> <span data-ttu-id="7947a-127">Tıklatın **Evet** tooconfirm veya **hiçbir** toocancel.</span><span class="sxs-lookup"><span data-stu-id="7947a-127">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![Duraklatma onaylayın][7]
3. <span data-ttu-id="7947a-129">SQL veri ambarı hello veritabanı başlatılırken hello durumudur **duraklatma**.</span><span class="sxs-lookup"><span data-stu-id="7947a-129">While SQL Data Warehouse is starting hello database, hello status is **Pausing**.</span></span>
4. <span data-ttu-id="7947a-130">Merhaba durum olduğunda **duraklatıldı**hello duraklatma işlemi yapılır ve, artık Dwu için ücretlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7947a-130">When hello status is **Paused**, hello pause operation is done and you are no longer being charged for DWUs.</span></span>

    ![Duraklatma durumu][4]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="7947a-132">Resume işlem</span><span class="sxs-lookup"><span data-stu-id="7947a-132">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="7947a-133">bir veritabanı tooresume:</span><span class="sxs-lookup"><span data-stu-id="7947a-133">tooresume a database:</span></span>

1. <span data-ttu-id="7947a-134">Açık hello [Azure portal] [ Azure portal] ve veritabanınızı açın.</span><span class="sxs-lookup"><span data-stu-id="7947a-134">Open hello [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="7947a-135">Durum bu hello fark **duraklatıldı**.</span><span class="sxs-lookup"><span data-stu-id="7947a-135">Notice that hello Status is **Paused**.</span></span>

    ![Duraklatma veritabanı][4]
2. <span data-ttu-id="7947a-137">tooresume hello veritabanı tıklatın **Başlat**, ve ardından bir onay iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="7947a-137">tooresume hello database click **Start**, and then a confirmation message appears.</span></span> <span data-ttu-id="7947a-138">Tıklatın **Evet** tooconfirm veya **hiçbir** toocancel.</span><span class="sxs-lookup"><span data-stu-id="7947a-138">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![Resume onaylayın][5]
3. <span data-ttu-id="7947a-140">SQL veri ambarı hello veritabanı başlatılırken hello durum "Sürdürülüyor" olur.</span><span class="sxs-lookup"><span data-stu-id="7947a-140">While SQL Data Warehouse is starting hello database, hello status is "Resuming".</span></span>
4. <span data-ttu-id="7947a-141">Merhaba durum olduğunda **çevrimiçi**, hello veritabanı hazır.</span><span class="sxs-lookup"><span data-stu-id="7947a-141">When hello status is **online**, hello database is ready.</span></span>

    ![Çevrimiçi durumu][6]

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="7947a-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7947a-143">Next steps</span></span>
<span data-ttu-id="7947a-144">Daha fazla bilgi için bkz: [yönetimine genel bakış][Management overview].</span><span class="sxs-lookup"><span data-stu-id="7947a-144">For more information, see [Management overview][Management overview].</span></span>

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
