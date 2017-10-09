---
title: "Azure işlevleri için aaaStream Analytics gerçek zamanlı işleme | Microsoft Docs"
description: "Bir hizmet veri yolu kuyruğu toopopulate bir Azure Redis önbelleği Stream Analytics işi hello çıktısından toouse bir Azure işlevi nasıl bağlanacağını öğrenin."
keywords: "veri akışı, redis önbelleği, hizmet veri yolu kuyruğu"
services: stream-analytics
author: ryancrawcour
manager: jhubbard
documentationcenter: 
ms.assetid: d428bb33-4244-4001-b93d-c77bed816527
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/28/2017
ms.author: ryancraw
ms.openlocfilehash: 5ef4fe76c2cadf896a80eeaf421f010c315918af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostore-data-from-azure-stream-analytics-in-an-azure-redis-cache-using-azure-functions"></a><span data-ttu-id="f91ab-104">Nasıl bir Azure Redis Azure işlevleri kullanarak önbelleğinde Azure akış analizi toostore verileri</span><span class="sxs-lookup"><span data-stu-id="f91ab-104">How toostore data from Azure Stream Analytics in an Azure Redis Cache using Azure Functions</span></span>
<span data-ttu-id="f91ab-105">Azure Stream Analytics, hızlı bir şekilde geliştirmek ve düşük maliyetli çözümleri toogain gerçek zamanlı Öngörüler cihazlar, algılayıcılar, altyapı ve uygulamaları ya da veri dağıtmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="f91ab-105">Azure Stream Analytics lets you rapidly develop and deploy low-cost solutions toogain real-time insights from devices, sensors, infrastructure, and applications, or any stream of data.</span></span> <span data-ttu-id="f91ab-106">Gerçek zamanlı yönetim ve izleme, komut ve denetim, sahtekarlık algılama, bağlı araba ve çok daha fazlasını gibi çeşitli kullanım örnekleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="f91ab-106">It enables various use cases such as real-time management and monitoring, command and control, fraud detection, connected cars and many more.</span></span> <span data-ttu-id="f91ab-107">Bu tür birçok senaryoda, bir Azure Redis önbelleği gibi dağıtılmış veri deposuna Azure akış analizi tarafından yüzdelik toostore veri isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f91ab-107">In many such scenarios, you may want toostore data outputted by Azure Stream Analytics into a distributed data store such as an Azure Redis cache.</span></span>

<span data-ttu-id="f91ab-108">Telekomünikasyon şirket parçası olan varsayalım.</span><span class="sxs-lookup"><span data-stu-id="f91ab-108">Suppose you are part of a telecommunications company.</span></span> <span data-ttu-id="f91ab-109">Burada'ten gelen birden fazla çağrı hello aynı kimlik toodetect SIM sahtekarlık çalıştığınız, adresindeki aynı Merhaba, fakat coğrafi olarak farklı zaman konumları.</span><span class="sxs-lookup"><span data-stu-id="f91ab-109">You are trying toodetect SIM fraud where multiple calls coming from hello same identity, at hello same time, but in different geographically locations.</span></span> <span data-ttu-id="f91ab-110">Bir Azure Redis Önbelleği'nde tüm hello olası sahte telefon aramaları depolamanın görevli.</span><span class="sxs-lookup"><span data-stu-id="f91ab-110">You are tasked with storing all hello potential fraudulent phone calls in an Azure Redis cache.</span></span> <span data-ttu-id="f91ab-111">Bu Web Günlüğü'ndeki, nasıl kolayca göreviniz tamamlayabileceğiniz üzerinde size rehberlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="f91ab-111">In this blog, we provide guidance on how you can easily complete your task.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f91ab-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f91ab-112">Prerequisites</span></span>
<span data-ttu-id="f91ab-113">Tam hello [gerçek zamanlı sahtekarlık algılama] [ fraud-detection] ASA için gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="f91ab-113">Complete hello [Real-time Fraud Detection][fraud-detection] walk-through for ASA</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="f91ab-114">Mimarisine genel bakış</span><span class="sxs-lookup"><span data-stu-id="f91ab-114">Architecture Overview</span></span>
![Ekran görüntüsü mimarisi](./media/stream-analytics-functions-redis/architecture-overview.png)

