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
# <a name="create-an-azure-sql-data-warehouse"></a>Azure SQL Data Warehouse oluşturma
> [!div class="op_single_selector"]
> * [Azure portal](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

Bu öğretici hello Azure portal toocreate AdventureWorksDW örnek veritabanı içeren bir SQL Data Warehouse kullanır.

## <a name="prerequisites"></a>Ön koşullar
başlatılan tooget, aşağıdakiler gerekir:

* **Azure hesabı**: ziyaret [Azure ücretsiz deneme sürümü] [ Azure Free Trial] veya [MSDN Azure KREDİLERİ] [ MSDN Azure Credits] toocreate bir hesap.
* **Azure SQL server**: bkz [hello Azure portal ile bir Azure SQL veritabanı oluşturma] [ Create an Azure SQL database in hello Azure portal] daha fazla ayrıntı için.

> [!NOTE]
> SQL Veri Ambarı'nın oluşturulması ek hizmet ücretlerinin alınmasına neden olabilir.  Ayrıntılı bilgi için bkz. [SQL Veri Ambarı fiyatlandırması][SQL Data Warehouse pricing].
>
>

## <a name="create-a-sql-data-warehouse"></a>SQL Data Warehouse oluşturma
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. **+ Yeni** > **Veritabanları** > **SQL Veri Ambarı**'na tıklayın.

    ![Oluştur](./media/sql-data-warehouse-get-started-provision/create-sample.gif)
3. Merhaba, **SQL Data Warehouse** dikey penceresinde, gerekli hello bilgileri doldurun, 'Oluştur' toocreate tuşuna basın.

    ![Veritabanı oluşturma](./media/sql-data-warehouse-get-started-provision/create-database.png)

   * **Sunucu**: İlk önce sunucunuzu seçmenizi öneririz.  
   * **Veritabanı adı**: kullanılan tooreference hello SQL Data Warehouse hello adı.  Benzersiz toohello sunucusu olmalıdır.
   * **Performans**: 400 [DWU][DWU] ile başlamanızı öneririz. Merhaba kaydırıcı toohello sola taşıyın veya tooadjust hello performansı veri ambarına veya ölçek yukarı veya aşağı oluşturulduktan sonra sağ.  Dwu, hakkında daha fazla toolearn gördüğünüz Belgelerimizi [ölçeklendirme](sql-data-warehouse-manage-compute-overview.md) veya bizim [fiyatlandırma sayfası][SQL Data Warehouse pricing].
   * **Abonelik**: Select hello [abonelik] , bu SQL Data Warehouse'un faturalanacağı.
   * **Kaynak grubu**: [kaynak grupları] [ Resource group] tasarlanmış kapsayıcıları toohelp Azure kaynağı koleksiyonunu yönetmek olan. [Kaynak grupları](../azure-resource-manager/resource-group-overview.md) hakkında daha fazla bilgi edinin.
   * **Kaynak seçme**: **Kaynak seç** > **Örnek** seçeneğine tıklayın. Azure otomatik olarak doldurur hello **örnek Seç** AdventureWorksDW seçeneğiyle.

   > [!NOTE]
   > SQL Data Warehouse için Hello varsayılan harmanlama sql_latin1_general_cp1_cı_as ' dir. Farklı bir harmanlama gerekirse [T-SQL] [ T-SQL] kullanılan toocreate hello veritabanı farklı bir harmanlama düzenine sahip olabilir.
   >
   >

1. Tıklatın **oluşturma** toocreate, SQL veri ambarı.
2. Birkaç dakika bekleyin. Veri ambarınız hazır olduğunda, toohello döndürülmelidir [Azure portal](https://portal.azure.com). SQL veri ambarı SQL veritabanlarınızın altında listelenen panonuz bulunamadı veya bu, kullanılan toocreate hello kaynak grubu.

    ![portal görünümü](./media/sql-data-warehouse-get-started-provision/database-portal-view.png)

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="next-steps"></a>Sonraki adımlar
SQL Data Warehouse oluşturduğunuza göre çok hazır olduğunuz[Bağlan](sql-data-warehouse-connect-overview.md) ve sorgulamaya başlayın.

SQL veri ambarında tooload verileri görmek hello [yüklemeye genel bakış](sql-data-warehouse-overview-load.md).

Merhaba toomigrate var olan bir veritabanı tooSQL veri ambarı çalışıyorsanız, bkz [geçişine genel bakış](sql-data-warehouse-overview-migrate.md) veya [geçiş yardımcı programı](sql-data-warehouse-migrate-migration-utility.md).

Güvenlik duvarı kuralları, Transact-SQL kullanarak de yapılandırılabilir. Daha fazla bilgi için bkz. [sp_set_firewall_rule][sp_set_firewall_rule] ve [sp_set_database_firewall_rule][sp_set_database_firewall_rule].

Aynı zamanda hello en iyi bir fikir toolook olan [en iyi uygulamalar][Best practices].

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
