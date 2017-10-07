---
title: "ExpressRoute ilişkili sanal ağlar Klasik tooResource Yöneticisi geçirme: Azure: PowerShell | Microsoft Docs"
description: "Bu sayfayı nasıl hattınız taşıdıktan sonra toomigrate sanal ağlar tooResource Yöneticisi ilişkili açıklar."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: e64506c6909296f98c5dd23b1437bc0b81f31c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-expressroute-associated-virtual-networks-from-classic-tooresource-manager"></a>ExpressRoute ilişkili sanal ağlar Klasik tooResource Yöneticisi geçirme

Bu makalede, expressroute bağlantı hattı taşıdıktan sonra toomigrate Azure ExpressRoute hello Klasik dağıtım modeli toohello Azure Resource Manager dağıtım modelinde sanal ağlara nasıl ilişkili açıklanmaktadır. 


## <a name="before-you-begin"></a>Başlamadan önce
* Hello hello Azure PowerShell modüllerinin en son sürümüne sahip olduğunuzu doğrulayın. Daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).
* Merhaba gözden geçirdiğinizden emin olun [Önkoşullar](expressroute-prerequisites.md), [yönlendirme gereksinimleri](expressroute-routing.md), ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.
* Altında sağlanan hello bilgileri gözden [bir expressroute bağlantı hattı Klasik tooResource Yöneticisi taşıma](expressroute-move.md). Tam olarak hello sınırları ve kısıtlamaları anladığınızdan emin olun.
* Merhaba hattı hello Klasik dağıtım modelinde tam olarak işlevsel olduğunu doğrulayın.
* Merhaba Resource Manager dağıtım modelinde oluşturulmuş bir kaynak grubu olduğundan emin olun.
* Kaynak geçiş belgeleri aşağıdaki hello gözden geçirin:

    * [Klasik tooAzure Resource Manager Iaas kaynaklardan Platform desteklenen geçişini](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [Teknik ya ilişkin ayrıntılar platform desteklenen geçiş Klasik tooAzure Kaynak Yöneticisi'nden](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
    * [Sık sorulan sorular: Platform desteklenen geçişini Klasik tooAzure Resource Manager Iaas kaynaklardan](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [En yaygın Geçiş hataları ve bunları azaltmanın yollarını gözden geçirin](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="supported-and-unsupported-scenarios"></a>Desteklenen ve desteklenmeyen senaryolar

* Bir expressroute bağlantı hattı hello Klasik toohello Resource Manager ortamından herhangi kesinti olmadan taşınabilir. Merhaba Klasik toohello Resource Manager ortamı kapalı kalma süresi olmadan gelen tüm expressroute bağlantı hattını taşıyabilirsiniz. Merhaba yönergeleri izleyin [PowerShell kullanarak hello Klasik toohello Resource Manager dağıtım modelinden ExpressRoute bağlantı hatları taşıma](expressroute-howto-move-arm.md). Bu bir önkoşul toomove kaynaklara bağlı toohello sanal ağdır.
* Sanal ağlar, ağ geçitleri ve ekli tooan aynı abonelik olabilir hello'daki expressroute bağlantı hattına olan ilişkili dağıtım hello sanal ağ içinde toohello Resource Manager ortamı herhangi kesinti olmadan geçirildi. Merhaba adımları açıklanan sonraki toomigrate kaynaklar sanal ağlar, ağ geçitleri ve sanal ağ içindeki hello dağıtılan sanal makineleri gibi izleyebilirsiniz. Bunlar geçirilmeden önce hello sanal ağlar doğru şekilde yapılandırıldığından emin olmanız gerekir. 
* Merhaba expressroute bağlantı hattı bazı kapalı kalma süresi toocomplete hello geçiş gerektiği sanal ağlar, ağ geçitleri ve ilişkili dağıtımları bulunmayan hello sanal ağ içinde aynı abonelik hello. Merhaba belge Hello son Kısım hello adımları takip toobe toomigrate kaynakları açıklar.
* Bir sanal ağ ExpressRoute ağ geçidi ve VPN ağ geçidi ile geçirilemez.

## <a name="move-an-expressroute-circuit-from-classic-tooresource-manager"></a>Bir expressroute bağlantı hattı Klasik tooResource Yöneticisi taşıma
Bir expressroute bağlantı hattı hello Klasik toohello toomigrate kaynaklarını denemeden önce Kaynak Yöneticisi'ni ortamı toohello expressroute bağlantı hattı bağlı taşımanız gerekir. tooaccomplish bu görev, makaleler hello bakın:

* Altında sağlanan hello bilgileri gözden [bir expressroute bağlantı hattı Klasik tooResource Yöneticisi taşıma](expressroute-move.md).
* [Bir bağlantı hattı Klasik tooResource Manager Azure PowerShell kullanarak Taşı](expressroute-howto-move-arm.md).
* Hello Azure Hizmet Yönetimi portalı kullanın. Merhaba iş akışı çok izleyebilirsiniz[yeni bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-portal-resource-manager.md) ve hello alma seçeneğini belirleyin. 

Bu işlem, kapalı kalma süresi gerektirmez. Merhaba geçiş işlemi devam ederken, şirket içi ve Microsoft arasında tootransfer veri devam edebilirsiniz.

## <a name="migrate-virtual-networks-gateways-and-associated-deployments"></a>Sanal ağlar, ağ geçitleri ve ilişkili dağıtımları geçirme

Merhaba toomigrate izleyeceğiniz adımlar kaynaklarınızı hello olup bağlıdır aynı abonelik, farklı Aboneliklerde ya da her ikisini de.

### <a name="migrate-virtual-networks-gateways-and-associated-deployments-in-hello-same-subscription-as-hello-expressroute-circuit"></a>Sanal ağlar, ağ geçitleri, geçirme ve expressroute bağlantı hattı hello gibi aynı abonelikle ilişkili dağıtımlarda hello
Bu bölümde hello adımları takip toobe toomigrate açıklanmaktadır bir sanal ağ, ağ geçidi ve ilişkili dağıtımlarda expressroute bağlantı hattı hello gibi aynı abonelik hello. Kapalı kalma süresi olmadan, bu geçiş ile ilişkilidir. Toouse tüm kaynakları hello geçiş işlemiyle devam edebilirsiniz. Merhaba geçiş işlemi devam ederken hello Yönetim düzeyi kilitlendi. 

1. Merhaba expressroute bağlantı hattı hello Klasik toohello Resource Manager ortamından taşındığından emin olun.
2. Bu hello sanal ağ uygun şekilde hello geçiş için hazırlandığından emin olun.
3. Aboneliğiniz kaynak geçişi için kaydolun. tooregister kaynak geçişi, PowerShell parçacığını aşağıdaki kullanım hello aboneliğinizin:

  ```powershell 
  Select-AzureRmSubscription -SubscriptionName <Your Subscription Name>
  Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  ```
4. Doğrulama, hazırlama ve geçirilir. toomove hello sanal ağ, PowerShell parçacığını aşağıdaki kullanım hello:

  ```powershell
  Move-AzureVirtualNetwork -Prepare $vnetName  
  Move-AzureVirtualNetwork -Commit $vnetName
  ```

  Ayrıca, geçiş hello aşağıdaki PowerShell cmdlet'ini çalıştırarak da iptal edebilirsiniz:

  ```powershell
  Move-AzureVirtualNetwork -Abort $vnetName
  ```

## <a name="next-steps"></a>Sonraki adımlar
* [Klasik tooAzure Resource Manager Iaas kaynaklardan Platform desteklenen geçişini](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [Teknik ya ilişkin ayrıntılar platform desteklenen geçiş Klasik tooAzure Kaynak Yöneticisi'nden](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
* [Sık sorulan sorular: Platform desteklenen geçişini Klasik tooAzure Resource Manager Iaas kaynaklardan](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [En yaygın Geçiş hataları ve bunları azaltmanın yollarını gözden geçirin](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
