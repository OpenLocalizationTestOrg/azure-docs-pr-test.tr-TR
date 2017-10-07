---
title: "Bir arada var olabilen ExpressRoute ve Siteden Siteye VPN bağlantıları yapılandırma: klasik: Azure | Microsoft Docs"
description: "Bu makalede ExpressRoute ve hello Klasik dağıtım modeli için bir arada var olabilen siteden siteye VPN bağlantısını nasıl yapılandıracağınız anlatılmaktadır."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: dcf1a5af-a289-466a-b812-0bfedbd2bda0
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: abb30fff55e8ec243f2920c5b2f70c43717755fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections-classic"></a>Birlikte bulunan ExpressRoute bağlantıları ile Siteden Siteye bağlantıları yapılandırma (klasik)
> [!div class="op_single_selector"]
> * [PowerShell - Resource Manager](expressroute-howto-coexist-resource-manager.md)
> * [PowerShell - Klasik](expressroute-howto-coexist-classic.md)
> 
> 

Merhaba özelliği tooconfigure siteden siteye VPN ve ExpressRoute sahip olmanın çeşitli avantajları vardır. ExressRoute için Güvenli Yük devretme yolu olarak siteden siteye VPN yapılandırabilir veya ExpressRoute aracılığıyla bağlanmayan siteden siteye VPN tooconnect toosites kullanın. Biz bu makalede her iki senaryoyu hello adımları tooconfigure ele alınacaktır. Bu makale toohello Klasik dağıtım modeli için geçerlidir. Bu yapılandırma hello Portalı'nda kullanılamıyor.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Azure dağıtım modelleri hakkında**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

> [!IMPORTANT]
> Aşağıdaki hello yönergeleri izlemeden önce ExpressRoute bağlantı hatlarının önceden yapılandırılmış olması gerekir. Merhaba kılavuzları çok izlediğinizden emin olun[bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-classic.md) ve [yönlendirmeyi yapılandırma](expressroute-howto-routing-classic.md) hello adımları izlemeden önce.
> 
> 

## <a name="limits-and-limitations"></a>Sınırlar ve sınırlamalar
* **Geçiş yönlendirmesi desteklenmez.** Siteden Siteye VPN aracılığıyla bağlanan yerel ağınız ve ExpressRoute aracılığıyla bağlanan yerel ağınız arasında (Azure aracılığıyla) yönlendirme yapamazsınız.
* **Noktadan siteye desteklenmez.** Noktadan siteye VPN bağlantıları toohello etkinleştiremiyor bağlı tooExpressRoute olduğu aynı sanal ağı. Noktadan siteye VPN ve ExpressRoute birlikte bulunamaz Merhaba aynı sanal ağ.
* **Zorlamalı tünel hello siteden siteye VPN ağ geçidinde etkinleştirilemez.** Yalnızca "tüm Internet'e bağlı trafik geri tooyour şirket içi ağ ExpressRoute aracılığıyla zorlayabilirsiniz".
* **Temel SKU ağ geçidi desteklenmez.** Temel SKU olmayan ağ geçidi için her iki hello kullanmalısınız [ExpressRoute ağ geçidi](expressroute-about-virtual-network-gateways.md) ve hello [VPN ağ geçidi](../vpn-gateway/vpn-gateway-about-vpngateways.md).
* **Yalnızca rota tabanlı VPN ağ geçidi desteklenir.** Rota tabanlı [VPN Gateway](../vpn-gateway/vpn-gateway-about-vpngateways.md) kullanmanız gerekir.
* **VPN ağ geçidiniz için statik rota yapılandırılmalıdır.** Yerel ağınıza bağlı tooboth ExpressRoute ve bir Site siteye VPN, bir statik yol, yerel ağ tooroute hello siteden siteye VPN bağlantısı toohello yapılandırılmış olması gerekiyor, ortak Internet.
* **İlk olarak ExpressRoute ağ geçidi yapılandırılmalıdır.** Merhaba siteden siteye VPN ağ geçidi eklemeden önce ilk hello ExpressRoute ağ geçidi oluşturmanız gerekir.

