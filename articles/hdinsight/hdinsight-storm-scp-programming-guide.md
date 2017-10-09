---
title: "aaaSCP.NET Programlama Kılavuzu | Microsoft Docs"
description: "Bilgi nasıl toouse SCP.NET toocreate. Hdınsight üzerinde Storm ile NET tabanlı Storm Topolojileri için kullanın."
services: hdinsight
documentationcenter: 
author: raviperi
manager: jhubbard
editor: cgronlun
ms.assetid: 34192ed0-b1d1-4cf7-a3d4-5466301cf307
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/16/2016
ms.author: raviperi
ms.openlocfilehash: a57f4217b07e0e82a3f36650308695fbb45d9128
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="scp-programming-guide"></a>SCP Programlama Kılavuzu
SCP platform toobuild gerçek zamanlı, güvenilir, tutarlı ve yüksek performans veri işleme uygulama olur. Üstünde oluşturulmuş [Apache Storm](http://storm.incubator.apache.org/) --bir akış hello OSS topluluğu tarafından tasarlanmış sistemi işleme. Storm Nathan Marz ve açık kaynaklıdır Twitter tarafından tasarlanmıştır. Bunu yararlanır [Apache ZooKeeper](http://zookeeper.apache.org/), başka bir Apache proje tooenable yüksek oranda güvenilir dağıtılmış koordinasyonu ve durum yönetimi. 

Yalnızca Windows üzerinde Storm hello SCP proje bağlantı noktası kurulmuş ancak hello proje uzantıları ve özelleştirme hello Windows ekosistemi için de eklenir. Merhaba uzantıları .NET geliştirme deneyimi ve kitaplıklarını içerir, Windows tabanlı bir dağıtım hello özelleştirme içerir. 

Merhaba genişletme ve özelleştirme toofork hello OSS projeleri gerekmez ve Storm üstünde oluşturulmuş türetilmiş ekosistemlerini yararlanan bir şekilde yapılır.

## <a name="processing-model"></a>İşlem modeli
SCP Hello verilerde diziler sürekli akışları olarak modellenir. Genellikle hello diziler bazı sıraya ilk akış sonra toplanmış ve içindeki bir Storm topolojisinin barındırılan iş mantığı tarafından dönüştürülen, son olarak hello çıktı diziler tooanother SCP sistem olarak yöneltilen veya kaydedilmiş toostores olması ister dağıtılmış dosya sistemi veya SQL Server veritabanları gibi çalışır.

![Bir veri deposu akışları veri tooprocessing besleme bir sıra diyagramı](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

Storm bir uygulama topolojisi hesaplama grafiği tanımlar. Veri akışı düğümler arasındaki bağlantıları gösterir ve her düğüm topolojisinde işleme mantığı içerir. Merhaba düğümleri tooinject giriş verilerini hello topoloji kullanılan toosequence hello veriler olabilir Spout'lar denir. Merhaba giriş verilerinin bulunduğu dosya günlükleri, işlemsel veritabanı, sistem performans sayacı gerçek verileri filtreleme hello Cıvatalar ve seçimleri ve toplama hem girdi ve çıktı veri akışları ile vb. hello düğüm olarak adlandırılır.

SCP en iyi çaba, en az bir kere destekler ve tam olarak-kez veri işleme. Bir dağıtılmış akış işleme uygulamasında, Ağ kaybı, makine hatasını ya da kullanıcı kodu hatası vb. gibi veri işleme sırasında çeşitli hatalar oluşabilir. En az bir kere işleme sağlar tüm veriler işlenir hata oluştuğunda en az bir kez otomatik olarak yeniden oynatmak tarafından aynı veri hello. En az bir kere işleme basit ve güvenilir olduğunu ve iyi birçok uygulamada uygun. Merhaba uygulaması tam sayım gerektirdiğinde hello aynı veri olası hello uygulama topolojisinde yürütülebilir beri ancak, örneğin, en az bir kere işleme yeterli değil. Bu durumda, tam olarak-işleme tasarlanmış sonra bile hello veri yeniden ve birden çok kez işlenen toomake emin hello sonuç doğru olur.

Dengeleme hello Java sanal makine (JVM) Storm hello kapak altında tabanlı SCP .NET geliştiricilerinin toodevelop gerçek zamanlı veri işlem uygulamalarını sağlar. Merhaba .NET ve JVM TCP yerel yuva iletişim kurar. Neredeyse her Spout/Cıvata bir .net/Java işlemi, hello kullanıcı mantığını .net işlem bir eklenti olarak çalıştığı çiftidir.

toobuild işleme uygulaması SCP en üstünde bir veri birkaç adım gereklidir:

* Tasarlayıp hello Spout'lar toopull veri sırasından.
* Tasarım ve Cıvatalar tooprocess hello giriş verisi uygulamak ve veri tooexternal depoları veritabanı gibi kaydedin.
* Merhaba topolojisi tasarım, gönderme ve hello topoloji çalıştırın. Merhaba topoloji köşeleri ve hello verileri tanımlayan akışları hello köşeleri arasında. SCP hello topoloji belirtimi alın ve her köşe mantıksal bir düğüm üzerinde çalıştığı bir Storm kümede dağıtın. Merhaba yük devretme ve ölçeklendirme hello Storm Görev Zamanlayıcı'yı dikkate.

Bu belgede bazı basit örnekler toowalk nasıl kullanacağınız toobuild veri işleme uygulama SCP ile.

## <a name="scp-plugin-interface"></a>SCP eklentisi arabirimi
SCP eklentileri (veya uygulamalar) hem de Visual Studio içinde hello geliştirme aşamasında çalışabilen ve üretim dağıtım sonrasında hello Storm ardışık düzenine takılı tek başına exe markalarıdır. Merhaba SCP eklenti yazma olduğundan yalnızca hello diğer standart Windows konsol uygulamaları yazma aynıdır. Spout/Cıvata için bazı arabirimi SCP.NET platform bildirir ve hello kullanıcı eklentisi kodu bu arabirimi uygulamalıdır. Bu tasarım ana amacı Hello hello kullanıcı kendi iş logics ve SCP.NET platformu tarafından işlenen diğer şeyleri toobe bırakarak odaklanabilirsiniz..

Merhaba kullanıcı eklentisi kodu hello aşağıdakilere arabirimlerinden biri, uygulamalıdır, hello topoloji işlem ya da işlem dışı olmasına ve hello bileşen spout veya Cıvata olmasına bağlıdır.

* ISCPSpout
* ISCPBolt
* ISCPTxSpout
* ISCPBatchBolt

### <a name="iscpplugin"></a>ISCPPlugin
ISCPPlugin hello ortak eklenti her türlü arabirimidir. Şu anda, onu bir kukla arabirimidir.

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a>ISCPSpout
ISCPSpout, işlemsel olmayan spout hello arabirimidir.

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

Zaman `NextTuple()` çağrıldığında hello C\# kullanıcı kodu bir veya daha fazla tanımlama grubu yayma. Yoksa hiçbir şey tooemit, bu yöntem döndürmelidir herhangi bir şey yayma olmadan. Dikkat edilmesi gereken, `NextTuple()`, `Ack()`, ve `Fail()` tümü tek bir iş parçacığı c sıkı döngü denir\# işlemi. Diziler tooemit olduğunda, kısa bir süre için (10 milisaniye gibi) değil toowaste olarak nedenle çok fazla CPU courteous toohave NextTuple uyku olduğu.

`Ack()`ve `Fail()` ack mekanizması belirtim dosyasında yalnızca etkin olarak adlandırılır. Merhaba `seqId` acked veya başarısız kullanılan tooidentify hello tanımlama grubu değil. Bu nedenle ACK işlemsel olmayan topolojisinde etkinleştirilirse, emit işlevi aşağıdaki hello içinde Spout kullanılmalıdır:

    public abstract void Emit(string streamId, List<object> values, long seqId); 

ACK işlemsel olmayan topolojisinde desteklenmiyorsa hello `Ack()` ve `Fail()` boş işlev olarak bırakılabilir.

Merhaba `parms` bu işlevler giriş parametrelerinde yalnızca boş sözlük, gelecekte kullanılmak üzere ayrılmıştır.

### <a name="iscpbolt"></a>ISCPBolt
ISCPBolt, işlemsel olmayan Cıvata hello arabirimidir.

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

Yeni tanımlama grubu kullanılabilir olduğunda, hello `Execute()` işlevi tooprocess çağrılır.

### <a name="iscptxspout"></a>ISCPTxSpout
ISCPTxSpout, işlem spout hello arabirimidir.

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

İşlem olmayan karşı erişmelerini'olduğu gibi `NextTx()`, `Ack()`, ve `Fail()` tümü tek bir iş parçacığı c sıkı döngü denir\# işlemi. Hiçbir veri tooemit olduğunda courteous toohave olan `NextTx` kısa bir süre (10 milisaniye) için çok fazla CPU değil toowaste olarak nedenle uyku.

`NextTx()`Yeni bir işlem toostart hello out parametresi olarak adlandırılır `seqId` ayrıca kullanılır kullanılan tooidentify hello işlem `Ack()` ve `Fail()`. İçinde `NextTx()`, kullanıcı veri tooJava yan yayma. Merhaba veri ZooKeeper toosupport yeniden yürütme içinde depolanır. ZooKeeper Hello kapasitesi sınırlı olduğundan, kullanıcı yalnızca meta veri, toplu veri işlem spout içinde değil yayması.

Storm yeniden yürütme bir işlem otomatik olarak başarısız olursa, bunu `Fail()` normal durumda çağrılmamalıdır. Ancak SCP işlem spout'un yayılan hello meta verileri işaretlerseniz çağırabilirsiniz `Fail()` hello meta veri olduğunda geçersiz.

Merhaba `parms` bu işlevler giriş parametrelerinde yalnızca boş sözlük, gelecekte kullanılmak üzere ayrılmıştır.

### <a name="iscpbatchbolt"></a>ISCPBatchBolt
ISCPBatchBolt, işlem Cıvata hello arabirimidir.

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

`Execute()`Yeni tanımlama grubu hello Cıvata ulaşan olduğunda çağrılır. `FinishBatch()`Bu işlem sona erdikten sonra çağrılır. Merhaba `parms` giriş parametresi, gelecekte kullanılmak üzere ayrılmıştır.

İşlem topolojisi için önemli bir kavram – olduğundan `StormTxAttempt`. İki alanı olan `TxId` ve `AttemptId`. `TxId`kullanılan tooidentify belirli bir işlemdir ve belirli bir işlem için birden çok deneme hello işlem başarısız olur ve durumunda olabilir yeniden. SCP.NET olacak yeni bir farklı ISCPBatchBolt nesne tooprocess her `StormTxAttempt`, yalnızca Java yan hangi Storm yapmak gibi. Bu tasarım Hello amacı toosupport paralel işlemleri işleme budur. Kullanıcı bunu göz önünde, işlem girişimi tamamlandı, hello karşılık gelen ISCPBatchBolt nesne yok ve atık toplanan tutmanız gerekir.

## <a name="object-model"></a>Nesne modeli
SCP.NET basit bir anahtar nesneleri kümesi ile geliştiriciler tooprogram için de sağlar. Bunlar **bağlamı**, **StateStore**, ve **SCPRuntime**. Merhaba geri kalan bölümünde, bu bölümün incelenecektir.

### <a name="context"></a>Bağlam
Bağlam çalışan bir ortam toohello uygulama sağlar. Her ISCPPlugin örneğinin (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) karşılık gelen bir bağlam örneği vardır. Bağlam tarafından sağlanan hello işlevselliği iki bölüme bölünmüş: bulunan (1) hello statik bölümü hello tüm C\# işlem, yalnızca hello belirli bağlam örneği için kullanılabilir olan (2) hello dinamik bölümü.

### <a name="static-part"></a>Statik bölümü
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

`Logger`Günlük amaçla sağlanır.

`pluginType`olan tooindicate hello eklentisi türü hello C kullanılan\# işlemi. Varsa hello C\# işlemi (olmadan Java) yerel test modda çalıştırılır, hello eklentisi tür `SCP_NET_LOCAL`.

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

`Config`Java taraftaki tooget yapılandırma parametrelerini sağlanır. Merhaba parametreleri Java taraftan geçirilen zaman C\# eklentisi başlatılır. Merhaba `Config` parametreleri iki parçalara bölünür: `stormConf` ve `pluginConf`.

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

`stormConf`Storm tarafından tanımlanan parametre ve `pluginConf` SCP tarafından tanımlanan hello parametre. Örneğin:

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

`TopologyContext`tooget hello topoloji bağlamı ile birden çok paralellik bileşenleri için en kullanışlı sağlanır. Örnek aşağıda verilmiştir:

    //demo how tooget TopologyContext info
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)                      
    {
        Context.Logger.Info("TopologyContext info:");
        TopologyContext topologyContext = Context.TopologyContext;                    
        Context.Logger.Info("taskId: {0}", topologyContext.GetThisTaskId());          
        taskIndex = topologyContext.GetThisTaskIndex();
        Context.Logger.Info("taskIndex: {0}", taskIndex);
        string componentId = topologyContext.GetThisComponentId();                    
        Context.Logger.Info("componentId: {0}", componentId);
        List<int> componentTasks = topologyContext.GetComponentTasks(componentId);  
        Context.Logger.Info("taskNum: {0}", componentTasks.Count);                    
    }

### <a name="dynamic-part"></a>Dinamik bölümü
Merhaba arabirimleri ilgili tooa belirli bağlam örneği olan. Merhaba bağlam örneği SCP.NET platformu tarafından oluşturulan ve toohello kullanıcı kodu geçirildi:

    // Declare hello Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple toodefault stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple toohello specific stream.
    public abstract void Emit(string streamId, List<object> values);  

ACK destekleme işlemsel olmayan spout için yöntemi aşağıdaki hello sağlanır:

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

ACK destekleme işlemsel olmayan Cıvata için açıkça gerektiği `Ack()` veya `Fail()` aldığı tanımlama grubu hello. Ve yeni tanımlama grubu yayma, ayrıca hello bağlayıcılarını hello yeni tanımlama grubu olarak belirtmeniz gerekir. yöntemler aşağıdaki hello sağlanır.

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a>StateStore
`StateStore`Meta Veri Hizmetleri, monoton sıra oluşturma ve bekleme serbest eşgüdüm sağlar. Üst düzey dağıtılmış eşzamanlılık soyutlamalar oluşturulabilen `StateStore`dağıtılmış kilitleri, dağıtılmış kuyruklar, engelleri ve işlem Hizmetleri dahil olmak üzere.

SCP uygulamaları hello kullanabilir `State` toopersist ZooKeeper, özellikle işlem topolojisi için bazı bilgileri nesne. Böylece işlem spout çöker ve yeniden başlatırsanız, ZooKeeper hello gerekli bilgileri almak ve hello ardışık düzeni yeniden yapılıyor.

Merhaba `StateStore` nesnenin çoğunlukla bu yöntemleri vardır:

    /// <summary>
    /// Static method tooretrieve a state store of hello given path and connStr 
    /// </summary>
    /// <param name="storePath">StateStore Path</param>
    /// <param name="connStr">StateStore Address</param>
    /// <returns>Instance of StateStore</returns>
    public static StateStore Get(string storePath, string connStr);

    /// <summary>
    /// Create a new state object in this state store instance
    /// </summary>
    /// <returns>State from StateStore</returns>
    public State Create();

    /// <summary>
    /// Retrieve all states that were previously uncommitted, excluding all aborted states 
    /// </summary>
    /// <returns>Uncommited States</returns>
    public IEnumerable<State> GetUnCommitted();

    /// <summary>
    /// Get all hello States in hello StateStore
    /// </summary>
    /// <returns>All hello States</returns>
    public IEnumerable<State> States();

    /// <summary>
    /// Get state or registry object
    /// </summary>
    /// <param name="info">Registry Name(Registry only)</param>
    /// <typeparam name="T">Type, Registry or State</typeparam>
    /// <returns>Return Registry or State</returns>
    public T Get<T>(string info = null);

    /// <summary>
    /// List all hello committed states
    /// </summary>
    /// <returns>Registries contain hello Committed State </returns> 
    public IEnumerable<Registry> Commited();

    /// <summary>
    /// List all hello Aborted State in hello StateStore
    /// </summary>
    /// <returns>Registries contain hello Aborted State</returns>
    public IEnumerable<Registry> Aborted();

    /// <summary>
    /// Retrieve an existing state object from this state store instance 
    /// </summary>
    /// <returns>State from StateStore</returns>
    /// <typeparam name="T">stateId, id of hello State</typeparam>
    public State GetState(long stateId)

Merhaba `State` nesnenin çoğunlukla bu yöntemleri vardır:

    /// <summary>
    /// Set hello status of hello state object toocommit 
    /// </summary>
    public void Commit(bool simpleMode = true); 

    /// <summary>
    /// Set hello status of hello state object tooabort 
    /// </summary>
    public void Abort();

    /// <summary>
    /// Put an attribute value under hello give key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <param name="attribute">State Attribute</param> 
    public void PutAttribute<T>(string key, T attribute); 

    /// <summary>
    /// Get hello attribute value associated with hello given key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <returns>State Attribute</returns>               
    public T GetAttribute<T>(string key);                    

Hello için `Commit()` yöntemi, simpleMode tootrue ayarladığınızda, onu yalnızca silecek ZooKeeper ZNode karşılık gelen hello. Aksi takdirde silecek geçerli ZNode hello ve hello kabul edilen yeni bir düğüm ekleme\_yolu.

### <a name="scpruntime"></a>SCPRuntime
SCPRuntime hello aşağıdaki iki yöntem sağlar.

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

`Initialize()`kullanılan tooinitialize hello SCP çalışma zamanı ortamı alır. Bu yöntemde, C hello\# işlem bağlanan toohello Java yan ve yapılandırma parametreleri alır ve topoloji bağlamı.

`LaunchPlugin()`kullanılan tookick selamlama iletisine kapalı döngü işliyor. Bu bir döngüde C hello\# eklentisi iletileri form Java yan (başlık ve denetim sinyalleri dahil) alır ve ardından belki de hello arabirim yöntemi çağırma işlemi Merhaba iletileri hello kullanıcı kodu tarafından sağlayın. Merhaba giriş parametresi yöntemi için `LaunchPlugin()` ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt arabirimini uygulayan nesne döndüren bir temsilci.

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

ISCPBatchBolt için biz alabilirsiniz `StormTxAttempt` gelen `parms`ve yeniden yürütülmüş bir girişim olduğunu toojudge kullanın. Bu genellikle hello yürütme Cıvata yapılır ve hello gösterilen `HelloWorldTx` örnek.

Genel olarak bakıldığında, hello SCP eklentileri burada iki modda çalışabilir:

1. Yerel Test modu: Bu modda SCP eklentileri hello (Merhaba C\# kullanıcı kodu) Visual Studio içinde hello geliştirme aşamasında çalıştırın. `LocalContext`Bu modda, yöntem tooserialize yayılan hello diziler toolocal dosyaları ve toomemory geri okuma sağlayan kullanılabilir.
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. Normal modu: Bu modda, hello SCP eklentileri storm java işlemi tarafından başlatılır.
   
    SCP eklentisi başlatmanın örnek aşağıda verilmiştir:
   
        namespace Scp.App.HelloWorld
        {
        public class Generator : ISCPSpout
        {
            … …
            public static Generator Get(Context ctx, Dictionary<string, Object> parms)
            {
            return new Generator(ctx);
            }
        }
   
        class HelloWorld
        {
            static void Main(string[] args)
            {
            /* Setting hello environment variable here can change hello log file name */
            System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "HelloWorld");
   
            SCPRuntime.Initialize();
            SCPRuntime.LaunchPlugin(new newSCPPlugin(Generator.Get));
            }
        }
        }

## <a name="topology-specification-language"></a>Topoloji belirtimi dili
SCP topoloji açıklayan ve SCP topolojileri yapılandırmak için etki alanı belirli bir dil belirtimidir. Storm'ın Clojure DSL üzerinde temel alır (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) ve SCP tarafından genişletilir.

Merhaba yürütme için doğrudan toostorm küme topolojisi belirtimleri'nin gönderilebilir ***runspec*** komutu.

SCP.NET sahip izleme işlevleri toodefine hello işlem topoloji ekleyin:

| **Yeni işlevleri** | **Parametreler** | **Açıklama** |
| --- | --- | --- |
| **Tx topolopy** |Topoloji adı<br />spout eşleme<br />Cıvata eşleme |Merhaba topoloji ada sahip bir işlem topolojisi tanımlayın &nbsp;tanımı harita ve hello Cıvatalar tanımı Haritası spout'lar |
| **SCP tx spout** |Exec adı<br />bağımsız değişken<br />Alanları |İşlem spout tanımlayın. Merhaba uygulaması ile çalışacak ***exec adı*** kullanarak ***args***.<br /><br />Merhaba ***alanları*** hello çıktı alanları spout için |
| **tx toplu Cıvata SCP** |Exec adı<br />bağımsız değişken<br />Alanları |Bir işlem toplu Cıvata tanımlayın. Merhaba uygulaması ile çalışacak ***exec adı*** kullanarak ***bağımsız değişken.***<br /><br />Merhaba alanlar Cıvata Merhaba çıktı alanları modudur. |
| **SCP-tx-yürütme-Cıvata** |Exec adı<br />bağımsız değişken<br />Alanları |Bir işlem Committer Cıvata tanımlayın. Merhaba uygulaması ile çalışacak ***exec adı*** kullanarak ***args***.<br /><br />Merhaba ***alanları*** hello çıktı alanları Cıvata için |
| **nontx topolopy** |Topoloji adı<br />spout eşleme<br />Cıvata eşleme |Merhaba topoloji adı, bir işlem topolojisi tanımlayın&nbsp; tanımı harita ve hello Cıvatalar tanımı Haritası spout'lar |
| **SCP spout** |Exec adı<br />bağımsız değişken<br />Alanları<br />parametreler |Bir işlem spout tanımlayın. Merhaba uygulaması ile çalışacak ***exec adı*** kullanarak ***args***.<br /><br />Merhaba ***alanları*** hello çıktı alanları spout için<br /><br />Merhaba ***parametreleri*** toospecify kullanarak isteğe bağlıdır, "nontransactional.ack.enabled" gibi bazı parametreler. |
| **SCP Cıvata** |Exec adı<br />bağımsız değişken<br />Alanları<br />parametreler |İşlem dışı Cıvata tanımlayın. Merhaba uygulaması ile çalışacak ***exec adı*** kullanarak ***args***.<br /><br />Merhaba ***alanları*** hello çıktı alanları Cıvata için<br /><br />Merhaba ***parametreleri*** toospecify kullanarak isteğe bağlıdır, "nontransactional.ack.enabled" gibi bazı parametreler. |

SCP.NET sahip izleyin anahtarlar tanımlı sözcükleri:

| **Anahtar sözcükler** | **Açıklama** |
| --- | --- |
| **: adı** |Merhaba topoloji adı tanımlayın |
| **: topolojisi** |Tanımlama işlevleri yukarıda hello kullanarak topolojisi hello ve olanları içinde derleme. |
| **: p** |Her spout veya Cıvata için Hello paralellik ipucu tanımlayın. |
| **: yapılandırma** |Tanımlama güncelleştirme var olanları hello veya parametre yapılandırma |
| **: şeması** |Merhaba, şema akış tanımlayın. |

Ve sık kullanılan parametreler:

| **Parametre** | **Açıklama** |
| --- | --- |
| **"plugin.name"** |Merhaba C# eklentisi exe dosyası adı |
| **"plugin.args"** |Eklenti bağımsız değişken |
| **"output.schema"** |Çıkış şeması |
| **"nontransactional.ack.enabled"** |Ack işlem topolojisi için etkinleştirilip etkinleştirilmediği |

Merhaba runspec komutu hello BITS ile birlikte dağıtılır, hello kullanım gibidir:

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

Merhaba ***kaynak dir*** parametre isteğe bağlıdır ve toospecify gerekir, tooplug C istediğinizde\# uygulama ve bu dizin hello uygulama, başlangıç bağımlılıkları ve yapılandırmaları içerecek.

Merhaba ***sınıf*** parametredir Ayrıca isteğe bağlı. Merhaba belirtim dosya Java Spout veya Cıvata içeriyorsa kullanılan toospecify hello Java sınıf olur.

## <a name="miscellaneous-features"></a>Çeşitli özellikler
### <a name="input-and-output-schema-declaration"></a>Girdi ve çıktı şema bildirimi
Merhaba kullanıcı c tanımlama grubu yayma\# işlemek, hello platform tooserialize hello tuple gereken byte [], aktarım tooJava yan ve Storm bu tanımlama grubu toohello hedefleri aktarım. Bu sırada aşağı akış bileşeni C hello\# işlemi geri java taraftan tanımlama grubu alır ve platforma göre toohello özgün türleri dönüştürme, bu işlemlerin hello Platform tarafından gizlenir.

toosupport hello serileştirme ve seri durumundan çıkarma, kullanıcı kodu hello girişleri ve çıkışları toodeclare hello şeması gerekir.

hello giriş/çıkış akışı şema bir sözlük olarak tanımlanmış, hello hello StreamId anahtarıdır ve hello sütun hello türlerini hello değerdir. Merhaba bileşen bildirilen çok akışları sahip olabilir.

    public class ComponentStreamSchema
    {
        public Dictionary<string, List<Type>> InputStreamSchema { get; set; }
        public Dictionary<string, List<Type>> OutputStreamSchema { get; set; }
        public ComponentStreamSchema(Dictionary<string, List<Type>> input, Dictionary<string, List<Type>> output)
        {
            InputStreamSchema = input;
            OutputStreamSchema = output;
        }
    }


Bağlam nesnesinde aşağıdaki API eklenen hello vardır:

    public void DeclareComponentSchema(ComponentStreamSchema schema)

Kullanıcı kodu yayılan hello diziler için bu akış tanımlanan hello şema uyma veya hello sistem çalışma zamanı özel durum atar emin olmanız gerekir.

### <a name="multi-stream-support"></a>Birden çok akış desteği
SCP destekler kullanıcı tooemit kod veya birden çok farklı akış hello adresindeki aynı almak zaman. Merhaba Emit yöntemi bir isteğe bağlı Akış ID parametresi yararlanırken hello destek hello bağlamı nesnesinde yansıtır.

Merhaba SCP.NET bağlam nesnesi öğesinde iki yöntem eklenmiştir. Kullanılan tooemit tanımlama grubu ya da diziler toospecify StreamId oldukları. Merhaba StreamId bir dize ve toobe hem c tutarlı gerekiyor\# ve topoloji tanımı Spec hello.

        /* Emit tuple toohello specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

Merhaba verme tooa var olmayan akışı çalışma zamanı özel durumları neden olur.

### <a name="fields-grouping"></a>Alanları gruplandırma
Merhaba yapı içinde alanları gruplandırmasındaki Strom SCP.NET içinde düzgün çalışmıyor. Hello Java Proxy tarafı, tüm hello alanları veri türleridir gerçekte byte [] ve gruplandırma hello alanlarını hello byte [] nesnesi karma kodu tooperform hello gruplandırma kullanır. Merhaba byte [] nesnesi karma kodu, bu nesnenin bellekte hello adresidir. [] Hello gruplandırma için iki bayt yanlış olması için aynı içerik ancak aynı adres hello değil o paylaşımı hello nesneleri.

Özelleştirilmiş gruplandırma yöntemi SCP.NET ekler ve hello byte [] toodo hello gruplandırma Merhaba içeriğine kullanır. İçinde **SPEC** hello sözdizimi dosya, benzer:

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


Burada,

1. "scp alan grup", "SCP tarafından uygulanan özelleştirilmiş alan gruplandırma" anlamına gelir.
2. ": tx"veya": tx olmayan" işlem topoloji olduğu anlamına gelir. Dizininden başlayarak hello tx olmayan topolojileri tx farklı olduğundan bu bilgileri ihtiyacımız var.
3. [0,1] anlamına alan kimlikleri, 0'dan başlayarak izleri hashset'i.

### <a name="hybrid-topology"></a>Karma topolojisi
Merhaba yerel Storm Java yazılır. SCP.Net Gelişmiş ve onu tooenable bizim Gümrük toowrite C\# toohandle kendi iş mantığı kod. Ancak aynı zamanda karma topolojiler yalnızca C içeren destekliyoruz\# spout'lar/Cıvatalar, aynı zamanda Java Spout/Cıvatalar.

### <a name="specify-java-spoutbolt-in-spec-file"></a>Java Spout/Cıvata belirtim dosyasında belirtin
Belirtim dosyasındaki "scp-spout" ve "scp-Cıvata" Ayrıca Java kullanılan toospecify Spout'lar ve Cıvatalar olabilir, örnek aşağıda verilmiştir:

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

Burada `microsoft.scp.example.HybridTopology.Generator` hello Java Spout sınıfı hello adıdır.

### <a name="specify-java-classpath-in-runspec-command"></a>Java sınıf runSpec komutunu belirtin
Java Spout'lar veya Cıvatalar içeren toosubmit topoloji istiyorsanız toofirst derleme hello Java Spout'lar veya Cıvatalar gerekir ve hello Jar dosyalarını alın. Ardından hello java topolojisi gönderirken hello Jar dosyalarını içeren bir sınıf belirtmeniz gerekir. Örnek aşağıda verilmiştir:

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

Burada **örnekler\\HybridTopology\\java\\hedef\\**  olan hello içeren klasör hello Java Spout/Cıvata Jar dosyasını.

### <a name="serialization-and-deserialization-between-java-and-c"></a>Seri hale getirme ve seri durumdan çıkarma Java ve C\ arasında
Java yan ve C bizim SCP bileşeni içerir\# yan. Sipariş toointeract ile yerel Java Spout'lar/Cıvatalar, serileştirme/seri durumdan çıkarma Java yan ve C uygulanması gereken\# hello grafiği aşağıdaki gösterildiği gibi tarafı.

![java bileşeni tooJava bileşen gönderme tooSCP bileşen gönderme diyagramı](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. **Seri hale getirme Java yan ve seri durumdan çıkarma c\# yan**
   
   Java taraf serileştirme ve seri durumundan çıkarma c için varsayılan uygulaması ilk sağladığımız\# yan. Java taraf Hello seri duruma getirme yöntemi belirtim dosyasında belirtilebilir:
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   Merhaba C seri durumdan çıkarma yöntemini\# yan C'de belirtilmelidir\# kullanıcı kodu:
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   Merhaba veri türü çok karmaşık değilse, çoğu durumda bu varsayılan uygulama işlemelidir. Bazı durumlarda, ya da hello kullanıcı veri türü çok karmaşık olduğu için veya hello bizim varsayılan uygulama performansını karşılamadığı için kullanıcının gereksinim, kullanıcı can eklenti kendi uygulama hello.
   
   Merhaba seri arabirimi Java'da yan olarak tanımlanır:
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   Merhaba seri durumdan C arabiriminde\# yan olarak tanımlanır:
   
   Ortak arabirimi ICustomizedInteropCSharpDeserializer
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. **Seri hale getirme c\# yan ve Java yan yana çıkarma**
   
   Merhaba seri duruma getirme yöntemi c\# yan C'de belirtilmelidir\# kullanıcı kodu:
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   Merhaba seri durumdan çıkarma yöntemini Java taraf belirtim dosyasında belirtilen:
   
     (scp-spout
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   Burada "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" Merhaba seri durumdan Çıkarıcının adıdır ve "microsoft.scp.example.HybridTopology.Person" Merhaba hedef sınıf hello verileri seri durumdan olduğu.
   
   Kullanıcı ayrıca eklenti yapabilir, kendi uygulama c\# seri hale getirici ve Java seri durumdan Çıkarıcının. Bu hello C arabirimidir\# seri hale getirici:
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   Bu Java kaldırıcı hello arabirimi.
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a>SCP ana mod
Bu modda, kullanıcı kendi kodlarını tooDLL derleyin ve SCP toosubmit topolojisi tarafından sağlanan SCPHost.exe kullanın. Merhaba belirtim dosyası şuna benzer:

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

Burada, `plugin.name` olarak belirtilen `SCPHost.exe` SCP SDK'sı tarafından sağlanan. Tam olarak üç parametre kabul eden SCPHost.exe:

1. Merhaba ilk olduğu hello DLL adı biridir `"HelloWorld.dll"` Bu örnekte.
2. Merhaba ikincisi olan hello sınıfı adıdır `"Scp.App.HelloWorld.Generator"` Bu örnekte.
3. Merhaba üçüncü bir hello çağrılan tooget ISCPPlugin örneği olabilir genel bir statik yöntem adıdır.

Ana mod, kullanıcı kodu DLL olarak derlenmiş ve SCP platformu tarafından çağrılır. Bu nedenle SCP platform hello tüm işleme mantığı üzerinde tam denetimi elde edebilirsiniz. Merhaba geliştirme deneyimi kolaylaştırmak ve bize de sonraki sürüm için daha fazla esneklik ve daha iyi geriye dönük uyumluluk Getir müşterilerimizin SCP ana mod toosubmit topolojisinde nedenle öneririz.

## <a name="scp-programming-examples"></a>SCP programlama örnekleri
### <a name="helloworld"></a>HelloWorld
**HelloWorld** çok basit bir örnek tooshow SCP.Net bakış değil. Adlı bir spout ile bir işlemsel olmayan topolojisi kullanır **Oluşturucu**ve adlı iki Cıvatalar **Bölümlendirici** ve **sayaç**. Merhaba spout **Oluşturucu** rastgele bazı cümleleri oluşturur ve bu cümleleri çok yayma**Bölümlendirici**. Merhaba Cıvata **Bölümlendirici** hello cümleleri toowords bölme ve bu sözcükleri çok yayma**sayaç** Cıvata. Merhaba Cıvata "sayacı" bir sözlük toorecord hello oluşum sayısı her sözcüğün kullanır.

İki belirtim dosya **HelloWorld.spec** ve **HelloWorld\_EnableAck.spec** Bu örnek için. Merhaba C içinde\# kodu, onu bulabilir ack Java taraftan hello pluginConf alarak etkinleştirilip etkinleştirilmediği çıkışı.

    /* demo how tooget pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

ACK etkinleştirilirse hello spout içinde bir sözlük acked edilmemiş kullanılan toocache hello diziler olur. Fail() çağrılırsa, hello başarısız tanımlama grubu yeniden yürütülmesi:

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        Context.Logger.Info("Fail, seqId: {0}", seqId);
        if (cachedTuples.ContainsKey(seqId))
        {
            /* get hello cached tuple */
            string sentence = cachedTuples[seqId];

            /* replay hello failed tuple */
            Context.Logger.Info("Re-Emit: {0}, seqId: {1}", sentence, seqId);
            this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), seqId);
        }
        else
        {
            Context.Logger.Warn("Fail(), can't find cached tuple for seqId {0}!", seqId);
        }
    }

