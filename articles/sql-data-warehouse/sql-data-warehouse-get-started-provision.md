---
title: "aaaCreate hello Azure portal'ın SQL Data Warehouse | Microsoft Docs"
description: "Azure SQL Data Warehouse'da bir toocreate hello Azure portalına nasıl öğrenin"
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: 552e496e-d560-419c-9996-6bbc80c521cb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: f5be6e3f2936e3af9d099854a468f8ce66fd8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-sql-data-warehouse"></a><span data-ttu-id="9f6f9-103">Azure SQL Data Warehouse oluşturma</span><span class="sxs-lookup"><span data-stu-id="9f6f9-103">Create an Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9f6f9-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="9f6f9-104">Azure portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="9f6f9-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="9f6f9-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="9f6f9-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f6f9-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="9f6f9-107">Bu öğretici hello Azure portal toocreate AdventureWorksDW örnek veritabanı içeren bir SQL Data Warehouse kullanır.</span><span class="sxs-lookup"><span data-stu-id="9f6f9-107">This tutorial uses hello Azure portal toocreate a SQL Data Warehouse that contains an AdventureWorksDW sample database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f6f9-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9f6f9-108">Prerequisites</span></span>
<span data-ttu-id="9f6f9-109">başlatılan tooget, aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="9f6f9-109">tooget started, you need:</span></span>

* <span data-ttu-id="9f6f9-110">**Azure hesabı**: ziyaret [Azure ücretsiz deneme sürümü] [ Azure Free Trial] veya [MSDN Azure KREDİLERİ] [ MSDN Azure Credits] toocreate bir hesap.</span><span class="sxs-lookup"><span data-stu-id="9f6f9-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] toocreate an account.</span></span>
* <span data-ttu-id="9f6f9-111">**Azure SQL server**: bkz [hello Azure portal ile bir Azure SQL veritabanı oluşturma] [ Create an Azure SQL database in hello Azure portal] daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="9f6f9-111">**Azure SQL server**:  See [Create an Azure SQL database with hello Azure portal][Create an Azure SQL database in hello Azure portal] for more details.</span></span>

> [!NOTE]
> <span data-ttu-id="9f6f9-112">SQL Veri Ambarı'nın oluşturulması ek hizmet ücretlerinin alınmasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="9f6f9-112">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="9f6f9-113">Ayrıntılı bilgi için bkz. [SQL Veri Ambarı fiyatlandırması][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="9f6f9-113">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="9f6f9-114">SQL Data Warehouse oluşturma</span><span class="sxs-lookup"><span data-stu-id="9f6f9-114">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="9f6f9-115">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9f6f9-115">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9f6f9-116">**+ Yeni** > **Veritabanları** > **SQL Veri Ambarı**'na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9f6f9-116">Click **+ New** > **Databases** > **SQL Data Warehouse**.</span></span>

    ![Oluştur](./media/sql-data-warehouse-get-started-provision/create-sample.gif)
