---
title: "Şirket içi ağ tooan Azure sanal ağı bağlanın: siteden siteye VPN (Klasik): portalı | Microsoft Docs"
description: "Şirket içi bir IPSec bağlantısı üzerinden tooan Azure sanal ağı ağ adımları toocreate genel Internet hello. Bu adımları hello portal kullanarak şirket içi siteden siteye VPN ağ geçidi bağlantı oluşturmanıza yardımcı olur."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/010/2017
ms.author: cherylmc
ms.openlocfilehash: b260bdf610b264458660b278bd32bf0fc5b519ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-using-hello-azure-portal-classic"></a>Hello Azure portal (Klasik) kullanarak siteden siteye bağlantı oluşturma

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

Bu makale size nasıl toouse hello Azure portal toocreate, şirket içi ağ toohello VNet bir siteden siteye VPN ağ geçidi bağlantısını gösterir. Bu makaledeki adımları Hello toohello Klasik dağıtım modeli uygulayın. Liste aşağıdaki hello farklı bir seçeneği seçerek farklı dağıtım aracını veya dağıtım modelini kullanarak bu yapılandırma ayrıca oluşturabilirsiniz:

> [!div class="op_single_selector"]
> * [Azure portal](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Azure portal (klasik)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

Kullanılan tooconnect bir siteden siteye VPN gateway bağlantısı olan bir IPSec/IKE (Ikev1 veya Ikev2) VPN tüneli üzerinden tooan Azure sanal ağı şirket içi ağ. Bağlantı bu tür bir VPN cihazı bulunan dışarıya dönük bir genel IP adresi atanmış tooit olan şirket içi gerektirir. VPN ağ geçitleri hakkında daha fazla bilgi için bkz. [VPN ağ geçidi hakkında](vpn-gateway-about-vpngateways.md).

![Siteden Siteye şirket içi ve dışı karışık VPN Gateway bağlantısı diyagramı](./media/vpn-gateway-howto-site-to-site-classic-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a>Başlamadan önce

Ölçüt yapılandırmaya başlamadan önce aşağıdaki hello karşıladığınızı doğrulayın:

* Merhaba Klasik dağıtım modelinde toowork istediğinizi doğrulayın. Merhaba Resource Manager dağıtım modelinde toowork istiyorsanız, bkz: [bir siteden siteye bağlantı (Resource Manager) oluşturmak](vpn-gateway-howto-site-to-site-resource-manager-portal.md). Mümkün olduğunda, hello Resource Manager dağıtım modeli kullanmanızı öneririz.
* Uyumlu bir VPN cihazı ve mümkün tooconfigure olan birisi olduğundan emin olun. Uyumlu VPN cihazları ve cihaz yapılandırması hakkında daha fazla bilgi için bkz.[VPN Cihazları Hakkında](vpn-gateway-about-vpn-devices.md).
* VPN cihazınız için dışarıya dönük genel bir IPv4 adresi olduğunu doğrulayın. Bu IP adresi bir NAT’nin arkasında olamaz.
* Bulunan hello IP adresi aralıklarıyla ilgili bilginiz yoksa, şirket içi ağ, bu ayrıntıları sizin için sağlayabilecek biriyle toocoordinate gerekir. Bu yapılandırma oluşturduğunuzda, Azure tooyour şirket içi konumu yönlendirilecek hello IP adresi aralığı önekleri belirtmeniz gerekir. Şirket içi ağınıza hello ağların hiçbiri diz tooconnect için istediğiniz hello sanal ağ alt ağı üzerinden olabilir.
* Şu anda, PowerShell gerekli toospecify hello paylaşılan anahtarı ve hello VPN ağ geçidi bağlantı oluşturun. Merhaba hello Azure Hizmet Yönetimi (SM) PowerShell cmdlet'lerinin en son sürümünü yükleyin. Daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview). Bu yapılandırma için PowerShell ile çalışırken yönetici olarak işlem yaptığınızdan emin olun. 

### <a name="values"></a>Bu alıştırma için örnek yapılandırma değerleri

Bu makaledeki örneklerde Hello değerleri aşağıdaki hello kullanın. Bu değerleri toocreate bir test ortamı kullanın veya toothem başvurun toobetter anlamak bu makaledeki hello örnekler.

* **VNet Name:** TestVNet1
* **Adres Alanı:** 
  * 10.11.0.0/16
  * 10.12.0.0/16 (bu alıştırma için isteğe bağlı)
* **Alt ağlar:**
  * FrontEnd: 10.11.0.0/24
  * BackEnd: 10.12.0.0/24 (bu alıştırma için isteğe bağlı)
* **GatewaySubnet:** 10.11.255.0/27
* **Kaynak Grubu:** TestRG1
* **Konum:** Doğu ABD
* **DNS Sunucusu:** 10.11.0.3 (bu alıştırma için isteğe bağlı)
* **Yerel site adı:** Site2
* **İstemci adres alanı:** Merhaba, şirket içi sitesinde yer alan adres alanı.

## <a name="CreatVNet"></a>1. Sanal ağ oluşturma

S2S bağlantısı için bir sanal ağ toouse oluşturduğunuzda, belirttiğiniz hello adres alanlarından herhangi biriyle hello istemci adres alanları için tooconnect istediğiniz hello yerel siteler için çakışmadığından emin toomake gerekir. Çakışan alt ağlarınız varsa bağlantınız düzgün şekilde gerçekleşmeyebilir.

* Bir VNet zaten varsa, hello ayarlarının VPN ağ geçidi tasarımınız ile uyumlu olduğunu doğrulayın. Diğer ağlar ile çakışabilen tooany alt ağlar belirli dikkat edin. 

* Sanal ağınız yoksa bir sanal ağ oluşturun. Ekran görüntüleri örnek olarak verilmiştir. Emin tooreplace hello değerleri kendi değerlerinizle olabilir.

### <a name="toocreate-a-virtual-network"></a>toocreate bir sanal ağ

1. Tarayıcıdan toohello gidin [Azure portal](http://portal.azure.com) ve gerekiyorsa Azure hesabınızla oturum açın.
2. **+** öğesine tıklayın. Merhaba, **arama hello Market** alanında, 'Sanal ağ' yazın. Bulun **sanal ağ** döndürülen hello listelemek ve tooopen hello'ı tıklatın **sanal ağ** sayfası.

  ![Sanal ağ ara sayfası](./media/vpn-gateway-howto-site-to-site-classic-portal/newvnetportal700.png)
3. Merhaba alt kısmındaki hello de hello sanal ağ sayfasından **dağıtım modeli seçin** açılır listesinde, select **Klasik**ve ardından **oluşturma**.

  ![Dağıtım modeli seçme](./media/vpn-gateway-howto-site-to-site-classic-portal/selectmodel.png)
4. Merhaba üzerinde **sanal network(classic) oluşturma** sayfasında, hello VNet ayarlarını yapılandırın. Bu sayfada, ilk adres alanınızı ve tek alt ağ adres aralığınızı eklersiniz. Merhaba VNet oluşturma işlemini tamamladıktan sonra geri dönün ve ek alt ağları ve adres alanlarını ekleyin.

  ![Sanal ağ oluşturma sayfası](./media/vpn-gateway-howto-site-to-site-classic-portal/createvnet.png "Sanal ağ oluşturma sayfası")
5. Bu hello doğrulayın **abonelik** hello doğru olduğundan. Merhaba açılan kullanarak abonelikleri değiştirebilirsiniz.
6. **Kaynak grubu**’na tıklayın, mevcut bir kaynak grubunu seçin ya da bir ad yazarak yeni bir tane oluşturun. Kaynak grupları hakkında daha fazla bilgi için [Azure Resource Manager’a Genel Bakış](../azure-resource-manager/resource-group-overview.md#resource-groups)’ı ziyaret edin.
7. Ardından, hello'ı seçin **konumu** ayarlarını. Merhaba kaynakları toothis VNet dağıtmadan bulunacağı Hello konumunu belirler.
8. Ağınızı hello Panoda kolayca toobe mümkün toofind istiyorsanız seçin **PIN toodashboard**. Tıklatın **oluşturma** toocreate Vnet'inizi.

  ![PIN toodashboard](./media/vpn-gateway-howto-site-to-site-classic-portal/pintodashboard150.png "PIN toodashboard")
9. 'Oluştur' tıklatıldığında sonra bir kutucuğu hello Vnet'inizin ilerleme durumunu yansıtır hello panosunda görüntülenir. VNet Hello döşeme değişiklikleri hello olarak oluşturuldu.

  ![Sanal ağ oluşturma kutucuğu](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deploying150.png "Creating virtual network")

Sanal ağınız oluşturulduktan sonra gördüğünüz **oluşturulan** altında listelenen **durum** hello Klasik Azure Portalı'ndaki hello ağlar sayfasında.

## <a name="additionaladdress"></a>2. Başka adres alanı ekleme

Sanal ağınızı oluşturduktan sonra başka adres alanı ekleyebilirsiniz. Ek adres alanı ekleme S2S yapılandırma gerekli bir parçası değil, ancak birden çok adres alanları gerektiriyorsa, hello aşağıdaki adımları kullanın:

1. Merhaba sanal ağlar hello Portalı'nda bulun.
2. Merhaba altında sanal ağınız için hello sayfasında **ayarları** 'yi tıklatın **adres alanı**.
3. Merhaba adres alanı sayfasında, tıklatın **+ Ekle** ve ek adres alanı girin.

## <a name="dns"></a>3. DNS sunucusu belirleme

DNS ayarları, S2S yapılandırmasının gerekli bir kısmı değildir, ancak ad çözünürlüğü istiyorsanız DNS gereklidir. Bir değer belirtildiğinde yeni bir DNS sunucusu oluşturulmaz. Merhaba, belirttiğiniz DNS sunucusu IP adresi, bağlandığınız hello kaynaklar için hello adları çözümlemek için bir DNS sunucusu olmalıdır. Merhaba örnek ayarları için özel bir IP adresi kullanılır. kullanırız hello IP adresi başlangıç IP adresi, DNS sunucunuzun değil büyük olasılıkla. Kendi değerlerinizi toouse emin olun.

Sanal ağınızı oluşturduktan sonra başlangıç IP adresi, bir DNS sunucusu toohandle ad çözümlemesinin ekleyebilirsiniz. Sanal ağınız için Hello Ayarları'nı açın, DNS sunucuları'nı tıklatın ve ad çözümlemesi için toouse istediğiniz hello DNS sunucusunun IP adresini hello ekleyin.

1. Merhaba sanal ağlar hello Portalı'nda bulun.
2. Merhaba altında sanal ağınız için hello sayfasında **ayarları** 'yi tıklatın **DNS sunucuları**.
3. Bir DNS sunucusu ekleyin.
4. toosave, Ayarlar'ı **kaydetmek** hello sayfanın üst kısmındaki hello.

## <a name="localsite"></a>4. Merhaba yerel site yapılandırma

Merhaba yerel site genellikle tooyour içi konumunuz anlamına gelir. Bir bağlantı ve hello VPN ağ geçidi toohello VPN cihazı yönlendirilecek hello IP adres aralıklarını oluşturacak hello VPN cihaz toowhich hello IP adresini içerir.

1. Merhaba Portalı'nda toocreate bir ağ geçidi istediğiniz toohello sanal ağı gidin.
2. Merhaba, sanal ağda hello sayfasında **genel bakış** hello VPN bağlantıları bölümündeki sayfasını tıklatın **ağ geçidi** tooopen hello **yeni VPN bağlantısı** sayfa.

  ![Tooconfigure ağ geçidi ayarları](./media/vpn-gateway-howto-site-to-site-classic-portal/beforegw125.png "tooconfigure ağ geçidi ayarları")
3. Merhaba üzerinde **yeni VPN bağlantısı** sayfasında, **siteden siteye**.
4. Tıklatın **yerel site - gerekli ayarları Yapılandır** tooopen hello **yerel site** sayfa. Hello ayarlarını yapılandırın ve ardından **Tamam** toosave hello ayarları.
  - **Ad:** , yerel site toomake için bir ad oluşturun, tooidentify için kolay.
  - **VPN ağ geçidi IP adresi:** hello hello VPN cihazı şirket içi ağınız için genel IP adresi budur. Merhaba VPN aygıt bir IPv4 ortak IP adresi gerektirir. Merhaba tooconnect istediğiniz VPN cihaz toowhich için geçerli bir ortak IP adresi belirtin. NAT'nin ardında olamaz ve Azure tarafından erişilebilir toobe sahiptir. Bilmiyorsanız VPN Cihazınızı hello IP adresi, (geçerli bir ortak IP adresi hello biçiminde olduğu sürece) her zaman bir yer tutucu değerini alın ve daha sonra değiştirin.
  - **İstemci adres alanı:** istediğiniz listesi hello IP adres aralıklarını toohello yerel şirket içi ağ bu ağ geçidi üzerinden yönlendirilir. Birden fazla adres alanı aralığı ekleyebilirsiniz. Burada belirttiğiniz hello aralıkları sanal ağınıza bağlanan diğer ağların aralıklarıyla ya da sanal ağ hello kendisini hello adres aralıklarını ile çakışmadığından emin olun.

  ![Yerel site](./media/vpn-gateway-howto-site-to-site-classic-portal/localnetworksite.png "Configure local site")

## <a name="gatewaysubnet"></a>5. Merhaba ağ geçidi alt ağı yapılandırma

VPN ağ geçidiniz için bir ağ geçidi alt ağı oluşturmanız gerekir. Hello ağ geçidi alt ağı hello VPN ağ geçidi Hizmetleri kullanın hello IP adreslerini içerir.

1. Merhaba üzerinde **yeni VPN bağlantısı** sayfası, select hello onay kutusunu **ağ geçidini hemen Oluştur**. İsteğe bağlı ağ geçidi Hello 'configuration' sayfası görüntülenir. Merhaba onay kutusunu seçmezseniz, hello sayfa tooconfigure hello ağ geçidi alt ağı görmezsiniz.

  ![Ağ geçidi yapılandırması - Alt ağ, boyut, yönlendirme türü](./media/vpn-gateway-howto-site-to-site-classic-portal/optional.png "Gateway configuration - Subnet, size, routing type")
2. tooopen hello **ağ geçidi Yapılandırması** sayfasında, **isteğe bağlı ağ geçidi yapılandırması - alt ağ, boyut, yönlendirme türü**.
3. Merhaba üzerinde **ağ geçidi Yapılandırması** sayfasında, **Subnet - gerekli ayarları Yapılandır** tooopen hello **alt ağ Ekle** sayfası.

  ![Ağ geçidi yapılandırması - ağ geçidi alt ağı](./media/vpn-gateway-howto-site-to-site-classic-portal/subnetrequired.png "Gateway configuration - gateway subnet")
4. Merhaba üzerinde **alt ağ Ekle** sayfasında, hello ağ geçidi alt ağı ekleyin. Merhaba, belirttiğiniz hello ağ geçidi alt ağı boyutunu toocreate istediğiniz hello VPN ağ geçidi yapılandırmasına bağlıdır. Olası toocreate ağ geçidi alt ağı /29 küçük olmakla birlikte, / 27 veya /28 kullanmanızı öneririz. Bu değer, daha fazla adres içeren daha büyük bir alt ağ oluşturur. Daha büyük bir ağ geçidi alt ağı kullanmak yeterli IP adreslerini tooaccommodate olası gelecekteki yapılandırmaları için sağlar.

  ![Ağ geçidi alt ağı ekleme](./media/vpn-gateway-howto-site-to-site-classic-portal/addgwsubnet.png "Add gateway subnet")

## <a name="sku"></a>6. Merhaba SKU ve VPN türünü belirtin

1. Select hello ağ geçidi **boyutu**. Merhaba ağ geçidi SKU'su toocreate sanal ağ geçidinizi kullanın budur. 'Varsayılan SKU' Hello Portalı'nda hello = **temel**. Klasik VPN ağ geçitleri hello eski (eski) ağ geçidi SKU'ları kullanın. Merhaba eski ağ geçidi SKU'ları hakkında daha fazla bilgi için bkz: [sanal ağ geçidi SKU'ları (eski SKU) ile çalışma](vpn-gateway-about-skus-legacy.md).

  ![SKUL ve VPN türü seçme](./media/vpn-gateway-howto-site-to-site-classic-portal/sku.png "Select SKU and VPN type")
2. Select hello **yönlendirme türü** ağ geçidiniz için. Olarak da bilinen hello VPN türü budur. Bir türü tooanother hello ağ geçidi dönüştürülemiyor önemli tooselect hello doğru ağ geçidi türü demektir. VPN Cihazınızı seçtiğiniz hello yönlendirme türü ile uyumlu olması gerekir. VPN türü hakkında daha fazla bilgi için bkz. [VPN Gateway Ayarları hakkında](vpn-gateway-about-vpn-gateway-settings.md#vpntype). Too'RouteBased başvuran makaleleri görebilirsiniz ' ve 'PolicyBased' VPN türleri. ' Dinamik 'karşılık gelen too'RouteBased', ve 'Static' karşılık gelen 'PolicyBased'.
3. Tıklatın **Tamam** toosave hello ayarları.
4. Merhaba üzerinde **yeni VPN bağlantısı** sayfasında, **Tamam** hello altındaki hello sayfa toobegin, sanal ağ geçidi oluşturma. Seçtiğiniz SKU Hello bağlı olarak, bir sanal ağ geçidi too45 dakika toocreate devam edebilir.

## <a name="vpndevice"></a>7. VPN cihazınızı yapılandırma

Siteden siteye bağlantıları tooan şirket içi ağ bir VPN cihazı gerektirir. Bu adımda VPN cihazınızı yapılandıracaksınız. VPN Cihazınızı yapılandırırken hello aşağıdaki gerekir:

- Paylaşılan bir anahtar. Bu olduğu hello aynı paylaşılan siteden siteye VPN bağlantınızı oluştururken belirttiğiniz anahtarı. Bu örneklerde temel bir paylaşılan anahtar kullanılır. Daha karmaşık bir anahtar toouse oluşturmak öneririz.
- Merhaba sanal ağ geçidinizin genel IP adresi. Hello Azure portal, PowerShell veya CLI kullanarak hello ortak IP adresini görüntüleyebilirsiniz.

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <a name="CreateConnection"></a>8. Merhaba bağlantısı oluşturma
Bu adımda, hello paylaşılan anahtarı ayarlayın ve hello bağlantı oluşturun. ayarladığınız hello anahtarı hello olmalıdır, VPN cihazı yapılandırmasında kullanılan aynı anahtarı.

> [!NOTE]
> Şu anda, bu adımı hello Azure portalında kullanılabilir değil. Hello Azure PowerShell cmdlet'lerini hello Hizmet Yönetimi (SM) sürümünü kullanmanız gerekir.
>

### <a name="step-1-connect-tooyour-azure-account"></a>1. Adım Azure hesabı tooyour Bağlan

1. Yükseltilmiş haklarla PowerShell Konsolunuzu açın ve tooyour hesap bağlanın. Bağlandığınız örnek toohelp aşağıdaki hello kullan:

  ```powershell
  Add-AzureAccount
  ```
2. Merhaba hesabının Hello abonelikleri kontrol edin.

  ```powershell
  Get-AzureSubscription
  ```
3. Birden fazla aboneliğiniz varsa, toouse istediğiniz hello aboneliği seçin.

  ```powershell
  Select-AzureSubscription -SubscriptionId "Replace_with_your_subscription_ID"
  ```

### <a name="step-2-set-hello-shared-key-and-create-hello-connection"></a>2. Adım Merhaba paylaşılan anahtar ayarlayın ve hello bağlantısı oluşturma

PowerShell ve hello Klasik dağıtım modeliyle çalışırken, bazen hello adları hello portalında kaynakların hello adları hello Azure PowerShell kullanırken toosee bekliyor değildir. Merhaba aşağıdaki adımları hello ağ yapılandırma dosyası tooobtain hello tam değerleri hello adları için dışarı aktarma yardımcı.

1. Bilgisayarınızda bir dizin oluşturun ve ardından hello ağ yapılandırma dosyası toohello dizini verin. Bu örnekte, hello ağ yapılandırmasını dışarı aktarılan tooC:\AzureNet dosyasıdır.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. Bir xml Düzenleyicisi ile Merhaba ağ yapılandırma dosyasını açın ve 'LocalNetworkSite adı' ve 'VirtualNetworkSite name' hello değerlerini denetleyin. Gereksinim duyduğunuz hello örnek tooreflect hello değerleri değiştirin. Boşluk içeren bir ad belirtirken, hello değeri tek tırnak işareti kullanın.

3. Merhaba paylaşılan anahtarı ayarlayın ve hello bağlantı oluşturun. Merhaba '-SharedKey' oluşturmak ve belirten bir değer. 'Abc123' kullandık Hello örnekte, ancak oluşturabileceğiniz (ve gereken) daha karmaşık bir şey kullanın. Burada belirttiğiniz başlangıç değeri şeydir önemli Hello hello aynı VPN Cihazınızı yapılandırırken belirtilen değeri olmalıdır.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group TestRG1 TestVNet1' `
  -LocalNetworkSiteName 'D1BFC9CB_Site2' -SharedKey abc123
  ```
Merhaba bağlantı oluşturulduğunda, hello sonucudur: **durumu: başarılı**.

## <a name="verify"></a>9. Bağlantınızı doğrulama

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

Merhaba bağlanma konusunda sorun yaşıyorsanız, bkz: **sorun giderme** hello İçindekiler hello sol bölmede bölümü.

## <a name="reset"></a>Nasıl tooreset bir VPN ağ geçidi

Bir veya daha fazla Siteden Siteye VPN tünelinde şirketler arası VPN bağlantısını kaybederseniz bir Azure VPN ağ geçidinin sıfırlanması yararlıdır. Bu durumda, şirket içi VPN cihazlarınızı tüm düzgün şekilde çalışıp çalışmadığını, ancak şu tooestablish hello Azure VPN ağ geçitleri ile IPSec tünelleri. Adımlar için bkz. [VPN ağ geçidini sıfırlama](vpn-gateway-resetgw-classic.md).

## <a name="changesku"></a>Nasıl toochange bir ağ geçidi SKU'su

Merhaba, bir ağ geçidi SKU'su toochange adımları için bkz: [bir ağ geçidi SKU'su yeniden boyutlandırma](vpn-gateway-about-SKUS-legacy.md).

## <a name="next-steps"></a>Sonraki adımlar

* Bağlantınız tamamlandıktan sonra sanal makineleri tooyour sanal ağları ekleyebilirsiniz. Daha fazla bilgi için bkz. [Sanal Makineler](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
* Zorlamalı Tünel Oluşturma hakkında bilgi için bkz. [Zorlamalı Tünel Oluşturma Hakkında](vpn-gateway-about-forced-tunneling.md).