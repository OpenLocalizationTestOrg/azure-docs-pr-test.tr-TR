---
title: aaaMonitor Application Insights ile bir SharePoint sitesi
description: "Yeni bir izleme anahtarı ile yeni bir uygulamayı izlemeye başlama"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2bfe5910-d673-4cf6-a5c1-4c115eae1be0
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2016
ms.author: bwren
ms.openlocfilehash: acfe99c24a4d77daec1017de0442ec952a1faba2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-sharepoint-site-with-application-insights"></a><span data-ttu-id="cecf3-103">Bir SharePoint sitesini Application Insights ile izleme</span><span class="sxs-lookup"><span data-stu-id="cecf3-103">Monitor a SharePoint site with Application Insights</span></span>
<span data-ttu-id="cecf3-104">Azure Application Insights hello kullanılabilirlik, performans ve kullanım uygulamalarınızın izler.</span><span class="sxs-lookup"><span data-stu-id="cecf3-104">Azure Application Insights monitors hello availability, performance and usage of your apps.</span></span> <span data-ttu-id="cecf3-105">Burada öğreneceksiniz nasıl tooset, bir SharePoint sitesi için.</span><span class="sxs-lookup"><span data-stu-id="cecf3-105">Here you'll learn how tooset it up for a SharePoint site.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="cecf3-106">Application Insights kaynağı oluşturma</span><span class="sxs-lookup"><span data-stu-id="cecf3-106">Create an Application Insights resource</span></span>
<span data-ttu-id="cecf3-107">Merhaba, [Azure portal](https://portal.azure.com), yeni bir Application Insights kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cecf3-107">In hello [Azure portal](https://portal.azure.com), create a new Application Insights resource.</span></span> <span data-ttu-id="cecf3-108">ASP.NET hello uygulama türü olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="cecf3-108">Choose ASP.NET as hello application type.</span></span>

![Özellikler'i tıklatın, başlangıç anahtarı seçin ve ctrl + C tuşlarına basın](./media/app-insights-sharepoint/01-new.png)

<span data-ttu-id="cecf3-110">açılır hello dikey penceresinde, burada, performans ve kullanım verileri uygulamanız hakkında görürsünüz hello yerdir.</span><span class="sxs-lookup"><span data-stu-id="cecf3-110">hello blade that opens is hello place where you'll see performance and usage data about your app.</span></span> <span data-ttu-id="cecf3-111">tooget geri tooit tooAzure, oturum açtığınızda, bir kutucuk için hello başlangıç ekranında bulmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cecf3-111">tooget back tooit next time you login tooAzure, you should find a tile for it on hello start screen.</span></span> <span data-ttu-id="cecf3-112">Alternatif olarak Gözat toofind'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="cecf3-112">Alternatively click Browse toofind it.</span></span>

## <a name="add-our-script-tooyour-web-pages"></a><span data-ttu-id="cecf3-113">Bizim betik tooyour web sayfaları ekleme</span><span class="sxs-lookup"><span data-stu-id="cecf3-113">Add our script tooyour web pages</span></span>
<span data-ttu-id="cecf3-114">Hızlı Başlangıç'ta web sayfaları için hello betik alın:</span><span class="sxs-lookup"><span data-stu-id="cecf3-114">In Quick Start, get hello script for web pages:</span></span>

![](./media/app-insights-sharepoint/02-monitor-web-page.png)

<span data-ttu-id="cecf3-115">Merhaba hemen önce Hello komut dosyası Ekle &lt;/head&gt; etiketi her sayfada tootrack istiyor.</span><span class="sxs-lookup"><span data-stu-id="cecf3-115">Insert hello script just before hello &lt;/head&gt; tag of every page you want tootrack.</span></span> <span data-ttu-id="cecf3-116">Web sitenizi bir ana sayfa varsa, hello betiği buraya koyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cecf3-116">If your website has a master page, you can put hello script there.</span></span> <span data-ttu-id="cecf3-117">Örneğin, bir ASP.NET MVC projesinde View\Shared\_Layout.cshtml’ye koyarsınız</span><span class="sxs-lookup"><span data-stu-id="cecf3-117">For example, in an ASP.NET MVC project, you'd put it in View\Shared\_Layout.cshtml</span></span>

<span data-ttu-id="cecf3-118">Merhaba betik hello telemetri tooyour Application Insights kaynağı yönlendirir hello izleme anahtarını içerir.</span><span class="sxs-lookup"><span data-stu-id="cecf3-118">hello script contains hello instrumentation key that directs hello telemetry tooyour Application Insights resource.</span></span>

### <a name="add-hello-code-tooyour-site-pages"></a><span data-ttu-id="cecf3-119">Merhaba kod tooyour site sayfaları ekleme</span><span class="sxs-lookup"><span data-stu-id="cecf3-119">Add hello code tooyour site pages</span></span>
#### <a name="on-hello-master-page"></a><span data-ttu-id="cecf3-120">Merhaba ana sayfada</span><span class="sxs-lookup"><span data-stu-id="cecf3-120">On hello master page</span></span>
<span data-ttu-id="cecf3-121">Merhaba sitenin ana sayfa düzenleyebilirsiniz varsa, hello sitesindeki her sayfada izleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="cecf3-121">If you can edit hello site's master page, that will provide monitoring for every page in hello site.</span></span>

<span data-ttu-id="cecf3-122">Hello Yöneticisi sayfasını gözden geçirin ve SharePoint Designer veya başka bir düzenleyici kullanarak düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cecf3-122">Check out hello master page and edit it using SharePoint Designer or any other editor.</span></span>

![](./media/app-insights-sharepoint/03-master.png)

<span data-ttu-id="cecf3-123">Merhaba kodu hello hemen önce ekleyin </head> etiketi.</span><span class="sxs-lookup"><span data-stu-id="cecf3-123">Add hello code just before hello </head> tag.</span></span> 

![](./media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a><span data-ttu-id="cecf3-124">Veya belirli sayfalarda</span><span class="sxs-lookup"><span data-stu-id="cecf3-124">Or on individual pages</span></span>
<span data-ttu-id="cecf3-125">toomonitor sayfaları, sınırlı sayıda ekleme hello betik ayrı olarak tooeach sayfası.</span><span class="sxs-lookup"><span data-stu-id="cecf3-125">toomonitor a limited set of pages, add hello script separately tooeach page.</span></span> 

<span data-ttu-id="cecf3-126">Web bölümü eklemek ve hello kod parçacığını içinde embed.</span><span class="sxs-lookup"><span data-stu-id="cecf3-126">Insert a web part and embed hello code snippet in it.</span></span>

![](./media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a><span data-ttu-id="cecf3-127">Uygulamanızla ilgili verileri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="cecf3-127">View data about your app</span></span>
<span data-ttu-id="cecf3-128">Uygulamanızı yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="cecf3-128">Redeploy your app.</span></span>

<span data-ttu-id="cecf3-129">Dönüş tooyour uygulaması dikey penceresinde hello [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cecf3-129">Return tooyour application blade in hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="cecf3-130">Merhaba ilk olayları aramada görünür.</span><span class="sxs-lookup"><span data-stu-id="cecf3-130">hello first events will appear in Search.</span></span> 

![](./media/app-insights-sharepoint/09-search.png)

<span data-ttu-id="cecf3-131">Daha fazla veri bekliyorsanız, birkaç saniye geçtikten sonra Yenile’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="cecf3-131">Click Refresh after a few seconds if you're expecting more data.</span></span>

<span data-ttu-id="cecf3-132">Merhaba genel bakış dikey penceresinden tıklayın **kullanım analizi** toosee toocharts, kullanıcılar, oturumlar ve sayfa görünümleri:</span><span class="sxs-lookup"><span data-stu-id="cecf3-132">From hello overview blade, click **Usage analytics** toosee toocharts of users, sessions and page views:</span></span>

![](./media/app-insights-sharepoint/06-usage.png)

<span data-ttu-id="cecf3-133">Tüm grafik toosee daha fazla ayrıntı - örneğin sayfa görünümleri tıklatın:</span><span class="sxs-lookup"><span data-stu-id="cecf3-133">Click any chart toosee more details - for example Page Views:</span></span>

![](./media/app-insights-sharepoint/07-pages.png)

<span data-ttu-id="cecf3-134">Veya Kullanıcılar:</span><span class="sxs-lookup"><span data-stu-id="cecf3-134">Or Users:</span></span>

![](./media/app-insights-sharepoint/08-users.png)

## <a name="capturing-user-id"></a><span data-ttu-id="cecf3-135">Kullanıcı Kimliğini Yakalama</span><span class="sxs-lookup"><span data-stu-id="cecf3-135">Capturing User Id</span></span>
<span data-ttu-id="cecf3-136">Merhaba standart web sayfası kod parçacığını hello kullanıcı kimliği SharePoint'ten yakalamaz, ancak bunu ile küçük bir değişiklik yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cecf3-136">hello standard web page code snippet doesn't capture hello user id from SharePoint, but you can do that with a small modification.</span></span>

1. <span data-ttu-id="cecf3-137">Uygulamanızın izleme anahtarını hello Essentials açılan Application Insights'ta kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="cecf3-137">Copy your app's instrumentation key from hello Essentials drop-down in Application Insights.</span></span> 

    ![](./media/app-insights-sharepoint/02-props.png)

1. <span data-ttu-id="cecf3-138">Merhaba izleme anahtarını aşağıdaki hello parçacığında 'XXXX için' değiştirin.</span><span class="sxs-lookup"><span data-stu-id="cecf3-138">Substitute hello instrumentation key for 'XXXX' in hello snippet below.</span></span> 
2. <span data-ttu-id="cecf3-139">SharePoint uygulamanızda hello parçacığı hello portaldan almak yerine Hello komut dosyası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="cecf3-139">Embed hello script in your SharePoint app instead of hello snippet you get from hello portal.</span></span>

```


<SharePoint:ScriptLink ID="ScriptLink1" name="SP.js" runat="server" localizable="false" loadafterui="true" /> 
<SharePoint:ScriptLink ID="ScriptLink2" name="SP.UserProfiles.js" runat="server" localizable="false" loadafterui="true" /> 

<script type="text/javascript"> 
var personProperties; 

// Ensure that hello SP.UserProfiles.js file is loaded before hello custom code runs. 
SP.SOD.executeOrDelayUntilScriptLoaded(getUserProperties, 'SP.UserProfiles.js'); 

function getUserProperties() { 
    // Get hello current client context and PeopleManager instance. 
    var clientContext = new SP.ClientContext.get_current(); 
    var peopleManager = new SP.UserProfiles.PeopleManager(clientContext); 

    // Get user properties for hello target user. 
    // tooget hello PersonProperties object for hello current user, use hello 
    // getMyProperties method. 

    personProperties = peopleManager.getMyProperties(); 

    // Load hello PersonProperties object and send hello request. 
    clientContext.load(personProperties); 
    clientContext.executeQueryAsync(onRequestSuccess, onRequestFail); 
} 

// This function runs if hello executeQueryAsync call succeeds. 
function onRequestSuccess() { 
var appInsights=window.appInsights||function(config){
function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
    }({
        instrumentationKey:"XXXX"
    });
    window.appInsights=appInsights;
    appInsights.trackPageView(document.title,window.location.href, {User: personProperties.get_displayName()});
} 

// This function runs if hello executeQueryAsync call fails. 
function onRequestFail(sender, args) { 
} 
</script> 


```



## <a name="next-steps"></a><span data-ttu-id="cecf3-140">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="cecf3-140">Next Steps</span></span>
* <span data-ttu-id="cecf3-141">[Web testleri](app-insights-monitor-web-app-availability.md) sitenizin toomonitor hello kullanılabilirlik.</span><span class="sxs-lookup"><span data-stu-id="cecf3-141">[Web tests](app-insights-monitor-web-app-availability.md) toomonitor hello availability of your site.</span></span>
* <span data-ttu-id="cecf3-142">Diğer uygulama türleri için [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cecf3-142">[Application Insights](app-insights-overview.md) for other types of app.</span></span>

<!--Link references-->


