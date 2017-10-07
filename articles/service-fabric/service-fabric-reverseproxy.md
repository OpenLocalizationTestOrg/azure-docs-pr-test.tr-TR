---
title: Service Fabric aaaAzure ters proxy | Microsoft Docs
description: "İç ve dış hello küme iletişimi toomicroservices için Service Fabric'ın ters proxy kullanın."
services: service-fabric
documentationcenter: .net
author: BharatNarasimman
manager: timlt
editor: vturecek
ms.assetid: 47f5c1c1-8fc8-4b80-a081-bc308f3655d3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/08/2017
ms.author: bharatn
ms.openlocfilehash: 0e7835a64ccd74293c7bdd8b41deae414c83dffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reverse-proxy-in-azure-service-fabric"></a>Azure Service Fabric ters proxy
Azure Service Fabric yerleşik hello ters proxy HTTP uç noktaları gösteren hello Service Fabric kümesindeki mikro giderir.

## <a name="microservices-communication-model"></a>Mikro iletişim modelini
Service Fabric mikro genellikle bir alt hello kümedeki sanal makinelerin çalışır ve bir sanal makine tooanother çeşitli nedenlerle taşıyabilirsiniz. Bu nedenle, hello uç noktaları mikro için dinamik olarak değiştirebilirsiniz. Merhaba tipik bir düzen toocommunicate toohello mikro hello aşağıdaki döngüsü çözmek şöyledir:

1. Başlangıçta hello adlandırma hizmeti aracılığıyla Hello hizmet konumu çözümleyin.
2. Toohello hizmetine bağlanın.
3. Bağlantı hataları Hello nedenini ve gerektiğinde Merhaba hizmet konumu yeniden çözümleyin.

Bu işlem genellikle hello hizmeti çözümleme ve Yeniden Dene'yi ilkeleri uygulayan bir yeniden deneme döngüsüne istemci-tarafı iletişim kitaplıklarında kaydırma içerir.
Daha fazla bilgi için bkz: [Bağlan ve Hizmetleri ile iletişim](service-fabric-connect-and-communicate-with-services.md).

### <a name="communicating-by-using-hello-reverse-proxy"></a>Merhaba ters proxy kullanarak iletişim
Merhaba kümedeki tüm hello düğümlere Hello ters proxy Service Fabric içinde çalışır. Bir istemcinin adına hello tüm hizmet çözümleme işlemi gerçekleştirir ve hello istemci isteğini iletir. Bu nedenle, hello kümede çalışan istemciler, yerel olarak çalışır aynı düğümde hello hello ters Ara sunucu kullanarak tüm istemci-tarafı HTTP iletişim kitaplıkları tootalk toohello hedef hizmetini kullanabilirsiniz.

![İç iletişim][1]

## <a name="reaching-microservices-from-outside-hello-cluster"></a>Dış hello kümeden mikro ulaşmasını
Merhaba varsayılan dış iletişim modelini mikro için burada her hizmetin doğrudan dış istemcilerden erişilemez bir katılımı modelidir. [Azure yük dengeleyici](../load-balancer/load-balancer-overview.md), mikro dış istemcileri arasındaki bir ağ sınırında olduğu ağ adresi çevirisi gerçekleştirir ve ileten dış toointernal IP: BağlantıNoktası uç noktaları ister. toomake mikro 's uç noktası doğrudan erişilebilir tooexternal istemciler, önce hizmet hello tooforward trafiği tooeach bağlantı noktası kullanan yük dengeleyici hello kümede yapılandırmanız gerekir. Ayrıca, çoğu mikro, özellikle durum bilgisi olan mikro hello kümenin tüm düğümlerinde dinamik yok. Merhaba mikro yük devretme düğümlerinde arasında taşıyabilirsiniz. Böyle durumlarda, yük dengeleyici etkili bir şekilde hello konumu belirlenemiyor hello çoğaltmaları toowhich, hedef düğümü hello trafiği iletmek.

