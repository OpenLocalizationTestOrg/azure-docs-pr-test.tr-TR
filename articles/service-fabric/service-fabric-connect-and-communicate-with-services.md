---
title: "aaaConnect ve Azure Service Fabric hizmetleriyle iletişim | Microsoft Docs"
description: "Nasıl tooresolve, bağlanmak ve Service Fabric hizmetleriyle iletişim öğrenin."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: msfussell
ms.assetid: 7d1052ec-2c9f-443d-8b99-b75c97266e6c
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/9/2017
ms.author: vturecek
ms.openlocfilehash: b8b374a71d4c5d21f48a560a3a8c81b357fe418d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-and-communicate-with-services-in-service-fabric"></a>Bağlanma ve Service Fabric Hizmetleri ile iletişim
Service Fabric içinde bir hizmet birden çok VM genellikle dağıtılmış bir Service Fabric kümesindeki herhangi bir yerde çalışır. Bu tek bir yerde tooanother hello hizmet sahibi tarafından ya da otomatik olarak Service Fabric tarafından taşınabilir. Hizmetleri statik olarak bağlı tooa belirli makine veya adresi olmayan.

Service Fabric uygulaması genellikle burada her hizmet özelleştirilmiş bir görev gerçekleştiren birçok farklı hizmetlerden oluşur. Bu hizmetler birbirine tooform ile bir web uygulaması farklı kısımlarını işleme gibi bir tam işlevi iletişim kurabilir. İstemci tooand bağlanan uygulamaları Hizmetleri ile iletişim vardır. Bu belgede ele nasıl tooset ile ve hizmetlerinizi Service Fabric içinde arasında iletişim kurma.

Bu Microsoft Virtual Academy video Ayrıca hizmet iletişimi ele alınmıştır:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=iYFCk76yC_6706218965">  
<img src="./media/service-fabric-connect-and-communicate-with-services/CommunicationVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="bring-your-own-protocol"></a>Kendi Protokolü Getir
Service Fabric, hizmetlerin hello yaşam döngüsünü yönetmenize yardımcı olur, ancak hizmetlerinizi neler hakkında kararlar yapmaz. Bu iletişim içerir. Gelen istekleri için bir uç nokta yukarı hizmetinizin fırsat tooset olduğundan, Service Fabric tarafından hizmetiniz açıldığında ne olursa olsun protokolü veya iletişim yığını kullanarak istediğiniz. Hizmetinizi normal üzerinde dinler **IP: BağlantıNoktası** bir URI gibi herhangi bir adres düzeni kullanarak adres. Birden fazla hizmet örneği veya çoğaltmaları bir ana bilgisayar işlemi, bu durumda bunlar toouse farklı bağlantı noktaları gerekir veya Windows hello http.sys çekirdek sürücüsü gibi bir bağlantı noktası paylaşma mekanizması kullanmak paylaşabilir. Her iki durumda da, her bir hizmet örneği veya bir ana bilgisayar işlemi yinelemede benzersiz olarak adreslenebilir olmalıdır.

![Hizmet uç noktaları][1]

## <a name="service-discovery-and-resolution"></a>Hizmet bulma ve çözümleme
Dağıtılmış bir sistemde Hizmetleri zaman içinde bir makine tooanother taşıyabilir. Bu kaynak Dengeleme, yükseltmeler, yük devretme veya genişleme dahil olmak üzere çeşitli nedenlerden kaynaklanabilir. Bu, hello hizmet toonodes farklı IP adresleriyle taşır ve hello hizmet dinamik olarak seçilen bağlantı noktası kullanıyorsa farklı bağlantı noktalarını açmanız hizmeti bitiş noktası adreslerini değiştirmek anlamına gelir.

![Hizmetlerinin dağıtımı][7]

Service Fabric adlandırma hizmeti bulma ve hizmeti adlı çözüm hello sağlar. Merhaba adlandırma hizmeti eşleyen bir tablo hizmet örneği üzerinde dinleme toohello uç nokta adresleri adlı tutar. Service Fabric tüm adlandırılmış hizmet örnekleri olarak URI'ler, örneğin temsil benzersiz adlara sahip `"fabric:/MyApplication/MyService"`. Merhaba hello hizmetin adını hello hizmet hello ömrü boyunca değiştirmez, hizmetleri taşıdığınızda, değiştirebileceğiniz hello uç nokta adresleri. Sabit URL'leri sahip ancak başlangıç IP adresi burada değişebilir benzer toowebsites budur. Ve Web sitesi URL'leri tooIP adresleri çözümler, hello Web'de benzer tooDNS Service Fabric hizmeti adları tootheir uç noktası adresi eşleşen bir kayıt sahiptir.

