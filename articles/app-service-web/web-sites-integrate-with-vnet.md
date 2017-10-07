---
title: "aaaIntegrate bir Azure sanal ağı ile bir uygulama"
description: "Nasıl gösterir tooconnect Azure App Service tooa yeni veya var olan Azure sanal ağındaki bir uygulama"
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: cephalin
ms.assetid: 90bc6ec6-133d-4d87-a867-fcf77da75f5a
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: ccompy
ms.openlocfilehash: a93c504481400245b02220b541a008a7c874d10a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-app-with-an-azure-virtual-network"></a>Uygulamanızı Azure sanal ağı ile tümleştirme
Bu belge hello Azure App Service sanal ağ tümleştirme özelliğini açıklar ve gösterir nasıl tooset kendisiyle yukarı uygulamalarında [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714). Azure sanal ağlar (Vnet'ler) ile bilginiz yoksa, tooplace birçok Azure kaynaklarınızı denetim Internet olmayan routeable ağ erişimi sağlayan bir özellik budur. Bu ağlar sonra VPN teknolojileri çeşitli kullanan bağlı tooyour şirket içi ağlar olabilir. Azure sanal ağlar hakkında daha fazla toolearn burada hello bilgilerle Başlat: [Azure Virtual Network'e genel bakış][VNETOverview]. 

Hello Azure App Service, iki tür vardır. 

1. Fiyatlandırma planı hello tam kapsamlı destekleyen hello çok kiracılı sistemleri
2. Ağınızı dağıtır hello uygulama hizmeti ortamı (ana) premium özelliğini. 

Bu belge, VNet tümleştirme ve uygulama hizmeti ortamı gider. Merhaba ana özelliği hakkında daha fazla toolearn istiyorsanız, burada hello bilgilerle Başlat: [uygulama hizmeti ortamı giriş][ASEintro].

VNet tümleştirme, sanal ağınızda bulunan web uygulama erişim tooresources sağlar ancak özel erişim tooyour web uygulaması hello sanal ağdan vermez. Özel site erişimi toomaking uygulamanızı özel ağdan gibi bir Azure sanal ağı içinde yalnızca erişilebilir başvuruyor. Özel site yalnızca bir dahili yük dengeleyici (ILB) ile yapılandırılmış bir ana ile erişilebilir. Bir ILB ana kullanılması hakkında daha fazla ayrıntı için buraya hello makale ile başlayın: [oluşturma ve bir ILB ana kullanarak][ILBASE]. 

VNet tümleştirme nerede kullanacağınız yaygın bir senaryo, web uygulama tooa veritabanından veya Azure sanal ağınızda bir sanal makinede çalışan bir web hizmetine erişim etkinleştiriliyor. VNet Tümleştirmesi ile tooexpose genel bir uç nokta uygulamalar için VM gerek yoktur ancak hello özel dışındaki Internet yönlendirilebilir adresler yerine kullanabilirsiniz. 

Merhaba VNet tümleştirme özelliği:

* Standart, Premium ya da planı fiyatlandırma Isolated gerektirir 
* Klasik veya Resource Manager Vnet'i ile çalışır 
* TCP ve UDP destekler
* Web, mobil ve API apps ile çalışır
* bir uygulama tooconnect tooonly 1 etkinleştirir birer birer VNet
* bir uygulama hizmeti planı'nda sanal ağlar toobe ile tümleşik toofive sağlar 
* bir uygulama hizmeti planında birden çok uygulama aynı VNet toobe kullandığı hello sağlar
* % 99,9 SLA toohello SLA son hello VNet ağ geçidi üzerinde destekler

VNet tümleştirme de dahil olmak üzere desteklemiyor bazı şeyler vardır:

* bir sürücü bağlama
* AD tümleştirmesi 
* NetBIOS
* Özel site erişimi

### <a name="getting-started"></a>Başlarken
İşte bazı şeyleri tookeep göz önünde web uygulama tooa sanal ağınıza bağlanmadan önce:

* VNet tümleştirme yalnızca çalışır uygulamaları ile bir **standart**, **Premium**, veya **Isolated** planı fiyatlandırma. Merhaba özelliğini etkinleştirir ve desteklenmeyen, uygulama hizmeti planı tooan ölçeklendirme planı fiyatlandırma uygulamalarınızı kendi kullandıkları sanal ağlara bağlantılar toohello kaybedersiniz. 
* Hedef sanal ağınız zaten varsa, noktadan siteye VPN bağlı tooan uygulama kullanılabilmesi için öncelikle bir dinamik yönlendirme ağ geçidi ile etkin olması gerekir. Ağ geçidi, statik yönlendirme ile yapılandırılmışsa, noktadan siteye sanal özel ağ (VPN) etkinleştiremezsiniz.
* Merhaba VNet hello olmalıdır, App Service Plan(ASP) aynı abonelik. 
* bir VNet ile tümleştirmek hello uygulamaları hello bu sanal ağ için belirtilen DNS kullanın.
* Varsayılan olarak tümleştirme uygulamalarınızı trafiği, sanal ağınızda tanımlanan hello yollar göre sanal ağınızı içine yalnızca rota. 

