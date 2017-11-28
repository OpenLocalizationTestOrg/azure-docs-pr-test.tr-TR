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
# <a name="using-multiple-input-files-and-component-properties-with-premium-encoder"></a><span data-ttu-id="0f736-103">Premium Kodlayıcı ile birden fazla giriş dosyaları ve bileşen özellikleri kullanma</span><span class="sxs-lookup"><span data-stu-id="0f736-103">Using multiple input files and component properties with Premium Encoder</span></span>
## <a name="overview"></a><span data-ttu-id="0f736-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="0f736-104">Overview</span></span>
<span data-ttu-id="0f736-105">İçinde ihtiyacınız olabilecek toocustomize bileşen özellikleri senaryo vardır küçük listesi XML içeriğini belirtin veya hello görevle gönderdiğinizde birden çok giriş dosyaları göndermek **Medya Kodlayıcısı Premium iş akışı** medya işlemcisi.</span><span class="sxs-lookup"><span data-stu-id="0f736-105">There are scenarios in which you might need toocustomize component properties, specify Clip List XML content, or send multiple input files when you submit a task with hello **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="0f736-106">Bazı örnekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0f736-106">Some examples are:</span></span>

* <span data-ttu-id="0f736-107">Video metin kaplayan ve her giriş video için çalışma zamanında hello metin değeri (örneğin, geçerli tarih hello) ayarlama.</span><span class="sxs-lookup"><span data-stu-id="0f736-107">Overlaying text on video and setting hello text value (for example, hello current date) at runtime for each input video.</span></span>
* <span data-ttu-id="0f736-108">Merhaba küçük liste XML (toospecify. bir veya birkaç kaynak dosyaları, ile veya olmadan kırpma, vb.) özelleştirme.</span><span class="sxs-lookup"><span data-stu-id="0f736-108">Customizing hello Clip List XML (toospecify one or several source files, with or without trimming, etc.).</span></span>
* <span data-ttu-id="0f736-109">Merhaba video kodlanmış sırada hello giriş video logo görüntüsü üst üste getirme.</span><span class="sxs-lookup"><span data-stu-id="0f736-109">Overlaying a logo image on hello input video while hello video is encoded.</span></span>
* <span data-ttu-id="0f736-110">Birden çok ses dil kodlaması.</span><span class="sxs-lookup"><span data-stu-id="0f736-110">Multiple audio language encoding.</span></span>

<span data-ttu-id="0f736-111">toolet hello **Medya Kodlayıcısı Premium iş akışı** bilmeniz hello görev oluşturduğunuzda ya da birden çok giriş dosyaları göndermek bazı özellikler hello iş akışında değiştiriyorsunuz, içeren bir yapılandırma dizesi toouse sahip  **setRuntimeProperties** ve/veya **transcodeSource**.</span><span class="sxs-lookup"><span data-stu-id="0f736-111">toolet hello **Media Encoder Premium Workflow** know that you are changing some properties in hello workflow when you create hello task or send multiple input files, you have toouse a configuration string that contains **setRuntimeProperties** and/or **transcodeSource**.</span></span> <span data-ttu-id="0f736-112">Bu konuda açıklanmaktadır nasıl toouse bunları.</span><span class="sxs-lookup"><span data-stu-id="0f736-112">This topic explains how toouse them.</span></span>

## <a name="configuration-string-syntax"></a><span data-ttu-id="0f736-113">Yapılandırma dizesi sözdizimi</span><span class="sxs-lookup"><span data-stu-id="0f736-113">Configuration string syntax</span></span>
<span data-ttu-id="0f736-114">Merhaba yapılandırma dizesi tooset görev kodlama hello içinde şuna benzer bir XML belgesi kullanır:</span><span class="sxs-lookup"><span data-stu-id="0f736-114">hello configuration string tooset in hello encoding task uses an XML document that looks like this:</span></span>

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

<span data-ttu-id="0f736-115">Merhaba aşağıdaki hello XML yapılandırması bir dosyadan okur hello C# kod, kendisiyle güncelleştirme sağ video filename hello ve bir işi toohello görev geçirir:</span><span class="sxs-lookup"><span data-stu-id="0f736-115">hello following is hello C# code that reads hello XML configuration from a file, update it with hello right video filename and passes it toohello task in a job:</span></span>

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

## <a name="customizing-component-properties"></a><span data-ttu-id="0f736-116">Bileşen özelliklerini özelleştirme</span><span class="sxs-lookup"><span data-stu-id="0f736-116">Customizing component properties</span></span>
### <a name="property-with-a-simple-value"></a><span data-ttu-id="0f736-117">Basit bir değere sahip özelliği</span><span class="sxs-lookup"><span data-stu-id="0f736-117">Property with a simple value</span></span>
<span data-ttu-id="0f736-118">Bazı durumlarda bu kullanışlı toocustomize Medya Kodlayıcısı Premium iş akışı tarafından yürütülen toobe geçiyor hello iş akışı dosyası ile birlikte bir bileşen özelliği olur.</span><span class="sxs-lookup"><span data-stu-id="0f736-118">In some cases, it is useful toocustomize a component property together with hello workflow file that is going toobe executed by Media Encoder Premium Workflow.</span></span>

