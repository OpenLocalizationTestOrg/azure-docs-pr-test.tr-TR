---
title: "aaaCluster kaynak yöneticisi küme açıklaması | Microsoft Docs"
description: "Service Fabric kümesi, hata etki alanlarını, yükseltme etki alanları, düğüm özellikleri ve hello küme kaynak yöneticisi için düğüm kapasiteler belirterek açıklayan."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 55f8ab37-9399-4c9a-9e6c-d2d859de6766
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: f2822075976bd54402af5ad56991b5b360dfb1d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="describing-a-service-fabric-cluster"></a>Service fabric kümesi açıklayan
Merhaba Service Fabric kümesi Kaynak Yöneticisi bir küme açıklamak için çeşitli mekanizmalar sağlar. Çalışma zamanı sırasında bu bilgileri tooensure hizmetlerinin yüksek düzeyde kullanılabilir hello kümede çalışan hello hello Küme Kaynak Yöneticisi'ni kullanır. Bu önemli kurallar zorlarken bu de toooptimize hello kaynak tüketimini hello küme içinde çalışır.

## <a name="key-concepts"></a>Önemli kavramlar
Merhaba Küme Kaynak Yöneticisi'ni bir küme açıklayan çeşitli özellikleri destekler:

* Hata etki alanları
* Yükseltme etki alanları
* Düğüm özellikleri
* Düğüm kapasitesi

## <a name="fault-domains"></a>Hata etki alanları
Hata etki alanı herhangi Eşgüdümlü hatası alanıdır. (Güç kaynağı hataları toodrive hataları toobad NIC ürün bilgisinde için kendi çeşitli nedenlerle üzerinde başarısız olacağından bu yana) tek bir makineye bir hata etki alanıdır. Aynı Ethernet anahtarı olan bağlı toohello olarak aynı hata etki alanı, hello makineler güç veya tek bir konumda tek bir kaynak paylaşımı makinelerdir. Donanım hatalarının toooverlap için doğal olduğundan, hata etki alanlarını kendiliğinden hiyerarşik ve Service Fabric URI'ler olarak temsil edilir.

Service Fabric bu bilgileri toosafely yer Hizmetleri kullandığından hata etki alanlarının doğru şekilde ayarlandığından emin önemlidir. Service Fabric aşağı hizmet toogo hata (bazı bileşen hello hatadan kaynaklanıyor) etki alanı hello kaybedilmesine neden olacağı şekilde tooplace Hizmetleri istememektedir. Hello Azure ortamı Service Fabric hello ortamı toocorrectly tarafından sağlanan hello hata etki alanı bilgilerini kullanır, sizin adınıza hello kümedeki hello düğümler yapılandırın. Service Fabric tek başına, hata etki alanlarını hello zamanında tanımlanan için bu hello küme ayarlama 

> [!WARNING]
> Bu hello hata etki alanı bilgileri tooService doku doğru sağlanır önemlidir. Örneğin, Service Fabric kümenin düğümleri beş fiziksel ana bilgisayarda çalışan 10 sanal makinelerde çalıştırılan varsayalım. Bu durumda, olsa bile 10 sanal makineyi, var. yalnızca 5 farklı (üst düzey) hata etki alanları. Aynı fiziksel ana bilgisayar neden hello paylaşımı VM'ler tooshare hello aynı kök hata etki alanı, fiziksel ana bilgisayarları başarısız olursa hata hello VM'ler deneyimi Eşgüdümlü beri.  
>
> Service Fabric bekliyor bu yana bir düğümün değil toochange hata etki alanı hello. Merhaba VM'ler, yüksek kullanılabilirliği gibi sağlamaya başka mekanizmalar [HA-VMs](https://technet.microsoft.com/en-us/library/cc967323.aspx), saydam VM'ler geçişini bir konak tooanother kullanın. Bu mekanizmaların etmeyin yeniden yapılandırın veya kod hello VM içinde çalışan hello bildirin. Bu nedenle, oldukları **desteklenmiyor** Service Fabric çalıştırmak için ortam olarak kümeleri. Service Fabric işe hello yalnızca yüksek oranda kullanılabilirlik teknolojisi olmalıdır. Dinamik VM geçiş gibi mekanizmaları SAN'lar, veya diğerleri gerekli değildir. Service Fabric, bu mekanizmaların ile birlikte kullandıysanız _azaltmak_ uygulama kullanılabilirliği ve güvenilirliği ek karmaşıklık tanıtmak için hata merkezi kaynakları ekleyin ve güvenilirlik kullanma ve Service Fabric de çakışan kullanılabilirlik stratejisi. 
>
>

Aşağıdaki Hello grafik tooFault etki alanları ve liste tüm farklı hataya neden etki alanları hello katkıda bulunan tüm hello varlıklar rengi. Bu örnekte, veri merkezleri ("DC"), kabin ("R") ve dikey pencerelerde ("B") sahip. Alanlara, her dikey birden fazla sanal makine tutuyorsa hello hata etki alanı hiyerarşisi başka bir katmana olabilir.

<center>
![Hata etki alanlarını düzenlenmiş düğümler][Image1]
</center>

Çalışma zamanı boyunca hello Service Fabric kümesi Kaynak Yöneticisi hello küme hello hata etki alanı olarak değerlendirir ve düzenleri planları. durum bilgisi olan çoğaltmaları hello veya durum bilgisiz örnekleri belirli bir hizmeti için ayrı hata etki alanı şekilde dağıtılır. Hata etki alanlarında Hello hizmet dağıtma hello hiyerarşinin herhangi bir düzeyde hata etki alanı başarısız olduğunda hello hello hizmetinin kullanılabilirliğini tehlikeye değil sağlar.

