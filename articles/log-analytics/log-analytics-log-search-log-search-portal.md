---
title: "aaaUsing hello günlük arama Azure günlük analizi portalında | Microsoft Docs"
description: "Bu makalede nasıl toocreate aramaları oturum ve hello günlük arama portal kullanarak günlük analizi çalışma alanınızda depolanan verileri çözümleyen açıklayan bir öğretici içerir.  Başlangıç Öğreticisi tooreturn farklı veri türlerini bazı basit sorguları çalıştırma ve sonuçları çözümleme içerir."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: bwren
ms.openlocfilehash: 2e6633d548bb508edc0c650d11d2c32fc6ee536c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-log-searches-in-azure-log-analytics-using-hello-log-search-portal"></a>Merhaba günlük arama portalı kullanarak Azure günlük analizi günlük aramalar oluşturun

> [!NOTE]
> Bu makalede hello günlük arama hello yeni sorgu dili kullanarak Azure günlük analizi portalında açıklanmaktadır.  Merhaba yeni dil hakkında daha fazla bilgi ve çalışma alanı hello yordamı tooupgrade almak [Azure günlük analizi çalışma alanı toonew günlük aramanızı yükseltme](log-analytics-log-search-upgrade.md).  
>
> Çalışma alanınızı yükseltilmiş toohello yeni sorgu dili bırakılmamışsa, çok başvurmalıdır[Bul günlük aramaları günlük analizi kullanarak verileri](log-analytics-log-searches.md) hello hello günlük arama Portalı'nın geçerli sürümü hakkında bilgi için.

