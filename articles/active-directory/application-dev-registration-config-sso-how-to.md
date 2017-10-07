---
title: "Yeni bir çok kiracılı uygulama aaaHow tooconfigure | Microsoft Docs"
description: "Nasıl tooconfigure tek oturum açma için özel bir uygulama geliştirdiğiniz ve Azure AD ile kaydediliyor."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4d3499d8885933516d6597fa9f87bcf88cd5a428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-a-new-multi-tenant-application"></a>Nasıl tooconfigure yeni bir çok kiracılı uygulama

Federasyon çoklu oturum açma (SSO) uygulamanızda etkinleştirme Openıd Connect, SAML 2.0 ve WS-Fed için Azure AD üzerinden federasyonunu olduğunda otomatik olarak etkinleştirilir. Son kullanıcılarınızın toosign zaten Azure AD varolan bir oturumla sahip olmasına rağmen karşılaşıyorsanız, uygulamanızı yanlış olasıdır.

* ADAL/MSAL kullanıyorsanız, olduğundan emin olun **PromptBehavior** çok ayarlamak**otomatik** yerine **her zaman**.

* Bir mobil uygulama oluşturuyorsanız tooenable aracılı veya aracılı olmayan SSO ek yapılandırma gerekebilir.

Android için bkz: [etkinleştirme arası SSO'nun Android içinde](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).<br>

İOS için bkz: [etkinleştirme arası SSO'nun iOS içinde](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).

## <a name="next-steps"></a>Sonraki adımlar

[Azure AD SSO](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)<br>

[Uygulama SSO Android içinde çapraz etkinleştirme](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)<br>

[Etkinleştirme arası SSO'nun iOS içinde](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)<br>

[Uygulamaları tooAzureAD tümleştirme](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)<br>

[İzin ve adının Azuread'i v2.0 için uygulamalar Yakınsanan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[Azuread'i StackOverflow](http://stackoverflow.com/questions/tagged/azure-active-directory)
