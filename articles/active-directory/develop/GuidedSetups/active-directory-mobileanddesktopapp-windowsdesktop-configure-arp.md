---
title: "aaaAzure AD v2 Windows Masaüstü Getting Started - Config | Microsoft Docs"
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
ms.openlocfilehash: d96d9eded200824a6f7ee234009dd0bb11b18b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a><span data-ttu-id="0189d-103">Merhaba uygulamanın kayıt bilgileri tooyour uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="0189d-103">Add hello application’s registration information tooyour app</span></span>
<span data-ttu-id="0189d-104">Bu adımda, tooadd hello uygulama kimliği tooyour proje gerekir.</span><span class="sxs-lookup"><span data-stu-id="0189d-104">In this step, you need tooadd hello Application Id tooyour project.</span></span>

1.  <span data-ttu-id="0189d-105">Açık `App.xaml.cs` ve hello içeren hello satırı değiştirin `ClientId` ile:</span><span class="sxs-lookup"><span data-stu-id="0189d-105">Open `App.xaml.cs` and replace hello line containing hello `ClientId` with:</span></span>

```csharp
private static string ClientId = "[Enter hello application Id here]";
```

### <a name="what-is-next"></a><span data-ttu-id="0189d-106">Sonraki nedir</span><span class="sxs-lookup"><span data-stu-id="0189d-106">What is Next</span></span>

[<span data-ttu-id="0189d-107">Test ve doğrulama</span><span class="sxs-lookup"><span data-stu-id="0189d-107">Test and Validate</span></span>](active-directory-mobileanddesktopapp-windowsdesktop-test.md)
