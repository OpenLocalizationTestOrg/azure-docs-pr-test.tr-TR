---
title: "Noktadan siteye ve sertifika kimlik doğrulaması kullanan bir bilgisayar tooa sanal bir ağa bağlanma: Azure Portal | Microsoft Docs"
description: "Sertifika kimlik doğrulaması kullanarak bir noktadan siteye VPN ağ geçidi bağlantısı oluşturarak bilgisayar tooyour Azure sanal ağı güvenli bir şekilde bağlanın. Bu makalede toohello Resource Manager dağıtım modeli uygular ve hello Azure portalını kullanır."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a15ad327-e236-461f-a18e-6dbedbf74943
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: 1419d6b4c160140b62d656b25bd02f6af7fd6655
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-azure-portal"></a>Bir noktadan siteye bağlantı tooa VNet yapılandırma sertifika kimlik doğrulaması kullanarak: Azure portal

Bu makalede nasıl toocreate hello Resource Manager dağıtım modeli kullanarak bir noktadan siteye bağlantı sahip bir VNet hello Azure portal gösterilmektedir. Bu yapılandırma, sertifikaları tooauthenticate hello istemci bağlanma kullanır. Liste aşağıdaki hello farklı bir seçeneği seçerek farklı dağıtım aracını veya dağıtım modelini kullanarak bu yapılandırma ayrıca oluşturabilirsiniz:

