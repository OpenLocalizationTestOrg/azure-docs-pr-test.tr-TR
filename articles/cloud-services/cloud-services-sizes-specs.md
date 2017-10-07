---
title: "Azure Cloud services aaaVirtual makine boyutları | Microsoft Docs"
description: "Merhaba başka bir sanal makine boyutları (ve kimlikler) için Azure bulut hizmeti web ve çalışan rolleri listeler."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 1127c23e-106a-47c1-a2e9-40e6dda640f6
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 93d91a67afc352f3d18c31e0dd5cf976bf46350c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sizes-for-cloud-services"></a>Cloud Services boyutları
Bu konuda hello kullanılabilir boyutları ve bulut Hizmeti rol örnekleri (web rolleri ve çalışan rolleri) için seçenekleri açıklar. Ayrıca, dağıtım konuları toobe toouse bu kaynakları planlarken göz önünde sağlar. İçine bir kimliği her boyutuna sahip, [hizmet tanımı dosyası](cloud-services-model-and-package.md#csdef). Her boyutu fiyatları hello üzerinde kullanılabilir olan [Cloud Services fiyatlandırması](https://azure.microsoft.com/pricing/details/cloud-services/) sayfası.

> [!NOTE]
> toosee ilgili Azure sınırları, bkz: [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../azure-subscription-service-limits.md)
>
>

## <a name="sizes-for-web-and-worker-role-instances"></a>Web ve çalışan rolü örnekleri için Boyutlar
Azure üzerinde gelen birden çok standart boyutları toochoose vardır. Bu boyutlarla ilgili önemli noktalardan bazıları şunlardır:

* D-serisi VM'ler, daha yüksek işlem gücü ve geçici disk performans talep tasarlanmış toorun uygulamalarıdır. D-serisi VM'ler hello geçici disk için daha hızlı işlemcilerde, daha yüksek bellek çekirdek oranı ve katı hal sürücüsü (SSD) sağlayın. Merhaba duyuru hello Azure blogu hakkında ayrıntılar için bkz [yeni D-serisi sanal makine boyutlarını](https://azure.microsoft.com/blog/2014/09/22/new-d-series-virtual-machine-sizes/).
* Dv2 serisi, takip toohello özgün D-serisi, daha güçlü bir CPU özellikleri. Merhaba Dv2 serisi CPU yaklaşık %35 hello daha hızlı D-serisi CPU'dur. En son nesil hello üzerinde temel aldığı 2.4 GHz Intel Xeon® E5-2673 v3 (Haswell) işlemci ve hello Intel Turbo artırma teknolojisi 2.0 GHz too3.1 gidebilirsiniz. Merhaba Dv2 serisi sahip D-serisi hello gibi aynı bellek ve disk yapılandırmalarını hello.
* G-serisi VM'ler hello en fazla belleği sunar ve Intel Xeon E5 V3 ailesi işlemcilere sahip konaklarda çalıştırın.
* Merhaba A-series VM'ler çeşitli donanım türleri ve işlemciler üzerinde dağıtılabilir. Merhaba boyutu hello donanım, üzerinde dağıtılan hello donanım bakılmaksızın örneğini çalıştıran hello için toooffer tutarlı işlemci performansı göre kısıtlanır. üzerinde bu boyut dağıtılır, toodetermine hello fiziksel donanım sorgu hello sanal donanım hello sanal makine içinde.
* Merhaba A0 boyutu hello fiziksel donanım üzerinde aşırı abone olur. Bu belirli boyutu için yalnızca diğer müşteri dağıtımları hello çalışan İş yükünüzün performansını etkileyebilir. Merhaba göreli performans konu tooan yaklaşık çeşitliliği yüzde 15 Beklenen hello temel aşağıda gösterilmiştir.

Merhaba fiyatlandırma Hello hello sanal makinenin boyutunu etkiler. Merhaba boyutu hello işleme, bellek ve depolama kapasitesini hello sanal makine de etkiler. Depolama maliyetleri hello depolama hesabında kullanılan sayfa ayrı ayrı göre hesaplanır. Ayrıntılar için bkz [Cloud Services fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/cloud-services/) ve [Azure Storage fiyatlandırması](https://azure.microsoft.com/pricing/details/storage/).

ilgili önemli noktalar aşağıdaki hello bir boyutuna karar vermenize yardımcı olabilir:

* Merhaba A8-A11 ve H-serisi boyutları olarak da bilinir: *işlem yoğunluklu örnekler*. Bu boyutlar çalıştıran hello donanım tasarlanmış ve işlem yoğunluklu için en iyi duruma getirilmiş ve ağ kullanımı yoğun uygulamalar, yüksek performanslı bilgi işlem (HPC) dahil olmak üzere uygulamalar, model ve benzetimleri küme. Merhaba A8-A11 serisi Intel Xeon E5-2670 2.6 GHZ @ ve Intel Xeon E5-2667 v3 3,2 GHz @ hello H-serisi kullanır. Ayrıntılı bilgi ve bu boyutları kullanma hakkında dikkat edilecek noktalar için bkz: [yüksek performanslı işlem VM boyutları](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Dv2 serisi, D-serisi, G serisi, daha hızlı CPU talep uygulamaları için ideal, daha iyi yerel disk performans ya da daha yüksek bellek taleplerini sahip. Bu seçenekler birçok kurumsal sınıf uygulama için güçlü bir bileşim sunar.
* Azure veri merkezlerinde hello fiziksel ana bilgisayarların bazıları A5 gibi– daha büyük sanal makine boyutları A11 desteklemeyebilir. Sonuç olarak, hello hata iletisi görebilirsiniz **başarısız tooconfigure sanal makine {makine adı}** veya **başarısız toocreate sanal makine {makine adı}** yeni bir varolan sanal makine tooa boyutlandırırken size; 16 Nisan 2013'ten önce oluşturulan bir sanal ağda yeni bir sanal makine oluşturma; veya yeni bir sanal makine tooan mevcut bulut hizmeti ekleme. Bkz: [hata: "Başarısız tooconfigure sanal makinesi"](https://social.msdn.microsoft.com/Forums/9693f56c-fcd3-4d42-850e-5e3b56c7d6be/error-failed-to-configure-virtual-machine-with-a5-a6-or-a7-vm-size?forum=WAVirtualMachinesforWindows) hello destek Forumunda her dağıtım senaryosu için geçici çözümler için.
* Aboneliğinizi Ayrıca belirli boyutu ailelerini dağıtabilirsiniz çekirdek hello sayısını sınırlayabilir. tooincrease bir kota Azure desteğine başvurun.

## <a name="performance-considerations"></a>Performansla ilgili önemli noktalar
Performansınızı hello Azure işlem birimi (ACU) tooprovide Azure SKU'ları ve büyük olasılıkla toosatisfy SKU olan tooidentify üzerinden bilgi işlem (CPU) performans karşılaştırma bir şekilde hello kavramı oluşturduk gerekiyor.  ACU şu anda Küçük (Standard_A1) VM'de 100 olarak standart haline getirilmiş ve diğer tüm SKU'lar, standart bir karşılaştırmalı testte sunabilecekleri yaklaşık hıza göre derecelendirilmiştir.

> [!IMPORTANT]
> Merhaba ACU yalnızca bir kılavuz olarak sağlanmıştır. iş yükü Hello sonuçları değişebilir.
>
>

<br>

| SKU Ailesi | ACU/Çekirdek |
| --- | --- |
| [ExtraSmall](#a-series) |50 |
| [Küçük ExtraLarge](#a-series) |100 |
| [A5-7](#a-series) |100 |
| [Standard_A1-8v2](#av2-series) |100 |
| [Standard_A2m-8mv2](#av2-series) |100 |
| [A8-A11](#a-series) |225* |
| [D1-14](#d-series) |160 |
| [D1-15v2](#dv2-series) |210-250* |
| [G1-5](#g-series) |180-240* |
| [H](#h-series) |290-300* |

İle işaretlenen ACUs bir * Intel® Turbo teknolojisi tooincrease CPU sıklığı kullanın ve performans artışı sağlar. Merhaba hello artırma miktarı hello VM boyutu, iş yükü ve hello üzerinde çalışan diğer iş yüklerini göre değişebilir aynı ana bilgisayar.

## <a name="size-tables"></a>Boyut tabloları
Merhaba aşağıdaki tablolarda hello boyutları ve sağladıkları hello kapasiteleri gösterilmektedir.

* Depolama kapasitesi GiB veya 1024^3 bayt cinsinden gösterilmiştir. Ne zaman diskleri karşılaştırma cinsinden ölçülen GB (1000 ^ 3 bayt) toodisks Gib'den içinde ölçülen (1024 ^ 3) kapasite numaraları Gib'den içinde verilen daha küçük olarak görünebilir unutmayın. Örneğin: 1023 GiB = 1098,4 GB
* Disk aktarım hızı, saniye başına giriş/çıkış işlemi sayısı (IOPS) ve MB/sn (MB/sn = 10^6 bayt/sn) üzerinden ölçülür.
* Veri diskleri önbelleğe alınmış veya alınmamış modlarda çalışabilir. Önbelleğe alınan veriler disk işlemi için çok hello konak önbellek modunu ayarlayın**ReadOnly** veya **ReadWrite**. Önbelleğe alınmamış veri diski işlemi için çok hello konağı önbellek modunu ayarla**hiçbiri**.
* En fazla ağ bant genişliği ayrılmış ve VM türü başına atanan hello maksimum toplanan bant genişliği ' dir. Merhaba sağ VM türü tooensure yeterli ağ kapasitesi seçmek için Kılavuzlar mevcuttur Hello en yüksek bant genişliği sağlar. Düşük, Orta, yüksek ve çok yüksek arasında taşırken uygun şekilde hello verimliliğini artırır. Gerçek ağ performansı, ağ ve uygulama yüklerinin yanı sıra uygulama ağ ayarları gibi birçok faktöre bağlıdır.

## <a name="a-series"></a>A Serisi
| Boyut            | CPU çekirdekleri | Bellek: GiB  | Yerel HDD: GiB       | Maksimum NIC/Ağ bant genişliği |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| ExtraSmall      | 1         | 0,768        | 20                   | 1/düşük |
| Küçük           | 1         | 1,75         | 225                  | 1/orta |
| Orta          | 2         | 3,5 GB       | 490                  | 1/orta |
| Büyük           | 4         | 7            | 1000                 | 2/yüksek |
| ExtraLarge      | 8         | 14           | 2040                 | 4/yüksek |
| A5              | 2         | 14           | 490                  | 1/orta |
| A6              | 4         | 28           | 1000                 | 2/yüksek |
| A7              | 8         | 56           | 2040                 | 4/yüksek |

## <a name="a-series---compute-intensive-instances"></a>A Serisi - Yoğun işlem gücü kullanımlı örnekler
Bilgi ve bu boyutları kullanma hakkında dikkat edilecek noktalar için bkz: [yüksek performanslı işlem VM boyutları](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

| Boyut            | CPU çekirdekleri | Bellek: GiB  | Yerel HDD: GiB       | Maksimum NIC/Ağ bant genişliği |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| A8 *             |8          | 56           | 1817                 | 2/yüksek |
| A9 *             |16         | 112          | 1817                 | 4/çok yüksek |
| A10             |8          | 56           | 1817                 | 2/yüksek |
| A11             |16         | 112          | 1817                 | 4/çok yüksek |

\*RDMA özellikli

## <a name="av2-series"></a>Av2 Serisi

| Boyut            | CPU çekirdekleri | Bellek: GiB  | Yerel SSD: GiB       | Maksimum NIC/Ağ bant genişliği |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_A1_v2  | 1         | 2            | 10                   | 1/orta                 |
| Standard_A2_v2  | 2         | 4            | 20                   | 2/orta                 |
| Standard_A4_v2  | 4         | 8            | 40                   | 4/yüksek                     |
| Standard_A8_v2  | 8         | 16           | 80                   | 8/yüksek                     |
| Standard_A2m_v2 | 2         | 16           | 20                   | 2/orta                 |
| Standard_A4m_v2 | 4         | 32           | 40                   | 4/yüksek                     |
| Standard_A8m_v2 | 8         | 64           | 80                   | 8/yüksek                     |


## <a name="d-series"></a>D Serisi
| Boyut            | CPU çekirdekleri | Bellek: GiB  | Yerel SSD: GiB       | Maksimum NIC/Ağ bant genişliği |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_D1     | 1         | 3,5          | 50                   | 1/orta |
| Standard_D2     | 2         | 7            | 100                  | 2/yüksek |
| Standard_D3     | 4         | 14           | 200                  | 4/yüksek |
| Standard_D4     | 8         | 28           | 400                  | 8/yüksek |
| Standard_D11    | 2         | 14           | 100                  | 2/yüksek |
| Standard_D12    | 4         | 28           | 200                  | 4/yüksek |
| Standard_D13    | 8         | 56           | 400                  | 8/yüksek |
| Standard_D14    | 16        | 112          | 800                  | 8/çok yüksek |

## <a name="dv2-series"></a>Dv2 Serisi
| Boyut            | CPU çekirdekleri | Bellek: GiB  | Yerel SSD: GiB       | Maksimum NIC/Ağ bant genişliği |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_D1_v2  | 1         | 3,5          | 50                   | 1/orta |
| Standard_D2_v2  | 2         | 7            | 100                  | 2/yüksek |
| Standard_D3_v2  | 4         | 14           | 200                  | 4/yüksek |
| Standard_D4_v2  | 8         | 28           | 400                  | 8/yüksek |
| Standard_D5_v2  | 16        | 56           | 800                  | 8/aşırı yüksek |
| Standard_D11_v2 | 2         | 14           | 100                  | 2/yüksek |
| Standard_D12_v2 | 4         | 28           | 200                  | 4/yüksek |
| Standard_D13_v2 | 8         | 56           | 400                  | 8/yüksek |
| Standard_D14_v2 | 16        | 112          | 800                  | 8/aşırı yüksek |
| İçin Standard_D15_v2 | 20        | 140          | 1000                | 8/aşırı yüksek |

## <a name="g-series"></a>G Serisi
| Boyut            | CPU çekirdekleri | Bellek: GiB  | Yerel SSD: GiB       | Maksimum NIC/Ağ bant genişliği |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_G1     | 2         | 28           | 384                  |1/yüksek |
| Standard_G2     | 4         | 56           | 768                  |2/yüksek |
| Standard_G3     | 8         | 112          | 1536                |4/çok yüksek |
| Standard_G4     | 16        | 224          | 3072                |8/aşırı yüksek |
| Standard_G5     | 32        | 448          | 6144                |8/aşırı yüksek |

## <a name="h-series"></a>H Serisi
Azure H-serisi sanal makine VM'ler molecular modelleme ve hesaplama sıvı dinamiği gibi yüksek son hesaplama gereksinimlerine yönelik hello İleri nesil yüksek performanslı bilgi işlem yok. Bu 8 ve 16 çekirdek VM'ler DDR4 bellek ve yerel SSD tabanlı depolama hello Intel Haswell E5-2667 V3 işlemci teknolojisi üzerinde oluşturulmuştur.

Ayrıca toohello önemli ölçüde CPU gücü hello H-serisi FDR InfiniBand ve birkaç bellek yapılandırmaları toosupport bellek yoğun hesaplama gereksinimleri kullanarak düşük gecikme süresi RDMA ağ için çeşitli seçenekler sunar.

| Boyut            | CPU çekirdekleri | Bellek: GiB  | Yerel SSD: GiB       | Maksimum NIC/Ağ bant genişliği |
|---------------- | --------- | ------------ | -------------------- | ---------------------------- |
| Standard_H8     | 8         | 56           | 1000                 | 8/yüksek |
| Standard_H16    | 16        | 112          | 2000                 | 8/çok yüksek |
| Standard_H8m    | 8         | 112          | 1000                 | 8/yüksek |
| Standard_H16m   | 16        | 224          | 2000                 | 8/çok yüksek |
| Standard_H16r*  | 16        | 112          | 2000                 | 8/çok yüksek |
| Standard_H16mr* | 16        | 224          | 2000                 | 8/çok yüksek |

\*RDMA özellikli

## <a name="configure-sizes-for-cloud-services"></a>Bulut Hizmetleri için boyutlarını yapılandırma
Merhaba hizmet modeli hello tarafından açıklanan bir parçası olarak bir rol örneği hello sanal makine boyutu belirtebilirsiniz [hizmet tanımı dosyası](cloud-services-model-and-package.md#csdef). Merhaba rol Hello boyutu hello CPU çekirdek sayısı, hello bellek kapasitesi ve örneğini çalıştıran tooa ayrılan hello yerel dosya sistemi boyutunu belirler. Uygulamanızın kaynak gereksinimi temel alan hello rol boyutunu seçin.

Merhaba rol boyutunu toobe ayarlama örneği [Standard_D2](#general-purpose-d) Web rol örneği için:

```xml
<WorkerRole name="Worker1" vmsize="Standard_D2">
...
</WorkerRole>
```

## <a name="changing-hello-size-of-an-existing-role"></a>Mevcut bir rolü Hello boyutunu değiştirme

İş yükü değişiklikleri veya kullanılabilir hale yeni VM boyutları Hello yapısı toochange hello rolünüze boyutunu isteyebilirsiniz. gerekir (yukarıda gösterildiği gibi), hizmet tanımı dosyasında hello VM boyutunu değiştirmek, bulut hizmetinizin yeniden paketleyin ve bunu dağıtmak için toodo. Bu olası toochange VM boyutları doğrudan hello portal veya PowerShell değil.

>[!TIP]
> Toouse farklı VM boyutları için rolünüze farklı ortamlarda (ör. istediğiniz VS üretim test). Tek yönlü toodo bu birden çok hizmet açıklaması (.csdef) dosyalarını projenizde toocreate olduğundan, sonra farklı bir bulut ortamı başına hizmet paketleri hello CSPack aracını kullanarak, otomatik derleme sırasında oluşturun. toolearn Bulutu hello öğeleri hakkında daha fazla paket Hizmetleri ve nasıl toocreate, görebileceği [hizmetleri modeli hello bulut nedir ve nasıl ı paket onu?](cloud-services-model-and-package.md)
>
>

## <a name="get-a-list-of-sizes"></a>Boyutlarının listesini al
PowerShell veya hello REST API tooget boyutlarının listesini kullanabilirsiniz. Merhaba REST API belgelenen [burada](https://msdn.microsoft.com/library/azure/dn469422.aspx). Merhaba aşağıdaki bulut hizmetiniz için şu anda kullanılabilir tüm hello boyutları listeler bir PowerShell komut kodudur.

```powershell
Get-AzureRoleSize | where SupportedByWebWorkerRoles -eq $true | select InstanceSize
```

## <a name="next-steps"></a>Sonraki adımlar
* [Azure aboneliği ve hizmet limitleri, kotalar ve kısıtlamalar](../azure-subscription-service-limits.md) hakkında bilgi edinin.
* Daha fazla bilgi edinin [VM boyutları hakkında yüksek performanslı işlem](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) HPC iş yükleri için.
