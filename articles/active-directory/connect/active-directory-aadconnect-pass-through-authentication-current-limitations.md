---
title: "Azure AD Connect: Doğrudan kimlik doğrulama - geçerli sınırlamalar | Microsoft Docs"
description: "Bu makalede, Azure Active Directory (Azure AD) doğrudan kimlik doğrulama hello geçerli sınırlamalar açıklanır."
services: active-directory
keywords: "Azure AD Connect doğrudan kimlik doğrulama, Active Directory yükleyin gerekli bileşenleri Azure AD, SSO, çoklu oturum açma"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: billmath
ms.openlocfilehash: 2933745d071aae205c44659e6ea92697f390effb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a>Azure Active Directory doğrudan kimlik doğrulaması: Geçerli sınırlamalar

>[!IMPORTANT]
>Azure AD doğrudan kimlik doğrulama şu anda önizlemede değil. Boş bir özelliktir ve Azure AD toouse Ücretli tüm sürümleri olması gerekmez. Doğrudan kimlik doğrulama kullanılabilir yalnızca Merhaba Dünya çapında örneğinde Azure ad ve değil [Microsoft Cloud Almanya](http://www.microsoft.de/cloud-deutschland) ve [Microsoft Azure kamu bulut](https://azure.microsoft.com/features/gov/).

## <a name="supported-scenarios"></a>Desteklenen senaryolar

Merhaba senaryoları aşağıdaki Önizleme sırasında tam olarak desteklenir:

- Tüm web uygulamalarına tarayıcı tabanlı kullanıcı oturum açma işlemleri.
- Kullanıcı oturum açma işlemleri destekleyen Office 365 istemci uygulamalara [modern kimlik doğrulaması](https://aka.ms/modernauthga).
- Windows 10 cihazlar için Azure AD katılım.
- Exchange ActiveSync desteği.

## <a name="unsupported-scenarios"></a>Desteklenmeyen senaryolar

Merhaba aşağıdaki senaryolar verilmiştir _değil_ Önizleme sırasında desteklenir:

- Kullanıcı oturum açma işlemlerine eski Office istemci uygulamalarına (Office 2013 veya önceki). Kuruluşlar kullanmaları tooswitch toomodern kimlik doğrulaması, mümkünse şunlardır. Modern kimlik doğrulama için doğrudan kimlik doğrulama desteği sağlar ancak da yardımcı olur, güvenli kullanıcı hesapları kullanarak [koşullu erişim](../active-directory-conditional-access.md) çok faktörlü kimlik doğrulama (MFA) gibi özellikleri.
- Kullanıcı oturum açmalarına Skype içine iş 2016 Skype dahil olmak üzere iş istemci uygulamaları için.
- Kullanıcı oturum açma işlemlerine PowerShell v1.0 içine. Bunun yerine PowerShell v2.0 kullanmanız önerilir.

>[!IMPORTANT]
>Desteklenmeyen senaryolar için çözüm olarak, üzerinde hello parola karma eşitlemesini etkinleştirmek [isteğe bağlı özellikler](active-directory-aadconnect-get-started-custom.md#optional-features) hello Azure AD Connect Sihirbazı sayfasında. Bir geri dönüş senaryoları önceki hello için parola karma eşitlemesi görür _yalnızca_ (ve _değil_ bir genel geri dönüş tooPass aracılığıyla kimlik doğrulaması olarak). Bu senaryolar gerekmiyorsa, parola karması eşitlemesi devre dışı bırakın.

## <a name="next-steps"></a>Sonraki adımlar
- [**Hızlı Başlangıç** ](active-directory-aadconnect-pass-through-authentication-quick-start.md) - hale getirmek ve Azure AD doğrudan kimlik doğrulama çalıştıran.
- [**Teknik derinlemesine** ](active-directory-aadconnect-pass-through-authentication-how-it-works.md) -bu özellik nasıl çalıştığını anlayın.
- [**Sık sorulan sorular** ](active-directory-aadconnect-pass-through-authentication-faq.md) -toofrequently sorular yanıtlanmaktadır.
- [**Sorun giderme** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -tooresolve ortak hello özelliğiyle nasıl sorunları öğrenin.
- [**Azure AD sorunsuz SSO** ](active-directory-aadconnect-sso.md) -tamamlayıcı bu özellik hakkında daha fazla bilgi edinin.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - yeni özellik istekleri dosyalama için.