<span data-ttu-id="0f736-119">Bir iş akışı videolarınızı üzerinde yer paylaşımları metni tasarlanmış ve (örneğin, geçerli tarih hello) hello metni toobe kümesi çalışma zamanında gerektiği varsayalım.</span><span class="sxs-lookup"><span data-stu-id="0f736-119">Suppose you designed a workflow that overlays text on your videos, and hello text (for example, hello current date) is supposed toobe set at runtime.</span></span> <span data-ttu-id="0f736-120">Merhaba hello katmana bileşeninin hello metin özelliği için yeni değer olarak görev kodlama hello ayarlamak hello metin toobe göndererek bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f736-120">You can do this by sending hello text toobe set as hello new value for hello text property of hello overlay component from hello encoding task.</span></span> <span data-ttu-id="0f736-121">Merhaba iş akışında (örneğin, hello konumu veya hello katmana rengini, hello bit hızı hello AVC Kodlayıcı, vb.), bu mekanizma toochange bir bileşenin diğer özelliklerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f736-121">You can use this mechanism toochange other properties of a component in hello workflow (such as hello position or color of hello overlay, hello bitrate of hello AVC encoder, etc.).</span></span>

<span data-ttu-id="0f736-122">**setRuntimeProperties** kullanılan toooverride hello bileşenleri hello iş akışının bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="0f736-122">**setRuntimeProperties** is used toooverride a property in hello components of hello workflow.</span></span>

<span data-ttu-id="0f736-123">Örnek:</span><span class="sxs-lookup"><span data-stu-id="0f736-123">Example:</span></span>

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

### <a name="property-with-an-xml-value"></a><span data-ttu-id="0f736-124">XML değeri özelliği</span><span class="sxs-lookup"><span data-stu-id="0f736-124">Property with an XML value</span></span>
<span data-ttu-id="0f736-125">tooset bir XML değer bekler bir özellik kapsülleyen kullanarak `<![CDATA[ and ]]>`.</span><span class="sxs-lookup"><span data-stu-id="0f736-125">tooset a property that expects an XML value, encapsulate by using `<![CDATA[ and ]]>`.</span></span>

<span data-ttu-id="0f736-126">Örnek:</span><span class="sxs-lookup"><span data-stu-id="0f736-126">Example:</span></span>

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
> <span data-ttu-id="0f736-127">Tooput bir satır başı dönüş hemen sonra emin `<![CDATA[`.</span><span class="sxs-lookup"><span data-stu-id="0f736-127">Make sure not tooput a carriage return just after `<![CDATA[`.</span></span>

### <a name="propertypath-value"></a><span data-ttu-id="0f736-128">propertyPath değeri</span><span class="sxs-lookup"><span data-stu-id="0f736-128">propertyPath value</span></span>
<span data-ttu-id="0f736-129">Merhaba propertyPath Hello önceki örneklerde olduğu "/ medya dosya giriş/dosya adı" veya "/ inactiveTimeout" veya "clipListXml".</span><span class="sxs-lookup"><span data-stu-id="0f736-129">In hello previous examples, hello propertyPath was "/Media File Input/filename" or "/inactiveTimeout" or "clipListXml".</span></span>
<span data-ttu-id="0f736-130">Bu, genel olarak, hello bileşenin hello adı hello özelliğinin hello adı olduğundan.</span><span class="sxs-lookup"><span data-stu-id="0f736-130">This is, in general, hello name of hello component, then hello name of hello property.</span></span> <span data-ttu-id="0f736-131">Merhaba yolu daha fazla veya daha az düzeyleri gibi olabilir "/ primarySourceFile" (Merhaba özelliği hello hello iş akışı kökünde olduğundan) veya "/ Video işleme/grafiği katmana/opaklık" (bir grupta hello katmana olduğu için).</span><span class="sxs-lookup"><span data-stu-id="0f736-131">hello path can have more or fewer levels, like "/primarySourceFile" (because hello property is at hello root of hello workflow) or "/Video Processing/Graphic Overlay/Opacity" (because hello Overlay is in a group).</span></span>    

<span data-ttu-id="0f736-132">toocheck hello yolu ve özellik adını, hemen her özelliğin kullanım hello eylem düğmesi.</span><span class="sxs-lookup"><span data-stu-id="0f736-132">toocheck hello path and property name, use hello action button that is immediately beside each property.</span></span> <span data-ttu-id="0f736-133">Bu eylem düğmesini tıklatın ve seçin **Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="0f736-133">You can click this action button and select **Edit**.</span></span> <span data-ttu-id="0f736-134">Bu, hello gerçek gösterir adı hello özelliğinin ve hemen üstünde, ad alanı hello.</span><span class="sxs-lookup"><span data-stu-id="0f736-134">This will show you hello actual name of hello property, and immediately above it, hello namespace.</span></span>

![Eylem/Düzenle](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture6_actionedit.png)

![Özellik](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture7_viewproperty.png)

## <a name="multiple-input-files"></a><span data-ttu-id="0f736-137">Birden çok giriş dosyaları</span><span class="sxs-lookup"><span data-stu-id="0f736-137">Multiple input files</span></span>
<span data-ttu-id="0f736-138">Her görev toohello gönderme **Medya Kodlayıcısı Premium iş akışı** iki varlıklar gerektirir:</span><span class="sxs-lookup"><span data-stu-id="0f736-138">Each task that you submit toohello **Media Encoder Premium Workflow** requires two assets:</span></span>

* <span data-ttu-id="0f736-139">Merhaba ilk biridir bir *iş akışı varlık* bir iş akışı dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="0f736-139">hello first one is a *Workflow Asset* that contains a workflow file.</span></span> <span data-ttu-id="0f736-140">Hello kullanarak iş akışı dosyalarını tasarlayabilirsiniz [iş akışı Tasarımcısı](media-services-workflow-designer.md).</span><span class="sxs-lookup"><span data-stu-id="0f736-140">You can design workflow files by using hello [Workflow Designer](media-services-workflow-designer.md).</span></span>
* <span data-ttu-id="0f736-141">Merhaba ikincisi olan bir *medya varlık* tooencode istediğiniz hello medya dosyaları içerir.</span><span class="sxs-lookup"><span data-stu-id="0f736-141">hello second one is a *Media Asset* that contains hello media file(s) that you want tooencode.</span></span>

