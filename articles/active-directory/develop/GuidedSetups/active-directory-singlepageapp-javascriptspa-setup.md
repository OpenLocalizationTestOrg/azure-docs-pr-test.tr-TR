---
title: aaaAzure AD v2 JS SPA destekli Kurulumu - Kurulumu | Microsoft Docs
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
ms.openlocfilehash: 19e15c6c8db8bea2975f30e7505af79ccad17e02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="setting-up-your-web-server-or-project"></a><span data-ttu-id="8431e-103">Web sunucusu veya projesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="8431e-103">Setting up your web server or project</span></span>

> <span data-ttu-id="8431e-104">Toodownload, bunun yerine bu örnek 's proje tercih ediyorsunuz?</span><span class="sxs-lookup"><span data-stu-id="8431e-104">Prefer toodownload this sample's project instead?</span></span> 
> - [<span data-ttu-id="8431e-105">Merhaba Visual Studio projesi indirme</span><span class="sxs-lookup"><span data-stu-id="8431e-105">Download hello Visual Studio project</span></span>](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/VisualStudio.zip)
>
> <span data-ttu-id="8431e-106">or</span><span class="sxs-lookup"><span data-stu-id="8431e-106">or</span></span>
> - <span data-ttu-id="8431e-107">[Merhaba proje dosyalarını indirmek](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip) Python gibi bir yerel web sunucusu için</span><span class="sxs-lookup"><span data-stu-id="8431e-107">[Download hello project files](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip) for a local web server, such as Python</span></span>
>
> <span data-ttu-id="8431e-108">Ve toohello atla [yapılandırma adımı](#create-an-application-express) tooconfigure hello kod örneği, yürütmeden önce.</span><span class="sxs-lookup"><span data-stu-id="8431e-108">And then  skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing it.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8431e-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8431e-109">Prerequisites</span></span>
<span data-ttu-id="8431e-110">Bir yerel web sunucusu gibi [Python http.server](https://www.python.org/downloads/), [http sunucu](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), ya da IIS Express ile tümleştirme [Visual Studio 2017](https://www.visualstudio.com/downloads/) gerekli toorun destekli bu kurulur.</span><span class="sxs-lookup"><span data-stu-id="8431e-110">A local web server such as [Python http.server](https://www.python.org/downloads/), [http-server](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), or IIS Express integration with [Visual Studio 2017](https://www.visualstudio.com/downloads/) is required toorun this guided setup.</span></span> 

<span data-ttu-id="8431e-111">Bu kılavuzdaki yönergeleri Python ve Visual Studio 2017 bağlıdır, ancak herhangi bir geliştirme ortamında veya Web sunucusu ücretsiz toouse eşitleyerek.</span><span class="sxs-lookup"><span data-stu-id="8431e-111">Instructions in this guide are based on both Python and Visual Studio 2017, but feel free toouse any other development environment or Web Server.</span></span>

## <a name="create-your-project"></a><span data-ttu-id="8431e-112">Projenizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="8431e-112">Create your project</span></span> 

> ### <a name="option-1-visual-studio"></a><span data-ttu-id="8431e-113">Seçenek 1: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8431e-113">Option 1: Visual Studio</span></span> 
> <span data-ttu-id="8431e-114">Visual Studio kullanarak ve yeni proje oluşturma, hello toocreate yeni bir Visual Studio çözüm adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="8431e-114">If you are using Visual Studio and are creating a new project, follow hello steps below toocreate a new Visual Studio solution:</span></span>
> 1.    <span data-ttu-id="8431e-115">Visual Studio'da:`File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="8431e-115">In Visual Studio:  `File` > `New` > `Project`</span></span>
> 2.    <span data-ttu-id="8431e-116">Altında `Visual C#\Web`seçin`ASP.NET Web Application (.NET Framework)`</span><span class="sxs-lookup"><span data-stu-id="8431e-116">Under `Visual C#\Web`, select `ASP.NET Web Application (.NET Framework)`</span></span>
> 3.    <span data-ttu-id="8431e-117">Uygulamanızı adlandırın ve tıklayın *Tamam*</span><span class="sxs-lookup"><span data-stu-id="8431e-117">Name your application and click *OK*</span></span>
> 4.    <span data-ttu-id="8431e-118">Altında `New ASP.NET Web Application`seçin`Empty`</span><span class="sxs-lookup"><span data-stu-id="8431e-118">Under `New ASP.NET Web Application`, select `Empty`</span></span>

<p/><!-- -->

> ### <a name="option-2-python-other-web-servers"></a><span data-ttu-id="8431e-119">Seçenek 2: Python / diğer web sunucuları</span><span class="sxs-lookup"><span data-stu-id="8431e-119">Option 2: Python/ other web servers</span></span>
> <span data-ttu-id="8431e-120">Yüklediğinizden emin olun [Python](https://www.python.org/downloads/), hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="8431e-120">Make sure you have installed [Python](https://www.python.org/downloads/), then follow hello step below:</span></span>
> - <span data-ttu-id="8431e-121">Bir klasör toohost uygulamanızı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8431e-121">Create a folder toohost your application.</span></span>


## <a name="create-your-single-page-applications-ui"></a><span data-ttu-id="8431e-122">Tek sayfalı uygulama kullanıcı Arabirimi oluşturma</span><span class="sxs-lookup"><span data-stu-id="8431e-122">Create your single page application’s UI</span></span>
1.  <span data-ttu-id="8431e-123">Oluşturma bir *index.html* JavaScript SPA dosyası.</span><span class="sxs-lookup"><span data-stu-id="8431e-123">Create an *index.html* file for your JavaScript SPA.</span></span> <span data-ttu-id="8431e-124">Visual Studio, select hello proje (Proje kök klasöründe) kullanıyorsanız, sağ tıklatın ve seçin: `Add`  >  `New Item`  >  `HTML page` ve index.html adlandırın</span><span class="sxs-lookup"><span data-stu-id="8431e-124">If you are using Visual Studio, select hello project (project root folder), right click and select: `Add` > `New Item` > `HTML page` and name it index.html</span></span>
2.  <span data-ttu-id="8431e-125">Aşağıdaki kod tooyour sayfası hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="8431e-125">Add hello following code tooyour page:</span></span>
```html
<!DOCTYPE html>
<html>
<head>
    <!-- bootstrap reference used for styling hello page -->
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

    <!-- This app uses cdn tooreference msal.js (recommended). 
         You can also download it from: https://github.com/AzureAD/microsoft-authentication-library-for-js -->
    <script src="https://secure.aadcdn.microsoftonline-p.com/lib/0.1.1/js/msal.min.js"></script>

    <!-- hello 'bluebird' and 'fetch' references below are required if you need toorun this application on Internet Explorer -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/bluebird/3.3.4/bluebird.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/fetch/2.0.3/fetch.min.js"></script>

    <script type="text/javascript" src="msalconfig.js"></script>
    <script type="text/javascript" src="app.js"></script>
</body>
</html>
````
