---
title: "Visual Studio Proje şablonları - Azure ile toplu çözümler derleme aaaStart | Microsoft Docs"
description: "Visual Studio Proje şablonları uygulamak ve Azure Batch işlem yoğunluklu iş yüklerini çalıştırmak nasıl yardımcı olabileceğini öğrenin."
services: batch
documentationcenter: .net
author: fayora
manager: timlt
editor: 
ms.assetid: 5e041ae2-25af-4882-a79e-3aa63c4bfb20
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a61c480ddc4dffd66c01220a137a3e852e39c338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-project-templates-toojump-start-batch-solutions"></a>Visual Studio Proje şablonları toojump başlangıç Batch çözümleri kullanın

Merhaba **İş Yöneticisi** ve **görev işlemci Visual Studio şablonları** toplu işlemi için kod toohelp sağlamak, tooimplement ve işlem yoğunluklu iş yüklerinizin batch ile Merhaba az Çalıştır çaba. Bu belge bu şablonları açıklar ve nasıl yönelik yönergeler sağlanmaktadır toouse bunları.

> [!IMPORTANT]
> Bu makalede, yalnızca bilgi geçerli toothese iki şablonları açıklanır ve hello Batch hizmeti ve ilgili tooit temel kavramları hakkında bilgi sahibi olduğunuzu varsayar: havuzlar, işlem düğümleri, işler ve görevler, iş yöneticisi görevleri, ortam değişkenleri ve diğer ilgili bilgiler. Daha fazla bilgi bulabilirsiniz [Azure Batch temel bilgileri](batch-technical-overview.md), [geliştiriciler için Batch özelliklerine genel bakış](batch-api-basics.md), ve [.NET için hello Azure Batch kitaplığını kullanmaya başlama](batch-dotnet-get-started.md).
> 
> 

## <a name="high-level-overview"></a>Yüksek düzey genel bakış
Merhaba İş Yöneticisi ve görev işlemci şablonları kullanılan toocreate iki yararlı bileşenleri olabilir:

* Bir işi bağımsız olarak, paralel olarak çalıştırılabilir birden çok görev içine ayırabilirsiniz iş Bölümlendirici uygulayan bir iş yöneticisi görevi.
* Kullanılan tooperform ön işleme ve sonrası işleme uygulama komut satırı geçici olabilir görev işlemci.

Örneğin, bir filmi işleme senaryosunda, hello iş Bölümlendirici tek film iş yüzlerce veya binlerce tek tek çerçeveler ayrı ayrı işlemek ayrı görevlerin kapatmanız. Buna bağlı olarak, hello görev işlemci uygulama gerekli toorender olan ve tüm bağımlı işlemleri her çerçeve işleme hello çağırma yanı (örneğin, kopyalama çizilir hello çerçeve tooa depolama konumu) ek eylemleri gerçekleştirin.

> [!NOTE]
> toouse her ikisini birden veya hello gereksinimleri işlem işinizin ve tercihlerinize bağlı olarak bunlardan yalnızca birini seçebilmeniz hello İş Yöneticisi ve görev işlemci şablonları birbirinden bağımsızdır.
> 
> 

Merhaba çizimde gösterildiği gibi bu şablonları kullanan bir işlem iş üç aşamanın gidin:

1. bir iş toohello Batch hizmeti, iş yöneticisi görevi hello İş Yöneticisi programı olarak belirterek azure'da Hello istemci kodu (örneğin, uygulama, web hizmeti, vb.) gönderir.
2. Merhaba Batch hizmeti bir işlem düğümünde hello iş yöneticisi görevi çalıştırır ve birçok gerektiği gibi hello parametreleri ve hello proje Bölümlendirici kodu teknik özelliklerine göre işlem düğümleri gibi hello iş Bölümlendirici başlatır hello görev işlemci görev sayısı belirtilen.
3. Hello görev işlemci görevler bağımsız olarak, paralel olarak tooprocess hello giriş verisi çalıştırın ve hello çıktı verilerini oluşturur.

![İstemci kodu hello Batch hizmeti ile nasıl etkileşim kurduğunu gösteren diyagram][diagram01]

## <a name="prerequisites"></a>Ön koşullar
toouse hello toplu şablonları hello aşağıdaki gerekir:

* Visual Studio 2015 yüklü bir bilgisayar. Toplu işlem şablonları, şu anda yalnızca Visual Studio 2015 için desteklenir.
* hello kullanılabilir hello toplu şablonları [Visual Studio Galerisi] [ vs_gallery] Visual Studio uzantıları olarak. Tooget hello şablonları iki yolu vardır:
  
  * Hello kullanarak hello şablonları yüklemek **Uzantılar ve güncelleştirmeler** Visual Studio iletişim kutusunda (daha fazla bilgi için bkz: [bulma ve Visual Studio uzantılarını kullanarak][vs_find_use_ext]). Merhaba, **Uzantılar ve güncelleştirmeler** iletişim kutusu, iki uzantıları aşağıdaki arama ve indirme hello:
    
    * Azure toplu iş yöneticisi işi Bölümlendirici ile
    * Azure Batch görev işlemci
  * Merhaba şablonları hello çevrimiçi galeriden için Visual Studio indirme: [Microsoft Azure toplu işlem proje şablonları][vs_gallery_templates]
* Toouse hello planlıyorsanız [uygulama paketleri](batch-application-packages.md) özelliği toodeploy hello İş Yöneticisi ve görev işlemci toohello toplu işlem düğümleri, toolink bir depolama hesabı tooyour toplu işlem hesabı gerekir.

