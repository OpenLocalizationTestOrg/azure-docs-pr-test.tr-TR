---
title: "Günlük analizi SQL analizi çözümde aaaAzure | Microsoft Docs"
description: "Hello Azure SQL analiz çözümü Azure SQL veritabanlarınızın yönetmenize yardımcı olur."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: b2712749-1ded-40c4-b211-abc51cc65171
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: fe228bb3cb3f9d578a84707c3917f02fbeb8a627
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-sql-database-using-azure-sql-analytics-preview-in-log-analytics"></a>Azure SQL veritabanı günlük analizi Azure SQL analizi (Önizleme) kullanarak izleme

![Azure SQL analizi simgesi](./media/log-analytics-azure-sql/azure-sql-symbol.png)

Hello Azure günlük analizi Azure SQL analizi çözümde toplar ve önemli SQL Azure performans ölçümleri visualizes. Merhaba çözümüyle topladığınız hello ölçümleri kullanarak özel izleme kurallarını ve uyarıları oluşturabilirsiniz. Azure SQL veritabanı izleyebilirsiniz ve esnek havuz ölçümler arasında birden çok Azure abonelikleri ve esnek havuzları ve bunları görselleştirin. Merhaba çözüm Ayrıca, uygulama yığınının her katmanda tooidentify sorunları yardımcı olur.  Kullandığı [Azure tanılama ölçümleri](log-analytics-azure-storage.md) günlük analizi ile birlikte tüm Azure SQL veritabanları ve esnek havuzlar ilgili toopresent verileri tek bir günlük analizi çalışma alanında görüntüler.

Şu anda too150, 000 Azure SQL veritabanları ve çalışma alanı başına 5.000 SQL esnek havuzlar yukarı Bu önizleme çözümünü destekler.

Merhaba günlük analizi için bulunan diğerleri gibi Azure SQL analiz çözümü izlemenize ve Azure kaynaklarınızı hello sistem durumu hakkında bildirim almak yardımcı olur; bu durumda, Azure SQL veritabanı. Microsoft Azure SQL veritabanı hello Azure bulut çalıştıran tanıdık SQL Server gibi özellikleri tooapplications sağlayan ölçeklenebilir ilişkisel veritabanı hizmetidir. Günlük analizi toocollect yardımcı olur, bağıntılı ve yapılandırılmış ve yapılandırılmamış verileri görselleştirin.

## <a name="connected-sources"></a>Bağlı kaynaklar

Hello Azure SQL analiz çözümü aracılarını tooconnect toohello günlük analizi hizmeti kullanmaz.

Aşağıdaki tablonun hello bu çözümü tarafından desteklenen hello bağlı kaynakları açıklar.

| Bağlı Kaynak | Destek | Açıklama |
| --- | --- | --- |
| [Windows aracıları](log-analytics-windows-agents.md) | Hayır | Doğrudan Windows aracıları hello çözümü tarafından kullanılmaz. |
| [Linux aracıları](log-analytics-linux-agents.md) | Hayır | Doğrudan Linux aracılarını hello çözümü tarafından kullanılmaz. |
| [SCOM yönetim grubu](log-analytics-om-agents.md) | Hayır | Merhaba SCOM Aracısı tooLog Analytics arasında doğrudan bağlantı hello çözümü tarafından kullanılmaz. |
| [Azure depolama hesabı](log-analytics-azure-storage.md) | Hayır | Günlük analizi depolama hesabından hello veri okuyamadı. |
| [Azure tanılama](log-analytics-azure-storage.md) | Evet | Azure ölçüm verileri tooLog Analytics doğrudan Azure tarafından gönderilir. |

## <a name="prerequisites"></a>Ön koşullar

