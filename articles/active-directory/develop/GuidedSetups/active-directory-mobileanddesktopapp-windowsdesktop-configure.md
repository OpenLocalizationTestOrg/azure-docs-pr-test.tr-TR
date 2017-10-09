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
## <a name="create-an-application-express"></a>(Hızlı) uygulama oluşturma
Merhaba uygulamanızda tooregister gereksinim artık *Microsoft uygulama kayıt portalı*:
1. Merhaba aracılığıyla uygulamanızı kaydetme [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)
2.  Uygulamanız ve e-posta için bir ad girin
3.  Kurulum destekli Hello seçeneğinin işaretli olduğundan emin olun
4.  Merhaba yönergeleri tooobtain hello uygulama kimliği izleyin ve kodunuza yapıştırın

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Uygulama kayıt bilgileri tooyour çözümünüz (Gelişmiş) ekleyin
Merhaba uygulamanızda tooregister gereksinim artık *Microsoft uygulama kayıt portalı*:
1. Toohello Git [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/portal/register-app) tooregister uygulama
2. Uygulamanız ve e-posta için bir ad girin 
3. Destekli kurulumu için Hello seçeneğinin işaretli olduğundan emin olun
4. Tıklatın `Add Platform`seçeneğini belirleyip `Native Application` ve kaydetme ulaştı.
5. Uygulama Kimliği Hello GUID kopyalayın, tooVisual Studio, açık dönün `App.xaml.cs` ve değiştirme `your_client_id_here` hello uygulama kimliği yalnızca kayıtlı ile:

```csharp
private static string ClientId = "your_application_id_here";
```
