---
title: aaaPartitioning Service Fabric Hizmetleri | Microsoft Docs
description: "Açıklar nasıl toopartition Service Fabric durum bilgisi olan hizmetler. Bölümler, veri ve işlem birlikte Genişletilebilir şekilde hello yerel makinede veri depolama sağlar."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 3b7248c8-ea92-4964-85e7-6f1291b5cc7b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: msfussell
ms.openlocfilehash: 6ead48716c08f4212535202ee69d169067d5c6d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="partition-service-fabric-reliable-services"></a>Bölüm Service Fabric güvenilir hizmetler
Bu makale, Azure Service Fabric güvenilir hizmetler bölümleme temel kavramları giriş toohello sağlar. Merhaba hello makalede kullanılan kaynak kodunu da kullanılabilir [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).

## <a name="partitioning"></a>Bölümleme
Bölümleme benzersiz tooService doku değil. Aslında, ölçeklenebilir hizmetler oluşturmaya bir çekirdek desenini değil. Daha geniş anlamda, biz durumu (veri) ayırma kavram olarak bölümlendirme hakkında düşünün ve daha küçük erişilebilir birimleri tooimprove ölçeklenebilirlik ve performans işlem. Bölümlendirme, iyi bilinen bir form [veri bölümlendirme][wikipartition], parçalama olarak da bilinir.

### <a name="partition-service-fabric-stateless-services"></a>Bölüm Service Fabric durum bilgisi olmayan hizmetler
Durum bilgisi olmayan hizmetler için bir hizmet bir veya daha fazla örneklerini içeren bir birimi olan bir bölüm hakkında düşünebilirsiniz. Şekil 1 bir durum bilgisi olmayan hizmetin bir bölüm kullanarak bir kümede dağıtılmış beş örneğiyle gösterir.

![Durum bilgisiz hizmeti](./media/service-fabric-concepts-partitioning/statelessinstances.png)

Gerçekten durum bilgisiz hizmet çözümlerine iki tür vardır. Merhaba ilk durumuna harici olarak örneğin (gibi hello oturum bilgilerini ve veri depolayan bir Web sitesi) bir Azure SQL veritabanında kalıcı bir hizmet biridir. Merhaba ikinci herhangi kalıcı durumunu yönetme değil yalnızca Hesaplama Hizmetleri (örneğin, bir hesap makinesi veya görüntü küçük resim oluşturma) olabilir.

İçinde bir durum bilgisi olmayan hizmetin bölümlendirme, çok nadir bir senaryo--ölçeklenebilirlik bir durumdur ve kullanılabilirlik normalde elde fazla örneğe ekleyerek. Durum bilgisiz hizmet örnekleri için birden çok bölüm toomeet özel yönlendirme ihtiyacınız olduğunda tooconsider istediğiniz hello yalnızca zamanı ister.

Örnek olarak, burada belirli bir aralıkla kimlikleri kullanıcılar yalnızca belirli bir hizmet örneği tarafından sunulması bir durum düşünün. Gerçekten bölümlenmiş arka uç (ör parçalı SQL veritabanı) sahip ve hangi hizmet örneğine toohello veritabanı parça--yazma veya diğer hazırlık işlemleri içinde gerçekleştirmesi toocontrol istediğinizde bir durum bilgisi olmayan hizmetin ne zaman bölüm, başka bir örnek verilmiştir Merhaba gerektiren durum bilgisiz hizmete hello aynı hello arka kullanılan bölümlenme bilgisi. Bu senaryo türlerini farklı şekillerde çözülebilir ve hizmet bölümleme gerektirmeyebilecek.

Bu kılavuzda Hello kalanı durum bilgisi olan hizmetler odaklanır.

### <a name="partition-service-fabric-stateful-services"></a>Bölüm Service Fabric durum bilgisi olan hizmetler
Service Fabric kılar kolay toodevelop ölçeklenebilir durum bilgisi olan hizmetler birinci sınıf bir yöntem sunarak toopartition durumu (veri). Üzerinden yüksek oranda güvenilir bir ölçek birimi olarak bir durum bilgisi olan hizmet bölüm hakkında kavramsal olarak, düşünebilirsiniz [çoğaltmaları](service-fabric-availability-services.md) , dağıtılmış ve bir kümede hello düğümleri arasında dengeli.