### <a name="helloworldtx"></a>HelloWorldTx
Merhaba **HelloWorldTx** örnek gösterir nasıl tooimplement işlem topolojisi. Adlı bir spout sahip **Oluşturucu**, bir toplu Cıvatalar adlı **kısmi-count**, ve bir yürütme Cıvata adlı **sayısı toplam**. Ayrıca üç önceden oluşturulmuş txt dosyaları vardır: **DataSource0.txt**, **DataSource1.txt** ve **DataSource2.txt**.

Spout her işlemde hello **Oluşturucu** rastgele iki dosyaları üç dosya önceden oluşturulmuş hello seçin ve hello iki dosya adları toohello yayma **kısmi-count** Cıvata. Merhaba Cıvata **kısmi-count** ilk hello dosya adı bu dosyada alınan hello tuple sonra açık hello dosya ve sayısı hello sözcük sayısını alın ve son olarak hello word numara toohello yayma **sayısı toplam**Cıvata. Merhaba **sayısı toplam** Cıvata hello toplam sayısı özetlemek.

tooachieve **tam olarak bir kez** semantiği, hello yürütme Cıvata **sayısı toplam** yeniden yürütülmüş bir işlem olup olmadığını toojudge gerekir. Bu örnekte, bir statik üye değişkeni vardır:

    public static long lastCommittedTxId = -1; 

