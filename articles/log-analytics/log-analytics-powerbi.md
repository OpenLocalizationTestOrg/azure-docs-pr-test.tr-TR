---
title: "aaaExport günlük analizi veri tooPower BI | Microsoft Docs"
description: "Power BI bir zengin Görselleştirmelerini ve raporları farklı veri kümelerinin analize sağlayan bir Microsoft bulut tabanlı iş analiz hizmetidir.  Görselleştirmeleri ve çözümleme araçları yararlanabilirsiniz şekilde günlük analizi sürekli olarak veri hello OMS depodan Power BI'a aktarabilirsiniz.  Bu makalede nasıl tooconfigure tooPower BI düzenli aralıklarla otomatik olarak dışarı aktarma günlük analizi sorgular açıklanmaktadır."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 83edc411-6886-4de1-aadd-33982147b9c3
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: bwren
ms.openlocfilehash: 4822f99677e5d1080c72e95cda410da81615bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="export-log-analytics-data-toopower-bi"></a>Günlük analizi veri tooPower BI dışarı aktarma

>[!NOTE]
> Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), sonra da günlük analizi veri tooPower BI dışa aktarmak için bu işlem artık çalışmaz.  Yükseltmeden önce oluşturulan tüm var olan zamanlamalar devre dışı bırakılacaktır. 
>
> Yükseltmeden sonra aynı platform Application Insights olarak Azure günlük analizi kullanır hello ve aynı işlemi olarak tooexport günlük analizi sorguları tooPower BI hello kullandığınız [hello işlem tooexport Application Insights sorgular tooPower BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).  Merhaba sorgu makalesinde açıklandığı gibi hello Analytics konsolunu kullanarak ya da dışa aktarabilirsiniz veya hello seçebilirsiniz **Power BI** hello günlük arama portal Merhaba ekranında hello üstündeki düğmesi.



[Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-get-started/) bir bulut tabanlı İş analizi hizmeti Microsoft'tan farklı veri kümelerinin analize zengin Görselleştirmelerini ve raporlar sunar.  Görselleştirmeleri ve çözümleme araçları yararlanabilirsiniz şekilde günlük analizi otomatik olarak veri hello OMS depodan Power BI'a aktarabilirsiniz.

Günlük analizi ile Power BI yapılandırırken kendi Power BI sonuçları toocorresponding kümelerinde verme günlük sorgular oluşturun.  Merhaba sorgu ve dışarı aktarma hello en son verilerle günlük analizi tarafından toplanan tookeep hello dataset toodate yukarı tanımlayan bir zamanlamaya göre çalıştır tooautomatically devam eder.

![Günlük analizi tooPower BI](media/log-analytics-powerbi/overview.png)

## <a name="power-bi-schedules"></a>Power BI zamanlamaları
A *Power BI zamanlama* kümesinden hello OMS depo tooa karşılık gelen Power BI ve bu arama tookeep hello veri kümesi geçerli ne sıklıkta çalıştırmak tanımlayan bir zamanlama bir veri kümesi aktarır günlük arama içerir.

Merhaba dataset Hello alanlarında hello günlük araması tarafından döndürülen hello kayıtları hello özelliklerini eşleşir.  Merhaba dataset tüm içerecektir sonra hello arama farklı türlerde kayıtları döndürüyorsa her hello hello özelliklerinden kayıt türleri dahil.  

