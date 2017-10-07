---
title: "Klasik sanal ağlar tooAzure Resource Manager sanal ağlara bağlanma: portalı | Microsoft Docs"
description: "Bilgi nasıl toocreate Klasik sanal ağlar ve Resource Manager VPN ağ geçidi ve hello portalını kullanarak sanal ağlar arasında bir VPN bağlantısı"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 5a90498c-4520-4bd3-a833-ad85924ecaf9
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: bef63b4e829335b2e1a9434a35ebfe33b4fd7373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-hello-portal"></a>Sanal ağlar farklı dağıtım modelinden hello portal kullanarak bağlan

Bu makale size nasıl tooconnect Klasik sanal ağlar tooResource Yöneticisi sanal ağlar tooallow hello hello ayrı dağıtım modelleri toocommunicate birbirleriyle bulunan kaynakları gösterir. Bu makaledeki adımları Hello öncelikle hello Azure portal kullanır, ancak hello makale bu listeden seçerek hello PowerShell kullanarak bu yapılandırmayı de oluşturabilirsiniz.

> [!div class="op_single_selector"]
> * [Portal](vpn-gateway-connect-different-deployment-models-portal.md)
> * [PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

Resource Manager Vnet'i klasik bir VNet tooa bağlanma benzer tooconnecting bir VNet tooan şirket içi site konumu değil. Her iki bağlantı türü bir VPN ağ geçidi tooprovide IPSec/IKE kullanarak güvenli bir tünel kullanın. Farklı Aboneliklerde ve farklı bölgelerdeki sanal ağlar arasında bir bağlantı oluşturabilirsiniz. Dinamik ya da rota tabanlı ile yapılandırıldığını hello ağ geçidi olduğu sürece bağlantıları tooon içi ağlar, zaten sanal ağlar da bağlanabilirsiniz. VNet-VNet bağlantıları hakkında daha fazla bilgi için bkz: Merhaba [VNet-VNet ile ilgili SSS](#faq) hello bu makalenin sonunda. 

Sanal ağlar hello varsa aynı bölgede isteyebilir tooinstead VNet eşlemesi kullanarak bunları bağlanma göz önünde bulundurun. VNet eşlemesi VPN ağ geçidini kullanmaz. Daha fazla bilgi için bkz. [VNet eşlemesi](../virtual-network/virtual-network-peering-overview.md). 

### <a name="prerequisites"></a>Ön koşullar

* Bu adımları iki sanal ağlar zaten oluşturulmuş olduğunu varsayalım. Bu makalede bir alıştırma olarak kullanıyorsanız ve sanal ağlar yoksa bağlantıları vardır hello adımları toohelp bunları oluşturmanız.
* Sanal ağlar birbirleri ile çakışmaması hello için Hello adres aralıkları veya hello biriyle çakışma diğer bağlantılar için ağ geçitleri bağlı olabilir, hello aralıkları doğrulayın.
* Kaynak Yöneticisi ve Hizmet Yönetimi (Klasik) için Hello son PowerShell cmdlet'lerini yükleyin. Bu makalede, hello Azure portal ve PowerShell kullanın. Gerekli toocreate hello hello Klasik VNet toohello Resource Manager Vnet'i bağlantısından powershell'dir. Daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview). 

### <a name="values"></a>Örnek ayarlar

Bu değerleri toocreate bir test ortamı kullanın veya toothem başvurun toobetter anlamak bu makaledeki hello örnekler.

**Klasik VNet**

Sanal ağ adı ClassicVNet = <br>
Adres alanı 10.0.0.0/24 = <br>
Alt ağ 1 10.0.0.0/27 = <br>
Kaynak grubu ClassicRG = <br>
Konum Batı ABD = <br>
GatewaySubnet 10.0.0.32/28 = <br>
Yerel site RMVNetLocal = <br>

**Resource Manager Vnet'i**

Sanal ağ adı RMVNet = <br>
Adres alanı 192.168.0.0/16 = <br>
Alt ağ 1 192.168.1.0/24 = <br>
GatewaySubnet 192.168.0.0/26 = <br>
Kaynak grubu RG1 = <br>
Konum Doğu ABD = <br>
Sanal ağ geçidi adı RMGateway = <br>
Ağ geçidi türü VPN = <br>
VPN türü = rota tabanlı <br>
Ağ geçidi genel IP adresi adı rmgwpip = <br>
Yerel ağ geçidi ClassicVNetLocal = <br>
Bağlantı adı RMtoClassic =

### <a name="connection-overview"></a>Bağlantı genel bakış

Bu yapılandırma için hello sanal ağlar arasında bir IPSec/IKE VPN tüneli üzerinden VPN ağ geçidi bağlantı oluşturun. Sanal ağ Aralıklarınızın hiçbiri birbirleriyle ya da bağlandıkları hello yerel ağlar biriyle çakışmadığından emin olun.

Merhaba aşağıdaki tabloda hello örnek sanal ağlar ve yerel siteleri nasıl tanımlanan bir örnek gösterilmektedir:

| Sanal Ağ | Adres alanı | Bölge | Toolocal ağ sitesine bağlanır |
|:--- |:--- |:--- |:--- |
| ClassicVNet |(10.0.0.0/24) |Batı ABD | RMVNetLocal (192.168.0.0/16) |
| RMVNet | (192.168.0.0/16) |Doğu ABD |ClassicVNetLocal (10.0.0.0/24) |

## <a name="classicvnet"></a>1. Merhaba Klasik VNet ayarlarını yapılandırın

Bu bölümde, hello yerel oluşturduğunuz ağ (yerel site) ve klasik VNet için hello sanal ağ geçidi. Klasik bir VNet yoktur ve bu adımları bir alıştırma olarak çalıştırıyorsanız, kullanarak bir sanal ağ oluşturabilirsiniz [bu makalede](../virtual-network/virtual-networks-create-vnet-classic-pportal.md) ve hello [örnek](#values) üstten ayarlarının değerleri.

Merhaba portal toocreate Klasik sanal ağ kullanırken, aşağıdaki adımları, aksi takdirde hello seçeneği toocreate bir Klasik sanal ağı görünmez hello kullanarak toohello sanal ağ dikey gitmeniz gerekir:

1. Merhaba tıklatın '+' tooopen hello 'Yeni' dikey.
2. 'Sanal ağ' Hello 'Arama hello Market' alanına yazın. Bunun yerine, ağ seçerseniz sanal ağ ->, klasik bir VNet hello seçeneği toocreate almazsınız.
3. 'Sanal ağ' hello listesi döndürdü bulun ve tooopen hello sanal ağ dikey tıklatın. 
4. Merhaba sanal ağ dikey penceresinde 'Klasik' toocreate klasik bir VNet seçin. 

Bir VPN ağ geçidi ile bir VNet zaten varsa o hello ağ geçidi dinamik olduğunu doğrulayın. Statik ise, gerekir ilk hello VPN ağ geçidini silin ve ardından devam edin.

Ekran görüntüleri örnek olarak verilmiştir. Merhaba değerleri kendi değerlerinizle emin tooreplace olması ya da hello kullan [örnek](#values) değerleri.

### <a name="part-1---configure-hello-local-site"></a>Bölüm 1 - hello yerel site yapılandırma

Açık hello [Azure portal](https://ms.portal.azure.com) ve Azure hesabınızla oturum açın.

1. Çok gidin**tüm kaynakları** ve hello bulun **ClassicVNet** hello listesinde.
2. Merhaba üzerinde **genel bakış** dikey penceresinde hello **VPN bağlantıları** bölümünde, hello tıklatın **ağ geçidi** grafik toocreate bir ağ geçidi.

    ![Bir VPN ağ geçidi yapılandırma](./media/vpn-gateway-connect-different-deployment-models-portal/gatewaygraphic.png "bir VPN ağ geçidi yapılandırma")
3. Merhaba üzerinde **yeni VPN bağlantısı** dikey penceresinde için **bağlantı türü**seçin **siteden siteye**.
4. İçin **yerel site**, tıklatın **gerekli ayarları Yapılandır**. Merhaba açılır **yerel site** dikey.
5. Merhaba üzerinde **yerel site** dikey penceresinde, adı toorefer toohello Resource Manager Vnet'i oluşturun. Örneğin, 'RMVNetLocal'.
6. Merhaba Resource Manager Vnet'i için Hello VPN ağ geçidi genel IP adresi zaten varsa, hello değeri Merhaba kullanın **VPN ağ geçidi IP adresi** alan. Bu adımları bir alıştırma olarak işleminden olduğundan veya bir sanal ağ geçidi için Resource Manager Vnet'i henüz yoksa, bir yer tutucu IP adresini yapabilirsiniz. Merhaba yer tutucu IP adresi geçerli bir biçim kullandığından emin olun. Daha sonra hello hello Resource Manager sanal ağ geçidinin genel IP adresi ile Merhaba yer tutucu IP adresini değiştirin.
7. İçin **istemci adres alanı**, hello sanal ağ IP adresi alanlarını hello Resource Manager Vnet'i için başlangıç değerlerini kullanın. Bu ayar kullanılan toospecify hello adres alanları tooroute toohello Resource Manager sanal ağdır.
8. Tıklatın **Tamam** toosave hello değerleri ve dönüş toohello **yeni VPN bağlantısı** dikey.

### <a name="part-2---create-hello-virtual-network-gateway"></a>Bölüm 2 - hello sanal ağ geçidi oluşturma

1. Merhaba üzerinde **yeni VPN bağlantısı** dikey penceresinde, select hello **ağ geçidini hemen Oluştur** onay kutusunu tıklatıp **isteğe bağlı ağ geçidi Yapılandırması** tooopen hello  **Ağ geçidi Yapılandırması** dikey. 

    ![Açık ağ geçidi yapılandırma dikey](./media/vpn-gateway-connect-different-deployment-models-portal/optionalgatewayconfiguration.png "açık ağ geçidi yapılandırma dikey penceresi")
2. Tıklatın **Subnet - gerekli ayarları Yapılandır** tooopen hello **alt ağ Ekle** dikey. Merhaba **adı** gerekli hello değerle zaten yapılandırılmış **GatewaySubnet**.
3. Merhaba **adres aralığı** toohello aralığı hello ağ geçidi alt ağı başvuruyor. Bir ağ geçidi alt ağı ile/29 oluşturabilseniz adres aralığı (3 adresleri), daha fazla IP adreslerini içeren bir ağ geçidi alt ağı oluşturma öneririz. Bu, daha fazla kullanılabilir IP adreslerini gerektirebilir gelecekteki yapılandırmaları uyum sağlayacak. Mümkünse, / 27 veya /28 kullanın. Bu adımları bir alıştırma olarak kullanıyorsanız, toohello başvurabilir [örnek](#values) değerleri. Tıklatın **Tamam** toocreate hello ağ geçidi alt ağı.
4. Merhaba üzerinde **ağ geçidi Yapılandırması** dikey penceresinde **boyutu** toohello ağ geçidi SKU'su başvuruyor. VPN ağ geçidinizi için SKU Hello ağ geçidi seçin.
5. Merhaba doğrulayın **yönlendirme türü** olan **dinamik**, ardından **Tamam** tooreturn toohello **yeni VPN bağlantısı** dikey.
6. Merhaba üzerinde **yeni VPN bağlantısı** dikey penceresinde tıklatın **Tamam** toobegin VPN ağ geçidinizi oluşturma. Bir VPN ağ geçidi oluşturma too45 dakika toocomplete alabilir.

### <a name="ip"></a>Bölüm 3 - kopyalama hello sanal ağ geçidi genel IP adresi

Merhaba sanal ağ geçidi oluşturulduktan sonra hello ağ geçidi IP adresini görüntüleyebilirsiniz. 

1. Tooyour gidin Klasik VNet ve tıklatın **genel bakış**.
2. Tıklatın **VPN bağlantıları** tooopen hello VPN bağlantıları dikey. Merhaba VPN bağlantıları dikey penceresinde hello genel IP adresini görüntüleyebilirsiniz. Bu tooyour sanal ağ geçidi atanmış hello genel IP adresidir. 
3. Not edin veya başlangıç IP adresi kopyalayın. Resource Manager yerel ağ geçidi yapılandırma ayarlarınızı ile çalışırken, sonraki adımlarda kullanın. Ağ geçidi bağlantılarınızı hello durumunu da görüntüleyebilirsiniz. Oluşturduğunuz bildirim hello yerel ağ sitesine 'Bağlanıyor' olarak listelenir. bağlantılarınızı oluşturduktan sonra hello durumunu değiştirir.
4. Merhaba ağ geçidi IP adresi kopyaladıktan sonra Hello dikey penceresini kapatın.

## <a name="rmvnet"></a>2. Merhaba Kaynak Yöneticisi VNet ayarlarını yapılandırın

Bu bölümde, Kaynak Yöneticisi'ni ağınız için hello sanal ağ geçidi ve hello yerel ağ geçidi oluşturun. Resource Manager Vnet'i yoktur ve bu adımları bir alıştırma olarak çalıştırıyorsanız, kullanarak bir sanal ağ oluşturabilirsiniz [bu makalede](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) ve hello [örnek](#values) üstten ayarlarının değerleri.

Ekran görüntüleri örnek olarak verilmiştir. Merhaba değerleri kendi değerlerinizle emin tooreplace olması ya da hello kullan [örnek](#values) değerleri.

### <a name="part-1---create-a-gateway-subnet"></a>Bölüm 1 - bir ağ geçidi alt ağı oluşturun.

Bir sanal ağ geçidi oluşturmadan önce ilk toocreate hello ağ geçidi alt ağı gerekir. CIDR sayısıyla 28 ya da daha büyük bir ağ geçidi alt ağı oluşturun. (/ 27, / 26, vb..)

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-rm-portal-include.md)]

### <a name="part-2---create-a-virtual-network-gateway"></a>Bölüm 2 - bir sanal ağ geçidi oluşturma

[!INCLUDE [vpn-gateway-add-gw-rm-portal](../../includes/vpn-gateway-add-gw-rm-portal-include.md)]

### <a name="createlng"></a>Bölüm 3 - bir yerel ağ geçidi oluşturma

Merhaba yerel ağ geçidi hello adres aralığı ve klasik VNet ve kendi sanal ağ geçidi ile ilişkili hello ortak IP adresi belirtir.

Bu adımları bir alıştırma olarak yapıyorsanız, toothese ayarları bakın:

| Sanal Ağ | Adres alanı | Bölge | Toolocal ağ sitesine bağlanır |Ağ geçidi genel IP adresi|
|:--- |:--- |:--- |:--- |:--- |
| ClassicVNet |(10.0.0.0/24) |Batı ABD | RMVNetLocal (192.168.0.0/16) |Merhaba toohello ClassicVNet ağ geçidi atanan genel IP adresi|
| RMVNet | (192.168.0.0/16) |Doğu ABD |ClassicVNetLocal (10.0.0.0/24) |Merhaba toohello RMVNet ağ geçidi atanan genel IP adresi.|

[!INCLUDE [vpn-gateway-add-lng-rm-portal](../../includes/vpn-gateway-add-lng-rm-portal-include.md)]

## <a name="modifylng"></a>3. Merhaba Klasik VNet yerel site ayarlarını değiştirme

Bu bölümde, hello yerel site ayarları hello Resource Manager VPN ağ geçidi IP adresi ile belirtirken kullanılan hello yer tutucu IP adresini değiştirin. Bu bölümde hello Klasik (SM) PowerShell cmdlet'lerini kullanır.

1. Hello Azure portal, toohello Klasik sanal ağ gidin.
2. Sanal ağınız için Hello dikey penceresinde **genel bakış**.
3. Merhaba, **VPN bağlantıları** bölümünde, yerel hello grafik sitenizdeki hello adına tıklayın.

    ![VPN bağlantıları](./media/vpn-gateway-connect-different-deployment-models-portal/vpnconnections.png "VPN bağlantıları")
4. Merhaba üzerinde **siteden siteye VPN bağlantıları** dikey penceresinde hello site hello adına tıklayın.

    ![Site adı](./media/vpn-gateway-connect-different-deployment-models-portal/sitetosite3.png "yerel site adı")
5. Merhaba bağlantı dikey penceresinde yerel sitenizi, hello yerel site tooopen hello hello adına tıklayın **yerel site** dikey.

    ![Açık yerel site](./media/vpn-gateway-connect-different-deployment-models-portal/openlocal.png "yerel site Aç")
6. Merhaba üzerinde **yerel site** dikey penceresinde, Değiştir hello **VPN ağ geçidi IP adresi** hello IP adresiyle hello Resource Manager ağ geçidi.

    ![Ağ geçidi IP adresi](./media/vpn-gateway-connect-different-deployment-models-portal/gwipaddress.png "ağ geçidi IP adresi")
7. Tıklatın **Tamam** tooupdate başlangıç IP adresi.

## <a name="RMtoclassic"></a>4. Resource Manager tooclassic bağlantısı oluşturma

Bu adımlarda, yapılandırdığınız hello Resource Manager Vnet'i hello bağlantısından toohello Klasik VNet kullanarak hello Azure portalı.

1. İçinde **tüm kaynakları**, hello yerel ağ geçidi bulun. Bizim örneğimizde, hello yerel ağ geçididir **ClassicVNetLocal**.
2. Tıklatın **yapılandırma** ve başlangıç IP adresi değeri hello için hello VPN ağ geçidi olduğundan emin olun Klasik VNet. Gerekirse, güncelleştirin ve ardından **kaydetmek**. Kapat hello dikey.
3. İçinde **tüm kaynakları**, hello yerel ağ geçidi'ı tıklatın.
4. Tıklatın **bağlantıları** tooopen hello bağlantıları dikey.
5. Merhaba üzerinde **bağlantıları** dikey penceresinde tıklatın  **+**  tooadd bir bağlantı.
6. Merhaba üzerinde **Bağlantı Ekle** dikey penceresinde, adı hello bağlantı. Örneğin, 'RMtoClassic'.
7. **Siteden siteye** bu dikey pencerede zaten seçilidir.
8. Bu site ile tooassociate istediğiniz hello sanal ağ geçidi seçin.
9. Oluşturma bir **paylaşılan anahtar**. Bu anahtar ayrıca hello Klasik VNet toohello Resource Manager Vnet'i oluşturduğunuz hello bağlantı kullanılır. Başlangıç anahtarı oluşturmak veya bir oluşturur. Örneğimizde 'abc123' kullanıyoruz, ancak daha karmaşık bir şey olabilir ve kullanmanız gerekir.
10. Tıklatın **Tamam** toocreate hello bağlantı.

##<a name="classictoRM"></a>5. Klasik tooResource Yöneticisi bağlantısı oluşturma

Bu adımlarda, hello Klasik VNet toohello Resource Manager Vnet'i hello bağlantısından yapılandırın. Bu adımları PowerShell gerektirir. Merhaba Portalı'nda bu bağlantı oluşturamıyor. İndirilen ve hello Klasik (SM) ve Kaynak Yöneticisi (RM) PowerShell cmdlet'lerini yüklü emin olun.

### <a name="1-connect-tooyour-azure-account"></a>1. Azure hesabı tooyour Bağlan

Yükseltilmiş haklara sahip Hello PowerShell konsolu açın ve oturum tooyour Azure hesabı. Merhaba aşağıdaki cmdlet'i, hello oturum açma kimlik bilgilerini Azure hesabınız için ister. Kullanılabilir tooAzure PowerShell; böylece oturum açtıktan sonra hesap ayarlarınızı indirilir.

```powershell
Login-AzureRmAccount
```
   
Birden fazla aboneliğiniz varsa, Azure aboneliklerinize listesini alın.

```powershell
Get-AzureRmSubscription
```

Merhaba abonelik toouse istediğinizi belirtin. 

```powershell
Select-AzureRmSubscription -SubscriptionName "Name of subscription"
```

Azure hesap toouse hello Klasik PowerShell cmdlet'leri (SM) ekleyin. toodo bu nedenle, komutu aşağıdaki hello kullanabilirsiniz:

```powershell
Add-AzureAccount
```

### <a name="2-view-hello-network-configuration-file-values"></a>2. Merhaba ağ yapılandırma dosyası değerlerini görüntüleme

Hello Azure portalında VNet oluşturduğunuzda, Azure kullandığı hello tam adı hello Azure portalında görünür değil. Örneğin, 'ClassicVNet' hello Azure portal adlı toobe görünür bir VNet hello ağ yapılandırma dosyasında bir kadar daha uzun bir ad olabilir. Merhaba adı şöyle görünebilir: 'Grup ClassicRG ClassicVNet'. Bu adımlarda, hello ağ yapılandırma dosyası ve görünüm hello değerlerini indirin.

Bilgisayarınızda bir dizin oluşturun ve ardından hello ağ yapılandırma dosyası toohello dizini verin. Bu örnekte, hello ağ yapılandırmasını dışarı aktarılan tooC:\AzureNet dosyasıdır.

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

Bir metin düzenleyicisi ve görünüm hello adı Klasik vnet ile Merhaba dosyasını açın. Hello adları PowerShell cmdlet'lerini çalıştırırken hello ağ yapılandırma dosyası kullanın.

- Sanal ağ adları olarak listelenen **VirtualNetworkSite adı =**
- Site adları olarak listelenen **LocalNetworkSite adı =**

### <a name="3-create-hello-connection"></a>3. Merhaba bağlantısı oluşturma

Merhaba paylaşılan anahtarı ayarlayın ve hello Klasik VNet toohello Resource Manager Vnet'i hello bağlantı oluşturun. Merhaba portal kullanarak hello paylaşılan anahtar ayarlanamıyor. Merhaba PowerShell cmdlet'leri Klasik sürümü hello kullanarak oturum açıp aşağıdaki adımları çalıştırdığınızdan emin olun. Bu nedenle, toodo kullanmak **Add-AzureAccount**. Aksi takdirde mümkün tooset hello olmaz '-AzureVNetGatewayKey'.

- Bu örnekte, **- vnetname adlı** hello adıdır hello olarak Klasik VNet ağ yapılandırma dosyanızda bulundu. 
- Merhaba **- LocalNetworkSiteName** ağ yapılandırma dosyanızda olarak hello yerel site için belirttiğiniz hello adı bulunamadı.
- Merhaba **- SharedKey** oluşturmak ve belirten bir değer. Bu örnekte, kullandık *abc123*, ancak daha karmaşık bir şey oluşturabilirsiniz. Burada belirttiğiniz başlangıç değeri şeydir önemli Hello hello aynı Resource Manager tooclassic bağlantınızı oluştururken, belirtilen değeri olmalıdır.

```powershell
Set-AzureVNetGatewayKey -VNetName "Group ClassicRG ClassicVNet" `
-LocalNetworkSiteName "172B9E16_RMVNetLocal" -SharedKey abc123
```

##<a name="verify"></a>6. Bağlantılarınızı doğrulayın

Azure portal veya PowerShell kullanarak bağlantılarınızı hello doğrulayabilirsiniz. Merhaba bağlantı oluşturuldu olarak doğrulanırken, toowait veya iki dakika gerekebilir. Bağlantı başarılı olduğunda, 'Bağlanıyor' too'Connected hello bağlantı durumu değiştirir '.

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a>Klasik VNet tooyour Resource Manager Vnet'i tooverify hello bağlantısından

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

###<a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a>Resource Manager Vnet'i tooyour tooverify hello bağlantısından Klasik VNet

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="faq"></a>Sanal ağlar arası bağlantılar hakkında SSS

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]