## <a name="enabling-vnet-integration"></a>VNet Integration etkinleştirme
Bu belge hello Azure portalında VNet tümleştirmesi için öncelikle kullanılarak odaklanmıştır. PowerShell kullanarak uygulamanızı ile VNet tümleştirme tooenable burada hello yönergeleri izleyin: [PowerShell kullanarak uygulama tooyour sanal ağınıza bağlamak][IntPowershell].

Uygulama tooa yeni veya var olan sanal ağınızı hello seçeneği tooconnect var. Yeni bir ağ tümleştirmenize bir parçası olarak oluşturursanız, ardından ayrıca toojust oluşturmaya izin ver hello VNet, dinamik yönlendirme ağ geçidi sizin için önceden yapılandırılmıştır ve noktası tooSite VPN etkindir. 

> [!NOTE]
> Yeni bir sanal ağ tümleştirme yapılandırması birkaç dakika sürebilir. 
> 
> 

tooenable VNet tümleştirmesi, uygulamanızın ayarlarını açın ve ardından ağ seçin. Merhaba açılan UI üç ağ seçenek sunar. Bu kılavuz yalnızca VNet tümleştirmeye ancak karma bağlantılar geçiyor ve App Service ortamları bu belgenin sonraki bölümlerinde ele alınmaktadır. 

Uygulamanızı hello planı fiyatlandırma doğru değilse, hello UI tooscale daha yüksek tercih ettiğiniz planı fiyatlandırma, planı tooa sağlar.

![][1]

### <a name="enabling-vnet-integration-with-a-pre-existing-vnet"></a>Önceden var olan bir VNet ile VNet tümleştirme etkinleştirme
Merhaba VNet tümleştirme UI, sanal ağlar listesinden tooselect sağlar. Merhaba Klasik sanal ağlar sonraki toohello VNet adı parantez belirtmek gibi "Klasik" Merhaba kelimesiyle olmalarını. Merhaba Resource Manager sanal ağlar ilk listelenen şekilde hello liste sıralanır. Hello aşağıda gösterilen görüntü yalnızca bir VNet seçilebilir görebilirsiniz. Bir sanal ağ dahil olmak üzere çıkışı gri olduğunu birden çok nedeni vardır:

* hesabınıza erişimi olan başka bir abonelik Hello VNet yer
* Merhaba VNet noktası etkin tooSite yok
* Merhaba VNet dinamik yönlendirme ağ geçidi yok

![][2]

tooenable tümleştirme tıklamanız yeterlidir hello toointegrate ile istediğiniz VNet üzerinde. Merhaba VNet seçtikten sonra uygulamanızı hello değişiklikleri tootake efekti için otomatik olarak yeniden başlatılır. 

##### <a name="enable-point-toosite-in-a-classic-vnet"></a>Klasik sanal ağda noktası tooSite etkinleştir
Ardından sanal ağınızın ağ geçidi yok ya da noktası tooSite sahip değilse, bu yukarı ilk tooset sahip. Bu klasik bir VNet için toodo Git toohello [Azure portal] [ AzurePortal] ve sanal Networks(classic) hello listesi ayarlamak duruma getirin. Buradan, toointegrate ile istediğiniz ve VPN bağlantıları adlı Essentials altındaki hello büyük kutuya tıklayın hello Ağ'ı tıklatın. Buradan, noktası toosite VPN oluşturun ve ağ geçidi oluşturmak bile sahip. Ağ geçidi oluşturma deneyim hello noktası toosite aracılığıyla Git sonra hazır hale gelmeden önce yaklaşık 30 dakika olur. 

![][8]

##### <a name="enabling-point-toosite-in-a-resource-manager-vnet"></a>Resource Manager Vnet'i içinde noktası tooSite etkinleştirme
Resource Manager Vnet'i bir ağ geçidi ve noktası tooSite tooconfigure kullanabilirsiniz ya da PowerShell belirtildiği gibi burada [PowerShell kullanarak bir noktadan siteye bağlantı tooa sanal ağ yapılandırma] [ V2VNETP2S] veya burada açıklandığı gibi hello Azure portal kullanın [hello Azure portal yapılandırma bir noktası siteye bağlantı tooa VNet kullanarak][V2VNETPortal]. Merhaba UI tooperform bu özelliği henüz kullanılamıyor. Başlangıç noktası tooSite yapılandırmasını toocreate sertifikaları gerektiğini unutmayın. WebApp toohello VNet bağlandığında otomatik olarak yapılandırılır. 

