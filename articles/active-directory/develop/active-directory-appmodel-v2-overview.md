---
title: "aaaAzure Active Directory v2.0 uç | Microsoft Docs"
description: "Bir giriş toobuilding uygulamalarla Microsoft Account ve Azure Active Directory oturum açma."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 2dee579f-fdf6-474b-bc2c-016c931eaa27
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ae5946b02c50ae5a6137dc1decae66c96647e875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-microsoft-account--azure-ad-users-in-a-single-app"></a>Oturum açma Microsoft Account & Azure AD kullanıcıların tek bir uygulamada
Merhaba geçmiş, hem kişisel Microsoft hesaplarını toosupport isteyen bir uygulama geliştiricisi olarak ve Azure Active Directory iş hesaplarından iki ayrı sistemleriyle gerekli toointegrate.  Merhaba **Azure AD v2.0 uç** her iki türdeki bir basit tümleştirmesi kullanılarak hesaba toosign sağlayan yeni bir kimlik doğrulaması API Sürüm tanıtır.  Merhaba v2.0 uç noktası kullanan uygulamalar hello REST API'lerini de tüketebileceği [Microsoft Graph](https://graph.microsoft.io) ya da türde bir hesabı kullanarak.

## <a name="getting-started"></a>Başlarken
En sevdiğiniz platformu listesi toobuild aşağıdaki hello bizim açık kaynak kitaplıkları ve çerçevelerini kullanarak bir uygulama seçin.  Alternatif olarak, bizim OAuth 2.0 & Openıd Connect Protokolü belgeleri toosend kullanmak & protokol iletilerini doğrudan bir kimlik doğrulama kitaplığı kullanmadan alırsınız.

<br />

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

## <a name="whats-new"></a>Yenilikler
Buraya Hello bilgileri nedir ve ne hello v2.0 uç noktası ile mümkün olmayan anlamak yararlı olacaktır.

* Merhaba hakkında bilgi edinin [yapı hello v2.0 uç noktası ile uygulama türleri](active-directory-v2-flows.md).
* Merhaba anlamak [sınırlamalar, sınırlamaları ve kısıtlamaları](active-directory-v2-limitations.md) hello v2.0 uç noktası ile.
* Bu genel bakış videosu hello v2.0 uç noktası için gözden geçirin:

>[!VIDEO https://channel9.msdn.com/Events/Build/2017/P4031/player]

## <a name="reference"></a>Başvuru
Bu bağlantılar hello platform derinlemesine keşfetmek için kullanışlıdır:

* [v2.0 protokol başvurusu](active-directory-v2-protocols.md)
* [v2.0 belirteç başvurusu](active-directory-v2-tokens.md)
* [v2.0 Kitaplığı Başvurusu](active-directory-v2-libraries.md)
* [Kapsamlar ve hello v2.0 uç onayı](active-directory-v2-scopes.md)
* [Merhaba Microsoft Graph](https://graph.microsoft.io)

## <a name="help--support"></a>Yardım ve Destek
Azure Active Directory üzerinde geliştirme hello en iyi yerler tooget Yardım bunlar.

* [Stack Overflow’da `azure-active-directory` ve `adal` etiketleri](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)
* [Azure Active Directory geri bildirimleri](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)


> [!NOTE]
> Yalnızca iş ve Okul hesapları Azure Active Directory'den toosign gereksiniminiz varsa, ile başlamalı bizim [Azure AD Geliştirici Kılavuzu](active-directory-developers-guide.md).  Merhaba v2.0 uç toosign Microsoft Kişisel hesaplarında açıkça isteyen geliştiriciler tarafından kullanılmaya yöneliktir.