- Azure aboneliği. Yoksa, için bir tane oluşturabilirsiniz [ücretsiz](https://azure.microsoft.com/free/).
- Günlük analizi çalışma alanı. Mevcut bir kullanabilir veya yapabilecekleriniz [yeni bir tane oluşturun](log-analytics-get-started.md) Bu çözüm kullanmaya başlamadan önce.
- Azure SQL veritabanları ve esnek havuzlar için Azure Tanılama'yı etkinleştirmek ve [toosend yapılandırmadan kendi veri tooLog Analytics](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).

## <a name="configuration"></a>Yapılandırma

Adımları tooadd hello Azure SQL analizi çözüm tooyour çalışma alanı aşağıdaki hello gerçekleştirin.

1. Hello Azure SQL analizi çözüm tooyour çalışma alanından eklemek [Azure Market](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) veya açıklanan hello işlemi kullanarak [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).
2. Hello Azure portal'ı tıklatın **yeni** (Merhaba + simgesi), kaynak hello listesinde seçin **izleme + Yönetim**.  
    ![İzleme + Yönetim](./media/log-analytics-azure-sql/monitoring-management.png)
3. Merhaba, **izleme + Yönetim** listesine **tümünü görmek**.
4. Merhaba, **önerilen** tıklatın **daha fazla** , hello yeni listesinde bulun **Azure SQL analizi (Önizleme)** ve seçin.  
    ![Azure SQL analiz çözümü](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)
5. Merhaba, **Azure SQL analizi (Önizleme)** dikey penceresinde tıklatın **oluşturma**.  
    ![Oluşturma](./media/log-analytics-azure-sql/portal-create.png)
6. Merhaba, **yeni çözüm oluşturmak** dikey penceresinde, tooadd hello çözüm tooand istediğiniz ardından tıklatın select hello çalışma **oluşturma**.  
    ![tooworkspace Ekle](./media/log-analytics-azure-sql/add-to-workspace.png)


### <a name="tooconfigure-multiple-azure-subscriptions"></a>tooconfigure birden çok Azure aboneliği

toosupport birden çok abonelik kullanmak hello PowerShell komut dosyasından [PowerShell kullanarak etkinleştirmek Azure kaynak ölçümleri günlük](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/). Merhaba çalışma kaynak kimliği hello betik toosend tanılama verilerini bir Azure aboneliği tooa çalışma alanında başka bir Azure aboneliğine kaynaklardan yürütülürken bir parametre olarak sağlayın.

**Örnek**

```
PS C:\> $WSID = "/subscriptions/<subID>/resourcegroups/oms/providers/microsoft.operationalinsights/workspaces/omsws"
```

```
PS C:\> .\Enable-AzureRMDiagnostics.ps1 -WSID $WSID
```

## <a name="using-hello-solution"></a>Merhaba çözümünü kullanarak

Merhaba çözüm tooyour çalışma eklediğinizde, Azure SQL analizi döşeme hello tooyour çalışma eklenir ve genel bakış bölümünde görüntülenir. Hello kutucuğu, Azure SQL veritabanı ve hello çözüm bağlandığı Azure SQL esnek havuzlar hello sayısını gösterir.

![Azure SQL analizi döşeme](./media/log-analytics-azure-sql/azure-sql-sol-tile.png)

### <a name="viewing-azure-sql-analytics-data"></a>Azure SQL analizi verileri görüntüleme

Tıklatın hello üzerinde **Azure SQL analizi** döşeme tooopen hello Azure SQL analizi Pano. Merhaba Pano hello dikey penceresi aşağıda tanımlanan içerir. Her dikey too15 kaynakları (abonelik, sunucu, esnek havuz ve veritabanı) listeler. Merhaba kaynakları tooopen hello Pano, belirli bir kaynak için birini tıklatın. Esnek havuz veya veritabanı seçili kaynak ölçümleri hello grafiklerle içerir. Bir grafik tooopen hello günlük arama iletişim kutusu'ı tıklatın.

| Dikey penceresi | Açıklama |
|---|---|
| Abonelikler | Abonelik sayısını bağlı sunucular, havuzları ve veritabanları ile listesi. |
| Sunucular | Bağlı havuzları ve veritabanları sayısı ile sunucuları listesi. |
| Esnek Havuzlar | En fazla GB ve gözlenen hello eDTU bağlı esnek havuzlar listesi süresi. |
|Veritabanları | Bağlı veritabanlarında gözlenen hello maksimum GB ve DTU listesi süresi.|


### <a name="analyze-data-and-create-alerts"></a>Verileri çözümlemek ve uyarı oluşturma

Uyarılar, Azure SQL veritabanı kaynaklardan gelen hello verilerle kolayca oluşturabilirsiniz. İşte birkaç faydalı [günlük arama](log-analytics-log-searches.md) uyarmak için kullanabileceğiniz sorgular:

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]


