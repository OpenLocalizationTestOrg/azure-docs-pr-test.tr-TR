---
title: "aaaCapacity ve Azure günlük analizi performans çözümde | Microsoft Docs"
description: "Kullanım hello kapasite ve performans günlük analizi toohelp anladığınızdan çözümde hello kapasite, Hyper-V sunucularının."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 51617a6f-ffdd-4ed2-8b74-1257149ce3d4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: c47bb1e8bb9d4460b0241e89a616f3b356844b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="plan-hyper-v-virtual-machine-capacity-with-hello-capacity-and-performance-solution-preview"></a>Hyper-V sanal makine kapasiteyle hello kapasite ve performans çözüm (Önizleme) planlama

![Kapasite ve performans simgesi](./media/log-analytics-capacity/capacity-solution.png)

Günlük analizi toohelp anladığınızdan performans çözümde hello kapasite, Hyper-V sunucularının ve hello kapasite kullanabilirsiniz. Hyper-V ortamınızı, göstererek Öngörüler hello konakları genel kullanımı (CPU, bellek ve disk) hello ve bu Hyper-V konakları üzerinde çalışan sanal makineleri hello Hello çözümü sağlar. Ölçüm, tüm tüm konaklar ve onların üzerinde çalışan hello VM'ler arasında CPU, bellek ve disk için toplanır.

Merhaba çözüm:

-   En yüksek ve düşük CPU ve bellek kullanımı ile ana bilgisayarları gösterir
-   En yüksek ve düşük CPU ve bellek kullanımı ile sanal makineleri gösterir
-   En yüksek ve en düşük IOPS ve üretilen iş kullanımı ile sanal makineleri gösterir
-   Sanal makineleri hangi ana bilgisayarlarında çalışan gösterir
-   Yüksek verimlilik, IOPS, üst disklerle hello ve gecikme Küme Paylaşılan Birimleri gösterir
- Toocustomize ve gruplara göre filtre sağlar

> [!NOTE]
> Merhaba kapasite ve performans çözümü kapasite yönetimi adlı önceki sürümü Hello System Center Operations Manager ve System Center Virtual Machine Manager gerekli. Bu güncelleştirilmiş çözüm bu bağımlılıkların yok.


## <a name="connected-sources"></a>Bağlı kaynaklar

Aşağıdaki tablonun hello bu çözümü tarafından desteklenen hello bağlı kaynakları açıklar.

| Bağlı Kaynak | Destek | Açıklama |
|---|---|---|
| [Windows aracıları](log-analytics-windows-agents.md) | Evet | Merhaba çözüm Windows aracılardan kapasite ve performans veri bilgilerini toplar. |
| [Linux aracıları](log-analytics-linux-agents.md) | Hayır    | Merhaba çözüm doğrudan Linux aracılarını kapasite ve performans verileri bilgi toplamaz.|
| [SCOM yönetim grubu](log-analytics-om-agents.md) | Evet |Merhaba çözüm bağlı SCOM yönetim grubunda aracıları kapasite ve performans verilerini toplar. Merhaba SCOM Aracısı tooOMS arasında doğrudan bağlantı gerekli değildir. Veri hello yönetim grubu toohello OMS depodan iletilir.|
| [Azure depolama hesabı](log-analytics-azure-storage.md) | Hayır | Azure depolama kapasite ve performans verilerini içermez.|

## <a name="prerequisites"></a>Ön koşullar

- Windows Server 2012 veya daha yüksek Hyper-V konakları, sanal makineler üzerinde Windows veya Operations Manager aracıları yüklenmelidir.


## <a name="configuration"></a>Yapılandırma

Adım tooadd hello kapasite ve performans çözüm tooyour çalışma alanı aşağıdaki hello gerçekleştirin.

- Kapasite hello hello işlemi kullanarak performans çözüm tooyour OMS çalışma açıklanan ekleyip [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).

## <a name="management-packs"></a>Yönetim paketleri

