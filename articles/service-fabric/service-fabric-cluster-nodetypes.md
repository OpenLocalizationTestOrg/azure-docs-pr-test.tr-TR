---
title: "Service Fabric düğüm türleri ve VM ölçek kümesi | Microsoft Docs"
description: "Service Fabric düğüm türleri VM ölçek kümesi ile ilgili ve nasıl uzak bir VM ölçek kümesi örneği veya bir küme düğümüne bağlanmak nasıl açıklanmaktadır."
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
ms.openlocfilehash: 3b1a22bb3653abb68fc73645ad2cb623fabc7736
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="the-relationship-between-service-fabric-node-types-and-virtual-machine-scale-sets"></a>Service Fabric düğüm türleri ve sanal makine ölçek kümeleri arasındaki ilişki
Sanal makine ölçek kümeleri dağıtmak ve sanal makinelerin bir koleksiyon kümesi olarak yönetmek için kullanabileceğiniz bir Azure işlem kaynaktır. Service Fabric kümesi içinde tanımlanan her düğüm türü bir ayrı VM ölçek kümesi ayarlanır. Her düğüm türü sonra ölçeklendirilebilir veya Aşağı bağımsız olarak, farklı bağlantı noktalarının açık olması ve farklı kapasite ölçümlerini olabilir.

Aşağıdaki ekran görüntüsünde iki düğüm türü olan bir küme gösterir: ön uç ve arka uç.  Her düğüm türü her beş düğüm yok.

![İki düğüm türleri olan kümesinin ekran görüntüsü][NodeTypes]

## <a name="mapping-vm-scale-set-instances-to-nodes"></a>VM ölçek kümesi örneklerinin düğümlerine eşleme
Yukarıda gördüğünüz gibi VM ölçek kümesi örneklerinin örneğinden 0'ı ve ardından gelecek oluşturan başlatın. Numaralandırma adlarında yansıtılır. Örneğin, BackEnd_0 0 arka uç VM ölçek kümesi örneğidir. Belirli bu VM ölçek kümesi BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 ve BackEnd_4 adlı beş örneğine sahip.

Bir VM ölçek kümesi ölçeklendirdiğinizde yeni bir örneği oluşturulur. Yeni VM ölçek kümesi örnek adı genellikle olacaktır VM ölçek kümesi adı + sonraki örneği sayısı. Bizim örneğimizde, BackEnd_5 değil.

## <a name="mapping-vm-scale-set-load-balancers-to-each-node-typevm-scale-set"></a>VM ölçek eşleme yük dengeleyici her düğüm türü/VM ölçek kümesi ayarlama
Sonra kümenizi portalından dağıtmış olan ya da bir kaynak grubundaki tüm kaynakların bir listesini aldığınızda sağlamış olduğumuz, ardından örnek Resource Manager şablonu kullanmış her VM ölçek kümesi veya düğüm türü için yük Dengeleyiciler görürsünüz.

Adı şöyle olur: **LB -&lt;NodeType adı&gt;**. Örneğin, LB-sfcluster4doc-bu ekran görüntüsünde gösterildiği gibi 0:

![Kaynaklar][Resources]

## <a name="remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node"></a>Uzaktan bağlantı VM ölçek kümesi örneği veya bir küme düğümü
Bir kümede tanımlanan her düğüm türü bir ayrı VM ölçek kümesi ayarlanır.  Düğüm türleri ölçeklendirilmiş anlamına yukarı veya Aşağı bağımsız olarak ve farklı VM SKU'ları yapılabilir. Sanal makineleri tek örnek VM ölçek kümesi örnekleri kendi sanal bir IP adresi al değil. Bu nedenle, bir IP adresi için aradığınız ve kullanabileceğiniz uzak bağlantı noktası belirli bir örneğine bağlanmak biraz zor olabilir.

Bunları bulmak için izleyebileceğiniz adımlar şunlardır.

### <a name="step-1-find-out-the-virtual-ip-address-for-the-node-type-and-then-inbound-nat-rules-for-rdp"></a>1. adım: düğüm türü için sanal IP adresi ve gelen NAT kuralları RDP öğrenin
Alabilmek için kaynak tanımı için bir parçası olarak tanımlanan gelen NAT kuralları değerleri almanız gereken **Microsoft.Network/loadBalancers**.

Portalda, yük dengeleyici dikey penceresine gidin ve ardından **ayarları**.

![LBBlade][LBBlade]

