---
title: "Noktadan siteye ve sertifika kimlik doğrulaması kullanan bir bilgisayar tooa sanal bir ağa bağlanma: Azure Portal Klasik | Microsoft Docs"
description: "Güvenli tooyour bağlanmak Klasik Azure sanal hello Azure portal kullanarak bir noktadan siteye VPN ağ geçidi bağlantısı oluşturarak ağ."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 65e14579-86cf-4d29-a6ac-547ccbd743bd
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 9b53ba43ee4dfb61defeec458905fb1f1b18c3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-classic-azure-portal"></a>Bir noktadan siteye bağlantı tooa VNet yapılandırma sertifika kimlik doğrulaması (Klasik) kullanarak: Azure portal

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

Bu makalede nasıl toocreate hello Klasik dağıtım modeli kullanarak bir noktadan siteye bağlantı sahip bir VNet hello Azure portal gösterilmektedir. Bu yapılandırma, sertifikaları tooauthenticate hello istemci bağlanma kullanır. Liste aşağıdaki hello farklı bir seçeneği seçerek farklı dağıtım aracını veya dağıtım modelini kullanarak bu yapılandırma ayrıca oluşturabilirsiniz:

> [!div class="op_single_selector"]
> * [Azure portal](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Azure portal (klasik)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>

Bir noktadan siteye (P2S) VPN ağ geçidi tek bir istemci bilgisayardan güvenli bağlantı tooyour sanal ağ oluşturmanıza olanak sağlar. Noktadan siteye VPN bağlantıları tooconnect tooyour VNet uzak bir konumdan, örneğin, evden veya bir Konferanstan telecommuting zaman istediğinizde faydalıdır. Tooconnect tooa VNet gereken yalnızca birkaç istemciniz P2S VPN de yararlı çözüm toouse bir siteden siteye VPN yerine durumdur. 

P2S kullanır, Güvenli Yuva Tünel Protokolü (bir SSL tabanlı VPN protokolü, SSTP), hello. P2S VPN bağlantısı, hello istemci bilgisayardan başlatılmasıyla oluşturulur.


![Noktadan Siteye diyagramı](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/point-to-site-connection-diagram.png)


Noktadan siteye sertifika kimlik doğrulaması bağlantıları hello aşağıdakileri gerektirir:

* Bir Dinamik VPN ağ geçidi.
* Merhaba karşıya yüklenen tooAzure bir kök sertifikası için ortak anahtarı (.cer dosyası). Bu dosya, güvenilen bir sertifika olarak kabul edilir ve kimlik doğrulaması için kullanılır.
* Bir istemci sertifikası hello kök sertifikasından oluşturulur ve bağlanacak her istemci bilgisayarda yüklü. Bu sertifika, istemci kimlik doğrulaması için kullanılır.
* Bir VPN istemcisi yapılandırma paketi oluşturulmalı ve bağlanan her istemci bilgisayara yüklenmelidir. Merhaba istemci yapılandırma paketi zaten hello gerekli bilgileri tooconnect toohello VNet ile Merhaba işletim sisteminde hello yerel VPN istemcisi yapılandırır.

Noktadan Siteye bağlantılar için bir VPN cihazına veya şirket içi genel kullanıma yönelik bir IP adresine gerek yoktur. Merhaba VPN bağlantı SSTP (Güvenli Yuva Tünel Protokolü) oluşturulur. Merhaba sunucu tarafında SSTP sürümleri 1.0, 1.1 ve 1.2 destekliyoruz. Merhaba istemci hangi sürümü toouse karar verir. Windows 8.1 ve sonraki sürümlerinde, SSTP'de varsayılan olarak 1.2 kullanılır. 

Merhaba noktadan siteye bağlantılar hakkında daha fazla bilgi için bkz: [noktası siteye SSS](#faq) hello bu makalenin sonunda.

### <a name="example-settings"></a>Örnek ayarlar

Aşağıdaki değerleri toocreate bir test ortamı hello kullanın veya toothese değerleri bkz toobetter anlamak bu makaledeki hello örnekler:

* **Ad: VNet1**
* **Adres alanı: 192.168.0.0/16**<br>Bu örnekte yalnızca bir adres alanı kullanılmaktadır. Sanal ağınıza ait birden fazla adres alanı olabilir.
* **Alt ağ adı: FrontEnd**
* **Alt ağ adres aralığı: 192.168.1.0/24**
* **Abonelik:** kullandığınızdan emin olun, birden fazla aboneliğiniz varsa doğru olanı hello.
* **Kaynak Grubu: TestRG**
* **Konum: Doğu ABD**
* **Bağlantı türü: Noktadan siteye**
* **İstemci Adres Alanı: 172.16.201.0/24**. Bu noktadan siteye bağlantıyı kullanarak sanal bir IP adresi almak toohello bağlanmak VPN istemcileri belirtilen havuzu hello.
* **GatewaySubnet: 192.168.200.0/24**. Merhaba ağ geçidi alt ağı, 'GatewaySubnet' hello adı kullanmanız gerekir.
* **Boyut:** Select hello ağ geçidi SKU'su toouse istiyor.
* **Yönlendirme Türü: Dinamik**

## <a name="vnetvpn"></a>1. Sanal ağ ve VPN ağ geçidi oluşturma

Başlamadan önce, bir Azure aboneliğiniz olduğunu doğrulayın. Henüz Azure aboneliğiniz yoksa [MSDN abonelik avantajlarınızı](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) etkinleştirebilir veya [ücretsiz bir hesap](https://azure.microsoft.com/pricing/free-trial) için kaydolabilirsiniz.

### <a name="createvnet"></a>1. Kısım - Sanal ağ oluşturma

Sanal ağınız yoksa bir sanal ağ oluşturun. Ekran görüntüleri örnek olarak verilmiştir. Emin tooreplace hello değerleri kendi değerlerinizle olabilir. toocreate kullanarak bir VNet Azure portalı, aşağıdaki adımları kullanın hello hello:

1. Tarayıcıdan toohello gidin [Azure portal](http://portal.azure.com) ve gerekiyorsa Azure hesabınızla oturum açın.
2. **Yeni**’ye tıklayın. Merhaba, **arama hello Market** alanında, 'Sanal ağ' yazın. Bulun **sanal ağ** döndürülen hello listelemek ve tooopen hello'ı tıklatın **sanal ağ** sayfası.

  ![Sanal ağ ara sayfası](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/newvnetportal700.png)
3. Merhaba alt kısmındaki hello de hello sanal ağ sayfasından **dağıtım modeli seçin** listesinde, seçin **Klasik**ve ardından **oluşturma**.

  ![Dağıtım modeli seçme](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/selectmodel.png)
4. Merhaba üzerinde **sanal ağ oluştur** sayfasında, hello VNet ayarlarını yapılandırın. Bu sayfada, ilk adres alanınızı ve tek alt ağ adres aralığınızı eklersiniz. Merhaba VNet oluşturma işlemini tamamladıktan sonra geri dönün ve ek alt ağları ve adres alanlarını ekleyin.

  ![Sanal ağ oluştur sayfası](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/vnet125.png)
5. Bu hello doğrulayın **abonelik** hello doğru olduğundan. Merhaba açılan kullanarak abonelikleri değiştirebilirsiniz.
6. **Kaynak grubu**’na tıklayın, ya varolan bir kaynak grubunu seçin ya da yeni kaynak grubunuz için bir ad yazarak yeni bir tane oluşturun. Yeni bir kaynak grubu oluşturuyorsanız, tooyour göre adı hello kaynak grubu yapılandırma değerlerini planlanan. Kaynak grupları hakkında daha fazla bilgi için [Azure Resource Manager’a Genel Bakış](../azure-resource-manager/resource-group-overview.md#resource-groups)’ı ziyaret edin.
7. Ardından, hello'ı seçin **konumu** ayarlarını. Merhaba kaynakları toothis VNet dağıtmadan bulunacağı Hello konumunu belirler.
8. Seçin **PIN toodashboard** toobe mümkün toofind ağınızı hello Panoda kolayca isterseniz ve ardından **oluşturma**.

  ![PIN toodashboard](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/pintodashboard150.png)
9. Create tıklandıktan sonra bir kutucuk Panonuzda hello Vnet'inizin ilerleme durumunu yansıtır görüntülenir. VNet Hello döşeme değişiklikleri hello olarak oluşturuldu.

  ![Sanal ağ kutucuğu oluşturma](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deploying150.png)
10. Sanal ağınız oluşturulduktan sonra gördüğünüz **oluşturulan** altında listelenen **durum** hello Klasik Azure Portalı'ndaki hello ağlar sayfasında.
11. DNS sunucusu ekleme (isteğe bağlı). Sanal ağınızı oluşturduktan sonra ad çözümlemesi için bir DNS sunucusu IP adresini hello ekleyebilirsiniz. Merhaba, belirttiğiniz DNS sunucusu IP adresi için ağınızı hello kaynaklarında hello adlarını çözümleyebildiğini bir DNS sunucusunun hello adresi olması gerekir.<br>tooadd bir DNS sunucusu sanal ağınız için hello Ayarları'nı açın, DNS sunucuları'nı tıklatın ve hello toouse istediğiniz hello DNS sunucusunun IP adresini ekleyin.

### <a name="gateway"></a>2. Kısım: Ağ geçidi alt ağı ve dinamik yönlendirme ağ geçidi oluşturma

Bu adımda bir ağ geçidi alt ağı ve dinamik yönlendirme ağ geçidi oluşturacaksınız. Hello hello Klasik dağıtım modeli için Azure portalı, hello ağ geçidi alt ağı ve hello ağ geçidi oluşturma hello aynı yapılabilir yapılandırma sayfaları.

1. Merhaba Portalı'nda toocreate bir ağ geçidi istediğiniz toohello sanal ağı gidin.
2. Merhaba, sanal ağda hello sayfasında **genel bakış** hello VPN bağlantıları bölümündeki sayfasını tıklatın **ağ geçidi**.

  ![Toocreate bir ağ geçidi'ı tıklatın](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/beforegw125.png)
3. Merhaba üzerinde **yeni VPN bağlantısı** sayfasında, **noktadan siteye**.

  ![Noktadan Siteye bağlantı türü](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/newvpnconnect.png)
4. İçin **istemci adres alanı**, başlangıç IP adresi aralığı ekleyin. Bu, hello VPN istemcileri bir IP adresi bağlanırken alır hello aralıktır. Çakışmayan bir özel IP adres aralığı bağlanacak olan hello şirket içi konumla veya hello tooconnect için istediğiniz VNet ile kullanın. Merhaba otomatik doldurulmuş aralığı silmek, ardından toouse istediğiniz hello özel IP adresi aralığını ekleyin.

  ![İstemci adres alanı](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clientaddress.png)
5. Select hello **ağ geçidini hemen Oluştur** onay kutusu.

  ![Ağ geçidini hemen oluşturma](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/creategwimm.png)
6. Tıklatın **isteğe bağlı ağ geçidi Yapılandırması** tooopen hello **ağ geçidi Yapılandırması** sayfası.

  ![İsteğe bağlı ağ geçidi yapılandırması'na tıklayın](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/optsubnet125.png)
7. Tıklatın **alt ağı yapılandırabilirsiniz gerekli ayarları** tooadd hello **ağ geçidi alt ağı**. Olası toocreate ağ geçidi alt ağı /29 küçük olmakla birlikte, en az/28 veya /27 seçerek daha fazla adreslerini içeren daha büyük bir alt ağı oluşturmanızı öneririz. Bu, gelecekteki hello isteyebileceğiniz yeterli adresleri tooaccommodate olası ek yapılandırmalar için izin verir. Ağ geçidi alt ağları ile çalışırken, bir ağ güvenlik grubu (NSG) toohello ağ geçidi alt ilişkilendirme kaçının. Bir ağ güvenlik grubu toothis alt ilişkilendirme beklendiği gibi çalışmıyor, VPN ağ geçidi toostop neden olabilir.

  ![GatewaySubnet ekleme](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/gwsubnet125.png)
8. Select hello ağ geçidi **boyutu**. Merhaba, sanal ağ geçidinizin hello ağ geçidi SKU'su boyutudur. Merhaba Portalı'nda hello varsayılan SKU olan **temel**. Ağ geçidi SKU’ları hakkında bilgi için bkz. [VPN Gateway Ayarları Hakkında](vpn-gateway-about-vpn-gateway-settings.md#gwsku).

  ![Ağ geçidi boyutu](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/gwsize125.png)
9. Select hello **yönlendirme türü** ağ geçidiniz için. P2S yapılandırmaları bir **Dinamik** yönlendirme türü gerektirir. Bu sayfayı yapılandırmayı bitirdiğinizde **Tamam**’a tıklayın.

  ![Yönlendirme türünü yapılandırma](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/routingtype125.png)
10. Merhaba üzerinde **yeni VPN bağlantısı** sayfasında, **Tamam** hello altındaki hello sayfa toobegin, sanal ağ geçidi oluşturma. Bir VPN ağ geçidi, seçtiğiniz hello ağ geçidi SKU'su bağlı olarak too45 dakika toocomplete yukarı alabilir.

## <a name="generatecerts"></a>2. Sertifika oluşturma

Sertifikalar için noktadan siteye VPN Azure tooauthenticate VPN istemcileri tarafından kullanılır. Ortak anahtar bilgileri hello kök sertifika tooAzure hello karşıya yükleyin. Merhaba ortak anahtar ardından 'güvenilir' olarak kabul edilir. İstemci sertifikaları gerekir hello güvenilen kök sertifika oluşturulur ve ardından her bir istemci bilgisayarı hello Sertifikalar-Geçerli kullanıcı/kişisel sertifika deposunda yüklü. bağlantı toohello VNet başlattığında hello kullanılan tooauthenticate hello istemci sertifikasıdır. 

Otomatik olarak imzalanan sertifikalar kullanıyorsanız bu sertifikaların belirli parametreler kullanılarak oluşturulması gerekir. Merhaba yönergeleri kullanarak otomatik olarak imzalanan bir sertifika oluşturabilir [PowerShell ve Windows 10](vpn-gateway-certificates-point-to-site.md), veya [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md). Otomatik olarak imzalanan sertifikayı otomatik olarak imzalanan kök sertifikalar ile çalışma ve istemci sertifikaları oluşturma hello olduğunda bu yönergeleri hello adımları izleyin önemlidir. Aksi takdirde, oluşturduğunuz hello sertifikaları P2S bağlantılarının ile uyumlu değil ve bağlantı hatası alırsınız.

### <a name="cer"></a>1. Kısım: hello ortak anahtarı (.cer) için hello kök sertifikası alma

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]

### <a name="genclientcert"></a>2. Kısım: İstemci sertifikası oluşturma

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="upload"></a>3. Merhaba kök sertifika .cer dosyasını karşıya yükleyin

Merhaba ağ geçidi oluşturulduktan sonra (Merhaba ortak anahtar bilgileri içeren) hello .cer dosyası için bir güvenilen kök sertifika tooAzure karşıya yükleyebilirsiniz. Merhaba kök sertifika tooAzure için özel anahtar hello karşıya yüklemeyin. Azure a.cer dosya yüklendikten sonra hello güvenilen kök sertifika oluşturulan bir istemci sertifikası yüklemiş tooauthenticate istemcileri kullanabilirsiniz. Gerektiğinde ek güvenilen kök sertifika dosyaları - 20 - daha sonra tooa toplam karşıya yükleyebilirsiniz.  

1. Hello üzerinde **VPN bağlantıları** bölüm hello Vnet'inizi için başlangıç sayfasında, tıklatın **istemcileri** grafik tooopen hello **noktası konumdan konuma VPN bağlantısı** sayfa.

  ![İstemciler](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clients125.png)
2. Merhaba üzerinde **noktadan siteye bağlantı** sayfasında, **yönetmek sertifikaları** tooopen hello **sertifikaları** sayfası.<br>

  ![Sertifikalar sayfası](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/ptsmanage.png)<br><br>
3. Merhaba üzerinde **sertifikaları** sayfasında, **karşıya** tooopen hello **karşıya yükleme sertifika** sayfası.<br>

    ![Sertifikaları karşıya yükle sayfası](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/uploadcerts.png)<br>
4. Başlangıç klasörü grafik toobrowse hello .cer dosyası için'ı tıklatın. Merhaba dosyasını seçin ve ardından **Tamam**. Yenileme hello sayfa toosee karşıya hello sertifika hello **sertifikaları** sayfası.

  ![Sertifikayı karşıya yükleme](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/upload.png)<br>

## <a name="vpnclientconfig"></a>4. Merhaba istemcisini yapılandırma

tooconnect tooa noktadan siteye VPN kullanarak VNet, her istemci paketi tooconfigure hello yerel Windows VPN istemcisi yüklemeniz gerekir. Merhaba yapılandırma paketi hello yerel Windows VPN istemcisi hello ayarları gerekli tooconnect toohello sanal ağ ile yapılandırır.

Hello sürüm hello istemci için hello mimarisi eşleştiği sürece, aynı VPN istemcisi yapılandırma paketini her istemci bilgisayarında hello kullanabilirsiniz. Merhaba, desteklenen istemci işletim sistemlerinin Hello listesi için bkz [noktadan siteye bağlantılar hakkında SSS](#faq) hello bu makalenin sonunda.

### <a name="generateconfigpackage"></a>1. Kısım: Oluşturmak ve hello VPN istemcisi yapılandırma paketini yükleyin

1. Hello Azure portalında, hello içinde **genel bakış** sayfasında ağınız için **VPN bağlantıları**, hello istemci grafik tooopen hello tıklatın **noktası siteye VPN bağlantı** sayfası.
2. Hello hello üstündeki **noktası siteye VPN bağlantısı** toohello istemci işletim sistemi üzerinde yüklenecek karşılık gelen hello indirme paketi tıklayın:

  * 64 bit istemciler için **VPN İstemcisi (64 bit)** seçeneğini belirleyin.
  * 32 bit istemciler için **VPN İstemcisi (32 bit)** seçeneğini belirleyin.

  ![VPN istemcisi yapılandırma paketini indirme](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/dlclient.png)<br>
3. Paketlenmiş hello oluşturur sonra indirin ve istemci bilgisayarınıza yükleyin. Bir SmartScreen açılır penceresi görürseniz **Daha fazla bilgi**’ye ve ardından **Yine de çalıştır**’a tıklayın. Diğer istemci bilgisayarlarda hello paket tooinstall da kaydedebilirsiniz.

### <a name="installclientcert"></a>2. Kısım: Yükleme hello istemci sertifikası

Toocreate bir P2S bağlantısı istiyorsanız hello dışında bir istemci bilgisayardan bir toogenerate hello istemci sertifikalarını kullandığınız, tooinstall bir istemci sertifikası gerekir. Bir istemci sertifikası yüklerken hello istemci sertifikası dışarı aktarılırken oluşturduğunuz hello parola gerekir. Genellikle, bu hello sertifikayı çift ve bu yükleme yalnızca bir konudur. Daha fazla bilgi için bkz. [Dışarı aktarılan istemci sertifikasını yükleme](vpn-gateway-certificates-point-to-site.md#install).

## <a name="connect"></a>5. TooAzure Bağlan

### <a name="connect-tooyour-vnet"></a>Tooyour VNet Bağlan

1. Merhaba istemci bilgisayarda, tooconnect tooyour Vnet'in tooVPN bağlantıları gidin ve oluşturduğunuz hello VPN bağlantısını bulun. Aynı sanal ağ olarak ad hello adlandırılır. **Bağlan**'a tıklayın. Bir açılır ileti toousing hello sertifika başvuran görünebilir. Bu durumda, tıklatın **devam** toouse yükseltilmiş ayrıcalıklar.
2. Merhaba üzerinde **bağlantı** durum sayfasında, tıklatın **Bağlan** toostart hello bağlantı. Görürseniz bir **Sertifika Seç** ekranında, hello istemci sertifikası gösteren toouse tooconnect istediğiniz hello biri olduğunu doğrulayın. Değilse, hello aşağı açılan okunu tooselect hello doğru sertifikayı kullanın ve ardından **Tamam**.

  ![VPN istemci bağlantısı](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clientconnect.png)
3. Bağlantınız kurulur.

  ![Kurulan bağlantı](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>P2S bağlantılarının sorunlarını giderme

[!INCLUDE [verify-client-certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

### <a name="verifyvpnconnect"></a>Merhaba VPN bağlantısını doğrulama

1. VPN bağlantınızın etkin olduğunu tooverify yükseltilmiş bir komut istemi açın ve çalıştırın *ipconfig/all*.
2. Merhaba sonuçları görüntüleyin. Başlangıç IP adresi aldığınız ağınızı oluştururken belirttiğiniz hello noktadan siteye bağlantı adres aralığı içinde hello adreslerinden biri olduğuna dikkat edin. Merhaba sonuçları benzer toothis örnek olmalıdır:

  ```
    PPP adapter VNet1:
        Connection-specific DNS Suffix .:
        Description.....................: VNet1
        Physical Address................:
        DHCP Enabled....................: No
        Autoconfiguration Enabled.......: Yes
        IPv4 Address....................: 192.168.130.2(Preferred)
        Subnet Mask.....................: 255.255.255.255
        Default Gateway.................:
        NetBIOS over Tcpip..............: Enabled
  ```

## <a name="connectVM"></a>Tooa sanal makineye bağlanma

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-classic-include.md)]

## <a name="add"></a>Güvenilen kök sertifika ekleme veya kaldırma

Azure’da güvenilen kök sertifikayı ekleyebilir veya kaldırabilirsiniz. Bir kök sertifikası kaldırdığınızda, o kökünden oluşturulan bir sertifika sahip istemciler mümkün tooauthenticate olmayacaktır ve böylece mümkün tooconnect olmaz. İstemci tooauthenticate ve bağlanmak istiyorsanız, yeni bir istemci sertifikası güvenilen (karşıya yüklenen) tooAzure olan bir kök sertifika oluşturulan tooinstall gerekir.

### <a name="addtrustedroot"></a>tooadd güvenilen bir kök sertifikası

Too20 güvenilen kök sertifika .cer dosyaları tooAzure ekleyebilirsiniz. Yönergeler için bkz: [bölüm 3 - karşıya yükleme hello kök sertifika .cer dosyasını](#upload).

### <a name="removetrustedroot"></a>tooremove güvenilen bir kök sertifikası

1. Hello üzerinde **VPN bağlantıları** bölüm hello Vnet'inizi için başlangıç sayfasında, tıklatın **istemcileri** grafik tooopen hello **noktası konumdan konuma VPN bağlantısı** sayfa.

  ![İstemciler](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clients125.png)
2. Merhaba üzerinde **noktadan siteye bağlantı** sayfasında, **yönetmek sertifikaları** tooopen hello **sertifikaları** sayfası.<br>

  ![Sertifikalar sayfası](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/ptsmanage.png)<br><br>
3. Merhaba üzerinde **sertifikaları** tooremove istediğiniz ardından tıklatın hello üç nokta sonraki toohello sertifika sayfasında, **silmek**.

  ![Kök sertifikayı sil](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deleteroot.png)<br>

## <a name="revokeclient"></a>İstemci sertifikasını iptal etme

İstemci sertifikalarını iptal edebilirsiniz. Merhaba sertifika iptal listesi tooselectively sağlayan tek bir istemci sertifikalarını temel alarak noktadan siteye bağlantı reddedin. Bu, güvenilen kök sertifikayı kaldırma işleminden farklıdır. Azure'dan bir güvenilen kök sertifika .cer kaldırırsanız, tüm istemci sertifikaları için oluşturulan ve imzalanmış hello iptal edilen kök sertifikası tarafından hello erişimi iptal eder. Bir istemci sertifikası iptal etmek hello kök sertifika yerine hello kök sertifika toocontinue toobe hello noktadan siteye bağlantı için kimlik doğrulaması için kullanılan gelen oluşturulan diğer sertifikaları hello sağlar.

Merhaba yaygın toouse hello kök sertifika toomanage erişim düzeyleri, ekip veya kuruluş bireysel kullanıcılar üzerinde ayrıntılı erişim denetimi için İptal edilen istemci sertifikalarını kullanırken bir uygulamadır.

### <a name="revokeclientcert"></a>toorevoke bir istemci sertifikası

Merhaba parmak izi toohello iptal listesine ekleyerek bir istemci sertifikası iptal edebilirsiniz.

1. Merhaba istemci sertifikası parmak izi alma. Daha fazla bilgi için bkz: [nasıl yapılır: bir sertifikanın parmak izini alma hello](https://msdn.microsoft.com/library/ms734695.aspx).
2. Merhaba bilgileri tooa metin düzenleyicisi kopyalayın ve sürekli bir dize olmasını tüm boşlukları Kaldır.
3. Toohello gidin **'Klasik sanal ağ adı' > noktadan siteye VPN bağlantısı > sertifikaları** sayfasında ve ardından **iptal listesi** tooopen hello iptal listesi sayfası. 
4. Merhaba üzerinde **iptal listesi** sayfasında, **+ Ekle sertifika** tooopen hello **Ekle sertifika toorevocation listesi** sayfası.
5. Merhaba üzerinde **Ekle sertifika toorevocation listesi** sayfasında, bir sürekli metin satırının boşluk olarak hello sertifika parmak izi yapıştırın. Tıklatın **Tamam** hello sayfanın hello sonundaki.
6. Güncelleştirme tamamlandıktan sonra hello sertifika artık kullanılan tooconnect olabilir. Bu sertifikayı kullanarak tooconnect deneyin istemcileri bu hello sertifika artık geçerli olduğunu bildiren bir ileti alırsınız.

## <a name="faq"></a>Noktadan Siteye hakkında SSS

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>Sonraki adımlar
Bağlantınız tamamlandıktan sonra sanal makineleri tooyour sanal ağları ekleyebilirsiniz. Daha fazla bilgi için bkz. [Sanal Makineler](https://docs.microsoft.com/azure/#pivot=services&panel=Compute). Ağ ve sanal makineler hakkında daha fazla toounderstand bkz [Azure ve Linux VM ağına genel bakış](../virtual-machines/linux/azure-vm-network-overview.md).
