---
title: "Visual Studio ve C# - Azure Hdınsight ile aaaApache Storm topolojileri | Microsoft Docs"
description: "Bilgi nasıl toocreate Storm topolojilerini C#. Basit word count topolojisi için Visual Studio hello Hadoop araçları kullanarak Visual Studio'da oluşturun."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 380d804f-a8c5-4b20-9762-593ec4da5a0d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/02/2017
ms.author: larryfr
ms.openlocfilehash: b3fb01a4dda144fd7fb4141e624e31e667f93753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-c-topologies-for-apache-storm-by-using-hello-data-lake-tools-for-visual-studio"></a>Visual Studio için hello Data Lake araçları kullanarak Apache Storm için C# topolojileri geliştirme

Nasıl toocreate hello Azure Data Lake (Hadoop) kullanarak C# Storm topolojisini için Visual Studio Araçları hakkında bilgi edinin. Bu belge Visual Studio'da bir Storm projesi oluşturma, yerel olarak test etme ve Azure Hdınsight kümesi üzerinde Apache Storm tooan dağıtma hello işleminde size yol göstermektedir.

Da bilgi nasıl C# ve Java bileşenlerini kullanan karma topolojiler toocreate.

> [!NOTE]
> Visual Studio ile Windows geliştirme ortamına Hello adımları bu belgede Bel hello derlenmiş proje gönderilen tooeither bir Linux veya Windows tabanlı Hdınsight kümesi olabilir. Yalnızca Linux tabanlı kümelerde 28 Ekim 2016'dan sonra oluşturulan SCP.NET topolojileri destekler.

toouse C# topolojisi Linux tabanlı bir küme ile Merhaba Microsoft.SCP.Net.SDK NuGet paketi, proje tooversion 0.10.0.6 tarafından kullanılan veya üzeri güncelleştirmeniz gerekir. Merhaba hello paketin sürümü yüklü Hdınsight üzerinde Storm hello ana sürümüne de eşleşmelidir.

| Hdınsight sürümü | Storm sürüm | SCP.NET sürüm | Varsayılan Mono sürümü |
|:-----------------:|:-------------:|:---------------:|:--------------------:|
| 3.3 |0.10.x |0.10.x.x</br>(yalnızca Windows tabanlı Hdınsight üzerinde) | NA |
| 3.4 | 0.10.0.x | 0.10.0.x | 3.2.8 |
| 3,5 | 1.0.2.x | 1.0.0.x | 4.2.1 |
| 3.6 | 1.1.0.x | 1.0.0.x | 4.2.8 |

> [!IMPORTANT]
> C# topolojileri Linux tabanlı kümelerde .NET 4.5 kullanın ve hello Hdınsight kümesinde Mono toorun kullanmanız gerekir. Denetleme [Mono Uyumluluk](http://www.mono-project.com/docs/about-mono/compatibility/) olası uyumsuzlukları için.

## <a name="install-visual-studio"></a>Visual Studio yükleme

Visual Studio sürümleri aşağıdaki hello birini kullanarak C# topolojileri SCP.NET ile geliştirme yapabilirsiniz:

