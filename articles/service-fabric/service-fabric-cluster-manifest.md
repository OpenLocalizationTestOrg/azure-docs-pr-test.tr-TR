---
title: "aaaConfigure Azure Service Fabric tek başına kümenizi | Microsoft Docs"
description: "Bilgi nasıl tooconfigure tek başına veya özel Service Fabric kümesi."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 0c5ec720-8f70-40bd-9f86-cd07b84a219d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dekapur
ms.openlocfilehash: ce2ad387162a05668bbd3a271c754776fe471850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-settings-for-standalone-windows-cluster"></a>Tek başına Windows kümesi için yapılandırma ayarları
Bir tek başına Service Fabric kümesi kullanarak tooconfigure nasıl hello bu makalede ***ClusterConfig.JSON*** dosya. Bu dosya toospecify bilgileri hello Service Fabric düğümleri ve IP adresleri, farklı türlerde düğümleri gibi hello ağ topolojisi arıza/yükseltme etki alanları, bakımından yanı sıra hello küme, hello güvenlik yapılandırmaları için tek başına kullanabilirsiniz Küme.

Olduğunda, [hello tek başına Service Fabric paketi Yükle](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), birkaç hello ClusterConfig.JSON dosyasının indirilen tooyour iş makine örneklerdir. Merhaba örnekleri sahip *DevCluster* adlarını, aynı makine, mantıksal düğümleri gibi hello üç tüm düğümlerde ile bir küme oluşturmanıza yardımcı olur. Bunlar dışında en azından bir düğümün bir birincil düğüm olarak işaretlenmesi gerekir. Bu küme bir geliştirme veya test ortamı için yararlıdır ve bir üretim kümesi olarak desteklenmiyor. Merhaba örnekleri sahip *MultiMachine* adlarında, her bir düğümde ayrı bir makine ile bir üretim kalite kümesi oluşturmanıza yardımcı olur.

1. *ClusterConfig.Unsecure.DevCluster.JSON* ve *ClusterConfig.Unsecure.MultiMachine.JSON* nasıl toocreate güvenli olmayan bir test veya üretim küme sırasıyla Göster. 
2. *ClusterConfig.Windows.DevCluster.JSON* ve *ClusterConfig.Windows.MultiMachine.JSON* toocreate test veya üretim küme güvenliği nasıl kullanarak Göster [Windows Güvenliği](service-fabric-windows-cluster-windows-security.md).
3. *ClusterConfig.X509.DevCluster.JSON* ve *ClusterConfig.X509.MultiMachine.JSON* toocreate test veya üretim küme güvenliği nasıl kullanarak Göster [X509 sertifika tabanlı güvenlik](service-fabric-windows-cluster-x509-security.md). 

İnceleyeceğiz artık çeşitli bölümlerini hello bir ***ClusterConfig.JSON*** olarak aşağıdaki dosya.

## <a name="general-cluster-configurations"></a>Genel küme yapılandırmaları
Bu hello geniş küme belirli yapılandırmalar, aşağıdaki hello JSON parçacığında gösterildiği gibi kapsar.

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",

Herhangi bir kolay ad tooyour Service Fabric küme toohello atayarak verebilirsiniz **adı** değişkeni. Merhaba **clusterConfigurationVersion** kümenizin; hello sürüm numarası, Service Fabric kümesi yükseltme her zaman artırmanız gerekir. Merhaba ancak bırakmalısınız **apiVersion** toohello varsayılan değeri.

<a id="clusternodes"></a>

