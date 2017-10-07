---
title: "Visual Studio Hortonworks Sandbox - Azure Hdınsight ile aaaData Lake araçları | Microsoft Docs"
description: "Nasıl toouse hello Azure Data Lake araçları Visual Studio için yerel bir VM'de çalıştıran hello Hortonworks sandbox ile bilgi edinin. Bu araçları ile oluşturun ve Hive veya Pig işleri hello sandbox ve görünüm iş çıktısı ve geçmiş çalıştırın."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e3434c45-95d1-4b96-ad4c-fb59870e2ff0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: 7a3406b28d87d953e9b5be387faa86268f47b935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-data-lake-tools-for-visual-studio-with-hello-hortonworks-sandbox"></a>Hello Azure Data Lake araçları Visual Studio için Hortonworks Sandbox hello ile kullanın.

Azure Data Lake genel Hadoop kümeleri ile çalışma araçları içerir. Bu belge, toouse hello Data Lake araçları ile Hortonworks yerel bir sanal makinede çalışan Sandbox hello hello adımları sağlar.

Merhaba Hortonworks Sandbox kullanarak geliştirme ortamınızı yerel olarak Hadoop ile toowork sağlar. Bir çözümü geliştirilmiştir ve toodeploy istediğiniz sonra onu ölçekte tooan Hdınsight kümesi sonra taşıyabilirsiniz.

## <a name="prerequisites"></a>Ön koşullar

* Merhaba Hortonworks korumalı alan, geliştirme ortamınızı bir sanal makinede çalışan. Bu belge yazılmış ve Oracle VirtualBox çalıştıran hello sandbox ile test. Merhaba hello sandbox ayarlama hakkında daha fazla bilgi için bkz: [hello Hortonworks sandbox ile başlayın.](hdinsight-hadoop-emulator-get-started.md) Belge.

* Visual Studio 2013, Visual Studio 2015 ve Visual Studio 2017 (herhangi bir sürümünü).

