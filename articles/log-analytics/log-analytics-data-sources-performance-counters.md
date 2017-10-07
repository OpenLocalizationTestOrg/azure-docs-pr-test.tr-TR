---
title: "aaaCollect ve Azure günlük analizi performans sayaçları analiz | Microsoft Docs"
description: "Performans sayaçları, Windows ve Linux aracıları günlük analizi tooanalyze performans tarafından toplanır.  Windows ve Linux aracıları, bunlar ayrıntılarını hello OMS deposunda depolanır ve nasıl nasıl tooconfigure koleksiyonu performans sayaçları bu makalede tooanalyze hello OMS portalında bunları."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 20e145e4-2ace-4cd9-b252-71fb4f94099e
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: magoedte
ms.openlocfilehash: 30146fecf8db1d8851b89fdb970f757bbb24abf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-and-linux-performance-data-sources-in-log-analytics"></a>Windows ve Linux performans veri kaynaklarında günlük analizi
Windows ve Linux performans sayaçları hello performansını donanım bileşenleri, işletim sistemleri ve uygulamalar hakkında bilgi sağlar.  Günlük analizi, uzun vadeli analiz ve raporlama için ek tooaggregating performans verileri neredeyse gerçek zamanlı (NRT) analizi için sık aralıklarla performans sayaçları toplayabilirsiniz.

![Performans sayaçları](media/log-analytics-data-sources-performance-counters/overview.png)

## <a name="configuring-performance-counters"></a>Performans sayaçları yapılandırma
Performans sayaçları hello hello OMS Portalı'nda yapılandırmak [günlük analizi ayarları veri menüde](log-analytics-data-sources.md#configuring-data-sources).

İlk Windows yapılandırın veya yeni bir OMS çalışma alanı için Linux performans sayaçları, verilen hello seçeneği tooquickly birkaç ortak sayaçları oluşturun.  Bunlar, bir onay kutusu sonraki tooeach ile listelenir.  Tooinitially istediğiniz herhangi bir sayaç oluşturduğunuzdan emin olun denetlenir ve ardından **Ekle hello Seçili performans sayaçlarını**.

Windows performans sayaçları için her performans sayacı için belirli bir örneği seçebilirsiniz. Linux performans sayaçları için seçtiğiniz her sayacı hello örneği tooall alt sayaçları hello üst sayacın geçerlidir. Merhaba aşağıdaki tabloda hello ortak örnekleri kullanılabilir tooboth Linux ve Windows performans sayaçlarını gösterir.