### <a name="reaching-microservices-via-hello-reverse-proxy-from-outside-hello-cluster"></a>Dış hello kümeden hello ters proxy aracılığıyla mikro ulaşmasını
Yük dengeleyicisi bir bireysel hizmet başlangıç bağlantı noktası yapılandırmak yerine, yalnızca hello ters proxy hello bağlantı yük dengeleyici yapılandırabilirsiniz. Bu yapılandırma hello küme dışındaki istemcilerin hello ters proxy ek yapılandırma olmadan kullanarak hello küme içindeki hizmetlere erişmek sağlar.

![Dış iletişimi][0]

> [!WARNING]
> Yük dengeleyicisi hello ters proxy'nın bağlantı noktası yapılandırdığınızda, bir HTTP uç noktası kullanıma hello kümedeki tüm mikro hello küme dışında adreslenebilir.
>
>


## <a name="uri-format-for-addressing-services-by-using-hello-reverse-proxy"></a>Merhaba ters proxy kullanarak Hizmetleri adresleme için URI biçimi
belirli bir Tekdüzen Kaynak Tanımlayıcısı (URI) biçimi tooidentify hello hizmet bölüm toowhich hello gelen isteği iletilmesi gereken hello ters proxy kullanır:

```
http(s)://<Cluster FQDN | internal IP>:Port/<ServiceInstanceName>/<Suffix path>?PartitionKey=<key>&PartitionKind=<partitionkind>&ListenerName=<listenerName>&TargetReplicaSelector=<targetReplicaSelector>&Timeout=<timeout_in_seconds>
```

