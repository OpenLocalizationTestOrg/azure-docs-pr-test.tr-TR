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
# <a name="monitor-a-sharepoint-site-with-application-insights"></a>Bir SharePoint sitesini Application Insights ile izleme
Azure Application Insights hello kullanılabilirlik, performans ve kullanım uygulamalarınızın izler. Burada öğreneceksiniz nasıl tooset, bir SharePoint sitesi için.

## <a name="create-an-application-insights-resource"></a>Application Insights kaynağı oluşturma
Merhaba, [Azure portal](https://portal.azure.com), yeni bir Application Insights kaynağı oluşturun. ASP.NET hello uygulama türü olarak seçin.

![Özellikler'i tıklatın, başlangıç anahtarı seçin ve ctrl + C tuşlarına basın](./media/app-insights-sharepoint/01-new.png)

açılır hello dikey penceresinde, burada, performans ve kullanım verileri uygulamanız hakkında görürsünüz hello yerdir. tooget geri tooit tooAzure, oturum açtığınızda, bir kutucuk için hello başlangıç ekranında bulmanız gerekir. Alternatif olarak Gözat toofind'ı tıklatın.

## <a name="add-our-script-tooyour-web-pages"></a>Bizim betik tooyour web sayfaları ekleme
Hızlı Başlangıç'ta web sayfaları için hello betik alın:

![](./media/app-insights-sharepoint/02-monitor-web-page.png)

Merhaba hemen önce Hello komut dosyası Ekle &lt;/head&gt; etiketi her sayfada tootrack istiyor. Web sitenizi bir ana sayfa varsa, hello betiği buraya koyabilirsiniz. Örneğin, bir ASP.NET MVC projesinde View\Shared\_Layout.cshtml’ye koyarsınız

Merhaba betik hello telemetri tooyour Application Insights kaynağı yönlendirir hello izleme anahtarını içerir.

### <a name="add-hello-code-tooyour-site-pages"></a>Merhaba kod tooyour site sayfaları ekleme
#### <a name="on-hello-master-page"></a>Merhaba ana sayfada
Merhaba sitenin ana sayfa düzenleyebilirsiniz varsa, hello sitesindeki her sayfada izleme sağlar.

Hello Yöneticisi sayfasını gözden geçirin ve SharePoint Designer veya başka bir düzenleyici kullanarak düzenleyebilirsiniz.

![](./media/app-insights-sharepoint/03-master.png)

Merhaba kodu hello hemen önce ekleyin </head> etiketi. 

![](./media/app-insights-sharepoint/04-code.png)

#### <a name="or-on-individual-pages"></a>Veya belirli sayfalarda
toomonitor sayfaları, sınırlı sayıda ekleme hello betik ayrı olarak tooeach sayfası. 

Web bölümü eklemek ve hello kod parçacığını içinde embed.

![](./media/app-insights-sharepoint/05-page.png)

## <a name="view-data-about-your-app"></a>Uygulamanızla ilgili verileri görüntüleme
Uygulamanızı yeniden dağıtın.

Dönüş tooyour uygulaması dikey penceresinde hello [Azure portal](https://portal.azure.com).

Merhaba ilk olayları aramada görünür. 

![](./media/app-insights-sharepoint/09-search.png)

Daha fazla veri bekliyorsanız, birkaç saniye geçtikten sonra Yenile’ye tıklayın.

Merhaba genel bakış dikey penceresinden tıklayın **kullanım analizi** toosee toocharts, kullanıcılar, oturumlar ve sayfa görünümleri:

![](./media/app-insights-sharepoint/06-usage.png)

Tüm grafik toosee daha fazla ayrıntı - örneğin sayfa görünümleri tıklatın:

![](./media/app-insights-sharepoint/07-pages.png)

Veya Kullanıcılar:

![](./media/app-insights-sharepoint/08-users.png)

## <a name="capturing-user-id"></a>Kullanıcı Kimliğini Yakalama
Merhaba standart web sayfası kod parçacığını hello kullanıcı kimliği SharePoint'ten yakalamaz, ancak bunu ile küçük bir değişiklik yapabilirsiniz.

1. Uygulamanızın izleme anahtarını hello Essentials açılan Application Insights'ta kopyalayın. 

    ![](./media/app-insights-sharepoint/02-props.png)

1. Merhaba izleme anahtarını aşağıdaki hello parçacığında 'XXXX için' değiştirin. 
2. SharePoint uygulamanızda hello parçacığı hello portaldan almak yerine Hello komut dosyası ekleyin.

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



## <a name="next-steps"></a>Sonraki Adımlar
* [Web testleri](app-insights-monitor-web-app-availability.md) sitenizin toomonitor hello kullanılabilirlik.
* Diğer uygulama türleri için [Application Insights](app-insights-overview.md).

<!--Link references-->