Service Fabric durum bilgisi olan hizmetler Hello bağlamında bölümleme toohello işleminin belirli bir hizmet bölümü hello tam hello hizmetinin durumunu bir kısmı için sorumlu olduğunu belirleme anlamına gelir. (Önce belirtildiği gibi bir bölüm kümesidir [çoğaltmaları](service-fabric-availability-services.md)). Service Fabric hakkında önemli bir şey, bunu hello bölümleri farklı düğümlerde yerleştirir ' dir. Bu toogrow tooa düğümün kaynak sınırı sağlar. Merhaba veri büyüme gereksinimlerine göre bölümleri büyümesine ve Service Fabric bölümleri düğümleri arasında yeniden dengeler. Bu, hello devam donanım kaynaklarını verimli bir şekilde kullanılmasını sağlar.

toogive bir örnek söylenebilir, 5 düğümlü bir küme ve yapılandırılmış toohave 10 bölümler ve üç çoğaltmaları hedefi bir hizmet ile başlar. Bu durumda, Service Fabric dengelemek ve hello çoğaltmalar Merhaba kümede--dağıtır ve iki birincil ile bitecek [çoğaltmaları](service-fabric-availability-services.md) düğüm başına.
Merhaba küme too10 düğümleri kullanıma tooscale artık ihtiyacınız varsa, Service Fabric hello birincil yeniden dengelemeniz [çoğaltmaları](service-fabric-availability-services.md) tüm 10 düğümleri arasında. Geri too5 düğümleri ölçeği, benzer şekilde, Service Fabric tüm hello çoğaltmalar Merhaba 5 düğümleri arasında yeniden dengelemeniz.  

Şekil 2 önce ve sonra hello küme ölçeklendirme 10 bölümlerinin hello dağılımını gösterir.

![Durum bilgisi olan hizmet](./media/service-fabric-concepts-partitioning/partitions.png)

Sonuç olarak, hello genişleme istemcilerinden gelen istekleri bilgisayarlar arasında dağıtılır, hello uygulamasının genel performansı geliştirildi ve veri erişim toochunks üzerinde Çekişme sınırlı olduğundan elde edilir.

## <a name="plan-for-partitioning"></a>Bölümleme planlama
Bir hizmet uygulamadan önce her zaman kullanıma gerekli tooscale stratejisi bölümleme hello düşünmelisiniz. Farklı yolu vardır, ancak bunların tümünün hangi Merhaba uygulaması tooachieve gereken odaklanın. Bu makalede Hello bağlamının şimdi hello bazıları daha önemli yönlerinden göz önünde bulundurun.

Toothink hello yapısı, hello ilk adım olarak bölümlenmiş toobe gereken hello durumu hakkında bir iyi yaklaşımdır.

Basit bir örnek atalım. Toobuild countywide yoklama için bir hizmet olsaydı, her şehir için bir bölüm hello ilçe oluşturabilirsiniz. Ardından, toothat Şehir karşılık gelen hello bölümünde hello şehirde hello oyları her kişi için saklayabilirsiniz. Şekil 3'içinde bulundukları kişiler ve hello Şehir kümesi gösterilmektedir.

![Basit bölüm](./media/service-fabric-concepts-partitioning/cities.png)

Şehir Hello popülasyonunu yaygın değiştikçe, çok miktarda veri (örneğin, Seattle) içeren bazı bölümleri ve çok az durumu (örneğin Kirkland) ile diğer bölümleri ile bitirebilirsiniz. Bu nedenle durumu eşit miktarda bölümlemeye sahip olmak hello etkisi nedir?

Merhaba örneği hakkında yeniden düşünüyorsanız, Seattle için hello oylarının tutan hello bölüm hello Kirkland bir değerinden daha fazla trafik alırsınız kolayca görebilirsiniz. Varsayılan olarak, Service Fabric hello hakkında emin yapar birincil ve ikincil çoğaltmaları her düğümde aynı sayıda. Bu nedenle, daha az trafik hizmet daha fazla trafik ve diğerleri hizmet çoğaltmaları tutun düğümleriyle bitirebilirsiniz. Soğuk noktalar bu bir kümede gibi ve, tercihen tooavoid etkin istersiniz.