<span data-ttu-id="0f736-142">Ne zaman size göndererek birden çok medya dosyaları toohello **Medya Kodlayıcısı Premium iş akışı** encoder kısıtlamaları aşağıdaki hello Uygula:</span><span class="sxs-lookup"><span data-stu-id="0f736-142">When you're sending multiple media files toohello **Media Encoder Premium Workflow** encoder, hello following constraints apply:</span></span>

* <span data-ttu-id="0f736-143">Tüm hello medya dosyaları bulunmalıdır hello aynı *medya varlık*.</span><span class="sxs-lookup"><span data-stu-id="0f736-143">All hello media files must be in hello same *Media Asset*.</span></span> <span data-ttu-id="0f736-144">Birden çok medya varlıkları kullanma desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="0f736-144">Using multiple Media Assets is not supported.</span></span>
* <span data-ttu-id="0f736-145">Bu medya varlık hello birincil dosya ayarlamanız gerekir (İdeal olarak, bu hello olan Kodlayıcı hello ana video dosyası tooprocess sorulan).</span><span class="sxs-lookup"><span data-stu-id="0f736-145">You must set hello primary file in this Media Asset (ideally, this is hello main video file that hello encoder is asked tooprocess).</span></span>
* <span data-ttu-id="0f736-146">Merhaba içeren gerekli toopass yapılandırma verilerini olduğu **setRuntimeProperties** ve/veya **transcodeSource** öğesi toohello işlemci.</span><span class="sxs-lookup"><span data-stu-id="0f736-146">It is necessary toopass configuration data that includes hello **setRuntimeProperties** and/or **transcodeSource** element toohello processor.</span></span>
  * <span data-ttu-id="0f736-147">**setRuntimeProperties** kullanılan toooverride hello filename özelliği ya da başka bir özellik hello iş akışının hello bileşenleri.</span><span class="sxs-lookup"><span data-stu-id="0f736-147">**setRuntimeProperties** is used toooverride hello filename property or another property in hello components of hello workflow.</span></span>
  * <span data-ttu-id="0f736-148">**transcodeSource** kullanılan toospecify hello küçük listesi XML içeriği değil.</span><span class="sxs-lookup"><span data-stu-id="0f736-148">**transcodeSource** is used toospecify hello Clip List XML content.</span></span>

<span data-ttu-id="0f736-149">Bağlantıları hello iş akışı'nda:</span><span class="sxs-lookup"><span data-stu-id="0f736-149">Connections in hello workflow:</span></span>

* <span data-ttu-id="0f736-150">Bir veya birkaç ortam dosyası girişi bileşenleri kullanır ve toouse planı **setRuntimeProperties** toospecify hello dosya adı, ardından hello birincil dosya bileşen PIN toothem bağlamayın.</span><span class="sxs-lookup"><span data-stu-id="0f736-150">If you use one or several Media File Input components and plan toouse **setRuntimeProperties** toospecify hello file name, then do not connect hello primary file component pin toothem.</span></span> <span data-ttu-id="0f736-151">Merhaba birincil dosya nesnesi ve hello medya dosyası Input(s) arasında bağlantı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="0f736-151">Make sure that there is no connection between hello primary file object and hello Media File Input(s).</span></span>
* <span data-ttu-id="0f736-152">Toouse küçük liste XML ve bir medya kaynağı bileşen tercih ederseniz, ardından, her ikisi de birbirine bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f736-152">If you prefer toouse Clip List XML and one Media Source component, then you can connect both together.</span></span>

![Hiçbir bağlantısından birincil kaynak dosya tooMedia dosya giriş](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture0_nopin.png)

<span data-ttu-id="0f736-154">*SetRuntimeProperties tooset hello filename özelliğini kullanırsanız, hello birincil dosya tooMedia dosya giriş bileşenleri hiçbir bağlantısı yoktur.*</span><span class="sxs-lookup"><span data-stu-id="0f736-154">*There is no connection from hello primary file tooMedia File Input component(s) if you use setRuntimeProperties tooset hello filename property.*</span></span>

![Küçük resim listesi XML tooClip kaynak listesi bağlantısından](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture1_pincliplist.png)

<span data-ttu-id="0f736-156">*Küçük resim listesi XML tooMedia kaynak bağlanabilir ve transcodeSource kullanabilirsiniz.*</span><span class="sxs-lookup"><span data-stu-id="0f736-156">*You can connect Clip List XML tooMedia Source and use transcodeSource.*</span></span>

### <a name="clip-list-xml-customization"></a><span data-ttu-id="0f736-157">Liste XML özelleştirmesi Kırp</span><span class="sxs-lookup"><span data-stu-id="0f736-157">Clip List XML customization</span></span>
<span data-ttu-id="0f736-158">Kullanarak çalışma zamanında hello akışında hello küçük liste XML belirtebilirsiniz **transcodeSource** hello yapılandırmasında XML dizesi.</span><span class="sxs-lookup"><span data-stu-id="0f736-158">You can specify hello Clip List XML in hello workflow at runtime by using **transcodeSource** in hello configuration string XML.</span></span> <span data-ttu-id="0f736-159">Bu hello küçük liste XML PIN bağlı toobe toohello medya kaynağı bileşen hello iş akışında gereklidir.</span><span class="sxs-lookup"><span data-stu-id="0f736-159">This requires hello Clip List XML pin toobe connected toohello Media Source component in hello workflow.</span></span>

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

<span data-ttu-id="0f736-160">Bu özellik tooname hello çıktı dosyaları 'İfadelerin' kullanarak toospecify /primarySourceFile toouse istediğiniz sonra hello küçük liste XML bir özellik olarak geçirme öneririz *sonra* hello /primarySourceFile özelliği, tooavoid Merhaba sahip küçük listesi hello /primarySourceFile ayarıyla geçersiz.</span><span class="sxs-lookup"><span data-stu-id="0f736-160">If you want toospecify /primarySourceFile toouse this property tooname hello output files by using 'Expressions', then we recommend passing hello Clip List XML as a property *after* hello /primarySourceFile property, tooavoid having hello Clip List be overridden by hello /primarySourceFile setting.</span></span>

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

<span data-ttu-id="0f736-161">Ek çerçeve doğru kırpma ile:</span><span class="sxs-lookup"><span data-stu-id="0f736-161">With additional frame-accurate trimming:</span></span>

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

## <a name="example-1--overlay-an-image-on-top-of-hello-video"></a><span data-ttu-id="0f736-162">Örnek 1: bir görüntü hello video en üstünde yer paylaşımı</span><span class="sxs-lookup"><span data-stu-id="0f736-162">Example 1 : Overlay an image on top of hello video</span></span>

### <a name="presentation"></a><span data-ttu-id="0f736-163">Sunu</span><span class="sxs-lookup"><span data-stu-id="0f736-163">Presentation</span></span>
<span data-ttu-id="0f736-164">Hello video kodlanmış sırada hello giriş video logosu görüntüde toooverlay istediğiniz bir örneği göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="0f736-164">Consider an example in which you want toooverlay a logo image on hello input video while hello video is encoded.</span></span> <span data-ttu-id="0f736-165">Bu örnekte, hello giriş video "Microsoft_HoloLens_Possibilities_816p24.mp4" olarak adlandırılır ve hello logosu "logo.png" olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="0f736-165">In this example, hello input video is named "Microsoft_HoloLens_Possibilities_816p24.mp4" and hello logo is named "logo.png".</span></span> <span data-ttu-id="0f736-166">Merhaba aşağıdaki adımları gerçekleştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="0f736-166">You should perform hello following steps:</span></span>

* <span data-ttu-id="0f736-167">Bir iş akışı varlık ile Merhaba iş akışı dosyası oluşturun (Merhaba aşağıdaki örneğine bakın).</span><span class="sxs-lookup"><span data-stu-id="0f736-167">Create a Workflow Asset with hello workflow file (see hello following example).</span></span>
* <span data-ttu-id="0f736-168">İki dosya içeren bir medya varlık, oluşturma: birincil dosya ve MyLogo.png hello gibi MyInputVideo.mp4.</span><span class="sxs-lookup"><span data-stu-id="0f736-168">Create a Media Asset, which contains two files: MyInputVideo.mp4 as hello primary file and MyLogo.png.</span></span>
* <span data-ttu-id="0f736-169">Bir görev toohello Medya Kodlayıcısı Premium iş akışı medya hello yukarıdaki işlemcisi giriş varlıklar göndermek ve yapılandırma dizesi aşağıdaki hello belirtin.</span><span class="sxs-lookup"><span data-stu-id="0f736-169">Send a task toohello Media Encoder Premium Workflow media processor with hello above input assets and specify hello following configuration string.</span></span>

<span data-ttu-id="0f736-170">Yapılandırma:</span><span class="sxs-lookup"><span data-stu-id="0f736-170">Configuration:</span></span>

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

<span data-ttu-id="0f736-171">Merhaba yukarıdaki örnekte, hello video dosyası hello adını toohello ortam dosyası girişi bileşeni ve hello primarySourceFile özelliği gönderilir.</span><span class="sxs-lookup"><span data-stu-id="0f736-171">In hello example above, hello name of hello video file is sent toohello Media File Input component and hello primarySourceFile property.</span></span> <span data-ttu-id="0f736-172">Merhaba logo dosyası Hello adını tooanother bağlı toohello grafik katmana bileşeni ortam dosyası girişi gönderilir.</span><span class="sxs-lookup"><span data-stu-id="0f736-172">hello name of hello logo file is sent tooanother Media File Input that is connected toohello graphic overlay component.</span></span>

> [!NOTE]
> <span data-ttu-id="0f736-173">Merhaba video dosyası adı toohello primarySourceFile özelliği gönderilir.</span><span class="sxs-lookup"><span data-stu-id="0f736-173">hello video file name is sent toohello primarySourceFile property.</span></span> <span data-ttu-id="0f736-174">Bunun nedeni Hello toouse hello iş akışındaki ifadeler, örneğin kullanarak hello doğru çıktı dosyası adı oluşturmak için bu bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="0f736-174">hello reason for this is toouse this property in hello workflow for building hello correct output file name using Expressions, for example.</span></span>

### <a name="step-by-step-workflow-creation"></a><span data-ttu-id="0f736-175">Adım adım iş akışı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0f736-175">Step-by-step workflow creation</span></span>
<span data-ttu-id="0f736-176">İki dosya girdi olarak alır bir iş akışı hello adımları toocreate şunlardır: bir video ve görüntü.</span><span class="sxs-lookup"><span data-stu-id="0f736-176">Here are hello steps toocreate a workflow that takes two files as input: a video and an image.</span></span> <span data-ttu-id="0f736-177">Merhaba görüntü hello video üstünde bulunacaktır.</span><span class="sxs-lookup"><span data-stu-id="0f736-177">It will overlay hello image on top of hello video.</span></span>

<span data-ttu-id="0f736-178">Açık **iş akışı Tasarımcısı** seçip **dosya** > **yeni çalışma alanı** > **kodlamasını şeması**.</span><span class="sxs-lookup"><span data-stu-id="0f736-178">Open **Workflow Designer** and select **File** > **New Workspace** > **Transcode Blueprint**.</span></span>

<span data-ttu-id="0f736-179">Merhaba yeni iş akışı üç öğeleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="0f736-179">hello new workflow shows three elements:</span></span>

* <span data-ttu-id="0f736-180">Birincil kaynak dosyası</span><span class="sxs-lookup"><span data-stu-id="0f736-180">Primary Source File</span></span>
* <span data-ttu-id="0f736-181">Küçük resim listesi XML'i</span><span class="sxs-lookup"><span data-stu-id="0f736-181">Clip List XML</span></span>
* <span data-ttu-id="0f736-182">Çıkış dosyası/varlık</span><span class="sxs-lookup"><span data-stu-id="0f736-182">Output File/Asset</span></span>  

![Yeni bir kodlama iş akışı](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture9_empty.png)

<span data-ttu-id="0f736-184">*Yeni bir kodlama iş akışı*</span><span class="sxs-lookup"><span data-stu-id="0f736-184">*New Encoding Workflow*</span></span>

<span data-ttu-id="0f736-185">Sipariş tooaccept hello giriş medya dosyasında bir medya dosyası giriş bileşeni ekleyerek başlayın.</span><span class="sxs-lookup"><span data-stu-id="0f736-185">In order tooaccept hello input media file, start with adding a Media File Input component.</span></span> <span data-ttu-id="0f736-186">tooadd bileşen toohello iş akışı hello deposu arama kutusuna aramanız ve istenen hello girişi hello Tasarımcı bölmesine sürükleyin.</span><span class="sxs-lookup"><span data-stu-id="0f736-186">tooadd a component toohello workflow, look for it in hello Repository search box and drag hello desired entry onto hello designer pane.</span></span>

<span data-ttu-id="0f736-187">Ardından, iş akışınızı tasarlamak için kullanılan hello video dosyası toobe ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0f736-187">Next, add hello video file toobe used for designing your workflow.</span></span> <span data-ttu-id="0f736-188">Bu nedenle, toodo hello arka plan bölmesi iş akışı Tasarımcısı'nda ve hello sağ özellik bölmesinde hello birincil kaynak dosya özelliği arayın.</span><span class="sxs-lookup"><span data-stu-id="0f736-188">toodo so, click hello background pane in Workflow Designer and look for hello Primary Source File property on hello right-hand property pane.</span></span> <span data-ttu-id="0f736-189">Merhaba klasör simgesine tıklayın ve hello uygun video dosyası seçin.</span><span class="sxs-lookup"><span data-stu-id="0f736-189">Click hello folder icon and select hello appropriate video file.</span></span>

![Birincil dosya kaynağı](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture10_primaryfile.png)

<span data-ttu-id="0f736-191">*Birincil dosya kaynağı*</span><span class="sxs-lookup"><span data-stu-id="0f736-191">*Primary File Source*</span></span>

<span data-ttu-id="0f736-192">Ardından, hello ortam dosyası girişi bileşeninde hello video dosyası belirtin.</span><span class="sxs-lookup"><span data-stu-id="0f736-192">Next, specify hello video file in hello Media File Input component.</span></span>   

![Medya dosya giriş kaynağı](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture11_mediafileinput.png)

<span data-ttu-id="0f736-194">*Medya dosya giriş kaynağı*</span><span class="sxs-lookup"><span data-stu-id="0f736-194">*Media File Input Source*</span></span>

<span data-ttu-id="0f736-195">Bu yapılır hemen hello medya dosyası giriş bileşen hello dosyasını inceleyin ve onu Denetlenmekte kendi çıktı PIN'ler tooreflect hello dosyasını doldurun.</span><span class="sxs-lookup"><span data-stu-id="0f736-195">As soon as this is done, hello Media File Input component will inspect hello file and populate its output pins tooreflect hello file that it inspected.</span></span>

<span data-ttu-id="0f736-196">Merhaba sonraki tooadd bir "Video veri türü güncelleştirici" toospecify hello renk alanı tooRec.709 adımdır.</span><span class="sxs-lookup"><span data-stu-id="0f736-196">hello next step is tooadd a "Video Data Type Updater" toospecify hello color space tooRec.709.</span></span> <span data-ttu-id="0f736-197">Bir "Video biçimi tooData düzeni/Düzen türü ayarlanan dönüştürücü" ekleme yapılandırılabilir düzlemsel =.</span><span class="sxs-lookup"><span data-stu-id="0f736-197">Add a "Video Format Converter" that is set tooData Layout/Layout type = Configurable Planar.</span></span> <span data-ttu-id="0f736-198">Bu hello katmana bileşen kaynağı olarak alınabilir hello video akışına tooa biçimi dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="0f736-198">This will convert hello video stream tooa format that can be taken as a source of hello overlay component.</span></span>

![Video veri türü güncelleştirici ve biçimine dönüştürücü](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter.png)

<span data-ttu-id="0f736-200">*Video veri türü güncelleştirici ve biçimine dönüştürücü*</span><span class="sxs-lookup"><span data-stu-id="0f736-200">*Video Data Type Updater and Format Converter*</span></span>

![Düzen türü yapılandırılabilir düzlemsel =](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter2.png)

<span data-ttu-id="0f736-202">*Düzen yapılandırılabilir düzlemsel türüdür*</span><span class="sxs-lookup"><span data-stu-id="0f736-202">*Layout type is Configurable Planar*</span></span>

<span data-ttu-id="0f736-203">Ardından, bir Video yer paylaşımı bileşen ekleyin ve hello (sıkıştırılmamış) video PIN toohello (sıkıştırılmamış) video PIN hello medya dosyası giriş bağlanın.</span><span class="sxs-lookup"><span data-stu-id="0f736-203">Next, add a Video Overlay component and connect hello (uncompressed) video pin toohello (uncompressed) video pin of hello media file input.</span></span>

<span data-ttu-id="0f736-204">Başka bir medya dosyası girdisi (tooload hello logo dosyası) eklemek, bu bileşeni tıklatın ve çok yeniden adlandırma "Medya dosyası giriş logosu" ve hello dosya özelliğinde bir görüntü (örneğin bir .png dosyası) seçin.</span><span class="sxs-lookup"><span data-stu-id="0f736-204">Add another Media File Input (tooload hello logo file), click on this component and rename it too"Media File Input Logo", and select an image (a .png file for example) in hello file property.</span></span> <span data-ttu-id="0f736-205">Merhaba sıkıştırılmamış görüntü PIN toohello sıkıştırılmamış görüntü PIN hello katmana bağlanın.</span><span class="sxs-lookup"><span data-stu-id="0f736-205">Connect hello Uncompressed image pin toohello Uncompressed image pin of hello overlay.</span></span>

![Bir katmana bileşeni ve görüntü dosyası kaynağı](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture13_overlay.png)

<span data-ttu-id="0f736-207">*Bir katmana bileşeni ve görüntü dosyası kaynağı*</span><span class="sxs-lookup"><span data-stu-id="0f736-207">*Overlay component and image file source*</span></span>

<span data-ttu-id="0f736-208">Toomodify hello hello video hello logosu konumunu istiyorsanız (örneğin, tooposition isteyebilirsiniz, hello üst dışına yüzde 10 sol köşe hello video), Temizle hello "El ile giriş" onay kutusunu.</span><span class="sxs-lookup"><span data-stu-id="0f736-208">If you want toomodify hello position of hello logo on hello video (for example, you might want tooposition it at 10 percent off of hello top left corner of hello video), clear hello "Manual Input" check box.</span></span> <span data-ttu-id="0f736-209">Bir medya dosyası giriş tooprovide hello logo dosyası toohello katmana bileşen kullanıldığı için bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f736-209">You can do this because you are using a Media File Input tooprovide hello logo file toohello overlay component.</span></span>

![Bir katmana konumu](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture14_overlay_position.png)

<span data-ttu-id="0f736-211">*Bir katmana konumu*</span><span class="sxs-lookup"><span data-stu-id="0f736-211">*Overlay position*</span></span>

<span data-ttu-id="0f736-212">tooencode video akışına tooH.264 Merhaba, hello AVC Video Kodlayıcısı ve AAC Kodlayıcı bileşenleri toohello Tasarımcı yüzeyine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0f736-212">tooencode hello video stream tooH.264, add hello AVC Video Encoder and AAC encoder components toohello designer surface.</span></span> <span data-ttu-id="0f736-213">Merhaba PIN'ler bağlayın.</span><span class="sxs-lookup"><span data-stu-id="0f736-213">Connect hello pins.</span></span>
<span data-ttu-id="0f736-214">Merhaba AAC Kodlayıcısı kurma ayarlamak ve ses biçimi dönüştürme/hazır seçin: 2.0 (M, R).</span><span class="sxs-lookup"><span data-stu-id="0f736-214">Set up hello AAC encoder and select Audio Format Conversion/Preset : 2.0 (L, R).</span></span>

![Ses ve görüntü Kodlayıcıları](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture15_encoders.png)

<span data-ttu-id="0f736-216">*Ses ve görüntü Kodlayıcıları*</span><span class="sxs-lookup"><span data-stu-id="0f736-216">*Audio and Video Encoders*</span></span>

<span data-ttu-id="0f736-217">Şimdi hello ekleyin **ISO Mpeg-4 çoğaltıcı** ve **dosya çıktısı** bileşenleri ve gösterildiği gibi hello PIN'ler bağlanın.</span><span class="sxs-lookup"><span data-stu-id="0f736-217">Now add hello **ISO Mpeg-4 Multiplexer** and **File Output** components and connect hello pins as shown.</span></span>

![Çoğaltıcı MP4 ve dosya çıktısı](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture16_mp4output.png)

<span data-ttu-id="0f736-219">*Çoğaltıcı MP4 ve dosya çıktısı*</span><span class="sxs-lookup"><span data-stu-id="0f736-219">*MP4 multiplexer and file output*</span></span>

<span data-ttu-id="0f736-220">Merhaba çıktı dosyası için tooset hello adı gerekir.</span><span class="sxs-lookup"><span data-stu-id="0f736-220">You need tooset hello name for hello output file.</span></span> <span data-ttu-id="0f736-221">Merhaba tıklatın **dosya çıktısı** bileşeni ve düzenleme hello ifade hello dosyası için:</span><span class="sxs-lookup"><span data-stu-id="0f736-221">Click hello **File Output** component and edit hello expression for hello file:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_withoverlay.mp4

![Dosya çıktı adı](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture17_filenameoutput.png)

<span data-ttu-id="0f736-223">*Dosya çıktı adı*</span><span class="sxs-lookup"><span data-stu-id="0f736-223">*File output name*</span></span>

<span data-ttu-id="0f736-224">Merhaba iş akışını çalıştırmak yerel olarak düzgün çalışmasını toocheck.</span><span class="sxs-lookup"><span data-stu-id="0f736-224">You can run hello workflow locally toocheck that it is running correctly.</span></span>

<span data-ttu-id="0f736-225">Sona erdikten sonra Azure Media Services çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f736-225">After it finishes, you can run it in Azure Media Services.</span></span>

<span data-ttu-id="0f736-226">İlk olarak, bir varlıkla Azure Media Services iki dosyada hazırlayın: hello video dosyası ve hello logosu.</span><span class="sxs-lookup"><span data-stu-id="0f736-226">First, prepare an asset in Azure Media Services with two files in it: hello video file and hello logo.</span></span> <span data-ttu-id="0f736-227">Merhaba .NET veya REST API'yi kullanarak bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f736-227">You can do this by using hello .NET or REST API.</span></span> <span data-ttu-id="0f736-228">Ayrıca hello Azure portal kullanarak bunu yapabilirsiniz veya [Azure Media Services Gezgini](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span><span class="sxs-lookup"><span data-stu-id="0f736-228">You can also do this by using hello Azure portal or [Azure Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span></span>

<span data-ttu-id="0f736-229">Bu öğretici şunların nasıl yapıldığını gösterir AMSE ile toomanage varlıklar.</span><span class="sxs-lookup"><span data-stu-id="0f736-229">This tutorial shows you how toomanage assets with AMSE.</span></span> <span data-ttu-id="0f736-230">İki yolu tooadd dosyaları tooan varlık vardır:</span><span class="sxs-lookup"><span data-stu-id="0f736-230">There are two ways tooadd files tooan asset:</span></span>

* <span data-ttu-id="0f736-231">Yerel bir klasör oluşturun, içinde hello iki dosyaları kopyalayın ve sürükleyip hello klasörü toohello **varlık** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="0f736-231">Create a local folder, copy hello two files in it, and drag and drop hello folder toohello **Asset** tab.</span></span>
* <span data-ttu-id="0f736-232">Bir varlık olarak Hello video dosyası yükleyin, hello varlık bilgilerini görüntülemek, toohello dosyaları sekmesine gidin ve bir ek (logosu) dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0f736-232">Upload hello video file as an asset, display hello asset information, go toohello files tab, and upload an additional file (logo).</span></span>

> [!NOTE]
> <span data-ttu-id="0f736-233">Emin tooset hello varlık (Merhaba ana video dosyası) bir birincil dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0f736-233">Make sure tooset a primary file in hello asset (hello main video file).</span></span>

![AMSE varlık dosyaları](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture18_assetinamse.png)

<span data-ttu-id="0f736-235">*AMSE varlık dosyaları*</span><span class="sxs-lookup"><span data-stu-id="0f736-235">*Asset files in AMSE*</span></span>

<span data-ttu-id="0f736-236">Merhaba varlık seçip tooencode Premium Kodlayıcı ile.</span><span class="sxs-lookup"><span data-stu-id="0f736-236">Select hello asset and choose tooencode it with Premium Encoder.</span></span> <span data-ttu-id="0f736-237">Merhaba iş akışı karşıya yükleyin ve onu seçin.</span><span class="sxs-lookup"><span data-stu-id="0f736-237">Upload hello workflow and select it.</span></span>

<span data-ttu-id="0f736-238">Merhaba düğmesi toopass veri toohello İşlemci'yi tıklatın ve aşağıdaki XML tooset hello çalışma zamanı özelliklere hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0f736-238">Click hello button toopass data toohello processor, and add hello following XML tooset hello runtime properties:</span></span>

![Premium Kodlayıcı AMSE içinde](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture19_amsepremium.png)

<span data-ttu-id="0f736-240">*Premium Kodlayıcı AMSE içinde*</span><span class="sxs-lookup"><span data-stu-id="0f736-240">*Premium Encoder in AMSE*</span></span>

<span data-ttu-id="0f736-241">Ardından, XML verilerini aşağıdaki hello yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="0f736-241">Then, paste hello following XML data.</span></span> <span data-ttu-id="0f736-242">Merhaba ortam dosyası girişi ve primarySourceFile için toospecify hello hello video dosyası adını gerekir.</span><span class="sxs-lookup"><span data-stu-id="0f736-242">You need toospecify hello name of hello video file for both hello Media File Input and primarySourceFile.</span></span> <span data-ttu-id="0f736-243">Merhaba adını hello dosya hello logo çok belirtin.</span><span class="sxs-lookup"><span data-stu-id="0f736-243">Specify hello name of hello file name for hello logo too.</span></span>

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

<span data-ttu-id="0f736-245">*setRuntimeProperties*</span><span class="sxs-lookup"><span data-stu-id="0f736-245">*setRuntimeProperties*</span></span>

<span data-ttu-id="0f736-246">Merhaba .NET SDK'sı toocreate kullanın ve hello görevi çalıştırırsanız, bu XML verileri hello yapılandırma dizesi olarak geçirilen toobe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="0f736-246">If you use hello .NET SDK toocreate and run hello task, this XML data has toobe passed as hello configuration string.</span></span>

```c#
public ITask AddNew(string taskName, IMediaProcessor mediaProcessor, string configuration, TaskOptions options);
```

<span data-ttu-id="0f736-247">Merhaba işi tamamlandıktan sonra hello hello MP4 dosyasına varlık hello katmana görüntüler çıktı!</span><span class="sxs-lookup"><span data-stu-id="0f736-247">After hello job is complete, hello MP4 file in hello output asset displays hello overlay!</span></span>

![Merhaba video yer paylaşımı](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture21_resultoverlay.png)

<span data-ttu-id="0f736-249">*Merhaba video yer paylaşımı*</span><span class="sxs-lookup"><span data-stu-id="0f736-249">*Overlay on hello video*</span></span>