ISCPBatchBolt örneği oluşturulduğunda, hello alırsınız `txAttempt` Giriş parametrelerinden:

    public static CountSum Get(Context ctx, Dictionary<string, Object> parms)
    {
        /* for transactional topology, we can get txAttempt from hello input parms */
        if (parms.ContainsKey(Constants.STORM_TX_ATTEMPT))
        {
            StormTxAttempt txAttempt = (StormTxAttempt)parms[Constants.STORM_TX_ATTEMPT];
            return new CountSum(ctx, txAttempt);
        }
        else
        {
            throw new Exception("null txAttempt");
        }
    }

Zaman `FinishBatch()` , hello adlandırılır `lastCommittedTxId` yeniden yürütülmüş bir işlem değilse güncelleştirme olacaktır.

    public void FinishBatch(Dictionary<string, Object> parms)
    {
        /* judge whether it is a replayed transaction? */
        bool replay = (this.txAttempt.TxId <= lastCommittedTxId);

        if (!replay)
        {
            /* If it is not replayed, update hello toalCount and lastCommittedTxId vaule */
            totalCount = totalCount + this.count;
            lastCommittedTxId = this.txAttempt.TxId;
        }
        … …
    }


### <a name="hybridtopology"></a>HybridTopology
Bu topoloji Spout Java ve C içeren\# Cıvata. SCP platform tarafından sağlanan hello varsayılan seri hale getirme ve seri durumdan çıkarma uygulaması kullanır. Ref hello lütfen **HybridTopology.spec** içinde **örnekler\\HybridTopology** hello belirtim dosya ayrıntıları için klasör ve **SubmitTopology.bat** nasıl toospecify Java sınıf.

