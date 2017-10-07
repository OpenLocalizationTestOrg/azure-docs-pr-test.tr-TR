---
title: "Sanal ağ tooan expressroute bağlantı hattı bağlantı: PowerShell: Klasik: Azure | Microsoft Docs"
description: "Bu belge nasıl hello Klasik dağıtım modeli ve PowerShell kullanarak sanal toolink (Vnet'ler) tooExpressRoute devreler ağları genel bir bakış sağlar."
services: expressroute
documentationcenter: na
author: ganesr
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 9b53fd72-9b6b-4844-80b9-4e1d54fd0c17
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/28/2017
ms.author: ganesr
ms.openlocfilehash: 6b8a01dcd4bbb9618ec3dd438cf0107538fb2a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-powershell-classic"></a>PowerShell (Klasik) kullanarak bir sanal ağ tooan expressroute bağlantı hattı Bağlan
> [!div class="op_single_selector"]
> * [Azure portal](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Azure CLI](howto-linkvnet-cli.md)
> * [Video - Azure portalı](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (klasik)](expressroute-howto-linkvnet-classic.md)
>

Bu makalede hello Klasik dağıtım modeli ve PowerShell kullanarak sanal ağlar (Vnet'ler) tooAzure ExpressRoute bağlantı hatları bağlama yardımcı olur. Sanal ağlar ya da içinde olabileceği hello aynı abonelik veya başka bir abonelik parçası olabilir.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Azure dağıtım modelleri hakkında**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a>Yapılandırma önkoşulları
1. Hello Azure PowerShell modüllerinin en son sürümünü hello gerekir. Merhaba PowerShell bölümünü hello hello son PowerShell modülleri indirebilirsiniz [Azure indirmeler sayfası](https://azure.microsoft.com/downloads/). Merhaba yönergeleri izleyin [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) nasıl hakkında adım adım yönergeler için tooconfigure bilgisayar toouse hello Azure PowerShell modüllerinizi.
2. Tooreview hello gereksinim [Önkoşullar](expressroute-prerequisites.md), [yönlendirme gereksinimleri](expressroute-routing.md), ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.
3. Etkin bir ExpressRoute bağlantı hattınızın olması gerekir.
   * Çok olarak Hello yönergeleri[bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-classic.md) ve bağlantı sağlayıcınız hello hattı etkinleştirin.
   * Bağlantı hattınız için yapılandırılmış Azure özel eşleme olduğundan emin olun. Merhaba bkz [yönlendirmeyi yapılandırma](expressroute-howto-routing-classic.md) yönlendirme yönergeleri için makalenin.
   * Azure özel eşleme yapılandırılır ve uçtan uca bağlantı etkinleştirebilmeniz için ağınız ve Microsoft arasında hello BGP eşliği yukarı olduğundan emin olun.
   * Bir sanal ağ ve oluşturulan ve tam olarak sağlanan bir sanal ağ geçidi olmalıdır. Çok olarak Hello yönergeleri[sanal ağ ExpressRoute için yapılandırma](expressroute-howto-vnet-portal-classic.md).

Too10 sanal ağlar tooan expressroute bağlantı hattı bağlayabilirsiniz. Tüm sanal ağları hello olmalıdır aynı coğrafi bölge. Çok sayıda sanal ağlar tooyour expressroute bağlantı hattı bağlantı veya diğer coğrafi bölgelerde hello ExpressRoute premium eklentisi etkinse olan sanal ağlara bağlantı. Merhaba denetleyin [SSS](expressroute-faqs.md) hello premium eklentisi hakkında daha fazla ayrıntı için.

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>Merhaba sanal bir ağa bağlan aynı abonelik tooa hattı
Cmdlet aşağıdaki hello kullanarak bir sanal ağ tooan expressroute bağlantı hattı bağlayabilirsiniz. Bu hello sanal ağ geçidi oluşturulur ve hello cmdlet'i çalıştırmadan önce bağlama için hazır olduğundan emin olun.

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
    Provisioned

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>Farklı bir abonelik tooa hattı sanal bir ağa bağlan
Bir expressroute bağlantı hattı birden çok abonelik paylaşabilirsiniz. Aşağıdaki şekilde hello arasında birden çok abonelik basit bir ExpressRoute bağlantı hatları için nasıl paylaşım works'ün şematik gösterir.

Her hello küçük bulutların hello büyük bulut içinde bir kuruluş içindeki toodifferent bölümler ait kullanılan toorepresent abonelikleri içindir. Kendi Hizmetleri--ancak hello Departmanlar dağıtma tek bir ExpressRoute bağlantı hattı tooconnect geri tooyour şirket içi ağ paylaşımı için her hello kuruluşunuz içinde hello bölümlerin kendi aboneliği kullanabilirsiniz. Tek bir bölüm (Bu örnekte: BT) hello expressroute bağlantı hattı sahip olabilir. Merhaba kuruluştaki diğer abonelikler hello expressroute bağlantı hattı kullanabilirsiniz.

> [!NOTE]
> Bağlantı ve bant genişliği ücretleri ayrılmış hello hattı için uygulanan toohello ExpressRoute bağlantı hattı sahip olacaktır. Tüm sanal ağları hello paylaşmak aynı bant genişliği.
> 
> 

![Çapraz abonelik bağlantısı](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a>Yönetim
Merhaba *devre sahibinden* hello ExpressRoute bağlantı hattı oluşturulur hello abonelik hello yönetici/Abonelikteki olduğu. Merhaba devre sahibinden Yöneticiler/coadministrators diğer abonelikler, başvurulan tooas yetkilendirebilir *hattı kullanıcılar*, toouse hello oldukları hattı ayrılmış. Yetkileri sonra yetkili toouse hello kuruluşun ExpressRoute bağlantı hattı can hattı kullanıcılar kendi abonelik toohello expressroute bağlantı hattı hello sanal ağa bağlayın.

Merhaba devre sahibinden hello güç toomodify ve revoke yetkilerini herhangi bir zamanda sahiptir. Bir yetkilendirme iptal erişimini iptal edildi hello abonelikten silinen tüm bağlantılar neden olur.

### <a name="circuit-owner-operations"></a>Bağlantı hattı sahibi işlemleri

**Bir yetkilendirme oluşturma**

Merhaba devre sahibinden yetkilendirir hello Yöneticiler diğer abonelikler toouse hello belirtilen hattı. Aşağıdaki örneğine hello hello yöneticisinin hello devrenin (Contoso BT) başka bir abonelik (geliştirme, Test) toolink tootwo sanal ağlar toohello hattı yukarı hello Yöneticisi sağlar. Merhaba Contoso BT yöneticisinin bu hello geliştirme, Test Microsoft kimliği belirtilerek sağlar. e-posta toohello Microsoft kimliği belirtildi. Hello cmdlet göndermez Merhaba devre sahibinden gereken tooexplicitly yetkilendirme hello diğer abonelik sahibi tamamlandığında hello bildirin.

    New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : **********************************
    MicrosoftIds        : devtest@contoso.com
    Used                : 0

**Yetkilerini gözden geçirme**

Merhaba devre sahibinden hello aşağıdaki cmdlet'i çalıştırarak belirli bir bağlantı hattı üzerinde verilen tüm yetkilerini gözden geçirebilirsiniz:

    Get-AzureDedicatedCircuitLinkAuthorization -ServiceKey: "**************************"

    Description         : EngineeringTeam
    Limit               : 3
    LinkAuthorizationId : ####################################
    MicrosoftIds        : engadmin@contoso.com
    Used                : 1

    Description         : MarketingTeam
    Limit               : 1
    LinkAuthorizationId : @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    MicrosoftIds        : marketingadmin@contoso.com
    Used                : 0

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : salesadmin@contoso.com
    Used                : 2


**Yetkilerini güncelleştiriliyor**

Merhaba devre sahibinden yetkilerini cmdlet'i aşağıdaki hello kullanarak değiştirebilirsiniz:

    Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5

    Description         : Dev-Test Links
    Limit               : 5
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : devtest@contoso.com
    Used                : 0


**Yetkilerini silme**

Merhaba devre sahibinden revoke/yetkilerini toohello kullanıcı hello aşağıdaki cmdlet'i çalıştırarak silme:

    Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"


### <a name="circuit-user-operations"></a>Bağlantı hattı kullanıcı işlemleri

**Yetkilerini gözden geçirme**

Hello hattı kullanıcı yetkilerini cmdlet'i aşağıdaki hello kullanarak gözden geçirebilirsiniz:

    Get-AzureAuthorizedDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : ContosoIT
    Location                         : Washington DC
    MaximumAllowedLinks              : 2
    ServiceKey                       : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled
    UsedLinks                        : 0

**Bağlantı yetkilerini itibaren**

Merhaba hattı kullanıcı cmdlet tooredeem aşağıdaki hello bağlantı yetkilendirme çalıştırabilirsiniz:

    New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'

    State VnetName
    ----- --------
    Provisioned SalesVNET1

Yeni bağlantılı hello abonelik hello sanal ağ için bu komutu çalıştırın:

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"

## <a name="next-steps"></a>Sonraki adımlar
ExpressRoute hakkında daha fazla bilgi için bkz: Merhaba [ExpressRoute SSS](expressroute-faqs.md).

