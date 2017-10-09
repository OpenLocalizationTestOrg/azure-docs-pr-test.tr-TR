---
title: "Günlük analizi aaaAnalyze veri kullanımı | Microsoft Docs"
description: "Kullanım hello kullanım günlük analizi tooview panosunda ne kadar veri toohello günlük analizi hizmeti gönderilen ve büyük miktarlarda verinin gönderilen neden giderebilirsiniz."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 74d0adcb-4dc2-425e-8b62-c65537cef270
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: magoedte
ms.openlocfilehash: c30373dd6edbe3ff900fbebc865575fee61ce14c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-usage-in-log-analytics"></a>Log Analytics'te veri kullanımını çözümleme
Günlük analizi hello hello veri ve gönderilen verileri hello farklı türlerde bilgisayarlar gönderilen toplanan, veri miktarını hakkında bilgi içerir.  Kullanım hello **günlük analizi kullanımını** Pano toosee hello veri miktarını gönderilen toohello günlük analizi hizmeti. Merhaba Pano bilgisayarlarınızı gösterir her çözümü tarafından toplanan veri miktarını ve ne kadar veri gönderiyor.

## <a name="understand-hello-usage-dashboard"></a>Merhaba kullanım Pano anlama
Merhaba **günlük analizi kullanım** Pano bilgisinden hello görüntüler:

- Veri hacmi
    - Zaman içindeki veri hacmi (geçerli zaman kapsamınıza bağlı olarak)
    - Çözüme göre veri hacmi
    - Bir bilgisayar ile ilişkilendirilmemiş olan veriler
- Bilgisayarlar
    - Veri gönderen bilgisayarlar
    - Son 24 içinde hiç veri göndermeyen bilgisayarlar
- Teklifler
    - Öngörü ve Analiz düğümleri
    - Otomasyon ve Kontrol düğümleri
    - Güvenlik düğümleri
- Performans
    - Toocollect ve dizin verilerini harcanan süre
- Sorgu listesi

![kullanım panosu](./media/log-analytics-usage/usage-dashboard01.png)

