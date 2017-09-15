---
title: Azure AD v2 JS SPA destekli Kurulumu - Kurulumu | Microsoft Docs
description: "JavaScript SPA uygulamaları Azure Active Directory v2 bitiş noktası tarafından erişim belirteçleri gerektiren bir API nasıl çağırabilirsiniz"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: fc9f88cc8d23abcfa8ea30e346192732b422ffa2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
## <a name="setting-up-your-web-server-or-project"></a><span data-ttu-id="2126f-103">Web sunucusu veya projesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="2126f-103">Setting up your web server or project</span></span>

> <span data-ttu-id="2126f-104">Bu örnek 's proje yerine indirmeyi tercih ediyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="2126f-104">Prefer to download this sample's project instead?</span></span> 
> - [<span data-ttu-id="2126f-105">Visual Studio projesi indirme</span><span class="sxs-lookup"><span data-stu-id="2126f-105">Download the Visual Studio project</span></span>](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/VisualStudio.zip)
>
> <span data-ttu-id="2126f-106">or</span><span class="sxs-lookup"><span data-stu-id="2126f-106">or</span></span>
> - <span data-ttu-id="2126f-107">[Proje dosyalarını indirmek](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip) Python gibi bir yerel web sunucusu için</span><span class="sxs-lookup"><span data-stu-id="2126f-107">[Download the project files](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip) for a local web server, such as Python</span></span>
>
> <span data-ttu-id="2126f-108">Ve ardından geçin [yapılandırma adımı](#create-an-application-express) kod örneği çalıştırmadan önce yapılandırmak için.</span><span class="sxs-lookup"><span data-stu-id="2126f-108">And then  skip to the [Configuration step](#create-an-application-express) to configure the code sample before executing it.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2126f-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2126f-109">Prerequisites</span></span>
<span data-ttu-id="2126f-110">Bir yerel web sunucusu gibi [Python http.server](https://www.python.org/downloads/), [http sunucu](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), ya da IIS Express ile tümleştirme [Visual Studio 2017](https://www.visualstudio.com/downloads/) Bu Destekli kurulumu çalıştırmak için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="2126f-110">A local web server such as [Python http.server](https://www.python.org/downloads/), [http-server](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), or IIS Express integration with [Visual Studio 2017](https://www.visualstudio.com/downloads/) is required to run this guided setup.</span></span> 

<span data-ttu-id="2126f-111">Bu kılavuzdaki yönergeleri Python ve Visual Studio 2017 bağlıdır, ancak herhangi bir geliştirme ortamı veya Web sunucusu kullanmak üzere çekinmeyin.</span><span class="sxs-lookup"><span data-stu-id="2126f-111">Instructions in this guide are based on both Python and Visual Studio 2017, but feel free to use any other development environment or Web Server.</span></span>

## <a name="create-your-project"></a><span data-ttu-id="2126f-112">Projenizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="2126f-112">Create your project</span></span> 

> ### <a name="option-1-visual-studio"></a><span data-ttu-id="2126f-113">Seçenek 1: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2126f-113">Option 1: Visual Studio</span></span> 
> <span data-ttu-id="2126f-114">Visual Studio kullanarak ve yeni proje oluşturma, yeni bir Visual Studio çözüm oluşturmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="2126f-114">If you are using Visual Studio and are creating a new project, follow the steps below to create a new Visual Studio solution:</span></span>
> 1.    <span data-ttu-id="2126f-115">Visual Studio'da:`File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="2126f-115">In Visual Studio:  `File` > `New` > `Project`</span></span>
> 2.    <span data-ttu-id="2126f-116">Altında `Visual C#\Web`seçin`ASP.NET Web Application (.NET Framework)`</span><span class="sxs-lookup"><span data-stu-id="2126f-116">Under `Visual C#\Web`, select `ASP.NET Web Application (.NET Framework)`</span></span>
> 3.    <span data-ttu-id="2126f-117">Uygulamanızı adlandırın ve tıklayın *Tamam*</span><span class="sxs-lookup"><span data-stu-id="2126f-117">Name your application and click *OK*</span></span>
> 4.    <span data-ttu-id="2126f-118">Altında `New ASP.NET Web Application`seçin`Empty`</span><span class="sxs-lookup"><span data-stu-id="2126f-118">Under `New ASP.NET Web Application`, select `Empty`</span></span>

<p/><!-- -->

> ### <a name="option-2-python-other-web-servers"></a><span data-ttu-id="2126f-119">Seçenek 2: Python / diğer web sunucuları</span><span class="sxs-lookup"><span data-stu-id="2126f-119">Option 2: Python/ other web servers</span></span>
> <span data-ttu-id="2126f-120">Yüklediğinizden emin olun [Python](https://www.python.org/downloads/), aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="2126f-120">Make sure you have installed [Python](https://www.python.org/downloads/), then follow the step below:</span></span>
> - <span data-ttu-id="2126f-121">Uygulamanızı barındırmak için bir klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2126f-121">Create a folder to host your application.</span></span>


## <a name="create-your-single-page-applications-ui"></a><span data-ttu-id="2126f-122">Tek sayfalı uygulama kullanıcı Arabirimi oluşturma</span><span class="sxs-lookup"><span data-stu-id="2126f-122">Create your single page application’s UI</span></span>
1.  <span data-ttu-id="2126f-123">Oluşturma bir *index.html* JavaScript SPA dosyası.</span><span class="sxs-lookup"><span data-stu-id="2126f-123">Create an *index.html* file for your JavaScript SPA.</span></span> <span data-ttu-id="2126f-124">Visual Studio kullanıyorsanız, projeyi (Proje kök klasöründe) seçin, sağ tıklatın ve seçin: `Add`  >  `New Item`  >  `HTML page` ve index.html adlandırın</span><span class="sxs-lookup"><span data-stu-id="2126f-124">If you are using Visual Studio, select the project (project root folder), right click and select: `Add` > `New Item` > `HTML page` and name it index.html</span></span>
2.  <span data-ttu-id="2126f-125">Sayfanıza aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="2126f-125">Add the following code to your page:</span></span>
```html
<!DOCTYPE html>
<html>
<head>
    <!-- bootstrap reference used for styling the page -->
    <link href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <title>JavaScript SPA Guided Setup</title>
</head>
<body style="margin: 40px">
    <button id="callGraphButton" type="button" class="btn btn-primary" onclick="callGraphApi()">Call Microsoft Graph API</button>
    <div id="errorMessage" class="text-danger"></div>
    <div class="hidden">
        <h3>Graph API Call Response</h3>
        <pre class="well" id="graphResponse"></pre>
    </div>
    <div class="hidden">
        <h3>Access Token</h3>
        <pre class="well" id="accessToken"></pre>
    </div>
    <div class="hidden">
        <h3>ID Token Claims</h3>
        <pre class="well" id="userInfo"></pre>
    </div>
    <button id="signOutButton" type="button" class="btn btn-primary hidden" onclick="signOut()">Sign out</button>

    <!-- This app uses cdn to reference msal.js (recommended). 
         You can also download it from: https://github.com/AzureAD/microsoft-authentication-library-for-js -->
    <script src="https://secure.aadcdn.microsoftonline-p.com/lib/0.1.1/js/msal.min.js"></script>

    <!-- The 'bluebird' and 'fetch' references below are required if you need to run this application on Internet Explorer -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/bluebird/3.3.4/bluebird.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/fetch/2.0.3/fetch.min.js"></script>

    <script type="text/javascript" src="msalconfig.js"></script>
    <script type="text/javascript" src="app.js"></script>
</body>
</html>
````