### <a name="scphostdemo"></a>SCPHostDemo
Bu örnekte olduğu hello HelloWorld aynı temelde. Merhaba yalnızca hello kullanıcı kodu DLL olarak derlenir ve hello topoloji SCPHost.exe kullanılarak gönderilen farktır. Ref hello bölüm "SCP ana modu" daha ayrıntılı açıklaması için lütfen.

## <a name="next-steps"></a>Sonraki Adımlar
Storm topolojilerini SCP kullanılarak oluşturulan bir örnekleri için hello aşağıdakilere bakın:

* [Visual Studio kullanarak Hdınsight üzerinde Apache Storm için C# topolojileri geliştirme](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [Hdınsight üzerinde Storm ile Azure Event hubs'tan işlem olayları](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [Bir C# Storm topolojisinde birden çok veri akışı oluşturma](hdinsight-storm-twitter-trending.md)
* [Power BI toovisualize veri bir Storm topolojisinin kullanın](hdinsight-storm-power-bi-topology.md)
* [Event Hubs Hdınsight üzerinde Storm kullanmaya aracın algılayıcı verilerini işlemek](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [Ayıklama, dönüştürme ve yükleme (ETL) Azure Event Hubs tooHBase gelen](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [Hdınsight üzerinde Storm ve HBase kullanarak olayları ilişkilendirmenize](hdinsight-storm-correlation-topology.md)