İçinde tooavoid Bu sipariş, bir bölümleme açısından iki şey yapmanız:

* Böylece tüm bölümleri arasında eşit olarak dağıtılır toopartition hello durumu deneyin.
* Rapor yük hello hizmeti için hello çoğaltmaları her biri. (Bu makalede hakkında daha fazla bilgi için kontrol [ölçümleri ve yük](service-fabric-cluster-resource-manager-metrics.md)). Service Fabric bellek miktarı veya kayıt sayısı gibi hizmetleri tarafından tüketilen hello yetenek tooreport yük sağlar. Hiçbir düğümü genel aşırı için bildirilen hello ölçülerine bağlı olarak, Service Fabric bazı bölümleri diğerlerinden daha yüksek yüklerini hizmet veren ve hello küme taşıma çoğaltmaları toomore uygun düğümleri tarafından yeniden dengeler algılar.

Bazı durumlarda, ne kadar veri belli bir bölüm olacak bilemezsiniz. Genel bir öneri toodo hem--olacak şekilde ilk olarak, bölümleme stratejisine kabul ederek, hello veri eşit hello bölümler ve saniye raporlama yük tarafından yayar.  Merhaba ilk yöntem hello ikinci erişim ya da yük geçici farklılıkları düzgünleştirme zamanla tutarken örnek, oylama hello açıklanan durumlarda engeller.

Bölüm planlamanın bir diğer unsuru toochoose hello doğru bölümleri toobegin ile sayısıdır.
Service Fabric açısından bakıldığında, hiçbir şey yoktur senaryonuz için beklenenden daha yüksek bir bölüm sayısı ile başlıyor engeller.
Aslında, hello en çok bölüm sayısı varsayarak bir geçerli bir yaklaşımdır.

Nadir durumlarda, ilk başta seçtiğiniz olandan daha fazla bölüm gerek yukarı bitebilir. Merhaba olaydan sonra hello bölüm sayısı değiştirilemez gibi bazı gelişmiş bölüm yaklaşımlar tooapply gerekir, hello yeni bir hizmet örneğini oluşturma gibi aynı hizmeti türü. Merhaba yönlendirir bazı istemci-tarafı mantığı toohello doğru hizmet örneği, istemci kodunuzun korumalıdır istemci-tarafı bilgisini temel alarak istekleri tooimplement de gerekir.

Planlama bölümleme için başka bir hello mevcut bilgisayar kaynaklarına noktadır. Merhaba durumu erişilen ve depolanan toobe gerektiği ilişkili toofollow şunlardır:

* Ağ bant genişliği sınırları
* Sistem bellek sınırları
* Disk depolama sınırları

Bu nedenle çalıştıran bir kümedeki kaynak kısıtlamaları içine çalıştırırsanız ne olur? Merhaba yanıt hello küme tooaccommodate hello yeni gereksinimlerini yalnızca ölçeklendirebilirsiniz ' dir.

[Merhaba kapasite planlama Kılavuzu](service-fabric-capacity-planning.md) ilişkin yönergeler sunar toodetermine kaç düğümleri kümenizi gerekiyor.

## <a name="get-started-with-partitioning"></a>Bölümlendirme ile çalışmaya başlama
Bu bölüm, hizmetinizi bölümlendirme ile tooget nasıl başlatılacağını açıklar.

Service Fabric üç bölümleme şeması seçeneği sunar:

* (Uniformınt64partition da bilinir) bölümleme aralıklı.
* Bölümleme adı. Bu model genelde kullanan uygulamalar, sınırlı kümesinde bucketed veri içeriyor. Adlandırılmış bölüm anahtarları olarak kullanılan veri alanlarının sık karşılaşılan örnekleri, bölge, posta kodları, müşteri grupları veya diğer iş sınırları olacaktır.
* Tek bölümleme. Merhaba hizmeti herhangi bir ek yönlendirme gerekmediğinde singleton bölümler genellikle kullanılır. Örneğin, durum bilgisi olmayan hizmetler varsayılan olarak bu bölümleme düzenini kullanın.