SCOM yönetim grubunuzu bağlı tooyour OMS çalışma ise, bu çözüm eklediğinizde, sonra Yönetim paketleri aşağıdaki hello SCOM yüklenir. Bu yönetim paketleri için bir yapılandırma veya bakım gerekmez.

- Microsoft.IntelligencePacks.CapacityPerformance

Merhaba 1201 olay benzer:


```
New Management Pack with id:"Microsoft.IntelligencePacks.CapacityPerformance", version:"1.10.3190.0" received.
```

Merhaba kapasite ve performans çözüm güncelleştirildiğinde hello sürüm numarasını değiştirir.

Çözüm yönetim paketleri güncelleştirilme biçimini daha fazla bilgi için bkz: [Operations Manager bağlanmak tooLog Analytics](log-analytics-om-agents.md).

## <a name="using-hello-solution"></a>Merhaba çözümünü kullanarak

Merhaba kapasite ve performans çözüm tooyour çalışma eklediğinizde, hello kapasite ve performans toohello genel bakış Panosu'na eklenir. Bu kutucuğu hello şu anda etkin Hyper-V konakları hello sayısını ve dönem seçili hello süredir izlenmekte etkin sanal makinelere sayısını görüntüler.

![Kapasite ve performans bölmesi](./media/log-analytics-capacity/capacity-tile.png)


### <a name="review-utilization"></a>Gözden geçirme kullanımı

Merhaba kapasite'ı tıklatın ve kapasite ve performans performans döşeme tooopen hello Pano. Merhaba Pano aşağıdaki tablonun hello hello sütunları içerir. Her sütun sütunun ölçütleri hello için kapsam ve zaman aralığını belirtilen eşleşen tooten öğeleri listeler. Tıklayarak tüm kayıtları döndüren bir günlük arama çalıştırabilirsiniz **tümünü görmek** hello altındaki hello sütununun veya hello sütun başlığını tıklatarak.

- **Ana bilgisayarlar**
    - **Ana bilgisayar CPU kullanımı** grafik eğilimini ana bilgisayarları hello CPU kullanımı ve süre seçili hello üzerinde tabanlı ana bilgisayar listesini gösterir. Merhaba çizgi grafiği tooview belirli bir noktaya ayrıntılarını zamanında üzerine gelerek. Merhaba grafik tooview günlük arama Ayrıntılar'ı tıklatın. Tüm ana bilgisayar adı tooopen günlük Ara'yı tıklatın ve barındırılan sanal makineleri için CPU sayaç ayrıntıları görüntüleyin.
    - **Ana bilgisayar bellek kullanımı** grafik eğilimini ana bilgisayarları hello bellek kullanımı ve süre seçili hello üzerinde tabanlı ana bilgisayar listesini gösterir. Merhaba çizgi grafiği tooview belirli bir noktaya ayrıntılarını zamanında üzerine gelerek. Merhaba grafik tooview günlük arama Ayrıntılar'ı tıklatın. Tüm ana bilgisayar adı tooopen günlük arama ve görünüm bellek sayacı ayrıntılarını barındırılan VM'ler için tıklatın.
