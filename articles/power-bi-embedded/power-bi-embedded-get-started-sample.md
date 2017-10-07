---
title: "bir örnek kullanmaya aaaGet"
description: "Power BI Embedded, iş zekası uygulamanıza etkileşimli Power BI raporları SDK tooadd kullanın"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: d8a9ef78-ad4e-4bc7-9711-89172dc5c548
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/02/2017
ms.author: asaxton
ms.openlocfilehash: 1fef9dd8e0f734b748b930d3f85ad4b517d9661e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-power-bi-embedded-sample"></a><span data-ttu-id="d1532-103">Power BI Embedded örneği kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="d1532-103">Get started with Power BI Embedded sample</span></span>

<span data-ttu-id="d1532-104">İle **Microsoft Power BI Embedded**, Power BI raporları sağ web veya mobil uygulamaları tümleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1532-104">With **Microsoft Power BI Embedded**, you can integrate Power BI reports right into your web or mobile applications.</span></span> <span data-ttu-id="d1532-105">Bu makalede, sizi, toohello tanıtmak **Power BI Embedded** get başlatılan örnek.</span><span class="sxs-lookup"><span data-stu-id="d1532-105">In this article, we'll introduce you toohello **Power BI Embedded** get started sample.</span></span>

<span data-ttu-id="d1532-106">Biz daha ilerlemeden önce kaynakları aşağıdaki toosave hello büyük olasılıkla isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d1532-106">Before we go any further, you'll probably want toosave hello following resources.</span></span> <span data-ttu-id="d1532-107">Bunlar Power BI raporları hello örnek uygulaması ve kendi uygulamalarınızı halinde çok tümleştirdiğinizde yardımcı olacağız.</span><span class="sxs-lookup"><span data-stu-id="d1532-107">They'll help you when integrating Power BI reports into hello sample app and your own apps too.</span></span>