Adlandırılmış ve özel formları aralıklı bölümlerinin tek bölümleme şemaları geçerlidir. Merhaba olduğu gibi varsayılan olarak, Service Fabric kullanmak için Visual Studio şablonları hello bölümlendirme, en yaygın ve kullanışlı bir aralıklı. Bu makalenin sonraki bölümlerinde Hello hello aralıklı bölümleme düzeni odaklanır.

### <a name="ranged-partitioning-scheme"></a>Bölümleme düzeni aralıklı
Kullanılan toospecify tamsayı budur (düşük anahtarı ve yüksek anahtar tarafından tanımlanır) aralığı ve bölüm (n) sayısı. N bölümler, her bir çakışmayan alt aralığı hello biri için sorumlu oluşturur genel anahtar aralığı'nı bölüm. Örneğin, ranged bölümleme düzeni düşük anahtar 0 ile 99 yüksek anahtarı ve 4 sayısını dört bölüm, aşağıda gösterildiği gibi oluşturursunuz.

![Bölümleme aralığı](./media/service-fabric-concepts-partitioning/range-partitioning.png)

Bir ortak toocreate hello veri kümesi içinde benzersiz bir anahtar göre bir karma bir yaklaşımdır. Bazı ortak anahtarları örnekleri bir araç kimlik numarası (Toplamıdır), bir çalışan kimliği veya benzersiz bir dize olabilir. Bu benzersiz anahtarı kullanarak, daha sonra bir karma kod, modül hello anahtar aralığı, toouse, anahtar olarak oluşturur. Merhaba üst ve alt sınır anahtar aralığı izin verilen hello belirtebilirsiniz.

### <a name="select-a-hash-algorithm"></a>Bir karma algoritması seçin
Karma önemli bir bölümü, karma algoritma seçme. Merhaba hedef toogroup benzer anahtarları birbirine yakın (yere göre hassas karma)--olup bir husustur veya etkinlik kapsamlı tüm bölümler (dağıtım karma) dağıtılması, daha yaygın olduğu.

iyi dağıtım karma algoritması Hello özellikleri şunlardır: kolay toocompute olan, birkaç çakışmaları olan ve hello anahtarları eşit dağıtır. İyi bir verimli karma algoritması hello bir örnektir [FNV-1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) karma algoritması.

Bir iyi genel karma kodu algoritması seçimler hello kaynaktır [karma işlevlerini Wikipedia sayfasında](http://en.wikipedia.org/wiki/Hash_function).

## <a name="build-a-stateful-service-with-multiple-partitions"></a>Durum bilgisi olan bir hizmet birden çok bölüm ile derleme
İlk güvenilir durum bilgisi olan hizmet birden çok bölüm oluşturalım. Bu örnekte, aynı harf hello hello ile başlayan tüm soyadlarını toostore istediğiniz çok basit bir uygulama oluşturacaksınız aynı bölüm.

Kod yazmadan önce hello bölümleri ve bölüm anahtarlarını ilgili toothink gerekir. 26 bölümleri (bir hello alfabe her harfin), ilgili gerekenler düşük ve yüksek anahtarlar hello?
Tam anlamıyla toohave bir bölüm harf başına istiyoruz gibi kendi anahtarını her harfi olduğu gibi biz 0 hello düşük anahtar ve 25 hello yüksek anahtar olarak kullanabilirsiniz.

> [!NOTE]
> Gerçekte hello dağıtım eşit olacak şekilde basitleştirilmiş bir senaryo budur. "S" veya "M" "X" Merhaba olanları başlangıç değerinden daha yaygın hello harflerle başlayan son adları veya "Y".
> 
> 

1. Açık **Visual Studio** > **dosya** > **yeni** > **proje**.
2. Merhaba, **yeni proje** iletişim kutusunda, Merhaba Service Fabric uygulaması seçin.
3. Merhaba proje "AlphabetPartitions" çağırın.
4. Merhaba, **bir hizmet oluşturma** iletişim kutusunda, seçin **durum bilgisi olan** hizmet ve "Alphabet.Processing" Merhaba resimde gösterildiği gibi çağırın.
       ![Visual Studio'da yeni hizmet iletişim kutusu][1]

  <!--  ![Stateful service screenshot](./media/service-fabric-concepts-partitioning/createstateful.png)-->

5. Bölümler Hello sayısını ayarlayın. Açık hello Applicationmanifest.xml dosya hello hello AlphabetPartitions proje ve güncelleştirme hello parametre aşağıda gösterildiği gibi Processing_PartitionCount too26 ApplicationPackageRoot klasöründe bulunan.
   
    ```xml
    <Parameter Name="Processing_PartitionCount" DefaultValue="26" />
    ```
   
    Tooupdate hello LowKey ve hello StatefulService hello aşağıda gösterildiği gibi ApplicationManifest.xml öğesinde HighKey özelliklerini de gerekir.
   
    ```xml
    <Service Name="Processing">
      <StatefulService ServiceTypeName="ProcessingType" TargetReplicaSetSize="[Processing_TargetReplicaSetSize]" MinReplicaSetSize="[Processing_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[Processing_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    ```
6. Bir uç nokta bağlantı noktası hello aşağıda gösterildiği gibi Alphabet.Processing hizmeti için (Merhaba PackageRoot klasöründe bulunur) ServiceManifest.xml hello uç nokta öğesi ekleyerek Hello hizmet toobe için erişilebilir, açın:
   
    ```xml
    <Endpoint Name="ProcessingServiceEndpoint" Port="8089" Protocol="http" Type="Internal" />
    ```
   
    Artık yapılandırılmış toolisten tooan 26 bölümleri olan dahili uç noktayı hello hizmetidir.
7. Ardından toooverride hello gerekir `CreateServiceReplicaListeners()` hello işleme sınıfının yöntemi.
   
   > [!NOTE]
   > Bu örnek için basit bir HttpCommunicationListener kullandığınızı varsayar. Güvenilir hizmet iletişimi hakkında daha fazla bilgi için bkz: [hello güvenilir hizmet iletişim modelini](service-fabric-reliable-services-communication.md).
   > 
   > 
8. Bir çoğaltma dinlediği hello URL için önerilen bir deseni biçimini izleyen hello olduğu: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.
    Bu nedenle hello doğru uç noktalarda ve bu deseni ile iletişimi dinleyici toolisten tooconfigure istiyor.
   
    Bu hizmetin birden fazla çoğaltma hello üzerinde barındırılabilir aynı bilgisayara nedenle toobe benzersiz toohello çoğaltma bu adresi gerekir. Bölüm kimliği + çoğaltma kimliği hello URL'de olan nedeni budur. HttpListener birden çok adresi hello hello URL öneki benzersiz olduğu sürece aynı bağlantı noktası üzerinde dinleme.
   
    Merhaba fazladan GUID burada ikincil çoğaltmaların salt okunur istekleri için de dinlemek Gelişmiş bir olay yok. Hello durum böyle olduğunda, birincil toosecondary tooforce istemcileri toore Çöz hello adresinden geçiş zaman yeni bir benzersiz adresi kullanıldığından emin toomake istiyorsunuz. '+' hello çoğaltma dinler tüm kullanılabilir konakları (IP, FQDM, localhost, vb.) hello üzerinde aşağıdaki kodu böylece buraya hello adresi bir örnekte gösterildiği gibi kullanılır.
   
    ```CSharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
         return new[] { new ServiceReplicaListener(context => this.CreateInternalListener(context))};
    }
    private ICommunicationListener CreateInternalListener(ServiceContext context)
    {
   
         EndpointResourceDescription internalEndpoint = context.CodePackageActivationContext.GetEndpoint("ProcessingServiceEndpoint");
         string uriPrefix = String.Format(
                "{0}://+:{1}/{2}/{3}-{4}/",
                internalEndpoint.Protocol,
                internalEndpoint.Port,
                context.PartitionId,
                context.ReplicaOrInstanceId,
                Guid.NewGuid());
   
         string nodeIP = FabricRuntime.GetNodeContext().IPAddressOrFQDN;
   
         string uriPublished = uriPrefix.Replace("+", nodeIP);
         return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInternalRequest);
    }
    ```
   
    Bu değer olan bu hello yayımlanan URL belirterek hello dinleme URL önekten biraz farklı.
    Merhaba dinleme URL tooHttpListener verilir. Merhaba yayımlanan yayımlanan toohello Service Fabric adlandırma hizmet bulma için kullanılan hizmeti, olan hello URL'dir. İstemciler, bu bulma hizmeti aracılığıyla bu adres için sorar. Merhaba adresi istemcileri sipariş tooconnect gereksinimlerini toohave hello gerçek IP veya FQDN hello düğümünün alın. Bu nedenle tooreplace gerekir '+' ile düğümün IP veya FQDN yukarıda gösterildiği gibi hello.
9. Merhaba son tooadd hello işleme mantığı toohello hizmeti aşağıda gösterildiği gibi bir adımdır.
   
    ```CSharp
    private async Task ProcessInternalRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        string output = null;
        string user = context.Request.QueryString["lastname"].ToString();
   
        try
        {
            output = await this.AddUserAsync(user);
        }
        catch (Exception ex)
        {
            output = ex.Message;
        }
   
        using (HttpListenerResponse response = context.Response)
        {
            if (output != null)
            {
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    private async Task<string> AddUserAsync(string user)
    {
        IReliableDictionary<String, String> dictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<String, String>>("dictionary");
   
        using (ITransaction tx = this.StateManager.CreateTransaction())
        {
            bool addResult = await dictionary.TryAddAsync(tx, user.ToUpperInvariant(), user);
   
            await tx.CommitAsync();
   
            return String.Format(
                "User {0} {1}",
                user,
                addResult ? "sucessfully added" : "already exists");
        }
    }
    ```
   
    `ProcessInternalRequest`Okuma hello hello sorgu dizesi parametresi kullanılan toocall hello bölümü ve çağrıları değerlerini `AddUserAsync` tooadd hello lastname toohello güvenilir sözlük `dictionary`.
10. Durum bilgisiz hizmet toohello proje toosee ekleyelim belirli bir bölüm nasıl çağırabilirsiniz.
    
    Bu hizmet hello lastname bir sorgu dizesi parametresi olarak kabul eder, hello bölüm anahtarı belirler ve toohello Alphabet.Processing hizmetini işleme gönderen basit bir web arabirimi olarak görev yapar.
11. Merhaba, **bir hizmet oluşturma** iletişim kutusunda, seçin **Stateless** hizmet ve aşağıda gösterildiği gibi "Alphabet.Web" çağırın.
    
    ![Durum bilgisiz hizmet ekran görüntüsü](./media/service-fabric-concepts-partitioning/createnewstateless.png).
12. Merhaba Alphabet.WebApi hizmet tooopen aşağıda gösterildiği gibi bir bağlantı kurmak, hello ServiceManifest.xml Hello uç nokta bilgileri güncelleştirin.
    
    ```xml
    <Endpoint Name="WebApiServiceEndpoint" Protocol="http" Port="8081"/>
    ```
13. Tooreturn koleksiyonunda hello sınıfı Web ServiceInstanceListeners gerekir. Yeniden basit HttpCommunicationListener tooimplement seçebilirsiniz.
    
    ```CSharp
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] {new ServiceInstanceListener(context => this.CreateInputListener(context))};
    }
    private ICommunicationListener CreateInputListener(ServiceContext context)
    {
        // Service instance's URL is hello node's IP & desired port
        EndpointResourceDescription inputEndpoint = context.CodePackageActivationContext.GetEndpoint("WebApiServiceEndpoint")
        string uriPrefix = String.Format("{0}://+:{1}/alphabetpartitions/", inputEndpoint.Protocol, inputEndpoint.Port);
        var uriPublished = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
        return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInputRequest);
    }
    ```
14. Şimdi tooimplement hello işleme mantığı gerekir. HttpCommunicationListener çağrıları hello `ProcessInputRequest` bir isteği ne zaman devreye girer. Bu nedenle devam edelim ve hello aşağıdaki kodu ekleyin.
    
    ```CSharp
    private async Task ProcessInputRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        String output = null;
        try
        {
            string lastname = context.Request.QueryString["lastname"];
            char firstLetterOfLastName = lastname.First();
            ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    
            ResolvedServicePartition partition = await this.servicePartitionResolver.ResolveAsync(alphabetServiceUri, partitionKey, cancelRequest);
            ResolvedServiceEndpoint ep = partition.GetEndpoint();
    
            JObject addresses = JObject.Parse(ep.Address);
            string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
            UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
            primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
            string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    
            output = String.Format(
                    "Result: {0}. <p>Partition key: '{1}' generated from hello first letter '{2}' of input value '{3}'. <br>Processing service partition ID: {4}. <br>Processing service replica address: {5}",
                    result,
                    partitionKey,
                    firstLetterOfLastName,
                    lastname,
                    partition.Info.Id,
                    primaryReplicaAddress);
        }
        catch (Exception ex) { output = ex.Message; }
    
        using (var response = context.Response)
        {
            if (output != null)
            {
                output = output + "added tooPartition: " + primaryReplicaAddress;
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    ```
    
    Şimdi arkasını adım adım yol gösterir. Merhaba kod okur hello ilk harfi hello sorgu dizesi parametresinin `lastname` bir char içine. Ardından, hello on altılık değeri çıkararak bu harfi için hello bölüm anahtarı belirler `A` hello son adları ilk harfi hello onaltılık değerinden.
    
    ```CSharp
    string lastname = context.Request.QueryString["lastname"];
    char firstLetterOfLastName = lastname.First();
    ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    ```
    
    Bu örnekte, 26 bölümler bölüm başına tek bölüm anahtarına sahip kullanıyoruz unutmayın.
    Ardından, biz hello hizmet bölüm elde `partition` hello kullanarak bu anahtar için `ResolveAsync` hello yöntemi `servicePartitionResolver` nesnesi. `servicePartitionResolver`olarak tanımlanır
    
    ```CSharp
    private readonly ServicePartitionResolver servicePartitionResolver = ServicePartitionResolver.GetDefault();
    ```
    
    Merhaba `ResolveAsync` yöntemi alır hello hizmet URI'si, hello bölüm anahtarı ve parametre olarak bir iptal belirteci. Merhaba işleme hizmeti için hizmet URI'si hello `fabric:/AlphabetPartitions/Processing`. Ardından, hello bölüm hello uç noktasını alın.
    
    ```CSharp
    ResolvedServiceEndpoint ep = partition.GetEndpoint()
    ```
    
    Son olarak, biz hello uç nokta URL'si artı hello querystring yapı ve işleme hizmeti hello çağırın.
    
    ```CSharp
    JObject addresses = JObject.Parse(ep.Address);
    string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
    UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
    primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
    string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    ```
    
    Merhaba işleme yaptıktan sonra biz hello çıkış geri yazma.
15. Merhaba son adımı tootest hello hizmetidir. Visual Studio kullanan uygulama parametreleri, yerel ve bulut dağıtımı. tootest hello hizmeti yerel olarak 26 bölümlerle tooupdate hello ihtiyacınız `Local.xml` aşağıda gösterildiği gibi hello ApplicationParameters klasöründe hello AlphabetPartitions proje dosyası:
    
    ```xml
    <Parameters>
      <Parameter Name="Processing_PartitionCount" Value="26" />
      <Parameter Name="WebApi_InstanceCount" Value="1" />
    </Parameters>
    ```
16. Dağıtımını tamamladıktan sonra hello hizmeti ve tüm bölümleri hello Service Fabric Explorer'ın kontrol edebilirsiniz.
    
    ![Service Fabric Explorer ekran görüntüsü](./media/service-fabric-concepts-partitioning/sfxpartitions.png)
17. Bir tarayıcıda girerek mantığı bölümleme hello sınayabilirsiniz `http://localhost:8081/?lastname=somename`. Her son adı ile aynı harf hello depolanıyor hello başlayan olduğunu görürsünüz aynı bölüm.
    
    ![Tarayıcı ekran görüntüsü](./media/service-fabric-concepts-partitioning/samplerunning.png)

Merhaba örnek Hello tüm kaynak kodunun edinilebilir [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).

## <a name="next-steps"></a>Sonraki adımlar
Service Fabric kavramları hakkında daha fazla bilgi için hello aşağıdakilere bakın:

* [Service Fabric hizmetlerin kullanılabilirliğini](service-fabric-availability-services.md)
* [Service Fabric Hizmetleri ölçeklenebilirliği](service-fabric-concepts-scalability.md)
* [Kapasite planlama için Service Fabric uygulamaları](service-fabric-capacity-planning.md)

[wikipartition]: https://en.wikipedia.org/wiki/Partition_(database)

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png