<span data-ttu-id="f91ab-116">Şekil önceki hello gösterildiği gibi Stream Analytics giriş verisi toobe akış sorgulanan ve tooan çıktı gönderilen sağlar.</span><span class="sxs-lookup"><span data-stu-id="f91ab-116">As shown in hello preceding figure, Stream Analytics allows streaming input data toobe queried and sent tooan output.</span></span> <span data-ttu-id="f91ab-117">Azure işlevleri, Hello çıktıya dayalı, sonra herhangi bir tür olay tetikleyebilir.</span><span class="sxs-lookup"><span data-stu-id="f91ab-117">Based on hello output, Azure Functions can then trigger some type of event.</span></span> 

<span data-ttu-id="f91ab-118">Bu blogdaki Biz bu ardışık hello Azure işlevleri Bölümü'odak veya daha açık belirtmek gerekirse hello önbelleğine sahte verileri depolayan bir olay tetikleme hello.</span><span class="sxs-lookup"><span data-stu-id="f91ab-118">In this blog, we focus on hello Azure Functions part of this pipeline, or more specifically hello triggering of an event that stores fraudulent data into hello cache.</span></span>
<span data-ttu-id="f91ab-119">Merhaba tamamladıktan sonra [gerçek zamanlı sahtekarlık algılama] [ fraud-detection] öğretici, elinizde bir giriş (bir event hub), bir sorgu ve önceden yapılandırılmış ve çalışan bir çıkış (blob depolama).</span><span class="sxs-lookup"><span data-stu-id="f91ab-119">After completing hello [Real-time Fraud Detection][fraud-detection] tutorial, you have an input (an event hub), a query, and an output (blob storage) already configured and running.</span></span> <span data-ttu-id="f91ab-120">Bu Web Günlüğü'ndeki biz hello çıktı toouse bir hizmet veri yolu kuyruğu bunun yerine değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f91ab-120">In this blog, we change hello output toouse a Service Bus Queue instead.</span></span> <span data-ttu-id="f91ab-121">Bundan sonra size bir Azure işlevi toothis sıra bağlayın.</span><span class="sxs-lookup"><span data-stu-id="f91ab-121">After that, we connect an Azure Function toothis queue.</span></span> 

## <a name="create-and-connect-a-service-bus-queue-output"></a><span data-ttu-id="f91ab-122">Oluşturma ve bir hizmet veri yolu kuyruğu çıkış bağlama</span><span class="sxs-lookup"><span data-stu-id="f91ab-122">Create and connect a Service Bus Queue output</span></span>
<span data-ttu-id="f91ab-123">toocreate bir hizmet veri yolu kuyruğu adımları 1 ve 2'ın hello .NET bölümü [hizmet veri yolu kuyrukları ile çalışmaya başlama][servicebus-getstarted].</span><span class="sxs-lookup"><span data-stu-id="f91ab-123">toocreate a Service Bus Queue, follow steps 1 and 2 of hello .NET section in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span>
<span data-ttu-id="f91ab-124">Şimdi şimdi hello oluşturulduğu hello sıra toohello Stream Analytics işi bağlanmak önceki sahtekarlık algılama gözden geçirme.</span><span class="sxs-lookup"><span data-stu-id="f91ab-124">Now let's connect hello queue toohello Stream Analytics job that was created in hello earlier fraud detection walk-through.</span></span>

1. <span data-ttu-id="f91ab-125">Toohello Hello Azure portal, Git **çıkışları** seçin ve iş dikey **Ekle** hello sayfanın üst kısmındaki hello.</span><span class="sxs-lookup"><span data-stu-id="f91ab-125">In hello Azure portal, go toohello **Outputs** blade of your job and select **Add** at hello top of hello page.</span></span>
   
    ![Çıkış ekleme](./media/stream-analytics-functions-redis/adding-outputs.png)
