---
title: "Doğrulanıyor bağlantısı: Sorun giderme kılavuzu Azure ExpressRoute | Microsoft Docs"
description: "Bu sayfa, sorun giderme ve bir expressroute bağlantı hattı son tooend bağlantısını doğrulama yönergelerini sağlar."
documentationcenter: na
services: expressroute
author: rambk
manager: tracsman
editor: 
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 713c39c7eafd77a4380b2a91902a9686f2ce1d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="verifying-expressroute-connectivity"></a>ExpressRoute bağlantısı doğrulanıyor
Bir şirket içi ağ bağlantı sağlayıcı tarafından kolaylaştırılan özel bir bağlantı üzerinden Microsoft bulut hello genişletir, ExpressRoute üç farklı ağ bölgeleri aşağıdaki hello içerir:

-   Müşteri ağ
-   Sağlayıcı ağ
-   Microsoft Veri merkezinde

Bu belgenin amacı Hello olduğu toohelp kullanıcı tooidentify nerede (veya bir olsa bile) bir bağlantı sorunu var ve hangi bölge içinde böylece tooseek Yardım uygun takım tooresolve hello sorundan. Microsoft destek gerekli tooresolve bir sorun varsa, bir destek bileti ile açmak [Microsoft Support][Support].

> [!IMPORTANT]
> Bu, hedeflenen toohelp tanılama ve basit sorunlarını giderme belgedir. Hedeflenen toobe Microsoft destek için yenileme değildir. Bir destek bileti ile açmak [Microsoft Support] [ Support] sağlanan hello yönergeleri kullanarak oluşturulamıyor toosolve hello sorun olması durumunda.
>
>

## <a name="overview"></a>Genel Bakış
Merhaba Aşağıdaki diyagramda hello mantıksal bağlantısını ExpressRoute kullanarak bir müşteri ağ tooMicrosoft ağ gösterilmektedir.
[![1]][1]

Diyagram önceki hello hello sayılar anahtar ağ noktalarını gösterir. Merhaba ağ noktaları genellikle ilişkili numaralarına göre bu makalede başvurulur.

Bağlı olarak Hello ExpressRoute bağlantı modeli (bulut Exchange birlikte bulundurma, noktadan noktaya Ethernet bağlantısı veya Any herhangi bir (IPVPN)) hello ağ noktalarını 3 ve 4 anahtarları (Katman 2 aygıtları) kullanılabilir. gösterilen hello anahtar ağ noktaları aşağıdaki gibidir:

1.  Müşteri işlem aygıt (örneğin, bir sunucu veya bilgisayar)
2.  CEs: Müşteri sınır yönlendiricileri 
3.  PEs (CE'e yönelik): sağlayıcısı sınır yönlendiricileri/müşteri sınır yönlendiricileri karşılıklı anahtarları. Bu belgedeki tooas PE CEs denir.
4.  PEs (MSEE'e yönelik): sağlayıcısı sınır yönlendiricileri/Msee'ler karşılıklı anahtarları. Bu belgedeki tooas PE Msee'ler denir.
5.  Msee'ler: Microsoft Enterprise Edge (MSEE) ExpressRoute yönlendiricileri
6.  Sanal ağ (VNet) ağ geçidi
7.  Cihaz hello Azure VNet üzerinde işlem

Merhaba bulut Exchange birlikte bulundurma veya noktadan noktaya Ethernet bağlantısı bağlantı modeli kullanılıyorsa, hello müşteri sınır yönlendiricisi (2) BGP eşliği (5) Msee'ler ile oluşturmanız. Ağ noktalarını 3 ve 4 hala var ancak katman 2 cihaz olarak biraz saydam.

Merhaba herhangi herhangi bir (IPVPN) bağlantı modeli kullanılıyorsa, PEs (MSEE'e yönelik) hello (4) BGP eşliği (5) Msee'ler ile kurmak. Yollar sonra geri toohello müşteri ağ hello IPVPN hizmet sağlayıcısı ağ üzerinden yayılır.

>[!NOTE]
>ExpressRoute, yüksek kullanılabilirlik için yedek bir BGP oturumları Msee'ler (5) PE Msee'ler (4) arasındaki çift Microsoft gerektirir. Ağ yolları yedek çifti de müşteri ağ arasında PE CEs teşvik. Ancak, herhangi herhangi bir (IPVPN) bağlantı modelinde, tek bir CE aygıt (2) bağlı tooone ya da daha fazla PEs (3) olabilir.
>
>

toovalidate bir expressroute bağlantı hattı, aşağıdaki adımları hello (noktasıyla ilişkili hello sayıyla hello ağ) ele alınmıştır:
1. [Bağlantı hattı hazırlama ve durumu (5) doğrula](#validate-circuit-provisioning-and-state)
2. [En az bir ExpressRoute doğrulamak eşliği, yapılandırılmış (5)](#validate-peering-configuration)
3. [Microsoft ve hello hizmet sağlayıcısı (bağlantı 4 ve 5 arasında) arasında ARP doğrula](#validate-arp-between-microsoft-and-the-service-provider)
4. [BGP ve hello MSEE (BGP 4 too5 VNet bağlıysa, 5 too6 arasındaki) yollara doğrula](#validate-bgp-and-routes-on-the-msee)
5. [Onay hello trafiği istatistikleri (trafik 5'ten geçirme)](#check-the-traffic-statistics)

Daha fazla doğrulama ve denetimleri hello gelecekteki iade geri aylık eklenecek!

##<a name="validate-circuit-provisioning-and-state"></a>Bağlantı hattı hazırlama ve durumunu doğrula
Oluşturulan toobe ve bu nedenle hizmet Hello bağlantı modeli bağımsız olarak, bir expressroute bağlantı hattı sahip devre sağlama için oluşturulan anahtarı. Bir expressroute bağlantı hattı sağlama PE Msee'ler (4) ve Msee'ler (5) arasında yedekli bir katman 2 bağlantı kurar. Hello makale nasıl toocreate, değiştirme, sağlamak ve bir expressroute bağlantı hattı doğrulayın daha fazla bilgi için bkz: [oluşturma ve bir expressroute bağlantı hattı değiştirme][CreateCircuit].

>[!TIP]
>Bir hizmet anahtarı, bir expressroute bağlantı hattı benzersiz olarak tanımlar. Bu belgede belirtilen hello powershell komutların çoğu için bu anahtar gereklidir. Ayrıca, Yardım ihtiyacınız olursa Microsoft'tan ya da bir expressroute bağlantı ortağı tootroubleshoot bir ExpressRoute sorun, hello hizmet sağlamak anahtar tooreadily hello hattı tanımlayın.
>
>

###<a name="verification-via-hello-azure-portal"></a>Hello Azure portal aracılığıyla doğrulama
Hello Azure portal'da, bir expressroute bağlantı hattı hello durumunu seçerek denetlenebilir ![2][2] expressroute bağlantı hattı üzerinde hello sol kenar çubuğu menüsüne ve ardından seçerek hello. Bir expressroute bağlantı seçme "Tüm kaynaklar" altında listelenen bağlantı hattı hello ExpressRoute bağlantı hattı dikey penceresi açılır. Merhaba, ![3][3] hello dikey penceresinde hello essentials hello aşağıdaki ekran görüntüsü gösterildiği gibi listelenen ExpressRoute bölümünü:

![4][4]    

Merhaba ExpressRoute Essentials içindeki *hattı durumu* hello Microsoft yan hello devreye hello durumunu gösterir. *Sağlayıcı durumu* hello hattı olup olmadığını gösteren *hazırlandı/değil sağlanan* hello hizmet sağlayıcı tarafında. 

Bir ExpressRoute bağlantı hattı toobe için işletimsel, hello *hattı durumu* olmalıdır *etkin* ve hello *sağlayıcı durumu* olmalıdır *hazırlandı*.

>[!NOTE]
>Merhaba, *hattı durumu* olduğu etkin değilse, ilgili kişi [Microsoft Support][Support]. Merhaba, *sağlayıcı durumu* olan sağlanan değil, hizmet sağlayıcınıza başvurun.
>
>

###<a name="verification-via-powershell"></a>PowerShell aracılığıyla doğrulama
toolist tüm ExpressRoute bağlantı hatları bir kaynak grubunda Merhaba, hello aşağıdaki komutu kullanın:

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG"

>[!TIP]
>Kaynak grubu adı hello Azure portal elde edebilirsiniz. Merhaba, bu belgenin önceki alt bölümüne bakın ve bu hello kaynak grubu adı hello örnek ekran görüntüsü listelenen not edin.
>
>

belirli bir expressroute bağlantı hattı komutu aşağıdaki kullanım hello bir kaynak grubunda tooselect:

    Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"

Örnek yanıt şöyledir:

    Name                             : Test-ER-Ckt
    ResourceGroupName                : Test-ER-RG
    Location                         : westus2
    Id                               : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                        "Name": "Standard_UnlimitedData",
                                        "Tier": "Standard",
                                        "Family": "UnlimitedData"
                                        }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             : 
    ServiceProviderProperties        : {
                                        "ServiceProviderName": "****",
                                        "PeeringLocation": "******",
                                        "BandwidthInMbps": 100
                                        }
    ServiceKey                       : **************************************
    Peerings                         : []
    Authorizations                   : []

tooconfirm bir expressroute bağlantı hattı çalıştığından, özellikle dikkat toohello alanları izleyen ödeme:

    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned

>[!NOTE]
>Merhaba, *CircuitProvisioningState* olduğu etkin değilse, ilgili kişi [Microsoft Support][Support]. Merhaba, *ServiceProviderProvisioningState* olan sağlanan değil, hizmet sağlayıcınıza başvurun.
>
>

###<a name="verification-via-powershell-classic"></a>PowerShell (Klasik) aracılığıyla doğrulama
toolist tüm ExpressRoute bağlantı hatları bir abonelik altında Merhaba, hello aşağıdaki komutu kullanın:

    Get-AzureDedicatedCircuit

tooselect belirli bir expressroute bağlantı hattı hello aşağıdaki komutu kullanın:

    Get-AzureDedicatedCircuit -ServiceKey **************************************

Örnek yanıt şöyledir:

    andwidth                         : 100
    BillingType                      : UnlimitedData
    CircuitName                      : Test-ER-Ckt
    Location                         : westus2
    ServiceKey                       : **************************************
    ServiceProviderName              : ****
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

tooconfirm bir expressroute bağlantı hattı çalıştığından, özellikle dikkat toohello alanları izleyen ödeme: ServiceProviderProvisioningState: sağlanan durum: etkin

>[!NOTE]
>Merhaba, *durum* olduğu etkin değilse, ilgili kişi [Microsoft Support][Support]. Merhaba, *ServiceProviderProvisioningState* olan sağlanan değil, hizmet sağlayıcınıza başvurun.
>
>

##<a name="validate-peering-configuration"></a>Eşleme yapılandırmasını doğrulayın
Merhaba expressroute bağlantı hattı sağlama tamamlanmış hello Hello hizmet sağlayıcısı sahip olduktan sonra bir yönlendirme yapılandırması hello MSEE PRs (4) Msee'ler (5) arasındaki expressroute bağlantı hattı üzerinden oluşturulabilir. Her expressroute bağlantı hattı bir, iki veya üç yönlendirme bağlamları etkin olabilir: (trafiği tooprivate sanal ağlar Azure) Azure özel eşleme, (trafiği toopublic azure'daki IP adresleri) Azure ortak eşleme ve Microsoft (trafiği tooOffice 365 eşleme ve Dynamics 365). Hakkında daha fazla bilgi için toocreate ve yönlendirme yapılandırmasını değiştirmek, hello makalesine bakın [oluşturma ve bir expressroute bağlantı hattı için yönlendirmeyi değiştirme][CreatePeering].

###<a name="verification-via-hello-azure-portal"></a>Hello Azure portal aracılığıyla doğrulama
>[!IMPORTANT]
>Merhaba; burada görüntülerle ExpressRoute eşlemeler olan Azure portal bilinen bir hata varsa *değil* hello hizmet sağlayıcısı tarafından yapılandırılmışsa hello Portalı'nda gösterilen. ExpressRoute eşlemeler hello portal veya PowerShell aracılığıyla ekleme *hello servis sağlayıcı ayarları geçersiz kılar*. Bu eylem hello hello expressroute bağlantı hattı üzerinde yönlendirmeyi keser ve hello hizmeti sağlayıcısı toorestore hello ayarlarının hello desteği gerektirir ve normal yönlendirme yeniden. Yalnızca bu hello hizmet sağlayıcısı yalnızca Katman 2 hizmetleri sağlayan belirli ise hello ExpressRoute eşlemeler değiştirin!
>
>

<p/>
>[!NOTE]
>Hizmet sağlayıcısı ve hello eşlemeler tarafından Hello hello Portalı'nda boş olması koşuluyla Katman 3 ise, PowerShell kullanılan toosee hello servis sağlayıcı yapılandırılmış ayarları olabilir.
>
>

Hello Azure portal'da, bir expressroute bağlantı hattı durumunu seçerek denetlenebilir ![2][2] expressroute bağlantı hattı üzerinde hello sol kenar çubuğu menüsüne ve ardından seçerek hello. Bir expressroute bağlantı seçme "Tüm kaynaklar" altında listelenen bağlantı hattı hello ExpressRoute bağlantı hattı dikey penceresi açılacaktır. Merhaba, ![3][3] bölümüne hello dikey penceresinde hello ExpressRoute hello aşağıdaki ekran görüntüsü gösterildiği gibi essentials'in listelenmesi:

![5][5]

Azure ortak ve Microsoft eşleme yönlendirme bağlamları etkin olmayan ancak örnek önceki hello belirtilen Azure özel eşleme yönlendirme bağlamı olarak etkinleştirilir. Başarılı bir şekilde etkinleştirilmiş bir eşleme bağlamı listelenen hello (BGP için gerekli) birincil ve ikincil noktadan noktaya alt ağlar da gerekir. Merhaba /30 alt ağlar hello Msee'ler hello arabirimi IP adresini ve PE Msee için kullanılır. 

>[!NOTE]
>Bir eşleme etkin değilse, atanan hello birincil ve ikincil alt ağları eşleşip eşleşmediğini denetleyin PE Msee'ler hello yapılandırmasına. Değilse, toochange hello yapılandırma, MSEE yönlendiricilerde çok başvurun[oluşturma ve bir expressroute bağlantı hattı için yönlendirmeyi değiştirme][CreatePeering]
>
>

###<a name="verification-via-powershell"></a>PowerShell aracılığıyla doğrulama
tooget hello Azure özel yapılandırma ayrıntılarını eşliği hello aşağıdaki komutları kullanın:

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt

Bir başarılı bir şekilde yapılandırılmış özel eşleme için bir örnek yanıt şöyledir:

    Name                       : AzurePrivatePeering
    Id                         : /subscriptions/***************************/resourceGroups/Test-ER-RG/providers/***********/expressRouteCircuits/Test-ER-Ckt/peerings/AzurePrivatePeering
    Etag                       : W/"################################"
    PeeringType                : AzurePrivatePeering
    AzureASN                   : 12076
    PeerASN                    : ####
    PrimaryPeerAddressPrefix   : 172.16.0.0/30
    SecondaryPeerAddressPrefix : 172.16.0.4/30
    PrimaryAzurePort           : 
    SecondaryAzurePort         : 
    SharedKey                  : 
    VlanId                     : 300
    MicrosoftPeeringConfig     : null
    ProvisioningState          : Succeeded

 Başarılı bir şekilde etkinleştirilmiş bir eşleme bağlamı listelenen hello birincil ve ikincil adres öneklerini gerekir. Merhaba /30 alt ağlar hello Msee'ler hello arabirimi IP adresini ve PE Msee için kullanılır.

tooget hello Azure genel yapılandırma ayrıntılarını eşliği hello aşağıdaki komutları kullanın:

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt

tooget hello Microsoft eşleme yapılandırma ayrıntılarını, hello aşağıdaki komutları kullanın:

    $ckt = Get-AzureRmExpressRouteCircuit -ResourceGroupName "Test-ER-RG" -Name "Test-ER-Ckt"
    Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -Circuit $ckt

Bir eşleme yapılandırılmamışsa bir hata iletisi olacaktır. Merhaba eşleme (Azure Bu örnekte eşliği genel) belirtildiği zaman bir örnek yanıt hello hattı içinde yapılandırılmamış:

    Get-AzureRmExpressRouteCircuitPeeringConfig : Sequence contains no matching element
    At line:1 char:1
        + Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering ...
        + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
            + CategoryInfo          : CloseError: (:) [Get-AzureRmExpr...itPeeringConfig], InvalidOperationException
            + FullyQualifiedErrorId : Microsoft.Azure.Commands.Network.GetAzureExpressRouteCircuitPeeringConfigCommand


<p/>
>[!NOTE]
>Bir eşleme etkin değilse hello atanan birincil ve ikincil alt ağları eşleşme hello hello yapılandırmasına PE MSEE bağlı olmadığını denetleyin. Ayrıca onay hello varsa düzeltin *Vlanıd*, *AzureASN*, ve *PeerASN* üzerinde Msee'ler kullanılır ve bu değerleri toohello hello üzerinde kullanılan olanları eşleniyorsa PE MSEE bağlanır. MD5 karma seçilirse, hello paylaşılan anahtar MSEE ve PE MSEE çiftine aynı olması gerekir. Merhaba MSEE yönlendiricilerde toochange hello yapılandırma başvurmak çok [oluşturma ve bir expressroute bağlantı hattı için yönlendirmeyi değiştirme] [CreatePeering].  
>
>

### <a name="verification-via-powershell-classic"></a>PowerShell (Klasik) aracılığıyla doğrulama
tooget hello Azure özel yapılandırma ayrıntılarını eşliği hello aşağıdaki komutu kullanın:

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

Özel bir başarılı bir şekilde yapılandırılmış eşleme için ek olarak, örnek yanıt şöyledir:

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : ####
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100

A başarılı bir şekilde, etkinleştirilmiş eşleme bağlam listelenen hello birincil ve ikincil eş alt sahip olabilir. Merhaba /30 alt ağlar hello Msee'ler hello arabirimi IP adresini ve PE Msee için kullanılır.

tooget hello Azure genel yapılandırma ayrıntılarını eşliği hello aşağıdaki komutları kullanın:

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

tooget hello Microsoft eşleme yapılandırma ayrıntılarını, hello aşağıdaki komutları kullanın:

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

>[!IMPORTANT]
>Katman 3 eşlemeler hello hizmet sağlayıcısı tarafından ayarlanan, hello ExpressRoute eşlemeler hello portal veya PowerShell aracılığıyla ayarlama hello servis sağlayıcı ayarları üzerine yazar. Merhaba sağlayıcı yan eşleme ayarları sıfırlama hello hizmet sağlayıcısının hello desteği gerektirir. Yalnızca bu hello hizmet sağlayıcısı yalnızca Katman 2 hizmetleri sağlayan belirli ise hello ExpressRoute eşlemeler değiştirin!
>
>

<p/>
>[!NOTE]
>Bir eşleme etkin değilse hello birincil ve ikincil eş atanan alt ağları eşleşme hello yapılandırmasına hello PE MSEE bağlı olmadığını denetleyin. Ayrıca onay hello varsa düzeltin *Vlanıd*, *AzureAsn*, ve *PeerAsn* üzerinde Msee'ler kullanılır ve bu değerleri toohello hello üzerinde kullanılan olanları eşleniyorsa PE MSEE bağlanır. Merhaba MSEE yönlendiricilerde toochange hello yapılandırma başvurmak çok [oluşturma ve bir expressroute bağlantı hattı için yönlendirmeyi değiştirme] [CreatePeering].
>
>

## <a name="validate-arp-between-microsoft-and-hello-service-provider"></a>ARP arasında Microsoft ve hello hizmeti sağlayıcısını doğrulayın
Bu bölüm, PowerShell (Klasik) komutlarını kullanır. Azure Resource Manager PowerShell komutları kullanıyorsanız, yönetici/ortak yönetici erişimi toohello abonelik aracılığıyla sahip olduğundan emin olun [Klasik Azure portalı][OldPortal]. Azure Resource Manager kullanarak sorun giderme için komutları toohello başvurun [hello Resource Manager dağıtım modeli alma ARP tablolarda] [ ARP] belge.

>[!NOTE]
>tooget ARP, hello Azure portalı ve Azure Resource Manager PowerShell komutları kullanılabilir. Hello Azure Resource Manager PowerShell komutları ile bir hatayla karşılaşılmazsa Klasik PowerShell komutlarını Klasik PowerShell komutları de Azure Resource Manager ExpressRoute bağlantı hatları ile çalışması olarak çalışması gerekir.
>
>

tooget hello hello özel eşliği olarak birincil MSEE'nin yönlendirici ARP tablosundan Merhaba, hello aşağıdaki komutu kullanın:

    Get-AzureDedicatedCircuitPeeringArpInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

Bir örnek yanıt hello başarılı senaryoda hello komutu için:

    ARP Info:

                 Age           Interface           IpAddress          MacAddress
                 113             On-Prem       10.0.0.1           e8ed.f335.4ca9
                   0           Microsoft       10.0.0.2           7c0e.ce85.4fc9

Benzer şekilde, hello hello hello MSEE ARP tablosundan kontrol edebilirsiniz *birincil*/*ikincil* yolu için *özel* /  *Ortak*/*Microsoft* eşlemeleri.

Merhaba aşağıdaki örnekte gösterildiği bir eşleme için hello komut yanıtı hello yok.

    ARP Info:
       
>[!NOTE]
>Merhaba ARP tablosu yoksa hello arabirimlerin IP adreslerini tooMAC adresleri, aşağıdaki bilgileri gözden geçirme hello eşlenmiş:
>1. Merhaba ilk IP adresi hello /30 alt arasında hello bağlantı için atanmışsa MSEE PR hello ve MSEE MSEE PR. hello arabirimde kullanılır Azure hello ikinci IP adresi Msee için her zaman kullanır.
>2. Merhaba müşteri (C-etiketi) ve hizmet (S-Tag) VLAN etiketlerini hem MSEE PR ve MSEE çifti eşleşip eşleşmediğini denetleyin.
>
>

## <a name="validate-bgp-and-routes-on-hello-msee"></a>BGP ve hello MSEE yollara doğrula
Bu bölüm, PowerShell (Klasik) komutlarını kullanır. Azure Resource Manager PowerShell komutları kullanıyorsanız, yönetici/ortak yönetici erişimi toohello abonelik aracılığıyla sahip olduğundan emin olun [Klasik Azure portalı][OldPortal]

>[!NOTE]
>Azure portalı ve Azure Resource Manager PowerShell komutları kullanılabilir tooget BGP bilgileri, her iki hello. Hello Azure Resource Manager PowerShell komutları ile bir hatayla karşılaşılmazsa Klasik PowerShell komutlarını Klasik PowerShell komutları de Azure Resource Manager ExpressRoute bağlantı hatları ile çalışması olarak çalışması gerekir.
>
>

tooget yönlendirme tablosunu (BGP komşu) için belirli bir yönlendirme bağlam Özet Merhaba, hello aşağıdaki komutu kullanın:

    Get-AzureDedicatedCircuitPeeringRouteTableSummary -AccessType Private -Path Primary -ServiceKey "*********************************"

Bir örnek yanıt şöyledir:

    Route Table Summary:

            Neighbor                   V                  AS              UpDown         StatePfxRcd
            10.0.0.1                   4                ####                8w4d                  50

Hello önceki örnekte gösterildiği gibi hello hello yönlendirme bağlamı ne kadar süreyle kurulduğunda için yararlı toodetermine komuttur. Ayrıca, yol önekleri hello eşleme yönlendirici tarafından tanıtılan sayısını gösterir.

>[!NOTE]
>Merhaba durumu etkin veya boş ise, hello birincil ve ikincil eş atanan alt ağları eşleşme hello yapılandırmasına hello PE MSEE bağlı olmadığını denetleyin. Ayrıca onay hello varsa düzeltin *Vlanıd*, *AzureAsn*, ve *PeerAsn* üzerinde Msee'ler kullanılır ve bu değerleri toohello hello üzerinde kullanılan olanları eşleniyorsa PE MSEE bağlanır. MD5 karma seçilirse, hello paylaşılan anahtar MSEE ve PE MSEE çiftine aynı olması gerekir. Merhaba MSEE yönlendiricilerde toochange hello yapılandırma başvurmak çok[oluşturma ve bir expressroute bağlantı hattı için yönlendirmeyi değiştirme][CreatePeering].
>
>

<p/>
>[!NOTE]
>Belirli bir eşlemesi içinde belirli hedefler erişilebilir değilse, toohello belirli eşleme bağlam ait hello Msee'ler hello rota tablosu denetleyin. (NATed IP olabilir) eşleşen bir önek hello yönlendirme tablosunda varsa, hello yolda NSG/güvenlik duvarları/ACL'leri varsa ve hello trafiğe olmadığını denetleyin.
>
>

tooget hello tam yönlendirme tablosundan MSEE hello üzerinde *birincil* hello belirli yolu *özel* yönlendirme bağlamı, komutu aşağıdaki kullanım hello:

    Get-AzureDedicatedCircuitPeeringRouteTableInfo -AccessType Private -Path Primary -ServiceKey "*********************************"

Merhaba komutu için bir örnek başarılı sonuç verilmiştir:

    Route Table Info:

             Network             NextHop              LocPrf              Weight                Path
         10.1.0.0/16            10.0.0.1                                       0    #### ##### #####     
         10.2.0.0/16            10.0.0.1                                       0    #### ##### #####
    ...

Benzer şekilde, hello yönlendirme hello hello MSEE tablosundan kontrol edebilirsiniz *birincil*/*ikincil* yolu için *özel* / *Ortak*/*Microsoft* eşleme bağlamı.

Merhaba aşağıdaki örnekte gösterildiği bir eşleme için hello komut yanıtı hello yok:

    Route Table Info:

##<a name="check-hello-traffic-statistics"></a>Onay hello trafiği istatistikleri
tooget hello birincil ve ikincil yol trafiğini istatistikleri--bayt ve bir kapatma--bir eşleme bağlamında, komutu aşağıdaki kullanım hello birleştirilmiş:

    Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf683b3a6e5c -AccessType Private

Örnek bir çıktı hello komut şöyledir:

    PrimaryBytesIn PrimaryBytesOut SecondaryBytesIn SecondaryBytesOut
    -------------- --------------- ---------------- -----------------
         240780020       239863857        240565035         239628474

Mevcut olmayan eşleme için hello komutunun örnek çıktı verilmiştir:

    Get-AzureDedicatedCircuitStats : ResourceNotFound: Can not find any subinterface for peering type 'Public' for circuit '97f85950-01dd-4d30-a73c-bf683b3a6e5c' .
    At line:1 char:1
    + Get-AzureDedicatedCircuitStats -ServiceKey 97f85950-01dd-4d30-a73c-bf ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Get-AzureDedicatedCircuitStats], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.GetAzureDedicatedCircuitPeeringStatsCommand

## <a name="next-steps"></a>Sonraki Adımlar
Daha fazla bilgi veya Yardım için bağlantılar aşağıdaki hello denetleyin:

- [Microsoft Destek][Support]
- [Oluşturma ve bir expressroute bağlantı hattı değiştirme][CreateCircuit]
- [Oluşturma ve bir expressroute bağlantı hattı için yönlendirmeyi değiştirme][CreatePeering]

<!--Image References-->
[1]: ./media/expressroute-troubleshooting-expressroute-overview/expressroute-logical-diagram.png "Mantıksal hızlı Rota bağlantısı"
[2]: ./media/expressroute-troubleshooting-expressroute-overview/portal-all-resources.png "Tüm kaynaklar simgesi"
[3]: ./media/expressroute-troubleshooting-expressroute-overview/portal-overview.png "Genel Bakış simgesi"
[4]: ./media/expressroute-troubleshooting-expressroute-overview/portal-circuit-status.png "ExpressRoute Essentials örnek ekran görüntüsü"
[5]: ./media/expressroute-troubleshooting-expressroute-overview/portal-private-peering.png "ExpressRoute Essentials örnek ekran görüntüsü"

<!--Link References-->
[Support]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[CreateCircuit]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-circuit-portal-resource-manager 
[CreatePeering]: https://docs.microsoft.com/azure/expressroute/expressroute-howto-routing-portal-resource-manager
[OldPortal]: https://manage.windowsazure.com
[ARP]: https://docs.microsoft.com/en-us/azure/expressroute/expressroute-troubleshooting-arp-resource-manager






