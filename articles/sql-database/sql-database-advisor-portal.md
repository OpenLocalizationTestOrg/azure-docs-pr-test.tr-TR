---
title: "aaaApply performans önerileri - Azure SQL veritabanı | Microsoft Docs"
description: "Azure SQL Database veya toocorrect performansını en iyi duruma getirebilirsiniz hello Azure portal toofind performans önerileri kullanabilirsiniz, iş yükü tanımlanan bazı sorunun."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: cda8a646-0584-4368-b28a-85cdd9b54fcd
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 0b2234840fc3254d235db9e7d18f5bc912851c6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="find-and-apply-performance-recommendations"></a>Bul ve performans önerileri uygulayın

Azure SQL Database veya toocorrect performansını en iyi duruma getirebilirsiniz hello Azure portal toofind performans önerileri kullanabilirsiniz, iş yükü tanımlanan bazı sorunun. **Performans öneri** sayfası Azure portalında olası etkilerini dayalı toofind hello üst olarak öneriler sağlar. 

## <a name="viewing-recommendations"></a>Öneriler görüntüleme

tooview ve doğru hello performans önerileri uygulamak [rol tabanlı erişim denetimi](../active-directory/role-based-access-control-what-is.md) Azure izinleri. **Okuyucu**, **SQL DB Katılımcısı** izinlerdir gerekli tooview önerileri ve **sahibi**, **SQL DB Katılımcısı** izinleri gereklidir tooexecute herhangi bir eylem; oluşturma veya dizinleri bırakın ve dizin oluşturmayı iptal et.

Azure Portal'da aşağıdaki adımları toofind performans önerileri hello kullan:

1. İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2. Çok Git**daha fazla hizmet** > **SQL veritabanları**, veritabanınızı seçin.
3. Çok gidin**performans öneri** tooview kullanılabilir önerileri hello Seçilen veritabanı için.

Performans shonw hello tablo benzer toohello biri üzerinde aşağıdaki şekilde hello gösterilen içinde önerileri:

![Öneriler](./media/sql-database-advisor-portal/recommendations.png)

Öneriler, olası performans kategorileri aşağıdaki hello içine etkilerini göre sıralanır:

| Etkisi | Açıklama |
|:--- |:--- |
| Yüksek |Yüksek etkisi önerileri hello en önemli performans etkisi sağlamalıdır. |
| Orta |Orta etkisi önerileri performansını artırmak, ancak önemli ölçüde değil. |
| Düşük |Düşük etkisi önerileri olmadan daha iyi performans sağlaması gerekir, ancak geliştirmeleri önemli ölçüde olmayabilir. |


> [!NOTE]
> Azure SQL veritabanı toomonitor etkinlikleri en az sipariş tooidentify bir günü için bazı öneriler gerekir. Bu etkinlik için rastgele yetersiz WINS'e daha hello Azure SQL veritabanı daha kolay tutarlı sorgu desenlerine için en iyi duruma getirebilirsiniz. Öneriler corrently kullanılabilir değilse, hello **performans öneri** sayfası, nedenini açıklayan bir ileti sağlar.
> 

Merhaba geçmiş işlemleri hello durumunu da görüntüleyebilirsiniz. Bir öneri veya durum toosee daha fazla ayrıntı seçin.

"Dizin oluşturma" öneri hello Azure portal'ın bir örneği burada verilmiştir.

![Dizin oluşturma](./media/sql-database-advisor-portal/sql-database-performance-recommendation.png)

## <a name="applying-recommendations"></a>Önerileri uygulama
Azure SQL veritabanına nasıl önerilerdir üzerinde tam denetim verir hello aşağıdaki üç seçenekten birini kullanarak etkin: 

* Tek tek önerileri biri aynı anda geçerlidir.
* Etkinleştirme hello otomatik ayarlama tooautomatically önerileri uygulayın.
* tooimplement bir öneri, T-SQL betiği veritabanınızı karşı önerilen hello el ile çalıştırın.

