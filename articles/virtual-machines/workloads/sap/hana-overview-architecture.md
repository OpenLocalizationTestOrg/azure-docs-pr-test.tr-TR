---
title: "aaaOverview ve Azure (büyük örnekler) üzerinde SAP HANA mimarisi | Microsoft Docs"
description: "Mimari genel bakış nasıl tooDeploy SAP HANA azure'da (büyük örnekler)."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e3ee6864af37ac322635eaef43e3c20101e3a769
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-overview-and-architecture-on-azure"></a>SAP HANA (büyük örnekler) genel bakış ve Azure üzerinde mimarisi

## <a name="what-is-sap-hana-on-azure-large-instances"></a>SAP HANA azure'da (büyük örnekler) nedir?

SAP HANA (büyük örneği) azure'da benzersiz çözüm tooAzure ' dir. Ayrıca Azure sanal makineleri dağıtma ve SAP HANA, Azure çalışan hello amaçla sunar tooproviding olasılığı toorun hello ve bir müşteri olarak ayrılmış tooyou çıplak sunucuları üzerinde SAP HANA dağıtın. bir müşteri olarak tooyou atanan konak/sunucu paylaşılmayan tam donanımında Hello SAP HANA Azure (büyük örnekler) çözüm üzerinde oluşturur. Merhaba sunucu donanımını işlem/sunucu, ağ ve depolama altyapısı içeren büyük damga olarak katıştırılır. Bir birleşim olarak olduğu sertifikalı HANA TDI. SAP HANA (büyük örnekler) azure'da Hello hizmet teklifinizi çeşitli farklı sunucu SKU'ları veya 72 CPU olan birimleri ve 960 CPU'lar ve 20 TB belleğe sahip 768 GB bellek toounits başlatarak boyutları sunar.

Merhaba müşteri yalıtımı hello altyapı damga içindeki gibi görünüyor, ayrıntılı kiracılar gerçekleştirilir:

- Ağ: Kiracı yalıtımı müşterilerin müşteri başına sanal ağlar altyapı yığınından içinde atanır. Bir kiracı tooa tek müşteri atanır. Bir müşteri, birden çok kiracıya sahip olabilir. Merhaba ağ yalıtımı kiracıların kiracılar hello altyapı damga düzeyinde arasındaki ağ iletişimi engelliyor. Kiracılar toohello ait olsa bile aynı müşteri.
- Depolama bileşenleri: depolama birimleri depolama sanal makinelerde yalıtımı tooit atanmış. Depolama birimleri tooone depolama sanal makine yalnızca atanabilir. Bir depolama alanı sanal makine özel olarak tooone tek Kiracı hello SAP HANA TDI sertifikalı altyapı yığınında atanır. Sonuç olarak bir belirli ve ilgili kiracısında yalnızca tooa depolama sanal makineye atanan depolama birimleri erişilebilir. Ve hello farklı dağıtılan kiracılar arasında görünmez.
- Sunucu veya ana bilgisayar: bir sunucu veya konak birimi müşteriler veya kiracılar arasında paylaşılmaz. Bir sunucu veya ana bilgisayar tooa müşteri dağıtılan, tooone tek bir kiracı atanmış bir atomik tam işlem birimi. **Hayır** donanım bölümleme veya yumuşak bölümleme kullanılırsa, neden size, bir konak ya da bir sunucu paylaşımı ile başka bir müşteri, bir müşteri olarak. Merhaba belirli Kiracı toohello depolama sanal makineye atanan depolama birimlerin bağlı toosuch bir sunucu olduğundan. Bir kiracı farklı SKU'ları özel olarak atanmış bir toomany sunucu ölçü olabilir.
- Azure (büyük örneği) altyapısı damga üzerinde bir SAP HANA içinde birçok farklı kiracıların dağıtılır ve diğer karşı hello Kiracı kavramları ağ, depolama ve işlem düzeyinde aracılığıyla yalıtılmış. 


Desteklenen toorun SAP HANA yalnızca bu tam sunucu birimleridir. Microsoft Azure sanal makinelerinde Hello SAP uygulama katmanı veya iş yükü donanımlar orta katman çalışıyor. Merhaba altyapı Damgalar Hello SAP HANA (büyük örneği) Azure üzerinde çalışan Azure (büyük örneği) birimlerdeki SAP HANA ve Azure sanal makineler arasında düşük gecikme süresi bağlantısı sağlanan bağlı toohello Azure ağ omurgalarında, bu nedenle, birimleridir.

Bu belge SAP HANA (büyük örneği) azure'da hello konuyu ele beş belgeleri biridir. Bu belgede, hello temel mimari, sorumlulukları, sağlanan hizmetlere ve üst düzey hello çözümünün özelliklerinin aracılığıyla gidin. Merhaba alanlar, ağ ve bağlantısı gibi birçok ilgili hello diğer dört belge ayrıntıları kapsayan ve listeleri ayrıntıya gidin. SAP HANA (büyük örneği) azure'da Hello belgelerine SAP NetWeaver yükleme yönlerini ve Azure vm'lerinde SAP NetWeaver dağıtımları kapsamaz. Bu konu aynı hello bulunan ayrı belgelerinde ele belge kapsayıcısı. 


Bu kılavuzun Hello beş bölümü aşağıdaki konularda hello kapsar:

- [SAP HANA (büyük örneği) genel bakış ve Azure üzerinde mimarisi](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [SAP HANA (büyük örnekler) altyapısı ve Azure ile ilgili bağlantı](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [Nasıl tooinstall ve Azure üzerinde SAP HANA (büyük örnekler) yapılandırma](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [SAP HANA (büyük örnekler) yüksek kullanılabilirlik ve olağanüstü durum kurtarma Azure ile ilgili](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [SAP HANA (büyük örnekler) sorun giderme ve Azure üzerinde izleme](troubleshooting-monitoring.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="definitions"></a>Tanımlar

Birçok ortak tanımlara hello mimari ve teknik dağıtım kılavuzu yaygın olarak kullanılır. Not hello hüküm ve anlamlarını aşağıdaki:

- **Iaas:** hizmet olarak altyapı
- **PaaS:** hizmet olarak Platform
- **SaaS:** hizmet olarak yazılım
- **SAP bileşen:** ECC, bant genişliği, çözüm Yöneticisi veya EP'deki gibi tek bir SAP uygulama SAP bileşenleri geleneksel ABAP veya Java teknolojiler ya da olmayan-tabanlı NetWeaver uygulama iş nesneleri gibi temel alabilir.
- **SAP ortamı:** SAP bileşenlerden bir veya daha fazla mantıksal olarak gruplandırılmış tooperform geliştirme, QAS, eğitim, DR veya üretim gibi bir iş işlevi.
- **SAP yatay:** BT yatay toohello tüm SAP varlıkları başvuruyor. Merhaba SAP yatay tüm üretim ve üretim dışı ortamlar içerir.
- **SAP sistem:** hello DBMS katman ve uygulama katmanı SAP ERP geliştirme sistemi, SAP BW test sistemini, SAP CRM üretim sistem, vb. birleşimi. Azure dağıtımları, bu iki şirket içi ve Azure arasında bölünen desteklemez. Bir SAP sistemidir ya da dağıtılmış şirket içi veya Azure'de dağıtılan anlamına gelir. Ancak, Azure veya şirket içi SAP yatay hello farklı sistemlerini dağıtabilirsiniz. Örneğin, hello SAP CRM üretim sistem şirket içi dağıtırken, azure'da hello SAP CRM geliştirme ve test sistemleri dağıtabilirsiniz. Azure'da (büyük örnekler) SAP HANA için Azure VM'de SAP sistemlerinin hello SAP uygulama katmanı barındırmak ve hello HANA büyük örneği damga biriminde ilgili SAP HANA örneğinde hello yöneliktir.
- **Büyük örneği damga:** SAP HANA TDI olan bir donanım altyapı yığını sertifikalı ve ayrılmış Azure içindeki toorun SAP HANA örnekleri.
- **SAP HANA azure'da (büyük örnekler):** Azure toorun HANA örneklerinde SAP HANA büyük örneği Damgalar farklı Azure bölgelerinde dağıtılmış donanım sertifikalı TDI hello teklif resmi adı. Merhaba ilgili terim **HANA büyük örneği** azure'da (büyük örnekler) kısaltması SAP HANA ve yaygın olarak kullanılan bu teknik dağıtım kılavuzu.
- **Şirket içi:** VM'ler dağıtılan tooan siteden siteye, çok siteli veya ExpressRoute bağlantısı hello şirket içi inizdeki ve Azure arasında sahip Azure aboneliğinizin bulunduğu bir senaryoyu açıklar. Ortak Azure belgelerine dağıtımları bu tür şirket içi senaryoları açıklanmıştır. Merhaba hello bağlantı tooextend şirket içi etki alanları, şirket içi Active Directory/OpenLDAP ve DNS Azure'da şirket içi nedeni. Merhaba şirket içi yatay genişletilmiş toohello hello Azure aboneliklerinden Azure varlıkları olduğu. Bu uzantı, hello VM'ler hello şirket içi etki alanının parçası olabilir. Merhaba şirket içi etki alanının etki alanı kullanıcıları hello sunucularına erişebilir ve Hizmetleri üzerindeki VM'ler (DBMS Hizmetleri gibi) çalıştırabilirsiniz. Dağıtılan VM'ler şirket içi ve Azure dağıtılan VM'ler arasında iletişim ve ad çözümleme mümkündür. Böyle hangi çoğu SAP varlıklar dağıtılan hello tipik bir senaryodur. Merhaba kılavuzlardan bkz [planlama ve tasarım VPN ağ geçidi için](../../../vpn-gateway/vpn-gateway-plan-design.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ve [hello Azure portalını kullanarak siteden siteye bağlantısı olan bir VNet oluşturma](../../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) daha ayrıntılı bilgi için.
- **Kiracı:** HANA büyük örnekleri damga içinde dağıtılan bir müşteri bir "Kiracı." yalıtılmış Bir kiracı hello ağ, depolama ve bilgi işlem katmanını diğer kiracıdan yalıtılmış. Bu nedenle, atanan toohello farklı kiracıların birbirine bakın veya üzerinde hello birbirleri ile iletişim kurmak depolama ve işlem bu birimleri HANA büyük örneği damgasının düzeyi. Bir müşteri farklı kiracıların toohave dağıtımlarını seçebilir. Daha sonra hello HANA büyük örneği damga düzeyi kiracılar arasında iletişim yoktur.

Çeşitli Microsoft Azure genel bulut SAP iş yükünü dağıtma hello konuda yayımlanan ek kaynaklar vardır. Herkes planlama ve SAP HANA dağıtımını Azure'da yürütme deneyimli ve hello sorumluları, Azure Iaas ve Azure Iaas SAP iş yükünü hello dağıtımını önerilir. Merhaba aşağıdaki kaynakları daha fazla bilgi sağlar ve devam etmeden önce başvurulan:


- [Microsoft Azure sanal makinelerde SAP çözümleri kullanma](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="certification"></a>Sertifika

NetWeaver sertifika hello yanında SAP Azure Iaas gibi belirli altyapılar üzerinde SAP HANA toosupport SAP HANA için özel bir sertifika gerektirir.

Merhaba çekirdeği SAP Not NetWeaver ve tooa derece SAP HANA sertifika [SAP Not #1928533 – Azure SAP uygulamaları: desteklenen ürünler ve Azure VM türleri](https://launchpad.support.sap.com/#/notes/1928533).

Bu [SAP Not #2316233 - Microsoft azure'da (büyük örnekler) SAP HANA](https://launchpad.support.sap.com/#/notes/2316233/E) de önemlidir. Bu kılavuzda açıklanan hello çözüm kapsar. Ayrıca, desteklenen toorun hello GS5 VM Azure tür SAP HANA kullanılabilir. [Bu durumda bilgi hello SAP Web sitesinde yayımlanır](http://global.sap.com/community/ebook/2014-09-02-hana-hardware/enEN/iaas.html).

Hello Azure (büyük örnekler) çözüm üzerinde SAP HANA başvurulan tooin SAP Not #2316233 Microsoft sağlar ve SAP müşterileri hello özelliği toodeploy büyük SAP Business Suite, SAP Business Warehouse (BW), S/4 HANA, BW/4HANA veya Azure diğer SAP HANA iş yükleri. SAP HANA ayrılmış donanım damga sertifikalı hello üzerinde tabanlı Hello çözümün ([SAP HANA uyarlanmış Datacenter tümleştirmesi – TDI](https://scn.sap.com/docs/DOC-63140)). SAP HANA TDI çalışan yapılandırılmış çözümün tüm SAP HANA tabanlı uygulamalar (SAP Business Suite SAP HANA üzerinde SAP HANA, S4/HANA ve BW4/HANA SAP Business Warehouse (BW) dahil) üzerinde hello toowork kalacaklarını bilmesinin hello güvenirlik sağlar Donanım altyapısı.

Karşılaştırılan toorunning SAP HANA Azure Virtual Machines'de Bu çözüm bir avantajı vardır — kadar büyük bellek birimleri için sağlar. Bu çözüm tooenable istiyorsanız, bazı unsur toounderstand vardır:

- Merhaba SAP uygulama katmanı ve SAP olmayan uygulamaları, Azure sanal hello normal Azure donanım damga olarak barındırılan sanal makineler (VM'ler) çalıştırın.
- Müşteri altyapı, veri merkezleri, şirket içi ve uygulama dağıtımlarını bağlı toohello Microsoft Azure bulut Platformu (önerilen) Azure ExpressRoute aracılığıyla veya sanal özel ağ (VPN). Active Directory (AD) ve DNS ayrıca Azure'da genişletilmiş.
- SAP HANA (büyük örnekler) azure'da Hello SAP HANA veritabanı örneği HANA iş yükü için çalışır. Azure Vm'lerinde çalışan yazılımı hello HANA örneği HANA büyük durumlarda çalışma ile etkileşim kurabilmesi hello büyük örneği damga Azure ağ uygulamasına bağlandı.
- SAP HANA Azure (büyük örnekler) ile ilgili donanım SUSE Linux Enterprise Server ile hizmet (Iaas) olarak bir altyapıda sağlanan ayrılmış donanım veya Red Hat Enterprise Linux, önceden yüklü değil. Güncelleştirmeler ve Bakım toohello işletim sistemi Azure sanal makinelerle ilgili daha fazla sizin sorumluluğunuzdadır aynıdır.
- Tüm ilgili devam eden işlemler ve Azure üzerinde SAP HANA yönetimler olduğu gibidir, HANA veya HANA büyük örneklerinin birimlerdeki herhangi bir ek bileşeni gerekli toorun SAP HANA yüklemesi sizin sorumluluğunuzdadır kullanır.
- Ayrıca toohello çözümler, burada açıklanan Azure aboneliğinizdeki tooSAP HANA azure'da (büyük örnekler) bağlanan diğer bileşenleri yükleyebilirsiniz.  Örneğin, ile iletişim ve/veya doğrudan toohello SAP HANA veritabanına etkinleştirme bileşenleri (atlama sunucular, RDP sunucuları, SAP HANA Studio, SAP BI senaryoları için SAP veri hizmetleri veya izleme çözümü ağ).
- Azure olduğu gibi HANA büyük örnekleri destekleyen yüksek kullanılabilirlik ve olağanüstü durum kurtarma işlevleri sunar.

## <a name="architecture"></a>Mimari

Bir üst düzey, hello Azure (büyük örnekler) çözüm üzerinde SAP HANA bağlı olduğu aynı Azure bölgesindeki hello bir büyük örneği damgası bulunan SAP yapılandırılmış TDI donanımda bulunan Azure Vm'leri ve hello veritabanı katmanı bulunan hello SAP uygulama katman vardır Iaas tooAzure.

> [!NOTE]
> Toodeploy hello SAP uygulama hello katmanında ihtiyacınız hello SAP DBMS katmanı olarak aynı Azure bölgesi. Bu Azure üzerinde SAP iş yükü hakkında yayımlanan bilgi iyi belgelenmiş kuralıdır. 

Merhaba SAP HANA Azure (büyük örnekler) ile ilgili genel mimarisi bir SAP TDI sertifikalı donanım yapılandırması (sanallaştırılmamış, çıplak metal, hello SAP HANA veritabanı için yüksek performanslı sunucusu) hello özelliği ve Azure tooscale esnekliğini sağlar kaynakları hello için uygulama katmanı toomeet gereksinimlerinizi SAP.

![SAP HANA Azure (büyük örnekler) ile ilgili mimari genel bakış](./media/hana-overview-architecture/image1-architecture.png)

Merhaba mimarisi gösterilen üç bölümlere ayrılmıştır:

- **Sağ:** son LOB uygulamaları (örneğin, SAP) erişen kullanıcılar ile veri merkezlerinde farklı uygulamaları çalıştıran bir şirket içi altyapı. İdeal olarak, bu altyapı sonra bağlı şirket içi Azure ile tooAzure [ExpressRoute](https://azure.microsoft.com/services/expressroute/).

- **Merkezi:** gösterir Azure Iaas ve bu durumda, Azure Vm'leri toohost SAP veya SAP HANA DBMS sistem olarak kullanan diğer uygulamalar kullanın. Azure VM'ler hello hafızası işlevi sağlayan küçük HANA örnekleri Azure Vm'lerde kendi uygulama katmanı ile birlikte dağıtılır. Hakkında daha fazla bilgi bulmak [sanal makineleri](https://azure.microsoft.com/services/virtual-machines/).
<br />Azure sanal ağlar (Vnet'ler) diğer uygulamalara birlikte kullanılan toogroup SAP sistemleri Azure ağdır. Bu sanal ağlar tooSAP HANA azure'da (büyük örnekler) yanı sıra tooon içi sistemleri bağlayın.
<br />SAP NetWeaver uygulamaları ve veritabanlarını toorun Microsoft Azure'da desteklenen için bkz: [SAP destek Not #1928533 – Azure SAP uygulamaları: desteklenen ürünler ve Azure VM türleri](https://launchpad.support.sap.com/#/notes/1928533). Azure SAP çözümlerini dağıtma belgelerini gözden geçirin:

  -  [Windows sanal makinelerde (VM'ler) SAP kullanma](../../virtual-machines-windows-sap-get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
  -  [Microsoft Azure sanal makinelerde SAP çözümleri kullanma](get-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

- **Sol:** hello SAP HANA hello Azure büyük örneği damga donanımda sertifikalı TDI gösterir. Merhaba HANA büyük örneği bağlı toohello hello bağlantısını aynı teknolojiye içi Azure'da hello kullanarak aboneliğinizin Azure Vnet birimleridir.

Hello Azure büyük örneği damga kendisini bileşenleri aşağıdaki hello birleştirir:

- **Bilgi işlem:** hello gerekli hesaplama yeteneği sağlamak ve SAP HANA sertifikalı olan Intel Xeon E7-8890v3 veya Intel Xeon E7-8890v4 işlemcilerini esas alan sunucuları.
- **Ağ:** A birleşik hello bilgi işlem, depolama ve LAN bileşenleri bağlantılar yüksek hızlı ağ yapısı.
- **Depolama:** birleşik ağ yapısı erişilen bir depolama altyapısını. Belirli bir depolama kapasitesi ise hello bağlı olarak belirli SAP HANA Azure (büyük örnekler) yapılandırmasında dağıtılan sağlanan (daha fazla depolama kapasitesi ek bir aylık ücret kullanılabilir).

İçinde Hello çok kiracılı altyapı hello büyük örneği damga yalıtılmış Kiracı müşteriler dağıtılır. Merhaba Kiracı dağıtımı sırasında Azure kaydınızı içinde tooname bir Azure aboneliği gerekir. Bu devam eden toobe hello Azure aboneliği hello HANA büyük örnekler karşı faturalandırılır toobe geçiyor. Bu kiracılar 1:1 ilişki toohello Azure aboneliğine sahip. Ağ olası tooaccess HANA büyük örneği birim olduğu akıllıca toodifferent ait farklı Azure Vnet gelen bir Azure bölgesindeki bir kiracıdaki Azure abonelikleri dağıtıldı. Bu Azure abonelikleri toobelong toohello gerekiyor ancak aynı Azure kayıt. 

Azure vm'lerle gibi Azure (büyük örnekler) üzerinde SAP HANA birden çok Azure bölgelerinde sunulur. Sipariş toooffer olağanüstü durum kurtarma özellikleri tooopt de seçebilirsiniz. Bir siyasi coğrafi bölge içindeki farklı büyük örneği Damgalar diğer bağlı tooeach ' dir. Örneğin, HANA büyük örneği damgaları Batı ABD ve BİZE Doğu, DR çoğaltma hello amacı için adanmış ağ bağlantısı üzerinden bağlanır. 

Farklı VM türler ile Azure sanal makineler arasında yalnızca seçebileceğiniz gibi farklı SKU'ları, HANA büyük SAP HANA farklı iş yükü türleri için özel olarak hazırlanmış örnekleri arasından seçim yapabilirsiniz. SAP bellek tooprocessor yuva oranları hello Intel işlemci nesli üzerinde göre değişen iş yükleri için geçerlidir; sunulan dört farklı SKU türü vardır:

Temmuz 2017'ten itibaren SAP HANA Azure (büyük örnekler) ile ilgili çeşitli yapılandırmaları hello Azure bölgeleri, ABD Batı ABD Doğu, Avustralya Doğu, Avustralya Güneydoğu, Batı Avrupa ve Kuzey Avrupa kullanılabilir:

| SAP Çözümü | CPU | Bellek | Depolama | Kullanılabilirlik |
| --- | --- | --- | --- | --- |
| OLAP için en iyi duruma getirilmiş: SAP BW, BW/4HANA<br /> veya SAP HANA Genel OLAP iş yükü için | SAP HANA Azure S72 üzerinde<br /> – 2 x Intel® Xeon İşlemci E7 8890 v3<br /> 36 CPU çekirdekleri ve 72 CPU iş parçacıkları |  768 GB |  3 TB | Kullanılabilir |
| --- | SAP HANA Azure S144 üzerinde<br /> -4 x Intel® Xeon İşlemci E7 8890 v3<br /> 72 CPU çekirdekleri ve 144 CPU iş parçacıkları |  1,5 TB |  6 TB | Artık sunulmuyor |
| --- | SAP HANA Azure S192 üzerinde<br /> -4 x Intel® Xeon İşlemci E7 8890 v4<br /> 96 CPU çekirdekleri ve 192 CPU iş parçacıkları |  2.0 TB |  8 TB | Kullanılabilir |
| --- | SAP HANA Azure S384 üzerinde<br /> – 8 x Intel® Xeon İşlemci E7 8890 v4<br /> 192 CPU çekirdekleri ve 384 CPU iş parçacıkları |  4.0 TB |  16 TB | Hazır tooOrder |
| OLTP için en iyi duruma getirilmiş: SAP Business paketi<br /> SAP HANA veya S/4HANA (OLTP)<br /> Genel OLTP | SAP HANA Azure S72m üzerinde<br /> – 2 x Intel® Xeon İşlemci E7 8890 v3<br /> 36 CPU çekirdekleri ve 72 CPU iş parçacıkları |  1,5 TB |  6 TB | Kullanılabilir |
|---| SAP HANA Azure S144m üzerinde<br /> -4 x Intel® Xeon İşlemci E7 8890 v3<br /> 72 CPU çekirdekleri ve 144 CPU iş parçacıkları |  3.0 TB |  12 TB | Artık sunulmuyor |
|---| SAP HANA Azure S192m üzerinde<br /> -4 x Intel® Xeon İşlemci E7 8890 v4<br /> 96 CPU çekirdekleri ve 192 CPU iş parçacıkları  |  4.0 TB |  16 TB | Kullanılabilir |
|---| SAP HANA Azure S384m üzerinde<br /> – 8 x Intel® Xeon İşlemci E7 8890 v4<br /> 192 CPU çekirdekleri ve 384 CPU iş parçacıkları |  6.0 TB |  18 TB | Hazır tooOrder |
|---| SAP HANA Azure S384xm üzerinde<br /> – 8 x Intel® Xeon İşlemci E7 8890 v4<br /> 192 CPU çekirdekleri ve 384 CPU iş parçacıkları |  8.0 TB |  22 TB |  Hazır tooOrder |
|---| SAP HANA Azure S576 üzerinde<br /> – 12 x Intel® Xeon İşlemci E7 8890 v4<br /> 288 CPU çekirdekleri ve 576 CPU iş parçacıkları |  12.0 TB |  28 TB | Hazır tooOrder |
|---| SAP HANA Azure S768 üzerinde<br /> – 16 x Intel® Xeon İşlemci E7 8890 v4<br /> 384 CPU çekirdekleri ve 768 CPU iş parçacıkları |  16,0 TB |  36 TB | Hazır tooOrder |
|---| SAP HANA Azure S960 üzerinde<br /> – 20 x Intel® Xeon İşlemci E7 8890 v4<br /> 480 CPU çekirdekleri ve 960 CPU iş parçacıkları |  20.0 TB |  46 TB | Hazır tooOrder |

- CPU çekirdekleri = olmayan-hiper iş parçacıklı CPU çekirdekleri hello Sum hello sunucu biriminin hello işlemcilerin toplamı.
- CPU iş parçacıkları = hiper iş parçacıklı CPU çekirdekleri hello Sum hello sunucu biriminin hello işlemcilerin tarafından sağlanan işlem iş parçacıklarının toplamı. Tüm birimleri varsayılan toouse tarafından Hyper-Threading yapılandırılır.


Merhaba yukarıdaki kullanılabilir olan veya 'artık sunulmaz' farklı yapılandırmaları de başvurulan [SAP destek Not #2316233 – Microsoft azure'da (büyük örnekler) SAP HANA](https://launchpad.support.sap.com/#/notes/2316233/E). 'Hazır tooOrder' işaretlenmiş hello yapılandırmaları hello SAP Not giriş yakında bulur. Ancak, bu örnek SKU'ları zaten Merhaba altı farklı Azure bölgeleri hello HANA büyük örneği hizmetinin kullanılabilir sıralanabilir.

Seçilen hello belirli yapılandırmalar, iş yükü, CPU kaynaklarını ve istenen bellek bağımlıdır. OLTP iş yükü tooleverage hello OLAP iş yükü için en iyi duruma getirilir SKU'ları mümkündür. 

SAP HANA sertifikalı TDI Hello donanım tüm hello teklifleri için temel var. Ancak, biz hello SKU'ları içine böler donanımı, iki farklı sınıflar arasında ayrım:

- S72, S72m, S144, S144m, S192 ve tooas hello 'ı sınıf türü' adlandırdığımız S192m SKU.
- S384, S384m, S384xm, S576, S768 ve adlandırdığımız S960 tooas SKU ' Type II class' hello.

Tam HANA büyük örneği damga yalnızca tek bir müşteri &#39; ayrılmamış önemli toonote olan s kullanın. Bu bulgu Azure üzerinde de dağıtılan ağ yapısı bağlı işlem ve depolama kaynaklarını toohello raflarının geçerlidir. Azure gibi HANA büyük örnekleri altyapı, farklı müşteri dağıtır &quot;kiracılar&quot; birbirlerinden üç düzeyi aşağıdaki hello yalıtılmış olan:

- Ağ: Merhaba HANA büyük örneği damga içindeki sanal ağlar yalıtımı.
- Depolama: Depolama birimleri depolama sanal makinelerde yalıtımı atanan ve depolama birimleri kiracılar arasında yalıtır.
- İşlem: sunucu birimleri tooa tek Kiracı atamasının ayrılmış. Hayır sabit veya sunucu birimleri için yumuşak bölümleme. Hiçbir tek bir sunucu veya konak birimi kiracılar arasında paylaştırma. 

Bu nedenle, farklı kiracılar arasında HANA büyük örnekleri birimlerinin hello dağıtımları diğer görünür tooeach değildir. Ya da HANA büyük örneği farklı kiracılar dağıtılan birimleri birbirine hello HANA büyük örneği damga düzeyi ile doğrudan iletişim. Yalnızca HANA büyük örneği biriminde bulunan bir kiracı tooeach HANA büyük örneği damga düzeyi hello diğer iletişim kurabilir.
Dağıtılan hello büyük örneği damga Kiracı fatura akıllıca tooone Azure aboneliği atanır. Bununla birlikte, içinde başka Azure abonelikleri Azure Vnet'den erişilebilen ağ wise aynı Azure kayıt hello. Merhaba, başka bir Azure aboneliği ile aynı dağıtırsanız Azure bölgesini de seçebilirsiniz tooask için ayrılmış bir HANA büyük örneği Kiracı.

SAP HANA HANA büyük örnekleri ve SAP HANA Azure'de dağıtılan Azure vm'lerinde çalışan çalışan arasında önemli farklılıklar vardır:

- SAP HANA (büyük örnekler) azure'da yok sanallaştırma katmanı yoktur. Merhaba hello temel tam donanım performansını alın.
- Azure farklı olarak, Azure (büyük örnekler) sunucusunda hello SAP HANA ayrılmış tooa belirli bir müşteri ' dir. Bir sunucu birim veya ana bilgisayarın sabit veya geçici bölümlenmiş hiçbir olasılığı vardır. Sonuç olarak, HANA büyük örneği birimi tüm tooa Kiracı olarak ve o tooyou bir müşteri olarak atanmış olarak kullanılır. Bir yeniden başlatma veya kapatma hello sunucusunun otomatik olarak toohello işletim sistemi ve başka bir sunucu üzerinde dağıtılan SAP HANA neden olmaz. (Türü için SKU'ları sınıfı, bir sunucu sorunlarla karşılaşabilirsiniz ve yeniden dağıtım gereken başka bir sunucu üzerinde gerçekleştirilen toobe hello tek özel durumdur.)
- Burada ana bilgisayar İşlemci türleri için en iyi fiyat/performans oranı hello seçilir, Azure, SAP HANA azure'da (büyük örnekler) için seçilen hello İşlemci türleri olan hello yüksek hello Intel E7v3 ve E7v4 işlemci satırının gerçekleştirme.


### <a name="running-multiple-sap-hana-instances-on-one-hana-large-instance-unit"></a>Çalışan bir HANA büyük örneği biriminde birden çok SAP HANA örnekler
Merhaba HANA büyük örneği birimler bir etkin SAP HANA örneğinde birden çok olası toohost değil. Sırayla toostill depolama anlık görüntüleri hello özelliklerini sağlayın ve olağanüstü durum kurtarma, bu tür bir yapılandırma örneği bir birim gerektirir. Şimdi itibariyle hello HANA büyük örneği birimler gibi bölünmüştür:

- S72, S72m, S144, S192: En küçük 256 GB hello ile 256 GB artışlarla birim başlatılıyor. 256 GB, 512 GB ve vb. gibi farklı aralıklarla birleşik toohello maksimum hello belleğe hello birimi olabilir.
- S144m ve S192m: 512 GB hello en küçük birim ile 256 GB artışlarla. 512 GB, 768 GB ve vb. gibi farklı aralıklarla birleşik toohello maksimum hello belleğe hello birimi olabilir.
- Tür II sınıfı: hello birim 2 TB'lık başlangıç en küçük ile 512 GB artışlarla. 512 GB, 1 TB, 1, 5 TB ve vb. gibi farklı aralıklarla birleşik toohello maksimum hello belleğe hello birimi olabilir.

Birden çok SAP HANA örneği çalıştıran bazı örnekler gibi görünebilir:

| SKU | Bellek Boyutu | Depolama Boyutu | Birden çok veritabanı boyutlarıyla |
| --- | --- | --- | --- |
| S72 | 768 GB | 3 TB | 1 x 768 GB HANA örneği<br /> ya da 1 x 512 GB örneği + 1 x 256 GB örneği<br /> ya da 3 x 256 GB örnekleri | 
| S72m | 768 GB | 3 TB | 3x512GB HANA örnekleri<br />ya da 1 x 512 GB örneği + 1 adet 1 TB örneği<br />ya da 6 x 256 GB örnekleri<br />veya 1x1.5 TB örneği | 
| S192m | 4 TB | 16 TB | 8 x 512 GB örnekleri<br />veya 4 x 1 TB örnekleri<br />ya da 4 x 512 GB örnekleri + 2 x 1 TB örnekleri<br />ya da 4 x 768 GB örnekleri + 2 x 512 GB örnekleri<br />ya da 1 x 4 TB örneği |
| S384xm | 8 TB | 22 TB | 4 x 2 TB örnekleri<br />ya da 2 x 4 TB örnekleri<br />ya 2 x 3 TB örnekleri + 1 x 2 TB örnekleri<br />ya da 2x2.5 TB örnekleri + 1 x 3 TB örnekleri<br />ya da 1 x 8 TB örneği |


Merhaba fikir alın. Kesinlikle vardır diğer Çeşitleme de. 


## <a name="operations-model-and-responsibilities"></a>İşlem modeli ve sorumlulukları

SAP HANA azure'da (büyük örnekler) ile sağlanan hello hizmeti Azure Iaas Hizmetleri ile hizalanır. SAP HANA için en iyi duruma getirilmiş yüklü bir işletim sistemi HANA büyük örnekleri örnek alın. Sizin sorumluluğunuzdadır Azure Iaas Vm'leri hello HANA, yüklenmesi gereken ek yazılımı yükleme OS sağlamlaştırma hello görevleri çoğu işletim hello işletim sistemi ve HANA ve güncelleştirme hello işletim sistemi ve HANA aynıdır. Microsoft işletim sistemi güncelleştirmeleri veya HANA güncelleştirmeleri size zorlamaz.

![SAP HANA (büyük örnekler) azure'da sorumlulukları](./media/hana-overview-architecture/image2-responsibilities.png)

Yukarıdaki hello diyagramda görüldüğü gibi SAP HANA (büyük örnekler) azure'da çok kiracılı altyapı bir hizmet teklifidir. Ve sonuç olarak, sorumluluk hello bölme hello için hello OS altyapı sınır, çoğu parçasıdır. Microsoft, tüm yönlerini hello hizmet hello satır hello işletim sisteminin aşağıda sorumludur ve hello işletim sistemi dahil hello satır sorumludur. Bu nedenle uyumluluk, güvenlik, uygulama yönetimi, temel ve işletim sistemi yönetimi için en güncel şirket içi yöntemleri kullanan kullanılan toobe devam edebilirsiniz. Merhaba sistemleri ağınızdaki tüm gelince oldukları gibi görünür.

Ancak, burada Microsoft en iyi sonuçlar için toowork birlikte toouse hello temel altyapı özelliklerine ihtiyaç alanları olduklarından bu hizmet SAP HANA için optimize edilmiştir.

liste aşağıdaki hello her hello katmanların ve sorumluluklarınızın daha fazla ayrıntı sağlar:

**Ağ:** tüm iç ağlar için SAP HANA, kendi erişim toohello depolama hello örnekleri (için genişleme ve diğer işlevleri), bağlantı toohello yatay ve bağlantısını arasında bağlantı çalıştıran hello büyük örneği damga hello Merhaba SAP uygulama katmanı Azure sanal makinelerinde barındırıldığı tooAzure. Ayrıca, olağanüstü durum kurtarma amacıyla çoğaltma için Azure veri merkezleri arasında geniş ağ bağlantısı içerir. Tüm ağları hello Kiracı tarafından bölümlenir ve QOS uyguladığınız.

**Depolama:** hello sanallaştırılmış bölümlenmiş depolama anlık görüntüleri yanı sıra, hello SAP HANA sunucuları tarafından gerekli tüm birimler için. 

**Sunucular:** hello ayrılmış fiziksel sunucuları toorun hello SAP HANA tootenants atanan DBs. Merhaba hello ı sınıf türü sunucularının donanım soyutlanır SKU'lar. Bu sunucular türleriyle hello sunucu yapılandırması toplanır ve bir fiziksel donanım tooanother fiziksel donanımdan taşınabilir profilleri tutulur. Bu tür bir (el ile) taşıma profil işlemler biraz karşılaştırılabilir tooAzure hizmet iyileştirme. Merhaba Hello sunucularının, böyle bir özellik türü II sınıfı SKU'ları sunulmamaktadır.

**SDDC:** kullanılan toomanage veri hello yönetim yazılımı, yazılım tanımlı varlıklar merkezleri. Ölçek, kullanılabilirlik ve performansı artırmak için Microsoft toopool kaynaklar sağlar.

**İşletim sistemi:** (SUSE Linux veya Red Hat Linux) seçtiğiniz işletim sistemi hello hello sunucularda çalışır. SAP HANA çalışan hello amaçla hello tek tek Linux satıcı tooMicrosoft tarafından sağlanan hello görüntüleri hello işletim sistemi görüntüleri, sağladığınız bağımsızdır. Gerekli toohave hello Linux satıcısı hello belirli SAP HANA iyileştirilmiş görüntüsü için bir abonelik var. Sizin Sorumluluklarınız hello OS satıcıyla hello görüntüleri kaydetme içerir. Microsoft tarafından handover Hello noktasından ayrıca herhangi başka hello Linux işletim sistemi düzeltme eki uygulama için sorumluluğu size aittir. Bu aynı zamanda düzeltme başarılı bir SAP HANA yüklemesi için gerekli olabilecek ek paketler içerir (tooSAP'ın HANA yükleme belgelerini ve SAP notlara bakın) ve hangi dahil edilmedi kendi SAP HANA hello belirli Linux satıcı tarafından en iyi duruma getirilmiş işletim sistemi görüntüsü. ilgili toomalfunction/iyileştirme hello işletim sistemi ve sürücüleri ilgili toohello belirli sunucu donanımını olan Merhaba işletim sistemi düzeltme eki uygulama hello müşteri Hello sorumluluğu da içerir. Veya tüm güvenlik veya işletim sistemi Merhaba işlevsel düzeltme eki uygulama. Müşteri'nin sorumluluğu da izleme ve kapasite planlamasına ait:

- CPU kaynak tüketimi
- Bellek tüketimi
- Disk birimleri ilgili toofree alanı, IOPS ve gecikme süresi
- HANA büyük örneği ve SAP uygulama katmanı arasındaki ağ birim trafiği

Merhaba altyapının HANA büyük örneklerinin yedekleme ve geri yükleme hello işletim sistemi birimi için işlevsellik sağlar. Bu işlevselliği de sizin sorumluluğunuzdadır kullanmaktır.

**Ara yazılım:** SAP HANA örneği, öncelikle hello. Yönetim, işlemleri ve izleme sizin sorumluluğunuzdadır. Yedekleme/geri yükleme ve olağanüstü durum kurtarma amacıyla toouse depolama anlık görüntüleri sağlayan sağlanan işlevi yoktur. Bu özellikler hello altyapısı tarafından sağlanır. Ancak, sizin Sorumluluklarınız bu özellikler sayesinde yüksek kullanılabilirlik ve olağanüstü durum kurtarma tasarımı, bunları yararlanan ve depolama anlık görüntüleri başarıyla çalıştırılıncaya izleme içerir.

**Veri:** SAP HANA tarafından yönetilen, verilerinizi ve yedekleme gibi diğer verilerin birimlerde bulunan dosya veya dosya paylaşımları. Sizin Sorumluluklarınız boş disk alanı izleme ve hello birimleri Merhaba içeriğine yönetme ve hello aktarılmadığı disk birimleri ve depolama anlık görüntüleri yedeklerini izleme içerir. Ancak, veri çoğaltma tooDR siteleri aktarılmadığı hello Microsoft sorumluluğundadır.

**Uygulamalar:** SAP uygulama örnekleri hello veya SAP olmayan uygulamalar, bu uygulamaların hello uygulama katmanı durumunda. Sizin Sorumluluklarınız dahil dağıtım, yönetim, operations ve bu uygulamaları izleme ilgili CPU kaynak kullanımı, bellek tüketimi, Azure depolama alanı tüketimi ve ağ bant genişliği tüketimi içinde toocapacity planlama Azure sanal ağlar ve Azure Vnet'ler tooSAP HANA azure'da (büyük örnekler).

**WAN:** hello kurmak iş yükleri için şirket içi tooAzure dağıtımlarından bağlantıları. Tüm müşterilerimizin HANA büyük örneğiyle Azure ExpressRoute bağlantısı kullanın. Bu bağlantı için bu bağlantının hello Kurulum sorumlu şekilde hello SAP HANA Azure (büyük örnekler) çözüm üzerinde bir parçası değil.

**Arşiv:** depolama hesaplarında kendi yöntemlerini kullanarak verileri tooarchive kopyalarını tercih edebilirsiniz. Arşivleme yönetimi, uyumluluk, maliyetleri ve işlemler gerektirir. Arşiv kopyalar ve Azure üzerinde yedeklemeler oluşturmak ve bunları uyumlu bir biçimde saklamak için sorumlu.

Merhaba bkz [azure'da (büyük örnekler) SAP HANA SLA](https://azure.microsoft.com/support/legal/sla/sap-hana-large/v1_0/).

## <a name="sizing"></a>Boyutlandırma

Boyutlandırma HANA büyük örnekleri için HANA için genel boyutlandırma daha farklı değildir. Mevcut ve sistemler, dağıtılan diğer RDBMS tooHANA gelen toomove istediğiniz, SAP, varolan SAP sistemleri üzerinde çalışan rapor sayısı sağlar. Merhaba veritabanı taşınan tooHANA ise, bu raporları hello veri denetleyin ve hello HANA örneği için bellek gereksinimleri hesaplayın. SAP notları tooget aşağıdaki hello nasıl toorun bu raporları hakkında daha fazla bilgi okuyun ve nasıl tooobtain en son düzeltme eklerinin/sürümlerine:

- [SAP Not #1793345 - HANA üzerinde SAP paketi için boyutlandırma](https://launchpad.support.sap.com/#/notes/1793345)
- [Not #1872170 - Suite HANA ve S/4 HANA boyutlandırma rapor SAP](https://launchpad.support.sap.com/#/notes/1872170)
- [SAP Not #2121330 - SSS: SAP BW rapor boyutlandırma HANA üzerinde](https://launchpad.support.sap.com/#/notes/2121330)
- [Not #1736976 - HANA boyutlandırma rapor BW için SAP](https://launchpad.support.sap.com/#/notes/1736976)
- [HANA üzerinde BW için Not #2296290 - yeni boyutlandırma rapor SAP](https://launchpad.support.sap.com/#/notes/2296290)

Yeşil alan uygulamaları için SAP hızlı Boyutlandırıcı SAP HANA üstünde yazılım hello uygulaması kullanılabilir toocalculate bellek gereksinimlerini ' dir.

Veri birimi büyüdükçe HANA yönelik bellek gereksinimleri artmaktadır, böylece toobe şimdi hello bellek tüketimi farkında istediğiniz ve devam eden toobe nedir mümkün toopredict olması gelecekteki hello. Merhaba bellek gereksinimlerine bağlı olarak, ardından, isteğe bağlı hello HANA büyük örneği SKU'ları, birine eşleyebilirsiniz.

## <a name="requirements"></a>Gereksinimler

Bu liste, SAP HANA (büyük örnekler) Azure üzerinde çalıştırmak için gereksinimler derler.

**Microsoft Azure:**

- Bağlantılı tooSAP HANA Azure (büyük örnekler) ile ilgili olabilir bir Azure aboneliği.
- Microsoft Premier Destek sözleşmenizi. Bkz: [SAP destek Not #2015553 – Microsoft Azure üzerinde SAP: Destek Önkoşullar](https://launchpad.support.sap.com/#/notes/2015553) ayrıntılı bilgi için ilgili toorunning SAP Azure içinde. HANA büyük örneği birimleri 384 ve daha fazla CPU ile kullanarak, tooextend hello Premier Destek sözleşmesi tooinclude Azure hızlı yanıt (ARR) da gerekir.
- Tanıma hello HANA büyük örneklerinin SAP ile SKU bir boyutlandırma gerçekleştirildikten sonra uygulamanız.

**Ağ bağlantısı:**

- Şirket içi tooAzure arasında Azure ExpressRoute: tooconnect, şirket içi veri merkezi tooAzure yapma emin tooorder en az 1 GB/sn arasında bağlantı ISS. 

**İşletim Sistemi:**

- SUSE Linux Enterprise Server 12 SAP uygulamaları için lisans.

> [!NOTE] 
> Merhaba Microsoft tarafından sunulan işletim sistemi ile SUSE kayıtlı değil ya da bir SMT örneği ile bağlı.

- SUSE Linux Abonelik Yönetim Aracı (Azure VM'de azure'da dağıtılan SMT). Bu hello özelliği için SAP HANA kayıtlı ve (olduğundan HANA büyük örnekleri veri merkezi içinde Internet erişimi yok) tarafından SUSE sırasıyla güncelleştirilen Azure (büyük örnekler) toobe sağlar. 
- Red Hat Enterprise Linux 6.7 veya 7.2 SAP HANA için için lisans.

> [!NOTE]
> Merhaba Microsoft tarafından sunulan işletim sistemi ile Red Hat kayıtlı değil veya bağlı BT tooa Red Hat Abonelik Yöneticisi örneği değil.

- Red Hat Abonelik Yöneticisi Azure bir Azure VM üzerinde dağıtılabilir. Merhaba Red Hat Abonelik Yöneticisi hello özelliği için SAP HANA kayıtlı ve hiçbir doğrudan internet içinden erişim hello Azure büyük örneği damgası üzerinde dağıtılan hello Kiracı (olduğu gibi) tarafından Red Hat sırasıyla güncelleştirilen Azure (büyük örnekler) toobe sağlar.
- SAP destek sözleşme Linux sağlayıcınız ile de toohave gerektirir. Bu gereksinim HANA büyük örneği veya hello olgu hello çözümü tarafından silinmeyen, azure'da çalışma, Linux. Farklı olarak bazı hello Linux Azure galeri görüntüleri hello Hizmet ücreti HANA büyük örneklerinin çözüm teklif hello dahil edilmez. Bu, bir müşteri toofulfill hello gereksinimleriyle SAP destek sözleşmeleri ilgili hello Linux dağıtıcı gibidir.   
   - SUSE Linux için destek gereksinimlerini sözleşme hello aramak [SAP Not #1984787 - SUSE LINUX Enterprise Server 12: yükleme notları](https://launchpad.support.sap.com/#/notes/1984787) ve [SAP Not #1056161 - SUSE öncelik SAP uygulamalarıdesteğini](https://launchpad.support.sap.com/#/notes/1056161).
   - Red Hat Linux için destek ve hizmet (toohello işletim sistemleri HANA büyük örneklerinin güncelleştirir. dahil toohave hello doğru abonelik düzeylerini gerekir Red Hat "RHEL için SAP Business uygulamaları" abonelik alma önerir. Destek Hizmetleri ile ilgili, denetleyip [SAP Not #2002167 - Red Hat Enterprise Linux 7.x: yükleme ve yükseltme](https://launchpad.support.sap.com/#/notes/2002167) ve [SAP Not #1496410 - Red Hat Enterprise Linux 6.x: yükleme ve yükseltme](https://launchpad.support.sap.com/#/notes/1496410) için Ayrıntıları.

**Veritabanı:**

- Lisansları ve SAP HANA (platform veya enterprise edition) için yazılım yükleme bileşenleri.

**Uygulamalar:**

- Lisansları ve yazılım yükleme bileşenleri tooSAP HANA bağlanma ve SAP ilgili tüm SAP uygulamaları için sözleşmeleri destekler.
- Lisansları ve tüm SAP olmayan uygulamalar için yazılım yükleme bileşenleri ilişkisi tooSAP HANA Azure (büyük örnekler) ortamında kullanılan ve destek sözleşmeleri ilgili.

**Yetenekler:**

- Deneyimi ve Azure Iaas ve bileşenleri hakkında bilgi.
- Deneyimi ve Azure SAP iş yükü dağıtma hakkında bilgi.
- SAP HANA yükleme kişisel onaylandı.
- Mimarı becerileri toodesign yüksek kullanılabilirlik ve olağanüstü durum kurtarma SAP HANA geçici SAP.

**SAP:**

- Beklenir bir SAP müşterisiyseniz ve bir desteğine sahip SAP ile sözleşme
- Merhaba HANA büyük örneği SKU'ları türü II sınıfı üzerinde özellikle uygulamaları için SAP HANA ve büyük ölçekli büyütme donanımda nihai yapılandırmaları sürümlerinde SAP ile tooconsult önemle önerilir.


## <a name="storage"></a>Depolama

Merhaba SAP HANA azure'da (büyük örnekler) için depolama düzeni SAP HANA hello belgelenen yönergeler, önerilen SAP aracılığıyla Azure Hizmet Yönetimi tarafından yapılandırılan [SAP HANA depolama gereksinimleri](http://go.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) teknik incelemesi.

Merhaba HANA büyük örneklerini hello ı sınıf türü dört kez hello bellek birimle depolama birimi olarak gelir. Merhaba türü HANA büyük örneği birimleri II sınıfının hello depolama toobe daha dört kez geçiyor değil. Merhaba birimleri HANA işlem günlüğü yedeklemeleri depolamak için amaçlanan bir birim gelir. Daha ayrıntılı olarak Bul [nasıl tooinstall ve Azure üzerinde SAP HANA (büyük örnekler) yapılandırma](hana-installation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Aşağıdaki tablonun depolama ayırma bakımından hello bakın. Merhaba tablo hello kapasite hello farklı HANA büyük örneği birimleri ile sağlanan hello farklı birimler için kabaca listeler.

| HANA büyük örneği SKU | hana/veri | hana/günlük | hana ve paylaşılan | Günlük/hana/yedekleme |
| --- | --- | --- | --- | --- |
| S72 | 1280 GB | 512 GB | 768 GB | 512 GB |
| S72m | 3328 GB | 768 GB |1280 GB | 768 GB |
| S192 | 4608 GB | 1024 GB | 1536 GB | 1024 GB |
| S192m | 11,520 GB | 1536 GB | 1792 GB | 1536 GB |
| S384 | 11,520 GB | 1536 GB | 1792 GB | 1536 GB |
| S384m | 12.000 GB | 2050 GB | 2050 GB | 2040 GB |
| S384xm | 16.000 GB | 2050 GB | 2050 GB | 2040 GB |
| S576 | 20.000 GB | 3100 GB | 2050 GB | 3100 GB |
| S768 | 28,000 GB | 3100 GB | 2050 GB | 3100 GB |
| S960 | 36,000 GB | 4100 GB | 2050 GB | 4100 GB |


Gerçek Dağıtılmış birimler dağıtım ve kullanılan tooshow hello birim boyutlarını aracını biraz göre farklılık gösterebilir.

HANA büyük örneği SKU ayırabilir, birkaç olası bölme parça örnekleri gibi görünür:

| GB bellek bölümü | hana/veri | hana/günlük | hana ve paylaşılan | Günlük/hana/yedekleme |
| --- | --- | --- | --- | --- |
| 256 | 400 GB | 160 GB | 304 GB | 160 GB |
| 512 | 768 GB | 384 GB | 512 GB | 384 GB |
| 768 | 1280 GB | 512 GB | 768 GB | 512 GB |
| 1024 | 1792 GB | 640 GB | 1024 GB | 640 GB |
| 1536 | 3328 GB | 768 GB | 1280 GB | 768 GB |


Araçlar toolook hello birimlerinin kullanılan ve biraz dağıtımda göre değişebilir kaba birim numaralarını bu boyutlarıdır. Ayrıca diğer bölüm boyutu vardır gibi 2,5 TB thinkable. Bu depolama boyutları olarak kullanılan yukarıdaki hello bölümler için benzer bir formülü olan hesaplanır. Merhaba terim 'partitions' hello işletim sistemi, bellek veya CPU kaynaklarını herhangi bir şekilde bölümlenir göstermez. HANA büyük örneği birim toodeploy birinde isteyebilirsiniz hello farklı HANA örnekleri tek için yalnızca depolama bölümleri gösterir. 

Bir müşteri olabilir gibi daha fazla depolama alanı için gerekir, 1 TB birimlerinde hello olasılığı tooadd depolama toopurchase ek depolama alanı gerekir. Bu ek depolama alanı ek bir birim eklenebilir veya bir veya daha fazla hello var olan birimler, kullanılan tooextend olabilir. Şu olası toodecrease hello boyutları hello birimlerin ilk olarak dağıtılan ve genellikle yukarıdaki hello tablo tarafından belirtildiği gibi değil. Bu da olası toochange hello adları hello birimlerin veya takma adlar değil. Merhaba depolama birimleri yukarıda açıklandığı gibi ekli toohello HANA büyük örneği NFS4 birimler olarak birimleridir.

Bir müşteri olarak toouse depolama anlık görüntüleri yedekleme/geri yükleme ve olağanüstü durum kurtarma amacıyla tercih edebilirsiniz. Bu konu hakkında daha fazla ayrıntı ayrıntıları [SAP HANA (büyük örnekler) yüksek kullanılabilirlik ve olağanüstü durum kurtarma Azure üzerinde](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="encryption-of-data-at-rest"></a>Bekleyen verilerin şifrelenmesi
Merhaba disklerinde depolanan gibi hello depolama HANA büyük örnekleri için kullanılan hello veri saydam bir şifreleme sağlar. HANA büyük örneği birim dağıtım sırasında bu tür bir şifreleme etkin hello seçeneği toohave sahip. Ayrıca zaten hello dağıtımdan sonra tooencrypted birimleri toochange da tercih edebilirsiniz. şifrelenmemiş tooencrypted birimlerden Hello taşıma saydamdır ve bir kapalı kalma süresi gerektirmez. 

Merhaba SKU'ları, LUN üzerinde depolanan hello birim hello önyükleme sınıf türü ile şifrelenir. Merhaba türü II sınıf örneklerinin SKU'ları, HANA büyük olması durumunda, işletim sistemi yöntemleriyle tooencrypt hello önyükleme LUN gerekir. 


## <a name="networking"></a>Ağ

Azure ağ Hello mimarisi, SAP uygulamaları HANA büyük örneklerinde anahtar bileşeni toosuccessful dağıtımıdır. Genellikle, Azure (büyük örnekler) dağıtımlarda SAP HANA veritabanları, CPU kaynak kullanımı ve bellek kullanımı çeşitli boyutlarda birkaç farklı SAP çözümleriyle birlikte daha büyük bir SAP yatay vardır. Büyük olasılıkla SAP yatay büyük olasılıkla kullanan bir karma olacak şekilde bu SAP sistemleri tüm SAP HANA üzerinde temel alır:

- SAP sistemleri şirket içinde dağıtılabilir. Tootheir boyutları bu sistemler şu anda Azure'da barındırılamaz; Klasik bir örnek Microsoft SQL daha fazla CPU gerektiren sunucusunda (Merhaba veritabanı) olarak çalışan bir üretim SAP ERP sistemi olabilir veya bellek kaynakları Azure VM'ler sağlayabilir.
- SAP HANA tabanlı SAP sistemleri şirket içi dağıtıldı.
- Azure vm'lerinde dağıtılan SAP sistemleri. Sınama, korumalı alan, geliştirme, bu sistemler olabilir veya üretim (vm'lerinde), kaynak kullanımı ve bellek talebe göre azure'da başarıyla dağıtabilirsiniz hello SAP NetWeaver tabanlı uygulamalardan herhangi biri için örnekler. Bu sistemler de veritabanlarını SQL Server gibi temel alabilir (bkz [SAP destek Not #1928533 – Azure SAP uygulamaları: desteklenen ürünler ve Azure VM türleri](https://launchpad.support.sap.com/#/notes/1928533/E)) veya SAP HANA (bkz [SAP HANA sertifikalı Iaas platformları](http://global.sap.com/community/ebook/2014-09-02-hana-hardware/enEN/iaas.html)).
- SAP HANA (büyük örneği) azure'da Azure büyük örneği Damgalar yararlanan SAP uygulama sunucuları (VM'ler üzerinde) azure'da dağıtılabilir.

Karma (ile dört veya daha fazla farklı dağıtım senaryolarında) SAP yatay tipik olsa da, Azure'da çalışan tam SAP yatay, birçok müşteri durumlar vardır. Microsoft Azure sanal makineleri daha güçlü gelmektedir gibi Azure üzerinde tüm SAP çözümleri taşıma müşteriler hello sayısını artırma.

SAP sistemleri Azure'de dağıtılan hello bağlamında ağ azure karmaşık değil. İlkeler aşağıdaki hello üzerinde dayanır:

- Azure sanal ağlar (Vnet'ler) tooon içi ağına bağlanır bağlı toobe toohello Azure expressroute bağlantı hattı gerekir.
- Şirket içi tooAzure bağlamak, genellikle bir expressroute bağlantı hattı 1 GB/sn veya daha yüksek bant genişliği olması gerekir. Bu en düşük bant genişliği, şirket içi sistemleri ve Azure sanal makinelerini (yanı sıra bağlantı tooAzure sistemler son kullanıcılar şirket içi) üzerinde çalışan sistemleri arasında veri aktarmak için yeterli bant genişliği sağlar.
- Azure sanal ağlar toocommunicate birbirleriyle içinde Azure gerek toobe tüm SAP sistemlerinde ayarlayın.
- Active Directory ve DNS barındırılan şirket içi Azure ExpressRoute aracılığıyla uygulamasına genişletilmiş.


> [!NOTE] 
> Açısından bir fatura, yalnızca tek bir Azure aboneliği yalnızca tooone tek Kiracı büyük örneği damgasında belirli bir Azure bölgesindeki bağlanabilir ve buna karşılık tek bir büyük örneği damga Kiracı yalnızca tooone Azure aboneliğine bağlı olabilir. Bu bulgu değil farklı tooany Faturalanabilir diğer Azure nesnedir

SAP HANA birden çok farklı Azure bölgelerinde (büyük örnekler) azure'da dağıtımı, ayrı Kiracı toobe sonuçlarında büyük örneği damga hello dağıtıldı. Hem hello altında Çalıştır ancak bu örnekler hello parçası olduğu sürece aynı Azure aboneliğinden aynı SAP yatay. 

> [!IMPORTANT] 
> Yalnızca Azure kaynak yönetimi dağıtımı, SAP HANA azure'da (büyük örnekler) ile desteklenir.

 

### <a name="additional-azure-vnet-information"></a>Ek Azure VNet bilgi

Sipariş tooconnect Azure VNet tooExpressRoute'da, Azure bir ağ geçidi oluşturulmalıdır (bkz [ExpressRoute için sanal ağ geçitleri hakkında](../../../expressroute/expressroute-about-virtual-network-gateways.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Azure bir ağ geçidi kullanılabilir ya da Azure (veya tooan Azure büyük örneği damga) dışında ExpressRoute tooan altyapısıyla ya da Azure sanal ağlar arasında tooconnect (bkz [PowerShell kullanarak kaynak yöneticisi için VNet-VNet bağlantı yapılandırma ](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Bu bağlantılar farklı MS Kurumsal kenarları (MSEE) yönlendiricilerden gelen sürece hello Azure ağ geçidi tooa en fazla dört farklı ExpressRoute bağlantıları bağlanabilir.  Daha fazla bilgi için bkz: [SAP HANA (büyük örnekler) altyapısı ve Azure ile ilgili bağlantı](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

> [!NOTE] 
> her ikisi de kullanım için hello Azure bir ağ geçidi sağlar verimlilik farklıdır (bkz [VPN Gateway hakkında](../../../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). bir sanal ağ geçidi ile elde edebilirsiniz hello en yüksek verimlilik 10 GB/sn bir ExpressRoute bağlantı kullanarak, ' dir. Göz önünde bulundurmanız Azure VNet ve bir sistemde bulunan bir Azure VM arasında dosya kopyalama (tek bir kopya akış olarak) şirket içi olduğunu hello hello farklı ağ geçidi SKU'ları tam verimini elde değil. hello sanal ağ geçidinin tooleverage hello tam bant, tek bir dosyayı paralel akış birden çok akışları veya kopya farklı dosyalarını kullanmalısınız.


### <a name="networking-architecture-for-hana-large-instances"></a>HANA büyük örnekleri için ağ mimarisi
Mimari HANA büyük örnekleri için ağ hello aşağıda gösterildiği gibi dört farklı bölümlerinde ayrılabilir:

- Şirket içi ağ ve ExpressRoute bağlantı tooAzure. Bu, hello müşteriler etki alanı ve ExpressRoute aracılığıyla bağlanan tooAzure parçasıdır. Bu hello'hello sağ alt köşesindeki hello grafik aşağıdaki parçasıdır.
- Azure ağı olarak kısaca yukarıda yeniden ağ geçidine sahip Azure Vnet ile açıklanan. Bu, uygulama gereksinimleri, güvenlik ve uyumluluk gereksinimlerini toofind hello uygun tasarımları gereken yeri bir alandır. HANA büyük örnekleri kullanılarak başka bir sanal ağlar ve Azure ağ geçidi SKU'ları toochoose sayısı bakımından göz önünde bulundurarak noktasıdır. Bu hello'hello sağ üst köşesinde, hello grafik bir parçasıdır.
- Azure içine ExpressRoute teknolojisi aracılığıyla bağlantı HANA büyük örnekleri. Bu bölümü dağıtılan ve Microsoft tarafından işlenir. Tek bir müşteri tooprovide bazı IP adres aralıklarını ise ve HANA büyük örnekleri bağlanmada varlıklarınızın hello dağıtımdan sonra ExpressRoute hello gibi toodo ihtiyacınız toohello Azure VNet(s) hattı (bkz [SAP HANA (büyük örnekler) altyapısı ve Azure ile ilgili bağlantı](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). 
- HANA büyük durumlarda ağ, hangi çoğunlukla bir müşteri olarak sizin için saydamdır.

![Azure sanal ağı tooSAP Azure (büyük örnekler) ve şirket içi HANA bağlı](./media/hana-overview-architecture/image3-on-premises-infrastructure.png)

Merhaba olgu HANA büyük örnekleri kullanın hello gereksinim tooget ExpressRoute tooAzure şirket içi varlıklarınızı bağlı değiştirmez. Ayrıca HANA büyük örneği birimlerinde barındırılan toohello HANA örnekleri bağlayan hangi ana hello uygulama katmanı hello Azure sanal makinelerini çalıştıran bir veya birden çok sanal ağlara sahip hello gereksinim değiştirmez. 

Merhaba fark tooSAP dağıtımlarda saf Azure, gelen hello bulguları ile:

- Merhaba HANA büyük örneği birimleri müşteri kiracınızın, Azure VNet(s) başka bir expressroute bağlantı hattı bağlanır. Sipariş tooseparate yük koşullarında sanal ağlar ExpressRoute bağlantıları ve Azure sanal ağlar ve HANA büyük örnekleri arasında bağlantılar paylaşmıyor hello şirket içi tooAzure hello aynı yönlendiriciler.
- Hello iş yükü hello SAP uygulama katmanı ve hello HANA örneği arasında çok sayıda küçük istekleri farklı yapısını profilidir ve veri gibi veri bloğu (sonuç kümeleri) SAP HANA hello uygulama katmanına içe aktarır.
- Merhaba SAP uygulama mimarisi burada veri şirket içi ve Azure arasında alınıp tipik senaryolar daha fazla hassas toonetwork gecikme olur.
- Merhaba VNet ağ geçidi en az iki ExpressRoute bağlantısı olan ve hello hello sanal ağ geçidinin gelen veriler için en yüksek bant genişliği hem bağlantılarını paylaşın.

Merhaba ağ gecikmesi Azure Vm'leri ve HANA büyük örneği birimleri arasında deneyimli bir tipik VM VM ağ gidiş dönüş gecikmesi yüksek olabilir. Hello Azure bölgesi bağımlı, hello değerleri ölçülen ortalama olarak aşağıda sınıflandırılmış hello 0.7 gidiş dönüş gecikme (ms) da aşabilir [SAP Not #1100926 - SSS: ağ performansı](https://launchpad.support.sap.com/#/notes/1100926/E). Yine de müşteriler SAP HANA tabanlı üretim SAP uygulamaları SAP HANA büyük örnekleri üzerinde çok başarıyla dağıtıldı. dağıtılan hello müşteriler, SAP HANA HANA büyük örneği birimlerini kullanarak SAP uygulamalarını çalıştırarak harika geliştirmeleri bildirdi. Yine de İş süreçlerinizi Azure HANA büyük durumlarda sınamanız gerekir.
 
Sipariş tooprovide belirleyici ağ gecikmesini Azure Vm'lerde HANA büyük örneği arasında hello seçimine hello Azure VNet ağ geçidi SKU'su gereklidir. Şirket içi ve Azure VM'ler arasında Hello trafik düzenlerini hello trafiği düzeni Azure Vm'leri ve HANA büyük örnekleri arasında küçük ancak yüksek WINS'e isteklerinin ve aktarılan veri birimleri toobe geliştirebilirsiniz. Sipariş toohave de işlenmiş gibi WINS'e hello UltraPerformance ağ geçidi SKU'su hello kullanımını öneririz. Merhaba HANA büyük örneği SKU'ları türü II sınıfının hello UltraPerformance ağ geçidi SKU'su Azure VNet ağ geçidi olarak hello kullanımını zorunludur.  

> [!IMPORTANT] 
> Hello hello SAP uygulama ve veritabanı katmanları arasındaki genel ağ trafiğini yalnızca HighPerformance hello veya UltraPerformance ağ geçidi SKU'ları sanal ağlar için tooSAP HANA azure'da (büyük örnekler) bağlamak için desteklenir. Tür II SKU'ları HANA büyük örneği için yalnızca hello UltraPerformance ağ geçidi SKU'su Azure VNet ağ geçidi olarak desteklenir.



### <a name="single-sap-system"></a>Tek SAP sistem

Yukarıda gösterilen hello şirket içi altyapı Azure'a ExpressRoute aracılığıyla bağlı ve hello expressroute bağlantı hattı bağlayan bir Microsoft Enterprise sınır yönlendiricisi (MSEE) içine (bkz [ExpressRoute teknik genel bakış](../../../expressroute/expressroute-introduction.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). Sonra oluşturulan, bu rota hello Microsoft Azure omurga bağlanır ve tüm Azure bölgeleri erişilebilir.

> [!NOTE] 
> SAP Windows'un Azure'da çalışan için toohello MSEE yakın toohello hello SAP yatay Azure bölgesinde bağlayın. Azure büyük örneği Damgalar ayrılmış MSEE aygıtları toominimize ağ gecikmesi Azure Vm'lerinde Azure Iaas ve büyük örnek Damgalar arasında üzerinden bağlanır.

Merhaba hello Azure VM'ler, SAP uygulama örnekleri, barındırma için sanal ağ geçidi bağlı toothat expressroute bağlantı hattı ve hello aynı Vnet'i bağlı tooa ayrı MSEE ayrılmış yönlendirici tooconnecting tooLarge örneği Damgalar.

Bu, burada hello SAP uygulama katmanı Azure üzerinde barındırılan ve hello SAP HANA veritabanına SAP HANA azure'da (büyük örnekler) üzerinde çalışan tek bir SAP sisteminin basit bir örnektir. Bu hello VNet ağ geçidi bant genişliği 2 GB/sn Hello varsayılır veya 10 GB/sn üretilen iş bir performans sorunu temsil etmiyor.

### <a name="multiple-sap-systems-or-large-sap-systems"></a>Birden çok SAP sistemleri veya büyük SAP sistemleri

TooSAP HANA Azure (büyük örnekler), onu &#39; bağlanan birden çok SAP sistemleri veya büyük SAP sistemleri dağıtılıyorsa makul tooassume hello sn'ye hello VNet ağ geçidi'nin bir ayak bağı. Böyle bir durumda toosplit hello uygulama katmanları birden fazla Azure Vnet gerekir. Recommendable toocreate olabilir durumlarda ister için tooHANA büyük örnekleri bağlanan özel sanal ağlar:

- NFS paylaşımlarını yedeklemeleri gerçekleştirmek barındıran doğrudan hello HANA örnekleri ' büyük örnekleri HANA tooa azure'da VM içinde
- Azure'da yönetilen HANA büyük örneği birimleri toodisk alandan büyük yedekleri ya da diğer dosyaları kopyalanıyor.

Ana bilgisayar hello depolama yönetin VM'ler büyük dosya etkisi engeller veya hello VNet hello SAP uygulama katmanı çalıştıran hello VM'ler görevi gören ağ geçidi üzerinde HANA büyük örnekleri tooAzure veri aktarımı ayrı Vnet'ler kullanıyor. 

Daha fazla ölçeklenebilir bir ağ mimarisi için:

- Tek, daha büyük bir SAP uygulama katmanı için birden fazla Azure Vnet yararlanın.
- Dağıtılan, her bir SAP sistemi karşılaştırılan toocombining için ayrı bir Azure sanal ağ dağıtmak altında ayrı alt ağlar bu SAP sistemler hello aynı sanal ağı.

 SAP HANA azure'da (büyük örnekler) için daha fazla ölçeklenebilir bir ağ mimarisi:

![SAP uygulama katmanı üzerinde birden fazla Azure Vnet dağıtma](./media/hana-overview-architecture/image4-networking-architecture.png)

Yukarıda gösterildiği gibi birden fazla Azure Vnet üzerinde Hello SAP uygulama katmanı veya bileşenleri, dağıtma, bu Azure Vnet barındırılan hello uygulamalar arasındaki iletişim sırasında oluşan kaçınılmaz gecikme yükü kullanıma sunuldu. Varsayılan olarak, Azure VM'ler arasındaki ağ trafiğini hello hello farklı sanal ağlar rotayı MSEE yönlendiriciler bu yapılandırmada yer. Ancak, bu yönlendirme Eylül 2016 itibaren iyileştirilebilir. yolu toooptimize hello ve hello gecikme iki arasındaki iletişimde aşağı Kes sanal ağlar hello içinde eşleme Azure Vnet gereğidir aynı bölgede. Bu sanal ağlar farklı Aboneliklerde olsa bile. Azure VNet eşlemesi, iki farklı Azure vnet'lerdeki sanal makineleri arasındaki iletişimi hello kullanarak kullanım hello Azure ağı omurga toodirectly birbirleri ile iletişim kurabilir. Böylece gösteren benzer gecikme süresine hello VM'ler içinde olacaksa gibi hello aynı sanal ağı. Hello Azure sanal ağ geçidi üzerinden bağlı IP adresi aralıklarını adresleme trafiği üzerinden yönlendirilir ancak tek tek sanal ağ geçidi hello VNet için hello. Merhaba makalesinde eşliği Azure VNet ayrıntılarını alabilirsiniz [VNet eşlemesi](https://docs.microsoft.com/azure/virtual-network/virtual-network-peering-overview).


### <a name="routing-in-azure"></a>Azure'da yönlendirme

SAP HANA azure'da (büyük örnekler) için iki önemli ağ yönlendirme noktalar vardır:

1. SAP HANA (büyük örnekler) azure'da hello ayrılmış ExpressRoute bağlantı yalnızca Azure VM'ler tarafından erişilebilir; doğrudan şirket içinden. Bazı yönetim istemcileri ve SAP çözüm şirket içi, çalışan Yöneticisi bağlanamıyor toohello SAP HANA veritabanına gibi doğrudan erişim gerektiren herhangi bir uygulama.

2. SAP HANA Azure (büyük örnekler) birimlerine sahip gönderilen hello müşteri olarak aralık atanan IP adresini hello sunucu IP havuzu adresinden (bkz [SAP HANA (büyük örnekler) altyapısı ve Azure ile ilgili bağlantı](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Ayrıntılar için).  Bu IP adresi hello Azure erişilebilen abonelikleri ve Azure Vnet'ler tooHANA azure'da (büyük örnekler) bağlanan ExpressRoute. Merhaba sunucu IP havuzu adres aralığı dışında atanmış IP adresini doğrudan toohello donanım birim atanır ve NAT'ed değil, bu çözüme yönelik hello ilk dağıtımları hello durumda, bu artık. 

> [!NOTE] 
> İçinde tooconnect tooSAP HANA azure'da (büyük örnekler) ihtiyacınız varsa bir _veri ambarı_ senaryosu, uygulamaları ve/veya son kullanıcıların gereken yeri tooconnect toohello SAP HANA veritabanına (doğrudan çalıştıran), başka bir ağ bileşeni olmalıdır kullanılan: ters proxy tooroute verileri, gelen tooand. Örneğin, F5 BIG-IP, NGINX ile trafik, Yöneticisi Azure sanal güvenlik duvarı/trafik yönlendirme çözümü olarak dağıtılabilir.

### <a name="internet-connectivity-of-hana-large-instances"></a>Internet bağlantısı HANA büyük örnekleri
HANA büyük örnekleri doğrudan internet bağlantısı yok. Bu örneğin hello işletim sistemi görüntüsüne doğrudan hello OS satıcı ile kaydetmek için yeteneklerini kısıtlıyor. Bu nedenle, yerel SLES SMT sunucusu veya RHEL Abonelik Yöneticisi toowork gerekebilir

### <a name="data-encryption-between-azure-vms-and-hana-large-instances"></a>Azure Vm'leri ve HANA büyük örnekleri arasında veri şifrelemesi
Azure VM'ler HANA büyük örnekleri arasında aktarılan veriler şifrelenmez. Ancak, tamamen hello HANA DBMS yan ve JDBC/ODBC tabanlı uygulamalar arasında hello exchange için trafiği şifrelemeyi etkinleştirebilirsiniz. Başvuru [SAP tarafından bu belgeleri](http://help-legacy.sap.com/saphelp_hanaplatform/helpdata/en/db/d3d887bb571014bf05ca887f897b99/content.htm?frameset=/en/dd/a2ae94bb571014a48fc3b22f8e919e/frameset.htm&current_toc=/en/de/ec02ebbb57101483bdf3194c301d2e/plain.htm&node_id=20&show_children=false)

### <a name="using-hana-large-instance-units-in-multiple-regions"></a>Birden çok bölgede HANA büyük örneği birimlerini kullanma

Olağanüstü durum kurtarma yanı sıra birden çok Azure bölgelerindeki diğer nedenleri toodeploy SAP HANA Azure (büyük örnekler) ile ilgili olabilir. Tooaccess HANA büyük örnekleri her hello dağıtılan hello VM'ler istediğiniz belki farklı sanal ağlar hello bölgelerdeki. Toohello farklı atanmış Hello IP adresleri beri hello Azure (ağ geçidi toohello örneklerini doğrudan bağlı) sanal ağlar ötesinde HANA büyük örnekleri birimleri yayılmaz olduğunda, bir hafif değiştirmek toohello yukarıda sunulan VNet tasarım: bir Azure VNet ağ geçidi farklı Msee'ler dışında farklı dört ExpressRoute bağlantı hatları işleyebilir ve hello büyük örneği Damgalar bağlı tooone olan her bir Vnet'teki bağlı toohello büyük örneği damga başka bir Azure bölgesindeki olabilir.

![Azure sanal ağlar farklı Azure bölgelerinde tooAzure büyük örneği Damgalar bağlı](./media/hana-overview-architecture/image8-multiple-regions.png)

Şekil gösterir yukarıda Hello nasıl hem de farklı Azure sanal ağlar hello bölgeleri olan hem de Azure bölgelerinde kullanılan tooconnect tooSAP HANA Azure (büyük örnekler) ile ilgili olan bağlı tootwo farklı ExpressRoute bağlantı hatları. Yeni sunulan Merhaba, hello dikdörtgen kırmızı satırları bağlantılardır. Bu bağlantılar ile dışında hello Azure sanal ağlar, bu sanal ağlar birini çalıştıran hello VM'ler her hello iki bölgelerde dağıtılan hello farklı HANA büyük örnekleri birimleri erişebilir. Yukarıdaki hello grafik gördüğünüz gibi şirket içi toohello iki Azure bölgelerinden iki ExpressRoute bağlantıları sahip olduğunuz varsayılır; Olağanüstü durum kurtarma nedenlerle önerilir.

> [!IMPORTANT] 
> Birden çok ExpressRoute bağlantı hatları kullandıysanız, AS yolu eklenmesini ve yerel tercih BGP ayarları kullanılan tooensure trafik yönlendirme uygun olması gerekir.


