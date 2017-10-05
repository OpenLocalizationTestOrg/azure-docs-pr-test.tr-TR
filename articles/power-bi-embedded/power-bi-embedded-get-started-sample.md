---
title: "Bir örnek ile kullanmaya başlama"
description: "Power BI Embedded, iş zekası uygulamanıza etkileşimli Power BI raporları eklemek için SDK'yi kullanın"
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
ms.openlocfilehash: c3cb1763f807220a4a829f410d7eb77974b25776
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-power-bi-embedded-sample"></a><span data-ttu-id="a5f89-103">Power BI Embedded örneği kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="a5f89-103">Get started with Power BI Embedded sample</span></span>

<span data-ttu-id="a5f89-104">İle **Microsoft Power BI Embedded**, Power BI raporları sağ web veya mobil uygulamaları tümleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5f89-104">With **Microsoft Power BI Embedded**, you can integrate Power BI reports right into your web or mobile applications.</span></span> <span data-ttu-id="a5f89-105">Bu makalede, biz size tanıtmak **Power BI Embedded** get başlatılan örnek.</span><span class="sxs-lookup"><span data-stu-id="a5f89-105">In this article, we'll introduce you to the **Power BI Embedded** get started sample.</span></span>

<span data-ttu-id="a5f89-106">Biz daha ilerlemeden önce aşağıdaki kaynaklara kaydetmek istersiniz.</span><span class="sxs-lookup"><span data-stu-id="a5f89-106">Before we go any further, you'll probably want to save the following resources.</span></span> <span data-ttu-id="a5f89-107">Bunlar Power BI raporları örnek uygulaması ve kendi uygulamalarınızı halinde çok tümleştirdiğinizde yardımcı olacağız.</span><span class="sxs-lookup"><span data-stu-id="a5f89-107">They'll help you when integrating Power BI reports into the sample app and your own apps too.</span></span>

