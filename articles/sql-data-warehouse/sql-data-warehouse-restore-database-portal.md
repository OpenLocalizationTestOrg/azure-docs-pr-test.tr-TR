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
# <a name="restore-azure-sql-data-warehouse-portal"></a>Azure SQL Data Warehouse (portal) geri yükleme
> [!div class="op_single_selector"]
> * [Genel bakış][Overview]
> * [Portal][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
>
>
Bu makalede, Azure portal kullanarak Azure SQL Data Warehouse toorestore hello nasıl öğreneceksiniz.

## <a name="before-you-begin"></a>Başlamadan önce
**DTU kapasitenizi doğrulayın.** SQL veri ambarı her bir örneğini varsayılan veri işleme birimi (DTU) kota olan bir SQL server tarafından (örneğin, myserver.database.windows.net) barındırılıyor. SQL veri ambarı geri yüklemeden önce SQL server'ınızdaki geri yüklemekte hello veritabanı için yeterli kalan DTU kota sahip olduğunu doğrulayın. toolearn toocalculate DTU kota veya toorequest daha fazla Dtu'lar nasıl görürüm [DTU kota değişiklik isteği][Request a DTU quota change].

## <a name="restore-an-active-or-paused-database"></a>Etkin ya da duraklatılmış bir veritabanını geri yükle
bir veritabanı toorestore:

1. İçinde toohello oturum [Azure portal][Azure portal].
2. Merhaba sol bölmesinde seçin **Gözat**ve ardından **SQL sunucuları**.

    ![Gözat seçin > SQL Server'lar](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. Sunucunuz bulun ve seçin.

    ![Sunucunuzu seçin](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. SQL veri ambarı Hello örneğini toorestore gelen istediğiniz ve seçin bulun.

    ![SQL veri ambarı toorestore Hello örneğini seçin](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. Merhaba veri ambarı dikey penceresinde Hello üstünde seçin **geri**.

    ![Geri yükleme seçin](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. Yeni bir belirtin **veritabanı adı**.
7. Son SELECT hello **geri yükleme noktası**.

   Merhaba en son geri yükleme noktası seçtiğinizden emin olun. Geri yükleme noktaları Eşgüdümlü Evrensel Saat (UTC) gösterilir çünkü hello varsayılan seçeneği hello en son geri yükleme noktası olmayabilir.

      ![Bir geri yükleme noktası seçin](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. **Tamam**’ı seçin.
9. Merhaba veritabanı geri yükleme işlemi başlayacak ve kullanabileceğiniz **bildirimleri** toomonitor hello işlemi.

> [!NOTE]
> Merhaba geri yükleme tamamlandıktan sonra izleyerek, kurtarılan veritabanının yapılandırabilirsiniz [kurtarma işleminden sonra veritabanını yapılandırma][Configure your database after recovery].
>
>

## <a name="restore-a-deleted-database"></a>Silinen veritabanını geri yükleme
Silinen bir veritabanını toorestore:

1. İçinde toohello oturum [Azure portal][Azure portal].
2. Merhaba sol bölmesinde seçin **Gözat**ve ardından **SQL sunucuları**.

    ![Gözat seçin > SQL Server'lar](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. Sunucunuz bulun ve seçin.

    ![Sunucunuzu seçin](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. Toohello aşağı **Operations** sunucunuzun dikey bölüm.
5. Select hello **veritabanlarını sildi** döşeme.

    ![Merhaba silinen veritabanları kutucuk seçin](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. Silinen hello veritabanını toorestore istediğinizi seçin.

    ![Bir veritabanı toorestore seçin](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. Yeni bir belirtin **veritabanı adı**.

    ![Merhaba veritabanı için bir ad ekleyin](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. **Tamam**’ı seçin.
9. Merhaba veritabanı geri yükleme işlemi başlayacak ve kullanabileceğiniz **bildirimleri** toomonitor hello işlemi.

> [!NOTE]
> Merhaba geri yükleme tamamlandıktan sonra veritabanınızı tooconfigure bkz [kurtarma işleminden sonra veritabanını yapılandırma][Configure your database after recovery].
>
>

## <a name="next-steps"></a>Sonraki adımlar
Merhaba okuma Azure SQL veritabanı sürümlerinin hello iş sürekliliği özellikleri hakkında toolearn [Azure SQL Database iş sürekliliğine genel bakış][Azure SQL Database business continuity overview].

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
