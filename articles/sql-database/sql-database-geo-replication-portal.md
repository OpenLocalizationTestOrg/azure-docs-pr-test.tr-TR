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
# <a name="configure-active-geo-replication-for-azure-sql-database-in-hello-azure-portal-and-initiate-failover"></a>Aktif coğrafi çoğaltma hello Azure portal ve başlatma yük devretme Azure SQL veritabanı için yapılandırma

Bu makale size nasıl gösterir tooconfigure aktif coğrafi çoğaltma SQL veritabanı için hello içinde [Azure portal](http://portal.azure.com) ve tooinitiate yük devretme.

hello Azure portal ile tooinitiate yük devretme bkz [planlanmış veya planlanmamış bir yük devretme hello Azure portal ile Azure SQL veritabanı için başlatmak](sql-database-geo-replication-portal.md).

tooconfigure aktif coğrafi hello Azure portal kullanarak çoğaltma, kaynak aşağıdaki hello gerekir:

* Azure SQL veritabanını: hello birincil veritabanı tooreplicate tooa farklı coğrafi bölge istiyor.

> [!Note]
Aktif coğrafi çoğaltma hello veritabanları arasında olmalıdır aynı abonelik.

## <a name="add-a-secondary-database"></a>İkincil bir veritabanı ekleyin
Merhaba aşağıdaki adımları yeni bir ikincil veritabanı bir coğrafi çoğaltma ortaklığı oluşturun.  

ikincil bir veritabanı tooadd hello abonelik sahibi veya ortak sahibi olmanız gerekir.

Merhaba ikincil veritabanı aynı hello birincil veritabanı olarak ad hello sahiptir ve varsa varsayılan olarak, hello aynı hizmet düzeyi. Merhaba ikincil veritabanı tek bir veritabanı veya veritabanı esnek havuzdaki olabilir. Daha fazla bilgi için bkz: [hizmet katmanları](sql-database-service-tiers.md).
Merhaba ikincil oluşturulan ve dağıtılan sonra veri hello birincil veritabanı toohello yeni ikincil veritabanından çoğaltmaya başlar.

> [!NOTE]
> (Örneğin, bir önceki coğrafi çoğaltma ilişkisi sonlandırma sonucunda) Hello ortak veritabanı zaten var. hello komutu başarısız olur.
> 

1. Merhaba, [Azure portal](http://portal.azure.com), tooset coğrafi çoğaltma için istediğiniz toohello veritabanı göz atın.
2. Merhaba SQL veritabanı sayfasında seçin **coğrafi çoğaltma**, sonra hello bölge toocreate hello ikincil veritabanını seçin. Merhaba birincil veritabanı barındırma hello bölgesi dışında herhangi bir bölgeyi seçebilirsiniz, ancak hello öneririz [eşleştirilmiş bölge](../best-practices-availability-paired-regions.md).
   
    ![Coğrafi çoğaltmayı yapılandırma](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. Seçin veya hello sunucuyu ve fiyatlandırma katmanı hello ikincil veritabanı için yapılandırın.
   
    ![İkincil yapılandırın](./media/sql-database-geo-replication-portal/create-secondary.png)
4. İsteğe bağlı olarak, ikincil veritabanı tooan esnek havuz ekleyebilirsiniz. bir havuzdaki toocreate hello ikincil veritabanını tıklatın **esnek havuz** ve hello hedef sunucu üzerindeki bir havuz seçin. Bir havuzu hello hedef sunucuda zaten mevcut olmalıdır. Bu iş akışı bir havuzu oluşturmaz.
5. Tıklatın **oluşturma** tooadd hello ikincil.
6. Merhaba ikincil veritabanı oluşturulur ve işlem dengeli hello başlar.
   
    ![İkincil yapılandırın](./media/sql-database-geo-replication-portal/seeding0.png)
7. İşlem dengeli hello tamamlandığında hello ikincil veritabanı durumunu görüntüler.
   
    ![Tam üretme](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a>Bir yük devretme başlatın

Merhaba ikincil veritabanının birincil anahtarlı toobecome hello olabilir.  

1. Merhaba, [Azure portal](http://portal.azure.com), birincil veritabanı hello coğrafi çoğaltma ortaklığı toohello göz atın.
2. Merhaba SQL veritabanı dikey penceresinde, seçin **tüm ayarları** > **coğrafi çoğaltma**.
3. Merhaba, **İKİNCİLLER** listesi, toobecome istediğiniz select hello veritabanı hello yeni birincil ve tıklayın **yük devretme**.
   
    ![Yük devretme](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. Tıklatın **Evet** toobegin hello yük devretme.

Merhaba komutu hello ikincil veritabanı hello birincil rolünde hemen geçer. 

Merhaba rolleri geçiş sırasında hangi sırasında her iki veritabanı (Merhaba 0 too25 saniye üzerinde sırasını) kullanılamaz kısa bir süre yoktur. Birden fazla ikincil veritabanları, hello komutu Hello birincil veritabanı otomatik olarak varsa, yeniden yapılandırır diğer ikincil tooconnect toohello yeni birincil hello. Merhaba tüm işlemi normal koşullarda dakika toocomplete değerinden almanız gerekir. 

> [!NOTE]
> Bu komut, bir kesinti durumunda hello veritabanının Hızlı Kurtarma için tasarlanmıştır. Yük devretme (yük devretme zorlanır) veri eşitleme tetikler.  Varsa Hello birincil çevrimiçi olduğunu ve bazı veri kaybı hello komut verildiğinde işlem yürüten ortaya çıkabilir. 
> 
> 

## <a name="remove-secondary-database"></a>İkincil veritabanını Kaldır
Bu işlem kalıcı olarak hello çoğaltma toohello ikincil veritabanı sonlandırır ve değişiklikleri hello ikincil tooa normal okuma-yazma veritabanının rolü hello. Merhaba bağlantı toohello ikincil veritabanının bozuk olması durumunda, hello komutu başarılı olur, ancak bağlantı geri yüklendikten sonra ikincil mu değil duruma okuma-yazma kadar hello.  

1. Merhaba, [Azure portal](http://portal.azure.com), birincil veritabanı hello coğrafi çoğaltma ortaklığı toohello göz atın.
2. Merhaba SQL veritabanı sayfasında seçin **coğrafi çoğaltma**.
3. Merhaba, **İKİNCİLLER** listesi, hello coğrafi çoğaltma ortaklığı gelen tooremove istediğiniz select hello veritabanı.
4. Tıklatın **çoğaltmayı durdurma**.
   
    ![İkincil Kaldır](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. Bir onay penceresi açılır. Tıklatın **Evet** tooremove hello hello coğrafi çoğaltma ortaklığı veritabanından. (Tooa okuma-yazma veritabanı tüm çoğaltma'nın parçası olmayan ayarlayın.)

## <a name="next-steps"></a>Sonraki adımlar
* Aktif coğrafi çoğaltma hakkında daha fazla toolearn bkz [aktif coğrafi çoğaltma](sql-database-geo-replication-overview.md).
* İş sürekliliğine genel bakış ve senaryolar için bkz: [iş sürekliliğine genel bakış](sql-database-business-continuity.md).

