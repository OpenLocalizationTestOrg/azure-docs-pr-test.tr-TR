---
title: "aaaStore Azure SQL veritabanı yedeklemeleri için too10 yıl ayarlama | Microsoft Docs"
description: "Azure SQL veritabanı depolanmasını yedekler too10 yıl nasıl destekler? öğrenin."
keywords: 
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 66fdb8b8-5903-4d3a-802e-af08d204566e
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 12/22/2016
ms.author: sashan
ms.openlocfilehash: 5825ebd4e3bd66b59b13aea603d377ef814a1df3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="store-azure-sql-database-backups-for-up-too10-years"></a>Too10 yıl yedeklemek için Azure SQL veritabanı yedeklemelerini depolamak
Birçok uygulama yasal varsa, uyumluluk ya da diğer iş amaçlı gerektiren tooretain veritabanı yedeklemeleri hello ötesinde 7-35 gün Azure SQL veritabanı tarafından sağlanan [otomatik yedeklemeler](sql-database-automated-backups.md). Merhaba uzun vadeli yedekleme bekletme özelliğini kullanarak, bir Azure kurtarma Hizmetleri kasasını için too10 yıl içinde SQL veritabanı yedeklerinizi depolayabilirsiniz. Too1, kasa başına 000 veritabanlarını yedeklemek depolayabilirsiniz. Ardından herhangi bir yedekleme hello kasa toorestore seçebileceğiniz yeni bir veritabanı olarak.

> [!IMPORTANT]
> Uzun vadeli yedekleme bekletme olduğundan şu anda önizlemede ve bölgeler aşağıdaki hello kullanılabilir: Avustralya Doğu, Avustralya Güneydoğu, Brezilya Güney, Orta ABD, Doğu Asya, Doğu ABD, Doğu ABD 2, Hindistan Orta, Hindistan Güney, Japonya Doğu, Japonya Batı, Kuzey Orta ABD, Kuzey Avrupa, Orta Güney ABD, Güneydoğu Asya, Batı Avrupa ve Batı ABD.
>

> [!NOTE]
> Kasa başına too200 veritabanlarını 24 saatlik dönem boyunca etkinleştirebilirsiniz. Her sunucu toominimize hello etkisini bu sınır için ayrı bir kasa kullanmanızı öneririz. 
> 

## <a name="how-sql-database-long-term-backup-retention-works"></a>SQL veritabanı uzun vadeli yedekleme bekletme nasıl çalışır?

Uzun vadeli yedekleme bekletme ile bir SQL veritabanı sunucusuna Azure kurtarma Hizmetleri kasası ile ilişkilendirebilirsiniz. 

* Merhaba kasası oluşturmanız gerekir hello hello SQL server oluşturulan aynı Azure aboneliği ve de aynı hello coğrafi bölge ve kaynak grubu. 
* Ardından, herhangi bir veritabanı için bir bekletme ilkesi de yapılandırın. Hello İlkesi nedenler hello haftalık tam veritabanı yedeklemeleri toobe toohello kurtarma Hizmetleri kasası kopyalanır ve hello belirtilen saklama dönemini (too10 yıl) korunur. 
* Ardından, bu yedeklemeler tooa yeni veritabanı hello abonelik herhangi bir sunucuya birinden hello veritabanını geri yükleyebilirsiniz. Azure depolama mevcut yedeklerden bir kopyasını oluşturur ve hello kopyalama performans hello varolan veritabanı üzerinde bir etkisi yoktur.

> [!TIP]
> Bir nasıl tooguide için bkz: [yapılandırma ve Azure SQL veritabanı uzun vadeli yedekleme bekletme geri](sql-database-long-term-backup-retention-configure.md).

## <a name="enable-long-term-backup-retention"></a>Uzun vadeli yedekleme bekletme etkinleştir

bir veritabanı için uzun vadeli yedekleme bekletme tooconfigure:

1. Hello bir Azure kurtarma Hizmetleri kasası oluşturma, SQL veritabanı sunucusu olarak aynı bölge, abonelik ve kaynak grubu. 
2. Merhaba sunucu toohello kasaya kaydedin.
3. Bir Azure kurtarma Hizmetleri koruma ilkesi oluşturun.
4. Uzun vadeli yedekleme bekletme gerektiren hello koruma İlkesi toohello veritabanları uygulayın.

