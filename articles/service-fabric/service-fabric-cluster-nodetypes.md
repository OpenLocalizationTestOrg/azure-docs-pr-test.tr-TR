---
title: "aaaService doku düğüm türleri ve VM ölçek kümesi | Microsoft Docs"
description: "Service Fabric düğüm türleri tooVM ölçek kümeleri nasıl ilişkili olduğunu ve tooremote nasıl bağlanacağını tooa VM ölçek kümesi örneği veya bir küme düğümü açıklar."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 5441e7e0-d842-4398-b060-8c9d34b07c48
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: chackdan
ms.openlocfilehash: 830ea2816f5864de146a77483c85de26f91c2425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-relationship-between-service-fabric-node-types-and-virtual-machine-scale-sets"></a>Service Fabric düğüm türleri ve sanal makine ölçek kümeleri arasındaki Hello ilişki
Sanal makine ölçek kümeleri toodeploy kullanın ve sanal makinelerin bir koleksiyon kümesi olarak yönetmek bir Azure işlem kaynaktır. Service Fabric kümesi içinde tanımlanan her düğüm türü bir ayrı VM ölçek kümesi ayarlanır. Her düğüm türü sonra ölçeklendirilebilir veya Aşağı bağımsız olarak, farklı bağlantı noktalarının açık olması ve farklı kapasite ölçümlerini olabilir.

Aşağıdaki ekran görüntüsü hello iki düğüm türü olan bir küme gösterir: ön uç ve arka uç.  Her düğüm türü her beş düğüm yok.

![İki düğüm türleri olan kümesinin ekran görüntüsü][NodeTypes]

## <a name="mapping-vm-scale-set-instances-toonodes"></a>VM ölçek kümesi örneklerinin toonodes eşleme
Yukarıda gördüğünüz gibi hello VM ölçek kümesi örneklerinin 0 örneğinden başlatın ve sonra artar. Merhaba numaralandırma hello adlarında yansıtılır. Örneğin, BackEnd_0 0 hello arka uç VM ölçek kümesi örneğidir. Belirli bu VM ölçek kümesi BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 ve BackEnd_4 adlı beş örneğine sahip.

Bir VM ölçek kümesi ölçeklendirdiğinizde yeni bir örneği oluşturulur. Merhaba yeni VM ölçek kümesi örnek adı genellikle olacaktır hello VM ölçek kümesi adı + hello sonraki örneği sayısı. Bizim örneğimizde, BackEnd_5 değil.

## <a name="mapping-vm-scale-set-load-balancers-tooeach-node-typevm-scale-set"></a>Ölçek kümesini yük Dengeleyiciler tooeach düğüm türü/VM ölçek kümesi VM eşleme
Sonra kümenizi hello portalından dağıtmış olan ya da bir kaynak grubundaki tüm kaynakların bir listesini aldığınızda sağlamış olduğumuz, ardından hello örnek Resource Manager şablonu kullanmış her VM ölçek kümesi veya düğüm türü için hello yük Dengeleyiciler görürsünüz.

Merhaba adı şöyle olur: **LB -&lt;NodeType adı&gt;**. Örneğin, LB-sfcluster4doc-bu ekran görüntüsünde gösterildiği gibi 0:

![Kaynaklar][Resources]

## <a name="remote-connect-tooa-vm-scale-set-instance-or-a-cluster-node"></a>Uzaktan bağlantı tooa VM ölçek kümesi örneği veya bir küme düğümü
Bir kümede tanımlanan her düğüm türü bir ayrı VM ölçek kümesi ayarlanır.  Anlamına gelir düğüm türleri hello Genişletilebilir yukarı veya Aşağı bağımsız olarak ve farklı VM SKU'ları yapılabilir. Sanal makineleri tek örnek hello VM ölçek kümesi örnekleri kendi sanal bir IP adresi al değil. Bir bit olabilir bir IP için bakarken zor adresi ve bağlantı noktası tooremote kullanabileceğiniz tooa belirli örneğe bağlanın.

Toodiscover izleyin hello adımlar şunlardır bunları.

### <a name="step-1-find-out-hello-virtual-ip-address-for-hello-node-type-and-then-inbound-nat-rules-for-rdp"></a>1. adım: hello sanal IP adresi hello düğüm türü için'i ve ardından gelen NAT kuralları RDP öğrenin
Tooget hello gerekir, sipariş tooget içinde hello kaynak tanımının bir parçası olarak tanımlanmış olan değerleri gelen NAT kuralları **Microsoft.Network/loadBalancers**.

Merhaba Portalı'nda toohello yük dengeleyici dikey gidin ve ardından **ayarları**.

![LBBlade][LBBlade]

