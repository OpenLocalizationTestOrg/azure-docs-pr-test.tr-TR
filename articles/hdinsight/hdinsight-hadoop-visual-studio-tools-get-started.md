---
title: "Visual Studio için Data Lake Araçları'nı kullanarak Hdınsight aaaConnect tooAzure | Microsoft Docs"
description: "Nasıl kümelerinin Azure Hdınsight ve çalışma Hive sorguları tooconnect tooHadoop Visual Studio için Data Lake araçları tooinstall ve kullanımı hakkında bilgi edinin."
keywords: "hadoop araçları, hive sorgusu, visual studio, visual studio hadoop"
services: HDInsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: ce9c572a-1e98-46bf-9581-13a9767f1fa5
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: jgao
ms.openlocfilehash: ff5819a64bebe5f4ab3cf763ce6c45c81aa34b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-hdinsight-and-run-hive-queries-using-data-lake-tools-for-visual-studio"></a>TooAzure Hdınsight bağlanmak ve Visual Studio için Data Lake Araçları'nı kullanarak Hive sorguları çalıştırma

Visual Studio tooconnect tooHadoop için toouse Data Lake araçları içinde nasıl kümeleri öğrenin [Azure Hdınsight](hdinsight-hadoop-introduction.md) ve Hive sorguları göndermek. Hdınsight kullanma hakkında daha fazla bilgi için bkz: [giriş tooHDInsight](hdinsight-hadoop-introduction.md) ve [Hdınsight kullanmaya başlama](hdinsight-hadoop-linux-tutorial-get-started.md). Bağlantı tooa Storm kümesi hakkında daha fazla bilgi için bkz: [Visual Studio kullanarak Hdınsight üzerinde Apache Storm için C# topolojileri](hdinsight-storm-develop-csharp-visual-studio-topology.md).

Visual Studio için Data Lake araçları, kullanılan tooaccess olabilir Data Lake Analytics ve Hdınsight.  Merhaba Data Lake araçları hakkında bilgi için [öğretici: Visual Studio için Data Lake Araçları'nı kullanarak U-SQL betikleri geliştirme](../data-lake-analytics/data-lake-analytics-data-lake-tools-get-started.md).

**Önkoşullar**

Bu öğretici ve kullanım hello Data Lake Visual Studio Araçları toocomplete hello aşağıdakiler gerekir:

* Azure Hdınsight kümesi: toocreate bir, bkz: [Linux tabanlı Hdınsight kullanmaya başlama](hdinsight-hadoop-linux-tutorial-get-started.md)
* Yazılımı aşağıdaki hello içeren bir iş istasyonu:
  
  * Windows 10, Windows 8.1, Windows 8 veya Windows 7.
  * Visual Studio 2013/2015/2017.
    
    > [!NOTE]
    > Şu anda, Visual Studio için Data Lake araçları hello yalnızca hello İngilizce sürüm ile birlikte gelir.
    > 
    > 

## <a name="install-data-lake-tools-for-visual-studio"></a>Visual Studio için Data Lake Araçları’nı yükleme.

Data Lake Araçları, Visual Studio 2017 için varsayılan olarak yüklenir. Hello kullanarak yüklemek için eski sürümleri, [Web Platformu yükleyicisi](https://www.microsoft.com/web/downloads/). Merhaba, Visual Studio sürümünüzle eşleşen birini seçmeniz gerekir. Visual Studio yüklüyse yoksa yükleyebilmek için en son Visual Studio Community ve Azure SDK'sı hello kullanarak hello [Web Platformu yükleyicisi](https://www.microsoft.com/web/downloads/):

![Visual Studio Web Platformu Yükleyicisi için Data Lake araçları. ] (./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.wpi.png "Kullanım Web Platformu yükleyicisi tooinstall Visual Studio için Data Lake araçları")

## <a name="connect-tooazure-subscriptions"></a>TooAzure abonelikleri Bağlan
Data Lake araçları tooconnect tooyour Hdınsight kümeleri, böylece Visual Studio için bazı temel yönetim işlemlerini gerçekleştirmenize ve Hive sorguları çalıştırın.

> [!NOTE]
> Bağlantı tooa genel Hadoop kümesi hakkında daha fazla bilgi için bkz: [yazma ve Visual Studio kullanarak Hive sorguları göndermek](http://blogs.msdn.com/b/xiaoyong/archive/2015/05/04/how-to-write-and-submit-hive-queries-using-visual-studio.aspx).
> 
> 

**tooconnect tooyour Azure aboneliği**

1. Visual Studio'yu açın.
2. Merhaba gelen **Görünüm** menüsünde tıklatın **Sunucu Gezgini** tooopen hello Sunucu Gezgini penceresi.
3. **Azure** seçeneğini ve sonra **HDInsight** seçeneğini genişletin.
   
   > [!NOTE]
   > Bildirim hello **Hdınsight görev listesi** penceresini açın. Göremiyorsanız, tıklatın **diğer pencereler** hello gelen **Görünüm** menüsüne ve ardından **Hdınsight Görev Listesi penceresi**.  
   > 
   > 
4. Azure aboneliği kimlik bilgilerinizi girin ve ardından **Oturum Aç**’a tıklayın. Bu yalnızca olduğundan, hiçbir zaman toohello Azure aboneliği bu iş istasyonunda Visual Studio'dan bağlanmadıysanız gerekir.
5. Sunucu Gezgini’nde, varolan HDInsight kümelerinin listesini görürsünüz. Tüm kümeleri yoksa, hello Azure portal, Azure PowerShell veya Hdınsight SDK hello kullanarak bir tane oluşturabilirsiniz. Daha fazla bilgi için bkz. [HDInsight kümesi oluşturma](hdinsight-hadoop-provision-linux-clusters.md).
   
   ![Visual Studio için Data Lake Araçları Sunucu Gezgini küme listesi](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.server.explorer.png "Visual Studio için Data Lake Araçları Sunucu Gezgini")
6. HDInsight kümesini genişletin. **Hive Veritabanları**, varsayılan depolama hesabı, bağlantılı depolama hesapları ve **Hadoop Hizmeti günlüğünü** görürsünüz. Daha fazla hello varlıklar genişletebilirsiniz.

Tooyour Azure aboneliğine bağlandıktan sonra mümkün toodo hello aşağıdakilerin olması:

**tooconnect toohello Visual Studio'dan Azure portalı**

* Sunucu Gezgini'nde, **Azure** > **HDInsight**’ı genişletin, HDInsight kümesine sağ tıklayın ve ardından **Kümeyi Azure portalında Yönet**’e tıklayın.

**tooask sorular ve Visual Studio geri bildirim**

* Hello gelen **Araçları** menüsünde tıklatın **Hdınsight**ve ardından **MSDN Forumu** tooask sorular veya tıklatın **görüş**.

## <a name="navigate-hello-linked-resources"></a>Merhaba bağlı kaynaklara gitme
Server Explorer'dan hello varsayılan depolama hesabını ve bağlı tüm depolama hesaplarını görebilirsiniz. Merhaba varsayılan depolama hesabını genişletirseniz, hello depolama hesabında Merhaba kapsayıcılara görebilirsiniz. Merhaba varsayılan depolama hesabı ve hello varsayılan kapsayıcı işaretlenmiştir. Merhaba kapsayıcılara tooview hello içeriği hiçbirini tıklayabilir.

![Visual Studio için Data Lake Araçları sunucu gezgini bağlı kaynakları listeleme](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.linked.resources.png "Bağlı kaynakları listeleme")

Bir kapsayıcı açtıktan sonra düğmeleri tooupload, silme ve indirme BLOB'ları aşağıdaki hello kullanabilirsiniz:

![Visual Studio için Data Lake Araçları sunucu gezgini blob işlemleri](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.blob.operations.png "Blob yükleme, silme ve indirme")

## <a name="run-a-hive-query"></a>Hive sorgusu çalıştırma
[Apache Hive](http://hive.apache.org), veri özetleme, sorgu ve analiz sağlamaya yönelik, Hadoop'ta kurulu bir veri ambarı altyapısıdır. Visual Studio için Data Lake Araçları Visual Studio'dan Hive sorguları çalıştırmayı destekler. Hive hakkında daha fazla bilgi için bkz. [HDInsight ile Hive kullanma](hdinsight-use-hive.md).

Bu zaman alıcıdır tootest Hive betiğini Hdınsight kümesine karşı olur. Birkaç dakika veya daha fazla sürebilir. Visual Studio için Data Lake araçları Hive betiğini yerel olarak bağlanan tooa dinamik küme olmadan doğrulayabiliyor.

Visual Studio için Data Lake araçları kullanıcılar toosee hello Hive işinin toplamak ve belirli Hive işlerine hello YARN günlüklerini görünmesini nedir da sağlar.

### <a name="view-hello-hivesampletable"></a>Görünüm hello **hivesampletable**
Tüm HDInsight kümeleri *hivesampletable* adlı örnek bir Hive tablosuyla birlikte gelir  Bu tablo tooshow, nasıl toolist Hive tablolarını hello tablo şemalarını görüntüleme ve hello satır listesi hello Hive kullanacağız tablo.

**toolist tabloları Hive ve Hive tablo şemasını görüntülemek**

1. Gelen **Sunucu Gezgini**, genişletin **Azure** > **Hdınsight** > tercih ettiğiniz hello küme > **Hive veritabanları**  >  **Varsayılan** > **hivesampletable** toosee hello tablo şemasını.
2. Sağ **hivesampletable**ve ardından **ilk 100 satırı görüntüle** toolist hello satır. Eşdeğer toorunning hello Hive sorgusu Hive ODBC sürücüsünü kullanarak aşağıdaki gibidir:
   
     SELECT * FROM hivesampletable LIMIT 100
   
   Merhaba satır sayısını özelleştirebilirsiniz.
   
   ![Data Lake Araçları: HDInsight Hive Visual Studio şema sorgusu](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.hive.schema.png "Hive sorgusu sonuçları")

### <a name="create-hive-tables"></a>Hive tabloları oluşturma
Merhaba GUI toocreate bir Hive tablosu veya Hive sorgularını kullanabilirsiniz. Hive sorgularını kullanma hakkında daha fazla bilgi için bkz. [Hive sorgularını çalıştırma](#run.queries).

**toocreate bir Hive tablosu**

1. **Sunucu Gezgini**’nde **Azure** > **HDInsight Kümeleri** HDInsight kümesi > **Hive Veritabanları**’nı genişletin ve sonra **varsayılan**’a sağ tıklayın ve **Tablo Oluştur**’a tıklayın.
2. Merhaba tablosunu yapılandırın.
3. Tıklatın **Create Table** toosubmit hello iş toocreate hello yeni Hive tablosu.
   
    ![Data Lake Araçları: HDInsight Visual Studio Araçları Hive tablosu oluşturma](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.create.hive.table.png "Hive tablosu oluşturma")

### <a name="run.queries"></a>Hive sorgularını çalıştırma ve doğrulama
İki yolla toocreate ve çalışma Hive sorguları vardır:

* Geçici sorgular oluşturma
* Hive uygulaması oluşturma

**toocreate, doğrulamak ve geçici sorgular çalıştırın**

1. **Sunucu Gezgini**’nde **Azure** seçeneğini ve ardından **HDInsight Kümeleri** seçeneğini genişletin.
2. Burada, toorun hello sorgu istediğiniz ve ardından sağ hello küme **Hive sorgusu yaz**.
3. Merhaba Hive sorgularını girin. Bildirim hello Hive düzenleyicisinin IntelliSense'i destekler. Yüklenmesini destekliyor Visual Studio için data Lake araçları, Hive betiğinizi düzenlerken uzak meta veri hello. Örneğin, "SELECT * FROM", IntelliSense listeler hello yazdığınızda tüm önerilen tablo adlarını hello. Bir tablo adı belirtildiğinde, hello sütun adları hello IntelliSense tarafından listelenir. Merhaba araçları neredeyse tüm Hive DML deyimleri, alt sorgular da destekler ve yerleşik UDF'ler hello.
   
    ![Data Lake Araçları: HDInsight Visual Studio Araçları IntelliSense](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.intellisense.table.names.png "U-SQL IntelliSense")
   
    ![Data Lake Araçları: HDInsight Visual Studio Araçları IntelliSense](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.intellisense.column.names.png "U-SQL IntelliSense")
   
   > [!NOTE]
   > Yalnızca Hdınsight araç çubuğunda seçilen hello meta hello kümelerin önerilir.
   > 
   > 
4. (İsteğe bağlı): tıklatın **betiği doğrula** toocheck hello betik söz dizimi hataları.
   
    ![Data Lake Araçları: Visual Studio için Data Lake Araçları yerel doğrulama](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.validate.hive.script.png "Betik doğrulama")
5. **Gönder** veya **Gönder (Gelişmiş) gönderme** seçeneğine tıklayın. Gelişmiş gönderme seçeneği hello ile yapılandırın **iş adı**, **bağımsız değişkenleri**, **ek yapılandırmalar**, ve **durum dizini**hello komut dosyası için:
   
    ![HDInsight Hadoop Hive sorgusu](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.submit.jobs.advanced.png "Sorgu gönderme")
   
    Merhaba işi gönderdikten sonra gördüğünüz bir **Hive işi Özet** penceresi.
   
    ![Bir HDInsight Hadoop Hive sorgusunun özeti](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.run.hive.job.summary.png "Hive iş özeti")
6. Kullanım hello **yenileme** tooupdate hello durum hello iş durumu değişinceye kadar çok düğmesini**tamamlandı**.
7. Merhaba alt toosee hello aşağıdaki Hello bağlantıları tıklatın: **sorgu iş**, **iş çıktısı**, **iş günlüğü**, veya **Yarn günlüğü**.

**toocreate ve Hive çözümü çalıştırın**

1. Merhaba gelen **dosya** menüsünde tıklatın **yeni**ve ardından **proje**.
2. Seçin **Hdınsight** hello sol bölmeden seçin **Hive uygulaması** hello Orta bölmede, hello özelliklerini girin ve ardından **Tamam**.
   
    ![Data Lake Araçları: HDInsight Visual Studio Araçları yeni Hive projesi](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.new.hive.project.png "Visual Studio'da Hive uygulamaları oluşturma")
3. Gelen **Çözüm Gezgini**, çift **Script.hql** tooopen onu.
4. toovalidate hello Hive betiğini hello tıklatabilirsiniz **betiği doğrula** button, veya hello betik hello Hive düzenleyicisinde sağ tıklayın ve ardından **betiği doğrula** hello bağlam menüsünden.

### <a name="view-hive-jobs"></a>Hive İşlerini Görüntüleme
Hive işleri için iş sorguları, iş çıktısı, iş günlükleri ve Yarn günlüklerini görüntüleyebilirsiniz. Daha fazla bilgi için hello önceki ekran görüntüsüne bakın.

Hello en son sürümü hello araçları, Hive işlerinizin toplama ve YARN günlüklerini görünmesini nedir toosee sağlar. YARN günlüğü, performans sorunlarını araştırmanıza yardımcı olabilir. HDInsight'ın YARN günlüklerini nasıl topladığı hakkında daha fazla bilgi için bkz. [HDInsight Uygulama Günlüklerine Programlamayla Erişme](hdinsight-hadoop-access-yarn-app-logs.md).

**tooview Hive işleri**

1. **Sunucu Gezgini**’nde **Azure** seçeneğini ve ardından **HDInsight** seçeneğini genişletin.
2. HDInsight kümesine sağ tıklayın ve ardından **İşleri Görüntüle**’ye tıklayın. Merhaba hello küme üzerinde çalışan işleri Hive listesini görürsünüz.
3. Merhaba iş listesi tooselect işinde bu tıklatın ve ardından kullanımı hello **Hive işi Özet** penceresi tooopen **sorgu iş**, **iş çıktısı**, **iş günlüğü**, veya **Yarn günlüğü**.
   
    ![Data Lake Araçları: HDInsight Visual Studio Araçları Hive işlerini görüntüleme](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.view.hive.jobs.png "Hive işlerini görüntüleme")

### <a name="faster-path-hive-execution-via-hiveserver2"></a>HiveServer2 aracılığıyla daha hızlı Hive yürütme
> [!NOTE]
> Bu özellik yalnızca HDInsight kümesi sürüm 3.2 ve üstünde çalışır.
> 
> 

Merhaba Data Lake araçları toosubmit Hive işleri aracılığıyla kullanılan [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (Templeton olarak da bilinir). İş ayrıntılarını uzun süre tooreturn sürdü ve hata bilgileri.
Sipariş toosolve bu performans sorunu, Data Lake araçları yürütür hello Hive işlerini doğrudan HiveServer2 aracılığıyla hello küme içindeki böylece RDP/SSH'yi atlar.
Toplama toobetter performans kullanıcılar aynı zamanda Tez grafiklerinde Hive görüntülemek ve görev ayrıntıları hello.

HDInsight kümesi sürüm 3.2 veya sonraki sürümlerinde **HiveServer2 aracılığıyla yürüt** düğmesi görebilirsiniz:

![Data Lake Visual Studio Araçları HiveServer2 aracılığıyla yürütme](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.execute.via.hiveserver2.png "HiveServer2 kullanarak Hive sorguları yürütme")

Geri gerçek zamanlı olarak akışı hello günlüklerine bakın ve hello Hive sorgusu Tez'de yürütülürse hello iş grafiklerini görebilirsiniz.

![Data Lake Visual Studio Araçları hızlı yol Hive yürütme](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.fast.path.hive.execution.png "İş grafiklerini görüntüleme")

**Sorguları HiveServer2 aracılığıyla yürütme ile Sorguları WebHCat aracılığıyla Gönderme arasındaki fark**

Sorguları HiveServer2 aracılığıyla yürütmenin birçok performans avantajı olmasına rağmen, bazı kısıtlamaları vardır. Bazı hello sınırlamaları üretim kullanımına uygun değildir. Merhaba aşağıdaki tabloda hello farklar gösterilmektedir:

|  | HiveServer2 aracılığıyla yürütme | WebHCat aracılığıyla gönderme |
| --- | --- | --- |
| Sorguları yürütme |(Tamamlayacağınız bir MapReduce işi "TempletonControllerJob" adlı) WebHCat Hello ek yükü ortadan kaldırır. |Bir sorgu WebHCat aracılığıyla yürütüldüğü sürece, WebHCat ek gecikme sağlayan bir MapReduce işi başlatır. |
| Geriye akış günlükleri |Yakın gerçek zamanlı. |yalnızca hello işi bittiğinde hello iş yürütme günlüklerini kullanılabilir. |
| İş geçmişini görüntüleme |Bir sorgu HiveServer2 aracılığıyla yürütülürse, buna ait iş geçmişi (iş günlüğü, iş çıktısı) korunmaz. Merhaba uygulama YARN kullanıcı Arabiriminde, sınırlı bilgiyle görüntülenebilir. |Bir sorgu WebHCat aracılığıyla yürütülürse, buna ait iş geçmişi (iş günlüğü, iş çıktısı) korunur ve Visual Studio/HDInsight SDK/PowerShell kullanarak görüntülenebilir. |
| Pencereyi kapatma |Merhaba windows açık tutmalısınız şekilde HiveServer2 aracılığıyla yürütme "zaman uyumlu" bir yöntemdir; Merhaba windows kapattıysanız hello sorgu yürütme iptal edilir. |Böylece hello sorgu WebHCat aracılığıyla gönderme ve Visual Studio'yu kapatın WebHCat aracılığıyla gönderme "zaman uyumsuz" bir yoludur. Geri dönün ve herhangi bir zamanda hello sonuçlarını görebilirsiniz. |

### <a name="tez-hive-job-performance-graph"></a>Tez Hive işi performans grafiği
Hive işlerini hello için performans grafikleri gösteren hello Data Lake araçları destek hello Tez yürütme altyapısı tarafından çalıştırılan. Tez'i etkinleştirme hakkında daha fazla bilgi için bkz. [HDInsight'ta Hive kullanma](hdinsight-use-hive.md). Gönderdikten sonra Visual Studio, Visual Studio Proje gösterir Hive hello grafik hello iş tamamlandığında.  Tooclick hello gerekebilir **yenileme** tooget hello en son iş durumunu düğmesine tıklayın.

> [!NOTE]
> Bu özellik yalnızca HDInsight kümesini 3.2.4.593 sürümünün üstü için geçerlidir ve sadece tamamlanan işler için kullanılabilir (işinizi WebHCat aracılığıyla gönderdiyseniz, bu grafik sorgunuzu ne zaman yürüttüğünüzü HiveServer2 aracılığıyla gösterir). Bu, hem Windows hem de Linux tabanlı kümelerde çalışır.
> 
> 

![Hadoop Hive Tez performans grafiği](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.hive.tez.performance.graph.png "İş durumu")

toohelp, Hive anlamak daha iyi sorgusu, hello araçları, bu sürümde hello Hive işleci görünümü ekler. Merhaba iş grafiğinin köşe hello toodouble tıklayın yeterlidir ve hello köşe tüm hello işleçleri görebilirsiniz. Bu işlece ilişkin daha fazla ayrıntı belirli işleci tooview de gelebilirsiniz.

### <a name="task-execution-view-for-hive-on-tez-jobs"></a>Tez işlerinde Hive için Görev yürütme
Tez işlerinde Hive kullanılabilir için Görev Yürütme Görünümü hello tooget yapılandırılmış ve görselleştirilmiş bilgi Hive işleri için ve diğer iş ayrıntılarını almak. Performans sorunları olduğunda hello görünüm tooget daha ayrıntılı bilgi kullanabilirsiniz. Böylece iş yapılandırmalarını veya sistem mimarisi görselleştirilen hello bilgilere göre ayarlayabilirsiniz Örneğin, her görevin nasıl çalıştığı ve hello (veri okuma/yazma, zamanlaması/başlangıç/bitiş zamanı, vb.), her görev hakkında ayrıntılı bilgi.

![Data Lake Visual Studio Araçları görev yürütme görünümü](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.task.execution.view.png "Görev yürütme görünümü")

## <a name="run-pig-scripts"></a>Pig betikleri çalıştırma
Visual Studio için Data Lake araçları oluşturulmasını destekler ve Pig betikleri tooHDInsight kümeleri gönderin. Kullanıcılar bir Pig proje şablonu oluşturmak ve hello betik tooHDInsight kümeleri gönderin.

## <a name="feedbacks--known-issues"></a>Geribildirimler ve Bilinen sorunlar
* Şu anda, HiveServer2 sonuçlar ideal olmayan salt metin biçiminde görüntülenir. Bunu düzeltmeye çalışıyoruz.
* Şu anda Hello sonuçlar NULL değerler ile başladıysa, hello sonuçlar gösterilmez. Biz bu sorunu düzelttik ve bu sorunu, engellenen bize bir e-posta veya ilgili kişi takım desteği ücretsiz toodrop hissedilmesini.
* Visual Studio tarafından oluşturulan hello HQL betiğini kullanıcının yerel bölge ayarı bağlı olarak kodlanır. Kullanıcı hello betik toocluster ikili olarak yüklerse, doğru şekilde yürütülmeyebilir.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, Visual hello Data Lake (Hdınsight) kullanarak Studio'dan tooconnect tooHDInsight nasıl kümeleri öğrenilen araçları paketini ve nasıl toorun bir Hive sorgusu. Daha fazla bilgi için bkz.

* [HDInsight'ta Hadoop Hive kullanma](hdinsight-use-hive.md)
* [HDInsight'ta Hadoop kullanmaya başlama](hdinsight-hadoop-linux-tutorial-get-started.md)
* [HDInsight'ta Hadoop işlerini gönderme](hdinsight-submit-hadoop-jobs-programmatically.md)
* [HDInsight'ta Hadoop ile Twitter verilerini çözümleme](hdinsight-analyze-twitter-data.md)

