---
title: "Azure AD v2 ASP.NET Web sunucusu alma başlatıldı - Config | Microsoft Docs"
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
ms.openlocfilehash: 0c627802ccfba230dcde2dafffee26cb1c895791
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="4ca8a-103">(Hızlı) uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="4ca8a-103">Create an application (Express)</span></span>
<span data-ttu-id="4ca8a-104">Uygulamanızı kaydetmeniz gerekir artık *Microsoft uygulama kayıt portalı*:</span><span class="sxs-lookup"><span data-stu-id="4ca8a-104">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="4ca8a-105">Uygulamanızı aracılığıyla kaydetme [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span><span class="sxs-lookup"><span data-stu-id="4ca8a-105">Register your application via the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span></span>
2.  <span data-ttu-id="4ca8a-106">Uygulamanız ve e-posta için bir ad girin</span><span class="sxs-lookup"><span data-stu-id="4ca8a-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="4ca8a-107">Kurulum destekli seçeneğinin işaretli olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="4ca8a-107">Make sure the option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="4ca8a-108">Uygulamanıza bir yeniden yönlendirme URL'si eklemek için yönergeleri izleyin</span><span class="sxs-lookup"><span data-stu-id="4ca8a-108">Follow the instructions to add a Redirect URL to your application</span></span>

## <a name="add-your-application-registration-information-to-your-solution-advanced"></a><span data-ttu-id="4ca8a-109">Uygulama kayıt bilgilerinizi çözümünüze (Gelişmiş) ekleyin</span><span class="sxs-lookup"><span data-stu-id="4ca8a-109">Add your application registration information to your solution (Advanced)</span></span>
<span data-ttu-id="4ca8a-110">Uygulamanızı kaydetmeniz gerekir artık *Microsoft uygulama kayıt portalı*:</span><span class="sxs-lookup"><span data-stu-id="4ca8a-110">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="4ca8a-111">Git [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/portal/register-app) bir uygulamayı kaydetmek için</span><span class="sxs-lookup"><span data-stu-id="4ca8a-111">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) to register an application</span></span>
2. <span data-ttu-id="4ca8a-112">Uygulamanız ve e-posta için bir ad girin</span><span class="sxs-lookup"><span data-stu-id="4ca8a-112">Enter a name for your application and your email</span></span> 
3.  <span data-ttu-id="4ca8a-113">Destekli kurulumu için seçeneğinin işaretli olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="4ca8a-113">Make sure the option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="4ca8a-114">Tıklatın `Add Platform`sonra seçin`Web`</span><span class="sxs-lookup"><span data-stu-id="4ca8a-114">Click `Add Platform`, then select `Web`</span></span>
5.  <span data-ttu-id="4ca8a-115">Visual Studio'ya geri dönün ve Çözüm Gezgini'nde, projeyi seçin ve ardından (bir özellik penceresinde F4 tuşuna basın görmüyorsanız) özellikleri penceresine bakın gidin</span><span class="sxs-lookup"><span data-stu-id="4ca8a-115">Go back to Visual Studio and, in Solution Explorer, select the project and look at the Properties window (if you don’t see a Properties window, press F4)</span></span>
6.  <span data-ttu-id="4ca8a-116">Değişiklik SSL etkin`True`</span><span class="sxs-lookup"><span data-stu-id="4ca8a-116">Change SSL Enabled to `True`</span></span>
7.  <span data-ttu-id="4ca8a-117">SSL URL'sini kopyalayın ve bu URL yönlendirme URL'si listesine kayıt Portalı'nın listesinde yönlendirme URL'si ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4ca8a-117">Copy the SSL URL and add this URL to the list of Redirect URLs in the Registration Portal’s list of Redirect URLs:</span></span><br/><br/>![Proje Özellikleri](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
8.  <span data-ttu-id="4ca8a-119">Aşağıdakileri ekleyin `web.config` bölümünün altında kök klasöründe yer `configuration\appSettings`:</span><span class="sxs-lookup"><span data-stu-id="4ca8a-119">Add the following in `web.config` located in the root folder under the section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="Enter_the_Application_Id_here" />
<add key="redirectUri" value="Enter_the_Redirect_URL_here" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
<!-- Workaround for Docs conversion bug -->
<ol start="9">
<li>
<span data-ttu-id="4ca8a-120">Değiştir `ClientId` yalnızca kayıtlı uygulama kimliği</span><span class="sxs-lookup"><span data-stu-id="4ca8a-120">Replace `ClientId` with the Application Id you just registered</span></span>
</li>
<li>
<span data-ttu-id="4ca8a-121">Değiştir `redirectUri` projenizin SSL URL'si</span><span class="sxs-lookup"><span data-stu-id="4ca8a-121">Replace `redirectUri` with the SSL URL of your project</span></span>
</li>
</ol>
<!-- End Docs -->
