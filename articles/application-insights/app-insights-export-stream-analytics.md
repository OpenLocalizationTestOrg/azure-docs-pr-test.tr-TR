---
title: "Azure Application Insights gelen akış analizi kullanarak dışarı aktarma | Microsoft Docs"
description: "Akış analizi sürekli dönüştürme, filtre uygulayabilir ve rota verilerini Application Insights ' dışarı aktar."
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
ms.openlocfilehash: 6a84d8ff67c420ce712de905ab1172632502a863
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="use-stream-analytics-to-process-exported-data-from-application-insights"></a><span data-ttu-id="a6b80-103">Application Insights dışarı aktarılan verileri işlemek için Stream Analytics kullanın</span><span class="sxs-lookup"><span data-stu-id="a6b80-103">Use Stream Analytics to process exported data from Application Insights</span></span>
<span data-ttu-id="a6b80-104">[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) veri işleme için ideal araçtır [Application Insights ' dışarı](app-insights-export-telemetry.md).</span><span class="sxs-lookup"><span data-stu-id="a6b80-104">[Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/) is the ideal tool for processing data [exported from Application Insights](app-insights-export-telemetry.md).</span></span> <span data-ttu-id="a6b80-105">Akış analizi, çeşitli kaynaklardan veri çeker.</span><span class="sxs-lookup"><span data-stu-id="a6b80-105">Stream Analytics can pull data from a variety of sources.</span></span> <span data-ttu-id="a6b80-106">Bu dönüştürme ve verilere filtre ve ardından havuzlarını çeşitli için rota.</span><span class="sxs-lookup"><span data-stu-id="a6b80-106">It can transform and filter the data, and then route it to a variety of sinks.</span></span>

<span data-ttu-id="a6b80-107">Bu örnekte, yeniden adlandırır Application Insights ' verileri alır ve bazı alanlar işler ve Power BI kanallar bir bağdaştırıcıya oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="a6b80-107">In this example, we'll create an adaptor that takes data from Application Insights, renames and processes some of the fields, and pipes it into Power BI.</span></span>

> [!WARNING]
> <span data-ttu-id="a6b80-108">Çok daha iyi ve daha kolay [Power BI'da Application Insights verileri görüntülemek için önerilen yollar](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="a6b80-108">There are much better and easier [recommended ways to display Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="a6b80-109">Burada gösterilen yol dışarı aktarılan verileri işlemek nasıl göstermek üzere yalnızca bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="a6b80-109">The path illustrated here is just an example to illustrate how to process exported data.</span></span>
> 
> 

![Blok Diyagramı PBI SA aracılığıyla dışarı aktarma](./media/app-insights-export-stream-analytics/020.png)

## <a name="create-storage-in-azure"></a><span data-ttu-id="a6b80-111">Depolama oluşturma</span><span class="sxs-lookup"><span data-stu-id="a6b80-111">Create storage in Azure</span></span>
<span data-ttu-id="a6b80-112">Depolama oluşturmanız gerekir böylece sürekli verme verileri Azure depolama hesabı her zaman çıkarır.</span><span class="sxs-lookup"><span data-stu-id="a6b80-112">Continuous export always outputs data to an Azure Storage account, so you need to create the storage first.</span></span>

1. <span data-ttu-id="a6b80-113">Aboneliğinizde bir "Klasik" depolama hesabı oluşturun [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a6b80-113">Create a "classic" storage account in your subscription in the [Azure portal](https://portal.azure.com).</span></span>
   
   ![Azure portalında yeni, verileri depolama seçin](./media/app-insights-export-stream-analytics/030.png)
2. <span data-ttu-id="a6b80-115">Bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a6b80-115">Create a container</span></span>
   
    ![Yeni depolama kapsayıcıları seçin, kapsayıcıları döşeme tıklatın ve ardından Ekle](./media/app-insights-export-stream-analytics/040.png)
3. <span data-ttu-id="a6b80-117">Depolama erişim tuşu kopyalama</span><span class="sxs-lookup"><span data-stu-id="a6b80-117">Copy the storage access key</span></span>
   
    <span data-ttu-id="a6b80-118">Akış analizi hizmetine giriş yakında ayarlamak için gerekir.</span><span class="sxs-lookup"><span data-stu-id="a6b80-118">You'll need it soon to set up the input to the stream analytics service.</span></span>
   
    ![Depolama ayarlarını, anahtarları, açın ve birincil erişim tuşunu bir kopyasını alın](./media/app-insights-export-stream-analytics/045.png)

## <a name="start-continuous-export-to-azure-storage"></a><span data-ttu-id="a6b80-120">Azure depolama alanına sürekli verme Başlat</span><span class="sxs-lookup"><span data-stu-id="a6b80-120">Start continuous export to Azure storage</span></span>
<span data-ttu-id="a6b80-121">[Sürekli verme](app-insights-export-telemetry.md) Application Insights Azure depolama alanına gelen verileri taşır.</span><span class="sxs-lookup"><span data-stu-id="a6b80-121">[Continuous export](app-insights-export-telemetry.md) moves data from Application Insights into Azure storage.</span></span>

1. <span data-ttu-id="a6b80-122">Azure portalında, uygulamanız için oluşturduğunuz Application Insights kaynağı göz atın.</span><span class="sxs-lookup"><span data-stu-id="a6b80-122">In the Azure portal, browse to the Application Insights resource you created for your application.</span></span>
   
    ![Gözat, Application Insights, uygulamanızı seçin](./media/app-insights-export-stream-analytics/050.png)
2. <span data-ttu-id="a6b80-124">Sürekli verme oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a6b80-124">Create a continuous export.</span></span>
   
    ![Ayarları, sürekli verme ekleme seçin](./media/app-insights-export-stream-analytics/060.png)

    <span data-ttu-id="a6b80-126">Daha önce oluşturduğunuz depolama hesabı seçin:</span><span class="sxs-lookup"><span data-stu-id="a6b80-126">Select the storage account you created earlier:</span></span>

    ![Dışa aktarma hedefi ayarlama](./media/app-insights-export-stream-analytics/070.png)

    <span data-ttu-id="a6b80-128">Görmek istediğiniz olay türlerini ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="a6b80-128">Set the event types you want to see:</span></span>

    ![Olay türlerini seçin](./media/app-insights-export-stream-analytics/080.png)

1. <span data-ttu-id="a6b80-130">Accumulate bazı veriler sağlar.</span><span class="sxs-lookup"><span data-stu-id="a6b80-130">Let some data accumulate.</span></span> <span data-ttu-id="a6b80-131">Arkanıza yaslanın ve kişilere uygulamanızın biraz kullanın.</span><span class="sxs-lookup"><span data-stu-id="a6b80-131">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="a6b80-132">Telemetri geldikçe ve istatistiksel grafiklerde görürsünüz [ölçüm Gezgini](app-insights-metrics-explorer.md) ve olayları tek tek [tanılama arama](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="a6b80-132">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="a6b80-133">Ve ayrıca, verileri depolama alanınızın dışa aktarır.</span><span class="sxs-lookup"><span data-stu-id="a6b80-133">And also, the data will export to your storage.</span></span> 
2. <span data-ttu-id="a6b80-134">Dışarı aktarılan verileri inceleyin.</span><span class="sxs-lookup"><span data-stu-id="a6b80-134">Inspect the exported data.</span></span> <span data-ttu-id="a6b80-135">Visual Studio'da, **görüntülemek / Cloud Explorer**ve Azure açın / depolama.</span><span class="sxs-lookup"><span data-stu-id="a6b80-135">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="a6b80-136">(Bu menü seçeneği yoksa, Azure SDK'yı yüklemeniz gerekir: Yeni Proje iletişim kutusunu açın ve Visual C# açın / bulut / .NET için Microsoft Azure SDK'sını alın.)</span><span class="sxs-lookup"><span data-stu-id="a6b80-136">(If you don't have this menu option, you need to install the Azure SDK: Open the New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![](./media/app-insights-export-stream-analytics/04-data.png)
   
    <span data-ttu-id="a6b80-137">Uygulama adı ve araçları anahtarından türetilen yol adı, ortak parçası not edin.</span><span class="sxs-lookup"><span data-stu-id="a6b80-137">Make a note of the common part of the path name, which is derived from the application name and instrumentation key.</span></span> 

<span data-ttu-id="a6b80-138">JSON biçiminde dosyaları blob yazılır.</span><span class="sxs-lookup"><span data-stu-id="a6b80-138">The events are written to blob files in JSON format.</span></span> <span data-ttu-id="a6b80-139">Her dosya bir veya daha fazla olaylar içerebilir.</span><span class="sxs-lookup"><span data-stu-id="a6b80-139">Each file may contain one or more events.</span></span> <span data-ttu-id="a6b80-140">Bu nedenle olay verileri okumak ve istiyoruz alanları filtrelemek isteriz.</span><span class="sxs-lookup"><span data-stu-id="a6b80-140">So we'd like to read the event data and filter out the fields we want.</span></span> <span data-ttu-id="a6b80-141">Her türlü verilerle yapabileceğimiz bir şey vardır, ancak bizim planı bugün Stream Analytics Power BI veri kanal kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="a6b80-141">There are all kinds of things we could do with the data, but our plan today is to use Stream Analytics to pipe the data to Power BI.</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="a6b80-142">Bir Azure akış analizi örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="a6b80-142">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="a6b80-143">Gelen [Klasik Azure portalı](https://manage.windowsazure.com/), Azure Stream Analytics hizmeti seçin ve yeni bir Stream Analytics işi oluştur:</span><span class="sxs-lookup"><span data-stu-id="a6b80-143">From the [Classic Azure Portal](https://manage.windowsazure.com/), select the Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-export-stream-analytics/090.png)

![](./media/app-insights-export-stream-analytics/100.png)

<span data-ttu-id="a6b80-144">Yeni iş oluşturulduğunda ayrıntılarını genişletin:</span><span class="sxs-lookup"><span data-stu-id="a6b80-144">When the new job is created, expand its details:</span></span>

![](./media/app-insights-export-stream-analytics/110.png)

### <a name="set-blob-location"></a><span data-ttu-id="a6b80-145">Blob konum ayarlama</span><span class="sxs-lookup"><span data-stu-id="a6b80-145">Set blob location</span></span>
<span data-ttu-id="a6b80-146">Sürekli verme blobundan giriş gerçekleştirecek şekilde ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="a6b80-146">Set it to take input from your Continuous Export blob:</span></span>

![](./media/app-insights-export-stream-analytics/120.png)

<span data-ttu-id="a6b80-147">Şimdi, depolama, daha önce not ettiğiniz hesabınızdan, birincil erişim anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="a6b80-147">Now you'll need the Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="a6b80-148">Bu depolama hesabı anahtarı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a6b80-148">Set this as the Storage Account Key.</span></span>

![](./media/app-insights-export-stream-analytics/130.png)

### <a name="set-path-prefix-pattern"></a><span data-ttu-id="a6b80-149">Set yol önek deseni</span><span class="sxs-lookup"><span data-stu-id="a6b80-149">Set path prefix pattern</span></span>
![](./media/app-insights-export-stream-analytics/140.png)

<span data-ttu-id="a6b80-150">**Tarih biçimi YYYY-AA-GG (tire ile) ayarladığınızdan emin olun.**</span><span class="sxs-lookup"><span data-stu-id="a6b80-150">**Be sure to set the Date Format to YYYY-MM-DD (with dashes).**</span></span>

<span data-ttu-id="a6b80-151">Stream Analytics girdi dosyaları depolama burada bulur önek yol deseni belirtir.</span><span class="sxs-lookup"><span data-stu-id="a6b80-151">The Path Prefix Pattern specifies where Stream Analytics finds the input files in the storage.</span></span> <span data-ttu-id="a6b80-152">Bunu sürekli verme verileri nasıl depolar karşılık gelecek şekilde ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a6b80-152">You need to set it to correspond to how Continuous Export stores the data.</span></span> <span data-ttu-id="a6b80-153">Aşağıdaki gibi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="a6b80-153">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="a6b80-154">Bu örnekte:</span><span class="sxs-lookup"><span data-stu-id="a6b80-154">In this example:</span></span>

* <span data-ttu-id="a6b80-155">`webapplication27`Application Insights kaynağı adı **tüm küçük**.</span><span class="sxs-lookup"><span data-stu-id="a6b80-155">`webapplication27` is the name of the Application Insights resource **all lower case**.</span></span>
* <span data-ttu-id="a6b80-156">`1234...`Application Insights kaynağı izleme anahtarını olan **tire atlama**.</span><span class="sxs-lookup"><span data-stu-id="a6b80-156">`1234...` is the instrumentation key of the Application Insights resource, **omitting dashes**.</span></span> 
* <span data-ttu-id="a6b80-157">`PageViews`Analiz etmek istediğiniz veri türüdür.</span><span class="sxs-lookup"><span data-stu-id="a6b80-157">`PageViews` is the type of data you want to analyze.</span></span> <span data-ttu-id="a6b80-158">Kullanılabilir türler filtresi sürekli dışarı aktarma ile Ayarla bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="a6b80-158">The available types depend on the filter you set in Continuous Export.</span></span> <span data-ttu-id="a6b80-159">Diğer kullanılabilir türleri görmek ve görmek için dışarı aktarılan verileri incelemek [veri modeli verme](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="a6b80-159">Examine the exported data to see the other available types, and see the [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="a6b80-160">`/{date}/{time}`bir desen tam anlamıyla yazılır.</span><span class="sxs-lookup"><span data-stu-id="a6b80-160">`/{date}/{time}` is a pattern written literally.</span></span>

> [!NOTE]
> <span data-ttu-id="a6b80-161">Yolun sağ alma emin olmak için depolama inceleyin.</span><span class="sxs-lookup"><span data-stu-id="a6b80-161">Inspect the storage to make sure you get the path right.</span></span>
> 
> 

### <a name="finish-initial-setup"></a><span data-ttu-id="a6b80-162">İlk Kurulumu tamamlayın</span><span class="sxs-lookup"><span data-stu-id="a6b80-162">Finish initial setup</span></span>
<span data-ttu-id="a6b80-163">Seri hale getirme biçimi onaylayın:</span><span class="sxs-lookup"><span data-stu-id="a6b80-163">Confirm the serialization format:</span></span>

![Onayla ve sihirbazı kapatın](./media/app-insights-export-stream-analytics/150.png)

<span data-ttu-id="a6b80-165">Sihirbazı kapatmak ve kurulumun tamamlanması için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="a6b80-165">Close the wizard and wait for the setup to complete.</span></span>

> [!TIP]
> <span data-ttu-id="a6b80-166">Bazı veri indirmek için örnek komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="a6b80-166">Use the Sample command to download some data.</span></span> <span data-ttu-id="a6b80-167">Sorgunuz hata ayıklamak için bir test örneği tutun.</span><span class="sxs-lookup"><span data-stu-id="a6b80-167">Keep it as a test sample to debug your query.</span></span>
> 
> 

## <a name="set-the-output"></a><span data-ttu-id="a6b80-168">Çıktı ayarlayın</span><span class="sxs-lookup"><span data-stu-id="a6b80-168">Set the output</span></span>
<span data-ttu-id="a6b80-169">Şimdi, işi seçin ve çıktı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a6b80-169">Now select your job and set the output.</span></span>

![Yeni kanal seçin, çıkışları, Ekle, Power BI'ı tıklatın](./media/app-insights-export-stream-analytics/160.png)

<span data-ttu-id="a6b80-171">Sağlayın, **iş veya Okul hesabı** akış analizi, Power BI kaynağa erişmek için yetki vermek için.</span><span class="sxs-lookup"><span data-stu-id="a6b80-171">Provide your **work or school account** to authorize Stream Analytics to access your Power BI resource.</span></span> <span data-ttu-id="a6b80-172">Ardından çıktı için ve tablo ve hedef Power BI veri kümesi için bir ad oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a6b80-172">Then invent a name for the output, and for the target Power BI dataset and table.</span></span>

![Üç adları stok](./media/app-insights-export-stream-analytics/170.png)

## <a name="set-the-query"></a><span data-ttu-id="a6b80-174">Sorgu ayarlayın</span><span class="sxs-lookup"><span data-stu-id="a6b80-174">Set the query</span></span>
<span data-ttu-id="a6b80-175">Sorgu çıktısını almak için giriş çevrilmesi yönetir.</span><span class="sxs-lookup"><span data-stu-id="a6b80-175">The query governs the translation from input to output.</span></span>

![İşi seçin ve sorguyu tıklayın.](./media/app-insights-export-stream-analytics/180.png)

<span data-ttu-id="a6b80-178">Doğru çıkış Al denetlemek için Test işlevini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a6b80-178">Use the Test function to check that you get the right output.</span></span> <span data-ttu-id="a6b80-179">Giriş sayfasından sürdü örnek verileri verin.</span><span class="sxs-lookup"><span data-stu-id="a6b80-179">Give it the sample data that you took from the inputs page.</span></span> 

### <a name="query-to-display-counts-of-events"></a><span data-ttu-id="a6b80-180">Olayların sayısını görüntülemek için sorgu</span><span class="sxs-lookup"><span data-stu-id="a6b80-180">Query to display counts of events</span></span>
<span data-ttu-id="a6b80-181">Bu sorgu yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="a6b80-181">Paste this query:</span></span>

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

* <span data-ttu-id="a6b80-182">dışarı aktarma girişi biz Giriş akışı verdiğiniz diğer adıdır</span><span class="sxs-lookup"><span data-stu-id="a6b80-182">export-input is the alias we gave to the stream input</span></span>
* <span data-ttu-id="a6b80-183">Biz tanımlanan çıkış diğer pbı çıkış adıdır</span><span class="sxs-lookup"><span data-stu-id="a6b80-183">pbi-output is the output alias we defined</span></span>
* <span data-ttu-id="a6b80-184">Kullanırız [dış uygulamak GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) olay adı bir iç içe geçmiş JSON arrray olduğundan.</span><span class="sxs-lookup"><span data-stu-id="a6b80-184">We use [OUTER APPLY GetElements](https://msdn.microsoft.com/library/azure/dn706229.aspx) because the event name is in a nested JSON arrray.</span></span> <span data-ttu-id="a6b80-185">Sonra Seç süre ad örnekleriyle sayısını birlikte olay adı seçer.</span><span class="sxs-lookup"><span data-stu-id="a6b80-185">Then the Select picks the event name, together with a count of the number of instances with that name in the time period.</span></span> <span data-ttu-id="a6b80-186">[Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) yan tümcesi süreleri 1 dakika içinde öğeleri gruplandırır.</span><span class="sxs-lookup"><span data-stu-id="a6b80-186">The [Group By](https://msdn.microsoft.com/library/azure/dn835023.aspx) clause groups the elements into time periods of 1 minute.</span></span>

### <a name="query-to-display-metric-values"></a><span data-ttu-id="a6b80-187">Ölçü değerlerini görüntülemek için sorgu</span><span class="sxs-lookup"><span data-stu-id="a6b80-187">Query to display metric values</span></span>
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

* <span data-ttu-id="a6b80-188">Bu sorgu olay süresi ve ölçüm değeri almak için ölçümleri telemetri ayrıntılı açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a6b80-188">This query drills into the metrics telemetry to get the event time and the metric value.</span></span> <span data-ttu-id="a6b80-189">Dış uygulamak GetElements düzeni satırları ayıklamak için kullanırız şekilde ölçüm bir dizi içinde değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="a6b80-189">The metric values are inside an array, so we use the OUTER APPLY GetElements pattern to extract the rows.</span></span> <span data-ttu-id="a6b80-190">"myMetric" ölçüm bu durumda adıdır.</span><span class="sxs-lookup"><span data-stu-id="a6b80-190">"myMetric" is the name of the metric in this case.</span></span> 

### <a name="query-to-include-values-of-dimension-properties"></a><span data-ttu-id="a6b80-191">Boyut özelliklerinin değerlerini dahil etmek için sorgu</span><span class="sxs-lookup"><span data-stu-id="a6b80-191">Query to include values of dimension properties</span></span>
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

* <span data-ttu-id="a6b80-192">Bu sorgu boyut dizisindeki sabit dizinindeki olan belirli bir boyut bağlı olarak boyut özelliklerinin değerlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="a6b80-192">This query includes values of the dimension properties without depending on a particular dimension being at a fixed index in the dimension array.</span></span>

## <a name="run-the-job"></a><span data-ttu-id="a6b80-193">İşi çalıştır</span><span class="sxs-lookup"><span data-stu-id="a6b80-193">Run the job</span></span>
<span data-ttu-id="a6b80-194">İşten başlatmak için geçmiş bir tarih seçin.</span><span class="sxs-lookup"><span data-stu-id="a6b80-194">You can select a date in the past to start the job from.</span></span> 

![İşi seçin ve sorguyu tıklayın.](./media/app-insights-export-stream-analytics/190.png)

<span data-ttu-id="a6b80-197">İş çalışıyor kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="a6b80-197">Wait until the job is Running.</span></span>

## <a name="see-results-in-power-bi"></a><span data-ttu-id="a6b80-198">Power BI sonuçlarına bakın</span><span class="sxs-lookup"><span data-stu-id="a6b80-198">See results in Power BI</span></span>
> [!WARNING]
> <span data-ttu-id="a6b80-199">Çok daha iyi ve daha kolay [Power BI'da Application Insights verileri görüntülemek için önerilen yollar](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="a6b80-199">There are much better and easier [recommended ways to display Application Insights data in Power BI](app-insights-export-power-bi.md).</span></span> <span data-ttu-id="a6b80-200">Burada gösterilen yol dışarı aktarılan verileri işlemek nasıl göstermek üzere yalnızca bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="a6b80-200">The path illustrated here is just an example to illustrate how to process exported data.</span></span>
> 
> 

<span data-ttu-id="a6b80-201">Power BI ile iş açın veya Okul hesabı ve veri kümesi ve Stream Analytics işi çıkış olarak tanımlanan tablo seçin.</span><span class="sxs-lookup"><span data-stu-id="a6b80-201">Open Power BI with your work or school account, and select the dataset and table that you defined as the output of the Stream Analytics job.</span></span>

![Power BI'da veri kümesi ve alanları seçin.](./media/app-insights-export-stream-analytics/200.png)

<span data-ttu-id="a6b80-203">Artık bu veri kümesi raporlarında ve panolarında kullanarak [Power BI](https://powerbi.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="a6b80-203">Now you can use this dataset in reports and dashboards in [Power BI](https://powerbi.microsoft.com).</span></span>

![Power BI'da veri kümesi ve alanları seçin.](./media/app-insights-export-stream-analytics/210.png)

## <a name="no-data"></a><span data-ttu-id="a6b80-205">Veri yok mu?</span><span class="sxs-lookup"><span data-stu-id="a6b80-205">No data?</span></span>
* <span data-ttu-id="a6b80-206">Denetleyin, [tarih biçimini ayarladıktan](#set-path-prefix-pattern) doğru olarak YYYY-AA-GG (çizgilerle ile).</span><span class="sxs-lookup"><span data-stu-id="a6b80-206">Check that you [set the date format](#set-path-prefix-pattern) correctly to YYYY-MM-DD (with dashes).</span></span>

## <a name="video"></a><span data-ttu-id="a6b80-207">Video</span><span class="sxs-lookup"><span data-stu-id="a6b80-207">Video</span></span>
<span data-ttu-id="a6b80-208">Noam Ben Zeev kullanarak Stream Analytics dışarı aktarılan verileri işlemek nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="a6b80-208">Noam Ben Zeev shows how to process exported data using Stream Analytics.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Export-to-Power-BI-from-Application-Insights/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a6b80-209">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a6b80-209">Next steps</span></span>
* [<span data-ttu-id="a6b80-210">Sürekli dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="a6b80-210">Continuous export</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="a6b80-211">Ayrıntılı veri özellik türleri ve değerleri için başvuru modeli.</span><span class="sxs-lookup"><span data-stu-id="a6b80-211">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="a6b80-212">Application Insights</span><span class="sxs-lookup"><span data-stu-id="a6b80-212">Application Insights</span></span>](app-insights-overview.md)