* [<span data-ttu-id="d1532-108">Örnek çalışma web uygulaması</span><span class="sxs-lookup"><span data-stu-id="d1532-108">Sample workspace web app</span></span>](http://go.microsoft.com/fwlink/?LinkId=761493)
* [<span data-ttu-id="d1532-109">Power BI Embedded API Başvurusu</span><span class="sxs-lookup"><span data-stu-id="d1532-109">Power BI Embedded API reference</span></span>](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* <span data-ttu-id="d1532-110">[Power BI Embedded .NET SDK'sı ](http://go.microsoft.com/fwlink/?LinkId=746472) (NuGet aracılığıyla kullanılabilir)</span><span class="sxs-lookup"><span data-stu-id="d1532-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (available via NuGet)</span></span>
* [<span data-ttu-id="d1532-111">JavaScript rapor örnek ekleme</span><span class="sxs-lookup"><span data-stu-id="d1532-111">JavaScript Report Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> <span data-ttu-id="d1532-112">Yapılandırabilirsiniz ve Power BI Embedded alma çalışma hello başlatılan örnek önce toocreate en az bir gereksinim **çalışma alanı koleksiyonu** Azure aboneliğinizde.</span><span class="sxs-lookup"><span data-stu-id="d1532-112">Before you can configure and run hello Power BI Embedded get started sample, you need toocreate at least one **Workspace Collection** in your Azure subscription.</span></span> <span data-ttu-id="d1532-113">toolearn nasıl toocreate bir **çalışma alanı koleksiyonu** hello Azure Portal bkz [Power BI Embedded ile çalışmaya başlama](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d1532-113">toolearn how toocreate a **Workspace Collection** in hello Azure Portal see [Getting Started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="configure-hello-sample-app"></a><span data-ttu-id="d1532-114">Merhaba örnek uygulamayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d1532-114">Configure hello sample app</span></span>

<span data-ttu-id="d1532-115">Şimdi Visual Studio geliştirme ortamında tooaccess hello bileşenleri gerekli toorun hello örnek uygulamanızı ayarlama aracılığıyla yol.</span><span class="sxs-lookup"><span data-stu-id="d1532-115">Let's walk through setting up your Visual Studio development environment tooaccess hello  components needed toorun hello sample app.</span></span>

1. <span data-ttu-id="d1532-116">İndirip hello sıkıştırmasını [Power BI Embedded - bir web uygulamasına bir rapor tümleştirme](http://go.microsoft.com/fwlink/?LinkId=761493) github'da örnek.</span><span class="sxs-lookup"><span data-stu-id="d1532-116">Download and unzip hello [Power BI Embedded - Integrate a report into a web app](http://go.microsoft.com/fwlink/?LinkId=761493) sample on GitHub.</span></span>
2. <span data-ttu-id="d1532-117">Açık **Powerbı embedded.sln** Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d1532-117">Open **PowerBI-embedded.sln** in Visual Studio.</span></span> <span data-ttu-id="d1532-118">Tooexecute hello gerekebilir **güncelleştirme paketini** hello NuGET Paket Yöneticisi konsolunda bu çözümde kullanılan sipariş tooupdate hello paketlerde komutu.</span><span class="sxs-lookup"><span data-stu-id="d1532-118">You may need tooexecute hello **Update-Package** command in hello NuGET Package Manager Console in order tooupdate hello packages used in this solution.</span></span>
3. <span data-ttu-id="d1532-119">Merhaba çözümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d1532-119">Build hello solution.</span></span>
4. <span data-ttu-id="d1532-120">Merhaba çalıştırmak **ProvisionSample** konsol uygulaması.</span><span class="sxs-lookup"><span data-stu-id="d1532-120">Run hello **ProvisionSample** console app.</span></span> <span data-ttu-id="d1532-121">Merhaba örnek konsol uygulamasındaki bir çalışma alanı sağlamak ve PBIX dosyasını içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="d1532-121">In hello sample console app, you provision a workspace and import a PBIX file.</span></span>
5. <span data-ttu-id="d1532-122">Yeni bir tooprovision **çalışma**, 1 seçeneğini belirleyin **koleksiyonu Yönetimi**ve ardından seçeneğini 6, **yeni bir çalışma alanı sağlanamadı**</span><span class="sxs-lookup"><span data-stu-id="d1532-122">tooprovision a new **Workspace**, select option 1, **Collection management**, and then select option 6, **Provision a new Workspace**</span></span>
6. <span data-ttu-id="d1532-123">Yeni bir tooimport **rapor**, 2, seçeneğini belirleyin **rapor Yönetim**ve seçenek 3, ardından **alma PBIX Masaüstü dosya bir çalışma alanına**.</span><span class="sxs-lookup"><span data-stu-id="d1532-123">tooimport a new **Report**, select option 2, **Report management**, and then select option 3, **Import PBIX Desktop file into a workspace**.</span></span>

7. <span data-ttu-id="d1532-124">Girin, **çalışma alanı koleksiyonu** adı ve **erişim tuşu**.</span><span class="sxs-lookup"><span data-stu-id="d1532-124">Enter your **Workspace Collection** name, and **Access Key**.</span></span> <span data-ttu-id="d1532-125">Bu hello alabilirsiniz **Azure Portal**.</span><span class="sxs-lookup"><span data-stu-id="d1532-125">You can get these in hello **Azure Portal**.</span></span> <span data-ttu-id="d1532-126">toolearn nasıl hakkında daha fazla tooget, **erişim tuşu**, bkz: [görünümü Power BI API'si erişim anahtarlarını](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) içinde Microsoft Power BI Embedded ile çalışmaya başlama.</span><span class="sxs-lookup"><span data-stu-id="d1532-126">toolearn more about how tooget your **Access Key**, see [View Power BI API Access Keys](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) in Get started with Microsoft Power BI Embedded.</span></span>

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. <span data-ttu-id="d1532-127">Kopyala ve yeni oluşturulan hello kaydedin **çalışma alanı kimliği** bu makalenin sonraki bölümlerinde toouse.</span><span class="sxs-lookup"><span data-stu-id="d1532-127">Copy and save hello newly created **Workspace ID** toouse later in this article.</span></span> <span data-ttu-id="d1532-128">Merhaba sonra **çalışma alanı kimliği** olan oluşturulan, bunu hello bulabilirsiniz **Azure Portal**.</span><span class="sxs-lookup"><span data-stu-id="d1532-128">After hello **Workspace ID** is created, you can find it hello **Azure Portal**.</span></span>

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. <span data-ttu-id="d1532-129">tooimport bir PBIX dosyası içine, **çalışma**, seçeneğini belirleyin **6. İçeri aktarma PBIX Masaüstü dosyası var olan bir çalışma alanına**.</span><span class="sxs-lookup"><span data-stu-id="d1532-129">tooimport a PBIX file into your **Workspace**, select option **6. Import PBIX Desktop file into an existing workspace**.</span></span> <span data-ttu-id="d1532-130">Kullanışlı dosya PBIX yoksa, hello indirebilirsiniz [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span><span class="sxs-lookup"><span data-stu-id="d1532-130">If you don't have a PBIX file handy, you can download hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>
10. <span data-ttu-id="d1532-131">İstenirse, için kolay bir ad girin, **Dataset**.</span><span class="sxs-lookup"><span data-stu-id="d1532-131">If prompted, enter a friendly name for your **Dataset**.</span></span>

<span data-ttu-id="d1532-132">Benzer bir yanıt görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="d1532-132">You should see a response like:</span></span>

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> <span data-ttu-id="d1532-133">PBIX dosyanızın tüm doğrudan sorgu bağlantıları içeriyorsa, seçeneği 7 tooupdate hello bağlantı dizeleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d1532-133">If your PBIX file contains any direct query connections, run option 7 tooupdate hello connection strings.</span></span>

<span data-ttu-id="d1532-134">Bu noktada, içeri aktarılan bir Power BI PBIX rapor vardır, **çalışma**.</span><span class="sxs-lookup"><span data-stu-id="d1532-134">At this point, you have a Power BI PBIX report imported into your **Workspace**.</span></span> <span data-ttu-id="d1532-135">Şimdi ne bakalım toorun hello **Power BI Embedded** başlatılan örnek web uygulamasını edinin.</span><span class="sxs-lookup"><span data-stu-id="d1532-135">Now, let's look at how toorun hello **Power BI Embedded** get started sample web app.</span></span>

## <a name="run-hello-sample-web-app"></a><span data-ttu-id="d1532-136">Merhaba örnek web uygulaması çalıştırın</span><span class="sxs-lookup"><span data-stu-id="d1532-136">Run hello sample web app</span></span>
<span data-ttu-id="d1532-137">Merhaba web uygulaması örneği içeri aktarılan raporlar işleyen örnek bir uygulama olduğundan, **çalışma**.</span><span class="sxs-lookup"><span data-stu-id="d1532-137">hello web app sample is a sample application that renders reports imported into your **Workspace**.</span></span> <span data-ttu-id="d1532-138">Nasıl tooconfigure hello web uygulaması örneği aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d1532-138">Here's how tooconfigure hello web app sample.</span></span>

1. <span data-ttu-id="d1532-139">Merhaba, **Powerbı katıştırılmış** Visual Studio çözümü, sağ tıklatın hello **EmbedSample** web uygulaması ve seçin **başlangıç projesi olarak ayarla**.</span><span class="sxs-lookup"><span data-stu-id="d1532-139">In hello **PowerBI-embedded** Visual Studio solution, right click hello **EmbedSample** web application, and choose **Set as StartUp project**.</span></span>
2. <span data-ttu-id="d1532-140">İçinde **web.config**, hello içinde **EmbedSample** web uygulaması, hello Düzenle **appSettings**: **AccessKey**,  **WorkspaceCollection** adı ve **Workspaceıd**.</span><span class="sxs-lookup"><span data-stu-id="d1532-140">In **web.config**, in hello **EmbedSample** web application, edit hello **appSettings**: **AccessKey**, **WorkspaceCollection** name, and **WorkspaceId**.</span></span>

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. <span data-ttu-id="d1532-141">Merhaba çalıştırmak **EmbedSample** web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="d1532-141">Run hello **EmbedSample** web application.</span></span>

<span data-ttu-id="d1532-142">Merhaba çalıştırdıktan sonra **EmbedSample** web uygulaması hello sol gezinti bölmesini içermelidir bir **raporları** menüsü.</span><span class="sxs-lookup"><span data-stu-id="d1532-142">Once you run hello **EmbedSample** web application, hello left navigation panel should contain a **Reports** menu.</span></span> <span data-ttu-id="d1532-143">içeri aktardığınız, tooview hello rapor genişletin **raporları**ve bir rapora tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d1532-143">tooview hello report you imported, expand **Reports**, and click a report.</span></span> <span data-ttu-id="d1532-144">Merhaba aldıysanız [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), hello örnek web uygulaması şuna benzeyebilir:</span><span class="sxs-lookup"><span data-stu-id="d1532-144">If you imported hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), hello sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

<span data-ttu-id="d1532-145">Bir raporu tıklattıktan sonra hello **EmbedSample** web uygulaması görünmelidir bir şey:</span><span class="sxs-lookup"><span data-stu-id="d1532-145">After you click a report, hello **EmbedSample** web application should look something this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-hello-sample-code"></a><span data-ttu-id="d1532-146">Merhaba örnek kod keşfetme</span><span class="sxs-lookup"><span data-stu-id="d1532-146">Explore hello sample code</span></span>

<span data-ttu-id="d1532-147">Merhaba **Microsoft Power BI Embedded** örnektir nasıl gösteren örnek bir web uygulaması toointegrate **Power BI** uygulamanıza raporlar.</span><span class="sxs-lookup"><span data-stu-id="d1532-147">hello **Microsoft Power BI Embedded** sample is an example web app that shows you how toointegrate **Power BI** reports into your app.</span></span> <span data-ttu-id="d1532-148">Bir Model-View-Controller (MVC) kullanan tasarım deseni toodemonstrate en iyi yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="d1532-148">It uses a Model-View-Controller (MVC) design pattern toodemonstrate best practices.</span></span> <span data-ttu-id="d1532-149">Bu bölüm içinde hello keşfedebilirsiniz hello örnek kod parçalarını vurgular **Powerbı katıştırılmış** web uygulaması çözümü.</span><span class="sxs-lookup"><span data-stu-id="d1532-149">This section highlights parts of hello sample code that you can explore within hello **PowerBI-embedded** web app solution.</span></span> <span data-ttu-id="d1532-150">Merhaba Model-View-Controller (MVC) deseni ayıran hello modelleme hello etki alanı, hello sunu ve üç ayrı sınıfları kullanıcı girişine bağlı hello eylemleri: Model, Görünüm ve denetim.</span><span class="sxs-lookup"><span data-stu-id="d1532-150">hello Model-View-Controller (MVC) pattern separates hello modeling of hello domain, hello presentation, and hello actions based on user input into three separate classes: Model, View, and Control.</span></span> <span data-ttu-id="d1532-151">MVC, hakkında daha fazla toolearn bkz [ASP.NET hakkında bilgi edinin](http://www.asp.net/mvc).</span><span class="sxs-lookup"><span data-stu-id="d1532-151">toolearn more about MVC, see [Learn About ASP.NET](http://www.asp.net/mvc).</span></span>

<span data-ttu-id="d1532-152">Merhaba **Microsoft Power BI Embedded** örnek kod gibi ayrılmış.</span><span class="sxs-lookup"><span data-stu-id="d1532-152">hello **Microsoft Power BI Embedded** sample code is separated as follows.</span></span> <span data-ttu-id="d1532-153">Hello örnek hello kod kolayca bulabilmeniz için her bölüm hello Powerbı embedded.sln çözüm hello dosya adını içerir.</span><span class="sxs-lookup"><span data-stu-id="d1532-153">Each section includes hello file name in hello PowerBI-embedded.sln solution so that you can easily find hello code in hello sample.</span></span>

> [!NOTE]
> <span data-ttu-id="d1532-154">Bu bölümde bir özeti nasıl hello kodu yazılmıştır gösterir hello örnek kod yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="d1532-154">This section is a summary of hello sample code that shows how hello code was written.</span></span> <span data-ttu-id="d1532-155">tooview hello tam örnek, Lütfen Visual Studio hello Powerbı embedded.sln çözümde yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d1532-155">tooview hello complete sample, please load hello PowerBI-embedded.sln solution in Visual Studio.</span></span>

### <a name="model"></a><span data-ttu-id="d1532-156">modeli</span><span class="sxs-lookup"><span data-stu-id="d1532-156">Model</span></span>

<span data-ttu-id="d1532-157">Merhaba örnek sahip bir **ReportsViewModel** ve **ReportViewModel**.</span><span class="sxs-lookup"><span data-stu-id="d1532-157">hello sample has a **ReportsViewModel** and **ReportViewModel**.</span></span>

<span data-ttu-id="d1532-158">**ReportsViewModel.cs**: Power BI raporları temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d1532-158">**ReportsViewModel.cs**: Represents Power BI Reports.</span></span>

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

<span data-ttu-id="d1532-159">**ReportViewModel.cs**: Power BI raporu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d1532-159">**ReportViewModel.cs**: Represents a Power BI Report.</span></span>

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a><span data-ttu-id="d1532-160">Bağlantı dizesi</span><span class="sxs-lookup"><span data-stu-id="d1532-160">Connection string</span></span>

<span data-ttu-id="d1532-161">Merhaba bağlantı dizesi biçimi aşağıdaki hello olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="d1532-161">hello connection string must be in hello following format:</span></span>

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

<span data-ttu-id="d1532-162">Ortak sunucu ve veritabanı özniteliklerini kullanarak başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="d1532-162">Using common server and database attributes will fail.</span></span> <span data-ttu-id="d1532-163">Örneğin: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span><span class="sxs-lookup"><span data-stu-id="d1532-163">For example: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span></span>

### <a name="view"></a><span data-ttu-id="d1532-164">Görünüm</span><span class="sxs-lookup"><span data-stu-id="d1532-164">View</span></span>

<span data-ttu-id="d1532-165">Merhaba **Görünüm** Power BI hello görüntüsünü yönetir **raporları** ve Power BI **rapor**.</span><span class="sxs-lookup"><span data-stu-id="d1532-165">hello **View** manages hello display of Power BI **Reports** and a Power BI **Report**.</span></span>

<span data-ttu-id="d1532-166">**Reports.cshtml**: üzerinden yineleme **Model.Reports** toocreate bir **ActionLink**.</span><span class="sxs-lookup"><span data-stu-id="d1532-166">**Reports.cshtml**: Iterate over **Model.Reports** toocreate an **ActionLink**.</span></span> <span data-ttu-id="d1532-167">Merhaba **ActionLink** şu şekilde oluşur:</span><span class="sxs-lookup"><span data-stu-id="d1532-167">hello **ActionLink** is composed as follows:</span></span>

| <span data-ttu-id="d1532-168">Bölümü</span><span class="sxs-lookup"><span data-stu-id="d1532-168">Part</span></span> | <span data-ttu-id="d1532-169">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1532-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d1532-170">Başlık</span><span class="sxs-lookup"><span data-stu-id="d1532-170">Title</span></span> |<span data-ttu-id="d1532-171">Merhaba rapor adı.</span><span class="sxs-lookup"><span data-stu-id="d1532-171">Name of hello Report.</span></span> |
| <span data-ttu-id="d1532-172">Sorgu dizesi</span><span class="sxs-lookup"><span data-stu-id="d1532-172">QueryString</span></span> |<span data-ttu-id="d1532-173">Bağlantı toohello rapor kimliği</span><span class="sxs-lookup"><span data-stu-id="d1532-173">A link toohello Report ID.</span></span> |

    <div id="reports-nav" class="panel-collapse collapse">
        <div class="panel-body">
            <ul class="nav navbar-nav">
                @foreach (var report in Model.Reports)
                {
                    var reportClass = Request.QueryString["reportId"] == report.Id ? "active" : "";
                    <li class="@reportClass">
                        @Html.ActionLink(report.Name, "Report", new { reportId = report.Id })
                    </li>
                }
            </ul>
        </div>
    </div>

<span data-ttu-id="d1532-174">Report.cshtml: Hello ayarlamak **Model.AccessToken**, ve Lambda ifadesi hello **PowerBIReportFor**.</span><span class="sxs-lookup"><span data-stu-id="d1532-174">Report.cshtml: Set hello **Model.AccessToken**, and hello Lambda expression for **PowerBIReportFor**.</span></span>

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a><span data-ttu-id="d1532-175">Denetleyici</span><span class="sxs-lookup"><span data-stu-id="d1532-175">Controller</span></span>

<span data-ttu-id="d1532-176">**DashboardController.cs**: PowerBIClient geçirme oluşturur bir **uygulama belirteci**.</span><span class="sxs-lookup"><span data-stu-id="d1532-176">**DashboardController.cs**: Creates a PowerBIClient passing an **app token**.</span></span> <span data-ttu-id="d1532-177">Bir JSON Web Token (JWT) hello oluşturulan **imzalama anahtarı** tooget hello **kimlik bilgileri**.</span><span class="sxs-lookup"><span data-stu-id="d1532-177">A JSON Web Token (JWT) is generated from hello **Signing Key** tooget hello **Credentials**.</span></span> <span data-ttu-id="d1532-178">Merhaba **kimlik bilgileri** kullanılan toocreate örneği olan **PowerBIClient**.</span><span class="sxs-lookup"><span data-stu-id="d1532-178">hello **Credentials** are used toocreate an instance of **PowerBIClient**.</span></span> <span data-ttu-id="d1532-179">Örneği olduktan sonra **PowerBIClient**, GetReports() ve GetReportsAsync() çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1532-179">Once you have an instance of **PowerBIClient**, you can call GetReports() and GetReportsAsync().</span></span>

<span data-ttu-id="d1532-180">CreatePowerBIClient()</span><span class="sxs-lookup"><span data-stu-id="d1532-180">CreatePowerBIClient()</span></span>

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

<span data-ttu-id="d1532-181">ActionResult Reports()</span><span class="sxs-lookup"><span data-stu-id="d1532-181">ActionResult Reports()</span></span>

    public ActionResult Reports()
    {
        using (var client = this.CreatePowerBIClient())
        {
            var reportsResponse = client.Reports.GetReports(this.workspaceCollection, this.workspaceId);

            var viewModel = new ReportsViewModel
            {
                Reports = reportsResponse.Value.ToList()
            };

            return PartialView(viewModel);
        }
    }


<span data-ttu-id="d1532-182">Görev<ActionResult> rapor (dize reportId)</span><span class="sxs-lookup"><span data-stu-id="d1532-182">Task<ActionResult> Report(string reportId)</span></span>

    public async Task<ActionResult> Report(string reportId)
    {
        using (var client = this.CreatePowerBIClient())
        {
            var reportsResponse = await client.Reports.GetReportsAsync(this.workspaceCollection, this.workspaceId);
            var report = reportsResponse.Value.FirstOrDefault(r => r.Id == reportId);
            var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

            var viewModel = new ReportViewModel
            {
                Report = report,
                AccessToken = embedToken.Generate(this.accessKey)
            };

            return View(viewModel);
        }
    }

### <a name="integrate-a-report-into-your-app"></a><span data-ttu-id="d1532-183">Uygulamanıza bir rapor tümleştirme</span><span class="sxs-lookup"><span data-stu-id="d1532-183">Integrate a report into your app</span></span>

<span data-ttu-id="d1532-184">Bulduktan sonra bir **rapor**, kullandığınız bir **IFRAME** tooembed hello Power BI **rapor**.</span><span class="sxs-lookup"><span data-stu-id="d1532-184">Once you have a **Report**, you use an **IFrame** tooembed hello Power BI **Report**.</span></span> <span data-ttu-id="d1532-185">Merhaba powerbi.js'nden bir kod parçacığı aşağıda verilmiştir **Microsoft Power BI Embedded** örnek.</span><span class="sxs-lookup"><span data-stu-id="d1532-185">Here is a code snippet from  powerbi.js in hello **Microsoft Power BI Embedded** sample.</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a><span data-ttu-id="d1532-186">Uygulamanıza filtre raporları</span><span class="sxs-lookup"><span data-stu-id="d1532-186">Filter reports embedded in your application</span></span>

<span data-ttu-id="d1532-187">Bir URL söz dizimini kullanarak eklenmiş bir raporu filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1532-187">You can filter an embedded report using a URL syntax.</span></span> <span data-ttu-id="d1532-188">toodo Bu, eklediğiniz bir **$filter** sorgu dizesi parametresi ile bir **eq** işleci tooyour iFrame src url belirtilen hello Filtresi ile.</span><span class="sxs-lookup"><span data-stu-id="d1532-188">toodo this, you add a **$filter** query string parameter with an **eq** operator tooyour iFrame src url with hello filter specified.</span></span> <span data-ttu-id="d1532-189">Merhaba filtre sorgu sözdizimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="d1532-189">Here is hello filter query syntax:</span></span>

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> <span data-ttu-id="d1532-190">{tableName/fieldName} boşluk ya da özel karakter içeremez.</span><span class="sxs-lookup"><span data-stu-id="d1532-190">{tableName/fieldName} cannot include spaces or special characters.</span></span> <span data-ttu-id="d1532-191">Merhaba {fieldValue} tek bir kategorik değer kabul eder.</span><span class="sxs-lookup"><span data-stu-id="d1532-191">hello {fieldValue} accepts a single categorical value.</span></span>  

## <a name="see-also"></a><span data-ttu-id="d1532-192">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="d1532-192">See also</span></span>

[<span data-ttu-id="d1532-193">Microsoft Power BI Embedded senaryoları</span><span class="sxs-lookup"><span data-stu-id="d1532-193">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="d1532-194">Power BI Embedded ile kimlik doğrulaması ve yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="d1532-194">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="d1532-195">Rapor ekleme</span><span class="sxs-lookup"><span data-stu-id="d1532-195">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="d1532-196">Veri kümesinden yeni rapor oluşturma</span><span class="sxs-lookup"><span data-stu-id="d1532-196">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="d1532-197">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="d1532-197">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="d1532-198">JavaScript Örnek Ekleme</span><span class="sxs-lookup"><span data-stu-id="d1532-198">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="d1532-199">Başka sorunuz mu var?</span><span class="sxs-lookup"><span data-stu-id="d1532-199">More questions?</span></span> [<span data-ttu-id="d1532-200">Merhaba Power BI topluluk deneyin</span><span class="sxs-lookup"><span data-stu-id="d1532-200">Try hello Power BI Community</span></span>](http://community.powerbi.com/)