* [<span data-ttu-id="a5f89-108">Örnek çalışma web uygulaması</span><span class="sxs-lookup"><span data-stu-id="a5f89-108">Sample workspace web app</span></span>](http://go.microsoft.com/fwlink/?LinkId=761493)
* [<span data-ttu-id="a5f89-109">Power BI Embedded API Başvurusu</span><span class="sxs-lookup"><span data-stu-id="a5f89-109">Power BI Embedded API reference</span></span>](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* <span data-ttu-id="a5f89-110">[Power BI Embedded .NET SDK'sı ](http://go.microsoft.com/fwlink/?LinkId=746472) (NuGet aracılığıyla kullanılabilir)</span><span class="sxs-lookup"><span data-stu-id="a5f89-110">[Power BI Embedded .NET SDK ](http://go.microsoft.com/fwlink/?LinkId=746472) (available via NuGet)</span></span>
* [<span data-ttu-id="a5f89-111">JavaScript rapor örnek ekleme</span><span class="sxs-lookup"><span data-stu-id="a5f89-111">JavaScript Report Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> <span data-ttu-id="a5f89-112">En az bir oluşturmanıza gerek yapılandırabilirsiniz ve Power BI Embedded alma çalışma başlatıldı örnek önce **çalışma alanı koleksiyonu** Azure aboneliğinizde.</span><span class="sxs-lookup"><span data-stu-id="a5f89-112">Before you can configure and run the Power BI Embedded get started sample, you need to create at least one **Workspace Collection** in your Azure subscription.</span></span> <span data-ttu-id="a5f89-113">Nasıl oluşturulacağını öğrenmek için bir **çalışma alanı koleksiyonu** Azure Portal görüyor [Power BI Embedded ile çalışmaya başlama](power-bi-embedded-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a5f89-113">To learn how to create a **Workspace Collection** in the Azure Portal see [Getting Started with Power BI Embedded](power-bi-embedded-get-started.md).</span></span>

## <a name="configure-the-sample-app"></a><span data-ttu-id="a5f89-114">Örnek uygulamayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a5f89-114">Configure the sample app</span></span>

<span data-ttu-id="a5f89-115">Şimdi örnek uygulamayı çalıştırmak için gerekli bileşenleri erişmek için Visual Studio geliştirme ortamını ayarlama aracılığıyla yol.</span><span class="sxs-lookup"><span data-stu-id="a5f89-115">Let's walk through setting up your Visual Studio development environment to access the  components needed to run the sample app.</span></span>

1. <span data-ttu-id="a5f89-116">İndirip sıkıştırmasını [Power BI Embedded - bir web uygulamasına bir rapor tümleştirme](http://go.microsoft.com/fwlink/?LinkId=761493) github'da örnek.</span><span class="sxs-lookup"><span data-stu-id="a5f89-116">Download and unzip the [Power BI Embedded - Integrate a report into a web app](http://go.microsoft.com/fwlink/?LinkId=761493) sample on GitHub.</span></span>
2. <span data-ttu-id="a5f89-117">Açık **Powerbı embedded.sln** Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a5f89-117">Open **PowerBI-embedded.sln** in Visual Studio.</span></span> <span data-ttu-id="a5f89-118">Yürütme gerekebilir **güncelleştirme paketini** bu çözümde kullanılan paketler güncelleştirmek için NuGET Paket Yöneticisi konsolunda komutu.</span><span class="sxs-lookup"><span data-stu-id="a5f89-118">You may need to execute the **Update-Package** command in the NuGET Package Manager Console in order to update the packages used in this solution.</span></span>
3. <span data-ttu-id="a5f89-119">Çözümü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a5f89-119">Build the solution.</span></span>
4. <span data-ttu-id="a5f89-120">Çalıştırma **ProvisionSample** konsol uygulaması.</span><span class="sxs-lookup"><span data-stu-id="a5f89-120">Run the **ProvisionSample** console app.</span></span> <span data-ttu-id="a5f89-121">Örnek konsol uygulamasındaki bir çalışma alanı sağlamak ve PBIX dosyasını içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="a5f89-121">In the sample console app, you provision a workspace and import a PBIX file.</span></span>
5. <span data-ttu-id="a5f89-122">Yeni bir sağlamak için **çalışma**, 1 seçeneğini belirleyin **koleksiyonu Yönetimi**ve ardından seçeneğini 6, **yeni bir çalışma alanı sağlanamadı**</span><span class="sxs-lookup"><span data-stu-id="a5f89-122">To provision a new **Workspace**, select option 1, **Collection management**, and then select option 6, **Provision a new Workspace**</span></span>
6. <span data-ttu-id="a5f89-123">Yeni bir almak için **rapor**, 2, seçeneğini belirleyin **rapor Yönetim**ve seçenek 3, ardından **PBIX Masaüstü içeri aktarma dosyası bir çalışma alanına**.</span><span class="sxs-lookup"><span data-stu-id="a5f89-123">To import a new **Report**, select option 2, **Report management**, and then select option 3, **Import PBIX Desktop file into a workspace**.</span></span>

7. <span data-ttu-id="a5f89-124">Girin, **çalışma alanı koleksiyonu** adı ve **erişim tuşu**.</span><span class="sxs-lookup"><span data-stu-id="a5f89-124">Enter your **Workspace Collection** name, and **Access Key**.</span></span> <span data-ttu-id="a5f89-125">Bunlar alabileceğiniz **Azure Portal**.</span><span class="sxs-lookup"><span data-stu-id="a5f89-125">You can get these in the **Azure Portal**.</span></span> <span data-ttu-id="a5f89-126">Nasıl alınacağı hakkında daha fazla bilgi için **erişim tuşu**, bkz: [görünümü Power BI API'si erişim anahtarlarını](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) içinde Microsoft Power BI Embedded ile çalışmaya başlama.</span><span class="sxs-lookup"><span data-stu-id="a5f89-126">To learn more about how to get your **Access Key**, see [View Power BI API Access Keys](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) in Get started with Microsoft Power BI Embedded.</span></span>

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. <span data-ttu-id="a5f89-127">Kopyala ve yeni oluşturulan kaydedin **çalışma alanı kimliği** bu makalenin sonraki bölümlerinde kullanılacak.</span><span class="sxs-lookup"><span data-stu-id="a5f89-127">Copy and save the newly created **Workspace ID** to use later in this article.</span></span> <span data-ttu-id="a5f89-128">Sonra **çalışma alanı kimliği** olan oluşturulan, onu bulabilirsiniz **Azure Portal**.</span><span class="sxs-lookup"><span data-stu-id="a5f89-128">After the **Workspace ID** is created, you can find it the **Azure Portal**.</span></span>

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. <span data-ttu-id="a5f89-129">Bir PBIX aktarmak için **çalışma**, seçeneğini belirleyin **6. İçeri aktarma PBIX Masaüstü dosyası var olan bir çalışma alanına**.</span><span class="sxs-lookup"><span data-stu-id="a5f89-129">To import a PBIX file into your **Workspace**, select option **6. Import PBIX Desktop file into an existing workspace**.</span></span> <span data-ttu-id="a5f89-130">Kullanışlı dosya PBIX yoksa, indirebilirsiniz [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span><span class="sxs-lookup"><span data-stu-id="a5f89-130">If you don't have a PBIX file handy, you can download the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>
10. <span data-ttu-id="a5f89-131">İstenirse, için kolay bir ad girin, **Dataset**.</span><span class="sxs-lookup"><span data-stu-id="a5f89-131">If prompted, enter a friendly name for your **Dataset**.</span></span>

<span data-ttu-id="a5f89-132">Benzer bir yanıt görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="a5f89-132">You should see a response like:</span></span>

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> <span data-ttu-id="a5f89-133">PBIX dosyanızın tüm doğrudan sorgu bağlantıları içeriyorsa, bağlantı dizelerini güncelleştirmek için 7 seçeneği çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a5f89-133">If your PBIX file contains any direct query connections, run option 7 to update the connection strings.</span></span>

<span data-ttu-id="a5f89-134">Bu noktada, içeri aktarılan bir Power BI PBIX rapor vardır, **çalışma**.</span><span class="sxs-lookup"><span data-stu-id="a5f89-134">At this point, you have a Power BI PBIX report imported into your **Workspace**.</span></span> <span data-ttu-id="a5f89-135">Şimdi çalıştırmak ne bakalım **Power BI Embedded** başlatılan örnek web uygulamasını edinin.</span><span class="sxs-lookup"><span data-stu-id="a5f89-135">Now, let's look at how to run the **Power BI Embedded** get started sample web app.</span></span>

## <a name="run-the-sample-web-app"></a><span data-ttu-id="a5f89-136">Örnek web uygulaması çalıştırın</span><span class="sxs-lookup"><span data-stu-id="a5f89-136">Run the sample web app</span></span>
<span data-ttu-id="a5f89-137">Web uygulaması örneği içeri aktarılan raporlar işleyen örnek bir uygulama olduğundan, **çalışma**.</span><span class="sxs-lookup"><span data-stu-id="a5f89-137">The web app sample is a sample application that renders reports imported into your **Workspace**.</span></span> <span data-ttu-id="a5f89-138">Web uygulaması örneği yapılandırma bırakılır.</span><span class="sxs-lookup"><span data-stu-id="a5f89-138">Here's how to configure the web app sample.</span></span>

1. <span data-ttu-id="a5f89-139">İçinde **Powerbı katıştırılmış** Visual Studio çözümü, sağ tıklatma **EmbedSample** web uygulaması ve seçin **başlangıç projesi olarak ayarla**.</span><span class="sxs-lookup"><span data-stu-id="a5f89-139">In the **PowerBI-embedded** Visual Studio solution, right click the **EmbedSample** web application, and choose **Set as StartUp project**.</span></span>
2. <span data-ttu-id="a5f89-140">İçinde **web.config**, **EmbedSample** web uygulaması, düzenleme **appSettings**: **AccessKey**, **WorkspaceCollection** adı ve **Workspaceıd**.</span><span class="sxs-lookup"><span data-stu-id="a5f89-140">In **web.config**, in the **EmbedSample** web application, edit the **appSettings**: **AccessKey**, **WorkspaceCollection** name, and **WorkspaceId**.</span></span>

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. <span data-ttu-id="a5f89-141">Çalıştırma **EmbedSample** web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="a5f89-141">Run the **EmbedSample** web application.</span></span>

<span data-ttu-id="a5f89-142">Çalıştırdığınız sonra **EmbedSample** web uygulaması, sol gezinti bölmesinin içermelidir bir **raporları** menüsü.</span><span class="sxs-lookup"><span data-stu-id="a5f89-142">Once you run the **EmbedSample** web application, the left navigation panel should contain a **Reports** menu.</span></span> <span data-ttu-id="a5f89-143">İçeri aktardığınız raporunu görüntülemek için Genişlet **raporları**ve bir rapora tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a5f89-143">To view the report you imported, expand **Reports**, and click a report.</span></span> <span data-ttu-id="a5f89-144">İçeri aktardığınız varsa [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), örnek web uygulaması şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="a5f89-144">If you imported the [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), the sample web app would look like this:</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

<span data-ttu-id="a5f89-145">Bir raporu tıklattıktan sonra **EmbedSample** web uygulaması görünmelidir bir şey:</span><span class="sxs-lookup"><span data-stu-id="a5f89-145">After you click a report, the **EmbedSample** web application should look something this:</span></span>

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-the-sample-code"></a><span data-ttu-id="a5f89-146">Örnek kod keşfetme</span><span class="sxs-lookup"><span data-stu-id="a5f89-146">Explore the sample code</span></span>

<span data-ttu-id="a5f89-147">**Microsoft Power BI Embedded** örnektir nasıl tümleştirileceği gösteren örnek bir web uygulaması **Power BI** uygulamanıza raporlar.</span><span class="sxs-lookup"><span data-stu-id="a5f89-147">The **Microsoft Power BI Embedded** sample is an example web app that shows you how to integrate **Power BI** reports into your app.</span></span> <span data-ttu-id="a5f89-148">Bir Model-View-Controller (MVC) tasarım deseni en iyi yöntemleri göstermek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="a5f89-148">It uses a Model-View-Controller (MVC) design pattern to demonstrate best practices.</span></span> <span data-ttu-id="a5f89-149">Bu bölüm içinde keşfedebilirsiniz örnek kod parçalarını vurgular **Powerbı katıştırılmış** web uygulaması çözümü.</span><span class="sxs-lookup"><span data-stu-id="a5f89-149">This section highlights parts of the sample code that you can explore within the **PowerBI-embedded** web app solution.</span></span> <span data-ttu-id="a5f89-150">Etki alanı, sunu ve üç ayrı sınıfları kullanıcı girişine bağlı eylemleri modelleme Model-View-Controller (MVC) deseni ayırır: Model, Görünüm ve denetim.</span><span class="sxs-lookup"><span data-stu-id="a5f89-150">The Model-View-Controller (MVC) pattern separates the modeling of the domain, the presentation, and the actions based on user input into three separate classes: Model, View, and Control.</span></span> <span data-ttu-id="a5f89-151">MVC hakkında daha fazla bilgi için bkz: [ASP.NET hakkında bilgi edinin](http://www.asp.net/mvc).</span><span class="sxs-lookup"><span data-stu-id="a5f89-151">To learn more about MVC, see [Learn About ASP.NET](http://www.asp.net/mvc).</span></span>

<span data-ttu-id="a5f89-152">**Microsoft Power BI Embedded** örnek kod gibi ayrılmış.</span><span class="sxs-lookup"><span data-stu-id="a5f89-152">The **Microsoft Power BI Embedded** sample code is separated as follows.</span></span> <span data-ttu-id="a5f89-153">Örnek kod kolayca bulabilmeniz için her bölüm Powerbı embedded.sln çözümde dosya adını içerir.</span><span class="sxs-lookup"><span data-stu-id="a5f89-153">Each section includes the file name in the PowerBI-embedded.sln solution so that you can easily find the code in the sample.</span></span>

> [!NOTE]
> <span data-ttu-id="a5f89-154">Bu bölümde, kodu nasıl yazılmıştır gösteren örnek kod bir özetidir.</span><span class="sxs-lookup"><span data-stu-id="a5f89-154">This section is a summary of the sample code that shows how the code was written.</span></span> <span data-ttu-id="a5f89-155">Tam örnek görüntülemek için lütfen Visual Studio Powerbı embedded.sln çözümde yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a5f89-155">To view the complete sample, please load the PowerBI-embedded.sln solution in Visual Studio.</span></span>

### <a name="model"></a><span data-ttu-id="a5f89-156">modeli</span><span class="sxs-lookup"><span data-stu-id="a5f89-156">Model</span></span>

<span data-ttu-id="a5f89-157">Örnek sahip bir **ReportsViewModel** ve **ReportViewModel**.</span><span class="sxs-lookup"><span data-stu-id="a5f89-157">The sample has a **ReportsViewModel** and **ReportViewModel**.</span></span>

<span data-ttu-id="a5f89-158">**ReportsViewModel.cs**: Power BI raporları temsil eder.</span><span class="sxs-lookup"><span data-stu-id="a5f89-158">**ReportsViewModel.cs**: Represents Power BI Reports.</span></span>

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

<span data-ttu-id="a5f89-159">**ReportViewModel.cs**: Power BI raporu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="a5f89-159">**ReportViewModel.cs**: Represents a Power BI Report.</span></span>

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a><span data-ttu-id="a5f89-160">Bağlantı dizesi</span><span class="sxs-lookup"><span data-stu-id="a5f89-160">Connection string</span></span>

<span data-ttu-id="a5f89-161">Bağlantı dizesi şu biçimde olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="a5f89-161">The connection string must be in the following format:</span></span>

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

<span data-ttu-id="a5f89-162">Ortak sunucu ve veritabanı özniteliklerini kullanarak başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="a5f89-162">Using common server and database attributes will fail.</span></span> <span data-ttu-id="a5f89-163">Örneğin: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span><span class="sxs-lookup"><span data-stu-id="a5f89-163">For example: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,</span></span>

### <a name="view"></a><span data-ttu-id="a5f89-164">Görünüm</span><span class="sxs-lookup"><span data-stu-id="a5f89-164">View</span></span>

<span data-ttu-id="a5f89-165">**Görünüm** Power BI görüntüsünü yönetir **raporları** ve Power BI **rapor**.</span><span class="sxs-lookup"><span data-stu-id="a5f89-165">The **View** manages the display of Power BI **Reports** and a Power BI **Report**.</span></span>

<span data-ttu-id="a5f89-166">**Reports.cshtml**: üzerinden yineleme **Model.Reports** oluşturmak için bir **ActionLink**.</span><span class="sxs-lookup"><span data-stu-id="a5f89-166">**Reports.cshtml**: Iterate over **Model.Reports** to create an **ActionLink**.</span></span> <span data-ttu-id="a5f89-167">**ActionLink** şu şekilde oluşur:</span><span class="sxs-lookup"><span data-stu-id="a5f89-167">The **ActionLink** is composed as follows:</span></span>

| <span data-ttu-id="a5f89-168">Bölümü</span><span class="sxs-lookup"><span data-stu-id="a5f89-168">Part</span></span> | <span data-ttu-id="a5f89-169">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a5f89-169">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a5f89-170">Başlık</span><span class="sxs-lookup"><span data-stu-id="a5f89-170">Title</span></span> |<span data-ttu-id="a5f89-171">Raporun adı.</span><span class="sxs-lookup"><span data-stu-id="a5f89-171">Name of the Report.</span></span> |
| <span data-ttu-id="a5f89-172">Sorgu dizesi</span><span class="sxs-lookup"><span data-stu-id="a5f89-172">QueryString</span></span> |<span data-ttu-id="a5f89-173">Rapor Kimliği Bağla</span><span class="sxs-lookup"><span data-stu-id="a5f89-173">A link to the Report ID.</span></span> |

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

<span data-ttu-id="a5f89-174">Report.cshtml: Ayarlamak **Model.AccessToken**ve Lambda ifadesi **PowerBIReportFor**.</span><span class="sxs-lookup"><span data-stu-id="a5f89-174">Report.cshtml: Set the **Model.AccessToken**, and the Lambda expression for **PowerBIReportFor**.</span></span>

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a><span data-ttu-id="a5f89-175">Denetleyici</span><span class="sxs-lookup"><span data-stu-id="a5f89-175">Controller</span></span>

<span data-ttu-id="a5f89-176">**DashboardController.cs**: PowerBIClient geçirme oluşturur bir **uygulama belirteci**.</span><span class="sxs-lookup"><span data-stu-id="a5f89-176">**DashboardController.cs**: Creates a PowerBIClient passing an **app token**.</span></span> <span data-ttu-id="a5f89-177">Bir JSON Web Token (JWT) oluşturulur **imzalama anahtarı** almak için **kimlik bilgileri**.</span><span class="sxs-lookup"><span data-stu-id="a5f89-177">A JSON Web Token (JWT) is generated from the **Signing Key** to get the **Credentials**.</span></span> <span data-ttu-id="a5f89-178">**Kimlik bilgileri** bir örneğini oluşturmak için kullanılan **PowerBIClient**.</span><span class="sxs-lookup"><span data-stu-id="a5f89-178">The **Credentials** are used to create an instance of **PowerBIClient**.</span></span> <span data-ttu-id="a5f89-179">Örneği olduktan sonra **PowerBIClient**, GetReports() ve GetReportsAsync() çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5f89-179">Once you have an instance of **PowerBIClient**, you can call GetReports() and GetReportsAsync().</span></span>

<span data-ttu-id="a5f89-180">CreatePowerBIClient()</span><span class="sxs-lookup"><span data-stu-id="a5f89-180">CreatePowerBIClient()</span></span>

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

<span data-ttu-id="a5f89-181">ActionResult Reports()</span><span class="sxs-lookup"><span data-stu-id="a5f89-181">ActionResult Reports()</span></span>

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


<span data-ttu-id="a5f89-182">Görev<ActionResult> rapor (dize reportId)</span><span class="sxs-lookup"><span data-stu-id="a5f89-182">Task<ActionResult> Report(string reportId)</span></span>

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

### <a name="integrate-a-report-into-your-app"></a><span data-ttu-id="a5f89-183">Uygulamanıza bir rapor tümleştirme</span><span class="sxs-lookup"><span data-stu-id="a5f89-183">Integrate a report into your app</span></span>

<span data-ttu-id="a5f89-184">Bulduktan sonra bir **rapor**, kullandığınız bir **IFRAME** Power BI katıştırmak için **rapor**.</span><span class="sxs-lookup"><span data-stu-id="a5f89-184">Once you have a **Report**, you use an **IFrame** to embed the Power BI **Report**.</span></span> <span data-ttu-id="a5f89-185">İçinde powerbi.js gelen kod parçacığı aşağıda verilmiştir **Microsoft Power BI Embedded** örnek.</span><span class="sxs-lookup"><span data-stu-id="a5f89-185">Here is a code snippet from  powerbi.js in the **Microsoft Power BI Embedded** sample.</span></span>

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a><span data-ttu-id="a5f89-186">Uygulamanıza filtre raporları</span><span class="sxs-lookup"><span data-stu-id="a5f89-186">Filter reports embedded in your application</span></span>

<span data-ttu-id="a5f89-187">Bir URL söz dizimini kullanarak eklenmiş bir raporu filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5f89-187">You can filter an embedded report using a URL syntax.</span></span> <span data-ttu-id="a5f89-188">Bunu yapmak için eklediğiniz bir **$filter** sorgu dizesi parametresi ile bir **eq** belirterek iFrame src URL'nize belirtilen filtre ile işleci.</span><span class="sxs-lookup"><span data-stu-id="a5f89-188">To do this, you add a **$filter** query string parameter with an **eq** operator to your iFrame src url with the filter specified.</span></span> <span data-ttu-id="a5f89-189">Filtre sorgu sözdizimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="a5f89-189">Here is the filter query syntax:</span></span>

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> <span data-ttu-id="a5f89-190">{tableName/fieldName} boşluk ya da özel karakter içeremez.</span><span class="sxs-lookup"><span data-stu-id="a5f89-190">{tableName/fieldName} cannot include spaces or special characters.</span></span> <span data-ttu-id="a5f89-191">{fieldValue} tek bir kategorik değer kabul eder.</span><span class="sxs-lookup"><span data-stu-id="a5f89-191">The {fieldValue} accepts a single categorical value.</span></span>  

## <a name="see-also"></a><span data-ttu-id="a5f89-192">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="a5f89-192">See also</span></span>

[<span data-ttu-id="a5f89-193">Microsoft Power BI Embedded senaryoları</span><span class="sxs-lookup"><span data-stu-id="a5f89-193">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="a5f89-194">Power BI Embedded ile kimlik doğrulaması ve yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="a5f89-194">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="a5f89-195">Rapor ekleme</span><span class="sxs-lookup"><span data-stu-id="a5f89-195">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="a5f89-196">Veri kümesinden yeni rapor oluşturma</span><span class="sxs-lookup"><span data-stu-id="a5f89-196">Create a new report from a dataset</span></span>](power-bi-embedded-create-report-from-dataset.md)  
[<span data-ttu-id="a5f89-197">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="a5f89-197">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="a5f89-198">JavaScript Örnek Ekleme</span><span class="sxs-lookup"><span data-stu-id="a5f89-198">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="a5f89-199">Başka sorunuz mu var?</span><span class="sxs-lookup"><span data-stu-id="a5f89-199">More questions?</span></span> [<span data-ttu-id="a5f89-200">Power BI Topluluğu'nu deneyin</span><span class="sxs-lookup"><span data-stu-id="a5f89-200">Try the Power BI Community</span></span>](http://community.powerbi.com/)
