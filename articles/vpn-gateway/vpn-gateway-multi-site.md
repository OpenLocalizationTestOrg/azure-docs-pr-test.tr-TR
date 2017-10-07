---
title: "VPN ağ geçidi ve PowerShell kullanarak bir sanal ağ toomultiple siteleri bağlamak: Klasik | Microsoft Docs"
description: "Bu makalede hello Klasik dağıtım modeli için bir VPN ağ geçidi kullanarak birden çok yerel şirket içi siteler tooa sanal ağ konusunda size yol gösterir."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-service-management
ms.assetid: b043df6e-f1e8-4a4d-8467-c06079e2c093
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: yushwang
ms.openlocfilehash: 5404b1c55ed3453b4dbc94dfd93e47c0812025f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection-classic"></a>Mevcut bir VPN ağ geçidi bağlantısı olan (Klasik) bir siteden siteye bağlantı tooa VNet ekleme

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

> [!div class="op_single_selector"]
> * [Azure portal](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [PowerShell (klasik)](vpn-gateway-multi-site.md)
>
>

Bu makalede, varolan bir bağlantıyı sahip PowerShell tooadd siteden siteye (S2S) bağlantıları tooa VPN ağ geçidi kullanılarak üzerinden açıklanmaktadır. Bu tür bir bağlantı başvurulan tooas "çok siteli" yapılandırma görülür. Merhaba bu makaledeki adımları hello Klasik dağıtım modeli (Hizmet Yönetimi olarak da bilinir) kullanılarak oluşturulmuş toovirtual ağlara uygulanır. Bu adımları tooExpressRoute /-siteye eşzamanlı bağlantı yapılandırmaları geçerli değildir.

### <a name="deployment-models-and-methods"></a>Dağıtım modelleri ve yöntemleri

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

Bu tabloda yeni makaleler olarak güncelleştiriyoruz ve ek araçlar bu yapılandırma için kullanılabilir hale gelir. Bir makale kullanılabilir olduğunda sizi doğrudan bu tablodan tooit bağlayın.

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="about-connecting"></a>Bağlama hakkında

Birden çok şirket içi siteler tooa tek bir sanal ağ bağlanabilir. Karma bulut çözümleri oluşturmak için özellikle çekici budur. Çok siteli bağlantı tooyour Azure sanal ağ geçidi oluşturma benzer toocreating diğer siteden siteye bağlantı sayısıdır. Aslında, Hello ağ geçidi dinamik olduğu sürece, mevcut bir Azure VPN ağ geçidi kullanabilirsiniz (rota tabanlı).

Bir statik ağ geçidi bağlı tooyour sanal ağınız zaten varsa, sipariş tooaccommodate birden çok sitede toorebuild hello sanal ağ gerek kalmadan hello ağ geçidi türü toodynamic değiştirebilirsiniz. Merhaba yönlendirme türü değiştirmeden önce şirket içi VPN ağ geçidinizi rota tabanlı VPN yapılandırmaları desteklediğinden emin olun.

![çok siteli diyagramı](./media/vpn-gateway-multi-site/multisite.png "çok siteli")

## <a name="points-tooconsider"></a>Noktaları tooconsider

**Mümkün toouse hello portal toomake değişiklikleri toothis sanal ağ olmayacaktır.** Merhaba portal kullanmak yerine toomake değişiklikleri toohello ağ yapılandırma dosyası gerekir. Merhaba Portalı'nda değişiklik yaparsanız, bu sanal ağ için çok siteli başvuru ayarlarınızı üzerine.

Rahat geliyor olmalıdır hello zamanına göre hello ağ yapılandırma dosyası kullanarak hello çok siteli yordamı tamamladınız. Ancak, ağ yapılandırmanızı üzerinde çalışan birden çok kişi varsa toomake herkes bu sınırlama hakkında bilir emin ihtiyacınız vardır. Bu, hello portal hiç kullanamazsınız anlamına gelmez. Başka yapılandırma değişiklikleri toothis belirli sanal ağ oluşturma dışında her şey için kullanabilirsiniz.

## <a name="before-you-begin"></a>Başlamadan önce

Yapılandırmaya başlamadan önce hello aşağıdaki sahip olduğunu doğrulayın:

* Uyumlu VPN donanım her konum şirket içi. Denetleme [sanal ağ bağlantısı için VPN aygıtları hakkında](vpn-gateway-about-vpn-devices.md) toobe uyumlu bilinen hello aygıt toouse istediğiniz bir şey ise tooverify.
* Bir dışarıya dönük IPv4 için genel IP adresi her VPN cihazı. Başlangıç IP adresi bir NAT'nin arkasında olamaz Bu gerekli değildir.
* Tooinstall hello en son sürümünü hello Azure PowerShell cmdlet'lerini gerekir. Toplama toohello Resource Manager sürümünde hello Hizmet Yönetimi (SM) sürümü yüklediğinizden emin olun. Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) daha fazla bilgi için.
* Birisinden VPN donanımınızın yapılandırma sırasında yeterli. Toohave nasıl güçlü bir anlayış gerekir tooconfigure VPN cihazı veya mu birisi birlikte çalışır.
* hello IP adresi aralığı (sizin zaten bir oluşturmadıysanız), sanal ağınızda toouse istiyor.
* Başlangıç IP adresi aralıkları için bağlanma hello yerel ağ sitelerinin her biri için. Toomake başlangıç IP adresi her tooconnect toodo olmayan çakışma istediğiniz hello yerel ağ sitesi için aralıkları emin olmanız gerekir. Aksi takdirde hello portalı veya REST API hello karşıya yüklenen hello yapılandırma reddeder.<br>Her ikisi de başlangıç IP adresi aralığı 10.2.3.0/24 içerir ve hedef adres 10.2.3.3 ile bir pakete sahip iki yerel ağ sitesi varsa, Azure toosend hello paket toobecause hello adres aralıkları istediğiniz hangi site Örneğin, bilmeniz olmayacaktır Çakışan. tooprevent yönlendirme sorunları, Azure tooupload örtüşen aralıklarına sahip bir yapılandırma dosyası izin vermez.

## <a name="1-create-a-site-to-site-vpn"></a>1. Siteden Siteye VPN oluşturma
Zaten bir dinamik yönlendirme ağ geçidi ile siteden siteye VPN harika varsa! Çok geçebilmeniz[hello sanal ağ yapılandırma ayarlarını dışarı aktar](#export). Aksi durumda, aşağıdaki hello:

### <a name="if-you-already-have-a-site-to-site-virtual-network-but-it-has-a-static-policy-based-routing-gateway"></a>Siteden siteye sanal ağ zaten var, ancak statik (ilke tabanlı) yönlendirme ağ geçidi varsa:
1. Ağ geçidi türü toodynamic yönlendirme değiştirin. Çok siteli VPN dinamik (olarak da bilinen rota tabanlı) yönlendirme ağ geçidi gerektirir. Ağ geçidiniz toochange yazın, toofirst delete hello mevcut ağ geçidine gereksinimi sonra yeni bir tane oluşturun. Yönergeler için bkz: [nasıl toochange hello ağ geçidiniz için VPN yönlendirme türü](vpn-gateway-configure-vpn-gateway-mp.md).  
2. Yeni ağ geçidiniz yapılandırın ve VPN tüneli oluşturur. Yönergeler için bkz: [hello Klasik Azure portalı bir VPN ağ geçidi yapılandırma](vpn-gateway-configure-vpn-gateway-mp.md). İlk olarak, ağ geçidi türü toodynamic yönlendirme değiştirin.

### <a name="if-you-dont-have-a-site-to-site-virtual-network"></a>Siteden siteye sanal ağınız yoksa:
1. Bu yönergeleri kullanarak, siteden siteye sanal ağ oluşturma: [bir siteden siteye VPN bağlantısının hello Klasik Azure portalı ile bir sanal ağ oluşturma](vpn-gateway-site-to-site-create.md).  
2. Bu yönergeleri kullanarak dinamik yönlendirme ağ geçidi yapılandırma: [bir VPN ağ geçidi yapılandırma](vpn-gateway-configure-vpn-gateway-mp.md). Emin tooselect olması **dinamik yönlendirme** , ağ geçidi türü.

## <a name="export"></a>2. Dışa aktarma hello ağ yapılandırma dosyası
Azure ağı yapılandırma dosyanızı hello aşağıdaki komutu çalıştırarak dışa aktarın. Merhaba dosya tooexport tooa farklı konumu gerekirse hello konumunu değiştirebilirsiniz.

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

## <a name="3-open-hello-network-configuration-file"></a>3. Açık hello ağ yapılandırma dosyası
Merhaba son adımda indirdiğiniz hello ağ yapılandırma dosyasını açın. İstediğiniz herhangi bir xml düzenleyicisi kullanın. Merhaba dosya benzer toohello aşağıdaki gibi görünmelidir:

        <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <LocalNetworkSites>
              <LocalNetworkSite name="Site1">
                <AddressSpace>
                  <AddressPrefix>10.0.0.0/16</AddressPrefix>
                  <AddressPrefix>10.1.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.2.3.4</VPNGatewayAddress>
              </LocalNetworkSite>
              <LocalNetworkSite name="Site2">
                <AddressSpace>
                  <AddressPrefix>10.2.0.0/16</AddressPrefix>
                  <AddressPrefix>10.3.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.4.5.6</VPNGatewayAddress>
              </LocalNetworkSite>
            </LocalNetworkSites>
            <VirtualNetworkSites>
              <VirtualNetworkSite name="VNet1" AffinityGroup="USWest">
                <AddressSpace>
                  <AddressPrefix>10.20.0.0/16</AddressPrefix>
                  <AddressPrefix>10.21.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="FE">
                    <AddressPrefix>10.20.0.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="BE">
                    <AddressPrefix>10.20.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="GatewaySubnet">
                    <AddressPrefix>10.20.2.0/29</AddressPrefix>
                  </Subnet>
                </Subnets>
                <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="Site1">
                      <Connection type="IPsec" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

## <a name="4-add-multiple-site-references"></a>4. Birden çok sitesi başvuruları ekleme
Site başvuru bilgileri ekleyip, yapılandırma değişikliklerini hale getireceğiz toohello ConnectionsToLocalNetwork/LocalNetworkSiteRef. Yeni bir yerel site başvurusu ekleme Azure toocreate yeni tünel tetikler. Merhaba aşağıdaki örnekte, tek siteli bağlantı için hello ağ yapılandırmadır. Yaptığınız değişiklikleri yaptıktan sonra hello dosyasını kaydedin.

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

(çok siteli yapılandırma Oluştur) tooadd ek sitesi başvuruları eklemeniz yeterlidir ek "LocalNetworkSiteRef" satırları hello aşağıdaki örnekte gösterildiği gibi:

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
      <LocalNetworkSiteRef name="Site2"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

## <a name="5-import-hello-network-configuration-file"></a>5. İçeri aktarma hello ağ yapılandırma dosyası
Merhaba ağ yapılandırma dosyasını içeri aktarın. Merhaba değişikliklerle bu dosyayı içeri aktardığınızda hello yeni tüneller eklenir. Merhaba tünelleri, daha önce oluşturduğunuz hello dinamik ağ geçidi kullanır. Merhaba Klasik portal veya PowerShell tooimport hello dosyası ya da kullanabilirsiniz.

## <a name="6-download-keys"></a>6. Anahtarları indirin
Yeni tüneller eklendikten sonra hello PowerShell cmdlet 'Get-AzureVNetGatewayKey' tooget hello IPSec/IKE önceden paylaşılan anahtarlar için her tünel kullanın.

Örneğin:

```powershell
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site1"
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site2"
```

İsterseniz, hello de kullanabilirsiniz *alma sanal ağ geçidi paylaşılan anahtarı* REST API tooget hello önceden paylaşılan anahtarlar.

## <a name="7-verify-your-connections"></a>7. Bağlantılarınızı doğrulayın
Merhaba çok siteli tünel durumunu kontrol edin. Her tünel Hello tuşları indirdikten sonra tooverify bağlantıları isteyeceksiniz. Sanal ağ listesi tünelleri, 'Get-AzureVnetConnection' tooget hello aşağıdaki örnekte gösterildiği gibi kullanın. VNet1 hello VNet hello adıdır.

```powershell
Get-AzureVnetConnection -VNetName VNET1
```

Örnek dönüş:

```
    ConnectivityState         : Connected
    EgressBytesTransferred    : 661530
    IngressBytesTransferred   : 519207
    LastConnectionEstablished : 5/2/2014 2:51:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site1' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site1
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7f68a8e6-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded

    ConnectivityState         : Connected
    EgressBytesTransferred    : 789398
    IngressBytesTransferred   : 143908
    LastConnectionEstablished : 5/2/2014 3:20:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site2' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site2
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7893b329-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded
```

## <a name="next-steps"></a>Sonraki adımlar

toolearn, VPN ağ geçitleri hakkında daha fazla bilgi görmek [VPN ağ geçitleri hakkında](vpn-gateway-about-vpngateways.md).
