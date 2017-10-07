---
title: "aaaCreate bir Java Azure Cosmos DB grafik veritabanıyla | Microsoft Docs"
description: "Java kod tooconnect tooand sorgu grafik verileri Azure Cosmos Gremlin kullanarak DB'de kullanabileceğiniz örnek sayısını gösterir."
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/24/2017
ms.author: denlee
ms.openlocfilehash: 595c0fb108f3dbe8c83674f0c9c4b0cdd3ab4c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-graph-database-using-java-and-hello-azure-portal"></a>Azure Cosmos DB: Java kullanarak bir grafik veritabanı oluşturmak ve Azure portal hello

Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir. Hızlı bir şekilde oluşturmak ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz. 

Bu hızlı başlangıç bir grafik oluşturur Azure Cosmos DB hello Azure portal araçları veritabanını kullanma. Bu hızlı başlangıç ayrıca tooquickly hello OSS kullanarak bir grafik veritabanını kullanarak bir Java konsol uygulaması oluşturma nasıl gösterilmektedir [Gremlin Java](https://mvnrepository.com/artifact/org.apache.tinkerpop/gremlin-driver) sürücü. Bu hızlı başlangıç içinde Hello yönergeler Java çalıştırabilen tüm işletim sisteminde izlenebilir. Bu hızlı başlangıç oluşturma ve grafik kaynaklarında hello UI veya program aracılığıyla, tercihinize hangisi değiştirme ile familiarizes. 

## <a name="prerequisites"></a>Ön koşullar

* [Java Development Kit (JDK) 1.7+](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * Ubuntu üzerinde çalıştırmak `apt-get install default-jdk` tooinstall hello JDK.
    * Emin tooset hello JAVA_HOME ortam değişkeni toopoint toohello klasörü hello JDK'ın yüklendiği olabilir.
* Bir [Maven](http://maven.apache.org/) ikili arşivi [indirin](http://maven.apache.org/download.cgi) ve [yükleyin](http://maven.apache.org/install.html)
    * Ubuntu üzerinde çalıştırdığınız `apt-get install maven` tooinstall Maven.
* [Git](https://www.git-scm.com/)
    * Ubuntu üzerinde çalıştırdığınız `sudo apt-get install git` tooinstall Git.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Veritabanı hesabı oluşturma

Bir grafik veritabanı oluşturabilmeniz için önce toocreate Azure Cosmos DB ile Gremlin (grafiği) veritabanı hesabı gerekir.

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>Grafik ekleme

Artık hello Azure portal toocreate bir grafik veritabanı hello Veri Gezgini aracını kullanabilirsiniz. 

1. Merhaba hello sol gezinti menüsünde, Azure portal'ı tıklatın **Veri Gezgini (Önizleme)**. 
2. Merhaba, **Veri Gezgini (Önizleme)** dikey penceresinde tıklatın **yeni bir grafik**, aşağıdaki bilgilerle hello kullanarak hello sayfasında doldurun:

    ![Hello Azure portal'ın Veri Gezgini](./media/create-graph-java/azure-cosmosdb-data-explorer.png)

    Ayar|Önerilen değer|Açıklama
    ---|---|---
    Veritabanı Kimliği|sample-database|Yeni veritabanı Hello kimliği. Veritabanı adı 1 ile 255 karakter arasında olmalı, `/ \ # ?` içermemeli ve boşlukla bitmemelidir.
    Grafik Kimliği|sample-graph|Merhaba kimliği, yeni bir grafik. Grafik adlara sahip hello veritabanı kimlikleri aynı karakter gereksinimleri.
    Depolama Kapasitesi| 10 GB|Merhaba varsayılan değeri bırakın. Merhaba depolama kapasitesi hello veritabanının budur.
    Aktarım hızı|400 RU|Merhaba varsayılan değeri bırakın. Tooreduce gecikme istiyorsanız hello verimlilik daha sonra ölçeklendirebilirsiniz.
    Bölüm anahtarı|Boş bırakın|Bu hızlı başlangıç Hello amaçla hello bölüm anahtarı boş bırakın.

3. Merhaba form doldurulur sonra tıklayın **Tamam**.

## <a name="clone-hello-sample-application"></a>Merhaba örnek uygulaması kopyalama

Şimdi şimdi kopyalama bir grafik uygulaması github'dan hello bağlantı dizesini ayarlamak ve çalıştırın. Ne kadar kolay toowork verilerle program aracılığıyla olduğunu görürsünüz. 

1. Git bash gibi bir git terminal penceresi açın ve `cd` tooa çalışma dizini.  

2. Çalışma hello aşağıdaki tooclone hello örnek depo komutu. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started.git
    ```

## <a name="review-hello-code"></a>Merhaba kod gözden geçirme

Neler olduğuna dair hello uygulamada hızlı bir gözden geçirme olalım. Açık hello `Program.java` dosya hello \src\GetStarted klasöründen ve bu kod satırları bulur. 

* Merhaba Gremlin `Client` hello yapılandırmadan başlatılmış `src/remote.yaml`.

    ```java
    cluster = Cluster.build(new File("src/remote.yaml")).create();
    ...
    client = cluster.connect();
    ```

* Bir dizi Gremlin adımı hello kullanarak yürütülme `client.submit` yöntemi.

    ```java
    ResultSet results = client.submit(gremlin);

    CompletableFuture<List<Result>> completableFutureResults = results.all();
    List<Result> resultList = completableFutureResults.get();

    for (Result result : resultList) {
        System.out.println(result.toString());
    }
    ```

## <a name="update-your-connection-string"></a>Bağlantı dizenizi güncelleştirme

1. Açık hello src/remote.yaml dosyası. 

3. Doldurun, *ana*, *kullanıcıadı*, ve *parola* hello src/remote.yaml dosyasındaki değerleri. Merhaba rest hello ayarlarının değiştirilen toobe gerek yoktur.

    Ayar|Önerilen değer|Açıklama
    ---|---|---
    Ana bilgisayarlar|[***.graphs.azure.com]|Bu tablodan sonraki hello ekran görüntüsüne bakın. Bu değer hello Gremlin URI hello hello sondaki ile köşeli ayraçlar içinde Azure Portalı'nın hello genel bakış sayfasında değerdir: 443 / kaldırıldı.<br><br>Bu değer ayrıca hello anahtarları sekmesinden, https:// kaldırma belgeleri toographs değiştirme ve hello sondaki kaldırma hello URI değeri kullanılarak alınabilir: 443 /.
    Kullanıcı adı|/dbs/sample-database/colls/sample-graph|Merhaba hello formunun kaynak `/dbs/<db>/colls/<coll>` nerede `<db>` varolan veritabanı adınız ve `<coll>` varolan koleksiyon adı.
    Parola|*Birincil ana anahtarınız*|Bu tablodan sonraki hello ikinci ekran görüntüsüne bakın. Bu değer, hello hello birincil anahtar kutusunda Azure portal hello anahtarları sayfasından alabilirsiniz, birincil anahtar olur. Merhaba kutusunun sağ tarafında üzerinde hello Hello Kopyala düğmesini kullanarak hello değerini kopyalayın.

    Merhaba Hello konakları değerini kopyalayın **Gremlin URI** başlangıç değerinden **genel bakış** sayfası. Boşsa, hello yönergeler hello konakları hello anahtarlar dikey penceresinden hello Gremlin URI oluşturma hakkında daha fazla tablo önceki hello satırda bakın.
![Hello Azure portal'hello genel bakış sayfasında hello Gremlin URI değeri görüntüleme ve kopyalama](./media/create-graph-java/gremlin-uri.png)

    Merhaba Hello parola değerini kopyalayın **birincil anahtar** hello gelen **anahtarları** dikey: ![görüntüleme ve kopyalama birincil anahtarınızı hello Azure portal, anahtarları sayfası](./media/create-graph-java/keys.png)

## <a name="run-hello-console-app"></a>Merhaba konsol uygulamasını çalıştırın

1. Penceresinde hello git terminal `cd` toohello azure-cosmos-db-graph-java-getting-started klasör.

2. Merhaba git terminal penceresinde yazın `mvn package` tooinstall hello Java paketleri gereklidir.

3. Merhaba git terminal penceresinde çalıştırın `mvn exec:java -D exec.mainClass=GetStarted.Program` içinde Java uygulamanız terminal penceresi toostart hello.

Merhaba terminal penceresi toohello grafik eklenmekte olan hello Köşeleri görüntüler. Merhaba program işlemi tamamlandıktan sonra geri toohello Azure portal, Internet tarayıcınızda geçin. 

<a id="add-sample-data"></a>
## <a name="review-and-add-sample-data"></a>Örnek verileri inceleme ve ekleme

Şimdi tooData Explorer geri dönün ve hello köşeleri toohello grafik eklenir ve ek veri noktaları ekleme bakın.

1. Veri Gezgini'nde hello genişletin **örnek veritabanı**/**örnek grafik**, tıklatın **grafik**ve ardından **Filtre Uygula**. 

   ![Yeni belgeler veri Gezgini'nde hello Azure portal oluşturun.](./media/create-graph-java/azure-cosmosdb-data-explorer-expanded.png)

2. Merhaba, **sonuçları** listesinde, hello yeni kullanıcılar eklenen toohello grafik dikkat edin. Seçin **ben** ve kendisine toorobin bağlandı dikkat edin. Merhaba köşeleri hello graph Explorer'a üzerinde hareket ettirin, yakınlaştırma ve uzaklaştırma ve hello grafik explorer yüzeyine hello boyutunu genişletin. 

   ![Merhaba grafikte veri Explorer'da hello Azure portalında yeni tepe](./media/create-graph-java/azure-cosmosdb-graph-explorer-new.png)

3. Merhaba Veri Gezgini'ni kullanarak, birkaç, yeni kullanıcılar toohello grafik ekleyelim. Merhaba tıklatın **yeni köşe** düğmesini tooadd veri tooyour grafiği.

   ![Yeni belgeler veri Gezgini'nde hello Azure portal oluşturun.](./media/create-graph-java/azure-cosmosdb-data-explorer-new-vertex.png)

4. Bir etiketi girin *kişi* aşağıdaki anahtarları ve toocreate hello ilk köşe hello grafikteki değerleri hello girin. Grafikteki her kişi için benzersiz özellikler oluşturabileceğinizi görürsünüz. Yalnızca hello kimliği anahtar gereklidir.

    anahtar|değer|Notlar
    ----|----|----
    id|ashley|Merhaba hello köşe için benzersiz tanımlayıcı. Kimlik belirtmezseniz, bir kimlik otomatik olarak oluşturulur.
    cinsiyet|kadın| 
    teknoloji | java | 

    > [!NOTE]
    > Bu hızlı başlangıçta bölümlenmemiş bir koleksiyon oluşturacağız. Merhaba koleksiyonu oluşturma sırasında bir bölüm anahtarı belirterek bölümlendirilmiş bir koleksiyon oluşturursanız, ancak, ardından tooinclude hello bölüm anahtarı bir anahtar olarak her yeni köşe gerekir. 

5. **Tamam** düğmesine tıklayın. Ekran toosee tooexpand gerekebilir **Tamam** hello ekranın hello üzerinde.

6. Tekrar **Yeni Köşe**’ye tıklayın ve ek yeni kullanıcıyı ekleyin. Bir etiketi girin *kişi* hello aşağıdaki enter anahtarları ve değerleri:

    anahtar|değer|Notlar
    ----|----|----
    id|rakesh|Merhaba hello köşe için benzersiz tanımlayıcı. Kimlik belirtmezseniz, bir kimlik otomatik olarak oluşturulur.
    cinsiyet|erkek| 
    okul|MIT| 

7. **Tamam** düğmesine tıklayın. 

8. Tıklatın **Filtre Uygula** hello varsayılan ile `g.V()` Filtresi. Tüm hello kullanıcıların artık Göster hello **sonuçları** listesi. Daha fazla veri ekleme gibi filtreler toolimit sonuçlarınızı kullanabilirsiniz. Varsayılan olarak, Veri Gezgini kullanır `g.V()` tooretrieve bu tooa farklı bir grafik, ancak tüm tepe değiştirebilirsiniz [grafik sorgu](tutorial-query-graph.md), gibi `g.V().count()`, tooreturn JSON biçiminde hello grafik tüm hello tepe sayısı.

9. Artık rakesh ve ashley arasında bağlantı kurabiliriz. Olun **ashley** hello seçili **sonuçları** listesinde, İleri'yi hello Düzenle düğmesi çok tıklatın**hedefleri** alt sağ tarafında. Pencere toosee hello toowiden gerekebilir **özellikleri** alanı.

   ![Merhaba hedef grafikteki bir köşesinin değiştirme](./media/create-graph-java/azure-cosmosdb-data-explorer-edit-target.png)

10. Merhaba, **hedef** kutusuna yazın *rakesh*ve hello **kenar etiket** kutusuna yazın *bilir*ve ardından hello onay kutusuna tıklayın.

   ![Veri Gezgininde ashley ve rakesh arasında bir bağlantı ekleyin](./media/create-graph-java/azure-cosmosdb-data-explorer-set-target.png)

11. Şimdi seçin **rakesh** hello sonuçları listesi ve ashley ve rakesh bağlı olup olmadığını bakın. 

   ![Veri Gezgini'nde bağlı iki köşe](./media/create-graph-java/azure-cosmosdb-graph-explorer.png)

    Ayrıca Veri Gezgini toocreate saklı yordamlar, UDF'ler ve Tetikleyicileri tooperform sunucu tarafı iş mantığı da kullanabilirsiniz ölçek işleme olarak. Veri Gezgini tüm hello yerleşik programlı veri erişim hello API'leri kullanılabilir gösterir, ancak tooyour verileri hello Azure portalında kolay erişim sağlar.



## <a name="review-slas-in-hello-azure-portal"></a>Gözden geçirme SLA'hello Azure portalı

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Kaynakları temizleme

Toocontinue toouse bu uygulamayı değil kullanacaksanız, bu hızlı başlangıç tarafından hello Azure portalında aşağıdaki adımları hello ile oluşturulan tüm kaynakları silin: 

1. Merhaba sol taraftaki menüden hello Azure portal'ın, **kaynak grupları** ve ardından oluşturduğunuz hello kaynak hello adına tıklayın. 
2. Kaynak grubu sayfanızda tıklatın **silmek**hello metin kutusuna hello kaynak toodelete hello adını yazın ve ardından **silmek**.

## <a name="next-steps"></a>Sonraki adımlar

Bu hızlı başlangıç toocreate bir Azure Cosmos DB hesap hello Veri Gezgini'ni kullanarak bir grafik oluşturma ve bir uygulama çalıştırmasına öğrendiniz. Artık daha karmaşık sorgular oluşturabilir ve Gremlin kullanarak güçlü grafik geçişi mantığını kullanabilirsiniz. 

> [!div class="nextstepaction"]
> [Gremlin kullanarak sorgulama](tutorial-query-graph.md)

