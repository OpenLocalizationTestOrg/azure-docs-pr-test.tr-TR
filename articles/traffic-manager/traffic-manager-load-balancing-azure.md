---
title: "Azure Hizmetleri aaaUsing Yük Dengelemesi | Microsoft Docs"
description: "Bu öğreticide, nasıl Azure yük dengeleyici Portföy hello toocreate kullanarak bir senaryo gösterilir: trafik Yöneticisi, uygulama ağ geçidi ve yük dengeleyici."
services: traffic-manager
documentationcenter: 
author: liumichelle
manager: vitinnan
editor: 
ms.assetid: f89be3be-a16f-4d47-bcae-db2ab72ade17
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/27/2016
ms.author: limichel
ms.openlocfilehash: d217047102d8c4828250dc0733e8ec9ee1e84b3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-load-balancing-services-in-azure"></a>Azure'da Yük Dengeleme Hizmetleri kullanma

## <a name="introduction"></a>Giriş

Microsoft Azure, birden çok ağ trafiğini nasıl dağıtıldığını yönetmek için hizmetleri ve Yük Dengeleme sağlar. Bu hizmetler ayrı ayrı kullanın veya kendi yöntemlerini gereksinimlerinize bağlı olarak, toobuild hello en iyi çözüm birleştirebilirsiniz.

Bu öğretici, biz öncelikle müşteri kullanım örneği tanımlayın ve Azure yük dengeleyici Portföy aşağıdaki hello kullanarak nasıl, daha sağlam hale getirilebilir ve kullanıcı görebilirsiniz: trafik Yöneticisi, uygulama ağ geçidi ve yük dengeleyici. Coğrafi olarak yedekli, trafik tooVMs dağıtır ve yardımcı olan bir dağıtım oluşturmak için adım adım yönergeler istekleri farklı türlerini yönetmek ardından sağlayın.

Kavramsal bir düzeyde, bu hizmetlerin her birini hello Yük Dengeleme hiyerarşi içinde farklı bir rol oynar.

* **Trafik Yöneticisi** Genel DNS Yük Dengeleme sağlar. Gelen DNS istekleri arar ve sağlıklı bir uç nokta ile yanıt verir, uygun şekilde hello yönlendirme ilkesi hello müşteri seçmiştir. Yönlendirme yöntemleri için Seçenekler şunlardır:
  * Performans yönlendirme toosend hello istek sahibi toohello yakın uç noktası bakımından gecikme süresi.
  * Diğer uç noktalar olarak yedekleme ile tüm trafik tooan endpoint toodirect yönlendirme önceliği.
  * Ağırlıklı yönlendirme, tooeach endpoint atanan hello ağırlıklı göre trafiği dağıtan hepsini.

  Merhaba istemci toothat uç noktası doğrudan bağlanır. Bir uç nokta sağlıksız olduğunu ve ardından yeniden yönlendirmeleri istemcileri tooanother sağlıklı örneği hello Azure trafik Yöneticisi algılar. Çok başvuran[Azure Traffic Manager belgeleri](traffic-manager-overview.md) toolearn hello hizmeti hakkında daha fazla.
* **Uygulama ağ geçidi** çeşitli katman 7 Yük Dengeleme özellikleri, uygulamanız için sunumu bir hizmet olarak uygulama teslim denetleyicisi (ADC) sağlar. CPU-yoğun SSL sonlandırma toohello uygulama ağ geçidi boşaltarak müşteriler toooptimize web grubu verimlilik sağlar. Diğer katman 7 Yönlendirme yetenekleri hepsini dağıtım gelen trafiği, tanımlama bilgisi tabanlı oturum benzeşimi, URL yolu tabanlı Yönlendirme ve hello özelliği toohost tek bir uygulama ağ geçidi arkasında birden çok Web siteleri içerir. Uygulama ağ geçidi, bir Internet'e dönük ağ geçidi, bir yalnızca iç ağ geçidi veya her ikisinin birleşimini yapılandırılabilir. Tam Azure uygulama ağ geçidi yönetilen, ölçeklenebilir ve yüksek oranda kullanılabilir. Daha iyi yönetilebilirlik için zengin tanılama ve günlüğe kaydetme özellikleri sağlar.
* **Yük Dengeleyici** hello Azure SDN yığını, yüksek performanslı, düşük gecikme süreli katman 4 Yük Dengeleme için Hizmetleri tüm UDP ve TCP protokollerini sağlama ayrılmaz bir parçasıdır. Gelen ve giden bağlantılara yönetir. Genel ve iç yük dengeli uç noktaları yapılandırabilir ve kuralları toomap tanımlamak gelen bağlantıları tooback uç havuzu hedefleri TCP ve HTTP sistem durumu yoklama seçenekleri toomanage hizmet kullanılabilirliği kullanarak.