## <a name="nodes-on-hello-cluster"></a>Merhaba küme düğümlerinde
Hello kullanarak Service Fabric kümenizde hello düğümleri yapılandırabilirsiniz **düğümleri** bölümünde, aşağıdaki kod parçacığında gösterildiği hello olarak.

    "nodes": [{
        "nodeName": "vm0",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType1",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType2",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],

Service Fabric kümesi en az 3 düğümleri içermesi gerekir. Kurulumunuzu göre daha fazla düğüm toothis bölümüne ekleyebilirsiniz. Aşağıdaki tablonun hello her düğüm için hello yapılandırma ayarları açıklanmaktadır.

| **Düğüm yapılandırması** | **Açıklama** |
| --- | --- |
| nodeName |Herhangi bir kolay ad toohello düğümü verebilirsiniz. |
| IP adresi |Bir komut penceresi açıp yazarak, düğümün IP adresini Hello bulmak `ipconfig`. Not hello IPv4 adresi ve toohello Ata **IPADDRESS** değişkeni. |
| nodeTypeRef |Her düğüm farklı düğüm türü atanabilir. Merhaba [düğüm türleri](#nodetypes) hello aşağıdaki bölümde tanımlanır. |
| faultDomain |Hello başarısız olabilir hata etki alanları etkinleştir küme yöneticileri toodefine hello fiziksel düğümde aynı tooshared fiziksel bağımlılıkları zaman. |
| upgradeDomain |Yükseltme etki alanları tanımlamak Service Fabric adresindeki hello hakkında aynı yükseltmeleri için kapatıldığından düğüm kümesi saat. Fiziksel gereksinimlere göre sınırlı değildir gibi yükseltme etki alanları, hangi düğümleri tooassign toowhich seçebilirsiniz. |

## <a name="cluster-properties"></a>Küme Özellikleri
Merhaba **özellikleri** hello ClusterConfig.JSON bölümünde şu kullanılan tooconfigure hello küme şekildedir.

<a id="reliability"></a>

### <a name="reliability"></a>Güvenilirlik
Merhaba kavramı **reliabilityLevel** hello çoğaltmaların sayısı veya hello birincil hello küme düğümlerinde çalıştırabilirsiniz hello Service Fabric Sistem Hizmetleri örnekleri tanımlar. Bu hizmetler hello güvenilirliğini belirler ve bu nedenle küme hello. Merhaba hello sistem tarafından hesaplanan küme oluşturma ve yükseltme zamanında değerdir.

### <a name="diagnostics"></a>Tanılama
Merhaba **diagnosticsStore** bölümü sağlar, tooconfigure parametreleri tooenable tanılama ve sorun giderme düğümü veya küme hataları hello aşağıdaki kod parçacığında gösterildiği gibi. 

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

Merhaba **meta veri** küme tanılama açıklaması ve kurulumunuzu uygun şekilde ayarlayabilirsiniz. Bu değişkenler ETW İzleme günlükleri, kilitlenme bilgi dökümleri yanı sıra performans sayaçlarını toplama de yardımcı olur. Okuma [işaretlenemedi](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) ve [ETW İzleme](https://msdn.microsoft.com/library/ms751538.aspx) ETW hakkında daha fazla bilgi için izleme günlüklerine. Tüm günlükleri de dahil olmak üzere [kilitlenme dökümleri](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) ve [performans sayaçları](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) yönlendirilmiş toohello olabilir **connectionString** makinenizde klasör. Aynı zamanda *AzureStorage* tanılama depolamak için. Aşağıdaki örnek kod parçacığında için bölümüne bakın.

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a>Güvenlik
Merhaba **güvenlik** bölüm güvenli tek başına Service Fabric kümesi için gerekli değildir. Aşağıdaki kod parçacığında hello bu bölümün parçası gösterir.

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

Merhaba **meta veri** güvenli kümenizi açıklaması ve kurulumunuzu uygun şekilde ayarlayabilirsiniz. Merhaba **ClusterCredentialType** ve **ServerCredentialType** hello küme ve hello düğümler uygulayan güvenlik hello türü belirlenemedi. Tooeither ayarlanabilir *X509* bir sertifika tabanlı güvenlik için veya *Windows* bir Azure Active Directory tabanlı güvenlik için. Merhaba hello geri kalanı **güvenlik** bölüm hello güvenlik hello türünü tabanlı olacaktır. Okuma [sertifikalar tabanlı güvenlik tek başına kümedeki](service-fabric-windows-cluster-x509-security.md) veya [tek başına kümede Windows Güvenliği](service-fabric-windows-cluster-windows-security.md) nasıl toofill hello çıkışı rest hello hakkında bilgi için **güvenlik**bölümü.

<a id="nodetypes"></a>

### <a name="node-types"></a>Düğüm türleri
Merhaba **nodeTypes** bölüm kümenizi sahip hello düğümleri hello türünü açıklar. En az bir düğüm türü, aşağıdaki hello parçacığında gösterildiği gibi bir küme için belirtilmelidir. 

    "nodeTypes": [{
        "name": "NodeType0",
        "clientConnectionEndpointPort": "19000",
        "clusterConnectionEndpointPort": "19001",
        "leaseDriverEndpointPort": "19002"
        "serviceConnectionEndpointPort": "19003",
        "httpGatewayEndpointPort": "19080",
        "reverseProxyEndpointPort": "19081",
        "applicationPorts": {
            "startPort": "20575",
            "endPort": "20605"
        },
        "ephemeralPorts": {
            "startPort": "20606",
            "endPort": "20861"
        },
        "isPrimary": true
    }]

Merhaba **adı** bu belirli düğüm türü için hello kolay addır. Bu düğüm türünde bir düğüm toocreate atamak kolay ad toohello **nodeTypeRef** bu düğüm için değişken belirtildiği gibi [yukarıda](#clusternodes). Her düğüm türü için kullanılacak hello bağlantı uç tanımlayın. Bu kümedeki başka bir uç nokta ile çakışmadığından sürece, bu bağlantı uç noktaları için herhangi bir bağlantı noktası numarası seçebilirsiniz. Çok düğümlü bir küme içinde olacaktır bir veya daha fazla birincil düğüm (yani **isPrimary** çok ayarlamak*true*) hello bağlı olarak [ **reliabilityLevel** ](#reliability). Okuma [Service Fabric kümesi kapasite planlama konuları](service-fabric-cluster-capacity.md) hakkında bilgi için **nodeTypes** ve **reliabilityLevel**ve hangi birincil ve hello tooknow birincil olmayan düğüm türleri. 

#### <a name="endpoints-used-tooconfigure-hello-node-types"></a>Uç noktaları tooconfigure hello düğüm türleri kullanılır
* *clientConnectionEndpointPort* hello istemci API'leri kullanırken hello istemci tooconnect toohello küme tarafından kullanılan hello bağlantı noktasıdır. 
* *clusterConnectionEndpointPort* hangi hello düğümleri birbiriyle hello bağlantı noktasıdır.
* *leaseDriverEndpointPort* hello düğümleri hala etkin olup olmadığını hello küme kira sürücü toofind tarafından kullanılan hello bağlantı noktasıdır. 
* *serviceConnectionEndpointPort* hello uygulamaları tarafından kullanılan başlangıç bağlantı noktası ve bu belirli düğüm üzerindeki hello Service Fabric istemcisi ile toocommunicate bir düğümde dağıtılan Hizmetleri.
* *httpGatewayEndpointPort* hello Service Fabric Explorer tooconnect toohello küme tarafından kullanılan hello bağlantı noktasıdır.
* *ephemeralPorts* hello geçersiz kılma [hello işletim sistemi tarafından kullanılan dinamik bağlantı noktaları](https://support.microsoft.com/kb/929851). Service Fabric uygulaması bağlantı noktaları olarak parçası kullanır ve hello kalan hello işletim sistemi için kullanılabilir olacak. Tüm amaçlar için hello örnek JSON dosyalarında verilen hello aralıkları kullanabilmek için de bu aralık toohello var olan bir aralığı hello işletim sistemi, mevcut eşlenir. Merhaba fark hello başlangıç ve hello uç bağlantı noktaları arasında en az 255 emin toomake gerekir. Bu aralık hello işletim sistemiyle paylaşılan beri bu fark, düşükse çakışmaları çalışabilir. Çalıştırarak yapılandırılmış hello dinamik bağlantı noktası aralığını görmek `netsh int ipv4 show dynamicport tcp`.
* *applicationPorts* hello Service Fabric uygulamaları tarafından kullanılan hello bağlantı noktalarıdır. Merhaba uygulama bağlantı noktası aralığı büyüklükte toocover hello uç nokta gereksinim uygulamalarınızın olmalıdır. Bu aralık hello makinede, yani hello hello dinamik bağlantı noktası aralığından özel *ephemeralPorts* hello yapılandırmasında belirlenen aralık.  Yeni bağlantı noktaları gereklidir, aynı zamanda her hello Güvenlik Duvarı'nı bu bağlantı noktaları açma ilgilenebilmek Service Fabric bunları kullanın. 
* *reverseProxyEndpointPort* bir isteğe bağlı ters proxy uç noktadır. Bkz: [Service Fabric Ters Proxy](service-fabric-reverseproxy.md) daha fazla ayrıntı için. 

### <a name="log-settings"></a>Günlük ayarları
Merhaba **fabricSettings** bölümü tooset hello kök dizinler hello Service Fabric veri ve günlükleri için sağlar. Bunlar yalnızca hello ilk küme oluşturma sırasında özelleştirebilirsiniz. Aşağıda bu bölüm için bir örnek parçacığı konusuna bakın.

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

İşletim sistemi çökme (Crash karşı) daha fazla güvenilirlik sağladığından bir işletim sistemi olmayan sürücü hello FabricDataRoot olarak ve FabricLogRoot kullanarak önerilir. Yalnızca hello veri kök özelleştirirseniz, ardından hello günlük kök hello veri kökü altındaki bir düzey yerleştirilecek olduğunu unutmayın.

### <a name="stateful-reliable-service-settings"></a>Durum bilgisi olan güvenilir hizmet ayarları
Merhaba **KtlLogger** bölümü güvenilir hizmetler için tooset hello genel yapılandırma ayarlarını sağlar. Bu ayarlar hakkında daha fazla ayrıntı için okuma [durum bilgisi olan güvenilir hizmetler yapılandırma](service-fabric-reliable-services-configuration.md).
Aşağıdaki örnek Hello alır toochange hello hello paylaşılan işlem günlüğü tooback durum bilgisi olan hizmetler için herhangi bir güvenilir koleksiyonu nasıl oluşturulacağını gösterir.

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a>Eklenti Özellikleri
tooconfigure eklenti özellikleri hello apiVersion yapılandırılmış olarak ' 04-2017' veya daha yüksek olmalıdır ve yapılandırılmış toobe addonFeatures gerekiyor:

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a>Kapsayıcı desteği
windows server kapsayıcı ve tek başına kümeleri için hyper-v kapsayıcı için tooenable kapsayıcı desteği, hello 'DnsService' Eklenti özelliğinin etkin toobe gerekir.


## <a name="next-steps"></a>Sonraki adımlar
Tek başına küme kurulumunuzu uygun şekilde yapılandırılmış ClusterConfig.JSON dosyanın tamamını olduktan sonra kümenizi aşağıdaki hello makale dağıtabilirsiniz [bir tek başına Service Fabric kümesi oluştur](service-fabric-cluster-creation-for-windows-server.md) ve çok devam[Service Fabric Explorer ile kümenizi görselleştirme](service-fabric-visualizing-your-cluster.md).