> [!NOTE]
> En iyi yöntem toouse ham verileri karşılıklı tooperforming komutları gibi kullanarak birleştirme döndürür. bir günlük arama sorgusu olduğundan [ölçü](log-analytics-search-reference.md#measure).  Power BI'da hello ham verilerden herhangi bir toplama ve hesaplamalar gerçekleştirebilirsiniz.
>
>

## <a name="connecting-oms-workspace-toopower-bi"></a>OMS çalışma tooPower BI bağlanma
Günlük analizi tooPower BI verebilmeniz hello aşağıdaki yordamı kullanarak OMS çalışma tooyour Power BI hesabınızı bağlanmanız gerekir.  

1. Merhaba Hello OMS konsolunda tıklatın **ayarları** döşeme.
2. Seçin **hesapları**.
3. Merhaba, **çalışma alanı bilgisi** bölümünde **tooPower BI hesabına bağlanmak**.
4. Merhaba, Power BI hesabının kimlik bilgilerini girin.

## <a name="create-a-power-bi-schedule"></a>Power BI zamanlama oluşturma
Merhaba aşağıdaki yordamı kullanarak her veri kümesi için Power BI zamanlama oluşturun.

1. Merhaba Hello OMS konsolunda tıklatın **günlük arama** döşeme.
2. Döndürür tooexport çok istediğiniz verileri hello kaydedilmiş bir aramayı seçin veya yazın yeni bir sorgu**Power BI**.  
3. Merhaba tıklatın **Power BI** düğmesi hello sayfa tooopen hello hello üstündeki **Power BI** iletişim.
4. Aşağıdaki tablo ve tıklayın hello Hello bilgi sağlamak **kaydetmek**.

| Özellik | Açıklama |
|:--- |:--- |
| Ad |Power BI zamanlamaları hello listesini görüntülediğinizde adı tooidentify hello zamanlama. |
| Kayıtlı arama |Merhaba günlük arama toorun.  Merhaba geçerli sorguyu seçin veya varolan kaydedilmiş bir aramayı hello açılır kutusundan seçin. |
| Zamanlama |Ne sıklıkta toorun hello kaydedilen arama ve toohello Power BI veri kümesi dışarı aktarma.  Merhaba değeri 15 dakika ile 24 saat arasında olmalıdır. |
| Veri kümesi adı |Power bı'da hello DataSet'in Hello adı.  Yoksa oluşturulur ve mevcut değilse güncelleştirilmiş. |

## <a name="viewing-and-removing-power-bi-schedules"></a>Görüntüleme ve Power BI zamanlamaları kaldırma
Aşağıdaki yordamı hello ile mevcut Power BI zamanlama hello listesini görüntüleyin.

1. Merhaba Hello OMS konsolunda tıklatın **ayarları** döşeme.
2. Seçin **Power BI**.

Ayrıca hello toohello ayrıntılarını zamanlama, hello sayısı zamanlama hello hello geçen hafta çalıştırıldı ve hello son eşitleme hello durumu görüntülenir.  Merhaba Eşitleme hatalarla karşılaştı, hello bağlantı toorun günlük arama hello hata ayrıntılarını ile kayıt tıklatabilirsiniz.

Bir zamanlama üzerinde hello tıklatarak kaldırabilirsiniz **X** hello içinde **Kaldır sütun**.  Seçerek bir zamanlama devre dışı bırakabilirsiniz **devre dışı**.  toomodify bir zamanlama kaldırmak ve hello yeni ayarlarla yeniden oluşturmanız gerekir.

![Power BI zamanlamaları](media/log-analytics-powerbi/schedules.png)

## <a name="sample-walkthrough"></a>Örnek gözden geçirme
Merhaba aşağıdaki bölümde, Power BI zamanlama oluşturma ve veri kümesi toocreate kullanma örneği basit bir rapor anlatılmaktadır.  Bu örnekte, bir bilgisayar kümesi için tüm performans verilerini dışa aktarılan tooPower BI olduğundan ve bir çizgi grafiği toodisplay işlemci kullanımı sonra oluşturulur.

### <a name="create-log-search"></a>Günlük arama oluşturma
Bir günlük veri aramak için toosend toohello dataset istiyoruz hello oluşturmaya başlayın.  Bu örnekte, ile başlayan bir ada sahip bilgisayarlar için tüm performans verileri döndüren bir sorgu kullanacağız *srv*.  

![Power BI zamanlamaları](media/log-analytics-powerbi/walkthrough-query.png)

### <a name="create-power-bi-search"></a>Power BI arama oluşturma
Merhaba öğesini **Power BI** düğmesini tooopen hello Power BI iletişim ve hello gerekli bilgileri sağlayın.  Bu arama toorun saatte istediğiniz ve adlı bir veri kümesi oluşturma *Contoso Perf*.  Zaten sahip olduğumuz istiyoruz hello veri oluşturuyor hello arama açık olduğundan, biz hello varsayılan seçimini koruyun *kullanım geçerli arama sorgusunu* için **kayıtlı arama**.

![Power BI arama](media/log-analytics-powerbi/walkthrough-schedule.png)

### <a name="verify-power-bi-search"></a>Power BI arama doğrulayın
Biz hello zamanlama doğru şekilde oluşturulmuş tooverify, biz hello listesini görüntülemek Power BI aramaları hello altında **ayarları** döşeme hello OMS panosunda.  Biz, birkaç dakika bekleyin ve hello eşitleme yapılmadı raporları kadar bu görünümü yenileyin.

![Power BI arama](media/log-analytics-powerbi/walkthrough-schedules.png)

### <a name="verify-hello-dataset-in-power-bi"></a>Power BI Hello kümesinde doğrulayın
Bizim hesabı içine oturumunuzu [powerbi.microsoft.com](http://powerbi.microsoft.com/) ve çok kaydırma**veri kümeleri** hello sol bölmenin hello altındaki.  Bu hello görebiliriz *Contoso Perf* dataset bizim verme başarıyla çalıştırıldığını belirten listelenir.

![Power BI veri kümesi](media/log-analytics-powerbi/walkthrough-datasets.png)

### <a name="create-report-based-on-dataset"></a>Veri kümesi üzerinde tabanlı rapor oluşturma
Biz hello seçin **Contoso Perf** dataset tıklayın **sonuçları** hello içinde **alanları** bölmesinde bu veri kümesinin parçası olan hello sağ tooview hello alanlar.  toocreate bir çizgi grafiği gösteren işlemci kullanımını her bilgisayar için aşağıdaki eylemler hello gerçekleştirin.

1. Merhaba çizgi grafiği görselleştirme seçin.
2. Sürükleme **ObjectName** çok**rapor düzeyi filtresi** ve denetleme **İşlemci**.
3. Sürükleme **CounterName** çok**rapor düzeyi filtresi** ve denetleme **% işlemci zamanı**.
4. Sürükleme **CounterValue** çok**değerleri**.
5. Sürükleme **bilgisayar** çok**gösterge**.
6. Sürükleme **TimeGenerated** çok**eksen**.

Bu hello elde edilen çizgi grafiği kümemize hello verilerle görüntülenen görebiliriz.

![Power BI çizgi grafiği](media/log-analytics-powerbi/walkthrough-linegraph.png)

### <a name="save-hello-report"></a>Merhaba raporu kaydedin
Biz hello üzerinde tıklatarak hello rapor kaydet Kaydet düğmesi Merhaba ekranında hello üstündeki ve bunu şimdi hello Raporlar bölümünde hello sol bölmesinde listelendiğini doğrulayın.

![Power BI raporları](media/log-analytics-powerbi/walkthrough-report.png)

## <a name="next-steps"></a>Sonraki adımlar
* Hakkında bilgi edinin [oturum aramaları](log-analytics-log-searches.md) olabilir toobuild sorguları dışarı tooPower BI.
* Daha fazla bilgi edinmek [Power BI](http://powerbi.microsoft.com) toobuild görselleştirmeleri dayalı üzerinde günlük analizi dışarı aktarır.