- **Sanal Makineler**
    - **VM CPU kullanımı** grafik eğilimini sanal makinelerin hello CPU kullanımı ve sanal makinelerin, süre seçili hello üzerinde bağlı listesini gösterir. Merhaba top için 3 VM hello çizgi grafiği tooview belirli bir noktaya ayrıntılarını zamanında üzerine gelerek. Merhaba grafik tooview günlük arama Ayrıntılar'ı tıklatın. Tüm VM adı tooopen günlük Ara'yı tıklatın ve hello VM toplanmış CPU sayaç ayrıntılarını görüntüleyin.
    - **VM bellek kullanımı** grafik eğilimini hello bellek kullanımı sanal makineler ve sanal makinelerin, süre seçili hello üzerinde bağlı listesini gösterir. Merhaba top için 3 VM hello çizgi grafiği tooview belirli bir noktaya ayrıntılarını zamanında üzerine gelerek. Merhaba grafik tooview günlük arama Ayrıntılar'ı tıklatın. Tüm VM adı tooopen günlük Ara'yı tıklatın ve toplanan bellek sayaç hello VM ayrıntılarını görüntüleyin.
    - **VM toplam Disk IOPS** hello grafik eğilimini toplam gösterir sanal makineler ve sanal makinelerin her biri için hello IOPS ile listesini IOPS disk tabanlı süre seçili hello üzerinde. Merhaba top için 3 VM hello çizgi grafiği tooview belirli bir noktaya ayrıntılarını zamanında üzerine gelerek. Merhaba grafik tooview günlük arama Ayrıntılar'ı tıklatın. Herhangi bir VM adı tooopen günlük arama ve toplanan disk IOPS sayaç hello VM için Ayrıntıları Görüntüle'yi tıklatın.
    - **VM toplam Disk verim** sanal makineler ve her hello toplam disk verimliliğini ile sanal makinelerin listesini, temel alınarak hello hello toplam disk verimliliğini grafik eğilimini seçili zaman aralığı gösterir. Merhaba top için 3 VM hello çizgi grafiği tooview belirli bir noktaya ayrıntılarını zamanında üzerine gelerek. Merhaba grafik tooview günlük arama Ayrıntılar'ı tıklatın. Tüm VM adı tooopen günlük Ara'yı tıklatın ve toplanan toplam disk verimlilik sayaç hello VM ayrıntılarını görüntüleyin.
- **Kümelenmiş paylaşılan birimler**
    - **Toplam verimlilik** her ikisi de hello toplamını okur ve kümelenmiş paylaşılan birimler üzerinde Yazar gösterir.
    - **Toplam IOPS** kümelenmiş paylaşılan birimler üzerinde saniye başına girdi/çıktı işlemleri hello toplamını gösterir.
    - **Toplam gecikme** kümelenmiş paylaşılan birimler üzerinde hello toplam gecikme süresini gösterir.
- **Ana bilgisayar yoğunluğu** hello üst döşeme konaklar ve sanal makineler kullanılabilir toohello çözüm hello toplam sayısını gösterir. Günlük arama Hello üst döşeme tooview ek Ayrıntılar'ı tıklatın. Ayrıca tüm tüm konaklar ve barındırılan sanal makineleri hello sayısını listeler. Bir ana bilgisayar toodrill hello VM günlük arama sonuçlarında Into düğmesini tıklayın.


![Pano Ana dikey penceresi](./media/log-analytics-capacity/dashboard-hosts.png)

![Pano virtual machines dikey penceresi](./media/log-analytics-capacity/dashboard-vms.png)


### <a name="evaluate-performance"></a>Performansı değerlendirme

Üretim bilgi işlem ortamlarını bir kuruluştaki tooanother ' büyük ölçüde farklılık gösterir. Kapasite ve performans iş yükleri nasıl Vm'leriniz çalıştırıyorsanız, ayrıca, bağlı olabilir ve normal düşünün. Performansını ölçmek için özel yordamlar toohelp tooyour ortamı geçerli olmayabilir. Daha fazla tavsiyeler genelleştirilmiş şekilde uygun toohelp daha iyidir. Microsoft çeşitli yayınlar tavsiyeler makaleleri toohelp performansı ölçme.