Service Fabric'ın Küme Kaynak Yöneticisi'ni kaç Katmanlar hello hata etki alanı hiyerarşisi vardır önemli değil. Ancak, hello kaybı herhangi bir kısmının hello hiyerarşi içinde çalışan hizmetler etkilemez tooensure çalışır. 

Varsa en iyisidir hello aynı sayıda her hello hata etki alanı hiyerarşisi derinlik düzeyini düğüm. Hata etki alanı "Ağaç" Merhaba kümenizdeki dengesiz ise, bu, hello küme Resource Manager toofigure hello en iyi ayırma Hizmetleri çıkışı zorlaştırır. İmbalanced hata etki alanlarını düzenleri, bazı etki alanlarına hello kaybı etkisi hello diğer etki alanlarındaki'den fazla hizmetlerin kullanılabilirliğini anlamına gelir. Merhaba küme kaynak yöneticisi arasında iki amacı sonuç olarak, bozuk: Hizmetleri üzerlerinde koyarak "kalın" Bu etki alanındaki toouse hello makineler istediği ve böylece bir etki alanı hello kaybı sorunlara neden olmayan diğer etki alanlarındaki tooplace Hizmetleri istiyor. 

İmbalanced etki alanları ne gibi görünüyor? Merhaba çizimde, iki farklı küme düzenleri gösterir. Merhaba ilk örnekte hello düğümleri hello hata etki alanları arasında eşit olarak dağıtılır. Hello ikinci örnekte, bir hata etki alanı diğer hata etki alanları hello daha pek çok daha fazla düğüm yok. 

<center>
![İki farklı küme düzenleri][Image2]
</center>

Azure üzerinde hata etki alanı bir düğümü içeren hello seçim sizin için yönetilir. Ancak, sağlamanız düğümleri hello sayısına bağlı olarak, hala hata etki alanları ile diğerlerinden daha fazla düğüm bunlara şunun. Örneğin, beş hata etki alanlarını hello kümedeki sahip, ancak yedi düğümler için belirli bir NodeType sağlamak söyleyin. Bu durumda, hello ilk iki hata etki alanı ile daha fazla düğüm sonlanır. Yalnızca birkaç örnekleri ile daha fazla NodeTypes toodeploy devam ederseniz, hello sorun kötü alır. Bu nedenle bu hello önermiştir her düğüm türü düğümlerin sayısı hata etki alanlarını hello sayısının katı.

## <a name="upgrade-domains"></a>Yükseltme etki alanları
Yükseltme etki alanlarının Service Fabric kümesi Kaynak Yöneticisi hello başka bir özelliği olan hello küme hello düzenini anlama. Yükseltme etki alanlarını tanımlayın hello yükseltilir düğümleri kümesi aynı anda. Yükseltme etki alanları Yardım hello Küme Kaynak Yöneticisi'ni Anlama ve yükseltme gibi yönetim işlemlerini düzenlemek.

Yükseltme etki alanlarının çok hata etki alanları gibi ancak birkaç önemli farklılıklar sahip değildir. İlk olarak, Eşgüdümlü donanım hataları alanlarının hata etki alanlarını tanımlayın. Diğer yandan Merhaba, ilke tarafından tanımlanan üzerinde etki alanlarını yükseltme. Toodecide yerine onu hello ortamı tarafından dikte edilmesini istediğiniz kaç alın. Sayıda yükseltme düğümleri yaptığınız gibi etki alanları olabilir. Başka bir hata etki alanları ve yükseltme etki alanları arasında yükseltme etki alanları hiyerarşik olmayan farktır. Bunun yerine, bunlar gibi basit bir etiketin daha fazla. 

Merhaba Aşağıdaki diyagramda üç yükseltme etki alanları üç hata etki alanlarında şeritli gösterilmektedir. Ayrıca, her farklı hata ve yükseltme etki alanları bittiği bir olası yerleşimini üç farklı çoğaltmalar için bir durum bilgisi olan hizmet gösterir. Bu yerleştirme hello ortasını hizmet yükseltmesi sırasında bir hata etki alanının hello zarar verir ve hello kod ve verilerin bir kopyasını çözümlenmedi.  

<center>
![Hata ve yükseltme etki alanları ile yerleştirme][Image3]
</center>

Yükseltme etki alanlarının, toohaving büyük sayılar Artıları ve eksileri vardır. Daha fazla yükseltme etki alanlarının her adımı hello yükseltin. daha ayrıntılı ve bu nedenle daha az sayıda düğümleri veya hizmetleri etkiler anlamına gelir. Sonuç olarak, daha az Hizmetleri toomove aynı anda daha az karmaşası hello sisteme giriş var. Merhaba hizmetinin daha az hello yükseltme sırasında sunulan herhangi bir sorundan etkilenmez beri bu tooimprove güvenilirlik eğilimi gösterir. Daha fazla yükseltme etki alanları kullanılabilir arabellek hello diğer düğümleri toohandle hello etkisini üzerinde daha az yükseltme anlamına gelir. Örneğin, beş yükseltme etki alanları varsa, her hello düğümleri trafiğinizi % 20 işleme kabaca. Bu yükseltme etki alanı aşağı tootake yükseltme için gerekiyorsa, bu yük toogo yere genellikle gerekir. Dört kalan yükseltme etki alanları sahip olduğundan, her yaklaşık %5 hello toplam trafik için yeriniz olması gerekir. Daha fazla yükseltme etki alanları daha az arabellek hello kümedeki hello düğümlere ihtiyaç duyacağınız anlamına gelir. Örneğin, 10 yükseltme etki alanları yerine sahip olmadığını göz önünde bulundurun. Bu durumda, her UD yalnızca yaklaşık %10 hello toplam trafik işleme. Bir yükseltme adımları, hello küme aracılığıyla her etki alanı yalnızca yaklaşık %1.1 hello toplam trafik için toohave yer gerekir. Daha fazla yükseltme etki alanları genellikle toorun izin düğümleriniz daha az ayrılmış kapasite gerektiğinden daha yüksek kullanımında. Merhaba aynı hata etki alanları için geçerlidir.  

