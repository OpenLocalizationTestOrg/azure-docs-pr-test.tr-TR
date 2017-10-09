---
title: "Azure SQL veritabanı için aaaQuery performansı öngörüleri | Microsoft Docs"
description: "Sorgu performansı izleme çoğu CPU kullanan bir Azure SQL veritabanı için sorgular hello tanımlar."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: c2f580b2-3835-453f-89f5-140e02dd2ea7
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 01cca26f85193c679365585cd676449c9db00e1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-query-performance-insight"></a>Azure SQL veritabanı sorgu performansı öngörüleri
İlişkisel veritabanları hello performans ayarlama ve yönetme önemli uzmanlık ve zaman yatırımı gerektiren bir görevdir. Sorgu performansı öngörüleri toospend veritabanı performans sorunlarını giderme hello aşağıdakileri sağlayarak daha az zaman verir:

* Veritabanları (DTU) kaynak tüketimi daha derin bir anlayış. 
* Merhaba üst sorgular tarafından potansiyel olarak performansı için ayarlanan süre/CPU/yürütme sayısı.
* bir sorgu hello ayrıntılarını aşağı özelliği toodrill Merhaba, metin ve kaynak kullanımı geçmişini görüntüleyin. 
* Performans tarafından gerçekleştirilen eylemler Göster ek açıklamaları ayarlama [SQL Azure veritabanı Danışmanı](sql-database-advisor.md)  



