---
title: "dosyaları ve bileşen özelliklerini Premium Kodlayıcı - Azure ile aaaMultiple giriş | Microsoft Docs"
description: "Bu konuda nasıl toouse setRuntimeProperties toouse birden çok girdi dosyaları ve özel veri toohello Medya Kodlayıcısı Premium iş akışı medya işlemcisi geçirmek açıklanmaktadır."
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: 7fb35bdd-9891-4401-a65b-ef3cc8190e8a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: xpouyat;anilmur;juliako
ms.openlocfilehash: e14d10fbf9669e0b88e5ba1c519f1ba5e0bafdd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-multiple-input-files-and-component-properties-with-premium-encoder"></a>Premium Kodlayıcı ile birden fazla giriş dosyaları ve bileşen özellikleri kullanma
## <a name="overview"></a>Genel Bakış
İçinde ihtiyacınız olabilecek toocustomize bileşen özellikleri senaryo vardır küçük listesi XML içeriğini belirtin veya hello görevle gönderdiğinizde birden çok giriş dosyaları göndermek **Medya Kodlayıcısı Premium iş akışı** medya işlemcisi. Bazı örnekler şunlardır:

* Video metin kaplayan ve her giriş video için çalışma zamanında hello metin değeri (örneğin, geçerli tarih hello) ayarlama.
* Merhaba küçük liste XML (toospecify. bir veya birkaç kaynak dosyaları, ile veya olmadan kırpma, vb.) özelleştirme.
* Merhaba video kodlanmış sırada hello giriş video logo görüntüsü üst üste getirme.
* Birden çok ses dil kodlaması.

toolet hello **Medya Kodlayıcısı Premium iş akışı** bilmeniz hello görev oluşturduğunuzda ya da birden çok giriş dosyaları göndermek bazı özellikler hello iş akışında değiştiriyorsunuz, içeren bir yapılandırma dizesi toouse sahip  **setRuntimeProperties** ve/veya **transcodeSource**. Bu konuda açıklanmaktadır nasıl toouse bunları.

## <a name="configuration-string-syntax"></a>Yapılandırma dizesi sözdizimi
Merhaba yapılandırma dizesi tooset görev kodlama hello içinde şuna benzer bir XML belgesi kullanır:

```xml
<?xml version="1.0" encoding="utf-8"?>
<transcodeRequest>
  <transcodeSource>
  </transcodeSource>
  <setRuntimeProperties>
    <property propertyPath="Media File Input/filename" value="VideoFileName.mp4" />
  </setRuntimeProperties>
</transcodeRequest>
```

Merhaba aşağıdaki hello XML yapılandırması bir dosyadan okur hello C# kod, kendisiyle güncelleştirme sağ video filename hello ve bir işi toohello görev geçirir:

```c#
string premiumConfiguration = ReadAllText(@"D:\home\site\wwwroot\Presets\SetRuntime.xml").Replace("VideoFileName", myVideoFileName);

// Declare a new job.
IJob job = _context.Jobs.Create("Premium Workflow encoding job");

// Get a media processor reference, and pass tooit hello name of hello 
// processor toouse for hello specific task.
IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

// Create a task with hello encoding details, using a string preset.
ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                              processor,
                              premiumConfiguration,
                              TaskOptions.None);

// Specify hello input assets
task.InputAssets.Add(workflow); // workflow asset
task.InputAssets.Add(video); // video asset with multiple files

// Add an output asset toocontain hello results of hello job. 
// This output is specified as AssetCreationOptions.None, which 
// means hello output asset is not encrypted. 
task.OutputAssets.AddNew("Output asset", AssetCreationOptions.None);
```

## <a name="customizing-component-properties"></a>Bileşen özelliklerini özelleştirme
### <a name="property-with-a-simple-value"></a>Basit bir değere sahip özelliği
Bazı durumlarda bu kullanışlı toocustomize Medya Kodlayıcısı Premium iş akışı tarafından yürütülen toobe geçiyor hello iş akışı dosyası ile birlikte bir bileşen özelliği olur.

