---
title: "aaaAzure AD .NET Protokolü'ne genel bakış | Microsoft Docs"
description: "Nasıl toouse HTTP iletileri tooauthorize tooweb uygulamaları ve web API kullanarak Azure AD kiracınızda erişin."
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/21/2016
ms.author: priyamo
ms.openlocfilehash: 5bd54af028c445afd3f35d67d47d7c84b476c757
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## Uygulamanızı AD kiracınıza kaydetme
İlk olarak, Azure Active Directory (Azure AD) Kiracı ile tooregister uygulamanız gerekir. Bu, uygulamanız için bir uygulama kimliği size, aynı zamanda tooreceive belirteçlerini etkinleştir.

* İçinde toohello oturum [Azure Portal](https://portal.azure.com).
* Azure AD kiracınıza hello sağ üst köşesinde hello sayfa hesabınızda tıklayarak seçin.
* Merhaba Sol Gezinti Bölmesi'nde tıklayın **Azure Active Directory**.
* **Uygulama Kayıtları**’na ve **Ekle**’ye tıklayın.
* Merhaba komut istemlerini izleyin ve yeni bir uygulama oluşturun. Bu öğretici için oluşturduğunuz uygulamanın web uygulaması veya yerel uygulama olması önemli değildir, ancak web uygulamaları veya yerel uygulamalar için belirli örnekler görmek istiyorsanız [hızlı başlangıç](../articles/active-directory/develop/active-directory-developers-guide.md) bölümümüze bakabilirsiniz.
  * Web uygulamaları için hello sağlamak **oturum açma URL'si** kullanıcılar, örneğin,'burada oturum açabilir, uygulamanızın hello temel URL olduğu `http://localhost:12345`.
<!--TODO: add once App ID URI is configurable: hello **App ID URI** is a unique identifier for your application. hello convention is toouse `https://<tenant-domain>/<app-name>`, e.g. `https://contoso.onmicrosoft.com/my-first-aad-app`-->
  * Yerel uygulamalar için sağlayan bir **yeniden yönlendirme URI'si**, hangi Azure AD tooreturn belirteci yanıtları kullanır. Bir değer belirli tooyour uygulama girin. Örneğin`http://MyFirstAADApp`
* Kayıt tamamladıktan sonra Azure AD, uygulamanızın benzersiz istemci tanıtıcısına atayın, uygulama kimliği hello Bu değer gerekir hello sonraki bölümlerde, bu nedenle hello uygulama sayfadan kopyalayın.
