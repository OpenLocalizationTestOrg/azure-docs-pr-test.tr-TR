---
title: "Hdınsight üzerinde Storm ve HBase ile zamanla aaaCorrelate olayları"
description: "Bilgi nasıl Hdınsight üzerinde Storm ve HBase kullanarak farklı zamanlarda gelmesini toocorrelate olaylar."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 17d11479-2d02-4790-8d29-05fb38351479
ms.service: hdinsight
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: f915eef77bbda5b02bfd02ad0b5a4923ff2f4f26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="correlate-events-that-arrive-at-different-times-using-storm-and-hbase"></a>Farklı zamanlarda geldiğinde olayları ilişkilendirmenize Storm ve HBase kullanma

Apache Storm ile kalıcı veri deposu kullanarak, farklı zamanlarda gelmesini veri girişi ilişkilendirebilirsiniz. Örneğin, bir kullanıcı oturumu toocalculate için oturum açma ve kapatma olayları nasıl uzun hello oturum bağlama devam.

Bu belgede, bilgi nasıl toocreate kullanıcı oturumları için oturum açma ve kapatma olayları izler ve hello süresini hello oturumunun hesaplar temel bir Storm C# topolojisi. Merhaba topolojisi HBase kalıcı veri deposu olarak kullanır. HBase tooperform Toplu sorguları hello geçmiş verileri tooproduce ek Öngörüler üzerinde sağlar. Örneğin, kaç kullanıcı oturumlarını başlatıldı veya belirli bir süre içinde sona erdi.

## <a name="prerequisites"></a>Ön koşullar

* Hdınsight için Visual Studio Araçları, Visual Studio ve hello. Daha fazla bilgi için bkz: [hello Hdınsight araçları Visual Studio için kullanmaya başlama](hdinsight-hadoop-visual-studio-tools-get-started.md).

* Hdınsight üzerinde Apache Storm küme (Windows tabanlı).

  > [!WARNING]
  > 28/10/2016 sonrasında oluşturulan Linux tabanlı Storm kümeleri üzerinde SCP.NET topolojileri destekleniyorsa hello HBase SDK 28/10/2016 itibariyle kullanılabilir .NET paketi için Linux tabanlı Hdınsight üzerinde düzgün çalışmıyor

* Hdınsight kümesi üzerinde Apache HBase (Linux veya Windows tabanlı).

  > [!IMPORTANT]
  > Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* [Java](https://java.com) 1,7 veya geliştirme ortamınız üzerinde daha büyük. Gönderilen toohello Hdınsight kümesi olduğunda Java kullanılan toopackage hello topolojisi olur.

  * Merhaba **JAVA_HOME** Java içeren ortam değişkeni gereken noktası toohello dizini.
  * Merhaba **%JAVA_HOME%/bin** directory hello yolunda olması gerekir

## <a name="architecture"></a>Mimari

![Merhaba topoloji aracılığıyla hello veri akışı diyagramı](./media/hdinsight-storm-correlation-topology/correlationtopology.png)

Olayları bağıntı ortak bir tanımlayıcı için hello olay kaynağı gerektirir. For example, bir kullanıcı kimliği, oturum kimliği veya diğer veri parçası a) benzersiz ve (b) dahil tüm gönderilen veriler tooStorm olmasıdır. Bu örnek, bir oturum kimliği bir GUID değeri toorepresent kullanır

Bu örnekte, iki Hdınsight kümeleri oluşur:

* HBase: geçmiş verileri kalıcı veri deposu
* Storm: tooingest gelen veri kullanılan

Merhaba veri rastgele hello Storm topolojisini tarafından oluşturulan ve aşağıdaki öğelerindeki Merhaba oluşur:

* Oturum kimliği: her oturuma benzersiz olarak tanımlayan bir GUID
* Olay: bir başlangıç veya bitiş olayı. Bu örnekte, başlangıç her zaman son önce gerçekleşir.
* Süresi: Merhaba olay hello zamanı.

Bu veriler işlenir ve HBase depolanır.

### <a name="storm-topology"></a>Storm topolojisi

Bir oturum başlatıldığında bir **Başlat** olay hello topolojisi tarafından alınır ve tooHBase oturum. Zaman bir **son** olayı alındığında, hello topoloji alır hello **Başlat** olay ve hello iki olaylar arasındaki süreyi hello hesaplar. Bu **süresi** değeri HBase sonra hello birlikte depolanır **son** olay bilgileri.

> [!IMPORTANT]
> Bu topoloji hello temel düzeni gösterir, ancak bir üretim çözüm senaryoları aşağıdaki Merhaba tootake tasarım gerekir:
>
> * Sıralama dışında gelen olayları
> * Yinelenen olay
> * Bırakılan olayları

Merhaba örnek topoloji bileşenleri aşağıdaki Merhaba oluşur:

* Session.cs: bir kullanıcı oturumunu Başlat zaman ve ne kadar süreyle hello oturum lasts bir rastgele oturum kimliği oluşturarak benzetimini yapar.

* Spout.cs: 100 oturum oluşturur, başlangıç olayı yayar, her oturum için hello rastgele zaman aşımı bekler ve bitiş olayı yayar. Ardından dönüştürür oturumları toogenerate yenilerini sona erdi.

* HBaseLookupBolt.cs: HBase oturum bilgi hello oturum kimliği toolook kullanır. Bitiş Olayı işlendiğinde hello karşılık gelen başlangıç olayı bulur ve hello süresini hello oturumunun hesaplar.

* HBaseBolt.cs: HBase bilgileri depolar.

* TypeHelper.cs: okuma / yazma tooHBase türü dönüştürme işlemine yardımcı olur.

### <a name="hbase-schema"></a>HBase şema

İçinde HBase, hello veriler ile Merhaba şema/ayarları aşağıdaki tabloda saklanır:

* Satır anahtarını: hello oturum kimliği için bu tablodaki satırları hello anahtar olarak kullanılır.

* Sütun ailesi: hello aile adı olan 'cf'. Bu serideki depolanan sütunlar şunlardır:

  * olay: başlangıç veya bitiş.

  * saat: hello zaman olay hello milisaniye cinsinden.

  * süre: Merhaba başlangıç ve bitiş olayı arasındaki uzunluğu.

* SÜRÜMLER: hello 'cf' ailesi her satır tooretain 5 sürümleri ayarlanır.

  > [!NOTE]
  > Günlük için belirli satır anahtarını depolanan önceki değerlerin sürümleridir. Varsayılan olarak, HBase, yalnızca bir satır en son sürümünü hello hello değerini döndürür. Bu durumda, hello aynı satır her bir satır sürümü hello zaman damgası değeri tarafından tanımlanan tüm olayları (başlatma, End) için kullanılır. Sürümleri için belirli bir kimliği günlüğe kaydedilen olayları bir geçmiş görünümünü sağlar

## <a name="download-hello-project"></a>Merhaba projenizi indirin

Merhaba örnek proje adresinden yüklenebilir [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).

Bu yükleme, C# projeleri aşağıdaki hello içerir:

* CorrelationTopology: rastgele kullanıcı oturumları için başlangıç ve bitiş olayları yayar C# Storm topolojisini. Her oturum arasındaki 1 ve 5 dakika sürer.

* SessionInfo: Merhaba HBase tablo oluşturur ve örnek sorguları saklı oturum verilerini tooreturn bilgilerini sağlayan C# konsol uygulaması.

## <a name="create-hello-table"></a>Merhaba tablosu oluşturma

1. Açık hello **SessionInfo** Visual Studio projesi.

2. İçinde **Çözüm Gezgini**, sağ hello **SessionInfo** proje ve seçin **özellikleri**.

    ![Seçili özellikleriyle menüsünün ekran görüntüsü](./media/hdinsight-storm-correlation-topology/selectproperties.png)

3. Seçin **ayarları**, sonra kümesi hello aşağıdaki değerler:

   * HBaseClusterURL: hello URL tooyour HBase kümesi. Örneğin, https://myhbasecluster.azurehdinsight.net.

   * HBaseClusterUserName: kümeniz Merhaba yönetici/HTTP kullanıcı hesabı

   * HBaseClusterPassword: hello hello yönetici/HTTP kullanıcı hesabının parolasını

   * HBaseTableName: Bu örnekle hello tablo toouse hello adı

   * HBaseTableColumnFamily: hello sütun ailesi adı

     ![Ayarları iletişim kutusu görüntüsü](./media/hdinsight-storm-correlation-topology/settings.png)

4. Merhaba çözümü çalıştırın. İstendiğinde, hello 'c' anahtar toocreate hello tablosunda HBase kümesi seçin.

## <a name="build-and-deploy-hello-storm-topology"></a>Derleme ve hello Storm topolojisini dağıtma

1. Açık hello **CorrelationTopology** Visual Studio'da çözüm.

2. İçinde **Çözüm Gezgini**, sağ hello **CorrelationTopology** proje ve Özellikler'i seçin.

3. Merhaba Özellikler penceresinde seçin **ayarları** ve bu proje için hello yapılandırma değerlerini girin. Merhaba ilk 5 olan hello tarafından kullanılan aynı değerleri hello **SessionInfo** proje:

   * HBaseClusterURL: hello URL tooyour HBase kümesi. Örneğin, https://myhbasecluster.azurehdinsight.net.

   * HBaseClusterUserName: kümeniz Merhaba yönetici/HTTP kullanıcı hesabı.

   * HBaseClusterPassword: hello Yöneticisi/HTTP kullanıcı hesabı hello parola.

   * HBaseTableName: Bu örnekle hello tablo toouse hello adı. Bu değer aynı hello olduğu hello SessionInfo projesinde kullanılan tablo adı.

   * HBaseTableColumnFamily: hello sütun ailesi adı. Bu değer aynı hello olan sütun ailesi hello SessionInfo projesinde kullanılan adı.

   > [!IMPORTANT]
   > Tarafından kullanılan hello adlarını Hello varsayılan değerler olarak hello HBaseTableColumnNames, değiştirmeyin **SessionInfo** tooretrieve veri.