Bir iş akışı videolarınızı üzerinde yer paylaşımları metni tasarlanmış ve (örneğin, geçerli tarih hello) hello metni toobe kümesi çalışma zamanında gerektiği varsayalım. Merhaba hello katmana bileşeninin hello metin özelliği için yeni değer olarak görev kodlama hello ayarlamak hello metin toobe göndererek bunu yapabilirsiniz. Merhaba iş akışında (örneğin, hello konumu veya hello katmana rengini, hello bit hızı hello AVC Kodlayıcı, vb.), bu mekanizma toochange bir bileşenin diğer özelliklerini kullanabilirsiniz.

**setRuntimeProperties** kullanılan toooverride hello bileşenleri hello iş akışının bir özelliktir.

Örnek:

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="MyInputVideo.mp4" />
      <property propertyPath="/primarySourceFile" value="MyInputVideo.mp4" />
      <property propertyPath="Optional Text Overlay/Text tooImage Converter/text" value="Today is Friday hello 13th of May, 2016"/>
  </setRuntimeProperties>
</transcodeRequest>
```

### <a name="property-with-an-xml-value"></a>XML değeri özelliği
tooset bir XML değer bekler bir özellik kapsülleyen kullanarak `<![CDATA[ and ]]>`.

Örnek:

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

> [!NOTE]
> Tooput bir satır başı dönüş hemen sonra emin `<![CDATA[`.

### <a name="propertypath-value"></a>propertyPath değeri
Merhaba propertyPath Hello önceki örneklerde olduğu "/ medya dosya giriş/dosya adı" veya "/ inactiveTimeout" veya "clipListXml".
Bu, genel olarak, hello bileşenin hello adı hello özelliğinin hello adı olduğundan. Merhaba yolu daha fazla veya daha az düzeyleri gibi olabilir "/ primarySourceFile" (Merhaba özelliği hello hello iş akışı kökünde olduğundan) veya "/ Video işleme/grafiği katmana/opaklık" (bir grupta hello katmana olduğu için).    

toocheck hello yolu ve özellik adını, hemen her özelliğin kullanım hello eylem düğmesi. Bu eylem düğmesini tıklatın ve seçin **Düzenle**. Bu, hello gerçek gösterir adı hello özelliğinin ve hemen üstünde, ad alanı hello.

![Eylem/Düzenle](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture6_actionedit.png)

![Özellik](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture7_viewproperty.png)

## <a name="multiple-input-files"></a>Birden çok giriş dosyaları
Her görev toohello gönderme **Medya Kodlayıcısı Premium iş akışı** iki varlıklar gerektirir:

* Merhaba ilk biridir bir *iş akışı varlık* bir iş akışı dosyası içerir. Hello kullanarak iş akışı dosyalarını tasarlayabilirsiniz [iş akışı Tasarımcısı](media-services-workflow-designer.md).
* Merhaba ikincisi olan bir *medya varlık* tooencode istediğiniz hello medya dosyaları içerir.

Ne zaman size göndererek birden çok medya dosyaları toohello **Medya Kodlayıcısı Premium iş akışı** encoder kısıtlamaları aşağıdaki hello Uygula:

* Tüm hello medya dosyaları bulunmalıdır hello aynı *medya varlık*. Birden çok medya varlıkları kullanma desteklenmiyor.
* Bu medya varlık hello birincil dosya ayarlamanız gerekir (İdeal olarak, bu hello olan Kodlayıcı hello ana video dosyası tooprocess sorulan).
* Merhaba içeren gerekli toopass yapılandırma verilerini olduğu **setRuntimeProperties** ve/veya **transcodeSource** öğesi toohello işlemci.
  * **setRuntimeProperties** kullanılan toooverride hello filename özelliği ya da başka bir özellik hello iş akışının hello bileşenleri.
  * **transcodeSource** kullanılan toospecify hello küçük listesi XML içeriği değil.

Bağlantıları hello iş akışı'nda:

* Bir veya birkaç ortam dosyası girişi bileşenleri kullanır ve toouse planı **setRuntimeProperties** toospecify hello dosya adı, ardından hello birincil dosya bileşen PIN toothem bağlamayın. Merhaba birincil dosya nesnesi ve hello medya dosyası Input(s) arasında bağlantı olduğundan emin olun.
* Toouse küçük liste XML ve bir medya kaynağı bileşen tercih ederseniz, ardından, her ikisi de birbirine bağlayabilirsiniz.

![Hiçbir bağlantısından birincil kaynak dosya tooMedia dosya giriş](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture0_nopin.png)

*SetRuntimeProperties tooset hello filename özelliğini kullanırsanız, hello birincil dosya tooMedia dosya giriş bileşenleri hiçbir bağlantısı yoktur.*

![Küçük resim listesi XML tooClip kaynak listesi bağlantısından](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture1_pincliplist.png)

*Küçük resim listesi XML tooMedia kaynak bağlanabilir ve transcodeSource kullanabilirsiniz.*

### <a name="clip-list-xml-customization"></a>Liste XML özelleştirmesi Kırp
Kullanarak çalışma zamanında hello akışında hello küçük liste XML belirtebilirsiniz **transcodeSource** hello yapılandırmasında XML dizesi. Bu hello küçük liste XML PIN bağlı toobe toohello medya kaynağı bileşen hello iş akışında gereklidir.

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <transcodeSource>
      <clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>video-part1.mp4</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>video-part1.mp4</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
      </clipList>
    </transcodeSource>
    <setRuntimeProperties>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

Bu özellik tooname hello çıktı dosyaları 'İfadelerin' kullanarak toospecify /primarySourceFile toouse istediğiniz sonra hello küçük liste XML bir özellik olarak geçirme öneririz *sonra* hello /primarySourceFile özelliği, tooavoid Merhaba sahip küçük listesi hello /primarySourceFile ayarıyla geçersiz.

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="c:\temp\start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>c:\temp\start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>c:\temp\start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

Ek çerçeve doğru kırpma ile:

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <trim>
              <inPoint fps="25">00:00:05:24</inPoint>
              <outPoint fps="25">00:00:10:24</outPoint>
            </trim>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <trim>
              <inPoint fps="25">00:00:05:24</inPoint>
              <outPoint fps="25">00:00:10:24</outPoint>
            </trim>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

## <a name="example-1--overlay-an-image-on-top-of-hello-video"></a>Örnek 1: bir görüntü hello video en üstünde yer paylaşımı

### <a name="presentation"></a>Sunu
Hello video kodlanmış sırada hello giriş video logosu görüntüde toooverlay istediğiniz bir örneği göz önünde bulundurun. Bu örnekte, hello giriş video "Microsoft_HoloLens_Possibilities_816p24.mp4" olarak adlandırılır ve hello logosu "logo.png" olarak adlandırılır. Merhaba aşağıdaki adımları gerçekleştirmeniz gerekir:

* Bir iş akışı varlık ile Merhaba iş akışı dosyası oluşturun (Merhaba aşağıdaki örneğine bakın).
* İki dosya içeren bir medya varlık, oluşturma: birincil dosya ve MyLogo.png hello gibi MyInputVideo.mp4.
* Bir görev toohello Medya Kodlayıcısı Premium iş akışı medya hello yukarıdaki işlemcisi giriş varlıklar göndermek ve yapılandırma dizesi aşağıdaki hello belirtin.

Yapılandırma:

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="/primarySourceFile" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

Merhaba yukarıdaki örnekte, hello video dosyası hello adını toohello ortam dosyası girişi bileşeni ve hello primarySourceFile özelliği gönderilir. Merhaba logo dosyası Hello adını tooanother bağlı toohello grafik katmana bileşeni ortam dosyası girişi gönderilir.

> [!NOTE]
> Merhaba video dosyası adı toohello primarySourceFile özelliği gönderilir. Bunun nedeni Hello toouse hello iş akışındaki ifadeler, örneğin kullanarak hello doğru çıktı dosyası adı oluşturmak için bu bir özelliktir.

### <a name="step-by-step-workflow-creation"></a>Adım adım iş akışı oluşturma
İki dosya girdi olarak alır bir iş akışı hello adımları toocreate şunlardır: bir video ve görüntü. Merhaba görüntü hello video üstünde bulunacaktır.

Açık **iş akışı Tasarımcısı** seçip **dosya** > **yeni çalışma alanı** > **kodlamasını şeması**.

Merhaba yeni iş akışı üç öğeleri gösterir:

* Birincil kaynak dosyası
* Küçük resim listesi XML'i
* Çıkış dosyası/varlık  

![Yeni bir kodlama iş akışı](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture9_empty.png)

*Yeni bir kodlama iş akışı*

Sipariş tooaccept hello giriş medya dosyasında bir medya dosyası giriş bileşeni ekleyerek başlayın. tooadd bileşen toohello iş akışı hello deposu arama kutusuna aramanız ve istenen hello girişi hello Tasarımcı bölmesine sürükleyin.

Ardından, iş akışınızı tasarlamak için kullanılan hello video dosyası toobe ekleyin. Bu nedenle, toodo hello arka plan bölmesi iş akışı Tasarımcısı'nda ve hello sağ özellik bölmesinde hello birincil kaynak dosya özelliği arayın. Merhaba klasör simgesine tıklayın ve hello uygun video dosyası seçin.

![Birincil dosya kaynağı](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture10_primaryfile.png)

*Birincil dosya kaynağı*

Ardından, hello ortam dosyası girişi bileşeninde hello video dosyası belirtin.   

![Medya dosya giriş kaynağı](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture11_mediafileinput.png)

*Medya dosya giriş kaynağı*

Bu yapılır hemen hello medya dosyası giriş bileşen hello dosyasını inceleyin ve onu Denetlenmekte kendi çıktı PIN'ler tooreflect hello dosyasını doldurun.

Merhaba sonraki tooadd bir "Video veri türü güncelleştirici" toospecify hello renk alanı tooRec.709 adımdır. Bir "Video biçimi tooData düzeni/Düzen türü ayarlanan dönüştürücü" ekleme yapılandırılabilir düzlemsel =. Bu hello katmana bileşen kaynağı olarak alınabilir hello video akışına tooa biçimi dönüştürür.

![Video veri türü güncelleştirici ve biçimine dönüştürücü](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter.png)

*Video veri türü güncelleştirici ve biçimine dönüştürücü*

![Düzen türü yapılandırılabilir düzlemsel =](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter2.png)

*Düzen yapılandırılabilir düzlemsel türüdür*

Ardından, bir Video yer paylaşımı bileşen ekleyin ve hello (sıkıştırılmamış) video PIN toohello (sıkıştırılmamış) video PIN hello medya dosyası giriş bağlanın.

Başka bir medya dosyası girdisi (tooload hello logo dosyası) eklemek, bu bileşeni tıklatın ve çok yeniden adlandırma "Medya dosyası giriş logosu" ve hello dosya özelliğinde bir görüntü (örneğin bir .png dosyası) seçin. Merhaba sıkıştırılmamış görüntü PIN toohello sıkıştırılmamış görüntü PIN hello katmana bağlanın.

![Bir katmana bileşeni ve görüntü dosyası kaynağı](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture13_overlay.png)

*Bir katmana bileşeni ve görüntü dosyası kaynağı*

Toomodify hello hello video hello logosu konumunu istiyorsanız (örneğin, tooposition isteyebilirsiniz, hello üst dışına yüzde 10 sol köşe hello video), Temizle hello "El ile giriş" onay kutusunu. Bir medya dosyası giriş tooprovide hello logo dosyası toohello katmana bileşen kullanıldığı için bunu yapabilirsiniz.

![Bir katmana konumu](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture14_overlay_position.png)

*Bir katmana konumu*

tooencode video akışına tooH.264 Merhaba, hello AVC Video Kodlayıcısı ve AAC Kodlayıcı bileşenleri toohello Tasarımcı yüzeyine ekleyin. Merhaba PIN'ler bağlayın.
Merhaba AAC Kodlayıcısı kurma ayarlamak ve ses biçimi dönüştürme/hazır seçin: 2.0 (M, R).

![Ses ve görüntü Kodlayıcıları](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture15_encoders.png)

*Ses ve görüntü Kodlayıcıları*

Şimdi hello ekleyin **ISO Mpeg-4 çoğaltıcı** ve **dosya çıktısı** bileşenleri ve gösterildiği gibi hello PIN'ler bağlanın.

![Çoğaltıcı MP4 ve dosya çıktısı](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture16_mp4output.png)

*Çoğaltıcı MP4 ve dosya çıktısı*

Merhaba çıktı dosyası için tooset hello adı gerekir. Merhaba tıklatın **dosya çıktısı** bileşeni ve düzenleme hello ifade hello dosyası için:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_withoverlay.mp4

![Dosya çıktı adı](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture17_filenameoutput.png)

*Dosya çıktı adı*

Merhaba iş akışını çalıştırmak yerel olarak düzgün çalışmasını toocheck.

Sona erdikten sonra Azure Media Services çalıştırabilirsiniz.

İlk olarak, bir varlıkla Azure Media Services iki dosyada hazırlayın: hello video dosyası ve hello logosu. Merhaba .NET veya REST API'yi kullanarak bunu yapabilirsiniz. Ayrıca hello Azure portal kullanarak bunu yapabilirsiniz veya [Azure Media Services Gezgini](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).

Bu öğretici şunların nasıl yapıldığını gösterir AMSE ile toomanage varlıklar. İki yolu tooadd dosyaları tooan varlık vardır:

* Yerel bir klasör oluşturun, içinde hello iki dosyaları kopyalayın ve sürükleyip hello klasörü toohello **varlık** sekmesi.
* Bir varlık olarak Hello video dosyası yükleyin, hello varlık bilgilerini görüntülemek, toohello dosyaları sekmesine gidin ve bir ek (logosu) dosyasını karşıya yükleyin.

> [!NOTE]
> Emin tooset hello varlık (Merhaba ana video dosyası) bir birincil dosya oluşturun.

![AMSE varlık dosyaları](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture18_assetinamse.png)

*AMSE varlık dosyaları*

Merhaba varlık seçip tooencode Premium Kodlayıcı ile. Merhaba iş akışı karşıya yükleyin ve onu seçin.

Merhaba düğmesi toopass veri toohello İşlemci'yi tıklatın ve aşağıdaki XML tooset hello çalışma zamanı özelliklere hello ekleyin:

![Premium Kodlayıcı AMSE içinde](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture19_amsepremium.png)

*Premium Kodlayıcı AMSE içinde*

Ardından, XML verilerini aşağıdaki hello yapıştırın. Merhaba ortam dosyası girişi ve primarySourceFile için toospecify hello hello video dosyası adını gerekir. Merhaba adını hello dosya hello logo çok belirtin.

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="/primarySourceFile" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

![setRuntimeProperties](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture20_amsexmldata.png)

*setRuntimeProperties*

Merhaba .NET SDK'sı toocreate kullanın ve hello görevi çalıştırırsanız, bu XML verileri hello yapılandırma dizesi olarak geçirilen toobe sahiptir.

```c#
public ITask AddNew(string taskName, IMediaProcessor mediaProcessor, string configuration, TaskOptions options);
```

Merhaba işi tamamlandıktan sonra hello hello MP4 dosyasına varlık hello katmana görüntüler çıktı!

![Merhaba video yer paylaşımı](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture21_resultoverlay.png)

*Merhaba video yer paylaşımı*

Merhaba örnek iş akışından indirebilirsiniz [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).

## <a name="example-2--multiple-audio-language-encoding"></a>Örnek 2: Birden çok ses dil kodlaması

Kodlama workfkow bulunan birden çok ses dili örneği [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).

Bu klasör kullanılan tooencode bir MXF dosya tooa çoklu MP4 dosyaları varlık birden çok ses izleri sahip olabilen bir örnek iş akışı içerir.

Bu iş akışı bir ses parçası hello MXF dosyayı içeren varsayar; Merhaba ek ses izleri ayrı ses dosyaları (WAV veya MP4...) geçirilmesi gerekir.

tooencode, lütfen şu adımları izleyin:

* Bir Media Services varlık hello MXF dosya ve hello ses dosyalarını (0 too18 ses dosyalarını) oluşturun.
* Merhaba MXF dosyayı birincil dosya olarak ayarlandığından emin olun.
* Bir işi ve hello Premium iş akışı Kodlayıcı işlemci kullanarak bir görev oluşturun. (MultiMP4-1080 p-19audio-v1.workflow) sağlanan hello iş akışı kullanın.
* (Azure medya Hizmetleri Gezgini, kullanım hello "xml veri toohello iş akışı geçirmek" düğmesini kullanırsanız) hello setruntime.xml veri toohello görev geçirin.
  * Lütfen hello XML veri toospecify hello doğru dosya adları ve dilleri etiketleri güncelleştirin.
  * Merhaba iş akışı ses 1 tooAudio 18 adlı ses bileşenleri içerir.
  * RFC5646 hello dil etiketi için desteklenir.

```xml
<?xml version="1.0" encoding="utf-16"?>
<transcodeRequest>
  <setRuntimeProperties>
    <property propertyPath="Media File Input Video/filename" value="MainVideo.mxf" />
    <property propertyPath="Language/language_code" value="en" />
    <property propertyPath="/primarySourceFile" value="MainVideo.mxf" />
    <property propertyPath="Audio 1/Media File Input/filename" value="french-audio.wav" />
    <property propertyPath="Audio 1/Language/language_code" value="fr" />
    <property propertyPath="Audio 2/Media File Input/filename" value="german-audio.wav" />
    <property propertyPath="Audio 2/Language/language_code" value="de" />
    <property propertyPath="Audio 3/Media File Input/filename" value="japanese-audio.wav" />
    <property propertyPath="Audio 3/Language/language_code" value="ja" />
  </setRuntimeProperties>
</transcodeRequest>
```

* Kodlanmış hello varlık çoklu dil ses izleri içerir ve bu parçaları Azure Media Player seçilebilir olması gerekir.

## <a name="see-also"></a>Ayrıca bkz.
* [Premium Azure Media Services kodlama Tanıtımı](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)
* [Nasıl toouse Premium Azure Media Services kodlama](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)
* [Azure Media Services ile isteğe bağlı içerik kodlama](media-services-encode-asset.md#media-encoder-premium-workflow)
* [Medya Kodlayıcısı Premium iş akışı biçimleri ve codec bileşenleri](media-services-premium-workflow-encoder-formats.md)
* [Örnek iş akışı dosyaları](https://github.com/AzureMediaServicesSamples/Encoding-Presets/tree/master/VoD/MediaEncoderPremiumWorkfows)
* [Azure Media Services Gezgini aracı](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a>Media Services’i öğrenme yolları
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Geri bildirimde bulunma
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
