---
title: "Power BI - Azure Hdınsight'ta Apache Storm aaaUse | Microsoft Docs"
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
ms.openlocfilehash: 194cd8220bd60475af1d64a110e4b23ef92e1bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-toovisualize-data-from-an-apache-storm-topology"></a>Power BI toovisualize veri bir Apache Storm topolojisini kullanma

Power BI raporları gibi toovisually görüntü verileri sağlar. Bu belgede nasıl bir örnek sağlanmaktadır toogenerate verilerini Power BI Hdınsight üzerinde Apache Storm toouse.

> [!NOTE]
> Merhaba bu belgedeki adımları Visual Studio ile Windows geliştirme ortamına dayanır. Merhaba derlenmiş proje gönderilen tooa Linux tabanlı Hdınsight kümesi olabilir. Yalnızca Linux tabanlı kümelerde sonra 10/28/2016 desteği SCP.NET topolojileri oluşturulur.
>
> toouse güncelleştirme hello Microsoft.SCP.Net.SDK NuGet paketi, proje tooversion 0.10.0.6 tarafından kullanılan ya da daha yüksek bir Linux tabanlı kümesi içeren bir C# topolojisi. Merhaba hello paketin sürümü yüklü Hdınsight üzerinde Storm hello ana sürümüne de eşleşmelidir. Örneğin, HDInsight sürüm 3.3 ve 3.4 üzerindeki Strom bileşenleri, Storm 0.10.x sürümünü kullanırken HDInsight 3.5 ile Storm 1.0.x kullanılır.
>
> C# topolojileri Linux tabanlı kümelerde .NET 4.5 kullanın ve hello Hdınsight kümesinde Mono toorun kullanmanız gerekir. Çoğu şeyler çalışır. Merhaba ancak denetlemelisiniz [Mono Uyumluluk](http://www.mono-project.com/docs/about-mono/compatibility/) olası uyumsuzlukları belge.
>
> Windows tabanlı veya Linux tabanlı Hdınsight ile çalışır, bu proje için bir Java sürümü için bkz: [işlem Azure Event Hubs (Java) hdınsight'ta Storm olaylarından](hdinsight-storm-develop-java-event-hub-topology.md).

## <a name="prerequisites"></a>Ön koşullar

* Bir Azure Active Directory kullanıcı ile [Power BI](https://powerbi.com) erişim.
* Hdınsight kümesi. Daha fazla bilgi için bkz: [Hdınsight üzerinde Storm kullanmaya başlama](hdinsight-apache-storm-tutorial-get-started-linux.md).

  > [!IMPORTANT]
  > Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Visual Studio (sürümleri aşağıdaki hello biri)

  * Visual Studio 2012 ile [güncelleştirme 4](http://www.microsoft.com/download/details.aspx?id=39305)
  * Visual Studio 2013 [güncelleştirme 4](http://www.microsoft.com/download/details.aspx?id=44921) veya [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)
  * [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * Visual Studio 2017 (herhangi bir sürümünü)

* Visual Studio için Hdınsight araçları Hello: bkz [hello Hdınsight araçları Visual Studio için kullanmaya başlama](hdinsight-hadoop-visual-studio-tools-get-started.md) yükleme bilgileri hakkında bilgi için.

## <a name="how-it-works"></a>Nasıl çalışır?

Bu örnek, rasgele Internet Information Services (IIS) günlük verileri oluşturur bir C# Storm topolojisinin içerir. Bu veri sonra tooa SQL veritabanına yazılır ve isteğe bağlı olarak buradan kullanılan toogenerate raporlar Power bı'da değildir.

dosyalar uygulama hello ana işlevi bu örnekte aşağıdaki hello:

* **SqlAzureBolt.cs**: hello Storm topolojisini tooSQL veritabanı üretilen bilgilerini yazar.
* **IISLogsTable.sql**: hello veriler depolanır hello Transact-SQL deyimleri kullanılan toogenerate hello veritabanı.

> [!WARNING]
> Hdınsight kümenize hello topoloji başlatmadan önce SQL veritabanında Hello tablo oluşturun.

## <a name="download-hello-example"></a>Merhaba örneği indirin

Merhaba karşıdan [Hdınsight C# Storm Power BI örnek](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi). toodownload, ya da çatalı/kullanarak kopya [git](http://git-scm.com/), veya hello **karşıdan** bağlantı toodownload hello arşiv .zip.

## <a name="create-a-database"></a>Veritabanı oluşturma

1. bir veritabanı toocreate hello hello adımları kullanın [SQL Database Öğreticisi](../sql-database/sql-database-get-started.md) belge.

2. Connect toohello veritabanı aşağıdaki hello tarafından adımları hello [tooa SQL veritabanı ile Visual Studio bağlanmak](../sql-database/sql-database-connect-query.md) belge.

3. Nesne Gezgini'nde hello veritabanını sağ tıklatın ve seçin **yeni sorgu**. Yapıştır hello Merhaba içeriğine **IISLogsTable.sql** hello dahil dosya hello sorgu penceresine proje indirilir ve ardından kullanın Ctrl + Shift + E tooexecute hello sorgu. Komutlar başarıyla tamamlandı hello bir ileti alırsınız.

## <a name="configure-hello-sample"></a>Merhaba örnek yapılandırma

1. Merhaba gelen [Azure portal](https://portal.azure.com), SQL veritabanınızı seçin. Merhaba gelen **Essentials** hello SQL veritabanı dikey, select bölümünü **veritabanı bağlantı dizelerini Göster**. Görüntülenen hello listesinden hello kopyalama **ADO.NET (SQL kimlik doğrulaması)** bilgi.

2. Merhaba örnek Visual Studio'da açın. Gelen **Çözüm Gezgini**açın hello **App.config** dosya ve giriş aşağıdaki hello bulun:

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    Hello yerine **TOBEFILLED ##** hello veritabanı bağlantı dizesi değerle hello önceki adımda kopyaladığınız. Değiştir **{,\_kullanıcı adı}** ve **{,\_parola}** hello kullanıcı adı ve parola hello veritabanı için.

3. Kaydedin ve hello dosyaları kapatın.

## <a name="deploy-hello-sample"></a>Merhaba örnek dağıtma

1. Gelen **Çözüm Gezgini**, sağ hello **StormToSQL** proje ve seçin **hdınsight'ta tooStorm gönderme**. Select hello Hdınsight hello kümeden **Storm kümesi** iletişim kutusu açılır.

   > [!NOTE]
   > Merhaba birkaç saniye sürebilir **Storm kümesi** açılır toopopulate sunucu adları ile.
   >
   > İstenirse, Azure aboneliğinizin hello oturum açma kimlik bilgilerini girin. Birden fazla aboneliğiniz varsa, toohello Hdınsight kümesi üzerinde Storm'a içeren bir oturum açın.

2. Merhaba topoloji gönderildiğinde hello __topoloji Görüntüleyicisi__ görüntülenir. tooview bu topoloji, hello listesinden seçim hello SqlAzureWriterTopology girişi.

    ![Seçili hello topolojisi ile Merhaba topolojileri](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    Bu görünüm toosee bilgileri hello topolojisine kullanın veya bir giriş (örneğin, hello SqlAzureBolt) toosee bilgi belirli tooa bileşeni hello topolojisinde çift tıklatın.

3. Merhaba sonra topoloji sahip başlattıysanız birkaç dakika toocreate hello veritabanı kullanılan dönüş toohello SQL sorgu penceresi. Merhaba varolan deyimleri sorgu aşağıdaki hello ile değiştirin:

        select * from iislogs;

    Kullanın Ctrl + Shift + E tooexecute hello sorgu ve veri aşağıdaki sonuçları benzer toohello alırsınız:

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    Bu veriler hello Storm topolojisini yazılmış.

## <a name="create-a-report"></a>Bir rapor oluşturun

1. Toohello bağlanmak [Azure SQL Veritabanı Bağlayıcısı](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) Power BI için. 

2. İçinde **veritabanları**seçin **almak**.

3. Seçin **Azure SQL veritabanı**ve ardından **Bağlan**.

    > [!NOTE]
    > Toodownload hello Power BI Desktop toocontinue istenebilir. Bu durumda, aşağıdaki adımları tooconnect hello kullanın:
    >
    > 1. Power BI Desktop açıp seçin __Veri Al__.
    > 2 seçin __Azure__ve ardından __Azure SQL veritabanı__.

4. Merhaba bilgi tooconnect tooyour Azure SQL veritabanı girin. Merhaba ziyaret ederek bu bilgiyi bulabilirsiniz [Azure portal](https://portal.azure.com) ve SQL veritabanınız seçme.

   > [!NOTE]
   > Kullanarak hello yenileme aralığı ve özel filtreler de ayarlayabilirsiniz **Gelişmiş Seçenekler etkinleştirmek** iletişim hello bağlantı.

5. Bağlandıktan sonra yeni bir veri kümesi ile aynı hello veritabanı olarak bağlı adını hello görürsünüz. Bir rapor tasarlama hello dataset toobegin seçin.

6. Gelen **alanları**, hello genişletin **IISLOGS** girişi. listeleri URI hello rapor kaynaklandığını, toocreate hello onay kutusunu seçin **bulunamadı.%N**.

    ![Rapor oluşturma](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. Ardından, sürükleyin **yöntemi** toohello rapor. Merhaba rapor güncelleştirmeleri toolist hello kaynaklandığını ve hello karşılık gelen HTTP yöntemini hello HTTP isteği için kullanılır.

    ![Merhaba yöntemi veri ekleme](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. Merhaba gelen **görselleştirmeleri** sütun, select hello **alanları** simgesine ve ardından hello aşağı ok sonraki çok**yöntemi** hello içinde **değerleri**bölümü. bir URI kaç kez sayısına erişilmeden, toodisplay seçin **sayısı**.

    ![Yöntemleri tooa sayısını değiştirme](./media/hdinsight-storm-power-bi-topology/count.png)

9. Ardından, hello'ı seçin **yığılmış sütun grafiği** toochange hello bilgileri nasıl görüntülenir.

    ![Değişen tooa yığın grafik](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. toosave hello raporu, select **kaydetmek** ve hello rapor için bir ad girin.

## <a name="stop-hello-topology"></a>Merhaba topolojiyi durdurma

durdurmak veya Hdınsight kümesinde Storm hello silme kadar hello topoloji toorun devam eder. toostop topoloji Merhaba, hello aşağıdaki adımları gerçekleştirin:

1. Visual Studio'da toohello topoloji Görüntüleyicisi dönün ve hello topoloji seçin.

2. Select hello **KILL** düğmesini toostop hello topolojisi.

    ![Merhaba topoloji özeti düğmesini KILL](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a>Kümenizi Sil

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Sonraki adımlar

Bu belgede, öğrenilen nasıl toosend verilerini bir Storm topolojisini tooSQL veritabanını, sonra görselleştirmek Power BI kullanarak hello verileri. Hakkında bilgi için Hdınsight üzerinde Storm kullanarak diğer Azure teknolojileriyle toowork belge aşağıdaki hello bakın:

* [HDInsight üzerinde Storm için örnek topolojiler](hdinsight-storm-example-topology.md)
