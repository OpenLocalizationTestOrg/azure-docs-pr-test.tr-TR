---
title: "Microsoft Azure ölçümlerini aaaOverview | Microsoft Docs"
description: "Ölçümleri ve bunların kullanılması Microsoft Azure genel bakış"
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 405ec51c-0946-4ec9-b535-60f65c4a5bd1
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: johnkem
ms.openlocfilehash: 2b97f51e0554dae95a929241ae1f0e25e5c215ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a>Microsoft Azure ölçümlerini genel bakış
Bu makalede Microsoft Azure, bunların avantajları ölçümleri nelerdir açıklanır ve nasıl kullanmadan toostart.  

## <a name="what-are-metrics"></a>Ölçümleri nelerdir?
Azure İzleyicisi tooconsume telemetri toogain görünürlük hello performans ve iş yüklerinizi Azure üzerinde durumunu sağlar. Merhaba en önemli Azure telemetri verilerini (performans sayaçlarını olarak da bilinir) hello ölçümleri çoğu Azure kaynaklar tarafından gösterilen türüdür. Azure İzleyicisi ve izleme ve sorun giderme için bu ölçümleri tüketen birkaç yolu tooconfigure sağlar.

## <a name="what-can-you-do-with-metrics"></a>Ölçümleri ile neler yapabileceğiniz?
Ölçümleri telemetri değerli bir kaynaktır ve görevleri aşağıdaki toodo hello etkinleştirin:

* **İzleme hello performans** kendi ölçümleri portal grafik Çizdirmek ve o grafik tooa panoya sabitleme kaynağın (örneğin, bir VM, Web sitesi ya da mantıksal uygulama).
* **Bir sorun bildirim alma** belirli bir eşiği ölçüm kestiği zaman etkileri kaynağınız performansını hello.
* **Otomatik eylemler yapılandırma**otomatik ölçeklendirmeyi bir kaynak veya runbook belirli bir eşiği ölçüm kestiği zaman tetiklemeden gibi.
* **Gelişmiş analizler gerçekleştirmek** veya kaynağınız performans ya da kullanım eğilimlerini üzerinde raporlama.
* **Arşiv** hello kaynağınız performans veya sistem durumu geçmişini **uyumluluk veya Denetim** amaçlar.

## <a name="what-are-hello-characteristics-of-metrics"></a>Ölçümleri hello özelliklerini nelerdir?
Ölçümleri hello aşağıdaki özelliklere sahiptir:

* Tüm ölçümleri sahip **bir dakikalık sıklığı**. Bir ölçü değeri dakikada, kaynaktan hello durumu ve kaynağınıza durumunu gerçek zamanlı görünürlük yakın vermiş alırsınız.
* Metrik **kullanılabilir hemen**. İçinde tooopt gerek yok veya ek tanılama ayarlayın.
* Erişebileceğiniz **geçmişi 30 gün** her ölçümü için. Merhaba son ve aylık eğilimler hello performans veya kaynağınız durumunu hızlı bir şekilde bakabilirsiniz.

Ayrıca şunları yapabilirsiniz:

* Bir ölçüm yapılandırma **bir bildirim gönderir ya da alan kural eylemi otomatik uyarı** zaman hello ölçüm kestiği ayarladığınız hello eşiği. Otomatik ölçeklendirme, tooscale kaynak toomeet gelen istekleri çıkışı sağlar ya da Web sitesi ya da bilgi işlem kaynakları yükler özel bir otomatik eylemdir. Bir otomatik ölçeklendirme veya kural tooscale bir eşik geçmeden bir ölçümü tabanlı ayarı yapılandırabilirsiniz.

* **Rota** tüm ölçümleri Application Insights veya günlük analizi (OMS) tooenable anlık analytics, arama ve kaynaklarınızı ölçümleri verileri üzerinde özel uyarı. Ölçümleri tooan olay hub'ı akışını göndermeden, sağlayarak toothen rota bunları tooAzure Stream Analytics veya neredeyse gerçek zamanlı analiz için toocustom uygulamalar. Tanılama ayarları kullanarak akış olay hub'ı ayarlayın.

* **Arşiv ölçümleri toostorage** daha uzun bekletme veya çevrimdışı raporlama için kullanın. Kaynağınız için tanılama ayarlarını yapılandırdığınızda, ölçümleri tooAzure Blob Depolama yönlendirebilirsiniz.

