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
## <a name="configure-your-aspnet-web-app-with-hello-applications-registration-information"></a>ASP.NET Web uygulamanız hello uygulamanın kayıt bilgileri ile yapılandırma

Bu adımda, proje toouse SSL yapılandırın ve ardından hello SSL URL tooconfigure uygulamanızın kayıt bilgileri kullanın. Bundan sonra hello uygulama Ekle ' kayıt bilgileri tooyour çözüm aracılığıyla *web.config*.

1.  Çözüm Gezgini'nde başlangıç projesi seçip hello arayın `Properties` (bir özellik penceresinde F4 tuşuna basın görmüyorsanız) penceresi
2.  Değişiklik `SSL Enabled` çok`True`
3.  Merhaba değerinden kopyalama `SSL URL` yukarıda hello yapıştırın `Redirect URL` alan bu sayfanın hello üste ve ardından *güncelleştirme*:<br/><br/>![Proje Özellikleri](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
4.  Merhaba aşağıdakileri ekleyin `web.config` bölümünde kökün klasörde bulunan dosya `configuration\appSettings`:

```xml
<add key="ClientId" value="[Enter hello application Id here]" />
<add key="RedirectUri" value="[Enter hello Redirect URL here]" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
