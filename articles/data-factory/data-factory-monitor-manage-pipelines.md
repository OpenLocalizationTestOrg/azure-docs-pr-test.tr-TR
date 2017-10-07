---
title: "aaaMonitor ve ardışık düzen hello Azure portal ve PowerShell kullanarak yönetme | Microsoft Docs"
description: "Nasıl toouse Azure portalı ve Azure PowerShell toomonitor hello ve hello Azure data factory'leri ve oluşturduğunuz ardışık düzen yönetmek öğrenin."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 9b0fdc59-5bbe-44d1-9ebc-8be14d44def9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: a8d3c7943e79450895ff754f06a37fdad1cbef92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-azure-portal-and-powershell"></a>İzleme ve hello Azure portal ve PowerShell kullanarak Azure Data Factory işlem hatlarını yönetme
> [!div class="op_single_selector"]
> * [Azure portal/Azure PowerShell kullanma](data-factory-monitor-manage-pipelines.md)
> * [Kullanılarak izleme ve yönetim uygulaması](data-factory-monitor-manage-app.md)


> [!IMPORTANT]
> Merhaba izleme ve yönetim uygulaması izleme ve veri işlem hatlarınızı yönetmek ve sorunları gidermek için daha iyi destek sağlar. Merhaba uygulaması kullanma hakkında daha fazla bilgi için bkz [izlemek ve hello izleme ve yönetim uygulaması kullanarak Data Factory işlem hatlarını yönetmek](data-factory-monitor-manage-app.md). 


Bu makalede nasıl toomonitor, yönetmek ve işlem hatlarınızı Azure portalı ve PowerShell kullanarak hata ayıklama açıklanmaktadır. Merhaba makale ayrıca nasıl toocreate uyarılar ve bilgiler almak sağlar hataları hakkında bildirim.

## <a name="understand-pipelines-and-activity-states"></a>Ardışık Düzen ve etkinlik durumlarını anlama
Hello Azure portal kullanarak şunları yapabilirsiniz:

* Veri fabrikanızın diyagramı olarak görüntüleyin.
* Bir ardışık düzendeki etkinlik görünümü.
* Giriş ve çıkış veri kümeleri görüntüleyin.

Bu bölümde ayrıca veri kümesi dilim durum tooanother durumundan nasıl geçiş açıklanmaktadır.   

