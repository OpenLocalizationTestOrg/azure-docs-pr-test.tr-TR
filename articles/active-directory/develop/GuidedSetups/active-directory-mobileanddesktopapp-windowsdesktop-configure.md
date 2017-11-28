---
title: "Azure AD v2 Windows Masaüstü tıklatmalarını başlatıldı - Config | Microsoft Docs"
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
ms.openlocfilehash: 1dfaa7ade664e43dcb9aa788b0197ca17e6ec4cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="eddb7-104">(Hızlı) uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="eddb7-104">Create an application (Express)</span></span>
<span data-ttu-id="eddb7-105">Uygulamanızı kaydetmeniz gerekir artık *Microsoft uygulama kayıt portalı*:</span><span class="sxs-lookup"><span data-stu-id="eddb7-105">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="eddb7-106">Uygulamanızı aracılığıyla kaydetme [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span><span class="sxs-lookup"><span data-stu-id="eddb7-106">Register your application via the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span></span>
2.  <span data-ttu-id="eddb7-107">Uygulamanız ve e-posta için bir ad girin</span><span class="sxs-lookup"><span data-stu-id="eddb7-107">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="eddb7-108">Kurulum destekli seçeneğinin işaretli olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="eddb7-108">Make sure the option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="eddb7-109">Uygulama Kimliğini almak ve kodunuza yapıştırmak için yönergeleri izleyin</span><span class="sxs-lookup"><span data-stu-id="eddb7-109">Follow the instructions to obtain the application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-to-your-solution-advanced"></a><span data-ttu-id="eddb7-110">Uygulama kayıt bilgilerinizi çözümünüze (Gelişmiş) ekleyin</span><span class="sxs-lookup"><span data-stu-id="eddb7-110">Add your application registration information to your solution (Advanced)</span></span>
<span data-ttu-id="eddb7-111">Uygulamanızı kaydetmeniz gerekir artık *Microsoft uygulama kayıt portalı*:</span><span class="sxs-lookup"><span data-stu-id="eddb7-111">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="eddb7-112">Git [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/portal/register-app) bir uygulamayı kaydetmek için</span><span class="sxs-lookup"><span data-stu-id="eddb7-112">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) to register an application</span></span>
2. <span data-ttu-id="eddb7-113">Uygulamanız ve e-posta için bir ad girin</span><span class="sxs-lookup"><span data-stu-id="eddb7-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="eddb7-114">Destekli kurulumu için seçeneğinin işaretli olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="eddb7-114">Make sure the option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="eddb7-115">Tıklatın `Add Platform`seçeneğini belirleyip `Native Application` ve kaydetme ulaştı.</span><span class="sxs-lookup"><span data-stu-id="eddb7-115">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5. <span data-ttu-id="eddb7-116">Uygulama kimliği GUID kopyalayın, Visual Studio, açık dön `App.xaml.cs` ve değiştirme `your_client_id_here` yalnızca kayıtlı uygulama kimliği:</span><span class="sxs-lookup"><span data-stu-id="eddb7-116">Copy the GUID in Application ID, go back to Visual Studio, open `App.xaml.cs` and replace `your_client_id_here` with the Application ID you just registered:</span></span>

```csharp
private static string ClientId = "your_application_id_here";
```