## <a name="scenario"></a>Senaryo

Bu örnek senaryoda, içeriği iki tür hizmet veren basit bir Web sitesi kullanırız: görüntüleri ve dinamik olarak oluşturulan Web sayfaları. Merhaba Web sitesi coğrafi olarak yedekli olmalıdır ve hello en yakın (en düşük gecikme süresi), kullanıcılardan kullanılmalıdır konumu toothem. Merhaba uygulama geliştiricisi eşleşen herhangi bir URL deseni/görüntüleri/Merhaba, karar vermiştir * hello hello web grubu kalanından farklı olan VM'ler ayrılmış havuzundan sunulur.

Ek olarak, yüksek oranda kullanılabilirlik kümesi üzerinde barındırılan tootalk tooa arka uç veritabanı hello varsayılan VM havuzu hello dinamik içeriği sunması gerekir. Merhaba tüm dağıtım Azure Resource Manager aracılığıyla ayarlanır.

Trafik Yöneticisi, uygulama ağ geçidi ve yük dengeleyici kullanarak sağlayan bu Web sitesi tooachieve bu tasarım hedeflerini:

* **Birden çok coğrafi artıklık**: tek bir bölge devre dışı kalırsa, trafik Yöneticisi yollar toohello en yakın bölgeyi hello uygulama sahibi bir müdahalesi olmadan sorunsuz bir şekilde trafiği.
* **Gecikme süresi sınırlı**: olmadığından trafik Yöneticisi otomatik olarak hello müşteri toohello en yakın bölgeyi yönlendirir, hello Web sayfası içeriği isterken hello müşteri deneyimleri daha düşük gecikme süresi.
* **Bağımsız ölçeklenebilirlik**: hello web uygulaması iş yükü içerik türüne göre ayrılmış olduğundan, hello uygulama sahibi hello isteği iş yükleri birbirinden bağımsız ölçeklendirebilirsiniz. Uygulama ağ geçidi hello trafiği üzerinde belirtilen hello yönlendirilmiş toohello sağ havuzları olmasını sağlar kuralları ve hello durumunu Merhaba uygulaması.
* **İç Yük Dengeleme**: çünkü yük dengeleyici olduğundan hello yüksek oranda kullanılabilirlik kümesi önünde hello etkin ve Sağlıklı uç noktası bir veritabanı için sunulan toohello uygulama, yalnızca. Ayrıca, bir veritabanı yöneticisi hello iş yükü hello ön uç uygulamadan bağımsız hello küme üzerinde etkin ve etkin olmayan çoğaltmaları dağıtarak en iyi duruma getirebilirsiniz. Yük Dengeleyici bağlantıları toohello yüksek oranda kullanılabilirlik kümesi sunar ve yalnızca iyi veritabanları bağlantı isteklerini almak sağlar.

Merhaba Aşağıdaki diyagramda bu senaryonun hello mimarisi gösterilmektedir:

![Yük Dengeleme diyagramı mimarisi](./media/traffic-manager-load-balancing-azure/scenario-diagram.png)

> [!NOTE]
> Bu örnek yalnızca Azure sunar hello Yük Dengeleme Hizmetleri birçok olası yapılandırmaları biridir. Trafik Yöneticisi, uygulama ağ geçidi ve yük dengeleyici karışık ve eşleşen toobest, Yük Dengeleme gereksinimlerinize uygun şekilde ayarlayabilir. Örneğin, SSL boşaltma veya katman 7 işlem gerekli değil, uygulama ağ geçidi yerine yük dengeleyici kullanılabilir.