### <a name="toowork-with-usage-data"></a>kullanım verileri ile toowork
1. Zaten yapmadıysanız, toohello içinde oturum [Azure portal](https://portal.azure.com) Azure aboneliğinizi kullanarak.
2. Merhaba üzerinde **Hub** menüsünde tıklatın **daha fazla hizmet** ve kaynakları hello listesinde yazın **günlük analizi**. Yazmaya başladığınızda liste filtreleri, girişinize göre hello. **Log Analytics**’i tıklayın.  
    ![Azure hub'ı](./media/log-analytics-usage/hub.png)
3. Merhaba **günlük analizi** Pano alanlarınızı listesini gösterir. Bir çalışma alanı seçin.
4. Merhaba, *çalışma* panoyu tıklatın **günlük analizi kullanım**.
5. Hello üzerinde **günlük analizi kullanımını** panoyu tıklatın **zaman: Son 24 saat** toochange hello zaman aralığı.  
    ![zaman aralığı](./media/log-analytics-usage/time.png)
6. Alanları Göster görünümü hello kullanım kategori Kanatlar ilgilendiğiniz. Bir dikey pencere seçin ve bir öğede daha fazla ayrıntı tooview ardından [günlük arama](log-analytics-log-searches.md).  
    ![örnek veri kullanım dikey penceresi](./media/log-analytics-usage/blade.png)
7. Merhaba günlük arama Panoda hello aramadan döndürülen hello sonuçlarını gözden geçirin.  
    ![örnek kullanım günlüğü araması](./media/log-analytics-usage/usage-log-search.png)

## <a name="create-an-alert-when-data-collection-is-higher-than-expected"></a>Toplanan veriler beklenenden fazlaysa uyarı oluşturma
Bu bölümde açıklanmıştır nasıl toocreate Uyarı:
- Veri hacmi belirtilen bir miktarı aştığında.
- Veri, tahmin edilen tooexceed belirtilen birimdir.

Log Analytics [uyarılarında](log-analytics-alerts-creating.md) arama sorguları kullanılır. Son 24 saat hello toplanan verilerin birden fazla 100 GB olduğunda hello aşağıdaki sorgu bir sonuç vardır:

`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(Quantity,1024)) as DataGB by Type | where DataGB > 100`

bir günde 100 GB'tan fazla veri gönderilecek hello aşağıdaki sorguyu basit bir formül toopredict kullanır: 

`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(mul(Quantity,8),1024)) as EstimatedGB by Type | where EstimatedGB > 100`

farklı veri birimde, değişiklik hello 100 hello tooalert tooalert istediğiniz GB toohello sayısını sorgular.

Açıklanan başlangıç adımları kullanın [bir uyarı kuralı oluştur](log-analytics-alerts-creating.md#create-an-alert-rule) veri toplama beklenenden daha yüksek olduğunda bildirim toobe.

24 saat içindeki 100 GB'tan fazla veri olduğunda hello ilk sorgu--hello uyarı oluştururken ayarlayın:
- **Ad** çok*24 saatte 100 GB'den büyük veri birimi*
- **Önem derecesi** çok*uyarı*
- **Arama sorgusu** çok`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(Quantity,1024)) as DataGB by Type | where DataGB > 100`
- **Zaman penceresi** çok*24 saat*.
- **Uyarı sıklığı** toobe bir hello kullanım verileri yalnızca saatte bir kez güncelleştiren bir işlem olduğundan saat.
- **Temel uyarı Oluştur** toobe *sonuçları sayısı*
- **Sonuç sayısı** toobe *0'dan büyük*

Açıklanan başlangıç adımları kullanın [Eylemler tooalert kuralları eklemeniz](log-analytics-alerts-actions.md) hello uyarı kuralı için bir e-posta, Web kancası veya runbook eylemi yapılandırın.

Ne zaman 24 saat içindeki 100 GB'tan fazla veri olacağını tahmin oluşturma hello uyarı hello ikinci sorguyu için--ayarlanır:
- **Ad** çok*veri birimi 24 saat içindeki 100 GB'den toogreater bekleniyor*
- **Önem derecesi** çok*uyarı*
- **Arama sorgusu** çok`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(mul(Quantity,8),1024)) as EstimatedGB by Type | where EstimatedGB > 100`
- **Zaman penceresi** çok*3 saat*.
- **Uyarı sıklığı** toobe bir hello kullanım verileri yalnızca saatte bir kez güncelleştiren bir işlem olduğundan saat.
- **Temel uyarı Oluştur** toobe *sonuçları sayısı*
- **Sonuç sayısı** toobe *0'dan büyük*

Bir uyarı aldığınızda, neden kullanım beklenenden daha büyük bölümü tootroubleshoot aşağıdaki hello hello adımları kullanın.

## <a name="troubleshooting-why-usage-is-higher-than-expected"></a>Kullanımın neden beklenenden daha yüksek olduğuyla ilgili sorunları giderme
Merhaba kullanım Pano yardımcı olan tooidentify neden kullanımı (ve bu nedenle maliyet) beklediğiniz daha yüksektir.

Yüksek kullanımın nedeni aşağıdakilerden biri veya her ikisidir:
- TooLog Analytics gönderilen beklenenden daha çok veri
- Veri tooLog Analytics gönderme beklenenden daha fazla düğüm

### <a name="check-if-there-is-more-data-than-expected"></a>Beklenenden daha fazla veri olup olmadığını denetleme 
Çoğu veri toobe toplanan hello neden olduğunu belirlemenize yardımcı iki anahtar bölümleri hello kullanım sayfasının vardır.

Merhaba *zaman içinde veri birimi* gönderme hello bilgisayarlar hello çoğu veri ve grafik hello toplam gönderilen veri hacmini gösterir. sürekli veya azalan kalan genel veri kullanımınızı artıyor yoksa hello grafik hello üstünde toosee sağlar. Merhaba bilgisayarların listesini hello çoğu veri gönderme hello 10 bilgisayarları gösterir.

Merhaba *çözüm bazında veri hacmi* grafik hello her çözüm ve hello çoğu veri gönderme hello çözümleri tarafından gönderilen veri hacmini gösterir. Merhaba grafik hello üstünde hello toplam zaman içinde her çözümü tarafından gönderilen veri hacmini gösterir. Bu bilgileri bir çözüm aynı veri ya da veri daha az zaman içinde tutar hello hakkında daha fazla veri göndermek isteyip tooidentify sağlar. çözümleri Hello listesini hello çoğu veri gönderme hello 10 çözümleri gösterir. 

Bu iki grafik, tüm verileri görüntüler. Bazı veriler faturalanabilir, bazıları ise ücretsizdir. yalnızca bu Faturalanabilir veriler üzerinde toofocus değiştirme hello arama sayfası tooinclude hello sorgusu `IsBillable=true`.  

![veri hacmi grafikleri](./media/log-analytics-usage/log-analytics-usage-data-volume.png)

Ara hello *veri birimi zamanla* grafik. toosee hello çözümleri ve hello belirli bir bilgisayar için en çok veri gönderme veri türleri hello hello bilgisayar adına tıklayın. Merhaba hello listesinde hello ilk bilgisayarın adını tıklatın.

Aşağıdaki ekran görüntüsü hello hello *Günlüğü Yönetimi / Perf* veri türü hello hello bilgisayar için en çok veri gönderiyor. 

![bilgisayar için veri hacmi](./media/log-analytics-usage/log-analytics-usage-data-volume-computer.png)

Ardından, toohello geri dönün *kullanım* Pano ve hello göz *çözüm bazında veri hacmi* grafik. Merhaba bir çözüm için çoğu veri gönderme toosee hello bilgisayarlar hello çözüm hello listesinde hello adını tıklatın. Merhaba listesindeki ilk çözüm hello hello adını tıklatın. 

İsteğe bağlı olarak aşağıdaki ekran görüntüsü hello bu hello onaylar *acmetomcat* bilgisayar hello hello günlük yönetim çözümünün çoğu veri gönderiyor.

![çözüm için veri hacmi](./media/log-analytics-usage/log-analytics-usage-data-volume-solution.png)

Gerekirse, ek çözümleme tooidentify büyük birimleri, bir çözüm ya da veri türü içinde gerçekleştirin. Örnek sorgular şunları içerir:

+ **Güvenlik** çözümü
  - `Type=SecurityEvent | measure count() by EventID`
+ **Günlük Yönetimi** çözümü
  - `Type=Usage Solution=LogManagement IsBillable=true | measure count() by DataType`
+ **Perf** veri türü
  - `Type=Perf | measure count() by CounterPath`
  - `Type=Perf | measure count() by CounterName`
+ **Event** veri türü
  - `Type=Event | measure count() by EventID`
  - `Type=Event | measure count() by EventLog, EventLevelName`
+ **Syslog** veri türü
  - `Type=Syslog | measure count() by Facility, SeverityLevel`
  - `Type=Syslog | measure count() by ProcessName`
+ **AzureDiagnostics** veri türü
  - `Type=AzureDiagnostics | measure count() by ResourceProvider, ResourceId`

Aşağıdaki adımları tooreduce hello toplanan günlüklerini hacmi hello kullan:

| Yüksek veri hacminin kaynağı | Nasıl tooreduce veri birimi |
| -------------------------- | ------------------------- |
| Güvenlik olayları            | [Yaygın veya en az güvenlik olaylarını](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/) seçin <br> Merhaba güvenlik denetim ilkesi yalnızca gerekli toocollect olaylarını değiştirin. Özellikle, hello gerek toocollect olayları gözden geçirin <br> - [filtre platformu denetimi](https://technet.microsoft.com/library/dd772749(WS.10).aspx) <br> - [kayıt defteri denetimi](https://docs.microsoft.com/windows/device-security/auditing/audit-registry)<br> - [dosya sistemi denetimi](https://docs.microsoft.com/windows/device-security/auditing/audit-file-system)<br> - [çekirdek nesnesi denetimi](https://docs.microsoft.com/windows/device-security/auditing/audit-kernel-object)<br> - [tanıtıcı değiştirme denetimi](https://docs.microsoft.com/windows/device-security/auditing/audit-handle-manipulation)<br> - [çıkarılabilir depolama birimi denetimi](https://docs.microsoft.com/windows/device-security/auditing/audit-removable-storage) |
| Performans sayaçları       | [Performans sayacı yapılandırmasını](log-analytics-data-sources-performance-counters.md) şöyle değiştirin: <br> -Koleksiyon hello sıklığını azaltın <br> - Performans sayaçlarının sayısını azaltın |
| Olay günlükleri                 | [Olay günlüğü yapılandırmasını](log-analytics-data-sources-windows-events.md) şöyle değiştirin: <br> -Toplanan olay günlüklerini hello sayısını azaltın <br> - Yalnızca gerekli olay düzeylerini toplayın. Örneğin, *Bilgi* düzeyindeki olayları toplamayın |
| Syslog                     | [Syslog yapılandırmasını](log-analytics-data-sources-syslog.md) şu şekilde değiştirin: <br> -Toplanan tesis hello sayısını azaltın <br> - Yalnızca gerekli olay düzeylerini toplayın. Örneği *Bilgi* ve *Hata Ayıklama* düzeyindeki olayları toplamayın |
| AzureDiagnostics           | Aşağıdaki amaçlarla kaynak günlüğü koleksiyonunu değiştirin: <br> -Kaynakları gönderme günlükleri tooLog Analytics hello sayısını azaltın <br> - Yalnızca gerekli günlükleri toplama |
| Merhaba çözüm gerekmeyen bilgisayardan çözüm verileri | Kullanım [çözüm hedefleme](../operations-management-suite/operations-management-suite-solution-targeting.md) toocollect gruplarından verileri yalnızca gerekli bilgisayarların. |

### <a name="check-if-there-are-more-nodes-than-expected"></a>Beklenenden çok düğüm olup olmadığını denetleme
Merhaba üzerinde olduğunda *her düğüm (OMS)* sizden ücret sonra fiyatlandırma katmanı, temel hello sayısına düğümleri ve kullandığınız çözümler. Kaç tane düğümlerinin her teklif hello kullanıldığını görmek *teklifleri* hello kullanım Pano bölümü.

![kullanım panosu](./media/log-analytics-usage/log-analytics-usage-offerings.png)

Tıklayın **tümünü görmek...**  tooview hello tam hello seçili teklif için veri gönderme bilgisayarların listesini.

Kullanım [çözüm hedefleme](../operations-management-suite/operations-management-suite-solution-targeting.md) toocollect gruplarından verileri yalnızca gerekli bilgisayarların.


## <a name="next-steps"></a>Sonraki adımlar
* Bkz: [günlük analizi aramaları oturum](log-analytics-log-searches.md) toolearn nasıl toouse hello arama dili. Arama sorguları tooperform ek çözümleme hello kullanım verilerini kullanabilirsiniz.
* Açıklanan başlangıç adımları kullanın [bir uyarı kuralı oluştur](log-analytics-alerts-creating.md#create-an-alert-rule) arama ölçütü bildirim toobe karşılanıyorsa
* Kullanım [çözüm hedefleme](../operations-management-suite/operations-management-suite-solution-targeting.md) toocollect gruplarından verileri yalnızca gerekli bilgisayarların
* [Yaygın veya en az güvenlik olaylarını](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/) seçin
* [Performans sayacı yapılandırmasını](log-analytics-data-sources-performance-counters.md) değiştirin
* [Olay günlüğü yapılandırmasını](log-analytics-data-sources-windows-events.md) değiştirin
* [Syslog yapılandırmasını](log-analytics-data-sources-syslog.md) değiştirin