## <a name="preparation"></a>Hazırlama
Bu, İş Yöneticisi ve görev işlemci programlar arasında daha kolay tooshare kodu olun çünkü görev işlemcinizin yanı sıra, İş Yöneticisi içerebilir bir çözüm oluşturmanızı öneririz. toocreate Bu çözüm, aşağıdaki adımları izleyin:

1. Visual Studio'yu açın ve seçin **dosya** > **yeni** > **proje**.
2. Altında **şablonları**, genişletin **diğer proje türleri**, tıklatın **Visual Studio çözümleri**ve ardından **boş çözüm**.
3. Bu çözüm (örneğin, "LitwareBatchTaskPrograms"), uygulama ve hello amacını açıklayan bir ad yazın.
4. toocreate hello yeni çözüm tıklatın **Tamam**.

## <a name="job-manager-template"></a>İş Yöneticisi şablonu
Merhaba İş Yöneticisi şablonu hello aşağıdaki eylemleri gerçekleştirebilirsiniz bir iş yöneticisi görevi tooimplement yardımcı olur:

* Bir iş birden çok görevlere bölün.
* Bu görevleri toorun batch gönderin.

> [!NOTE]
> İş Yöneticisi görevleri hakkında daha fazla bilgi için bkz: [geliştiriciler için Batch özelliklerine genel bakış](batch-api-basics.md#job-manager-task).
> 
> 

### <a name="create-a-job-manager-using-hello-template"></a>Merhaba şablonu kullanarak bir iş yöneticisi oluşturma
tooadd daha önce oluşturduğunuz bir iş yöneticisi toohello çözüm adımları izleyin:

1. Var olan çözümünüzü Visual Studio'da açın.
2. Çözüm Gezgini'nde, sağ hello çözüm tıklatın **Ekle** > **yeni proje**.
3. Altında **Visual C#**, tıklatın **bulut**ve ardından **Azure toplu iş yöneticisi işi Bölümlendirici ile**.
4. Uygulamanızı açıklayan ve bu projeyi hello İş Yöneticisi (örneğin tanımlayan bir ad yazın "LitwareJobManager").
5. toocreate hello proje tıklatın **Tamam**.
6. Son olarak, yapı hello proje tooforce Visual Studio tooload tüm NuGet paketlerini başvurulan ve değiştirmeye başlamadan önce proje hello tooverify geçerli değil.

### <a name="job-manager-template-files-and-their-purpose"></a>İş Yöneticisi şablon dosyalarını ve amaçları
Merhaba İş Yöneticisi şablonunu kullanarak bir proje oluşturduğunuzda, kod dosyaları üç grupları oluşturur:

* Merhaba ana program dosyası (Program.cs). Bu, hello program giriş noktası ve en üst düzey özel durum işleme içerir. Normalde toomodify bu gereksinim duyduğunuz döndürmemelidir.
* Merhaba Framework dizini. Bu görevleri toohello toplu işlem, vb. ekleme parametreleri açmak hello İş Yöneticisi programı tarafından – hello 'ortak' işlerini sorumlu hello dosyalarını içerir. Ayrıca, bu dosyaları normalde toomodify gerekir döndürmemelidir.
* Merhaba iş Bölümlendirici dosyası (JobSplitter.cs). Bir işi görevlere bölmek için uygulamaya özgü mantığınızı yerleştireceğiniz budur.

Elbette ek dosyalar gerekli toosupport hello iş mantığı bölme hello karmaşıklığına bağlı olarak, iş Bölümlendirici kod ekleyebilirsiniz.

Merhaba şablon ayrıca .csproj dosya, app.config, packages.config, vb. gibi standart .NET proje dosyalarını oluşturur.

Bu bölümde Hello kalan hello farklı dosya ve kendi kod yapısını ve her sınıf yaptığı açıklanmaktadır.

![Merhaba İş Yöneticisi şablonu çözümünü gösteren Visual Studio Çözüm Gezgini][solution_explorer01]

**Framework dosyaları**

* `Configuration.cs`: İş yapılandırma verilerinin toplu işlem hesabı ayrıntıları, bağlantılı depolama hesabının kimlik bilgilerini, iş ve görev bilgileri ve iş parametrelerini gibi hello yüklenmesini yalıtır. Ayrıca (Merhaba toplu belgelerinde görevler için ortam ayarları bakın) tooBatch tanımlı ortam değişkenleri hello Configuration.EnvironmentVariable sınıfı aracılığıyla erişim sağlar.
* `IConfiguration.cs`: Merhaba yapılandırma sınıf uyarlamasını özetleri Merhaba, yapabilmeniz birim testi sahte veya sahte yapılandırma nesnesi kullanarak, iş Bölümlendirici.
* `JobManager.cs`: Hello İş Yöneticisi programı hello bileşenlerinin düzenler. Merhaba iş Bölümlendirici çağırma hello iş Bölümlendirici başlatma Merhaba sorumludur ve hello iş Bölümlendirici toohello görevi göndereni tarafından döndürülen hello görevleri gönderme.
* `JobManagerException.cs`: Hello İş Yöneticisi tooterminate gerektiren bir hatayı temsil eder. JobManagerException belirli tanılama bilgileri sonlandırma bir parçası olarak burada sağlanabilir kullanılan toowrap 'beklenen' hatası sayısıdır.
* `TaskSubmitter.cs`: Bu sınıf sorumlu tooadding görevleri hello proje Bölümlendirici toohello toplu işi tarafından döndürülen ' dir. Merhaba JobManager sınıfı hello görev dizisi verimli ancak zamanında toplama toohello iş için toplu içine toplar, ardından her toplu işlem için bir arka plan iş parçacığında TaskSubmitter.SubmitTasks çağırır.

**İş Bölümlendirici**

`JobSplitter.cs`: Bu sınıf hello iş görevlere bölmek için uygulamaya özgü mantığını içerir. Merhaba framework çağırır hello JobSplitter.Split yöntemi tooobtain ekler görevleri bir dizi toohello iş hello yöntemi olarak bunları döndürür. Bu hello burada işinizin hello mantığı ekleme sınıftır. Merhaba bölme yöntemi tooreturn toopartition hello iş istediğiniz hello görevleri temsil eden CloudTask örneklerinin bir dizisini uygulayın.

**Standart .NET komut satırı proje dosyaları**

* `App.config`: Standart .NET uygulama yapılandırma dosyası.
* `Packages.config`: Standart NuGet paket bağımlılık dosyası.
* `Program.cs`: Hello program giriş noktası ve en üst düzey özel durum işleme içerir.

### <a name="implementing-hello-job-splitter"></a>Merhaba iş Bölümlendirici uygulama
Merhaba İş Yöneticisi şablonu projeyi açtığınızda hello proje hello JobSplitter.cs dosya varsayılan olarak açık olacaktır. Merhaba Split() yöntemi Göster aşağıdaki kullanarak mantığı, iş yükü hello görevler için bölme hello uygulayabilirsiniz:

```csharp
/// <summary>
/// Gets hello tasks into which toosplit hello job. This is where you inject
/// your application-specific logic for decomposing hello job into tasks.
///
/// hello job manager framework invokes hello Split method for you; you need
/// only tooimplement it, not toocall it yourself. Typically, your
/// implementation should return tasks lazily, for example using a C#
/// iterator and hello "yield return" statement; this allows tasks toobe added
/// and toostart running while splitting is still in progress.
/// </summary>
/// <returns>hello tasks toobe added toohello job. Tasks are added automatically
/// by hello job manager framework as they are returned by this method.</returns>
public IEnumerable<CloudTask> Split()
{
    // Your code for hello split logic goes here.
    int startFrame = Convert.ToInt32(_parameters["StartFrame"]);
    int endFrame = Convert.ToInt32(_parameters["EndFrame"]);

    for (int i = startFrame; i <= endFrame; i++)
    {
        yield return new CloudTask("myTask" + i, "cmd /c dir");
    }
}
```

> [!NOTE]
> Merhaba hello bölümünde açıklanan `Split()` hello yalnızca hello hello mantığı toosplit işleriniz farklı görevlere ekleyerek, toomodify hedeflenen İş Yöneticisi şablonu kodu bölümünü bir yöntemdir. Toomodify hello şablonu farklı bir bölümünü istiyorsanız, lütfen familiarized toplu nasıl çalıştığı ile olduğundan emin olun ve hello bazılarını deneyin [toplu kod örnekleri][github_samples].
> 
> 

Split() uygulamanıza erişimi:

* İş parametreleri hello aracılığıyla hello `_parameters` alan.
* Merhaba CloudJob hello aracılığıyla temsil eden hello iş nesnesi `_job` alan.
* Merhaba CloudTask nesnesini temsil eden hello iş yöneticisi görevi, hello aracılığıyla `_jobManagerTask` alan.

`Split()` Uygulaması tooadd görevleri toohello işi doğrudan gerekmez. Bunun yerine, kodunuzu CloudTask nesnelerinin bir dizisi döndürmelidir ve bunlar toohello iş otomatik olarak hello iş Bölümlendirici çağırma hello framework sınıfları tarafından eklenir. Ortak toouse C# ' ın yineleyici olduğu (`yield return`) yerine mümkün olan en kısa sürede çalıştıran hello görevleri toostart böylece gibi tüm görevleri toobe için bekleyen hesaplanan tooimplement iş ayırıcılar özelliği.

**İş Bölümlendirici hatası**

İş Bölümlendirici hatayla karşılaşırsa ya da gerekir:

* Merhaba C# kullanarak hello dizisi sonlandırmak `yield break` deyimi, hangi servis talebi hello İş Yöneticisi işleneceğini başarılı olarak; veya
* Servis talebi hello iş yöneticisi başarısız olarak kabul edilir ve nasıl hello istemci bunu yapılandırdığına bağlı olarak denenen bir özel durum:).

