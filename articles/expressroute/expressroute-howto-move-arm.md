---
title: "ExpressRoute bağlantı hatları Klasik tooResource Yöneticisi taşıma: PowerShell: Azure | Microsoft Docs"
description: "Bu sayfayı nasıl toomove Klasik hattı toohello Resource Manager dağıtım modeli PowerShell kullanarak açıklar."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 08152836-23e7-42d1-9a56-8306b341cd91
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/03/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 8dcadafca5e4f40773902cec5786eba1dbe133eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="move-expressroute-circuits-from-hello-classic-toohello-resource-manager-deployment-model-using-powershell"></a>PowerShell kullanarak hello Klasik toohello Resource Manager dağıtım modelinden ExpressRoute bağlantı hatları taşıma

toouse hello Klasik ve Resource Manager dağıtım modeli için expressroute bağlantı hattı, hello hattı toohello Resource Manager dağıtım modeli taşımanız gerekir. Merhaba aşağıdaki bölümlerde, PowerShell kullanarak hattınız taşımanıza yardımcı olur.

## <a name="before-you-begin"></a>Başlamadan önce

* Merhaba hello Azure PowerShell modüllerinin en son sürümüne sahip olduğunuzdan emin olun (en az sürüm 1.0). Daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).
* Merhaba gözden geçirdiğinizden emin olun [Önkoşullar](expressroute-prerequisites.md), [yönlendirme gereksinimleri](expressroute-routing.md), ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.
* Altında sağlanan hello bilgileri gözden [bir expressroute bağlantı hattı Klasik tooResource Yöneticisi taşıma](expressroute-move.md). Tam olarak hello sınırları ve kısıtlamaları anladığınızdan emin olun.
* Merhaba hattı hello Klasik dağıtım modelinde tam olarak işlevsel olduğunu doğrulayın.
* Merhaba Resource Manager dağıtım modelinde oluşturulmuş bir kaynak grubu olduğundan emin olun.

## <a name="move-an-expressroute-circuit"></a>Bir expressroute bağlantı hattı taşıma

### <a name="step-1-gather-circuit-details-from-hello-classic-deployment-model"></a>Adım 1: hello Klasik dağıtım modelinden bağlantı hattı ayrıntılarını toplama

Toohello Azure Klasik ortamı oturum ve hello hizmet anahtarı toplayın.

1. İçinde tooyour Azure hesabı oturum açın.

  ```powershell
  Add-AzureAccount
  ```

2. Merhaba uygun Azure aboneliğini seçin.

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. Merhaba PowerShell modülleri Azure ve ExpressRoute için içeri aktarın.

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. Tooget hello hizmeti anahtarları aşağıda Hello cmdlet'ini tüm ExpressRoute bağlantı hatları için kullanın. Merhaba Hello anahtarları aldıktan sonra kopyalama **hizmet anahtarı** hello devrenin toomove toohello Resource Manager dağıtım modeli istiyor.

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a>2. adım: Oturum açın ve bir kaynak grubu oluşturun

Toohello Resource Manager ortamında oturum açın ve yeni bir kaynak grubu oluşturun.

1. Tooyour Azure Resource Manager ortamında oturum açın.

  ```powershell
  Login-AzureRmAccount
  ```

2. Merhaba uygun Azure aboneliğini seçin.

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. Bir kaynak grubu zaten yoksa toocreate yeni bir kaynak grubu aşağıdaki kod parçacığını hello değiştirin.

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-hello-expressroute-circuit-toohello-resource-manager-deployment-model"></a>3. adım: Merhaba ExpressRoute bağlantı hattı toohello Resource Manager dağıtım modeline taşıma

Artık hazır toomove hello Klasik dağıtım modeli toohello Resource Manager dağıtım modeli, expressroute bağlantı hattı şunlardır. Devam etmeden önce sağlanan hello bilgileri gözden [hello Klasik toohello Resource Manager dağıtım modelinden bir expressroute bağlantı hattı taşıma](expressroute-move.md).

toomove hattınızı değiştirin ve aşağıdaki kod parçacığında hello çalıştırın:

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> Merhaba taşıma tamamlandıktan sonra hello önceki cmdlet'te listelenen hello yeni adı kullanılan tooaddress hello kaynak olacaktır. Merhaba hattı temelde yeniden adlandırılacak.
> 

## <a name="modify-circuit-access"></a>Bağlantı hattı erişimi değiştirme

### <a name="tooenable-expressroute-circuit-access-for-both-deployment-models"></a>tooenable her iki dağıtım modeli için ExpressRoute bağlantı hattı erişim

Klasik ExpressRoute bağlantı hattı toohello Resource Manager dağıtım modeli taşıdıktan sonra erişim tooboth dağıtım modellerini etkinleştirebilirsiniz. Aşağıdaki cmdlet'leri tooenable erişim tooboth dağıtım modellerini hello çalıştırın:

1. Merhaba hattı ayrıntıları alın.

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. "Klasik işlemleri izin ver" tooTRUE ayarlayın.

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. Merhaba hattı güncelleştirin. Bu işlemi başarıyla tamamlandıktan sonra mümkün tooview hello hattı hello Klasik dağıtım modelinde olacaktır.

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. Aşağıdaki cmdlet'i tooget hello hello expressroute bağlantı hattı ayrıntılarını hello çalıştırın. Listelenen mümkün toosee hello hizmet anahtarı olması gerekir.

  ```powershell
  get-azurededicatedcircuit
  ```

5. Artık bağlantılar toohello expressroute bağlantı hattı Resource Manager sanal ağlar için Klasik sanal ağlar ve hello Resource Manager komutları için hello Klasik dağıtım modeli komutlarını kullanarak da yönetebilirsiniz. Merhaba aşağıdaki makalelere bağlantılar toohello expressroute bağlantı hattı yönetmenize yardımcı olur:

    * [Sanal ağ tooyour expressroute bağlantı hattı hello Resource Manager dağıtım modelinde bağlantı](expressroute-howto-linkvnet-arm.md)
    * [Sanal ağ tooyour expressroute bağlantı hattı hello Klasik dağıtım modelinde bağlantı](expressroute-howto-linkvnet-classic.md)

### <a name="toodisable-expressroute-circuit-access-toohello-classic-deployment-model"></a>toodisable ExpressRoute bağlantı hattı erişim toohello Klasik dağıtım modeli

Cmdlet'leri toodisable erişim toohello Klasik dağıtım modeli izleyen hello çalıştırın.

1. Merhaba expressroute bağlantı hattı ayrıntılarını alın.

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. "Klasik işlemleri izin ver" tooFALSE ayarlayın.

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. Merhaba hattı güncelleştirin. Bu işlemi başarıyla tamamlandıktan sonra mümkün tooview hello hattı hello Klasik dağıtım modelinde olmaz.

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a>Sonraki adımlar

* [Oluşturma ve expressroute bağlantı hattı için yönlendirmeyi değiştirme](expressroute-howto-routing-arm.md)
* [Sanal ağ tooyour expressroute bağlantı hattı bağlantı](expressroute-howto-linkvnet-arm.md)