<span data-ttu-id="0f736-250">Merhaba örnek iş akışından indirebilirsiniz [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span><span class="sxs-lookup"><span data-stu-id="0f736-250">You can download hello sample workflow from [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span></span>

## <a name="example-2--multiple-audio-language-encoding"></a><span data-ttu-id="0f736-251">Örnek 2: Birden çok ses dil kodlaması</span><span class="sxs-lookup"><span data-stu-id="0f736-251">Example 2 : Multiple audio language encoding</span></span>

<span data-ttu-id="0f736-252">Kodlama workfkow bulunan birden çok ses dili örneği [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).</span><span class="sxs-lookup"><span data-stu-id="0f736-252">An example of multiple audio language encoding workfkow is available in [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).</span></span>

<span data-ttu-id="0f736-253">Bu klasör kullanılan tooencode bir MXF dosya tooa çoklu MP4 dosyaları varlık birden çok ses izleri sahip olabilen bir örnek iş akışı içerir.</span><span class="sxs-lookup"><span data-stu-id="0f736-253">This folder contains a sample workflow which can be used tooencode a MXF file tooa multi MP4 files asset with multiple audio tracks.</span></span>

<span data-ttu-id="0f736-254">Bu iş akışı bir ses parçası hello MXF dosyayı içeren varsayar; Merhaba ek ses izleri ayrı ses dosyaları (WAV veya MP4...) geçirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="0f736-254">This workflow assumes that hello MXF file contains one audio track ; hello additional audio tracks should be passed as seperate audio files (WAV or MP4...).</span></span>

<span data-ttu-id="0f736-255">tooencode, lütfen şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="0f736-255">tooencode, please follow these steps:</span></span>

* <span data-ttu-id="0f736-256">Bir Media Services varlık hello MXF dosya ve hello ses dosyalarını (0 too18 ses dosyalarını) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0f736-256">Create a Media Services asset with hello MXF file and hello Audio files (0 too18 audio files).</span></span>
* <span data-ttu-id="0f736-257">Merhaba MXF dosyayı birincil dosya olarak ayarlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="0f736-257">Make sure that hello MXF file is set as a primary file.</span></span>
* <span data-ttu-id="0f736-258">Bir işi ve hello Premium iş akışı Kodlayıcı işlemci kullanarak bir görev oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0f736-258">Create a job and a task using hello Premium Workflow Encoder processor.</span></span> <span data-ttu-id="0f736-259">(MultiMP4-1080 p-19audio-v1.workflow) sağlanan hello iş akışı kullanın.</span><span class="sxs-lookup"><span data-stu-id="0f736-259">Use hello workflow provided (MultiMP4-1080p-19audio-v1.workflow).</span></span>
* <span data-ttu-id="0f736-260">(Azure medya Hizmetleri Gezgini, kullanım hello "xml veri toohello iş akışı geçirmek" düğmesini kullanırsanız) hello setruntime.xml veri toohello görev geçirin.</span><span class="sxs-lookup"><span data-stu-id="0f736-260">Pass hello setruntime.xml data toohello task (if you use Azure Media Services Explorer, use hello “pass xml data toohello workflow” button).</span></span>
  * <span data-ttu-id="0f736-261">Lütfen hello XML veri toospecify hello doğru dosya adları ve dilleri etiketleri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="0f736-261">Please update hello XML data toospecify hello correct file names and languages tags.</span></span>
  * <span data-ttu-id="0f736-262">Merhaba iş akışı ses 1 tooAudio 18 adlı ses bileşenleri içerir.</span><span class="sxs-lookup"><span data-stu-id="0f736-262">hello workflow has audio components named Audio 1 tooAudio 18.</span></span>
  * <span data-ttu-id="0f736-263">RFC5646 hello dil etiketi için desteklenir.</span><span class="sxs-lookup"><span data-stu-id="0f736-263">RFC5646 is supported for hello language tag.</span></span>

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

* <span data-ttu-id="0f736-264">Kodlanmış hello varlık çoklu dil ses izleri içerir ve bu parçaları Azure Media Player seçilebilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0f736-264">hello encoded asset will contain multi language audio tracks and these tracks should be selectable in Azure Media Player.</span></span>

## <a name="see-also"></a><span data-ttu-id="0f736-265">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="0f736-265">See also</span></span>
* [<span data-ttu-id="0f736-266">Premium Azure Media Services kodlama Tanıtımı</span><span class="sxs-lookup"><span data-stu-id="0f736-266">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="0f736-267">Nasıl toouse Premium Azure Media Services kodlama</span><span class="sxs-lookup"><span data-stu-id="0f736-267">How toouse Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="0f736-268">Azure Media Services ile isteğe bağlı içerik kodlama</span><span class="sxs-lookup"><span data-stu-id="0f736-268">Encoding on-demand content with Azure Media Services</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)
* [<span data-ttu-id="0f736-269">Medya Kodlayıcısı Premium iş akışı biçimleri ve codec bileşenleri</span><span class="sxs-lookup"><span data-stu-id="0f736-269">Media Encoder Premium Workflow formats and codecs</span></span>](media-services-premium-workflow-encoder-formats.md)
* [<span data-ttu-id="0f736-270">Örnek iş akışı dosyaları</span><span class="sxs-lookup"><span data-stu-id="0f736-270">Sample workflow files</span></span>](https://github.com/AzureMediaServicesSamples/Encoding-Presets/tree/master/VoD/MediaEncoderPremiumWorkfows)
* [<span data-ttu-id="0f736-271">Azure Media Services Gezgini aracı</span><span class="sxs-lookup"><span data-stu-id="0f736-271">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="0f736-272">Media Services’i öğrenme yolları</span><span class="sxs-lookup"><span data-stu-id="0f736-272">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="0f736-273">Geri bildirimde bulunma</span><span class="sxs-lookup"><span data-stu-id="0f736-273">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