birden çok etki alanı yükseltme sonucunda hello dezavantajı, yükseltmeleri tootake uzun eğilimindedir ' dir. Service Fabric, bir sonraki yükseltme etki alanı tamamlandıktan ve tooupgrade hello başlatmadan önce bir denetim gerçekleştirmediğini saat kısa bir süre bekler. Bu gecikmeler hello yükseltme devam etmeden önce hello yükseltme tarafından sunulan algılama sorunları etkinleştirin. Merhaba kolaylığını kabul edilebilir olduğundan aynı anda hello hizmeti çok fazla etkilemesini hatalı değişiklikleri önler.

Çok az yükseltme etki alanına sahip birçok negatif yan etkileri – tek tek her yükseltme etki alanı aşağı ve büyük bölümünü yükseltiliyor genel kapasitenizi kullanılamıyor. Örneğin, yalnızca üç yükseltme etki alanı varsa, aynı anda yaklaşık 1/3 genel hizmet veya küme kapasite sürüyor. Toohave küme toohandle hello yükünüzü hello rest içinde yeterli kapasiteye sahip olduğundan çok hizmetinizin aşağı aynı anda sahip arzu değil. Bu arabellek anlamına gelir normal işlemi sırasında aksi durumdakinden daha az yüklenen düğümleri olan koruma. Bu, hizmetiniz çalıştıran hello maliyetini artırır.

Hiçbir gerçek toohello toplam sayısını sınırla hatası veya yükseltme etki alanlarının bir ortam ya da nasıl birbiriyle kısıtlamaları yoktur. Birkaç ortak desenler vardır Bununla:

- Hata etki alanları ve yükseltme etki alanları 1:1 eşlenmiş
- Bir yükseltme etki alanı her düğüm (fiziksel veya sanal işletim sistemi örneği)
- Burada hello hata etki alanları ve yükseltme etki alanlarının bir matris genellikle hello çizgileri çalışan makineler ile form "şeritli" veya "matris" modeli

<center>
![Hata ve yükseltme etki alanı düzenleri][Image4]
</center>

Hangi düzeni toochoose hiçbir en iyi yanıt, her bazı Artıları ve eksileri vardır. Örneğin, hello 1FD:1UD basit tooset yukarı modelidir. Merhaba 1 yükseltme etki alanı düğümü modeli başına hangi kişiler için kullanılan gibi çoğu. Yükseltme sırasında her düğüm bağımsız olarak güncelleştirilir. Bu, benzer toohow küçük makineler kümesi hello son el ile yükseltildi. 

Merhaba en yaygın hello FD/UD matrisi, burada hello FDs ve UDs bir tablo oluşturur ve düğümler hello çapraz başlangıç yerleştirilir modelidir. Bu varsayılan Azure Service Fabric kümeleri olarak kullanılan hello modelidir. Birçok düğümleri içeren kümeler için her şeyi hello yoğun matris düzeni gibi yukarıdaki bakan sonlandırır.

## <a name="fault-and-upgrade-domain-constraints-and-resulting-behavior"></a>Hata ve yükseltme etki alanı kısıtlamaları ve bunun sonucunda oluşan davranışı
Merhaba küme Resource Manager tookeep hizmet arıza ve kısıtlama olarak yükseltme etki alanları arasında dengeli hello desire değerlendirir. Kısıtlamalar hakkında daha fazla bilgi için [bu makalede](service-fabric-cluster-resource-manager-management-integration.md). Hata ve yükseltme etki alanı kısıtlamaları durumu hello: "verili hizmet bölüm için hiçbir zaman olması gerektiğini fark *birden büyük* hello hizmet nesneleri (durum bilgisiz hizmet örneği veya durum bilgisi olan hizmet çoğaltmaları) sayısı iki etki alanı arasında." Bu, belirli taşır veya bu kısıtlamayı ihlal hazırlıklara önler.

Bir örneğe bakalım. Altı düğümü, beş hata etki alanları ve beş yükseltme etki alanları ile yapılandırılmış bir kümeye sahip olduğunuzu varsayalım.

|  | FD0 | FD1 | FD2 | FD3 | FD4 |
| --- |:---:|:---:|:---:|:---:|:---:|
| **UD0** |N1 | | | | |
| **UD1** |N6 |N2 | | | |
| **UD2** | | |N3 | | |
| **UD3** | | | |N4 | |
| **UD4** | | | | |N5 |