## <a name="setting-up-hello-load-balancing-stack"></a>Merhaba Yük Dengeleme yığını ayarlama

### <a name="step-1-create-a-traffic-manager-profile"></a>1. adım: bir Traffic Manager profilini oluşturma

1. Hello Azure portal'ı tıklatın **yeni**ve ardından arama hello Market "Trafik Yöneticisi profili."
2. Merhaba üzerinde **oluşturma trafik Yöneticisi profili** dikey penceresinde, aşağıdaki temel bilgilerle hello girin:

  * **Ad**: Traffic Manager profilinize bir DNS ön ek adı verin.
  * **Yönlendirme yöntemi**: Merhaba trafik yönlendirme yöntemini ilkesi seçin. Merhaba yöntemleri hakkında daha fazla bilgi için bkz: [hakkında Traffic Manager trafik yönlendirme yöntemleri](traffic-manager-routing-methods.md).
  * **Abonelik**: hello profil içeren hello abonelik seçin.
  * **Kaynak grubu**: hello profili içeriyor. Select hello kaynak grubu. Yeni veya var olan kaynak grubu olabilir.
  * **Kaynak grubu konumu**: trafik Yöneticisi hizmeti küreseldir ve belirli sınırlı değildir tooa konumudur. Ancak, hello trafik Yöneticisi profili ile ilişkilendirilmiş hello meta veri bulunduğu bir bölge hello grubu belirtmeniz gerekir. Bu konum hello çalışma zamanı kullanılabilirliğini hello profil üzerinde bir etkisi yoktur.

3. Tıklatın **oluşturma** toogenerate hello trafik Yöneticisi profili.

  !["Trafik Yöneticisi oluşturma" dikey penceresi](./media/traffic-manager-load-balancing-azure/s1-create-tm-blade.png)

### <a name="step-2-create-hello-application-gateways"></a>2. adım: uygulama ağ geçitleri hello oluşturma

1. Merhaba hello sol bölmede Azure portal'ı tıklatın **yeni** > **ağ** > **uygulama ağ geçidi**.
2. Merhaba uygulama ağ geçidi ile ilgili temel bilgileri aşağıdaki hello girin:

  * **Ad**: hello uygulama ağ geçidi hello adı.
  * **SKU boyutunu**: Merhaba boyutu hello uygulama ağ geçidi, küçük, Orta veya büyük kullanılabilir.
  * **Örnek sayısını**: hello örnek sayısı, 2 ile 10 arasında bir değer.
  * **Kaynak grubu**: hello uygulama ağ geçidi tutan hello kaynak grubu. Varolan bir kaynak grubu veya yeni bir tane olabilir.
  * **Konum**: hello bölge için aynı hello hello uygulama ağ geçidi, konumu hello kaynak grubu olarak. Başlangıç konumu önemlidir, hello sanal ağ ve genel IP hello olması gerektiğinden hello ağ geçidi ile aynı konumda.
3. **Tamam** düğmesine tıklayın.
4. Merhaba sanal ağ, alt ağ, ön uç IP ve hello uygulama ağ geçidi için dinleyici yapılandırmalarını tanımlayın. Bu senaryoda, hello ön uç IP adresidir **ortak**, böylece bunu bir uç nokta toohello trafik Yöneticisi profili daha sonra eklenen toobe.
5. Merhaba dinleyicisi seçenekleri aşağıdaki hello birini yapılandırın:
    * HTTP kullanırsanız, bir şey yok tooconfigure. **Tamam** düğmesine tıklayın.
    * Daha fazla HTTPS kullanırsanız, bu yapılandırma gereklidir. Çok başvuran[bir uygulama ağ geçidi oluşturma](../application-gateway/application-gateway-create-gateway-portal.md)başlayarak adım 9. Merhaba yapılandırmasını tamamladıktan sonra tıklatın **Tamam**.