| Örnek adı | Açıklama |
| --- | --- |
| \_Toplam |Tüm hello örnekleri toplamı |
| \* |Tüm örnekleri |
| (/ &#124; / var) |Eşleşen adlandırılmış örnekleri: / veya /var |

### <a name="windows-performance-counters"></a>Windows performans sayaçları

![Windows performans sayaçlarını yapılandırın](media/log-analytics-data-sources-performance-counters/configure-windows.png)

Bu yordam tooadd yeni bir Windows performans sayacı toocollect izleyin.

1. Tür hello hello sayaç hello biçiminde hello metin kutusuna adını *nesne (örnek) \counter*.  Yazmaya başladığınızda, ortak sayaçların eşleşen bir listesi sunulur.  Hello listesi veya kendi yazın ya da bir sayaç seçebilirsiniz.  Belirterek belirli bir sayaç için tüm örnekleri döndürebilir *object\counter*.  

    SQL Server performans sayaçları adlandırılmış örneklerin toplarken, tüm örnek sayaçları Başlarken adlı *MSSQL$* ve ardından hello örneği hello adı.  Örneğin, toocollect hello günlük önbelleği isabet oranı sayaç INST2, tüm veritabanlarından hello veritabanı performans nesnesi için adlandırılmış SQL örneği için belirtmeniz `MSSQL$INST2:Databases(*)\Log Cache Hit Ratio`.

2. Tıklatın  **+**  veya basın **Enter** tooadd hello sayaç toohello listesi.
3. Bir sayaç eklediğinizde, 10 saniye hello varsayılan kullanır, **örnekleme aralığı**.  Merhaba toplanan performans verilerini tooreduce hello depolama gereksinimlerini isterseniz bu tooa daha yüksek değer olan too1800 saniyedir (30 dakika) değiştirebilirsiniz.
4. Ekleme sayaçları bittiğinde, hello tıklatın **kaydetmek** Merhaba ekranında toosave hello yapılandırma hello üstündeki düğmesi.

### <a name="linux-performance-counters"></a>Linux performans sayaçları

![Linux performans sayaçları yapılandırmak](media/log-analytics-data-sources-performance-counters/configure-linux.png)

Bu yordam tooadd yeni Linux performans sayacı toocollect izleyin.

1. Varsayılan olarak, tüm yapılandırma değişiklikleri otomatik olarak tooall aracıları gönderilir.  Linux aracıları için bir yapılandırma dosyası toohello Fluentd veri toplayıcı gönderilir.  Bu dosyada el ile her Linux Aracısı toomodify isterseniz hello kutunun işaretini *aşağıdaki yapılandırma toomy Linux makineler Uygula* ve aşağıdaki hello yönergeleri izleyin.
2. Tür hello hello sayaç hello biçiminde hello metin kutusuna adını *nesne (örnek) \counter*.  Yazmaya başladığınızda, ortak sayaçların eşleşen bir listesi sunulur.  Hello listesi veya kendi yazın ya da bir sayaç seçebilirsiniz.  
3. Tıklatın  **+**  veya basın **Enter** tooadd hello sayaç toohello hello nesne için diğer sayaçlarının listesi.
4. Bir nesne kullanımı için tüm sayaçlar aynı hello **örnekleme aralığı**.  Merhaba varsayılan değer 10 saniyedir.  Merhaba toplanan performans verilerini tooreduce hello depolama gereksinimlerini istiyorsanız bu tooa daha yüksek değer olan too1800 saniyedir (30 dakika) değiştirin.
5. Ekleme sayaçları bittiğinde, hello tıklatın **kaydetmek** Merhaba ekranında toosave hello yapılandırma hello üstündeki düğmesi.

#### <a name="configure-linux-performance-counters-in-configuration-file"></a>Linux performans sayaçları yapılandırma dosyasındaki yapılandırma
Merhaba OMS portalı kullanarak Linux performans sayaçlarını yapılandırmak yerine hello Linux Aracısı Yapılandırma dosyalarını düzenleme hello seçeneğiniz vardır.  Performans ölçümleri toocollect hello yapılandırmasında tarafından denetlenen **/etc/opt/microsoft/omsagent/\<çalışma alanı kimliği\>/conf/omsagent.conf**.

Tek bir olarak hello yapılandırma dosyasındaki her nesne veya kategorisi, performans ölçümleri toocollect tanımlanmalıdır `<source>` öğesi. Merhaba sözdizimi aşağıdaki hello deseni izler.

    <source>
      type oms_omi  
      object_name "Processor"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 30s
    </source>


Bu öğe Hello parametrelerinde aşağıdaki tablonun hello açıklanmaktadır.

| Parametreler | Açıklama |
|:--|:--|
| Nesne\_adı | Nesne adı hello koleksiyonu. |
| örnek\_regex |  A *normal ifade* hangi örnekleri toocollect tanımlama. Merhaba değeri: `.*` tüm örneklerini belirtir. yalnızca hello için toocollect işlemci ölçümleri \_toplam örneğini belirtmek `_Total`. toocollect işlem ölçümlerini yalnızca crond veya sshd örneği Merhaba, belirttiğiniz: ' (crond\|sshd)'. |
| Sayaç\_adı\_regex | A *normal ifade* hangi (Merhaba nesnesi) sayaçları toocollect tanımlama. Merhaba nesnesi için tüm sayaçlar toocollect belirtin: `.*`. toocollect hello bellek nesnesi için yalnızca alanı sayaçları değiştirme, örneğin, size belirtebilirsiniz:`.+Swap.+` |
| interval | Sıklık hangi hello nesnesinin sayaçları toplanır. |


Merhaba aşağıdaki tabloda hello nesneleri ve hello yapılandırma dosyasında belirttiğiniz sayaçları listeler.  Ek sayaçları belirli uygulamalar için kullanılabilir olduğundan açıklandığı gibi [toplama günlük analizi Linux uygulamaları için performans sayaçları](log-analytics-data-sources-linux-applications.md).

| Nesne adı | Sayaç adı |
|:--|:--|
| Mantıksal Disk | % Boş Inode'lar |
| Mantıksal Disk | % Boş alan |
| Mantıksal Disk | % Kullanılan Inode'lar |
| Mantıksal Disk | % Kullanılan alan |
| Mantıksal Disk | Disk okuma bayt/sn |
| Mantıksal Disk | Disk Okuma/sn |
| Mantıksal Disk | Disk aktarımı/sn |
| Mantıksal Disk | Disk Yazma Bayt/sn |
| Mantıksal Disk | Disk Yazma/sn |
| Mantıksal Disk | Boş megabayt |
| Mantıksal Disk | Mantıksal Disk Bayt/sn |
| Bellek | % Kullanılabilir bellek |
| Bellek | % Kullanılabilir takas alanı |
| Bellek | % Kullanılan bellek |
| Bellek | % Kullanılan takas alanı |
| Bellek | Kullanılabilir MBayt belleği |
| Bellek | Kullanılabilir MBayt değiştirme |
| Bellek | Sayfa Okuma/sn |
| Bellek | Sayfa Yazma/sn |
| Bellek | Sayfa/sn |
| Bellek | Kullanılan MBayt takas alanı |
| Bellek | Kullanılan bellek MBayt |
| Ağ | Aktarılan toplam bayt sayısı |
| Ağ | Alınan toplam bayt sayısı |
| Ağ | Toplam bayt sayısı |
| Ağ | Aktarılan toplam paket sayısı |
| Ağ | Alınan toplam paket sayısı |
| Ağ | Toplam Rx hataları |
| Ağ | Toplam Tx hataları |
| Ağ | Toplam çakışmaları |
| Fiziksel Disk | Ort. Disk sn/Okuma |
| Fiziksel Disk | Ort. Disk sn/Aktarım |
| Fiziksel Disk | Ort. Disk sn/yazma |
| Fiziksel Disk | Fiziksel Disk Bayt/sn |
| İşlem | PCT ayrıcalıklı zamanı |
| İşlem | PCT kullanıcı zamanı |
| İşlem | Kullanılan bellek KB |
| İşlem | Paylaşılan sanal bellek |
| İşlemci | % DPC Zamanı |
| İşlemci | % Boş zaman |
| İşlemci | % Kesme Zamanı |
| İşlemci | % GÇ bekleme zamanı |
| İşlemci | % İyi zaman |
| İşlemci | % Ayrıcalıklı Zaman |
| İşlemci | % İşlemci zamanı |
| İşlemci | % Kullanıcı Zamanı |
| Sistem | Boş fiziksel bellek |
| Sistem | Disk belleği dosyasındaki boş alan |
| Sistem | Boş sanal bellek |
| Sistem | İşlemler |
| Sistem | Disk belleği dosyalarında depolanan boyut |
| Sistem | Açık kalma süresi |
| Sistem | Kullanıcılar |


Aşağıdaki hello varsayılan için performans ölçümleri yapılandırmadır.

    <source>
      type oms_omi
      object_name "Physical Disk"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 5m
    </source>

    <source>
      type oms_omi
      object_name "Logical Disk"
      instance_regex ".*
      counter_name_regex ".*"
      interval 5m
    </source>

    <source>
      type oms_omi
      object_name "Processor"
      instance_regex ".*
      counter_name_regex ".*"
      interval 30s
    </source>

    <source>
      type oms_omi
      object_name "Memory"
      instance_regex ".*"
      counter_name_regex ".*"
      interval 30s
    </source>

## <a name="data-collection"></a>Veri toplama
Günlük analizi sayaç yüklü olan tüm aracıları, belirtilen örnek aralıkta tüm belirtilen performans sayaçlarını toplar.  Merhaba veri değil toplanır ve hello ham veriler OMS aboneliğiniz ile belirtilen hello süresi için tüm günlük arama görünümlerde kullanılabilir.

## <a name="performance-record-properties"></a>Performans kaydı Özellikler
Performans kayıtları sahip bir tür **Perf** ve aşağıdaki tablonun hello hello özelliklere sahiptir.

| Özellik | Açıklama |
|:--- |:--- |
| Bilgisayar |Olay hello bilgisayar toplandığı. |
| CounterName |Merhaba performans sayacı adı |
| Sayaç yolu |Merhaba sayaç hello formunda tam yolunu \\ \\ \<bilgisayar >\\nesne(örnek)\\sayacı. |
| CounterValue |Merhaba sayaç sayısal değeri. |
| InstanceName |Merhaba olay örneğinin adı.  Hiçbir örnek varsa boş. |
| ObjectName |Merhaba performans nesnesi adı |
| SourceSystem |Aracı hello veri türü toplandığı. <br><br>OpsManager – Windows aracı, ya da doğrudan bağlanın veya SCOM <br> Linux – tüm Linux aracıları  <br> AzureStorage – Azure tanılama |
| TimeGenerated |Tarih ve saat hello veri örneklenen. |

## <a name="sizing-estimates"></a>Boyutlandırma tahmin eder
 Belirli bir sayaç koleksiyonu 10 saniyelik aralıklarda için kabaca bir tahmin örneği başına günde yaklaşık 1 MB ' dir.  Formül aşağıdaki hello ile belirli bir sayaç hello depolama gereksinimlerini tahmin edebilirsiniz.

    1 MB x (number of counters) x (number of agents) x (number of instances)

## <a name="log-searches-with-performance-records"></a>Performans kayıtlarla günlük aramalar
Merhaba aşağıdaki tabloda farklı performans kayıtları almak günlük arama örnekleri sağlar.

| Sorgu | Açıklama |
|:--- |:--- |
| Türü Perf = |Tüm performans verileri |
| Türü Perf bilgisayar = "Bilgisayarım" = |Belirli bir bilgisayardaki tüm performans verileri |
| Türü Perf CounterName = "Geçerli Disk Sırası Uzunluğu" = |Belirli bir sayaç için tüm performans verileri |
| Türü Perf = (ObjectName işlemci =) CounterName "% işlemci zamanı" InstanceName = = _Total &#124; Bilgisayar tarafından AVGCPU olarak AVG(Average) ölçme |Tüm bilgisayarlardaki ortalama CPU kullanımı |
| Türü Perf = (CounterName = "% işlemci zamanı") &#124;  Bilgisayar tarafından ölçü max(Max) |Tüm bilgisayarlardaki en fazla CPU kullanımı |
| Türü Perf ObjectName = MantıksalDisk CounterName = = "Geçerli Disk Sırası Uzunluğu" bilgisayar = "MyComputerName" &#124; Ölçü InstanceName tarafından Avg(Average) |Belirli bir bilgisayarın tüm hello örneklerde ortalama geçerli Disk Sırası Uzunluğu |
| Türü Perf CounterName = = "DiskTransfers/sn" &#124; Bilgisayar tarafından ölçü percentile95(Average) |95 yüzdebirlik, Disk aktarımı/sn tüm bilgisayarlardaki |
| Türü Perf CounterName = "% işlemci zamanı" InstanceName = = "_Toplam" &#124; AVG(CounterValue) 1 saat bilgisayar aralığına göre ölçün |Saatlik tüm bilgisayarlardaki CPU kullanımı ortalaması |
| Türü Perf bilgisayar = "Bilgisayarım" CounterName = % * InstanceName = = _Total &#124; Ölçü percentile70(CounterValue) CounterName aralığı 1 saat |Belirli bir bilgisayar için her % yüzde sayacın saatlik 70 yüzdebirlik |
| Türü Perf CounterName = "% işlemci zamanı" InstanceName = "_Toplam" = (bilgisayar = "Bilgisayarım") &#124; Min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) 1 saat bilgisayar aralığına göre ölçün |Saatlik ortalama, en az, en fazla ve 75-yüzdelik CPU kullanımı belirli bir bilgisayar için |
| Türü Perf ObjectName = = "MSSQL$ INST2: veritabanları" InstanceName ana = | Tüm performans verilerini hello veritabanı performans hello ana veritabanı için SQL Server örneği INST2 adlı hello nesne.  

>[!NOTE]
> Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), sorguları yukarıda hello toohello aşağıdaki değişeceğinden sonra.