Şimdi biz bir TargetReplicaSetSize ile (veya Instancecount bir durum bilgisi olmayan bir hizmet için) bir hizmet beş oluşturduğunuzu varsayalım. Merhaba çoğaltmaları kara N1 N5 üzerinde. Aslında, N6 hiçbir zaman kaç Hizmetleri bu oluşturduğunuz gibi olsun kullanılır. Ancak neden? Merhaba birbirinden hello geçerli düzeni ve N6 seçilirse ne olacağını bakalım.

Var ve çoğaltmaları hata ve yükseltme etki alanı başına toplam sayısı hello hello düzeni şöyledir:

|  | FD0 | FD1 | FD2 | FD3 | FD4 | UDTotal |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| **UD0** |R1 | | | | |1 |
| **UD1** | |R2 | | | |1 |
| **UD2** | | |R3 | | |1 |
| **UD3** | | | |R4 | |1 |
| **UD4** | | | | |R5 |1 |
| **FDTotal** |1 |1 |1 |1 |1 |- |

Bu düzen, hata etki alanı ve yükseltme etki alanı başına düğüm bakımından dengelenir. Ayrıca, çoğaltma hata ve yükseltme etki alanı başına hello sayısı bakımından dengelenir. Her etki alanı olan hello düğümleri aynı sayıda ve hello aynı çoğaltmaların sayısı.

Şimdi, N6 yerine N2 kullandık neler olacağını konumundaki bakalım. Nasıl hello çoğaltmaları sonra dağıtılmış?

|  | FD0 | FD1 | FD2 | FD3 | FD4 | UDTotal |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| **UD0** |R1 | | | | |1 |
| **UD1** |R5 | | | | |1 |
| **UD2** | | |R2 | | |1 |
| **UD3** | | | |R3 | |1 |
| **UD4** | | | | |R4 |1 |
| **FDTotal** |2 |0 |1 |1 |1 |- |

Bu düzen hello hata etki alanı kısıtlaması için bizim tanımını ihlal ediyor. FD1 iki toplam sıfır, FD0 ve FD1 yapmayı hello birbirinden sahipken FD0 iki çoğaltması yok. Merhaba Küme Kaynak Yöneticisi, bu düzenleme izin vermiyor. Benzer şekilde biz N2 ve N6 (yerine N1 ve N2) kaldırdıysa biz alın:

|  | FD0 | FD1 | FD2 | FD3 | FD4 | UDTotal |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| **UD0** | | | | | |0 |
| **UD1** |R5 |R1 | | | |2 |
| **UD2** | | |R2 | | |1 |
| **UD3** | | | |R3 | |1 |
| **UD4** | | | | |R4 |1 |
| **FDTotal** |1 |1 |1 |1 |1 |- |

Bu düzen, hata etki alanlarını bakımından dengelenir. Ancak, şimdi onu hello yükseltme etki alanı kısıtlaması ihlal. UD1 iki sahipken UD0 sıfır çoğaltmalarına sahip olmasıdır. Bu nedenle, bu düzeni ayrıca geçersiz ve hello küme kaynak yöneticisi tarafından çekilmesi olmaz. 

## <a name="configuring-fault-and-upgrade-domains"></a>Hata ve yükseltme etki alanlarını yapılandırma
Hata etki alanları ve yükseltme etki alanları tanımlama yapılır otomatik olarak Azure Service Fabric dağıtımları barındırılan. Service Fabric alır ve Azure hello ortam bilgileri kullanır.

Kendi kümenizi oluşturmakta olduğunuz (veya toorun geliştirme belirli bir topolojisinde istediğiniz varsa), kendiniz hello hata etki alanı ve etki alanı yükseltme bilgileri sağlayabilir. Bu örnekte, üç "veri merkezleri" (her üç rafları) yayılan dokuz düğümlü bir yerel geliştirme küme tanımlayın. Bu küme üç yükseltme bu üç veri merkezi arasında şeritli etki alanı da sahiptir. Merhaba yapılandırma örneği aşağıdadır: 

ClusterManifest.xml

```xml
  <Infrastructure>
    <!-- IsScaleMin indicates that this cluster runs on one-box /one single server -->
    <WindowsServer IsScaleMin="true">
      <NodeList>
        <Node NodeName="Node01" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType01" FaultDomain="fd:/DC01/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node02" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType02" FaultDomain="fd:/DC01/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node03" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType03" FaultDomain="fd:/DC01/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
        <Node NodeName="Node04" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType04" FaultDomain="fd:/DC02/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node05" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType05" FaultDomain="fd:/DC02/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node06" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType06" FaultDomain="fd:/DC02/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
        <Node NodeName="Node07" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType07" FaultDomain="fd:/DC03/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node08" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType08" FaultDomain="fd:/DC03/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node09" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType09" FaultDomain="fd:/DC03/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
      </NodeList>
    </WindowsServer>
  </Infrastructure>
```

tek başına dağıtımlarında ClusterConfig.json

```json
"nodes": [
  {
    "nodeName": "vm1",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm2",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm3",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD3"
  },
  {
    "nodeName": "vm4",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm5",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm6",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD3"
  },
  {
    "nodeName": "vm7",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm8",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm9",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD3"
  }
],
```

> [!NOTE]
> Kümeler Azure Resource Manager aracılığıyla tanımlarken, hata etki alanları ve yükseltme etki alanlarının Azure tarafından atanır. Bu nedenle, düğüm türleri ve sanal makine ölçek kümeleri için Azure Resource Manager şablonunda hello tanımı hata etki alanı veya etki alanı yükseltme bilgileri içermez.
>