#### <a name="configure-url-routing-for-application-gateways"></a>Uygulama ağ geçitleri için URL yönlendirmeyi yapılandırma

Bir arka uç havuzu seçtiğinizde, yol tabanlı bir kuralla yapılandırılmış bir uygulama ağ geçidi toplama tooround deneme dağıtımlarında hello istek URL'si bir yolu desenini alır. Bu senaryoda, bir kural yol tabanlı toodirect herhangi bir URL ile ekliyoruz "/images/\*" toohello görüntü sunucu havuzu. URL yapılandırma hakkında daha fazla bilgi için yol tabanlı bir uygulama ağ geçidi için yönlendirme başvurmak çok[bir uygulama ağ geçidi için bir yol tabanlı kural oluşturma](../application-gateway/application-gateway-create-url-route-portal.md).

![Uygulama ağ geçidi web katmanı diyagramı](./media/traffic-manager-load-balancing-azure/web-tier-diagram.png)

1. Kaynak grubundan hello önceki bölümde oluşturduğunuz hello uygulama ağ geçidi örneğini toohello gidin.
2. Altında **ayarları**seçin **arka uç havuzları**ve ardından **Ekle** tooadd hello VM'ler hello web katmanı arka uç havuzları ile tooassociate istiyor.
3. Merhaba üzerinde **arka uç havuzu ekleme** dikey penceresinde hello arka uç havuzu hello adı ve hello havuzunda bulunan hello makinelerin tüm hello IP adreslerini girin. Bu senaryoda, biz sanal makinelerin iki arka uç sunucu havuzu bağlanırsınız.

  ![Uygulama ağ geçidi "arka uç havuzu Ekle" dikey](./media/traffic-manager-load-balancing-azure/s2-appgw-add-bepool.png)

4. Altında **ayarları** hello uygulama ağ geçidi için seçin **kuralları**ve ardından hello **yol temelli** düğmesini tooadd bir kural.

  ![Uygulama ağ geçidi kuralları "Yoluna bağlı" düğmesi](./media/traffic-manager-load-balancing-azure/s2-appgw-add-pathrule.png)

5. Merhaba üzerinde **yol tabanlı Kuralı Ekle** dikey penceresinde, aşağıdaki bilgilerle hello sağlayarak hello kuralını yapılandırın.

   Temel ayarlar:

   + **Ad**: hello Portalı'nda erişilebilir olan hello kural hello kolay adı.
   + **Dinleyici**: hello kural için kullanılan hello dinleyicisi.
   + **Varsayılan arka uç havuzu**: hello varsayılan kuralı ile kullanılan arka uç havuzu toobe hello.
   + **Varsayılan HTTP ayarları**: hello HTTP ayarları toobe hello varsayılan kuralı ile kullanılır.

   Yol tabanlı kurallar:

   + **Ad**: hello yol tabanlı kural hello kolay adı.
   + **Yollar**: trafiği iletmek için kullanılan hello yol kuralı.
   + **Arka uç havuzu**: Bu kural ile kullanılan arka uç havuzu toobe hello.
   + **HTTP ayarı**: hello HTTP ayarları toobe bu kuralla kullanılır.

   > [!IMPORTANT]
   > Yollar: Geçerli yolları başlamalıdır "/". joker karakter hello "\*" Merhaba sonunda izin verilir. Geçerli örnekler /xyz, /xyz\*, veya /xyz/\*.

   ![Uygulama ağ geçidi "Yol tabanlı Kuralı Ekle" dikey penceresi](./media/traffic-manager-load-balancing-azure/s2-appgw-pathrule-blade.png)

### <a name="step-3-add-application-gateways-toohello-traffic-manager-endpoints"></a>3. adım: uygulama ağ geçitleri toohello trafik Yöneticisi uç noktaları ekleme

Bu senaryoda, trafik farklı bölgelerde bulunur (adımları önceki hello yapılandırıldığı gibi) bağlı tooapplication ağ geçitleri yöneticisidir. Merhaba uygulama ağ geçitleri yapılandırılır, hello sonraki tooconnect adımdır bunları tooyour trafik Yöneticisi profili.