İçinde **ayarları**, tıklayın **gelen NAT kuralları**. Bu şimdi toohello ilk VM ölçek kümesi örnek IP adresi ve bağlantı noktası tooremote kullanabileceğiniz hello verir bağlayın. Merhaba ekran görüntüsünde, olmasından **104.42.106.156** ve **3389**

![NATRules][NATRules]

### <a name="step-2-find-out-hello-port-that-you-can-use-tooremote-connect-toohello-specific-vm-scale-set-instancenode"></a>2. adım: başlangıç bağlantı noktası tooremote kullanabileceğiniz öğrenin bağlanmak toohello belirli VM ölçek kümesi örnek/düğüm
Bu belgede daha önce hello VM ölçek kümesi örneklerinin toohello düğümleri nasıl eşleneceğine hakkında açıklandı. Merhaba tam bağlantı noktasına bu toofigure kullanacağız.

Merhaba bağlantı noktalarını hello VM ölçek kümesi örnek artan düzende ayrılır. Bu nedenle hello ön uç düğüm türü için my örnekte, her hello beş örneklerinin hello bağlantı noktalarını hello aşağıda verilmiştir. artık toodo VM ölçek kümesi Örneğiniz için aynı eşleme hello.

| **VM ölçek kümesi örneği** | **Bağlantı Noktası** |
| --- | --- |
| FrontEnd_0 |3389 |
| FrontEnd_1 |3390 |
| FrontEnd_2 |3391 |
| FrontEnd_3 |3392 |
| FrontEnd_4 |3393 |
| FrontEnd_5 |3394 |

### <a name="step-3-remote-connect-toohello-specific-vm-scale-set-instance"></a>3. adım: Uzaktan bağlanma toohello belirli VM ölçek kümesi örneği
Uzak Masaüstü Bağlantısı tooconnect toohello FrontEnd_1 kullanmam Hello ekran görüntüsünde:

![RDP][RDP]

## <a name="how-toochange-hello-rdp-port-range-values"></a>Nasıl toochange hello RDP bağlantı noktası aralığı değerleri
### <a name="before-cluster-deployment"></a>Küme dağıtım öncesinde
Bir Resource Manager şablonu kullanarak hello küme ayarlarken hello hello aralığı belirtebilirsiniz **inboundNatPools**.

Toohello kaynak tanımı gitmek **Microsoft.Network/loadBalancers**. Altında Bul hello açıklamasını **inboundNatPools**.  Hello yerine *frontendPortRangeStart* ve *frontendportrangeend değeri* değerleri.

![InboundNatPools][InboundNatPools]

### <a name="after-cluster-deployment"></a>Küme dağıtım sonrası
Bu biraz daha karmaşıktır ve silinmesini hello Vm'lerde neden olabilir. Şimdi, Azure PowerShell kullanarak tooset yeni değerlere sahip olur. Azure PowerShell 1.0 veya üstü makinenize yüklü olduğundan emin olun. Daha önceden yapmadıysanız ı kesinlikle özetlenen hello adımları izleyin önermek [nasıl tooinstall ve Azure PowerShell yapılandırın.](/powershell/azure/overview)

İçinde tooyour Azure hesabı oturum açın. Bu PowerShell komutunu herhangi bir nedenden dolayı başarısız olursa, doğru şekilde yüklenmemiş Azure PowerShell yüklü olup olmadığını kontrol etmeniz gerekir.

```
Login-AzureRmAccount
```

Yük Dengeleyici tooget Ayrıntılar aşağıdaki hello çalıştırın ve hello değerlerini hello açıklamasını görmek **inboundNatPools**:

```
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load balancer name>
```

Şimdi *frontendportrangeend değeri* ve *frontendPortRangeStart* istediğiniz toohello değerler.

```
$PropertiesObject = @{
    #Property = value;
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName <RG name> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load Balancer name> -ApiVersion <use hello API version that get returned> -Force
```


## <a name="next-steps"></a>Sonraki adımlar
* [Merhaba "Herhangi bir yere dağıtma" özelliği ve Azure tarafından yönetilen kümeleriyle karşılaştırma genel bakış](service-fabric-deploy-anywhere.md)
* [Küme güvenliği](service-fabric-cluster-security.md)
* [Service Fabric SDK ve çalışmaya başlama](service-fabric-get-started.md)

<!--Image references-->
[NodeTypes]: ./media/service-fabric-cluster-nodetypes/NodeTypes.png
[Resources]: ./media/service-fabric-cluster-nodetypes/Resources.png
[InboundNatPools]: ./media/service-fabric-cluster-nodetypes/InboundNatPools.png
[LBBlade]: ./media/service-fabric-cluster-nodetypes/LBBlade.png
[NATRules]: ./media/service-fabric-cluster-nodetypes/NATRules.png
[RDP]: ./media/service-fabric-cluster-nodetypes/RDP.png