### <a name="creating-a-pre-configured-vnet"></a>Önceden yapılandırılmış bir sanal ağ oluşturma
Merhaba uygulama kullanıcı Arabirimi ağ hizmeti sahipse hello yetenek toodo toocreate bir ağ geçidi ve noktadan siteye ile yapılandırılmış yeni bir VNet o'i ancak yalnızca Resource Manager Vnet'i için istiyorsanız. Bir ağ geçidi ile klasik VNet ve noktadan siteye toocreate istiyorsanız, daha sonra toodo bu el ile Merhaba ağ kullanıcı arabirimi aracılığıyla gerekir. 

Resource Manager Vnet'i hello VNet tümleştirme UI aracılığıyla toocreate seçmeniz yeterlidir **yeni sanal ağ oluştur** ve sağlar:

* Sanal ağ adı
* Sanal ağ adres bloğu
* Alt ağ adı
* Alt ağ adres bloğu
* Ağ geçidi adres bloğu
* Noktadan siteye adres bloğu

Bu VNet tooconnect tooany diğer ağlara istiyorsanız, bu ağ ile çakışıyor IP adresi alanı çekme kaçınmanız gerekir. 

> [!NOTE]
> Bir ağ geçidi ile Resource Manager Vnet'i oluşturulması yaklaşık 30 dakika sürer ve şu anda hello VNet uygulamanızla tümleştirin değil. Sanal ağınızı hello ağ geçidiyle oluşturulduktan sonra toocome geri tooyour uygulama VNet tümleştirme UI gerekir ve yeni sanal ağınızı seçin.
> 
> 

![][3]

Azure sanal özel ağ adresleri içinde normal olarak oluşturulur. Varsayılan hello tarafından VNet tümleştirme özelliği bu IP adresi aralıklarını sanal ağınızı hedefleyen trafik yönlendirir. Merhaba özel IP adres aralıklarını şunlardır:

* -Bu olduğu hello aynı 10.0.0.0 - 10.0.0.0/8 10.255.255.255
* -Bu olduğu hello aynı 172.16.0.0 - 172.16.0.0/12 172.31.255.255 
* -Bu olduğu hello aynı 192.168.0.0 - 192.168.0.0/16 192.168.255.255

Merhaba VNet adres alanı CIDR gösteriminde belirtilen toobe gerekir. İle CIDR gösteriminde bilginiz yoksa, bu adres blokları IP adresi ve hello ağ maskesi temsil eden bir tamsayı kullanarak belirtmek için bir yöntemdir. Hızlı başvuru olarak 10.1.0.0/24 256 adresleri olacaktır ve 10.1.0.0/25 128 adresleri olacağını göz önünde bulundurun. Bir /32 bir IPv4 adresiyle yalnızca 1 adresi olacaktır. 

Merhaba DNS sunucusu bilgileri burada ayarlarsanız, ağınız için ayarlanır. VNet oluşturulduktan sonra bu bilgileri hello VNet kullanıcı deneyimleri düzenleyebilirsiniz. Merhaba hello VNet DNS değiştirirseniz, tooperform eşitleme ağ işlemi gerekir.

Merhaba VNet tümleştirme UI kullanarak klasik bir VNet oluşturduğunuzda, hello bir sanal ağ oluşturur, uygulamanızın aynı kaynak grubunda. 

## <a name="how-hello-system-works"></a>Merhaba sistem nasıl çalışır?
Merhaba perde arkasında bu özellik, uygulama tooyour VNet üzerinde noktadan siteye VPN teknolojisi tooconnect oluşturur. Azure uygulama hizmetinde uygulamaları bir uygulamada doğrudan bir sanal ağ sanal makinelerle gerçekleştirilir gibi sağlama önleyen bir çok kiracılı sistem mimarisi vardır. Noktadan siteye teknolojisine oluşturarak, biz ağ erişim toojust hello sanal makine hello uygulama barındırma sınırlayın. Uygulamalarınızı tooaccess yapılandırmadan hello ağlar yalnızca erişebilmesi için erişim toohello ağ bu uygulama konaklarda daha sınırlıdır. 

![][4]

Bir DNS sunucusu ile sanal ağınızı yapılandırmadıysanız, uygulamanızın toouse IP adreslerini tooreach kaynak hello VNet gerekir. IP adresleri kullanırken, bu özelliğin hello ana avantajı toouse hello özel adresler özel ağınızdaki sağlar, olduğunu unutmayın. Merhaba VNet tümleştirme özelliği kullanmadığınız ve üzerinden iletişim kuran uygulamanızı toouse genel IP adresleri, VM'lerin biri için ayarlarsanız Internet hello.

## <a name="managing-hello-vnet-integrations"></a>Merhaba VNet tümleştirmeler yönetme
özelliği tooconnect hello ve tooa VNet bir uygulama düzeyinde bulunur bağlantısını kesin. Birden çok uygulama arasında VNet tümleştirme hello etkileyebilecek bir ASP düzeyinde işlemleridir. Merhaba hello uygulama düzeyinde gösterilen UI sanal ağınızda ayrıntılarını alabilirsiniz. Aynı bilgiler de ASP hello düzeyi görüntülenir hello çoğunu. 

