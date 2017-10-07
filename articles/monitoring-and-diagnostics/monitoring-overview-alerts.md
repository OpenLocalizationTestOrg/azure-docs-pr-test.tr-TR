---
title: "Microsoft Azure ve Azure İzleyicisi uyarı aaaOverview | Microsoft Docs"
description: "Uyarıları toomonitor Azure kaynak ölçümleri, olayları ve günlükleri etkinleştirmek ve belirttiğiniz bir koşul karşılandığında bildirim."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: a6dea224-57bf-43d8-a292-06523037d70b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: robb
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d080080666fedc9eefda6b35cdea3714785d2223
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-alerts-in-microsoft-azure"></a>Microsoft Azure içindeki uyarıları nedir?
Bu makalede, Microsoft Azure, hangi uyarı çeşitli kaynaklardan bu uyarıları, faydaları ve tooget kullanarak ile çalışmaya nasıl amacıyla hello hello açıklanmaktadır. Özellikle tooAzure İzleyici uygulanır ancak işaretçileri tooother hizmetleri de uyarılar sağlar. Uyarıları verilerin üzerine tooconfigure koşulları izin verir ve son izleme verilerini hello hello koşullara uyan bildirim hale Azure'da izleme, bir yöntem sunar.

## <a name="taxonomy-of-azure-alerts"></a>Azure uyarıları sınıflandırma
Azure kullanır hello aşağıdaki toodescribe uyarıları ve bunların işlevlerini koşulları:
* **Uyarı** -sağlandığında etkin hale gelir ölçüt (bir veya daha fazla kural ya da koşullar) tanımı.
* **Etkin** - hello durum hello olduğunda bir uyarı tarafından tanımlanan ölçütleri karşılanıyorsa.
* **Çözümlenen** - hello durum hello olduğunda bir uyarı tarafından tanımlanan ölçütleri artık karşılanıyorsa önceden karşılanıp sonra.
* **Bildirim** -hello etkin hale uyarı dışına tabanlı gerçekleştirilecek eylem.
* **Eylem** -gönderilen belirli çağrı tooa alıcı bir uyarı (örneğin, bir adresi e-postayla gönderme veya tooa Web kancası URL'si nakil). Bildirimleri genellikle birden çok eylem tetikleyebilir.

## <a name="alerts-in-different-azure-services"></a>Farklı Azure Hizmetleri uyarıları
Uyarıları hizmetlerini izleme birkaç Azure kullanılabilir. Nasıl ve ne zaman toouse bu hizmetleri, bilgi [bu makaleye bakın](./monitoring-overview.md). Azure üzerinde kullanılabilir hello uyarı türleri dökümünü şöyledir:

| Hizmet | Uyarı türü | Desteklenen hizmetler | Açıklama |
|---|---|---|---|
| Azure İzleyici | [Ölçüm uyarıları](./insights-alerts-portal.md) | [Azure İzleyicisi'nden desteklenen ölçümleri](./monitoring-supported-metrics.md) | Herhangi bir platform düzeyi ölçümü belirli bir koşulun karşıladığında bir bildirim alın (örneğin, bir VM CPU % son 5 dakika hello için 90 büyüktür). |
| Azure İzleyici | [Etkinlik günlüğü uyarıları](./monitoring-activity-log-alerts.md) | Azure Kaynak Yöneticisi'nde kullanılabilen tüm kaynak türleri | Bildirim herhangi seçildiğinde yeni olay hello içinde [Azure etkinlik günlüğü](./monitoring-overview-activity-logs.md) (örneğin, "VM silme" işlemi içinde myProductionResourceGroup oluştuğunda veya yeni bir hizmet durumu olay "Etkin" olarak ile eşleşen belirli koşullar "Hello durumu görünür). |
| Application Insights | [Ölçüm uyarıları](../application-insights/app-insights-alerts.md) | Herhangi bir uygulama toosend veri tooApplication Öngörüler işaretlenir | Herhangi bir uygulama düzeyi ölçümü belirli bir koşulun karşıladığında bir bildirim alın (örneğin, sunucu yanıt süresi 2 saniyeden uzun). |
| Application Insights | [Web testi uyarıları](../application-insights/app-insights-monitor-web-app-availability.md) | Tüm Web sitesi toosend veri tooApplication Öngörüler işaretlenir | Kullanılabilirlik ve yanıt hızını bir Web sitesinin beklentilerini altında olduğunda bir bildirim alırsınız. |
| Log Analytics | [Günlük analizi uyarıları](../log-analytics/log-analytics-alerts.md) | Herhangi bir hizmet toosend veri günlük analizi yapılandırılmış. | Günlük analizi arama sorgusu ölçüm ve/veya olay veriler üzerinde belirli ölçütleri karşıladığında bir bildirim alırsınız. |

## <a name="alerts-on-azure-monitor-data"></a>Azure İzleyicisi veri uyarılar
Azure izleyiciden--ölçüm uyarıları ve etkinlik günlüğü uyarıları iki türde bir veri dışına uyarı yok.

* **Ölçüm uyarıları** -belirtilen bir ölçüm hello değerini atadığınız bir eşik kestiği bu uyarı tetikler. Merhaba uyarı hello uyarı "(Merhaba eşiği aşıldığında ve hello Uyarı koşulu karşılanıncaya olduğunda) etkinleştirildiğinde" yanı sıra, "(Merhaba eşik yeniden çapraz ve hello koşulu artık karşılanmıyor olduğunda) çözümlendiğinde" bir uyarı oluşturur. Azure İzleyici tarafından desteklenen kullanılabilir ölçümler büyüyen bir listesi için bkz [Azure monitörde desteklenen ölçüm listesine](monitoring-supported-metrics.md).
* **Etkinlik günlüğü uyarıları** -filtre atadığınız ölçütleri eşleşen bir etkinlik günlüğü olay oluşturulduğunda tetikleyen bir akış günlük uyarı. Bu uyarılar yalnızca bir duruma sahip "Merhaba uyarı altyapısı yalnızca hello filtre ölçütü tooany yeni olay uygular bu yana, etkinleştirildi". Yeni bir hizmet durumu olay oluştuğunda kullanılan toobecome haberdar olmanız veya bir kullanıcı veya uygulama "sanal makineyi silin.", aboneliğinizde, örneğin, bir işlem gerçekleştirdiğinde, bu uyarılar kullanabilirsiniz

Azure İzleyicisi aracılığıyla kullanılabilir tanılama günlük verilerini için yönlendirme hello veri günlük analizi ve günlük analizi uyarıyı kullanarak halinde öneririz. Merhaba Aşağıdaki diyagramda Azure İzleyici ve, kavramsal olarak, bu verileri dışına nasıl uyarı veri kaynakları özetler.

![Açıklanan uyarıları](./media/monitoring-overview-alerts/Alerts_Overview_Resource_v4.png)

## <a name="how-do-i-receive-a-notification-on-an-azure-monitor-alert"></a>Bir Azure İzleyicisi uyarı bildirim nasıl alıyor musunuz?
Tarihsel olarak, farklı hizmetler Azure uyarılardan kendi yerleşik bildirim yöntemleri kullanılır. İleride, Azure İzleyici Eylem grupları adı verilen bir yeniden kullanılabilir bildirim gruplandırma sunar. --E-posta adresi herhangi bir sayı, telefon numaralarını (SMS için) ya da Web kancası URL'leri--bildirim alıcıları bir dizi eylem grupları belirtin ve dilediğiniz zaman bir uyarı başvuruları eylem grubu hello etkinleştirilir tüm alıcılar bu bildirim alırsınız. Bu, tooreuse alıcıları (örneğin, üzerinde çağrısı mühendislik listenize) gruplandırması arasında çok sayıda uyarı nesne sağlar. Şu anda yalnızca etkinlik günlüğü uyarıları eylem gruplarını kullanın hale getirir, ancak diğer Azure birkaç uyarı türleri de Eylem grupları kullanarak çalışma.

Eylem grupları tooa Web kancası URL'si toplama tooemail adresleri ve SMS numaraları göndererek bildirim destekler. Bu otomasyon ve düzeltme, örneğin, kullanarak sağlar:
    - Azure Otomasyonu Runbook
    - Azure işlevi
    - Azure mantıksal uygulama
    - bir üçüncü taraf hizmeti

Ölçüm uyarıları Eylem grupları henüz kullanmayın. Tek bir ölçüm uyarıdaki bildirimleri yapılandırabilirsiniz:
* E-posta, belirttiğiniz bildirimleri toohello Hizmet Yöneticisi, tooco yöneticileri veya tooadditional e-posta adresleri gönderin.
* Sağlayan bir Web kancası toolaunch ek Otomasyon Eylemler çağırın.

## <a name="next-steps"></a>Sonraki adımlar
Uyarı kuralları ve bunları kullanarak yapılandırma hakkında bilgi alın:

* Daha fazla bilgi edinmek [ölçümleri](monitoring-overview-metrics.md)
* Yapılandırma [Azure Portalı aracılığıyla ölçüm uyarıları](insights-alerts-portal.md)
* Yapılandırma [ölçüm PowerShell uyarıları](insights-alerts-powershell.md)
* Yapılandırma [ölçüm uyarıları komut satırı arabirimi (CLI)](insights-alerts-command-line-interface.md)
* Yapılandırma [ölçüm uyarıları Azure İzleyici REST API'si](https://msdn.microsoft.com/library/azure/dn931945.aspx)
* Daha fazla bilgi edinmek [etkinlik günlüğü](monitoring-overview-activity-logs.md)
* Yapılandırma [Azure Portalı aracılığıyla etkinlik günlüğü uyarıları](monitoring-activity-log-alerts.md)
* Yapılandırma [etkinlik günlüğü uyarıları aracılığıyla kaynak yöneticisi](monitoring-create-activity-log-alerts-with-resource-manager-template.md)
* Gözden geçirme hello [etkinlik günlüğü uyarı Web kancası şeması](monitoring-activity-log-alerts-webhook.md)
* Daha fazla bilgi edinmek [hizmet bildirimleri](monitoring-service-notifications.md)
* Daha fazla bilgi edinmek [Eylem grupları](monitoring-action-groups.md)
