---
title: "Dışarı aktarmak için SQL Azure Application Insights | Microsoft Docs"
description: "Sürekli olarak Application Insights verileri kullanarak Stream Analytics SQL verin."
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
ms.openlocfilehash: d51e80509ffb63cef0d01133a2295d58757d5b1a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="walkthrough-export-to-sql-from-application-insights-using-stream-analytics"></a><span data-ttu-id="7ce22-103">İzlenecek yol: Uygulama kullanarak Stream Analytics ilişkin bilgiler için SQL dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="7ce22-103">Walkthrough: Export to SQL from Application Insights using Stream Analytics</span></span>
<span data-ttu-id="7ce22-104">Bu makalede, telemetri verilerini taşıma gösterilmektedir [Azure Application Insights] [ start] kullanarak bir Azure SQL veritabanına [sürekli verme] [ export] ve [Azure akış analizi](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="7ce22-104">This article shows how to move your telemetry data from [Azure Application Insights][start] into an Azure SQL database by using [Continuous Export][export] and [Azure Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> 

<span data-ttu-id="7ce22-105">Sürekli verme telemetri verileri JSON biçiminde Azure depolama alanına taşır.</span><span class="sxs-lookup"><span data-stu-id="7ce22-105">Continuous export moves your telemetry data into Azure Storage in JSON format.</span></span> <span data-ttu-id="7ce22-106">Biz Azure akış analizi kullanarak JSON nesneleri ayrıştırabilir ve bir veritabanı tablosundaki satırları oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="7ce22-106">We'll parse the JSON objects using Azure Stream Analytics and create rows in a database table.</span></span>

<span data-ttu-id="7ce22-107">(Daha genellikle sürekli verme kendi uygulamalarınızı Application Insights'a gönderme telemetri analizi yapmak için yoludur.</span><span class="sxs-lookup"><span data-stu-id="7ce22-107">(More generally, Continuous Export is the way to do your own analysis of the telemetry your apps send to Application Insights.</span></span> <span data-ttu-id="7ce22-108">Dışarı aktarılan telemetriyle veri toplama gibi başka işlemler yapmak için bu kod örneği uyarlayabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="7ce22-108">You could adapt this code sample to do other things with the exported telemetry, such as aggregation of data.)</span></span>

<span data-ttu-id="7ce22-109">İzlemek istediğiniz uygulamayı zaten sahip varsayımıyla başlayacağız.</span><span class="sxs-lookup"><span data-stu-id="7ce22-109">We'll start with the assumption that you already have the app you want to monitor.</span></span>

<span data-ttu-id="7ce22-110">Bu örnekte, biz sayfası görünüm verilerini kullanarak, ancak aynı düzeni özel etkinlikler ve özel durumlar gibi diğer veri türleri için kolayca genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="7ce22-110">In this example, we will be using the page view data, but the same pattern can easily be extended to other data types such as custom events and exceptions.</span></span> 

## <a name="add-application-insights-to-your-application"></a><span data-ttu-id="7ce22-111">Uygulamanıza Application Insights ekleyin</span><span class="sxs-lookup"><span data-stu-id="7ce22-111">Add Application Insights to your application</span></span>
<span data-ttu-id="7ce22-112">Başlamak için:</span><span class="sxs-lookup"><span data-stu-id="7ce22-112">To get started:</span></span>

1. <span data-ttu-id="7ce22-113">[Web sayfalarınız için Application Insights'ı ayarlamak](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="7ce22-113">[Set up Application Insights for your web pages](app-insights-javascript.md).</span></span> 
   
    <span data-ttu-id="7ce22-114">(Bu örnekte, istemci tarayıcıları sayfa görünümü verileri işleme biz odaklanmak, ancak Application Insights'ı için sunucu tarafı ayarlayabilir, [Java](app-insights-java-get-started.md) veya [ASP.NET](app-insights-asp-net.md) uygulama ve istek işleme, bağımlılık ve diğer sunucu telemetri.)</span><span class="sxs-lookup"><span data-stu-id="7ce22-114">(In this example, we'll focus on processing page view data from the client browsers, but you could also set up Application Insights for the server side of your [Java](app-insights-java-get-started.md) or [ASP.NET](app-insights-asp-net.md) app and process request, dependency and other server telemetry.)</span></span>
2. <span data-ttu-id="7ce22-115">Uygulamanızı yayımlayın ve telemetri verilerini Application Insights kaynağınıza görünmesini izleyin.</span><span class="sxs-lookup"><span data-stu-id="7ce22-115">Publish your app, and watch telemetry data appearing in your Application Insights resource.</span></span>

## <a name="create-storage-in-azure"></a><span data-ttu-id="7ce22-116">Depolama oluşturma</span><span class="sxs-lookup"><span data-stu-id="7ce22-116">Create storage in Azure</span></span>
<span data-ttu-id="7ce22-117">Depolama oluşturmanız gerekir böylece sürekli verme verileri Azure depolama hesabı her zaman çıkarır.</span><span class="sxs-lookup"><span data-stu-id="7ce22-117">Continuous export always outputs data to an Azure Storage account, so you need to create the storage first.</span></span>

1. <span data-ttu-id="7ce22-118">Aboneliğinizde depolama hesabı oluşturma [Azure portal][portal].</span><span class="sxs-lookup"><span data-stu-id="7ce22-118">Create a storage account in your subscription in the [Azure portal][portal].</span></span>
   
    ![Azure portalında yeni, verileri depolama birimi seçin.](./media/app-insights-code-sample-export-sql-stream-analytics/040-store.png)
2. <span data-ttu-id="7ce22-122">Bir kapsayıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7ce22-122">Create a container</span></span>
   
    ![Yeni depolama kapsayıcıları seçin, kapsayıcıları döşeme tıklatın ve ardından Ekle](./media/app-insights-code-sample-export-sql-stream-analytics/050-container.png)
3. <span data-ttu-id="7ce22-124">Depolama erişim tuşu kopyalama</span><span class="sxs-lookup"><span data-stu-id="7ce22-124">Copy the storage access key</span></span>
   
    <span data-ttu-id="7ce22-125">Akış analizi hizmetine giriş yakında ayarlamak için gerekir.</span><span class="sxs-lookup"><span data-stu-id="7ce22-125">You'll need it soon to set up the input to the stream analytics service.</span></span>
   
    ![Depolama ayarlarını, anahtarları, açın ve birincil erişim tuşunu bir kopyasını alın](./media/app-insights-code-sample-export-sql-stream-analytics/21-storage-key.png)

## <a name="start-continuous-export-to-azure-storage"></a><span data-ttu-id="7ce22-127">Azure depolama alanına sürekli verme Başlat</span><span class="sxs-lookup"><span data-stu-id="7ce22-127">Start continuous export to Azure storage</span></span>
1. <span data-ttu-id="7ce22-128">Azure portalında, uygulamanız için oluşturduğunuz Application Insights kaynağı göz atın.</span><span class="sxs-lookup"><span data-stu-id="7ce22-128">In the Azure portal, browse to the Application Insights resource you created for your application.</span></span>
   
    ![Gözat, Application Insights, uygulamanızı seçin](./media/app-insights-code-sample-export-sql-stream-analytics/060-browse.png)
2. <span data-ttu-id="7ce22-130">Sürekli verme oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7ce22-130">Create a continuous export.</span></span>
   
    ![Ayarları, sürekli verme ekleme seçin](./media/app-insights-code-sample-export-sql-stream-analytics/070-export.png)

    <span data-ttu-id="7ce22-132">Daha önce oluşturduğunuz depolama hesabı seçin:</span><span class="sxs-lookup"><span data-stu-id="7ce22-132">Select the storage account you created earlier:</span></span>

    ![Dışa aktarma hedefi ayarlama](./media/app-insights-code-sample-export-sql-stream-analytics/080-add.png)

    <span data-ttu-id="7ce22-134">Görmek istediğiniz olay türlerini ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="7ce22-134">Set the event types you want to see:</span></span>

    ![Olay türlerini seçin](./media/app-insights-code-sample-export-sql-stream-analytics/085-types.png)


1. <span data-ttu-id="7ce22-136">Accumulate bazı veriler sağlar.</span><span class="sxs-lookup"><span data-stu-id="7ce22-136">Let some data accumulate.</span></span> <span data-ttu-id="7ce22-137">Arkanıza yaslanın ve kişilere uygulamanızın biraz kullanın.</span><span class="sxs-lookup"><span data-stu-id="7ce22-137">Sit back and let people use your application for a while.</span></span> <span data-ttu-id="7ce22-138">Telemetri geldikçe ve istatistiksel grafiklerde görürsünüz [ölçüm Gezgini](app-insights-metrics-explorer.md) ve olayları tek tek [tanılama arama](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="7ce22-138">Telemetry will come in and you'll see statistical charts in [metric explorer](app-insights-metrics-explorer.md) and individual events in [diagnostic search](app-insights-diagnostic-search.md).</span></span> 
   
    <span data-ttu-id="7ce22-139">Ve ayrıca, verileri depolama alanınızın dışa aktarır.</span><span class="sxs-lookup"><span data-stu-id="7ce22-139">And also, the data will export to your storage.</span></span> 
2. <span data-ttu-id="7ce22-140">Dışarı aktarılan verileri, ya da portal - Seç **Gözat**, depolama hesabınızı seçin ve ardından **kapsayıcıları** - ya da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7ce22-140">Inspect the exported data, either in the portal - choose **Browse**, select your storage account, and then **Containers** - or in Visual Studio.</span></span> <span data-ttu-id="7ce22-141">Visual Studio'da, **görüntülemek / Cloud Explorer**ve Azure açın / depolama.</span><span class="sxs-lookup"><span data-stu-id="7ce22-141">In Visual Studio, choose **View / Cloud Explorer**, and open Azure / Storage.</span></span> <span data-ttu-id="7ce22-142">(Bu menü seçeneği yoksa, Azure SDK'yı yüklemeniz gerekir: Yeni Proje iletişim kutusunu açın ve Visual C# açın / bulut / .NET için Microsoft Azure SDK'sını alın.)</span><span class="sxs-lookup"><span data-stu-id="7ce22-142">(If you don't have this menu option, you need to install the Azure SDK: Open the New Project dialog and open Visual C# / Cloud / Get Microsoft Azure SDK for .NET.)</span></span>
   
    ![Visual Studio'da açın Server Browser, Azure, depolama](./media/app-insights-code-sample-export-sql-stream-analytics/087-explorer.png)
   
    <span data-ttu-id="7ce22-144">Uygulama adı ve araçları anahtarından türetilen yol adı, ortak parçası not edin.</span><span class="sxs-lookup"><span data-stu-id="7ce22-144">Make a note of the common part of the path name, which is derived from the application name and instrumentation key.</span></span> 

<span data-ttu-id="7ce22-145">JSON biçiminde dosyaları blob yazılır.</span><span class="sxs-lookup"><span data-stu-id="7ce22-145">The events are written to blob files in JSON format.</span></span> <span data-ttu-id="7ce22-146">Her dosya bir veya daha fazla olaylar içerebilir.</span><span class="sxs-lookup"><span data-stu-id="7ce22-146">Each file may contain one or more events.</span></span> <span data-ttu-id="7ce22-147">Bu nedenle olay verileri okumak ve istiyoruz alanları filtrelemek isteriz.</span><span class="sxs-lookup"><span data-stu-id="7ce22-147">So we'd like to read the event data and filter out the fields we want.</span></span> <span data-ttu-id="7ce22-148">Her türlü verilerle yapabileceğimiz bir şey vardır, ancak bizim planı bugün Stream Analytics verileri bir SQL veritabanını taşımak için kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="7ce22-148">There are all kinds of things we could do with the data, but our plan today is to use Stream Analytics to move the data to a SQL database.</span></span> <span data-ttu-id="7ce22-149">Bu, çok sayıda ilginç sorguları çalıştırmak kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="7ce22-149">That will make it easy to run lots of interesting queries.</span></span>

## <a name="create-an-azure-sql-database"></a><span data-ttu-id="7ce22-150">Bir Azure SQL veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7ce22-150">Create an Azure SQL Database</span></span>
<span data-ttu-id="7ce22-151">Bir kez daha, aboneliğinizde başlayarak [Azure portal][portal], veritabanı oluşturma (ve yeni bir sunucu zaten bir olduğuna sürece) verileri yazacak şekilde.</span><span class="sxs-lookup"><span data-stu-id="7ce22-151">Once again starting from your subscription in [Azure portal][portal], create the database (and a new server, unless you've already got one) to which you'll write the data.</span></span>

![Yeni, verileri, SQL](./media/app-insights-code-sample-export-sql-stream-analytics/090-sql.png)

<span data-ttu-id="7ce22-153">Veritabanı sunucusu Azure hizmetlerine erişime izin verdiğinden emin olun:</span><span class="sxs-lookup"><span data-stu-id="7ce22-153">Make sure that the database server allows access to Azure services:</span></span>

![Gözat, sunucuları, sunucunuz, ayarları, güvenlik duvarı, Azure erişime izin ver](./media/app-insights-code-sample-export-sql-stream-analytics/100-sqlaccess.png)

## <a name="create-a-table-in-azure-sql-db"></a><span data-ttu-id="7ce22-155">Azure SQL DB tablosu oluşturma</span><span class="sxs-lookup"><span data-stu-id="7ce22-155">Create a table in Azure SQL DB</span></span>
<span data-ttu-id="7ce22-156">Tercih edilen Yönetim aracınızla önceki bölümde oluşturulan veritabanına bağlanın.</span><span class="sxs-lookup"><span data-stu-id="7ce22-156">Connect to the database created in the previous section with your preferred management tool.</span></span> <span data-ttu-id="7ce22-157">Bu kılavuzda, biz kullanacağınız [SQL Server Yönetim Araçları](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="7ce22-157">In this walkthrough, we will be using [SQL Server Management Tools](https://msdn.microsoft.com/ms174173.aspx) (SSMS).</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/31-sql-table.png)

<span data-ttu-id="7ce22-158">Yeni bir sorgu oluşturun ve aşağıdaki T-SQL Yürüt:</span><span class="sxs-lookup"><span data-stu-id="7ce22-158">Create a new query, and execute the following T-SQL:</span></span>

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

<span data-ttu-id="7ce22-159">Bu örnekte, sayfa görünümleri verilerden kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="7ce22-159">In this sample, we are using data from page views.</span></span> <span data-ttu-id="7ce22-160">Kullanılabilir diğer verileri görmek için JSON çıktısını inceleyin ve bakın [veri modeli verme](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="7ce22-160">To see the other data available, inspect your JSON output, and see the [export data model](app-insights-export-data-model.md).</span></span>

## <a name="create-an-azure-stream-analytics-instance"></a><span data-ttu-id="7ce22-161">Bir Azure akış analizi örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="7ce22-161">Create an Azure Stream Analytics instance</span></span>
<span data-ttu-id="7ce22-162">Gelen [Klasik Azure portalı](https://manage.windowsazure.com/), Azure Stream Analytics hizmeti seçin ve yeni bir Stream Analytics işi oluştur:</span><span class="sxs-lookup"><span data-stu-id="7ce22-162">From the [Classic Azure Portal](https://manage.windowsazure.com/), select the Azure Stream Analytics service, and create a new Stream Analytics job:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/37-create-stream-analytics.png)

![](./media/app-insights-code-sample-export-sql-stream-analytics/38-create-stream-analytics-form.png)

<span data-ttu-id="7ce22-163">Yeni iş oluşturulduğunda ayrıntılarını genişletin:</span><span class="sxs-lookup"><span data-stu-id="7ce22-163">When the new job is created, expand its details:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/41-sa-job.png)

#### <a name="set-blob-location"></a><span data-ttu-id="7ce22-164">Blob konum ayarlama</span><span class="sxs-lookup"><span data-stu-id="7ce22-164">Set blob location</span></span>
<span data-ttu-id="7ce22-165">Sürekli verme blobundan giriş gerçekleştirecek şekilde ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="7ce22-165">Set it to take input from your Continuous Export blob:</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/42-sa-wizard1.png)

<span data-ttu-id="7ce22-166">Şimdi, depolama, daha önce not ettiğiniz hesabınızdan, birincil erişim anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="7ce22-166">Now you'll need the Primary Access Key from your Storage Account, which you noted earlier.</span></span> <span data-ttu-id="7ce22-167">Bu depolama hesabı anahtarı ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7ce22-167">Set this as the Storage Account Key.</span></span>

![](./media/app-insights-code-sample-export-sql-stream-analytics/46-sa-wizard2.png)

#### <a name="set-path-prefix-pattern"></a><span data-ttu-id="7ce22-168">Set yol önek deseni</span><span class="sxs-lookup"><span data-stu-id="7ce22-168">Set path prefix pattern</span></span>
![](./media/app-insights-code-sample-export-sql-stream-analytics/47-sa-wizard3.png)

<span data-ttu-id="7ce22-169">Tarih biçimi ayarladığınızdan emin olun **YYYY-AA-GG** (ile **tire**).</span><span class="sxs-lookup"><span data-stu-id="7ce22-169">Be sure to set the Date Format to **YYYY-MM-DD** (with **dashes**).</span></span>

<span data-ttu-id="7ce22-170">Önek yol deseni Stream Analytics girdi dosyaları depolama alanına nasıl bulacağını belirler.</span><span class="sxs-lookup"><span data-stu-id="7ce22-170">The Path Prefix Pattern specifies how Stream Analytics finds the input files in the storage.</span></span> <span data-ttu-id="7ce22-171">Bunu sürekli verme verileri nasıl depolar karşılık gelecek şekilde ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7ce22-171">You need to set it to correspond to how Continuous Export stores the data.</span></span> <span data-ttu-id="7ce22-172">Aşağıdaki gibi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="7ce22-172">Set it like this:</span></span>

    webapplication27_12345678123412341234123456789abcdef0/PageViews/{date}/{time}

<span data-ttu-id="7ce22-173">Bu örnekte:</span><span class="sxs-lookup"><span data-stu-id="7ce22-173">In this example:</span></span>

* <span data-ttu-id="7ce22-174">`webapplication27`Application Insights kaynağı adı **tüm alt durumda**.</span><span class="sxs-lookup"><span data-stu-id="7ce22-174">`webapplication27` is the name of the Application Insights resource, **all in lower case**.</span></span> 
* <span data-ttu-id="7ce22-175">`1234...`Application Insights kaynağı izleme anahtarını olan **kaldırılan çizgilerle**.</span><span class="sxs-lookup"><span data-stu-id="7ce22-175">`1234...` is the instrumentation key of the Application Insights resource **with dashes removed**.</span></span> 
* <span data-ttu-id="7ce22-176">`PageViews`Analiz etmek istiyoruz veri türüdür.</span><span class="sxs-lookup"><span data-stu-id="7ce22-176">`PageViews` is the type of data we want to analyze.</span></span> <span data-ttu-id="7ce22-177">Kullanılabilir türler filtresi sürekli dışarı aktarma ile Ayarla bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="7ce22-177">The available types depend on the filter you set in Continuous Export.</span></span> <span data-ttu-id="7ce22-178">Diğer kullanılabilir türleri görmek ve görmek için dışarı aktarılan verileri incelemek [veri modeli verme](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="7ce22-178">Examine the exported data to see the other available types, and see the [export data model](app-insights-export-data-model.md).</span></span>
* <span data-ttu-id="7ce22-179">`/{date}/{time}`bir desen tam anlamıyla yazılır.</span><span class="sxs-lookup"><span data-stu-id="7ce22-179">`/{date}/{time}` is a pattern written literally.</span></span>

<span data-ttu-id="7ce22-180">Application Insights kaynağınıza iKey ve adını almak için genel bakış sayfasında Essentials açın veya ayarları'nı açın.</span><span class="sxs-lookup"><span data-stu-id="7ce22-180">To get the name and iKey of your Application Insights resource, open Essentials on its overview page, or open Settings.</span></span>

#### <a name="finish-initial-setup"></a><span data-ttu-id="7ce22-181">İlk Kurulumu tamamlayın</span><span class="sxs-lookup"><span data-stu-id="7ce22-181">Finish initial setup</span></span>
<span data-ttu-id="7ce22-182">Seri hale getirme biçimi onaylayın:</span><span class="sxs-lookup"><span data-stu-id="7ce22-182">Confirm the serialization format:</span></span>

![Onayla ve sihirbazı kapatın](./media/app-insights-code-sample-export-sql-stream-analytics/48-sa-wizard4.png)

<span data-ttu-id="7ce22-184">Sihirbazı kapatmak ve kurulumun tamamlanması için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="7ce22-184">Close the wizard and wait for the setup to complete.</span></span>

> [!TIP]
> <span data-ttu-id="7ce22-185">Giriş yolu doğru şekilde ayarladığınızdan emin denetlemek için örnek işlevini kullanın.</span><span class="sxs-lookup"><span data-stu-id="7ce22-185">Use the Sample function to check that you have set the input path correctly.</span></span> <span data-ttu-id="7ce22-186">Başarısız olursa: olup olmadığını veri depolama alanı için seçtiğiniz örnek zaman aralığı içinde denetleyin.</span><span class="sxs-lookup"><span data-stu-id="7ce22-186">If it fails: Check that there is data in the storage for the sample time range you chose.</span></span> <span data-ttu-id="7ce22-187">Giriş tanımı düzenleyin ve ayarlayın depolama hesabı, yol öneki ve tarih biçimi doğru denetleyin.</span><span class="sxs-lookup"><span data-stu-id="7ce22-187">Edit the input definition and check you set the storage account, path prefix and date format correctly.</span></span>
> 
> 

## <a name="set-query"></a><span data-ttu-id="7ce22-188">Set sorgu</span><span class="sxs-lookup"><span data-stu-id="7ce22-188">Set query</span></span>
<span data-ttu-id="7ce22-189">Sorgu bölümünü açın:</span><span class="sxs-lookup"><span data-stu-id="7ce22-189">Open the query section:</span></span>

![Stream analytics sorgu seçin](./media/app-insights-code-sample-export-sql-stream-analytics/51-query.png)

<span data-ttu-id="7ce22-191">Varsayılan sorguyla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="7ce22-191">Replace the default query with:</span></span>

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

<span data-ttu-id="7ce22-192">İlk birkaç Özellikleri Sayfası görünüm verilerini belirli olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="7ce22-192">Notice that the first few properties are specific to page view data.</span></span> <span data-ttu-id="7ce22-193">Dışarı aktarma diğer telemetri türlerinin farklı özelliklere sahip olur.</span><span class="sxs-lookup"><span data-stu-id="7ce22-193">Exports of other telemetry types will have different properties.</span></span> <span data-ttu-id="7ce22-194">Bkz: [ayrıntılı özellik türleri ve değerleri için veri modeli başvurusu.](app-insights-export-data-model.md)</span><span class="sxs-lookup"><span data-stu-id="7ce22-194">See the [detailed data model reference for the property types and values.](app-insights-export-data-model.md)</span></span>

## <a name="set-up-output-to-database"></a><span data-ttu-id="7ce22-195">Veritabanı için çıktı ayarlama</span><span class="sxs-lookup"><span data-stu-id="7ce22-195">Set up output to database</span></span>
<span data-ttu-id="7ce22-196">SQL çıktısı olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="7ce22-196">Select SQL as the output.</span></span>

![Çıkış akış analizleri seçin](./media/app-insights-code-sample-export-sql-stream-analytics/53-store.png)

<span data-ttu-id="7ce22-198">SQL veritabanı belirtin.</span><span class="sxs-lookup"><span data-stu-id="7ce22-198">Specify the SQL database.</span></span>

![Veritabanınızın ayrıntıları doldurun](./media/app-insights-code-sample-export-sql-stream-analytics/55-output.png)

<span data-ttu-id="7ce22-200">Sihirbazı kapatmak ve çıktı ayarlanmış bir bildirim bekler.</span><span class="sxs-lookup"><span data-stu-id="7ce22-200">Close the wizard and wait for a notification that the output has been set up.</span></span>

## <a name="start-processing"></a><span data-ttu-id="7ce22-201">İşlemini Başlat</span><span class="sxs-lookup"><span data-stu-id="7ce22-201">Start processing</span></span>
<span data-ttu-id="7ce22-202">İş eylemi çubuğundan başlatın:</span><span class="sxs-lookup"><span data-stu-id="7ce22-202">Start the job from the action bar:</span></span>

![Akış analizi Başlat'ı tıklatın.](./media/app-insights-code-sample-export-sql-stream-analytics/61-start.png)

<span data-ttu-id="7ce22-204">Şimdi veya başlamak eski veri başlatmayı veri işlemeye başlaması seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7ce22-204">You can choose whether to start processing the data starting from now, or to start with earlier data.</span></span> <span data-ttu-id="7ce22-205">İkincisi verme sürekli bir süredir çalışıyor olsaydı yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="7ce22-205">The latter is useful if you have had Continuous Export already running for a while.</span></span>

![Akış analizi Başlat'ı tıklatın.](./media/app-insights-code-sample-export-sql-stream-analytics/63-start.png)

<span data-ttu-id="7ce22-207">Birkaç dakika sonra SQL Server Yönetim Araçları için geri dönün ve içinde akan verilere izleyin.</span><span class="sxs-lookup"><span data-stu-id="7ce22-207">After a few minutes, go back to SQL Server Management Tools and watch the data flowing in.</span></span> <span data-ttu-id="7ce22-208">Örneğin, şöyle bir sorguyu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7ce22-208">For example, use a query like this:</span></span>

    SELECT TOP 100 *
    FROM [dbo].[PageViewsTable]


## <a name="related-articles"></a><span data-ttu-id="7ce22-209">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="7ce22-209">Related articles</span></span>
* [<span data-ttu-id="7ce22-210">Akış analizi kullanarak Powerbı dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="7ce22-210">Export to PowerBI using Stream Analytics</span></span>](app-insights-export-power-bi.md)
* [<span data-ttu-id="7ce22-211">Ayrıntılı veri özellik türleri ve değerleri için başvuru modeli.</span><span class="sxs-lookup"><span data-stu-id="7ce22-211">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)
* [<span data-ttu-id="7ce22-212">Application ınsights'ta sürekli dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="7ce22-212">Continuous Export in Application Insights</span></span>](app-insights-export-telemetry.md)
* [<span data-ttu-id="7ce22-213">Application Insights</span><span class="sxs-lookup"><span data-stu-id="7ce22-213">Application Insights</span></span>](https://azure.microsoft.com/services/application-insights/)

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[export]: app-insights-export-telemetry.md
[metrics]: app-insights-metrics-explorer.md
[portal]: http://portal.azure.com/
[start]: app-insights-overview.md

