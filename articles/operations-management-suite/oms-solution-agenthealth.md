---
title: "aaaAgent OMS sistem durumu çözümüne | Microsoft Docs"
description: "Bu makalede anlamak nasıl toouse Bu çözüm toomonitor hello durumunu hedeflenen toohelp olan doğrudan raporlama tooOMS veya System Center Operations Manager aracıları."
services: operations-management-suite
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: operations-management-suite
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: magoedte
ms.openlocfilehash: 071b14b4ab7af6680ae458eaa331246755c5bb56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
#  <a name="agent-health-solution-in-oms"></a>OMS’de Aracı Durumu çözümü
Merhaba aracı sistem durumu OMS çözümde, tüm doğrudan raporlama toohello OMS çalışma veya System Center Operations Manager yönetim grubu bağlı tooOMS, yanıt vermeyen ve gönderen işletimsel verileri hello aracıları için anlamanıza yardımcı olur.  İzlemek burada bunlar coğrafi olarak dağıtılmış ve diğer sorgular toomaintain tanıma hello dağıtım Azure, diğer bulut ortamları veya şirket içi dağıtılan aracıların gerçekleştirmek kaç aracıları dağıtılan de izleyebilirsiniz.    

## <a name="prerequisites"></a>Ön koşullar
Bu çözüm dağıtmadan önce şu anda desteklenen onaylayın [Windows aracıları](../log-analytics/log-analytics-windows-agents.md) toohello OMS çalışma raporlama ya da tooan raporlama [Operations Manager yönetim grubu](../log-analytics/log-analytics-om-agents.md) ile tümleşik, OMS çalışma alanı.    

## <a name="solution-components"></a>Çözüm bileşenleri
Bu çözüm tooyour çalışma ve doğrudan bağlı aracısı veya Operations Manager bağlı yönetim grubuna eklenen kaynaklar aşağıdaki hello oluşur.

### <a name="management-packs"></a>Yönetim paketleri
System Center Operations Manager yönetim grubunuzu bağlı tooan OMS çalışma ise, yönetim paketleri aşağıdaki hello Operations Manager'da yüklenir.  Bu çözüm eklendikten sonra bu yönetim paketleri doğrudan bağlı Windows bilgisayarlarına da yüklenir. Hiçbir şey tooconfigure veya bu yönetim paketleri ile yönetin.

* Microsoft System Center Advisor HealthAssessment Direct Channel Intelligence Pack  (Microsoft.IntelligencePacks.HealthAssessmentDirect)
* Microsoft System Center Advisor HealthAssessment Server Channel Intelligence Pack (Microsoft.IntelligencePacks.HealthAssessmentViaServer).  

Çözüm yönetim paketleri güncelleştirilme biçimini daha fazla bilgi için bkz: [Operations Manager bağlanmak tooLog Analytics](../log-analytics/log-analytics-om-agents.md).

## <a name="configuration"></a>Yapılandırma
Merhaba işlemi kullanarak OMS çalışma açıklanan hello aracı sistem durumu çözüm tooyour eklemek [çözümleri Ekle](../log-analytics/log-analytics-add-solutions.md). Başka bir yapılandırma işlemi gerekmez.


## <a name="data-collection"></a>Veri toplama
### <a name="supported-agents"></a>Desteklenen aracılar
Aşağıdaki tablonun hello bu çözümü tarafından desteklenen hello bağlı kaynakları açıklar.

| Bağlı Kaynak | Destekleniyor | Açıklama |
| --- | --- | --- |
| Windows aracıları | Evet | Sinyal olayları doğrudan Windows aracılarından toplanır.|
| System Center Operations Manager yönetim grubu | Evet | Sinyal olayları 60 saniyede toohello yönetim grubuna raporlama aracılardan toplanır ve tooLog Analytics iletilir. Operations Manager aracıları tooLog arasında doğrudan bağlantı Analytics gerekli değildir. Sinyal Olayı veri hello yönetim grubu toohello günlük analizi depodan iletilir.|

## <a name="using-hello-solution"></a>Merhaba çözümünü kullanarak
Merhaba çözüm tooyour OMS çalışma eklediğinizde, hello **aracı sistem durumu** döşeme tooyour OMS Pano eklenir. Bu kutucuğu hello toplam aracıların hello sayısını ve yanıt vermeyen aracıları son 24 saat hello gösterir.<br><br> ![Panodaki Aracı Durumu Çözüm kutucuğu](./media/oms-solution-agenthealth/agenthealth-solution-tile-homepage.png)

