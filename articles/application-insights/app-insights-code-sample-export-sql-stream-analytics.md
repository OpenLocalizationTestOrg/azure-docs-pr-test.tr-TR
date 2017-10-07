---
title: Azure Application Insights tooSQL verme | Microsoft Docs
description: "Sürekli olarak kullanarak Stream Analytics Application Insights veri tooSQL verin."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 48903032-2c99-4987-9948-d6e4559b4a63
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/06/2015
ms.author: bwren
ms.openlocfilehash: 58b579499113751a088dc7e66cbec71529773322
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-export-toosql-from-application-insights-using-stream-analytics"></a><span data-ttu-id="caa75-103">İzlenecek yol: uygulama kullanarak Stream Analytics ilişkin bilgiler tooSQL dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="caa75-103">Walkthrough: Export tooSQL from Application Insights using Stream Analytics</span></span>
<span data-ttu-id="caa75-104">Bu makalede gösterilmektedir nasıl toomove telemetri verilerinizden [Azure Application Insights] [ start] kullanarak bir Azure SQL veritabanına [sürekli verme] [ export] ve [Azure akış analizi](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="caa75-104">This article shows how toomove your telemetry data from [Azure Application Insights][start] into an Azure SQL database by using [Continuous Export][export] and [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> 

<span data-ttu-id="caa75-105">Sürekli verme telemetri verileri JSON biçiminde Azure depolama alanına taşır.</span><span class="sxs-lookup"><span data-stu-id="caa75-105">Continuous export moves your telemetry data into Azure Storage in JSON format.</span></span> <span data-ttu-id="caa75-106">Biz Azure akış analizi kullanarak hello JSON nesneleri ayrıştırabilir ve bir veritabanı tablosundaki satırları oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="caa75-106">We'll parse hello JSON objects using Azure Stream Analytics and create rows in a database table.</span></span>

<span data-ttu-id="caa75-107">(Daha genel olarak, sürekli verme hello yolu toodo olduğundan, kendi analiz hello telemetri uygulamalarınızı tooApplication Öngörüler Gönder.</span><span class="sxs-lookup"><span data-stu-id="caa75-107">(More generally, Continuous Export is hello way toodo your own analysis of hello telemetry your apps send tooApplication Insights.</span></span> <span data-ttu-id="caa75-108">Bu kod örneği toodo veri toplama gibi hello dışarı telemetri ile başka şeyler uyarlayabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="caa75-108">You could adapt this code sample toodo other things with hello exported telemetry, such as aggregation of data.)</span></span>

<span data-ttu-id="caa75-109">Merhaba varsayımıyla toomonitor hello uygulamayı zaten sahip başlayacağız.</span><span class="sxs-lookup"><span data-stu-id="caa75-109">We'll start with hello assumption that you already have hello app you want toomonitor.</span></span>

<span data-ttu-id="caa75-110">Bu örnekte, biz hello sayfası görünüm verilerini kullanarak, ancak hello aynı düzeni kolayca tooother veri türleri özel etkinlikler ve özel durumlar gibi genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="caa75-110">In this example, we will be using hello page view data, but hello same pattern can easily be extended tooother data types such as custom events and exceptions.</span></span> 

## <a name="add-application-insights-tooyour-application"></a><span data-ttu-id="caa75-111">Application Insights tooyour uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="caa75-111">Add Application Insights tooyour application</span></span>
<span data-ttu-id="caa75-112">tooget başlatıldı:</span><span class="sxs-lookup"><span data-stu-id="caa75-112">tooget started:</span></span>

1. <span data-ttu-id="caa75-113">[Web sayfalarınız için Application Insights'ı ayarlamak](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="caa75-113">[Set up Application Insights for your web pages](app-insights-javascript.md).</span></span> 
   
    <span data-ttu-id="caa75-114">(Bu örnekte, sayfa görünümü verileri hello istemci tarayıcıları işleme biz odaklanmak, ancak Application Insights'ı için hello sunucu tarafı ayarlayabilir, [Java](app-insights-java-get-started.md) veya [ASP.NET](app-insights-asp-net.md) uygulama ve işlem isteği bağımlılık ve diğer sunucu telemetri.)</span><span class="sxs-lookup"><span data-stu-id="caa75-114">(In this example, we'll focus on processing page view data from hello client browsers, but you could also set up Application Insights for hello server side of your [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md) app and process request, dependency and other server telemetry.)</span></span>
2. <span data-ttu-id="caa75-115">Uygulamanızı yayımlayın ve telemetri verilerini Application Insights kaynağınıza görünmesini izleyin.</span><span class="sxs-lookup"><span data-stu-id="caa75-115">Publish your app, and watch telemetry data appearing in your Application Insights resource.</span></span>

## <a name="create-storage-in-azure"></a><span data-ttu-id="caa75-116">Depolama oluşturma</span><span class="sxs-lookup"><span data-stu-id="caa75-116">Create storage in Azure</span></span>
<span data-ttu-id="caa75-117">Toocreate hello depolama önce gerekir böylece sürekli dışarı aktarma veri tooan Azure depolama hesabı, her zaman çıkarır.</span><span class="sxs-lookup"><span data-stu-id="caa75-117">Continuous export always outputs data tooan Azure Storage account, so you need toocreate hello storage first.</span></span>

1. <span data-ttu-id="caa75-118">Merhaba, aboneliğinizde depolama hesabı oluşturma [Azure portal][portal].</span><span class="sxs-lookup"><span data-stu-id="caa75-118">Create a storage account in your subscription in hello [Azure portal][portal].</span></span>
   
    ![Azure portalında yeni, verileri depolama birimi seçin.](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. <span data-ttu-id="caa75-122">Bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="caa75-122">Create a container</span></span>
   
    ![Merhaba yeni depolama kapsayıcıları seçin, Merhaba kapsayıcılara döşeme tıklatın ve ardından Ekle](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. <span data-ttu-id="caa75-124">Merhaba depolama erişim tuşu kopyalama</span><span class="sxs-lookup"><span data-stu-id="caa75-124">Copy hello storage access key</span></span>
   
    <span data-ttu-id="caa75-125">Bunu en kısa sürede tooset hello giriş toohello stream analytics hizmeti yukarı ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="caa75-125">You'll need it soon tooset up hello input toohello stream analytics service.</span></span>
   
    ![Merhaba depolama ayarları, anahtarları, açın ve hello birincil erişim anahtarını bir kopyasını alın](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-tooazure-storage"></a><span data-ttu-id="caa75-127">Sürekli verme tooAzure depolama Başlat</span><span class="sxs-lookup"><span data-stu-id="caa75-127">Start continuous export tooAzure storage</span></span>
1. <span data-ttu-id="caa75-128">Hello Azure portal, uygulamanız için oluşturulan toohello Application Insights kaynağı göz atın.</span><span class="sxs-lookup"><span data-stu-id="caa75-128">In hello Azure portal, browse toohello Application Insights resource you created for your application.</span></span>
   
    ![Gözat, Application Insights, uygulamanızı seçin](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. <span data-ttu-id="caa75-130">Sürekli verme oluşturun.</span><span class="sxs-lookup"><span data-stu-id="caa75-130">Create a continuous export.</span></span>
   
    ![Ayarları, sürekli verme ekleme seçin](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    <span data-ttu-id="caa75-132">Daha önce oluşturduğunuz hello depolama hesabı seçin:</span><span class="sxs-lookup"><span data-stu-id="caa75-132">Select hello storage account you created earlier:</span></span>

    ![Merhaba dışa aktarma hedefi ayarlama](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    <span data-ttu-id="caa75-134">İstediğiniz hello olay türlerini toosee ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="caa75-134">Set hello event types you want toosee:</span></span>

    ![Olay türlerini seçin](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. <span data-ttu-id="caa75-136">Accumulate bazı veriler sağlar.</span><span class="sxs-lookup"><span data-stu-id="caa75-136">Let some data accumulate.</span></span> <span data-ttu-id="caa75-137">Arkanıza yaslanın ve kişilere uygulamanızın biraz kullanın.</span><span class="sxs-lookup"><span data-stu-id="caa75-137">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="caa75-138">Telemetri geldikçe ve istatistiksel grafiklerde görürsünüz [ölçüm Gezgini](app-insights-metrics-explorer.md) ve olayları tek tek [tanılama arama](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="caa75-138">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="caa75-139">Ve ayrıca hello veri tooyour depolama dışa aktarır.</span><span class="sxs-lookup"><span data-stu-id="caa75-139">And also, hello data will export tooyour storage.</span></span> 
2. <span data-ttu-id="caa75-140">Merhaba portalında ya da dışa hello verileri - Seç **Gözat**, depolama hesabınızı seçin ve ardından **kapsayıcıları** - ya da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="caa75-140">Inspect hello exported data, either in hello portal - choose **Browse**, select your storage account, and then **Containers** - or in Visual Studio.</span></span> <span data-ttu-id="caa75-141">Visual Studio'da, **görüntülemek / Cloud Explorer**ve Azure açın / depolama.</span><span class="sxs-lookup"><span data-stu-id="caa75-141">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="caa75-142">(Bu menü seçeneği yoksa, tooinstall hello Azure SDK'sı gerekir: hello yeni proje iletişim kutusu açın ve Visual C# açın / bulut / .NET için Microsoft Azure SDK'sını alın.)</span><span class="sxs-lookup"><span data-stu-id="caa75-142">(If you don't have this menu option, you need tooinstall hello Azure SDK: Open hello New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![Visual Studio'da açın Server Browser, Azure, depolama](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    <span data-ttu-id="caa75-144">Merhaba ortak hello uygulama adı ve araçları anahtarından türetilen hello yol adı parçası not edin.</span><span class="sxs-lookup"><span data-stu-id="caa75-144">Make a note of hello common part of hello path name, which is derived from hello application name and instrumentation key.</span></span> 

<span data-ttu-id="caa75-145">Merhaba olayları tooblob dosyaları JSON biçiminde yazılır.</span><span class="sxs-lookup"><span data-stu-id="caa75-145">hello events are written tooblob files in JSON format.</span></span> <span data-ttu-id="caa75-146">Her dosya bir veya daha fazla olaylar içerebilir.</span><span class="sxs-lookup"><span data-stu-id="caa75-146">Each file may contain one or more events.</span></span> <span data-ttu-id="caa75-147">Bu nedenle tooread hello olay verileri ve filtre istiyoruz hello alanları isteriz.</span><span class="sxs-lookup"><span data-stu-id="caa75-147">So we'd like tooread hello event data and filter out hello fields we want.</span></span> <span data-ttu-id="caa75-148">Her türlü hello verilerle yapabileceğimiz bir şey vardır, ancak bizim planı bugün toouse Stream Analytics toomove hello veri tooa SQL veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="caa75-148">There are all kinds of things we could do with hello data, but our plan today is toouse Stream Analytics toomove hello data tooa SQL database.</span></span> <span data-ttu-id="caa75-149">Bu kolay toorun çok sayıda ilginç sorguları hale getirir.</span><span class="sxs-lookup"><span data-stu-id="caa75-149">That will make it easy toorun lots of interesting queries.</span></span>

## <a name="create-an-azure-sql-database"></a><span data-ttu-id="caa75-150">Bir Azure SQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="caa75-150">Create an Azure SQL Database</span></span>
<span data-ttu-id="caa75-151">Bir kez daha, aboneliğinizde başlayarak [Azure portal][portal], hello veritabanı oluşturma (ve yeni bir sunucu zaten bir olduğuna sürece) toowhich hello veri yazma.</span><span class="sxs-lookup"><span data-stu-id="caa75-151">Once again starting from your subscription in [Azure portal][portal], create hello database (and a new server, unless you've already got one) toowhich you'll write hello data.</span></span>

![Yeni, verileri, SQL](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

<span data-ttu-id="caa75-153">Merhaba veritabanı sunucusunu tooAzure Hizmetleri erişimine izin verdiğinden emin olun:</span><span class="sxs-lookup"><span data-stu-id="caa75-153">Make sure that hello database server allows access tooAzure services:</span></span>

![Gözat, sunucuları, sunucunuz, ayarları, güvenlik duvarı, erişim izni tooAzure](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a><span data-ttu-id="caa75-155">Azure SQL DB tablosu oluşturma</span><span class="sxs-lookup"><span data-stu-id="caa75-155">Create a table in Azure SQL DB</span></span>
<span data-ttu-id="caa75-156">Tercih edilen Yönetim aracınızla hello önceki bölümde oluşturduğunuz toohello veritabanını bağlayın.</span><span class="sxs-lookup"><span data-stu-id="caa75-156">Connect toohello database created in hello previous section with your preferred management tool.</span></span> <span data-ttu-id="caa75-157">Bu kılavuzda, biz kullanacağınız [SQL Server Yönetim Araçları](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="caa75-157">In this walkthrough, we will be using [SQL Server Management Tools](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

<span data-ttu-id="caa75-158">Yeni bir sorgu oluşturun ve aşağıdaki T-SQL hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="caa75-158">Create a new query, and execute hello following T-SQL:</span></span>

```SQL

CREATE TABLE [dbo].[PageViewsTable](
    [pageName] [nvarchar](max) NOT NULL,
    [viewCount] [int] NOT NULL,
    [url] [nvarchar](max) NULL,
    [urlDataPort] [int] NULL,
    [urlDataprotocol] [nvarchar](50) NULL,
    [urlDataHost] [nvarchar](50) NULL,
    [urlDataBase] [nvarchar](50) NULL,
    [urlDataHashTag] [nvarchar](max) NULL,
    [eventTime] [datetime] NOT NULL,
    [isSynthetic] [nvarchar](50) NULL,
    [deviceId] [nvarchar](50) NULL,
    [deviceType] [nvarchar](50) NULL,
    [os] [nvarchar](50) NULL,
    [osVersion] [nvarchar](50) NULL,
    [locale] [nvarchar](50) NULL,
    [userAgent] [nvarchar](max) NULL,
    [browser] [nvarchar](50) NULL,
    [browserVersion] [nvarchar](50) NULL,
    [screenResolution] [nvarchar](50) NULL,
    [sessionId] [nvarchar](max) NULL,
    [sessionIsFirst] [nvarchar](50) NULL,
    [clientIp] [nvarchar](50) NULL,
    [continent] [nvarchar](50) NULL,
    [country] [nvarchar](50) NULL,
    [province] [nvarchar](50) NULL,
    [city] [nvarchar](50) NULL
)

CREATE CLUSTERED INDEX [pvTblIdx] ON [dbo].[PageViewsTable]
(
    [eventTime] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, SORT_IN_TEMPDB = OFF, DROP_EXISTING = OFF, ONLINE = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON)

```

![](./media/app-insights-code-sample-export-sql-stream-analytics/34-create-table.png)

<span data-ttu-id="caa75-159">Bu örnekte, sayfa görünümleri verilerden kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="caa75-159">In this sample, we are using data from page views.</span></span> <span data-ttu-id="caa75-160">toosee kullanılabilir diğer veri Merhaba, JSON çıktısını inceleyin ve hello bkz [veri modeli verme](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="caa75-160">toosee hello other data available, inspect your JSON output, and see hello [export data model](app-insights-export-data-model.md).</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="caa75-161">Bir Azure akış analizi örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="caa75-161">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="caa75-162">Merhaba gelen [Klasik Azure portalı](https://manage.windowsazure.com/)hello Azure Stream Analytics hizmeti seçin ve yeni bir Stream Analytics işi oluştur:</span><span class="sxs-lookup"><span data-stu-id="caa75-162">From hello [Classic Azure Portal](https://manage.windowsazure.com/), select hello Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

<span data-ttu-id="caa75-163">Merhaba yeni iş oluşturulduğunda ayrıntılarını genişletin:</span><span class="sxs-lookup"><span data-stu-id="caa75-163">When hello new job is created, expand its details:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a><span data-ttu-id="caa75-164">Blob konum ayarlama</span><span class="sxs-lookup"><span data-stu-id="caa75-164">Set blob location</span></span>
<span data-ttu-id="caa75-165">Sürekli verme blob tootake girişten ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="caa75-165">Set it tootake input from your Continuous Export blob:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

<span data-ttu-id="caa75-166">Şimdi, depolama, daha önce not ettiğiniz hesabınızdan, hello birincil erişim anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="caa75-166">Now you'll need hello Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="caa75-167">Bu depolama hesabı anahtarı hello ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="caa75-167">Set this as hello Storage Account Key.</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a><span data-ttu-id="caa75-168">Set yol önek deseni</span><span class="sxs-lookup"><span data-stu-id="caa75-168">Set path prefix pattern</span></span>
![](./media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

<span data-ttu-id="caa75-169">Emin tooset hello tarih biçimi fazla olması**YYYY-AA-GG** (ile **tire**).</span><span class="sxs-lookup"><span data-stu-id="caa75-169">Be sure tooset hello Date Format too**YYYY-MM-DD** (with **dashes**).</span></span>

<span data-ttu-id="caa75-170">Stream Analytics hello giriş dosyaları hello depoda nasıl bulacağını Hello yol önek deseni belirtir.</span><span class="sxs-lookup"><span data-stu-id="caa75-170">hello Path Prefix Pattern specifies how Stream Analytics finds hello input files in hello storage.</span></span> <span data-ttu-id="caa75-171">Tooset gerekir, toocorrespond toohow sürekli verme hello verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="caa75-171">You need tooset it toocorrespond toohow Continuous Export stores hello data.</span></span> <span data-ttu-id="caa75-172">Aşağıdaki gibi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="caa75-172">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="caa75-173">Bu örnekte:</span><span class="sxs-lookup"><span data-stu-id="caa75-173">In this example:</span></span>

* <span data-ttu-id="caa75-174">`webapplication27`Merhaba Application Insights kaynağı Hello adıdır **tüm alt durumda**.</span><span class="sxs-lookup"><span data-stu-id="caa75-174">`webapplication27` is hello name of hello Application Insights resource, **all in lower case**.</span></span> 
* <span data-ttu-id="caa75-175">`1234...`Merhaba izleme anahtarını hello Application Insights kaynağı olan **kaldırılan çizgilerle**.</span><span class="sxs-lookup"><span data-stu-id="caa75-175">`1234...` is hello instrumentation key of hello Application Insights resource **with dashes removed**.</span></span> 
* <span data-ttu-id="caa75-176">`PageViews`Merhaba türü verilerin tooanalyze istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="caa75-176">`PageViews` is hello type of data we want tooanalyze.</span></span> <span data-ttu-id="caa75-177">Merhaba kullanılabilir türler hello filtresi sürekli dışarı aktarma ile Ayarla bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="caa75-177">hello available types depend on hello filter you set in Continuous Export.</span></span> <span data-ttu-id="caa75-178">Kullanılabilir diğer türleri Hello dışarı aktarılan verileri toosee hello inceleyin ve hello bakın [veri modeli verme](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="caa75-178">Examine hello exported data toosee hello other available types, and see hello [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="caa75-179">`/{date}/{time}`bir desen tam anlamıyla yazılır.</span><span class="sxs-lookup"><span data-stu-id="caa75-179">`/{date}/{time}` is a pattern written literally.</span></span>

<span data-ttu-id="caa75-180">tooget hello adı ve Application Insights kaynağınıza iKey Essentials kendi genel bakış sayfasında açın veya ayarları'nı açın.</span><span class="sxs-lookup"><span data-stu-id="caa75-180">tooget hello name and iKey of your Application Insights resource, open Essentials on its overview page, or open Settings.</span></span>

#### <a name="finish-initial-setup"></a><span data-ttu-id="caa75-181">İlk Kurulumu tamamlayın</span><span class="sxs-lookup"><span data-stu-id="caa75-181">Finish initial setup</span></span>
<span data-ttu-id="caa75-182">Merhaba seri hale getirme biçimi onaylayın:</span><span class="sxs-lookup"><span data-stu-id="caa75-182">Confirm hello serialization format:</span></span>

![Onayla ve sihirbazı kapatın](./media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

<span data-ttu-id="caa75-184">Merhaba sihirbazı kapatın ve hello Kurulum toocomplete için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="caa75-184">Close hello wizard and wait for hello setup toocomplete.</span></span>

> [!TIP]
> <span data-ttu-id="caa75-185">Merhaba Giriş yolu doğru şekilde ayarladığınızdan emin hello örnek işlevi toocheck kullanın.</span><span class="sxs-lookup"><span data-stu-id="caa75-185">Use hello Sample function toocheck that you have set hello input path correctly.</span></span> <span data-ttu-id="caa75-186">Başarısız olursa: olup olmadığını veri seçtiğiniz hello örnek zaman aralığı için hello depolama birimindeki denetleyin.</span><span class="sxs-lookup"><span data-stu-id="caa75-186">If it fails: Check that there is data in hello storage for hello sample time range you chose.</span></span> <span data-ttu-id="caa75-187">Merhaba giriş tanımını düzenlemek ve hello depolama hesabı, yol öneki ve tarih biçimi doğru denetleyin.</span><span class="sxs-lookup"><span data-stu-id="caa75-187">Edit hello input definition and check you set hello storage account, path prefix and date format correctly.</span></span>
> 
> 

## <a name="set-query"></a><span data-ttu-id="caa75-188">Set sorgu</span><span class="sxs-lookup"><span data-stu-id="caa75-188">Set query</span></span>
<span data-ttu-id="caa75-189">Merhaba sorgu bölümünü açın:</span><span class="sxs-lookup"><span data-stu-id="caa75-189">Open hello query section:</span></span>

![Stream analytics sorgu seçin](./media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

<span data-ttu-id="caa75-191">Merhaba varsayılan sorguyla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="caa75-191">Replace hello default query with:</span></span>

```SQL

    SELECT flat.ArrayValue.name as pageName
    , flat.ArrayValue.count as viewCount
    , flat.ArrayValue.url as url
    , flat.ArrayValue.urlData.port as urlDataPort
    , flat.ArrayValue.urlData.protocol as urlDataprotocol
    , flat.ArrayValue.urlData.host as urlDataHost
    , flat.ArrayValue.urlData.base as urlDataBase
    , flat.ArrayValue.urlData.hashTag as urlDataHashTag
      ,A.context.data.eventTime as eventTime
      ,A.context.data.isSynthetic as isSynthetic
      ,A.context.device.id as deviceId
      ,A.context.device.type as deviceType
      ,A.context.device.os as os
      ,A.context.device.osVersion as osVersion
      ,A.context.device.locale as locale
      ,A.context.device.userAgent as userAgent
      ,A.context.device.browser as browser
      ,A.context.device.browserVersion as browserVersion
      ,A.context.device.screenResolution.value as screenResolution
      ,A.context.session.id as sessionId
      ,A.context.session.isFirst as sessionIsFirst
      ,A.context.location.clientip as clientIp
      ,A.context.location.continent as continent
      ,A.context.location.country as country
      ,A.context.location.province as province
      ,A.context.location.city as city
    INTO
      AIOutput
    FROM AIinput A
    CROSS APPLY GetElements(A.[view]) as flat


```

<span data-ttu-id="caa75-192">Belirli toopage görünüm verilerini olduğuna ilk birkaç özellikleri hello edin.</span><span class="sxs-lookup"><span data-stu-id="caa75-192">Notice that hello first few properties are specific toopage view data.</span></span> <span data-ttu-id="caa75-193">Dışarı aktarma diğer telemetri türlerinin farklı özelliklere sahip olur.</span><span class="sxs-lookup"><span data-stu-id="caa75-193">Exports of other telemetry types will have different properties.</span></span> <span data-ttu-id="caa75-194">Merhaba bkz [ayrıntılı hello özellik türleri ve değerleri için veri modeli başvurusu.](app-insights-export-data-model.md)</span><span class="sxs-lookup"><span data-stu-id="caa75-194">See hello [detailed data model reference for hello property types and values.](app-insights-export-data-model.md)</span></span>

## <a name="set-up-output-toodatabase"></a><span data-ttu-id="caa75-195">Çıktı toodatabase ayarlayın</span><span class="sxs-lookup"><span data-stu-id="caa75-195">Set up output toodatabase</span></span>
<span data-ttu-id="caa75-196">SQL hello çıkış olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="caa75-196">Select SQL as hello output.</span></span>

![Çıkış akış analizleri seçin](./media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

<span data-ttu-id="caa75-198">Merhaba SQL veritabanı belirtin.</span><span class="sxs-lookup"><span data-stu-id="caa75-198">Specify hello SQL database.</span></span>

![Veritabanınızın Hello ayrıntıları doldurun](./media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

<span data-ttu-id="caa75-200">Merhaba sihirbazı kapatın ve hello çıkış ayarlanmış bir bildirim bekler.</span><span class="sxs-lookup"><span data-stu-id="caa75-200">Close hello wizard and wait for a notification that hello output has been set up.</span></span>

## <a name="start-processing"></a><span data-ttu-id="caa75-201">İşlemini Başlat</span><span class="sxs-lookup"><span data-stu-id="caa75-201">Start processing</span></span>
<span data-ttu-id="caa75-202">Merhaba iş hello eylem çubuğundan başlatın:</span><span class="sxs-lookup"><span data-stu-id="caa75-202">Start hello job from hello action bar:</span></span>

![Akış analizi Başlat'ı tıklatın.](./media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

<span data-ttu-id="caa75-204">Toostart işleme şimdi veya daha önceki verilerle toostart başlayarak verileri hello olup olmadığını seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="caa75-204">You can choose whether toostart processing hello data starting from now, or toostart with earlier data.</span></span> <span data-ttu-id="caa75-205">Merhaba ikinci verme sürekli bir süredir çalışıyor olsaydı yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="caa75-205">hello latter is useful if you have had Continuous Export already running for a while.</span></span>

![Akış analizi Başlat'ı tıklatın.](./media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

<span data-ttu-id="caa75-207">Birkaç dakika sonra tooSQL sunucu yönetim araçları geri dönün ve içinde veri hello akan izleyin.</span><span class="sxs-lookup"><span data-stu-id="caa75-207">After a few minutes, go back tooSQL Server Management Tools and watch hello data flowing in.</span></span> <span data-ttu-id="caa75-208">Örneğin, şöyle bir sorguyu kullanın:</span><span class="sxs-lookup"><span data-stu-id="caa75-208">For example, use a query like this:</span></span>

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a><span data-ttu-id="caa75-209">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="caa75-209">Related articles</span></span>
* [<span data-ttu-id="caa75-210">Akış analizi kullanarak tooPowerBI dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="caa75-210">Export tooPowerBI using Stream Analytics</span></span>](app-insights-export-power-bi.md)
* [<span data-ttu-id="caa75-211">Ayrıntılı veri başvuru hello özellik türleri ve değerleri için model.</span><span class="sxs-lookup"><span data-stu-id="caa75-211">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="caa75-212">Application ınsights'ta sürekli dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="caa75-212">Continuous Export in Application Insights</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="caa75-213">Application Insights</span><span class="sxs-lookup"><span data-stu-id="caa75-213">Application Insights</span></span>](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

