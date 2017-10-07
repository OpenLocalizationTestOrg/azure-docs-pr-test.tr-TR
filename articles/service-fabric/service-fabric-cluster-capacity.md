---
title: "aaaPlanning hello Service Fabric kümesi kapasite | Microsoft Docs"
description: "Service Fabric kümesi kapasite planlama konuları. Nodetypes, dayanıklılık ve güvenilirlik katmanları"
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 4c584f4a-cb1f-400c-b61f-1f797f11c982
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: chackdan
ms.openlocfilehash: 83272ce7fefe698eef755cf66493c2874cc3b120
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-cluster-capacity-planning-considerations"></a>Service Fabric kümesi kapasite planlama konuları
Her üretim dağıtımı için kapasite planlamasının önemli bir adımdır. Bu işlemin bir parçası olarak tooconsider sahip hello öğelerini bazıları aşağıda verilmiştir.

* Merhaba düğüm sayısı, küme gereksinimlerini toostart çıkışı ile türleri
* Merhaba özellikleri her bir düğüm türü (boyutu, birincil, internet'e yönelik, sanal makineleri, vb. sayısı)
* Merhaba küme Hello güvenilirlik ve dayanıklılık özellikleri

Bize kısaca bu öğelerin her birini gözden geçirin.

## <a name="hello-number-of-node-types-your-cluster-needs-toostart-out-with"></a>Merhaba düğüm sayısı, küme gereksinimlerini toostart çıkışı ile türleri
Oluşturmakta hangi hello küme için kullanılan toobe gittiği ve hangi tür uygulamaların planlama toofigure gereken ilk olarak, bu kümesine toodeploy. Clear hello amacına hello küme olup olmadığı, büyük olasılıkla olmayan henüz tooenter hello kapasite planlama işlemi hazır.

Kümenizin çıkışı toostart ile gereken düğüm türleri Hello sayısı kurun.  Her düğüm türü eşlenmiş tooa sanal makine ölçek kümesi değil. Her düğüm türü sonra ölçeklendirilebilir veya Aşağı bağımsız olarak, farklı bağlantı noktalarının açık olması ve farklı kapasite ölçümlerini olabilir. Bu nedenle hello karar düğüm türleri hello sayısının temelde ilgili önemli noktalar aşağıdaki toohello birlikte gelir:

* Uygulamanız birden çok hizmetlere sahip olmadığı ve bunlardan herhangi birinin toobe ortak veya İnternete gerekiyor? Tipik uygulamalar, bir istemciden giriş aldığı bir ön uç ağ geçidi hizmeti ve iletişim kuran bir veya daha fazla arka uç hizmetleriyle hello ön uç hizmetleri içerir. Bu nedenle bu durumda, en az iki düğüm türleri sahip sonlandırın.
* (Uygulamanızı kurma), hizmetler, daha fazla RAM veya daha yüksek CPU döngüsü gibi farklı altyapı gereksinimleri var mı? Örneğin, bir ön uç hizmeti ve arka uç hizmeti toodeploy içeren istediğiniz bu Merhaba uygulaması bize varsayın. Merhaba ön uç hizmeti bağlantı noktalarının toohello açık olan küçük Vm'lerde (örneğin, D2 VM boyutları) çalışabilir Internet.  Merhaba arka uç hizmeti, Bununla birlikte, hesaplama yoğun ve gereksinimlerini toorun Internet olmayan daha büyük sanal makineleri üzerinde (VM boyutları D4, D6, D15 gibi ile) karşılıklı.
  
  Bu örnekte, tooput karar verebilirsiniz rağmen tüm hizmetleri tek bir düğüm türünde Merhaba, bunları bir kümede iki düğüm türleriyle yerleştirmenizi öneririz.  Bu düğüm her tür toohave farklı özellikleri VM boyutu veya internet bağlantısı gibi sağlar. VM Hello sayısı Genişletilebilir bağımsız olarak, de.  
* Merhaba gelecekteki tahmin edilemez olduğundan, bildiğiniz bulguları ile gidin ve uygulamalarınız ile toostart gereken düğüm türleri hello sayısı karar verin. Her zaman ekleyebilir veya düğüm türleri daha sonra kaldırabilirsiniz. Service Fabric kümesi en az bir düğüm türü olmalıdır.

## <a name="hello-properties-of-each-node-type"></a>Her düğüm türünün Hello özellikleri
Merhaba **düğüm türü** bulut Hizmetleri'nde eşdeğer tooroles olarak görülebilir. Düğüm türleri hello VM boyutları, VM'ler hello sayısını ve bunların özelliklerini tanımlar. Service Fabric kümesi içinde tanımlanan her düğüm türü ayrı sanal makine ölçek kümesi ayarlanır. Sanal makine ölçek kümesi bir Azure işlem kaynaktır toodeploy kullanın ve sanal makinelerin bir koleksiyon kümesi olarak yönetin. Farklı sanal makine ölçek kümesi tanımlanan, her düğüm türü sonra ölçeklendirilebilir veya Aşağı bağımsız olarak, farklı bağlantı noktalarının açık olması ve farklı kapasite ölçümlerini olabilir.

Okuma [bu belgeyi](service-fabric-cluster-nodetypes.md) Nodetypes toovirtual makine ölçek kümesinin hello ilişki hakkında daha fazla ayrıntı için nasıl tooRDP hello örnekleri birine yeni bağlantı noktalarını açmak vb..

Kümenizi birden fazla olabilir düğüm türü, ancak hello birincil düğüm türü (Merhaba hello portalında tanımlayan birinci) üretim iş yükleri için kullanılan küme için en az beş VM'ler (veya test kümeleri için en az üç sanal makineleri) olmalıdır. Resource Manager şablonu kullanarak hello kümesi oluşturuyorsanız, ardından Ara **birincil** hello düğüm türü tanımı altında özniteliği. Merhaba birincil düğüm türü hello düğümü Service Fabric Sistem Hizmetleri yerleştirildiği türüdür.  

### <a name="primary-node-type"></a>Birincil düğüm türü
Birden çok düğüm türleri ile bir küme için bunlardan birini toochoose toobe birincil gerekir. Birincil düğüm türü hello özellikleri şunlardır:

* Merhaba **VM'ler en küçük boyut** hello birincil düğüm türü hello tarafından belirlenir için **dayanıklılık katmanı** seçtiğiniz. Merhaba hello dayanıklılık katmanı için Bronz varsayılandır. Hangi hello dayanıklılık katmanı hakkında ayrıntılı bilgi için aşağı kaydırın olan ve hello değerleri sürer.  
* Merhaba **VM'ler en az sayıda** hello birincil düğüm türü hello tarafından belirlenir için **güvenilirlik katmanı** seçtiğiniz. Merhaba hello güvenilirlik katmanı için Gümüş varsayılandır. Hangi hello güvenilirlik katmanı hakkında ayrıntılı bilgi için aşağı kaydırın olan ve hello değerleri sürer. 


* Merhaba Service Fabric Sistem Hizmetleri (örneğin, hello Küme Yöneticisi hizmeti veya Image Store hizmeti) hello birincil düğüm türü ve bunu hello güvenilirlik yerleştirilir ve dayanıklılık hello kümesinin hello güvenilirlik katmanı değeri ve dayanıklılık katmanı tarafından belirlenir değer hello birincil düğüm türü seçin.

![İki düğüm türleri olan kümesinin ekran görüntüsü ][SystemServices]

### <a name="non-primary-node-type"></a>Olmayan birincil düğüm türü
Bir kümenin birden fazla düğüm türleri ile bunların hello rest birincil olmayan ve bir birincil düğüm türü yoktur. Birincil olmayan düğüm türü hello özellikleri şunlardır:

* Merhaba en küçük boyut VM'ler bu düğüm türü için seçtiğiniz hello dayanıklılık katmanı tarafından belirlenir. Merhaba hello dayanıklılık katmanı için Bronz varsayılandır. Hangi hello dayanıklılık katmanı hakkında ayrıntılı bilgi için aşağı kaydırın olan ve hello değerleri sürer.  
* Merhaba minimum sayısı VM'ler için bu düğüm türü olabilir. Ancak, bu sayı hello uygulama/hizmetleri bu düğüm türü toorun istediğiniz çoğaltmalarının hello sayısına dayalı seçmelisiniz. Merhaba küme dağıttıktan sonra hello sayısında VM'ler düğüm türü artırılabilir.

## <a name="hello-durability-characteristics-of-hello-cluster"></a>Merhaba dayanıklılık hello küme özelliklerini
Merhaba dayanıklılık katmanı hello temel Azure altyapısı ile Vm'leriniz sahip kullanılan tooindicate toohello sistem hello ayrıcalıkları ' dir. Merhaba birincil düğüm türü'nde, bu ayrıcalık Service Fabric toopause hello sistem hizmetleri ve durum bilgisi olan hizmetlerinizi hello çekirdek gereksinimleri etkileyen herhangi VM düzeyinde altyapı istek (örneğin, bir VM yeniden başlatma, VM yeniden görüntü oluşturma veya VM geçiş) sağlar. Merhaba birincil olmayan düğüm türleri'nde, bu ayrıcalık hello çekirdek gereksinimleri içinde çalışan, durum bilgisi olan hizmetler için etkileyen herhangi VM düzeyinde altyapı isteklere VM yeniden başlatma, VM yeniden görüntü oluşturma, VM geçiş vb. gibi Service Fabric toopause izin verir.

Bu ayrıcalık değerleri aşağıdaki hello ifade edilir:

* Altın - hello altyapı UD başına iki saatlik bir süre işleri duraklatıldı. Altın dayanıklılık, yalnızca tam düğümü VM SKU'ları D15_V2, G5 vb. gibi üzerinde etkinleştirilebilir.
* Gümüş - hello altyapı işleri UD başına 10 dakikalık bir süre duraklatıldı ve tüm standart vm'lerde tek çekirdek ve yukarıdaki kullanılabilir.
* Bronz - ayrıcalıkların. Bu, hello varsayılandır. Yalnızca bu dayanıklılık düzeyi düğüm türleri için Çalıştır kullanın _yalnızca_ durum bilgisiz iş yükleri. 

> [!WARNING]
> Bronz dayanıklılık çalıştıran NodeTypes elde _ayrıcalıkların_. Bu, durum bilgisiz iş yükleri etkisi altyapı işleri durduruldu gecikmeli ya olduğunu anlamına gelir. Bu tür işleri kapalı kalma süresi ve diğer sorunlar neden yüklerinizi hala etkileyebilir mümkündür. Her tür üretim iş yükü için en az çalışan Gümüş önerilir. 
> 

Her düğüm türleri için toochoose dayanıklılık düzeyi alın. Bir düğüm türü toohave altın dayanıklılık düzeyini seçebilirsiniz veya Gümüş ve hello diğer Bronz hello aynı küme. **5 düğümleri dayanıklılık altın veya gümüş sahip tüm düğüm-türü için minimum sayısını korumalıdır**. 

**Gümüş veya altın dayanıklılık düzeyleri kullanmanın yararları**
 
1. Bir ölçek işleminde gerekli adımları Hello sayısını azaltan (diğer bir deyişle, düğümü devre dışı bırakma ve Kaldır-ServiceFabricNodeState denir otomatik olarak)
2. Veri kaybı son tooa müşteri tarafından başlatılan yerinde VM SKU değiştirme işlemi veya Azure altyapı işlemleri Hello riskini azaltır.
     
**Dezavantajlarını Gümüş veya altın dayanıklılık düzeyleri**
 
1. Dağıtımları tooyour sanal makine ölçek kümesi ve diğer ilgili Azure kaynaklarını) Gecikmeli, zaman aşımına veya tamamen sorunları kümenizdeki veya hello altyapı düzeyinde tarafından engellendi. 
2. Merhaba sayısı arttıkça [çoğaltma yaşam döngüsü olayları](service-fabric-reliable-services-advanced-usage.md#stateful-service-replica-lifecycle ) (örneğin, birincil takasları) tooautomated düğümü deactivations Azure altyapı işlemleri sırasında son.

### <a name="recommendations-on-when-toouse-silver-or-gold-durability-levels"></a>Ne zaman hakkında öneriler toouse Gümüş veya altın dayanıklılık düzeyleri

Kullanım Gümüş veya altın dayanıklılık o ana bilgisayar durum bilgisi olan tüm düğüm türleri için Hizmetleri, beklenen tooscale (VM örneği sayısını azaltmak) sık sık ve dağıtım işlemlerini bu ölçek işlemleri basitleştirme lehinde Gecikmeli tercih. Merhaba genişleme senaryoları (VM'ler örnekleri ekleme) hello dayanıklılık katmanı tercih ettiğiniz çalmak değil, yalnızca ölçek içinde değil.

### <a name="operational-recommendations-for-hello-node-type-that-you-have-set-toosilver-or-gold-durability-level"></a>Merhaba düğüm için işletimsel önerileri toosilver veya altın dayanıklılık düzeyi ayarlamış olduğunuz yazın.

1. Küme ve uygulamalar her zaman sağlıklı tutmak ve uygulamalar tooall yanıt emin olun [hizmet çoğaltma yaşam döngüsü olayları](service-fabric-reliable-services-advanced-usage.md#stateful-service-replica-lifecycle) (derleme yinelemede kalmış gibi) zamanında.
2. Daha güvenli şekilde toomake VM SKU değişiklik (Ölçek yukarı/aşağı) benimsemeyi: bir sanal makine ölçek kümesi VM SKU'su olduğu kendiliğinden hello değiştirme güvenli olmayan bir işlem ve bu nedenle, mümkünse kaçınılmalıdır. Burada, tooavoid sık karşılaşılan sorunları izleyebilirsiniz hello işlem verilmiştir.
    - **Birincil olmayan nodetypes için:** , yeni sanal makine ölçek kümesi oluşturma, hello hizmet yerleştirme kısıtlaması tooinclude hello yeni sanal makine ölçek kümesi/düğüm türü değiştirme ve ardından azaltmak, önerilen eski sanal makine ölçek kümesi hello örnek sayısı too0, bir düğümü birer birer (toomake hello düğümleri kaldırılmasını hello küme hello güvenilirliğini etkilemeyen emin olur).
    - **Merhaba birincil nodetype için:** hello birincil düğüm türünde VM SKU değiştirmeyin bizim önerilir. Merhaba yeni SKU kapasitesi için hello nedeni, biz daha fazla örnekleri ekleme önerilir veya mümkünse, yeni bir küme oluşturun. Hiçbir seçim yapmanız gerekirse, yeni SKU hello değişiklikler toohello sanal makine ölçek kümesi modeli tanımı tooreflect olun. Yalnızca bir nodetype kümeniz varsa, daha sonra durum bilgisi olan uygulamaların tooall yanıt emin olun [hizmet çoğaltma yaşam döngüsü olayları](service-fabric-reliable-services-advanced-usage.md#stateful-service-replica-lifecycle) (derleme yinelemede kalmış gibi) zamanında ve hizmet çoğaltma yeniden oluşturma süresi beş dakikadan daha kısa bir süre (için Gümüş dayanıklılık düzeyi) olur. 


> [!WARNING]
> Değişen hello için en az Gümüş dayanıklılık çalıştırmayan VM ölçek kümesi VM SKU boyutunu maskelenmesi önerilen değil. VM SKU boyutunu değiştirme veri bozucu yerinde altyapı bir işlemdir. En az bazı özelliği toodelay veya İzleyici bu değişikliği hello işlemi dataloss durum bilgisi olan hizmetler için neden veya durum bilgisiz iş yükleri için bile diğer unforseen işletimsel sorunlara neden mümkündür. 
> 
    
3. Tüm sanal makine ölçek MR etkin olan kümesi için en az beş düğüm sayısını koru
4. Rastgele VM örneklerini silmek değil, her zaman sanal makine ölçek kümesi ölçek özelliği tuşunu kullanın. rastgele VM örnekleri Hello silinmesini UD ve FD üzerinden yayılan hello VM örneğinde dengede değil oluşturma bir olasılığı vardır. Bu dengesizliği hello sistemleri özelliği tooproperly Yük Dengeleme hello hizmet örnekleri/hizmet çoğaltmalar arasında olumsuz yönde etkileyebilir.
6. (VM örneklerini kaldırma), Ölçek gerçekleştirilir gibi yalnızca tek bir düğüme aynı anda otomatik ölçeklendirme kullanıyorsanız, ardından hello kurallarını ayarlayın. Aynı anda birden fazla örneği Ölçeklendirmesi güvenli değil.
7. Birincil düğüm türü Ölçeklendirmesi varsa, hiçbir zaman onu birden çok hangi hello güvenilirlik katmanı sağlar ölçeğini.


## <a name="hello-reliability-characteristics-of-hello-cluster"></a>Merhaba kümesinin Hello güvenilirliği
Merhaba güvenilirlik katmanı kullanılan tooset hello hello birincil düğüm türü bu kümede toorun istediğiniz hello sistem hizmetlerinin çoğaltmaların sayısı. Çoğaltma daha fazla hello sayısı Merhaba, hello daha güvenilir hello sistem kümenizdeki hizmetleridir.  

Merhaba güvenilirlik katmanı değerleri aşağıdaki hello alabilir:

* Platinum - Çalıştır hello Sistem Hizmetleri ile 9 hedef çoğaltma kümesi sayısı
* Altın - Çalıştır hello Sistem Hizmetleri ile 7 hedef çoğaltma kümesi sayısı
* Gümüş - Çalıştır hello Sistem Hizmetleri ile 5 hedef çoğaltma kümesi sayısı 
* Bronz - Çalıştır hello Sistem Hizmetleri ile 3 hedef çoğaltma kümesi sayısı

> [!NOTE]
> Seçtiğiniz hello güvenilirlik katmanı hello düğüm sayısı alt sınırı birincil düğüm türünüz olmalıdır belirler. 
> 
> 


### <a name="recommendations-for-hello-reliability-tier"></a>Merhaba güvenilirlik katmanı ilgili öneriler.

 Artırabilir ya da hello boyutunun kümenizin (tüm düğüm türleri VM örnekleri toplamı hello), bir katmanlı tooanother kümenizden hello güvenilirliğini güncelleştirmeniz gerekir. Bunun yapılması hello Küme yükseltme gerekli toochange hello Sistem Hizmetleri çoğaltma kümesi sayısı tetikler. Merhaba yükseltme ilerleme toocomplete için düğümleri ekleme gibi tüm diğer değişiklikler toohello küme, yapmadan önce bekleyin.  Merhaba yükseltme Service Fabric Explorer veya çalıştırarak hello ilerlemesini izleyebilirsiniz [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

Merhaba güvenilirlik katmanı seçme özelliği üzerinde hello öneri aşağıda verilmiştir.

| **Küme boyutu** | **Güvenilirlik katmanı** |
| --- | --- |
| 1 |Belirtmeyin güvenilirlik katmanı parametre Merhaba, hello sistem hesaplar |
| 3 |Bronz |
| 5 veya 6|Gümüş |
| 7 veya 8 |Altın |
| 9 ve sonraki sürümü |Platinum |




## <a name="primary-node-type---capacity-guidance"></a>Birincil düğüm türü - Kapasite Kılavuzu

İşte hello birincil düğüm türü kapasite planlaması için Başlangıç Kılavuzu

1. **Herhangi bir üretim iş yükü Azure VM sayısı örnekleri toorun:** 5 en az bir birincil düğüm türü boyutunu belirtmeniz gerekir. 
2. **VM sayısı örnekleri azure'da toorun test iş yüklerini** minimum birincil düğüm türü boyutu 1 veya 3 belirtebilirsiniz. tek düğümlü bir küme, özel bir yapılandırma ve bu nedenle ile çalışır Merhaba, bu küme dışında ölçek desteklenmiyor. Merhaba tek düğümlü bir küme, güvenilirlik ve bu nedenle, Resource Manager şablonu, sahip olduğunuz tooremove/değil, yapılandırmayı belirtin (Merhaba yapılandırma değeri ayarı olmayan değil yeterli). Ayarlarsanız portalı yoluyla hello tek düğümlü bir küme ayarlamak, ardından hello yapılandırması otomatik olarak dikkate. 1 ve 3 düğümlü kümeler, üretim iş yükleri çalıştırmak için desteklenmez. 
3. **VM SKU:** birincil düğüm türü olduğundan hello Sistem Hizmetleri çalıştırdığı, hello VM seçmek için gerekir Al hesap hello genel yoğun saatler içine yüklemek, SKU planlama tooplace hello kümesine. Burada - ortalama hello birincil düğüm türü, "Lungs", oxygen tooyour beyin sağladıkları olduğu düşüncelerinizi benzerleme tooillustrate işte ve bu nedenle, gövde hello beyin yeterli oxygen almazsa yükselmesine. 

Bir küme Hello kapasite gereksinimlerini belirlenir olduğundan iş yükü tarafından toorun hello kümedeki planlama, belirli iş yükü nitel yönlendirme ile sunuyoruz olamaz, ancak İşte hello geniş Kılavuzu toohelp kullanmaya başlama

Üretim iş yükleri için 


- Merhaba VM SKU standart D3 veya standart D3_V2 veya eşdeğer bir en az yerel SSD 14 GB ile önerilir.
- desteklenen minimum hello VM SKU standart D1 veya standart D1_V2 veya eşdeğer bir en az yerel SSD 14 GB ile kullanılır. 
- Kısmi çekirdek standart A0 gibi VM SKU'ları üretim iş yükleri için desteklenmiyor.
- Standart A1 SKU performans nedenleriyle üretim iş yükleri için desteklenmez.


## <a name="non-primary-node-type---capacity-guidance-for-stateful-workloads"></a>Olmayan birincil düğüm türü - durum bilgisi olan iş yükleri için kapasite Kılavuzu

Service fabric kullanarak durum bilgisi olan iş yükleri için bu kılavuzu olduğundan [güvenilir koleksiyonları veya reliable Actors](service-fabric-choose-framework.md) hello birincil olmayan düğüm türünde çalışan.


**VM örneği sayısı:** durum bilgisi olan üretim iş yükleri için en az ve hedef çoğaltma sayısı 5 ile çalıştırmanızı önerilir. Bu, kararlı durumda, her bir hata etki alanı ve yükseltme etki alanı'nda (çoğaltma kümesinden) çoğaltma şunun olduğunu anlamına gelir. Merhaba tüm güvenilirlik katmanı kavram hello birincil düğüm türü için bir yol toospecify sistem hizmetleri için bu bir ayardır. Bu nedenle aynı hello göz önünde bulundurarak tooyour durum bilgisi olan hizmetleri de geçerlidir.

Durum bilgisi olan iş yükleri içinde çalıştırıyorsanız, bu nedenle üretim iş yükleri için hello minimum önerilen olmayan birincil düğüm türü 5, boyutudur.


**VM SKU:** her düğümüne tooplace VM SKU onun için seçtiğiniz gerçekleştirmeniz gereken hesap hello yoğun yük, hello planlamak için bu hello düğüm uygulama hizmetlerinizi burada çalıştırıyorsanız, türüdür. Merhaba nodetype kapasite gereksinimlerini Merhaba, ancak İşte kullanmaya başlama hello geniş Kılavuzu toohelp belirli iş yükü, nitel yönlendirme ile biz sağlayamaz şekilde hello kümedeki toorun planladığınız iş yükü tarafından belirlenir

Üretim iş yükleri için 

- Merhaba VM SKU standart D3 veya standart D3_V2 veya eşdeğer bir en az yerel SSD 14 GB ile önerilir.
- desteklenen minimum hello VM SKU standart D1 veya standart D1_V2 veya eşdeğer bir en az yerel SSD 14 GB ile kullanılır. 
- Kısmi çekirdek standart A0 gibi VM SKU'ları üretim iş yükleri için desteklenmiyor.
- Standart A1 SKU üretim iş yükleri için performansı artırmak için özellikle olmayan desteklenmiyor.


## <a name="non-primary-node-type---capacity-guidance-for-stateless-workloads"></a>Olmayan birincil düğüm türü - durum bilgisiz iş yükleri için kapasite Kılavuzu

Bu kılavuz, hello birincil olmayan nodetype üzerinde çalışan durum bilgisiz iş yükleri.

**VM örneği sayısı:** durum bilgisiz üretim iş yükleri için desteklenen minimum hello birincil düğüm olmayan yazı tipi boyutu 2'dir. Bu toorun sağlar, iki durum bilgisiz örneği, uygulama ve hizmet toosurvive vererek hello VM örneği kaybı. 

> [!NOTE]
> Kümenizi bir service fabric sürümü 5.6 değerinden üzerinde çalışıyorsa, hello tooa üründe son birincil olmayan düğüm türü tooless, 5'ten aşağı ölçeklendirmesi (5.6 Bu sorun düzeltilmiştir) çalışma zamanı, sonuçları çağırmanız kadar sağlıksız, kapatma küme sistem durumu [ Remove-ServiceFabricNodeState cmd](https://docs.microsoft.com/powershell/servicefabric/vlatest/Remove-ServiceFabricNodeState) hello uygun düğümü ada sahip. Okuma [Service Fabric kümesi içeri veya dışarı gerçekleştirmek](service-fabric-cluster-scale-up-down.md) daha fazla ayrıntı için
> 
>

**VM SKU:** her düğümüne tooplace VM SKU onun için seçtiğiniz gerçekleştirmeniz gereken hesap hello yoğun yük, hello planlamak için bu hello düğüm uygulama hizmetlerinizi burada çalıştırıyorsanız, türüdür. Merhaba nodetype kapasite gereksinimlerini Merhaba, ancak İşte kullanmaya başlama hello geniş Kılavuzu toohelp belirli iş yükü, nitel yönlendirme ile biz sağlayamaz şekilde hello kümedeki toorun planladığınız iş yükü tarafından belirlenir

Üretim iş yükleri için 


- Merhaba VM SKU standart D3 veya standart D3_V2 veya eşdeğer önerilir. 
- desteklenen minimum hello VM SKU standart D1 veya standart D1_V2 veya eşdeğer kullanılır. 
- Kısmi çekirdek standart A0 gibi VM SKU'ları üretim iş yükleri için desteklenmiyor.
- Standart A1 SKU performans nedenleriyle üretim iş yükleri için desteklenmez.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a>Sonraki adımlar
Kapasite planlama tamamlayın ve küme ayarlama sonra hello aşağıdaki okuyun:

* [Service Fabric kümesi güvenliği](service-fabric-cluster-security.md)
* [Service Fabric sistem durumu modeli giriş](service-fabric-health-introduction.md)
* [İlişki Nodetypes tooVirtual makine ölçek kümesi](service-fabric-cluster-nodetypes.md)

<!--Image references-->
[SystemServices]: ./media/service-fabric-cluster-capacity/SystemServices.png
