---
title: "aaaWhat günlük analizi Operations Management Suite (OMS) mı? | Microsoft Belgeleri"
description: "Log Analytics, bulut ve şirket içi ortamınızdaki kaynaklar tarafından oluşturulan işletimsel verileri toplayıp analiz etmenize yardımcı olan bir Operations Management Suite (OMS) hizmetidir.  Bu makalede hello farklı bileşenleri günlük analizi ve bağlantıları toodetailed içerik kısa bir genel bakış sağlar."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: bd90b460-bacf-4345-ae31-26e155beac0e
ms.service: log-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/12/2017
ms.author: bwren
ms.openlocfilehash: b35da77e3782f7c1fe54cc34142f8cd9f2eb57d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-log-analytics"></a>Log Analytics nedir?
Günlük analizi olan bir hizmet olarak [Operations Management Suite \(OMS\) ](../operations-management-suite/operations-management-suite-overview.md) , performans ve kullanılabilirlik, Bulut ve şirket içi ortamları toomaintain izler.  Bulut ve şirket içi ortamları ve diğer izleme araçları tooprovide analiz kaynaklar tarafından birden çok kaynakları genelinde oluşturulan veri toplar.  Günlük analizi, nasıl çalıştığı, genel bir bakış sağlar, bu makalede kısa tartışma hello değerinin sağlar ve daha fazla sorgulaması için bağlantılar toomore içeriği ayrıntılı.