* Visual Studio 2012 ile [güncelleştirme 4](http://www.microsoft.com/download/details.aspx?id=39305)

* Visual Studio 2013 [güncelleştirme 4](http://www.microsoft.com/download/details.aspx?id=44921) veya [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)

* Visual Studio 2015 veya [Visual Studio 2015 topluluk](https://go.microsoft.com/fwlink/?LinkId=532606)

* Visual Studio 2017 (herhangi bir sürümünü)

## <a name="install-data-lake-tools-for-visual-studio"></a>Visual Studio için yükleme Data Lake araçları

Visual Studio için Data Lake araçları tooinstall izleyin hello adımlarda [Visual Studio için Data Lake araçları kullanarak çalışmaya başlama](hdinsight-hadoop-visual-studio-tools-get-started.md).

## <a name="install-java"></a>Java'yı yükleme

Visual Studio'dan bir Storm topolojisinin gönderdiğinizde, SCP.NET hello topoloji ve bağımlılıklarını içeren bir zip dosyası oluşturur. Java kullanılan toocreate olduğundan daha Linux tabanlı kümelerde ile uyumlu bir biçimde kullandığından bu dosyaları zip.

1. Geliştirme ortamınızı Hello Java Geliştirme Seti (JDK) 7 veya sonraki bir sürümü yükleyin. Alabileceğiniz Oracle JDK gelen hello [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html). Aynı zamanda [diğer Java dağıtımları](http://openjdk.java.net/).

2. Merhaba `JAVA_HOME` Java içeren ortam değişkeni gereken noktası toohello dizini.

3. Merhaba `PATH` ortam değişkeni hello içermelidir `%JAVA_HOME%\bin` dizin.

Konsol uygulaması Java ve hello JDK düzgün yüklendiğini C# tooverify aşağıdaki hello kullanabilirsiniz:

```csharp
using System;
using System.IO;
namespace ConsoleApplication2
{
   class Program
   {
       static void Main(string[] args)
       {
           string javaHome = Environment.GetEnvironmentVariable(“JAVA_HOME”);
           if (!string.IsNullOrEmpty(javaHome))
           {
               string jarExe = Path.Combine(javaHome + @”\bin”, “jar.exe”);
               if (File.Exists(jarExe))
               {
                   Console.WriteLine(“JAVA Is Installed properly”);
                    return;
               }
               else
               {
                   Console.WriteLine(“A valid JAVA JDK is not found. Looks like JRE is installed instead of JDK.”);
               }
           }
           else
           {
             Console.WriteLine(“A valid JAVA JDK is not found. JAVA_HOME environment variable is not set.”);
           }
       }  
   }
}
```

## <a name="storm-templates"></a>Storm şablonları

Visual Studio için Data Lake araçları Hello şablonları aşağıdaki hello sağlar:

| Proje türü | Gösterir |
| --- | --- |
| Storm uygulaması |Boş bir Storm topolojisini projesi. |
| Storm Azure SQL yazıcı örnek |Nasıl toowrite tooAzure SQL veritabanı. |
| Storm Azure Cosmos DB okuyucu örneği |Nasıl tooread Azure Cosmos DB'den. |
| Storm Azure Cosmos DB yazan örnek |Nasıl toowrite tooAzure Cosmos DB. |
| Storm EventHub okuyucu örneği |Nasıl tooread Azure Event hubs'tan. |
| Storm EventHub yazan örnek |Nasıl toowrite tooAzure olay hub'ları. |
| Storm HBase okuyucu örneği |Hdınsight'ta HBase gelen tooread nasıl kümeleri. |
| Storm HBase yazan örnek |Nasıl toowrite tooHBase hdınsight kümeleri. |
| Storm karma örnek |Nasıl toouse bir Java bileşeni. |
| Storm örnek |Temel word count topolojisi. |

> [!WARNING]
> Tüm Şablonları Linux tabanlı Hdınsight ile çalışır. Merhaba şablonları tarafından kullanılan Nuget paketleri Mono ile uyumlu olmayabilir. Merhaba denetleyin [Mono Uyumluluk](http://www.mono-project.com/docs/about-mono/compatibility/) belge ve hello kullan [.NET taşınabilirlik Çözümleyicisi](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) tooidentify olası sorunları.

Bu belgedeki Hello adımlarda hello temel Storm uygulaması proje türü toocreate bir topoloji kullanın.

### <a name="hbase-templates-notes"></a>HBase şablonları notları

Merhaba HBase okuyucu ve yazıcı şablonları hello HBase REST API değil hello HBase Java API, Hdınsight kümesinde bir HBase ile toocommunicate kullanın.

### <a name="eventhub-templates-notes"></a>EventHub şablonları notları

> [!IMPORTANT]
> Merhaba Java tabanlı EventHub spout EventHub okuyucu şablon sürüm 3.5 veya sonrasını hdınsight'ta Storm çalışmayabilir hello ile birlikte gelen bileşeni. Bu bileşen güncelleştirilmiş bir sürümü kullanılabilir [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).

Bu kullanan örnek bir topoloji için bkz: bileşen ve Hdınsight 3.5 üzerinde Storm ile works [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).

## <a name="create-a-c-topology"></a>Bir C# topolojisi oluşturma

1. Visual Studio'ni açın, **dosya** > **yeni**ve ardından **proje**.

2. Merhaba gelen **yeni proje** penceresinde genişletin **yüklü** > **şablonları**seçip **Azure Data Lake**. Merhaba şablonları listesinden **Storm uygulaması**. Merhaba ekranında Hello altındaki girin **WordCount** Merhaba uygulaması hello adından farklı.

    ![Yeni Proje penceresinin ekran penceresi](./media/hdinsight-storm-develop-csharp-visual-studio-topology/new-project.png)

3. Başlangıç projesi oluşturduktan sonra aşağıdaki dosyaları hello olmalıdır:

   * **Program.cs**: hello topoloji projeniz için bu dosyayı tanımlar. Bir spout ve bir Cıvata oluşan bir varsayılan topolojisi varsayılan olarak oluşturulur.

   * **Spout.cs**: rastgele sayılar yayar bir örnek spout.

   * **Bolt.cs**: hello spout'un gösterilen sayıların sayısı tutan bir örnek Cıvata.

     Başlangıç projesi oluşturduğunuzda, NuGet yüklemeleri son hello [SCP.NET paket](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).

     [!INCLUDE [scp.net version important](../../includes/hdinsight-storm-scpdotnet-version.md)]

### <a name="implement-hello-spout"></a>Uygulama hello spout

1. Açık **Spout.cs**. Spout'lar, bir dış kaynaktan topolojisinde kullanılan tooread verilerdir. bir spout için Hello ana bileşeni vardır:

   * **NextTuple**: Merhaba spout tooemit yeni diziler izin verildiğinde Storm tarafından çağrılır.

   * **ACK** (yalnızca işlem topolojisi): hello spout gönderilen diziler için başlangıç topolojisinde başka bileşenler tarafından başlatılan onayları işler. Bir tanımlama grubu aktarımının aşağı akış bileşenleri tarafından başarıyla işlendi bilmeniz hello spout olanak sağlar.

   * **Başarısız** (yalnızca işlem topolojisi): işleme, başarısız hello topoloji içindeki diğer bileşenlere işleme tanımlama grubu. Başarısız yöntemi uygulama verir toore-yeniden işlenebilir böylece hello tanımlama grubu yayma.

2. Merhaba Hello içeriğini değiştirin **Spout** metin aşağıdaki hello sınıfıyla. Bu spout bir cümle rastgele hello topoloji yayar.

    ```csharp
    private Context ctx;
    private Random r = new Random();
    string[] sentences = new string[] {
        "hello cow jumped over hello moon",
        "an apple a day keeps hello doctor away",
        "four score and seven years ago",
        "snow white and hello seven dwarfs",
        "i am at two with nature"
    };

    public Spout(Context ctx)
    {
        // Set hello instance context
        this.ctx = ctx;

        Context.Logger.Info("Generator constructor called");

        // Declare Output schema
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // hello schema for hello default output stream is
        // a tuple that contains a string field
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(null, outputSchema));
    }

    // Get an instance of hello spout
    public static Spout Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Spout(ctx);
    }

    public void NextTuple(Dictionary<string, Object> parms)
    {
        Context.Logger.Info("NextTuple enter");
        // hello sentence toobe emitted
        string sentence;

        // Get a random sentence
        sentence = sentences[r.Next(0, sentences.Length - 1)];
        Context.Logger.Info("Emit: {0}", sentence);
        // Emit it
        this.ctx.Emit(new Values(sentence));

        Context.Logger.Info("NextTuple exit");
    }

    public void Ack(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }
    ```

### <a name="implement-hello-bolts"></a>Merhaba Cıvatalar uygulama

1. Merhaba varolan silme **Bolt.cs** hello proje dosyasından.

2. İçinde **Çözüm Gezgini**hello projesine sağ tıklayın ve seçin **Ekle** > **yeni öğe**. Merhaba listesinden **Storm Cıvata**ve girin **Splitter.cs** hello adı. İkinci Cıvata adlı bu işlem toocreate yineleyin **Counter.cs**.

   * **Splitter.cs**: cümleleri tek tek sözcüklere böler ve yeni akış sözcüklerin yayar Cıvata uygular.

   * **Counter.cs**: her sözcüğün sayar ve sözcükleri ve hello sayısı her sözcüğün için yeni bir akış yayar Cıvata uygular.

     > [!NOTE]
     > Bu Cıvatalar toostreams okuyup, ancak bir veritabanı veya hizmet gibi kaynakları ile Cıvata toocommunicate de kullanabilirsiniz.

3. Açık **Splitter.cs**. Varsayılan olarak yalnızca bir yöntemi vardır: **yürütme**. Merhaba Cıvata işlemek için bir tanımlama grubu aldığında hello yürütme yöntemi adı verilir. Burada, okuma ve gelen diziler işlemek ve giden tanımlama grubu yayma.

4. Merhaba Hello içeriğini değiştirin **Bölümlendirici** koddan hello sınıfıyla:

    ```csharp
    private Context ctx;

    // Constructor
    public Splitter(Context ctx)
    {
        Context.Logger.Info("Splitter constructor called");
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // Input contains a tuple with a string field (hello sentence)
        inputSchema.Add("default", new List<Type>() { typeof(string) });
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // Outbound contains a tuple with a string field (hello word)
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance of hello bolt
    public static Splitter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Splitter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello sentence from hello tuple
        string sentence = tuple.GetString(0);
        // Split at space characters
        foreach (string word in sentence.Split(' '))
        {
            Context.Logger.Info("Emit: {0}", word);
            //Emit each word
            this.ctx.Emit(new Values(word));
        }

        Context.Logger.Info("Execute exit");
    }
    ```

5. Açık **Counter.cs**ve hello sınıfı içeriği hello şununla değiştirin:

    ```csharp
    private Context ctx;

    // Dictionary for holding words and counts
    private Dictionary<string, int> counts = new Dictionary<string, int>();

    // Constructor
    public Counter(Context ctx)
    {
        Context.Logger.Info("Counter constructor called");
        // Set instance context
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string field - hello word
        inputSchema.Add("default", new List<Type>() { typeof(string) });

        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string and integer field - hello word and hello word count
        outputSchema.Add("default", new List<Type>() { typeof(string), typeof(int) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance
    public static Counter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Counter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello word from hello tuple
        string word = tuple.GetString(0);
        // Do we already have an entry for hello word in hello dictionary?
        // If no, create one with a count of 0
        int count = counts.ContainsKey(word) ? counts[word] : 0;
        // Increment hello count
        count++;
        // Update hello count in hello dictionary
        counts[word] = count;

        Context.Logger.Info("Emit: {0}, count: {1}", word, count);
        // Emit hello word and count information
        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new List<SCPTuple> { tuple }, new Values(word, count));
        Context.Logger.Info("Execute exit");
    }
    ```

### <a name="define-hello-topology"></a>Merhaba topolojisi tanımlayın

Spout'lar ve Cıvatalar bileşenler arasında hello veri akışını tanımlayan bir grafik halinde düzenlenir. Bu topoloji, hello grafiği aşağıdaki gibidir:

![Bileşenleri nasıl düzenlenir diyagramı](./media/hdinsight-storm-develop-csharp-visual-studio-topology/wordcount-topology.png)

Cümleleri hello spout yayılan ve hello Bölümlendirici Cıvata, dağıtılmış tooinstances demektir. Merhaba Bölümlendirici Cıvata hello cümleleri dağıtılmış toohello sayaç Cıvata olan sözcüklere keser.

Sözcük sayısını yerel olarak hello sayaç örneğinde tutulmadığından toomake belirli kelimeleri toohello akış emin istiyoruz aynı sayacı Cıvata örneği. Her bir örnek, belirli kelimeleri izler. Merhaba Bölümlendirici Cıvata hiçbir durumunu koruyan olduğundan, gerçekten hello Bölümlendirici hangi örneğinin hangi tümceyi alır önemli değildir.

Açık **Program.cs**. Merhaba önemli yöntemi **GetTopologyBuilder**, hangi olduğu kullanılan toodefine hello topoloji tooStorm gönderildi. Merhaba Değiştir **GetTopologyBuilder** kod tooimplement hello topoloji daha önce açıklanan aşağıdaki hello ile:

```csharp
// Create a new topology named 'WordCount'
TopologyBuilder topologyBuilder = new TopologyBuilder("WordCount" + DateTime.Now.ToString("yyyyMMddHHmmss"));

// Add hello spout toohello topology.
// Name hello component 'sentences'
// Name hello field that is emitted as 'sentence'
topologyBuilder.SetSpout(
    "sentences",
    Spout.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"sentence"}}
    },
    1);
// Add hello splitter bolt toohello topology.
// Name hello component 'splitter'
// Name hello field that is emitted 'word'
// Use suffleGrouping toodistribute incoming tuples
//   from hello 'sentences' spout across instances
//   of hello splitter
topologyBuilder.SetBolt(
    "splitter",
    Splitter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word"}}
    },
    1).shuffleGrouping("sentences");

// Add hello counter bolt toohello topology.
// Name hello component 'counter'
// Name hello fields that are emitted 'word' and 'count'
// Use fieldsGrouping tooensure that tuples are routed
//   toocounter instances based on hello contents of field
//   position 0 (hello word). This could also have been
//   List<string>(){"word"}.
//   This ensures that hello word 'jumped', for example, will always
//   go toohello same instance
topologyBuilder.SetBolt(
    "counter",
    Counter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word", "count"}}
    },
    1).fieldsGrouping("splitter", new List<int>() { 0 });

// Add topology config
topologyBuilder.SetTopologyConfig(new Dictionary<string, string>()
{
    {"topology.kryo.register","[\"[B\"]"}
});

return topologyBuilder;
```

## <a name="submit-hello-topology"></a>Merhaba topoloji gönderme

1. İçinde **Çözüm Gezgini**hello projesine sağ tıklayın ve seçin **hdınsight'ta tooStorm gönderme**.

   > [!NOTE]
   > İstenirse, Azure aboneliğinizin hello kimlik bilgilerini girin. Birden fazla aboneliğiniz varsa, toohello Hdınsight kümesi üzerinde Storm'a içeren bir oturum açma.

2. Hdınsight kümesi üzerinde Storm'a hello seçin **Storm kümesi** aşağı açılan listeyi ve ardından **gönderme**. Merhaba gönderimi hello kullanarak başarılı olursa, izleyebilirsiniz **çıkış** penceresi.

3. Merhaba topoloji başarıyla gönderildi, hello **Storm topolojilerini** hello küme görünür. Select hello **WordCount** topoloji topoloji çalıştıran hello hakkında hello listesi tooview bilgi.

   > [!NOTE]
   > Ayrıca görüntüleyebilirsiniz **Storm topolojilerini** gelen **Sunucu Gezgini**. Genişletme **Azure** > **Hdınsight**, Hdınsight kümesinde bir Storm sağ tıklayın ve ardından **görünüm Storm topolojilerini**.

    Merhaba topolojisinde hello bileşenler hakkında bilgi tooview hello diyagramı hello bileşeninde çift tıklayın.

4. Merhaba gelen **topoloji özeti** görüntülemek için tıklatın **KILL** toostop hello topolojisi.

   > [!NOTE]
   > Storm topolojilerini toorun devre dışı bırakılır veya hello küme silinene kadar devam eder.

## <a name="transactional-topology"></a>İşlem topolojisi

Merhaba önceki işlem olmayan topolojidir. Merhaba bileşenleri hello topolojisinde işlevselliği tooreplaying iletileri kullanılmaz. Bir işlem topolojisi ilişkin bir örnek, bir proje oluşturmak ve **Storm örnek** hello proje türü olarak.

İşlem topolojileri toosupport yeniden yürütme veri aşağıdaki hello uygulayın:

* **Meta verileri önbelleğe alma**: Merhaba spout yayılan hello verileri alınır ve bir hata oluşursa yeniden yayılan böylece hello veriler hakkındaki meta verileri depolamak gerekir. Merhaba örnek tarafından yayılan hello veriler küçük olduğundan hello ham verileri her tanımlama grubu için bir sözlük yeniden yürütme için depolanır.

* **ACK**: hello topolojisinde her Cıvata çağırabilirsiniz `this.ctx.Ack(tuple)` bir tanımlama grubu başarıyla işlediği tooacknowledge. Tüm Cıvatalar acked hello tanımlama grubu varsa, hello `Ack` hello spout yöntemi çağrılır. Merhaba `Ack` yöntemi yeniden yürütme için önbelleğe hello spout tooremove veri sağlar.

* **Başarısız**: her Cıvata çağırabilirsiniz `this.ctx.Fail(tuple)` tooindicate bu işlem için bir tanımlama grubu yapamadı. Merhaba hatası yayar toohello `Fail` burada hello tanımlama grubu yeniden kullanarak hello spout yöntemi önbelleğe alınan meta verileri.

* **Sıra kimliği**: bir tanımlama grubu yayma, benzersiz sıra kimliği belirtilebilir. Bu değer hello tanımlama grubu yeniden yürütme (Ack ve başarısız) işleme tanımlar. Örneğin, hello spout hello **Storm örnek** project veri yayma zaman hello şunları kullanır:

        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), lastSeqId);

    Bu kod içinde yer alan hello sırası kimliği değeri olan bir cümle toohello varsayılan akış içeren bir tanımlama grubu yayar **lastSeqId**. Bu örnek için **lastSeqId** gösterilen her bir tanımlama grubu için artırılır.

Hello gösterildiği gibi **Storm örnek** proje, bir bileşenin işlem olup yapılandırmasını temel alarak zamanında ayarlanmış olabilir.

## <a name="hybrid-topology-with-c-and-java"></a>C# ve Java ile karma topolojisi

Burada bazı bileşenleri C# ve diğerleri Java Visual Studio toocreate karma topolojiler için Data Lake Araçları'nı da kullanabilirsiniz.

Bir karma topolojisi ilişkin bir örnek, bir proje oluşturmak ve **Storm karma örnek**. Bu örnek türü kavramları aşağıdaki hello gösterir:

* **Java spout** ve **C# Cıvata**: tanımlıysa **HybridTopology_javaSpout_csharpBolt**.

    * İşlem sürüm tanımlanan **HybridTopologyTx_javaSpout_csharpBolt**.

* **C# spout** ve **Java Cıvata**: tanımlıysa **HybridTopology_csharpSpout_javaBolt**.

    * İşlem sürüm tanımlanan **HybridTopologyTx_csharpSpout_javaBolt**.

  > [!NOTE]
  > Bu sürüm ayrıca nasıl toouse Clojure kod bir Java bileşeni olarak bir metin dosyasından gösterir.


Merhaba proje gönderildiğinde, kullanılan tooswitch hello topoloji yalnızca hello taşıma `[Active(true)]` toohello küme göndermeden önce toouse, istediğiniz deyimi toohello topolojisi.

> [!NOTE]
> Gerekli tüm hello Java dosyaları hello bu projede bir parçası olarak sağlanan **JavaDependency** klasör.

Oluştururken ve karma topolojisi gönderme hello aşağıdakileri göz önünde bulundurun:

* Kullanmalısınız **JavaComponentConstructor** toocreate hello spout veya Cıvata için Java sınıfı örneği.

* Kullanmanız gereken **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** tooserialize veri içine veya Java bileşenleri Java'dan dışında tooJSON nesneleri.

* Merhaba topoloji toohello sunucu gönderirken hello kullanmalısınız **ek yapılandırmalar** seçeneği toospecify hello **Java dosya yolları**. Belirtilen hello yolu Java sınıfları içeren hello JAR dosyalarını içeren hello dizin olmalıdır.

### <a name="azure-event-hubs"></a>Azure Event Hubs

SCP.NET sürüm 0.9.4.203 bir yeni sınıf ve hello olay hub'ı spout (olay hub'larından okuyan bir Java spout) ile çalışmak için özellikle yöntemi sunar. Bir olay hub'ı spout kullanan bir topolojisi oluşturduğunuzda, hello aşağıdaki yöntemleri kullanın:

* **EventHubSpoutConfig** sınıfı: Merhaba spout bileşeni için hello yapılandırma içeren bir nesne oluşturur.

* **TopologyBuilder.SetEventHubSpout** yöntemi: hello olay hub'ı spout bileşen toohello topoloji ekler.

> [!NOTE]
> Merhaba hala kullanmalısınız **CustomizedInteropJSONSerializer** üretilen hello spout'un tooserialize veriler.

## <a id="configurationmanager"></a>ConfigurationManager kullanın

Kullanmayan **ConfigurationManager** tooretrieve yapılandırma değerleri Cıvata ve bileşenleri spout. Bunun yapılması bir null işaretçi özel durumu neden olabilir. Bunun yerine, hello yapılandırma projeniz için bir anahtar ve değer çifti hello topoloji bağlamda olarak hello Storm topolojisini geçirilir. Yapılandırma değerlerini kullanır her bileşenin bunları başlatma sırasında hello bağlamından almanız gerekir.

Merhaba aşağıdaki kodu gösterir nasıl tooretrieve bu değerler:

```csharp
public class MyComponent : ISCPBolt
{
    // toohold configuration information loaded from context
    Configuration configuration;
    ...
    public MyComponent(Context ctx, Dictionary<string, Object> parms)
    {
        // Save a copy of hello context for this component instance
        this.ctx = ctx;
        // If it exists, load hello configuration for hello component
        if(parms.ContainsKey(Constants.USER_CONFIG))
        {
            this.configuration = parms[Constants.USER_CONFIG] as System.Configuration.Configuration;
        }
        // Retrieve hello value of "Foo" from configuration
        var foo = this.configuration.AppSettings.Settings["Foo"].Value;
    }
    ...
}
```

Kullanırsanız, bir `Get` yöntemi tooreturn bileşeniniz ait bir örnek sağlamanız hem hello geçirir `Context` ve `Dictionary<string, Object>` parametreleri toohello Oluşturucusu. Merhaba aşağıdaki temel bir örnektir `Get` düzgün bu değerleri geçirir yöntemi:

```csharp
public static MyComponent Get(Context ctx, Dictionary<string, Object> parms)
{
    return new MyComponent(ctx, parms);
}
```

## <a name="how-tooupdate-scpnet"></a>Nasıl tooupdate SCP.NET

Paket yükseltmesi NuGet aracılığıyla SCP.NET en son sürümleri destekler. Yeni bir güncelleştirme kullanılabilir olduğunda, bir yükseltme bildirimi alırsınız. toomanually denetleyin, yükseltme için şu adımları izleyin:

1. İçinde **Çözüm Gezgini**hello projesine sağ tıklayın ve seçin **NuGet paketlerini Yönet**.

2. Merhaba Paket Yöneticisi'nden seçin **güncelleştirmeleri**. Bir güncelleştirme olup olmadığını listelenir. Tıklatın **güncelleştirme** hello paket tooinstall için bunu.

> [!IMPORTANT]
> Projenizin NuGet kullanmadı SCP.NET önceki bir sürümüyle oluşturulduysa, aşağıdaki adımları tooupdate tooa daha yeni sürüm hello gerçekleştirmeniz gerekir:
>
> 1. İçinde **Çözüm Gezgini**hello projesine sağ tıklayın ve seçin **NuGet paketlerini Yönet**.
> 2. Hello kullanarak **arama** alanına arayın ve ardından ekleyin, **Microsoft.SCP.Net.SDK** toohello projesi.

## <a name="troubleshoot-common-issues-with-topologies"></a>Topolojileri ile ilgili genel sorunları giderme

### <a name="null-pointer-exceptions"></a>Null işaretçi özel durumlar

Bir C# topolojisi ile Linux tabanlı Hdınsight kümesi kullanırken, Cıvata ve kullanan bileşenleri spout **ConfigurationManager** tooread yapılandırma ayarlarını çalışma zamanında null işaretçi özel durumlar döndürebilir.

projeniz için Hello yapılandırma hello Storm topolojisini hello topoloji bağlamında bir anahtar ve değer çifti olarak geçirilir. Bunlar hazırlarken, tooyour bileşenleri geçirilen hello dictionary nesnesinden alınabilir.

Daha fazla bilgi için bkz: Merhaba [ConfigurationManager](#configurationmanager) bu belgenin bölüm.

### <a name="systemtypeloadexception"></a>System.TypeLoadException

Bir C# topolojisi ile Linux tabanlı Hdınsight kümesi kullanırken, aşağıdaki hata hello karşılaşabilirsiniz:

    System.TypeLoadException: Failure has occurred while loading a type.

Mono destekleyen .NET hello sürümü ile uyumlu olmayan bir ikili kullandığınızda bu hata oluşur.

Linux tabanlı Hdınsight kümeleri için projeniz .NET 4. 5'için derlenmiş ikili dosyaları kullandığından emin olun.

### <a name="test-a-topology-locally"></a>Bir topoloji yerel olarak test etme

Kolay toodeploy bazı durumlarda, bir topoloji tooa küme olmasına rağmen tootest yerel olarak bir topoloji gerekebilir. Bu öğreticide yerel geliştirme ortamınızı hello örnek topoloji test ve adımları toorun aşağıdaki hello kullanın.

> [!WARNING]
> Yerel test yalnızca çalışır için basic, C#-yalnızca topolojileri. Karma topolojiler veya birden çok akış kullanmak Topolojileri için yerel test kullanamazsınız.

1. İçinde **Çözüm Gezgini**hello projesine sağ tıklayın ve seçin **özellikleri**. Merhaba Proje Özellikleri'nde hello değiştirme **çıktı türü** çok**konsol uygulaması**.

    ![Vurgulanan çıktı türü ile Proje Özellikleri'nin ekran görüntüsü](./media/hdinsight-storm-develop-csharp-visual-studio-topology/outputtype.png)

   > [!NOTE]
   > Toochange hello unutmayın **çıktı türü** çok geri**sınıf kitaplığı** hello topoloji tooa küme dağıtmadan önce.

2. İçinde **Çözüm Gezgini**hello projesine sağ tıklayın ve ardından **Ekle** > **yeni öğe**. Seçin **sınıfı**ve girin **LocalTest.cs** hello sınıfı adı. Son olarak, tıklatın **Ekle**.

3. Açık **LocalTest.cs**ve hello aşağıdakileri ekleyin **kullanarak** hello üstünde deyimi:

    ```csharp
    using Microsoft.SCP;
    ```

4. Kullanım hello aşağıdaki kod hello Merhaba içeriğine **LocalTest** sınıfı:

    ```csharp
    // Drives hello topology components
    public void RunTestCase()
    {
        // An empty dictionary for use when creating components
        Dictionary<string, Object> emptyDictionary = new Dictionary<string, object>();

        #region Test hello spout
        {
            Console.WriteLine("Starting spout");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext spoutCtx = LocalContext.Get();
            // Get a new instance of hello spout, using hello local context
            Spout sentences = Spout.Get(spoutCtx, emptyDictionary);

            // Emit 10 tuples
            for (int i = 0; i < 10; i++)
            {
                sentences.NextTuple(emptyDictionary);
            }
            // Use LocalContext toopersist hello data stream toofile
            spoutCtx.WriteMsgQueueToFile("sentences.txt");
            Console.WriteLine("Spout finished");
        }
        #endregion

        #region Test hello splitter bolt
        {
            Console.WriteLine("Starting splitter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext splitterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Splitter splitter = Splitter.Get(splitterCtx, emptyDictionary);

            // Set hello data stream toohello data created by hello spout
            splitterCtx.ReadFromFileToMsgQueue("sentences.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = splitterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                splitter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            splitterCtx.WriteMsgQueueToFile("splitter.txt");
            Console.WriteLine("Splitter bolt finished");
        }
        #endregion

        #region Test hello counter bolt
        {
            Console.WriteLine("Starting counter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext counterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Counter counter = Counter.Get(counterCtx, emptyDictionary);

            // Set hello data stream toohello data created by splitter bolt
            counterCtx.ReadFromFileToMsgQueue("splitter.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = counterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                counter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            counterCtx.WriteMsgQueueToFile("counter.txt");
            Console.WriteLine("Counter bolt finished");
        }
        #endregion
    }
    ```

    Şu anda tooread hello kod açıklamaları aracılığıyla alın. Bu kodu kullanır **LocalContext** toorun hello bileşenlerinde hello geliştirme ortamını ve hello veri akışı bileşenleri tootext dosyaları hello yerel sürücüde arasında devam ettirir.

1. Açık **Program.cs**ve toohello aşağıdaki hello ekleyin **ana** yöntemi:

    ```csharp
    Console.WriteLine("Starting tests");
    System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "WordCount-LocalTest");
    // Initialize hello runtime
    SCPRuntime.Initialize();

    //If we are not running under hello local context, throw an error
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)
    {
        throw new Exception(string.Format("unexpected pluginType: {0}", Context.pluginType));
    }
    // Create test instance
    LocalTest tests = new LocalTest();
    // Run tests
    tests.RunTestCase();
    Console.WriteLine("Tests finished");
    Console.ReadKey();
    ```

2. Merhaba değişiklikleri kaydedin ve ardından **F5** veya seçin **hata ayıklama** > **hata ayıklamayı Başlat** toostart hello projesi. Bir konsol penceresi görünür ve günlük hello testleri ilerleme durumunun gerekir. Zaman **testleri tamamlandı** görüntülenirse, herhangi bir anahtar tooclose hello penceresi tuşuna basın.

3. Kullanım **Windows Explorer** projenizi içeren toolocate başlangıç dizini. Örneğin: **C:\Users\<your_user_name > \Documents\Visual Studio 2013\Projects\WordCount\WordCount**. Bu dizinde açmak **Bin**ve ardından **hata ayıklama**. Merhaba testlerini çalıştırdığınızda oluşturulamadığı hello metin dosyaları görmeniz gerekir: sentences.txt, counter.txt ve splitter.txt. Her metin dosyasını açın ve hello veri inceleyin.

   > [!NOTE]
   > Dize verilerini bu dosyalardaki ondalık değerleri dizisi olarak devam ettirir. Örneğin, \[[97,103,111]] hello içinde **splitter.txt** dosyasıdır hello word *ve*.

> [!NOTE]
> Emin tooset hello olması **proje türü** çok geri**sınıf kitaplığı** Hdınsight kümesinde Storm tooa dağıtmadan önce.

### <a name="log-information"></a>Günlük bilgileri

Kolayca bilgi topoloji bileşenlerinizi kullanarak oturum `Context.Logger`. Örneğin, hello aşağıdaki bilgilendirici günlük girişi oluşturur:

```csharp
Context.Logger.Info("Component started");
```

Günlüğe kaydedilen bilgileri hello görüntülenebilir **Hadoop hizmeti günlüğünü**, içinde bulunan **Sunucu Gezgini**. Hdınsight kümesi üzerinde Storm'a için Hello girişi genişletin ve ardından **Hadoop hizmeti günlüğünü**. Son olarak, hello günlük dosyası tooview seçin.

> [!NOTE]
> Merhaba günlükleri Merhaba, küme tarafından kullanılan Azure depolama hesabı depolanır. Visual Studio'da tooview hello günlükleri, toohello hello depolama hesabı sahibi Azure aboneliği oturum açmanız gerekir.

### <a name="view-error-information"></a>Hata bilgilerini görüntüleme

çalışan bir topoloji oluşmuş tooview hataları hello aşağıdaki adımları kullanın:

1. Gelen **Sunucu Gezgini**, Hdınsight kümesinde Storm hello sağ tıklatın ve seçin **görünüm Storm topolojilerini**.

2. Hello için **Spout** ve **Cıvatalar**, hello **son hata** sütun hello son hata hakkında bilgi içerir.

3. Select hello **Spout kimliği** veya **Cıvata kimliği** listelenen hatalı hello bileşeni için. Görüntülenen, ek hata hello Ayrıntıları sayfasında hello listelenen bilgileri **hataları** hello sayfanın hello kısmına.

4. tooobtain daha fazla bilgi, select bir **bağlantı noktası** hello gelen **yürütücüler** hello sayfasının bölümünde, toosee hello Storm çalışan günlük hello son birkaç dakika için.

### <a name="errors-submitting-topologies"></a>Topolojileri gönderme hataları

Topoloji tooHDInsight gönderilirken hatalarla karşılaşırsanız, Hdınsight kümenize topoloji gönderimini işlemek hello sunucu tarafı bileşenleri için günlükleri bulabilirsiniz. Bu günlükleri, komutu bir komut satırından aşağıdaki kullanım hello tooretrieve:

    scp sshuser@clustername-ssh.azurehdinsight.net:/var/log/hdinsight-scpwebapi/hdinsight-scpwebapi.out .

Değiştir __sshuser__ hello hello küme için SSH kullanıcı hesabı ile. Değiştir __clustername__ hello Hdınsight kümesi hello adı. Kullanma hakkında daha fazla bilgi için `scp` ve `ssh` Hdınsight ile bkz [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

Gönderimleri birden çok nedenlerden dolayı başarısız olabilir:

* JDK yüklü değil veya hello yolunda değil.
* Gerekli Java bağımlılıkları hello gönderisine dahil edilmez.
* Uyumsuz bağımlılıkları.
* Yinelenen topoloji adları.

Merhaba, `hdinsight-scpwebapi.out` günlük içeren bir `FileNotFoundException`, bu koşullar aşağıdaki hello tarafından kaynaklanabilir:

* Merhaba JDK hello geliştirme ortamı hello yolu değil. JDK yüklü hello geliştirme ortamını ve, o hello doğrulayın `%JAVA_HOME%/bin` hello yoludur.
* Java bağımlılığı eksik. Tüm gerekli .jar dosyalar hello gönderimi bir parçası olarak dahil emin olun.

## <a name="next-steps"></a>Sonraki adımlar

Bir örnek veriler işlenirken için Event hubs, bkz: [işlem Hdınsight üzerinde Storm ile Azure Event Hubs olaylarından](hdinsight-storm-develop-csharp-event-hub-topology.md).

Veri akışı birden çok akışlara böler bir C# topolojisi örneği için bkz: [C# Storm örnek](https://github.com/Blackmist/csharp-storm-example).

C# topolojileri, oluşturma hakkında daha fazla bilgi toodiscover bkz [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).

Hdınsight ile daha fazla yol toowork ve Hdınsight örnekleri üzerinde daha fazla Storm için belgeler aşağıdaki hello bakın:

**Microsoft SCP.NET**

* [SCP Programlama Kılavuzu](hdinsight-storm-scp-programming-guide.md)

**Hdınsight üzerinde Apache Storm**

* [Dağıtma ve hdınsight'ta Apache Storm topolojileri izleme](hdinsight-storm-deploy-monitor-topology.md)
* [HDInsight üzerinde Storm için örnek topolojiler](hdinsight-storm-example-topology.md)

**Hdınsight'ta Apache Hadoop**

* [Hdınsight'ta Hadoop ile Hive kullanma](hdinsight-use-hive.md)
* [Hdınsight'ta Hadoop ile pig kullanma](hdinsight-use-pig.md)
* [Hdınsight'ta Hadoop ile MapReduce kullanma](hdinsight-use-mapreduce.md)

**Hdınsight üzerinde Apache HBase**

* [Hdınsight'ta HBase ile çalışmaya başlama](hdinsight-hbase-tutorial-get-started.md)