1. Traffic Manager profilinizin açın. Bu nedenle, toodo ara kaynak grubunda veya hello trafik Yöneticisi profili hello adını arayın **tüm kaynakları**.
2. Merhaba sol bölmesinde seçin **uç noktaları**ve ardından **Ekle** tooadd bir uç nokta.

  ![Trafik Yöneticisi uç noktaları "Ekle" düğmesi](./media/traffic-manager-load-balancing-azure/s3-tm-add-endpoint.png)

3. Merhaba üzerinde **uç nokta ekleme** dikey penceresinde, aşağıdaki bilgilerle hello girerek bir uç nokta oluşturun:

  * **Tür**: uç nokta tooload dengele hello türünü seçin. Bu senaryoda seçin **Azure uç noktası** biz önceden yapılandırılmış toohello uygulama ağ geçidi örnekleri bağlandığınız için.
  * **Ad**: hello endpoint hello adını girin.
  * **Hedef kaynak türünün**: seçin **genel IP adresi** ve ardından, **hedef kaynak**, daha önce yapılandırılan hello uygulama ağ geçidinin genel IP hello seçin.

   ![Trafik Yöneticisi "uç nokta Ekle" dikey](./media/traffic-manager-load-balancing-azure/s3-tm-add-endpoint-blade.png)

4. Traffic Manager profilinizin DNS hello ile erişerek kurulumunuzu sınayabilirsiniz artık (Bu örnekte: TrafficManagerScenario.trafficmanager.net). İsteği yeniden gönderin, ortaya çıkarmak veya VM'ler ve farklı bölgelerde oluşturulan web sunucuları aşağı Getir ve hello trafik Yöneticisi profili ayarları tootest ayarlarınızı değiştirin.

### <a name="step-4-create-a-load-balancer"></a>4. adım: bir yük dengeleyici oluşturma

Bu senaryoda, yük dengeleyici hello web katmanı toohello veritabanları yüksek oranda kullanılabilirlik kümesi içinde bağlantılarından dağıtır.

Yüksek kullanılabilirlik veritabanı Kümenizin SQL Server AlwaysOn kullanıyorsanız, çok başvuran[bir veya daha fazla her zaman üzerinde kullanılabilirlik grubu dinleyicileri yapılandırma](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md) adım adım yönergeler için.

Bir iç yük dengeleyici yapılandırma hakkında daha fazla bilgi için bkz: [hello Azure portalında bir iç yük dengeleyici oluşturma](../load-balancer/load-balancer-get-started-ilb-arm-portal.md).

1. Merhaba hello sol bölmede Azure portal'ı tıklatın **yeni** > **ağ** > **yük dengeleyici**.
2. Merhaba üzerinde **oluşturma yük dengeleyici** dikey penceresinde, yük dengeleyici için bir ad seçin.
3. Set hello **türü** çok**iç**, hello uygun sanal ağ ve alt ağ hello yük dengeleyici tooreside için seçin.
4. Altında **IP adresi ataması**, şunlardan birini seçin **dinamik** veya **statik**.
5. Altında **kaynak grubu**, hello yük dengeleyici için hello kaynak grubunu seçin.
6. Altında **konumu**, hello hello yük dengeleyici için uygun bölgeyi seçin.
7. Tıklatın **oluşturma** toogenerate hello yük dengeleyici.

#### <a name="connect-a-back-end-database-tier-toohello-load-balancer"></a>Bir arka uç veritabanı katmanı toohello yük dengeleyici Bağlan

1. Kaynak grubundan hello önceki adımlarda oluşturduğunuz hello yük dengeleyici bulunamıyor.
2. Altında **ayarları**, tıklatın **arka uç havuzları**ve ardından **Ekle** tooadd bir arka uç havuzu.

  ![Yük Dengeleyici "arka uç havuzu Ekle" dikey](./media/traffic-manager-load-balancing-azure/s4-ilb-add-bepool.png)