* Kolayca bulmak, erişim ve **tüm ölçümleri görüntülemek** hello bir kaynak seçin ve bir grafik hello ölçümleri çizim Azure portal aracılığıyla.

* **Tüketen** hello yeni Azure İzleyici REST API'leri aracılığıyla hello ölçümleri.

* **Sorgu** kullanarak ölçümleri PowerShell cmdlet'leri hello veya platformlar arası REST API hello.

  ![Azure İzleyicisi'nde ölçümleri yönlendirme](./media/monitoring-overview-metrics/Metrics_Overview_v4.png)

## <a name="access-metrics-via-hello-portal"></a>Merhaba Portalı aracılığıyla erişim ölçümleri
Aşağıda nasıl toocreate kullanarak bir ölçüm grafik hello Azure portal, hızlı bir kılavuz vardır.

### <a name="tooview-metrics-after-creating-a-resource"></a>bir kaynak oluşturduktan sonra tooview ölçümleri
1. Açık hello Azure portalı.
2. Azure App Service Web sitesi oluşturun.
3. Bir Web sitesini oluşturduktan sonra toohello Git **genel bakış** dikey penceresinde hello Web sitesinin.
4. Yeni ölçümleri olarak görüntüleyebileceğiniz bir **izleme** döşeme. Ardından, hello döşemesini düzenleyin ve daha fazla ölçümleri seçin.

   ![Azure İzleyicisi'nde kaynak ölçümleri](./media/monitoring-overview-metrics/MetricsOverview1.png)

### <a name="tooaccess-all-metrics-in-a-single-place"></a>tooaccess tek bir yerde tüm ölçümleri
1. Açık hello Azure portalı.
2. Yeni toohello gidin **İzleyici** sekmesi ve seçin ve ardından hello **ölçümleri** altındaki seçeneği.
3. Abonelik, kaynak grubu ve hello hello kaynağın adını hello aşağı açılan listeden seçin.
4. Görünüm hello kullanılabilir ölçümler listesi. Ardından ilgilendiğiniz ve tasarlayın hello ölçümü seçin.
5. Bu toohello Pano hello sağ üst köşesinde hello PIN'i tıklayarak sabitleyebilirsiniz.

   ![Azure İzleyici tek bir yerde tüm ölçümlerini erişim](./media/monitoring-overview-metrics/MetricsOverview2.png)

> [!NOTE]
> Herhangi bir ek tanılama ayar sanal makine ölçek ayarlar ve VM'lerin (Azure Resource Manager tabanlı) ana bilgisayar düzeyinde ölçümleri erişebilirsiniz. Bu yeni ana bilgisayar düzeyinde ölçümleri, Windows ve Linux örnekleri için kullanılabilir. Bu ölçümler toobe hello Azure tanılama Vm'lerinizdeki veya sanal makine ölçek kümeleri kapatmanız erişim toowhen sahip konuk işletim sistemi düzeyinde ölçümleri ile kafası değildir. Tanılama, yapılandırma hakkında daha fazla toolearn bkz [Microsoft Azure tanılama nedir](../azure-diagnostics.md).
>
>

## <a name="access-metrics-via-hello-rest-api"></a>Merhaba REST API aracılığıyla erişim ölçümleri
Azure ölçümleri hello Azure İzleyici API'leri erişilebilir. Yardımcı iki API'ları bulmak ve erişim ölçümleri vardır:

* Kullanım hello [Azure İzleyici ölçüm tanımlarını REST API](https://msdn.microsoft.com/library/mt743621.aspx) tooaccess hello hizmeti için kullanılabilir ölçümleri listesi.
* Kullanım hello [Azure İzleyici ölçümleri REST API](https://msdn.microsoft.com/library/mt743622.aspx) tooaccess hello gerçek ölçüm verileri.

> [!NOTE]
> Bu makale hello ölçümleri hello aracılığıyla kapsamaktadır [ölçümleri için yeni API](https://msdn.microsoft.com/library/dn931930.aspx) Azure kaynakları için. Merhaba API sürümü hello yeni ölçüm tanımlarını API 2016-03-01 ve ölçüm API'si için hello sürümü 2016-09-01. Merhaba eski ölçüm tanımlarını ve ölçümler API sürümü 2014-04-01 hello ile erişilebilir.
>
>

Hello Azure İzleyici REST API'lerini kullanarak daha ayrıntılı bilgi için bkz: [Azure İzleyici REST API izlenecek](monitoring-rest-api-walkthrough.md).

## <a name="export-metrics"></a>Dışarı aktarma ölçümleri
Toohello gidebilirsiniz **tanılama ayarları** dikey penceresinde hello altında **İzleyici** ölçümleri sekmesinde ve görünüm hello dışa aktarma seçenekleri. Toobe tooBlob depolama, tooAzure olay hub'ları veya tooOMS bahsedilen kullanım örnekleri için yönlendirilmiş ölçümleri (ve tanılama günlükleri) daha önce bu makalede seçebilirsiniz.

 ![Azure İzleyicisi'nde ölçümleri dışa aktarma seçenekleri](./media/monitoring-overview-metrics/MetricsOverview3.png)

Bu Resource Manager şablonları yapılandırabilirsiniz [PowerShell](insights-powershell-samples.md), [Azure CLI](insights-cli-samples.md), veya [REST API'leri](https://msdn.microsoft.com/library/dn931943.aspx).

## <a name="take-action-on-metrics"></a>Ölçümleri eylem
tooreceive bildirimleri veya ölçüm verileri otomatik al eylemleri, uyarı kuralları veya otomatik ölçeklendirme ayarlarını yapılandırabilirsiniz.

### <a name="configure-alert-rules"></a>Uyarı kurallarını yapılandırma
Uyarı kuralları ölçümleri yapılandırabilirsiniz. Bu uyarı kuralları, bir ölçüm belirli bir eşiği aşıldığında, kontrol edebilirsiniz. Bunlar daha sonra e-posta ile bildir veya özel komut dosyaları kullanılan toorun olabilir bir Web kancası tetiklenecek. Merhaba Web kancası tooconfigure üçüncü taraf ürün tümleştirmeler de kullanabilirsiniz.

 ![Ölçümleri ve Azure İzleyicisi'nde uyarı kuralları](./media/monitoring-overview-metrics/MetricsOverview4.png)

### <a name="autoscale-your-azure-resources"></a>Otomatik ölçeklendirme Azure kaynakları
Bazı Azure kaynakları veya iş yüklerinizi birden çok örneği toohandle ölçeklendirme hello desteklemez. Otomatik ölçeklendirme tooApp hizmeti (Web uygulamaları), sanal makine ölçek kümeleri ve klasik Azure Cloud Services uygulanır. İş yükünüzün etkiler belirli bir ölçüm belirttiğiniz bir eşik kestiği otomatik ölçeklendirme kurallarını tooscale veya yapılandırabilirsiniz. Daha fazla bilgi için bkz: [otomatik ölçeklendirmeyi genel bakış](monitoring-overview-autoscale.md).

 ![Ölçümleri ve Azure İzleyicisi'nde otomatik ölçeklendirme](./media/monitoring-overview-metrics/MetricsOverview5.png)

## <a name="learn-about-supported-services-and-metrics"></a>Desteklenen hizmetler ve ölçümleri hakkında bilgi edinin
Yeni bir ölçüm altyapısı Azure izleyicisidir. Azure portal ve hello yeni sürümü hello Azure İzleyici API hello Azure hizmetlerinde aşağıdaki hello destekler:

* Sanal makineleri (Azure Resource Manager tabanlı)
* Sanal makine ölçek kümeleri
* Batch
* Olay hub'ları ad alanı
* Hizmet veri yolu ad alanı (yalnızca premium SKU)
* SQL veritabanı (sürüm 12)
* SQL esnek havuzu
* Web Siteleri
* Web sunucu grupları
* Logic Apps
* IOT hub'ları
* Redis Önbelleği
* Ağ: Uygulama ağ geçitleri
* Arama

Tüm desteklenen hello Hizmetleri ve bunların ölçümlere ayrıntılı bir listesini görüntüleyebileceğiniz [Azure İzleyici ölçümleri--kaynak türü başına desteklenen ölçümleri](monitoring-supported-metrics.md).

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede toohello bağlantılarda bakın. Ayrıca, hakkında bilgi edinin:  

* [Otomatik ölçeklendirme için ortak ölçümleri](insights-autoscale-common-metrics.md)
* [Nasıl toocreate uyarı kuralları](insights-alerts-portal.md)
* [Günlük analizi ile Azure depolama biriminden günlüklerini analiz edin](../log-analytics/log-analytics-azure-storage.md)