![Hizmet uç noktaları][2]

Çözümleme ve tooservices bağlanan bir döngüde çalıştırılacak adımları izleyerek hello içerir:

* **Gidermek**: bir hizmet yayımlandığı Get hello uç nokta hello adlandırma hizmeti.
* **Connect**: ne olursa olsun, bu uç noktada kullandığı protokol üzerinden toohello hizmetine bağlanın.
* **Yeniden deneme**: herhangi bir sayıda nedenlerle hello son zaman hello uç noktası adresi çözümlenmiş başlatıldığından beri hello hizmet taşınmışsa örnek için bir bağlantı girişimi başarısız olabilir. Bu durumda çözümleme önceki hello ve bağlanma adımları ihtiyacınız denenen toobe ve hello bağlantı başarılı olana kadar bu döngü yinelenir.

## <a name="connecting-tooother-services"></a>Tooother Hizmetleri bağlanma
Bir kümedeki Hello düğümler üzerinde hello olduğundan tooeach bağlanma Hizmetleri başka bir küme içindeki genellikle doğrudan diğer hizmetlerin hello uç noktaları erişebilirsiniz aynı yerel ağ. toomake hizmetleri arasında daha kolay tooconnect, Service Fabric adlandırma hizmeti kullanan ek hizmetleri hello sağlar. DNS hizmeti ve bir ters proxy hizmeti.


### <a name="dns-service"></a>DNS hizmeti
Birçok hizmetler, özellikle kapsayıcılı hizmetler var olan bir URL adı olduğundan mümkün tooresolve olan bu hello standart DNS Protokolü (Merhaba adlandırma hizmeti Protokolü) yerine çok kullanışlı bir yoldur, özellikle uygulamada "kaldırın ve shift" senaryoları. Bu, tam olarak hangi hello DNS hizmeti yapar olur. Toomap DNS adları tooa hizmet adı sağlar ve bu nedenle uç noktası IP adresi çözümlenemiyor. 

Gösterildiği hello Aşağıdaki diyagramda, hello hello Service Fabric kümede çalışan DNS hizmeti, ardından hello adlandırma hizmeti tooreturn hello bitiş noktası adreslerini tooconnect için tarafından çözümlenen DNS adlarını tooservice adlarını eşler. Merhaba hizmeti için Hello DNS ad hello oluşturma sırasında sağlanır. 

![Hizmet uç noktaları][9]

Toouse hello DNS hizmeti nasıl görürüm hakkında daha fazla ayrıntı için [Azure Service Fabric DNS hizmetinde](service-fabric-dnsservice.md) makalesi.

### <a name="reverse-proxy-service"></a>Ters proxy hizmeti
Hello ters proxy services HTTP uç noktaları HTTPS dahil olmak üzere sunan hello kümedeki giderir. diğer hizmetler çağırma Hello ters proxy büyük ölçüde basitleştirir ve belirli bir sahip yöntemleriyle URI biçimlendirmek ve hello gidermek, tanıtıcıları bağlanma, başka bir kullanarak bir hizmet toocommunicate için gerekli yeniden deneme adımları adlandırma hizmeti hello. Diğer bir deyişle, diğer hizmetler bu URL çağrılması kadar basit hale getirerek çağrılırken Merhaba, adlandırma hizmetinden gizler.

![Hizmet uç noktaları][10]

Nasıl toouse hello ters proxy hizmeti hakkında daha fazla bilgi için bkz [ters proxy Azure Service Fabric](service-fabric-reverseproxy.md) makalesi.

## <a name="connections-from-external-clients"></a>Dış istemcilerden gelen bağlantıları
Bir kümedeki Hello düğümler üzerinde hello olduğundan tooeach bağlanma Hizmetleri başka bir küme içindeki genellikle doğrudan diğer hizmetlerin hello uç noktaları erişebilirsiniz aynı yerel ağ. Bazı ortamlarda, sınırlı bir dizi bağlantı noktası üzerinden harici giriş trafiğini yönlendiren bir yük dengeleyicinin arkasındaki bir küme ancak olabilir. Bu durumlarda, hizmetleri yine birbirleri ile iletişim kurmak ve adlandırma hizmeti kullanarak bir adres hello ancak ek adımlar çekildiği tooallow dış istemcilere tooconnect tooservices olmalıdır çözmek.

## <a name="service-fabric-in-azure"></a>Azure Service Fabric
Azure Service Fabric kümesi bir Azure yük dengeleyici yer alır. Tüm dış trafiğin toohello küme hello yük dengeleyici üzerinden geçmesi gerekir. Merhaba yük dengeleyici otomatik olarak trafik iletir rastgele bir verilen bağlantı noktası tooa gelen trafik *düğümü* aynı bağlantı noktasını açın hello sahiptir. Hello Azure yük dengeleyici yalnızca hello üzerinde açık bağlantı noktalarını bildiği *düğümleri*, bağlantı noktalarının açık kişi tarafından hakkında bilmez *Hizmetleri*.