Tıklatın hello üzerinde **aracı sistem durumu** döşeme tooopen hello **aracı sistem durumu** Pano.  Merhaba Pano aşağıdaki tablonun hello hello sütunları içerir. Her sütun, belirtilen zaman aralığı hello sütunun ölçütlerine uyan sayısına göre hello üst on olaylarını listeler. Merhaba tüm liste seçerek sağlar günlük arama çalıştırabilirsiniz **tümünü görmek** hello sağ alt her sütunun veya hello sütun başlığını tıklatarak.

| Sütun | Açıklama |
|--------|-------------|
| Zaman içinde aracı sayısı | Hem Linux hem de Windows aracıları için yedi günlük bir dönem boyunca aracı sayınızın eğilimi.|
| Yanıt vermeyen aracı sayısı | Son 24 saatte bir sinyal hello gönderilen henüz aracıları listesi.|
| İşletim Sistemi Türüne Göre Dağılım | Ortamınızda kaçar tane Windows ve Linux aracısı olduğuna ilişkin bir bölüm.|
| Aracı Sürümüne Göre Dağılım | Ortamınıza ve her biri sayısını yüklü hello farklı Aracı sürümleri bölümü.|
| Aracı Kategorisine Göre Dağılım | Bir bölüm sinyal olaylarını gönderme aracıların hello farklı kategoride: doğrudan aracıları, OpsMgr aracıları veya hello OpsMgr Management Server.|
| Yönetim Grubuna Göre Dağılım | Merhaba farklı SCOM Yönetim grupları, ortamınızdaki bölümü.|
| Aracıların coğrafi konumu | Merhaba farklı ülkelerden aracıları ve her ülkedeki yüklü aracıları hello sayısı toplam sayısını sahip olduğu bir bölümü.|
| Yüklü Ağ Geçidi Sayısı | Merhaba hello OMS yüklü ağ geçidi ve bu sunucular listesini sahip sunucuları sayısı.|

![Aracı Durumu Çözüm panosu örneği](./media/oms-solution-agenthealth/agenthealth-solution-dashboard.png)  

## <a name="log-analytics-records"></a>Log Analytics kayıtları
Merhaba çözüm hello OMS deposunda bir tür kaydı oluşturur.  

### <a name="heartbeat-records"></a>Sinyal kayıtları
**Sinyal** türünde bir kayıt oluşturulur.  Bu kayıtları, aşağıdaki tablonun hello hello özelliklere sahiptir.  

| Özellik | Açıklama |
| --- | --- |
| Tür | *Sinyal*|
| Kategori | Değer *Doğrudan Aracı*, *SCOM Aracısı* veya *SCOM Yönetim Sunucusu*’dur.|
| Bilgisayar | Bilgisayar adı.|
| OSType | Windows veya Linux işletim sistemi.|
| OSMajorVersion | İşletim sistemi ana sürümü.|
| OSMinorVersion | İşletim sistemi alt sürümü.|
| Sürüm | OMS Aracısı veya Operations Manager Aracısı sürümü.|
| SCAgentChannel | Değer *Doğrudan* ve/veya *SCManagementServer*’dır.|
| IsGatewayInstalled | OMS Ağ Geçidi yüklüyse değer *true*, aksi takdirde *false* olur.|
| ComputerIP | Merhaba bilgisayarın IP adresi.|
| RemoteIPCountry | Bilgisayarın dağıtıldığı coğrafi konum.|
| ManagementGroupName | Operations Manager yönetim grubunun adı.|
| SourceComputerId | Bilgisayarın benzersiz kimliği.|
| RemoteIPLongitude | Bilgisayarın coğrafi konumunun boylamı.|
| RemoteIPLatitude | Bilgisayarın coğrafi konumunun enlemi.|

Raporlama tooan Operations Manager yönetim sunucusu, iki sinyal gönderir ve SCAgentChannel özelliğin değerini her ikisi de dahil her bir aracının **doğrudan** ve **SCManagementServer** ne bağlı olarak Günlük analizi veri kaynakları ve çözümleri, OMS aboneliğinizde etkinleştirmiş olmanız gerekir. Geri çağırma, çözümleri verileri doğrudan Operations Manager'dan gönderilen Yönetim sunucusu toohello OMS web hizmeti veya hello nedeniyle hello aracısında toplanan verilerin hacmi doğrudan hello Aracısı tooOMS web hizmetinden gönderildiği demektir. Merhaba değerine sahip sinyal olaylar **SCManagementServer**, hello ComputerIP değeri hello IP adresidir hello yönetim sunucusu hello veri gerçekte tarafından yüklendikten sonra.  Sinyallerin SCAgentChannel ayarlandığı çok**doğrudan**, hello Aracısı hello ortak IP adresi olacak.  

## <a name="sample-log-searches"></a>Örnek günlük aramaları
Merhaba aşağıdaki tabloda bu çözüm tarafından toplanan kayıtları için örnek günlük aramaları sağlar.