Bu makalede nasıl toocreate aramaları oturum ve hello günlük arama portal kullanarak günlük analizi çalışma alanınızda depolanan verileri çözümleyen açıklayan bir öğretici içerir.  Başlangıç Öğreticisi tooreturn farklı veri türlerini bazı basit sorguları çalıştırma ve sonuçları çözümleme içerir.  Merhaba günlük arama portalında doğrudan değiştirmek yerine hello sorgu değiştirmek için özellikler odaklanır.  Merhaba doğrudan hello sorgu düzenleme hakkında daha fazla bilgi için bkz [sorgu dili başvurusu](https://go.microsoft.com/fwlink/?linkid=856079).

Merhaba günlük arama portalı yerine hello Advanced Analytics portalında toocreate aramaları Bkz [hello Analytics portalı ile çalışmaya başlama](https://go.microsoft.com/fwlink/?linkid=856587).  Her iki portalları hello kullanın dil tooaccess hello hello günlük analizi çalışma alanındaki aynı veri aynı sorgu.

## <a name="prerequisites"></a>Ön koşullar
Bu öğretici, bir günlük analizi çalışma alanı hello sorguları tooanalyze için veri üretir en az bir bağlı kaynağıyla zaten sahip olduğunuzu varsayar.  

- Bir çalışma alanı yoksa, ücretsiz bir tane oluşturabilirsiniz adresindeki hello yordamı kullanarak [günlük analizi çalışma alanı ile çalışmaya başlama](log-analytics-get-started.md).
- En az bir bağlanma [Windows Aracısı](log-analytics-windows-agents.md) veya bir [Linux Aracısı](log-analytics-linux-agents.md) toohello çalışma.  

## <a name="open-hello-log-search-portal"></a>Açık hello günlük arama portalı
Merhaba günlük arama portal açarak başlayın.  Hello Azure portal veya hello OMS portalı erişebilir.

1. Açık hello Azure portalı.
2. TooLog Analytics gidin ve çalışma alanınızı seçin.
3. Her iki select **günlük arama** hello seçerek Azure portal veya başlatma hello OMS portalında toostay **OMS portalı** ve ardından hello günlük arama düğmesini tıklatarak.

![Günlük Ara düğmesi](media/log-analytics-log-search-log-search-portal/log-search-button.png)

## <a name="create-a-simple-search"></a>Basit Arama oluşturma
Merhaba hızlı şekilde tooretrieve bazı veri toowork ile tablodaki tüm kayıtları döndürür basit bir sorgudur.  Tüm Windows veya Linux istemcileri bağlı tooyour çalışma varsa ya da olay (Windows) veya Syslog (Linux) tablosu hello verilerde sahip olacaksınız.

Merhaba arama kutusu sorguları izleyen bir hello yazın ve hello arama düğmesini tıklatın.  

```
Event
```
```
Syslog
```

Veriler hello varsayılan liste görünümünde döndürülür ve kaç tane toplam kaydı döndürülmedi görebilirsiniz.

![Basit Sorgu](media/log-analytics-log-search-log-search-portal/log-search-portal-01.png)

Yalnızca hello ilk birkaç özellikleri her kaydın görüntülenir.  Tıklatın **daha fazla Göster** toodisplay belirli bir kayıt için tüm özellikleri.

![Kayıt ayrıntıları](media/log-analytics-log-search-log-search-portal/log-search-portal-02.png)

## <a name="set-hello-time-scope"></a>Başlangıç saati kapsamını ayarlama
Günlük analizi tarafından toplanan her kaydına sahip bir **TimeGenerated** bu hello kayıt başlangıç tarihi ve saati içeren özelliği oluşturuldu.  Merhaba günlük arama portal sorguda yalnızca kayıtlarıyla döndürür bir **TimeGenerated** yan hello ekranın sol hello üzerinde görüntülenen hello zaman kapsam içinde.  

Merhaba zaman filtresi hello açılır seçerek veya hello kaydırıcı değiştirerek değiştirebilirsiniz.  Merhaba kaydırıcı hello göreli her zaman diliminin hello aralıkta için kayıt sayısını gösteren bir çubuk grafiği görüntüler.  Bu kesimin hello aralığı bağlı olarak değişir.

Merhaba varsayılan saat kapsamı **1 gün**.  Bu değeri çok değiştirmek**7 gün**, ve hello kayıtlarının toplam sayısını artırın.

![Tarih saat kapsamı](media/log-analytics-log-search-log-search-portal/log-search-portal-03.png)

## <a name="filter-results-of-hello-query"></a>Merhaba sorgu sonuçlarını filtreleme
Merhaba üzerinde hello ekranın sol tarafındaki doğrudan değiştirmeden toohello Sorgu filtreleme tooadd sağlayan hello Filtre Bölmesi ' dir.  Çeşitli özellikleri döndürülen hello kayıtların üst on değerleriyle kendi kayıt sayısı ile birlikte görüntülenir.

İle çalışıyorsanız **olay**, select hello onay kutusu sonraki çok**hata** altında **EVENTLEVELNAME**.   İle çalışıyorsanız **Syslog**, select hello onay kutusu sonraki çok**hata** altında **önem düzeyi**.  Bu tooerror olayları toolimit hello aşağıdaki hello tooone sonuçları hello sorgu değiştirir.

```
Event | where (EventLevelName == "Error")
```
```
Syslog | where (SeverityLevel == "err")
```

![Filtre](media/log-analytics-log-search-log-search-portal/log-search-portal-04.png)

Seçerek Ekle özellikleri toohello filtre bölmesi **toofilters ekleme** hello özelliği menüsünden hello kayıtları biri.

![Toofilter menü ekleme](media/log-analytics-log-search-log-search-portal/log-search-portal-02a.png)

Aynı filtre seçerek hello ayarlayabilirsiniz **filtre** toofilter istediğiniz hello özelliği menüsünden hello içeren bir kaydı.  

Merhaba yeterlidir **filtre** adlarının mavi olan özellikleri seçeneği.  Bunlar *aranabilir* için dizin alanları arama koşulları.  Gri alanlar *serbest metin aranabilir* hello yalnızca olan alanları **Göster başvuruları** seçeneği.  Bu seçenek, o değeri herhangi bir özellik olan kayıtları döndürür.

![Filtre menüsü](media/log-analytics-log-search-log-search-portal/log-search-portal-01a.png)

Merhaba seçerek tek bir özellik hello sonuçlarına gruplandırabilirsiniz **Group by** hello kayıt menü seçeneği.  Bu ekler bir [özetlemek](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/summarize-operator) hello sonuçları bir grafik görüntüler tooyour sorgu işleci.  Birden fazla özellik gruplandırabilirsiniz, ancak tooedit hello sorgu doğrudan gerekir.  Select hello kayıt menü sonraki hello hello **bilgisayar** özelliği ve select **'Bilgisayar' grupla**.  

![Bilgisayar grubu](media/log-analytics-log-search-log-search-portal/log-search-portal-10.png)

## <a name="work-with-results"></a>Sonuçları ile çalışma
Merhaba günlük arama portal çeşitli hello bir sorgunun sonuçlarını ile çalışmak için özellikler vardır.  Filtre ve Grup sonuçları tooanalyze hello veri hello gerçek sorgu değiştirilmeden sıralama yapabilirsiniz;  Varsayılan olarak bir sorgunun sonuçlarını sıralı değil.

tooview hello verileri filtreleme ve sıralama, için ek seçenekler sağlayan Tablo formunda tıklatın **tablo**.  

![Tablo görünümü](media/log-analytics-log-search-log-search-portal/log-search-portal-05.png)

Bu kayıt kayıt tooview hello ayrıntılarını tarafından Hello oka tıklayın.

![Sıralama sonuçları](media/log-analytics-log-search-log-search-portal/log-search-portal-06.png)

Herhangi bir alanı kendi sütun başlığına tıklayarak sıralayın.

![Sıralama sonuçları](media/log-analytics-log-search-log-search-portal/log-search-portal-07.png)

Merhaba filtre düğmesini tıklatarak ve bir filtre koşulu sağlayan hello sütununda belirli bir değer hello sonuçlarına filtre.

![Sonuçları filtresi](media/log-analytics-log-search-log-search-portal/log-search-portal-08.png)

Bir sütunda, sütun başlığı toohello üst hello sonuçlarının sürükleyerek gruplandırın.  Birden çok sütun toohello üst sürükleyerek üzerinde birden çok alan gruplandırabilirsiniz.

![Grup sonuçları](media/log-analytics-log-search-log-search-portal/log-search-portal-09.png)



## <a name="work-with-performance-data"></a>Performans verileri ile çalışma
Windows ve Linux aracıları için performans verilerini hello günlük analizi çalışma alanında hello depolandığı **Perf** tablo.  Diğer kaydı gibi performans kayıtları aramak ve biz tüm performans kayıtları olayları ile olduğu gibi veren basit bir sorgu yazabilirsiniz.

```
Perf
```

![Performans verileri](media/log-analytics-log-search-log-search-portal/log-search-portal-11.png)

Tüm performans nesneleri ve sayaçları kayıtlarını milyonlarca ancak döndüren çok kullanışlı değildir.  Doğrudan hello günlük arama kutusuna toofilter hello veri yukarıda kullanılan ya da yalnızca hello aşağıdakileri yazın aynı yöntemleri sorgu hello kullanabilirsiniz.  Bu, Windows ve Linux bilgisayarlar için kullanım kayıtları yalnızca işlemci döndürür.

```
Perf | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time")
```

![İşlemci kullanımı](media/log-analytics-log-search-log-search-portal/log-search-portal-12.png)

Bu hello veri tooa belirli sayaç sınırlar, ancak bunu hala bu özellikle yararlı bir formda put değil.  Bir çizgi grafiği hello verileri görüntülemek, ancak ilk toogroup gerekir, bilgisayar ve TimeGenerated.  toogroup birden çok alana ihtiyacınız toomodify hello sorgu doğrudan hello sorgu toohello aşağıdaki şekilde değiştirin.  Bu hello kullanır [avg](https://docs.loganalytics.io/docs/Language-Reference/Aggregation-functions/avg()) hello işlevini **CounterValue** özelliği toocalculate hello her bir saat içinde ortalama değer.

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated
```

![Performans veri grafiği](media/log-analytics-log-search-log-search-portal/log-search-portal-13.png)

Hello veri uygun gruplandırılmış, onu visual grafik hello ekleyerek görüntüleyebileceğiniz [işleme](https://docs.loganalytics.io/docs/Language-Reference/Tabular-operators/render-operator) işleci.  

```
Perf  | where (ObjectName == "Processor")  | where (CounterName == "% Processor Time") | summarize avg(CounterValue) by Computer, TimeGenerated | render timechart
```

![Çizgi grafiği](media/log-analytics-log-search-log-search-portal/log-search-portal-14.png)

## <a name="next-steps"></a>Sonraki adımlar

- Hello günlük analizi sorgu dili hakkında daha fazla bilgi [hello Analytics portalı ile çalışmaya başlama](https://go.microsoft.com/fwlink/?linkid=856079).
- Hello kullanarak bir öğreticide yol [Advanced Analytics portalı](https://go.microsoft.com/fwlink/?linkid=856587) olanak sağlayan toorun hello aynı sorgular ve erişim hello hello günlük arama portalı aynı verileri.