![Azure yük dengeleyici ve Service Fabric topolojisi][3]

Örneğin, sipariş tooaccept bağlantı noktasındaki dış trafiğini içinde **80**, şeyler aşağıdaki hello yapılandırılmış olması gerekir:

1. Bağlantı noktası 80 üzerinde dinleyen bir hizmet yazma. Bağlantı noktası 80'hello hizmetin ServiceManifest.xml yapılandırmak ve bir dinleyici hello hizmetinde, örneğin, bir kendi kendini barındıran web sunucusu açın.

    ```xml
    <Resources>
        <Endpoints>
            <Endpoint Name="WebEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>
    ```
    ```csharp
        class HttpCommunicationListener : ICommunicationListener
        {
            ...

            public Task<string> OpenAsync(CancellationToken cancellationToken)
            {
                EndpointResourceDescription endpoint =
                    serviceContext.CodePackageActivationContext.GetEndpoint("WebEndpoint");

                string uriPrefix = $"{endpoint.Protocol}://+:{endpoint.Port}/myapp/";

                this.httpListener = new HttpListener();
                this.httpListener.Prefixes.Add(uriPrefix);
                this.httpListener.Start();

                string publishUri = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
                return Task.FromResult(publishUri);
            }

            ...
        }

        class WebService : StatelessService
        {
            ...

            protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
            {
                return new[] { new ServiceInstanceListener(context => new HttpCommunicationListener(context))};
            }

            ...
        }
    ```
    ```java
        class HttpCommunicationlistener implements CommunicationListener {
            ...

            @Override
            public CompletableFuture<String> openAsync(CancellationToken arg0) {
                EndpointResourceDescription endpoint =
                    this.serviceContext.getCodePackageActivationContext().getEndpoint("WebEndpoint");
                try {
                    HttpServer server = com.sun.net.httpserver.HttpServer.create(new InetSocketAddress(endpoint.getPort()), 0);
                    server.start();

                    String publishUri = String.format("http://%s:%d/",
                        this.serviceContext.getNodeContext().getIpAddressOrFQDN(), endpoint.getPort());
                    return CompletableFuture.completedFuture(publishUri);
                } catch (IOException e) {
                    throw new RuntimeException(e);
                }
            }

            ...
        }

        class WebService extends StatelessService {
            ...

            @Override
            protected List<ServiceInstanceListener> createServiceInstanceListeners() {
                <ServiceInstanceListener> listeners = new ArrayList<ServiceInstanceListener>();
                listeners.add(new ServiceInstanceListener((context) -> new HttpCommunicationlistener(context)));
                return listeners;       
            }

            ...
        }
    ```
2. Service Fabric kümesi oluşturma ve bağlantı noktasını belirtin **80** hello hizmetini barındıran hello düğüm türü için bir özel uç nokta bağlantı noktası olarak. Birden fazla düğüm türü varsa, ayarlayabileceğiniz bir *yerleştirme kısıtlaması* hello özel uç noktası portunu sahip hello düğüm türünde yalnızca çalıştırdığı hello hizmet tooensure üzerinde.

    ![Düğüm türü bir bağlantı noktası açın][4]
3. Merhaba Küme oluşturulduktan sonra hello Azure yük dengeleyici hello küme kaynak grubu tooforward trafiği 80 numaralı bağlantı noktasında yapılandırın. Hello Azure portal aracılığıyla bir küme oluştururken, bu otomatik olarak yapılandırılan her özel uç nokta bağlantı noktası için ayarlanır.

    ![Hello Azure yük dengeleyici trafiği ilet][5]
4. Azure yük dengeleyici kullanan bir araştırma toodetermine olup hello veya değil toosend trafiği tooa belirli düğüm. Merhaba araştırma düzenli aralıklarla denetimleri hello düğümü yanıt vermeyen her düğüm toodetermine üzerinde bir uç nokta. Hello araştırma tooreceive yanıt yapılandırılmış birkaç kez sonra başarısız olursa, trafiğin toothat düğümü gönderme hello yük dengeleyici durdurur. Hello Azure portal aracılığıyla bir küme oluştururken, bir yoklama yapılandırılmış her özel uç nokta bağlantı noktası için otomatik olarak ayarlanır.

    ![Hello Azure yük dengeleyici trafiği ilet][8]