toosummarize, hello çözüm çeşitli performans sayaçları dahil olmak üzere kaynaklardan kapasite ve performans verilerini toplar. Çeşitli yüzeyleri hello çözümde sunulan bu kapasite ve performans verilerini kullanır ve, sonuçları toothose hello adresindeki karşılaştırmak [Hyper-V performansı ölçme](https://msdn.microsoft.com/library/cc768535.aspx) makalesi. Merhaba makale uzun bir süre önce yayımlanan rağmen hello ölçümleri, ilgili önemli noktalar ve yönergeleri hala geçerli. Merhaba makale bağlantılar tooother kullanışlı kaynaklar içerir.


## <a name="sample-log-searches"></a>Örnek günlük aramaları

Aşağıdaki tablonun hello toplanır ve bu çözümü tarafından hesaplanan kapasite ve performans verileri için örnek günlük aramaları sağlar.

| Sorgu | Açıklama |
|---|---|
| Tüm ana bilgisayar bellek yapılandırmaları | <code>Type=Perf ObjectName="Capacity and Performance" CounterName="Host Assigned Memory MB" &#124; measure avg(CounterValue) as MB by InstanceName</code> |
| Tüm VM bellek yapılandırmaları | <code>Type=Perf ObjectName="Capacity and Performance" CounterName="VM Assigned Memory MB" &#124; measure avg(CounterValue) as MB by InstanceName</code> |
| Toplam Disk IOPS tüm VM'ler arasında dökümü | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="VHD Reads/s" OR CounterName="VHD Writes/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Toplam Disk verim tüm VM'ler arasında dökümü | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="VHD Read MB/s" OR CounterName="VHD Write MB/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Tüm CSV'lerin boyunca toplam IOPS dökümü | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Reads/s" OR CounterName="CSV Writes/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Tüm CSV'lerin boyunca toplam verimlilik dökümü | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Read MB/s" OR CounterName="CSV Write MB/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Tüm CSV'lerin boyunca toplam gecikme dökümü | <code> Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Read Latency" OR CounterName="CSV Write Latency") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |

>[!NOTE]
> Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), sorguları yukarıda hello toohello aşağıdaki değişeceğinden sonra.

> | Sorgu | Açıklama |
|:--- |:--- |
| Tüm ana bilgisayar bellek yapılandırmaları | Perf & #124; Burada ObjectName "Kapasite ve performans" == ve CounterName "Atanan bellek MB ana bilgisayar" & #124; == MB özetlemek InstanceName tarafından avg(CounterValue) = |
| Tüm VM bellek yapılandırmaları | Perf & #124; Burada ObjectName "Kapasite ve performans" == ve CounterName "VM atanan bellek MB" & #124; == MB özetlemek InstanceName tarafından avg(CounterValue) = |
| Toplam Disk IOPS tüm VM'ler arasında dökümü | Perf & #124; Burada ObjectName "Kapasite ve performans" == ve (CounterName "VHD okuma/s" ya da CounterName == "VHD yazma/s" ==) & #124; AggregatedValue özetlemek bin (TimeGenerated, 1 h), tarafından avg(CounterValue) = CounterName, InstanceName |
| Toplam Disk verim tüm VM'ler arasında dökümü | Perf & #124; Burada ObjectName "Kapasite ve performans" == ve (CounterName "VHD okuma MB/s" ya da CounterName == "VHD yazma MB/sn" ==) & #124; AggregatedValue özetlemek bin (TimeGenerated, 1 h), tarafından avg(CounterValue) = CounterName, InstanceName |
| Tüm CSV'lerin boyunca toplam IOPS dökümü | Perf & #124; Burada ObjectName "Kapasite ve performans" == ve (CounterName "CSV okuma/s" ya da CounterName == "CSV yazma/s" ==) & #124; AggregatedValue özetlemek bin (TimeGenerated, 1 h), tarafından avg(CounterValue) = CounterName, InstanceName |
| Tüm CSV'lerin boyunca toplam verimlilik dökümü | Perf & #124; Burada ObjectName "Kapasite ve performans" == ve (CounterName "CSV okuma/s" ya da CounterName == "CSV yazma/s" ==) & #124; AggregatedValue özetlemek bin (TimeGenerated, 1 h), tarafından avg(CounterValue) = CounterName, InstanceName |
| Tüm CSV'lerin boyunca toplam gecikme dökümü | Perf & #124; Burada ObjectName "Kapasite ve performans" == ve (CounterName "CSV okuma gecikme" veya CounterName == "CSV yazma gecikmesi" ==) & #124; AggregatedValue özetlemek bin (TimeGenerated, 1 h), tarafından avg(CounterValue) = CounterName, InstanceName |


## <a name="next-steps"></a>Sonraki adımlar
* Kullanım [günlük analizi aramaları oturum](log-analytics-log-searches.md) tooview ayrıntılı kapasite ve performans verileri.
