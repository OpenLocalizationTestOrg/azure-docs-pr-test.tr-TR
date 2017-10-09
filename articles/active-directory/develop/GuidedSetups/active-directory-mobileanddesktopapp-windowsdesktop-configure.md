---
title: "aaaAzure AD v2 Windows Masaüstü Getting Started - Config | Microsoft Docs"
description: "Nasıl bir Windows Masaüstü .NET (XAML) uygulama erişim belirteci almak ve Azure Active Directory v2 bitiş noktası tarafından korunan bir API çağrısı. | Microsoft Azure | Microsoft Azure"
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
ms.openlocfilehash: 39c257e3e0cb09491f6fe005877601bd46824d12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="62112-104">(Hızlı) uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="62112-104">Create an application (Express)</span></span>
<span data-ttu-id="62112-105">Merhaba uygulamanızda tooregister gereksinim artık *Microsoft uygulama kayıt portalı*:</span><span class="sxs-lookup"><span data-stu-id="62112-105">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="62112-106">Merhaba aracılığıyla uygulamanızı kaydetme [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span><span class="sxs-lookup"><span data-stu-id="62112-106">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span></span>
2.  <span data-ttu-id="62112-107">Uygulamanız ve e-posta için bir ad girin</span><span class="sxs-lookup"><span data-stu-id="62112-107">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="62112-108">Kurulum destekli Hello seçeneğinin işaretli olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="62112-108">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="62112-109">Merhaba yönergeleri tooobtain hello uygulama kimliği izleyin ve kodunuza yapıştırın</span><span class="sxs-lookup"><span data-stu-id="62112-109">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="62112-110">Uygulama kayıt bilgileri tooyour çözümünüz (Gelişmiş) ekleyin</span><span class="sxs-lookup"><span data-stu-id="62112-110">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="62112-111">Merhaba uygulamanızda tooregister gereksinim artık *Microsoft uygulama kayıt portalı*:</span><span class="sxs-lookup"><span data-stu-id="62112-111">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="62112-112">Toohello Git [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/portal/register-app) tooregister uygulama</span><span class="sxs-lookup"><span data-stu-id="62112-112">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="62112-113">Uygulamanız ve e-posta için bir ad girin</span><span class="sxs-lookup"><span data-stu-id="62112-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="62112-114">Destekli kurulumu için Hello seçeneğinin işaretli olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="62112-114">Make sure hello option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="62112-115">Tıklatın `Add Platform`seçeneğini belirleyip `Native Application` ve kaydetme ulaştı.</span><span class="sxs-lookup"><span data-stu-id="62112-115">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5. <span data-ttu-id="62112-116">Uygulama Kimliği Hello GUID kopyalayın, tooVisual Studio, açık dönün `App.xaml.cs` ve değiştirme `your_client_id_here` hello uygulama kimliği yalnızca kayıtlı ile:</span><span class="sxs-lookup"><span data-stu-id="62112-116">Copy hello GUID in Application ID, go back tooVisual Studio, open `App.xaml.cs` and replace `your_client_id_here` with hello Application ID you just registered:</span></span>

```csharp
private static string ClientId = "your_application_id_here";
```