*Azure SQL veritabanı yüksek DTU*

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/DATABASES/"* MetricName=dtu_consumption_percent | measure Avg(Average) by Resource interval 5minutes
```

*Azure SQL Database esnek havuzunu üzerinde yüksek DTU*

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource interval 5minutes
```

Bu uyarı tabanlı sorgular tooalert belirli eşiklere Azure SQL veritabanı ve esnek havuzlar için kullanabilirsiniz. OMS çalışma alanınız için bir uyarı tooconfigure:

#### <a name="tooconfigure-an-alert-for-your-workspace"></a>tooconfigure çalışma alanınız için bir uyarı

1. Toohello Git [OMS portalı](http://mms.microsoft.com/) ve oturum açın.
2. Merhaba çözüm için yapılandırdığınız hello çalışma alanını açın.
3. Merhaba Hello genel bakış sayfasında, tıklatın **Azure SQL analizi (Önizleme)** döşeme.
4. Merhaba örnek sorguları birini çalıştırın.
5. Günlük aramada tıklatın **uyarı**.  
![Aramada uyarısı oluştur](./media/log-analytics-azure-sql/create-alert01.png)
6. Merhaba üzerinde **uyarı kuralı Ekle** sayfasında hello uygun özelliklerini yapılandırmak ve istediğiniz ve ardından özel eşikler hello **kaydetmek**.  
![Uyarı kuralı Ekle](./media/log-analytics-azure-sql/create-alert02.png)

### <a name="act-on-azure-sql-analytics-data"></a>Azure SQL analizi verilerde işlem yapmak

Örnek olarak, gerçekleştirebileceğiniz hello en yararlı sorguları toocompare hello DTU kullanımı tüm Azure SQL esnek havuzlar için tüm Azure abonelikleri biridir. Veritabanı işleme birimi (DTU) sağlayan bir şekilde toodescribe hello temel, standart ve Premium veritabanlarını ve havuzları performans düzeyinin göreli kapasitesini. Dtu'lar CPU karışık bir ölçüyü temel alır, bellek, okur ve yazar. Dtu'lar artırdıkça hello güç sunulan hello performans düzeyi artar. Örneğin, 1 DTU performans düzeyiyle beş kez daha fazla güç 5 Dtu'ya sahip bir performans düzeyine sahip. Maksimum DTU kota tooeach sunucusu ve esnek havuzu geçerlidir.

Günlük arama sorgusu aşağıdaki hello çalıştırarak, aşırı veya üzerinde SQL Azure esnek havuzları kullanan, kolayca anlayabilirsiniz.

```
Type=AzureMetrics ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource | display LineChart
```

>[!NOTE]
> Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), sorgu yukarıda hello toohello aşağıdaki değişeceğinden sonra.
>
>`search in (AzureMetrics) isnotempty(ResourceId) and "/ELASTICPOOLS/" and MetricName == "dtu_consumption_percent" | summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 1h), Resource | render timechart`

Aşağıdaki örneğine hello bir esnek havuz yüksek kullanımı % 100 yakın olduğunu görebilirsiniz başkalarının çok az kullanım varken DTU. Azure etkinlik günlükleri kullanarak, ortamınızda başka tootroubleshoot olası en son değişiklikler araştırabilirsiniz.

![Günlük arama sonuçları - yüksek kullanım](./media/log-analytics-azure-sql/log-search-high-util.png)

## <a name="see-also"></a>Ayrıca bkz.

- Kullanım [günlük aramaları](log-analytics-log-searches.md) günlük analizi tooview ayrıntılı Azure SQL veri.
- [Kendi panolar oluşturun](log-analytics-dashboards.md) Azure SQL verilerini göstererek.
- [Uyarı oluşturma](log-analytics-alerts.md) belirli Azure SQL olayları olduğunda.
