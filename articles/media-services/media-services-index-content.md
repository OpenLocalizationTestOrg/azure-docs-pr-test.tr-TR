---
title: "Azure Media Indexer ortam dosyalarıyla aaaIndexing"
description: "Azure Media Indexer medya dosyalarınızı aranabilir toomake içeriği ve toogenerate tam metin dökümü kapalı açıklamalı alt yazı ve anahtar sözcükler için sağlar. Bu konuda gösterilmektedir nasıl toouse medya dizin oluşturucu."
services: media-services
documentationcenter: 
author: Asolanki
manager: cfowler
editor: 
ms.assetid: 827a56b2-58a5-4044-8d5c-3e5356488271
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/20/2017
ms.author: adsolank;juliako;johndeu
ms.openlocfilehash: c1bed774e302e61ca3510668645dc2015b434a0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-media-files-with-azure-media-indexer"></a>Azure Media Indexer ortam dosyalarıyla dizin oluşturma
Azure Media Indexer medya dosyalarınızı aranabilir toomake içeriği ve toogenerate tam metin dökümü kapalı açıklamalı alt yazı ve anahtar sözcükler için sağlar. Tek bir medya dosyasını işleyebileceğiniz gibi, birden çok medya dosyasını toplu olarak da işleyebilirsiniz.  

> [!IMPORTANT]
> İçerik dizin oluştururken emin toouse açıkça konuşma (olmadan, arka plan müzik, parazit, efektleri veya mikrofon hiss) sahip medya dosyalarını olun. Uygun içeriğin bazı örnekleri şunlardır: kaydedilen toplantılar, dersleri veya sunuları. Merhaba aşağıdaki içerik dizin oluşturma işlemi için uygun olmayabilir: filmler, TV programları karma ses ve ses efekti ile herhangi bir şey kötü içeriği arka plan gürültü (hiss) ile kaydedilmiş.
> 
> 

Bir dizin oluşturma işi çıkışları aşağıdaki hello oluşturabilirsiniz:

* Kapalı açıklamalı alt yazı dosyaları biçimleri aşağıdaki hello: **SAMI**, **TTML**, ve **WebVTT**.
  
    Kapalı açıklamalı alt yazı dosyaları bir dizin oluşturma işi hello kaynak videoda nasıl tanınabilir hello konuşma hangi puanları olan Recognizability adlı bir etiket içerir.  Kullanılabilirlik için Recognizability tooscreen çıktı dosyaları hello değerini kullanabilirsiniz. Düşük bir puan tooaudio kalite nedeniyle kötü dizin sonuçlar anlamına gelir.