> | Sorgu | Açıklama |
|:--- |:--- |
| Perf |Tüm performans verileri |
| Perf &#124; Burada bilgisayar "Bilgisayarım" == |Belirli bir bilgisayardaki tüm performans verileri |
| Perf &#124; CounterName burada "Geçerli Disk Sırası Uzunluğu" == |Belirli bir sayaç için tüm performans verileri |
| Perf &#124; Burada ObjectName "İşlemci" ve CounterName == "% işlemci zamanı" ve InstanceName == "_Toplam" &#124; == AVGCPU özetlemek bilgisayar tarafından avg(Average) = |Tüm bilgisayarlardaki ortalama CPU kullanımı |
| Perf &#124; CounterName burada "% işlemci zamanı" & #124 ==; AggregatedValue özetlemek bilgisayar tarafından max(Max) = |Tüm bilgisayarlardaki en fazla CPU kullanımı |
| Perf &#124; Burada ObjectName "MantıksalDisk" ve CounterName == "Geçerli Disk Sırası Uzunluğu" ve bilgisayar == "MyComputerName" &#124; == AggregatedValue özetlemek InstanceName tarafından avg(Average) = |Belirli bir bilgisayarın tüm hello örneklerde ortalama geçerli Disk Sırası Uzunluğu |
| Perf &#124; CounterName burada "DiskTransfers/sn" & #124 ==; AggregatedValue özetlemek yüzdebirlik (ortalama, 95) bilgisayar tarafından = |95 yüzdebirlik, Disk aktarımı/sn tüm bilgisayarlardaki |
| Perf &#124; "% işlemci zamanı" ve InstanceName CounterName burada == "_Toplam" &#124; == AggregatedValue özetlemek bin (TimeGenerated, 1 h), bilgisayar tarafından avg(CounterValue) = |Saatlik tüm bilgisayarlardaki CPU kullanımı ortalaması |
| Perf &#124; Burada bilgisayar "Bilgisayarım" ve CounterName startswith_cs "%" ve InstanceName == "_Toplam" &#124; == AggregatedValue özetlemek depo tarafından (TimeGenerated, 1 h), CounterName yüzdebirlik (CounterValue, 70) = | Belirli bir bilgisayar için her % yüzde sayacın saatlik 70 yüzdebirlik |
| Perf &#124; "% işlemci zamanı" ve InstanceName CounterName burada == "_Toplam" ve bilgisayar == "Bilgisayarım" &#124; == ["min(CounterValue)"] özetlemek min(CounterValue), = ["avg(CounterValue)"] avg(CounterValue), = ["percentile75(CounterValue)"] yüzdebirlik (CounterValue, 75), = ["max(CounterValue)"] bin (TimeGenerated, 1 h), bilgisayar tarafından max(CounterValue) = |Saatlik ortalama, en az, en fazla ve 75-yüzdelik CPU kullanımı belirli bir bilgisayar için |
| Perf &#124; Burada ObjectName == "MSSQL$ INST2: veritabanları" ve InstanceName "ana" == | Tüm performans verilerini hello veritabanı performans hello ana veritabanı için SQL Server örneği INST2 adlı hello nesne.  

