---
title: "aaaAlert yönetim çözümü Operations Management Suite (OMS) | Microsoft Docs"
description: "Merhaba günlük analizi uyarı Yönetimi çözümünde hello uyarıları, ortamınızdaki tüm analiz etmenize yardımcı olur.  Toplama tooconsolidating uyarıları OMS içinde oluşturulan bunu uyarıları bağlı System Center Operations Manager yönetim gruplarından günlük analizi aktarır."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: fe5d534e-0418-4e2f-9073-8025e13271a8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: aff9bd8d88839c5227bb9ec3a1b5209a3cd7cdf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="alert-management-solution-in-operations-management-suite-oms"></a>Uyarı yönetimi çözümü Operations Management Suite (OMS)

![Uyarı Yönetimi simgesi](media/log-analytics-solution-alert-management/icon.png)

Merhaba uyarı yönetimi çözümü hello uyarıların günlük analizi deponuzun analiz etmenize yardımcı olur.  Bu uyarıların bir çeşitli kaynaklardan bu kaynakları da dahil olmak üzere ortaya çıkabilir [günlük analizi tarafından oluşturulan](log-analytics-alerts.md) veya [Nagios veya Zabbix içeri](log-analytics-linux-agents.md).  Merhaba çözüm ayrıca uyarıları birinden alır [bağlı System Center Operations Manager Yönetim grupları](log-analytics-om-agents.md).

## <a name="prerequisites"></a>Ön koşullar
Merhaba çözümün çalıştığı hello günlük analizi deposundaki türüne sahip herhangi bir kayıt ile **uyarı**, herhangi bir yapılandırmadır gerekli toocollect gerçekleştirmeniz gerekir böylece bu kayıtları.

- Günlük analizi uyarılar için [uyarı kuralları oluşturmak](log-analytics-alerts.md) toocreate uyarı kayıtlarında doğrudan hello deposu.
- Nagios ve Zabbix uyarılar için [bu sunucuları yapılandırmak](log-analytics-linux-agents.md) toosend tooLog Analytics uyarır.
- System Center Operations Manager uyarılar için [Operations Manager yönetim grubu tooyour günlük analizi çalışma alanınız bağlanmak](log-analytics-om-agents.md).  System Center Operations Manager'da oluşturulan herhangi bir uyarı günlük analizi alınır.  

## <a name="configuration"></a>Yapılandırma
Merhaba işlemi kullanarak OMS çalışma açıklanan hello uyarı yönetimi çözümü tooyour eklemek [çözümleri Ekle](log-analytics-add-solutions.md).  Başka bir yapılandırma işlemi gerekmez.

## <a name="management-packs"></a>Yönetim paketleri
Ardından System Center Operations Manager yönetim grubunuzu bağlı tooyour OMS çalışma ise, bu çözüm eklediğinizde, yönetim paketleri aşağıdaki hello System Center Operations Manager'da yüklenir.  Yapılandırma veya gerekli hello yönetim paketlerinin bakım yoktur.  

* Microsoft System Center Advisor uyarı Yönetimi (Microsoft.IntelligencePacks.AlertManagement)

Çözüm yönetim paketleri güncelleştirilme biçimini daha fazla bilgi için bkz: [Operations Manager bağlanmak tooLog Analytics](log-analytics-om-agents.md).

## <a name="data-collection"></a>Veri toplama
### <a name="agents"></a>Aracılar
Aşağıdaki tablonun hello bu çözümü tarafından desteklenen hello bağlı kaynakları açıklar.

| Bağlı Kaynak | Destek | Açıklama |
|:--- |:--- |:--- |
| [Windows aracıları](log-analytics-windows-agents.md) | Hayır |Doğrudan Windows aracıları uyarılar oluşturmaz.  Günlük analizi uyarılar olaylarından oluşturulabilir ve aracıları Windows'dan toplanan performans verileri. |
| [Linux aracıları](log-analytics-linux-agents.md) | Hayır |Doğrudan Linux aracılarını uyarılar oluşturmaz.  Günlük analizi uyarılar olayları ve performans verilerini Linux aracılarını toplanan oluşturulabilir.  Nagios ve Zabbix uyarıları hello Linux Aracısı gerektiren bu sunuculardan toplanır. |
| [System Center Operations Manager yönetim grubu](log-analytics-om-agents.md) |Evet |Operations Manager aracıları oluşturulan uyarıların toohello yönetim grubu teslim ve tooLog Analytics iletilir.<br><br>Operations Manager aracıları tooLog arasında doğrudan bağlantı Analytics gerekli değildir. Uyarı verileri hello yönetim grubu toohello günlük analizi depodan iletilir. |