3. Merhaba üzerinde **arka uç havuzu ekleme** dikey penceresinde hello hello arka uç havuzunun adını girin.
4. Makineleri tek tek veya bir kullanılabilirlik kümesi toohello arka uç havuzu ekleyin.

#### <a name="configure-a-probe"></a>Bir araştırma yapılandırmanız

1. İçinde yük dengeleyici altında **ayarları**seçin **yoklamaları**ve ardından **Ekle** tooadd bir araştırma.

 ![Yük Dengeleyici "Ekle araştırma" dikey penceresi](./media/traffic-manager-load-balancing-azure/s4-ilb-add-probe.png)

2. Merhaba üzerinde **Ekle araştırma** dikey penceresinde hello araştırma hello adını girin.
3. Select hello **Protokolü** hello araştırma için. Bir veritabanı için bir HTTP araştırmasını yerine bir TCP araştırması isteyebilirsiniz. Yük Dengeleyici araştırmalar hakkında daha fazla toolearn başvurmak çok[anlayın yük dengeleyici araştırmalar](../load-balancer/load-balancer-custom-probe-overview.md).
4. Merhaba girin **bağlantı noktası** hello araştırma erişmek için kullanılan, veritabanı toobe biri.
5. Altında **aralığı**, ne sıklıkta tooprobe hello uygulama belirtin.
6. Altında **sağlıksız durum eşiği**, hello arka uç VM toobe sağlıksız kabul için oluşması gereken sürekli araştırma hataları hello sayısını belirtin.
7. Tıklatın **Tamam** toocreate hello araştırma.

#### <a name="configure-hello-load-balancing-rules"></a>Merhaba Yük Dengeleme kurallarını yapılandırma

1. Altında **ayarları** , yük dengeleyici seçin **Yük Dengeleme kuralları**ve ardından **Ekle** toocreate bir kural.
2. Merhaba üzerinde **Ekle Yük Dengeleme kuralını** dikey penceresinde hello girin **adı** hello Yük Dengeleme kuralı için.
3. Merhaba seçin **ön uç IP adresi** Merhaba yük dengeleyici, **Protokolü**, ve **bağlantı noktası**.
4. Altında **arka uç bağlantı noktası**, başlangıç bağlantı noktası toobe hello arka uç havuzunda kullanılan belirtin.
5. Select hello **arka uç havuzu** ve hello **araştırma** hello önceki adımları tooapply hello kuralında için oluşturulmuş.
6. Altında **oturum kalıcılığını**, nasıl hello oturumları toopersist istediğinizi seçin.
7. Altında **boş durma zaman aşımlarını**, hello boşta kalma zaman aşımından önce dakika sayısını belirtin.
8. Altında **kayan IP**, şunlardan birini seçin **devre dışı** veya **etkin**.
9. Tıklatın **Tamam** toocreate hello kuralı.

### <a name="step-5-connect-web-tier-vms-toohello-load-balancer"></a>5. adım: web katmanı VM'ler toohello yük dengeleyici bağlanma

Şimdi biz web katmanı Vm'leriniz için herhangi bir veritabanı bağlantısı üzerinde çalışan hello uygulamalarda hello IP adresi ve yük dengeleyici ön uç bağlantı noktası yapılandırın. Bu sanal makineleri üzerinde çalışan belirli toohello uygulamaları yapılandırmadır. tooconfigure hello hedef IP adresi ve bağlantı noktası, toohello uygulamanızın belgelerine bakın. toofind hello hello Azure portal'ın hello ön uç IP adresi üzerinde hello toohello ön uç IP havuzu Git **yük dengeleyici ayarları** dikey.

![Yük Dengeleyici "Ön uç IP havuzu" Gezinti Bölmesi](./media/traffic-manager-load-balancing-azure/s5-ilb-frontend-ippool.png)

## <a name="next-steps"></a>Sonraki adımlar

* [Trafik Yöneticisi'nin genel bakış](traffic-manager-overview.md)
* [Uygulama ağ geçidi'ne genel bakış](../application-gateway/application-gateway-introduction.md)
* [Azure Load Balancer’a genel bakış](../load-balancer/load-balancer-overview.md)