## <a name="node-properties-and-placement-constraints"></a>Düğüm özellikleri ve yerleştirme kısıtlamaları
Bazen (aslında hello zamanının çoğunu), belirli türde bir hello kümedeki düğümler üzerinde yalnızca belirli iş yüklerini çalıştırmak toowant tooensure oluşturacağız. Örneğin, diğerleri olmayabilir ancak bazı iş yükü GPU veya SSD gerektirebilir. Neredeyse her n katmanlı mimarisi ölçeklendiriyor donanım tooparticular iş yükleri hedefleme harika bir örnektir. Belirli makineler ön uç veya hello uygulamanın tarafı hizmet veren API hello olarak sunulan toohello istemciler veya Internet hello. Genellikle, farklı donanım kaynakları olan farklı makinelerde hello işlem ya da depolama katmanları hello çalışmanın işleyin. Çoğunlukla bunlar _değil_ doğrudan tooclients kullanıma sunulan veya Internet hello. Service Fabric burada belirli iş yükleri üzerinde belirli donanım yapılandırmalarını toorun gereken durumlarda olduğunu bekliyor. Örneğin:

* bir Service Fabric ortamına varolan n katmanlı uygulama "kaldırılmış ve gölgeye" olarak adlandırılmıştır
* bir iş yükü toorun belirli donanım üzerinde performans, Ölçek veya güvenlik yalıtımı nedeniyle istemektedir.
* Bir iş yükü İlkesi ya da kaynak tüketimi nedeniyle diğer iş yüklerini üzerinden olmalıdır

toosupport yapılandırmaları, bu tür Service Fabric uygulanan toonodes olabilir etiketleri birinci sınıf kavramı vardır. Bu etiketler adlı **düğümü özellikleri**. **Kısıtlamalarından** olan hello deyimleri bağlı bir veya daha fazla düğüm özelliklerini seçin tooindividual Hizmetleri. Kısıtlamalarından Hizmetleri çalıştırdığı tanımlar. Merhaba kısıtlamaları Genişletilebilir kümesidir - herhangi bir anahtar/değer çifti çalışabilirsiniz. 

<center>
![Düzen farklı iş yükleri küme][Image5]
</center>

### <a name="built-in-node-properties"></a>Düğüm özellikleri yerleşik
Service Fabric toodefine sahip hello kullanıcı otomatik olarak kullanılabilecek bazı varsayılan düğüm özelliklerini tanımlayan bunları. her düğümde tanımlanan hello varsayılan özelliklerdir hello **NodeType** ve hello **NodeName**. Bu nedenle örneğin yerleştirme kısıtlama olarak yazabilirsiniz `"(NodeType == NodeType03)"`. Genellikle NodeType toobe en yaygın olarak kullanılan hello özelliklerinden biri bulduk. Bir makine türüyle 1:1 karşılık gelen beri yararlı olur. Her makine türünün karşılık gelen bir geleneksel n katmanlı uygulama iş yükündeki tooa türü.

<center>
![Yerleştirme kısıtlamaları ve düğüm özellikleri][Image6]
</center>

## <a name="placement-constraint-and-node-property-syntax"></a>Yerleştirme kısıtlaması ve düğüm özellik sözdizimi 
Merhaba düğümü özelliğinde belirtilen hello değeri veya uzun imzalı bir string, bool, olabilir. Merhaba deyimi hello hizmetine bir yerleştirme adlı *kısıtlaması* hello hizmeti hello kümede burada çalışabilir kısıtlar beri. Merhaba kısıtlaması hello farklı bir düğüme hello küme özelliklerinde çalıştırır herhangi bir Boole ifadesini olabilir. Bu boolean deyimlerinde Hello geçerli seçiciler şunlardır:

1) belirli ifadeleri oluşturmak için koşullu denetimleri

| Deyimi | Sözdizimi |
| --- |:---:|
| "eşit" | "==" |
| "eşit değil" | "!=" |
| "büyüktür" | ">" |
| "değerinden büyük veya eşit" | ">=" |
| "küçüktür" | "<" |
| "küçük veya eşit" | "<=" |

2) gruplandırma ve mantıksal işlemleri için Boole ifadeleri

| Deyimi | Sözdizimi |
| --- |:---:|
| "ve" | "&&" |
| "veya" | "&#124;&#124;" |
| "değil" | "!" |
| "grubu olarak tek bir deyimde" | "()" |

Temel kısıtlama deyimleri bazı örnekleri aşağıda verilmiştir.

  * `"Value >= 5"`
  * `"NodeColor != green"`
  * `"((OneProperty < 100) || ((AnotherProperty == false) && (OneProperty >= 100)))"`

Burada hello genel yerleştirme kısıtlaması deyimi "True" çok değerlendirir yalnızca düğümler üzerinde yerleştirilen hello hizmetine sahip olabilirsiniz. Tanımlanmış bir özellik olmayan düğümleri içeren bu özellik her yerleştirme kısıtlamayla eşleşmiyor.

Düğüm özellikleri verilen düğüm türü için tanımlı aşağıdaki o hello varsayalım:

ClusterManifest.xml

```xml
    <NodeType Name="NodeType01">
      <PlacementProperties>
        <Property Name="HasSSD" Value="true"/>
        <Property Name="NodeColor" Value="green"/>
        <Property Name="SomeProperty" Value="5"/>
      </PlacementProperties>
    </NodeType>
```

tek başına dağıtımlarında ClusterConfig.json ya da Azure için Template.json aracılığıyla kümeleri barındırılan. 

