---
title: "aaaUse Ambari Tez görünümü Hdınsight - Azure ile | Microsoft Docs"
description: "Nasıl toouse hello Ambari Tez görüntülemek toodebug Tez işlerinde Hdınsight'ta öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 9c39ea56-670b-4699-aba0-0f64c261e411
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 5d61bd0403c98284c86982073af91468ae62ac60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-ambari-views-toodebug-tez-jobs-on-hdinsight"></a>Hdınsight üzerinde Ambari görünümleri toodebug Tez işlerinde kullanın

Merhaba Hdınsight için Ambari Web kullanıcı Arabirimi Tez kullanan kullanılan toounderstand ve hata ayıklama işleri olabilir bir Tez görünümü içerir. bir grafik bağlı öğelerinin her öğenin ayrıntısına ve istatistikleri ve günlük kaydı bilgilerini almak hello Tez görünümü toovisualize hello iş sağlar.

> [!IMPORTANT]
> Bu belgedeki Hello adımlar Linux kullanan bir Hdınsight kümesi gerektirir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz: [Hdınsight bileşen sürümü oluşturma](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Ön koşullar

* Linux tabanlı Hdınsight kümesi. Küme oluşturma adımları için bkz: [Linux tabanlı Hdınsight kullanmaya başlama](hdinsight-hadoop-linux-tutorial-get-started.md).
* HTML5'i destekleyen modern bir web tarayıcısı.

## <a name="understanding-tez"></a>Tez anlama

Tez geleneksel MapReduce işleme büyük hızlarından sağlayan hadoop'ta veri işleme için genişletilebilir bir çerçevedir. Linux tabanlı Hdınsight kümeleri için bunu hello varsayılan Hive için altyapısıdır.

Tez yönlendirilmiş Çevrimsiz grafik (Merhaba işlerinin gerekli eylemlerin sırasını açıklayan DAG) oluşturur. Tek tek Eylemler köşeleri olarak adlandırılır ve hello parçası yürütmek genel işi. Merhaba gerçek yürütme hello iş köşe tarafından tanımlanan bir görev çağrılır ve hello kümedeki birden çok düğüm arasında dağıtılmış.

### <a name="understanding-hello-tez-view"></a>Anlama hello Tez görünümü

Hello Tez görünümü, çalışan işlemler üzerinde hem geçmiş bilgileri hem de bilgi sağlar. Bu bilgileri, bir iş kümeler arasında nasıl dağıtıldığını gösterir. Ayrıca görevleri ve köşeleri tarafından kullanılan sayaçları görüntüler ve toohello iş ilgili hata bilgileri. Aşağıdaki senaryolar hello yararlı bilgiler teklif edebilir:

* Uzun süre çalışan işlemleri görüntüleme, izleme harita ilerlemesini hello ve görevleri azaltır.
* Başarılı veya başarısız işlemler toolearn ilişkin geçmiş verileri analiz etme işleme nasıl geliştirilmiş veya neden başarısız oldu.

## <a name="generate-a-dag"></a>Bir DAG oluştur

Merhaba Tez altyapısı kullanan bir iş hello görünüm yalnızca veri varsa, Tez çalışmakta olduğu veya sahip olan çalıştıran daha önce. Basit Hive sorguları, Tez kullanmadan çözülebilir. Daha karmaşık Bu filtreleme, gruplama, sıralama, birleşimler, vb. sorgular. Merhaba Tez altyapısını kullanır.

Aşağıdaki adımları toorun Tez kullanan bir Hive sorgusu hello kullan:

1. Toohttps://CLUSTERNAME.azurehdinsight.net, bir web tarayıcısında gidin nerede **CLUSTERNAME** Hdınsight kümenize hello adıdır.

2. Merhaba hello sayfanın üst kısmındaki hello Hello menüsünden seçin **görünümleri** simgesi. Bu simgeyi bir dizi kare gibi görünüyor. Görüntülenen hello açılır seçin **Hive görünümü**.

    ![Hive görünümünü seçme](./media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. Merhaba Hive görünümü yüklediğinde, Yapıştır hello aşağıdaki sorgu hello sorgu Düzenleyicisi'ni ve ardından **yürütme**.

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    Merhaba işi tamamlandıktan sonra hello görüntülenen hello çıktı görmeniz gerekir **sorgu işleminin sonuçları** bölümü. Merhaba sonuçları benzer toohello metin aşağıdaki gibi olmalıdır:

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. Select hello **günlük** sekmesi. Metin aşağıdaki bilgileri benzer toohello bakın:

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    Merhaba Kaydet **uygulama kimliği** olarak bu değer hello sonraki bölümde kullanılan değer.

## <a name="use-hello-tez-view"></a>Merhaba Tez görünüm kullanın

1. Merhaba hello sayfanın üst kısmındaki hello Hello menüsünden seçin **görünümleri** simgesi. Görüntülenen hello açılır seçin **Tez Görünüm**.

    ![Tez görünümü seçme](./media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. Merhaba Tez görünüm yüklediğinde, şu anda çalışmakta olan veya kaldırılmış hive sorguları listesini hello küme üzerinde çalışan bakın.

    ![Tüm DAG'leri](./media/hdinsight-debug-ambari-tez-view/tez-view-home.png)

3. Yalnızca bir giriş varsa, önceki bölümde hello çalıştırdığınız hello sorgu içindir. Birden çok girdi varsa, hello hello sayfanın başında hello alanlarını kullanarak arama yapabilirsiniz.

4. Select hello **sorgu kimliği** bir Hive sorgusu için. Merhaba sorgu ilgili bilgiler görüntülenir.

    ![DAG ayrıntıları](./media/hdinsight-debug-ambari-tez-view/query-details.png)

5. Bu sayfada Hello sekmeleri bilgisinden tooview hello izin ver:

    * **Sorgu ayrıntıları**: hello Hive sorgusu hakkında ayrıntılar.
    * **Zaman Çizelgesi**: her aşaması ne kadar sürdü hakkında bilgi.
    * **Yapılandırmaları**: Bu sorgu için kullanılan hello yapılandırma.

    Gelen __sorgu ayrıntıları__ hello bağlantılar toofind hello bilgilerini kullanabilirsiniz __uygulama__ veya hello __DAG__ bu sorgu için.
    
    * Merhaba __uygulama__ bağlantı hello bu sorgu için YARN uygulama hakkında daha fazla bilgi görüntüler. Buradan hello YARN uygulama günlüklerini erişebilir.
    * Merhaba __DAG__ bağlantı hello yönlendirilmiş Çevrimsiz grafik, bu sorgu için hakkında daha fazla bilgi görüntüler. Buradan, grafiksel hello DAG görüntüleyebilirsiniz. Ayrıca hello köşeleri hello DAG içinde hakkında bilgi bulabilirsiniz.

## <a name="next-steps"></a>Sonraki Adımlar

Toouse hello Tez nasıl görüntüleyebilirim öğrendiniz, daha fazla bilgi edinmek [hdınsight'ta Hive kullanarak](hdinsight-use-hive.md).

Daha ayrıntılı Tez teknik bilgi için bkz: Merhaba [Hortonworks Tez sayfanın](http://hortonworks.com/hadoop/tez/).

Ambari kullanarak Hdınsight ile ilgili daha fazla bilgi için bkz: [hello Ambari Web kullanıcı arabirimini kullanarak yönetin Hdınsight kümeleri](hdinsight-hadoop-manage-ambari.md)