> [!div class="op_single_selector"]
> * [Azure portal](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Azure portal (klasik)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

Bir noktadan siteye (P2S) VPN ağ geçidi tek bir istemci bilgisayardan güvenli bağlantı tooyour sanal ağ oluşturmanıza olanak sağlar. Noktadan siteye VPN bağlantıları tooconnect tooyour VNet uzak bir konumdan, örneğin, evden veya bir Konferanstan telecommuting zaman istediğinizde faydalıdır. Tooconnect tooa VNet gereken yalnızca birkaç istemciniz P2S VPN de yararlı çözüm toouse bir siteden siteye VPN yerine durumdur. 

P2S kullanır, Güvenli Yuva Tünel Protokolü (bir SSL tabanlı VPN protokolü, SSTP), hello. P2S VPN bağlantısı, hello istemci bilgisayardan başlatılmasıyla oluşturulur.

![Noktadan Siteye diyagramı](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/point-to-site-connection-diagram.png)

Noktadan siteye sertifika kimlik doğrulaması bağlantıları hello aşağıdakileri gerektirir:

* RouteBased VPN ağ geçidi.
* Merhaba karşıya yüklenen tooAzure bir kök sertifikası için ortak anahtarı (.cer dosyası). Merhaba sertifika yüklendikten sonra güvenilen bir sertifika olarak kabul edilir ve kimlik doğrulaması için kullanılır.
* Merhaba kök sertifikasından oluşturulur ve toohello VNet bağlanacak her istemci bilgisayarda yüklü bir istemci sertifikası. Bu sertifika, istemci kimlik doğrulaması için kullanılır.
* VPN istemcisi yapılandırma paketi. Merhaba VPN istemcisi yapılandırma paketini hello hello istemci tooconnect toohello VNet için gerekli bilgileri içerir. Merhaba paket yerel toohello Windows işletim sistemi hello mevcut VPN istemcisi yapılandırır. Merhaba yapılandırma paketini kullanarak bağlanan her istemci yapılandırılması gerekir.

Noktadan Siteye bağlantılar için bir VPN cihazına veya şirket içi genel kullanıma yönelik bir IP adresine gerek yoktur. Merhaba VPN bağlantı SSTP (Güvenli Yuva Tünel Protokolü) oluşturulur. Merhaba sunucu tarafında SSTP sürümleri 1.0, 1.1 ve 1.2 destekliyoruz. Merhaba istemci hangi sürümü toouse karar verir. Windows 8.1 ve sonraki sürümlerinde, SSTP'de varsayılan olarak 1.2 kullanılır.

Merhaba noktadan siteye bağlantılar hakkında daha fazla bilgi için bkz: [noktası siteye SSS](#faq) hello bu makalenin sonunda.

#### <a name="example"></a>Örnek değerler

Aşağıdaki değerleri toocreate bir test ortamı hello kullanın veya toothese değerleri bkz toobetter anlamak bu makaledeki hello örnekler:

* **VNet Adı:** VNet1
* **Adres alanı:** 192.168.0.0/16<br>Bu örnekte yalnızca bir adres alanı kullanılmaktadır. Sanal ağınıza ait birden fazla adres alanı olabilir.
* **Alt ağ adı:** FrontEnd
* **Alt ağ adres aralığı:** 192.168.1.0/24
* **Abonelik:** kullandığınızdan emin olun, birden fazla aboneliğiniz varsa doğru olanı hello.
* **Kaynak Grubu:** TestRG
* **Konum:** Doğu ABD
* **GatewaySubnet:** 192.168.200.0/24<br>
* **DNS sunucusu:** (isteğe bağlı) ad çözümlemesi için toouse istediğiniz hello DNS sunucusunun IP adresi.
* **Sanal ağ geçidi adı:** VNet1GW
* **Ağ geçidi türü:** VPN
* **VPN türü:** Rota tabanlı
* **Genel IP adresi adı:** VNet1GWpip
* **Bağlantı türü:** Noktadan siteye
* **İstemci adres havuzu:** 172.16.201.0/24<br>Toohello bu noktadan siteye bağlantıyı kullanarak VNet bağlantı VPN istemcileri hello istemci adres havuzundan bir IP adresi alır.

## <a name="createvnet"></a>1. Sanal ağ oluşturma

Başlamadan önce, bir Azure aboneliğiniz olduğunu doğrulayın. Henüz Azure aboneliğiniz yoksa [MSDN abonelik avantajlarınızı](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) etkinleştirebilir veya [ücretsiz bir hesap](https://azure.microsoft.com/pricing/free-trial) için kaydolabilirsiniz.

[!INCLUDE [Basic Point-to-Site VNet](../../includes/vpn-gateway-basic-p2s-vnet-rm-portal-include.md)]

## <a name="gatewaysubnet"></a>2. Ağ geçidi alt ağı ekleme

Sanal ağ tooa geçidiniz bağlanmadan önce öncelikle toocreate hello ağ geçidi alt ağı gerekir hello sanal ağ toowhich için tooconnect istiyor. Merhaba ağ geçidi Hizmetleri hello ağ geçidi alt ağda belirtilen hello IP adreslerini kullanır. Mümkünse, / 28 veya /27 CIDR bloğu kullanarak bir ağ geçidi alt ağı oluşturmak tooprovide tooaccommodate gelecekteki ek yapılandırma gereksinimlerini yeterli IP adresi.

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-p2s-rm-portal-include.md)]

## <a name="dns"></a>3. DNS sunucusu belirtme (isteğe bağlı)

Sanal ağınızı oluşturduktan sonra başlangıç IP adresi, bir DNS sunucusu toohandle ad çözümlemesinin ekleyebilirsiniz. Hello DNS sunucusu, bu yapılandırma için isteğe bağlıdır, ancak ad çözümlemesi istiyorsanız gereklidir. Bir değer belirtildiğinde yeni bir DNS sunucusu oluşturulmaz. Merhaba, belirttiğiniz DNS sunucusu IP adresi, bağlandığınız hello kaynaklar için hello adları çözümlemek için bir DNS sunucusu olmalıdır. Bu örnek için özel bir IP adresi kullandık, ancak bu hello IP adresinin DNS sunucunuzun olmadığını olasıdır. Kendi değerlerinizi toouse emin olun.

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="creategw"></a>4. Sanal ağ geçidi oluşturma

[!INCLUDE [create-gateway](../../includes/vpn-gateway-add-gw-p2s-rm-portal-include.md)]

## <a name="generatecert"></a>5. İstemci sertifikaları oluşturma

Sertifikalar tooa VNet bir noktadan siteye VPN bağlantısı üzerinden bağlanan Azure tooauthenticate istemciler tarafından kullanılır. Bir kök sertifikası edindikten sonra [karşıya](#uploadfile) ortak anahtar bilgileri tooAzure hello. Merhaba kök sertifikası sonra 'güvenilir' Azure tarafından bağlantısı için P2S toohello sanal ağ üzerinden kabul edilir. Ayrıca hello güvenilen kök sertifika istemci sertifikalarını oluşturmak ve bunları her istemci bilgisayara yükleyin. bağlantı toohello VNet başlattığında hello istemci sertifikası kullanılan tooauthenticate hello istemcidir. 

### <a name="getcer"></a>1. Merhaba .cer dosyasını hello kök sertifikası için edinin

[!INCLUDE [root-certificate](../../includes/vpn-gateway-p2s-rootcert-include.md)]

### <a name="generateclientcert"></a>2. İstemci sertifikası oluşturma

[!INCLUDE [generate-client-cert](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="addresspool"></a>6. Merhaba istemci adres havuzu ekleme

Merhaba istemci adres havuzu, belirttiğiniz özel IP adresleri aralığıdır. bir noktadan siteye VPN üzerinden bağlanan hello istemcileri bu aralığından bir IP adresi alır. Çakışmayan bir özel IP adres aralığı, bağlanması hello şirket içi konumu veya hello tooconnect için istediğiniz sanal ağ kullanın.

1. Merhaba sanal ağ geçidi oluşturulduktan sonra toohello gidin **ayarları** hello sanal ağ geçidi sayfasının bölümünde. Merhaba, **ayarları** 'yi tıklatın **noktadan siteye Yapılandırması** tooopen hello **noktası için-Site-yapılandırma** sayfası.

  ![Noktadan Siteye sayfası](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/gatewayblade.png)
2. Merhaba üzerinde **noktası için-Site-yapılandırma** sayfasında hello otomatik doldurulmuş aralığı silmek, ardından toouse istediğiniz hello özel IP adresi aralığını ekleyin. Tıklatın **kaydetmek** toovalidate ve hello ayarı kaydedin.

  ![İstemci adres havuzu](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/ipaddresspool.png)

## <a name="uploadfile"></a>7. Merhaba kök sertifika ortak sertifika veri yükleme

Merhaba ağ geçidi oluşturulduktan sonra hello hello kök sertifika tooAzure için ortak anahtar bilgileri karşıya yükleyin. Merhaba ortak sertifika verileri yüklendikten sonra Azure hello güvenilen kök sertifika oluşturulan bir istemci sertifikası yüklemiş tooauthenticate istemcileri kullanabilirsiniz. 20 ek güvenilen kök sertifikalar yukarı tooa toplam karşıya yükleyebilirsiniz.

1. Sertifikaları üzerinde hello eklenen **noktadan siteye Yapılandırması** hello sayfasında **kök sertifika** bölümü.  
2. Base-64 kodlanmış X.509 (.cer) dosyası olarak hello kök sertifikasını dışarı emin olun. Merhaba sertifika metin düzenleyicisiyle açın için tooexport hello sertifika bu biçiminde olması gerekir.
3. Merhaba sertifika Not Defteri gibi bir metin düzenleyicisiyle açın. Merhaba sertifika veri kopyalama işlemi sırasında satır başı veya satır beslemelerini olmadan sürekli bir satır olarak hello metin kopyaladığınızdan emin olun. Merhaba metin düzenleyicisi too'Show simgesi/tüm karakterleri toosee hello satır döndürür ve satır besleme karakterlerini göster görünümünüzde toomodify gerekebilir. Bölüm sürekli tek bir çizgi olarak aşağıdaki yalnızca hello kopyalayın:

  ![Sertifika verileri](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/copycert.png)
4. Merhaba sertifika verileri hello yapıştırma **ortak sertifika verileri** alan. **Ad** hello sertifika ve ardından **kaydetmek**. Too20 güvenilen kök sertifikaları ekleyebilirsiniz.

  ![Sertifika yükleme](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/rootcertupload.png)

## <a name="clientconfig"></a>8. Oluştur ve hello VPN istemcisi yapılandırma paketini yükleyin

tooconnect tooa noktadan siteye VPN kullanarak VNet, her istemci hello yerel VPN istemcisi ile hello ayarlarını yapılandıran istemci yapılandırma paketi ve gerekli tooconnect toohello sanal ağ olan dosyaları yüklemeniz gerekir. Merhaba VPN istemcisi yapılandırma paketini hello yerel Windows VPN istemcisi yapılandırır, yeni veya farklı bir VPN istemcisi yükleme yapmaz.

Hello sürüm hello istemci için hello mimarisi eşleştiği sürece, aynı VPN istemcisi yapılandırma paketini her istemci bilgisayarında hello kullanabilirsiniz. Merhaba, desteklenen istemci işletim sistemlerinin Hello listesi için bkz [noktadan siteye bağlantılar hakkında SSS](#faq) hello bu makalenin sonunda.

### <a name="step-1---generate-and-download-hello-client-configuration-package"></a>1. adım - oluşturmak ve hello istemcisi yapılandırma paketini indirme

1. Merhaba üzerinde **noktadan siteye Yapılandırması** sayfasında, **karşıdan VPN istemcisi** tooopen hello **karşıdan VPN istemcisi** sayfası. Bir veya iki hello paket toogenerate için dakika sürer.

  ![VPN istemcisi indirme 1](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/downloadvpnclient1.png)
2. İstemci için Hello doğru paketi seçin ve ardından **karşıdan**. Merhaba yapılandırma paketi dosyasını kaydedin. Merhaba VPN istemcisi yapılandırma paketini toohello sanal ağ bağlanan her istemci bilgisayara yükleyin.

  ![VPN istemcisi indirme 2](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/vpnclient.png)

### <a name="step-2---install-hello-client-configuration-package"></a>2. adım - yükleme hello istemci yapılandırma paketi

1. Kopya hello yapılandırma dosyasını yerel olarak tooconnect tooyour sanal ağ istediğiniz toohello bilgisayar. 
2. Merhaba .exe dosyası tooinstall hello paketi hello istemci bilgisayarda çift tıklatın. Merhaba yapılandırma paketi oluşturduğundan, imzalı değil ve bir uyarı görebilirsiniz. Windows SmartScreen popup alırsanız tıklatın **daha fazla bilgi** (soldaki hello), ardından **yine de çalıştırmaya** tooinstall hello paket.
3. Merhaba paket hello istemci bilgisayara yükleyin. Windows SmartScreen popup alırsanız tıklatın **daha fazla bilgi** (soldaki hello), ardından **yine de çalıştırmaya** tooinstall hello paket.
4. Merhaba istemci bilgisayarda çok gidin**ağ ayarlarını** tıklatıp **VPN**. Merhaba VPN bağlantısı hello bağlanır hello sanal ağ adını gösterir.

## <a name="installclientcert"></a>9. Dışarı aktarılan bir istemci sertifikasını yükleme

Toocreate bir P2S bağlantısı istiyorsanız hello dışında bir istemci bilgisayardan bir toogenerate hello istemci sertifikalarını kullandığınız, tooinstall bir istemci sertifikası gerekir. Bir istemci sertifikası yüklerken hello istemci sertifikası dışarı aktarılırken oluşturduğunuz hello parola gerekir. Genellikle, bu hello sertifikayı çift ve bu yükleme yalnızca bir konudur.

Merhaba istemci sertifikası (Merhaba varsayılandır) hello tüm sertifika zinciri ile birlikte bir .pfx olarak aktarılmış olduğundan emin olun. Aksi takdirde hello kök sertifika bilgilerini hello istemci bilgisayarda mevcut değil ve hello istemci mümkün tooauthenticate düzgün olmayacaktır. Daha fazla bilgi için bkz. [Dışarı aktarılan istemci sertifikasını yükleme](vpn-gateway-certificates-point-to-site.md#install).

## <a name="connect"></a>10. TooAzure Bağlan

1. Merhaba istemci bilgisayarda, tooconnect tooyour Vnet'in tooVPN bağlantıları gidin ve oluşturduğunuz hello VPN bağlantısını bulun. Aynı sanal ağ olarak ad hello adlandırılır. **Bağlan**'a tıklayın. Bir açılır ileti toousing hello sertifika başvuran görünebilir. Tıklatın **devam** toouse yükseltilmiş ayrıcalıklar.

2. Merhaba üzerinde **bağlantı** durum sayfasında, tıklatın **Bağlan** toostart hello bağlantı. Görürseniz bir **Sertifika Seç** ekranında, hello istemci sertifikası gösteren toouse tooconnect istediğiniz hello biri olduğunu doğrulayın. Değilse, hello aşağı açılan okunu tooselect hello doğru sertifikayı kullanın ve ardından **Tamam**.

  ![VPN istemci tooAzure bağlanır](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/clientconnect.png)
3. Bağlantınız kurulur.

  ![Bağlantı kuruldu](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>P2S bağlantılarının sorunlarını giderme

[!INCLUDE [verifies client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <a name="verify"></a>11. Bağlantınızı doğrulama

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

## <a name="add"></a>Güvenilen kök sertifika ekleme veya kaldırma

Azure’da güvenilen kök sertifikayı ekleyebilir veya kaldırabilirsiniz. Bir kök sertifikası kaldırdığınızda, o kökünden oluşturulan bir sertifika sahip istemciler mümkün tooauthenticate olmayacaktır ve böylece mümkün tooconnect olmaz. İstemci tooauthenticate ve bağlanmak istiyorsanız, yeni bir istemci sertifikası güvenilen (karşıya yüklenen) tooAzure olan bir kök sertifika oluşturulan tooinstall gerekir.

### <a name="tooadd-a-trusted-root-certificate"></a>tooadd güvenilen bir kök sertifikası

Too20 güvenilen kök sertifika .cer dosyaları tooAzure ekleyebilirsiniz. Yönergeler için hello bölümüne bakın [bir güvenilen kök sertifika karşıya](#uploadfile) bu makalede.

### <a name="tooremove-a-trusted-root-certificate"></a>tooremove güvenilen bir kök sertifikası

1. tooremove bir güvenilen kök sertifika gidin toohello **noktadan siteye Yapılandırması** sanal ağ geçidiniz için sayfa.
2. Merhaba, **kök sertifika** bölüm hello sayfasının tooremove istediğiniz hello sertifikayı bulun.
3. Merhaba üç nokta sonraki toohello sertifikası'nı tıklatın ve ardından 'Kaldır' ı tıklatın.

## <a name="revokeclient"></a>İstemci sertifikasını iptal etme

İstemci sertifikalarını iptal edebilirsiniz. Merhaba sertifika iptal listesi tooselectively sağlayan tek bir istemci sertifikalarını temel alarak noktadan siteye bağlantı reddedin. Bu, güvenilen kök sertifika kaldırma işleminden farklıdır. Azure'dan bir güvenilen kök sertifika .cer kaldırırsanız, tüm istemci sertifikaları için oluşturulan ve imzalanmış hello iptal edilen kök sertifikası tarafından hello erişimi iptal eder. Bir istemci sertifikası iptal etmek hello kök sertifika yerine hello kök sertifika toocontinue toobe kimlik doğrulaması için kullanılan gelen oluşturulan diğer sertifikaları hello sağlar.

Merhaba yaygın toouse hello kök sertifika toomanage erişim düzeyleri, ekip veya kuruluş bireysel kullanıcılar üzerinde ayrıntılı erişim denetimi için İptal edilen istemci sertifikalarını kullanırken bir uygulamadır.

### <a name="toorevoke-a-client-certificate"></a>toorevoke bir istemci sertifikası

Merhaba parmak izi toohello iptal listesine ekleyerek bir istemci sertifikası iptal edebilirsiniz.

1. Merhaba istemci sertifikası parmak izi alma. Daha fazla bilgi için bkz: [nasıl tooretrieve hello bir sertifikanın parmak izini](https://msdn.microsoft.com/library/ms734695.aspx).
2. Merhaba bilgileri tooa metin düzenleyicisi kopyalayın ve sürekli bir dize olmasını tüm boşlukları Kaldır.
3. Toohello sanal ağ geçidi gidin **noktası için-site-yapılandırma** sayfası. Merhaba budur çok kullanılan aynı sayfa[bir güvenilen kök sertifika karşıya](#uploadfile).
4. Merhaba, **sertifikalar iptal** bölümünde, (Bu yoksa toobe hello sertifika genel adı) hello sertifika için kolay bir ad girin.
5. Kopyalama ve yapıştırma hello parmak izi dize toohello **parmak izi** alan.
6. Merhaba parmak izi doğrular ve toohello iptal listesine otomatik olarak eklenir. Bu hello Merhaba ekranında bir ileti görüntülenir listesi güncelleştiriyor. 
7. Güncelleştirme tamamlandıktan sonra hello sertifika artık kullanılan tooconnect olabilir. Bu sertifikayı kullanarak tooconnect deneyin istemcileri bu hello sertifika artık geçerli olduğunu bildiren bir ileti alırsınız.

## <a name="faq"></a>Noktadan Siteye hakkında SSS

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>Sonraki adımlar
Bağlantınız tamamlandıktan sonra sanal makineleri tooyour sanal ağları ekleyebilirsiniz. Daha fazla bilgi için bkz. [Sanal Makineler](https://docs.microsoft.com/azure/#pivot=services&panel=Compute). Ağ ve sanal makineler hakkında daha fazla toounderstand bkz [Azure ve Linux VM ağına genel bakış](../virtual-machines/linux/azure-vm-network-overview.md).
