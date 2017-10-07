---
title: "aaaUpgrading Azure günlük analizi toonew günlük arama | Microsoft Docs"
description: "Merhaba yeni günlük analizi sorgu dili neredeyse işte ve hello genel önizlemede katılabilirsiniz.  Bu makalede hello yeni dil hello avantajları ve nasıl tooconvert çalışma alanınızı."
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
ms.date: 08/08/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 7659c9d1467cab79d3a16e73b52b507ed281b002
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-your-azure-log-analytics-workspace-toonew-log-search"></a>Azure günlük analizi çalışma alanı toonew günlük aramanızı yükseltme

> [!NOTE]
> Yükseltme toohello yeni günlük analizi sorgu dili olan çok zaman şu anda isteğe bağlı verme[hello yeni dil artırmalarını yukarı](https://go.microsoft.com/fwlink/?linkid=856078).  

Merhaba yeni günlük analizi sorgu dili işte ve bunu, çalışma tootake avantajı tooupgrade gerekir.  Bu makalede hello yeni dil hello avantajları ve nasıl tooconvert çalışma alanınızı.  Ardından tooupgrade şimdi seçmezseniz, çalışma alanınızı her zaman olduğu gibi toooperate oldu, ancak otomatik olarak daha sonraki bir tarihte dönüştürdü devam eder.  Bu tarih ayarlandığında önemli zaman ve bildirim alırsınız.

Bu makalede hello yeni dil ve hello yükseltme işlemi hakkındaki ayrıntıları sağlar.

## <a name="why-hello-new-language"></a>Yeni dil neden hello?
Biz, tüm geçiş sorunları yoktur ve biz yalnızca hello eğlenceli bunu hello sorgu dilini değiştirme olmayan anlayın.  Bu değişiklik tooour günlük analizi müşterilerin önemli değeri sağlayacak birkaç nedeni vardır.

- **Basit ancak güçlü.** yapıları daha fazla ile benzer tooSQL gibi hello eski dilinden doğal dil ve Hello yeni daha kolay toounderstand dilidir.
- **Tam yöneltme dili.**  Merhaba yeni dil hello eski dilinden daha kapsamlı Yöneltme özellikleri vardır.  Neredeyse tüm çıktı için daha önce mümkün olandan daha karmaşık sorgular yöneltilen tooanother komutu toocreate olabilir.
- **Arama zaman alan ayıklamaları.**  Merhaba yeni dil hello eski dilinden daha gelişmiş çalışma zamanı hesaplanan alanları destekler.  Karmaşık hesaplamalar için genişletilmiş alanları kullanın ve ardından hello hesaplanan alanları birleşimler ve toplamalar dahil olmak üzere ek komutlar için kullanın.
- **Gelişmiş birleştirmeler.**  Merhaba yeni dil hello eski dilinden hello özelliği toojoin birden çok alan tablolarda dahil olmak üzere daha gelişmiş birleştirmeler sağlayan, iç ve dış birleştirmeler kullanın ve genişletilmiş alanlar üzerinde birleştirin.
- **İşlevler tarih veya saat.**  Merhaba yeni dil eski dil hello tarih/saat işlevleri daha gelişmiş.
- **Akıllı çözümlemeleri.**  Merhaba yeni dil veri kümelerini ve karşılaştırma farklı veri kümelerinin algoritmaları tooevaluate düzenleri Gelişmiş.
- **Gelişmiş Analytics portalı.**  Merhaba gelişmiş analizler portalı sunar çözümleme özelliklerini çok satırlı dahil olmak üzere hello günlük analizi portalında kullanılamaz sorguları, ek görselleştirmeleri ve Gelişmiş tanılama düzenleme.
- **Diğer uygulamalarla tutarlılık.**  Yeni dil ve hello Gelişmiş analizi portalında Application Insights analizleri için kullanılan zaten hello.  Günlük analizi için uygulama tutarlılığı Azure Hizmetleri genelinde sağlar.
- **Power BI ile daha iyi tümleştirme.** Zengin veri dönüştürme yeteneklerini kullanabilir şekilde hello yeni dil sorguları dışarı aktarılan tooPower BI Desktop olabilir.
- **Daha fazlasını.** Toohello başvuran [Azure günlük analizi sorgu dili](https://docs.loganalytics.io) site ayrıntılarının ve öğreticiler hello yeni dil için.


## <a name="when-can-i-upgrade"></a>Ne zaman ı yükseltebilir miyim?
Bunu diğerlerinden önce bazı bölgelerde kullanılabilir olan şekilde hello yükseltme tüm Azure bölgeler arasında alınacak.  Sunucunuzdan çalışma alanınıza tooupgrade davet hello üstte hello mor başlık gördüğünüzde yükseltilmiş kullanılabilir toobe olduğunda anlarsınız.

![Yükseltme 1](media/log-analytics-log-search-upgrade/upgrade-01a.png)

## <a name="what-happens-when-i-upgrade"></a>Sürümüne yükseltme ne olur?
Çalışma alanınızda Dönüştür, tüm kaydedilmiş aramaları, uyarı kuralları ve Görünüm Tasarımcısı hello ile oluşturduğunuz görünümler otomatik olarak dönüştürülen toohello yeni dil verilebilir.  Çözümlerinde dahil aramaları otomatik olarak dönüştürülmez, ancak bunları açtığınızda, bunun yerine hello anında dönüştürüldüğüne.  Tamamen saydam tooyou budur.

## <a name="can-i-go-back-after-i-upgrade"></a>Geri ı yükselttikten sonra ı gidebilir miyim?
Yükselttiğinizde, çalışma alanınızın tam bir yedekleme anlık görüntüsünü tüm kaydedilmiş aramaları, uyarı kuralı ve görünümleri içeren alınır.  Toorestore böylece daha sonra üzerinde isterse, eski çalışma.

toorestore eski alanınıza çok Git**ayarları** çalışma alanınızdaki ve ardından **yükseltme Özet**.  Daha sonra hello seçeneği çok belirleyebilirsiniz**geri eski çalışma**.  

![Eski geri yükleme](media/log-analytics-log-search-upgrade/restore-legacy-b.png)

## <a name="how-do-i-perform-hello-upgrade"></a>Merhaba yükseltme nasıl yaparım?
Merhaba mor başlık hello portal hello üstündeki gördüğünüzde, çalışma alanınızı yükseltebilirsiniz.  

1.  Bildiren hello mor başlığında tıklayarak Hello yükseltme işlemini başlatmadan **daha fazla bilgi edinin ve yükseltme**.<br>![Yükseltme 2](media/log-analytics-log-search-upgrade/upgrade-01a.png)<br>
2.  Merhaba hello yükseltme bilgileri sayfasında hello yükseltme hakkında ek bilgi aracılığıyla okuyun.<br>![Yükseltme 2](media/log-analytics-log-search-upgrade/upgrade-03.png)<br>
3.  Tıklatın **Şimdi Yükselt** toostart hello yükseltme.<br>![Yükseltme 4](media/log-analytics-log-search-upgrade/upgrade-04.png)<br>Merhaba sağ üst köşesinde bir bildirim kutusunda hello durumunu gösterir.<br>![5 yükseltme](media/log-analytics-log-search-upgrade/upgrade-05.png)
4.  Bu kadar!  Toohello günlük arama sayfası toohave yükseltilmiş çalışma alanınızı göz gidin.<br>![Yükseltme 6](media/log-analytics-log-search-upgrade/upgrade-06.png)<br>

Merhaba yükseltme toofail neden olan bir sorunla karşılaşırsanız, toohello gidebilirsiniz [tartışma Forumu](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights) ve sorunuzu gönderin veya [bir destek isteği oluşturmak](../azure-supportability/how-to-create-azure-support-request.md) hello Azure Portalı'ndan.

## <a name="how-do-i-learn-hello-new-language"></a>Merhaba yeni dil nasıl bilgi?
Birden fazla hizmet tarafından kullanıldığından oluşturduk bir [dış site toohost hello belgelerine](https://docs.loganalytics.io/) hello yeni dil için.  Bu, öğreticiler, örnekler ve toospeed gelen bir tam başvuru toohelp içerir. Bir öğretici hello yeni dil desteğini, size yol [sorguları ile çalışmaya başlama](https://go.microsoft.com/fwlink/?linkid=856078) ve erişim hello dil başvurusu, [günlük analizi sorgu dili](https://go.microsoft.com/fwlink/?linkid=856079).  

Zaten aşinaysanız hello ile eski günlük analizi ancak sorgu dili, ardından tooyour çalışma hello yükseltmesinin bir parçası eklenen hello dil dönüştürücü kullanabilirsiniz.

Yalnızca eski sorgunuzu yazın ve ardından **Dönüştür** toosee hello çevrilmiş sürümü.  Ya da hello arama düğmesini toorun hello arama veya Kopyala'yı tıklatın ve dönüştürülen hello sorgu toouse bir uyarı kuralı gibi başka bir yere yapıştırın. ardından kullanabilirsiniz.

![Dil dönüştürücü](media/log-analytics-log-search-upgrade/language-converter.png)


## <a name="next-steps"></a>Sonraki adımlar
- Kullanıma bir [hello yeni dil öğretici](https://go.microsoft.com/fwlink/?linkid=856078).
- İzlenecek yol bir [hello günlük arama portal kullanarak öğretici](log-analytics-log-search-log-search-portal.md) hello yeni sorgu dili.
- Yeni bir giriş toohello almak [Advanced Analytics portalı](https://go.microsoft.com/fwlink/?linkid=856587).