![][5]

Merhaba ağ özellik durumu sayfasından uygulamanızı bağlı tooyour VNet olup olmadığını görebilirsiniz. Sanal ağ geçidiniz için herhangi bir nedenle çalışmıyorsa, ardından bu değil bağlı olarak gösterir. 

Düzey VNet tümleştirme UI hello uygulamasında artık kullanılabilir tooyou sahip hello bilgileri hello aynı olarak hello ayrıntı bilgileri ASP hello alınamadı. Bu öğeler şunlardır:

* Sanal ağ adı - bu bağlantıyı hello Azure sanal ağı kullanıcı arabirimini açar
* Konumu - bu ağınızı hello konumunu yansıtır. Başka bir konumda bir VNet ile olası toointegrate olur.
* Sertifika durumu - hello uygulama ve hello VNet arasında kullanılan sertifikalar toosecure hello VPN bağlantısı vardır. Bu eşitlenmiş bir test tooensure yansıtır.
* Ağ geçidi durumu - geçitlerinizin aşağı herhangi bir nedenle olmalıdır ardından uygulamanızı hello VNet kaynaklarında erişemiyor. 
* VNet adres alanı - Vnet'inizi için başlangıç IP adresi alanını budur. 
* Noktası tooSite adres alanı - hello noktası toosite IP adres alanı sanal ağınızı budur. Uygulamanızı hello bu adres alanındaki IP birinden gelen olarak iletişimi gösterir. 
* Site toosite adres alanı - Site tooSite VPN'ler tooconnect kullanabilir, VNet tooyour kaynakları veya tooother VNet şirket. VPN bağlantısı burada gösterir hello IP aralıkları ile tanımlanmış sonra yapılandırılmış olması gerekir.
* DNS sunucuları - burada listelenen sonra VNet ile yapılandırılmış DNS sunucuları varsa.
* Toohello VNet IP'leri yönlendirilen - Vnet'inizi için tanımlanan yönlendirme olan IP adresleri listesi vardır ve bu adresleri burada gösterilecek. 

Merhaba uygulama, sanal ağ tümleştirmesinin görünümünde sürebilir hello yalnızca uygulamanızdan hello için şu anda bağlı VNet toodisconnect işlemdir. toodo, bu yalnızca tıklatın'hello üstünde bağlantısını kesin. Bu eylem, sanal ağınızı değiştirmez. Merhaba VNet ve hello ağ geçitleri de dahil olmak üzere yapılandırmasıyla değişmeden kalır. Sanal ağınızı sonra toodelete istiyorsanız toofirst delete hello kaynaklar hello ağ geçitleri de dahil olmak üzere gerekir. 

Merhaba App Service planı görünümü birkaç ek işlem vardır. Bu aynı zamanda farklı daha hello uygulamadan erişilebilir. tooreach hello ASP ağ UI açmanız yeterlidir ASP UI ve aşağı kaydırın. Ağ özellik durumu adlı bir kullanıcı Arabirimi öğesi yok. VNet tümleştirme geçici küçük bazı ayrıntılar sağlar. Bu kullanıcı Arabirimi üzerindeki tıklatılması hello ağ özellik durumu kullanıcı arabirimini açar. Ardından tıklatırsanız hello VNet tümleştirmeler bu ASP açılır listeleri UI hello üzerinde "Buraya toomanage tıklayın".

![][6]

Merhaba hello ASP iyi tooremember hello sanal ağlar ile tümleştirme hello konumlarını bakıldığında konumudur. Merhaba VNet başka bir konumda olduğunda, daha büyük bir olasılıkla toosee gecikme sorunlardır. 

Merhaba sanal ağlar ile tümleşik uygulamalarınızı ile bu ASP ve kaç tane sağlayabilirsiniz tümleşik olduğu bir anımsatıcı kaç tane sanal ağlar üzerinde değil. 

toosee ayrıntıları hello ilgilendiğiniz VNet yalnızca tıklayarak her VNet üzerinde eklendi. Ayrıca daha önce not ettiğiniz toohello ayrıntıları Merhaba, VNet kullanarak bu ASP uygulamalarında listesini de görebilirsiniz. 

İle saygı var. tooactions iki birincil eylemlerdir. Merhaba önce Vnet'inizi uygulamanızı trafiğe sürücü hello özelliği tooadd yollar olur. Merhaba ikinci hello özelliği toosync sertifikaları ve ağ bilgilerini eylemdir.

![][7]