### <a name="collection-frequency"></a>Toplama sıklığı
- Uyarı kayıtları hello deposunda saklanır kullanılabilir toohello çözüm olduğunu.
- Uyarı verileri hello Operations Manager yönetim grubu tooLog analizi üç dakikada gönderilir.  

## <a name="using-hello-solution"></a>Merhaba çözümünü kullanarak
Merhaba uyarı yönetimi çözümü tooyour OMS çalışma eklediğinizde, hello **uyarı Yönetimi** döşeme tooyour OMS Pano eklenir.  Bu kutucuğu sayısı ve grafik gösterimi hello son 24 saat içinde hello oluşturulan etkin uyarıların sayısını görüntüler.  Bu zaman aralığı değiştiremezsiniz.

![Uyarı Yönetimi döşeme](media/log-analytics-solution-alert-management/tile.png)

Tıklatın hello üzerinde **uyarı Yönetimi** döşeme tooopen hello **uyarı Yönetimi** Pano.  Merhaba Pano aşağıdaki tablonun hello hello sütunları içerir.  Her sütun sütunun ölçütleri hello için kapsam ve zaman aralığını belirtilen sayısı eşleşen tarafından hello üst 10 uyarıları listeler.  Merhaba tüm liste tıklayarak sağlar günlük arama çalıştırabilirsiniz **tümünü görmek** hello altındaki hello sütununun veya hello sütun başlığını tıklatarak.

| Sütun | Açıklama |
|:--- |:--- |
| Kritik uyarılar |Tüm Uyarıları önem derecesi Kritik Uyarı adına göre gruplandırılır.  Bir uyarı adı toorun bu uyarı için tüm kayıtları döndüren bir günlük Ara'yı tıklatın. |
| Uyarı bildirimleri |Tüm uyarıları uyarı adına göre gruplandırılmış uyarı önem derecesi.  Bir uyarı adı toorun bu uyarı için tüm kayıtları döndüren bir günlük Ara'yı tıklatın. |
| Etkin SCOM uyarıları |Tüm uyarıları Operations Manager'dan dışındaki herhangi bir durum ile toplanan *kapalı* kaynağı tarafından oluşturulan hello uyarısının gruplandırılır. |
| Tüm etkin uyarıları |Tüm uyarıları uyarı adına göre gruplandırılmış herhangi bir önem derecesi. Yalnızca Operations Manager uyarıları ile herhangi bir durum dışında içeren *kapalı*. |

Toohello sağa kaydırırsanız hello Pano üzerinde tooperform tıklayabilirsiniz birkaç genel sorgular listeler bir [günlük arama](log-analytics-log-searches.md) uyarı veriler için.

![Uyarı Yönetim Panosu](media/log-analytics-solution-alert-management/dashboard.png)


## <a name="log-analytics-records"></a>Log Analytics kayıtları
Merhaba uyarı yönetimi çözümü çözümler herhangi bir tür kaydıyla **uyarı**.  Günlük analizi tarafından oluşturulan veya Nagios veya Zabbix toplanan uyarılar hello çözümü tarafından doğrudan toplanmadı.

Merhaba çözüm uyarıları System Center Operations Manager'dan içe ve her bir türü ile ilgili bir kayıt oluşturur **uyarı** ve SourceSystem, **OpsManager**.  Bu kayıtları, aşağıdaki tablonun hello hello özelliklere sahiptir:  

| Özellik | Açıklama |
|:--- |:--- |
| Tür |*Uyarı* |
| SourceSystem |*OpsManager* |
| AlertContext |XML biçiminde oluşturulan hello uyarı toobe neden hello veri öğesi ayrıntıları. |
| AlertDescription |Merhaba uyarı ayrıntılı bir açıklaması. |
| Alertıd |Merhaba uyarı GUID. |
| AlertName |Merhaba uyarı adı. |
| AlertPriority |Merhaba uyarı öncelik düzeyi. |
| AlertSeverity |Merhaba uyarı önem derecesi. |
| AlertState |Merhaba uyarının son çözümleme durumu. |
| LastModifiedBy |Merhaba uyarıyı son değiştiren hello kullanıcının adı. |
| ManagementGroupName |Burada Merhaba uyarının oluşturulmasının hello yönetim grubunun adı. |
| RepeatCount |Sayısı aynı uyarının oluşturulmasının hello aynı çözülmüş bu yana nesne izlenen hello için zaman. |
| Çözüm bulan |Merhaba uyarı çözümleyen hello kullanıcının adı. Merhaba uyarı henüz çözümlenmediyse, boş. |
| SourceDisplayName |İzleme hello uyarı nesnesi hello adını görüntüler. |
| SourceFullName |İzleme hello uyarı nesnesi hello tam adı. |
| Ticketıd |Bilet kimliği hello uyarı hello System Center Operations Manager ortamı uyarıları biletlerini atamak için bir işlem ile tümleşiktir.  Bir anahtarı yok, boş bir kimlik atanır. |
| TimeGenerated |Oluşturulduğu tarihi ve uyarının hello zaman. |
| TimeLastModified |Tarih ve saat uyarı hello son değiştirildi. |
| TimeRaised |Tarih ve saat uyarı hello üretilmiştir. |
| TimeResolved |Tarih ve saat uyarı hello çözülmüş. Merhaba uyarı henüz çözümlenmediyse, boş. |