* **http (s):** hello ters proxy yapılandırılmış tooaccept HTTP veya HTTPS trafiği olabilir. HTTPS iletme için çok başvuran[tooa güvenli service hello ters proxy ile bağlanma](service-fabric-reverseproxy-configure-secure-communication.md) HTTPS üzerinde ters proxy Kurulum toolisten sahip olduğunda.
* **Küme tam etki alanı adı (FQDN) | iç IP:** dış istemcileri için böylece mycluster.eastus.cloudapp.azure.com gibi hello küme etki üzerinden erişilebilen hello ters proxy yapılandırabilirsiniz. Varsayılan olarak, hello ters proxy her düğüm üzerinde çalışır. İç trafiği için hello ters proxy 10.0.0.1 gibi herhangi bir iç düğüm IP'yi veya localhost üzerinde erişilebilir.
* **Bağlantı noktası:** hello ters proxy için belirtilen hello gibi bağlantı noktası 19081, budur.
* **ServiceInstanceName:** bu hello tam hello olmadan tooreach çalıştığınız dağıtılan hello hizmet örneği adıdır "fabric: /" düzeni. Örneğin, tooreach hello *fabric: / myapp/myservice/* hizmeti, kullandığınız *myapp/myservice*.

    Merhaba hizmet örneği adı büyük/küçük harf duyarlıdır. Merhaba URL'deki hello hizmet örneği adı için farklı büyük/küçük harf kullanarak hello istekleri toofail 404 ile (bulunamadı) neden olur.
* **Sonek yol:** hello gerçek URL yolu gibi budur *myapi/değerleri/ekleme/3*, tooconnect için istediğiniz hello hizmeti.
* **PartitionKey:** bölümlenmiş bir hizmet için bu hello hesaplanan bölüm tooreach istediğiniz hello bölümünün anahtarıdır. Bu Not *değil* bölüm kimliği GUID hello. Bu parametre hello tek bölüm düzeni kullanan Hizmetleri için gerekli değildir.
* **PartitionKind:** hello hizmet bölüm düzeni budur. Bu, 'Int64Range' veya 'Adlı' olabilir. Bu parametre hello tek bölüm düzeni kullanan Hizmetleri için gerekli değildir.
* **ListenerName** hello hello hizmetinden noktalarıdır hello biçimi {"Bitiş": {"Listener1": "Bitiş noktası 1", "Listener2": "Endpoint2"...}}. Birden çok uç nokta Hello hizmet sunan olduğunda bu hello endpoint tanımlar için o hello istemci isteği iletilir. Merhaba hizmet yalnızca bir dinleyici varsa bu atlanabilir.
* **TargetReplicaSelector** bu hello hedef çoğaltma veya örnek nasıl seçilen belirtir.
  * Merhaba hedef hizmet durum bilgisi olan olduğunda hello TargetReplicaSelector hello aşağıdakilerden biri olabilir: 'PrimaryReplica', 'RandomSecondaryReplica' veya 'RandomReplica'. Bu parametre belirtilmediğinde hello 'PrimaryReplica' varsayılandır.
  * Merhaba hedef hizmet durum bilgisiz olduğunda ters proxy hello hizmet bölüm tooforward hello isteği için rastgele bir örneğini seçer.
* **Zaman aşımı:** bu hello istemci isteği adına hello ters proxy toohello hizmeti tarafından oluşturulan hello HTTP isteği için hello zaman aşımını belirtir. Merhaba varsayılan değer 60 saniyedir. Bu isteğe bağlı bir parametredir.

### <a name="example-usage"></a>Örnek Kullanım
Örnek olarak, hello atalım *fabric: / MyApp/MyService* URL aşağıdaki hello üzerinde bir HTTP dinleyicisi açar hizmeti:

```
http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/
```

Merhaba hizmet için hello kaynağı şunlardır:

* `/index.html`
* `/api/users/<userId>`

Merhaba hizmetini bölümleme hello singleton kullanıyorsa, hello *PartitionKey* ve *PartitionKind* sorgu dizesi parametreleri gerekli değildir ve hello hizmeti hello ağ geçidi olarak kullanarak üst sınırına:

* Harici olarak:`http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService`
* Dahili olarak:`http://localhost:19081/MyApp/MyService`

Merhaba hizmetini bölümleme hello Tekdüzen Int64 kullanıyorsa, hello *PartitionKey* ve *PartitionKind* sorgu dizesi parametreleri kullanılan tooreach hello hizmetinin bir bölüm olması gerekir:

* Harici olarak:`http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`
* Dahili olarak:`http://localhost:19081/MyApp/MyService?PartitionKey=3&PartitionKind=Int64Range`

Merhaba hizmet sunan, tooreach hello kaynakları yalnızca yerleştirin hello kaynak yolu hello hizmet adı hello URL'de sonra:

* Harici olarak:`http://mycluster.eastus.cloudapp.azure.com:19081/MyApp/MyService/index.html?PartitionKey=3&PartitionKind=Int64Range`
* Dahili olarak:`http://localhost:19081/MyApp/MyService/api/users/6?PartitionKey=3&PartitionKind=Int64Range`

Merhaba ağ geçidi, ardından bu istekleri toohello hizmetin URL iletir:

* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/index.html`
* `http://10.0.0.5:10592/3f0d39ad-924b-4233-b4a7-02617c6308a6-130834621071472715/api/users/6`

## <a name="special-handling-for-port-sharing-services"></a>Bağlantı noktası paylaşımı için bir özel işleme Hizmetleri
Azure uygulama ağ geçidi hizmet yeniden adresi ve bir hizmet erişildiğinde hello isteği yeniden deneyin tooresolve çalışır. İstemci kodu değil tooimplement kendi hizmet çözümlemesi gerekir ve döngüsü çözmek uygulama ağ geçidi önemli bir avantajı olmasıdır.

Genellikle, bir hizmetine ulaşılamıyor zaman hello hizmet örneği veya çoğaltma farklı bir düğüme tooa normal yaşam döngüsünün parçası olarak taşındı. Bu gerçekleştiğinde, ağ bağlantısı hatası bir uç nokta hello üzerinde daha uzun hiçbir açık adres başlangıçta çözülmüş olduğunu belirten bir uygulama ağ geçidi alabilirsiniz.

Ancak, çoğaltmalar veya hizmet örneklerinin bir ana bilgisayar işlemi paylaşabilir ve ayrıca bir http.sys tabanlı bir web sunucusu tarafından barındırılan bir bağlantı noktası paylaşabilen dahil olmak üzere:

* [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener%28v=vs.110%29.aspx)
* [ASP.NET Core WebListener](https://docs.asp.net/latest/fundamentals/servers.html#weblistener)
* [Katana](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.OwinSelfHost/)

Bu durumda, hello ana bilgisayar işlemi ve toorequests ancak hello hizmet örneği çözümlenmiş ya da çoğaltma artık hello ana bilgisayarda kullanılabilir yanıt hello web sunucusu kullanılabilir olasıdır. Bu durumda, hello ağ geçidi hello web sunucusundan bir HTTP 404 yanıtı alırsınız. Bu nedenle, bir HTTP 404 iki ayrı anlama gelir:

- Durum #1: hello hizmet adresinin doğru olduğundan, ancak istenen kullanıcı hello hello kaynak yok.
- Durum #2: hello hizmeti adresi yanlış ve istenen kullanıcı hello hello kaynak farklı bir kümede mevcut.

Merhaba ilk olarak bir normal HTTP kullanıcı hata olarak kabul edilen 404, olur. Ancak, hello ikinci durumda, mevcut bir kaynak hello kullanıcı istedi. Uygulama ağ geçidi hello hizmet çünkü kendisine taşındı oluşturulamıyor toolocate oluştu. Uygulama ağ geçidi gereksinimlerini tooresolve hello adresi yeniden ve yeniden deneme hello isteği.

Uygulama ağ geçidi, bu nedenle bu iki çalışmaları arasında bir şekilde toodistinguish gerekir. toomake ayrım, bir ipucu hello sunucusundan gerekli olur.

* Varsayılan olarak, uygulama ağ geçidi örneği #2 varsayar ve hello istek tooresolve ve sorunu yeniden dener.
* tooindicate durum #1 tooApplication ağ geçidi, bir HTTP yanıt üstbilgisi aşağıdaki hello hello hizmet döndürmesi gerekir:

  `X-ServiceFabric : ResourceNotFound`

Bu bir HTTP yanıt üstbilgisi hangi hello istenen kaynak yok normal bir HTTP 404 durumu gösterir ve uygulama ağ geçidi tooresolve hello hizmeti adresi yeniden denemez.

## <a name="setup-and-configuration"></a>Kurulum ve yapılandırma

### <a name="enable-reverse-proxy-via-azure-portal"></a>Azure Portalı aracılığıyla ters proxy etkinleştir

Azure portalı, yeni bir Service Fabric kümesi oluşturulurken bir seçenek tooenable ters proxy sağlar.
Altında **oluşturma Service Fabric kümesi**, adım 2: küme yapılandırması, düğüm türü yapılandırması hello onay kutusu çok seçin "Etkinleştirme ters proxy".
Güvenli ters proxy yapılandırmak için SSL sertifikası adım 3'te belirtilebilir: güvenlik, küme güvenlik ayarlarını yapılandırma, select hello onay kutusu çok "ters proxy için bir SSL sertifikası Ekle" ve hello sertifika ayrıntılarını girin.

### <a name="enable-reverse-proxy-via-azure-resource-manager-templates"></a>Ters proxy aracılığıyla Azure Resource Manager şablonları etkinleştir

Merhaba kullanabilirsiniz [Azure Resource Manager şablonu](service-fabric-cluster-creation-via-arm.md) tooenable hello için ters proxy hizmeti yapıda hello küme.

Çok başvuran[HTTPS Ters Proxy Yapılandırma güvenli bir kümede](https://github.com/ChackDan/Service-Fabric/tree/master/ARM Templates/ReverseProxySecureSample#configure-https-reverse-proxy-in-a-secure-cluster) için Azure Resource Manager şablonu güvenli ters proxy bir sertifika ve işleme sertifika rollover tooconfigure örnekleri.

İlk olarak, toodeploy istediğiniz hello küme için hello Şablon Al. Merhaba örnek şablonları kullanabilir veya özel bir Resource Manager şablonu oluşturun. Ardından, aşağıdaki adımları hello kullanarak hello ters proxy etkinleştirebilirsiniz:

1. Merhaba ters proxy için bir bağlantı noktası hello tanımlamak [parametreleri bölümüne](../azure-resource-manager/resource-group-authoring-templates.md) hello şablonunun.

    ```json
    "SFReverseProxyPort": {
        "type": "int",
        "defaultValue": 19081,
        "metadata": {
            "description": "Endpoint for Service Fabric Reverse proxy"
        }
    },
    ```
2. Her hello nodetype nesnelerin hello Hello bağlantı noktasını belirtin **küme** [kaynak türü bölümü](../azure-resource-manager/resource-group-authoring-templates.md).

    başlangıç bağlantı noktası hello parametre adı reverseProxyEndpointPort tanımlanır.

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        ...
       "nodeTypes": [
          {
           ...
           "reverseProxyEndpointPort": "[parameters('SFReverseProxyPort')]",
           ...
          },
        ...
        ],
        ...
    }
    ```
3. 1. adımda belirttiğiniz başlangıç bağlantı noktası için hello Azure yük dengeleyici kuralları ayarlama dış hello Azure küme gelen tooaddress hello ters proxy.

    ```json
    {
        "apiVersion": "[variables('lbApiVersion')]",
        "type": "Microsoft.Network/loadBalancers",
        ...
        ...
        "loadBalancingRules": [
            ...
            {
                "name": "LBSFReverseProxyRule",
                "properties": {
                    "backendAddressPool": {
                        "id": "[variables('lbPoolID0')]"
                    },
                    "backendPort": "[parameters('SFReverseProxyPort')]",
                    "enableFloatingIP": "false",
                    "frontendIPConfiguration": {
                        "id": "[variables('lbIPConfig0')]"
                    },
                    "frontendPort": "[parameters('SFReverseProxyPort')]",
                    "idleTimeoutInMinutes": "5",
                    "probe": {
                        "id": "[concat(variables('lbID0'),'/probes/SFReverseProxyProbe')]"
                    },
                    "protocol": "tcp"
                }
            }
        ],
        "probes": [
            ...
            {
                "name": "SFReverseProxyProbe",
                "properties": {
                    "intervalInSeconds": 5,
                    "numberOfProbes": 2,
                    "port":     "[parameters('SFReverseProxyPort')]",
                    "protocol": "tcp"
                }
            }  
        ]
    }
    ```
4. Merhaba ters proxy hello bağlantı noktasında tooconfigure SSL sertifikaları Ekle hello sertifika toohello ***reverseProxyCertificate*** hello özelliğinde **küme** [kaynak türü bölümü](../resource-group-authoring-templates.md).

    ```json
    {
        "apiVersion": "2016-09-01",
        "type": "Microsoft.ServiceFabric/clusters",
        "name": "[parameters('clusterName')]",
        "location": "[parameters('clusterLocation')]",
        "dependsOn": [
            "[concat('Microsoft.Storage/storageAccounts/', parameters('supportLogStorageAccountName'))]"
        ],
        "properties": {
            ...
            "reverseProxyCertificate": {
                "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                "x509StoreName": "[parameters('sfReverseProxyCertificateStoreName')]"
            },
            ...
            "clusterState": "Default",
        }
    }
    ```

### <a name="supporting-a-reverse-proxy-certificate-thats-different-from-hello-cluster-certificate"></a>Merhaba küme sertifikadan farklı bir ters proxy sertifikası destekleme
 Merhaba ters proxy sertifika hello küme korur hello sertifikasından farklıysa, ardından hello daha önce sertifika hello sanal makineye yüklenmesi ve böylece Service Fabric toohello erişim denetim listesi (ACL) eklenen belirtilen erişim. Bu hello yapılabilir **virtualMachineScaleSets** [kaynak türü bölümü](../resource-group-authoring-templates.md). Yükleme için bu sertifika toohello osProfile ekleyin. Merhaba uzantısı hello şablon bölümünü hello ACL hello sertifikada güncelleştirebilirsiniz.

  ```json
  {
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Compute/virtualMachineScaleSets",
    ....
      "osProfile": {
          "adminPassword": "[parameters('adminPassword')]",
          "adminUsername": "[parameters('adminUsername')]",
          "computernamePrefix": "[parameters('vmNodeType0Name')]",
          "secrets": [
            {
              "sourceVault": {
                "id": "[parameters('sfReverseProxySourceVaultValue')]"
              },
              "vaultCertificates": [
                {
                  "certificateStore": "[parameters('sfReverseProxyCertificateStoreValue')]",
                  "certificateUrl": "[parameters('sfReverseProxyCertificateUrlValue')]"
                }
              ]
            }
          ]
        }
   ....
   "extensions": [
          {
              "name": "[concat(parameters('vmNodeType0Name'),'_ServiceFabricNode')]",
              "properties": {
                      "type": "ServiceFabricNode",
                      "autoUpgradeMinorVersion": false,
                      ...
                      "publisher": "Microsoft.Azure.ServiceFabric",
                      "settings": {
                        "clusterEndpoint": "[reference(parameters('clusterName')).clusterEndpoint]",
                        "nodeTypeRef": "[parameters('vmNodeType0Name')]",
                        "dataPath": "D:\\\\SvcFab",
                        "durabilityLevel": "Bronze",
                        "testExtension": true,
                        "reverseProxyCertificate": {
                          "thumbprint": "[parameters('sfReverseProxyCertificateThumbprint')]",
                          "x509StoreName": "[parameters('sfReverseProxyCertificateStoreValue')]"
                        },
                  },
                  "typeHandlerVersion": "1.0"
              }
          },
      ]
    }
  ```
> [!NOTE]
> Merhaba küme sertifika tooenable hello ters proxy var olan bir kümede farklı sertifikaları kullandığınızda, hello ters proxy sertifikası yükleyin ve hello ters proxy etkinleştirmeden önce hello ACL hello kümede güncelleştirin. Tam hello [Azure Resource Manager şablonu](service-fabric-cluster-creation-via-arm.md) bahsedilen hello ayarlarını kullanarak dağıtım daha önce bir dağıtım tooenable hello ters proxy başlamadan önce adımları 1-4.

## <a name="next-steps"></a>Sonraki adımlar
* HTTP iletişimi Hizmetleri'nde arasında örneğine bakın bir [örnek proje github'da](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started).
* [İletme toosecure HTTP hizmeti ile Merhaba ters proxy](service-fabric-reverseproxy-configure-secure-communication.md)
* [Güvenilir hizmetler remoting ile uzak yordam çağrıları](service-fabric-reliable-services-communication-remoting.md)
* [Web API OWIN güvenilir Hizmetleri'nde kullanır](service-fabric-reliable-services-communication-webapi.md)
* [Güvenilir hizmetler kullanarak WCF iletişimi](service-fabric-reliable-services-communication-wcf.md)
* Ek ters proxy yapılandırma seçenekleri için ApplicationGateway/Http bölümüne başvurun [özelleştirme Service Fabric kümesi ayarlarını](service-fabric-cluster-fabric-settings.md).

[0]: ./media/service-fabric-reverseproxy/external-communication.png
[1]: ./media/service-fabric-reverseproxy/internal-communication.png
