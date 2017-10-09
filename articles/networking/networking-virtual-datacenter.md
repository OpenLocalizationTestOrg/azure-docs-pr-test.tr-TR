---
title: aaaMicrosoft Azure sanal veri merkezi | Microsoft Docs
description: "Nasıl toobuild Azure'da sanal verilerinizi merkezi bilgi edinin"
services: networking
author: tracsman
manager: rossort
tags: azure-resource-manager
ms.service: virtual-network
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jonor
ms.openlocfilehash: 84f77b16edaece202a6a94b6107f1c9585ec7f38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-virtual-data-center"></a>Microsoft Azure sanal veri merkezi
**Microsoft Azure**: hızlı hareket, tasarruf, şirket içi uygulamaları ve verileri tümleştirme

## <a name="overview"></a>Genel Bakış
Şirket içi uygulamalar tooAzure geçirme, bile önemli değişiklikler (bir yaklaşım "kaldırın ve shift" denir), kuruluşların hello yararları güvenli ve ekonomik bir altyapı sağlar. Toomake hello en ancak bulut bilgi işlem olası hello çeviklik kuruluşların kendi mimarileri tootake yeteneklerinden Azure gelişmesi. Microsoft Azure hiper ölçekli hizmetler ve altyapı, Kurumsal düzeydeki özellikleri ve güvenilirlik ve karma bağlantı için birçok seçenek sunar. Müşteriler, bu bulut aracılığıyla ya da hizmetleri tooaccess Internet hello veya özel ağ bağlantısı sağlayan Azure ExpressRoute ile seçebilir. Merhaba Microsoft Azure platformu tooseamlessly altyapılarını hello bulutunu oluşturmak ve genişletmek için çok katmanlı mimarileri müşterilerin olanak tanır. Ayrıca, güvenlik hizmetleri sunarak Microsoft iş ortaklarının geliştirilmiş özellikleri sağlar ve azure'da toorun olan sanal gereçler en iyi duruma getirilmiş.

Bu makalede desenleri genel bir bakış sağlar ve birçok müşteri n tüm toohello bulut taşıma hakkında düşünürken, yüz mimari ölçek, performans ve güvenlik sorunları kullanılan toosolve olabilir tasarımları hello. Nasıl toofit farklı Kuruluş BT rolleri hello yönetim ve idare hello sisteminin da ele alınmıştır, Vurgu toosecurity gereksinimleri ve maliyet iyileştirmesi ile bir genel bakış.

## <a name="what-is-a-virtual-data-center"></a>Sanal veri merkezi nedir?
Merhaba, erken gün içinde hello ortak spektrumun tasarlanmış toohost tek, nispeten yalıtılmış uygulamalar, bundan çözümleri bulut. Bu yaklaşım da birkaç yıldır çalışmıştır. Ancak, bulutun avantajlarını hello çözümleri belirgin hale geldi ve birden çok büyük ölçekli iş yüklerini olan ve güvenlik, güvenilirlik, performans, adresleme hello bulut üzerinde barındırılan dağıtımların bir maliyetlerinin veya daha fazla bölgeler hello önemli hale geldi Merhaba bulut hizmeti yaşam döngüsünü.

Merhaba aşağıdaki bulut dağıtım diyagram güvenlik açıkları (kırmızı kutu) ve en iyi duruma getirme ağ sanal Gereçleri yer bazı örnekleri (sarı kutusu) iş yüklerinde gösterir.

[![0]][0]

Merhaba sanal veri merkezi (vDC) toosupport kurumsal iş yüklerinin ölçeklendirmeye yönelik bu gerekliliğini gelen doğdu ve hello hello genel buluta büyük ölçekli uygulamalar destekleme olduğunda ortaya çıkan hello sorunlarıyla toodeal gerekir.

VDC yalnızca hello uygulama iş yüklerini hello bulut, ancak aynı zamanda hello ağ, güvenlik, yönetim ve altyapı (örneğin, DNS ve Dizin Hizmetleri) değil. Genellikle de bir özel bağlantı geri tooan içi ağ veya veri merkezi sağlar. TooAzure giderek daha fazla iş yükleri taşımak gibi bu iş yükleri yerleştirilir hello altyapı ve nesneleri destekleme hakkında önemli toothink gereklidir. Dikkatle kaynakları nasıl yapılandırıldığı hakkında düşünmeye "bağımsız veri akışı, güvenlik modelleri ve uyumluluk sorunları ayrı olarak yönetilmelidir iş yükü Adaları" yüzlerce hello artışı önleyebilirsiniz.

Sanal veri merkezi temelde ortak destekleyici İşlevler, özellikler ve altyapı ile ayrı ancak ilgili varlıklar koleksiyonudur. Tümleşik bir vDC iş yüklerinizi görüntüleyerek nedeniyle daha az maliyet sağlarsınız ölçeğin bileşeni ve veri ile en iyi duruma getirilmiş güvenlik tooeconomies daha kolay işlemleri, yönetim ve uyumluluk denetimleri ile birlikte merkezileşmeyi akış.

> [!NOTE]
> VDC hello toounderstand olduğundan önemlidir **değil** bir ayrık Azure ürün, ancak çeşitli özellikleri ve yetenekleri hello birleşimi çok tam gereksinimlerinizi karşılayacak. vDC iş yükleri ve Azure kullanım toomaximize hakkında kaynakları ve yeteneklerini hello bulutta düşünüyorum bir yoludur. Merhaba sanal DC bu nedenle bir modüler nasıl yaklaşımdır toobuild hello Azure kuruluş roller ve sorumluluklar uyarak, BT Hizmetleri ayarlama.

Merhaba vDC iş yükleri ve Azure uygulamalarınızı senaryoları aşağıdaki Merhaba alma kuruluşların yardımcı olabilir:

-   Birden çok ilişkili iş yüklerinin barındırma
-   Bir şirket içi ortamına tooAzure geçirme iş yüklerini
-   Paylaşılan veya merkezi güvenliği ve erişim gereksinimleri iş yüklerinde uygulama
-   DevOps ve merkezi BT büyük bir kuruluş için uygun şekilde karıştırma