**Yönlendirme** ne ağınızı uygulamanızdan içine trafiği yönlendirerek için kullanılır, sanal ağınızda tanımlanan hello yollar daha önce belirtildiği gibi. Bu özellik müşterilerin toosend ek giden trafik bir uygulamadan hello VNet içine ve bunlar için istediğiniz yere sağlanır ancak bazı kullanımları vardır. Toohello trafiği neler toohow hello müşteri tamamlandıktan sonra kendi sanal yapılandırır. 

**Sertifikaları** hello sertifika durumu hello VPN bağlantısı için kullanıyoruz hello sertifikaları iyi uygulama hizmeti toovalidate hello tarafından gerçekleştirilen bir onay yansıtır. VNet tümleştirme etkinleştirildiğinde, ardından bu hello bu ASP tüm uygulamalardan ilk VNet tümleştirme toothat ise yoktur sertifikaları tooensure hello güvenlik hello bağlantının gerekli exchange. Merhaba sertifikaları birlikte hello DNS yapılandırmasını, yollar ve hello ağ açıklayan benzer başka şeyler alın.
Bu sertifikalar veya ağ bilgileri değiştiyse, tooclick "Eşitleme ağ" gerekir. **Not**: kısa bir kesinti uygulamanızı ve ağınızı arasında Bağlantısı'nda neden "Eşitleme ağ" tıklattığınızda. Uygulamanızı yeniden başlatılmamış olsa da, bağlantı kaybı hello site toonot işlevinizi düzgün neden olabilir. 

## <a name="accessing-on-premises-resources"></a>Erişme şirket içi kaynakları
Merhaba VNet tümleştirme özelliği hello yararları ağınızı bağlıysa tooyour ağ sitesi tooSite VPN ile uygulamalarınızı uygulamanızı tooyour şirket kaynaklarına erişim sağlayabilirsiniz sonra şirket içi olduğunu biridir. Tooupdate ihtiyacınız ancak bu toowork için şirket içi VPN ağ geçidinizi hello ile noktası tooSite IP aralığınızı için yönlendirir. Merhaba betikleri tooconfigure kullanılan sonra hello Site tooSite VPN ilk ayarlandığında noktası tooSite VPN dahil olmak üzere rotalar ayarlamanız gerekir. Site tooSite VPN oluşturduktan sonra başlangıç noktası tooSite VPN eklerseniz, ardından, tooupdate hello yollar el ile yapmanız gerekir. Ağ geçidi değişir ve olmayan toodo nasıl burada açıklanan ayrıntılar. 

> [!NOTE]
> Merhaba VNet tümleştirme özelliği, bir ExpressRoute ağ geçidi sahip bir VNet ile birlikte bir uygulamayı tümleştirin değil. Merhaba ExpressRoute ağ geçidi olarak yapılandırılmış olsa bile [bir arada bulunma modu] [ VPNERCoex] hello VNet tümleştirme çalışmaz. ExpressRoute bağlantısı üzerinden tooaccess kaynaklarına gereksinim sonra kullanabileceğiniz bir [uygulama hizmeti ortamı][ASE], sanal ağınızda çalışır.
> 
> 

## <a name="pricing-details"></a>Fiyatlandırma ayrıntıları
Birkaç vardır hello VNet tümleştirme özelliği kullanırken bilmeniz gereken nüanslarını fiyatlandırma. Bu özelliğin kullanımının toohello 3 ilgili ücretleri vardır:

* ASP fiyatlandırma katmanı gereksinimleri
* Veri aktarım maliyetleri
* VPN ağ geçidi maliyetleri.

Bu özellik, uygulamalar, toobe mümkün toouse için ihtiyaç toobe standart veya Premium App Service planı. Burada bu maliyetlerini hakkında daha fazla ayrıntı görebilirsiniz: [App Service fiyatlandırması][ASPricing]. 

Merhaba VNet olsa bile, VNet tümleştirme bağlantısı üzerinden giden veri aynı hello toohello şekilde noktası VPN'ler işlenir tooSite, her zaman bir ücret sahip olduğunuz veri merkezi. toosee bu giderleri nelerdir, burada göz: [veri aktarım fiyatlandırma ayrıntıları][DataPricing]. 

Merhaba son öğeyi hello VNet ağ geçitleri hello maliyetidir. Site tooSite VPN gibi başka bir şey için hello ağ geçitleri gerek duymuyorsanız, ağ geçitleri toosupport hello VNet tümleştirme özelliği için ödeme yapıyorsanız. Burada bu maliyetlerinde ayrıntıları vardır: [VPN ağ geçidi fiyatlandırma][VNETPricing]. 

