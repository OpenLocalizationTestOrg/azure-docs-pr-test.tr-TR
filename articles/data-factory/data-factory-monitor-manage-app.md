---
title: "aaaMonitor ve veri ardışık - Azure yönetme | Microsoft Docs"
description: "Nasıl toouse izleme ve yönetim uygulaması toomonitor hello ve Azure data factory'leri ve ardışık düzen yönetmek öğrenin."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f3f07bc4-6dc3-4d4d-ac22-0be62189d578
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: spelluru
ms.openlocfilehash: 5e4ef6ec5fb8ebc9bda0be7899a39a51d58403d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-data-factory-pipelines-by-using-hello-monitoring-and-management-app"></a>İzleme ve hello izleme ve yönetim uygulaması kullanarak Azure Data Factory işlem hatlarını yönetme
> [!div class="op_single_selector"]
> * [Azure portal/Azure PowerShell kullanma](data-factory-monitor-manage-pipelines.md)
> * [Kullanılarak izleme ve yönetim uygulaması](data-factory-monitor-manage-app.md)
>
>

Bu makalede nasıl toouse izleme ve yönetim uygulaması toomonitor Merhaba, yönetmek ve Data Factory işlem hatlarınızı hata ayıklama açıklanmaktadır. Toocreate hatalarında bildirim tooget nasıl uyarıları bilgi de sağlar. Merhaba uygulaması tarafından izledikleri hello aşağıdaki video kullanmaya başlamak:

> [!NOTE]
> hello Portalı'nda bkz Hello video gösterilen hello kullanıcı arabirimi tam olarak eşleşmiyor olabilir. Biraz daha eski olduğu, ancak kavramları kalır hello aynı. 

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Azure-Data-Factory-Monitoring-and-Managing-Big-Data-Piplines/player]
>

## <a name="launch-hello-monitoring-and-management-app"></a>Merhaba izleme ve yönetim uygulamasını başlatın
toolaunch hello izleme ve yönetim uygulaması hello'ı tıklatın **İzleyici & Yönet** döşeme hello üzerinde **Data Factory** veri fabrikanızın dikey.

![Döşeme hello Data Factory giriş sayfasında izleme](./media/data-factory-monitor-manage-app/MonitoringAppTile.png)

Ayrı bir pencerede açmak hello izleme ve yönetim uygulaması görmeniz gerekir.  

![İzleme ve Yönetim uygulaması](./media/data-factory-monitor-manage-app/AppLaunched.png)

> [!NOTE]
> Bu hello web tarayıcısının "Yetkilendiriliyor..." takılmış görürseniz, hello temizleyin **üçüncü taraf tanımlama bilgilerini engelleyebilir ve site verileri** onay kutusu--veya seçili, Canlı oluşturmak için bir özel durum **login.microsoftonline.com** ve tooopen hello uygulama yeniden deneyin.


Merhaba etkinlik Windows hello Orta bölmesindeki listesinde, her bir etkinlik çalışması için bir etkinlik penceresine bakın. Örneğin, hello zamanlanan etkinlik toorun için beş saatten saatlik varsa, beş veri dilimi ile ilişkili beş etkinlik windows bakın. Etkinlik windows hello altındaki hello listesinde görmüyorsanız, aşağıdaki hello:
 
- Güncelleştirme hello **başlangıç zamanı** ve **bitiş saati** hello üst toomatch hello filtreler başlangıç ve bitiş zamanları, ardışık ve hello ardından **Uygula** düğmesi.  
- Merhaba etkinlik Windows listesi otomatik olarak yenilenmez. Merhaba tıklatın **yenileme** hello hello araç çubuğundan düğme **etkinlik Windows** listesi.  