2. <span data-ttu-id="f91ab-127">Seçin **hizmet veri yolu kuyruğu** hello olarak **havuzu** ve Merhaba ekranında hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="f91ab-127">Choose **Service Bus Queue** as hello **Sink** and follow hello instructions on hello screen.</span></span> <span data-ttu-id="f91ab-128">Olması emin toochoose hello ad alanı hello hizmet veri yolu kuyruğu oluşturduğunuz [hizmet veri yolu kuyrukları ile çalışmaya başlama][servicebus-getstarted].</span><span class="sxs-lookup"><span data-stu-id="f91ab-128">Be sure toochoose hello namespace of hello Service Bus Queue you created in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span> <span data-ttu-id="f91ab-129">İşiniz bittiğinde hello "sağ" düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f91ab-129">Click hello "right" button when you are finished.</span></span>
3. <span data-ttu-id="f91ab-130">Hello aşağıdaki değerleri belirtin:</span><span class="sxs-lookup"><span data-stu-id="f91ab-130">Specify hello following values:</span></span>
   
   * <span data-ttu-id="f91ab-131">**Olayı seri hale getirici biçimi**: JSON</span><span class="sxs-lookup"><span data-stu-id="f91ab-131">**Event Serializer Format**: JSON</span></span>
   * <span data-ttu-id="f91ab-132">**Kodlama**: UTF8</span><span class="sxs-lookup"><span data-stu-id="f91ab-132">**Encoding**: UTF8</span></span>
   * <span data-ttu-id="f91ab-133">**Biçim**: ayrılmış çizgi</span><span class="sxs-lookup"><span data-stu-id="f91ab-133">**FORMAT**: Line separated</span></span>
4. <span data-ttu-id="f91ab-134">Merhaba tıklatın **oluşturma** tooadd bu kaynak ve akış analizi toohello depolama hesabı başarıyla bağlanabildiğinizi tooverify düğme.</span><span class="sxs-lookup"><span data-stu-id="f91ab-134">Click hello **Create** button tooadd this source and tooverify that Stream Analytics can successfully connect toohello storage account.</span></span>
5. <span data-ttu-id="f91ab-135">Merhaba, **sorgu** sekmesinde, hello geçerli sorgu hello şununla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f91ab-135">In hello **Query** tab, replace hello current query with hello following.</span></span> <span data-ttu-id="f91ab-136">Değiştir * [YOUR hizmet veri yolu adı] * 3. adımda oluşturduğunuz hello çıkış ada sahip.</span><span class="sxs-lookup"><span data-stu-id="f91ab-136">Replace *[YOUR SERVICE BUS NAME] * with hello output name you created in step 3.</span></span> 
   
    ```    
   
        SELECT 
            System.Timestamp as Time, CS1.CallingIMSI, CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, CS1.SwitchNum as Switch1, CS2.SwitchNum as Switch2
   
        INTO [YOUR SERVICE BUS NAME]
   
        FROM CallStream CS1 TIMESTAMP BY CallRecTime
        JOIN CallStream CS2 TIMESTAMP BY CallRecTime
            ON CS1.CallingIMSI = CS2.CallingIMSI AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5
   
        WHERE CS1.SwitchNum != CS2.SwitchNum
   
    ```

## <a name="create-an-azure-redis-cache"></a><span data-ttu-id="f91ab-137">Azure Redis Cache oluşturma</span><span class="sxs-lookup"><span data-stu-id="f91ab-137">Create an Azure Redis Cache</span></span>
<span data-ttu-id="f91ab-138">Hello .NET bölümünde izleyerek bir Azure Redis önbelleği oluşturma [nasıl tooUse Azure Redis önbelleği] [ use-rediscache] hello bölüm adlı kadar ***hello önbellek istemcilerini yapılandırın***.</span><span class="sxs-lookup"><span data-stu-id="f91ab-138">Create an Azure Redis cache by following hello .NET section in [How tooUse Azure Redis Cache][use-rediscache] until hello section called ***Configure hello cache clients***.</span></span>
<span data-ttu-id="f91ab-139">Tamamlandıktan sonra yeni bir Redis önbelleği sahip.</span><span class="sxs-lookup"><span data-stu-id="f91ab-139">Once complete, you have a new Redis Cache.</span></span> <span data-ttu-id="f91ab-140">Altında **tüm ayarları**seçin **erişim anahtarları** ve hello Not ***birincil bağlantı dizesi***.</span><span class="sxs-lookup"><span data-stu-id="f91ab-140">Under **All settings**, select **Access keys** and note down hello ***Primary connection string***.</span></span>

