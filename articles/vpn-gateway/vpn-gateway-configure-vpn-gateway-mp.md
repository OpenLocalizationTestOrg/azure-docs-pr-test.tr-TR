---
title: "Bir VPN ağ geçidi yapılandırın: Klasik portalında: Azure | Microsoft Docs"
description: "Bu makalede, sanal ağ VPN ağ geçidi yapılandırma ve ağ geçidi yönlendirme VPN türü değiştirme aracılığıyla anlatılmaktadır. Toohello Klasik dağıtım modeli ve hello Klasik portalında aşağıdaki adımları uygulayın."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fbe59ba8-b11f-4d21-9bb1-225ec6c6d351
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/04/2017
ms.author: cherylmc
ms.openlocfilehash: 00d2fa18bab6eb24b33ddb18113f2a557db638d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vpn-gateway-in-hello-classic-portal"></a>Bir VPN ağ geçidi hello Klasik portalında yapılandırın 
Toocreate Azure ile şirket içi konumunuz arasında güvenli şirket içi bağlantısı istiyorsanız, bir sanal ağ geçidi toocreate gerekir. Bir VPN ağ geçidi sanal ağ geçidi belirli bir türde değil. Merhaba Klasik dağıtım modelinde bir VPN ağ geçidi iki VPN yönlendirme türlerden biri olabilir: statik veya dinamik. Merhaba seçtiğiniz VPN türü hem, ağ tasarım planınızı ve toouse istediğiniz hello şirket içi VPN aygıtını bağlıdır. VPN cihazları hakkında daha fazla bilgi için bkz: [VPN aygıtları hakkında](vpn-gateway-about-vpn-devices.md).

**Azure dağıtım modelleri hakkında**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-overview"></a>Yapılandırmasına genel bakış
Merhaba aşağıdaki adımlar, VPN ağ geçidinizi hello Klasik Portalı'nda yapılandırmada size yol gösterir. Bu adımlar toogateways hello Klasik dağıtım modeli kullanılarak oluşturulan sanal ağlar için geçerlidir. Şu anda, tüm ağ geçitleri hello yapılandırma ayarlarını hello Azure portalında kullanılabilir. Olduklarında, toohello Azure portal geçerli yönergeleri yeni bir dizi oluşturacağız.

### <a name="before-you-begin"></a>Başlamadan önce
Ağ geçidi yapılandırmadan önce sanal ağınızı ilk toocreate gerekir. Adımları toocreate şirket içi bağlantılar için bir sanal ağ için bkz: [sanal ağ ile bir siteden siteye VPN bağlantısı yapılandırma](vpn-gateway-site-to-site-create.md), veya [NoktadansiteyeVPNbağlantısıilesanalağyapılandırma](vpn-gateway-point-to-site-create.md). Sonra aşağıdaki adımları tooconfigure hello VPN ağ geçidi hello kullanın ve VPN Cihazınızı tooconfigure gereksinim hello bilgileri toplayın. 