3. <span data-ttu-id="9f6f9-118">Merhaba, **SQL Data Warehouse** dikey penceresinde, gerekli hello bilgileri doldurun, 'Oluştur' toocreate tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="9f6f9-118">In hello **SQL Data Warehouse** blade, fill in hello information needed, then press 'Create' toocreate.</span></span>

    ![Veritabanı oluşturma](./media/sql-data-warehouse-get-started-provision/create-database.png)

   * <span data-ttu-id="9f6f9-120">**Sunucu**: İlk önce sunucunuzu seçmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="9f6f9-120">**Server**: We recommend you select your server first.</span></span>  
   * <span data-ttu-id="9f6f9-121">**Veritabanı adı**: kullanılan tooreference hello SQL Data Warehouse hello adı.</span><span class="sxs-lookup"><span data-stu-id="9f6f9-121">**Database name**: hello name that is used tooreference hello SQL Data Warehouse.</span></span>  <span data-ttu-id="9f6f9-122">Benzersiz toohello sunucusu olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9f6f9-122">It must be unique toohello server.</span></span>
   * <span data-ttu-id="9f6f9-123">**Performans**: 400 [DWU][DWU] ile başlamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="9f6f9-123">**Performance**: We recommend starting with 400 [DWUs][DWU].</span></span> <span data-ttu-id="9f6f9-124">Merhaba kaydırıcı toohello sola taşıyın veya tooadjust hello performansı veri ambarına veya ölçek yukarı veya aşağı oluşturulduktan sonra sağ.</span><span class="sxs-lookup"><span data-stu-id="9f6f9-124">You can move hello slider toohello left or right tooadjust hello performance of your data warehouse, or scale up or down after creation.</span></span>  <span data-ttu-id="9f6f9-125">Dwu, hakkında daha fazla toolearn gördüğünüz Belgelerimizi [ölçeklendirme](sql-data-warehouse-manage-compute-overview.md) veya bizim [fiyatlandırma sayfası][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="9f6f9-125">toolearn more about DWUs, see our documentation on [scaling](sql-data-warehouse-manage-compute-overview.md) or our [pricing page][SQL Data Warehouse pricing].</span></span>
   * <span data-ttu-id="9f6f9-126">**Abonelik**: Select hello [abonelik] , bu SQL Data Warehouse'un faturalanacağı.</span><span class="sxs-lookup"><span data-stu-id="9f6f9-126">**Subscription**: Select hello [subscription] that this SQL Data Warehouse will bill to.</span></span>
   * <span data-ttu-id="9f6f9-127">**Kaynak grubu**: [kaynak grupları] [ Resource group] tasarlanmış kapsayıcıları toohelp Azure kaynağı koleksiyonunu yönetmek olan.</span><span class="sxs-lookup"><span data-stu-id="9f6f9-127">**Resource group**: [Resource groups][Resource group] are containers designed toohelp you manage a collection of Azure resources.</span></span> <span data-ttu-id="9f6f9-128">[Kaynak grupları](../azure-resource-manager/resource-group-overview.md) hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="9f6f9-128">Learn more about [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="9f6f9-129">**Kaynak seçme**: **Kaynak seç** > **Örnek** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9f6f9-129">**Select source**: Click **Select source** > **Sample**.</span></span> <span data-ttu-id="9f6f9-130">Azure otomatik olarak doldurur hello **örnek Seç** AdventureWorksDW seçeneğiyle.</span><span class="sxs-lookup"><span data-stu-id="9f6f9-130">Azure automatically populates hello **Select sample** option with AdventureWorksDW.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9f6f9-131">SQL Data Warehouse için Hello varsayılan harmanlama sql_latin1_general_cp1_cı_as ' dir.</span><span class="sxs-lookup"><span data-stu-id="9f6f9-131">hello default collation for a SQL Data Warehouse is SQL_Latin1_General_CP1_CI_AS.</span></span> <span data-ttu-id="9f6f9-132">Farklı bir harmanlama gerekirse [T-SQL] [ T-SQL] kullanılan toocreate hello veritabanı farklı bir harmanlama düzenine sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="9f6f9-132">If a different collation is needed, [T-SQL][T-SQL] can be used toocreate hello database with a different collation.</span></span>
   >
   >

1. <span data-ttu-id="9f6f9-133">Tıklatın **oluşturma** toocreate, SQL veri ambarı.</span><span class="sxs-lookup"><span data-stu-id="9f6f9-133">Click **Create** toocreate your SQL Data Warehouse.</span></span>
2. <span data-ttu-id="9f6f9-134">Birkaç dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="9f6f9-134">Wait for a few minutes.</span></span> <span data-ttu-id="9f6f9-135">Veri ambarınız hazır olduğunda, toohello döndürülmelidir [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9f6f9-135">When your data warehouse is ready, you should be returned toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9f6f9-136">SQL veri ambarı SQL veritabanlarınızın altında listelenen panonuz bulunamadı veya bu, kullanılan toocreate hello kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="9f6f9-136">You can find your SQL Data Warehouse on your dashboard, listed under your SQL Databases, or in hello resource group that you used toocreate it.</span></span>

    ![portal görünümü](./media/sql-data-warehouse-get-started-provision/database-portal-view.png)

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="9f6f9-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9f6f9-138">Next steps</span></span>
<span data-ttu-id="9f6f9-139">SQL Data Warehouse oluşturduğunuza göre çok hazır olduğunuz[Bağlan](sql-data-warehouse-connect-overview.md) ve sorgulamaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="9f6f9-139">Now that you have created a SQL Data Warehouse, you are ready too[Connect](sql-data-warehouse-connect-overview.md) and begin querying.</span></span>

<span data-ttu-id="9f6f9-140">SQL veri ambarında tooload verileri görmek hello [yüklemeye genel bakış](sql-data-warehouse-overview-load.md).</span><span class="sxs-lookup"><span data-stu-id="9f6f9-140">tooload data into SQL Data Warehouse, see hello [loading overview](sql-data-warehouse-overview-load.md).</span></span>

<span data-ttu-id="9f6f9-141">Merhaba toomigrate var olan bir veritabanı tooSQL veri ambarı çalışıyorsanız, bkz [geçişine genel bakış](sql-data-warehouse-overview-migrate.md) veya [geçiş yardımcı programı](sql-data-warehouse-migrate-migration-utility.md).</span><span class="sxs-lookup"><span data-stu-id="9f6f9-141">If you are trying toomigrate an existing database tooSQL Data Warehouse, see hello [Migration overview](sql-data-warehouse-overview-migrate.md) or use [Migration Utility](sql-data-warehouse-migrate-migration-utility.md).</span></span>

<span data-ttu-id="9f6f9-142">Güvenlik duvarı kuralları, Transact-SQL kullanarak de yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="9f6f9-142">Firewall rules can also be configured using Transact-SQL.</span></span> <span data-ttu-id="9f6f9-143">Daha fazla bilgi için bkz. [sp_set_firewall_rule][sp_set_firewall_rule] ve [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span><span class="sxs-lookup"><span data-stu-id="9f6f9-143">For more information, see [sp_set_firewall_rule][sp_set_firewall_rule] and [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span></span>

<span data-ttu-id="9f6f9-144">Aynı zamanda hello en iyi bir fikir toolook olan [en iyi uygulamalar][Best practices].</span><span class="sxs-lookup"><span data-stu-id="9f6f9-144">It's also a great idea toolook at hello [Best practices][Best practices].</span></span>

<!--Article references-->
[Create an Azure SQL database in hello Azure portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[resource groups]: ../azure-resource-manager/resource-group-template-deploy-portal.md
[Best practices]: sql-data-warehouse-best-practices.md
[DWU]: sql-data-warehouse-overview-what-is.md
[abonelik]: ../azure-glossary-cloud-terminology.md#subscription
[resource group]: ../azure-glossary-cloud-terminology.md#resource-group
[T-SQL]: ./sql-data-warehouse-get-started-create-database-tsql.md

<!--MSDN references-->
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