![Ekran görüntüsü mimarisi](./media/stream-analytics-functions-redis/redis-cache-keys.png)

## <a name="create-an-azure-function"></a><span data-ttu-id="f91ab-142">Bir Azure işlevi oluşturma</span><span class="sxs-lookup"><span data-stu-id="f91ab-142">Create an Azure Function</span></span>
<span data-ttu-id="f91ab-143">İzleyin [ilk Azure işlevinizi oluşturma] [ functions-getstarted] öğretici tooget Azure işlevleri ile başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="f91ab-143">Follow [Create your first Azure Function][functions-getstarted] tutorial tooget started with Azure Functions.</span></span> <span data-ttu-id="f91ab-144">İster toouse sonra İleri çok atlayabilirsiniz bir Azure işlevi zaten varsa[tooRedis önbellek yazma](#Writing-to-Redis-Cache)</span><span class="sxs-lookup"><span data-stu-id="f91ab-144">If you already have an Azure function you would like toouse, then skip ahead too[Writing tooRedis Cache](#Writing-to-Redis-Cache)</span></span>

1. <span data-ttu-id="f91ab-145">Merhaba portal hello sol gezinti bölmesinden uygulama Hizmetleri'ni seçin ve ardından, Azure işlevi uygulama adı tooget toohello işlevin app Web sitesi tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f91ab-145">In hello portal, select App Services from hello left-hand navigation, then click your Azure function app name tooget toohello Function's app website.</span></span>
    <span data-ttu-id="f91ab-146">![Uygulama Hizmetleri işlevi listesinin ekran görüntüsü](./media/stream-analytics-functions-redis/app-services-function-list.png)</span><span class="sxs-lookup"><span data-stu-id="f91ab-146">![Screenshot of app services function list](./media/stream-analytics-functions-redis/app-services-function-list.png)</span></span>
2. <span data-ttu-id="f91ab-147">Tıklatın **yeni işlev > ServiceBusQueueTrigger – C#**.</span><span class="sxs-lookup"><span data-stu-id="f91ab-147">Click **New Function > ServiceBusQueueTrigger – C#**.</span></span> <span data-ttu-id="f91ab-148">Aşağıdaki alanları Hello için bu yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="f91ab-148">For hello following fields, follow these instructions:</span></span>
   
   * <span data-ttu-id="f91ab-149">**Kuyruk adı**: aynı adı hello sırada oluşturduğunuzda girdiğiniz hello adı olarak hello [hizmet veri yolu kuyrukları ile çalışmaya başlama] [ servicebus-getstarted] (Merhaba hizmet veri yolu hello adı değil).</span><span class="sxs-lookup"><span data-stu-id="f91ab-149">**Queue name**: hello same name as hello name you entered when you created hello queue in [Get Started with Service Bus Queues][servicebus-getstarted] (not hello name of hello service bus).</span></span> <span data-ttu-id="f91ab-150">Stream Analytics çıktı bağlı toohello hello sırasına kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f91ab-150">Make sure you use hello queue that is connected toohello Stream Analytics output.</span></span>
   * <span data-ttu-id="f91ab-151">**Hizmet veri yolu bağlantı**: seçin **bir bağlantı dizesi eklemek**.</span><span class="sxs-lookup"><span data-stu-id="f91ab-151">**Service Bus connection**: Select **Add a connection string**.</span></span> <span data-ttu-id="f91ab-152">toofind hello bağlantı dizesi, Git toohello Klasik portal seçin **Service Bus**, Merhaba, oluşturduğunuz hizmet veri yolu ve **bağlantı bilgilerini** Merhaba ekranında hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="f91ab-152">toofind hello connection string, go toohello classic portal, select **Service Bus**, hello service bus you created, and **CONNECTION INFORMATION** at hello bottom of hello screen.</span></span> <span data-ttu-id="f91ab-153">Bu sayfada ana Merhaba ekranında olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f91ab-153">Make sure you are on hello main screen on this page.</span></span> <span data-ttu-id="f91ab-154">Kopyalama ve hello bağlantı dizesini yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="f91ab-154">Copy and paste hello connection string.</span></span> <span data-ttu-id="f91ab-155">Ücretsiz tooenter herhangi bir bağlantı adı eşitleyerek.</span><span class="sxs-lookup"><span data-stu-id="f91ab-155">Feel free tooenter any connection name.</span></span>
     
       ![Hizmet veri yolu bağlantı ekran görüntüsü](./media/stream-analytics-functions-redis/servicebus-connection.png)
   * <span data-ttu-id="f91ab-157">**ErişimHakları**: seçin **yönetme**</span><span class="sxs-lookup"><span data-stu-id="f91ab-157">**AccessRights**: Choose **Manage**</span></span>
3. <span data-ttu-id="f91ab-158">**Oluştur**'a tıklayın</span><span class="sxs-lookup"><span data-stu-id="f91ab-158">Click **Create**</span></span>

## <a name="writing-tooredis-cache"></a><span data-ttu-id="f91ab-159">Yazma tooRedis önbelleği</span><span class="sxs-lookup"><span data-stu-id="f91ab-159">Writing tooRedis Cache</span></span>
<span data-ttu-id="f91ab-160">Artık Service Bus kuyruğundaki iletileri okuyan bir Azure işlevi oluşturduk.</span><span class="sxs-lookup"><span data-stu-id="f91ab-160">We have now created an Azure Function that reads from a Service Bus Queue.</span></span> <span data-ttu-id="f91ab-161">Tüm toodo sol özelliği bu veri toohello Redis önbelleği bizim işlevi toowrite kullanın.</span><span class="sxs-lookup"><span data-stu-id="f91ab-161">All that is left toodo is use our Function toowrite this data toohello Redis Cache.</span></span> 

1. <span data-ttu-id="f91ab-162">Yeni oluşturduğunuz seçin **ServiceBusQueueTrigger**, tıklatıp **işlev uygulaması ayarları** hello sağ üst köşedeki üzerinde.</span><span class="sxs-lookup"><span data-stu-id="f91ab-162">Select your newly created **ServiceBusQueueTrigger**, and click **Function app settings** on hello top right corner.</span></span> <span data-ttu-id="f91ab-163">Seçin **Git tooApp hizmet ayarları > Ayarlar > Uygulama ayarları**</span><span class="sxs-lookup"><span data-stu-id="f91ab-163">Select **Go tooApp Service Settings > Settings > Application settings**</span></span>
2. <span data-ttu-id="f91ab-164">Hello bağlantı dizeleri bölümü, hello bir ad oluşturmak **adı** bölümü.</span><span class="sxs-lookup"><span data-stu-id="f91ab-164">In hello Connection strings section, create a name in hello **Name** section.</span></span> <span data-ttu-id="f91ab-165">Yapıştırma hello birincil bağlantı dizesi hello bulunamadı **Redis önbelleği oluşturma** hello adımla **değeri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="f91ab-165">Paste hello primary connection string you found in hello **Create a Redis Cache** step into hello **Value** section.</span></span> <span data-ttu-id="f91ab-166">Seçin **özel** burada yazacaktır **SQL veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="f91ab-166">Select **Custom** where it says **SQL Database**.</span></span>
3. <span data-ttu-id="f91ab-167">Tıklatın **kaydetmek** hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="f91ab-167">Click **Save** at hello top.</span></span>
   
    ![Hizmet veri yolu bağlantı ekran görüntüsü](./media/stream-analytics-functions-redis/function-connection-string.png)
4. <span data-ttu-id="f91ab-169">Şimdi toohello uygulama hizmet ayarlarını geri dönün ve seçin **Araçlar > uygulama hizmeti Düzenleyicisi'ni (Önizleme) > üzerinde > Git**.</span><span class="sxs-lookup"><span data-stu-id="f91ab-169">Now go back toohello App Service Settings and select **Tools > App Service Editor (Preview) > On > Go**.</span></span>
   
    ![Hizmet veri yolu bağlantı ekran görüntüsü](./media/stream-analytics-functions-redis/app-service-editor.png)
5. <span data-ttu-id="f91ab-171">Tercih ettiğiniz bir düzenleyicide adlı bir JSON dosyası oluşturun **project.json** ile aşağıdaki hello ve tooyour yerel diske kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f91ab-171">In an editor of your choice, create a JSON file named **project.json** with hello following and save it tooyour local disk.</span></span>
   
        {
            "frameworks": {
                "net46": {
                    "dependencies": {
                        "StackExchange.Redis":"1.1.603",
                        "Newtonsoft.Json": "9.0.1"
                    }
                }
            }
        }
6. <span data-ttu-id="f91ab-172">Bu dosya, işlevin (değil WWWROOT) kök dizine hello karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f91ab-172">Upload this file into hello root directory of your function (not WWWROOT).</span></span> <span data-ttu-id="f91ab-173">Adlı bir dosya görmelisiniz **böylece project.lock.json** otomatik olarak görüntülenmiyorsa, o hello Nuget onaylayan "StackExchange.Redis" ve "Newtonsoft.Json" paketleri içeri aktarıldığını.</span><span class="sxs-lookup"><span data-stu-id="f91ab-173">You should see a file named **project.lock.json** automatically appear, confirming that hello Nuget packages “StackExchange.Redis” and “Newtonsoft.Json” have been imported.</span></span>
7. <span data-ttu-id="f91ab-174">Merhaba, **run.csx** dosya, hello önceden oluşturulan kodu koddan hello ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f91ab-174">In hello **run.csx** file, replace hello pre-generated code with hello following code.</span></span> <span data-ttu-id="f91ab-175">2. adımda oluşturulan hello adıyla "Bağlantı adı" Merhaba lazyConnection işlevinde değiştirin **veri hello Redis önbelleğine depolamak**.</span><span class="sxs-lookup"><span data-stu-id="f91ab-175">In hello lazyConnection function, replace “CONN NAME” with hello name you created in step 2 of **Store data into hello Redis cache**.</span></span>

````

    using System;
    using System.Threading.Tasks;
    using StackExchange.Redis;
    using Newtonsoft.Json;
    using System.Configuration;

    public static void Run(string myQueueItem, TraceWriter log)
    {
        log.Info($"Function processed message: {myQueueItem}");

        // Connection refers tooa property that returns a ConnectionMultiplexer
        IDatabase db = Connection.GetDatabase();
        log.Info($"Created database {db}");

        // Parse JSON and extract hello time
        var message = JsonConvert.DeserializeObject<dynamic>(myQueueItem);
        string time = message.time;
        string callingnum1 = message.callingnum1;

        // Perform cache operations using hello cache object...
        // Simple put of integral data types into hello cache
        string key = time + " - " + callingnum1;
        db.StringSet(key, myQueueItem);
        log.Info($"Object put in database. Key is {key} and value is {myQueueItem}");

        // Simple get of data types from hello cache
        string value = db.StringGet(key);
        log.Info($"Database got: {value}"); 
    }

    // Connect toohello Service Bus
    private static Lazy<ConnectionMultiplexer> lazyConnection = 
        new Lazy<ConnectionMultiplexer>(() =>
            {
                var cnn = ConfigurationManager.ConnectionStrings["CONN NAME"].ConnectionString
                return ConnectionMultiplexer.Connect();
            });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

````

## <a name="start-hello-stream-analytics-job"></a><span data-ttu-id="f91ab-176">Merhaba Stream Analytics işi Başlat</span><span class="sxs-lookup"><span data-stu-id="f91ab-176">Start hello Stream Analytics job</span></span>
1. <span data-ttu-id="f91ab-177">Merhaba telcodatagen.exe uygulaması başlatın.</span><span class="sxs-lookup"><span data-stu-id="f91ab-177">Start hello telcodatagen.exe application.</span></span> <span data-ttu-id="f91ab-178">Merhaba kullanım aşağıdaki gibidir:````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span><span class="sxs-lookup"><span data-stu-id="f91ab-178">hello usage is as follows: ````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span></span>
2. <span data-ttu-id="f91ab-179">Merhaba portalında Hello akış analizi işi dikey penceresinden tıklayın **Başlat** hello sayfanın üst kısmındaki hello.</span><span class="sxs-lookup"><span data-stu-id="f91ab-179">From hello Stream Analytics Job blade in hello portal, click **Start** at hello top of hello page.</span></span>
   
    ![Başlangıç işi ekran görüntüsü](./media/stream-analytics-functions-redis/starting-job.png)
3. <span data-ttu-id="f91ab-181">Merhaba, **başlangıç işi** görünür, dikey seçin **şimdi** ve hello ardından **Başlat** hello ekranın hello düğmesini.</span><span class="sxs-lookup"><span data-stu-id="f91ab-181">In hello **Start job** blade that appears, select **Now** and then click hello **Start** button at hello bottom of hello screen.</span></span> <span data-ttu-id="f91ab-182">Merhaba iş durumu tooStarting değiştirir ve bazı değişiklikler tooRunning saat sonra.</span><span class="sxs-lookup"><span data-stu-id="f91ab-182">hello job status changes tooStarting and after some time changes tooRunning.</span></span>
   
    ![Başlatma işi zaman seçimi ekran görüntüsü](./media/stream-analytics-functions-redis/start-job-time.png)

## <a name="run-solution-and-check-results"></a><span data-ttu-id="f91ab-184">Çözümü çalıştırmak ve sonuçları denetleyin</span><span class="sxs-lookup"><span data-stu-id="f91ab-184">Run solution and check results</span></span>
<span data-ttu-id="f91ab-185">Tooyour geri dönerseniz **ServiceBusQueueTrigger** sayfasında, görmelisiniz oturum deyimleri.</span><span class="sxs-lookup"><span data-stu-id="f91ab-185">Going back tooyour **ServiceBusQueueTrigger** page, you should now see log statements.</span></span> <span data-ttu-id="f91ab-186">Bu günlükler hello veritabanına put hello hizmet veri yolu kuyruğu, gelen bir şey var ve başlangıç anahtarı olarak hello zaman kullanarak getirilen Göster!</span><span class="sxs-lookup"><span data-stu-id="f91ab-186">These logs show that you got something from hello Service Bus Queue, put it into hello database, and fetched it out using hello time as hello key!</span></span>

<span data-ttu-id="f91ab-187">verilerinizi, Redis önbelleğinde olan tooverify hello yeni Portalı'nda tooyour Redis önbelleği sayfasına gidin (Merhaba önceki gösterildiği gibi [bir Azure Redis önbelleği oluşturma](#Create-an-Azure-Redis-Cache) adım) ve konsol seçin.</span><span class="sxs-lookup"><span data-stu-id="f91ab-187">tooverify that your data is in your Redis cache, go tooyour Redis cache page in hello new portal (as shown in hello preceding [Create an Azure Redis Cache](#Create-an-Azure-Redis-Cache) step) and select Console.</span></span>

<span data-ttu-id="f91ab-188">Şimdi veri aslında hello önbelleğinde olduğunu Redis komutları tooconfirm yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f91ab-188">Now you can write Redis commands tooconfirm that data is in fact in hello cache.</span></span>

![Redis konsolunun ekran görüntüsü](./media/stream-analytics-functions-redis/redis-console.png)

## <a name="next-steps"></a><span data-ttu-id="f91ab-190">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f91ab-190">Next steps</span></span>
<span data-ttu-id="f91ab-191">Biz hello yeni şey Azure işlevleri hakkında Çoğalması akış analizi birlikte yapabilirsiniz ve bu yeni olanaklar sizin için kilidini açarak umuyoruz.</span><span class="sxs-lookup"><span data-stu-id="f91ab-191">We’re excited about hello new things Azure Functions and Stream analytics can do together, and we hope this unlocks new possibilities for you.</span></span> <span data-ttu-id="f91ab-192">Sonraki istediğiniz üzerinde hiçbir görüş bildirmek isterseniz, ücretsiz toouse hello eşitleyerek [Azure UserVoice sitesinde](https://feedback.azure.com/forums/270577-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="f91ab-192">If you have any feedback on what you want next, feel free toouse hello [Azure UserVoice site](https://feedback.azure.com/forums/270577-stream-analytics).</span></span>

<span data-ttu-id="f91ab-193">Yeni Microsoft Azure varsa, tootry davet ediyoruz uzaklaştırmak için imzalama tarafından bir [ücretsiz Azure deneme hesabı](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f91ab-193">If you are new Microsoft Azure, we invite you tootry it out by signing up for a [free Azure trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="f91ab-194">Yeni tooStream Analytics olduğunuz sonra çok davet ediyoruz[ilk Stream Analytics işi oluşturmak](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="f91ab-194">If you are new tooStream Analytics, then we invite you too[create your first Stream Analytics job](stream-analytics-create-a-job.md).</span></span>

<span data-ttu-id="f91ab-195">Herhangi bir gereksinim duyarsanız Yardım veya sorularınız varsa, ileti [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) veya [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics) forumlar.</span><span class="sxs-lookup"><span data-stu-id="f91ab-195">If you need any help or have questions, post on [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) or [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics) forums.</span></span> 

<span data-ttu-id="f91ab-196">Kaynakları aşağıdaki hello de görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f91ab-196">You can also see hello following resources:</span></span>

* [<span data-ttu-id="f91ab-197">Azure İşlevleri geliştirici başvurusu</span><span class="sxs-lookup"><span data-stu-id="f91ab-197">Azure Functions developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="f91ab-198">Azure işlevleri C# Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="f91ab-198">Azure Functions C# developer reference</span></span>](../azure-functions/functions-reference-csharp.md)
* [<span data-ttu-id="f91ab-199">Azure işlevleri F # Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="f91ab-199">Azure Functions F# developer reference</span></span>](../azure-functions/functions-reference-fsharp.md)
* [<span data-ttu-id="f91ab-200">Azure işlevleri NodeJS Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="f91ab-200">Azure Functions NodeJS developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="f91ab-201">Azure işlevleri Tetikleyicileri ve bağlamaları</span><span class="sxs-lookup"><span data-stu-id="f91ab-201">Azure Functions triggers and bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
* [<span data-ttu-id="f91ab-202">Nasıl toomonitor Azure Redis önbelleği</span><span class="sxs-lookup"><span data-stu-id="f91ab-202">How toomonitor Azure Redis Cache</span></span>](../redis-cache/cache-how-to-monitor.md)

<span data-ttu-id="f91ab-203">Tüm hello en son haberleri ve özellikleri, güncel toostay izleyin [ @AzureStreaming ](https://twitter.com/AzureStreaming) Twitter'da.</span><span class="sxs-lookup"><span data-stu-id="f91ab-203">toostay up-to-date on all hello latest news and features, follow [@AzureStreaming](https://twitter.com/AzureStreaming) on Twitter.</span></span>

[fraud-detection]: stream-analytics-real-time-fraud-detection.md
[servicebus-getstarted]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[use-rediscache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md
[functions-getstarted]: ../azure-functions/functions-create-first-azure-function.md
