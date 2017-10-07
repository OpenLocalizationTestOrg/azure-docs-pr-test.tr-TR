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
# <a name="get-started-with-power-bi-embedded-sample"></a>Power BI Embedded örneği kullanmaya başlama

İle **Microsoft Power BI Embedded**, Power BI raporları sağ web veya mobil uygulamaları tümleştirebilirsiniz. Bu makalede, sizi, toohello tanıtmak **Power BI Embedded** get başlatılan örnek.

Biz daha ilerlemeden önce kaynakları aşağıdaki toosave hello büyük olasılıkla isteyeceksiniz. Bunlar Power BI raporları hello örnek uygulaması ve kendi uygulamalarınızı halinde çok tümleştirdiğinizde yardımcı olacağız.

* [Örnek çalışma web uygulaması](http://go.microsoft.com/fwlink/?LinkId=761493)
* [Power BI Embedded API Başvurusu](https://msdn.microsoft.com/en-US/library/azure/mt711507.aspx)
* [Power BI Embedded .NET SDK'sı ](http://go.microsoft.com/fwlink/?LinkId=746472) (NuGet aracılığıyla kullanılabilir)
* [JavaScript rapor örnek ekleme](https://microsoft.github.io/PowerBI-JavaScript/demo)

> [!NOTE] 
> Yapılandırabilirsiniz ve Power BI Embedded alma çalışma hello başlatılan örnek önce toocreate en az bir gereksinim **çalışma alanı koleksiyonu** Azure aboneliğinizde. toolearn nasıl toocreate bir **çalışma alanı koleksiyonu** hello Azure Portal bkz [Power BI Embedded ile çalışmaya başlama](power-bi-embedded-get-started.md).

## <a name="configure-hello-sample-app"></a>Merhaba örnek uygulamayı yapılandırma

Şimdi Visual Studio geliştirme ortamında tooaccess hello bileşenleri gerekli toorun hello örnek uygulamanızı ayarlama aracılığıyla yol.

1. İndirip hello sıkıştırmasını [Power BI Embedded - bir web uygulamasına bir rapor tümleştirme](http://go.microsoft.com/fwlink/?LinkId=761493) github'da örnek.
2. Açık **Powerbı embedded.sln** Visual Studio. Tooexecute hello gerekebilir **güncelleştirme paketini** hello NuGET Paket Yöneticisi konsolunda bu çözümde kullanılan sipariş tooupdate hello paketlerde komutu.
3. Merhaba çözümü oluşturun.
4. Merhaba çalıştırmak **ProvisionSample** konsol uygulaması. Merhaba örnek konsol uygulamasındaki bir çalışma alanı sağlamak ve PBIX dosyasını içeri aktarın.
5. Yeni bir tooprovision **çalışma**, 1 seçeneğini belirleyin **koleksiyonu Yönetimi**ve ardından seçeneğini 6, **yeni bir çalışma alanı sağlanamadı**
6. Yeni bir tooimport **rapor**, 2, seçeneğini belirleyin **rapor Yönetim**ve seçenek 3, ardından **alma PBIX Masaüstü dosya bir çalışma alanına**.

7. Girin, **çalışma alanı koleksiyonu** adı ve **erişim tuşu**. Bu hello alabilirsiniz **Azure Portal**. toolearn nasıl hakkında daha fazla tooget, **erişim tuşu**, bkz: [görünümü Power BI API'si erişim anahtarlarını](power-bi-embedded-get-started.md#view-power-bi-api-access-keys) içinde Microsoft Power BI Embedded ile çalışmaya başlama.

    ![](media/powerbi-embedded-get-started-sample/azure-portal.png)
8. Kopyala ve yeni oluşturulan hello kaydedin **çalışma alanı kimliği** bu makalenin sonraki bölümlerinde toouse. Merhaba sonra **çalışma alanı kimliği** olan oluşturulan, bunu hello bulabilirsiniz **Azure Portal**.

    ![](media/powerbi-embedded-get-started-sample/workspace-id.png)
9. tooimport bir PBIX dosyası içine, **çalışma**, seçeneğini belirleyin **6. İçeri aktarma PBIX Masaüstü dosyası var olan bir çalışma alanına**. Kullanışlı dosya PBIX yoksa, hello indirebilirsiniz [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).
10. İstenirse, için kolay bir ad girin, **Dataset**.

Benzer bir yanıt görmeniz gerekir:

```
Checking import state... Publishing
Checking import state... Succeeded
```

> [!NOTE]
> PBIX dosyanızın tüm doğrudan sorgu bağlantıları içeriyorsa, seçeneği 7 tooupdate hello bağlantı dizeleri çalıştırın.

Bu noktada, içeri aktarılan bir Power BI PBIX rapor vardır, **çalışma**. Şimdi ne bakalım toorun hello **Power BI Embedded** başlatılan örnek web uygulamasını edinin.

## <a name="run-hello-sample-web-app"></a>Merhaba örnek web uygulaması çalıştırın
Merhaba web uygulaması örneği içeri aktarılan raporlar işleyen örnek bir uygulama olduğundan, **çalışma**. Nasıl tooconfigure hello web uygulaması örneği aşağıda verilmiştir.

1. Merhaba, **Powerbı katıştırılmış** Visual Studio çözümü, sağ tıklatın hello **EmbedSample** web uygulaması ve seçin **başlangıç projesi olarak ayarla**.
2. İçinde **web.config**, hello içinde **EmbedSample** web uygulaması, hello Düzenle **appSettings**: **AccessKey**,  **WorkspaceCollection** adı ve **Workspaceıd**.

    ```
    <appSettings>
        <add key="powerbi:AccessKey" value="" />
        <add key="powerbi:ApiUrl" value="https://api.powerbi.com" />
        <add key="powerbi:WorkspaceCollection" value="" />
        <add key="powerbi:WorkspaceId" value="" />
    </appSettings>
    ```
3. Merhaba çalıştırmak **EmbedSample** web uygulaması.

Merhaba çalıştırdıktan sonra **EmbedSample** web uygulaması hello sol gezinti bölmesini içermelidir bir **raporları** menüsü. içeri aktardığınız, tooview hello rapor genişletin **raporları**ve bir rapora tıklayın. Merhaba aldıysanız [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547), hello örnek web uygulaması şuna benzeyebilir:

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-sample-left-nav.png)

Bir raporu tıklattıktan sonra hello **EmbedSample** web uygulaması görünmelidir bir şey:

![](media/powerbi-embedded-get-started-sample/sample-web-app.png)

## <a name="explore-hello-sample-code"></a>Merhaba örnek kod keşfetme

Merhaba **Microsoft Power BI Embedded** örnektir nasıl gösteren örnek bir web uygulaması toointegrate **Power BI** uygulamanıza raporlar. Bir Model-View-Controller (MVC) kullanan tasarım deseni toodemonstrate en iyi yöntemleri. Bu bölüm içinde hello keşfedebilirsiniz hello örnek kod parçalarını vurgular **Powerbı katıştırılmış** web uygulaması çözümü. Merhaba Model-View-Controller (MVC) deseni ayıran hello modelleme hello etki alanı, hello sunu ve üç ayrı sınıfları kullanıcı girişine bağlı hello eylemleri: Model, Görünüm ve denetim. MVC, hakkında daha fazla toolearn bkz [ASP.NET hakkında bilgi edinin](http://www.asp.net/mvc).

Merhaba **Microsoft Power BI Embedded** örnek kod gibi ayrılmış. Hello örnek hello kod kolayca bulabilmeniz için her bölüm hello Powerbı embedded.sln çözüm hello dosya adını içerir.

> [!NOTE]
> Bu bölümde bir özeti nasıl hello kodu yazılmıştır gösterir hello örnek kod yer almaktadır. tooview hello tam örnek, Lütfen Visual Studio hello Powerbı embedded.sln çözümde yükleyin.

### <a name="model"></a>modeli

Merhaba örnek sahip bir **ReportsViewModel** ve **ReportViewModel**.

**ReportsViewModel.cs**: Power BI raporları temsil eder.

    public class ReportsViewModel
    {
        public List<Report> Reports { get; set; }
    }

**ReportViewModel.cs**: Power BI raporu temsil eder.

    public classReportViewModel
    {
        public IReport Report { get; set; }

        public string AccessToken { get; set; }
    }

### <a name="connection-string"></a>Bağlantı dizesi

Merhaba bağlantı dizesi biçimi aşağıdaki hello olmalıdır:

```
Data Source=tcp:MyServer.database.windows.net,1433;Initial Catalog=MyDatabase
```

Ortak sunucu ve veritabanı özniteliklerini kullanarak başarısız olur. Örneğin: Server=tcp:MyServer.database.windows.net,1433;Database=MyDatabase,

### <a name="view"></a>Görünüm

Merhaba **Görünüm** Power BI hello görüntüsünü yönetir **raporları** ve Power BI **rapor**.

**Reports.cshtml**: üzerinden yineleme **Model.Reports** toocreate bir **ActionLink**. Merhaba **ActionLink** şu şekilde oluşur:

| Bölümü | Açıklama |
| --- | --- |
| Başlık |Merhaba rapor adı. |
| Sorgu dizesi |Bağlantı toohello rapor kimliği |

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

Report.cshtml: Hello ayarlamak **Model.AccessToken**, ve Lambda ifadesi hello **PowerBIReportFor**.

    @model ReportViewModel

    ...

    <div class="side-body padding-top">
        @Html.PowerBIAccessToken(Model.AccessToken)
        @Html.PowerBIReportFor(m => m.Report, new { style = "height:85vh" })
    </div>

### <a name="controller"></a>Denetleyici

**DashboardController.cs**: PowerBIClient geçirme oluşturur bir **uygulama belirteci**. Bir JSON Web Token (JWT) hello oluşturulan **imzalama anahtarı** tooget hello **kimlik bilgileri**. Merhaba **kimlik bilgileri** kullanılan toocreate örneği olan **PowerBIClient**. Örneği olduktan sonra **PowerBIClient**, GetReports() ve GetReportsAsync() çağırabilirsiniz.

CreatePowerBIClient()

    private IPowerBIClient CreatePowerBIClient()
    {
        var credentials = new TokenCredentials(accessKey, "AppKey");
        var client = new PowerBIClient(credentials)
        {
            BaseUri = new Uri(apiUrl)
        };

        return client;
    }

ActionResult Reports()

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


Görev<ActionResult> rapor (dize reportId)

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

### <a name="integrate-a-report-into-your-app"></a>Uygulamanıza bir rapor tümleştirme

Bulduktan sonra bir **rapor**, kullandığınız bir **IFRAME** tooembed hello Power BI **rapor**. Merhaba powerbi.js'nden bir kod parçacığı aşağıda verilmiştir **Microsoft Power BI Embedded** örnek.

![](media/powerbi-embedded-get-started-sample/power-bi-embedded-iframe-code.png)

## <a name="filter-reports-embedded-in-your-application"></a>Uygulamanıza filtre raporları

Bir URL söz dizimini kullanarak eklenmiş bir raporu filtreleyebilirsiniz. toodo Bu, eklediğiniz bir **$filter** sorgu dizesi parametresi ile bir **eq** işleci tooyour iFrame src url belirtilen hello Filtresi ile. Merhaba filtre sorgu sözdizimi şöyledir:

```
https://app.powerbi.com/reportEmbed
?reportId=d2a0ea38-...-9673-ee9655d54a4a&
$filter={tableName/fieldName}%20eq%20'{fieldValue}'
```

> [!NOTE]
> {tableName/fieldName} boşluk ya da özel karakter içeremez. Merhaba {fieldValue} tek bir kategorik değer kabul eder.  

## <a name="see-also"></a>Ayrıca bkz.

[Microsoft Power BI Embedded senaryoları](power-bi-embedded-scenarios.md)  
[Power BI Embedded ile kimlik doğrulaması ve yetkilendirme](power-bi-embedded-app-token-flow.md)  
[Rapor ekleme](power-bi-embedded-embed-report.md)  
[Veri kümesinden yeni rapor oluşturma](power-bi-embedded-create-report-from-dataset.md)  
[Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[JavaScript Örnek Ekleme](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
Başka sorunuz mu var? [Merhaba Power BI topluluk deneyin](http://community.powerbi.com/)