Merhaba anahtar toounlock hello vDC avantajları, bir merkezi topolojisi (hub ve bağlı bileşen) Azure özellikleri karışımını içeren: [Azure VNet][VNet], [Nsg'ler] [ NSG], [VNet eşlemesi][VNetPeering], [kullanıcı tanımlı yolları (UDR)][UDR]ve Azure kimlikle [ Rol tabanlı erişim denetimini (RBAC)][RBAC].

## <a name="who-needs-a-virtual-data-center"></a>Sanal bir veri merkezi gerek duyan?
Birkaç Azure iş yüklerinin birden çok toomove gereken herhangi bir Azure müşteriye ortak kaynakları kullanma hakkında düşünmekten yararlı olabilir. Merhaba büyüklük bağlı olarak hatta tek tek uygulamalar hello modellerini kullanan yararlanabilir ve bileşenleri toobuild vDC kullanılır.

Kuruluşunuzda bir merkezi BT, ağ güvenliği varsa ve/veya uyumluluk takım/departmanı, vDC yardımcı İlkesi noktaları, vergi, ayrımı zorlamak ve uygulama ekipleri çok verilirken ortak bileşenleri temel hello bütünlüğünü sağlamak olabilir özgürlük ve olduğu gibi denetim gereksinimlerinize uygun.

TooDevOps aradığınız kuruluşlar hello ağ tooprovide cep Azure kaynaklarınızın yetkili ve (abonelik veya kaynak grubunda ortak bir abonelik) grubu içindeki toplam denetime sahip olduklarından emin olmak hello vDC kavramları kullanan ve güvenlik sınırları bir merkezi ilke hub VNet ve kaynak grubu tarafından tanımlanan uyumlu kalır.

## <a name="considerations-on-implementing-a-virtual-data-center"></a>Sanal bir veri merkezi uygulama konusunda dikkat edilecek noktalar
VDC tasarlarken, birkaç bileşendirler sorunları tooconsider vardır:

-   Kimlik ve Dizin Hizmetleri
-   Güvenlik altyapısı
-   Bağlantı toohello bulut
-   Merhaba bulut içinde bağlantısı

##### <a name="identity-and-directory-service"></a>*Kimlik ve dizin hizmeti*
Kimlik ve Dizin Hizmetleri olan temel bir yönü, tüm veri merkezleri, her iki şirket içi ve hello bulutta. Erişim ve yetkilendirme tooservices hello vDC içinde ilgili tooall yönlerini kimliğidir. toohelp yalnızca yetkili kullanıcılar ve işlemlerin Azure hesabınıza erişin ve kaynakları, Azure kimlik doğrulaması için çeşitli türlerde kimlik bilgilerini kullanan emin olun. Bunlar (tooaccess Azure hesabı hello) parolalar, şifreleme anahtarları, dijital imzalar ve sertifikaları içerir. [*Azure çok faktörlü kimlik doğrulaması* (MFA)] [ MFA] Azure hizmetlerine erişmek için güvenlik ek katmanıdır. Azure MFA sağlar kolay doğrulama seçeneklerini aralıklı güçlü kimlik doğrulaması — telefon araması, SMS mesajı veya mobil uygulama bildirimi — ve müşterilerin toochoose hello yöntemi tercih izin verin.

Büyük bir kuruluş toodefine kimliklerini hello yönetimi, kimlik doğrulama, yetkilendirme, rolleri ve ayrıcalıkları içinde veya hello vDC açıklayan bir kimlik yönetim işlemi gerekir. Bu işlem, Hello hedeflerini tooincrease güvenlik ve verimlilik, maliyet, kapalı kalma süresi ve yinelenen manuel görevleri yükünü azaltırken olması gerekir.

Kuruluşlar/farklı satırı-in-işletmeler için (LOB'lar) Hizmetleri zorlu bir karışımını gerektirebilir ve çalışanlar genellikle farklı projelerle söz konusu olduğunda farklı roller sahiptir. VDC her belirli rol tanımları, iyi idare ile çalışan tooget sistemler ile farklı ekipler arasında iyi iş Birliği gerektirir. Merhaba matris ve sorumlulukları, erişim hakları çok karmaşık olabilir. VDC Identity management aracılığıyla gerçekleştirilir [ *Azure Active Directory* (AAD)] [ AAD] ve rol tabanlı erişim denetimi (RBAC).

Bir dizin hizmeti, bulma, yönetme, yönetme ve gündelik öğeleri ve ağ kaynakları düzenleme için bir paylaşılan bilgileri altyapısıdır. Bu kaynaklar, birimler, klasörleri, dosyaları, yazıcılar, kullanıcılar, gruplar, cihazları ve diğer nesneleri içerebilir. Merhaba ağdaki her bir kaynağın bir nesne hello dizin sunucusu tarafından kabul edilir. Bir kaynak hakkında bilgi, bu kaynak veya nesne ile ilişkili öznitelikleri koleksiyonu olarak depolanır.

Oturum açma için Azure Active Directory (AAD üzerinde) tüm Microsoft online iş hizmetlerini kullanır ve diğer kimlik gerekiyor. Azure Active Directory, temel dizin hizmetleri, gelişmiş kimlik yönetimi ve uygulama erişim yönetimi özelliklerini bir araya getiren kapsamlı bir kimlik ve erişim yönetimi bulut çözümüdür. AAD şirket içi Active tooenable tek oturum için tüm bulut tabanlı açma ve yerel olarak barındırılan (şirket içi) uygulamalarını Directory ile tümleştirilebilir. Şirket içi Active Directory kullanıcı özniteliklerini Hello otomatik olarak eşitlenen tooAAD olabilir.

Tek bir genel yönetici gerekli değil tooassign vDC tüm izinleri olan. Bunun yerine her belirli bölüm (ya da Grup kullanıcılar veya hello dizin hizmeti Hizmetleri'nde) hello izinleri gerekli toomanage vDC içinde kendi kaynaklarını sahip olabilir. İzinleri yapılandırma Dengeleme gerektirir. Çok fazla izinler performans verimliliği engel ve çok az veya gevşek izinleri güvenlik riskleri artırabilirsiniz. Azure rol tabanlı erişim denetimi (RBAC) tooaddress vDC kaynaklar için ayrıntılı erişim yönetimi sunarak bu sorunu yardımcı olur.

##### <a name="security-infrastructure"></a>*Güvenlik altyapısı*
Güvenlik, bir vDC hello bağlamında çoğunlukla ilgili toohello ayrımı hello vDC'ın belirli bir sanal ağ segment ve nasıl toocontrol giriş ve çıkış akışlarına hello vDC trafiği altyapısıdır. Azure dağıtımlar arasında yetkisiz ve istenmeyen trafiği engelleyen çok kiracılı mimariyi temel alır, sanal ağ (VNet) yalıtım kullanarak, erişim denetim listeleri (ACL'ler), yük dengeleyicileri ve trafik akışını ilkeleri ile birlikte IP filtreleri. İç ağ trafiğini ağ adresi çevirisi (NAT) dış trafiğinden ayırır.

Hello Azure yapı altyapı kaynakları tootenant iş yüklerini ayırır ve sanal makinelerden (VM'ler) iletişim tooand yönetir. Hello Azure hiper yönetici sanal makineleri ve güvenli bir şekilde yollar ağ trafiği tooguest OS kiracılar arasında bellek ve işlem ayırmayı zorlar.

##### <a name="connectivity-toohello-cloud"></a>*Bağlantı toohello bulut*
Merhaba vDC dış ağlara toooffer Hizmetleri toocustomers, iş ortakları ve/veya iç kullanıcılar ile bağlantısı gerekir. Bu genellikle bağlantı anlamına gelir değil yalnızca toohello Internet, aynı zamanda tooon içi ağlar ve veri merkezleri.

Müşteriler kendi güvenlik ilkeleri toocontrol ne oluşturmak ve belirli vDC barındırılan hizmetleri denetleyicisinden erişilebilir nasıl (ile incelemesi) filtreleme ve trafiği ağ sanal Gereçleri ve özel yönlendirme ilkeleri ve filtreleme (ağ) kullanarak Internet hello Kullanıcı tanımlı Yönlendirme ve ağ güvenlik grupları).

Kuruluşlar çoğunlukla tooconnect VDC tooon içi veri merkezleri veya diğer kaynakları gerekir. Azure ve şirket içi ağlar arasında Hello bağlantısı, bu nedenle etkili bir mimari tasarlarken önemli en boy olur. İşletmenin Azure'da vDC ve şirket arasındaki bir bağlantısı iki farklı şekilde toocreate vardır: transit hello Internet üzerinden ve/veya özel doğrudan bağlantılar.

Bir [ **Azure siteden siteye VPN** ] [ VPN] güvenli üzerinden kurulan hello vDC şifrelenmiş ve şirket içi ağlar arasında hello Internet üzerinden bir bağlantı hizmetidir. bağlantılar (IPSec/IKE tüneller). Azure siteden siteye bağlantı esnek, hızlı toocreate ise ve başka hiçbir tedarik gerektirmez, tüm bağlantıları üzerinden bağlandıkları Internet hello.

[**ExpressRoute** ] [ ExR] bir Azure bağlantısı hizmeti şirket içi ağlar vDC ve hello arasında özel bağlantılar oluşturmanızı sağlar. ExpressRoute bağlantıları üzerinde genel Internet hello ve daha yüksek güvenlik, güvenilirlik ve daha yüksek hızlı bir şekilde (too10 Gbps) tutarlı gecikme süresi ile birlikte teklif geçmemektedir. ExpressRoute müşteriler özel bağlantıları ile ilişkili uyumluluk kuralları hello faydaları elde edebilirsiniz ExpressRoute olarak VDC için çok kullanışlıdır.

ExpressRoute bağlantılarını dağıtma ile bir ExpressRoute servis sağlayıcı çekici içerir. Toostart ihtiyaç müşteriler, bu yaygın tooinitially kullanım hello vDC ve şirket içi kaynaklar arasında siteden siteye VPN tooestablish bağlantısını ve ardından tooExpressRoute bağlantı geçirin.

##### <a name="connectivity-within-hello-cloud"></a>*Merhaba bulut içinde bağlantısı*
[Sanal ağlar] [ VNet] ve [VNet eşlemesi] [ VNetPeering] hello temel bağlantı Hizmetleri vDC içinde ağ. Bir sanal ağ yalıtım vDC kaynaklar için doğal bir sınır garanti eder ve VNet eşlemesi verir intercommunication hello içinde farklı sanal ağlar arasında aynı Azure bölgesi. VNet içinde ve sanal ağlar arasındaki trafik denetimi gereken bir dizi güvenlik kuralları belirtilen erişim denetimi listeleri toomatch ([ağ güvenlik grubu][NSG]), [ağ sanal Gereçleri ] [ NVA]ve özel yönlendirme tabloları ([UDR][UDR]).

## <a name="virtual-data-center-overview"></a>Sanal veri merkezi genel bakış

### <a name="topology"></a>Topoloji
Tek bir Azure bölgesi içinde genişletilmiş hello sanal veri merkezi hub ve bağlı bileşen modeli

[![1]][1]

Merhaba hub olduğunu denetleyen ve farklı bölgelere arasında giriş ve/veya çıkış trafiği inceler hello merkezi bölgesi: Internet, şirket içi ve bağlı bileşen hello. Merhaba hub ve bağlı bileşen topolojisi hello BT departmanı yetersizliğini ve Etkilenme hello olasılığını azaltırken bir etkili şekilde tooenforce güvenlik ilkeleri merkezi bir konumda sağlar.

Merhaba hub hello bağlı bileşen tarafından tüketilen hello ortak hizmet bileşenleri içerir. Ortak merkezi hizmetlerinin bazı tipik örnekler şunlardır:

-   Merhaba Windows Active Directory altyapısı (ADFS hizmeti ile Merhaba ilgili) alma erişim toohello iş yüklerini spoke hello önce güvenilmeyen ağlardan erişme lisanslamasını kullanıcı kimlik doğrulaması için gerekli
-   Bir DNS hizmeti tooresolve hello bağlı bileşen, tooaccess kaynakları şirket içi ve hello Internet hello iş yükü için adlandırma
-   Tooimplement çoklu oturum açma iş yükleri üzerinde bir PKI altyapısı
-   Merhaba bağlı bileşen ve Internet arasında akış denetimi (TCP/UDP)
-   Merhaba spoke ve şirket içi arasında akış denetimi
-   İsterseniz, akış denetimi ve başka bir uç arasında

Merhaba vDC birden fazla bağlı bileşen arasında hello paylaşılan hub altyapısını kullanarak genel maliyeti azaltır.

Her bağlı bileşen Hello rolü toohost iş yükleri farklı türde olabilir. Merhaba bağlı bileşen de modüler bir yaklaşım için yinelenebilir dağıtımlara sağlayabilirsiniz (örneğin, geliştirme ve test, kullanıcı kabul testi, ön üretim ve üretim) Merhaba, aynı iş yükleri. Merhaba bağlı bileşen de kullanılan toosegregate olması ve farklı gruplar (örneğin, DevOps gruplar), kuruluşunuzdaki etkinleştirin. Bir bağlı bileşen içinde bu temel iş yükü veya karmaşık çok katmanlı iş yükleri trafiği ile Merhaba katmanlar arasında kontrol olası toodeploy olur.

##### <a name="subscription-limits-and-multiple-hubs"></a>Abonelik sınırlarını ve birden çok hub'ları
Azure'da hello türü ne olursa olsun, her bileşen bir Azure aboneliği dağıtılır. farklı Azure abonelikleri Azure bileşenlerinin Hello yalıtım erişim ve yetkilendirme farklı düzeyleri ayarlama gibi farklı LOB'lar hello gereksinimlerini karşılayabilen.

Her BT sistemi olduğu gibi olsa da, platformlar sınırları tek bir vDC bağlı bileşen, toolarge sayısı ölçeklendirebilirsiniz. Merhaba hub kısıtlamaları ve sınırları olan ilişkili tooa belirli Azure aboneliğiniz dağıtımıdır (örneğin, VNet eşlemeler - max sayısını görmek [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları] [ Limits] Ayrıntılar için). Burada sınırları bir sorun olabilir durumlarda hello mimarisi ölçeklendirebilirsiniz en fazla bir hub ve bağlı bileşen tek hub bağlı bileşen tooa kümeden hello modelini genişleterek daha fazla. Express Route veya siteden siteye VPN kullanarak bir veya daha fazla Azure bölgelerindeki çok sayıda hub birbirine bağlanabilir.

[![2]][2]

Hello kullanıma sunulması, çok sayıda hub hello maliyet ve yönetim çaba hello sisteminin artırır ve yalnızca ölçeklenebilirlik tarafından hizalı (örnek: sistem sınırlarını veya artıklık) ve bölgesel çoğaltma (örnekler: son kullanıcı performans veya olağanüstü durum kurtarma). Çok sayıda hub gerektiren senaryolarda, tüm hello hub'ları aynı işletimsel kolaylığı için hizmetleri kümesi toooffer hello çaba.

##### <a name="interconnection-between-spokes"></a>Bağlı bileşen arasında bağlantısı
Tek bir bağlı bileşen içinde olası tooimplement karmaşık çok katmanları iş yükleri olur. Çok katmanlı yapılandırmaları aynı sanal ağı ve filtreleme hello akar Nsg'leri kullanarak hello alt ağlar (her katman için bir) kullanılarak uygulanabilir.

Üzerindeki diğer yandan Merhaba, bir Mimarı toodeploy çok katmanlı bir iş yükü birden çok Vnet'lerde isteyebilirsiniz. VNet eşlemesi kullanarak, bağlı bileşen tooother bağlı bileşen hello içinde bağlanıp aynı hub'ı veya farklı hub. Bu senaryo tipik örneğidir hello veritabanı farklı bir spoke (VNet) içinde dağıtılırken uygulama işleme sunucularının bir spoke (VNet) olduğu hello durumdur. Bu durumda, bu kolay toointerconnect VNet eşlemesi ile Merhaba bağlı bileşen ve böylece hello hub'ı aracılığıyla transiting kaçının. Bir mimari ve güvenlik inceledikten hello hub atlayarak önemli güvenlik veya yalnızca hello hub bulunabilir noktaları denetimini atla değil gerçekleştirilen tooensure olmalıdır.

[![3]][3]

Bağlı bileşen da hub'ı olarak davranan birbirine tooa spoke olabilir. Bu yaklaşımın iki düzeyli hiyerarşisi oluşturur: hello alt bağlı bileşen (düzey 1) hello hiyerarşi, hello hub hale bağlı hello daha yüksek düzeyde (düzey 0). vDC, Hello bağlı bileşen tooforward hello trafiği toohello merkezi hub tooreach toohello şirket içi ağ veya Internet gerekir. Bir hub iki düzeyde mimarisiyle basit hub bağlı ilişki hello yararları kaldırır karmaşık yönlendirme tanıtır.

Azure karmaşık topolojiler olanak tanısa da hello temel ilkeler hello vDC kavram Yinelenebilirlik ve Basitlik biridir. toominimize yönetim çabası vDC referans mimarisi önerilen hello hello basit hub bağlı tasarımdır.

### <a name="components"></a>Bileşenler
Sanal veri merkezi dört temel bileşen türü yapılır: **altyapı**, **Çevre ağları**, **iş yükleri**, ve **izleme**.

Her bileşen türü çeşitli Azure özellikleri ve kaynakları oluşur. VDC birden çok bileşenleri türleri ve hello birçok çeşidi örnekleri aynı oluşur bileşen türü. Örneğin, farklı uygulamaların temsil birçok farklı, mantıksal olarak ayrılmış iş yükü örnekleri olabilir. Bu farklı bileşeni türlerini kullanın ve örnekleri tooultimately hello vDC oluşturun.

[![4]][4]

Merhaba vDC önceki üst düzey mimarisini hello hub bağlı bileşen topolojisi farklı bölgelerde kullanılır farklı bileşen türleri gösterir. Merhaba diyagramı hello mimarisi çeşitli kısımlarını altyapı bileşenlerini gösterir.

Bir (için bir şirket içi DC'ye veya vDC) iyi bir uygulama erişim hakları ve ayrıcalıkları grup tabanlı olmalıdır. Erişim ilkeleri ekipleri ve yapılandırma hataları en aza içinde yardımları genelinde tutarlı bir şekilde koruma grupları ile ilgili, tek tek kullanıcılar yerine yardımcı olur. Atama ve kaldırma kullanıcıların tooand uygun gruplarından hello ayrıcalıkları belirli bir kullanıcının güncel tutma yardımcı olur.

Her rol grubunu hangi Grup hangi iş yükü ile ilişkili olduğunu kolay tooidentify kolaylaştırarak adları benzersiz bir önek olması gerekir. Örneğin, bir kimlik doğrulama hizmeti barındıran bir iş yükü adlı grupları olabilir *AuthServiceNetOps, AuthServiceSecOps, AuthServiceDevOps ve AuthServiceInfraOps.* Benzer şekilde için merkezi rol veya rolleri değil ilgili tooa belirli bir hizmeti, "Corp" ile başlayan *CorpNetOps* örneğin.

Birçok kuruluş, gruplar tooprovide rolleri önemli bir dökümünü aşağıdaki hello çeşitlemesi kullanın:

-   Merhaba *merkezi BT grubu (Corp)* hello sahiplik hakları toocontrol (örneğin, ağ ve güvenlik) altyapı bileşeni vardır ve bu nedenle toohave hello hello abonelikte katılımcı rolü gerekiyor (ve denetime sahiptir Merhaba hub) ve ağ hello bağlı bileşen katkıda bulunan hakları. Büyük kuruluş sık'Bu yönetim sorumlulukları gibi birden çok ekibin arasında bölme; bir ağ işlemlerini (CorpNetOps) grubu (odaklanılan özel ağ üzerinde) ve güvenlik işlemleri (CorpSecOps) grubu (için güvenlik duvarı ve güvenlik ilkesini sorumlu). Bu belirli bir durumda, iki farklı gruplar bu özel roller atama için oluşturulan toobe gerekir.
-   Merhaba *geliştirme & test (AppDevOps) grubu* hello sorumluluk toodeploy iş yükleri (uygulamalarına veya hizmetlerine) vardır. Bu grubun hello sanal makine Katılımcısı, Iaas dağıtımları ve/veya bir veya daha fazla PaaS katkıda bulunanlar rol alır (bkz [Azure rol tabanlı erişim denetimi için yerleşik roller][Roles]). İsteğe bağlı olarak dev hello & test takımı toohave görünürlük güvenlik ilkeleri (Nsg'ler) ve hello hub'ın içinde yönlendirme ilkeleri (UDR) ya da belirli bir bağlı bileşen gerekebilir. Bu nedenle, toplama toohello rollerinde, katkıda bulunan iş yükleri için bu grubun Ayrıca ağ okuyucu hello rolü gerekir.
-   Merhaba *işlem ve bakımı grubu (CorpInfraOps veya AppInfraOps)* üretim iş yükleri yönetme hello sorumluluk sahip. Bu grubun toobe herhangi bir üretim aboneliğiniz iş yüklerini abonelik katılımcı gerekir. Bir ek yükseltme destek ekibi grubunun hello rolüne sahip abonelik katkıda bulunan üretim ve sipariş toofix olası yapılandırma sorunlarını hello üretimde de hello merkezi hub abonelikte gerekiyorsa bazı kuruluşlar da değerlendirebilir ortam.

VDC Hello hub'ı yönetme hello merkezi BT grupları için oluşturulan grupları hello iş yükü düzeyinde karşılık gelen gruplarınız şekilde yapılandırılmıştır. Ayrıca toomanaging hub kaynakları yalnızca hello merkezi BT grupları mümkün toocontrol dış erişim ve hello abonelik en üst düzey izinleri olacaktır. Ancak, iş yükü grupları mümkün toocontrol kaynakları ve bunların VNet bağımsız olarak merkezi BT üzerinde izinleri olacaktır.

Merhaba vDC gereksinimlerini toobe toosecurely konak farklı satırı-in-işletmeler arasında (LOB'lar) birden çok proje bölümlenmiş. Tüm projeleri farklı yalıtılmış ortamlara (geliştirme, UAT, üretim) gerektirir. Her bu ortamlar için ayrı Azure abonelikleri doğal yalıtımı sağlar.

[![5]][5]

Merhaba önceki diyagramda hello kuruluşun projeleri, kullanıcılar, gruplar ve hello Azure bileşenleri dağıtıldığı hello ortamlar arasındaki ilişkiyi gösterir.

Genellikle, BT, bir ortam (veya katman) birden çok uygulama, dağıtılan ve yürütülen bir sistemdir. Büyük kuruluşlar kullanmak bir geliştirme ortamı (değişiklikler ilk olarak yapılan ve test) ve bir üretim ortamında (ne son kullanıcılar kullanın). Bu ortamlarda, genellikle birkaç hazırlık ortamları bunları Between tooallow aşamalı dağıtımı (ürün), test ve sorun oluşması durumunda geri alma ile ayrılır. Dağıtım mimarilerinin büyük ölçüde farklılık, ancak genellikle hello basic (Geliştirme) geliştirme sırasında başlayıp (üretim) üretim sırasında işlemi hala izlenir.

Çok katmanlı ortamlar bu tür için ortak bir mimarisini DevOps (geliştirme ve test etme), UAT (hazırlama) ve üretim ortamlarını oluşur. Kuruluşlar tek yararlanabilir veya toodefine erişim ve hakları toothese ortamlar birden çok Azure AD Kiracı. Merhaba önceki diyagramda söz konusu iki yerde farklı gösterilmektedir Azure AD kiracılarıyla kullanılır: DevOps ve UAT ve özel olarak üretim için diğer hello için bir tane.

Merhaba varlığı farklı Azure AD kiracılar ortamlar arasında hello ayırmayı zorlar. Merhaba aynı kullanıcı grubunu (örneğin, merkezi BT) farklı bir URI tooaccess farklı bir AD Kiracı kullanarak tooauthenticate hello rolleri veya da hello DevOps izinleriyle veya üretim ortamlarında projenin değiştirmek. farklı bir kullanıcı kimlik doğrulaması tooaccess farklı ortamlarda Hello varlığını olası kesintileri ve insan hataları neden diğer sorunları azaltır.

#### <a name="component-type-infrastructure"></a>Bileşen türü: altyapısı
Bu bileşen türü altyapısını destekleyen hello çoğunu bulunduğu olur. Ayrıca Burada, merkezi BT, güvenlik ve/veya uyumluluk ekipler, çoğu zaman.

[![6]][6]

Altyapı bileşenlerine vDC hello farklı bileşenleri arasındaki bir bağlantısı sağlayın ve hello hub hem hello bağlı bileşen de mevcuttur. Merhaba yönetme ve hello altyapı bileşenlerini koruma sorumluluğunu genellikle toohello Orta atanır BT ve/veya güvenlik ekibine.

Merhaba BT altyapı grubu, birincil görevleri hello tooguarantee hello tutarlılık IP adresi şemaların hello kuruluş genelinde biridir. Merhaba özel IP adresi alanı atanan toohello vDC toobe tutarlı ve şirket içi ağlarınız Atanan özel IP adresleri ile çakışan değil gerekir.

NAT hello şirket içi sınır yönlendiricileri veya Azure'da IP adresi çakışmalarını ortamları önleyebilirsiniz beklerken zorluklar tooyour altyapı bileşenlerini ekler. Yönetim basitliği NAT toohandle IP sorunları kullanarak önerilen bir çözüm değildir şekilde hello anahtar vDC, amaçlarını biridir.

Altyapı bileşenlerine işlevselliği aşağıdaki hello içerir:

-   [**Kimlik ve Dizin Hizmetleri**][AAD]. Azure'daki erişim tooevery kaynak türü, bir dizin hizmetinde depolanan kimlik tarafından denetlenir. Merhaba dizin hizmeti depoları yalnızca kullanıcıların listesini Merhaba, ancak Ayrıca belirli bir Azure aboneliği içindeki erişim hakları tooresources hello. Bu hizmetler yalnızca bulut bulunabilir veya Active Directory'de depolanan şirket içi kimlik ile eşitlenebilir.
-   [**Sanal ağ**][VPN]. Sanal ağlar vDC ana bileşenlerinin biridir ve trafik yalıtımı sınırında hello Azure platformu toocreate etkinleştirin. Tek veya birden çok sanal ağ kesimleri, her biri belirli bir IP ağ öneki (alt ağ), bir sanal ağ oluşur. Sanal ağ Hello nerede Iaas sanal makineleri ve PaaS Hizmetleri özel iletişim kurup bir iç çevre alanı tanımlar. Sanal makineleri (ve PaaS Hizmetleri) bir sanal ağ olamaz iletişim farklı bir sanal ağ tooVMs (ve PaaS Hizmetleri'nde) tarafından bile her iki sanal ağ oluşturulursa hello doğrudan aynı müşteri altında hello aynı abonelik. Yalıtım müşteri sanal makineleri sağlar önemli bir özelliktir ve iletişim bir sanal ağ içindeki özel kalır.
-   [**UDR**][UDR]. Bir sanal ağ içinde trafik hello sistem yönlendirme tablosu üzerinde göre varsayılan yönlendirilir. Bir kullanıcı tanımlamak ağ yöneticileri tooone ya da daha fazla alt ağlar toooverwrite hello davranışını hello sistem yönlendirme tablosu ilişkilendirmek ve sanal ağ içinde bir iletişim yolu tanımlamak özel bir yönlendirme tablosu yoldur. belirli özel VM'ler ve/veya ağ sanal Gereçleri ve yük dengeleyici hello hub ve bağlı bileşen hello mevcut yoluyla hello spoke aktarım gelen o çıkış trafiği Udr'ler Hello varlığını güvence altına alır.
-   [**NSG**][NSG]. Bir ağ güvenlik grubu, trafik IP kaynakları, hedef IP, protokolleri, IP kaynak bağlantı noktaları ve IP hedef bağlantı noktalarına filtreleme gibi davranan güvenlik kuralları listesidir. Merhaba NSG uygulanan tooa alt ağ, bir Azure VM veya her ikisi ile ilişkili bir sanal NIC kartı olabilir. Merhaba Nsg'ler temel tooimplement doğru akış denetimi hello hub ve bağlı bileşen hello ' dir. NSG hello tarafından karşılanan güvenlik düzeyini Hello hangi bağlantı noktalarını açmanız ve hangi amaçla bir işlev değil. Müşteriler, ana bilgisayar tabanlı güvenlik duvarları gibi IPtables sahip VM başına ek filtreler uygulamak veya Windows Güvenlik Duvarı hello.
-   **DNS**. Merhaba vDC Vnet'ler kaynaklarında Hello ad çözümlemesi DNS yoluyla sağlanır. Merhaba varsayılan DNS adı çözümlemesini Hello kapsamını sınırlı toohello VNet ' dir. Genellikle, özel bir DNS hizmeti hello hub ortak Hizmetleri bir parçası olarak dağıtılan toobe gerekiyor, ancak DNS Hizmetleri ana tüketicileri hello hello spoke bulunur. Gerekirse, müşterilerin DNS bölgeleri toohello bağlı bileşen temsiliyle hiyerarşik bir DNS yapı oluşturabilirsiniz.
-   [** Abonelik] [ SubMgmt] ve [kaynak grubu Yönetim][RGMgmt]**. Bir abonelik doğal sınır toocreate Azure içinde birden çok kaynak grupları tanımlar. Bir Abonelikteki kaynakların kaynak grupları adlı mantıksal kapsayıcılarında birlikte birleştirilir. Merhaba kaynak grubu vDC bir mantıksal Grup tooorganize hello kaynaklarını temsil eder.
-   [**RBAC**][RBAC]. RBAC, olası toomap kuruluş, toorestrict kullanıcılar tooonly belirli bir alt eylem izin vererek hakları tooaccess belirli Azure kaynakları ile birlikte rolüdür. RBAC ile Merhaba uygun rol toousers, grupları ve uygulamaları hello ilgili kapsam içinde atayarak erişim izni verebilir. bir rol ataması Hello kapsamını bir Azure aboneliği, bir kaynak grubu veya tek bir kaynak olabilir. RBAC devralma izin verir. Bir üst kapsamda atanan bir rol, ayrıca içerdiği toohello alt erişim verir. RBAC kullanarak, görevlerini kurabilmeleri ve tooperform işlerini gereksinim yalnızca hello miktarını erişim toousers verin. Örneğin, kullanım RBAC toolet bir çalışan yönetmek bir Abonelikteki sanal makineleri başka bir SQL veritabanları hello içinde yönetebilirsiniz sırasında aynı abonelik.
-   [**VNet eşlemesi**][VNetPeering]. Merhaba kullanılan temel özellik toocreate hello vDC, VNet eşlemesi, iki sanal ağlar (Vnet'ler) hello bağlayan bir mekanizma altyapısıdır hello Azure veri merkezinin hello ağ üzerinden aynı bölgede.

#### <a name="component-type-perimeter-networks"></a>Bileşen türü: Çevre ağları
[Çevre ağı] [ DMZ] bileşenleri (çevre ağı olarak da bilinir) ile şirket içi veya fiziksel veri merkezi ağlarını, tüm bağlantı tooand hello Internet gelen tooprovide ağ bağlantısı sağlar. Burada, ağ ve güvenlik muhtemelen çoğu zaman, ekipler de olabilir.

Gelen paket hello güvenlik Gereçleri hello hub'hello güvenlik duvarı, Kimlikleri ve IP'leri, gibi hello bağlı bileşen hello arka uç sunucuları ulaşmadan önce akışına. Internet'e bağlı paketler hello iş yükleri de ilke zorlaması, denetleme ve denetim amacıyla, hello ağ ayrılmadan önce hello çevre ağında hello güvenlik Gereçleri akışına.

Çevre ağ bileşenleri hello aşağıdaki özellikleri sağlar:

-   [Sanal ağlar][VNet], [UDR][UDR], [NSG][NSG]
-   [Ağ sanal gereç][NVA]
-   [Yük Dengeleyici][ALB]
-   [Uygulama ağ geçidi][AppGW] / [WAF][WAF]
-   [Genel IP'ler][PIP]

Genellikle, merkezi hello BT ve güvenlik ekiplerinden gereksinim tanımı ve hello Çevre ağları işlemlerini sorumluluğu.

[![7]][7]

Merhaba önceki diyagramda gösterilmektedir hello zorlama iki çevreyi erişim toohello ile internet ve şirket içi ağ, her ikisi de hello hub yerleşik. Tek bir hub hello çevre ağ toointernet toosupport çok sayıda Web uygulaması Güvenlik Duvarı (WAFs) ve/veya güvenlik duvarları birden çok grupları kullanarak LOB'lar ölçeklendirebilirsiniz.

[**Sanal ağlar** ] [ VNet] hello hub'ı birden çok alt ağlar toohost hello farklı türde hizmetlerini sahip bir VNet üzerinde oluşturulan genellikle filtreleme ve gelen trafiği tooor inceleniyor hello NVAs, WAFs, üzerinden internet'e ve Azure uygulama ağ geçidi.

[**UDR** ] [ UDR] UDR kullanarak, müşterilerin dağıtabilir güvenlik duvarları, Kimlikleri/IP'leri ve diğer sanal gereçler ve ağ trafiğini yönlendirmek bu güvenlik Gereçleri güvenlik sınırı İlkesi zorlaması, Denetim ve denetleme yoluyla. Udr'ler, belirli özel VM'ler, ağ sanal Gereçleri ve hello vDC tarafından kullanılan yük dengeleyici üzerinden trafik transits hello hem hello hub ve hello bağlı bileşen tooguarantee oluşturulabilir. VM'ler hello spoke transit toohello doğru sanal gereçler içinde yerleşik üretilen, trafiği tooguarantee, bir UDR gereken toobe hello sonraki atlama hello hello iç yük dengeleyici ön uç IP adresini ayarlayarak hello spoke hello alt ağlarında ayarlayın. Merhaba iç yük dengeleyici hello iç trafiği toohello sanal gereçler (yük dengeleyici arka uç havuzu) dağıtır.

[![8]][8]

[**Ağ sanal Gereçleri** ] [ NVA] çevre ağı ile internet güvenlik duvarları ve/veya Web uygulaması Güvenlik Duvarı (WAFs) bir gruba normalde yönetilen erişim toohello hello hub hello.

Bu uygulamalar toosuffer çeşitli güvenlik açıkları ve olası güvenlik açıklarına eğilimindedir ve farklı LOB'lar yaygın olarak birçok web uygulaması kullanın. Web uygulamaları güvenlik duvarları, özel bir ürün köpek toodetect saldırılarına karşı web uygulamaları (HTTP/HTTPS) genel bir Güvenlik Duvarı'den daha kapsamlı kullanılan ' dir. Gelenek güvenlik duvarı teknolojisi ile karşılaştırıldığında, WAFs belirli özellikler tooprotect iç web sunucuları tehditlere karşı kümesine sahiptir.

Bir güvenlik duvarı grubu dağıtımınızla birlikte bir dizi güvenlik kuralları tooprotect hello iş yükleri ile aynı ortak yönetim hello bağlı bileşen ve Denetim erişim tooon içi ağları barındırılan hello altında çalışan güvenlik duvarı bir grubudur. Bir güvenlik duvarı grubu daha az WAF ile karşılaştırıldığında yazılım özelleştirilmiş sahiptir, ancak kapsam toofilter ve herhangi bir türde çıkış ve giriş trafiği incelemek kapsamlı bir uygulama vardır. Güvenlik Duvarı grupları ağ sanal hello Azure Market kullanılabilir olan uygulamaları (NVAs) aracılığıyla Azure'da normal olarak uygulanır.

NVAs toouse bir dizi hello Internet trafiği için önerilen ve trafik kaynaklanan için başka bir şirket içi. Hiçbir güvenlik çevre ağ trafiği hello iki küme arasındaki sağladığı gibi her ikisi için yalnızca bir kümesini NVAs kullanarak bir güvenlik riski oluşturur. Ayrı NVAs kullanarak denetim güvenlik kuralları hello karmaşıklığını azaltır ve hangi kuralları toowhich gelen ağ isteği karşılık gelen temizleyin kolaylaştırır.

En büyük kuruluşlar birden çok etki alanı yönetin. Azure DNS, belirli bir etki alanı için kullanılan toohost hello DNS kayıtlarını olabilir. Örnek olarak, hello hello Azure dış yük dengeleyici (veya hello WAFs) sanal IP adresi (VIP) içinde bir Azure DNS kaydına hello A kaydı kaydedilebilir.

[**Azure yük dengeleyici** ] [ ALB] Azure yük dengeleyici yüksek oranda kullanılabilir bir gelen trafiği yükü dengelenmiş bir kümede tanımlanmış hizmet örnekleri arasında dağıtabilirsiniz katman 4 (TCP, UDP) hizmeti sunar. Ön uç (genel IP uç noktaları veya özel IP uç noktaları) toohello yük dengeleyiciden ile veya adres çevirisi tooa arka uç IP adresi havuzu (örnekler olan; kümesi olmadan dağıtılabilir trafiği gönderilir Ağ sanal Gereçleri veya VM'ler).

Azure yük dengeleyici çeşitli sunucu örnekleri de hello hello durumunu araştırma ve bir araştırma toorespond hello yük dengeleyici durakları trafiği toohello sağlıksız örneği gönderme başarısız olduğunda. VDC içinde bir dış yük dengeleyici hello varlığını hello hub'ı (örneğin, Bakiye hello trafiği tooNVAs) ve hello bağlı bileşen (çok katmanlı uygulaması farklı VM'ler arasındaki trafiği Dengeleme gibi tooperform görevleri) sunuyoruz.

[**Uygulama ağ geçidi** ] [ AppGW] Microsoft Azure uygulama ağ geçidi çeşitli katman 7 Yük Dengeleme, uygulamanız için sunumu bir hizmet olarak uygulama teslim Denetleyicisi'ni (ADC) sağlayan özel bir sanal gereç olduğu. Bu CPU yoğunluklu SSL sonlandırma toohello uygulama ağ geçidi boşaltarak toooptimize web grubu verimlilik sağlar. Tek bir uygulama ağ geçidi arkasında birden çok Web sitesini hepsini bir kez dağıtımını gelen trafik, tanımlama bilgisi tabanlı oturum benzeşimi, URL yolu tabanlı Yönlendirme ve hello özelliği toohost dahil olmak üzere diğer katman 7 Yönlendirme yetenekleri de sağlar. Bir web uygulaması Güvenlik Duvarı (WAF) de hello uygulama ağ geçidi WAF SKU bir parçası olarak sağlanır. Bu SKU tooweb uygulamalardan ortak web Güvenlik Açıkları ve açıkları koruma sağlar. Application Gateway; İnternet'e yönelik ağ geçidi, yalnızca dahili ağ geçidi veya bu ikisinin bir birleşimi olarak yapılandırılabilir. 

[**Genel IP'ler** ] [ PIP] tooyour kaynak toobe izin veren, tooassociate hizmet uç noktaları tooa genel IP adresi erişilen bazı Azure özellikleri etkinleştir hello Internet. Bu uç nokta hello Azure sanal ağı üzerinde ağ adresi çevirisi (NAT) tooroute trafiği toohello iç adresi ve bağlantı noktasını kullanır. Bu yol hello birincil dış trafiğin toopass hello sanal ağda yoludur. hangi trafik geçirilen yapılandırılmış toodetermine Hello genel IP adresleri olabilir ve nasıl ve nerede toohello sanal ağda çevrilir.

#### <a name="component-type-monitoring"></a>Bileşen türü: izleme
İzleme bileşenleri görünürlük ve tümünden uyarı diğer bileşenleri türleri hello sağlar. Tüm takımların erişim toomonitoring hello bileşenleri için sahip olmanız gerekir ve Hizmetleri erişime sahip. Merkezi yardım masasına veya işlemleri takımlar varsa, bu bileşenler tarafından sağlanan tümleşik toohave erişim toohello verileri gereksiniminiz olacaktır.

Barındırılan kaynaklara günlüğe kaydetme ve Azure Hizmetleri tootrack hello davranışını izleme azure teklifleri farklı türde. İdare ve azure'da iş yüklerini denetimin tabanlı yalnızca üzerinde toplama günlük verilerini, aynı zamanda belirli bildirilen olaylara dayanarak hello özelliği tootrigger Eylemler olur.

Azure günlükleri başlıca iki türde vardır:

-   [**Etkinlik günlükleri** ] [ ActLog] ("İşlem günlüğü" olarak da bilinir) hello Azure aboneliği kaynaklarında gerçekleştirilen hello işlemleri hakkında bilgi sağlar. Bu günlükler aboneliklerinizi hello denetim düzlemi olaylarını bildirin. Her Azure kaynak denetim günlüklerini oluşturur.

-   [**Azure tanılama günlüklerini** ] [ DiagLog] olan bir kaynak tarafından oluşturulan günlükleri, zengin, sık hello işlemi bu kaynağın hakkında veriler sağlar. Bu günlükler Merhaba içeriğine kaynak türüne göre değişir.

[![9]][9]

Bir vDC, son derece önemli tootrack hello Nsg'ler günlükleri, özellikle bu bilgiler verilmiştir:

-   [**Olay günlükleri**][NSGLog]: hangi NSG kuralları uygulanan tooVMs ve örnek rolleriniz MAC adresine dayalı olan bilgiler sağlar.
-   [**Sayaç günlükleri**][NSGLog]: her NSG edildi yürütülen toodeny kural izin verme veya trafiği kaç kez izler.

Tüm günlükler, Denetim, statik çözümleme veya yedekleme amacıyla Azure depolama hesaplarında depolanabilir. Merhaba günlükleri bir Azure depolama hesabında depolanır, müşterilerin farklı türlerini kullanabilirsiniz çerçeveler tooretrieve prep, analiz etmek ve bu veri tooreport hello durumu ve sistem durumu, bulut kaynaklarının görselleştirin.

İzleme içi sistemleri ve genişletebilirsiniz büyük kuruluşlar zaten standart framework framework toointegrate günlükleri bulut dağıtımları tarafından oluşturulan almış olması gereken. Tüm hello hello bulutta oturum tookeep istediğiniz kuruluşlar için [Microsoft Operations Management Suite (OMS)] [ OMS] harika bir seçenektir. OMS, bulut tabanlı bir hizmet olarak uygulandığından altyapı hizmetlerine en az yatırımla onu kısa süre içinde çalışır duruma getirebilirsiniz. OMS ayrıca System Center Operations Manager tooextend gibi System Center bileşenleri ile varolan yönetim yatırımlarınızı hello bulutunu tümleştirebilirsiniz.

OMS günlük analizi hello OMS framework toohelp bileşeninin toplamak, ilişkilendirmek, arama ve günlük ve performans verilerini vermemizi bileşenleri işletim sistemleri, uygulamaları, altyapı bulut tarafından oluşturulan olur. Bu, tümleşik arama ve özel panolar tooanalyze tüm hello kayıtları vDC içinde iş yüklerini kullanılarak gerçek zamanlı operasyonel Öngörüler müşteriler verir.

#### <a name="component-type-workloads"></a>Bileşen türü: iş yükleri
İş yükü, gerçek uygulama ve hizmetlerinize bulunduğu bileşenleridir. Burada, uygulama geliştirme çoğu zaman, ekipler de olabilir.

Merhaba iş yükünün olanaklar gerçekten sonsuzdur. Merhaba, birkaçı hello olası iş yükü türleri şunlardır:

**İç iş KOLU uygulamaları**

İş kolu satır, bir kuruluşun bilgisayar uygulamaları kritik toohello devam eden işlemi uygulamalardır. İş KOLU uygulamaları, bazı ortak özelliklere sahiptir:

-   **Etkileşimli**. İş KOLU uygulamaları doğası gereği etkileşimli: veriler girilir ve sonuç/raporları döndürülür.
-   **Veri tabanlı**. İş KOLU uygulamaları sık erişim toohello veritabanları veya diğer depolama yoğunluklu verilerdir.
-   **Tümleşik**. Uygulamaları teklif tümleştirme içinde veya hello kuruluşunuz dışındaki diğer sistemlerle LOB.

**Müşteri Web sitelerini (Internet veya dahili e yönelik) karşılıklı** hello Internet ile etkileşim çoğu uygulamayı web siteleridir. Azure'un sunduğu hello yetenek toorun bir web sitesi bir Iaas VM veya gelen bir [Azure Web Apps] [ WebApps] site (PaaS). Azure Web Apps hello spoke vDC, Web uygulamaları hello hello dağıtımını izin sanal ağlar ile tümleştirmeyi destekler. Hello VNET tümleştirme ile tooexpose bir Internet uç nokta uygulamalarınız için gerekli değildir ancak hello kaynakları özel dışındaki Internet yönlendirilebilir adres özel ağınızdan yerine kullanabilirsiniz.

**Büyük veri analizi** tooscale tooa çok büyük hacimli yukarı verilere ihtiyaç duyduğunda veritabanları düzgün ölçeği değil. Hadoop teknoloji toorun dağıtılmış sorgular çok sayıda düğümü üzerinde paralel bir sistem sunar. Müşterilerin sahip hello seçeneği toorun veri iş yüklerini Iaas Vm'si veya PaaS ([Hdınsight][HDI]). Hdınsight bağlı bileşen hello vDC, dağıtılan tooa kümede olabilir, konum tabanlı bir sanal ağ dağıtma destekler.

**Olaylar ve ileti**
[Azure Event Hubs] [ EventHubs] toplar, dönüştüren ve milyonlarca etkinliği depolayan bir hiper ölçek telemetri alım hizmetidir. Dağıtılmış bir akış platform olarak, düşük gecikme süresi ve yapılandırılabilir zaman bekletme, Azure'da telemetri oldukça büyük miktardaki tooingest etkinleştirme sunar ve bu verileri birden çok uygulamalardan okuyun. Event Hubs ile tek bir akış gerçek zamanlı ve toplu tabanlı ardışık düzen destekleyebilir.

İleti hizmeti uygulamalar ve hizmetler arasında yüksek oranda güvenilir bir bulut aracılığıyla uygulanabilir [Azure Service Bus] [ ServiceBus] teklifleri zaman uyumsuz ile birlikte istemci ve sunucu arasında Mesajlaşma aracılı yapılandırılmış ilk olarak ilk çıkar (FIFO) Mesajlaşma ve yayımlama/abonelik yetenekleri.

[![10]][10]

### <a name="multiple-vdc"></a>Birden çok vDC
Şu ana kadar bu makalede hello temel bileşenleri ve tooa dayanıklı vDC katkıda mimarisi açıklayan bir tek vDC üzerinde odaklı. Azure yük dengeleyici, NVAs, kullanılabilirlik kümeleri, diğer mekanizmaları birlikte ölçek kümeleri gibi Azure özellikleri üretim hizmetlerinizi toobuild düz SLA düzeyleri izin tooa sistem katkıda.

Ancak, tek bir vDC tek bir bölge içinde barındırılan ve tüm bu bölge etkileyebilecek güvenlik açığı toomajor hizmet kesintisi. Tooachieve istediğiniz müşterilerin yüksek SLA tooprotect hello Hizmetleri aracılığıyla aynı farklı bölgelerde yerleştirilen iki (veya daha fazla) VDC proje hello dağıtımları gerekir.

Ek tooSLA sorunlarını burada birden çok VDC dağıtma mantıklı birkaç yaygın senaryo vardır:

-   Bölge/genel durum
-   Olağanüstü Durum Kurtarma
-   DC arasındaki mekanizması toodivert trafiği

#### <a name="regionalglobal-presence"></a>Bölge/genel durum
Azure veri merkezleri, dünya çapında çok sayıda bölgelerde yok. Birden çok Azure veri merkezlerinde seçerken, müşterilerin tooconsider iki ilgili faktörler gerekir: coğrafi uzaklıklar ve gecikme süresi. Müşterilerin hello VDC hello vDC hello son kullanıcılar, toooffer hello en iyi kullanıcı deneyimini arasındaki hello uzaklığı arasındaki tooevaluate hello coğrafi uzaklığı gerekir.

Merhaba VDC barındırıldığı Azure bölgesi da ihtiyacınız tooconform kuruluşunuz altında faaliyet yasal dairesi tarafından kurulan yasal düzenleme gereksinimlerine sahip.

#### <a name="disaster-recovery"></a>Olağanüstü Durum Kurtarma
Merhaba bir olağanüstü durum kurtarma planı iş yükü ilgilenen kesinlikle ilgili toohello türü ve farklı VDC arasında hello özelliği toosynchronize hello iş yükü durumunu uygulamasıdır. İdeal olarak, müşterilerin çoğu, iki farklı VDC tooimplement hızlı yük devretme yönteminde çalıştıran dağıtımlar arasında toosynchronize uygulama verilerini istiyorsunuz. Hassas toolatency çoğu uygulamalardır ve veri eşitlemesine olası zaman aşımı ve gecikme neden.

Eşitleme veya farklı VDC uygulamaların sinyal izleme bunların arasındaki iletişimi gerektirir. Farklı bölgelerdeki iki VDC üzerinden bağlı olması gerekir:

-   Merhaba vDC hub bağlı toohello olduğunda ExpressRoute özel eşleme aynı expressroute bağlantı hattı
-   birden çok ExpressRoute bağlantı hatları bağlı toohello ExpressRoute bağlantı hatları şirket omurga ve vDC kafes aracılığıyla bağlanan
-   Her Azure bölgesindeki vDC hub'larınız arasında siteden siteye VPN bağlantıları

Genellikle hello ExpressRoute bağlantısı tercih edilen hello daha yüksek bant genişliği ve tutarlı gecikme nedeniyle hello Microsoft omurga transiting zaman mekanizmadır.

Farklı bölgelerde bulunan iki (veya daha fazla) farklı VDC arasında dağıtılan bir uygulama yok Sihirli tarif toovalidate yoktur. Müşteriler çalışmalı ağ niteliğe testleri tooverify hello gecikme süresi ve bant genişliği hello bağlantıları ve hedef zaman uyumlu veya zaman uyumsuz veri çoğaltma uygun olup olmadığını ve hangi hello en iyi kurtarma süresi hedefi (RTO) olabilir, iş yükleri.

#### <a name="mechanism-toodivert-traffic-between-dc"></a>DC arasındaki mekanizması toodivert trafiği
Bir etkin teknik toodivert hello trafiği içinde bir DC tooanother gelen DNS temel alır. [Azure Traffic Manager] [ TM] kullanan etki alanı adı sistemi (DNS) mekanizması toodirect hello son kullanıcı trafiği toohello en uygun ortak uç belirli vDC hello. Araştırmalar, üzerinden trafik Yöneticisi düzenli aralıklarla farklı VDC ortak uç noktalarını hello hizmetinin durumunu denetler ve bu uç başarısız olması durumunda, bu otomatik olarak toohello ikincil vDC yönlendirir.

Trafik Yöneticisi Azure genel Uç noktalara çalışır ve kullanılabilir, örneğin, toocontrol ve yönlendir trafiği tooAzure VM'ler hello Web uygulamalarında vDC gerekli. Trafik Yöneticisi bile hello karşılaştıkları tüm Azure bölgesi başarısız esnektir ve birkaç ölçütlere göre farklı VDC içinde hizmet uç noktaları için kullanıcı trafiğinin hello dağıtımını kontrol edebilirsiniz (örneğin, belirli bir vDC hizmetinde hata veya seçme Merhaba istemci için en düşük ağ gecikmesini hello ile Merhaba vDC).

### <a name="conclusion"></a>Sonuç
Merhaba sanal veri merkezi bir yaklaşım toodata merkezi geçiş maliyetlerini azaltır ve sistem basitleştirme, bulut kaynak kullanımını en üst düzeye çıkarır Azure ölçeklenebilir bir mimaride özellikleri ve yetenekleri toocreate bir bileşimini kullanır hello buluta değil idare. Merhaba vDC kavram hello hub ortak paylaşılan hizmetler sağlamayı ve belirli uygulamalar/iş yükleri hello bağlı bileşen içinde vererek bir hub'a bağlı bileşen topolojisi temel alır. VDC hello yapısı nerede farklı Departmanlar (Merkezi BT, DevOps, işlem ve bakımı) birlikte her rolleri ve görevleri belirli bir listesiyle birlikte çalışacak şirket rollerin eşleşir. VDC "Kaldırın ve Shift" geçiş için hello gereksinimleri karşılıyor ancak de toonative bulut dağıtımları birçok avantaj sağlar.

## <a name="references"></a>Başvurular
özellikler aşağıdaki hello bu belgede ele alınan. Daha fazla Hello bağlantılar toolearn'ı tıklatın.

| | | |
|-|-|-|
|Ağ Özellikleri|Yük Dengeleme|Bağlantı|
|[Azure sanal ağlar][VNet]</br>[Ağ güvenlik grupları][NSG]</br>[NSG günlüklerini][NSGLog]</br>[Kullanıcı tanımlı yönlendirme][UDR]</br>[Ağ sanal Gereçleri][NVA]</br>[Genel IP adresleri][PIP]|[Azure yük dengeleyici (L3)][ALB]</br>[Uygulama ağ geçidi (L7)][AppGW]</br>[Web uygulaması güvenlik duvarı][WAF]</br>[Azure trafik Yöneticisi][TM] |[VNet eşlemesi][VNetPeering]</br>[Sanal özel ağ][VPN]</br>[ExpressRoute][ExR]
|Kimlik</br>|İzleme</br>|En İyi Uygulamalar</br>|
|[Azure Active Directory][AAD]</br>[Çok faktörlü kimlik doğrulaması][MFA]</br>[Rol tabanlı erişim denetimleri][RBAC]</br>[Varsayılan AAD rolleri][Roles] |[Etkinlik günlükleri][ActLog]</br>[Tanılama günlükleri][DiagLog]</br>[Microsoft Operations Management Suite][OMS]</br> |[En iyi yöntemler Çevre ağları][DMZ]</br>[Abonelik Yönetimi][SubMgmt]</br>[Kaynak grubu Yönetim][RGMgmt]</br>[Azure abonelik limitleri][Limits] |
|Diğer Azure Hizmetleri|
|[Azure Web uygulamaları][WebApps]</br>[Hdınsights (Hadoop)][HDI]</br>[Event Hubs][EventHubs]</br>[Service Bus][ServiceBus]|



## <a name="next-steps"></a>Sonraki Adımlar
 - Araştır [VNet eşlemesi][VNetPeering], hello underpinning teknolojisi vDC hub ve bağlı bileşen tasarımları
 - Uygulama [AAD] [ AAD] tooget Başlarken [RBAC] [ RBAC] araştırması
 - Bir abonelik ve kaynak yönetim modeli geliştirmek ve RBAC toomeet hello yapısı, gereksinimler, model ve kuruluşunuzun tanımlar. Merhaba en önemli etkinlik planlama. Yeniden düzenlemeyi, birleşmeler, yeni ürün satırlar, vb. için pratik, kadar planlayın.

<!--Image References-->
[0]: ./media/networking-virtual-datacenter/redundant-equipment.png "Bileşen çakışma örnekleri" 
[1]: ./media/networking-virtual-datacenter/vdc-high-level.png "Hub ve bağlı bileşen vDC üst düzey örneği"
[2]: ./media/networking-virtual-datacenter/hub-spokes-cluster.png "Hub ve bağlı bileşen kümesi"
[3]: ./media/networking-virtual-datacenter/spoke-to-spoke.png "Spoke spoke"
[4]: ./media/networking-virtual-datacenter/vdc-block-level-diagram.png "Blok düzeyi hello vDC diyagramı"
[5]: ./media/networking-virtual-datacenter/users-groups-subsciptions.png "Kullanıcılar, gruplar, abonelikleri ve projeleri"
[6]: ./media/networking-virtual-datacenter/infrastructure-high-level.png "Üst düzey altyapı diyagramı"
[7]: ./media/networking-virtual-datacenter/highlevel-perimeter-networks.png "Üst düzey altyapı diyagramı"
[8]: ./media/networking-virtual-datacenter/vnet-peering-perimeter-neworks.png "VNet eşlemesi ve Çevre ağları"
[9]: ./media/networking-virtual-datacenter/high-level-diagram-monitoring.png "İzleme için üst düzey diyagramı"
[10]: ./media/networking-virtual-datacenter/high-level-workloads.png "İş yükü için üst düzey diyagramı"

<!--Link References-->
[Limits]: https://docs.microsoft.com/azure/azure-subscription-service-limits
[Roles]: https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles
[VNet]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview
[NSG]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg 
[VNetPeering]: https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview 
[UDR]: https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview 
[RBAC]: https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is
[MFA]: https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication
[AAD]: https://docs.microsoft.com/azure/active-directory/active-directory-whatis
[VPN]: https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways 
[ExR]: https://docs.microsoft.com/azure/expressroute/expressroute-introduction 
[NVA]: https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/nva-ha
[SubMgmt]: https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-subscription-governance 
[RGMgmt]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview
[DMZ]: https://docs.microsoft.com/azure/best-practices-network-security
[ALB]: https://docs.microsoft.com/azure/load-balancer/load-balancer-overview
[PIP]: https://docs.microsoft.com/azure/virtual-network/resource-groups-networking#public-ip-address
[AppGW]: https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction
[WAF]: https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview
[ActLog]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs 
[DiagLog]: https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs
[NSGLog]: https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log
[OMS]: https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview
[WebApps]: https://docs.microsoft.com/azure/app-service-web/
[HDI]: https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-introduction
[EventHubs]: https://docs.microsoft.com/azure/event-hubs/event-hubs-what-is-event-hubs 
[ServiceBus]: https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview
[TM]: https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview
