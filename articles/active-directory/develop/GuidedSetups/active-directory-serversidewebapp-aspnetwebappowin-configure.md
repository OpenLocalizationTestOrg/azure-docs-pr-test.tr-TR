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
## <a name="create-an-application-express"></a>(Hızlı) uygulama oluşturma
Merhaba uygulamanızda tooregister gereksinim artık *Microsoft uygulama kayıt portalı*:
1. Merhaba aracılığıyla uygulamanızı kaydetme [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)
2.  Uygulamanız ve e-posta için bir ad girin
3.  Kurulum destekli Hello seçeneğinin işaretli olduğundan emin olun
4.  Merhaba yönergeleri tooadd tekrar yönlendirme URL'sini tooyour uygulama izleyin

## <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Uygulama kayıt bilgileri tooyour çözümünüz (Gelişmiş) ekleyin
Merhaba uygulamanızda tooregister gereksinim artık *Microsoft uygulama kayıt portalı*:
1. Toohello Git [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/portal/register-app) tooregister uygulama
2. Uygulamanız ve e-posta için bir ad girin 
3.  Destekli kurulumu için Hello seçeneğinin işaretli olduğundan emin olun
4.  Tıklatın `Add Platform`sonra seçin`Web`
5.  TooVisual Studio geri dönün ve, Çözüm Gezgini'nde başlangıç projesini seçin ve (bir özellik penceresinde F4 tuşuna basın görmüyorsanız) hello özellikleri penceresine bakın
6.  SSL etkin çok değiştirme`True`
7.  Merhaba SSL URL'sini kopyalayın ve bu URL yeniden yönlendirme URL'si toohello listesi hello kayıt Portalı'nın yönlendirme URL'si listesinde ekleyin:<br/><br/>![Proje Özellikleri](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
8.  Merhaba aşağıdakileri ekleyin `web.config` hello bölümünde hello kök klasöründe yer alan `configuration\appSettings`:

```xml
<add key="ClientId" value="Enter_the_Application_Id_here" />
<add key="redirectUri" value="Enter_the_Redirect_URL_here" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
<!-- Workaround for Docs conversion bug -->
<ol start="9">
<li>
Değiştir `ClientId` hello uygulama kimliği yalnızca kayıtlı sahip
</li>
<li>
Değiştir `redirectUri` hello projenizin SSL URL ile
</li>
</ol>
<!-- End Docs -->