> [!NOTE]
> Azure Resource Manager şablonu hello düğümünüz türü genellikle parametreli. "NodeType01 yerine", "[parameters('vmNodeType1Name')]" gibi görünür.
>

```json
"nodeTypes": [
    {
        "name": "NodeType01",
        "placementProperties": {
            "HasSSD": "true",
            "NodeColor": "green",
            "SomeProperty": "5"
        },
    }
],
```

Hizmet yerleşimi oluşturabilirsiniz *kısıtlamaları* gösterildiği gibi bir hizmet için:

C#

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
serviceDescription.PlacementConstraints = "(HasSSD == true && SomeProperty >= 4)";
// add other required servicedescription fields
//...
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceType -Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementConstraint "HasSSD == true && SomeProperty >= 4"
```

Tüm düğümleri NodeType01 geçerliyse, bu düğüm türü hello kısıtlaması ile öğesini de seçebilirsiniz "(NodeType == NodeType01)".

Merhaba harika bir hizmetin kısıtlamalarından çalışmalarıdır bunlar dinamik olarak çalışma zamanı sırasında güncelleştirilmesi biridir. Bu nedenle gerekiyorsa, bir hizmet hello kümede hareket ettirin, ekleyip kaldırabilirsiniz gereksinimleri, vb.. Service Fabric hello hizmet yukarı ve kullanılabilir bile, bu tür değişiklikleri yapılan kaldığından emin olma mvc'deki.

C# ' TA:

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.PlacementConstraints = "NodeType == NodeType01";
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/app/service"), updateDescription);
```

PowerShell:

```posh
Update-ServiceFabricService -Stateful -ServiceName $serviceName -PlacementConstraints "NodeType == NodeType01"
```

Kısıtlamalarından her farklı adlı hizmet örneği için belirtilir. Güncelleştirmeleri her zaman hello yerine uygulamanız (üzerine yaz) ne daha önce belirtildi.

Merhaba Küme tanımı bir düğümde hello özelliklerini tanımlar. Bir düğümün özelliklerini değiştirme küme yapılandırması yükseltme gerektirir. Bir düğümün özellikleri yükseltme her etkilenen düğüm toorestart tooreport yeni özelliklerini gerektirir. Bunlar çalışırken yükseltme Service Fabric tarafından yönetilir.

## <a name="describing-and-managing-cluster-resources"></a>Açıklayan ve küme kaynaklarını yönetme
Merhaba işleri tüm orchestrator olan toohelp en önemli birini hello küme kaynak tüketimini yönetin. Küme kaynaklarını yönetme farklı şunları anlamına gelebilir. İlk olarak, var. makineler aşırı yüklü olmadığını sağlamaktır. Bu makineler bunlar işleyebileceğinden daha fazla hizmet çalıştırmıyor emin olma anlamına gelir. İkinci olarak, Yük Dengeleme ve kritik toorunning Hizmetleri verimli bir şekilde olan en iyi duruma getirme yoktur. Başkalarının soğuk durumdayken maliyet etkili veya performans hassas hizmet teklifleri bazı düğümler toobe etkin izin veremez. Etkin düğümleri tooresource Çekişme ve düşük performans ve soğuk düğümleri küçülttüğü iyi bir şekilde temsil kaynakları ve artan maliyetleri sağlama. 

Service Fabric kaynakları olarak temsil eden `Metrics`. Toodescribe tooService doku istediğiniz mantıksal veya fiziksel kaynak ölçümleridir. "WorkQueueDepth" veya "MemoryInMb" gibi şeyleri ölçümleri örnekleridir. Düğümlerde Service Fabric yönetebilecek hello fiziksel kaynakları hakkında bilgi için bkz: [kaynak İdaresi](service-fabric-resource-governance.md). Özel ölçümleri ve kullanımları yapılandırma hakkında daha fazla bilgi için bkz: [bu makalede](service-fabric-cluster-resource-manager-metrics.md)

Ölçümleri yerleşimi kısıtlamaları ve düğüm özellikleri farklıdır. Düğüm, statik tanımlayıcıları hello düğümlerin kendilerini özelliklerdir. Ölçümleri düğümünüz kaynaklar ve bir düğümde çalıştırdığınızda hizmetlerini kullanma açıklanmaktadır. Bir düğüm özelliği "HasSSD" olabilir ve tootrue ya da yanlış ayarlayabilirsiniz. kullanılabilir alan miktarını Hello bu SSD ve ne kadar hizmetler tarafından kullanılan "DriveSpaceInMb" gibi bir ölçü olacaktır. 

Merhaba Service Fabric kümesi Kaynak Yöneticisi hello ölçümleri ortalama hangi hello adlarını anlamıyor kısıtlamalarından ve düğüm özellikleri için olduğu gibi önemli toonote olur. Ölçüm adları yalnızca dizelerdir. Bu bir iyi bir uygulama toodeclare belirsiz olabilir, oluşturduğunuz hello ölçüm adları bir parçası olarak birimidir.