4. Merhaba özellikleri kaydedin, sonra Merhaba projeyi oluşturun.

5. İçinde **Çözüm Gezgini**, hello projesine sağ tıklatın ve **hdınsight'ta tooStorm gönderme**. İstenirse, Azure aboneliğinizin hello kimlik bilgilerini girin.

   ![Merhaba görüntüsü gönderme toostorm menü öğesi](./media/hdinsight-storm-correlation-topology/submittostorm.png)

6. Merhaba, **gönderme topoloji** iletişim, bu topolojiyle toodeploy istediğiniz select hello Storm kümesi.

   > [!NOTE]
   > Merhaba ilk kez bir topoloji göndermek, birkaç saniye tooretrieve hello Hdınsight kümelerinizi adını sürebilir.

7. Merhaba topoloji gönderilen ve karşıya toohello küme silindikten sonra hello **Storm topoloji görünümü** açar ve topoloji çalıştıran hello görüntüler. toorefresh hello veri, select hello **CorrelationTopology** ve hello hello Yenile düğmesini kullanın hello sayfasının sağ üst.

   ![Merhaba topoloji görünümü görüntüsü](./media/hdinsight-storm-correlation-topology/topologyview.png)

   Merhaba topoloji bir veri üreterek başladığında hello değerinde hello **Emitted** sütun artırır.

   > [!NOTE]
   > Merhaba, **Storm topoloji görünümü** yok otomatik olarak açmak, kullanın hello adımları tooopen onu:
   >
   > 1. İçinde **Çözüm Gezgini**, genişletin **Azure**, genişletin ve ardından **Hdınsight**.
   > 2. Topoloji hello sağ hello Storm kümesi üzerinde çalışan ve ardından **görünüm Storm topolojileri**

## <a name="query-hello-data"></a>Merhaba verileri Sorgulama

Veri yayılan sonra aşağıdaki adımları tooquery hello veri hello kullanın.

1. Toohello iade **SessionInfo** projesi. Çalıştıran yeni bir örneğini başlatabilirsiniz.

2. İstendiğinde, seçin **s** toosearch başlangıç olayı. Bir başlangıç istendiğinde tooenter olan ve zaman toodefine bir zaman aralığı - end bu iki kez arasındaki yalnızca olayları döndürülür.

    Kullanım hello aşağıdaki hello başlangıç girerken biçimlendirmek ve bitiş zamanları: ss: dd ve ''M' veya 'pm'. Örneğin, 23:20:00.

    oturum tooreturn olayları hello Storm topolojisini dağıtıldı önce bir başlangıç saati ve şimdi bir bitiş saatini kullanın. Merhaba dönüş verileri metin aşağıdaki girişleri benzer toohello içerir:

        Session e6992b3e-79be-4991-afcf-5cb47dd1c81c started at 6/5/2015 6:10:15 PM. Timestamp = 1433527820737

Son olayları works hello için aynı başlangıç olayları olarak aranıyor. Ancak, son olayları hello başlangıç olayından sonra 1 ile 5 dakika arasında rastgele oluşturulur. Birkaç zaman aralıkları toofind hello bitiş olayları tootry olabilir. Bitiş olayları hello oturum - hello başlangıç olay zamanı ve bitiş olay saati arasındaki farkı hello hello süresini de içerir. Bitiş olayları için verileri bir örneği burada verilmiştir:

    Session fc9fa8e6-6892-4073-93b3-a587040d892e lasted 2 minutes, and ended at 6/5/2015 6:12:15 PM

> [!NOTE]
> Girdiğiniz hello saat değerlerini yerel saat olsa da, hello sorgusundan döndürülen hello UTC saattir.

## <a name="stop-hello-topology"></a>Merhaba topolojiyi durdurma

Hazır toostop hello topoloji olduğunda toohello dönmek **CorrelationTopology** Visual Studio projesi. Merhaba, **Storm topoloji görünümü**, hello topoloji seçin ve ardından hello **KILL** hello topoloji görünümü hello üstündeki düğmesi.

## <a name="delete-your-cluster"></a>Kümenizi Sil

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Sonraki adımlar

Daha fazla Storm örnekler için bkz: [Hdınsight üzerinde Storm için örnek topolojiler](hdinsight-storm-example-topology.md).