Her iki durumda da herhangi bir görevi zaten hello iş Bölümlendirici tarafından döndürülen ve eklenen toohello toplu uygun toorun olacaktır. Bu toohappen istemiyorsanız, olabilir:

* Merhaba iş Bölümlendirici döndürmeden önce Hello işi Sonlandır
* Bunu dönmeden önce hello tüm görev koleksiyon formüle (diğer bir deyişle, dönüş bir `ICollection<CloudTask>` veya `IList<CloudTask>` bir C# yineleyici kullanarak, iş Bölümlendirici uygulamak yerine)
* Tüm Görevler hello başarılı şekilde tamamlandığını hello İş Yöneticisi üzerinde bağımlı görev bağımlılıkları toomake kullanın

**İş Yöneticisi'ni yeniden deneme**

Merhaba iş yöneticisi başarısız olursa, hello istemci yeniden deneme ayarlarına bağlı olarak hello Batch hizmeti tarafından denenen. Merhaba framework görevleri toohello iş eklediğinde, zaten mevcut herhangi bir görevi yoksayar genel olarak, güvenli olmasıdır. Ancak, görevleri hesaplama pahalı ise, toohello iş zaten eklenmiş olan görevleri yeniden hesaplanması tooincur hello maliyetini istemeyen; Buna karşılık, hello yeniden çalıştırırsanız olduğu garanti edilemez toogenerate hello aynı görev kimlikleri hello 'çoğaltmaları Yoksay' davranışı ilkenin etkisini gösterip değil sonra. Bu durumlarda zaten yapılmış ve bu, örneğin tooyield görevleri başlatmadan önce bir CloudJob.ListTasks gerçekleştirerek kullanmamasını, iş Bölümlendirici toodetect hello çalışmanızı tasarlamanız gerekir.

### <a name="exit-codes-and-exceptions-in-hello-job-manager-template"></a>Çıkış kodları ve hello İş Yöneticisi şablonunda özel durumlar
Çıkış kodları ve özel durumları bir programı çalıştırma mekanizması toodetermine hello sonucu sağlayın ve herhangi bir sorun hello hello programın yürütülmesini tooidentify yardımcı olabilir. Merhaba İş Yöneticisi şablonu hello çıkış kodları ve bu bölümde açıklanan özel durumları uygular.

Merhaba iş Manager şablonu ile gerçekleştirilen bir iş yöneticisi görevi üç olası çıkış kodlarını döndürebilirsiniz:

| Kod | Açıklama |
| --- | --- |
| 0 |Merhaba iş yöneticisi başarıyla tamamlandı. İş Bölümlendirici kodunuzu toocompletion çalıştırılmış ve tüm görevler toohello iş eklendi. |
| 1 |Merhaba iş yöneticisi görevi hello program 'beklenen' bir parçası olarak bir özel durum ile başarısız oldu. tanılama bilgileri ile çevrilmiş tooa JobManagerException Hello özel durum ve mümkün olduğunda, çözümü için öneriler hatası hello. |
| 2 |Merhaba iş yöneticisi görevi 'beklenmeyen' bir özel durumla başarısız oldu. Merhaba özel durum günlüğe kaydedilen toostandard çıkış ancak hello İş Yöneticisi oldu oluşturulamıyor tooadd ek tanılama ya da düzeltme bilgileri. |

Merhaba hatadan önce iş yöneticisi görevi hatası hello durumda bazı görevler hala toohello hizmet eklenmemiş olabilir. Bu görevleri normal olarak çalışır. "İş Bölümlendirici hatası" yukarıda bu kod yolu hakkında bilgi için bkz.

Özel durumlar tarafından döndürülen tüm hello bilgileri stdout.txt ve stderr.txt dosyalarına yazılır. Daha fazla bilgi için bkz: [işleme hatası](batch-api-basics.md#error-handling).

### <a name="client-considerations"></a>İstemci değerlendirmeleri
Bu bölümde, bu şablona dayalı bir iş yöneticisi çağrılırken, bazı istemci uygulama gereksinimleri açıklanmaktadır. Bkz: [istemci kodu toopass parametreleri ve ortam değişkenlerinin nasıl hello](#pass-environment-settings) parametreleri ve ortam ayarlarını geçirme hakkında bilgi.

**Zorunlu kimlik bilgileri**

Sipariş tooadd görevleri toohello Azure toplu işlemde hello iş yöneticisi görevi Azure Batch hesabı URL'si ve anahtar gerektirir. Bu ortam değişkenleri YOUR_BATCH_URL ve YOUR_BATCH_KEY adlı geçmesi gerekir. Bu hello iş yöneticisi görevi ortam ayarları ayarlayabilirsiniz. Örneğin, C# istemci olarak:

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    new EnvironmentSetting("YOUR_BATCH_URL", "https://account.region.batch.azure.com"),
    new EnvironmentSetting("YOUR_BATCH_KEY", "{your_base64_encoded_account_key}"),
};
```
**Depolama kimlik bilgileri**

Genellikle, hello istemci tooprovide hello bağlantılı depolama hesabı kimlik bilgileri toohello iş yöneticisi görevi (a) çoğu iş yöneticileri tooexplicitly erişim hello bağlantılı depolama hesabı gerekmez ve (b) hello bağlantılı depolama hesabına genellikle sağlanan çünkü gerekmez Merhaba iş ortak ortamı ayarı olarak tooall görevler. Değil sağlıyorsanız hello hello ortak ortam ayarları aracılığıyla depolama hesabı bağlı ve erişim toolinked depolama hello İş Yöneticisi gerektirir, ardından hello bağlantılı depolama kimlik bilgilerini aşağıdaki gibi sağlamanız:

```csharp
job.JobManagerTask.EnvironmentSettings = new [] {
    /* other environment settings */
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

**İş Yöneticisi görevi ayarları**

Merhaba istemci hello İş Yöneticisi ayarlamalıdır *killJobOnCompletion* çok bayrak**false**.

Merhaba istemci tooset için genellikle güvenlidir *runExclusive* çok**false**.

Merhaba istemci hello kullanması gereken *resourceFiles* veya *applicationPackageReferences* koleksiyonu toohave hello İş Yöneticisi yürütülebilir (ve gerekli DLL'leri) dağıtılan toohello işlem düğümü.

Başarısız olursa varsayılan olarak, hello İş Yöneticisi denenecek değil. İş Yöneticisi mantığa bağlı hello istemci tooenable deneme aracılığıyla isteyebilirsiniz *kısıtlamaları*/*maxTaskRetryCount*.

**Proje ayarları**

Görev bağımlılıkları ile Merhaba iş Bölümlendirici yayar, hello istemci hello işin usesTaskDependencies tootrue ayarlamanız gerekir.

Merhaba iş Bölümlendirici modelde hangi hello iş Bölümlendirici oluşturur üzerine istemcileri toowish tooadd görevleri toojobs için olağan dışı. Merhaba istemci bu nedenle normal olarak ayarlamalıdır hello işin *onAllTasksComplete* çok**terminatejob**.

## <a name="task-processor-template"></a>Görev işlemci şablonu
Bir görev işlemci şablonu tooimplement hello aşağıdaki eylemleri gerçekleştirebilirsiniz görev işlemci yardımcı olur:

* Her toplu görev toorun tarafından gerekli hello bilgilerini ayarlayın.
* Her toplu iş görevi tarafından istenen tüm eylemler çalıştırın.
* Görev çıktıları toopersistent depolama kaydedin.

Bir görev işlemci değil gerekli toorun görevleri batch görev işlemci kullanımının hello önemli bir avantajı, bir konumdaki tüm görev yürütme eylemleri sarmalayıcı tooimplement sağlar olsa da. Örneğin, her görevin hello bağlamda çeşitli uygulamalar toorun ihtiyacınız varsa veya gereksinim duyarsanız toocopy veri toopersistent depolama tamamladıktan sonra her görev.

Basit veya karmaşık, olarak ve birçok veya olarak az sayıda İş yükünüzün gerektirdiği şekilde Hello görev işlemcisi tarafından gerçekleştirilen hello eylemler olabilir. Ayrıca, bir görev işlemci halinde tüm görev eylemleri uygulayarak, taşımalarına güncelleştirebilir veya değişiklikleri tooapplications ya da iş yükü gereksinimlerine bağlı olarak Eylemler ekleyebilirsiniz. Ancak, bazı durumlarda Örneğin hızlı bir şekilde basit bir komut satırından başlatılan bir iş çalışmadığı zaman gereksiz karmaşıklık ekleyebilirsiniz gibi hello en iyi çözüm, uygulamanız için bir görev işlemci olmayabilir.

### <a name="create-a-task-processor-using-hello-template"></a>Merhaba şablonu kullanarak bir görev işlemcisi oluşturma
tooadd daha önce oluşturduğunuz bir görev işlemci toohello çözüm adımları izleyin:

1. Var olan çözümünüzü Visual Studio'da açın.
2. Çözüm Gezgini'nde, sağ hello çözüm tıklatın **Ekle**ve ardından **yeni proje**.
3. Altında **Visual C#**, tıklatın **bulut**ve ardından **Azure Batch görev İşlemci**.
4. Uygulamanızı açıklayan ve bu projeyi görev işlemci (örneğin hello olarak tanımlayan bir ad yazın "LitwareTaskProcessor").
5. toocreate hello proje tıklatın **Tamam**.
6. Son olarak, yapı hello proje tooforce Visual Studio tooload tüm NuGet paketlerini başvurulan ve değiştirmeye başlamadan önce proje hello tooverify geçerli değil.

### <a name="task-processor-template-files-and-their-purpose"></a>Görev işlemci şablon dosyalarını ve amaçları
Merhaba görev işlemci şablonu kullanarak bir proje oluşturduğunuzda, kod dosyaları üç grupları oluşturur:

* Merhaba ana program dosyası (Program.cs). Bu, hello program giriş noktası ve en üst düzey özel durum işleme içerir. Normalde toomodify bu gereksinim duyduğunuz döndürmemelidir.
* Merhaba Framework dizini. Bu görevleri toohello toplu işlem, vb. ekleme parametreleri açmak hello İş Yöneticisi programı tarafından – hello 'ortak' işlerini sorumlu hello dosyalarını içerir. Ayrıca, bu dosyaları normalde toomodify gerekir döndürmemelidir.
* Merhaba görev işlemcisi dosyasını (TaskProcessor.cs). Bir görev (genellikle tooan varolan yürütülebilir çağırarak) yürütmek, uygulamaya özgü mantığınızı yerleştireceğiniz budur. Ek veri indirme veya sonuç dosyalarını karşıya yükleme gibi ön ve işlem sonrası kodu da buraya ekleyin.

Elbette, ek dosyalar hello iş mantığı bölme hello karmaşıklığına bağlı olarak, görev işlemci kodu gerekli toosupport ekleyebilirsiniz.

Merhaba şablon ayrıca .csproj dosya, app.config, packages.config, vb. gibi standart .NET proje dosyalarını oluşturur.

Bu bölümde Hello kalan hello farklı dosya ve kendi kod yapısını ve her sınıf yaptığı açıklanmaktadır.

![Merhaba görev işlemci şablon çözümünü gösteren Visual Studio Çözüm Gezgini][solution_explorer02]

**Framework dosyaları**

* `Configuration.cs`: İş yapılandırma verilerinin toplu işlem hesabı ayrıntıları, bağlantılı depolama hesabının kimlik bilgilerini, iş ve görev bilgileri ve iş parametrelerini gibi hello yüklenmesini yalıtır. Ayrıca (Merhaba toplu belgelerinde görevler için ortam ayarları bakın) tooBatch tanımlı ortam değişkenleri hello Configuration.EnvironmentVariable sınıfı aracılığıyla erişim sağlar.
* `IConfiguration.cs`: Merhaba yapılandırma sınıf uyarlamasını özetleri Merhaba, yapabilmeniz birim testi sahte veya sahte yapılandırma nesnesi kullanarak, iş Bölümlendirici.
* `TaskProcessorException.cs`: Hello İş Yöneticisi tooterminate gerektiren bir hatayı temsil eder. TaskProcessorException belirli tanılama bilgileri sonlandırma bir parçası olarak burada sağlanabilir kullanılan toowrap 'beklenen' hatası sayısıdır.

**Görev işlemci**

* `TaskProcessor.cs`: Hello görev çalıştırır. Merhaba framework hello TaskProcessor.Run yöntemini çağırır. Bu hello burada göreviniz hello uygulamaya özgü mantığını Ekle sınıftır. Merhaba Çalıştır yönteme uygulayın:
  * Ayrıştırma ve herhangi bir görev parametre doğrulama
  * Merhaba komut satırı oluşturan tooinvoke istediğiniz tüm dış programı
  * Hata ayıklama amacıyla gerektirebilecek herhangi tanılama bilgileri günlüğe kaydet
  * Bu komut satırını kullanarak bir işlem Başlat
  * Merhaba işlem tooexit bekle
  * Başarılı veya başarısız olursa hello işlem toodetermine hello çıkış kodu yakalama
  * İstediğiniz tüm çıktı dosyaları tookeep toopersistent depolama kaydedin

**Standart .NET komut satırı proje dosyaları**

* `App.config`: Standart .NET uygulama yapılandırma dosyası.
* `Packages.config`: Standart NuGet paket bağımlılık dosyası.
* `Program.cs`: Hello program giriş noktası ve en üst düzey özel durum işleme içerir.

## <a name="implementing-hello-task-processor"></a>Merhaba görev işlemci uygulama
Merhaba görev işlemci şablon projeyi açtığınızda hello proje hello TaskProcessor.cs dosya varsayılan olarak açık olacaktır. Aşağıda gösterilen hello Run() yöntemi kullanarak, iş yükü hello görevleri çalıştırmak hello mantığı uygulayabilirsiniz:

```csharp
/// <summary>
/// Runs hello task processing logic. This is where you inject
/// your application-specific logic for decomposing hello job into tasks.
///
/// hello task processor framework invokes hello Run method for you; you need
/// only tooimplement it, not toocall it yourself. Typically, your
/// implementation will execute an external program (from resource files or
/// an application package), check hello exit code of that program and
/// save output files toopersistent storage.
/// </summary>
public async Task<int> Run()

{
    try
    {
        //Your code for hello task processor goes here.
        var command = $"compare {_parameters["Frame1"]} {_parameters["Frame2"]} compare.gif";
        using (var process = Process.Start($"cmd /c {command}"))
        {
            process.WaitForExit();
            var taskOutputStorage = new TaskOutputStorage(
            _configuration.StorageAccount,
            _configuration.JobId,
            _configuration.TaskId
            );
            await taskOutputStorage.SaveAsync(
            TaskOutputKind.TaskOutput,
            @"..\stdout.txt",
            @"stdout.txt"
            );
            return process.ExitCode;
        }
    }
    catch (Exception ex)
    {
        throw new TaskProcessorException(
        $"{ex.GetType().Name} exception in run task processor: {ex.Message}",
        ex
        );
    }
}
```
> [!NOTE]
> Merhaba hello Run() yöntemi açıklamalı bölümünde hello yalnızca hello görevleri çalıştırmak hello mantığı, iş yükü ekleyerek, toomodify için tasarlanmıştır Merhaba görev işlemci şablonu kodu bölümüdür. Toomodify hello şablonu farklı bir bölümünü istiyorsanız, Lütfen ilk önce toplu hello toplu belgelerini gözden geçirin ve hello toplu kod örnekleri birkaç çalışırken işleyişi ile edinin.
> 
> 

Merhaba Run() yöntemi hello komut satırı başlatarak, bir veya daha fazla işlemlerini başlatma, tüm işlem toocomplete için bekleyen hello sonuçları kaydetme ve son olarak bir çıkış kodu ile döndürme sorumludur. Merhaba Run() yöntemi mantığını görevleriniz için işleme hello uygulamak burada ' dir. Merhaba görev işlemci framework hello Run() yöntemi için çağırır; toocall gerekmez, kendiniz.

Run() uygulamanıza erişimi:

* Görev parametreleri hello aracılığıyla hello `_parameters` alan.
* Merhaba aracılığıyla iş ve görev kimlikleri hello `_jobId` ve `_taskId` alanları.
* Merhaba aracılığıyla Hello görev Yapılandırması `_configuration` alan.

**Görev hatası**

Hata durumunda bir özel durum atma tarafından hello Run() yöntemi çıkabilirsiniz ancak bu hello en üst düzey özel durum işleyici hello Görev çıkış kodu denetiminde durumda bırakır. Böylece hatası, farklı türlerde tanılama amacıyla örneğin ayırabilmesi toocontrol hello çıkış kodu ihtiyacınız varsa veya bazı modu hatası sonlandırması gerekir çünkü hello iş ve diğerleri vermemelisiniz ardından döndürerek hello Run() yöntemi çıkmalıdır bir sıfır olmayan çıkış kodu. Bu hello Görev çıkış kodu olur.

### <a name="exit-codes-and-exceptions-in-hello-task-processor-template"></a>Çıkış kodları ve hello görev işlemci şablonunda özel durumları
Çıkış kodları ve özel durumları bir programı çalıştırma mekanizması toodetermine hello sonucu sağlayın ve bunlar hello hello programın yürütülmesini herhangi bir sorunu tanımlamaya yardımcı olabilir. Merhaba görev işlemci şablon hello çıkış kodları ve bu bölümde açıklanan özel durumları uygular.

Merhaba görev işlemci şablonla uygulanan bir işlemci görevi üç olası çıkış kodlarını döndürebilirsiniz:

| Kod | Açıklama |
| --- | --- |
| [Process.ExitCode][process_exitcode] |Merhaba görev işlemci toocompletion verdi. Bu, çağrılan bu hello program başarılı anlamına gelmez, Not – yalnızca bu hello görev işlemci başarıyla çağrılır ve özel durumlar olmadan tüm sonrası işleme yapılır. Merhaba çıkış kodu Hello anlamını çağrılan hello programına bağımlıdır – hello program başarılı oldu ve başka bir çıkış kodu hello programı başarısız oldu anlamına gelir. çıkış kodu 0 genellikle anlamına gelir. |
| 1 |Merhaba görev işlemci hello program 'beklenen' bir parçası olarak bir özel durum ile başarısız oldu. Merhaba özel durum çevrilmiş tooa `TaskProcessorException` tanılama bilgileriyle ve mümkün olduğunda, çözümü için öneriler hatası hello. |
| 2 |Merhaba görev İşlemci 'beklenmeyen' bir özel durumla başarısız oldu. Merhaba özel durum günlüğe kaydedilen toostandard çıkış ancak hello görev işlemci oldu oluşturulamıyor tooadd ek tanılama ya da düzeltme bilgileri. |

> [!NOTE]
> Çıkış kodları 1 ve 2 tooindicate belirli hata modları çağırmayı hello program kullanıyorsa, ardından çıkış kodlarını 1 ve 2 görev İşlemci hataları için belirsiz kullanmaktır. Bu görev işlemci hata kodları toodistinctive çıkış kodları hello özel durumlarda hello Program.cs dosyasını düzenleyerek değiştirebilirsiniz.
> 
> 

Özel durumlar tarafından döndürülen tüm hello bilgileri stdout.txt ve stderr.txt dosyalarına yazılır. Daha fazla bilgi için hata işleme, hello toplu belgelerine bakın.

### <a name="client-considerations"></a>İstemci değerlendirmeleri
**Depolama kimlik bilgileri**

Azure blob depolama toopersist çıkarır, örneğin hello dosya kuralları Yardımcısı kitaplığı kullanarak görev işlemci kullanır sonra çok erişmesi gereken*ya da* bulut depolama hesabının kimlik bilgilerini hello *veya* paylaşılan erişim imzası (SAS) içeren bir blob kapsayıcı URL. Merhaba şablon ortak ortam değişkenleri aracılığıyla kimlik bilgilerini sağlamak için destek içerir. İstemci hello depolama kimlik bilgilerini aşağıdaki gibi geçirebilirsiniz:

```csharp
job.CommonEnvironmentSettings = new [] {
    new EnvironmentSetting("LINKED_STORAGE_ACCOUNT", "{storageAccountName}"),
    new EnvironmentSetting("LINKED_STORAGE_KEY", "{storageAccountKey}"),
};
```

Merhaba depolama hesabı hello TaskProcessor sınıfı hello aracılığıyla kullanılabilir durumda `_configuration.StorageAccount` özelliği.

Toouse SAS kapsayıcı URL'SİYLE tercih ederseniz, bu da bir iş ortak ortamı ayarı aracılığıyla geçirebilirsiniz ancak hello görev işlemci şablonu şu anda bu için yerleşik destek içermez.

**Depolama Kurulumu**

Bu hello istemci veya iş yöneticisi görevi oluşturmanız gereken görevleri tarafından hello görevleri toohello iş eklemeden önce herhangi bir kapsayıcıdaki önerilir. Bu, bir kapsayıcı URL'si ile SAS kullanırsanız, bu nedenle bir URL izni toocreate hello kapsayıcı içermez zorunludur. Depolama hesabı kimlik bilgileri, geçirdiğiniz olsa bile hello kapsayıcısında toocall CloudBlobContainer.CreateIfNotExistsAsync sahip her görev kaydeder önerilir.

## <a name="pass-parameters-and-environment-variables"></a>Parametreleri ve ortam değişkenleri
### <a name="pass-environment-settings"></a>Geçişi ortam ayarları
Bir istemci bilgileri toohello iş yöneticisi görevi hello biçiminde ortam ayarlarını geçirebilirsiniz. İşlem iş hello bir parçası olarak çalıştırılan oluşturma hello görev işlemci görevlerini olduğunda bu bilgileri daha sonra hello iş yöneticisi görevi tarafından kullanılabilir. Ortam ayarları geçirebilirsiniz hello bilgi örnekleri şunlardır:

* Depolama hesabı adı ve hesap anahtarları
* Batch hesabı URL'si
* Toplu işlem hesabı anahtarı

Merhaba Batch hizmeti hello kullanarak basit bir mekanizma toopass ortam ayarları tooa iş yöneticisi görevi sahip `EnvironmentSettings` özelliğinde [Microsoft.Azure.Batch.JobManagerTask][net_jobmanagertask].

Örneğin, tooget hello `BatchClient` örneği ortam değişkenleri hello istemciden hello URL kod ve paylaşılan anahtar kimlik bilgilerini hello toplu işlem hesabı için bir toplu işlem hesabı için geçirebilirsiniz. Benzer şekilde, toohello toplu işlem hesabı olan tooaccess hello depolama hesabı bağlı, ortam değişkenleri olarak hello depolama hesabı adı ve hello depolama hesabı anahtarı geçirin.

### <a name="pass-parameters-toohello-job-manager-template"></a>Parametreleri toohello İş Yöneticisi şablonu geçirin
Çoğu durumda, yararlı toopass iş başına parametreleri toohello iş yöneticisi görevi, işlem bölme ya da toocontrol hello işi, veya iş tooconfigure hello görevlerde hello. Merhaba iş yöneticisi görevinin kaynak dosyası olarak parameters.json adlı bir JSON dosyası karşıya yükleyerek bunu yapabilirsiniz. Merhaba parametreleri hello kullanılabilir dönüşebilir `JobSplitter._parameters` hello İş Yöneticisi şablonu alanındaki.

> [!NOTE]
> Merhaba yerleşik parametre işleyicisi yalnızca dize-dize sözlükler destekler. Toopass karmaşık JSON değerleri parametre değerleri olarak istiyorsanız toopass dizeleri olarak gerektiğinde ve hello iş Bölümlendirici ayrıştırma veya hello framework'ün değiştirme `Configuration.GetJobParameters` yöntemi.
> 
> 

### <a name="pass-parameters-toohello-task-processor-template"></a>Parametreleri toohello görev işlemci şablon geçirin
Parametreleri tooindividual görevleri geçirebilirsiniz hello görev işlemci şablonu kullanılarak uygulanan. Merhaba iş manager şablonu ile gibi adlı bir kaynak dosyasını hello görev işlemci şablonu arar

Parameters.JSON ve bulduğu IF hello parametreleri sözlüğü olarak yükler. Birkaç nasıl toopass parametreleri toohello görev işlemci görevler için Seçenekler şunlardır:

* Merhaba iş parametrelerini JSON yeniden kullanabilirsiniz. Bu, iyi hello yalnızca parametreleri (örneğin, bir işleme yükseklik ve genişlik için) iş genelinde olanları ise çalışır. toodo Bu, bir CloudTask hello iş Bölümlendirici oluştururken, hello iş yöneticisi görevi'nin ResourceFiles başvuru toohello parameters.json kaynak dosya nesnesi ekleme (`JobSplitter._jobManagerTask.ResourceFiles`) toohello CloudTask'ın ResourceFiles koleksiyonu.
* Oluşturmak ve bir görev özgü parameters.json belge iş Bölümlendirici yürütme bir parçası olarak yüklemek ve bu blob hello görevin kaynak dosyaları koleksiyonundaki başvuru. Farklı görevler farklı parametreler varsa, bu gereklidir. Bir örnek hello çerçeve dizini parametre olarak toohello görev geçirildiği 3B işleme senaryo olabilir.

> [!NOTE]
> Merhaba yerleşik parametre işleyicisi yalnızca dize-dize sözlükler destekler. Toopass karmaşık JSON değerleri parametre değerleri olarak istiyorsanız toopass dizeleri olarak gerektiğinde ve hello görev işlemcide ayrıştırma veya hello framework'ün değiştirme `Configuration.GetTaskParameters` yöntemi.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
### <a name="persist-job-and-task-output-tooazure-storage"></a>İşi Sürdür ve çıktı tooAzure depolama görev
Batch çözümü geliştirme yararlı bir diğer araç [Azure toplu işlem dosyası kuralları][nuget_package]. Batch .NET uygulamaları tooeasily deponuzda bu .NET sınıf kitaplığı (şu anda önizlemede) kullanın ve görev çıktıları tooand Azure Depolama'dan alın. [Azure toplu işlem iş ve görev çıktısı kalıcı](batch-task-output.md) hello kitaplığı ve kullanım tam bir irdelemesi içerir.

### <a name="batch-forum"></a>Toplu işlem Forumu
Merhaba [Azure toplu işlem Forumu] [ forum] MSDN'de mükemmel toodiscuss toplu yerleştirin ve hello hizmeti hakkında soru sorun olduğunu. HEAD üzerinde üzerinden faydalı "Yapışkan" gönderiler için ve Batch çözümlerinizi derleme sırasında çıktıkları anda sorularınızı gönderin.

[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[net_jobmanagertask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobmanagertask.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[process_exitcode]: https://msdn.microsoft.com/library/system.diagnostics.process.exitcode.aspx
[vs_gallery]: https://visualstudiogallery.msdn.microsoft.com/
[vs_gallery_templates]: https://go.microsoft.com/fwlink/?linkid=820714
[vs_find_use_ext]: https://msdn.microsoft.com/library/dd293638.aspx

[diagram01]: ./media/batch-visual-studio-templates/diagram01.png
[solution_explorer01]: ./media/batch-visual-studio-templates/solution_explorer01.png
[solution_explorer02]: ./media/batch-visual-studio-templates/solution_explorer02.png