* Anahtar dosyası (XML).
* Ses BLOB dosya (AIB) SQL server ile kullanmak için dizin oluşturma.
  
    Daha fazla bilgi için bkz: [kullanarak AIB dosyaları Azure Media Indexer ve SQL Server ile](https://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/).

Bu konu, nasıl toocreate dizin çok işleri gösterir**bir varlık dizin** ve **birden çok dosya dizin**.

Merhaba en son Azure Media Indexer güncelleştirmeler için bkz: [Media Services bloglar](#preset).

## <a name="using-configuration-and-manifest-files-for-indexing-tasks"></a>Dizin oluşturma görevlerini yapılandırması ve bildirim dosyalarını kullanma
Görev yapılandırmayı kullanarak, daha fazla ayrıntı için dizin oluşturma görevleri belirtebilirsiniz. Örneğin, ortam dosyası için hangi meta veri toouse belirtebilirsiniz. Bu meta veriler, sözlük hello dil altyapısı tooexpand tarafından kullanılan ve hello konuşma tanıma doğruluğunu önemli ölçüde artırır.  Sizin de mümkün toospecify, istenen çıkış dosyalarıdır.

Bildirim dosyası kullanarak birden çok medya dosyaları aynı anda aynı zamanda işleyebilir.

Daha fazla bilgi için bkz: [görev Önayar Azure Media Indexer için](https://msdn.microsoft.com/library/dn783454.aspx).

## <a name="index-an-asset"></a>Bir varlık dizin
Merhaba aşağıdaki yöntemi bir medya dosyası bir varlık olarak yükler ve iş tooindex hello varlığı oluşturur.

Merhaba medya dosyası herhangi bir yapılandırma dosyası belirtilmişse, tüm varsayılan ayarlarla dizine olduğunu unutmayın.

    static bool RunIndexingJob(string inputMediaFilePath, string outputFolder, string configurationFile = "")
    {
        // Create an asset and upload hello input media file toostorage.
        IAsset asset = CreateAssetAndUploadSingleFile(inputMediaFilePath,
            "My Indexing Input Asset",
            AssetCreationOptions.None);

        // Declare a new job.
        IJob job = _context.Jobs.Create("My Indexing Job");

        // Get a reference toohello Azure Media Indexer.
        string MediaProcessorName = "Azure Media Indexer";
        IMediaProcessor processor = GetLatestMediaProcessorByName(MediaProcessorName);

        // Read configuration from file if specified.
        string configuration = string.IsNullOrEmpty(configurationFile) ? "" : File.ReadAllText(configurationFile);

        // Create a task with hello encoding details, using a string preset.
        ITask task = job.Tasks.AddNew("My Indexing Task",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input asset toobe indexed.
        task.InputAssets.Add(asset);

        // Add an output asset toocontain hello results of hello job.
        task.OutputAssets.AddNew("My Indexing Output Asset", AssetCreationOptions.None);

        // Use hello following event handler toocheck job progress.  
        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

        // Launch hello job.
        job.Submit();

        // Check job execution and wait for job toofinish.
        Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
        progressJobTask.Wait();

        // If job state is Error, hello event handling
        // method for job progress should log errors.  Here we check
        // for error state and exit if needed.
        if (job.State == JobState.Error)
        {
            Console.WriteLine("Exiting method due toojob error.");
            return false;
        }

        // Download hello job outputs.
        DownloadAsset(task.OutputAssets.First(), outputFolder);

        return true;
    }

    static IAsset CreateAssetAndUploadSingleFile(string filePath, string assetName, AssetCreationOptions options)
    {
        IAsset asset = _context.Assets.Create(assetName, options);

        var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
        assetFile.Upload(filePath);

        return asset;
    }

    static void DownloadAsset(IAsset asset, string outputDirectory)
    {
        foreach (IAssetFile file in asset.AssetFiles)
        {
            file.Download(Path.Combine(outputDirectory, file.Name));
        }
    }

    static IMediaProcessor GetLatestMediaProcessorByName(string mediaProcessorName)
    {
        var processor = _context.MediaProcessors
        .Where(p => p.Name == mediaProcessorName)
        .ToList()
        .OrderBy(p => new Version(p.Version))
        .LastOrDefault();

        if (processor == null)
            throw new ArgumentException(string.Format("Unknown media processor",
                                                       mediaProcessorName));

        return processor;
    }  
<!-- __ -->
### <a id="output_files"></a>Çıkış dosyaları
Varsayılan olarak, aşağıdaki çıktı dosyaları hello bir dizin oluşturma işi oluşturur. Merhaba dosyaları hello ilk çıkış varlığı depolanır.

Birden fazla giriş medya dosyası olduğunda, dizin oluşturucu hello işi çıkış, 'JobResult.txt' adlı bildirim dosyası oluşturur. Her giriş medya dosyası için hello elde edilen AIB, SAMI, TTML, WebVTT ve anahtar sözcüğü dosyaları, sıralı olarak numaralandırılmış ve adlandırılmış hello "Diğer" kullanma.

| Dosya adı | Açıklama |
| --- | --- |
| **InputFileName.aib** |Ses dizin blob dosyası. <br/><br/> Ses dizin Blob (AIB) dosyası Microsoft SQL server tam metin araması kullanılarak aranabilecek bir ikili dosyadır.  çok daha zengin bir arama deneyimi sağlayan her sözcüğün alternatifleri içerdiğinden hello AIB hello basit açıklamalı alt yazı dosyaları, daha güçlü dosyasıdır. <br/> <br/>Makine çalışan Microsoft SQL server 2008 veya sonraki sürümünü hello dizin oluşturucu SQL eklentiye hello yüklenmesini gerektirir. Microsoft SQL kullanarak AIB Hello arama server tam metin araması hello arama kapalı açıklamalı alt yazı dosyaları WAMI tarafından oluşturulan çok daha doğru arama sonuçları sağlar. Merhaba AIB hello kapalı açıklamalı alt yazı dosyaları ancak benzer hangi ses içeren hello ses her parçası için en yüksek güvenilirlik word hello word alternatifleri içermesidir. Konuşma sözcükler aranıyor upmost önemini ise, toouse hello AIB içinde ile birlikte Microsoft SQL Server önerilir.<br/><br/> toodownload eklenti Merhaba, tıklatın <a href="http://aka.ms/indexersql">Azure Media Indexer SQL eklenti</a>. <br/><br/>Bu Apache Lucene/Solr toosimply dizin hello video hello kapalı başlık ve anahtar sözcüğü XML dosyaları esasında da olası tooutilize diğer arama motorları, ancak bu daha az doğru arama sonuçlarında neden olur. |
| **InputFileName.smi**<br/>**InputFileName.ttml**<br/>**InputFileName.vtt** |SAMI, TTML ve WebVTT biçimleri kapalı açıklamalı alt yazı (CC) dosyalar.<br/><br/>Kullanılan toomake ses olabilir ve erişilebilir toopeople işitme engelli ile video dosyaları.<br/><br/>Kapalı açıklamalı alt yazı dosyaları dahil etme adlı bir etiket <b>Recognizability</b> hangi hello kaynak videoda nasıl tanınabilir hello konuşma dayalı bir dizin oluşturma işi puanlar olduğu.  Merhaba değerini kullanabilirsiniz <b>Recognizability</b> tooscreen çıkış dosyaları için kullanılabilirlik. Düşük bir puan tooaudio kalite nedeniyle kötü dizin sonuçlar anlamına gelir. |
| **InputFileName.kw.xml<br/>InputFileName.info** |Anahtar sözcüğü ve bilgi dosyaları. <br/><br/>Anahtar sözcük dosyasını sıklığı ve uzaklık bilgileri hello konuşma içerikten ayıklanan anahtar sözcükler içeren bir XML dosyasıdır. <br/><br/>Bilgi dosyası tanınan her terim hakkında ayrıntılı bilgi içeren bir düz metin dosyasıdır. Merhaba ilk satırı özeldir ve hello Recognizability puan içerir. Sonraki her satırı veri aşağıdaki hello sekmeyle ayrılmış bir listesi verilmiştir: başlangıç zamanı, bitiş zamanı, sözcük/tümcecik, güven. saniye cinsinden Hello kez verilir ve hello güvenirlik 0-1'den bir sayı olarak verilir. <br/><br/>Örnek satırı: "1.20 1.45 word 0.67" <br/><br/>Gösterilen toosearch Bing, Google veya Microsoft SharePoint toomake hello medya dosyalarını daha bulunabilir veya hatta kullanılan toodeliver gibi daha ilgili ads altyapıları veya bu dosyaları birkaç tooperform konuşma çözümlemeleri gibi amaçlar için kullanılabilir. |
| **JobResult.txt** |Çıktı bildirimi, yalnızca aşağıdaki bilgilerle hello içeren birden çok dosya dizin oluştururken mevcut:<br/><br/><table border="1"><tr><th>InputFile</th><th>Diğer ad</th><th>MediaLength</th><th>Hata</th></tr><tr><td>a.mp4</td><td>Media_1</td><td>300</td><td>0</td></tr><tr><td>b.mp4</td><td>Media_2</td><td>0</td><td>3000</td></tr><tr><td>c.mp4</td><td>Media_3</td><td>600</td><td>0</td></tr></table><br/> |

Aksi takdirde tüm giriş medya dosyalarınızın başarılı bir şekilde dizine, hello dizin oluşturma işi 4000 hata koduyla başarısız olur. Daha fazla bilgi için bkz: [hata kodları](#error_codes).

## <a name="index-multiple-files"></a>Birden çok dosya dizin
yöntemini aşağıdaki hello bir varlık birden çok medya dosyalarını yükler ve iş tooindex bir toplu işlemde bu dosyaları oluşturur.

Merhaba .lst uzantısına sahip bir bildirim dosyası oluşturulur ve hello varlık içine karşıya yükleniyor. Merhaba bildirim dosyası tüm hello varlık dosyaları hello listesini içerir. Daha fazla bilgi için bkz: [görev Önayar Azure Media Indexer için](https://msdn.microsoft.com/library/dn783454.aspx).

    static bool RunBatchIndexingJob(string[] inputMediaFiles, string outputFolder)
    {
        // Create an asset and upload toostorage.
        IAsset asset = CreateAssetAndUploadMultipleFiles(inputMediaFiles,
            "My Indexing Input Asset - Batch Mode",
            AssetCreationOptions.None);

        // Create a manifest file that contains all hello asset file names and upload toostorage.
        string manifestFile = "input.lst";            
        File.WriteAllLines(manifestFile, asset.AssetFiles.Select(f => f.Name).ToArray());
        var assetFile = asset.AssetFiles.Create(Path.GetFileName(manifestFile));
        assetFile.Upload(manifestFile);

        // Declare a new job.
        IJob job = _context.Jobs.Create("My Indexing Job - Batch Mode");

        // Get a reference toohello Azure Media Indexer.
        string MediaProcessorName = "Azure Media Indexer";
        IMediaProcessor processor = GetLatestMediaProcessorByName(MediaProcessorName);

        // Read configuration.
        string configuration = File.ReadAllText("batch.config");

        // Create a task with hello encoding details, using a string preset.
        ITask task = job.Tasks.AddNew("My Indexing Task - Batch Mode",
            processor,
            configuration,
            TaskOptions.None);

        // Specify hello input asset toobe indexed.
        task.InputAssets.Add(asset);

        // Add an output asset toocontain hello results of hello job.
        task.OutputAssets.AddNew("My Indexing Output Asset - Batch Mode", AssetCreationOptions.None);

        // Use hello following event handler toocheck job progress.  
        job.StateChanged += new EventHandler<JobStateChangedEventArgs>(StateChanged);

        // Launch hello job.
        job.Submit();

        // Check job execution and wait for job toofinish.
        Task progressJobTask = job.GetExecutionProgressTask(CancellationToken.None);
        progressJobTask.Wait();

        // If job state is Error, hello event handling
        // method for job progress should log errors.  Here we check
        // for error state and exit if needed.
        if (job.State == JobState.Error)
        {
            Console.WriteLine("Exiting method due toojob error.");
            return false;
        }

        // Download hello job outputs.
        DownloadAsset(task.OutputAssets.First(), outputFolder);

        return true;
    }

    private static IAsset CreateAssetAndUploadMultipleFiles(string[] filePaths, string assetName, AssetCreationOptions options)
    {
        IAsset asset = _context.Assets.Create(assetName, options);

        foreach (string filePath in filePaths)
        {
            var assetFile = asset.AssetFiles.Create(Path.GetFileName(filePath));
            assetFile.Upload(filePath);
        }

        return asset;
    }

### <a name="partially-succeeded-job"></a>Kısmen başarılı oldu işi
Aksi takdirde tüm giriş medya dosyalarınızın başarılı bir şekilde dizine, hello dizin oluşturma işi 4000 hata koduyla başarısız olur. Daha fazla bilgi için bkz: [hata kodları](#error_codes).

Merhaba aynı çıkışları (olarak başarılı iş) oluşturulur. Hata sütun değerlerini toohello göre hangi girdi dosyalarını başarısız olan, toohello çıkış bildirim dosyası toofind başvurabilir. Merhaba elde edilen AIB, SAMI, TTML, WebVTT ve başarısız giriş dosyaları için anahtar sözcüğü dosyaları oluşturulmayacak.

### <a id="preset"></a>Azure Media Indexer için görev Önayar
Azure Media Indexer işleme hello hello görev yanı sıra önceden belirlenmiş bir isteğe bağlı görev sağlayarak özelleştirilebilir.  Merhaba bu yapılandırma xml hello biçimi açıklanmıştır.

| Ad | Gerektirme | Açıklama |
| --- | --- | --- |
| **Giriş** |False |Varlık dosyaları tooindex istiyor.</p><p>Azure Media Indexer ortam dosya biçimleri aşağıdaki hello destekler: MP4, WMV, MP3, M4A, WMA, AAC, WAV.</p><p>Merhaba dosya adı (s) hello belirtebilirsiniz **adı** veya **listesi** hello özniteliği **giriş** (aşağıda gösterildiği gibi) öğesi. Hangi varlık dosyası tooindex belirtmezseniz hello birincil dosya çekilir. Herhangi bir birincil varlık dosyası ayarlarsanız hello ilk hello giriş varlık dosyasında dizine alınır.</p><p>tooexplicitly hello varlık dosya adı belirtin, yapın:<br/>`<input name="TestFile.wmv">`<br/><br/>Ayrıca, birden çok varlık dosyaları aynı anda (too10 dosyaları) dizin oluşturabilirsiniz. toodo bu:<br/><br/><ol class="ordered"><li><p>Bir metin dosyası (bildirim dosyası) oluşturun ve bir .lst uzantısı verin. </p></li><li><p>Tüm hello varlık dosya adlarının bir listesini giriş varlık toothis bildirim dosyanıza ekleyin. </p></li><li><p>(Karşıya yükleme) thanifest dosya toohello varlık ekleyin.  </p></li><li><p>Merhaba bildirim dosyası Hello adını hello giriş'ın liste özniteliğinde belirtin.<br/>`<input list="input.lst">`</li></ol><br/><br/>Not: 10'dan fazla dosyaları toohello bildirim dosyası eklerseniz, iş dizin hello hello 2006 hata kodu ile başarısız olur. |
| **Meta veriler** |False |Hello için meta veri sözlüğünü uyarlama için kullanılan varlık dosyaları belirtilen.  Yararlı tooprepare dizin oluşturucu toorecognize standart sözlük sözcükler uygun isimleri gibi.<br/>`<metadata key="..." value="..."/>` <br/><br/>Size sağlayabilir **değerleri** önceden tanımlanmış **anahtarları**. Şu anda anahtarları aşağıdaki hello desteklenir:<br/><br/>"title" ve "Açıklama" sözlük uyarlama tootweak hello dili için kullanılan - işiniz için model ve konuşma tanıma doğruluğunu artırmak.  Merhaba değerleri dizin göreviniz hello süresince hello içeriği tooaugment hello iç sözlüğünü kullanarak Internet aramaları toofind bağlam ilgili metin belgeleri, çekirdek değer.<br/>`<metadata key="title" value="[Title of hello media file]" />`<br/>`<metadata key="description" value="[Description of hello media file] />"` |
| **özellikleri** <br/><br/> Sürüm 1.2 eklendi. Şu anda, konuşma tanıma ("ASR") yalnızca desteklenen hello özelliğidir. |False |Merhaba konuşma tanıma özelliği hello ayarları anahtarları aşağıdaki sahiptir:<table><tr><th><p>Anahtar</p></th>        <th><p>Açıklama</p></th><th><p>Örnek değer</p></th></tr><tr><td><p>Dil</p></td><td><p>Merhaba doğal dil toobe Hello multimedya dosyasında tanınmıyor.</p></td><td><p>İngilizce, İspanyolca</p></td></tr><tr><td><p>CaptionFormats</p></td><td><p>noktalı virgülle ayrılmış listesini hello istenen çıkış resim yazısı biçimleri (varsa)</p></td><td><p>ttml; sami webvtt</p></td></tr><tr><td><p>GenerateAIB</p></td><td><p>Bir AIB dosyası (kullanmak için SQL Server ve hello müşteri dizin oluşturucu IFilter ile) gerekli olup olmadığını belirten bir Boole bayrağı.  Daha fazla bilgi için bkz: <a href="http://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/">kullanarak AIB dosyaları Azure Media Indexer ve SQL Server ile</a>.</p></td><td><p>TRUE; False</p></td></tr><tr><td><p>GenerateKeywords</p></td><td><p>Bir anahtar sözcük XML dosyasını gerekli olup olmadığını belirten bir Boole bayrağı.</p></td><td><p>TRUE; FALSE. </p></td></tr><tr><td><p>ForceFullCaption</p></td><td><p>Tam tooforce (anlamlılık düzeyi bağımsız olarak) başlıkları olup olmadığını belirten bir Boole bayrağı.  </p><p>Varsayılan durumda sözcükler % 50 anlamlılık düzeyi'den az olan tümcecikleri hello son resim yazısı çıkışlarından atlanmış ve üç nokta tarafından değiştirildi ("...") false değeridir.  Merhaba elipsler resim yazısı kalite denetimi ve denetim için faydalıdır.</p></td><td><p>TRUE; FALSE. </p></td></tr></table> |

### <a id="error_codes"></a>Hata kodları
Bir hata Hello durumda Azure Media Indexer bildirmelisiniz hata kodları aşağıdaki hello birini yedekleyin:

| Kod | Ad | Olası nedenler |
| --- | --- | --- |
| 2000 |Geçersiz yapılandırma |Geçersiz yapılandırma |
| 2001 |Geçersiz giriş varlıklar |Giriş varlıklar veya boş varlık eksik. |
| 2002 |Geçersiz bildirim |Bildirim boş veya geçersiz öğeleri bildirimi içerir. |
| 2003 |Başarısız toodownload medya dosyası |Bildirim dosyasında geçersiz URL. |
| 2004 |Desteklenmeyen protokol |Medya URL'nin protokolü desteklenmiyor. |
| 2005 |Desteklenmeyen dosya türü |Giriş medya dosya türü desteklenmiyor. |
| 2006 |Çok fazla giriş dosyaları |Merhaba giriş bildiriminde 10'dan fazla dosyası yok. |
| 3000 |Başarısız toodecode medya dosyası |Desteklenmeyen medya codec <br/>or<br/> Bozuk medya dosyası <br/>or<br/> Giriş medya ses akış yok. |
| 4000 |Toplu dizin oluşturma kısmen başarılı oldu |Bazı dosyalar hello giriş medya dizine toobe başarısız oldu. Daha fazla bilgi için bkz: <a href="#output_files">çıkış dosyaları</a>. |
| diğer |İç hata |Lütfen destek ekibi ile iletişime geçin. indexer@microsoft.com |

## <a id="supported_languages"></a>Desteklenen diller
Şu anda hello İngilizce ve İspanyolca dil desteklenir. Daha fazla bilgi için bkz: [hello 1.2 sürümü yayın blog gönderisi](https://azure.microsoft.com/blog/2015/04/13/azure-media-indexer-spanish-v1-2/).

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>İlgili bağlantılar
[Azure Media Services Analytics a genel bakış](media-services-analytics-overview.md)

[Azure Media Indexer ve SQL Server ile AIB dosyalarını kullanma](https://azure.microsoft.com/blog/2014/11/03/using-aib-files-with-azure-media-indexer-and-sql-server/)

[Azure Media Indexer 2 Önizleme ile medya dosyalarını dizin oluşturma](media-services-process-content-with-indexer2.md)