## <a name="is-log-analytics-for-you"></a>Log Analytics sizin için uygun mu?
Azure ortamınız için kullandığınız geçerli bir izleme aracı yoksa, Azure kaynaklarınıza ilişkin izleme verilerini toplayıp çözümleyen [Azure İzleyici](../monitoring-and-diagnostics/monitoring-overview.md) ile çalışmaya başlayabilirsiniz.  Günlük analizi yapabilirsiniz [Azure İzleyicisi'nden veri toplama](log-analytics-azure-storage.md) toocorrelate, diğer verilerle ve ek çözümleme sağlar.

Şirket içi ortamınız toomonitor istediğiniz veya var olan Azure İzleyici veya System Center Operations Manager gibi hizmetleri kullanarak izleme varsa, günlük analizi önemli değer ekleyebilirsiniz.  Verileri doğrudan aracılarınızdan ve bu diğer araçlardan tek bir depoya toplayabilir.  Log Analytics’in günlük aramaları, görünümler ve çözümler gibi analiz araçları, tüm ortamınıza ilişkin merkezi bir analiz sağlamak üzere toplanan tüm verilerle çalışır.


## <a name="using-log-analytics"></a>Log Analytics kullanma
Günlük analizi hello OMS portalı veya hello herhangi bir tarayıcısında çalıştırmak ve erişim tooconfiguration ayarlarını sizinle ve birden çok araçları tooanalyze sağlayın ve toplanan verilerde işlem yapmak Azure portalı üzerinden erişebilirsiniz.  Merhaba portalından yararlanabileceğiniz [oturum aramaları](log-analytics-log-searches.md) sorguları tooanalyze toplanan verileri oluşturmak burada [panolar](log-analytics-dashboards.md) en değerli aramalarınız grafik görünümlerle özelleştirebileceğiniz ve [çözümleri](log-analytics-add-solutions.md) ek işlevsellik ve çözümleme araçları sağlar.

Merhaba aşağıdaki görüntüdür hello OMS Portalı'ndan hello için Özet bilgiler görüntüler hangi gösterir hello Pano [çözümleri](#add-functionality-with-management-solutions) hello çalışma alanında yüklenir.  Bu çözüm için hello verileri içine herhangi döşeme toodrill hakkında daha fazla tıklatabilirsiniz.

![OMS portalı](media/log-analytics-overview/portal.png)

Günlük analizi sorgu dili tooquickly alma içerir ve hello deposundaki verileri birleştiremedi.  Oluşturma ve kaydetme [günlük aramaları](log-analytics-log-searches.md) toodirectly hello Portalı'nda veri çözümlemek veya önemli bir koşul hello hello sorgunun sonuçlarını gösteriyorsa, günlük aramaları otomatik olarak toocreate bir uyarı çalıştırılan.

![Günlük araması](media/log-analytics-overview/log-search.png)

tooget genel ortamınızı hello durumunu hızlı bir grafik görünümünü, kaydedilmiş günlük aramaları tooyour görsel ekleyebilirsiniz [Pano](log-analytics-dashboards.md).   

![Pano](media/log-analytics-overview/dashboard.png)

Günlük analizi dışında sipariş tooanalyze veri içinde hello verileri hello OMS depodan araçlarınızla gibi verebilirsiniz [Power BI](log-analytics-powerbi.md) veya Excel.  Merhaba da kullanabilirsiniz [günlük arama API](log-analytics-log-search-api.md) günlük analizi veri veya diğer sistemlerle toointegrate yararlanan toobuild özel çözümler.

## <a name="add-functionality-with-management-solutions"></a>Yönetim çözümleriyle işlevsellik ekleme
[Yönetim çözümleri](log-analytics-add-solutions.md) ek veri ve analiz araçları tooLog analizi sağlayarak işlevselliği tooOMS ekleyin.  Bunlar, ayrıca günlük aramaları veya hello panosunda hello çözümü tarafından sağlanan ek kullanıcı arabirimi tarafından çözümlenebilir toplanan yeni kayıt türleri toobe tanımlayabilir.  Aşağıdaki örnek görüntü Hello hello gösterir [değişiklik izleme çözümü](log-analytics-change-tracking.md)

![Değişiklik İzleme çözümü](media/log-analytics-overview/change-tracking.png)

Çeşitli işlevlere yönelik çözümler mevcuttur ve sürekli olarak başka çözümler eklenmektedir.  Kullanılabilir çözümler kolayca göz atabilir ve [tooyour OMS çalışma Ekle](log-analytics-add-solutions.md) hello Çözümleri Galerisi veya Azure Marketi.  Çoğu çözüm otomatik olarak dağıtılıp hemen çalışmaya başlarken, bazıları biraz yapılandırma gerektirebilir.

![Çözüm Galerisi](media/log-analytics-overview/solution-gallery.png)

## <a name="log-analytics-components"></a>Log Analytics bileşenleri
Merhaba günlük analizi merkezi hello Azure bulut barındırılan hello OMS depodur.  Verileri hello depoya yapılandırma veri kaynakları ve ekleme çözümleri tooyour abonelik tarafından bağlı kaynaklardan toplanır.  Veri kaynakları ve çözümleri her kendi özellikleri vardır, ancak hala birlikte sorguları toohello deposunda analiz farklı kayıt türleri oluşturur.  Bu, farklı veri türleri ile aynı araçları ve yöntemleri toowork farklı bir kaynak tarafından toplanan toouse hello sağlar.

![OMS deposu](media/log-analytics-overview/overview.png)

Bağlı kaynakları hello bilgisayarları ve günlük analizi tarafından toplanan verileri üreten diğer kaynakları ' dir.  Bu, doğrudan bağlanan [Windows](log-analytics-windows-agents.md) ve [Linux](log-analytics-linux-agents.md) bilgisayarlarına yüklenmiş aracıları veya [bağlı System Center Operations Manager yönetim grubundaki](log-analytics-om-agents.md) aracıları içerebilir.  Azure kaynakları için Log Analytics, [Azure İzleyici ve Azure Tanılama](log-analytics-azure-storage.md)’dan veri toplar.

[Veri kaynakları](log-analytics-data-sources.md) hello farklı bağlı her kaynaktan toplanan veri türleridir.  Bu içerir [olayları](log-analytics-data-sources-windows-events.md) ve [performans verileri](log-analytics-data-sources-performance-counters.md) gelen [Windows](log-analytics-data-sources-windows-events.md) ve Linux aracıları gibi ek toosources [IIS günlüklerini](log-analytics-data-sources-iis-logs.md)ve [özel metin günlükleri](log-analytics-data-sources-custom-logs.md).  Toocollect istediğiniz ve otomatik olarak teslim tooeach bağlı kaynak hello yapılandırmadır her veri kaynağı yapılandırın.

Özel gereksinimlerin sonra hello kullanabilirsiniz [HTTP veri toplayıcı API](log-analytics-data-collector-api.md) toowrite veri toohello bir REST API istemcisi depodan.

## <a name="log-analytics-architecture"></a>Log Analytics mimarisi
Günlük analizi hello dağıtım gereksinimleri Hello merkezi bileşenleri hello Azure bulut barındırılan bu yana en az.  Bu, toocorrelate izin ver ve toplanan verileri çözümlemek toplama toohello Hizmetleri'nde hello deposu içerir.  Bu yüzden istemci yazılımı için bir gereksinim hello portal herhangi bir tarayıcıdan erişilebilir.

[Windows](log-analytics-windows-agents.md) ve [Linux](log-analytics-linux-agents.md) bilgisayarlarındaki aracıları yüklemeniz gerekir, ancak zaten [bağlı SCOM yönetim grubunun](log-analytics-om-agents.md) üyesi olan bilgisayarlar için ek aracıya gerek yoktur.  SCOM aracıları toocommunicate kendi veri tooLog Analytics iletir yönetim sunucuları ile devam eder.  Bazı çözümleri ancak aracıları toocommunicate günlük analizi ile doğrudan gerektirir.  Her bir çözüm için Hello belgelerine iletişim gereklilikleri belirtmeniz gerekecektir.

[Log Analytics için kaydolduğunuzda](log-analytics-get-started.md) bir OMS çalışma alanı oluşturursunuz.  Merhaba çalışma alanının kendi veri deposu, veri kaynakları ve çözümlerle benzersiz bir günlük analizi ortamı olarak düşünebilirsiniz. Birden çok çalışma, abonelik toosupport üretim gibi birden çok ortamlar oluşturmak ve test.

![Log Analytics mimarisi](media/log-analytics-overview/architecture.png)

## <a name="next-steps"></a>Sonraki adımlar
* [Ücretsiz bir günlük analizi hesap için kaydolun](log-analytics-get-started.md) kendi ortamınızda tootest.
* Görünüm hello farklı [veri kaynakları](log-analytics-data-sources.md) hello OMS havuzunda kullanılabilir toocollect veri.
* [Merhaba kullanılabilir hello Çözümleri Galerisi çözümlerinde Gözat](log-analytics-add-solutions.md) tooadd işlevselliği tooLog Analytics.

