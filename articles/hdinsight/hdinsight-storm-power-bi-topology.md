---
title: "Power BI - Azure Hdınsight Apache Storm kullanın | Microsoft Docs"
description: "Hdınsight'ta bir Apache Storm kümesi üzerinde çalışan bir C# topolojisi gelen verileri kullanarak bir Power BI raporu oluşturun."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 36fe3b9c-5232-4464-8d75-95403b6da7a1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/31/2017
ms.author: larryfr
ms.openlocfilehash: 36487c0c34e5a4bb955bbc15c8c96b9e838aeb44
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-power-bi-to-visualize-data-from-an-apache-storm-topology"></a>Apache Storm topolojisini verilerini görselleştirmek için Power BI kullanın

Power BI, raporları gibi veri görsel olarak görüntülemenizi sağlar. Bu belge, Hdınsight üzerinde Apache Storm için Power BI veri oluşturmak nasıl bir örnek sağlar.

> [!NOTE]
> Bu belgede yer alan adımlar Visual Studio ile Windows geliştirme ortamına dayanır. Linux tabanlı Hdınsight kümesi için derlenmiş proje gönderilebilir. Yalnızca Linux tabanlı kümelerde sonra 10/28/2016 desteği SCP.NET topolojileri oluşturulur.
>
> Bir C# topolojisi Linux tabanlı bir küme ile kullanmak için sürüm 0.10.0.6 için projeniz tarafından kullanılan ya da daha yüksek Microsoft.SCP.Net.SDK NuGet paketi güncelleştirme. Paketin sürümünün ayrıca HDInsight üzerinde yüklü olan Storm ana sürümüyle eşleşmesi gerekir. Örneğin, HDInsight sürüm 3.3 ve 3.4 üzerindeki Strom bileşenleri, Storm 0.10.x sürümünü kullanırken HDInsight 3.5 ile Storm 1.0.x kullanılır.
>
> Linux tabanlı kümelerdeki C# topolojilerinin .NET 4.5 kullanması ve HDInsight kümesi üzerinde çalışması için Mono kullanması gerekir. Çoğu şeyler çalışır. Ancak denetlemelisiniz [Mono Uyumluluk](http://www.mono-project.com/docs/about-mono/compatibility/) olası uyumsuzlukları belge.
>
> Windows tabanlı veya Linux tabanlı Hdınsight ile çalışır, bu proje için bir Java sürümü için bkz: [işlem Azure Event Hubs (Java) hdınsight'ta Storm olaylarından](hdinsight-storm-develop-java-event-hub-topology.md).

## <a name="prerequisites"></a>Ön koşullar

* Bir Azure Active Directory kullanıcı ile [Power BI](https://powerbi.com) erişim.
* Hdınsight kümesi. Daha fazla bilgi için bkz: [Hdınsight üzerinde Storm kullanmaya başlama](hdinsight-apache-storm-tutorial-get-started-linux.md).

  > [!IMPORTANT]
  > Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Visual Studio (aşağıdaki sürümlerinden biri)

  * Visual Studio 2012 ile [güncelleştirme 4](http://www.microsoft.com/download/details.aspx?id=39305)
  * Visual Studio 2013 [güncelleştirme 4](http://www.microsoft.com/download/details.aspx?id=44921) veya [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)
  * [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * Visual Studio 2017 (herhangi bir sürümünü)

* Visual Studio için Hdınsight araçları: bkz [Visual Studio için Hdınsight araçları kullanarak çalışmaya başlama](hdinsight-hadoop-visual-studio-tools-get-started.md) yükleme bilgileri hakkında bilgi için.

## <a name="how-it-works"></a>Nasıl çalışır?

Bu örnek, rasgele Internet Information Services (IIS) günlük verileri oluşturur bir C# Storm topolojisinin içerir. Bu veriler daha sonra bir SQL veritabanına yazılır ve buradan Power BI'da raporlar üretmek için kullanılır.

Aşağıdaki dosyaları bu örnek ana işlevlerini uygular:

* **SqlAzureBolt.cs**: SQL veritabanı için Storm topolojisinde üretilen bilgilerini yazar.
* **IISLogsTable.sql**: verileri depolanan veritabanı oluşturmak için kullanılan Transact-SQL deyimleri.

> [!WARNING]
> Tablo, SQL veritabanında topoloji Hdınsight kümenize başlatmadan önce oluşturun.

## <a name="download-the-example"></a>Örnek indirme

Karşıdan [Hdınsight C# Storm Power BI örnek](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi). İndirmek için ya da çatalı/kullanarak kopya [git](http://git-scm.com/), veya **karşıdan** arşivin bir .zip indirmek için bağlantı.

## <a name="create-a-database"></a>Veritabanı oluşturma

1. Bir veritabanı oluşturmak için adımlarda kullanmak [SQL Database Öğreticisi](../sql-database/sql-database-get-started.md) belge.

2. İçindeki adımları izleyerek veritabanına bağlan [Visual Studio ile SQL veritabanına bağlanma](../sql-database/sql-database-connect-query.md) belge.

3. Nesne Gezgini'nde veritabanını sağ tıklatın ve seçin **yeni sorgu**. İçeriğini Yapıştır **IISLogsTable.sql** dosya sorgu penceresine indirilen projeye dahil ve ardından sorguyu yürütmek için Ctrl + Shift + E kullanın. Komutların başarıyla tamamlandığını bir ileti alırsınız.

## <a name="configure-the-sample"></a>Örnek yapılandırma

1. Gelen [Azure portal](https://portal.azure.com), SQL veritabanınızı seçin. Gelen **Essentials** select SQL veritabanı dikey bölümünü **veritabanı bağlantı dizelerini Göster**. Görüntülenen listesinden kopyalama **ADO.NET (SQL kimlik doğrulaması)** bilgi.

2. Örnek Visual Studio'da açın. Gelen **Çözüm Gezgini**, açık **App.config** dosya ve şu girişi bulun:

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    Değiştir **TOBEFILLED ##** veritabanı bağlantı dizesi değerle önceki adımda kopyaladığınız. Değiştir **{,\_kullanıcı adı}** ve **{,\_parola}** kullanıcı adı ve parola veritabanı için.

3. Kaydedin ve dosyaları kapatın.

## <a name="deploy-the-sample"></a>Örnek dağıtma

1. Gelen **Çözüm Gezgini**, sağ **StormToSQL** proje ve seçin **Hdınsight üzerinde Storm Gönder**. Hdınsight küme seçin **Storm kümesi** iletişim kutusu açılır.

   > [!NOTE]
   > Bu işlem birkaç saniye sürebilir **Storm kümesi** sunucu adlarıyla doldurmak için açılır.
   >
   > İstenirse, Azure aboneliğiniz için oturum açma kimlik bilgilerini girin. Birden fazla aboneliğiniz varsa, Hdınsight kümesi üzerinde Storm'a içeren oturum açın.

2. Topoloji gönderildiğinde __topoloji Görüntüleyicisi__ görüntülenir. Bu topoloji görüntülemek için listeden SqlAzureWriterTopology girişi seçin.

    ![Seçili topolojisi ile topolojileri](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    Topolojisi hakkında bilgi için bu görünümü kullanın veya bir bileşen topolojisinde özgü bilgileri görmek için bir giriş (örneğin, SqlAzureBolt) çift tıklatın.

3. Birkaç dakika, veritabanı oluşturmak için kullanılan SQL sorgu penceresine dönüş topolojisine sahip sonra verdi. Varolan deyimleri aşağıdaki sorguyla değiştirin:

        select * from iislogs;

    Kullanım Ctrl + Shift + E sorgu ve çalıştırmak için aşağıdaki veri benzer sonuçlar almanız gerekir:

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    Bu veri Storm topolojisini yazılmış.

## <a name="create-a-report"></a>Bir rapor oluşturun

1. Bağlanmak [Azure SQL Veritabanı Bağlayıcısı](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) Power BI için. 

2. İçinde **veritabanları**seçin **almak**.

3. Seçin **Azure SQL veritabanı**ve ardından **Bağlan**.

    > [!NOTE]
    > Devam etmek için Power BI Desktop'u indirin istenebilir. Bu durumda, bağlanmak için aşağıdaki adımları kullanın:
    >
    > 1. Power BI Desktop açıp seçin __Veri Al__.
    > 2 seçin __Azure__ve ardından __Azure SQL veritabanı__.

4. Azure SQL veritabanınıza bağlanmak için gereken bilgileri girin. Ziyaret ederek bu bilgiyi bulabilirsiniz [Azure portal](https://portal.azure.com) ve SQL veritabanınız seçme.

   > [!NOTE]
   > Kullanarak yenileme aralığı ve özel filtreler de ayarlayabilirsiniz **Gelişmiş Seçenekler etkinleştirmek** Bağlan iletişim kutusundan.

5. Bağlı sonra bağlı veritabanı olarak aynı ada sahip yeni bir veri kümesi görürsünüz. Bir rapor tasarlamaya başlamak için veri kümesini seçin.

6. Gelen **alanları**, genişletin **IISLOGS** girişi. URI gövdelerini listeleyen bir rapor oluşturmak için onay kutusunu seçin **bulunamadı.%N**.

    ![Rapor oluşturma](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. Ardından, sürükleyin **yöntemi** rapor. Gövdelerini ve HTTP isteği için kullanılan karşılık gelen HTTP yöntemini listelemek için rapor güncelleştirir.

    ![yöntem veri ekleme](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. Gelen **görselleştirmeleri** sütun seçin **alanları** simgesini ve sonra aşağı oka yanına seçin **yöntemi** içinde **değerleri** bölümü. Bir URI erişilen kaç kez sayısını görüntülemek için seçin **sayısı**.

    ![İçin yöntemleri sayısını değiştirme](./media/hdinsight-storm-power-bi-topology/count.png)

9. Ardından, **yığılmış sütun grafiği** bilgilerin nasıl görüntüleneceğini değiştirmek için.

    ![Yığılmış grafiğe değiştirme](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. Raporu kaydetmek için seçin **kaydetmek** ve rapor için bir ad girin.

## <a name="stop-the-topology"></a>Topolojiyi durdurma

Topoloji, durdurmak veya Hdınsight kümesinde Storm silmek kadar çalışmaya devam eder. Topoloji durdurmak için aşağıdaki adımları gerçekleştirin:

1. Visual Studio'da topoloji görüntüleyiciye dönün ve topolojiyi seçin.

2. Seçin **KILL** topolojiyi durdurma düğmesi.

    ![Özet topoloji düğmesini KILL](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a>Kümenizi Sil

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Sonraki adımlar

Bu belgede, bir Storm topolojisinin SQL veritabanına veri göndermek ve Power BI kullanarak verileri Görselleştir öğrendiniz. Hdınsight üzerinde Storm kullanarak diğer Azure teknolojileri ile çalışma konusunda daha fazla bilgi için aşağıdaki belgesine bakın:

* [HDInsight üzerinde Storm için örnek topolojiler](hdinsight-storm-example-topology.md)
