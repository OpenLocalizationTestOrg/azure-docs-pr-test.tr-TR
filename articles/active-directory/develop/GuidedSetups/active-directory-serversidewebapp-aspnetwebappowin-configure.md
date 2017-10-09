---
title: aaaAzure AD v2 ASP.NET Web sunucusu Getting Started - Config | Microsoft Docs
description: "Microsoft oturum açma Openıd Connect standardını kullanan geleneksel web tarayıcı tabanlı bir uygulama ile ASP.NET çözümünü uygulama"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: e666be4622ad30aaa1e12e49ae56bbe1e129b2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="35012-103">(Hızlı) uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="35012-103">Create an application (Express)</span></span>
<span data-ttu-id="35012-104">Merhaba uygulamanızda tooregister gereksinim artık *Microsoft uygulama kayıt portalı*:</span><span class="sxs-lookup"><span data-stu-id="35012-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="35012-105">Merhaba aracılığıyla uygulamanızı kaydetme [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span><span class="sxs-lookup"><span data-stu-id="35012-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span></span>
2.  <span data-ttu-id="35012-106">Uygulamanız ve e-posta için bir ad girin</span><span class="sxs-lookup"><span data-stu-id="35012-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="35012-107">Kurulum destekli Hello seçeneğinin işaretli olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="35012-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="35012-108">Merhaba yönergeleri tooadd tekrar yönlendirme URL'sini tooyour uygulama izleyin</span><span class="sxs-lookup"><span data-stu-id="35012-108">Follow hello instructions tooadd a Redirect URL tooyour application</span></span>

## <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="35012-109">Uygulama kayıt bilgileri tooyour çözümünüz (Gelişmiş) ekleyin</span><span class="sxs-lookup"><span data-stu-id="35012-109">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="35012-110">Merhaba uygulamanızda tooregister gereksinim artık *Microsoft uygulama kayıt portalı*:</span><span class="sxs-lookup"><span data-stu-id="35012-110">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="35012-111">Toohello Git [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/portal/register-app) tooregister uygulama</span><span class="sxs-lookup"><span data-stu-id="35012-111">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="35012-112">Uygulamanız ve e-posta için bir ad girin</span><span class="sxs-lookup"><span data-stu-id="35012-112">Enter a name for your application and your email</span></span> 
3.  <span data-ttu-id="35012-113">Destekli kurulumu için Hello seçeneğinin işaretli olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="35012-113">Make sure hello option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="35012-114">Tıklatın `Add Platform`sonra seçin`Web`</span><span class="sxs-lookup"><span data-stu-id="35012-114">Click `Add Platform`, then select `Web`</span></span>
5.  <span data-ttu-id="35012-115">TooVisual Studio geri dönün ve, Çözüm Gezgini'nde başlangıç projesini seçin ve (bir özellik penceresinde F4 tuşuna basın görmüyorsanız) hello özellikleri penceresine bakın</span><span class="sxs-lookup"><span data-stu-id="35012-115">Go back tooVisual Studio and, in Solution Explorer, select hello project and look at hello Properties window (if you don’t see a Properties window, press F4)</span></span>
6.  <span data-ttu-id="35012-116">SSL etkin çok değiştirme`True`</span><span class="sxs-lookup"><span data-stu-id="35012-116">Change SSL Enabled too`True`</span></span>
7.  <span data-ttu-id="35012-117">Merhaba SSL URL'sini kopyalayın ve bu URL yeniden yönlendirme URL'si toohello listesi hello kayıt Portalı'nın yönlendirme URL'si listesinde ekleyin:</span><span class="sxs-lookup"><span data-stu-id="35012-117">Copy hello SSL URL and add this URL toohello list of Redirect URLs in hello Registration Portal’s list of Redirect URLs:</span></span><br/><br/>![Proje Özellikleri](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
8.  <span data-ttu-id="35012-119">Merhaba aşağıdakileri ekleyin `web.config` hello bölümünde hello kök klasöründe yer alan `configuration\appSettings`:</span><span class="sxs-lookup"><span data-stu-id="35012-119">Add hello following in `web.config` located in hello root folder under hello section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="Enter_the_Application_Id_here" />
<add key="redirectUri" value="Enter_the_Redirect_URL_here" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
<!-- Workaround for Docs conversion bug -->
<ol start="9">
<li>
<span data-ttu-id="35012-120">Değiştir `ClientId` hello uygulama kimliği yalnızca kayıtlı sahip</span><span class="sxs-lookup"><span data-stu-id="35012-120">Replace `ClientId` with hello Application Id you just registered</span></span>
</li>
<li>
<span data-ttu-id="35012-121">Değiştir `redirectUri` hello projenizin SSL URL ile</span><span class="sxs-lookup"><span data-stu-id="35012-121">Replace `redirectUri` with hello SSL URL of your project</span></span>
</li>
</ol>
<!-- End Docs -->