İçinde **ayarları**, tıklayın **gelen NAT kuralları**. Bu artık IP adresini verir ve kullanabileceğiniz uzak bağlantı noktası ilk VM ölçek kümesi örneğine bağlanın. Aşağıdaki ekran görüntüsünde, olmasından **104.42.106.156** ve **3389**

![NATRules][NATRules]

### <a name="step-2-find-out-the-port-that-you-can-use-to-remote-connect-to-the-specific-vm-scale-set-instancenode"></a>2. adım: uzaktan için kullandığınız bağlantı noktası belirli VM ölçek kümesi örnek/düğüme bağlanmak çıkış Bul
Bu belgede daha önce VM ölçek kümesi örneklerinin düğümlerine nasıl eşleneceğine hakkında açıklandı. Tam bağlantı noktasına bulmak için kullanacağız.

Bağlantı noktaları, VM ölçek kümesi örnek artan düzende ayrılır. Bu nedenle ön uç düğüm türü için my örnekte beş örneklerinin her biri için bağlantı noktalarını aşağıda verilmiştir. Şimdi VM ölçek kümesi Örneğiniz için aynı eşleme yapmanız gerekir.

| **VM ölçek kümesi örneği** | **Bağlantı Noktası** |
| --- | --- |
| FrontEnd_0 |3389 |
| FrontEnd_1 |3390 |
| FrontEnd_2 |3391 |
| FrontEnd_3 |3392 |
| FrontEnd_4 |3393 |
| FrontEnd_5 |3394 |

### <a name="step-3-remote-connect-to-the-specific-vm-scale-set-instance"></a>3. adım: Uzaktan bağlanmak için belirli VM ölçek kümesi örneği
Aşağıdaki ekran görüntüsünde, t FrontEnd_1 bağlanmak için Uzak Masaüstü bağlantısı kullanın:

![RDP][RDP]

## <a name="how-to-change-the-rdp-port-range-values"></a>RDP bağlantı noktası aralığı değerlerini değiştirme
### <a name="before-cluster-deployment"></a>Küme dağıtım öncesinde
Bir Resource Manager şablonu kullanarak kümeyi ayarlarken aralığında belirtebilirsiniz **inboundNatPools**.

İçin kaynak tanımı gidin **Microsoft.Network/loadBalancers**. Altında Bul açıklaması **inboundNatPools**.  Değiştir *frontendPortRangeStart* ve *frontendportrangeend değeri* değerleri.

![InboundNatPools][InboundNatPools]

### <a name="after-cluster-deployment"></a>Küme dağıtım sonrası
Bu biraz daha karmaşıktır ve silinmesini VM'ler neden olabilir. Artık Azure PowerShell'i kullanarak yeni değerleri ayarlamak bulunacaktır. Azure PowerShell 1.0 veya üstü makinenize yüklü olduğundan emin olun. Daha önceden yapmadıysanız ı kesinlikle özetlenen adımları izleyin önermek [nasıl Azure PowerShell'i yükleme ve yapılandırma.](/powershell/azure/overview)

Azure hesabınızda oturum açın. Bu PowerShell komutunu herhangi bir nedenden dolayı başarısız olursa, doğru şekilde yüklenmemiş Azure PowerShell yüklü olup olmadığını kontrol etmeniz gerekir.

```
Login-AzureRmAccount
```

Yük dengeleyicide ayrıntıları almak için aşağıdaki komutu çalıştırın ve değerlerin açıklaması için bkz: **inboundNatPools**:

```
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load balancer name>
```

Şimdi *frontendportrangeend değeri* ve *frontendPortRangeStart* istediğiniz değerleri.

```
$PropertiesObject = @{
    #Property = value;
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName <RG name> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load Balancer name> -ApiVersion <use the API version that get returned> -Force
```


## <a name="next-steps"></a>Sonraki adımlar
* ["Her yere dağıtma" özelliği ve Azure tarafından yönetilen kümeleriyle karşılaştırma genel bakış](service-fabric-deploy-anywhere.md)
* [Küme güvenliği](service-fabric-cluster-security.md)
* [Service Fabric SDK ve çalışmaya başlama](service-fabric-get-started.md)

<!--Image references-->
[NodeTypes]: ./media/service-fabric-cluster-nodetypes/NodeTypes.png
[Resources]: ./media/service-fabric-cluster-nodetypes/Resources.png
[InboundNatPools]: ./media/service-fabric-cluster-nodetypes/InboundNatPools.png
[LBBlade]: ./media/service-fabric-cluster-nodetypes/LBBlade.png
[NATRules]: ./media/service-fabric-cluster-nodetypes/NATRules.png
[RDP]: ./media/service-fabric-cluster-nodetypes/RDP.png
