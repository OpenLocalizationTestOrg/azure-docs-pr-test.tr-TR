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
# <a name="manage-compute-power-in-azure-sql-data-warehouse-azure-portal"></a>Azure SQL Data warehouse'da (Azure portalı) işlem güç yönetimi
> [!div class="op_single_selector"]
> * [Genel Bakış](sql-data-warehouse-manage-compute-overview.md)
> * [Portal](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>


## <a name="scale-compute-power"></a>Ölçek işlem gücü
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

toochange işlem kaynakları:

1. Açık hello [Azure portal][Azure portal], veritabanınızı açın ve tıklayın **ölçek**.

    ![Ölçek'ı tıklatın][1]
2. Merhaba ölçek dikey penceresinde hello kaydırıcıyı sola veya toochange hello DWU ayarını sağ.

    ![Kaydırıcıyı taşıyın][2]
3. **Kaydet** düğmesine tıklayın. Bir onay iletisi görüntülenir. Tıklatın **Evet** tooconfirm veya **hiçbir** toocancel.

    ![Kaydet’e tıklayın.][3]

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>Duraklatma işlem
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

bir veritabanı toopause:

1. Açık hello [Azure portal] [ Azure portal] ve veritabanınızı açın. Durum bu hello fark **çevrimiçi**.

    ![Çevrimiçi durumu][6]
2. toosuspend işlem ve bellek kaynakları tıklatın **duraklatma**, ve ardından bir onay iletisi görüntülenir. Tıklatın **Evet** tooconfirm veya **hiçbir** toocancel.

    ![Duraklatma onaylayın][7]
3. SQL veri ambarı hello veritabanı başlatılırken hello durumudur **duraklatma**.
4. Merhaba durum olduğunda **duraklatıldı**hello duraklatma işlemi yapılır ve, artık Dwu için ücretlendirilirsiniz.

    ![Duraklatma durumu][4]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>Resume işlem
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

bir veritabanı tooresume:

1. Açık hello [Azure portal] [ Azure portal] ve veritabanınızı açın. Durum bu hello fark **duraklatıldı**.

    ![Duraklatma veritabanı][4]
2. tooresume hello veritabanı tıklatın **Başlat**, ve ardından bir onay iletisi görüntülenir. Tıklatın **Evet** tooconfirm veya **hiçbir** toocancel.

    ![Resume onaylayın][5]
3. SQL veri ambarı hello veritabanı başlatılırken hello durum "Sürdürülüyor" olur.
4. Merhaba durum olduğunda **çevrimiçi**, hello veritabanı hazır.

    ![Çevrimiçi durumu][6]

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi için bkz: [yönetimine genel bakış][Management overview].

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