tooconfigure, Yönet'i ve bir Azure kurtarma Hizmetleri kasası Otomatik yedeklemelerin uzun vadeli yedekleme bekletme bir veritabanını geri, hello aşağıdakilerden birini yapın:

* Hello Azure portal kullanarak: tıklatın **uzun vadeli yedekleme bekletme**, bir veritabanı seçin ve ardından **yapılandırma**. 

   ![Uzun vadeli yedekleme bekletme için bir veritabanı seçin](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

* PowerShell kullanarak: çok Git[yapılandırma ve Azure SQL veritabanı uzun vadeli yedekleme bekletme geri](sql-database-long-term-backup-retention-configure.md).

## <a name="restore-a-database-thats-stored-with-hello-long-term-backup-retention-feature"></a>Merhaba uzun vadeli yedekleme bekletme özelliğiyle depolanan bir veritabanını geri yükle

uzun vadeli yedekleme bekletme yedekten toorecover:

1. Liste hello kasası hello yedekleme depolandığı.
2. Eşlenen tooyour mantıksal sunucu listesi hello kapsayıcı.
3. Eşlenen tooyour veritabanı hello kasa içinde listesi hello veri kaynağı.
4. Kullanılabilir toorestore listesi hello kurtarma noktalarını.
5. Merhaba kurtarma noktası toohello hedef sunucudan aboneliğinizi içinde Hello veritabanını geri yükleyin.

tooconfigure, Yönet'i ve bir Azure kurtarma Hizmetleri kasası Otomatik yedeklemelerin uzun vadeli yedekleme bekletme bir veritabanını geri, hello aşağıdakilerden birini yapın:

* Hello Azure portal kullanarak: çok Git[hello Azure portalı Yönet uzun vadeli yedekleme bekletme kullanarak](sql-database-long-term-backup-retention-configure.md). 

* PowerShell kullanarak: çok Git[uzun vadeli yedekleme bekletme PowerShell kullanarak yönetme](sql-database-long-term-backup-retention-configure.md).

## <a name="get-pricing-for-long-term-backup-retention"></a>Uzun vadeli yedekleme bekletme için fiyatlandırma Al

SQL veritabanı uzun vadeli yedekleme bekletme ücret toohello göre [oranları fiyatlandırma Azure yedekleme Hizmetleri](https://azure.microsoft.com/pricing/details/backup/).

Merhaba SQL veritabanı sunucusuna kayıtlı toohello kasası sonra hello kasasında depolanan hello haftalık yedekleri tarafından kullanılan toplam depolama hello için ücretlendirilirsiniz.

## <a name="view-available-backups-that-are-stored-in-long-term-backup-retention"></a>Uzun vadeli yedekleme bekletme içinde depolanan kullanılabilir yedekleri görüntüle

tooconfigure, Yönet'i ve hello Azure portal kullanarak bir veritabanını bir Azure kurtarma Hizmetleri kasası Otomatik yedeklemelerin uzun vadeli yedekleme bekletme geri, hello aşağıdakilerden birini yapın:

* Hello Azure portal kullanarak: çok Git[hello Azure portalı Yönet uzun vadeli yedekleme bekletme kullanarak](sql-database-long-term-backup-retention-configure.md). 

* PowerShell kullanarak: çok Git[uzun vadeli yedekleme bekletme PowerShell kullanarak yönetme](sql-database-long-term-backup-retention-configure.md).

## <a name="disable-long-term-retention"></a>Uzun vadeli bekletme devre dışı bırak

Merhaba kurtarma hizmeti üzerinde bekletme ilkesi sağlanan hello bağlı olarak yedeklemeler hello temizlenmesi otomatik olarak yönetir. 

belirli veritabanı toohello kasa için gönderen hello yedeklemeleri toostop hello bekletme ilkesi bu veritabanı için kaldırın.
  
```
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName 'RG1' -ServerName 'Server1' -DatabaseName 'DB1' -State 'Disabled' -ResourceId $policy.Id
```

> [!NOTE]
> Merhaba kasasına zaten olan hello yedeklemeleri etkilenmez. Kendi saklama süresi sona erdiğinde, bunlar hello kurtarma hizmeti tarafından otomatik olarak silinir.

## <a name="long-term-backup-retention-faq"></a>Uzun vadeli yedekleme bekletme SSS

**El ile de hello kasasında belirli yedeklemelerinize silebilmek için?**

Şu anda değil. Merhaba saklama süresi sona erdiğinde hello kasası yedekler otomatik olarak temizlenir.

**My server toostore yedeklemeleri toomore bir kasa daha kayıt mi?**

Hayır, aynı anda yedeklemeleri tooonly bir kasa şu anda depolayabilirsiniz.

**Farklı Aboneliklerde kasası ve sunucu olabilir?**

Merhaba kasası ve sunucu hello Hayır, şu anda olmalıdır aynı abonelik ve kaynak grubu.

**I my sunucunun bölgesinden farklı bir bölgede oluşturulan bir kasa kullanabilir miyim?**

Hayır, hello kasası ve sunucu olmalıdır hello aynı bölge toominimize zaman kopyalayın ve trafiği ücretlere kaçının.

**Kaç tane veritabanları t bir kasaya depolayabilir miyim?**

Şu anda too1, kasa başına 000 veritabanlarını yedeklemek destekliyoruz. 

**Abonelik başına kaç tane kasalarını oluşturabilirim?**

Abonelik başına too25 kasa oluşturabilirsiniz.

**Kasa başına günde kaç tane veritabanları yapılandırabilir miyim?**

Günde bir kasa başına 200 veritabanları ayarlayabilirsiniz.

**Uzun vadeli yedekleme bekletme esnek havuzları ile çalışır mı?**

Evet. Herhangi bir veritabanı hello havuzunda hello bekletme ilkesi ile yapılandırılabilir.

**Merhaba yedekleme oluşturulduğu hello zaman seçebilir miyim?**

Hayır, SQL veritabanı hello yedekleme zamanlaması toominimize hello performans etkisini veritabanlarınızı denetler.

**Saydam veri şifreleme için veritabanı etkin var. Bunu hello kasayla kullanabilir miyim?** 

Evet, saydam veri şifreleme desteklenir. Merhaba özgün veritabanı artık mevcut olsa bile hello kasadan hello veritabanını geri yükleyebilirsiniz.

**Aboneliğimi askıya alınırsa hello kasasında hello yedeklemeleri ile ne olur?** 

Aboneliğiniz askıya alınırsa hello varolan veritabanları ve yedeklemeleri korur. Yeni yedeklemeler kopyalanan toohello kasası olup olmadığı. Merhaba aboneliği yeniden sonra hello hizmet yedeklemeleri toohello kasası kopyalama devam eder. Kasanızı hello abonelik askıya alınmadan önce var. kopyalanan hello yedeklemeler kullanarak erişilebilir toohello geri yükleme işlemleri olur. 

**I indirin veya toohello SQL server geri toohello SQL veritabanı yedekleme dosyaları erişim alabilirim?**

Hayır, şu anda.

**Olası toohave olan birden çok, bir SQL bekletme ilkesi içinde (günlük, haftalık, aylık, Yıllık) zamanlar.**

Hayır, birden çok zamanlamaları, yalnızca sanal makine yedeklemeler için şu anda kullanılabilir.

**Ne biz uzun vadeli yedekleme bekletme aktif coğrafi çoğaltma ikincil veritabanı bir veritabanı üzerinde ayarlama?**

Biz yedeklemeleri çoğaltmaları yok tuttuğundan, da şu anda ikincil veritabanlarında uzun vadeli yedekleme bekletme için bir seçenek yoktur. Ancak, bu nedenle kullanıcılar tooset aktif coğrafi çoğaltma ikincil veritabanında uzun vadeli yedekleme bekletme ayarlama önemlidir:
* Bir yük devretme olur ve bir birincil veritabanı hello veritabanı hale biz tam karşıya yüklenen toovault olduğu yedekleme, alın.
* Hiçbir ek yok uzun vadeli yedekleme bekletme ikincil bir veritabanı üzerinde ayarlamak için maliyet toohello müşteri.

## <a name="next-steps"></a>Sonraki adımlar
Veritabanı Yedeklemeleri yanlışlıkla Bozulması veya silinmesi verileri korumak için herhangi bir iş sürekliliği ve olağanüstü durum kurtarma stratejiniz temel parçası oldukları. toolearn hakkında diğer SQL veritabanı iş sürekliliği çözümleri Merhaba, bkz: [iş sürekliliğine genel bakış](sql-database-business-continuity.md).
