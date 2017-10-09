---
title: "aaaMonitoring & performans ayarlama - Azure SQL veritabanı | Microsoft Docs"
description: "Azure SQL veritabanı'nda ayarlama değerlendirme ve geliştirme performans ipuçları."
services: sql-database
documentationcenter: 
author: v-shysun
manager: felixwu
editor: 
keywords: "sql performans ayarlama, veritabanı performans ayarlama, sql performans ipuçları, ayarlama sql veritabanı performans ayarlama"
ms.assetid: eb7b3f66-3b33-4e1b-84fb-424a928a6672
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: v-shysun
ms.openlocfilehash: 9e196831902aa6ea841ef14caf5713e82ebfc62d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-and-performance-tuning"></a>İzleme ve performans ayarlama

Azure SQL veritabanı otomatik olarak yönetilir ve burada kolayca kullanımı izlemek, ekleyin veya kaynakları (CPU, bellek, g/ç) kaldırmak esnek veri hizmeti veritabanınızın performansını veya tooyour iş yüküne uyum veritabanı izin önerileri bulun ve otomatik olarak performansını iyileştirin.

Bu makalede izleme ve performans Azure SQL veritabanı'nda kullanılabilen seçenekleri ayarlama genel bakış sağlar.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="monitoring-and-troubleshooting-database-performance"></a>İzleme ve veritabanı performans sorunlarını giderme

Tooeasily veritabanı kullanımını izlemek ve hello performans sorunlarına neden sorguları tanımlamak, azure SQL veritabanı sağlar. Azure portal veya sistem görünümleri kullanarak veritabanı performansını izleyebilirsiniz. İzleme ve veritabanı performans sorunlarını giderme seçenekleri aşağıdaki hello vardır:

1. Merhaba, [Azure portal](https://portal.azure.com), tıklatın **SQL veritabanları**, hello veritabanı seçin ve ardından hello izleme grafik toolook kendi maksimum yaklaşan kaynaklar için kullanın. DTU tüketimi varsayılan olarak gösterilir. Tıklatın **Düzenle** toochange hello zaman aralığı ve gösterilen değerleri.
2. Kullanım [sorgu performansı öngörüleri](sql-database-query-performance.md) harcamanız tooidentify hello sorguları hello en kaynakların.
3. Dinamik Yönetim görünümlerini (Dmv'leri), genişletilmiş olaylar kullanabilirsiniz (`XEvents`), ve SSMS tooget performans parametrelerinde gerçek zamanlı sorgu deposu hello.

Merhaba bkz [performans Kılavuzu konu](sql-database-performance-guidance.md) toofind teknikleri bu raporları veya görünümleri kullanarak bazı sorun belirlerseniz Azure SQL veritabanı performansını tooimprove kullanabilirsiniz.

> [!IMPORTANT] 
> Her zaman hello kullanmanız önerilir Management Studio tooremain en son sürümünü Azure ve SQL veritabanı güncelleştirmeleri tooMicrosoft ile eşitlenir. [SQL Server Management Studio’yu güncelleyin](https://msdn.microsoft.com/library/mt238290.aspx).
>

## <a name="optimize-database-tooimprove-performance"></a>Veritabanı tooimprove performansı en iyi duruma getirme

Azure SQL veritabanı tooidentify fırsatları tooimprove etkinleştirir ve kaynakları gözden geçirerek değiştirmeden Sorgu performansı en iyi duruma getirme [performans ayarlama önerileri](sql-database-advisor.md). Veritabanı performansının düşük olmasına yol açan yaygın nedenler, dizinlerin eksik olması ve sorguların hatalı bir şekilde iyileştirilmesidir. İş yükünüzün ayarlama bu önerileri tooimprove performansını uygulayabilirsiniz.
Let Azure SQL veritabanı çok kullanabileceğiniz[otomatik olarak Sorgularınızın performansını en iyi duruma](sql-database-automatic-tuning.md) uygulayarak tüm öneriler ve bunlar veritabanı performansını iyileştirmek doğrulama tanımlanır. Veritabanınızın seçenekleri tooimprove performansını izleyen hello kullanabilirsiniz:

1. Kullanım [SQL veritabanı Danışmanı](sql-database-advisor-portal.md) tooview önerileri oluşturma ve dizinleri bırakmayı, sorguları kümesini parametreleştirme ve şema sorunlarını giderme.
2. [Otomatik ayarlamayı etkinleştirmek](sql-database-automatic-tuning-enable.md) ve Azure otomatik olarak tanımlanan düzeltme performans sorunlarını veritabanı SQL izin verin.

## <a name="improving-database-performance-with-more-resources"></a>Daha fazla kaynak ile veritabanı performansı iyileştirme

Son olarak, veritabanınızın performansını artırabilir hiçbir işlem yapılabilir öğeler varsa, Azure SQL veritabanı'nda kullanılabilen kaynakları hello miktarını değiştirebilirsiniz. Daha fazla kaynak hello değiştirerek atayabilirsiniz [hizmet katmanı](sql-database-service-tiers.md) , bir tek başına veritabanı veya herhangi bir anda bir esnek havuz edtu hello'larını artırın.
1. Tek başına veritabanları için şunları yapabilirsiniz [hizmet katmanları değiştirmek](sql-database-service-tiers.md) isteğe bağlı tooimprove veritabanı performansı.
2. Birden çok veritabanı için kullanmayı [esnek havuzlar](sql-database-elastic-pool-guidance.md) tooscale kaynakları otomatik olarak.

## <a name="tune-and-refactor-application-or-database-code"></a>Ayarlama ve düzenleme uygulama veya veritabanı kodu

Uygulama kodu toomore en iyi şekilde değiştirebilirsiniz hello veritabanı, dizinleri değiştirmek, planları zorla veya toomanually uyum hello veritabanı tooyour iş yükü ipuçlarını kullanın. El ile ayarlama ve hello hello kodu yeniden yazma işlemi için bazı yönergeler ve ipuçları bulmak [performans Kılavuzu konu](sql-database-performance-guidance.md) makalesi.


## <a name="next-steps"></a>Sonraki adımlar

- tooenable ayarlama Azure SQL veritabanı ve let otomatik otomatik ayarı özelliğini tam olarak İş yükünüzün yönetmek için bkz: [otomatik ayarlamayı etkinleştirmek](sql-database-automatic-tuning-enable.md).
- toouse el ile ayarlama, gözden geçirebilirsiniz [önerileri Azure portalında ayarlama](sql-database-advisor-portal.md) ve el ile Merhaba sorgularınızı performansını olanları uygulayın.
- Değiştirme, değiştirerek, veritabanında mevcut olan kaynaklar [Azure SQL Database hizmet katmanları](sql-database-performance-guidance.md)