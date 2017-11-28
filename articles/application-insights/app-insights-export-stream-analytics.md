---
title: "Azure Application Insights gelen akış analizi kullanarak aaaExport | Microsoft Docs"
description: "Akış analizi sürekli dönüştürebilirsiniz, filtre ve rota hello veri Application Insights ' dışarı aktarma."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 31594221-17bd-4e5e-9534-950f3b022209
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: fda9b64f588c520833b2669eafdf650efc3de6be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-stream-analytics-tooprocess-exported-data-from-application-insights"></a><span data-ttu-id="4ffde-103">Application Insights kullanım Stream Analytics tooprocess verilen verileri</span><span class="sxs-lookup"><span data-stu-id="4ffde-103">Use Stream Analytics tooprocess exported data from Application Insights</span></span>
<span data-ttu-id="4ffde-104">[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) veri işlemeye hello ideal araçtır [Application Insights ' dışarı](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="4ffde-104">[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) is hello ideal tool for processing data [exported from Application Insights](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="4ffde-105">Akış analizi, çeşitli kaynaklardan veri çeker.</span><span class="sxs-lookup"><span data-stu-id="4ffde-105">Stream Analytics can pull data from a variety of sources.</span></span> <span data-ttu-id="4ffde-106">Bu dönüştürme ve hello verilere filtre ve ardından havuzlarını tooa çeşitli rota.</span><span class="sxs-lookup"><span data-stu-id="4ffde-106">It can transform and filter hello data, and then route it tooa variety of sinks.</span></span>

<span data-ttu-id="4ffde-107">Bu örnekte, yeniden adlandırır Application Insights ' verileri alır ve bazı hello alanlarını işler ve Power BI kanallar bir bağdaştırıcıya oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="4ffde-107">In this example, we'll create an adaptor that takes data from Application Insights, renames and processes some of hello fields, and pipes it into Power BI.</span></span>

> [!WARNING]
> <span data-ttu-id="4ffde-108">Çok daha iyi ve daha kolay [toodisplay Application Insights Power BI'daki veriler, önerilen yollar](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="4ffde-108">There are much better and easier [recommended ways toodisplay Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="4ffde-109">Merhaba burada gösterilen yalnızca bir örnek tooillustrate yoludur nasıl tooprocess verilen verileri.</span><span class="sxs-lookup"><span data-stu-id="4ffde-109">hello path illustrated here is just an example tooillustrate how tooprocess exported data.</span></span>
> 
> 

![Blok Diyagramı SA tooPBI aracılığıyla dışarı aktarma](./media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a><span data-ttu-id="4ffde-111">Depolama oluşturma</span><span class="sxs-lookup"><span data-stu-id="4ffde-111">Create storage in Azure</span></span>
<span data-ttu-id="4ffde-112">Toocreate hello depolama önce gerekir böylece sürekli dışarı aktarma veri tooan Azure depolama hesabı, her zaman çıkarır.</span><span class="sxs-lookup"><span data-stu-id="4ffde-112">Continuous export always outputs data tooan Azure Storage account, so you need toocreate hello storage first.</span></span>

1. <span data-ttu-id="4ffde-113">Aboneliğinizdeki hello "Klasik" depolama hesabı oluşturma [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4ffde-113">Create a "classic" storage account in your subscription in hello [Azure portal](https://portal.azure.com).</span></span>
   
   ![Azure portalında yeni, verileri depolama seçin](./media/app-insights-export-stream-analytics/030.png)
2. <span data-ttu-id="4ffde-115">Bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4ffde-115">Create a container</span></span>
   
    ![Merhaba yeni depolama kapsayıcıları seçin, Merhaba kapsayıcılara döşeme tıklatın ve ardından Ekle](./media/app-insights-export-stream-analytics/040.png)
3. <span data-ttu-id="4ffde-117">Merhaba depolama erişim tuşu kopyalama</span><span class="sxs-lookup"><span data-stu-id="4ffde-117">Copy hello storage access key</span></span>
   
    <span data-ttu-id="4ffde-118">Bunu en kısa sürede tooset hello giriş toohello stream analytics hizmeti yukarı ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="4ffde-118">You'll need it soon tooset up hello input toohello stream analytics service.</span></span>
   
    ![Merhaba depolama ayarları, anahtarları, açın ve hello birincil erişim anahtarını bir kopyasını alın](./media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-tooazure-storage"></a><span data-ttu-id="4ffde-120">Sürekli verme tooAzure depolama Başlat</span><span class="sxs-lookup"><span data-stu-id="4ffde-120">Start continuous export tooAzure storage</span></span>
<span data-ttu-id="4ffde-121">[Sürekli verme](app-insights-export-telemetry.md) Application Insights Azure depolama alanına gelen verileri taşır.</span><span class="sxs-lookup"><span data-stu-id="4ffde-121">[Continuous export](app-insights-export-telemetry.md) moves data from Application Insights into Azure storage.</span></span>

1. <span data-ttu-id="4ffde-122">Hello Azure portal, uygulamanız için oluşturulan toohello Application Insights kaynağı göz atın.</span><span class="sxs-lookup"><span data-stu-id="4ffde-122">In hello Azure portal, browse toohello Application Insights resource you created for your application.</span></span>
   
    ![Gözat, Application Insights, uygulamanızı seçin](./media/app-insights-export-stream-analytics/050.png)
2. <span data-ttu-id="4ffde-124">Sürekli verme oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4ffde-124">Create a continuous export.</span></span>
   
    ![Ayarları, sürekli verme ekleme seçin](./media/app-insights-export-stream-analytics/060.png)

    <span data-ttu-id="4ffde-126">Daha önce oluşturduğunuz hello depolama hesabı seçin:</span><span class="sxs-lookup"><span data-stu-id="4ffde-126">Select hello storage account you created earlier:</span></span>

    ![Merhaba dışa aktarma hedefi ayarlama](./media/app-insights-export-stream-analytics/070.png)

    <span data-ttu-id="4ffde-128">İstediğiniz hello olay türlerini toosee ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="4ffde-128">Set hello event types you want toosee:</span></span>

    ![Olay türlerini seçin](./media/app-insights-export-stream-analytics/080.png)

1. <span data-ttu-id="4ffde-130">Accumulate bazı veriler sağlar.</span><span class="sxs-lookup"><span data-stu-id="4ffde-130">Let some data accumulate.</span></span> <span data-ttu-id="4ffde-131">Arkanıza yaslanın ve kişilere uygulamanızın biraz kullanın.</span><span class="sxs-lookup"><span data-stu-id="4ffde-131">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="4ffde-132">Telemetri geldikçe ve istatistiksel grafiklerde görürsünüz [ölçüm Gezgini](app-insights-metrics-explorer.md) ve olayları tek tek [tanılama arama](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="4ffde-132">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="4ffde-133">Ve ayrıca hello veri tooyour depolama dışa aktarır.</span><span class="sxs-lookup"><span data-stu-id="4ffde-133">And also, hello data will export tooyour storage.</span></span> 
2. <span data-ttu-id="4ffde-134">Dışa aktarılan hello veri inceleyin.</span><span class="sxs-lookup"><span data-stu-id="4ffde-134">Inspect hello exported data.</span></span> <span data-ttu-id="4ffde-135">Visual Studio'da, **görüntülemek / Cloud Explorer**ve Azure açın / depolama.</span><span class="sxs-lookup"><span data-stu-id="4ffde-135">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="4ffde-136">(Bu menü seçeneği yoksa, tooinstall hello Azure SDK'sı gerekir: hello yeni proje iletişim kutusu açın ve Visual C# açın / bulut / .NET için Microsoft Azure SDK'sını alın.)</span><span class="sxs-lookup"><span data-stu-id="4ffde-136">(If you don't have this menu option, you need tooinstall hello Azure SDK: Open hello New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![](./media/app-insights-export-stream-analytics/04-data.png)
   
    <span data-ttu-id="4ffde-137">Merhaba ortak hello uygulama adı ve araçları anahtarından türetilen hello yol adı parçası not edin.</span><span class="sxs-lookup"><span data-stu-id="4ffde-137">Make a note of hello common part of hello path name, which is derived from hello application name and instrumentation key.</span></span> 

<span data-ttu-id="4ffde-138">Merhaba olayları tooblob dosyaları JSON biçiminde yazılır.</span><span class="sxs-lookup"><span data-stu-id="4ffde-138">hello events are written tooblob files in JSON format.</span></span> <span data-ttu-id="4ffde-139">Her dosya bir veya daha fazla olaylar içerebilir.</span><span class="sxs-lookup"><span data-stu-id="4ffde-139">Each file may contain one or more events.</span></span> <span data-ttu-id="4ffde-140">Bu nedenle tooread hello olay verileri ve filtre istiyoruz hello alanları isteriz.</span><span class="sxs-lookup"><span data-stu-id="4ffde-140">So we'd like tooread hello event data and filter out hello fields we want.</span></span> <span data-ttu-id="4ffde-141">Her türlü hello verilerle yapabileceğimiz bir şey vardır, ancak bizim bugün toouse Stream Analytics toopipe hello veri tooPower BI planınızdır.</span><span class="sxs-lookup"><span data-stu-id="4ffde-141">There are all kinds of things we could do with hello data, but our plan today is toouse Stream Analytics toopipe hello data tooPower BI.</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="4ffde-142">Bir Azure akış analizi örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="4ffde-142">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="4ffde-143">Merhaba gelen [Klasik Azure portalı](https://manage.windowsazure.com/)hello Azure Stream Analytics hizmeti seçin ve yeni bir Stream Analytics işi oluştur:</span><span class="sxs-lookup"><span data-stu-id="4ffde-143">From hello [Classic Azure Portal](https://manage.windowsazure.com/), select hello Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-export-stream-analytics/090.png)

![](./media/app-insights-export-stream-analytics/100.png)

<span data-ttu-id="4ffde-144">Merhaba yeni iş oluşturulduğunda ayrıntılarını genişletin:</span><span class="sxs-lookup"><span data-stu-id="4ffde-144">When hello new job is created, expand its details:</span></span>

![](./media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a><span data-ttu-id="4ffde-145">Blob konum ayarlama</span><span class="sxs-lookup"><span data-stu-id="4ffde-145">Set blob location</span></span>
<span data-ttu-id="4ffde-146">Sürekli verme blob tootake girişten ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="4ffde-146">Set it tootake input from your Continuous Export blob:</span></span>

![](./media/app-insights-export-stream-analytics/120.png)

<span data-ttu-id="4ffde-147">Şimdi, depolama, daha önce not ettiğiniz hesabınızdan, hello birincil erişim anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="4ffde-147">Now you'll need hello Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="4ffde-148">Bu depolama hesabı anahtarı hello ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4ffde-148">Set this as hello Storage Account Key.</span></span>

![](./media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a><span data-ttu-id="4ffde-149">Set yol önek deseni</span><span class="sxs-lookup"><span data-stu-id="4ffde-149">Set path prefix pattern</span></span>
![](./media/app-insights-export-stream-analytics/140.png)

<span data-ttu-id="4ffde-150">**Emin tooset hello tarih biçimi tooYYYY-aa-gg (çizgilerle) olabilir.**</span><span class="sxs-lookup"><span data-stu-id="4ffde-150">**Be sure tooset hello Date Format tooYYYY-MM-DD (with dashes).**</span></span>

<span data-ttu-id="4ffde-151">Stream Analytics hello giriş dosyaları hello depolama burada bulur Hello yol önek deseni belirtir.</span><span class="sxs-lookup"><span data-stu-id="4ffde-151">hello Path Prefix Pattern specifies where Stream Analytics finds hello input files in hello storage.</span></span> <span data-ttu-id="4ffde-152">Tooset gerekir, toocorrespond toohow sürekli verme hello verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="4ffde-152">You need tooset it toocorrespond toohow Continuous Export stores hello data.</span></span> <span data-ttu-id="4ffde-153">Aşağıdaki gibi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="4ffde-153">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="4ffde-154">Bu örnekte:</span><span class="sxs-lookup"><span data-stu-id="4ffde-154">In this example:</span></span>

* <span data-ttu-id="4ffde-155">`webapplication27`Merhaba Application Insights kaynağı Hello adıdır **tüm küçük**.</span><span class="sxs-lookup"><span data-stu-id="4ffde-155">`webapplication27` is hello name of hello Application Insights resource **all lower case**.</span></span>
* <span data-ttu-id="4ffde-156">`1234...`Merhaba izleme anahtarını hello Application Insights kaynağı olan **tire atlama**.</span><span class="sxs-lookup"><span data-stu-id="4ffde-156">`1234...` is hello instrumentation key of hello Application Insights resource, **omitting dashes**.</span></span> 
* <span data-ttu-id="4ffde-157">`PageViews`Merhaba türü tooanalyze istediğiniz verileri.</span><span class="sxs-lookup"><span data-stu-id="4ffde-157">`PageViews` is hello type of data you want tooanalyze.</span></span> <span data-ttu-id="4ffde-158">Merhaba kullanılabilir türler hello filtresi sürekli dışarı aktarma ile Ayarla bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="4ffde-158">hello available types depend on hello filter you set in Continuous Export.</span></span> <span data-ttu-id="4ffde-159">Kullanılabilir diğer türleri Hello dışarı aktarılan verileri toosee hello inceleyin ve hello bakın [veri modeli verme](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="4ffde-159">Examine hello exported data toosee hello other available types, and see hello [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="4ffde-160">`/{date}/{time}`bir desen tam anlamıyla yazılır.</span><span class="sxs-lookup"><span data-stu-id="4ffde-160">`/{date}/{time}` is a pattern written literally.</span></span>

> [!NOTE]
> <span data-ttu-id="4ffde-161">Merhaba depolama toomake hello yolu doğru alma emin inceleyin.</span><span class="sxs-lookup"><span data-stu-id="4ffde-161">Inspect hello storage toomake sure you get hello path right.</span></span>
> 
> 

### <a name="finish-initial-setup"></a><span data-ttu-id="4ffde-162">İlk Kurulumu tamamlayın</span><span class="sxs-lookup"><span data-stu-id="4ffde-162">Finish initial setup</span></span>
<span data-ttu-id="4ffde-163">Merhaba seri hale getirme biçimi onaylayın:</span><span class="sxs-lookup"><span data-stu-id="4ffde-163">Confirm hello serialization format:</span></span>

![Onayla ve sihirbazı kapatın](./media/app-insights-export-stream-analytics/150.png)

<span data-ttu-id="4ffde-165">Merhaba sihirbazı kapatın ve hello Kurulum toocomplete için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="4ffde-165">Close hello wizard and wait for hello setup toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="4ffde-166">Merhaba örnek komut toodownload bazı verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="4ffde-166">Use hello Sample command toodownload some data.</span></span> <span data-ttu-id="4ffde-167">Bu bir test örneği toodebug sorgunuzu tutun.</span><span class="sxs-lookup"><span data-stu-id="4ffde-167">Keep it as a test sample toodebug your query.</span></span>
> 
> 

## <a name="set-hello-output"></a><span data-ttu-id="4ffde-168">Set hello çıktı</span><span class="sxs-lookup"><span data-stu-id="4ffde-168">Set hello output</span></span>
<span data-ttu-id="4ffde-169">Şimdi, işi seçin ve hello çıkış ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4ffde-169">Now select your job and set hello output.</span></span>

![Merhaba yeni kanal seçin, çıkışları, Ekle, Power BI'ı tıklatın](./media/app-insights-export-stream-analytics/160.png)

<span data-ttu-id="4ffde-171">Sağlayın, **iş veya Okul hesabı** tooauthorize Stream Analytics tooaccess Power BI kaynağınız.</span><span class="sxs-lookup"><span data-stu-id="4ffde-171">Provide your **work or school account** tooauthorize Stream Analytics tooaccess your Power BI resource.</span></span> <span data-ttu-id="4ffde-172">Ardından hello çıktı için ve hello hedef Power BI veri kümesi ve tablo için bir ad oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4ffde-172">Then invent a name for hello output, and for hello target Power BI dataset and table.</span></span>

![Üç adları stok](./media/app-insights-export-stream-analytics/170.png)

## <a name="set-hello-query"></a><span data-ttu-id="4ffde-174">Set hello sorgu</span><span class="sxs-lookup"><span data-stu-id="4ffde-174">Set hello query</span></span>
<span data-ttu-id="4ffde-175">Merhaba sorgu giriş toooutput hello çevrilmesi yönetir.</span><span class="sxs-lookup"><span data-stu-id="4ffde-175">hello query governs hello translation from input toooutput.</span></span>

![Merhaba işi seçin ve sorguyu tıklayın.](./media/app-insights-export-stream-analytics/180.png)

<span data-ttu-id="4ffde-178">Merhaba sağ çıkış Al hello Test işlevi toocheck kullanın.</span><span class="sxs-lookup"><span data-stu-id="4ffde-178">Use hello Test function toocheck that you get hello right output.</span></span> <span data-ttu-id="4ffde-179">Merhaba giriş sayfadan sürdü hello örnek veri verin.</span><span class="sxs-lookup"><span data-stu-id="4ffde-179">Give it hello sample data that you took from hello inputs page.</span></span> 

### <a name="query-toodisplay-counts-of-events"></a><span data-ttu-id="4ffde-180">Sorgu toodisplay olayları sayısı</span><span class="sxs-lookup"><span data-stu-id="4ffde-180">Query toodisplay counts of events</span></span>
<span data-ttu-id="4ffde-181">Bu sorgu yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="4ffde-181">Paste this query:</span></span>

```SQL

    SELECT
      flat.ArrayValue.name,
      count(*)
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.[event]) as flat
    GROUP BY TumblingWindow(minute, 1), flat.ArrayValue.name
```

* <span data-ttu-id="4ffde-182">Biz toohello akış girişine vermiş hello diğer dışarı aktarma girişi adıdır</span><span class="sxs-lookup"><span data-stu-id="4ffde-182">export-input is hello alias we gave toohello stream input</span></span>
* <span data-ttu-id="4ffde-183">pbı çıkış tanımladığımız hello çıkış diğer adıdır</span><span class="sxs-lookup"><span data-stu-id="4ffde-183">pbi-output is hello output alias we defined</span></span>
* <span data-ttu-id="4ffde-184">Kullanırız [dış uygulamak GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) hello olay adı bir iç içe geçmiş JSON arrray olduğundan.</span><span class="sxs-lookup"><span data-stu-id="4ffde-184">We use [OUTER APPLY GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) because hello event name is in a nested JSON arrray.</span></span> <span data-ttu-id="4ffde-185">Ardından hello Select Çekmeleri bir sayısını hello hello süre ad örnekleriyle birlikte olay adı hello.</span><span class="sxs-lookup"><span data-stu-id="4ffde-185">Then hello Select picks hello event name, together with a count of hello number of instances with that name in hello time period.</span></span> <span data-ttu-id="4ffde-186">Merhaba [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) yan tümcesi süreleri 1 dakika içinde hello öğeleri gruplandırır.</span><span class="sxs-lookup"><span data-stu-id="4ffde-186">hello [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) clause groups hello elements into time periods of 1 minute.</span></span>

### <a name="query-toodisplay-metric-values"></a><span data-ttu-id="4ffde-187">Sorgu toodisplay ölçüm değerleri</span><span class="sxs-lookup"><span data-stu-id="4ffde-187">Query toodisplay metric values</span></span>
```SQL

    SELECT
      A.context.data.eventtime,
      avg(CASE WHEN flat.arrayvalue.myMetric.value IS NULL THEN 0 ELSE  flat.arrayvalue.myMetric.value END) as myValue
    INTO
      [pbi-output]
    FROM
      [export-input] A
    OUTER APPLY GetElements(A.context.custom.metrics) as flat
    GROUP BY TumblingWindow(minute, 1), A.context.data.eventtime

``` 

* <span data-ttu-id="4ffde-188">Bu sorgu hello ölçümleri telemetri tooget hello olay süresi ve hello ölçüm değeri olarak ayrıntılı açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="4ffde-188">This query drills into hello metrics telemetry tooget hello event time and hello metric value.</span></span> <span data-ttu-id="4ffde-189">Merhaba dış uygulamak GetElements düzeni tooextract hello satırları kullanırız şekilde hello ölçüm bir dizi içinde değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="4ffde-189">hello metric values are inside an array, so we use hello OUTER APPLY GetElements pattern tooextract hello rows.</span></span> <span data-ttu-id="4ffde-190">"myMetric" Merhaba hello ölçüm bu durumda adıdır.</span><span class="sxs-lookup"><span data-stu-id="4ffde-190">"myMetric" is hello name of hello metric in this case.</span></span> 

### <a name="query-tooinclude-values-of-dimension-properties"></a><span data-ttu-id="4ffde-191">Sorgu tooinclude değerleri boyut özellikleri</span><span class="sxs-lookup"><span data-stu-id="4ffde-191">Query tooinclude values of dimension properties</span></span>
```SQL

    WITH flat AS (
    SELECT
      MySource.context.data.eventTime as eventTime,
      InstanceId = MyDimension.ArrayValue.InstanceId.value,
      BusinessUnitId = MyDimension.ArrayValue.BusinessUnitId.value
    FROM MySource
    OUTER APPLY GetArrayElements(MySource.context.custom.dimensions) MyDimension
    )
    SELECT
     eventTime,
     InstanceId,
     BusinessUnitId
    INTO AIOutput
    FROM flat

```

* <span data-ttu-id="4ffde-192">Bu sorgu hello boyut dizisindeki sabit dizinindeki olan belirli bir boyut bağlı olarak hello boyut özelliklerinin değerlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="4ffde-192">This query includes values of hello dimension properties without depending on a particular dimension being at a fixed index in hello dimension array.</span></span>

## <a name="run-hello-job"></a><span data-ttu-id="4ffde-193">Merhaba işini çalıştır</span><span class="sxs-lookup"><span data-stu-id="4ffde-193">Run hello job</span></span>
<span data-ttu-id="4ffde-194">Merhaba toostart hello işten geçmiş bir tarih seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4ffde-194">You can select a date in hello past toostart hello job from.</span></span> 

![Merhaba işi seçin ve sorguyu tıklayın.](./media/app-insights-export-stream-analytics/190.png)

<span data-ttu-id="4ffde-197">Merhaba işi çalışıyor kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="4ffde-197">Wait until hello job is Running.</span></span>

## <a name="see-results-in-power-bi"></a><span data-ttu-id="4ffde-198">Power BI sonuçlarına bakın</span><span class="sxs-lookup"><span data-stu-id="4ffde-198">See results in Power BI</span></span>
> [!WARNING]
> <span data-ttu-id="4ffde-199">Çok daha iyi ve daha kolay [toodisplay Application Insights Power BI'daki veriler, önerilen yollar](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="4ffde-199">There are much better and easier [recommended ways toodisplay Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="4ffde-200">Merhaba burada gösterilen yalnızca bir örnek tooillustrate yoludur nasıl tooprocess verilen verileri.</span><span class="sxs-lookup"><span data-stu-id="4ffde-200">hello path illustrated here is just an example tooillustrate how tooprocess exported data.</span></span>
> 
> 

<span data-ttu-id="4ffde-201">Power BI iş veya Okul hesabı ve select hello dataset ve hello hello Stream Analytics işi çıkış olarak tanımlanan tablo açın.</span><span class="sxs-lookup"><span data-stu-id="4ffde-201">Open Power BI with your work or school account, and select hello dataset and table that you defined as hello output of hello Stream Analytics job.</span></span>

![Power BI'da veri kümesi ve alanları seçin.](./media/app-insights-export-stream-analytics/200.png)

<span data-ttu-id="4ffde-203">Artık bu veri kümesi raporlarında ve panolarında kullanarak [Power BI](https://powerbi.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="4ffde-203">Now you can use this dataset in reports and dashboards in [Power BI](https://powerbi.microsoft.com).</span></span>

![Power BI'da veri kümesi ve alanları seçin.](./media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a><span data-ttu-id="4ffde-205">Veri yok mu?</span><span class="sxs-lookup"><span data-stu-id="4ffde-205">No data?</span></span>
* <span data-ttu-id="4ffde-206">Denetleyin, [kümesi hello tarih biçimi](#set-path-prefix-pattern) doğru tooYYYY-aa-gg (çizgilerle ile).</span><span class="sxs-lookup"><span data-stu-id="4ffde-206">Check that you [set hello date format](#set-path-prefix-pattern) correctly tooYYYY-MM-DD (with dashes).</span></span>

## <a name="video"></a><span data-ttu-id="4ffde-207">Video</span><span class="sxs-lookup"><span data-stu-id="4ffde-207">Video</span></span>
<span data-ttu-id="4ffde-208">Noam Ben Zeev tooprocess akış analizi kullanarak verileri nasıl dışa gösterir.</span><span class="sxs-lookup"><span data-stu-id="4ffde-208">Noam Ben Zeev shows how tooprocess exported data using Stream Analytics.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4ffde-209">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4ffde-209">Next steps</span></span>
* [<span data-ttu-id="4ffde-210">Sürekli dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="4ffde-210">Continuous export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="4ffde-211">Ayrıntılı veri başvuru hello özellik türleri ve değerleri için model.</span><span class="sxs-lookup"><span data-stu-id="4ffde-211">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="4ffde-212">Application Insights</span><span class="sxs-lookup"><span data-stu-id="4ffde-212">Application Insights</span></span>](app-insights-overview.md)