Bu adımları bir Data Factory uygulama tootest yoksa, öğretici hello: [veritabanını Data Factory kullanarak Blob Storage tooSQL veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

## <a name="understand-hello-monitoring-and-management-app"></a>Merhaba izleme ve yönetim uygulaması anlama
Merhaba soldaki üç sekme vardır: **kaynak Gezgini**, **izleme görünümleri**, ve **uyarıları**. Merhaba ilk sekme (**kaynak Gezgini**) varsayılan olarak seçilidir.

### <a name="resource-explorer"></a>Kaynak Gezgini
Merhaba aşağıdakilere bakın:

* Merhaba kaynak Gezgini **ağaç görünümü** hello sol bölmede.
* Merhaba **diyagram görünümü** hello orta bölmesinde hello üstünde.
* Merhaba **etkinlik Windows** hello orta bölmesinde hello altındaki listesi.
* Merhaba **özellikleri**, **etkinlik penceresini Explorer**, ve **betik** hello sağ bölmedeki sekmeleri.

Kaynak Gezgini, ağaç görünümünde hello veri fabrikasında tüm kaynakları (komut zincirleri, veri kümeleri, bağlı hizmetler) bakın. Ne zaman kaynak Gezgini, bir nesne seçin:

* Merhaba Data Factory varlığı hello diyagram görünümü vurgulanan ilişkili.
* [Etkinlik pencerelerine ilişkili](data-factory-scheduling-and-execution.md) hello altındaki hello etkinlik Windows listesinde vurgulanır.  
* Merhaba hello seçili nesnenin özelliklerini hello Özellikler penceresinde hello sağ bölmede gösterilir.
* Merhaba hello seçili nesnenin JSON tanımını gösterilir, varsa. Örneğin: bağlı hizmet, bir veri kümesi veya işlem hattı.

![Kaynak Gezgini](./media/data-factory-monitor-manage-app/ResourceExplorer.png)

Merhaba bkz [zamanlama ve yürütme](data-factory-scheduling-and-execution.md) etkinlik windows hakkında ayrıntılı kavramsal bilgi için makalenin.

### <a name="diagram-view"></a>Diyagram Görünümü
Hello diyagram görünümü veri fabrikasının bölmeden cam toomonitor sağlar ve bir veri fabrikası ve varlıklarını yönetin. Ne zaman bir Data Factory varlığı (dataset/ardışık düzeni) hello diyagram görünümü seçin:

* Merhaba veri fabrikası varlık hello ağaç görünümünde seçilir.
* Merhaba, windows hello etkinlik Windows listesinde vurgulanan etkinlik ilişkili.
* Hello hello seçili nesnenin özelliklerini hello Özellikleri penceresinde görüntülenir.

Merhaba ardışık düzen (duraklatılmış durumda değil) etkin olduğunda, yeşil bir çizgiyle gösterilir:

![Çalışan işlem hattı](./media/data-factory-monitor-manage-app/PipelineRunning.png)

Duraklatma, sürdürme veya hello diyagram görünümünde seçerek ve hello komut çubuğunda hello düğmelerini kullanarak bir ardışık düzen sonlandırmak.

![Merhaba komut çubuğunda Duraklat/Sürdür](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)
 
Merhaba ardışık düzeninde hello diyagram görünümü için üç komut çubuğu düğmelerini vardır. Merhaba ikinci düğme toopause hello ardışık kullanabilirsiniz. Duraklatma etkinliklerini çalışmakta hello sonlandırmak değil ve bunları toocompletion devam olanak tanır. Merhaba üçüncü düğme hello ardışık düzen duraklatır ve kendi etkinlikleri yürütme varolan sona erer. Merhaba ilk düğme hello ardışık düzen sürdürür. İşlem hattınızı duraklatıldığında hello ardışık hello rengi değişir. Örneğin, duraklatılmış bir ardışık düzen görüntü aşağıdaki hello şuna benzer: 

![Ardışık Düzen duraklatıldı](./media/data-factory-monitor-manage-app/PipelinePaused.png)

Çoklu seçim iki veya daha fazla ardışık düzen hello Ctrl tuşunu kullanarak yapabilirsiniz. Aynı anda birden çok ardışık düzen hello komut çubuğu düğmelerini toopause/sürdürmeden kullanabilirsiniz.

Ayrıca sağ ardışık düzen ve seçenekleri belirleyin toosuspend sürdürün veya bir işlem hattı sonlandırılacak. 

![Ardışık düzeni için bağlam menüsü](./media/data-factory-monitor-manage-app/right-click-menu-for-pipeline.png)

Merhaba tıklatın **açık işlem hattı** hello ardışık düzende tüm hello etkinlik toosee seçeneği. 

![İşlem hattı menüsünü açma](./media/data-factory-monitor-manage-app/OpenPipelineMenu.png)

Açılan hello ardışık düzen Görünümü'nde hello ardışık düzende tüm etkinlik bakın. Bu örnekte, yalnızca bir etkinlik yok: kopyalama etkinliği. 

![Açılan ardışık düzen](./media/data-factory-monitor-manage-app/OpenedPipeline.png)

toogo toohello önceki görünüme geri hello veri fabrikası adı hello üstünde hello içerik haritası menüsünde'ı tıklatın.

Bir çıkış veri kümesi veya hello çıktı veri kümesi üzerinde farenizi taşıdığınızda seçtiğinizde hello ardışık düzen görünümünde bu veri kümesi için hello etkinlik Windows açılır pencere görürsünüz.

![Etkinlik Windows açılır penceresi](./media/data-factory-monitor-manage-app/ActivityWindowsPopup.png)

Hello bir etkinlik penceresini toosee ayrıntıları tıklattığınız **özellikleri** hello sağ bölmedeki penceresi.

![Etkinlik penceresini özellikleri](./media/data-factory-monitor-manage-app/ActivityWindowProperties.png)

Merhaba sağ bölmede, toohello geçiş **etkinlik penceresini Explorer** toosee Ayrıntılar sekmesi.

![Etkinlik penceresini Gezgini](./media/data-factory-monitor-manage-app/ActivityWindowExplorer.png)

Ayrıca bkz: **değişkenleri çözülmüş** hello bir etkinliğin her çalıştırma denemesi için **denemeleri** bölümü.

![Çözümlenen değişkenleri](./media/data-factory-monitor-manage-app/ResolvedVariables.PNG)

Geçiş toohello **betik** sekmesinde hello seçili nesne için toosee hello JSON betik tanımı.   

![Komut dosyası sekmesi](./media/data-factory-monitor-manage-app/ScriptTab.png)

Etkinlik pencerelerine üç yerde görebilirsiniz:

* Merhaba etkinlik Windows hello diyagram görünümü (Orta bölme) açılır.
* Etkinlik penceresini Explorer Hello hello sağ bölmedeki.
* Merhaba alt bölmesinde Hello etkinlik Windows listesi.

Hello etkinlik Windows açılır ve etkinlik penceresini Gezgini'nde, önceki hafta toohello kaydırın ve hello kullanarak sonraki hafta hello sol ve sağ ok.

![Etkinlik penceresini Explorer sol/sağ ok](./media/data-factory-monitor-manage-app/ActivityWindowExplorerLeftRightArrows.png)

Merhaba diyagram görünümü Hello kısımda bu düğmeleri Bkz: yakınlaştırma, uzaklaştırma, yakınlaştırma tooFit yakınlaştırma % 100, kilit düzeni. Merhaba **kilit düzeni** düğmesi önler yanlışlıkla tablolar ve ardışık düzen hello diyagram görünümü taşınmasını. Bu varsayılan olarak açıktır. Uygulamayı kapatın ve varlıkları hello diyagramında hareket ettirin. Devre dışı bıraktığınızda, hello Son düğmesine tooautomatically konumu tablolar ve ardışık düzen kullanabilirsiniz. Giriş veya çıkış hello fare tekerleği kullanarak da yakınlaştırabilirsiniz.

![Diyagram görünümü yakınlaştırma komutları](./media/data-factory-monitor-manage-app/DiagramViewZoomCommands.png)

### <a name="activity-windows-list"></a>Etkinlik Windows listesi
Merhaba etkinlik Windows hello orta bölmesinde hello altındaki tüm etkinlik windows hello kaynak Gezgini veya hello diyagram görünümü seçili hello veri kümesi için görüntüler. Varsayılan olarak, hello hello son etkinlik penceresini hello üstünde görmek anlamına gelir, azalan sırada listesidir.

![Etkinlik Windows listesi](./media/data-factory-monitor-manage-app/ActivityWindowsList.png)

Bu liste, kullanım hello Yenile düğmesini hello araç toomanually üzerinde yenilemek için otomatik olarak yenilenmez.  

Etkinlik windows hello durumları aşağıdaki biri olabilir:

<table>
<tr>
    <th align="left">Durum</th><th align="left">Alt durum</th><th align="left">Açıklama</th>
</tr>
<tr>
    <td rowspan="8">Bekleniyor</td><td>ScheduleTime</td><td>Başlangıç saati hello etkinlik penceresini toorun için gelen kurmadı.</td>
</tr>
<tr>
<td>DatasetDependencies</td><td>Merhaba Yukarı Akış bağımlılıkları hazır değil.</td>
</tr>
<tr>
<td>ComputeResources</td><td>Merhaba işlem kaynakları kullanılabilir değil.</td>
</tr>
<tr>
<td>ConcurrencyLimit</td> <td>Tüm hello etkinlik örnekleri diğer etkinlik windows çalıştıran meşgul.</td>
</tr>
<tr>
<td>ActivityResume</td><td>Merhaba etkinlik duraklatıldı ve sürdürülene kadar hello etkinlik windows çalıştıramaz.</td>
</tr>
<tr>
<td>Yeniden deneyin</td><td>Merhaba Etkinlik yürütme yeniden deneniyor.</td>
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
<td>Merhaba etkinlik penceresini işleniyor.</td>
</tr>
<tr>
<td rowspan="4">Başarısız oldu</td><td>Süresi sona erdi</td><td>Merhaba Etkinlik yürütme hello etkinliği tarafından izin daha uzun sürdü.</td>
</tr>
<tr>
<td>İptal edildi</td><td>Merhaba etkinlik penceresini kullanıcı eylemi tarafından iptal edildi.</td>
</tr>
<tr>
<td>Doğrulama</td><td>Doğrulama başarısız oldu.</td>
</tr>
<tr>
<td>-</td><td>Merhaba etkinlik penceresini oluşturulan veya doğrulanmamış toobe başarısız oldu.</td>
</tr>
<td>Hazır</td><td>-</td><td>Merhaba etkinlik penceresini tüketimi için hazırdır.</td>
</tr>
<tr>
<td>Atlandı</td><td>-</td><td>Merhaba etkinlik penceresini işlenen değildi.</td>
</tr>
<tr>
<td>None</td><td>-</td><td>Bir etkinlik penceresi tooexist farklı bir durum ile kullanılan ancak sıfırlandı.</td>
</tr>
</table>


Merhaba listesi etkinliği penceresindeki tıklattığınızda hello onunla ilgili ayrıntıları görürsünüz **etkinlik Windows Explorer** veya hello **özellikleri** penceresinde hello sağ.

![Etkinlik penceresini Gezgini](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-2.png)

### <a name="refresh-activity-windows"></a>Etkinlik pencerelerine Yenile
Merhaba ayrıntıları otomatik olarak yenilenir değil, bu nedenle toomanually yenileme hello etkinlik windows listesi çubuğu hello komutunda hello Yenile düğmesini (Merhaba ikinci düğme) kullanın.  

### <a name="properties-window"></a>Özellik penceresi
Merhaba Özellikleri penceresinde hello en sağ bölmesinde hello izleme ve yönetim uygulaması bulunur.

![Özellik penceresi](./media/data-factory-monitor-manage-app/PropertiesWindow.png)

Merhaba kaynak Gezgini (ağaç görünümü) seçili hello öğenin özelliklerini görüntüler diyagram görünümü veya etkinlik Windows listesi.

### <a name="activity-window-explorer"></a>Etkinlik penceresini Gezgini
Merhaba **etkinlik penceresini Explorer** ' hello izleme ve yönetim uygulaması hello en sağ bölmesinde bir penceredir. Merhaba etkinlik Windows açılır penceresi veya hello etkinlik Windows listedeki seçili hello etkinlik penceresini hakkındaki ayrıntıları görüntüler.

![Etkinlik penceresini Gezgini](./media/data-factory-monitor-manage-app/ActivityWindowExplorer-3.png)

Merhaba üstünde hello Takvim görünümünde tıklatarak tooanother faaliyet penceresi arasında geçiş yapabilirsiniz. Ayrıca, önceki hafta hello üst toosee etkinlik windows hello adresindeki hello sol ok/sağ ok düğmelerini kullanın veya sonraki hafta hello.

Merhaba alt bölmesinde toorerun hello etkinlik penceresinde hello araç çubuğu düğmelerini kullanın veya hello bölmesini hello ayrıntılarında yenileyin.

### <a name="script"></a>Betik
Merhaba kullanabilirsiniz **betik** sekmesini tooview hello hello JSON tanımını seçili Data Factory varlığı (bağlı hizmet, veri kümesi veya işlem hattı).

![Komut dosyası sekmesi](./media/data-factory-monitor-manage-app/ScriptTab.png)

## <a name="use-system-views"></a>Sistem görünümleri kullanma
Merhaba izleme ve yönetim uygulamasını içeren önceden derlenmiş sistem görünümleri (**son etkinlik windows**, **başarısız etkinliği windows**, **ilerleme durumu etkinlik windows**), Veri fabrikanızın tooview son/başarısız/Süren etkinlik pencerelerine izin verin.

Geçiş toohello **izleme görünümleri** tıklatarak hello sol sekmesinde.

![İzleme görünümleri sekmesi](./media/data-factory-monitor-manage-app/MonitoringViewsTab.png)

Şu anda desteklenen üç sistem görünümleri vardır. Bir seçenek toosee seçin son etkinlik windows, başarısız olan etkinliği windows veya devam eden etkinlik windows hello etkinlik Windows listesinde (sonundaki hello hello orta bölmesinde).

Merhaba seçtiğinizde **son etkinlik windows** seçeneği, gördüğünüz hello azalan tüm son etkinlik windows **zaman'son deneme**.

Merhaba kullanabilirsiniz **başarısız etkinliği windows** toosee tüm başarısız etkinliği windows hello listesinde görüntülemek. Itanium tabanlı sistemler için hello listesi toosee ayrıntıları ilgili hello içinde başarısız olan etkinliği penceresi seçin **özellikleri** penceresi veya hello **etkinlik penceresini Explorer**. Ayrıca, başarısız olan etkinliği penceresi için herhangi bir günlük indirebilirsiniz.

## <a name="sort-and-filter-activity-windows"></a>Sıralama ve filtreleme etkinliği windows
Değişiklik hello **başlangıç zamanı** ve **bitiş saati** hello komut çubuğu toofilter etkinlik pencereleri ayarlarında. Hello başlangıç ve bitiş zamanı değiştirdikten sonra hello düğmesi sonraki toohello bitiş saati toorefresh hello etkinlik Windows listesi tıklayın.

![Başlangıç ve bitiş zamanlarını](./media/data-factory-monitor-manage-app/StartAndEndTimes.png)

> [!NOTE]
> Şu anda tüm saatler UTC biçiminde hello izleme ve yönetim uygulaması arasındadır.
>
>

Merhaba, **etkinlik Windows listesi**, bir sütun hello adına tıklayın (örneğin: durum).

![Etkinlik Windows liste sütun menüsü](./media/data-factory-monitor-manage-app/ActivityWindowsListColumnMenu.png)

Yapabileceğiniz hello aşağıdaki:

* Artan sırada Sırala.
* Azalan sırada sıralayın.
* Bir veya daha fazla değerlerle (hazır, bekliyor vb.) filtreleyin.

Bir sütunda bir filtre belirttiğinizde, filtrelenmiş değerleri hello sütundaki hello değerleri gösterir bu sütun için etkin hello filtre düğmesini bakın.

![Merhaba etkinlik Windows listesinin bir sütuna filtre](./media/data-factory-monitor-manage-app/ActivityWindowsListFilterInColumn.png)

Kullanabileceğiniz hello aynı açılır pencere tooclear filtreler. tüm filtreleri hello etkinlik Windows listesi için tooclear hello komut çubuğunda hello filtreyi düğmesini tıklatın.

![Merhaba etkinlik Windows listesi için tüm filtreleri temizlemek](./media/data-factory-monitor-manage-app/ClearAllFiltersActivityWindowsList.png)

## <a name="perform-batch-actions"></a>Toplu işlemleri
### <a name="rerun-selected-activity-windows"></a>Seçili etkinlik windows yeniden çalıştırın
Bir etkinlik penceresi seçin, aşağı ok hello ilk komut çubuğu düğmesi için hello tıklatın ve seçin **yeniden Çalıştır** / **ile upstream ardışık düzeninde yeniden**. Merhaba seçtiğinizde **ile upstream ardışık düzeninde yeniden** seçeneği, tüm Yukarı Akış etkinliği windows de yeniden çalıştırır.
    ![Bir etkinlik penceresi yeniden](./media/data-factory-monitor-manage-app/ReRunSlice.png)

Ayrıca birden çok etkinlik windows hello listesinden seçin ve hello yeniden aynı anda. Toofilter etkinlik windows hello durumlarına dayalı isteyebilirsiniz (örneğin: **başarısız**)--ve başarısız hello etkinlik windows hello etkinlik windows toofail neden hello sorunu düzelttikten sonra yeniden çalıştırın. Merhaba bölümden etkinlik windows hello listesinde filtreleme hakkında ayrıntılar için bkz.  

### <a name="pauseresume-multiple-pipelines"></a>Birden çok ardışık düzen Duraklat/Sürdür
Çoklu iki veya daha fazla ardışık düzen hello Ctrl tuşunu kullanarak yapabilirsiniz. (Hangi görüntü aşağıdaki hello hello kırmızı dikdörtgende içinde vurgulanır) hello komut çubuğu düğmelerini kullanabilirsiniz toopause/sürdürmeden bunları.

![Merhaba komut çubuğunda Duraklat/Sürdür](./media/data-factory-monitor-manage-app/SuspendResumeOnCommandBar.png)

## <a name="create-alerts"></a>Uyarı oluşturma
Merhaba **uyarıları** sayfası, bir uyarı ve görünüm/düzenleme/silme mevcut uyarıları oluşturmanıza olanak sağlar. Sizin de devre dışı bırak/uyarı etkinleştirebilirsiniz. toosee uyarılar sayfasında Merhaba, hello tıklatın **uyarıları** sekmesi.

![Uyarılar sekmesi](./media/data-factory-monitor-manage-app/AlertsTab.png)

### <a name="toocreate-an-alert"></a>toocreate bir uyarı
1. Tıklatın **eklemek uyarı** tooadd bir uyarı. Merhaba gördüğünüz **ayrıntıları** sayfası.

    ![Uyarılar - ayrıntılar sayfası oluşturma](./media/data-factory-monitor-manage-app/CreateAlertDetailsPage.png)
2. Merhaba belirtin **adı** ve **açıklama** tıklatın ve hello uyarı için **sonraki**. Merhaba görmelisiniz **filtreleri** sayfası.

    ![Uyarılar - filtreleri sayfa oluşturma](./media/data-factory-monitor-manage-app/CreateAlertFiltersPage.png)
3. Select hello **olay**, **durum**, ve **substatus** (isteğe bağlı) toocreate istediğiniz bir Data Factory hizmeti için uyarı öğesini tıklatıp **sonraki**. Merhaba görmelisiniz **alıcılar** sayfası.

    ![Uyarılar - alıcılar sayfa oluşturma](./media/data-factory-monitor-manage-app/CreateAlertRecipientsPage.png)
4. Select hello **abonelik yöneticileri e-posta** seçeneği ve/veya girin bir **ek yönetici e-posta**, tıklatıp **son**. Merhaba uyarı hello listesinde görmeniz gerekir.

    ![Uyarılar listesinde](./media/data-factory-monitor-manage-app/AlertsList.png)

Merhaba Uyarılar listesinde hello uyarı tooedit/silme/devre dışı bırak/etkinleştir ile bir uyarı ilişkili hello düğmelerini kullanın.

### <a name="eventstatussubstatus"></a>Alt olay/durumu/durum
Merhaba aşağıdaki tabloda kullanılabilir olayları ve durumları (ve alt durumlar) hello listesini sağlar.

| Olay adı | Durum | Alt durum |
| --- | --- | --- |
| Başlatılan Çalıştır etkinliği |başlatıldı |Başlangıç |
| Tamamlanan etkinlik |Başarılı oldu |Başarılı oldu |
| Tamamlanan etkinlik |Başarısız oldu |Başarısız olan kaynak ayırma<br/><br/>Başarısız yürütme<br/><br/>Zaman aşımına uğradı<br/><br/>Başarısız doğrulamayı<br/><br/>terk |
| İsteğe bağlı HDI kümesi oluşturma başlatıldı |başlatıldı |-|
| İsteğe bağlı HDI kümesi başarıyla oluşturuldu |Başarılı oldu |-|
| İsteğe bağlı HDI kümesi silindi |Başarılı oldu |-|

### <a name="tooedit-delete-or-disable-an-alert"></a>tooedit, silmek veya uyarıyı devre dışı bırak

(Kırmızı ile vurgulanan) düğmeleri tooedit, silmek veya devre dışı bir uyarı aşağıdaki hello kullanın.

![Uyarıları düğmeleri](./media/data-factory-monitor-manage-app/AlertButtons.png)