## <a name="prerequisites"></a>Ön koşullar
* Sorgu performansı öngörüleri gerektirir [Query Store](https://msdn.microsoft.com/library/dn817826.aspx) veritabanınızda etkindir. Merhaba portal Query Store çalışmıyorsa tooturn ister üzerinde.

## <a name="permissions"></a>İzinler
Merhaba aşağıdaki [rol tabanlı erişim denetimi](../active-directory/role-based-access-control-what-is.md) izinler gerekli toouse sorgu performansı öngörüleri şunlardır: 

* **Okuyucu**, **sahibi**, **katkıda bulunan**, **SQL DB Katılımcısı**, veya **SQL Server Katılımcısı** izinler tooview hello üst kaynak tüketen sorguları ve grafikler gereklidir. 
* **Sahibi**, **katkıda bulunan**, **SQL DB Katılımcısı**, veya **SQL Server Katılımcısı** gerekli tooview sorgu metni izinlerdir.

## <a name="using-query-performance-insight"></a>Sorgu performansı öngörüleri kullanma
Sorgu performansı öngörüleri kolayca toouse şöyledir:

* Açık [Azure portal](https://portal.azure.com/) ve Bul veritabanı tooexamine istiyor. 
  * Destek ve sorun giderme, sol taraftaki menüden "Sorgu performansı öngörüleri" seçin.
* Merhaba ilk sekmesinde üst kaynak tüketen sorguları hello listesini gözden geçirin.
* Bir sorguyu tooview ayrıntılarını seçin.
* Açık [SQL Azure veritabanı Danışmanı](sql-database-advisor.md) ve herhangi bir önerimiz kullanılabilir olup olmadığını denetleyin.
* Kaydırma çubuklarını kullanın veya aralık gözlenen simgeler toochange Yakınlaştır.
  
    ![Performans Panosu](./media/sql-database-query-performance/performance.png)

> [!NOTE]
> Birkaç saat veri SQL veritabanı tooprovide sorgu performansı öngörüleri için Query Store tarafından yakalanan toobe gerekir. Merhaba veritabanı sahip hiç etkinlik yok veya sorgu deposu belirli bir dönemdeki sırasında etkin değil, hello grafikleri döneme görüntülenirken boş olur. Çalışır durumda değilse herhangi bir anda Query Store sağlayabilir.   
> 
> 

## <a name="review-top-cpu-consuming-queries"></a>Kaynak tüketen sorguları üst CPU gözden geçirin
Merhaba, [portal](http://portal.azure.com) aşağıdaki hello:

1. Tooa SQL veritabanını bulun ve tıklatın **tüm ayarları** > **destek + sorun giderme** > **sorgu performansı öngörüleri**. 
   
    ![Sorgu Performansı Öngörüleri][1]
   
    Merhaba üst sorgular görünümünü açar ve hello üst CPU tüketim sorguları listelenir.
2. Ayrıntılar için hello grafiğin etrafında'ı tıklatın.<br>Merhaba çubukları hello seçilen zaman aralığı boyunca seçili hello sorgular tarafından tüketilen CPU % gösterirken hello üst çizgi hello veritabanı için genel DTU % gösterir (örneğin, **geçen hafta** seçili her çubuk bir gününü temsil eder).
   
    ![üst sorguları][2]
   
    Merhaba alt kılavuz hello görünür sorgular için toplanan bilgileri temsil eder.
   
   * Sorgu kimliği - sorgu veritabanı içinde benzersiz tanıtıcısı.
   * CPU (toplama işlevini bağlıdır) sorgu observable aralığı sırasında başına.
   * Sorgu başına süre (toplama işlevini bağlıdır).
   * Belirli bir sorgu için yürütmeleri toplam sayısı.
     
     Seçin, tek tek sorguları tooinclude temizleyin veya onay kutularını kullanarak hello grafikten içermeyecek.
3. Verilerinizi eski hale gelirse hello tıklatın **yenileme** düğmesi.
4. Kaydırıcılar ve Yakınlaştırma düğmeleri toochange gözlem aralığı kullanın ve ani araştırın: ![ayarları](./media/sql-database-query-performance/zoom.png)
5. İsteğe bağlı olarak, farklı bir görünüm istiyorsanız, seçebileceğiniz **özel** sekmesinde ve ayarlayın:
   
   * Ölçüm (CPU süresi, yürütme sayısı)
   * Zaman aralığı (son 24 saat, geçen hafta geçen ay). 
   * Sorgu sayısı.
   * Toplama işlevi.
     
     ![ayarlar](./media/sql-database-query-performance/custom-tab.png)

## <a name="viewing-individual-query-details"></a>Sorguyu ayrıntılarını görüntüleme
tooview sorgu ayrıntıları:

1. En sık kullanılan sorguların hello listesindeki herhangi bir sorgu tıklayın.
   
    ![Ayrıntıları](./media/sql-database-query-performance/details.png)
2. Merhaba Ayrıntılar görünümünü açar ve hello sorguları CPU süresi/tüketim/yürütme sayısı zamanla ayrılmıştır.
3. Ayrıntılar için hello grafiğin etrafında'ı tıklatın.
   
   * Üst grafik genel veritabanı DTU % satırıyla, ve hello çubukları hello seçili sorgu tarafından tüketilen CPU % olduğunu gösterir.
   * İkinci grafik hello seçili sorgu tarafından toplam süresini gösterir.
   * Alt grafik hello seçili sorgu tarafından yürütmeleri toplam sayısını gösterir.
     
     ![Sorgu Ayrıntıları][3]
4. İsteğe bağlı olarak, kaydırma çubuklarını kullanın, Yakınlaştırma düğmeleri veya tıklatın **ayarları** toocustomize sorgu verinin nasıl görüntüleneceğini veya toopick farklı bir zaman aralığı.

## <a name="review-top-queries-per-duration"></a>Üst sorguları süre her gözden geçirin
Merhaba son güncelleştirmesinde sorgu performansı öngörüleri, olası performans sorunlarını belirlemenize yardımcı olabilecek iki yeni ölçümleri gösterdiğimizi: süresi ve yürütme sayısı.<br>

Uzun süre çalışan sorgular uzun kaynakları kilitleme, diğer kullanıcıların engelleme ve ölçeklenebilirlik sınırlama hello büyük potansiyeline sahiptir. Bunlar ayrıca hello en iyi duruma getirme adaylardır.<br>

uzun süre çalışan sorgular tooidentify:

1. Açık **özel** sorgu performansı öngörüleri bir sekmede Seçilen veritabanı için
2. Değiştirme ölçümleri toobe **süresi**
3. Sorgular ve Gözlem aralığı sayısını seçin
4. Toplama işlevi seçin
   
   * **Sum** tüm gözlem aralığı sırasında tüm sorgu yürütme süresini ekler.
   * **Max** tüm gözlem aralığında hangi yürütme süresi en fazla sorguları bulur.
   * **Ortalama** ortalama yürütme süresi tüm sorgu yürütmeleri ve size göstermek bulur hello üst bu ortalamalar dışında. 
     
     ![Sorgu süresi][4]

## <a name="review-top-queries-per-execution-count"></a>Üst sorguları yürütme sayısı her gözden geçirin
Çok sayıda yürütmeleri değil etkileyen veritabanının kendisi ve kaynak kullanımı düşük olabilir, ancak genel uygulama alabilirsiniz yavaş.

Bazı durumlarda, çok yüksek yürütme sayısı ağ tooincrease açabilir gidiş dönüş. Gidiş dönüş performansını önemli ölçüde etkiler. Konu toonetwork gecikme süresi ve toodownstream sunucu gecikme süresi oldukları. 

Örneğin, birçok veri tabanlı Web sitesi yoğun olarak her kullanıcı isteğine hello veritabanı erişin. Bağlantı havuzu yardımcı olur, hello artan sırada ağ trafiği ve hello veritabanı sunucusu üzerindeki işlem yükü performansını olumsuz etkileyebilir.  Genel öneriler tookeep dönüşleri tooan minimuma round ' dir.

tooidentify sık sorgular ("chatty") sorguları yürütülen:

1. Açık **özel** sorgu performansı öngörüleri bir sekmede Seçilen veritabanı için
2. Değiştirme ölçümleri toobe **yürütme sayısı**
3. Sorgular ve Gözlem aralığı sayısını seçin
   
    ![sorgu yürütme sayısı][5]

## <a name="understanding-performance-tuning-annotations"></a>Performans ayarlama ek açıklamaları anlama
Sorgu performansı öngörüleri, iş yükü keşfetme sırasında hello grafik üstünde dikey çizgi simgelerle fark edebilirsiniz.<br>

Bu simgeleri ek açıklamaları; yine de uygun istiyor musunuz? tarafından gerçekleştirilen eylemler etkileyen performans temsil [SQL Azure veritabanı Danışmanı](sql-database-advisor.md). Vurgulama ek açıklama tarafından hello eylem hakkında temel bilgileri alın:

![Sorgu ek açıklaması][6]

Daha fazla tooknow istediğiniz veya Danışmanı öneriyi hello simgesine tıklayın. Eylem ayrıntılarını açar. Etkin bir öneri ise hemen komutunu kullanarak uygulayabilirsiniz.

![Sorgu ek açıklama Ayrıntıları][7]

### <a name="multiple-annotations"></a>Birden çok ek açıklama.
Yakınlaştırma düzeyi nedeniyle, diğer Kapat tooeach olan ek açıklamaları birine daraltılmış olduğunu, mümkündür. Bu özel simgesi ile temsil edilir, tıklatarak nerede ek açıklamaları listesi gruplandırılmış açık yeni dikey penceresi gösterilir.
Sorgular ve performans Eylemler ayarlama bağıntı toobetter yükünüzü anlamanıza yardımcı olabilir. 

## <a name="optimizing-hello-query-store-configuration-for-query-performance-insight"></a>Sorgu performansı öngörüleri için en iyi duruma getirme hello sorgu deposu yapılandırma
Query Store iletileri aşağıdaki hello kullanımınız sorgu performansı öngörüleri sırasında karşılaşabileceğiniz:

* "Query Store düzgün bu veritabanında yapılandırılmamış. Daha fazla toolearn burayı."
* "Query Store düzgün bu veritabanında yapılandırılmamış. Burada toochange ayarlar'ı tıklatın." 

Query Store mümkün toocollect yeni veri değilse bu iletiler genellikle görünür. 

Query Store salt okunur durumda ve en iyi şekilde parametrelerinin ilk durumda olur. Bu sorgu deposunun boyutunu artırmayı veya sorgu deposunun temizlenmesi düzeltebilirsiniz.

![qds düğmesi][8]

Query Store kapalı olduğu veya parametreler en iyi şekilde oluşturulmamış ikinci durumda olur. <br>Aşağıdaki komutları çalıştırarak veya doğrudan portalından hello bekletme ve yakalama İlkesi ve etkinleştir Query Store değiştirebilirsiniz:

![qds düğmesi][9]

### <a name="recommended-retention-and-capture-policy"></a>Önerilen bekletme ve yakalama İlkesi
Bekletme ilkeleri iki tür vardır:

* En büyük boyut olduğunda otomatik olarak yakın veri temizleyecek kümesi tooAUTO ulaşıldığında boyutu - tabanlı.
* Temel - saat biz ayarlanmadıysa, varsayılan olarak 30 günden eski bilgileri too30 gün anlamına gelir, Query Store alanı dışında çalıştırırsanız, siler, sorgu

Yakalama ilke kümesine:

* **Tüm** -tüm sorgular yakalar.
* **Otomatik** -sık sorgular ve önemsiz derleme ve çalıştırma süresi sorgularıyla yok sayılır. Eşikleri yürütme sayısı, derleme ve çalışma zamanı süresi için dahili olarak belirlenir. Merhaba varsayılan seçenek budur.
* **Hiçbiri** -Query Store yeni sorgular yakalamayı durdurur ancak, çalışma zamanı istatistikleri zaten yakalanan sorgular için hala toplanır.

Tüm ilkeler tooAUTO ve temiz İlkesi too30 gün ayarı öneririz:

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);

Query Store boyutunu artırın. Bu bağlantı tooa veritabanı tarafından gerçekleştirilen veren sorgu şu olabilir:

    ALTER DATABASE [YourDB]
    SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);

Toowait istemiyorsanız, Query Store temizleyebilirsiniz ancak bu ayarları uygulamak yeni sorgular toplama sorgu deposu sonunda hale getirir. 

> [!NOTE]
> Aşağıdaki sorgu yürütme hello Query Store tüm geçerli bilgileri silinmesine neden olur. 
> 
> 

    ALTER DATABASE [YourDB] SET QUERY_STORE CLEAR;


## <a name="summary"></a>Özet
Sorgu performansı öngörüleri sorgu iş yükü hello etkisini ve toodatabase kaynak tüketimini ilişkilendirilme şekli anlamanıza yardımcı olur. Bu özellik, kaynak tüketen sorguları hello üst hakkında bilgi edinin ve bir sorun haline gelmeden önce hello olanları toofix kolayca tanımlayın.

## <a name="next-steps"></a>Sonraki adımlar
SQL veritabanınız hello performansını iyileştirme konusunda ek öneriler için tıklatın [önerileri](sql-database-advisor.md) hello üzerinde **sorgu performansı öngörüleri** dikey.

![Performans Danışmanı](./media/sql-database-query-performance/ia.png)

<!--Image references-->
[1]: ./media/sql-database-query-performance/tile.png
[2]: ./media/sql-database-query-performance/top-queries.png
[3]: ./media/sql-database-query-performance/query-details.png
[4]: ./media/sql-database-query-performance/top-duration.png
[5]: ./media/sql-database-query-performance/top-execution.png
[6]: ./media/sql-database-query-performance/annotation.png
[7]: ./media/sql-database-query-performance/annotation-details.png
[8]: ./media/sql-database-query-performance/qds-off.png
[9]: ./media/sql-database-query-performance/qds-button.png

