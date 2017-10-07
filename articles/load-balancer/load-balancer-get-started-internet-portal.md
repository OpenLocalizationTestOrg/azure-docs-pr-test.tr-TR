---
title: "aaaCreate bir Internet'e yönelik Yük Dengeleyici - Azure portalı | Microsoft Docs"
description: "Resource Manager kullanarak toocreate bir Internet'e yönelik Yük Dengeleyici hello Azure portalına nasıl öğrenin"
services: load-balancer
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: aa9d26ca-3d8a-4a99-83b7-c410dd20b9d0
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: annahar
ms.openlocfilehash: 390ba8ec1474c54cf2c0022c4a3c219d21b1a659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-hello-azure-portal"></a>Hello Azure portal kullanarak bir Internet'e yönelik Yük Dengeleyici oluşturma

> [!div class="op_single_selector"]
> * [Portal](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Şablon](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Bu makalede, hello Resource Manager dağıtım modeli yer almaktadır. Ayrıca [nasıl toocreate bir Internet'e yönelik Yük Dengeleyici Klasik dağıtım kullanarak bilgi edinin](load-balancer-get-started-internet-classic-portal.md)

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

Bu hello bitti toobe toocreate bir yük dengeleyici ve ayrıntılı olarak tooaccomplish hello hedef yapıldığını açıklayan tek tek görev dizisi kapsar.

## <a name="what-is-required-toocreate-an-internet-facing-load-balancer"></a>Gerekli toocreate bir Internet'e yönelik Yük Dengeleyici nedir?

Nesneleri toodeploy bir yük dengeleyici aşağıdaki hello yapılandırmak ve toocreate gerekir.

* Ön uç IP yapılandırması: Gelen ağ trafiği için genel IP adreslerini içerir.
* Arka uç adres havuzu - hello yük dengeleyici gelen hello sanal makineleri tooreceive ağ trafiği için ağ arabirimlerine (NIC'ler) içerir.
* Yük Dengeleme kuralları - hello yük dengeleyici tooport hello arka uç adres havuzundaki ortak bir bağlantı noktası eşleme kurallarını içerir.
* Gelen NAT kuralları - noktasında hello yük dengeleyici tooa hello arka uç adres havuzundaki belirli bir sanal makine için genel bir bağlantı noktası eşleme kurallarını içerir.
* Yoklamaları - sistem durumu kullanılan araştırmalar toocheck kullanılabilirliği hello arka uç adres havuzundaki sanal makineler örnekleri içerir.

Azure Resource Manager içindeki yük dengeleyici bileşenleri hakkında daha fazla bilgi için bkz. [Azure Resource Manager Yük Dengeleyici desteği](load-balancer-arm.md).

## <a name="set-up-a-load-balancer-in-azure-portal"></a>Azure portalında yük dengeleyici kurma

> [!IMPORTANT]
> Bu örnekte **myVNet** adında bir sanal ağınız olduğu varsayılmaktadır. Çok başvuran[sanal ağ oluşturma](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) toodo bu. Ayrıca bir alt ağ içinde olduğunu varsayar **myVNet** adlı **LB alt olması** ve adlı iki VM **web1** ve **web2** sırasıyla içinde Merhaba aynı kullanılabilirlik kümesinde çağrılan **myAvailSet** içinde **myVNet**. Çok başvuran[bu bağlantıyı](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toocreate VM'ler.

1. Tarayıcıdan toohello Azure portalına gidin: [http://portal.azure.com](http://portal.azure.com) ve Azure hesabınızda oturum açın.
2. Merhaba üst sol tarafında Merhaba ekranında seçin **yeni** > **ağ** > **yük dengeleyici.**
3. Merhaba, **oluşturma yük dengeleyici** dikey penceresinde, yük dengeleyici için bir ad yazın. Burada **myLoadBalancer** kullanılmıştır.
4. **Tür** bölümünde **Genel**’i seçin.
5. **Genel IP adresi** bölümünde **myPublicIP** adında yeni bir genel IP oluşturun.
6. Kaynak Grubu altında **myRG**’yi seçin. Ardından uygun bir **Konum** seçin ve **Tamam**’a tıklayın. Merhaba yük dengeleyici toodeploy sonra başlar ve toosuccessfully tam dağıtım birkaç dakika sürer.

    ![Yük dengeleyicinin kaynak grubunu güncelleştirme](./media/load-balancer-get-started-internet-portal/1-load-balancer.png)

## <a name="create-a-back-end-address-pool"></a>Arka uç adres havuzu oluşturma

1. Başarıyla dağıtılan yük dengeleyicinizi kaynaklarınızdan seçin. Ayarlar’ın altında Arka Uç Havuzları’nı seçin. Arka uç havuzunuz için bir ad girin. Üzerinde hello ardından **Ekle** düğmesi görüntülenir hello dikey penceresinde hello üstündeki bulunun.
2. Tıklayın **bir sanal makine Ekle** hello içinde **arka uç havuzu ekleme** dikey.  **Kullanılabilirlik kümesi** bölümünde **Kullanılabilirlik kümesi seç**’e tıklayıp **myAvailSet**’i seçin. Ardından, **hello sanal makineleri seçin** altında sanal makineler bölümü hello dikey penceresinde hello ve tıklayın **web1** ve **web2**, Yük Dengeleme için oluşturulmuş iki VM hello. Hem mavi onay işaretleri toohello hello resimde gösterildiği gibi sol olduğundan emin olun. ' Ye tıklayın **seçin** tarafından Tamam hello ve ardından bu dikey penceresinde **seçin sanal makineleri** dikey ve ardından **Tamam** hello içinde **arka uç havuzu ekleme** Dikey.

    ![Toohello arka uç adres havuzu ekleme- ](./media/load-balancer-get-started-internet-portal/3-load-balancer-backend-02.png)

3. Toomake bildirimlerinizi bırakma listede aşağı doğru olduğundan emin olup bir güncelleştirme denetleyin hello yük dengeleyici arka uç havuzu ekleme tooupdating hello ağ arabiriminde kaydetme hem VM'ler hello için ilgili **web1** ve **web2**.

## <a name="create-a-probe-lb-rule-and-nat-rules"></a>Araştırma, LB kuralı ve NAT kuralları oluşturma

1. Durum araştırması oluşturun.

    Yük dengeleyicinizin Ayarlar sayfasında Araştırmalar’ı seçin. Ardından **Ekle** hello dikey penceresinde hello üstünde bulunur.

    Bir araştırma iki yolu tooconfigure vardır: HTTP veya TCP. Bu örnekte HTTP gösterilmektedir ancak TCP de benzer şekilde yapılandırılabilir.
    Merhaba gerekli bilgileri güncelleştirin. Daha önceden belirtildiği üzere **myLoadBalancer**, 80 numaralı bağlantı noktasına gelen trafik için yük dengeleme gerçekleştirir. Seçilen hello yolu HealthProbe.aspx aralığı 15 saniye ve sağlıksız durum eşiği. 2'dir. İşlemi tamamladıktan sonra tıklatın **Tamam** toocreate hello araştırma.

    'İ' hello simgesi toolearn tek tek Bu yapılandırmalar ve nasıl değiştirilen toocater tooyour gereksinimleri olabilir hakkında daha fazla üzerinde gezdirin.

    ![Araştırma ekleme](./media/load-balancer-get-started-internet-portal/4-load-balancer-probes.png)

2. Yük dengeleyici kuralı oluşturun.

    Yük Dengeleme kuralları hello de, yük dengeleyici ayarları bölümünde tıklayın. Merhaba yeni dikey penceresinde tıklayın **Ekle**. Kuralınıza bir ad verin. Burada HTTP kullanılmıştır. Merhaba ön uç bağlantı noktası ve arka uç bağlantı noktasını seçin. Burada ikisi için de 80 seçilmiştir. Seçin **LB arka uç** arka uç havuzu ve daha önce oluşturduğunuz hello olarak **HealthProbe** araştırma hello gibi. Diğer yapılandırmalar tooyour gereksinimlerine göre ayarlanabilir. Tamam toosave hello Yük Dengeleme kuralını'ye tıklayın.

    ![Yük dengeleme kuralı ekleme](./media/load-balancer-get-started-internet-portal/5-load-balancing-rules.png)

3. Gelen NAT kuralları oluşturma

    Gelen NAT kuralları, yük dengeleyicinin hello ayarları bölümünde'i tıklatın. ' I tıklatın, hello yeni dikey **Ekle**. Ardından gelen NAT kuralınıza bir ad verin. Burada **inboundNATrule1** kullanılmıştır. Merhaba hedef hello genel IP önceden oluşturulmuş olmalıdır. Özel hizmeti altında'i seçin ve toouse istediğiniz hello protokolü seçin. Burada TCP seçilmiştir. Hedef bağlantı noktası, bu durumda, 3389 hello ve 3441 Hello bağlantı noktası girin. ardından Tamam toosave bu kural'ı tıklatın.

    Merhaba ilk kural oluşturulduktan sonra bağlantı noktası 3442 tooTarget bağlantı noktasından 3389 inboundNATrule2 adlı hello ikinci gelen NAT kuralı için bu adımı yineleyin.

    ![Gelen NAT kuralı ekleme](./media/load-balancer-get-started-internet-portal/6-load-balancer-inbound-nat-rules.png)

## <a name="remove-a-load-balancer"></a>Yük Dengeleyici kaldırma

toodelete bir yük dengeleyici select hello yük dengeleyici tooremove istiyor. Merhaba, *yük dengeleyici* dikey penceresinde, tıklatın **silmek** hello dikey penceresinde hello üstünde bulunan. Ardından açılan istemde **Evet**’i seçin.

## <a name="next-steps"></a>Sonraki adımlar

[Bir iç yük dengeleyici yapılandırmaya başlayın](load-balancer-get-started-ilb-arm-cli.md)

[Yük dengeleyici dağıtım modu yapılandırma](load-balancer-distribution-mode.md)

[Yük dengeleyiciniz için boşta TCP zaman aşımı ayarlarını yapılandırma](load-balancer-tcp-idle-timeout.md)
