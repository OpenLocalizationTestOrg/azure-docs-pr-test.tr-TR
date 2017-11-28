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
ms.openlocfilehash: badc47e131290a56a507592f944a0fc7093260a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="configure-your-aspnet-web-app-with-hello-applications-registration-information"></a><span data-ttu-id="8f26b-103">ASP.NET Web uygulamanız hello uygulamanın kayıt bilgileri ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="8f26b-103">Configure your ASP.NET Web App with hello application's registration information</span></span>

<span data-ttu-id="8f26b-104">Bu adımda, proje toouse SSL yapılandırın ve ardından hello SSL URL tooconfigure uygulamanızın kayıt bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="8f26b-104">In this step, you will configure your project toouse SSL, and then use hello SSL URL tooconfigure your application’s registration information.</span></span> <span data-ttu-id="8f26b-105">Bundan sonra hello uygulama Ekle ' kayıt bilgileri tooyour çözüm aracılığıyla *web.config*.</span><span class="sxs-lookup"><span data-stu-id="8f26b-105">After this, add hello application’ registration information tooyour solution via *web.config*.</span></span>

1.  <span data-ttu-id="8f26b-106">Çözüm Gezgini'nde başlangıç projesi seçip hello arayın `Properties` (bir özellik penceresinde F4 tuşuna basın görmüyorsanız) penceresi</span><span class="sxs-lookup"><span data-stu-id="8f26b-106">In Solution Explorer, select hello project and look at hello `Properties` window (if you don’t see a Properties window, press F4)</span></span>
2.  <span data-ttu-id="8f26b-107">Değişiklik `SSL Enabled` çok`True`</span><span class="sxs-lookup"><span data-stu-id="8f26b-107">Change `SSL Enabled` too`True`</span></span>
3.  <span data-ttu-id="8f26b-108">Merhaba değerinden kopyalama `SSL URL` yukarıda hello yapıştırın `Redirect URL` alan bu sayfanın hello üste ve ardından *güncelleştirme*:</span><span class="sxs-lookup"><span data-stu-id="8f26b-108">Copy hello value from `SSL URL` above and paste it in hello `Redirect URL` field on hello top of this page, then click *Update*:</span></span><br/><br/><span data-ttu-id="8f26b-109">![Proje Özellikleri](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)</span><span class="sxs-lookup"><span data-stu-id="8f26b-109">![Project properties](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)</span></span><br />
4.  <span data-ttu-id="8f26b-110">Merhaba aşağıdakileri ekleyin `web.config` bölümünde kökün klasörde bulunan dosya `configuration\appSettings`:</span><span class="sxs-lookup"><span data-stu-id="8f26b-110">Add hello following in `web.config` file located in root’s folder, under section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="[Enter hello application Id here]" />
<add key="RedirectUri" value="[Enter hello Redirect URL here]" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