## <a name="capacity"></a>Kapasite
Tüm kaynak etkinleştirdiyseniz *Dengeleme*, Service Fabric'ın Küme Kaynak Yöneticisi hala sağlamak hiçbir düğüm kapasitesi sonuçlandı olduğunu. Kapasite taşmaları yönetme hello küme çok dolu veya hello iş yükünün düğümlerinden büyük olduğu sürece mümkündür. Kapasitesi ise başka bir *kısıtlaması* toounderstand bu hello Küme Kaynak Yöneticisi'ni kullanan düğüm bir kaynağın ne kadarının. Kapasite kalan da hello küme için bir bütün olarak izlenir. Merhaba kapasite ve hello tüketim hello hizmeti düzeyinde ölçümleri cinsinden ifade edilir. Bu nedenle örneğin hello ölçüm "ClientConnections" olabilir ve belirli bir düğümün 32768 "ClientConnections" için bir kapasiteye sahip. Diğer düğümlere o düğümü üzerinde çalıştıran bazı hizmet deyin, şu anda "ClientConnections" Merhaba ölçüsünün 32256 kullanan diğer sınırlamaları olabilir.

Çalışma zamanı sırasında Kalan kapasite hello kümedeki ve düğümlere hello küme Resource Manager izler. Sipariş tootrack kapasite hello Küme Kaynağı Yöneticisi her hizmetin kullanımı hello hizmetinin çalıştığı düğümün kapasiteden çıkarır. Bu bilgiyle nereye hello Service Fabric kümesi Kaynak Yöneticisi şekil tooplace veya düğüm kapasitesi geçmez, böylece çoğaltmaları taşıyın.

<center>
![Küme düğümlerini ve kapasite][Image7]
</center>

C# ' TA:

```csharp
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
ServiceLoadMetricDescription metric = new ServiceLoadMetricDescription();
metric.Name = "ClientConnections";
metric.PrimaryDefaultLoad = 1024;
metric.SecondaryDefaultLoad = 0;
metric.Weight = ServiceLoadMetricWeight.High;
serviceDescription.Metrics.Add(metric);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("ClientConnections,High,1024,0)
```

Merhaba küme bildiriminde tanımlanan kapasiteleri görebilirsiniz:

ClusterManifest.xml

```xml
    <NodeType Name="NodeType03">
      <Capacities>
        <Capacity Name="ClientConnections" Value="65536"/>
      </Capacities>
    </NodeType>
```

tek başına dağıtımlarında ClusterConfig.json ya da Azure için Template.json aracılığıyla kümeleri barındırılan. 

```json
"nodeTypes": [
    {
        "name": "NodeType03",
        "capacities": {
            "ClientConnections": "65536",
        }
    }
],
```

Yaygın olarak bir hizmetin değişiklikleri dinamik olarak yükleyin. "ClientConnections" yineleme yükünü 1024 too2048 ancak çalışan ardından yalnızca o ölçüm için kalan 512 kapasitesi olduğu hello düğümü değiştiğini söyleyin. Bu düğüm üzerinde yeterli alan olmadığından şimdi bu çoğaltma veya örneğinin yerleştirme, geçersiz. Merhaba küme Resource Manager tookick sahiptir ve hello düğüm kapasitesi aşağıda geri alın. Bu düğüm tooother düğümlerden biri veya daha fazla hello çoğaltmaları veya örnekleri taşıyarak kapasitesi ise hello düğümü üzerindeki yükü azaltır. Çoğaltmaları taşırken hello küme kaynak yöneticisi bu hareketleri toominimize hello maliyetini çalışır. Taşıma maliyeti ele alınmıştır [bu makalede](service-fabric-cluster-resource-manager-movement-cost.md) daha hakkında hello küme Resource Manager stratejileri dengelenmesi ve kurallar açıklanmaktadır [burada](service-fabric-cluster-resource-manager-metrics.md).

## <a name="cluster-capacity"></a>Küme kapasite
Nasıl hello Service Fabric kümesi Kaynak Yöneticisi Koru hello genel çok tam olmasını küme? İyi yok çok dinamik yük ile bunu yapabilirsiniz. Hizmetleri hello küme kaynak yöneticisi tarafından gerçekleştirilen eylemler bağımsız olarak kendi yük depo olabilir. Sonuç olarak, yarın ünlü olduğunda kümenizle yeterli boş alan bugün underpowered olabilir. Bu, tooprevent sorunlarını baked bazı denetimler vardır belirtti. yapabiliriz hello ilk hello küme toobecome tam neden olacağından yeni iş yüklerine hello oluşturulmasını engellemek şeydir.

Durum bilgisi olmayan bir hizmet oluşturmak ve onunla ilişkili bazı yük sahip söyleyin. Merhaba hizmet hello "DiskSpaceInMb" ölçüm hakkında cares varsayalım. Ayrıca, devam eden tooconsume beş birimleri hello hizmetinin her örneği için "DiskSpaceInMb" olduğunu düşünelim. Toocreate üç hello hizmet örneklerini istiyor. Harika! Böylece "DiskSpaceInMb" toobe 15 birimleri ihtiyacımız anlamına gelir hello küme bize sırayla tooeven sunmak mümkün toocreate bu hizmet örneği olabilir. Merhaba küme Resource Manager sürekli hello kapasitesi ve her ölçümü tüketimini hesaplar hello kümede hello kalan kapasite belirleyebilirsiniz. Yeterli alan yoksa hello küme Resource Manager reddeder hello hizmeti çağrısı oluşturun.

Merhaba gereksinim yalnızca 15 birimler kullanılabilir olmadığından, bu alanı birçok farklı yolu ayrılamadı. Örneğin, olabilir bir kalan birim kapasitesi 15 farklı düğümlerde ya da üç kalan birim kapasitesi beş farklı düğümlerde. Bu yüzden beş birimler kullanılabilir üç düğümlerinde hello küme Resource Manager şeyler düzenleyebilirsiniz hello hizmeti yerleştirir. Düzenler hello küme genellikle hello küme dolmak veya hello varolan Hizmetleri herhangi bir nedenden dolayı birleştirilmiş olamaz sürece mümkündür.