## <a name="troubleshooting"></a>Sorun giderme
Merhaba özelliği yukarı kolay tooset olsa da, deneyiminizi sorun boş olacaktır anlamına gelmez. Karşılaşmamanız gerekir istenen uç noktanızı var. erişme tootest bağlantı hello uygulama konsolundan kullanabileceğiniz bazı yardımcı programları sorunlardır. Kullanabileceğiniz iki konsol deneyimleri vardır. Merhaba Kudu konsolundan biridir ve hello diğer hello Azure portal ulaşabileceği hello konsoludur. Uygulamanızı tooget toohello Kudu konsolundan Git tooTools Kudu ->. Bu olduğu hello aynı çok giderek olarak [sitename]. scm.azurewebsites.net. Bu açılır yalnızca Git toohello hata ayıklama konsolunu sekmesini tooget toohello Azure portal barındırılan konsolunda ardından uygulamanızı Git sonra tooTools Konsolu ->. 

#### <a name="tools"></a>Araçlar
Merhaba araçları ping, nslookup ve tracert toosecurity kısıtlamaları nedeniyle hello konsolu üzerinden çalışmaz. toofill hello void eklenen iki ayrı araçları olmuştur. Sipariş tootest DNS işlevindeki nameresolver.exe adında bir aracı eklendi. Merhaba sözdizimi aşağıdaki gibidir:

    nameresolver.exe hostname [optional: DNS Server]

Uygulamanızı bağımlı nameresolver toocheck hello ana bilgisayar adlarını kullanabilirsiniz. Bu şekilde, DNS ile yanlış yapılandırılmış herhangi bir şey varsa veya belki de erişim tooyour DNS sunucusu yok test edebilirsiniz.

Merhaba sonraki aracı TCP bağlantısı tooa ana bilgisayarı ve bağlantı noktası bileşimi için tootest sağlar. Bu araç tcpping.exe olarak adlandırılır ve hello sözdizimi aşağıdaki gibidir:

    tcpping.exe hostname [optional: port]

Merhaba tcpping yardımcı programı belirli ana bilgisayarı ve bağlantı noktası ulaşmak varsa söyler. Yalnızca başarı gösterebilir varsa: hello ana bilgisayarı ve bağlantı noktası bileşimi dinleyen bir uygulamanın yoktur ve ağ erişimi uygulama toohello belirtilen ana bilgisayar ve bağlantı noktası yok.

#### <a name="debugging-access-toovnet-hosted-resources"></a>Barındırılan kaynaklara erişim tooVNet hata ayıklama
Uygulamanızı belirli bir ana bilgisayarı ve bağlantı noktası ulaşmasını engellemeniz şey vardır. Başlangıç zamanının çoğunu üç şey biridir:

* **Hello bir güvenlik duvarı olduğu şekilde** hello şekilde bir güvenlik duvarınız varsa, hello TCP zaman aşımı karşılaşır. 21 saniye bu durumda olur. Merhaba tcpping aracı tootest bağlantısı kullanın. TCP zaman aşımı, güvenlik duvarları ötesinde toomany şeyler nedeniyle olabilir ancak var. Başlat. 
* **DNS erişilebilir değil** hello DNS zaman aşımı olan üç saniyede bir DNS sunucusu. İki DNS sunucusu varsa, hello zaman aşımı 6 saniyedir. DNS çalışıyorsanız nameresolver toosee kullanın. Merhaba, VNet ile yapılandırılmış DNS kullanmaz nslookup kullanamazsınız unutmayın.
* **Geçersiz P2S IP aralığı** hello noktası toosite IP aralığı hello RFC 1918 özel IP aralıkları toobe gerekir (10.0.0.0-10.255.255.255 / 172.16.0.0-172.31.255.255 / 192.168.0.0-192.168.255.255). Merhaba aralık dışında IP'leri kullanıyorsa şeyler çalışmaz. 

Bu öğeleri sorununuzu alamıyorsanız, gibi basit şeyleri hello için ilk bakış: 

* Ağ geçidi Hello hello Portalı'nda yukarı olduğu gösteriyor mu?
* Sertifikaları eşit olacak şekilde gösteriyor?
* Bir "eşitleme ağında" Merhaba etkilenen ASP yapmadan herkes hello ağ yapılandırmasını değiştirmek mi? 

Ağ geçidi kapalı ise, getirmeniz yedekleyin. Sertifikalarınızı eşitlenmemiş varsa, VNet tümleştirme toohello ASP görünümünü gidin ve "Eşitleme ağ" isabet. İle yapılan değişiklik tooyour VNet yapılandırmasını olmuştur ve eşitleme değildi şüpheleniyorsanız olur, ASP sonra VNet tümleştirme toohello ASP görünümünü gidin ve "Eşitleme ağ" sadece bir anımsatıcı olarak isabet, bu kısa bir kesinti VNet bağlantınızı ve uygulamalarınızı neden olur . 

Ardından, tüm ise sorun, biraz daha derin toodig gerekir:

* Olan var. VNet tümleştirme tooreach kaynaklarında kullanan diğer uygulamalar hello aynı Vnet'i? 
* Toohello uygulama Konsolu gidin ve tcpping tooreach, sanal ağınızda herhangi diğer kaynakları kullanılsın mı? 

