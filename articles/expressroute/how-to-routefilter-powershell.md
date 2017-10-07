---
title: "Azure ExpressRoute Microsoft eşliği için rota filtrelerini yapılandırın: PowerShell | Microsoft Docs"
description: "Bu makalede Microsoft PowerShell kullanarak Peering için nasıl tooconfigure yol filtreleri açıklanır"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 395bcf7d6ad43c643ff041b154f8e4b797083e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a>Microsoft eşlemesi için rota filtreleri yapılandırma

Yol filtreleri şekilde tooconsume bir alt kümesini Microsoft eşleme yoluyla desteklenen hizmetler şunlardır. Bu makale Yardım yapılandırmak ve ExpressRoute bağlantı hatları için yol filtreleri yönetmek Hello adımları.

Dynamics 365 Hizmetleri ve işletme için Office 365 Hizmetleri Exchange Online, SharePoint Online ve Skype gibi hello Microsoft eşleme aracılığıyla erişilebilir. Microsoft eşlemesi bir expressroute bağlantı hattı yapılandırıldığında, tüm ön eklerin ilgili toothese Hizmetleri oluşturulmuş hello BGP oturumları bildirilir. BGP topluluk değeri hello önek sunulan ekli tooevery önek tooidentify hello hizmetidir. Merhaba BGP topluluk değerlerini ve eşlemek için hello Hizmetleri listesi için bkz: [BGP toplulukları](expressroute-routing.md#bgp).

Bağlantı tooall Hizmetleri gerektiriyorsa, çok sayıda önekleri BGP bildirilir. Bu, ağınızdaki yönlendiricileri tarafından tutulan hello yol tablolarını hello boyutunu önemli ölçüde artırır. Yalnızca bir alt kümesini Hizmetleri Microsoft eşliği ile sunulan tooconsume planlıyorsanız, yol tablolarınız iki yolla hello boyutunu azaltabilirsiniz. Şunları yapabilirsiniz:

- İstenmeyen önekleri BGP toplulukları yol filtreleri uygulayarak filtreleyin. Bu standart bir ağ uygulaması ve birçok ağ içinde yaygın olarak kullanılır.

- Rota filtrelerini tanımlayın ve bunları tooyour expressroute bağlantı hattı uygulayabilirsiniz. Bir rota filtre hello listesi sağlar hizmetlerini, yeni bir kaynak Microsoft eşleme yoluyla tooconsume planlamaktır. ExpressRoute yönlendiriciler yalnızca hello rota filtrede tanımlanan toohello Hizmetleri ait önekleri hello listesi gönderir.

### <a name="about"></a>Rota filtreler hakkında

Microsoft eşlemesi, expressroute bağlantı hattı üzerinde yapılandırıldığında, hello Microsoft sınır yönlendiricileri hello sınır yönlendiricileri (sizin ya da bağlantı sağlayıcınızın) BGP oturumları çifti oluşturun. Yol yok tanıtılan tooyour ağ tabanlıdır. tooenable yol tanıtımları tooyour ağ, bir rota filtre ilişkilendirmeniz gerekir.

Bir rota filtre expressroute bağlantı hattı 's Microsoft eşleme yoluyla tooconsume istediğiniz hizmetleri tanımlamanıza olanak sağlar. Tüm hello BGP topluluk değerlerini temelde beyaz listesi var. Bir rota filtre kaynağı tanımlandı ve tooan expressroute bağlantı hattı bağlı sonra toohello BGP topluluk değerlerini eşlemek tüm ön eklerin tanıtılan tooyour ağ tabanlıdır.

Office 365 Hizmetleri bunlardaki ile toobe mümkün tooattach yol filtreleri, yetkilendirme tooconsume Office 365 Hizmetleri ExpressRoute aracılığıyla olması gerekir. ExpressRoute aracılığıyla yetkili tooconsume Office 365 Hizmetleri olmayan hello işlemi tooattach yol filtreleri başarısız olur. Merhaba Yetkilendirme işlemi hakkında daha fazla bilgi için bkz: [Office 365 için Azure ExpressRoute](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd). Bağlantı tooDynamics 365 Hizmetleri, önceki tüm yetkilendirme gerektirmez.

> [!IMPORTANT]
> Önceki tooAugust 1 yapılandırılmış olan ExpressRoute bağlantı hatları Microsoft eşliği, yol filtreleri tanımlanmamış olsa bile 2017 Microsoft eşleme aracılığıyla tanıtılan tüm hizmet ön eklerin sahip olur. Ve 1 Ağustos 2017 sonrasında yapılandırılmış ExpressRoute bağlantı hatları, Microsoft eşlemesi sahip olmaz tüm ön eklerin rota filtre bağlanana kadar tanıtılan toohello hattı.
> 
> 

### <a name="workflow"></a>İş akışı

Microsoft eşleme aracılığıyla toobe mümkün toosuccessfully tooservices bağlanma, hello aşağıdaki yapılandırma adımları tamamlamanız gerekir:

- Microsoft sağlanan eşlemesini sahip etkin bir expressroute olması gerekir. Bu görevleri yönergeleri tooaccomplish aşağıdaki hello kullanabilirsiniz:
  - [Bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-arm.md) ve devam etmeden önce bağlantı sağlayıcınız tarafından etkinleştirilen hello hattı sahip. Hello expressroute bağlantı hattının sağlanmış ve etkin durumda olması gerekir.
  - [Microsoft eşlemesi oluşturmak](expressroute-circuit-peerings.md) doğrudan hello BGP oturumu yönetiyorsanız. Veya, bağlantı sağlayıcınız hattınız için eşlemesini Microsoft sağlamak.

-  Oluşturma ve bir rota filtre yapılandırmanız gerekir.
    - Tanımlamak hello Microsoft eşleme yoluyla tooconsume ile Hizmetleri
    - Merhaba BGP topluluk değerlerini hello servisleri ile ilişkili olan listesini belirlemesini
    - Bir kural tooallow hello önek listesi eşleşen hello BGP topluluk değerlerini oluşturun

-  Merhaba rota filtre toohello expressroute bağlantı hattı ilişkilendirmeniz gerekir.

## <a name="before-you-begin"></a>Başlamadan önce

Yapılandırmaya başlamadan önce aşağıdaki ölçütleri hello karşıladığından emin olun:

 - Merhaba hello Azure Resource Manager PowerShell cmdlet'lerinin en son sürümünü yükleyin. Daha fazla bilgi için bkz: [yükleyin ve Azure PowerShelll yapılandırma](/powershell/azure/install-azurerm-ps).

  > [!NOTE]
  > Merhaba PowerShell Galerisi yerine hello yükleyici kullanarak Hello en son sürümünü yükleyin. Merhaba, yükleyici şu anda gerekli hello cmdlet'leri desteklemez.
  > 

 - Gözden geçirme hello [Önkoşullar](expressroute-prerequisites.md) ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.

 - Etkin bir ExpressRoute bağlantı hattınızın olması gerekir. Çok olarak Hello yönergeleri[bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-arm.md) ve devam etmeden önce bağlantı sağlayıcınız tarafından etkinleştirilen hello hattı sahip. Hello expressroute bağlantı hattının sağlanmış ve etkin durumda olması gerekir.

 - Etkin bir Microsoft eşlemesi olması gerekir. Bölümündeki yönergeleri izleyin [oluşturma ve eşleme yapılandırmasını değiştirme](expressroute-circuit-peerings.md)

### <a name="log-in-tooyour-azure-account"></a>Azure hesabı tooyour içinde oturum

Bu yapılandırmaya başlamadan önce tooyour Azure hesabı oturum açmanız gerekir. Merhaba cmdlet hello Azure hesabınızda oturum açma kimlik bilgilerini ister. Kullanılabilir tooAzure PowerShell şekilde oturum açtıktan sonra hesap ayarlarınızı indirir.

PowerShell Konsolunuzu yükseltilmiş ayrıcalıklarla açın ve tooyour hesap bağlanın. Bağlandığınız örnek toohelp aşağıdaki hello kullan:

```powershell
Login-AzureRmAccount
```

Birden çok Azure aboneliğiniz varsa, hello hesabının hello abonelikleri kontrol edin.

```powershell
Get-AzureRmSubscription
```

Merhaba abonelik toouse istediğinizi belirtin.

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <a name="prefixes"></a>1. adım. Önekleri ve BGP topluluk değerlerini listesini alma

### <a name="1-get-a-list-of-bgp-community-values"></a>1. BGP topluluk değerlerini listesini al

Cmdlet tooget hello Microsoft eşleme aracılığıyla erişilebilir hizmetleriyle ilişkili BGP topluluk değerlerini listesi aşağıdaki hello kullanın ve bunlarla ilişkilendirilmiş önekleri listesini hello:

```powershell
Get-AzureRmBgpServiceCommunity
```
### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a>2. Merhaba değerler listesini toouse istiyor olun

BGP topluluk değerlerini istediğiniz listesini toouse hello rota filtrede olun. Örnek olarak, hello Dynamics 365 Hizmetleri için BGP topluluk değeri 12076:5040 ' dir.

## <a name="filter"></a>2. adım. Bir rota filtre ve bir filtre kuralı oluşturma

Bir rota filtre yalnızca bir kuralınız olabilir ve hello kural 'İzin ver' türünde olmalıdır. Bu kural, kendisiyle ilişkilendirilmiş BGP topluluk değerlerini listesini olabilir.

### <a name="1-create-a-route-filter"></a>1. Bir rota filtresi oluşturma

İlk olarak, hello rota filtre oluşturun. 'Yeni-AzureRmRouteFilter' Hello komutu yalnızca bir rota filtre kaynağı oluşturur. Hello kaynak oluşturduktan sonra ardından bir kural oluşturmak ve toohello rota filtre nesnesi ekleme gerekir. Komut toocreate aşağıdaki hello rota filtre kaynak çalıştırın:

```powershell
New-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup" -Location "West US"
```

### <a name="2-create-a-filter-rule"></a>2. Bir filtre kuralı oluşturma

Merhaba örnekte gösterildiği gibi BGP toplulukları bir dizi virgülle ayrılmış bir liste belirtebilirsiniz. Komut toocreate aşağıdaki hello yeni bir kural çalıştırın:
 
```powershell
$rule = New-AzureRmRouteFilterRuleConfig -Name "Allow-EXO-D365" -Access Allow -RouteFilterRuleType Community -CommunityList "12076:5010,12076:5040"
```

### <a name="3-add-hello-rule-toohello-route-filter"></a>3. Merhaba kural toohello rota Filtresi Ekle

Komut tooadd hello filtre kuralı toohello rota filtresi aşağıdaki hello çalıştırın:
 
```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.Rules.Add($rule)
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <a name="attach"></a>3. adım. Merhaba rota filtre tooan expressroute bağlantı hattı ekleme

Komut tooattach hello rota filtre toohello expressroute bağlantı hattı, yalnızca Microsoft eşlemesi sahip olduğu varsayılarak aşağıdaki hello çalıştırın:

```powershell
$ckt.Peerings[0].RouteFilter = $routefilter 
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="getproperties"></a>bir rota filtre tooget hello özellikleri

bir rota filtre tooget hello özellikleri hello aşağıdaki adımları kullanın:

1. Komut tooget hello rota filtre kaynak aşağıdaki hello çalıştırın:

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  ```
2. Merhaba rota filtre kuralları hello aşağıdaki komutu çalıştırarak hello rota filtre kaynak için alın:

  ```powershell
  $routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
  $rule = $routefilter.Rules[0]
  ```

## <a name="updateproperties"></a>bir rota filtre tooupdate hello özellikleri

Merhaba rota filtre zaten bağlıysa, tooa hattı, güncelleştirmeleri toohello BGP topluluk listesinin otomatik olarak oluşturulan hello BGP oturumları aracılığıyla uygun önek tanıtım değişiklikleri yayar. Merhaba BGP topluluk hello aşağıdaki komutu kullanarak, rota filtre listesini güncelleştirebilirsiniz:

```powershell
$routefilter = Get-AzureRmRouteFilter -Name "RouteFilterName" -ResourceGroupName "ExpressRouteResourceGroupName"
$routefilter.rules[0].Communities = "12076:5030", "12076:5040"
Set-AzureRmRouteFilter -RouteFilter $routefilter
```

## <a name="detach"></a>toodetach bir expressroute bağlantı hattı rota filtresi

Bir rota filtre expressroute bağlantı hattı hello ayrılmış sonra hiçbir önekleri hello BGP oturumu aracılığıyla bildirilir. Komutu aşağıdaki hello kullanarak ExpressRoute devresi rota filtresinden ayırabilirsiniz:
  
```powershell
$ckt.Peerings[0].RouteFilter = $null
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="delete"></a>bir rota filtre toodelete

Delete değilse bir rota filtre tooany hattı bağlı yalnızca kullanabilirsiniz. Bu hello rota filtre olmadığından emin olun toodelete denemeden önce tooany hattı bağlı onu. Komutu aşağıdaki hello kullanarak bir rota filtre silebilirsiniz:

```powershell
Remove-AzureRmRouteFilter -Name "MyRouteFilter" -ResourceGroupName "MyResourceGroup"
```

## <a name="next-steps"></a>Sonraki adımlar

ExpressRoute hakkında daha fazla bilgi için bkz: Merhaba [ExpressRoute SSS](expressroute-faqs.md).