Bir VPN ağ geçidi zaten var ve toochange hello VPN yönlendirme türü istiyorsanız, bkz [nasıl toochange hello ağ geçidiniz için VPN yönlendirme türü](#how-to-change-the-vpn-routing-type-for-your-gateway).

## <a name="create-a-vpn-gateway"></a>VPN ağ geçidi oluşturun
1. Merhaba, [Klasik Azure portalı](https://manage.windowsazure.com), hello üzerinde **ağlar** sayfasında, sanal ağınız için o hello Durum sütununda doğrulayın **oluşturulan**.
2. Merhaba, **adı** sütunu, sanal ağınızı hello adına tıklayın.
3. Merhaba üzerinde **Pano** sayfasında, bu VNet henüz yapılandırılmış bir ağ geçidi olmadığına dikkat edin. Ağ geçidi hello adımları tooconfigure ilerledikçe, bu durum görürsünüz.

![Ağ geçidi oluşturulmadı](./media/vpn-gateway-configure-vpn-gateway-mp/IC717025.png)

Bundan sonra hello sayfasının hello altında öğesini **ağ geçidi Oluştur**. Her ikisini seçebilirsiniz *statik yönlendirme* veya *dinamik yönlendirme*. Merhaba seçtiğiniz VPN yönlendirme türü, birkaç etkene bağlıdır. Örneğin, hangi VPN Cihazınızı destekler ve toosupport noktadan siteye bağlantıları ihtiyacınız olup olmadığı. Denetleme [sanal ağ bağlantısı için VPN aygıtları hakkında](vpn-gateway-about-vpn-devices.md) tooverify hello gereken VPN yönlendirme türü. Merhaba ağ geçidi oluşturulduktan sonra silme ve hello ağ geçidi yeniden oluşturma olmadan ağ geçidi VPN yönlendirme türleri arasında değiştiremezsiniz. Ne zaman hello sistem sizden hello oluşturulan ağ geçidi'ye tıklayın, istediğiniz tooconfirm **Evet**.

![Ağ geçidi VPN yönlendirme türü](./media/vpn-gateway-configure-vpn-gateway-mp/IC717026.png)

Ağ geçidi oluştururken, başlangıç sayfasında hello ağ geçidi grafiği tooyellow değiştirir ve diyor dikkat edin *ağ geçidi oluşturma*. Merhaba ağ geçidi toocreate too45 dakika yukarı sürebilir. Diğer yapılandırma ayarlarıyla İleri taşımadan önce hello ağ geçidi tamamlanana kadar bekleyin.

![Ağ geçidi oluşturma](./media/vpn-gateway-configure-vpn-gateway-mp/IC717027.png)

Ne zaman hello ağ geçidi değişiklikleri çok*bağlanıyor*, VPN cihazınız için gerekir hello bilgi toplayabilir.

![Ağ geçidi bağlanma](./media/vpn-gateway-configure-vpn-gateway-mp/IC717028.png)

## <a name="site-to-site-connections"></a>Siteden siteye bağlantılar

### <a name="step-1-gather-information-for-your-vpn-device-configuration"></a>1. Adım VPN cihazınızın yapılandırması bilgileri toplayın
Merhaba ağ geçidi oluşturulduktan sonra bir siteden siteye bağlantı oluşturuyorsanız, VPN cihazınızın yapılandırması bilgileri toplayın. Bu bilgiler hello üzerinde bulunan **Pano** sayfasında sanal ağınız için:

1. **Ağ geçidi IP adresi -** başlangıç IP adresi üzerinde hello bulunabilir **Pano** sayfası. Ağ geçidiniz kadar sonra oluşturmayı tamamlandıktan mümkün toosee olmayacaktır.
2. **Paylaşılan anahtar -** tıklatın **yönetme anahtarı** Merhaba ekranında hello sonundaki. Merhaba simgesi sonraki toohello anahtar toocopy'ı tıklatın, tooyour Pano yapıştırın ve başlangıç anahtarı kaydedin. Bu düğme, yalnızca tek S2S VPN tüneli olduğunda çalışır. Birden fazla S2S VPN tünelleri varsa, hello kullanın *alma sanal ağ geçidi paylaşılan anahtarı* API veya PowerShell cmdlet'ini.

![Anahtarı yönetme](./media/vpn-gateway-configure-vpn-gateway-mp/IC717029.png)

### <a name="step-2--configure-your-vpn-device"></a>2. Adım  VPN cihazınızı yapılandırma
Siteden siteye bağlantıları tooan şirket içi ağ bir VPN cihazı gerektirir. Yapılandırma adımları için tüm VPN aygıtları sağlamıyorsa olsa da, bağlantılar yararlı aşağıdaki hello hello bilgi bulabilirsiniz:

- Uyumlu VPN cihazları hakkında bilgi için bkz. [VPN Cihazları](vpn-gateway-about-vpn-devices.md). 
- Bağlantılar toodevice yapılandırma ayarları için bkz: [doğrulanan VPN cihazları](vpn-gateway-about-vpn-devices.md#devicetable). Bu bağlantılar en iyi çabalarımız sonucu elde ettiğimiz bağlantılardır. Her zaman, en iyi toocheck hello son yapılandırma bilgilerini için cihaz üreticinize olur.
- Cihaz yapılandırma örneklerini düzenleme hakkında daha fazla bilgi için bkz. [Örnekleri düzenleme](vpn-gateway-about-vpn-devices.md#editing).
- IPsec/IKE parametreleri için bkz. [Parametreler](vpn-gateway-about-vpn-devices.md#ipsec).
- VPN Cihazınızı yapılandırmadan önce denetlemek [bilinen cihaz uyumluluk sorunları](vpn-gateway-about-vpn-devices.md#known) hello VPN aygıtının toouse istiyor.

VPN Cihazınızı yapılandırırken, aşağıdaki öğelerindeki hello gerekir:

- Merhaba sanal ağ geçidinizin genel IP adresi. Bu giderek toohello tarafından bulabilir **genel bakış** dikey sanal ağınız için.
- Paylaşılan bir anahtar. Bu olduğu hello aynı paylaşılan siteden siteye VPN bağlantınızı oluştururken belirttiğiniz anahtarı. Bu örneklerde çok temel bir paylaşılan anahtar kullanılır. Daha karmaşık bir anahtar toouse oluşturmanız gerekir.

Merhaba VPN cihazı yapılandırıldıktan sonra ağınız için hello panosu sayfasında, güncelleştirilmiş bağlantı bilgilerini görüntüleyebilirsiniz.

### <a name="step-3-verify-your-local-network-ranges-and-vpn-gateway-ip-address"></a>3. Adım Yerel ağ Aralıklarınızın ve VPN ağ geçidi IP adresini doğrulayın
#### <a name="verify-your-vpn-gateway-ip-address"></a>VPN ağ geçidi IP adresinizi doğrulayın
Ağ geçidi tooconnect için düzgün şekilde, VPN cihazınız için başlangıç IP adresi doğru hello şirket içi yapılandırmanızla ilgili belirtilen yerel ağ için yapılandırılması gerekir. Genellikle, bu hello siteden siteye yapılandırma işlemi sırasında yapılandırılır. Ancak, daha önce bu yerel ağ ile farklı bir cihaz kullandığınız ya da bu yerel ağ için başlangıç IP adresi değişti, hello ayarları toospecify hello doğru ağ geçidi IP adresi düzenleyin.

1. tooverify, ağ geçidi IP adresi tıklatın **ağlar** hello portal sol bölmesinde ve ardından **yerel ağlar** hello sayfanın üst kısmındaki hello. Oluşturduğunuz her bir yerel ağ VPN ağ geçidi adresi hello görürsünüz. tooedit başlangıç IP adresi, hello VNet seçin ve tıklatın **Düzenle** hello sayfanın hello sonundaki.
2. Merhaba üzerinde **, yerel ağ ayrıntılarını belirtin** sayfasında, başlangıç IP adresi Düzenle ve hello sayfanın hello sonundaki hello İleri okuna tıklayın.
3. Merhaba üzerinde **hello adres alanını belirtin** sayfasında, ayarlarınızı hello alt sağ toosave hello onay işaretine tıklayın.

#### <a name="verify-hello-address-ranges-for-your-local-networks"></a>Yerel ağlar için başlangıç adresi aralıklarını doğrulama
Merhaba ağ geçidi tooyour şirket içi konumu aracılığıyla Hello doğru trafiği tooflow için her bir IP adresi aralığı belirttiğiniz tooverify gerekir. Her aralık Azure listelenmelidir **yerel ağlar** yapılandırma. Ağ yapılandırması Hello şirket içi konumunuz bağlı olarak, bu biraz büyük bir görev olabilir. Listelenen hello aralıklar içinde yer alan bir IP adresi için bağlı trafiği hello sanal ağ VPN ağ geçidi üzerinden gönderilir. Merhaba, liste toobe özel aralıkları sahip değilseniz, şirket içi yapılandırmanızı alabilir tooverify istediğiniz ancak gelen trafiği hello aralıkları.

bir yerel ağ tooadd veya düzenleme hello aralıklarını hello aşağıdaki adımları kullanın:

1. tooedit başlangıç IP adresi aralıkları için bir yerel ağ tıklatın **ağlar** hello portal sol bölmesinde ve ardından **yerel ağlar** hello sayfanın üst kısmındaki hello. Merhaba Portalı'nda listelediğiniz hello en kolay yolu tooview hello aralıkları olduğundan üzerinde hello **Düzenle** sayfası. aralıkları, select VNet hello ve tıklayın toosee **Düzenle** hello sayfanın hello sonundaki.
2. Merhaba üzerinde **, yerel ağ ayrıntılarını belirtin** sayfasında, herhangi bir değişiklik yapmayın. Merhaba sayfanın hello sonundaki Hello İleri okuna tıklayın.
3. Merhaba üzerinde **hello adres alanını belirtin** sayfasında, ağ adres alanı değişiklikleri yapın. Ardından hello onay işareti toosave yapılandırmanızı tıklayın.

## <a name="how-tooview-gateway-traffic"></a>Nasıl tooview ağ geçidi trafiği
Ağ geçidi ve ağ geçidi trafiği sanal ağınızdan görüntüleyebilirsiniz **Pano** sayfası.

Merhaba üzerinde **Pano** sayfasında hello aşağıdaki görüntüleyebilirsiniz:

* Merhaba hem verileri hem de giden veriler, ağ geçidi üzerinden akan veri miktarı.
* Sanal ağınız için belirtilen hello DNS sunucularının adlarını Hello.
* Ağ geçidiniz ile VPN cihazınız arasındaki Hello bağlantı.
* Merhaba kullanılan tooconfigure anahtarı ağ geçidi bağlantı tooyour VPN cihazınız paylaşılan.

## <a name="how-toochange-hello-vpn-routing-type-for-your-gateway"></a>Nasıl toochange hello ağ geçidiniz için VPN yönlendirme türü
Bazı bağlantı yapılandırmaları yalnızca belirli bir ağ geçidi yönlendirme türleri için kullanılabilir olmadığından toochange hello ağ geçidi VPN yönlendirme türü mevcut bir VPN ağ geçidi gerektiğini fark edebilirsiniz. Örneğin, bir statik ağ geçidi sahip tooadd noktadan siteye bağlantı tooan zaten mevcut olan siteden siteye bağlantı isteyebilirsiniz. Noktadan siteye bağlantılar dinamik ağ geçidi gerektirir. Bu, P2S bağlantısı tooconfigure anlamına gelir, ağ geçidiniz VPN yönlendirme türü statik toodynamic gelen toochange gerekir.

Toochange bir ağ geçidi yönlendirme VPN türü gerekiyorsa, hello mevcut ağ geçidini silin ve ardından hello yeni yönlendirme türü ile yeni bir ağ geçidi oluşturmak. Toodelete hello tüm sanal ağ toochange hello ağ geçidi yönlendirme türü gerek yoktur.

Ağ geçidi yönlendirme VPN türü değiştirmeden önce emin tooverify VPN Cihazınızı toouse istediğiniz hello yönlendirme türünü desteklediğinden emin olun. bkz: toodownload yeni yönlendirme yapılandırma örnekleri ve onay VPN cihaz gereksinimleri [sanal ağ bağlantısı için VPN aygıtları hakkında](vpn-gateway-about-vpn-devices.md).

> [!IMPORTANT]
> Bir sanal ağ VPN ağ geçidi sildiğinizde, hello toohello ağ geçidi atanan VIP yayımlanır. Merhaba ağ geçidi yeniden oluşturduğunuzda, yeni bir VIP tooit atanır.
> 
> 

1. **Merhaba mevcut VPN ağ geçidini silin.**
   
    Merhaba üzerinde **Pano** sayfasında sanal ağınız için hello sayfanın toohello gidin ve tıklayın **silmek ağ geçidi**. Ağ geçidi hello hello bildirim bekle silindi. Ağ geçidi silinip silinmediğini hello bildirimi Merhaba ekranında aldıktan sonra yeni bir ağ geçidi oluşturabilirsiniz.
2. **Yeni bir VPN ağ geçidi oluşturun.**
   
    Başlangıç sayfası toocreate yeni bir ağ geçidi hello üstünde Hello yordamı kullanın: [bir VPN ağ geçidi oluşturma](#create-a-vpn-gateway).

## <a name="next-steps"></a>Sonraki adımlar
Sanal makineler tooyour sanal ağ ekleyebilirsiniz. Bkz: [nasıl toocreate özel bir sanal makine](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Tooconfigure bir noktası konumdan konuma VPN bağlantısı istiyorsanız, bkz: [noktadan siteye VPN bağlantısı yapılandırma](vpn-gateway-point-to-site-create.md).