* Merhaba [.NET için Azure SDK](https://azure.microsoft.com/downloads/) 2.7.1 veya üzeri.

* Merhaba [Visual Studio için Azure Data Lake Araçları](https://www.microsoft.com/download/details.aspx?id=49504).

## <a name="configure-passwords-for-hello-sandbox"></a>Parolalar hello korumalı alan için yapılandırma

Hortonworks Sandbox çalıştıran bu hello emin olun. Ardından hello hello adımları [hello Hortonworks Sandbox başlamak](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) belge. Bu adımları hello SSH hello parolasını yapılandırma `root` hesap ve Ambari hello `admin` hesabı. Bu parolalar, Visual Studio'dan toohello sandbox bağlandığınızda kullanılır.

## <a name="connect-hello-tools-toohello-sandbox"></a>Merhaba araçları toohello sandbox Bağlan

1. Visual Studio'ni açın, **Görünüm**ve ardından **Sunucu Gezgini**.

2. Gelen **Sunucu Gezgini**, sağ hello **Hdınsight** giriş ve ardından **tooHDInsight öykünücüsü bağlanmak**.

    ![Ekran görüntüsü, Sunucu Gezgini, ile Bağlan tooHDInsight vurgulanmış öykünücüsü](./media/hdinsight-hadoop-emulator-visual-studio/connect-emulator.png)

3. Merhaba gelen **tooHDInsight öykünücüsü bağlanmak** iletişim kutusunda, Ambari için yapılandırılmış hello parola girin.

    ![Vurgulanan parola metin kutusu ile iletişim kutusunun ekran görüntüsü](./media/hdinsight-hadoop-emulator-visual-studio/enter-ambari-password.png)

    Seçin **sonraki** toocontinue.

4. Kullanım hello **parola** hello için yapılandırdığınız alan tooenter hello parola `root` hesabı. Merhaba diğer alanlarını hello varsayılan değeri bırakın.

    ![Vurgulanan parola metin kutusu ile iletişim kutusunun ekran görüntüsü](./media/hdinsight-hadoop-emulator-visual-studio/enter-root-password.png)

    Seçin **sonraki** toocontinue.

5. Merhaba Hizmetleri toofinish doğrulamasının tamamlanmasını bekleyin. Bazı durumlarda, doğrulama başarısız ve tooupdate hello yapılandırma sor. Doğrulama başarısız olursa, seçin **güncelleştirme**ve hello yapılandırma ve doğrulama hello hizmet toofinish için bekleyin.

    ![Güncelleştirme düğmesi vurgulanan iletişim kutusunun ekran görüntüsü](./media/hdinsight-hadoop-emulator-visual-studio/fail-and-update.png)

    > [!NOTE]
    > Merhaba güncelleştirme işlemini Hortonworks Sandbox yapılandırma toowhat Visual Studio için hello Data Lake araçları tarafından beklenen Ambari toomodify hello kullanır.

6. Doğrulama tamamlandıktan sonra seçin **son** toocomplete yapılandırma.
    ![Bitiş düğmesi vurgulanan iletişim kutusunun ekran görüntüsü](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)

     >[!NOTE]
     > Merhaba, geliştirme ortamı ve hello toohello sanal makine ayrılmış bellek miktarı hızını bağlı olarak, bu birkaç dakika tooconfigure alın ve hello Hizmetleri Doğrula.

Bu adımları uyguladıktan sonra artık elinizde bir **Hdınsight yerel küme** hello altında Sunucu Gezgininde girdisi **Hdınsight** bölümü.

## <a name="write-a-hive-query"></a>Bir Hive sorgusu Yaz

Hive yapılandırılmış verilerle çalışmak için bir SQL benzeri sorgu dili (HiveQL) sağlar. Aşağıdaki adımları toolearn toorun isteğe bağlı hello yerel küme karşı nasıl sorgular hello kullanın.

1. İçinde **Sunucu Gezgini**, daha önce eklediğiniz hello yerel küme hello girişini sağ tıklatın ve ardından **Hive sorgusu yaz**.

    ![Ekran görüntüsü, Sunucu Gezgini, yazma vurgulanmış Hive sorgusu ile](./media/hdinsight-hadoop-emulator-visual-studio/write-hive-query.png)

    Yeni bir sorgu penceresi görünür. Burada hızla yapabilecekleriniz yazma ve bir sorgu toohello yerel küme gönderin.

2. Merhaba yeni sorgu penceresinde hello aşağıdaki komutu girin:

        select count(*) from sample_08;

    toorun hello sorgu, select **gönderme** hello penceresinin hello üstünde. Merhaba diğer değerleri bırakın (**toplu** ve sunucu adı) hello varsayılan değerleri.

    ![Merhaba Gönder düğmesi vurgulanan Sorgu penceresinin ekran görüntüsü](./media/hdinsight-hadoop-emulator-visual-studio/submit-hive.png)

    Ayrıca hello açılır menü sonraki çok kullanabileceğiniz**gönderme** tooselect **Gelişmiş**. Gelişmiş Seçenekleri hello iş gönderdiğinizde tooprovide ek seçenekler sağlar.

    ![Gönderme betik ekran iletişim kutusu](./media/hdinsight-hadoop-emulator-visual-studio/advanced-hive.png)

3. Merhaba sorgu gönderdikten sonra hello iş durumu görüntülenir. Hadoop tarafından işlendiği hello iş durumu hello işi hakkındaki bilgileri görüntüler. **İş durumu** hello hello işinin durumunu sağlar. Merhaba durumu düzenli aralıklarla güncelleştirilir veya hello simgesi toorefresh hello durumunu Yenile el ile kullanabilirsiniz.

    ![İş vurgulanmış durumu ile iş görünümünde ekran iletişim kutusu](./media/hdinsight-hadoop-emulator-visual-studio/job-state.png)

    Merhaba sonra **iş durumu** çok değiştirir**tamamlandı**, yönlendirilmiş Çevrimsiz grafik (DAG) görüntülenir. Bu diyagramda tarafından Tez hello Hive sorgusu işlenirken belirlendi hello yürütme yolu açıklanmaktadır. Tez hello varsayılan yürütme Hive için hello yerel kümede altyapısıdır.

    > [!NOTE]
    > Linux tabanlı Hdınsight kümelerini kullanırken Tez ayrıca hello varsayılandır. Merhaba varsayılan Windows tabanlı Hdınsight üzerinde değil. toouse, burada, hello satırı ekleyin `set hive.execution.engine = tez;` Hive sorgunuzu toohello başlangıcı.

    Kullanım hello **iş çıktısı** bağlantı tooview hello çıktı. Bu durumda, bu 823, hello hello sample_08 tablodaki satır sayısını gösterir. Hello kullanarak hello işle ilgili tanılama bilgileri görüntüleyebilirsiniz **iş günlüğü** ve **karşıdan YARN günlüğü** bağlantılar.

4. Ayrıca Hive işleri etkileşimli olarak hello değiştirerek çalıştırabilirsiniz **toplu** çok alan**etkileşimli**. Ardından **yürütme**.

    ![Vurgulanan etkileşimli ekran ve yürütme düğmeleri](./media/hdinsight-hadoop-emulator-visual-studio/interactive-query.png)

    Akışlar hello işleme toohello sırasında oluşturulan çıktı günlüğünü etkileşimli bir sorgu **HiveServer2 çıkış** penceresi.

    > [!NOTE]
    > Merhaba bilgi olduğu hello hello kullanılabilir aynı **iş günlüğü** bir işi tamamlandıktan sonra bağlantı.

    ![Çıktı oturum ekran görüntüsü](./media/hdinsight-hadoop-emulator-visual-studio/hiveserver2-output.png)

## <a name="create-a-hive-project"></a>Bir Hive projesi oluşturma

Ayrıca, birden çok Hive betiği içeren bir proje oluşturabilirsiniz. Komut dosyaları ilgili ya da bir sürüm denetim sisteminde toostore betikleri istediğiniz bir proje kullanın.

1. Visual Studio'da seçin **dosya**, **yeni**ve ardından **proje**.

2. Projeleri Hello listeden genişletin **şablonları**, genişletin **Azure Data Lake**ve ardından **HIVE (Hdınsight)**. Merhaba şablonları listesinden **örnek Hive**. Bir ad ve konum girin ve ardından **Tamam**.

    ![Yeni Proje penceresinin ekran penceresiyle Azure Data Lake, HIVE, örnek Hive ve Tamam'ı vurgulanmış](./media/hdinsight-hadoop-emulator-visual-studio/new-hive-project.png)

Merhaba **örnek Hive** projeyi içeren iki komut **WebLogAnalysis.hql** ve **SensorDataAnalysis.hql**. Bu komut dosyalarını kullanarak aynı hello gönderebilirsiniz **gönderme** hello penceresinde hello üstündeki düğmesi.

## <a name="create-a-pig-project"></a>Pig proje oluşturma

Hive yapılandırılmış verilerle çalışmak için SQL benzeri bir dille sağlarken, Pig verileri dönüşümleri gerçekleştirerek çalışır. Pig toodevelop sağlayan bir dil (Pig Latin) bir ardışık düzen Dönüşümlerin sağlar. toouse Pig hello yerel kümeyle şu adımları izleyin:

1. Visual Studio'yu açın ve seçin **dosya**, **yeni**ve ardından **proje**. Projeleri Hello listeden genişletin **şablonları**, genişletin **Azure Data Lake**ve ardından **Pig (Hdınsight)**. Merhaba şablonları listesinden **Pig uygulama**. Konum, bir ad girin ve ardından **Tamam**.

    ![Yeni Proje penceresinin ekran penceresiyle Azure Data Lake, Pig, Pig uygulama ve Tamam'ı vurgulanmış](./media/hdinsight-hadoop-emulator-visual-studio/new-pig.png)

2. Metin hello Merhaba içeriğine aşağıdaki hello girin **script.pig** bu proje ile oluşturulmuş dosyası.

        a = LOAD '/demo/data/Website/Website-Logs' AS (
            log_id:int,
            ip_address:chararray,
            date:chararray,
            time:chararray,
            landing_page:chararray,
            source:chararray);
        b = FILTER a BY (log_id > 100);
        c = GROUP b BY ip_address;
        DUMP c;

    Pig, Hive farklı bir dil kullanıyor, ancak hello işleri çalıştırma nasıl hello aracılığıyla her iki dilleri arasında tutarlıdır **gönderme** düğmesi. Seçme hello yanında aşağı açılan **gönderme** Pig için Gelişmiş Gönder iletişim kutusu görüntüler.

    ![Gönderme betik ekran iletişim kutusu](./media/hdinsight-hadoop-emulator-visual-studio/advanced-pig.png)

3. Merhaba iş durumunu ve çıkışını de görüntülenir, aynı bir Hive sorgusu hello.

    ![Tamamlanan Pig işi ekran görüntüsü](./media/hdinsight-hadoop-emulator-visual-studio/completed-pig.png)

## <a name="view-jobs"></a>İşleri görüntüle

Data Lake araçları de tooeasily Hadoop üzerinde çalışan işleri hakkındaki bilgileri görüntüleyin olanak sağlar. Merhaba yerel kümede çalışan adımları toosee hello işleri aşağıdaki hello kullanın.

1. Gelen **Sunucu Gezgini**hello yerel kümeye sağ tıklayın ve ardından **işleri görüntüle**. Gönderilen toohello küme silinmiş işlerinin listesi görüntülenir.

    ![Ekran görüntüsü, Sunucu Gezgini, ile vurgulanan işleri görüntüle](./media/hdinsight-hadoop-emulator-visual-studio/view-jobs.png)

2. İşlerini Hello listeden bir tooview hello iş ayrıntılarını seçin.

    ![Ekran görüntüsü, iş tarayıcı vurgulanmış hello işleri biriyle](./media/hdinsight-hadoop-emulator-visual-studio/view-job-details.png)

    Görüntülenen hello bağlantılar, tooview hello çıkış ve günlük bilgileri de dahil olmak üzere bir Hive veya Pig sorgu çalıştırdıktan sonra gördüğünüz benzer toowhat bilgilerdir.

3. Ayrıca, değiştirebilir ve buradan hello işi yeniden gönderin.

## <a name="view-hive-databases"></a>Hive veritabanları görüntüleyin

1. İçinde **Sunucu Gezgini**, hello genişletin **Hdınsight yerel küme** girişi genişletin ve ardından **Hive veritabanları**. Merhaba **varsayılan** ve **xademo** veritabanları hello yerel kümede görüntülenir. Bir veritabanını genişletmeden hello veritabanı içinde hello tabloları gösterir.

    ![Sunucu Gezgini ekran veritabanları ile genişletilmiş](./media/hdinsight-hadoop-emulator-visual-studio/expanded-databases.png)

2. Bir tablo genişleterek bu tablonun hello sütunlarını görüntüler. tooquickly görünümü hello verileri, bir tablo sağ tıklatın ve seçin **ilk 100 satırı görüntüle**.

    ![Ekran görüntüsü, Sunucu Gezgini, Genişletilmiş Tablo ve Görünüm ilk 100 seçilen satırı ile](./media/hdinsight-hadoop-emulator-visual-studio/view-100.png)

### <a name="database-and-table-properties"></a>Veritabanı ve tablo özellikleri

Bir veritabanı veya tablo hello özelliklerini görüntüleyebilirsiniz. Seçme **özellikleri** hello Özellikler penceresinde seçili hello öğenin ayrıntılarını görüntüler. Örneğin, ekran aşağıdaki hello gösterilen hello bilgileri bakın:

![Ekran görüntüsü, Özellikler penceresi](./media/hdinsight-hadoop-emulator-visual-studio/properties.png)

### <a name="create-a-table"></a>Bir tablo oluşturma

toocreate bir tabloda bir veritabanını sağ tıklatın ve ardından **Create Table**.

![Ekran görüntüsü, Sunucu Gezgini, ile vurgulanan Tablo Oluştur](./media/hdinsight-hadoop-emulator-visual-studio/create-table.png)

Daha sonra bir form kullanarak hello tablosu oluşturabilirsiniz. Ekran aşağıdaki hello Hello altındaki gördüğünüz kullanılan toocreate hello tablosu ham HiveQL hello.

![Ekran görüntüsü hello form toocreate tablo kullanılan](./media/hdinsight-hadoop-emulator-visual-studio/create-table-form.png)

## <a name="next-steps"></a>Sonraki adımlar

* [Merhaba ipleri hello Hortonworks korumalı alan, öğrenme](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [Hadoop Öğreticisi - HDP ile çalışmaya başlama](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)