Hello Azure yük dengeleyici ve hello araştırma hakkında hello yalnızca bildiğiniz önemli tooremember olan *düğümleri*, değil hello *Hizmetleri* hello düğümlerinde çalışıyor. Hello Azure yük dengeleyici her zaman toohello araştırma yanıt trafiği toonodes gönderir, dikkatli olunması gerekir böylece tooensure Hizmetleri mümkün toorespond toohello araştırma olan hello düğümlerinde kullanılabilir.

## <a name="reliable-services-built-in-communication-api-options"></a>Güvenilir hizmetler: Yerleşik iletişim API seçenekleri
Merhaba Reliable Services framework birkaç önceden derlenmiş iletişim seçenekleri ile birlikte gelir. programlama modeli, hello iletişimi framework ve hizmetlerinizi yazılan dil programlama hello hello hello seçimine hakkında bir en iyi işinize hello karar bağlıdır.

* **Belirli bir protokol:** iletişim framework'ün belirli bir seçim yok ancak tooget bir şey yukarı ve çalışan hızla istediğiniz durumunda hello ideal seçenek sizin için [hizmet remoting](service-fabric-reliable-services-communication-remoting.md), veren Reliable Services ve Reliable Actors için kesin tür belirtilmiş uzak yordam çağrıları. Bu hello kolay ve hızlı şekilde tooget hizmet iletişimi ile başlatıldı. Hizmet remoting service adresleri, bağlantı, yeniden deneyin ve hata işleme çözünürlüğü işler. Bu, hem C# ve Java uygulamaları için kullanılabilir.
* **HTTP**: dilden bağımsız iletişim için HTTP bir endüstri standardı seçim araçları ve HTTP sunucularıyla birçok farklı dillerde, Service Fabric tarafından desteklenen tüm kullanılabilir sağlar. Hizmetleri dahil olmak üzere, kullanılabilir tüm HTTP yığınını kullanma [ASP.NET Web API](service-fabric-reliable-services-communication-webapi.md) C# uygulamaları için. C# ile yazılmış istemcileri hello yararlanabilir `ICommunicationClient` ve `ServicePartitionClient` , ancak sınıfları Java için hello kullan `CommunicationClient` ve `FabricServicePartitionClient` sınıfları [hizmet çözümleme, HTTP bağlantılarını ve yeniden deneme döngüsü](service-fabric-reliable-services-communication.md).
* **WCF**: WCF iletişimi çerçeve olarak kullanan var olan kodu olması durumunda hello kullanabilirsiniz `WcfCommunicationListener` hello sunucu tarafı için ve `WcfCommunicationClient` ve `ServicePartitionClient` hello istemci sınıfları. Bu ancak yalnızca Windows tabanlı kümelerde C# uygulamaları için kullanılabilir. Bu makalede daha fazla ayrıntı için bkz: [WCF tabanlı bir uygulama hello iletişimi yığınının](service-fabric-reliable-services-communication-wcf.md).

## <a name="using-custom-protocols-and-other-communication-frameworks"></a>Özel protokoller ve diğer iletişim çerçeveleri kullanma
Hizmetleri kullanma herhangi bir protokolü veya framework iletişimi için özel bir ikili protokol TCP yuvaları ya da aracılığıyla akış olaylarını üzerinden olup olmadığını [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) veya [Azure IOT Hub](https://azure.microsoft.com/services/iot-hub/). Service Fabric iletişimi tüm hello toodiscover çalışma ve bağlanmak, iletişim yığını, Tak API'leri sizden soyutlanır sağlar. Bu makalede hello hakkında bkz [güvenilir hizmet iletişim modelini](service-fabric-reliable-services-communication.md) daha fazla ayrıntı için.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba kavramları ve hello kullanılabilir API'ler hakkında daha fazla bilgi edinmek [Reliable Services iletişim modelini](service-fabric-reliable-services-communication.md), sonra hızlı şekilde kullanmaya başlamanızı [hizmet remoting](service-fabric-reliable-services-communication-remoting.md) veya ayrıntılı toolearn nasıl gidin toowrite bir kullanarak iletişim dinleyici [OWIN kendini barındırma ile Web API](service-fabric-reliable-services-communication-webapi.md).

[1]: ./media/service-fabric-connect-and-communicate-with-services/serviceendpoints.png
[2]: ./media/service-fabric-connect-and-communicate-with-services/namingservice.png
[3]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancertopology.png
[4]: ./media/service-fabric-connect-and-communicate-with-services/nodeport.png
[5]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerport.png
[7]: ./media/service-fabric-connect-and-communicate-with-services/distributedservices.png
[8]: ./media/service-fabric-connect-and-communicate-with-services/loadbalancerprobe.png
[9]: ./media/service-fabric-connect-and-communicate-with-services/dns.png
[10]: ./media/service-fabric-reverseproxy/internal-communication.png