## <a name="configuration-designs"></a>Yapılandırma tasarımları
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a>Siteden siteye VPN’i ExpressRoute için bir yük devretme yolu olarak yapılandırma
Siteden siteye bir VPN bağlantısını ExpressRoute için yedek olarak yapılandırabilirsiniz. Bu, yalnızca toovirtual ağlar bağlantılı toohello Azure özel eşleme yoluna geçerlidir. Azure ortak ve Microsoft eşlemeleri aracılığıyla erişilebilen hizmetler için VPN tabanlı yük devretme çözümü yoktur. Merhaba expressroute bağlantı hattı her zaman hello birincil bağlantıdır. Yalnızca hello expressroute bağlantı hattı başarısız olursa veri hello siteden siteye VPN üzerinden akar. 

> [!NOTE]
> Zaman aynı olan iki yollar hello expressroute bağlantı hattı siteden siteye VPN üzerinden tercih edilen olmakla birlikte, Azure doğru hello paketin hedef hello uzun önek eşleştirme toochoose hello rota kullanır.
> 
> 

![Bir arada var olma](media/expressroute-howto-coexist-classic/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a>ExpressRoute aracılığıyla bağlanılmayan bir siteden siteye VPN tooconnect toosites yapılandırın
Burada bazı siteler tooAzure siteden siteye VPN üzerinden doğrudan bağlanın ve bazı sitelerin ExpressRoute üzerinden bağlanması ağınız yapılandırabilirsiniz. 

![Bir arada var olma](media/expressroute-howto-coexist-classic/scenario2.jpg)

> [!NOTE]
> Bir sanal ağı geçiş yönlendiricisi olarak yapılandıramazsınız.
> 
> 

## <a name="selecting-hello-steps-toouse"></a>Merhaba adımları toouse seçme
Bir arada var olabilen sipariş tooconfigure bağlantıları yordamları toochoose iki farklı kümesi vardır. Seçtiğiniz hello yapılandırma yordamı için tooconnect istediğiniz veya yeni bir sanal ağ toocreate istediğiniz var olan bir sanal ağ olup olmadığına bağlıdır.

* I yoksa bir VNet ve toocreate biri gerekir.
  
    Bir sanal ağ zaten sahip değilseniz, bu yordamı, hello Klasik dağıtım modeli kullanılarak ve yeni ExpressRoute ve siteden siteye VPN bağlantıları oluşturma yeni bir sanal ağ oluşturma size yol gösterir. tooconfigure, hello makale bölümdeki hello adımları [toocreate yeni bir sanal ağ ve bir arada var olabilen bağlantılar](#new).
* Zaten bir klasik dağıtım modeli VNet’im var.
  
    Mevcut bir Siteden Siteye VPN bağlantısı veya ExpressRoute bağlantısına sahip bir sanal ağınız zaten olabilir. Merhaba makale bölümüne [tooconfigure zaten olan bir VNet için aynı anda mevcut bağlantılar](#add) hello ağ geçidini silme ve ardından yeni ExpressRoute ve siteden siteye VPN bağlantıları oluşturma size yol gösterir. Hello adımları Hello yeni bağlantıları oluştururken, belirli bir sırada doldurulmalıdır unutmayın. Diğer makaleler toocreate Hello yönergeleri, ağ geçitleri ve bağlantıları kullanmayın.
  
    Bu yordamda, bir arada var olabilen bağlantılar oluşturmayı, ağ geçidi, toodelete gerektirir ve yeni ağ geçitlerini yapılandırmak. Bu, şirket içi bağlantılarınız için kapalı kalma süresi silin ve ağ geçidiniz ve bağlantıları oluşturun, ancak toomigrate gerekmez tüm sanal makineleri veya hizmetleri tooa yeni sanal ağınızın olacağı anlamına gelir. Yapılandırılmış toodo şekilde olmaları durumunda, ağ geçidi yapılandırması sırasında VM'ler ve hizmetler hello yük dengeleyici üzerinden kullanıma mümkün toocommunicate olmaya devam eder.

## <a name="new"></a>toocreate yeni bir sanal ağ ve arada var olabilen bağlantılar
Bu yordamda, bir VNet oluşturma ve bir arada var olabilen Siteden Siteye ve ExpressRoute bağlantıları oluşturma adım adım açıklanmıştır.

1. Tooinstall hello en son sürümünü hello Azure PowerShell cmdlet'lerini gerekir. Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) hello PowerShell cmdlet'lerini yükleme hakkında daha fazla bilgi. Bu yapılandırma için kullanacağınız hello cmdlet'leri ne tanımanız değerinden biraz farklı olabileceğini unutmayın. Bu yönergelerde emin toouse hello cmdlet'leri belirtilmiş. 
2. Sanal ağınız için bir şema oluşturun. Merhaba yapılandırma şeması hakkında daha fazla bilgi için bkz: [Azure Virtual Network yapılandırma şeması](https://msdn.microsoft.com/library/azure/jj157100.aspx).
   
    Şemanızı oluşturduğunuzda, aşağıdaki değerleri hello kullandığınızdan emin olun:
   
   * Merhaba hello sanal ağ ağ geçidi alt ağı/27 veya daha kısa bir önek (örneğin, /26 veya/25) olmalıdır.
   * Merhaba ağ geçidi bağlantı türü "ayrılmış" olmalıdır.
     
             <VirtualNetworkSite name="MyAzureVNET" Location="Central US">
               <AddressSpace>
                 <AddressPrefix>10.17.159.192/26</AddressPrefix>
               </AddressSpace>
               <Subnets>
                 <Subnet name="Subnet-1">
                   <AddressPrefix>10.17.159.192/27</AddressPrefix>
                 </Subnet>
                 <Subnet name="GatewaySubnet">
                   <AddressPrefix>10.17.159.224/27</AddressPrefix>
                 </Subnet>
               </Subnets>
               <Gateway>
                 <ConnectionsToLocalNetwork>
                   <LocalNetworkSiteRef name="MyLocalNetwork">
                     <Connection type="Dedicated" />
                   </LocalNetworkSiteRef>
                 </ConnectionsToLocalNetwork>
               </Gateway>
             </VirtualNetworkSite>
3. Oluşturma ve xml şeması dosyanızı yapılandırdıktan sonra hello dosyasını karşıya yükleyin. Bu, sanal ağınızı oluşturur.
   
    Cmdlet tooupload aşağıdaki hello dosyanızı hello değerini kendi değerlerinizle değiştirerek kullanın.
   
        Set-AzureVNetConfig -ConfigurationPath 'C:\NetworkConfig.xml'
4. <a name="gw"></a>ExpressRoute ağ geçidi oluşturun. Emin toospecify olması olarak hello *standart*, *HighPerformance*, veya *UltraPerformance* ve GatewayType hello *DynamicRouting*.
   
    Aşağıdaki örnek, hello değerleri kendinizinkilerle değiştirerek hello kullanın.
   
        New-AzureVNetGateway -VNetName MyAzureVNET -GatewayType DynamicRouting -GatewaySKU HighPerformance
5. Merhaba ExpressRoute ağ geçidi toohello expressroute bağlantı hattı bağlayın. Bu adımı tamamladıktan sonra şirket içi ağınız ve ExpressRoute aracılığıyla Azure arasında hello bağlantı kurulur.
   
        New-AzureDedicatedCircuitLink -ServiceKey <service-key> -VNetName MyAzureVNET
6. <a name="vpngw"></a>Ardından, Siteden Siteye VPN ağ geçidinizi oluşturun. Merhaba gatewaysku *standart*, *HighPerformance*, veya *UltraPerformance* ve hello GatewayType olmalıdır *DynamicRouting*.
   
        New-AzureVirtualNetworkGateway -VNetName MyAzureVNET -GatewayName S2SVPN -GatewayType DynamicRouting -GatewaySKU  HighPerformance
   
    Merhaba ağ geçidi kimliği ve hello ortak IP dahil olmak üzere tooretrieve hello sanal ağ ağ geçidi ayarlarını kullanabilir hello `Get-AzureVirtualNetworkGateway` cmdlet'i.
   
        Get-AzureVirtualNetworkGateway
   
        GatewayId            : 348ae011-ffa9-4add-b530-7cb30010565e
        GatewayName          : S2SVPN
        LastEventData        :
        GatewayType          : DynamicRouting
        LastEventTimeStamp   : 5/29/2015 4:41:41 PM
        LastEventMessage     : Successfully created a gateway for hello following virtual network: GNSDesMoines
        LastEventID          : 23002
        State                : Provisioned
        VIPAddress           : 104.43.x.y
        DefaultSite          :
        GatewaySKU           : HighPerformance
        Location             :
        VnetId               : 979aabcf-e47f-4136-ab9b-b4780c1e1bd5
        SubnetId             :
        EnableBgp            : False
        OperationDescription : Get-AzureVirtualNetworkGateway
        OperationId          : 42773656-85e1-a6b6-8705-35473f1e6f6a
        OperationStatus      : Succeeded
7. Bir yerel site VPN ağ geçidi varlığı oluşturun. Bu komut, şirket içi VPN ağ geçidinizi yapılandırmaz. Bunun yerine, hello genel IP gibi tooprovide hello yerel ağ geçidi ayarları sağlar ve hello Azure VPN ağ geçidi tooit bağlanabilmesi hello şirket içi adres alanı.
   
   > [!IMPORTANT]
   > Merhaba siteden siteye VPN için yerel site Hello hello netcfg içinde tanımlı değil. Bunun yerine, bu cmdlet toospecify hello yerel site parametrelerini kullanmanız gerekir. Portalı veya hello netcfg dosyasını kullanarak tanımlayamazsınız.
   > 
   > 
   
    Aşağıdaki örnek, hello değerleri kendi değerlerinizle değiştirerek hello kullanın.
   
        New-AzureLocalNetworkGateway -GatewayName MyLocalNetwork -IpAddress <MyLocalGatewayIp> -AddressSpace <MyLocalNetworkAddress>
   
   > [!NOTE]
   > Yerel ağınızda birden çok yol varsa, hepsini bir dizi olarak geçirebilirsiniz.  $MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")  
   > 
   > 

    Merhaba ağ geçidi kimliği ve hello ortak IP dahil olmak üzere tooretrieve hello sanal ağ ağ geçidi ayarlarını kullanabilir hello `Get-AzureVirtualNetworkGateway` cmdlet'i. Merhaba aşağıdaki örneğine bakın.

        Get-AzureLocalNetworkGateway

        GatewayId            : 532cb428-8c8c-4596-9a4f-7ae3a9fcd01b
        GatewayName          : MyLocalNetwork
        IpAddress            : 23.39.x.y
        AddressSpace         : {10.1.2.0/24}
        OperationDescription : Get-AzureLocalNetworkGateway
        OperationId          : ddc4bfae-502c-adc7-bd7d-1efbc00b3fe5
        OperationStatus      : Succeeded


1. Yerel VPN cihaz tooconnect toohello yeni ağ geçidinizi yapılandırın. VPN Cihazınızı yapılandırırken 6. adımda alınan hello bilgileri kullanın. VPN cihazını yapılandırma hakkında daha fazla bilgi için bkz. [VPN Cihazı Yapılandırma](../vpn-gateway/vpn-gateway-about-vpn-devices.md).
2. Bağlantı hello siteden siteye VPN ağ geçidinde Azure toohello yerel ağ geçidi.
   
    Bu örnekte, Connectedentityıd çalıştırarak bulabilirsiniz hello yerel ağ geçidi kimliği olan `Get-AzureLocalNetworkGateway`. Hello kullanarak Virtualnetworkgatewayıd'yi bulabilirsiniz `Get-AzureVirtualNetworkGateway` cmdlet'i. Bu adımdan sonra hello siteden siteye VPN bağlantısı aracılığıyla yerel ağınız ve Azure arasında hello bağlantı kurulur.

        New-AzureVirtualNetworkGatewayConnection -connectedEntityId <local-network-gateway-id> -gatewayConnectionName Azure2Local -gatewayConnectionType IPsec -sharedKey abc123 -virtualNetworkGatewayId <azure-s2s-vpn-gateway-id>

## <a name="add"></a>zaten olan bir VNet için tooconfigure aynı anda mevcut bağlantılar
Varolan bir sanal ağınız varsa, hello ağ geçidi alt ağ boyutunu kontrol edin. Merhaba ağ geçidi alt ağı /28 veya/29 ise, öncelikle hello sanal ağ geçidini silmek ve hello ağ geçidi alt ağ boyutunu artırın. Merhaba bu bölümdeki adımlar bunu nasıl yapacağınızı gösterir toodo.

Merhaba ağ geçidi alt ağı /27 ise veya daha büyük ve hello sanal ağ ExpressRoute üzerinden bağlı olduğundan, hello adımları atlayın ve çok devam["6. adım - siteden siteye VPN ağ geçidi oluşturma"](#vpngw) hello önceki bölümdeki.

> [!NOTE]
> Merhaba mevcut ağ geçidini sildiğinizde, bu yapılandırma üzerinde çalışırken, yerel şirket hello bağlantı tooyour sanal ağ kaybedersiniz.
> 
> 

1. Tooinstall hello en son sürümünü hello Azure Resource Manager PowerShell cmdlet'lerini gerekir. Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) hello PowerShell cmdlet'lerini yükleme hakkında daha fazla bilgi. Bu yapılandırma için kullanacağınız hello cmdlet'leri ne tanımanız değerinden biraz farklı olabileceğini unutmayın. Bu yönergelerde emin toouse hello cmdlet'leri belirtilmiş. 
2. Merhaba mevcut ExpressRoute veya siteden siteye VPN ağ geçidini silin. Aşağıdaki cmdlet, hello değerleri kendi değerlerinizle değiştirerek hello kullanın.
   
        Remove-AzureVNetGateway –VnetName MyAzureVNET
3. Merhaba sanal ağ şemasını dışarı aktarın. Aşağıdaki PowerShell cmdlet'ini, hello değerleri kendi değerlerinizle değiştirerek hello kullanın.
   
        Get-AzureVNetConfig –ExportToFile “C:\NetworkConfig.xml”
4. Merhaba ağ geçidi alt ağı/27 veya daha kısa bir önek (örneğin, / 26 veya /25) böylece hello ağ yapılandırma dosyası şeması düzenleyin. Merhaba aşağıdaki örneğine bakın. 
   
   > [!NOTE]
   > Yeterli IP adresi, sanal ağ tooincrease hello ağ geçidi alt ağı boyutuna sahip değilseniz, daha fazla IP adresi alanı tooadd gerekir. Merhaba yapılandırma şeması hakkında daha fazla bilgi için bkz: [Azure Virtual Network yapılandırma şeması](https://msdn.microsoft.com/library/azure/jj157100.aspx).
   > 
   > 
   
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.17.159.224/27</AddressPrefix>
          </Subnet>
5. Önceki ağ geçidiniz siteden siteye VPN ise, da hello bağlantı türü çok değiştirmelisiniz**adanmış**.
   
                 <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="MyLocalNetwork">
                      <Connection type="Dedicated" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
6. Bu noktada, hiçbir ağ geçidi olmayan bir VNet’e sahip olursunuz. toocreate yeni ağ geçitleri ve bağlantılarınızı tamamlamak, devam edebilmeniz [4. adım - bir ExpressRoute ağ geçidi oluşturma](#gw), önceki adımları kümesini hello bulunan.

## <a name="next-steps"></a>Sonraki adımlar
ExpressRoute hakkında daha fazla bilgi için bkz: Merhaba [ExpressRoute SSS](expressroute-faqs.md)

