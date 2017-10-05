---
title: "Microsoft Azure ölçümlerini genel bakış | Microsoft Docs"
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
ms.openlocfilehash: 3aff83ab2c157a18f4af6200a79bae7e5d6f0ea2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a>Microsoft Azure ölçümlerini genel bakış
Microsoft Azure'da ölçümleri nelerdir bu makalede faydaları ve bunları kullanmaya başlamak nasıl.  

## <a name="what-are-metrics"></a>Ölçümleri nelerdir?
Azure İzleyicisi, performans ve sistem durumu, iş yüklerinin Azure üzerinde görünürlük elde etmek için telemetri kullanmasına olanak sağlar. En önemli Azure telemetri verileri çoğu Azure kaynaklar tarafından gösterilen (performans sayaçlarını olarak da bilinir) ölçümleri türüdür. Azure İzleyicisi'ni yapılandırma ve izleme ve sorun giderme için bu ölçümleri kullanmak için çeşitli yöntemler sağlar.

## <a name="what-can-you-do-with-metrics"></a>Ölçümleri ile neler yapabileceğiniz?
Ölçümleri telemetri değerli bir kaynaktır ve aşağıdaki görevleri yapmanıza olanak sağlar:

* **Performans İzleme** kendi ölçümleri portal grafik Çizdirmek ve bu grafik bir Pano için sabitleme kaynağın (örneğin, bir VM, Web sitesi ya da mantıksal uygulama).
* **Bir sorun bildirim alma** , etkiler, kaynak performans ölçüm belirli bir eşiği kestiği olduğunda.
* **Otomatik eylemler yapılandırma**otomatik ölçeklendirmeyi bir kaynak veya runbook belirli bir eşiği ölçüm kestiği zaman tetiklemeden gibi.
* **Gelişmiş analizler gerçekleştirmek** veya kaynağınız performans ya da kullanım eğilimlerini üzerinde raporlama.
* **Arşiv** kaynağınız performans veya sistem durumu geçmişini **uyumluluk veya Denetim** amaçlar.

## <a name="what-are-the-characteristics-of-metrics"></a>Ölçümleri özelliklerini nelerdir?
Ölçümleri aşağıdaki özelliklere sahiptir:

* Tüm ölçümleri sahip **bir dakikalık sıklığı**. Bir ölçü değeri dakikada, kaynaktan durumu ve kaynağınıza durumunu gerçek zamanlı görünürlük yakın vermiş alırsınız.
* Metrik **kullanılabilir hemen**. Kabul ya da ek tanılama ayarlamak gerekmez.
* Erişebileceğiniz **geçmişi 30 gün** her ölçümü için. Son ve aylık eğilimler performansı veya kaynağınız durumunu hızlı bir şekilde bakabilirsiniz.

Ayrıca şunları yapabilirsiniz:

* Bir ölçüm yapılandırma **bir bildirim gönderir ya da alan kural eylemi otomatik uyarı** zaman ölçümü kestiği ayarladığınız eşiği. Otomatik ölçeklendirme, gelen istekleri karşılamak için kaynağı kullanıma ölçeklendirmenizi sağlar veya Web sitesi ya da bilgi işlem kaynakları yükler özel bir otomatik eylemdir. Bir eşik geçmeden bir ölçüm bağlı içeri veya dışarı ölçeklendirmek için otomatik ölçeklendirme ayarı kural yapılandırabilirsiniz.

* **Rota** tüm ölçümleri anlık analytics, arama ve kaynaklarınızı ölçümleri verileri üzerinde özel uyarı etkinleştirmek için Application Insights ya da günlük analizi (OMS). Ayrıca bunları Azure Stream Analytics veya neredeyse gerçek zamanlı analiz için özel uygulamalar yönlendirmenize olanak sağlayarak bir olay Hub'ına ölçümleri akışını sağlayabilirsiniz. Tanılama ayarları kullanarak akış olay hub'ı ayarlayın.

* **Arşiv depolama ölçümleri** daha uzun bekletme veya çevrimdışı raporlama için kullanın. Kaynağınız için tanılama ayarlarını yapılandırdığınızda, Azure Blob depolama alanına ölçümlerinizi yönlendirebilirsiniz.

