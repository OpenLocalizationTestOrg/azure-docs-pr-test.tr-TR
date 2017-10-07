---
title: Azure CDN aaaLog analize | Microsoft Docs
description: "Müşteri, Günlük çözümlemesi için Azure CDN etkinleştirebilirsiniz."
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 95e18b3c-b987-46c2-baa8-a27a029e3076
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: v-semcev
ms.openlocfilehash: 56e5a4fec46fd156cf38252732afb4522741d009
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-logs-for-azure-cdn"></a>Azure CDN için tanılama günlükleri

CDN uygulamanız için etkinleştirdikten sonra büyük olasılıkla toomonitor hello CDN kullanım, teslim hello durumunu denetleyin ve olası sorunları giderme. Azure CDN ile bu özellikleri sağlar [CDN temel analiz](cdn-analyze-usage-patterns.md) ve [tanılama günlükleri](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)

## <a name="cdn-core-analytics"></a>CDN temel analiz
Verizon standart veya premium profil ile geçerli bir Azure CDN kullanıcı olarak, önceden mümkün tooview temel analiz hello ek portal hello "Manage" seçeneğinden hello Azure portal aracılığıyla erişilebilir demektir. 

## <a name="azure-diagnostic-logs"></a>Azure tanılama günlükleri

Bu yeni özellik ile Azure, şimdi temel analiz görüntüleyebilir ve bunları dahil olmak üzere bir veya daha fazla hedefleri kaydedin:

 - Azure Storage hesabı
 - Azure Event Hubs
 - [OMS günlük analizi deposu](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started)
 
 Bu özellik tooVerizon (standart ve Premium) ve Akamai (standart) CDN profilleri ait tüm CDN uç noktası için kullanılabilir.

Özelleştirilmiş bir biçimde tüketebileceği böylece tanılama günlükleri tooexport temel kullanım ölçümleri, CDN uç noktası tooa çeşitli kaynaklardan gelen izin verin. Örneğin, bunu veri aktarma türleri hello:

- Veri tooblob depolama verme, tooCSV aktarın ve grafikleri oluşturun excel.
- Veri tooevent hub'ları dışarı aktarın ve diğer azure hizmetleriyle verilerle ilişkilendirmek.
- Kendi OMS çalışma alanındaki veri toolog analizi ve görünüm verileri dışarı aktarma

Merhaba aşağıdaki şekilde veri tipik bir CDN temel analiz görünüme gösterilmektedir.

![Portal - tanılama günlükleri](./media/cdn-diagnostics-log/01_OMS-workspace.png)

*Şekil 1 - CDN temel analiz görünümü*

izlenecek yol aşağıdaki hello hello çekirdek analiz verileri, adımlar hello özelliğini etkinleştirme ve bunları toovarious hedefleri teslim etme ve bu hedefleri tüketen hello şeması geçer.

## <a name="enable-logging-with-azure-portal"></a>Azure portal ile günlük kaydını etkinleştir

> [!NOTE]
> Merhaba tanılama günlükleri açık olan **kapalı** varsayılan olarak. 

CDN temel analiz tooenable günlüğüyle Hello adımları izleyin:

İçinde toohello oturum [Azure portal](http://portal.azure.com). İş akışınız için etkin CDN zaten yoksa [Azure CDN'yi etkinleştirme](cdn-create-new-endpoint.md) devam etmeden önce.

1. Merhaba Portalı'nda çok gidin**CDN profili**.
2. CDN profili seçin ve ardından hello CDN uç noktası tooenable istediğiniz **tanılama günlükleri**.

    ![Portal - tanılama günlükleri](./media/cdn-diagnostics-log/02_Browse-to-Diagnostics-logs.png)

3. Çok Git**tanılama günlükleri** altında dikey **izleme** bölümünde ardından hello durumu çok değiştirin**üzerinde**.

    ![Portal - tanılama günlükleri](./media/cdn-diagnostics-log/03_Diagnostics-logs-options.png)

### <a name="enable-logging-with-azure-storage"></a>Azure Storage ile günlük kaydını etkinleştir
    
toouse Azure Storage toostore hello günlükleri, seçin **arşiv tooa depolama hesabı**, bekletme günleri seçin ve tıklatın **CoreAnalytics** altında **günlük**.

![Portal - tanılama günlükleri](./media/cdn-diagnostics-log/04_Diagnostics-logs-storage.png)

*Şekil 2 - Azure Storage ile günlüğe kaydetme*

### <a name="logging-with-oms-log-analytics"></a>OMS günlük analizi ile günlüğe kaydetme

toouse OMS günlük analizi toostore hello günlükleri, şu adımları izleyin:

1. Merhaba gelen **tanılama günlükleri** altında dikey **izleme**seçin **tooLog Analytics gönderme** gelen 

    ![Portal - tanılama günlükleri](./media/cdn-diagnostics-log/05_Ready-to-Configure.png)    

2. Merhaba günlük analizi günlük yapılandırma üzerinde tıklayarak yapılandırın. Bu, önceki bir çalışma alanı seçin veya yeni bir tane oluşturun tooa iletişim götürür.

    ![Portal - tanılama günlükleri](./media/cdn-diagnostics-log/06_Choose-workspace.png)

3. Tıklatın **yeni çalışma alanı oluşturma**.

    ![Portal - tanılama günlükleri](./media/cdn-diagnostics-log/07_Create-new.png)

4. Ardından, yeni çalışma alanı adı, varolan abonelik, kaynak grubu (yeni veya var olan), konum ve fiyatlandırma katmanı seçmelisiniz. Bu yapılandırma tooyour panoya sabitleme hello seçeneğiniz vardır. Tamam toocomplete hello Yapılandırması'nı tıklatın.

    Ardından, OMS çalışma ve kaynak grubu adları ile çalışma alanınızı görmeniz gerekir. Adları benzersiz olmalıdır ve yalnızca harf, rakam ve kısa çizgi kullanabilirsiniz. Boşluk ve alt çizgi izin verilmiyor. 

    ![Portal - tanılama günlükleri](./media/cdn-diagnostics-log/08_Workspace-resource.png)

5. Sonraki çalışma alanınız oluşturuldu ve yapılandırma ekranında oturum tooyour döndürülen belirten kısa bir ileti alırsınız. Günlük analizi çalışma alanınız hello adını doğrulayabilirsiniz.

    ![Portal - tanılama günlükleri](./media/cdn-diagnostics-log/09_Return-to-logging.png)

    Merhaba günlük analizi yapılandırması ayarladıktan sonra CDN günlüğü için hello CoreAnalytics kutuyu da işaretlemeleri emin olun.

6. Her şeyi tooyour istediğiniz ise, hello tıklatın **kaydetmek** hello yapılandırma iletişim hello üstündeki düğmesi.

    ![Portal - tanılama günlükleri](./media/cdn-diagnostics-log/10_Save-me.png)

    Merhaba **kaydetmek** düğmesi artık etkin ve o hello üzerinde veya düğmeyi açık, ancak mavi mor yerine sunulmuştur.

7. Yeni bir OMS çalışma alanınızı toosee istiyorsanız, Git tooyour Azure portal panosunda, günlük analizi çalışma alanınız hello adını tıklatın. Çalışma alanınızı sonraki görürsünüz (OMS çalışma hello solda vurgulanmış olduğundan emin olun). Merhaba OMS portalı döşeme toosee üzerinde hello OMS deposu alanınızdaki'ı tıklatın. 

    ![Portal - tanılama günlükleri](./media/cdn-diagnostics-log/11_OMS-dashboard.png) 

    OMS deponuz hazır toolog veri sunulmuştur. İçinde bu verileri tooconsume sipariş, kullanmalısınız bir [OMS çözüm](#consuming-oms-log-analytics-data), bu makalenin sonraki bölümlerinde kapsanan.

Günlük verileri gecikmeler hakkında daha fazla bilgi için [burada](#log-data-delays).

## <a name="enable-logging-with-powershell"></a>PowerShell ile günlük kaydını etkinleştir

Aşağıda Azure PowerShell cmdlet'leri aracılığıyla tooenable ve get tanılama günlüklerini nasıl hello üzerinde bir örnektir.

###<a name="enabling-diagnostic-logs-in-a-storage-account"></a>Bir depolama hesabında oturum tanılama etkinleştirme

İlk oturum açın ve bir abonelik seçin:

    Login-AzureRmAccount 

    Select-AzureSubscription -SubscriptionId 


bir depolama hesabına tanılama günlüklerine tooEnable bu komutu kullanın:

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Cdn/profiles/{profileName}/endpoints/{endpointName}" -StorageAccountId "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicStorage/storageAccounts/{storageAccountName}" -Enabled $true -Categories CoreAnalytics
```
tooEnable tanılama günlükleri bir OMS çalışma alanında, bu komutu kullanın:

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId "/subscriptions/`{subscriptionId}<subscriptionId>
    .<subscriptionName>" -WorkspaceId "/subscriptions/<workspaceId>.<workspaceName>" -Enabled $true -Categories CoreAnalytics 
```



## <a name="consuming-diagnostics-logs-from-azure-storage"></a>Azure depolama biriminden tanılama günlüklerini kullanma
Nasıl bunlar içinde Azure Storage hesabını düzenlenir ve sağlayan örnek kodu toodownload hello tooa CSV dosyasına kaydeder, bu bölümde hello CDN temel analiz hello şeması açıklanır.

### <a name="using-microsoft-azure-storage-explorer"></a>Microsoft Azure Storage Gezgini kullanma
Hello çekirdek analiz verileri Azure depolama hesabı hello erişmeden önce önce bir aracı tooaccess Merhaba içeriğine bir depolama hesabı gerekir. Varken çeşitli araçlar kullanılabilir hello pazarında, hello önerdiğimiz bir hello Microsoft Azure Storage Gezgini ' dir. Merhaba aracından indirebilirsiniz [burada](http://storageexplorer.com/). Merhaba yazılım yükleyip yapılandırdıktan sonra toouse hedef toohello CDN tanılama günlükleri yapılandırılan aynı Azure depolama hesabı hello.

1.  Açık **Microsoft Azure Storage Gezgini**
2.  Merhaba depolama hesabını bulun
3.  Toohello Git **"Blob kapsayıcıları"** düğümü altında bu depolama hesabı ve hello düğümünü genişletin
4.  Adlı select hello kapsayıcı **"Öngörüler günlükleri coreanalytics"** ve çift tıklatın
5.  Sonuçları göster ayarlama gibi görünen hello ile ilk düzeyi, başlangıç hello sağ taraftaki bölmede **"ResourceId ="**. Merhaba dosya görene kadar tüm hello şekilde tıklayarak devam **PT1H.json**. Not hello yolu açıklaması için aşağıdaki hello bakın.
6.  Her bir blob **PT1H.json** temsil eder, belirli bir CDN uç noktası veya kendi özel etki alanı için bir saat analiz günlükleri hello.
7.  Bu JSON dosyasının Merhaba içeriğine Hello şeması hello bölümünde hello çekirdek analiz günlükleri şema açıklanan


> [!NOTE]
> **BLOB yol biçimi**
> 
> Çekirdek analiz günlükleri saatte üretilir. Bir saat için tüm veriler toplanır ve bir JSON yükü olarak tek bir Azure Blob içinde depolanır. Merhaba yolu toothis Azure Blob hiyerarşik bir yapı gibi görünür. Bu çünkü hello Depolama Gezgini araçları Yorumlar '/' dizin ayırıcı olarak ve kolaylık sağlamak için hello hiyerarşisini gösterir. Aslında, hello tam yolunu yalnızca hello blob adını temsil eder. Bu ad hello BLOB adlandırma kuralı aşağıdaki hello izler 
    
    resourceId=/SUBSCRIPTIONS/{Subscription Id}/RESOURCEGROUPS/{Resource Group Name}/PROVIDERS/MICROSOFT.CDN/PROFILES/{Profile Name}/ENDPOINTS/{Endpoint Name}/ y={Year}/m={Month}/d={Day}/h={Hour}/m={Minutes}/PT1H.json

**Alanları açıklaması:**

|değer|Açıklama|
|-------|---------|
|Abonelik Kimliği    |Hello Azure abonelik kimliği. Merhaba GUID biçiminde budur.|
|Kaynak |Merhaba kaynak grubu toowhich hello CDN kaynak grubu adı ait.|
|Profil adı |Merhaba CDN profili adı|
|Uç nokta adı |Merhaba CDN uç noktası adı|
|Yıl|  Örneğin, 2017 hello yılın 4 basamaklı gösterimi|
|Ay| Merhaba ay numarasına 2 basamaklı gösterimi. 01 Ocak =... 12 Aralık =|
|Gün|   Merhaba ayın hello 2 basamak gösterimi|
|PT1H.JSON| Merhaba analytics verilerinin depolandığı gerçek JSON dosyası|

### <a name="exporting-hello-core-analytics-data-tooa-csv-file"></a>Merhaba çekirdek analiz verileri tooa CSV dosyasını dışarı aktarma

toomake kolay tooaccess sağladığımız temel analiz hello BT kullanılan tooeasily olabilen bir düz virgülle ayrılmış dosya biçimine hello JSON dosyaları indirme sağlayan bir araç için bir örnek kodu grafikler veya diğer toplamaları oluşturun.

İşte nasıl hello aracını kullanabilirsiniz:

1.  Merhaba github bağlantıyı ziyaret edin: [https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv](https://github.com/Azure-Samples/azure-cdn-samples/tree/master/CoreAnalytics-ExportToCsv )
2.  Merhaba kodu indirme
3.  Yönergeler toocompile izleyin ve yapılandırma
4.  Merhaba aracını çalıştırın
5.  Sonuçta elde edilen CSV dosyasını hello analiz verileri basit bir düz hiyerarşi içinde gösterir.

## <a name="consuming-diagnostics-logs-from-an-oms-log-analytics-repository"></a>Tanılama günlüklerini bir OMS günlük analizi depodan kullanma
Günlük analizi Operations Management Suite (OMS), Bulut ve şirket içi ortamları toomaintain kendi kullanılabilirliğini ve performansını izler bir hizmettir. Bulut ve şirket içi ortamları ve diğer izleme araçları tooprovide analiz kaynaklar tarafından birden çok kaynakları genelinde oluşturulan veri toplar. 

Günlük analizi toouse, şunları yapmalısınız [günlük kaydını etkinleştir](#enable-logging-with-azure-storage) bu makalenin önceki bölümlerinde açıklanan toohello Azure OMS günlük analizi deposu.

### <a name="using-hello-oms-repository"></a>Merhaba OMS deposu kullanma

 Diyagram aşağıdaki hello hello girdi hello mimarisi ve hello deposu çıkışları gösterir:

![OMS günlük analizi deposu](./media/cdn-diagnostics-log/12_Repo-overview.png)

*Şekil 3 - günlük analizi deposu*

Yönetim çözümleri kullanılarak hello verileri çeşitli şekillerde görüntüleyebilirsiniz. Merhaba yönetim çözümleri edinebilirsiniz [Azure Marketi](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/monitoring-management?page=1&subcategories=management-solutions).

Merhaba tıklayarak yönetim çözümleri Azure Marketi'nden yükleyebilirsiniz **Şimdi Al** her çözüm hello sonundaki bağlantı.

### <a name="adding-an-oms-cdn-management-solution"></a>OMS CDN yönetim çözümünü ekleme

Bu adımları tooadd bir yönetim çözümü izleyin:

1.   Zaten yapmadıysanız, toohello içinde Azure aboneliğinizi kullanarak Azure portalında oturum açın ve tooyour Pano gidin.
    ![Azure Panosu](./media/cdn-diagnostics-log/13_Azure-dashboard.png)

2. Merhaba, **yeni** altında dikey **Market**seçin **izleme + Yönetim**.

    ![Market](./media/cdn-diagnostics-log/14_Marketplace.png)

3. Merhaba, **izleme + Yönetim** dikey penceresinde tıklatın **tümünü görmek**.

    ![Tümünü incele](./media/cdn-diagnostics-log/15_See-all.png)

4.  CDN hello arama kutusuna arayın.

    ![Tümünü incele](./media/cdn-diagnostics-log/16_Search-for.png)

5.  Seçin **Azure CDN temel analiz**. 

    ![Tümünü incele](./media/cdn-diagnostics-log/17_Core-analytics.png)

6.  ' I tıklattıktan sonra **oluşturma**, size yeni bir OMS çalışma alanı toocreate sorular veya mevcut bir kullanın. 

    ![Tümünü incele](./media/cdn-diagnostics-log/18_Adding-solution.png)

7.  Önce oluşturduğunuz hello çalışma alanını seçin. Ardından tooadd bir Otomasyon hesabı gerekir.

    ![Tümünü incele](./media/cdn-diagnostics-log/19_Add-automation.png)

8. Merhaba aşağıdaki ekran doldurmak zorunda hello Otomasyon hesabı form gösterilmektedir. 

    ![Tümünü incele](./media/cdn-diagnostics-log/20_Automation.png)

9. Merhaba Otomasyon hesabı oluşturduktan sonra hazır tooadd olan çözümünüzü. Merhaba tıklatın **oluşturma** düğmesi.

    ![Tümünü incele](./media/cdn-diagnostics-log/21_Ready.png)

10. Çözümünüzü tooyour çalışma alanı şimdi eklendi. Azure portal Pano tooyour geri dönün.

    ![Tümünü incele](./media/cdn-diagnostics-log/22_Dashboard.png)

    Merhaba günlük analizi çalışma alanı toogo tooyour çalışma alanı oluşturulduğunda'ı tıklatın. 

11. Merhaba tıklatın **OMS portalı** toosee yeni çözümünüz hello OMS portalında döşeme.

    ![Tümünü incele](./media/cdn-diagnostics-log/23_workspace.png)

12. OMS portalı Merhaba ekranında aşağıdaki gibi görünmelidir:

    ![Tümünü incele](./media/cdn-diagnostics-log/24_OMS-solution.png)

    Merhaba döşeme toosee birini birkaç görünüm verilerinizi tıklatın.

    ![Tümünü incele](./media/cdn-diagnostics-log/25_Interior-view.png)

    Sola kaydırma yapabilirsiniz veya daha fazla sağ toosee tek bir görünüm hello verilerini temsil eden yerleştirir. 

    Merhaba döşeme birine tıklayarak verileriniz hakkında daha fazla ayrıntı sağlar.

     ![Tümünü incele](./media/cdn-diagnostics-log/26_Further-detail.png)

### <a name="offers-and-pricing-tiers"></a>Teklifler ve fiyatlandırma katmanları

Teklifler ve OMS yönetim çözümleri için fiyatlandırma katmanlarına görebilirsiniz [burada](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-add-solutions#offers-and-pricing-tiers).

### <a name="customizing-views"></a>Görünümlerini özelleştirme

Hello kullanarak verilerinizi hello görünümünü özelleştirebilirsiniz **Görünüm Tasarımcısı**. Tooyour OMS çalışma alanına gidin ve tasarlamaya hello tıklayarak **Görünüm Tasarımcısı** döşeme.

![Görünüm Tasarımcısı](./media/cdn-diagnostics-log/27_Designer.png)

Sürükleme ve grafik türleri hello soldan bırakın ve sol hello üzerinde tooanalyze istediğiniz hello veri ayrıntıları doldurun.

![Görünüm Tasarımcısı](./media/cdn-diagnostics-log/28_Designer.png)

    
## <a name="log-data-delays"></a>Günlük verileri gecikmeleri

Verizon günlük veri gecikmeleri | Akamai günlük veri gecikmeleri
--- | ---
Verizon günlük verilerini 1 saat Gecikmeli ve uç nokta yayma işlemi tamamlandıktan sonra görünen too2 saatleri toostart yukarı gerçekleştirin. | Akamai günlük verilerini Gecikmeli 24 saat ve 24 saatten daha önce oluşturulduysa görünen too2 saatleri toostart alır. Yeni oluşturulduysa, görünen hello günlükleri toostart için too25 saatlerini alabilir.

## <a name="diagnostic-log-types-for-cdn-core-analytics"></a>CDN temel analiz için tanılama günlük türleri

HTTP yanıtı istatistiklerinin ve CDN POP/kenarları hello görülen çıkış istatistikleri gösteren ölçümleri içeren temel analiz günlükleri şu anda sunuyoruz.

### <a name="core-analytics-metrics-details"></a>Çekirdek Analytics ölçümleri ayrıntıları
Aşağıdaki tablonun hello ölçümleri temel analiz günlüklerini hello kullanılabilir bir listesini gösterir. Bu farklara en az olmasına rağmen tüm ölçümleri tüm sağlayıcılardan kullanılabilir. Ayrıca aşağıdaki tablonun hello belirli bir metrik sağlayıcıdan kullanılabilir olup olmadığını gösterir. Merhaba ölçümleri trafiği üzerlerinde sahip CDN uç için kullanılabilir olduğunu unutmayın.


|Ölçüm                     | Açıklama   | Verizon  | Akamai 
|---------------------------|---------------|---|---|
| RequestCountTotal         |Bu süre boyunca isteği isabet toplam sayısı| Evet  |Evet   |
| RequestCountHttpStatus2xx |Bir 2xx HTTP kod (örneğin, 200, 202) sonuçlandı tüm isteklerin sayısı              | Evet  |Evet   |
| RequestCountHttpStatus3xx | Bir 3xx HTTP kod (örneğin, 300, 302) sonuçlandı tüm isteklerin sayısı              | Evet  |Evet   |
| RequestCountHttpStatus4xx |Bir 4xx HTTP kod (örneğin, 400, 404) sonuçlandı tüm isteklerin sayısı               | Evet   |Evet   |
| RequestCountHttpStatus5xx | Bir 5xx HTTP kod (örneğin, 500, 504) sonuçlandı tüm isteklerin sayısı              | Evet  |Evet   |
| RequestCountHttpStatusOthers |  Diğer tüm HTTP kodları (dışında 2xx-5xx) sayısı | Evet  |Evet   |
| RequestCountHttpStatus200 | 200 HTTP kod yanıtıyla sonuçlanan tüm isteklerin sayısı              |Hayır   |Evet   |
| RequestCountHttpStatus206 | 206 HTTP kod yanıtıyla sonuçlanan tüm isteklerin sayısı              |Hayır   |Evet   |
| RequestCountHttpStatus302 | Bir 302 HTTP kod yanıtıyla sonuçlanan tüm isteklerin sayısı              |Hayır   |Evet   |
| RequestCountHttpStatus304 |  304 HTTP kod yanıtıyla sonuçlanan tüm isteklerin sayısı             |Hayır   |Evet   |
| RequestCountHttpStatus404 | 404 HTTP kod yanıtıyla sonuçlanan tüm isteklerin sayısı              |Hayır   |Evet   |
| RequestCountCacheHit |Önbelleği isabet sonuçlandı tüm isteklerin sayısı. Bu, doğrudan hello POP toohello istemci hello varlık sunulduğu anlamına gelir.               | Evet  |Hayır   |
| RequestCountCacheMiss | Önbellek isabetsizliği sonuçlandı tüm isteklerin sayısı. Bu hello varlık hello POP en yakın toohello istemcide bulunamadı ve bu nedenle kaynak hello alınan anlamına gelir.              |Evet   | Hayır  |
| RequestCountCacheNoCache | Merhaba kenar tooa kullanıcı yapılandırmasını son önbelleğe engellenir tooan varlık isteklerinin tüm sayısı.              |Evet   | Hayır  |
| RequestCountCacheUncacheable | Merhaba varlığın Cache-Control tarafından önbelleğe alınmış engellenir tooassets ister ve bunu POP veya hello HTTP istemci tarafından önbelleğe alınması gereken değil olduğunu belirtmek üstbilgileri süresi tüm sayısı                |Evet   |Hayır   |
| RequestCountCacheOthers | Tarafından yukarıda kapsanmayan önbellek durumundaki tüm isteklerin sayısı.              |Evet   | Hayır  |
| EgressTotal | Giden veri aktarımı GB              |Evet   |Evet   |
| EgressHttpStatus2xx | Giden veri aktarımı * 2xx HTTP durum kodları GB ile yanıtlar için            |Evet   |Hayır   |
| EgressHttpStatus3xx | 3xx HTTP durum kodları GB ile yanıtlar için giden veri aktarımı              |Evet   |Hayır   |
| EgressHttpStatus4xx | 4xx HTTP durum kodları GB ile yanıtlar için giden veri aktarımı               |Evet   | Hayır  |
| EgressHttpStatus5xx | 5xx HTTP durum kodları GB ile yanıtlar için giden veri aktarımı               |Evet   |  Hayır |
| EgressHttpStatusOthers | Giden veri aktarımı için diğer HTTP durum kodları GB yanıtları                |Evet   |Hayır   |
| EgressCacheHit |  Giden veri teslim edilen yanıtlar için doğrudan hello CDN önbellekten CDN POP/kenarları hello üzerinde aktarımı  |Evet   |  Hayır |
| EgressCacheMiss | Sırasında değil POP sunucu en yakın hello bulunan ve hello kaynak sunucudan alınan yanıt için giden veri aktarımı              |Evet   |  Hayır |
| EgressCacheNoCache | Merhaba kenar tooa kullanıcı yapılandırmasını son önbelleğe engellenir varlıklar için giden veri aktarımı.                |Evet   |Hayır   |
| EgressCacheUncacheable | Merhaba varlığın Cache-Control ve/veya onu POP veya hello HTTP istemci tarafından önbelleğe alınması gereken değil olduğunu belirtmek Expires üstbilgileri tarafından önbelleğe engellenir varlıklar için giden veri aktarımı                    |Evet   | Hayır  |
| EgressCacheOthers |  Giden veri diğer önbellek senaryolar için aktarır.             |Evet   | Hayır  |

* Giden veri aktarımı CDN POP sunucuları toohello istemciden teslim tootraffic başvuruyor.


### <a name="schema-of-hello-core-analytics-logs"></a>Merhaba çekirdek analiz günlükleri şeması 

Tüm günlükleri JSON biçiminde depolanır ve her bir giriş hello şema altına aşağıdaki dize alanları vardır:

```json
    "records": [
        {
            "time": "2017-04-27T01:00:00",
            "resourceId": "<ARM Resource Id of hello CDN Endpoint>",
            "operationName": "Microsoft.Cdn/profiles/endpoints/contentDelivery",
            "category": "CoreAnalytics",
            "properties": {
                "DomainName": "<Name of hello domain for which hello statistics is reported>",
                "RequestCountTotal": integer value,
                "RequestCountHttpStatus2xx": integer value,
                "RequestCountHttpStatus3xx": integer value,
                "RequestCountHttpStatus4xx": integer value,
                "RequestCountHttpStatus5xx": integer value,
                "RequestCountHttpStatusOthers": integer value,
                "RequestCountHttpStatus200": integer value,
                "RequestCountHttpStatus206": integer value,
                "RequestCountHttpStatus302": integer value,
                "RequestCountHttpStatus304": integer value,
                "RequestCountHttpStatus404": integer value,
                "RequestCountCacheHit": integer value,
                "RequestCountCacheMiss": integer value,
                "RequestCountCacheNoCache": integer value,
                "RequestCountCacheUncacheable": integer value,
                "RequestCountCacheOthers": integer value,
                "EgressTotal": double value,
                "EgressHttpStatus2xx": double value,
                "EgressHttpStatus3xx": double value,
                "EgressHttpStatus4xx": double value,
                "EgressHttpStatus5xx": double value,
                "EgressHttpStatusOthers": double value,
                "EgressCacheHit": double value,
                "EgressCacheMiss": double value,
                "EgressCacheNoCache": double value,
                "EgressCacheUncacheable": double value,
                "EgressCacheOthers": double value,
            }
        }

    ]
}
```

Burada Başlangıç 'saati' hello istatistikleri bildirilen hello saat sınır hello başlangıç saati gösterir. Ölçüm çift veya tamsayı değeri yerine bir CDN sağlayıcı tarafından desteklenmediğinde bir null değer olacaktır. Bu null değer ölçüm hello yokluğu gösterir ve bu 0 değerinden farklı. Ayrıca, bu ölçümleri hello uç noktasında yapılandırılmış etki alanı başına bir dizi olacaktır unutmayın.

Aşağıdaki örnek özellikleri:

```json
{
     "DomainName": "manlingakamaitest2.azureedge.net",
     "RequestCountTotal": 480,
     "RequestCountHttpStatus2xx": 480,
     "RequestCountHttpStatus3xx": 0,
     "RequestCountHttpStatus4xx": 0,
     "RequestCountHttpStatus5xx": 0,
     "RequestCountHttpStatusOthers": 0,
     "RequestCountHttpStatus200": 480,
     "RequestCountHttpStatus206": 0,
     "RequestCountHttpStatus302": 0,
     "RequestCountHttpStatus304": 0,
     "RequestCountHttpStatus404": 0,
     "RequestCountCacheHit": null,
     "RequestCountCacheMiss": null,
     "RequestCountCacheNoCache": null,
     "RequestCountCacheUncacheable": null,
     "RequestCountCacheOthers": null,
     "EgressTotal": 0.09,
     "EgressHttpStatus2xx": null,
     "EgressHttpStatus3xx": null,
     "EgressHttpStatus4xx": null,
     "EgressHttpStatus5xx": null,
     "EgressHttpStatusOthers": null,
     "EgressCacheHit": null,
     "EgressCacheMiss": null,
     "EgressCacheNoCache": null,
     "EgressCacheUncacheable": null,
     "EgressCacheOthers": null
}

```

## <a name="additional-resources"></a>Ek kaynaklar

* [Azure tanılama günlükleri](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)
* [Azure CDN ek Portalı aracılığıyla temel analiz](https://docs.microsoft.com/azure/cdn/cdn-analyze-usage-patterns)
* [Azure OMS günlük analizi](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-overview)
* [Azure günlük analizi REST API'si](https://docs.microsoft.com/en-us/rest/api/loganalytics)