### <a name="navigate-tooyour-data-factory"></a>Tooyour veri fabrikası gidin
1. İçinde toohello oturum [Azure portal](https://portal.azure.com).
2. Tıklatın **veri fabrikaları** hello sol hello menüsünde. Göremiyorsanız, tıklatın **daha fazla hizmet >**ve ardından **veri fabrikaları** hello altında **INTELLİGENCE + ANALİZ** kategorisi.

   ![Tümüne Gözat > veri fabrikaları](./media/data-factory-monitor-manage-pipelines/browseall-data-factories.png)
3. Merhaba üzerinde **veri fabrikaları** dikey penceresinde, ilgilendiğiniz select hello veri fabrikası.

    ![Veri Fabrikası seçin](./media/data-factory-monitor-manage-pipelines/select-data-factory.png)

   Merhaba veri fabrikası için hello giriş sayfasını görmeniz gerekir.

   ![Data factory dikey penceresi](./media/data-factory-monitor-manage-pipelines/data-factory-blade.png)

#### <a name="diagram-view-of-your-data-factory"></a>Veri fabrikanızın diyagram görünümü
Merhaba **diyagramı** data factory görünümünü hello veri fabrikası ve varlıklarını yönetmenize ve bölmeden cam toomonitor sağlar. toosee hello **diyagramı** 'ı tıklatın, görüntüleyin, veri fabrikası **diyagramı** hello giriş sayfasında hello veri fabrikası için.

![Diyagram görünümü](./media/data-factory-monitor-manage-pipelines/diagram-view.png)

Yakınlaştırma, yakınlaştırma toofit, yakınlaştırma too100%, kilit hello düzeni hello diyagramı çıkışı, yakınlaştırma ve otomatik olarak ardışık düzen ve veri kümeleri yerleştir. Merhaba veri çizgileri bilgileri de görebilirsiniz (diğer bir deyişle, seçilen öğelerin Yukarı Akış ve aşağı akış öğelerini göster).

### <a name="activities-inside-a-pipeline"></a>Bir işlem hattı içindeki etkinlikler
1. Merhaba ardışık düzen sağ tıklayın ve ardından **açık işlem hattı** toosee hello etkinlikler için girdi ve çıktı veri kümeleriyle birlikte potansiyel satış hello tüm etkinlikler. Bu özellik, işlem hattınızı birden fazla etkinlik içerir ve tek bir ardışık toounderstand hello işletimsel çizgileri istediğinizde yararlı olur.

    ![İşlem hattı menüsünü açma](./media/data-factory-monitor-manage-pipelines/open-pipeline-menu.png)     
2. Aşağıdaki örneğine hello kopyalama etkinliği bir girdi ve çıktı hello düzenindeki bakın. 

    ![Bir işlem hattı içindeki etkinlikler](./media/data-factory-monitor-manage-pipelines/activities-inside-pipeline.png)
3. Merhaba tıklatarak geri toohello hello data Factory giriş sayfasına gidebilirsiniz **veri fabrikası** hello içerik haritası hello sol üst köşesinde bağlantıyı.

    ![Geri toodata Fabrika gidin](./media/data-factory-monitor-manage-pipelines/navigate-back-to-data-factory.png)

### <a name="view-hello-state-of-each-activity-inside-a-pipeline"></a>Her etkinliği bir ardışık düzen içinde hello durumunu görüntüleyin
Merhaba durumunu hello etkinliği tarafından üretilen hello veri kümeleri görüntüleyerek hello geçerli bir etkinlik durumunu görüntüleyebilirsiniz.

Merhaba çift tıklatarak **OutputBlobTable** hello içinde **diyagramı**, farklı etkinlik çalışması içinde bir ardışık düzen tarafından üretilen tüm hello dilimler görebilirsiniz. Merhaba kopyalama etkinliği Merhaba son sekiz saat başarıyla çalıştırdı ve hello içinde hello dilimlerinin görebilirsiniz **hazır** durumu.  

![Merhaba ardışık durumu](./media/data-factory-monitor-manage-pipelines/state-of-pipeline.png)

Merhaba dataset dilimler hello veri fabrikasında durumları aşağıdaki hello biri olabilir:

<table>
<tr>
    <th align="left">Durum</th><th align="left">Bölgesine</th><th align="left">Açıklama</th>
</tr>
<tr>
    <td rowspan="8">Bekleniyor</td><td>ScheduleTime</td><td>Başlangıç saati hello dilim toorun için gelen kurmadı.</td>
</tr>
<tr>
<td>DatasetDependencies</td><td>Merhaba Yukarı Akış bağımlılıkları hazır değil.</td>
</tr>
<tr>
<td>ComputeResources</td><td>Merhaba işlem kaynakları kullanılabilir değil.</td>
</tr>
<tr>
<td>ConcurrencyLimit</td> <td>Tüm hello etkinlik örnekleri diğer dilimleri çalıştırıyor.</td>
</tr>
<tr>
<td>ActivityResume</td><td>Merhaba etkinlik duraklatıldı ve hello etkinlik sürdürülene kadar hello dilimler çalıştırılamaz.</td>
</tr>
<tr>
<td>Yeniden deneyin</td><td>Etkinlik yürütme yeniden deneniyor.</td>
</tr>
<tr>
<td>Doğrulama</td><td>Doğrulama henüz başlatılmadı.</td>
</tr>
<tr>
<td>ValidationRetry</td><td>Doğrulama denenen bekleme toobe ' dir.</td>
</tr>
<tr>
<tr>
<td rowspan="2">Devam ediyor</td><td>Doğrulama</td><td>Doğrulama devam ediyor.</td>
</tr>
<td>-</td>
<td>Merhaba dilim işleniyor.</td>
</tr>
<tr>
<td rowspan="4">Başarısız oldu</td><td>Süresi sona erdi</td><td>Merhaba Etkinlik yürütme hello etkinliği tarafından izin daha uzun sürdü.</td>
</tr>
<tr>
<td>İptal edildi</td><td>Merhaba dilim kullanıcı eylemi tarafından iptal edildi.</td>
</tr>
<tr>
<td>Doğrulama</td><td>Doğrulama başarısız oldu.</td>
</tr>
<tr>
<td>-</td><td>Merhaba dilim oluşturulan ve/veya doğrulanmış toobe başarısız oldu.</td>
</tr>
<td>Hazır</td><td>-</td><td>Merhaba dilim kullanıma hazır olur.</td>
</tr>
<tr>
<td>Atlandı</td><td>None</td><td>Merhaba dilimin işlenmekte olan değil.</td>
</tr>
<tr>
<td>None</td><td>-</td><td>Bir dilim tooexist farklı bir durum ile kullanılan ancak sıfırlandı.</td>
</tr>
</table>



Merhaba dilim girişinde tıklayarak bir dilim hello ayrıntılarını görüntüleyebilirsiniz **en son güncelleştirilen dilimler** dikey.

![Dilim ayrıntıları](./media/data-factory-monitor-manage-pipelines/slice-details.png)

Hello dilim birden çok kez yürütülmüşse, birden çok satır hello bkz **etkinlik çalışır** listesi. Hello çalıştırmak hello girişi tıklayarak Çalıştır etkinliği hakkında ayrıntılı bilgi görüntüleyebileceğiniz **etkinlik çalışır** listesi. Merhaba liste varsa bir hata iletisi ile birlikte tüm hello günlük dosyalarını gösterir. Bu özellik, veri fabrikası tooleave kalmadan yararlı tooview ve hata ayıklama günlüklerini kullanılabilir.

![Etkinlik çalışma ayrıntıları](./media/data-factory-monitor-manage-pipelines/activity-run-details.png)

Merhaba dilim hello değilse **hazır** durumu, hazır değil ve geçerli dilimin yürütülmesini hello hello engelleme hello Yukarı Akış dilimleri görebilirsiniz **hazır olmayan Yukarı Akış dilimleri** listesi. Bu özellik, dilim olduğunda yararlıdır **bekleyen** durumu ve istediğiniz dilim hello toounderstand hello Yukarı Akış bağımlılıkları bekliyor.

![Hazır olmayan yukarı akış dilimleri](./media/data-factory-monitor-manage-pipelines/upstream-slices-not-ready.png)

### <a name="dataset-state-diagram"></a>Veri kümesi durumu diyagramı
Veri Fabrikası dağıtmak ve hello ardışık düzen geçerli bir etkin döneme sahip sonra hello dataset durum tooanother geçiş böler. Şu anda durumu diyagramı aşağıdaki hello hello dilim durumunu izler:

![Durum Diyagramı](./media/data-factory-monitor-manage-pipelines/state-diagram.png)

Merhaba veri fabrikasında veri kümesi durumu geçişi akışı hello aşağıdadır: bekleme içinde-ilerleme/Sürüyor (doğrulama) -> hazır/başarısız->.

Merhaba dilim başlatır bir **bekleyen** durumu, yürütülmeden önce karşılanıp önkoşulları toobe için bekleniyor. Ardından, hello Etkinliğin başlangıç yürütme ve hello dilim girer içine bir **sürüyor** durumu. Merhaba Etkinlik yürütme başarılı veya başarısız. Merhaba dilim olarak işaretli **hazır** veya **başarısız**bağlı olarak hello hello yürütme sonucu.

Merhaba dilim toogo hello gelen geri sıfırlayabilirsiniz **hazır** veya **başarısız** durumu toohello **bekleyen** durumu. Merhaba dilim durumu çok işaretleyebilirsiniz**atla**, yürütme ve hello dilim işlenmiyor hello etkinlik engeller.

## <a name="pause-and-resume-pipelines"></a>Ardışık Düzen Durdur
Azure PowerShell kullanarak işlem hatlarınızı yönetebilirsiniz. Örneğin, duraklatma ve ardışık düzen Azure PowerShell cmdlet'lerini çalıştırarak sürdürme. 

> [!NOTE] 
> Merhaba diyagram görünümü, duraklatma ve sürdürme ardışık düzen desteklemez. Bir kullanıcı arabirimi toouse istiyorsanız hello izleme ve yönetme uygulaması kullanın. Merhaba uygulaması kullanma hakkında daha fazla bilgi için bkz [izlemek ve hello izleme ve yönetim uygulaması kullanarak Data Factory işlem hatlarını yönetmek](data-factory-monitor-manage-app.md) makalesi. 

Duraklat/işlem hatları hello kullanarak askıya alabilirsiniz **Suspend-AzureRmDataFactoryPipeline** PowerShell cmdlet'i. Bu cmdlet, bir sorun düzeltilene kadar toorun hatlarınızı istemediğiniz yararlıdır. 

```powershell
Suspend-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
Örneğin:

```powershell
Suspend-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

Merhaba ardışık ile Merhaba sorun çözüldükten sonra hello aşağıdaki PowerShell komutunu çalıştırarak askıya hello ardışık düzen devam edebilirsiniz:

```powershell
Resume-AzureRmDataFactoryPipeline [-ResourceGroupName] <String> [-DataFactoryName] <String> [-Name] <String>
```
Örneğin:

```powershell
Resume-AzureRmDataFactoryPipeline -ResourceGroupName ADF -DataFactoryName productrecgamalbox1dev -Name PartitionProductsUsagePipeline
```

## <a name="debug-pipelines"></a>Ardışık Düzen hata ayıklama
Azure Data Factory Zengin özellikleri sizin için toodebug sağlar ve ardışık düzen hello Azure portalı ve Azure PowerShell kullanarak sorun giderme.

> [! Bu çok daha kolay kullanarak hataları izleme hello tootroubleshot ve yönetim uygulaması Not}. Merhaba uygulaması kullanma hakkında daha fazla bilgi için bkz [izlemek ve hello izleme ve yönetim uygulaması kullanarak Data Factory işlem hatlarını yönetmek](data-factory-monitor-manage-app.md) makalesi. 

### <a name="find-errors-in-a-pipeline"></a>Ardışık düzeninde hataları bulma
Ardışık düzeninde hello etkinlik başarısız olursa hello ardışık düzen tarafından üretilen hello dataset hello hatası nedeniyle bir hata durumunda olur. Hata ayıklama ve yöntemleri aşağıdaki hello kullanarak Azure Data factory'de hatalarında sorun giderme.

#### <a name="use-hello-azure-portal-toodebug-an-error"></a>Hello Azure portal toodebug hata kullanın
1. Merhaba üzerinde **tablo** dikey penceresinde hello sahip hello sorun dilimi tıklatın **durum** çok ayarlamak**başarısız**.

   ![Sorun dilim ile tablo dikey penceresi](./media/data-factory-monitor-manage-pipelines/table-blade-with-error.png)
2. Merhaba üzerinde **veri dilimi** dikey penceresinde hello etkinlik başarısız Çalıştır'ı tıklatın.

   ![Veri dilimi bir hata ile](./media/data-factory-monitor-manage-pipelines/dataslice-with-error.png)
3. Merhaba üzerinde **etkinlik çalışma ayrıntıları** dikey penceresinde hello Hdınsight işleme ile ilişkili olan hello dosyaları karşıdan yükleyebilirsiniz. Tıklatın **karşıdan** hello hata hakkındaki ayrıntılar içeren durumu/stderr toodownload hello hata günlüğü dosyası için.

   ![Etkinlik ayrıntıları dikey penceresinde hatası ile çalıştırma](./media/data-factory-monitor-manage-pipelines/activity-run-details-with-error.png)     

#### <a name="use-powershell-toodebug-an-error"></a>PowerShell toodebug hata kullanın
1. **PowerShell**’i başlatın.
2. Merhaba çalıştırmak **Get-AzureRmDataFactorySlice** toosee hello dilimleri ve bunların durumlarını komutu. Merhaba durumuna sahip bir dilim görmeniz gerekir **başarısız**.        

    ```powershell   
    Get-AzureRmDataFactorySlice [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime] <DateTime> [[-EndDateTime] <DateTime> ] [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```   
   Örneğin:

    ```powershell   
    Get-AzureRmDataFactorySlice -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime 2014-05-04 20:00:00
    ```

   Değiştir **StartDateTime** hattınızı başlangıç saati ile. 
3. Şimdi, hello çalıştırın **Get-AzureRmDataFactoryRun** cmdlet tooget etkinliği hakkında ayrıntılı bilgi hello hello dilim için çalıştırın.

    ```powershell   
    Get-AzureRmDataFactoryRun [-ResourceGroupName] <String> [-DataFactoryName] <String> [-DatasetName] <String> [-StartDateTime]
    <DateTime> [-Profile <AzureProfile> ] [ <CommonParameters>]
    ```

    Örneğin:

    ```powershell   
    Get-AzureRmDataFactoryRun -ResourceGroupName ADF -DataFactoryName LogProcessingFactory -DatasetName EnrichedGameEventsTable -StartDateTime "5/5/2014 12:00:00 AM"
    ```

    Merhaba StartDateTime hello önceki adımda not ettiğiniz hello hata/sorun dilim için hello başlangıç zamanı değeridir. Merhaba tarih-saat çift tırnak içine alınabilir.
4. Benzer toohello aşağıda hello hata ilişkin ayrıntıları içeren bir çıktı görmeniz gerekir:

    ```   
    Id                      : 841b77c9-d56c-48d1-99a3-8c16c3e77d39
    ResourceGroupName       : ADF
    DataFactoryName         : LogProcessingFactory3
    DatasetName               : EnrichedGameEventsTable
    ProcessingStartTime     : 10/10/2014 3:04:52 AM
    ProcessingEndTime       : 10/10/2014 3:06:49 AM
    PercentComplete         : 0
    DataSliceStart          : 5/5/2014 12:00:00 AM
    DataSliceEnd            : 5/6/2014 12:00:00 AM
    Status                  : FailedExecution
    Timestamp               : 10/10/2014 3:04:52 AM
    RetryAttempt            : 0
    Properties              : {}
    ErrorMessage            : Pig script failed with exit code '5'. See wasb://        adfjobs@spestore.blob.core.windows.net/PigQuery
                                    Jobs/841b77c9-d56c-48d1-99a3-
                8c16c3e77d39/10_10_2014_03_04_53_277/Status/stderr' for
                more details.
    ActivityName            : PigEnrichLogs
    PipelineName            : EnrichGameLogsPipeline
    Type                    :
    ```
5. Merhaba çalıştırabilirsiniz **Kaydet AzureRmDataFactoryLog** hello hello çıkışı görmek ve hello kullanarak hello günlük dosyalarını indirmek kimliği değeri cmdlet'iyle **- DownloadLogsoption** hello cmdlet'i için.

    ```powershell
    Save-AzureRmDataFactoryLog -ResourceGroupName "ADF" -DataFactoryName "LogProcessingFactory" -Id "841b77c9-d56c-48d1-99a3-8c16c3e77d39" -DownloadLogs -Output "C:\Test"
    ```

## <a name="rerun-failures-in-a-pipeline"></a>Ardışık düzeninde hataları yeniden çalıştırın

> [!IMPORTANT]
> Daha kolay tootroubleshoot hataları olan ve izleme ve yönetim uygulaması kullanarak yeniden çalıştır başarısız dilimler hello. Merhaba uygulaması kullanma hakkında daha fazla bilgi için bkz [izlemek ve hello izleme ve yönetim uygulaması kullanarak Data Factory işlem hatlarını yönetmek](data-factory-monitor-manage-app.md). 

### <a name="use-hello-azure-portal"></a>Hello Azure portalını kullanın
Sorun giderme ve hata ayıklama hataları ardışık düzeninde sonra toohello hata dilim gezinme ve hello tıklayarak hataları çalıştırabilirsiniz **çalıştırmak** hello komut çubuğunda düğmesi.

![Başarısız bir dilimi yeniden çalıştırın](./media/data-factory-monitor-manage-pipelines/rerun-slice.png)

(Örneğin, veri kullanılamıyorsa) durumda hello dilim doğrulama bir ilke hatası nedeniyle başarısız oldu, hello hatası düzeltin ve yeniden hello tıklayarak doğrulamayı **doğrulama** hello komut çubuğunda düğmesi.

![Hataları giderin ve doğrulama](./media/data-factory-monitor-manage-pipelines/fix-error-and-validate.png)

### <a name="use-azure-powershell"></a>Azure PowerShell kullanma
Hello kullanarak hataları çalıştırabilirsiniz **Set-AzureRmDataFactorySliceStatus** cmdlet'i. Merhaba bkz [Set-AzureRmDataFactorySliceStatus](https://msdn.microsoft.com/library/mt603522.aspx) sözdizimi ve hello cmdlet'i hakkındaki diğer ayrıntılar için konu.

**Örnek:**

Merhaba aşağıdaki örnek ayarlar hello tablo 'DAWikiAggregatedData' too'Waiting tüm dilimleri hello durumunu ' hello Azure data factory'de 'WikiADF'.

Merhaba 'Güncelleştirme türü' too'UpstreamInPipeline ayarlanmış ', yani her dilim Merhaba tablonun tüm hello bağımlı (Yukarı Akış) tablolar ve durumlarını too'Waiting ayarlanır'. Bu parametre 'Bireysel' için başka bir olası değer hello.

```powershell
Set-AzureRmDataFactorySliceStatus -ResourceGroupName ADF -DataFactoryName WikiADF -DatasetName DAWikiAggregatedData -Status Waiting -UpdateType UpstreamInPipeline -StartDateTime 2014-05-21T16:00:00 -EndDateTime 2014-05-21T20:00:00
```

## <a name="create-alerts"></a>Uyarı oluşturma
Azure günlükleri kullanıcı olayları bir Azure kaynak olduğunda (örneğin, veri fabrikası) oluşturulan, güncelleştirilmiş veya silinmiş. Bu olaylara bağlı olarak uyarıları oluşturabilirsiniz. Veri Fabrikası toocapture çeşitli ölçümleri kullanın ve ölçümleri uyarılar oluşturabilir. Gerçek zamanlı izleme için olayları kullanın ve ölçümleri geçmiş amaçları için kullanmak öneririz.

### <a name="alerts-on-events"></a>Uyarı olayları
Azure olayları, Azure kaynaklarınızı neler olduğunu içine yararlı bilgiler sağlar. Azure Data Factory kullanırken, olaylar oluşturulur zaman:

* Veri Fabrikası oluşturulduğunda, silinmiş veya güncelleştirildiğinde.
* Veri işleme ("çalışır") olarak başlatıldı veya tamamlandı.
* İsteğe bağlı Hdınsight kümesi oluşturulduğunda veya kaldırılmış.

Bu kullanıcı olaylarına uyarılar oluşturabilir ve bunları toosend e-posta bildirimleri toohello yönetici ve coadministrators hello aboneliğin yapılandırın. Ayrıca, tooreceive e-posta bildirimleri hello koşullar karşılandığında isteyen kullanıcıların ek e-posta adresini belirtebilirsiniz. Bu özellik, hataları üzerinde bildirim tooget ve toocontinuously İzleyici, veri fabrikası istemediğiniz istediğinizde yararlıdır.

> [!NOTE]
> Şu anda hello portal olayları uyarıları göstermez. Kullanım hello [izleme ve yönetim uygulaması](data-factory-monitor-manage-app.md) toosee tüm uyarılar.


#### <a name="specify-an-alert-definition"></a>Bir uyarı tanımı belirtin
bir uyarı tanımı toospecify, uyarı toobe istediğiniz hello işlemleri açıklayan bir JSON dosyası oluşturun. Aşağıdaki örneğine hello hello uyarısı hello RunFinished işlemi için bir e-posta bildirimi gönderir. toobe belirli, bir e-posta bildirimi gönderildi hello veri fabrikasında bir farklı çalıştır tamamlandı ve Çalıştır hello başarısız oldu (durum = FailedExecution).

```JSON
{
    "contentVersion": "1.0.0.0",
     "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters": {},
    "resources":
    [
        {
            "name": "ADFAlertsSlice",
            "type": "microsoft.insights/alertrules",
            "apiVersion": "2014-04-01",
            "location": "East US",
            "properties":
            {
                "name": "ADFAlertsSlice",
                "description": "One or more of hello data slices for hello Azure Data Factory has failed processing.",
                "isEnabled": true,
                "condition":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.ManagementEventRuleCondition",
                    "dataSource":
                    {
                        "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleManagementEventDataSource",
                        "operationName": "RunFinished",
                        "status": "Failed",
                        "subStatus": "FailedExecution"   
                    }
                },
                "action":
                {
                    "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails": [ "<your alias>@contoso.com" ]
                }
            }
        }
    ]
}
```

Kaldırabileceğiniz **subStatus** hello belirli bir arıza uyarı toobe istemiyorsanız, JSON tanımını gelen.

Bu örnek, aboneliğinizdeki tüm veri fabrikaları için hello uyarı ayarlar. Merhaba uyarı toobe belirli veri fabrikası için ayarlamak istiyorsanız, veri fabrikası belirtebilirsiniz **resourceUri** hello içinde **dataSource**:

```JSON
"resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>"
```

Merhaba aşağıdaki tabloda kullanılabilir işlemleri ve durumları (ve alt durumlar) hello listesini sağlar.

| İşlem adı | Durum | Alt durum |
| --- | --- | --- |
| RunStarted |başlatıldı |Başlangıç |
| RunFinished |Başarısız / başarılı oldu |FailedResourceAllocation<br/><br/>Başarılı oldu<br/><br/>FailedExecution<br/><br/>Süresi sona erdi<br/><br/>< iptal edildi<br/><br/>FailedValidation<br/><br/>terk |
| OnDemandClusterCreateStarted |başlatıldı | |
| OnDemandClusterCreateSuccessful |Başarılı oldu | |
| OnDemandClusterDeleted |Başarılı oldu | |

Bkz: [uyarı kuralı oluştur](https://msdn.microsoft.com/library/azure/dn510366.aspx) hello örnekte kullanılan hello JSON öğeleri hakkında ayrıntılı bilgi için.

#### <a name="deploy-hello-alert"></a>Merhaba uyarı dağıtma
toodeploy hello uyarı, hello Azure PowerShell cmdlet'ini kullanın **New-AzureRmResourceGroupDeployment**hello aşağıdaki örnekte gösterildiği gibi:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\ADFAlertFailedSlice.json  
```

Merhaba kaynak grubuna dağıtım başarıyla tamamladıktan sonra aşağıdaki iletileri hello bakın:

```
VERBOSE: 7:00:48 PM - Template is valid.
WARNING: 7:00:48 PM - hello StorageAccountName parameter is no longer used and will be removed in a future release.
Please update scripts tooremove this parameter.
VERBOSE: 7:00:49 PM - Create template deployment 'ADFAlertFailedSlice'.
VERBOSE: 7:00:57 PM - Resource microsoft.insights/alertrules 'ADFAlertsSlice' provisioning status is succeeded

DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

> [!NOTE]
> Merhaba kullanabilirsiniz [uyarı kuralı oluştur](https://msdn.microsoft.com/library/azure/dn510366.aspx) REST API toocreate bir uyarı kuralı. Merhaba JSON yükü benzer toohello JSON örnektir.  


#### <a name="retrieve-hello-list-of-azure-resource-group-deployments"></a>Azure kaynak grubu dağıtımı Hello listesini alma
tooretrieve hello listesi dağıtılan Azure kaynak grubu dağıtımı, hello cmdlet'ini kullanın **Get-AzureRmResourceGroupDeployment**hello aşağıdaki örnekte gösterildiği gibi:

```powershell
Get-AzureRmResourceGroupDeployment -ResourceGroupName adf
```

```
DeploymentName    : ADFAlertFailedSlice
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 10/11/2014 2:01:00 AM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           :
```

#### <a name="troubleshoot-user-events"></a>Kullanıcı olaylarına sorun giderme
1. Merhaba tıkladıktan sonra oluşturulan tüm hello olayları görebilirsiniz **ölçümleri ve işlemleri** döşeme.

    ![Ölçümleri ve işlemleri bölmesi](./media/data-factory-monitor-manage-pipelines/metrics-and-operations-tile.png)
2. Merhaba tıklatın **olayları** toosee hello olaylar bölmesi.

    ![Olaylar bölmesi](./media/data-factory-monitor-manage-pipelines/events-tile.png)
3. Merhaba üzerinde **olayları** dikey penceresinde, olaylar, filtrelenmiş olayları ve benzeri ayrıntılarını görebilirsiniz.

    ![Olaylar dikey penceresi](./media/data-factory-monitor-manage-pipelines/events-blade.png)
4. Tıklatın bir **işlemi** bir hataya neden olur hello işlemleri listesinde.

    ![Bir işlem seçin](./media/data-factory-monitor-manage-pipelines/select-operation.png)
5. Tıklatın bir **hata** olay toosee hello hata ayrıntıları.

    ![Olay hatası](./media/data-factory-monitor-manage-pipelines/operation-error-event.png)

Bkz: [Azure Insight cmdlet'leri](https://msdn.microsoft.com/library/mt282452.aspx) tooadd kullanabilirsiniz, PowerShell cmdlet'leri almak veya uyarıları kaldırın. Merhaba kullanmanın bazı örnekler şunlardır **Get-AlertRule** cmdlet:

```powershell
get-alertrule -res $resourceGroup -n ADFAlertsSlice -det
```

```
Properties :
Action      : Microsoft.Azure.Management.Insights.Models.RuleEmailAction
Condition   :
DataSource :
EventName             :
Category              :
Level                 :
OperationName         : RunFinished
ResourceGroupName     :
ResourceProviderName  :
ResourceId            :
Status                : Failed
SubStatus             : FailedExecution
Claims                : Microsoft.Azure.Management.Insights.Models.RuleManagementEventClaimsDataSource
Condition      :
Description : One or more of hello data slices for hello Azure Data Factory has failed processing.
Status      : Enabled
Name:       : ADFAlertsSlice
Tags       :
$type          : Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/ADFAlertsSlice
Location   : West US
Name       : ADFAlertsSlice
```

```powershell
Get-AlertRule -res $resourceGroup
```
```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0

Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest3
Location   : West US
Name       : FailedExecutionRunsWest3
```

```powershell
Get-AlertRule -res $resourceGroup -Name FailedExecutionRunsWest0
```

```
Properties : Microsoft.Azure.Management.Insights.Models.Rule
Tags       : {[$type, Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage]}
Id         : /subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/microsoft.insights/alertrules/FailedExecutionRunsWest0
Location   : West US
Name       : FailedExecutionRunsWest0
```

Get-help komutları toosee ayrıntılarını ve örnekler hello Get-AlertRule cmdlet'i için aşağıdaki hello çalıştırın.

```powershell
get-help Get-AlertRule -detailed
```

```powershell
get-help Get-AlertRule -examples
```


Merhaba uyarı oluşturma olayları görüyorsanız hello portal dikey penceresinde, ancak e-posta bildirimleri almadığınız, belirtilen hello e-posta adresi dış gönderenlerden tooreceive e-postaları ayarlanmış olup olmadığını denetleyin. Hello uyarı e-postalar, e-posta ayarlarınız tarafından engellenmiş.

### <a name="alerts-on-metrics"></a>Ölçümleri uyarılar
Veri fabrikasında çeşitli ölçümleri yakalamak ve ölçümleri uyarılar oluşturabilir. İzleme ve uyarılar, veri fabrikası hello dilimleri ölçümlerini aşağıdaki hello oluşturun:

* **Başarısız çalıştırır**
* **Başarılı çalıştırır**

Bu ölçümler yararlıdır ve genel başarılı ve başarısız genel bir bakış hello veri fabrikasında çalıştıran tooget yardımcı olur. Olduğundan her zaman dilimi Çalıştır ölçümleri gösterilen. Başında hello başlangıç saati, bu ölçümleri toplanır ve tooyour depolama hesabı gönderilir. bir depolama hesabı ayarlamanız tooenable ölçümleri.

#### <a name="enable-metrics"></a>Ölçümleri etkinleştir
tooenable ölçümleri tıklatın hello hello aşağıdakini **Data Factory** dikey penceresinde:

**İzleme** > **ölçüm** > **tanılama ayarlarını** > **tanılama**

![Tanılama bağlantı](./media/data-factory-monitor-manage-pipelines/diagnostics-link.png)

Merhaba üzerinde **tanılama** dikey penceresinde tıklatın **üzerinde**hello depolama hesabını seçin ve'ı tıklatın **kaydetmek**.

![Tanılama dikey penceresi](./media/data-factory-monitor-manage-pipelines/diagnostics-blade.png)

Hello ölçümleri toobe hello üzerinde görünür tooone saattir yukarı sürebilir **izleme** dikey çünkü ölçümleri toplama saatlik olur.

### <a name="set-up-an-alert-on-metrics"></a>Ölçümler hakkında bir uyarı ayarlama
Merhaba tıklatın **Data Factory ölçümleri** döşeme:

![Veri Fabrikası ölçümleri kutucuğu](./media/data-factory-monitor-manage-pipelines/data-factory-metrics-tile.png)

Merhaba üzerinde **ölçüm** dikey penceresinde tıklatın **+ uyarı Ekle** hello araç çubuğunda.
![Data factory ölçüm dikey penceresi > Uyarı Ekle](./media/data-factory-monitor-manage-pipelines/add-alert.png)

Merhaba üzerinde **uyarı kuralı eklemek** sayfasında, aşağıdaki adımları hello ve tıklayın **Tamam**.

* Merhaba uyarı için bir ad girin (örnek: "uyarı başarısız oldu").
* Merhaba uyarı için bir açıklama girin (örnek: "bir hata oluştuğunda bir e-posta Gönder").
* Bir ("Çalıştığında başarısız oldu" vs. ölçümünü seçin "Başarılı çalışır").
* Bir koşul ve bir eşik değeri belirtin.   
* Merhaba süreyi belirtin.
* Bir e-posta tooowners, Katkıda Bulunanlar ve okuyucular gönderilmesi gerekip gerekmediğini belirtin.

![Data factory ölçüm dikey penceresi > Uyarı kuralı Ekle](./media/data-factory-monitor-manage-pipelines/add-an-alert-rule.png)

Sonra Hello uyarı kuralı başarıyla eklendi, hello dikey penceresi kapanır ve üzerinde hello hello yeni uyarı gördüğünüz **ölçüm** dikey.

![Data factory ölçüm dikey penceresi > eklenen yeni uyarı](./media/data-factory-monitor-manage-pipelines/failed-alert-in-metric-blade.png)

Merhaba uyarılar hello sayısı görmeniz gerekir **uyarı kuralları** döşeme. Merhaba tıklatın **uyarı kuralları** döşeme.

![Data factory ölçüm dikey penceresi - uyarı kuralları](./media/data-factory-monitor-manage-pipelines/alert-rules-tile-rules.png)

Merhaba üzerinde **uyarı kuralları** dikey penceresinde, var olan tüm uyarıları görebilir. bir uyarı, tooadd tıklatın **uyarı Ekle** hello araç.

![Uyarı kuralları dikey penceresi](./media/data-factory-monitor-manage-pipelines/alert-rules-blade.png)

### <a name="alert-notifications"></a>Uyarı bildirimleri
Merhaba uyarı kuralı hello koşulu ile eşleşen sonra hello uyarı etkinleştirildikten bildiren bir e-posta almanız gerekir. Merhaba sorun çözüldüğünde ve hello Uyarı koşulu artık eşleşmiyor sonra hello uyarı çözümlendiğinde bildiren bir e-posta alır.

Bu davranış için bir uyarı kuralı niteleyen her hatasında bir bildirim burada gönderilen olaylar farklıdır.

### <a name="deploy-alerts-by-using-powershell"></a>PowerShell kullanarak uyarıları dağıtma
Ölçümleri aynı hello için uyarıları dağıtabilirsiniz olaylar için bunu yolu.

**Uyarı tanımı**

```JSON
{
    "contentVersion" : "1.0.0.0",
    "$schema" : "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "parameters" : {},
    "resources" : [
    {
            "name" : "FailedRunsGreaterThan5",
            "type" : "microsoft.insights/alertrules",
            "apiVersion" : "2014-04-01",
            "location" : "East US",
            "properties" : {
                "name" : "FailedRunsGreaterThan5",
                "description" : "Failed Runs greater than 5",
                "isEnabled" : true,
                "condition" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
                    "dataSource" : {
                        "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
                        "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
                        "resourceUri" : "/SUBSCRIPTIONS/<subscriptionId>/RESOURCEGROUPS/<resourceGroupName
>/PROVIDERS/MICROSOFT.DATAFACTORY/DATAFACTORIES/<dataFactoryName>",
                        "metricName" : "FailedRuns"
                    },
                    "threshold" : 5.0,
                    "windowSize" : "PT3H",
                    "timeAggregation" : "Total"
                },
                "action" : {
                    "$type" : "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
                    "odata.type" : "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
                    "customEmails" : ["abhinav.gpt@live.com"]
                }
            }
        }
    ]
}
```

Değiştir *Subscriptionıd*, *resourceGroupName*, ve *dataFactoryName* uygun değerlerle hello örnekteki.

*metricName* şu anda iki değer destekler:

* FailedRuns
* SuccessfulRuns

**Merhaba uyarı dağıtma**

toodeploy hello uyarı, hello Azure PowerShell cmdlet'ini kullanın **New-AzureRmResourceGroupDeployment**hello aşağıdaki örnekte gösterildiği gibi:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName adf -TemplateFile .\FailedRunsGreaterThan5.json
```

Başarılı dağıtım sonrasında iletiden görmeniz gerekir:

```
VERBOSE: 12:52:47 PM - Template is valid.
VERBOSE: 12:52:48 PM - Create template deployment 'FailedRunsGreaterThan5'.
VERBOSE: 12:52:55 PM - Resource microsoft.insights/alertrules 'FailedRunsGreaterThan5' provisioning status is succeeded


DeploymentName    : FailedRunsGreaterThan5
ResourceGroupName : adf
ProvisioningState : Succeeded
Timestamp         : 7/27/2015 7:52:56 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
Outputs           
```

Merhaba de kullanabilirsiniz **Ekle AlertRule** cmdlet toodeploy bir uyarı kuralı. Merhaba bkz [Ekle AlertRule](https://msdn.microsoft.com/library/mt282468.aspx) ayrıntı ve örnekler için konu.  

## <a name="move-a-data-factory-tooa-different-resource-group-or-subscription"></a>Bir veri fabrikası tooa farklı bir kaynak grubuna veya aboneliğe taşıma
Veri Fabrikası tooa farklı bir kaynak grubunda veya farklı bir abonelik hello kullanarak taşıyabilirsiniz **taşıma** hello giriş sayfasında veri fabrikanızın düğmesini çubuğu komutu.

![Veri Fabrikası taşıma](./media/data-factory-monitor-manage-pipelines/MoveDataFactory.png)

Bu gibi durumlarda, ilgili kaynakları (örneğin, hello data factory ile ilişkili olan uyarılar), ayrıca hello veri fabrikası birlikte taşıyabilirsiniz.

![Taşıma kaynaklar iletişim kutusu](./media/data-factory-monitor-manage-pipelines/MoveResources.png)