| Sorgu | Açıklama |
| --- | --- |
| Type=Heartbeat &#124; distinct Computer |Toplam aracı sayısı |
| Type=Heartbeat &#124; measure max(TimeGenerated) as LastCall by Computer &#124; where LastCall < NOW-24HOURS |Merhaba son 24 saat içinde yanıt vermeyen aracıların sayısı |
| Type=Heartbeat &#124; measure max(TimeGenerated) as LastCall by Computer &#124; where LastCall < NOW-15MINUTES |Merhaba son 15 dakika içinde yanıt vermeyen aracıların sayısı |
| Type=Heartbeat TimeGenerated>NOW-24HOURS Computer IN {Type=Heartbeat TimeGenerated>NOW-24HOURS &#124; distinct Computer} &#124; measure max(TimeGenerated) as LastCall by Computer |Bilgisayarların çevrimiçi (Merhaba son 24 saat) |
| Type=Heartbeat TimeGenerated>NOW-24HOURS Computer NOT IN {Type=Heartbeat TimeGenerated>NOW-30MINUTES &#124; distinct Computer} &#124; measure max(TimeGenerated) as LastCall by Computer |Toplam aracıları çevrimdışı son 30 dakika (için hello son 24 saat) |
| Type=Heartbeat &#124; measure countdistinct(Computer) by OSType |İşletim sistemi türüne göre zaman içinde aracı sayısı eğilimini görün|
| Type=Heartbeat&#124;measure countdistinct(Computer) by OSType |İşletim Sistemi Türüne Göre Dağılım |
| Type=Heartbeat&#124;measure countdistinct(Computer) by Version |Aracı Sürümüne Göre Dağılım |
| Type=Heartbeat&#124;measure count() by Category |Aracı Kategorisine Göre Dağılım |
| Type=Heartbeat&#124;measure countdistinct(Computer) by ManagementGroupName | Yönetim Grubuna Göre Dağılım |
| Type=Heartbeat&#124;measure countdistinct(Computer) by RemoteIPCountry |Aracıların coğrafi konumu |
| Type=Heartbeat IsGatewayInstalled=true&#124;Distinct Computer |Yüklü OMS Ağ Geçidi Sayısı |


>[!NOTE]
> Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](../log-analytics/log-analytics-log-search-upgrade.md), sorguları yukarıda hello toohello aşağıdaki değişeceğinden sonra.
>
>| Sorgu | Açıklama |
|:---|:---|
| Heartbeat &#124; distinct Computer |Toplam aracı sayısı |
| Heartbeat &#124; summarize LastCall = max(TimeGenerated) by Computer &#124; where LastCall < ago(24h) |Merhaba son 24 saat içinde yanıt vermeyen aracıların sayısı |
| Heartbeat &#124; summarize LastCall = max(TimeGenerated) by Computer &#124; where LastCall < ago(15m) |Merhaba son 15 dakika içinde yanıt vermeyen aracıların sayısı |
| Heartbeat &#124; where TimeGenerated > ago(24h) and Computer in ((Heartbeat &#124; where TimeGenerated > ago(24h) &#124; distinct Computer)) &#124; summarize LastCall = max(TimeGenerated) by Computer |Bilgisayarların çevrimiçi (Merhaba son 24 saat) |
| Heartbeat &#124; where TimeGenerated > ago(24h) and Computer !in ((Heartbeat &#124; where TimeGenerated > ago(30m) &#124; distinct Computer)) &#124; summarize LastCall = max(TimeGenerated) by Computer |Toplam aracıları çevrimdışı son 30 dakika (için hello son 24 saat) |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by OSType |İşletim sistemi türüne göre zaman içinde aracı sayısı eğilimini görün|
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by OSType |İşletim Sistemi Türüne Göre Dağılım |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by Version |Aracı Sürümüne Göre Dağılım |
| Heartbeat &#124; summarize AggregatedValue = count() by Category |Aracı Kategorisine Göre Dağılım |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by ManagementGroupName | Yönetim Grubuna Göre Dağılım |
| Heartbeat &#124; summarize AggregatedValue = dcount(Computer) by RemoteIPCountry |Aracıların coğrafi konumu |
| Heartbeat &#124; where iff(isnotnull(toint(IsGatewayInstalled)), IsGatewayInstalled == true, IsGatewayInstalled == "true") == true &#124; distinct Computer |Yüklü OMS Ağ Geçidi Sayısı |

## <a name="next-steps"></a>Sonraki adımlar

* Log Analytics’ten uyarı oluşturma hakkında daha ayrıntılı bilgi edinmek için bkz. [Log Analytics’teki Uyarılar](../log-analytics/log-analytics-alerts.md) .