* Kolayca bulmak, erişim ve **tüm ölçümleri görüntülemek** bir kaynak seçin ve bir grafik ölçümleri çizim Azure Portalı aracılığıyla.

* **Tüketen** yeni Azure İzleyici REST API'leri aracılığıyla ölçümleri.

* **Sorgu** PowerShell cmdlet'lerini veya platformlar arası REST API kullanarak ölçümleri.

  ![Azure İzleyicisi'nde ölçümleri yönlendirme](./media/monitoring-overview-metrics/Metrics_Overview_v4.png)

## <a name="access-metrics-via-the-portal"></a>Portal üzerinden erişim ölçümleri
Aşağıda Azure portalını kullanarak bir ölçüm grafik oluşturmak nasıl hızlı bir kılavuz vardır.

### <a name="to-view-metrics-after-creating-a-resource"></a>Bir kaynak oluşturduktan sonra ölçümleri görüntülemek için
1. Azure Portalı'nı açın.
2. Azure App Service Web sitesi oluşturun.
3. Bir Web sitesini oluşturduktan sonra Git **genel bakış** Web sitesinin dikey.
4. Yeni ölçümleri olarak görüntüleyebileceğiniz bir **izleme** döşeme. Ardından, döşemesini düzenleyin ve daha fazla ölçümleri seçin.

   ![Azure İzleyicisi'nde kaynak ölçümleri](./media/monitoring-overview-metrics/MetricsOverview1.png)

### <a name="to-access-all-metrics-in-a-single-place"></a>Tüm ölçümlerini tek bir yerde erişmek için
1. Azure Portalı'nı açın.
2. Yeni gidin **İzleyici** sekmesini seçin ve sonra **ölçümleri** altındaki seçeneği.
3. Aboneliğiniz, kaynak grubu ve kaynak adının aşağı açılan listeden seçin.
4. Kullanılabilir ölçümler listesini görüntüleyin. Ardından ilgilendiğiniz ve tasarlayın ölçümü seçin.
5. Bu Pano için sabitleme sağ üst köşesinde üzerinde tıklayarak sabitleyebilirsiniz.

   ![Azure İzleyici tek bir yerde tüm ölçümlerini erişim](./media/monitoring-overview-metrics/MetricsOverview2.png)

> [!NOTE]
> Herhangi bir ek tanılama ayar sanal makine ölçek ayarlar ve VM'lerin (Azure Resource Manager tabanlı) ana bilgisayar düzeyinde ölçümleri erişebilirsiniz. Bu yeni ana bilgisayar düzeyinde ölçümleri, Windows ve Linux örnekleri için kullanılabilir. Bu ölçümler zaman Azure tanılama Vm'lerinizdeki veya sanal makine ölçek kümeleri kapatmanız erişiminiz olan konuk işletim sistemi düzeyinde ölçümleri ile karıştırılmamalıdır üzeresiniz. Tanılama yapılandırma hakkında daha fazla bilgi edinmek için [Microsoft Azure tanılama nedir](../azure-diagnostics.md).
>
>

## <a name="access-metrics-via-the-rest-api"></a>REST API üzerinden erişim ölçümleri
Azure ölçümleri Azure İzleyici API'leri erişilebilir. Yardımcı iki API'ları bulmak ve erişim ölçümleri vardır:

* Kullanım [Azure İzleyici ölçüm tanımlarını REST API](https://msdn.microsoft.com/library/mt743621.aspx) hizmeti için kullanılabilir ölçümleri listesi erişmek için.
* Kullanım [Azure İzleyici ölçümleri REST API](https://msdn.microsoft.com/library/mt743622.aspx) gerçek ölçümleri verilere erişmek için.

> [!NOTE]
> Bu makale aracılığıyla ölçümleri kapsamaktadır [ölçümleri için yeni API](https://msdn.microsoft.com/library/dn931930.aspx) Azure kaynakları için. Yeni ölçüm tanımlarını API için API sürümü 2016-03-01 ve ölçüm API'si sürümü 2016-09-01. Eski ölçüm tanımlarını ve ölçümler API sürümü 2014-04-01 ile erişilebilir.
>
>

Azure İzleyici REST API'lerini kullanarak daha ayrıntılı bilgi için bkz: [Azure İzleyici REST API izlenecek](monitoring-rest-api-walkthrough.md).

## <a name="export-metrics"></a>Dışarı aktarma ölçümleri
Gidebilirsiniz **tanılama ayarları** altında dikey **İzleyici** sekmesinde ve ölçümleri için dışarı aktarma seçeneklerini görüntüleyin. Blob depolama alanına yönlendirilecek ölçümleri (ve tanılama günlükleri) Azure Event Hubs veya OMS bu makalede daha önce bahsedilen kullanım örnekleri için seçebileceğiniz.

 ![Azure İzleyicisi'nde ölçümleri dışa aktarma seçenekleri](./media/monitoring-overview-metrics/MetricsOverview3.png)

Bu Resource Manager şablonları yapılandırabilirsiniz [PowerShell](insights-powershell-samples.md), [Azure CLI](insights-cli-samples.md), veya [REST API'leri](https://msdn.microsoft.com/library/dn931943.aspx).

## <a name="take-action-on-metrics"></a>Ölçümleri eylem
Bildirimleri almak veya ölçüm verilerini otomatik eylemleri için uyarı kuralları veya otomatik ölçeklendirme ayarlarını yapılandırabilirsiniz.

### <a name="configure-alert-rules"></a>Uyarı kurallarını yapılandırma
Uyarı kuralları ölçümleri yapılandırabilirsiniz. Bu uyarı kuralları, bir ölçüm belirli bir eşiği aşıldığında, kontrol edebilirsiniz. Bunlar daha sonra e-posta ile bildir veya özel komut dosyaları çalıştırmak için kullanılan bir Web kancası tetiklenecek. Web kancası, üçüncü taraf ürün tümleştirmeler yapılandırmak için de kullanabilirsiniz.

 ![Ölçümleri ve Azure İzleyicisi'nde uyarı kuralları](./media/monitoring-overview-metrics/MetricsOverview4.png)

### <a name="autoscale-your-azure-resources"></a>Otomatik ölçeklendirme Azure kaynakları
Bazı Azure kaynaklarını veya ölçeklendirme, iş yüklerini işlemek üzere birden çok örneğini destekler. Otomatik ölçeklendirme, uygulama hizmeti (Web uygulamaları), sanal makine ölçek kümeleri ve klasik Azure bulut Hizmetleri için geçerlidir. İş yükünüzün etkiler belirli bir ölçüm belirttiğiniz bir eşik kestiği olduğunda veya ölçeklendirmek için otomatik ölçeklendirme kuralları yapılandırabilirsiniz. Daha fazla bilgi için bkz: [otomatik ölçeklendirmeyi genel bakış](monitoring-overview-autoscale.md).

 ![Ölçümleri ve Azure İzleyicisi'nde otomatik ölçeklendirme](./media/monitoring-overview-metrics/MetricsOverview5.png)

## <a name="learn-about-supported-services-and-metrics"></a>Desteklenen hizmetler ve ölçümleri hakkında bilgi edinin
Yeni bir ölçüm altyapısı Azure izleyicisidir. Azure portalı ve Azure İzleyici API yeni sürüm aşağıdaki Azure hizmetlerini destekler:

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

Desteklenen tüm hizmetleri ve bunların ölçümlere ayrıntılı bir listesini görüntüleyebileceğiniz [Azure İzleyici ölçümleri--kaynak türü başına desteklenen ölçümleri](monitoring-supported-metrics.md).

## <a name="next-steps"></a>Sonraki adımlar
Bu makale boyunca bağlantılara bakın. Ayrıca, hakkında bilgi edinin:  

* [Otomatik ölçeklendirme için ortak ölçümleri](insights-autoscale-common-metrics.md)
* [Uyarı kuralları oluşturma](insights-alerts-portal.md)
* [Günlük analizi ile Azure depolama biriminden günlüklerini analiz edin](../log-analytics/log-analytics-azure-storage.md)