## <a name="buffered-capacity"></a>Arabelleğe alınan kapasite
Arabelleğe alınan kapasite hello Küme Kaynak Yöneticisi'ni başka bir özelliğidir. Merhaba kısmı ayırma sağlar genel düğüm kapasitesi. Bu kapasite arabellek yalnızca kullanılan tooplace yükseltmeleri ve düğüm hataları sırasında hizmetleridir. Arabelleğe alınan kapasite ölçüm tüm düğümler için başına genel olarak belirtilir. ayrılmış hello kapasiteyi çekme hello değeri hello sayıda hata ve yükseltme hello kümedeki sahip etki alanları bir işlevdir. Daha fazla hata ve yükseltme etki alanları anlamına gelir için arabelleğe alınan kapasite daha düşük bir sayı seçebilirsiniz. Daha fazla etki alanı varsa, küme toobe daha küçük miktarda kullanılabilir yükseltmeleri ve hataları sırasında bekleyebilirsiniz. Belirtilen hello düğüm kapasitesi bir ölçüm için ayrıca varsa arabelleğe alınan kapasite belirtme yalnızca anlamlıdır.

Aşağıda, nasıl toospecify kapasite arabelleğe ilişkin bir örnek verilmiştir:

ClusterManifest.xml

```xml
        <Section Name="NodeBufferPercentage">
            <Parameter Name="SomeMetric" Value="0.15" />
            <Parameter Name="SomeOtherMetric" Value="0.20" />
        </Section>
```

tek başına dağıtımlarında ClusterConfig.json ya da Azure için Template.json aracılığıyla kümeleri barındırılan:

```json
"fabricSettings": [
  {
    "name": "NodeBufferPercentage",
    "parameters": [
      {
          "name": "SomeMetric",
          "value": "0.15"
      },
      {
          "name": "SomeOtherMetric",
          "value": "0.20"
      }
    ]
  }
]
```

Merhaba küme bir ölçüm için arabelleğe alınan kapasite dışında olduğunda yeni hizmetleri hello oluşturma başarısız olur. Yeni hizmetler toopreserve hello arabellek Hello oluşturulmasını önleme yükseltmeleri ve hataları düğümleri toogo kapasite aşımı neden yok sağlar. Arabelleğe alınan kapasite isteğe bağlıdır, ancak bir ölçüm için bir kapasite tanımlayan herhangi bir küme önerilir.

Merhaba küme kaynak yöneticisi bu yük bilgilerini gösterir. Her ölçüm için bu bilgileri içerir: 
  - Merhaba kapasite ayarlarını arabelleğe alındı.
  - Merhaba toplam kapasite
  - Merhaba geçerli tüketim
  - Dengeli veya her ölçümü olup olmadığı kabul edilir
  - Merhaba standart sapma hakkındaki istatistiklerdir
  - en fazla ve en az yük hello olan hello düğümler  
  
Aşağıdaki örnek, çıktı olarak bakın:

```posh
PS C:\Users\user> Get-ServiceFabricClusterLoadInformation
LastBalancingStartTimeUtc : 9/1/2016 12:54:59 AM
LastBalancingEndTimeUtc   : 9/1/2016 12:54:59 AM
LoadMetricInformation     :
                            LoadMetricName        : Metric1
                            IsBalancedBefore      : False
                            IsBalancedAfter       : False
                            DeviationBefore       : 0.192450089729875
                            DeviationAfter        : 0.192450089729875
                            BalancingThreshold    : 1
                            Action                : NoActionNeeded
                            ActivityThreshold     : 0
                            ClusterCapacity       : 189
                            ClusterLoad           : 45
                            ClusterRemainingCapacity : 144
                            NodeBufferPercentage  : 10
                            ClusterBufferedCapacity : 170
                            ClusterRemainingBufferedCapacity : 125
                            ClusterCapacityViolation : False
                            MinNodeLoadValue      : 0
                            MinNodeLoadNodeId     : 3ea71e8e01f4b0999b121abcbf27d74d
                            MaxNodeLoadValue      : 15
                            MaxNodeLoadNodeId     : 2cc648b6770be1bc9824fa995d5b68b1
```

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba mimarisi ve bilgi akışını hello küme Resource Manager içinde hakkında daha fazla bilgi için kullanıma [bu makalede](service-fabric-cluster-resource-manager-architecture.md)
* Birleştirme ölçümleri tanımlama tek yönlü tooconsolidate yayılmak yerine düğümlerde yüktür. toolearn nasıl tooconfigure birleştirme, çok bakın[bu makalede](service-fabric-cluster-resource-manager-defragmentation-metrics.md)
* Merhaba baştan başlatın ve [giriş toohello Service Fabric kümesi Kaynak Yöneticisi Al](service-fabric-cluster-resource-manager-introduction.md)
* toofind hello Küme Kaynak Yöneticisi yönetir ve dengeleyen hello kümedeki yük hakkında hello makalesine üzerinde kullanıma [Yük Dengeleme](service-fabric-cluster-resource-manager-balancing.md)

[Image1]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-domains.png
[Image2]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-uneven-fault-domain-layout.png
[Image3]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domains-with-placement.png
[Image4]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domain-layout-strategies.png
[Image5]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-layout-different-workloads.png
[Image6]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-placement-constraints-node-properties.png
[Image7]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-nodes-and-capacity.png
