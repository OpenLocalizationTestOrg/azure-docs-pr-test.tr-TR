---
title: "Azure AD v2 Windows Masaüstü tıklatmalarını başlatıldı - Config | Microsoft Docs"
description: "Nasıl bir Windows Masaüstü .NET (XAML) uygulama erişim belirteci almak ve Azure Active Directory v2 bitiş noktası tarafından korunan bir API çağrısı."
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
ms.openlocfilehash: 5e83171846517496e221f0a84565cdf7b77514df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
## <a name="add-the-applications-registration-information-to-your-app"></a><span data-ttu-id="480c7-103">Uygulamanın kayıt bilgileri ekleme</span><span class="sxs-lookup"><span data-stu-id="480c7-103">Add the application’s registration information to your app</span></span>
<span data-ttu-id="480c7-104">Bu adımda, projenize uygulama kimliği eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="480c7-104">In this step, you need to add the Application Id to your project.</span></span>

1.  <span data-ttu-id="480c7-105">Açık `App.xaml.cs` ve satırını içeren Değiştir `ClientId` ile:</span><span class="sxs-lookup"><span data-stu-id="480c7-105">Open `App.xaml.cs` and replace the line containing the `ClientId` with:</span></span>

```csharp
private static string ClientId = "[Enter the application Id here]";
```

### <a name="what-is-next"></a><span data-ttu-id="480c7-106">Sonraki nedir</span><span class="sxs-lookup"><span data-stu-id="480c7-106">What is Next</span></span>

[<span data-ttu-id="480c7-107">Test ve doğrulama</span><span class="sxs-lookup"><span data-stu-id="480c7-107">Test and Validate</span></span>](active-directory-mobileanddesktopapp-windowsdesktop-test.md)
