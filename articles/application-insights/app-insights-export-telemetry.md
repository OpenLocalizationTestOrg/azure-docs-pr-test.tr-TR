---
title: Application Insights telemetrisini aaaContinuous verilmesini | Microsoft Docs
description: "Microsoft Azure tanılama ve kullanım verileri toostorage dışarı aktarın ve buradan indirin."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b859200-b484-4c98-9d9f-929713f1030c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: bwren
ms.openlocfilehash: be9ed7e05922c1c8186df9ca4e642862adaa5fd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="export-telemetry-from-application-insights"></a><span data-ttu-id="ce1c9-103">Application Insights telemetrisini dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="ce1c9-103">Export telemetry from Application Insights</span></span>
<span data-ttu-id="ce1c9-104">Tookeep telemetrinizi hello standart tutma süresinden daha uzun süre istiyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="ce1c9-104">Want tookeep your telemetry for longer than hello standard retention period?</span></span> <span data-ttu-id="ce1c9-105">Veya özelleştirilmiş bir şekilde işlemek?</span><span class="sxs-lookup"><span data-stu-id="ce1c9-105">Or process it in some specialized way?</span></span> <span data-ttu-id="ce1c9-106">Sürekli verme bunun için idealdir.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-106">Continuous Export is ideal for this.</span></span> <span data-ttu-id="ce1c9-107">Merhaba Application Insights portalında görmek hello olayları Microsoft Azure'un dışarı aktarılan toostorage JSON biçiminde olabilir.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-107">hello events you see in hello Application Insights portal can be exported toostorage in Microsoft Azure in JSON format.</span></span> <span data-ttu-id="ce1c9-108">Buradan, verilerinizi indirin ve size kod yazma tooprocess gerekir.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-108">From there you can download your data and write whatever code you need tooprocess it.</span></span>  

<span data-ttu-id="ce1c9-109">Sürekli verme özelliğini kullanarak ek bir ücret maruz kalabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-109">Using Continuous Export may incur an additional charge.</span></span> <span data-ttu-id="ce1c9-110">Denetleyin, [fiyatlandırma modeli](http://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="ce1c9-110">Check your [pricing model](http://azure.microsoft.com/pricing/details/application-insights/).</span></span>

<span data-ttu-id="ce1c9-111">Sürekli verme ayarlamadan önce tooconsider isteyebilirsiniz bazı alternatifleri vardır:</span><span class="sxs-lookup"><span data-stu-id="ce1c9-111">Before you set up continuous export, there are some alternatives you might want tooconsider:</span></span>

* <span data-ttu-id="ce1c9-112">Merhaba dışa aktarma düğmesi ölçümleri veya Ara dikey penceresinde hello üstündeki tablolar ve grafikler tooan Excel elektronik tablosu aktarmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-112">hello Export button at hello top of a metrics or search blade lets you transfer tables and charts tooan Excel spreadsheet.</span></span>

* <span data-ttu-id="ce1c9-113">[Analytics](app-insights-analytics.md) telemetri için güçlü sorgu dili sağlar.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-113">[Analytics](app-insights-analytics.md) provides a powerful query language for telemetry.</span></span> <span data-ttu-id="ce1c9-114">Ayrıca sonuçlarını dışarı aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-114">It can also export results.</span></span>
* <span data-ttu-id="ce1c9-115">Çok arıyorsanız[Power BI verilerinizi keşfedin](app-insights-export-power-bi.md), bunu sürekli verme kullanmadan yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-115">If you're looking too[explore your data in Power BI](app-insights-export-power-bi.md), you can do that without using Continuous Export.</span></span>
* <span data-ttu-id="ce1c9-116">Merhaba [veri erişim REST API](https://dev.applicationinsights.io/) siz telemetrinize programlı erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-116">hello [Data access REST API](https://dev.applicationinsights.io/) lets you access your telemetry programmatically.</span></span>

<span data-ttu-id="ce1c9-117">Sürekli verme (burada, kalarak için istediğiniz sürece), veri toostorage kopyaladıktan sonra hello normal Application Insights'ta hala kullanılabilir olduğundan [saklama dönemi](app-insights-data-retention-privacy.md).</span><span class="sxs-lookup"><span data-stu-id="ce1c9-117">After Continuous Export copies your data toostorage (where it can stay for as long as you like), it's still available in Application Insights for hello usual [retention period](app-insights-data-retention-privacy.md).</span></span>

## <span data-ttu-id="ce1c9-118"><a name="setup"></a>Sürekli bir dışarı aktarma oluşturma</span><span class="sxs-lookup"><span data-stu-id="ce1c9-118"><a name="setup"></a> Create a Continuous Export</span></span>
1. <span data-ttu-id="ce1c9-119">Merhaba, uygulamanız için Application Insights kaynağı, sürekli verme açın ve seçin **Ekle**:</span><span class="sxs-lookup"><span data-stu-id="ce1c9-119">In hello Application Insights resource for your app, open Continuous Export and choose **Add**:</span></span>

    ![Aşağı kaydırın ve sürekli ver](./media/app-insights-export-telemetry/01-export.png)

2. <span data-ttu-id="ce1c9-121">Veri türleri Hello telemetri seçin tooexport istiyor.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-121">Choose hello telemetry data types you want tooexport.</span></span>

3. <span data-ttu-id="ce1c9-122">Oluşturma veya seçme bir [Azure depolama hesabı](../storage/common/storage-introduction.md) toostore hello veri istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-122">Create or select an [Azure storage account](../storage/common/storage-introduction.md) where you want toostore hello data.</span></span>

    > [!Warning]
    > <span data-ttu-id="ce1c9-123">Varsayılan olarak, toohello hello depolama konumu ayarlanacak Application Insights kaynağınıza aynı coğrafi bölgede.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-123">By default, hello storage location will be set toohello same geographical region as your Application Insights resource.</span></span> <span data-ttu-id="ce1c9-124">Farklı bir bölgede depolarsanız, aktarım ödemelere maruz kalabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-124">If you store in a different region, you may incur transfer charges.</span></span>

    ![Dışarı aktarmak, hedef depolama hesabı Ekle'yi ve ardından yeni bir depolama alanı oluşturmak veya mevcut deposunu seçin](./media/app-insights-export-telemetry/02-add.png)

4. <span data-ttu-id="ce1c9-126">Oluşturma veya hello depolama alanında bir kapsayıcı seçin:</span><span class="sxs-lookup"><span data-stu-id="ce1c9-126">Create or select a container in hello storage:</span></span>

    ![Seç olay türleri](./media/app-insights-export-telemetry/create-container.png)

<span data-ttu-id="ce1c9-128">Dışa aktarma oluşturduktan sonra olmaya başlar.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-128">Once you've created your export, it starts going.</span></span> <span data-ttu-id="ce1c9-129">Yalnızca hello verme oluşturduktan sonra ulaşan Veri Al</span><span class="sxs-lookup"><span data-stu-id="ce1c9-129">You only get data that arrives after you create hello export.</span></span>

<span data-ttu-id="ce1c9-130">Yaklaşık bir saat hello depolama birimindeki verileri görüntülenmeden önce bir gecikme olabilir.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-130">There can be a delay of about an hour before data appears in hello storage.</span></span>

### <a name="tooedit-continuous-export"></a><span data-ttu-id="ce1c9-131">tooedit sürekli dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="ce1c9-131">tooedit continuous export</span></span>

<span data-ttu-id="ce1c9-132">Toochange hello olay türleri istiyorsanız, daha sonra yalnızca hello verme düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="ce1c9-132">If you want toochange hello event types later, just edit hello export:</span></span>

![Seç olay türleri](./media/app-insights-export-telemetry/05-edit.png)

### <a name="toostop-continuous-export"></a><span data-ttu-id="ce1c9-134">toostop sürekli dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="ce1c9-134">toostop continuous export</span></span>

<span data-ttu-id="ce1c9-135">toostop hello verme tıklatın devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-135">toostop hello export, click Disable.</span></span> <span data-ttu-id="ce1c9-136">Etkinleştirme yeniden tıklattığınızda hello verme yeni verilerle yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-136">When you click Enable again, hello export will restart with new data.</span></span> <span data-ttu-id="ce1c9-137">Dışarı aktarma devre dışıyken hello Portalı'nda gelen hello verileri alamazsınız.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-137">You won't get hello data that arrived in hello portal while export was disabled.</span></span>

<span data-ttu-id="ce1c9-138">toostop hello verme kalıcı olarak silin.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-138">toostop hello export permanently, delete it.</span></span> <span data-ttu-id="ce1c9-139">Bunun yapılması, veri depolama biriminden silmez.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-139">Doing so doesn't delete your data from storage.</span></span>

### <a name="cant-add-or-change-an-export"></a><span data-ttu-id="ce1c9-140">Ekleyemez veya verme değiştirmek mi?</span><span class="sxs-lookup"><span data-stu-id="ce1c9-140">Can't add or change an export?</span></span>
* <span data-ttu-id="ce1c9-141">tooadd ya da değişiklik dışarı sahibi, katkıda bulunan veya uygulama Öngörüler katkıda erişim hakları gerekir.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-141">tooadd or change exports, you need Owner, Contributor or Application Insights Contributor access rights.</span></span> <span data-ttu-id="ce1c9-142">[Rolleri hakkında bilgi edinin][roles].</span><span class="sxs-lookup"><span data-stu-id="ce1c9-142">[Learn about roles][roles].</span></span>

## <span data-ttu-id="ce1c9-143"><a name="analyze"></a>Hangi olayların alıyorum?</span><span class="sxs-lookup"><span data-stu-id="ce1c9-143"><a name="analyze"></a> What events do you get?</span></span>
<span data-ttu-id="ce1c9-144">Biz hesaplamak konum verileri hello istemci IP adresinden eklediğimiz hello dışarı aktarılan verileri uygulamanızdan aldığımız hello ham telemetri olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-144">hello exported data is hello raw telemetry we receive from your application, except that we add location data which we calculate from hello client IP address.</span></span>

<span data-ttu-id="ce1c9-145">Tarafından atılan veri [örnekleme](app-insights-sampling.md) dışarı hello veri bulunmaz.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-145">Data that has been discarded by [sampling](app-insights-sampling.md) is not included in hello exported data.</span></span>

<span data-ttu-id="ce1c9-146">Hesaplanan diğer ölçümleri dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-146">Other calculated metrics are not included.</span></span> <span data-ttu-id="ce1c9-147">Örneğin, ortalama CPU kullanımı verme yok ancak hello ortalama hesaplanan hello ham telemetri verme.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-147">For example, we don't export average CPU utilisation, but we do export hello raw telemetry from which hello average is computed.</span></span>

<span data-ttu-id="ce1c9-148">Merhaba verileri de herhangi hello sonuçlarını içerir [kullanılabilirlik web testleri](app-insights-monitor-web-app-availability.md) ayarlamış olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-148">hello data also includes hello results of any [availability web tests](app-insights-monitor-web-app-availability.md) that you have set up.</span></span>

> [!NOTE]
> <span data-ttu-id="ce1c9-149">**Örnekleme.**</span><span class="sxs-lookup"><span data-stu-id="ce1c9-149">**Sampling.**</span></span> <span data-ttu-id="ce1c9-150">Uygulamanız çok miktarda veri gönderiyorsa, hello örnekleme özelliği çalışır ve yalnızca bir kesir oluşturulan hello telemetri gönderin.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-150">If your application sends a lot of data, hello sampling feature may operate and send only a fraction of hello generated telemetry.</span></span> [<span data-ttu-id="ce1c9-151">Örnekleme hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-151">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <span data-ttu-id="ce1c9-152"><a name="get"></a>Merhaba veri inceleyin.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-152"><a name="get"></a> Inspect hello data</span></span>
<span data-ttu-id="ce1c9-153">Merhaba depolama hello portalında doğrudan inceleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-153">You can inspect hello storage directly in hello portal.</span></span> <span data-ttu-id="ce1c9-154">Tıklatın **Gözat**, depolama hesabınızı seçin ve ardından açın **kapsayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-154">Click **Browse**, select your storage account, and then open **Containers**.</span></span>

<span data-ttu-id="ce1c9-155">Visual Studio'da Azure depolama tooinspect açmak **Görünüm**, **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-155">tooinspect Azure storage in Visual Studio, open **View**, **Cloud Explorer**.</span></span> <span data-ttu-id="ce1c9-156">(Bu menü komutu yoksa tooinstall hello Azure SDK'sı gerekir: açık hello **yeni proje** iletişim kutusunda, Visual C# ' ı genişletin / Bulut ve **.NET için Microsoft Azure SDK almak**.)</span><span class="sxs-lookup"><span data-stu-id="ce1c9-156">(If you don't have that menu command, you need tooinstall hello Azure SDK: Open hello **New Project** dialog, expand Visual C#/Cloud and choose **Get Microsoft Azure SDK for .NET**.)</span></span>

<span data-ttu-id="ce1c9-157">Blob deposu açtığınızda, blob dosya kümesini içeren bir kapsayıcı göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-157">When you open your blob store, you'll see a container with a set of blob files.</span></span> <span data-ttu-id="ce1c9-158">Merhaba, Application Insights kaynağı adı, izleme anahtarı, telemetri-türü/tarih/saat türetilen her dosyanın URI.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-158">hello URI of each file derived from your Application Insights resource name, its instrumentation key, telemetry-type/date/time.</span></span> <span data-ttu-id="ce1c9-159">(Merhaba kaynak adının tamamen küçük harflerden ve tire hello izleme anahtarı atlar.)</span><span class="sxs-lookup"><span data-stu-id="ce1c9-159">(hello resource name is all lowercase, and hello instrumentation key omits dashes.)</span></span>

![Uygun bir araçla Hello blob deposu inceleyin.](./media/app-insights-export-telemetry/04-data.png)

<span data-ttu-id="ce1c9-161">Başlangıç tarihi ve saati UTC ve hello telemetri hello deposunda borç - değil hello zaman oluşturulduğu zaman.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-161">hello date and time are UTC and are when hello telemetry was deposited in hello store - not hello time it was generated.</span></span> <span data-ttu-id="ce1c9-162">Kod toodownload hello verileri yazarsanız, bu nedenle onu doğrusal olarak hello verilerine taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-162">So if you write code toodownload hello data, it can move linearly through hello data.</span></span>

<span data-ttu-id="ce1c9-163">Merhaba biçiminde hello yolu şöyledir:</span><span class="sxs-lookup"><span data-stu-id="ce1c9-163">Here's hello form of hello path:</span></span>

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

<span data-ttu-id="ce1c9-164">Burada</span><span class="sxs-lookup"><span data-stu-id="ce1c9-164">Where</span></span>

* <span data-ttu-id="ce1c9-165">`blobCreationTimeUtc`depolama alanı hazırlama blob hello iç oluşturulduğu süresi</span><span class="sxs-lookup"><span data-stu-id="ce1c9-165">`blobCreationTimeUtc` is time when blob was created in hello internal staging storage</span></span>
* <span data-ttu-id="ce1c9-166">`blobDeliveryTimeUtc`blob kopyalanan toohello verme hedef depolama olduğunda başlangıç zamanı</span><span class="sxs-lookup"><span data-stu-id="ce1c9-166">`blobDeliveryTimeUtc` is hello time when blob is copied toohello export destination storage</span></span>

## <span data-ttu-id="ce1c9-167"><a name="format"></a>Veri biçimi</span><span class="sxs-lookup"><span data-stu-id="ce1c9-167"><a name="format"></a> Data format</span></span>
* <span data-ttu-id="ce1c9-168">Her bir blob birden çok içeren bir metin dosyasıdır ' \n'-separated satır.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-168">Each blob is a text file that contains multiple '\n'-separated rows.</span></span> <span data-ttu-id="ce1c9-169">Bir süre kabaca yarım bir dakika boyunca işlenen hello telemetri içerir.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-169">It contains hello telemetry processed over a time period of roughly half a minute.</span></span>
* <span data-ttu-id="ce1c9-170">Her satır bir istek veya sayfa görünümü gibi bir telemetri veri noktasını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-170">Each row represents a telemetry data point such as a request or page view.</span></span>
* <span data-ttu-id="ce1c9-171">Her satır bir biçimlendirilmemiş bir JSON dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-171">Each row is an unformatted JSON document.</span></span> <span data-ttu-id="ce1c9-172">Toosit isterseniz ve yerinde stare, Visual Studio'da açın ve seçin, Gelişmiş biçim dosyasını düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="ce1c9-172">If you want toosit and stare at it, open it in Visual Studio and choose Edit, Advanced, Format File:</span></span>

![Görünüm hello telemetri uygun aracıyla](./media/app-insights-export-telemetry/06-json.png)

<span data-ttu-id="ce1c9-174">Süreler olduğunuz nerede 10 000 işaretlerini çizgilerine içinde 1ms =.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-174">Time durations are in ticks, where 10 000 ticks = 1ms.</span></span> <span data-ttu-id="ce1c9-175">Örneğin, bu değerleri 1ms süresini göster toosend isteği hello tarayıcısından 3ms ve 1.8s tooprocess hello sayfa hello tarayıcıda tooreceive:</span><span class="sxs-lookup"><span data-stu-id="ce1c9-175">For example, these values show a time of 1ms toosend a request from hello browser, 3ms tooreceive it, and 1.8s tooprocess hello page in hello browser:</span></span>

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[<span data-ttu-id="ce1c9-176">Ayrıntılı veri başvuru hello özellik türleri ve değerleri için model.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-176">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)

## <a name="processing-hello-data"></a><span data-ttu-id="ce1c9-177">Merhaba veri işleme</span><span class="sxs-lookup"><span data-stu-id="ce1c9-177">Processing hello data</span></span>
<span data-ttu-id="ce1c9-178">Küçük bir ölçekte bazı kod toopull parçalayın verilerinizi yazma, elektronik tabloya okuyun ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-178">On a small scale, you can write some code toopull apart your data, read it into a spreadsheet, and so on.</span></span> <span data-ttu-id="ce1c9-179">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ce1c9-179">For example:</span></span>

    private IEnumerable<T> DeserializeMany<T>(string folderName)
    {
      var files = Directory.EnumerateFiles(folderName, "*.blob", SearchOption.AllDirectories);
      foreach (var file in files)
      {
         using (var fileReader = File.OpenText(file))
         {
            string fileContent = fileReader.ReadToEnd();
            IEnumerable<string> entities = fileContent.Split('\n').Where(s => !string.IsNullOrWhiteSpace(s));
            foreach (var entity in entities)
            {
                yield return JsonConvert.DeserializeObject<T>(entity);
            }
         }
      }
    }

<span data-ttu-id="ce1c9-180">Daha büyük bir kod örneği için bkz: [çalışan rolü kullanarak][exportasa].</span><span class="sxs-lookup"><span data-stu-id="ce1c9-180">For a larger code sample, see [using a worker role][exportasa].</span></span>

## <span data-ttu-id="ce1c9-181"><a name="delete"></a>Eski verileri Sil</span><span class="sxs-lookup"><span data-stu-id="ce1c9-181"><a name="delete"></a>Delete your old data</span></span>
<span data-ttu-id="ce1c9-182">Lütfen depolama kapasitesi yönetme ve gerekirse hello eski verileri silmek için sorumlu olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-182">Please note that you are responsible for managing your storage capacity and deleting hello old data if necessary.</span></span>

## <a name="if-you-regenerate-your-storage-key"></a><span data-ttu-id="ce1c9-183">Depolama anahtarınızı yeniden oluşturursanız...</span><span class="sxs-lookup"><span data-stu-id="ce1c9-183">If you regenerate your storage key...</span></span>
<span data-ttu-id="ce1c9-184">Merhaba anahtar tooyour depolama değiştirirseniz, sürekli verme çalışmayı durdurur.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-184">If you change hello key tooyour storage, continuous export will stop working.</span></span> <span data-ttu-id="ce1c9-185">Azure hesabınızda bir bildirim görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-185">You'll see a notification in your Azure account.</span></span>

<span data-ttu-id="ce1c9-186">Merhaba sürekli Dışarı Aktar dikey penceresini açın ve dışa aktarma düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-186">Open hello Continuous Export blade and edit your export.</span></span> <span data-ttu-id="ce1c9-187">Hello verme hedef düzenlemek, ancak yalnızca hello aynı depolama seçili bırakın.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-187">Edit hello Export Destination, but just leave hello same storage selected.</span></span> <span data-ttu-id="ce1c9-188">Tamam tooconfirm'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-188">Click OK tooconfirm.</span></span>

![Düzen hello sürekli verme, açın ve üç dışa aktarma hedefi kapatın.](./media/app-insights-export-telemetry/07-resetstore.png)

<span data-ttu-id="ce1c9-190">Merhaba sürekli verme yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-190">hello continuous export will restart.</span></span>

## <a name="export-samples"></a><span data-ttu-id="ce1c9-191">Dışarı aktarma örnekleri</span><span class="sxs-lookup"><span data-stu-id="ce1c9-191">Export samples</span></span>

* <span data-ttu-id="ce1c9-192">[Akış analizi kullanarak tooSQL dışarı aktarma][exportasa]</span><span class="sxs-lookup"><span data-stu-id="ce1c9-192">[Export tooSQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="ce1c9-193">Stream Analytics örnek 2</span><span class="sxs-lookup"><span data-stu-id="ce1c9-193">Stream Analytics sample 2</span></span>](app-insights-export-stream-analytics.md)

<span data-ttu-id="ce1c9-194">Büyük ölçek üzerinde dikkate [Hdınsight](https://azure.microsoft.com/services/hdinsight/) -hello bulutta Hadoop kümeleri.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-194">On larger scales, consider [HDInsight](https://azure.microsoft.com/services/hdinsight/) - Hadoop clusters in hello cloud.</span></span> <span data-ttu-id="ce1c9-195">Hdınsight çeşitli teknolojiler yönetmek ve büyük veri çözümleme sağlar ve Application Insights ' dışarı tooprocess veri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-195">HDInsight provides a variety of technologies for managing and analyzing big data, and you could use it tooprocess data that has been exported from Application Insights.</span></span>

## <a name="q--a"></a><span data-ttu-id="ce1c9-196">Soru-Cevap</span><span class="sxs-lookup"><span data-stu-id="ce1c9-196">Q & A</span></span>
* <span data-ttu-id="ce1c9-197">*Ancak tüm istiyorum tek seferlik bir indirme bir grafik.*</span><span class="sxs-lookup"><span data-stu-id="ce1c9-197">*But all I want is a one-time download of a chart.*</span></span>  

    <span data-ttu-id="ce1c9-198">Evet, bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-198">Yes, you can do that.</span></span> <span data-ttu-id="ce1c9-199">Merhaba dikey penceresinde Hello üstünde tıklatın **verileri dışa aktar**.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-199">At hello top of hello blade, click **Export Data**.</span></span>
* <span data-ttu-id="ce1c9-200">*Bir verme ayarlayın, ancak my deposunda verisi yok.*</span><span class="sxs-lookup"><span data-stu-id="ce1c9-200">*I set up an export, but there's no data in my store.*</span></span>

    <span data-ttu-id="ce1c9-201">Hello verme ayarladığınız bu yana Application Insights uygulamanızdan tüm telemetri aldınız mı?</span><span class="sxs-lookup"><span data-stu-id="ce1c9-201">Did Application Insights receive any telemetry from your app since you set up hello export?</span></span> <span data-ttu-id="ce1c9-202">Yalnızca yeni verileri alırsınız.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-202">You'll only receive new data.</span></span>
* <span data-ttu-id="ce1c9-203">*I tooset verme yukarı denedi ancak erişim reddedildi*</span><span class="sxs-lookup"><span data-stu-id="ce1c9-203">*I tried tooset up an export, but was denied access*</span></span>

    <span data-ttu-id="ce1c9-204">Kuruluşunuz tarafından Hello hesabına ait toobe hello sahipler veya katkıda bulunanlar grupların üyesi varsa.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-204">If hello account is owned by your organization, you have toobe a member of hello owners or contributors groups.</span></span>
* <span data-ttu-id="ce1c9-205">*Düz toomy kendi şirket içi depolama dışa aktarabilirsiniz?*</span><span class="sxs-lookup"><span data-stu-id="ce1c9-205">*Can I export straight toomy own on-premises store?*</span></span>

    <span data-ttu-id="ce1c9-206">Hayır, özür dileriz.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-206">No, sorry.</span></span> <span data-ttu-id="ce1c9-207">Bizim verme Altyapısı şu anda yalnızca Azure storage ile şu anda çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-207">Our export engine currently only works with Azure storage at this time.</span></span>  
* <span data-ttu-id="ce1c9-208">*My deposunda put veri herhangi sınırı toohello miktarını var mı?*</span><span class="sxs-lookup"><span data-stu-id="ce1c9-208">*Is there any limit toohello amount of data you put in my store?*</span></span>

    <span data-ttu-id="ce1c9-209">Hayır.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-209">No.</span></span> <span data-ttu-id="ce1c9-210">Merhaba verme silene kadar biz verisi itmesi tutmak.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-210">We'll keep pushing data in until you delete hello export.</span></span> <span data-ttu-id="ce1c9-211">Biz blob storage için hello dış sınırına ulaşıp ancak oldukça büyük durdurmanız.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-211">We'll stop if we hit hello outer limits for blob storage, but that's pretty huge.</span></span> <span data-ttu-id="ce1c9-212">Bu, kullandığınız ne kadar depolama alanı tooyou toocontrol olur.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-212">It's up tooyou toocontrol how much storage you use.</span></span>  
* <span data-ttu-id="ce1c9-213">*Kaç tane BLOB'lar ı hello depolama alanında görmeniz gerekir?*</span><span class="sxs-lookup"><span data-stu-id="ce1c9-213">*How many blobs should I see in hello storage?*</span></span>

  * <span data-ttu-id="ce1c9-214">Her veri türü için (veri kullanılabiliyorsa) seçili tooexport, yeni blob dakikada oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-214">For every data type you selected tooexport, a new blob is created every minute (if data is available).</span></span>
  * <span data-ttu-id="ce1c9-215">Ayrıca, yüksek trafiğe sahip uygulamalar için ek bölüm birimleri ayrılır.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-215">In addition, for applications with high traffic, additional partition units are allocated.</span></span> <span data-ttu-id="ce1c9-216">Bu durumda her birimi dakikada bir blob oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-216">In this case each unit creates a blob every minute.</span></span>
* <span data-ttu-id="ce1c9-217">*Merhaba anahtar toomy depolama yeniden veya hello kapsayıcısının hello adı değiştirildi ve hello verme artık çalışmıyor.*</span><span class="sxs-lookup"><span data-stu-id="ce1c9-217">*I regenerated hello key toomy storage or changed hello name of hello container, and now hello export doesn't work.*</span></span>

    <span data-ttu-id="ce1c9-218">Merhaba verme düzenleyin ve hello dışarı aktarma hedefi dikey penceresini açın.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-218">Edit hello export and open hello export destination blade.</span></span> <span data-ttu-id="ce1c9-219">Merhaba öncekiyle aynı depolama seçili bırakın ve Tamam tooconfirm'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-219">Leave hello same storage selected as before, and click OK tooconfirm.</span></span> <span data-ttu-id="ce1c9-220">Dışarı aktarma yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-220">Export will restart.</span></span> <span data-ttu-id="ce1c9-221">Merhaba değişiklik hello son birkaç gün içinde ise, veri kaybı olmaz.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-221">If hello change was within hello past few days, you won't lose data.</span></span>
* <span data-ttu-id="ce1c9-222">*Merhaba verme duraklatabilir miyim?*</span><span class="sxs-lookup"><span data-stu-id="ce1c9-222">*Can I pause hello export?*</span></span>

    <span data-ttu-id="ce1c9-223">Evet.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-223">Yes.</span></span> <span data-ttu-id="ce1c9-224">Devre dışı bırak'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-224">Click Disable.</span></span>

## <a name="code-samples"></a><span data-ttu-id="ce1c9-225">Kod örnekleri</span><span class="sxs-lookup"><span data-stu-id="ce1c9-225">Code samples</span></span>

* [<span data-ttu-id="ce1c9-226">Akış analizi örneği</span><span class="sxs-lookup"><span data-stu-id="ce1c9-226">Stream Analytics sample</span></span>](app-insights-export-stream-analytics.md)
* <span data-ttu-id="ce1c9-227">[Akış analizi kullanarak tooSQL dışarı aktarma][exportasa]</span><span class="sxs-lookup"><span data-stu-id="ce1c9-227">[Export tooSQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="ce1c9-228">Ayrıntılı veri başvuru hello özellik türleri ve değerleri için model.</span><span class="sxs-lookup"><span data-stu-id="ce1c9-228">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md
