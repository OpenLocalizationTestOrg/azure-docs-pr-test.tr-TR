---
title: "Ağ İzleyicisi aaaIntroduction tooAzure | Microsoft Docs"
description: "Bu sayfa hello Ağ İzleyicisi hizmetini izleme genel bir bakış sağlar ve Azure kaynaklarında görselleştirme ağ bağlı"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 14bc2266-99e3-42a2-8d19-bd7257fec35e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: 283b3fa6add05d9bad6d5dbdae1524344d1bfc7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-monitoring-overview"></a>Azure ağı izlemeye genel bakış

Müşterilerin bir uçtan uca ağ Azure VNet, ExpressRoute, uygulama ağ geçidi, yük Dengeleyiciler ve daha fazlasını gibi çeşitli tek tek ağ kaynaklarına oluşturma ve yönetme tarafından oluşturun. İzleme her hello ağ kaynaklarına kullanılabilir. Kaynak düzey izleme olarak toothis izlemeyi başvurun.

Merhaba uç tooend ağ karmaşık yapılandırmalar ve senaryo tabanlı ağ izlemekte gereken karmaşık senaryolar oluşturma kaynakları arasındaki etkileşimler sahip olabilir.

Bu makalede senaryo ve kaynak düzeyi izleme kapsar. Azure'da ağ izleme kapsamlı ve iki geniş kategorisi kapsar:

* [**Ağ İzleyicisi** ](#network-watcher) -senaryo tabanlı izleme Ağ İzleyicisi Merhaba özellikleriyle sağlanır. Bu hizmet içeren paket yakalama, sonraki atlama IP akış, güvenlik grubu görünümü, NSG akış günlükleri doğrulayın. Senaryo düzeyi izleme Karşıtlık tooindividual ağ kaynak izleme ağ kaynaklarına bir uçtan tooend görünümünü sağlar.
* [**Kaynak İzleme** ](#network-resource-level-monitoring) -kaynak düzeyi izleme dört özellikleri, tanılama günlükleri, ölçümleri, sorun giderme ve kaynak durumu oluşur. Bu özelliklerin tümü hello ağ kaynak düzeyinde oluşturulur.

## <a name="network-watcher"></a>Ağ İzleyicisi

Ağ İzleyicisi'ni ve koşullar bir ağ düzeyinde senaryo içinde gelen ve giden Azure Tanılama, toomonitor sağlayan bölgesel bir hizmettir. Ağ Tanılama ve görselleştirme Ağ İzleyicisi ile kullanılabilen araçlar anlamak, tanılama ve Öngörüler tooyour Azure ağında geçirmesine yardımcı olur.

Ağ İzleyicisi'ni şu anda özellikleri aşağıdaki hello sahiptir:

* **[Topoloji](network-watcher-topology-overview.md)**  -bir ağ seviye görünümü gösteren hello çeşitli bağlantılar ve ağ kaynakları bir kaynak grubunda arasındaki ilişkilendirmeleri sağlar.
* **[Değişken paket yakalama](network-watcher-packet-capture-overview.md)**  -bir sanal makine ve paket verilerini yakalar. Gelişmiş seçenekleri ve mümkün tooset anda gibi ince ayar denetimleri filtreleme ve boyut sınırlamaları yönlülük sağlayın. Merhaba paket verileri blob Mağazası'nda veya .cap biçiminde hello yerel diskte depolanabilir.
* **[IP akış doğrulayın](network-watcher-ip-flow-verify-overview.md)**  -paket izin verilen veya reddedilen denetimleri temel akış bilgi 5-tanımlama grubu paket parametrelerine (hedef IP, kaynak IP, hedef bağlantı noktası, kaynak bağlantı noktası ve protokol). Başlangıç paketi bir güvenlik grubu tarafından engellenirse hello kuralı ve hello Paket reddedildi Grup döndürülür.
* **[Sonraki atlama](network-watcher-next-hop-overview.md)**  -hello toodiagnose herhangi yanlış yapılandırılmış kullanıcı tanımlı yollar etkinleştirme Azure ağ yapısında yönlendirilen paketler için sonraki atlama hello belirler.
* **[Güvenlik grubu görünümü](network-watcher-security-group-view-overview.md)**  -bir VM üzerinde uygulanan hello etkili ve uygulanan güvenlik kuralları alır.
* **[NSG akış günlük](network-watcher-nsg-flow-logging-overview.md)**  -akış günlükleri ağ güvenlik grupları için izin verilen veya hello Grup hello güvenlik kuralları tarafından reddedilen toocapture günlükleri ilgili tootraffic sağlar. Merhaba akışı bir 5-tanımlama grubu bilgileriyle – kaynak IP, hedef IP, kaynak bağlantı noktası, hedef bağlantı noktası ve protokol tanımlanır.
* **[Sanal ağ geçidi ve bağlantı sorunlarını giderme](network-watcher-troubleshoot-manage-rest.md)**  -hello özelliği tootroubleshoot sağlayan sanal ağ geçitleri ve ağ bağlantıları.
* **[Ağ abonelik sınırları](#network-subscription-limits)**  -sınırları karşı tooview ağ kaynağı kullanımı sağlar.
* **[Tanılama günlük yapılandırma](#diagnostic-logs)**  – bölmeden tooenable sağlar veya bir kaynak grubunda ağ kaynakları için tanılama günlükleri devre dışı bırakın.
* **[Bağlantı (Önizleme)](network-watcher-connectivity-overview.md)**  -endpoint verilen bir sanal makine tooa arasında doğrudan TCP bağlantı kurma hello olasılığını doğrular.

### <a name="role-based-access-control-rbac-in-network-watcher"></a>Rol tabanlı erişim denetimi (RBAC) Ağ İzleyicisi

Ağ İzleyicisi'ni kullanan hello [Azure rol tabanlı erişim denetimi (RBAC) modeli](../active-directory/role-based-access-control-what-is.md). Aşağıdaki izinleri hello Ağ İzleyicisi Merhaba tarafından gereklidir. Önemli toomake Ağ İzleyicisi API'leri başlatılıyor veya hello Portalı'ndan Ağ İzleyicisi'ni kullanmak için kullanılan bu hello rol gerekli hello erişimi emin olur.

|Kaynak| İzin|
|---|---| 
|Microsoft.Storage/ |Okuma|
|Microsoft.Authorization/| Okuma| 
|Microsoft.Resources/subscriptions/resourceGroups/| Okuma|
|Microsoft.Storage/storageAccounts/listServiceSas/ | Eylem|
|Microsoft.Storage/storageAccounts/listAccountSas/ |Eylem|
|Microsoft.Storage/storageAccounts/listKeys/ | Eylem|
|Microsoft.Compute/virtualMachines/ |Okuma|
|Microsoft.Compute/virtualMachines/ |Yazma|
|Microsoft.Compute/virtualMachineScaleSets/ |Okuma|
|Microsoft.Compute/virtualMachineScaleSets/ |Yazma|
|Microsoft.Network/networkWatchers/packetCaptures/ |Okuma|
|Microsoft.Network/networkWatchers/packetCaptures/| Yazma|
|Microsoft.Network/networkWatchers/packetCaptures/| Sil|
|Microsoft.Network/networkWatchers/ |Yazma |
|Microsoft.Network/networkWatchers/| Okuma |
|Microsoft.Insights/alertRules/ |*|
|Microsoft.Support/ | *|

### <a name="network-subscription-limits"></a>Ağ abonelik sınırları

Ağ abonelik sınırları her bir abonelikte kullanılabilir kaynakları hello sayısının karşı bir bölgede hello ağ kaynağının hello kullanım ayrıntılarını sağlayın.

![Ağ abonelik sınırı][nsl]

## <a name="network-resource-level-monitoring"></a>Ağ kaynak düzeyi izleme

özellikler aşağıdaki Merhaba, kaynak düzeyi izleme için kullanılabilir:

### <a name="audit-log"></a>Denetim günlüğü

Ağların hello yapılandırmasının bir parçası gerçekleştirilen işlemleri günlüğe kaydedilir. Bu günlükler hello Azure portal görüntülenebilir veya Power BI gibi Microsoft araçları veya üçüncü taraf araçlarını kullanarak alınamıyor. Denetim günlüklerini hello portal, PowerShell'i, CLI ve Rest API kullanılabilir. Denetim günlükleri hakkında daha fazla bilgi için bkz: [denetim işlemleri Resource Manager ile](../resource-group-audit.md)

Denetim günlükleri, tüm ağ kaynaklarına yapılan işlemleri için kullanılabilir.

### <a name="metrics"></a>Ölçümler

Performans ölçümleri ve bir süre boyunca toplanan sayaçları ölçümleridir. Ölçümleri uygulama ağ geçidi için şu anda kullanılabilir. Ölçümleri kullanılan tootrigger uyarıları eşiğine dayalı olabilir. Bkz: [uygulama ağ geçidi tanılama](../application-gateway/application-gateway-diagnostics.md) tooview ölçümleri kullanılan toocreate uyarıları nasıl olabilir.

![Ölçümleri görüntüleyin][metrics]

### <a name="diagnostic-logs"></a>Tanılama günlükleri

Dönemsel ve spontaneous olayları ağ kaynakları tarafından oluşturulan ve gönderilen tooan olay hub'ı ya da günlük analizi depolama hesaplarında oturum. Bu günlükleri bir kaynak hello durumunu fikir sağlar. Bu günlükler Power BI ve günlük analizi gibi araçları görüntülenebilir. nasıl tooview tanılama günlükleri, ziyaret toolearn [günlük analizi](../log-analytics/log-analytics-azure-networking-analytics.md).

Tanılama günlükleri için kullanılabilir [yük dengeleyici](../load-balancer/load-balancer-monitor-log.md), [ağ güvenlik grupları](../virtual-network/virtual-network-nsg-manage-log.md), yollar ve [uygulama ağ geçidi](../application-gateway/application-gateway-diagnostics.md).

Ağ İzleyicisi görünümü bir tanılama günlükleri sağlar. Bu görünüm, tanılama günlüğünün destekleyen tüm ağ kaynaklarını içerir. Bu görünümden etkinleştirin ve ağ kaynaklarını kolayca ve hızlı bir şekilde devre dışı bırakın.

![günlükler][logs]

### <a name="troubleshooting"></a>Sorun giderme

Dikey penceresinde hello portalında bir deneyim sorun giderme hello ağ kaynaklarını tek tek bir kaynakla ilişkili toodiagnose karşılaşılan bugün sağlanır. Bu deneyim, ağ kaynaklarına - ExpressRoute, VPN ağ geçidi, uygulama ağ geçidi, ağ güvenlik günlükleri, yollar, DNS, yük dengeleyici ve trafik Yöneticisi aşağıdaki hello için kullanılabilir. Kaynak düzey sorun giderme hakkında daha fazla toolearn ziyaret [Tanıla ve çözümleme sorunlarını Azure sorun giderme](https://azure.microsoft.com/blog/azure-troubleshoot-diagonse-resolve-issues/)

![sorun giderme bilgileri][TS]

### <a name="resource-health"></a>Kaynak durumu

bir ağ kaynağına Hello durumunu düzenli olarak sağlanır. Bu tür kaynaklar VPN ağ geçidi ve VPN tüneli içerir. Kaynak durumu hello Azure portalı üzerinde erişilebilir. Kaynak durumu hakkında daha fazla toolearn ziyaret [kaynak sistem durumu genel bakış](../resource-health/resource-health-overview.md)

## <a name="next-steps"></a>Sonraki adımlar

Ağ İzleyicisi hakkında daha fazla bilgi sonra için bilgi alabilirsiniz:

Paket yakalama VM üzerinde ziyaret ederek yapmak [hello Azure portal değişken paket yakalama](network-watcher-packet-capture-manage-portal.md)

Öngörülü izleme ve Tanılama'yı kullanarak gerçekleştirmek [uyarının paket yakalama](network-watcher-alert-triggered-packet-capture.md).

Güvenlik açıklarıyla algılamak [Wireshark paket yakalamayla çözümleme](network-watcher-deep-packet-inspection.md), açık kaynaklı araçları kullanarak.

Merhaba bazıları hakkında bilgi edinin başka bir anahtar [ağı yetenekleri](../networking/networking-overview.md) Azure.

<!--Image references-->
[TS]: ./media/network-watcher-monitoring-overview/troubleshooting.png
[logs]: ./media/network-watcher-monitoring-overview/logs.png
[metrics]: ./media/network-watcher-monitoring-overview/metrics.png
[nsl]: ./media/network-watcher-monitoring-overview/nsl.png