Merhaba yukarıdaki biri doğruysa, VNet tümleştirme sorun yoktur ve hello başka bir yere sorunudur. Ana bilgisayar: bağlantı noktası neden ulaşamıyor hiçbir basit yol toosee olduğundan burada toobe daha zor alır budur. Merhaba nedenler bazıları şunlardır:

* bir güvenlik duvarı erişim toohello uygulama bağlantı noktası toosite IP aralığınızı noktasından önleme, ana bilgisayarda çalışır duruma getirdikten. Çapraz alt ağlar genellikle ortak erişim gerektirir.
* Hedef ana bilgisayar kullanılamıyor
* Uygulamanızı çalışmıyor
* ana bilgisayar adı veya hello yanlış IP vardı
* Uygulamanızı beklediğiniz daha farklı bir bağlantı noktasında dinliyor. Bunu barındıran olma ve "netstat - aon" kullanma başlangıç cmd isteminden denetleyebilirsiniz. Bu kimliği hangi bağlantı noktası üzerinde dinleme hangi işlemin gösterir. 
* Ağ güvenlik grupları bunlar erişim tooyour uygulama ana bilgisayarı ve bağlantı noktası toosite IP aralığınızı noktasından engeller şekilde yapılandırılır

Merhaba tüm aralığından tooallow erişmeniz gerekir böylece uygulamanız kullanacağı noktası tooSite IP aralığınızı içinde hangi IP bilmiyorsanız unutmayın. 

Ek hata ayıklama adımları içerir:

* başka bir VM, VNet ve girişimi tooreach, kaynak konak: bağlantı noktası buradan oturum açın. Bazı TCP ping yardımcı programları vardır bu amaçla kullanabileceğiniz veya telnet değilse bile kullanabilirsiniz olması gerekir. Bu bir sanal makineden bağlantısı varsa hello burada yalnızca toodetermine amaçtır. 
* bir uygulamayı başka bir VM getirecek ve erişim toothat ana bilgisayarı ve bağlantı noktası uygulamanızdan hello konsolundan test

#### <a name="on-premises-resources"></a>Şirket içi kaynakları ####
Uygulamanızı kaynakları şirket erişemiyorsa, hello ilk şey denetlemeniz gerekir, sanal ağınızda ulaşabileceği bir kaynak olur. Çalışan tooreach VM hello VNet ile şirket içi uygulamadan hello deneyin. Telnet veya TCP ping yardımcı programını kullanabilirsiniz. VM, şirket içi kaynağa bağlanamazsa, Site tooSite VPN bağlantınızın çalıştığından emin olun. Çalışıyorsa, aynı şeyleri hello şirket içi ağ geçidi yapılandırma ve durum yanı sıra daha önce not ettiğiniz hello denetleyin. 

Şimdi sanal ağınızı barındırılıyorsa VM şirket içi sisteminizi ulaşabilir ancak hello neden hello aşağıdaki olabilir sonra uygulamanızı olamaz:

* Şirket içi ağ geçidiniz, noktası toosite IP aralıklarıyla yollarınızı yapılandırılmamış
* Ağ güvenlik grupları noktası tooSite IP aralığınızı erişimi engelliyor
* Şirket içi güvenlik duvarlarında noktası tooSite IP aralığınızı gelen trafiği engelleme
* Şirket içi ağınıza ulaşmasını noktası tabanlı tooSite trafiğinizi önler ağınızı kullanıcı tanımlı bir Route(UDR) var

## <a name="hybrid-connections-and-app-service-environments"></a>Karma bağlantılar ve uygulama hizmeti ortamları
Barındırılan tooVNet kaynaklarına erişim sağlayan üç özellikler vardır. Bunlar:

* VNet tümleştirme
* Karma Bağlantılar
* App Service ortamları

Karma bağlantılar tooinstall hello karma bağlantı Manager(HCM) ağınızdaki adlı bir geçiş aracısı gerektirir. Merhaba HCM toobe mümkün tooconnect tooAzure ve ayrıca tooyour uygulama gerekir. Bu şirket içi ağınız gibi uzak bir ağdan özellikle harika bir çözümdür veya bir internet erişilebilir uç nokta gerektirmediğinden bile başka bir bulut ağ barındırılabilir. Merhaba HCM yalnızca Windows üzerinde çalışır ve tooprovide yüksek kullanılabilirlik çalıştıran toofive örneği olabilir. Karma bağlantılar yalnızca destekler TCP ancak ve her HC bitiş toomatch tooa belirli ana bilgisayar: bağlantı noktası bileşimi yoktur. 