## <a name="viewing-performance-data"></a>Performans verileri görüntüleme
Performans verileri günlük Ara çalıştırdığınızda hello **listesi** görünümü, varsayılan olarak görüntülenir.  Grafik formundaki tooview hello verileri tıklatın **ölçümleri**.  Ayrıntılı bir grafik görünümü için hello tıklatın  **+**  sonraki tooa sayacı.  

![Daraltılmış ölçümleri Görünüm](media/log-analytics-data-sources-performance-counters/metricscollapsed.png)

tooaggregate performans verileri günlük arama görmek [isteğe bağlı ölçüm toplama ve OMS görselleştirme](http://blogs.technet.microsoft.com/msoms/2016/02/26/on-demand-metric-aggregation-and-visualization-in-oms/).


## <a name="next-steps"></a>Sonraki adımlar
* [Linux uygulamalardan performans sayaçlarını Topla](log-analytics-data-sources-linux-applications.md) MySQL ve Apache HTTP Server dahil olmak üzere.
* Hakkında bilgi edinin [oturum aramaları](log-analytics-log-searches.md) tooanalyze hello veri toplanan veri kaynakları ve çözümler.  
* Toplanan veriler çok dışarı[Power BI](log-analytics-powerbi.md) ek görselleştirmeleri ve analiz için.
