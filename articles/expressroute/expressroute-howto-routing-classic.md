---
title: "Nasıl tooconfigure (eşleme) bir expressroute bağlantı hattı için yönlendirmeyi: Azure: Klasik | Microsoft Docs"
description: "Bu makalede, oluşturma ve sağlama hello özel, genel ve Microsoft bir expressroute bağlantı hattı eşlemesi hello adım adım anlatılmaktadır. Bu makalede ayrıca nasıl toocheck hello durumu, güncelleştirme veya bağlantı hattınız için eşlemeleri silme gösterilmektedir."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: a4bd39d2-373a-467a-8b06-36cfcc1027d2
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: dc5bcc4b86c3bc965a88281b6c2a660f3bc58eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a>Oluşturma ve bir expressroute bağlantı hattı (Klasik) için eşleme değiştirme
> [!div class="op_single_selector"]
> * [Azure portal](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [Azure CLI](howto-routing-cli.md)
> * [Video - özel eşliği](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [Video - ortak eşleme](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [Video - Microsoft eşlemesi](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell (klasik)](expressroute-howto-routing-classic.md)
> 

Bu makalede hello adımları toocreate anlatılmaktadır ve PowerShell ve hello Klasik dağıtım modeli kullanarak bir expressroute için yönlendirme yapılandırması yönetin. Merhaba adımları de nasıl toocheck hello durumu, güncelleştirme veya silin ve bir expressroute bağlantı hattı için eşlemeler yetkisini kaldırma gösterilir.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Azure dağıtım modelleri hakkında**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]


## <a name="configuration-prerequisites"></a>Yapılandırma önkoşulları
* Hello Azure Hizmet Yönetimi (SM) PowerShell cmdlet'lerinin en son sürümünü hello gerekir. Daha fazla bilgi için bkz: [Azure PowerShell cmdlet'leri ile çalışmaya başlama](/powershell/azure/overview).  
* Merhaba gözden geçirdiğinizden emin olun [Önkoşullar](expressroute-prerequisites.md) hello sayfasında [yönlendirme gereksinimleri](expressroute-routing.md) sayfası ve hello [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce sayfasında.
* Etkin bir ExpressRoute bağlantı hattınızın olması gerekir. Çok olarak Hello yönergeleri[bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-classic.md) ve devam etmeden önce bağlantı sağlayıcınız tarafından etkinleştirilen hello hattı sahip. Merhaba expressroute bağlantı hattı, aşağıda açıklanan toobe mümkün toorun hello cmdlet'leri için sağlanmış ve etkin durumda olması gerekir.

> [!IMPORTANT]
> Bu yönergeler yalnızca Katman 2 bağlantı hizmetleri sunan hizmet sağlayıcıları ile oluşturulan toocircuits geçerlidir. Yönetilen Katman 3 hizmetleri (genellikle MPLS gibi bir IPVPN) sunan bir hizmet sağlayıcısı kullanıyorsanız, bağlantı sağlayıcınız yönlendirmeyi sizin için yapılandırır ve yönetir.
> 
> 

Bir ExpressRoute bağlantı hattı için bir, iki veya üç eşlemenin tamamını (Azure özel, Azure ortak ve Microsoft) yapılandırabilirsiniz. Eşlemeleri seçtiğiniz herhangi bir sırayla yapılandırabilirsiniz. Bununla birlikte, her eşleme birer birer başlangıç yapılandırmasını tamamlayın emin olmanız gerekir.


### <a name="log-in-tooyour-azure-account-and-select-a-subscription"></a>Tooyour Azure hesabı oturum ve bir abonelik seçin
1. Yükseltilmiş haklarla PowerShell Konsolunuzu açın ve tooyour hesap bağlanın. Bağlandığınız örnek toohelp aşağıdaki hello kullan:

        Login-AzureRmAccount

2. Merhaba hesabının Hello abonelikleri kontrol edin.

        Get-AzureRmSubscription

3. Birden fazla aboneliğiniz varsa, toouse istediğiniz hello aboneliği seçin.

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. Ardından, aşağıdaki cmdlet'i tooadd hello Azure aboneliği tooPowerShell hello Klasik dağıtım modeli için kullanın.

        Add-AzureAccount


## <a name="azure-private-peering"></a>Azure özel eşlemesi
Bu bölümde nasıl toocreate, alma, güncelleştirme ve hello bir expressroute bağlantı hattı için Azure özel eşleme yapılandırmasını silme hakkında yönergeler sağlar. 

### <a name="toocreate-azure-private-peering"></a>Azure özel eşleme toocreate
1. **ExpressRoute için Hello PowerShell modülünü içeri aktarın.**
   
    Merhaba ExpressRoute cmdlet'lerini kullanmaya sipariş toostart hello PowerShell oturumunda hello Azure ve ExpressRoute modülleri almanız gerekir. Çalışma hello aşağıdaki tooimport hello Azure ve ExpressRoute modülleri hello PowerShell oturumuna komutları.  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **Bir expressroute bağlantı hattı oluşturun.**
   
    Merhaba yönergeleri toocreate izleyin bir [expressroute bağlantı hattı](expressroute-howto-circuit-classic.md) ve hello bağlantı sağlayıcı tarafından sağlanan sahip. Bağlantı sağlayıcınız yönetilen Katman 3 Hizmetleri sunuyorsa, bağlantı sağlayıcısı tooenable Azure sizin için eşlemeyi özel isteyebilir. Bu durumda, hello sonraki bölümlerde listelenen toofollow yönergeleri gerekmez. Ancak, bağlantı sağlayıcınız yönlendirmeyi sizin için hattınızı oluşturduktan sonra yönetmiyorsa aşağıdaki hello yönergeleri izleyin. 
3. **Merhaba ExpressRoute bağlantı hattı tooensure sağlandığından denetleyin.**
   
    Merhaba expressroute bağlantı hattı sağlanan ve ayrıca etkinleştirilirse toosee işaretlemeniz gerekir. Merhaba örneğe bakın.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Merhaba hattı hazırlandı ve etkin gösterdiğinden emin olun. Seçili değilse, bağlantı sağlayıcısı tooget ile hattı gerekli toohello durum ve duruma çalışır.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Merhaba bağlantı hattı için Azure özel eşlemesini yapılandırın.**
   
    Merhaba sonraki adımlara devam etmeden önce aşağıdaki öğelerindeki hello sahip olduğunuzdan emin olun:
   
   * Bir/30 alt ağı hello birincil bağlantı için. Bu, sanal ağlar için ayrılmış herhangi bir adres alanının parçası olmamalıdır.
   * Bir/30 alt ağı hello ikincil bağlantı için. Bu, sanal ağlar için ayrılmış herhangi bir adres alanının parçası olmamalıdır.
   * Geçerli bir VLAN kimliği tooestablish bu eşlemenin. Hiçbir diğer eşliği emin hello devredeki aynı VLAN kimliğini kullanan hello
   * Eşleme için AS numarası. 2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz. Bu eşleme için özel bir AS numarası kullanabilirsiniz. 65515’i kullanmadığınızdan emin olun.
   * Toouse birini seçerseniz bir MD5 karma değeri. **Bu isteğe bağlıdır**.
     
    Bağlantı hattınız için Azure özel eşleme cmdlet tooconfigure aşağıdaki hello çalıştırabilirsiniz.
     
        Yeni AzureBGPPeering - AccessType özel - ServiceKey "***" - PrimaryPeerSubnet "10.0.0.0/30" - SecondaryPeerSubnet "10.0.0.4/30" - PeerAsn 1234 - Vlanıd 100
     
    Bir MD5 karma değeri toouse seçerseniz, aşağıdaki hello cmdlet'ini kullanabilirsiniz.
     
        Yeni AzureBGPPeering - AccessType özel - ServiceKey "***" - PrimaryPeerSubnet "10.0.0.0/30" - SecondaryPeerSubnet "10.0.0.4/30" - PeerAsn 1234 - Vlanıd 100 - SharedKey "A1B2C3D4"
     
     > [!IMPORTANT]
     > AS numaranızı müşteri ASN’si değil eşleme ASN’si olarak belirttiğinizden emin olun.
     > 
     > 

### <a name="tooview-azure-private-peering-details"></a>tooview Azure özel eşleme ayrıntıları
Hello aşağıdaki cmdlet'i kullanarak yapılandırma ayrıntılarını alabilirsiniz

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100


### <a name="tooupdate-azure-private-peering-configuration"></a>Azure özel eşleme yapılandırmasını tooupdate
Cmdlet aşağıdaki hello kullanarak hello yapılandırmasını herhangi bir bölümünü güncelleştirebilirsiniz. Merhaba aşağıdaki örnekte, hello hello hattının VLAN kimliği 100 too500 güncelleştiriliyor.

    Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"

### <a name="toodelete-azure-private-peering"></a>Azure özel eşleme toodelete
Hello aşağıdaki cmdlet'i çalıştırarak eşleme yapılandırmanızı kaldırabilirsiniz.

> [!WARNING]
> Bu cmdlet'i çalıştırmadan önce tüm sanal ağları expressroute bağlantı hattı hello bağlantısız olduğundan emin olmalısınız. 
> 
> 

    Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"


## <a name="azure-public-peering"></a>Azure ortak eşleme
Bu bölümde, nasıl toocreate, alma, güncelleştirme ve hello bir expressroute bağlantı hattı için Azure ortak eşleme yapılandırmasını silme hakkında yönergeler sağlar.

### <a name="toocreate-azure-public-peering"></a>Azure ortak eşleme toocreate
1. **ExpressRoute için Hello PowerShell modülünü içeri aktarın.**
   
    Merhaba ExpressRoute cmdlet'lerini kullanmaya sipariş toostart hello PowerShell oturumunda hello Azure ve ExpressRoute modülleri almanız gerekir. Çalışma hello aşağıdaki tooimport hello Azure ve ExpressRoute modülleri hello PowerShell oturumuna komutları. 
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **ExpressRoute bağlantı hattı oluşturma**
   
    Merhaba yönergeleri toocreate izleyin bir [expressroute bağlantı hattı](expressroute-howto-circuit-classic.md) ve hello bağlantı sağlayıcı tarafından sağlanan sahip. Bağlantı sağlayıcınız yönetilen Katman 3 Hizmetleri sunuyorsa, bağlantı sağlayıcısı tooenable Azure sizin için eşlemeyi genel isteyebilir. Bu durumda, hello sonraki bölümlerde listelenen toofollow yönergeleri gerekmez. Ancak, bağlantı sağlayıcınız yönlendirmeyi sizin için hattınızı oluşturduktan sonra yönetmiyorsa aşağıdaki hello yönergeleri izleyin.
3. **ExpressRoute bağlantı hattı tooensure sağlandığından denetleyin**
   
    Merhaba expressroute bağlantı hattı sağlanan ve ayrıca etkinleştirilirse toosee işaretlemeniz gerekir. Merhaba örneğe bakın.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Merhaba hattı hazırlandı ve etkin gösterdiğinden emin olun. Seçili değilse, bağlantı sağlayıcısı tooget ile hattı gerekli toohello durum ve duruma çalışır.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Merhaba bağlantı hattı için Azure ortak eşlemesini yapılandırın**
   
    Devam etmeden önce aşağıdaki bilgilerle hello olduğundan emin olun.
   
   * Bir/30 alt ağı hello birincil bağlantı için. Bu geçerli bir ortak IPv4 öneki olmalıdır.
   * Bir/30 alt ağı hello ikincil bağlantı için. Bu geçerli bir ortak IPv4 öneki olmalıdır.
   * Geçerli bir VLAN kimliği tooestablish bu eşlemenin. Hiçbir diğer eşliği emin hello devredeki aynı VLAN kimliğini kullanan hello
   * Eşleme için AS numarası. 2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.
   * Toouse birini seçerseniz bir MD5 karma değeri. **Bu isteğe bağlıdır**.
     
    Bağlantı hattınız için Azure ortak eşleme cmdlet tooconfigure aşağıdaki hello çalıştırabilirsiniz
     
        Yeni AzureBGPPeering - AccessType ortak - ServiceKey "***" - PrimaryPeerSubnet "131.107.0.0/30" - SecondaryPeerSubnet "131.107.0.4/30" - PeerAsn 1234 - Vlanıd 200
     
    Bir MD5 karma değeri toouse seçerseniz hello cmdlet'i kullanabilirsiniz
     
        Yeni AzureBGPPeering - AccessType ortak - ServiceKey "***" - PrimaryPeerSubnet "131.107.0.0/30" - SecondaryPeerSubnet "131.107.0.4/30" - PeerAsn 1234 - Vlanıd 200 - SharedKey "A1B2C3D4"
     
     > [!IMPORTANT]
     > AS numaranızı müşteri ASN’si değil eşleme ASN’si olarak belirttiğinizden emin olun.
     > 
     > 

### <a name="tooview-azure-public-peering-details"></a>tooview Azure genel eşliği ayrıntıları
Hello aşağıdaki cmdlet'i kullanarak yapılandırma ayrıntılarını alabilirsiniz

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 131.107.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 131.107.0.4/30
    State                          : Enabled
    VlanId                         : 200


### <a name="tooupdate-azure-public-peering-configuration"></a>Azure ortak eşleme yapılandırmasını tooupdate
Cmdlet aşağıdaki hello kullanarak hello yapılandırmasını herhangi bir bölümünü güncelleştirebilirsiniz

    Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"

Merhaba hello hattının VLAN kimliği 200 too600 örnek yukarıda hello içinde gelen güncelleştiriliyor.

### <a name="toodelete-azure-public-peering"></a>Azure ortak eşleme toodelete
Hello aşağıdaki cmdlet'i çalıştırarak eşleme yapılandırmanızı kaldırabilirsiniz

    Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

## <a name="microsoft-peering"></a>Microsoft eşlemesi
Bu bölümde, nasıl toocreate, alma, güncelleştirme ve bir expressroute bağlantı hattı için Microsoft eşleme yapılandırmasını hello silme hakkında yönergeler sağlar. 

### <a name="toocreate-microsoft-peering"></a>toocreate Microsoft eşlemesi
1. **ExpressRoute için Hello PowerShell modülünü içeri aktarın.**
   
    Merhaba ExpressRoute cmdlet'lerini kullanmaya sipariş toostart hello PowerShell oturumunda hello Azure ve ExpressRoute modülleri almanız gerekir. Çalışma hello aşağıdaki tooimport hello Azure ve ExpressRoute modülleri hello PowerShell oturumuna komutları.  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **ExpressRoute bağlantı hattı oluşturma**
   
    Merhaba yönergeleri toocreate izleyin bir [expressroute bağlantı hattı](expressroute-howto-circuit-classic.md) ve hello bağlantı sağlayıcı tarafından sağlanan sahip. Bağlantı sağlayıcınız yönetilen Katman 3 Hizmetleri sunuyorsa, bağlantı sağlayıcısı tooenable Azure sizin için eşlemeyi özel isteyebilir. Bu durumda, hello sonraki bölümlerde listelenen toofollow yönergeleri gerekmez. Ancak, bağlantı sağlayıcınız yönlendirmeyi sizin için hattınızı oluşturduktan sonra yönetmiyorsa aşağıdaki hello yönergeleri izleyin.
3. **ExpressRoute bağlantı hattı tooensure sağlandığından denetleyin**
   
    Merhaba expressroute bağlantı hattı hazırlandı ve etkin durumda ise toosee işaretlemeniz gerekir.
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    Merhaba hattı hazırlandı ve etkin gösterdiğinden emin olun. Seçili değilse, bağlantı sağlayıcısı tooget ile hattı gerekli toohello durum ve duruma çalışır.
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **Microsoft eşlemesini Hello bağlantı hattı için yapılandırın**
   
    Devam etmeden önce bilgilerini aşağıdaki hello sahip olduğunuzdan emin olun.
   
   * Bir/30 alt ağı hello birincil bağlantı için. Bu size ait ve bir RIR / IRR içinde kayıtlı bir geçerli ortak IPv4 ön eki olmalıdır.
   * Bir/30 alt ağı hello ikincil bağlantı için. Bu size ait ve bir RIR / IRR içinde kayıtlı bir geçerli ortak IPv4 ön eki olmalıdır.
   * Geçerli bir VLAN kimliği tooestablish bu eşlemenin. Hiçbir diğer eşliği emin hello devredeki aynı VLAN kimliğini kullanan hello
   * Eşleme için AS numarası. 2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.
   * Tanıtılan önekler: listesini sağlamanız gerekir tüm ön eklerin hello BGP oturumu üzerinden tooadvertise planlayın. Yalnızca ortak IP adresi ön ekleri kabul edilir. Toosend ön ek kümesi planlıyorsanız, virgülle ayrılmış bir liste gönderebilirsiniz. Bu ön eklerin bir RIR içinde kayıtlı tooyou olmalıdır / IRR.
   * Müşteri ASN'si: eşleme AS numarasına kayıtlı toohello olmayan önekleri reklam, kayıtlı oldukları numara toowhich hello belirtebilirsiniz. **Bu isteğe bağlıdır**.
   * Yönlendirme kayıt defteri adı: Merhaba RIR belirtebilirsiniz / hangi hello karşı AS numarası ve önekleri IRR kayıtlı.
   * Toouse birini seçerseniz bir MD5 karma değeri. **Bu isteğe bağlıdır.**
     
    Bağlantı hattınız için cmdlet tooconfigure Microsoft pering aşağıdaki hello çalıştırabilirsiniz
     
        Yeni AzureBGPPeering - AccessType Microsoft - ServiceKey "***" - PrimaryPeerSubnet "131.107.0.0/30" - SecondaryPeerSubnet "131.107.0.4/30" - Vlanıd 300 - PeerAsn 1234 - CustomerAsn 2245 - AdvertisedPublicPrefixes "123.0.0.0/30" - RoutingRegistryName "ARIN" - SharedKey "A1B2C3D4"

### <a name="tooview-microsoft-peering-details"></a>tooview Microsoft eşleme ayrıntıları
Hello aşağıdaki cmdlet'i kullanarak yapılandırma ayrıntılarını alabilirsiniz.

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 123.0.0.0/30
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 2245
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : ARIN
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 300


### <a name="tooupdate-microsoft-peering-configuration"></a>tooupdate Microsoft eşleme yapılandırması
Cmdlet aşağıdaki hello kullanarak hello yapılandırmasını herhangi bir bölümünü güncelleştirebilirsiniz.

    Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="toodelete-microsoft-peering"></a>toodelete Microsoft eşlemesi
Hello aşağıdaki cmdlet'i çalıştırarak eşleme yapılandırmanızı kaldırabilirsiniz.

    Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

## <a name="next-steps"></a>Sonraki adımlar
Ardından, [VNet tooan expressroute bağlantı hattı bağlantı](expressroute-howto-linkvnet-classic.md).

* İş akışları hakkında daha fazla bilgi için bkz: [ExpressRoute iş akışları](expressroute-workflows.md).
* Bağlantı hattı eşlemesi hakkında daha fazla bilgi için bkz. [ExpressRoute bağlantı hattı ve yönlendirme etki alanları](expressroute-circuit-peerings.md).

