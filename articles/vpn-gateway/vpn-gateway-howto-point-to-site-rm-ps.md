---
title: "Bilgisayar tooan noktası Site kullanarak Azure sanal ağı bağlanmak ve sertifika kimlik doğrulaması: PowerShell | Microsoft Docs"
description: "Sertifika kimlik doğrulaması kullanarak bir noktadan siteye VPN ağ geçidi bağlantısı oluşturarak güvenli bir şekilde bir bilgisayar tooyour sanal ağına bağlayın. Bu makalede toohello Resource Manager dağıtım modeli uygular ve PowerShell kullanır."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3eddadf6-2e96-48c4-87c6-52a146faeec6
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: b962e4b1946a4ae17d4eb2b920ed54437bc26b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-powershell"></a>Bir noktadan siteye bağlantı tooa VNet yapılandırma sertifika kimlik doğrulaması kullanarak: PowerShell

Bu makalede toocreate hello Resource Manager dağıtım noktası Site bağlantısında sahip bir VNet nasıl model PowerShell kullanarak gösterilmektedir. Bu yapılandırma, sertifikaları tooauthenticate hello istemci bağlanma kullanır. Liste aşağıdaki hello farklı bir seçeneği seçerek farklı dağıtım aracını veya dağıtım modelini kullanarak bu yapılandırma ayrıca oluşturabilirsiniz:

> [!div class="op_single_selector"]
> * [Azure portal](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Azure portal (klasik)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

Bir noktadan siteye (P2S) VPN ağ geçidi tek bir istemci bilgisayardan güvenli bağlantı tooyour sanal ağ oluşturmanıza olanak sağlar. Noktadan siteye VPN bağlantıları tooconnect tooyour VNet uzak bir konumdan, örneğin, evden veya bir Konferanstan telecommuting zaman istediğinizde faydalıdır. Tooconnect tooa VNet gereken yalnızca birkaç istemciniz P2S VPN de yararlı çözüm toouse bir siteden siteye VPN yerine durumdur.

P2S kullanır, Güvenli Yuva Tünel Protokolü (bir SSL tabanlı VPN protokolü, SSTP), hello. P2S VPN bağlantısı, hello istemci bilgisayardan başlatılmasıyla oluşturulur.

![Bilgisayar tooan Azure VNet - noktadan siteye bağlantı diyagramı Bağlan](./media/vpn-gateway-howto-point-to-site-rm-ps/point-to-site-diagram.png)

Noktadan siteye sertifika kimlik doğrulaması bağlantıları hello aşağıdakileri gerektirir:

* RouteBased VPN ağ geçidi.
* Merhaba karşıya yüklenen tooAzure bir kök sertifikası için ortak anahtarı (.cer dosyası). Merhaba sertifika yüklendikten sonra güvenilen bir sertifika olarak kabul edilir ve kimlik doğrulaması için kullanılır.
* Merhaba kök sertifikasından oluşturulur ve toohello VNet bağlanacak her istemci bilgisayarda yüklü bir istemci sertifikası. Bu sertifika, istemci kimlik doğrulaması için kullanılır.
* VPN istemcisi yapılandırma paketi. Merhaba VPN istemcisi yapılandırma paketini hello hello istemci tooconnect toohello VNet için gerekli bilgileri içerir. Merhaba paket yerel toohello Windows işletim sistemi hello mevcut VPN istemcisi yapılandırır. Merhaba yapılandırma paketini kullanarak bağlanan her istemci yapılandırılması gerekir.

Noktadan Siteye bağlantılar için bir VPN cihazına veya şirket içi genel kullanıma yönelik bir IP adresine gerek yoktur. Merhaba VPN bağlantı SSTP (Güvenli Yuva Tünel Protokolü) oluşturulur. Merhaba sunucu tarafında SSTP sürümleri 1.0, 1.1 ve 1.2 destekliyoruz. Merhaba istemci hangi sürümü toouse karar verir. Windows 8.1 ve sonraki sürümlerinde, SSTP'de varsayılan olarak 1.2 kullanılır. 

Merhaba noktadan siteye bağlantılar hakkında daha fazla bilgi için bkz: [noktası siteye SSS](#faq) hello bu makalenin sonunda.

## <a name="before-beginning"></a>Başlamadan önce

* Azure aboneliğiniz olduğunu doğrulayın. Henüz Azure aboneliğiniz yoksa [MSDN abonelik avantajlarınızı](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) etkinleştirebilir veya [ücretsiz bir hesap](https://azure.microsoft.com/pricing/free-trial) için kaydolabilirsiniz.
* Merhaba hello Azure Resource Manager PowerShell cmdlet'lerinin en son sürümünü yükleyin. PowerShell cmdlet'lerini yükleme hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

### <a name="example"></a>Örnek değerler

Merhaba örnek değerleri toocreate bir test ortamı kullanın veya toothese değerleri bkz toobetter anlamak bu makaledeki hello örnekler. Merhaba değişkenler bölümünde ayarlarız [1](#declare) hello makalenin. Merhaba adımları bir kılavuz kullanın ve bunları değiştirmeden hello değerleri kullanın veya tooreflect değiştirmek ortamınızı. 

* **Ad: VNet1**
* **Adres alanı: 192.168.0.0/16** ve **10.254.0.0/16**<br>Bu örnekte, bu yapılandırma ile birden çok adres alanları çalışır birden fazla adres alanı tooillustrate kullanırız. Ancak, bu yapılandırma için birden çok adres alanı gerekli değildir.
* **Alt ağ adı: FrontEnd**
  * **Alt ağ adres aralığı: 192.168.1.0/24**
* **Alt ağ adı: BackEnd**
  * **Alt ağ adres aralığı: 10.254.1.0/24**
* **Alt ağ adı: GatewaySubnet**<br>Merhaba alt ağ adı *GatewaySubnet* hello VPN ağ geçidi toowork için zorunludur.
  * **Ağ Geçidi Alt Ağ adres aralığı: 192.168.200.0/24** 
* **VPN istemcisi adres havuzu: 172.16.201.0/24**<br>Toohello bu noktadan siteye bağlantıyı kullanarak VNet bağlantı VPN istemcileri, VPN istemci adres havuzu hello bir IP adresi alırsınız.
* **Abonelik:** kullandığınızdan emin olun, birden fazla aboneliğiniz varsa doğru olanı hello.
* **Kaynak Grubu: TestRG**
* **Konum: Doğu ABD**
* **DNS sunucusu: IP adresi** hello DNS sunucusunun ad çözümlemesi için toouse istiyor.
* **Ağ Geçidi Adı: Vnet1GW**
* **Ortak IP adı: VNet1GWPIP**
* **VpnType: RouteBased** 

## <a name="declare"></a>1. Oturum açma ve değişkenleri ayarlama

Bu bölümde, oturum açın ve bu yapılandırma için kullanılan hello değerlerini bildirin. Hello olarak bildirilen değerler hello örnek komut dosyalarını kullanılır. Merhaba değerleri tooreflect kendi ortamınızdaki değiştirin. Veya değerleri bildirilen hello kullanın ve hello adımları bir alıştırma olarak gidin.

1. PowerShell Konsolunuzu yükseltilmiş ayrıcalıklarla açın ve tooyour Azure hesabı oturum. Bu cmdlet hello oturum açma kimlik bilgilerini ister. Kullanılabilir tooAzure PowerShell; böylece oturum açtıktan sonra hesap ayarlarınızı indirir.

  ```powershell
  Login-AzureRmAccount
  ```
2. Azure aboneliklerinizin bir listesini alın.

  ```powershell
  Get-AzureRmSubscription
  ```
3. Merhaba abonelik toouse istediğinizi belirtin.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
4. Toouse istediğiniz hello değişkenleri bildirin. Aşağıdaki örnek, hello değerleri gerektiğinde kendi değiştirerek hello kullanın.

  ```powershell
  $VNetName  = "VNet1"
  $FESubName = "FrontEnd"
  $BESubName = "Backend"
  $GWSubName = "GatewaySubnet"
  $VNetPrefix1 = "192.168.0.0/16"
  $VNetPrefix2 = "10.254.0.0/16"
  $FESubPrefix = "192.168.1.0/24"
  $BESubPrefix = "10.254.1.0/24"
  $GWSubPrefix = "192.168.200.0/26"
  $VPNClientAddressPool = "172.16.201.0/24"
  $RG = "TestRG"
  $Location = "East US"
  $DNS = "10.1.1.3"
  $GWName = "VNet1GW"
  $GWIPName = "VNet1GWPIP"
  $GWIPconfName = "gwipconf"
  ```

## <a name="ConfigureVNet"></a>2. Sanal ağ yapılandırma

1. Bir kaynak grubu oluşturun.

  ```powershell
  New-AzureRmResourceGroup -Name $RG -Location $Location
  ```
2. Merhaba adlandırarak hello sanal ağ alt ağı yapılandırmaları oluşturmak *ön uç*, *arka uç*, ve *GatewaySubnet*. Bu önekleri Merhaba, bildirilen VNet adres alanı bir parçası olması gerekir.

  ```powershell
  $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
  $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
  $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
  ```
3. Merhaba sanal ağ oluşturun.

  Bu örnekte, hello DNS sunucusu isteğe bağlıdır. Bir değer belirtildiğinde yeni bir DNS sunucusu oluşturulmaz. Merhaba, belirttiğiniz DNS sunucusu IP adresi, bağlandığınız hello kaynaklar için hello adları çözümlemek için bir DNS sunucusu olmalıdır. Bu örnek için özel bir IP adresi kullandık, ancak bu hello IP adresinin DNS sunucunuzun olmadığını olasıdır. Kendi değerlerinizi toouse emin olun.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer $DNS
  ```
4. Oluşturduğunuz hello sanal ağ için Hello değişkenleri belirtin.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  ```
5. Bir VPN ağ geçidinin genel bir IP adresi olmalıdır. Başlangıç IP adresi kaynağı ilk isteği ve ardından sanal ağ geçidinizi oluştururken tooit bakın. Başlangıç IP adresi toohello kaynak Hello VPN ağ geçidi oluşturulup dinamik olarak atanır. VPN Gateway hizmeti şu anda yalnızca *Dinamik* Genel IP adresi ayırmayı desteklemektedir. Statik bir Genel IP adresi ataması isteğinde bulunamazsınız. Ancak, tooyour VPN ağ geçidi atandıktan sonra hello IP adresini değiştirse anlamına gelmez. ağ geçidi Hello genel IP adresi değişiklikleri hello zaman hello yalnızca zaman silinmiş ve yeniden oluşturulmalıdır. VPN ağ geçidiniz üzerinde gerçekleştirilen yeniden boyutlandırma, sıfırlama veya diğer iç bakım/yükseltme işlemleri sırasında değişmez.

  Dinamik olarak atanan bir genel IP adresi isteyin.

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```

## <a name="creategateway"></a>3. Merhaba VPN ağ geçidi oluşturma

Yapılandırın ve hello sanal ağ geçidi için sanal ağınızı oluşturun.

* Merhaba *- GatewayType* olmalıdır **Vpn** ve hello *- VpnType* olmalıdır **RouteBased**.
* Bir VPN ağ geçidi hello bağlı olarak too45 dakika toocomplete yukarı sürebilir [ağ geçidi SKU'su](vpn-gateway-about-vpn-gateway-settings.md) seçin.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
-Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
-VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 `
```

## <a name="addresspool"></a>4. Merhaba VPN istemci adres havuzu ekleme

Merhaba VPN ağ geçidi oluşturduktan sonra hello VPN istemci adres havuzu ekleyebilirsiniz. Merhaba VPN istemci adres havuzu içinden hello VPN istemcileri bir IP adresi bağlanırken alma hello aralıktır. Çakışmayan bir özel IP adres aralığı, bağlanması hello şirket içi konumla veya hello tooconnect için istediğiniz VNet ile kullanın. Bu örnekte, hello VPN istemci adres havuzu olarak bildirilmiş bir [değişkeni](#declare) 1. adımda.

```powershell
$Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
```

## <a name="Certificates"></a>5. İstemci sertifikaları oluşturma

Sertifikalar için noktadan siteye VPN Azure tooauthenticate VPN istemcileri tarafından kullanılır. Ortak anahtar bilgileri hello kök sertifika tooAzure hello karşıya yükleyin. Merhaba ortak anahtar ardından 'güvenilir' olarak kabul edilir. İstemci sertifikaları gerekir hello güvenilen kök sertifika oluşturulur ve ardından her bir istemci bilgisayarı hello Sertifikalar-Geçerli kullanıcı/kişisel sertifika deposunda yüklü. bağlantı toohello VNet başlattığında hello kullanılan tooauthenticate hello istemci sertifikasıdır. 

Otomatik olarak imzalanan sertifikalar kullanıyorsanız bu sertifikaların belirli parametreler kullanılarak oluşturulması gerekir. Merhaba yönergeleri kullanarak otomatik olarak imzalanan bir sertifika oluşturabilir [PowerShell ve Windows 10](vpn-gateway-certificates-point-to-site.md), veya Windows 10 yoksa, kullanabileceğiniz [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md). Otomatik olarak imzalanan kök sertifikalar ve istemci sertifikalarını oluştururken hello yönergelerindeki hello adımları izleyin önemlidir. Aksi takdirde, oluşturduğunuz hello sertifikaları P2S bağlantılarının ile uyumlu değil ve bağlantı hatası alırsınız.

### <a name="cer"></a>1. Merhaba .cer dosyasını hello kök sertifikası için edinin

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]


### <a name="generate"></a>2. İstemci sertifikası oluşturma

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="upload"></a>6. Merhaba kök sertifika ortak anahtar bilgileri karşıya yükle

VPN ağ geçidini oluşturma işleminin tamamlandığını doğrulayın. Bu tamamlandıktan sonra (Merhaba ortak anahtar bilgileri içeren) hello .cer dosyası için bir güvenilen kök sertifika tooAzure karşıya yükleyebilirsiniz. Azure a.cer dosya yüklendikten sonra hello güvenilen kök sertifika oluşturulan bir istemci sertifikası yüklemiş tooauthenticate istemcileri kullanabilirsiniz. Gerektiğinde ek güvenilen kök sertifika dosyaları - 20 - daha sonra tooa toplam karşıya yükleyebilirsiniz.

1. Merhaba değerini kendi değerlerinizle değiştirerek sertifika adınızı Hello değişken bildirin.

  ```powershell
  $P2SRootCertName = "P2SRootCert.cer"
  ```
2. Merhaba dosya yolu kendinizinkilerle değiştirin ve ardından hello cmdlet'lerini çalıştırın.

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
  ```
3. Merhaba ortak anahtar bilgileri tooAzure karşıya yükleyin. Azure Hello sertifika bilgilerini yüklendikten sonra bir güvenilen kök sertifika bu toobe göz önünde bulundurur.

   ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
  ```

## <a name="clientconfig"></a>7. Merhaba VPN istemcisi yapılandırma paketini indirme

tooconnect tooa noktadan siteye VPN kullanarak VNet, her istemci hello yerel VPN istemcisi ile hello ayarlarını yapılandıran istemci yapılandırma paketi ve gerekli tooconnect toohello sanal ağ olan dosyaları yüklemeniz gerekir. Merhaba VPN istemcisi yapılandırma paketini hello yerel Windows VPN istemcisi yapılandırır, yeni veya farklı bir VPN istemcisi yükleme yapmaz. 

Hello sürüm hello istemci için hello mimarisi eşleştiği sürece, aynı VPN istemcisi yapılandırma paketini her istemci bilgisayarında hello kullanabilirsiniz. Merhaba, desteklenen istemci işletim sistemlerinin Hello listesi için bkz [noktadan siteye bağlantılar hakkında SSS](#faq) hello bu makalenin sonunda.

1. Merhaba ağ geçidi oluşturulduktan sonra oluşturmak ve hello istemcisi yapılandırma paketini indirin. Bu örnek, 64-bit istemciler için hello paketi indirir. Toodownload hello 32 bit istemci istiyorsanız, 'Amd64' 'x86' ile değiştirin. Merhaba VPN istemcisi hello Azure portal kullanarak da yükleyebilirsiniz.

  ```powershell
  Get-AzureRmVpnClientPackage -ResourceGroupName $RG `
  -VirtualNetworkGatewayName $GWName -ProcessorArchitecture Amd64
  ```
2. Alma hello bağlantı çevreleyen tooremove hello teklifleri verdiğiniz tooa web tarayıcı toodownload hello paketi, döndürülen hello bağlantı kopyalayıp yeniden açın. 
3. Paketini indirin ve hello hello istemci bilgisayara yükleyin. Bir SmartScreen açılır penceresi görürseniz **Daha fazla bilgi**’ye ve ardından **Yine de çalıştır**’a tıklayın. Diğer istemci bilgisayarlarda hello paket tooinstall da kaydedebilirsiniz.
4. Merhaba istemci bilgisayarda çok gidin**ağ ayarlarını** tıklatıp **VPN**. Merhaba VPN bağlantısı hello bağlanır hello sanal ağ adını gösterir.

## <a name="clientcertificate"></a>8. Dışarı aktarılan bir istemci sertifikasını yükleme

Toocreate bir P2S bağlantısı istiyorsanız hello dışında bir istemci bilgisayardan bir toogenerate hello istemci sertifikalarını kullandığınız, tooinstall bir istemci sertifikası gerekir. Bir istemci sertifikası yüklerken hello istemci sertifikası dışarı aktarılırken oluşturduğunuz hello parola gerekir. Genellikle, bu hello sertifikayı çift ve bu yükleme yalnızca bir konudur.

Merhaba istemci sertifikası (Merhaba varsayılandır) hello tüm sertifika zinciri ile birlikte bir .pfx olarak aktarılmış olduğundan emin olun. Aksi takdirde hello kök sertifika bilgilerini hello istemci bilgisayarda mevcut değil ve hello istemci mümkün tooauthenticate düzgün olmayacaktır. Daha fazla bilgi için bkz. [Dışarı aktarılan istemci sertifikasını yükleme](vpn-gateway-certificates-point-to-site.md#install). 

## <a name="connect"></a>9. TooAzure Bağlan

1. Merhaba istemci bilgisayarda, tooconnect tooyour Vnet'in tooVPN bağlantıları gidin ve oluşturduğunuz hello VPN bağlantısını bulun. Aynı sanal ağ olarak ad hello adlandırılır. **Bağlan**'a tıklayın. Bir açılır ileti toousing hello sertifika başvuran görünebilir. Tıklatın **devam** toouse yükseltilmiş ayrıcalıklar. 
2. Merhaba üzerinde **bağlantı** durum sayfasında, tıklatın **Bağlan** toostart hello bağlantı. Görürseniz bir **Sertifika Seç** ekranında, hello istemci sertifikası gösteren toouse tooconnect istediğiniz hello biri olduğunu doğrulayın. Değilse, hello aşağı açılan okunu tooselect hello doğru sertifikayı kullanın ve ardından **Tamam**.

  ![VPN istemci tooAzure bağlanır](./media/vpn-gateway-howto-point-to-site-rm-ps/clientconnect.png)
3. Bağlantınız kurulur.

  ![Bağlantı kuruldu](./media/vpn-gateway-howto-point-to-site-rm-ps/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>P2S bağlantılarının sorunlarını giderme

[!INCLUDE [client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <a name="verify"></a>10. Bağlantınızı doğrulama

1. VPN bağlantınızın etkin olduğunu tooverify yükseltilmiş bir komut istemi açın ve çalıştırın *ipconfig/all*.
2. Merhaba sonuçları görüntüleyin. Başlangıç IP adresi aldığınız yapılandırmanızda belirtilen hello noktadan siteye VPN istemci adres havuzu içindeki hello adresleri birini olduğuna dikkat edin. Merhaba, benzer toothis örnek karşılaşılır:

  ```
  PPP adapter VNet1:
      Connection-specific DNS Suffix .:
      Description.....................: VNet1
      Physical Address................:
      DHCP Enabled....................: No
      Autoconfiguration Enabled.......: Yes
      IPv4 Address....................: 172.16.201.3(Preferred)
      Subnet Mask.....................: 255.255.255.255
      Default Gateway.................:
      NetBIOS over Tcpip..............: Enabled
  ```

## <a name="connectVM"></a>Tooa sanal makineye bağlanma

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <a name="addremovecert"></a>Kök sertifika ekleme veya kaldırma

Azure’da güvenilen kök sertifikayı ekleyebilir veya kaldırabilirsiniz. Bir kök sertifikası kaldırdığınızda, oluşturulan hello kök sertifikasından bir sertifika olan istemcileri kimlik doğrulaması yapamaz ve tooconnect mümkün olmayacaktır. İstemci tooauthenticate ve bağlanmak istiyorsanız, yeni bir istemci sertifikası güvenilen (karşıya yüklenen) tooAzure olan bir kök sertifika oluşturulan tooinstall gerekir.

### <a name="addtrustedroot"></a>tooadd güvenilen bir kök sertifikası

Too20 kök sertifika .cer dosyaları tooAzure ekleyebilirsiniz. bir kök sertifika Ekle Yardım Hello aşağıdaki adımları:

#### <a name="certmethod1"></a>1. Yöntem

Merhaba en verimli yöntemi tooupload bir kök sertifikası budur.

1. Merhaba .cer dosyasını tooupload hazırlayın:

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert3.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64_3 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64_3
  ```
2. Merhaba dosyasını karşıya yükleyin. Aynı anda yalnızca bir dosya yükleyebilirsiniz.

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64_3
  ```

3. Sertifika dosyası karşıya hello tooverify:

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

#### <a name="certmethod2"></a>2. Yöntem

Bu yöntem yöntemi 1'den daha fazla adım vardır, ancak var olan hello aynı sonucu. Tooview hello sertifika verilere ihtiyaç durumunda dahil edilir.

1. Oluşturma ve hello yeni kök sertifika tooadd tooAzure hazırlayın. Base-64 olarak kodlanmış X.509 gibi hello ortak anahtarı dışarı aktar (. CER) ve bir metin düzenleyicisiyle açın. Hello aşağıdaki örnekte gösterildiği gibi Hello değerleri kopyalayın:

  ![sertifika](./media/vpn-gateway-howto-point-to-site-rm-ps/copycert.png)

  > [!NOTE]
  > Merhaba sertifika veri kopyalama işlemi sırasında satır başı veya satır beslemelerini olmadan sürekli bir satır olarak hello metin kopyaladığınızdan emin olun. Merhaba metin düzenleyicisi too'Show simgesi/tüm karakterleri toosee hello satır döndürür ve satır besleme karakterlerini göster görünümünüzde toomodify gerekebilir.
  >
  >

2. Merhaba sertifika adı ve anahtar bilgileri bir değişken olarak belirtin. Merhaba bilgileri kendi hello gösterildiği gibi aşağıdaki örnekle değiştirin:

  ```powershell
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
3. Merhaba yeni kök sertifikasını ekleyin. Tek seferde yalnızca bir sertifika ekleyebilirsiniz.

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
4. Bu hello yeni sertifika doğru şekilde aşağıdaki örneğine hello kullanılarak eklenen doğrulayabilirsiniz:

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

### <a name="removerootcert"></a>tooremove bir kök sertifikası

1. Merhaba değişkenleri bildirin.

  ```powershell
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
2. Merhaba sertifika kaldırın.

  ```powershell
  Remove-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
3. Sertifika hello örnek tooverify aşağıdaki kullanım hello başarıyla kaldırıldı.

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

## <a name="revoke"></a>İstemci sertifikasını iptal etme

İstemci sertifikalarını iptal edebilirsiniz. Merhaba sertifika iptal listesi tooselectively sağlayan tek bir istemci sertifikalarını temel alarak noktadan siteye bağlantı reddedin. Bu, güvenilen kök sertifika kaldırma işleminden farklıdır. Azure'dan bir güvenilen kök sertifika .cer kaldırırsanız, tüm istemci sertifikaları için oluşturulan ve imzalanmış hello iptal edilen kök sertifikası tarafından hello erişimi iptal eder. Bir istemci sertifikası iptal etmek hello kök sertifika yerine hello kök sertifika toocontinue toobe kimlik doğrulaması için kullanılan gelen oluşturulan diğer sertifikaları hello sağlar.

Merhaba yaygın toouse hello kök sertifika toomanage erişim düzeyleri, ekip veya kuruluş bireysel kullanıcılar üzerinde ayrıntılı erişim denetimi için İptal edilen istemci sertifikalarını kullanırken bir uygulamadır.

### <a name="revokeclientcert"></a>toorevoke bir istemci sertifikası

1. Merhaba istemci sertifikası parmak izi alma. Daha fazla bilgi için bkz: [nasıl tooretrieve hello bir sertifikanın parmak izini](https://msdn.microsoft.com/library/ms734695.aspx).
2. Merhaba bilgileri tooa metin düzenleyicisi kopyalayın ve sürekli bir dize olmasını tüm boşlukları Kaldır. Bu dize bir değişken olarak hello sonraki adımda bildirildi.
3. Merhaba değişkenleri bildirin. Alınan emin toodeclare hello parmak izi hello önceki adımda olun.

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
4. Merhaba parmak izi toohello iptal edilen sertifikaların listesini ekleyin. Merhaba parmak izi eklendiğinde "Başarılı" konusuna bakın.

  ```powershell
  Add-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG `
  -Thumbprint $RevokedThumbprint1
  ```
5. Bu hello parmak izi toohello sertifika iptal listesi eklenen doğrulayın.

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```
6. Merhaba parmak izi eklendikten sonra hello sertifika artık kullanılan tooconnect olabilir. Bu sertifikayı kullanarak tooconnect deneyin istemcileri bu hello sertifika artık geçerli olduğunu bildiren bir ileti alırsınız.

### <a name="reinstateclientcert"></a>tooreinstate bir istemci sertifikası

Bir istemci sertifikası, iptal edilen istemci sertifikalarını hello listeden hello parmak izi kaldırarak yeniden başlatabilirsiniz.

1. Merhaba değişkenleri bildirin. Merhaba doğru parmak izi tooreinstate istediğiniz hello sertifika bildirme emin olun.

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
2. Merhaba sertifika parmak izi hello sertifikayı iptal listesinden kaldırın.

  ```powershell
  Remove-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -Thumbprint $RevokedThumbprint1
  ```
3. Merhaba parmak izi hello iptal listesinden kaldırılır, denetleyin.

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```

## <a name="faq"></a>Noktadan Siteye hakkında SSS

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>Sonraki adımlar
Bağlantınız tamamlandıktan sonra sanal makineleri tooyour sanal ağları ekleyebilirsiniz. Daha fazla bilgi için bkz. [Sanal Makineler](https://docs.microsoft.com/azure/#pivot=services&panel=Compute). Ağ ve sanal makineler hakkında daha fazla toounderstand bkz [Azure ve Linux VM ağına genel bakış](../virtual-machines/linux/azure-vm-network-overview.md).
