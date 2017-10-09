---
title: "Sanal ağlar arasında bir bağlantı oluşturun: Klasik: Azure portal | Microsoft Docs"
description: "Nasıl birlikte tooconnect Azure sanal ağları PowerShell kullanarak ve klasik Azure portalı hello."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: f29c3c091d049ff96cf59f4c28ab86a100bcb5fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-connection-classic"></a>VNet-VNet bağlantı (Klasik) yapılandırma

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

Bu makale size nasıl gösterir toocreate sanal ağlar arasında bir VPN ağ geçidi bağlantısı. Merhaba sanal ağları olabilir hello aynı ya da farklı bölgelerde ve gelen aynı hello ya da farklı Aboneliklerde. Bu makalede Hello adımlar toohello Klasik dağıtım modeli ve hello Azure portal geçerlidir. Liste aşağıdaki hello farklı bir seçeneği seçerek farklı dağıtım aracını veya dağıtım modelini kullanarak bu yapılandırma ayrıca oluşturabilirsiniz:

> [!div class="op_single_selector"]
> * [Azure portal](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Azure CLI](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Azure portal (klasik)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Farklı dağıtım modellerini bağlama - Azure portalı](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Farklı dağıtım modellerini bağlama - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

![VNet tooVNet bağlantı diyagramı](./media/vpn-gateway-howto-vnet-vnet-portal-classic/v2vclassic.png)

## <a name="about-vnet-to-vnet-connections"></a>Sanal Ağdan Sanal Ağa bağlantıları hakkında

Bir VPN ağ geçidi kullanarak hello Klasik dağıtım modelinde bir sanal ağ tooanother sanal ağ (VNet-VNet) bağlanma benzer tooconnecting bir sanal ağ tooan şirket içi site konumuna olur. Her iki bağlantı türü bir VPN ağ geçidi tooprovide IPSec/IKE kullanarak güvenli bir tünel kullanın.

Merhaba bağlandığınız sanal ağlar farklı Aboneliklerde ve farklı bölgelerde olabilir. VNet tooVNet iletişimini çok siteli yapılandırmalarla birleştirebilirsiniz. Bu özellik şirket içi ve şirket dışı bağlantıyla ağ içi bağlantıyı birleştiren ağ topolojileri kurabilmenize olanak sağlar.

![VNet tooVNet bağlantıları](./media/vpn-gateway-howto-vnet-vnet-portal-classic/aboutconnections.png)

### <a name="why"></a>Sanal ağları neden bağlamalıyız?

Aşağıdaki nedenlerden Merhaba tooconnect sanal ağlar isteyebilirsiniz:

* **Çapraz bölge coğrafi artıklığı ve coğrafi-durum**

  * Kendi coğrafi çoğaltma veya eşitlemenizi, güvenli bağlantıyla İnternet’te uç noktalara gitmeden ayarlayabilirsiniz.
  * Azure yük dengeleyici ve Microsoft veya üçüncü taraf kümeleme teknolojisi yüksek oranda kullanılabilir iş yükü coğrafi yedeklilik ile birçok Azure bölgesinde ayarlayabilirsiniz. Bir önemli SQL Always On kullanılabilirlik grupları: birden fazla Azure bölgesine yayılan ile yukarı tooset örnektir.
* **Güçlü yalıtım sınırı ile bölgesel çok katmanlı uygulamalar**

  * İçinde hello aynı bölge, güçlü yalıtım ve güvenli arası katmanı iletişimi ile birlikte bağlı birden çok sanal ağlar ile çok katmanlı uygulamalar ayarlayabilirsiniz.
* **Abonelik, Azure arası kuruluş iletişiminde arası**

  * Birden çok Azure aboneliğiniz varsa, farklı Aboneliklerde iş yüklerini birlikte güvenli bir şekilde sanal ağlar arasında bağlanabilirsiniz.
  * Kuruluşlar veya hizmet sağlayıcıları için Azure içinde güvenli VPN teknolojisi ile çapraz kuruluş iletişim etkinleştirebilirsiniz.

VNet-VNet bağlantıları hakkında daha fazla bilgi için bkz: [VNet-VNet konuları](#faq) hello bu makalenin sonunda.

### <a name="before-you-begin"></a>Başlamadan önce

Bu alıştırmaya başlamadan önce indirin ve hello hello Azure Hizmet Yönetimi (SM) PowerShell cmdlet'lerinin en son sürümünü yükleyin. Daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview). Hello portal hello adımları çoğu için kullanıyoruz, ancak PowerShell toocreate hello bağlantıları hello sanal ağlar arasında kullanmanız gerekir. Hello Azure portal kullanarak hello bağlantı oluşturulamıyor.

## <a name="plan"></a>1. adım -, IP adres aralıklarını planlama

Bu sanal ağlarınızın tooconfigure kullanacağınız önemli toodecide hello aralıkları olur. Bu yapılandırma için sanal ağ Aralıklarınızın hiçbiri birbirleriyle ya da bağlandıkları hello yerel ağlar biriyle çakışmayan emin olmanız gerekir.

Merhaba aşağıdaki tabloda gösterilmektedir nasıl bir örnek toodefine, sanal ağlar. Merhaba aralıkları yalnızca bir kılavuz olarak kullanın. Merhaba aralıkları, sanal ağlar için aşağı yazın. Sonraki adımlar için bu bilgileri gerekir.

**Örnek**

| Sanal Ağ | Adres alanı | Bölge | Toolocal ağ sitesine bağlanır |
|:--- |:--- |:--- |:--- |
| TestVNet1 |TestVNet1<br>(10.11.0.0/16)<br>(10.12.0.0/16) |Doğu ABD |VNet4Local<br>(10.41.0.0/16)<br>(10.42.0.0/16) |
| TestVNet4 |TestVNet4<br>(10.41.0.0/16)<br>(10.42.0.0/16) |Batı ABD |VNet1Local<br>(10.11.0.0/16)<br>(10.12.0.0/16) |

## <a name="vnetvalues"></a>2. adım - hello sanal ağlar oluşturun

Hello iki sanal ağ oluşturma [Azure portal](https://portal.azure.com). Merhaba toocreate Klasik sanal ağlar adımları için bkz: [Klasik sanal ağ oluşturma](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). 

Merhaba portal toocreate Klasik sanal ağ kullanırken, aşağıdaki adımları, aksi takdirde hello seçeneği toocreate bir Klasik sanal ağı görünmez hello kullanarak toohello sanal ağ dikey gitmeniz gerekir:

1. Merhaba tıklatın '+' tooopen hello 'Yeni' dikey.
2. 'Sanal ağ' Hello 'Arama hello Market' alanına yazın. Bunun yerine, ağ seçerseniz sanal ağ ->, klasik bir VNet hello seçeneği toocreate almazsınız.
3. 'Sanal ağ' hello listesi döndürdü bulun ve tooopen hello sanal ağ dikey tıklatın. 
4. Merhaba sanal ağ dikey penceresinde 'Klasik' toocreate klasik bir VNet seçin. 

Bu makalede bir alıştırma olarak kullanıyorsanız, örnek değerleri aşağıdaki hello kullanabilirsiniz:

**TestVNet1 için değerler**

Ad: TestVNet1<br>
Adres alanı: 10.11.0.0/16, 10.12.0.0/16 (isteğe bağlı)<br>
Alt ağ adı: varsayılan<br>
Alt ağ adresi aralığı: 10.11.0.1/24<br>
Kaynak grubu: ClassicRG<br>
Location: East US<br>
GatewaySubnet: 10.11.1.0/27

**TestVNet4 için değerler**

Ad: TestVNet4<br>
Adres alanı: 10.41.0.0/16, 10.42.0.0/16 (isteğe bağlı)<br>
Alt ağ adı: varsayılan<br>
Alt ağ adresi aralığı: 10.41.0.1/24<br>
Kaynak grubu: ClassicRG<br>
Location: West US<br>
GatewaySubnet: 10.41.1.0/27

**Sanal ağlar oluştururken göz hello ayarları aşağıdaki alın:**

* **Sanal ağ adres alanları** – hello sanal ağ adres alanları sayfasında, sanal ağınız için toouse istediğiniz hello adres aralığını belirtin. Bunlar toohello VM'ler ve toothis sanal ağı dağıtmak diğer rol örneklerine atanacak hello dinamik IP adresleridir.<br>Bu VNet bağlanacağı başka sanal ağlara veya şirket içi konumlara hello hello adres alanları seçtiğiniz herhangi biri için hello adres alanları ile örtüşemez.

* **Konum** – bir sanal ağ oluşturduğunuzda, Azure bir konum (bölge) ile ilişkilendirin. Örneğin, Batı ABD fiziksel olarak bulunan tooyour sanal ağ toobe olan Vm'leriniz dağıtılan istiyorsanız, o konumu seçin. Oluşturduktan sonra sanal ağınızla ilişkili hello konumu değiştirilemiyor.

**Sanal ağlar oluşturduktan sonra ayarlar aşağıdaki hello ekleyebilirsiniz:**

* **Adres alanı** – ek adres alanı, bu yapılandırma için gerekli değildir, ancak hello VNet oluşturduktan sonra ek adres alanı ekleyebilirsiniz.

* **Alt ağlar** – ek alt ağlar bu yapılandırma için gerekli değildir, ancak Vm'lerinizi diğer rol örneklerinizden ayrı bir alt ağda toohave isteyebilirsiniz.

* **DNS sunucuları** – hello DNS sunucusu adı ve IP adresi girin. Bu ayarla bir DNS sunucusu oluşturulmaz. Bu sanal ağ için ad çözümlemesi için toouse istediğiniz toospecify hello DNS sunucuları sağlar.

Bu bölümdeki hello bağlantı türü, hello yerel site, yapılandırma ve hello ağ geçidi oluşturun.

## <a name="localsite"></a>3. adım - hello yerel site yapılandırma

Azure hello ayarlarını nasıl tooroute hello sanal ağlar arasında trafiği her yerel ağ sitesi toodetermine belirtildi. Her bir Vnet'teki tooroute trafiği istediğiniz toohello ilgili yerel ağ işaret etmelidir. Toouse toorefer tooeach yerel ağ sitesine hello adını belirleyin. En iyi toouse bir tanımlayıcı değil.

Örneğin, TestVNet1 'VNet4Local' adlı, oluşturduğunuz tooa yerel ağ sitesine bağlanır. VNet4Local Hello ayarlarını hello adres öneklerini için testvnet4'ü içerir.

Merhaba yerel olan her bir Vnet'teki hello için diğer sanal ağ sitesi. örnek değerler aşağıdaki hello yapılandırmamızın için kullanılır:

| Sanal Ağ | Adres alanı | Bölge | Toolocal ağ sitesine bağlanır |
|:--- |:--- |:--- |:--- |
| TestVNet1 |TestVNet1<br>(10.11.0.0/16)<br>(10.12.0.0/16) |Doğu ABD |VNet4Local<br>(10.41.0.0/16)<br>(10.42.0.0/16) |
| TestVNet4 |TestVNet4<br>(10.41.0.0/16)<br>(10.42.0.0/16) |Batı ABD |VNet1Local<br>(10.11.0.0/16)<br>(10.12.0.0/16) |

1. TestVNet1 hello Azure portalı bulun. Merhaba, **VPN bağlantıları** bölüm hello dikey pencerenin tıklatın **ağ geçidi**.

    ![Ağ geçidi yok](./media/vpn-gateway-howto-vnet-vnet-portal-classic/nogateway.png)
2. Merhaba üzerinde **yeni VPN bağlantısı** sayfasında, **siteden siteye**.
3. Tıklatın **yerel site** tooopen yerel site sayfası hello ve hello ayarlarını yapılandırın.
4. Merhaba üzerinde **yerel site** sayfasında, yerel site adı. Bizim örneğimizde, biz 'VNet4Local' hello yerel site adı.
5. İçin **VPN ağ geçidi IP adresi**, geçerli bir biçimde olduğu sürece, istediğiniz herhangi bir IP adresi kullanabilirsiniz. Genellikle, bir VPN cihazı için hello gerçek dış IP adresi kullanırsınız. Ancak, klasik bir VNet-VNet yapılandırması toohello ağ geçidi ağınız için atanan hello genel IP adresi kullanın. Merhaba sanal ağ geçidi henüz oluşturduğunuz koşuluyla, bir yer tutucu olarak herhangi bir geçerli ortak IP adresi belirtin.<br>Bu boş bırakmayın - bu yapılandırma için isteğe bağlı değil. Sonraki adımda, bu ayarlar geri dönün ve Azure ürettiği sonra bunları hello karşılık gelen sanal ağ ağ geçidi IP adresiyle yapılandırın.
6. İçin **istemci adres alanı**, diğer Vnet'in hello hello adres alanı kullanın. Örnek planlama tooyour bakın. Tıklatın **Tamam** toosave ayarlarınızı ve geri dönüş toohello **yeni VPN bağlantısı** dikey.

    ![yerel site](./media/vpn-gateway-howto-vnet-vnet-portal-classic/localsite.png)

## <a name="gw"></a>4. adım - hello sanal ağ geçidi oluşturma

Her sanal ağ, bir sanal ağ geçidi olmalıdır. Merhaba sanal ağ geçidi yönlendirir ve trafiği şifreler.

1. Merhaba üzerinde **yeni VPN bağlantısı** dikey penceresinde, select hello onay kutusunu **ağ geçidini hemen Oluştur**.
2. Tıklatın **alt ağ, boyut, yönlendirme türü**. Merhaba üzerinde **ağ geçidi Yapılandırması** dikey penceresinde tıklatın **alt**.
3. Merhaba ağ geçidi alt ağ adı otomatik olarak hello gerekli adı 'GatewaySubnet' ile doldurulur. Merhaba **adres aralığı** toohello VPN ağ geçidi Hizmetleri ayrılan hello IP adreslerini içerir. Bazı yapılandırmalar /29 ancak, en iyi toouse ağ geçidi alt ağı/28 ya da /27 izin daha fazla IP adresi için Ağ Geçidi Hizmetleri hello gerektirebilir tooaccommodate gelecekteki yapılandırmaları. Bizim örnek ayarlarında 10.11.1.0/27 kullanırız. Merhaba adres alanı ayarlamanız ve ardından **Tamam**.
4. Merhaba yapılandırma **ağ geçidi boyutu**. Bu ayar toohello başvuruyor [ağ geçidi SKU'su](vpn-gateway-about-vpn-gateway-settings.md#gwsku).
5. Merhaba yapılandırma **yönlendirme türü**. Bu yapılandırma için yönlendirme türü hello **dinamik**. Merhaba ağ geçidi kesmeden ve yeni bir tane oluşturun sürece hello yönlendirme türü daha sonra değiştiremezsiniz.
6. **Tamam** düğmesine tıklayın.
7. Merhaba üzerinde **yeni VPN bağlantısı** dikey penceresinde tıklatın **Tamam** toobegin hello sanal ağ geçidi oluşturma. Bir ağ geçidi oluşturma 45 dakika veya daha fazla hello seçilen ağ geçidi SKU'su bağlı olarak genellikle alabilir.

## <a name="vnet4settings"></a>5. adım - TestVNet4 ayarlarını yapılandırma

Çok Hello adımları yineleyin[bir yerel site oluşturma](#localsite) ve [hello sanal ağ geçidi Oluştur](#gw) hello değerleri gerektiğinde değiştirerek tooconfigure TestVNet4,. Bu bir alıştırma olarak yapıyorsanız, hello kullan [örnek değerler](#vnetvalues).

## <a name="updatelocal"></a>Adım 6 - güncelleştirme hello yerel siteleri

Her iki sanal ağlar için sanal ağ geçitlerini oluşturulduktan sonra hello yerel siteleri ayarlamanız gerekir **VPN ağ geçidi IP adresi** değerleri.

|VNet adı|Bağlantılı site|Ağ geçidi IP adresi|
|:--- |:--- |:--- |
|TestVNet1|VNet4Local|TestVNet4 için VPN ağ geçidi IP adresi|
|TestVNet4|VNet1Local|TestVNet1 için VPN ağ geçidi IP adresi|

### <a name="part-1---get-hello-virtual-network-gateway-public-ip-address"></a>Bölüm 1 - Get hello sanal ağ geçidi genel IP adresi

1. Sanal ağınızı hello Azure portalı bulun.
2. Tooopen hello VNet tıklatın **genel bakış** dikey. Merhaba dikey olarak **VPN bağlantıları**, sanal ağ geçidiniz için hello IP adresini görüntüleyebilirsiniz.

  ![Genel IP](./media/vpn-gateway-howto-vnet-vnet-portal-classic/publicIP.png)
3. Başlangıç IP adresi kopyalayın. Merhaba sonraki bölümde kullanır.
4. TestVNet4 için bu adımları yineleyin

### <a name="part-2---modify-hello-local-sites"></a>Bölüm 2 - hello yerel siteleri değiştirme

1. Sanal ağınızı hello Azure portalı bulun.
2. Merhaba VNet üzerinde **genel bakış** dikey penceresinde hello yerel site'ı tıklatın.

  ![Yerel site oluşturuldu](./media/vpn-gateway-howto-vnet-vnet-portal-classic/local.png)
3. Merhaba üzerinde **siteden siteye VPN bağlantıları** dikey penceresinde hello yerel site toomodify istediğiniz hello adına tıklayın.

  ![Yerel site Aç](./media/vpn-gateway-howto-vnet-vnet-portal-classic/openlocal.png)
4. Merhaba tıklatın **yerel site** toomodify istiyor.

  ![Site değiştirme](./media/vpn-gateway-howto-vnet-vnet-portal-classic/connections.png)
5. Güncelleştirme hello **VPN ağ geçidi IP adresi** tıklatıp **Tamam** toosave hello ayarları.

  ![ağ geçidi IP](./media/vpn-gateway-howto-vnet-vnet-portal-classic/gwupdate.png)
6. Diğer dikey pencereleri kapatmak hello.
7. TestVNet4 için bu adımları yineleyin.

## <a name="getvalues"></a>7. adım - hello ağ yapılandırma dosyası alma değerleri

Hello Azure portalında Klasik sanal ağlar oluşturduğunuzda, görüntülediğiniz hello adı için PowerShell kullanın hello tam adı değil. Örneğin, toobe adlı görünür bir VNet **TestVNet1** hello Portalı'nda hello ağ yapılandırma dosyasında bir kadar daha uzun bir ad olabilir. Merhaba adı şöyle görünebilir: **Grup ClassicRG TestVNet1**. Bağlantılarınızı oluşturduğunuzda hello ağ yapılandırma dosyasında gördüğünüz önemli toouse hello değerleri kullanılabilir.

Merhaba, aşağıdaki adımları tooyour Azure hesabı bağlanır ve indirme ve görünüm hello ağ yapılandırma dosyası tooobtain hello değerleri bağlantılarınız için gereklidir.

1. Merhaba hello Azure Hizmet Yönetimi (SM) PowerShell cmdlet'lerinin en son sürümünü yükleyip yeniden açın. Daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

2. Yükseltilmiş haklarla PowerShell Konsolunuzu açın ve tooyour hesap bağlanın. Bağlandığınız örnek toohelp aşağıdaki hello kullan:

  ```powershell
  Login-AzureRmAccount
  ```

  Merhaba hesabının Hello abonelikleri kontrol edin.

  ```powershell
  Get-AzureRmSubscription
  ```

  Birden fazla aboneliğiniz varsa, toouse istediğiniz hello aboneliği seçin.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
  ```

  Ardından, aşağıdaki cmdlet'i tooadd hello Azure aboneliği tooPowerShell hello Klasik dağıtım modeli için kullanın.

  ```powershell
  Add-AzureAccount
  ```
3. Dışarı aktarma ve hello ağ yapılandırma dosyasını görüntüleyin. Bilgisayarınızda bir dizin oluşturun ve ardından hello ağ yapılandırma dosyası toohello dizini verin. Bu örnekte, çok hello ağ yapılandırma dosyasını dışarı**C:\AzureNet**.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
4. Bir metin düzenleyicisi ve adlarıyla görünüm hello sanal ağlar ve siteler Hello dosyasını açın. Bunlar, bağlantılarınızı oluştururken kullandığınız hello ad olacaktır.<br>Sanal ağ adları olarak listelenen **VirtualNetworkSite adı =**<br>Site adları olarak listelenen **LocalNetworkSiteRef adı =**

## <a name="createconnections"></a>8. adım - hello VPN ağ geçidi bağlantıları oluşturma

Tüm hello önceki adımları tamamladıktan sonra hello IPSec/IKE önceden paylaşılan anahtarlar ayarlayın ve hello bağlantı oluşturun. Bu adımlar, PowerShell kullanıyor. Merhaba Klasik dağıtım modeli için VNet-VNet bağlantıları hello Azure portal yapılandırılamaz.

Merhaba örneklerde paylaşılan anahtar hello bildirimi olan tam olarak hello aynı. Merhaba paylaşılan anahtarı her zaman aynı olmalıdır. Sanal ağlar ve yerel ağ sitelerinin hello tam adlarıyla Bu örneklerde hello değerleri emin tooreplace olması.

1. Merhaba TestVNet1 tooTestVNet4 bağlantı oluşturun.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group ClassicRG TestVNet1' `
  -LocalNetworkSiteName '17BE5E2C_VNet4Local' -SharedKey A1b2C3D4
  ```
2. Merhaba TestVNet4 tooTestVNet1 bağlantı oluşturun.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group ClassicRG TestVNet4' `
  -LocalNetworkSiteName 'F7F7BFC7_VNet1Local' -SharedKey A1b2C3D4
  ```
3. Merhaba bağlantıları tooinitialize bekleyin. Hello ağ geçidi başlatıldı sonra hello durumu 'Başarılı' dir.

  ```
  Error          :
  HttpStatusCode : OK
  Id             :
  Status         : Successful
  RequestId      :
  StatusCode     : OK
  ```

## <a name="faq"></a>Klasik sanal ağlar için VNet-VNet konuları
* Merhaba sanal ağlar hello olabilir aynı ya da farklı Aboneliklerde.
* Merhaba sanal ağlar hello olabilir aynı veya farklı Azure bölgeleri (konumlara).
* Bir bulut hizmeti ya da yük dengeleme uç noktası, birbirlerine bağlı olsa da sanal ağlara yayılamaz.
* Birden çok sanal ağları birbirine bağlama hiçbir VPN cihazı gerektirmez.
* VNet-VNet Azure sanal ağları bağlamayı destekler. Bağlanan sanal makineleri desteklemez veya tooa sanal ağ olmayan bulut Hizmetleri dağıtılabilir.
* VNet-VNet dinamik yönlendirme ağ geçitleri gerektirir. Azure statik yönlendirme ağ geçitleri desteklenmez.
* Sanal ağ bağlantısı, çoklu site VPN’leri ile eşzamanlı olarak kullanılabilir. En fazla 10 VPN tünelleri tooeither diğer sanal ağları veya şirket içi sitelere bağlanan sanal ağ VPN ağ geçidi için yoktur.
* Merhaba adres alanları hello sanal ağlar ve şirket içi yerel ağ sitesi çakışmaması gerekir. Çakışan adres alanlarının sanal ağları veya karşıya yükleme netcfg yapılandırma dosyaları toofail hello oluşturulmasına neden olur.
* Bir çift sanal ağ arasındaki yedekli tüneller desteklenmez.
* Tüm VPN tünelleri Merhaba VNet, P2S VPN'ler dahil olmak üzere, hello hello VPN ağ geçidi için kullanılabilir bant genişliğini paylaştırmak ve aynı VPN ağ geçidi çalışma süresi SLA azure'da hello.
* VNet-VNet trafiği Azure omurga hello arasında geçen.

## <a name="next-steps"></a>Sonraki adımlar
Bağlantılarınızı doğrulayın. Bkz: [bir VPN ağ geçidi bağlantısını doğrulama](vpn-gateway-verify-connection-resource-manager.md).