Merhaba uygulama hizmeti ortamı özelliği, sanal ağınızda toorun hello Azure App Service örneği sağlar. Bu uygulamalar erişim kaynaklarınızı ağınızı ek adımlar olmadan sağlar. Bazı too14 GB RAM, temel Dv2 arkadaşlarınızla kullanabilirsiniz hello bir uygulama hizmeti ortamı'nın diğer yararları şunlardır. Başka bir avantaj gereksinimlerinizi hello sistem toomeet ölçeklendirebilirsiniz olmalıdır. ASP sınırlı too20 örnekleri olduğu hello çok kiracılı ortamlarının aksine, ASE'de too100 ASP örneği ölçeklendirebilirsiniz. Merhaba şeyler ile VNet tümleştirme olmayan bir ana ile alma bir uygulama hizmeti ortamı ExpressRoute VPN ile çalışabilirsiniz biridir. 

Varken bazı servis talebi çakışma kullanır, bu özellik hiçbiri hello hiçbirini başkalarının değiştirebilirsiniz. Hangi özelliği toouse bağlı tooyour ihtiyaçları olan bilmek. Örneğin:

* Geliştirici misiniz ve yalnızca toorun Azure sitede isterseniz ve sahip erişim hello veritabanı masanıza altında hello istasyonunda hello kolay şey toouse karma bağlantılar ise. 
* Çok sayıda web hello genel bulut özelliklerinde tooput isteyen büyük bir kuruluş olan ve bunları kendi ağ yönetmek, hello uygulama hizmeti ortamı ile toogo istiyor. 
* Uygulama hizmeti sayıda varsa uygulamalar barındırılan ve yalnızca sanal ağınızı tooaccess kaynaklarında istediğiniz, sonra VNet tümleştirme hello şekilde toogo. 

Merhaba kullanım örnekleri bazı Basitlik vardır ilgili yönü. Sanal ağınızı zaten bağlıysa, tooyour VNet tümleştirme kullanarak ağ, şirket içi veya bir uygulama hizmeti ortamı tooconsume şirket içi kaynakları kolay bir yoludur. Daha fazla genel gider tooset site toosite VPN ağınızı ile yukarı hello HCM yükleme ile karşılaştırıldığında çok ise hello üzerinde tooyour şirket içi ağ ağınızı değilse, diğer yandan, bağlı. 

Ötesine işlevsel farklılıklar Merhaba, var. Ayrıca farklar fiyatlandırma. bir Premium hizmet teklifleri hello çoğu ağ yapılandırma seçenekleri ayrıca tooother harika özellikler teklifi Hello uygulama hizmeti ortamı özelliğidir. VNet tümleştirme standart veya Premium ASP kullanılabilir ve güvenli bir şekilde hello çok kiracılı uygulama hizmeti ağınızdan kaynaklarında tüketen için mükemmeldir. Karma bağlantılar şu anda bağlı olan, ücretsiz başlayıp aşamalı olarak daha pahalı alma düzeyleri fiyatlandırma olan hesap ihtiyacınız hello miktarına bağlı BizTalk. Bu tooworking birçok ağlarda olsa geldiğinde, 100'den de ayrı ağlar tooaccess kaynaklarında etkinleştirebilirsiniz karma bağlantılar gibi diğer hiçbir özellik yok. 

<!--Image references-->
[1]: ./media/web-sites-integrate-with-vnet/vnetint-upgradeplan.png
[2]: ./media/web-sites-integrate-with-vnet/vnetint-existingvnet.png
[3]: ./media/web-sites-integrate-with-vnet/vnetint-createvnet.png
[4]: ./media/web-sites-integrate-with-vnet/vnetint-howitworks.png
[5]: ./media/web-sites-integrate-with-vnet/vnetint-appmanage.png
[6]: ./media/web-sites-integrate-with-vnet/vnetint-aspmanage.png
[7]: ./media/web-sites-integrate-with-vnet/vnetint-aspmanagedetail.png
[8]: ./media/web-sites-integrate-with-vnet/vnetint-vnetp2s.png

<!--Links-->
[VNETOverview]: http://azure.microsoft.com/documentation/articles/virtual-networks-overview/ 
[AzurePortal]: http://portal.azure.com/
[ASPricing]: http://azure.microsoft.com/pricing/details/app-service/
[VNETPricing]: http://azure.microsoft.com/pricing/details/vpn-gateway/
[DataPricing]: http://azure.microsoft.com/pricing/details/data-transfers/
[V2VNETP2S]: http://azure.microsoft.com/documentation/articles/vpn-gateway-howto-point-to-site-rm-ps/
[IntPowershell]: http://azure.microsoft.com/documentation/articles/app-service-vnet-integration-powershell/
[ASEintro]: http://docs.microsoft.com/azure/app-service/app-service-environment/intro
[ILBASE]: http://docs.microsoft.com/azure/app-service/app-service-environment/create-ilb-ase
[V2VNETPortal]: https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal
[VPNERCoex]: http://docs.microsoft.com/en-us/azure/expressroute/expressroute-howto-coexist-resource-manager
[ASE]: http://docs.microsoft.com/azure/app-service/app-service-environment/intro