## <a name="sample-log-searches"></a>Örnek günlük aramaları
Merhaba aşağıdaki tabloda bu çözüm tarafından toplanan uyarı kayıtları için örnek günlük aramaları sağlar: 

| Sorgu | Açıklama |
|:--- |:--- |
| Tür uyarı SourceSystem = OpsManager AlertSeverity = hata TimeRaised = > şimdi - 24 saat |Merhaba sırasında son 24 saatte oluşturulan kritik uyarılar |
| Tür uyarı AlertSeverity = uyarı TimeRaised = > şimdi - 24 saat |Son 24 saat Hello sırasında oluşturulan uyarı bildirimleri |
| Tür uyarı SourceSystem = OpsManager AlertState =! kapalı TimeRaised = > şimdi 24 saatlik &#124; Ölçü count() SourceDisplayName bazında sayı olarak |Merhaba sırasında son 24 saatte oluşturulan etkin uyarılara sahip kaynaklar |
| Tür uyarı SourceSystem = OpsManager AlertSeverity = hata TimeRaised = > şimdi 24 saatlik AlertState! kapalı = |Son 24 hala etkin olan saat Hello sırasında oluşturulan kritik uyarılar |
| Tür uyarı SourceSystem = OpsManager TimeRaised = > şimdi 24 saatlik AlertState = kapalı |Son 24 şimdi kapatılan saat Hello sırasında oluşturulan uyarılar |
| Tür uyarı SourceSystem = OpsManager TimeRaised = > şimdi - 1 gün &#124; Ölçü count() AlertSeverity bazında sayı olarak |Merhaba önem derecesine göre gruplandırılmış son 1 gün sırasında oluşturulan uyarılar |
| Tür uyarı SourceSystem = OpsManager TimeRaised = > şimdi - 1 gün &#124; RepeatCount desc sıralama |Merhaba yineleme sayısına göre sıralanmış son 1 gün sırasında oluşturulan uyarılar |


>[!NOTE]
> Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), sorguları önceki hello toohello aşağıdaki değişeceğinden sonra:
>
>| Sorgu | Açıklama |
|:---|:---|
| Hi &#124; Burada SourceSystem "OpsManager" ve AlertSeverity == "error" ve TimeRaised == > ago(24h) |Merhaba sırasında son 24 saatte oluşturulan kritik uyarılar |
| Hi &#124; Burada AlertSeverity "uyarı" ve TimeRaised == > ago(24h) |Son 24 saat Hello sırasında oluşturulan uyarı bildirimleri |
| Hi &#124; Burada SourceSystem "OpsManager" ve AlertState ==! "Kapalı" = ve TimeRaised > ago(24h) &#124; Count özetlemek SourceDisplayName tarafından count() = |Merhaba sırasında son 24 saatte oluşturulan etkin uyarılara sahip kaynaklar |
| Hi &#124; Burada SourceSystem "OpsManager" ve AlertSeverity == "error" ve TimeRaised == > ago(24h) ve AlertState! "Kapalı" = |Son 24 hala etkin olan saat Hello sırasında oluşturulan kritik uyarılar |
| Hi &#124; Burada SourceSystem "OpsManager" ve TimeRaised == > ago(24h) ve AlertState "Kapalı" == |Son 24 şimdi kapatılan saat Hello sırasında oluşturulan uyarılar |
| Hi &#124; Burada SourceSystem "OpsManager" ve TimeRaised == > ago(1d) &#124; Count özetlemek AlertSeverity tarafından count() = |Merhaba önem derecesine göre gruplandırılmış son 1 gün sırasında oluşturulan uyarılar |
| Hi &#124; Burada SourceSystem "OpsManager" ve TimeRaised == > ago(1d) &#124; RepeatCount desc sıralama |Merhaba yineleme sayısına göre sıralanmış son 1 gün sırasında oluşturulan uyarılar |


## <a name="next-steps"></a>Sonraki adımlar
* Log Analytics’ten uyarı oluşturma hakkında daha ayrıntılı bilgi edinmek için bkz. [Log Analytics’teki Uyarılar](log-analytics-alerts.md) .