Her öneri tooview ayrıntılarını seçin ve ardından **görüntülemek betik** tooreview hello tam ayrıntılarını hello öneri nasıl oluşturulur.

Merhaba veritabanı çevrimiçi kalır sırada hello öneri uygulanan--performans öneri veya hiçbir zaman otomatik ayarlama kullanarak bir veritabanını çevrimdışı duruma getirir.

### <a name="apply-an-individual-recommendation"></a>Tek bir öneriyi
Gözden geçirin ve aynı anda önerileri bir kabul edebilir.

1. Merhaba üzerinde **önerileri** dikey penceresinde, öneri seçin.
2. Merhaba üzerinde **ayrıntıları** dikey penceresinde **Uygula** düğmesi.
   
    ![öneriyi](./media/sql-database-advisor-portal/apply.png)

Seçili öneri hello veritabanı üzerinde uygulanır.

### <a name="removing-recommendations-from-hello-list"></a>Öneriler hello listesinden kaldırılıyor
Öneriler listesi tooremove hello listeden istediğiniz öğeleri içeriyorsa, hello öneri atabilirsiniz:

1. Merhaba listesinde bir öneri seçin **önerileri** tooopen hello ayrıntıları.
2. Tıklatın **atmak** hello üzerinde **ayrıntıları** dikey.

İsterseniz, atılan öğeler geri toohello ekleyebilirsiniz **önerileri** listesi:

1. Merhaba üzerinde **önerileri** dikey penceresinde **atılan Görünüm**.
2. Atılan bir öğeyi hello listesi tooview ayrıntılarını seçin.
3. İsteğe bağlı olarak, tıklayın **geri atmak** tooadd hello dizin geri toohello ana listesi **önerileri**.


### <a name="enable-automatic-tuning"></a>Otomatik ayarlamayı etkinleştirme
Hello Azure SQL veritabanı tooimplement önerileri otomatik olarak ayarlayabilirsiniz. Öneriler kullanılabilir duruma geldiğinde otomatik olarak uygulanır. Olarak hello tarafından yönetilen tüm öneriler hello performans etkisi olumsuz hello öneri ise hizmet geri alınacak.

1. Merhaba üzerinde **önerileri** dikey penceresinde tıklatın **otomatikleştirme**:
   
    ![Advisor ayarları](./media/sql-database-advisor-portal/settings.png)
2. Eylemler tooautomate seçin:
   
    ![Dizinleri önerilir](./media/sql-database-advisor-portal/automation.png)

### <a name="manually-run-hello-recommended-t-sql-script"></a>T-SQL betiği önerilen hello elle çalıştırma
Herhangi bir önerisi seçin ve ardından **görüntülemek betik**. Bu komut, veritabanına karşı çalışırlar toomanually hello öneriyi uygulamanız.

*El ile gerçekleştirilen dizinler değil izlenen ve performans etkisi hello hizmeti tarafından doğrulanan* önerilen oluşturma tooverify sonra bu dizinler izlemek için bunlar performans artışı sağlar ve ayarlamak veya onları silin gerekli. Dizin oluşturma hakkında daha fazla bilgi için bkz: [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).

### <a name="canceling-recommendations"></a>Öneriler iptal etme
Bulunan önerileri bir **bekleyen**, **doğrulama**, veya **başarı** durumu iptal edilemez. Önerileri durumuna sahip bir **Executing** iptal edilemez.

1. Bir öneri hello seçin **ayarlama geçmişi** alanı tooopen hello **önerileri ayrıntıları** dikey.
2. Tıklatın **iptal** tooabort hello işleminin, hello öneri uygulanıyor.

## <a name="monitoring-operations"></a>İzleme işlemleri
Bir öneri uygulama eşzamanlı olarak gerçekleşebilir değil. Merhaba portal öneri hello durumunu ilişkin ayrıntılar sağlar. Merhaba, bir dizin olabilir olası durumlar şunlardır:

| Durum | Açıklama |
|:--- |:--- |
| Beklemede |Komut alındı ve çalıştırılmak üzere zamanlanmış öneri uygulayın. |
| Yürütme |Merhaba öneri uygulanmaktadır. |
| Doğrulama |Öneri başarıyla uygulandı ve hello hizmet hello avantajları ölçme. |
| Başarılı |Öneri başarıyla uygulandı ve avantajları ölçülür. |
| Hata |Merhaba öneri uygulama hello işlemi sırasında bir hata oluştu. Bu geçici bir sorun veya büyük olasılıkla bir şema değişikliği toohello tablosu olabilir ve hello komut dosyası artık geçerli değil. |
| Geri alma |Merhaba öneri uygulandı, ancak kullanıcı dışı olarak kabul edildi ve otomatik olarak geri döndürülüyor. |
| Döndürüldü |Merhaba öneri geri döndürüldü. |

Bir işlemdeki önerisi hello listesi toosee daha fazla ayrıntı tıklatın:

![Dizinleri önerilir](./media/sql-database-advisor-portal/operations.png)

### <a name="reverting-a-recommendation"></a>Bir öneri dönüştürme
Merhaba performans önerileri tooapply hello öneri kullandıysanız hello performans etkisi toobe negatif bulursa (el ile Merhaba T-SQL komut dosyası çalıştırılamadı anlamına gelir), otomatik olarak onu döner. Toorevert yalnızca istediğiniz herhangi bir nedenle bir öneri yapabileceğiniz varsa hello aşağıdaki:

1. Başarıyla uygulandı öneri hello seçin **geçmişi ayarlama** alanı.
2. Tıklatın **Revert** hello üzerinde **öneri ayrıntılarını** dikey.

![Dizinleri önerilir](./media/sql-database-advisor-portal/details.png)

## <a name="monitoring-performance-impact-of-index-recommendations"></a>Dizin önerileri performans etkisini izleme
Önerileri başarıyla uygulandıktan sonra (şu anda, dizin işlemleri ve yalnızca sorguları önerileri Parametreleştirme) tıklayabilirsiniz **sorgu öngörüleri** hello öneri Ayrıntılar dikey tooopen üzerinde [sorgu Performansı öngörüleri](sql-database-query-performance.md) ve üst sorgularınızı hello performans etkisini bakın.

![İzleyici performansına etkisi](./media/sql-database-advisor-portal/query-insights.png)

## <a name="summary"></a>Özet
Azure SQL veritabanı SQL veritabanı performansı artırmak için öneriler sağlar. T-SQL komut dosyaları, tek tek yanı sıra ve tam otomatik, sağlayarak veritabanınızı en iyi duruma getirme ve sonuçta sorgu performansını iyileştirme yararlı bir Yardım alın.

## <a name="next-steps"></a>Sonraki adımlar
Önerilerinizi izlemek ve tooapply devam bunları toorefine performans. Veritabanı iş yüklerini, dinamik ve sürekli olarak değiştirin. Azure SQL veritabanı toomonitor devam edecek ve veritabanınızın performansı artırmak öneriler sağlar. 

* Bkz: [otomatik ayarlama](sql-database-automatic-tuning.md) hakkında daha fazla bilgi toolearn hello Azure SQL veritabanı'nda otomatik ayarlama.
* Bkz: [performans önerileri](sql-database-advisor.md) Azure SQL veritabanı performans önerileri genel bakış.
* Bkz: [sorgu performansı öngörüleri](sql-database-query-performance.md) üst sorgularınızı hello performans etkisini görüntüleme hakkında toolearn.

## <a name="additional-resources"></a>Ek kaynaklar
* [Sorgu deposu](https://msdn.microsoft.com/library/dn817826.aspx)
* [DİZİN OLUŞTURMA](https://msdn.microsoft.com/library/ms188783.aspx)
* [Rol tabanlı erişim denetimi](../active-directory/role-based-access-control-what-is.md)

