---
title: "aaaHow tooconfigure tek oturum açma tooan uygulama proxy'si uygulama | Microsoft Docs"
description: "Çoklu oturum açma tooyour uygulama proxy uygulama hızlı bir şekilde nasıl yapılandırabileceğiniz"
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
ms.openlocfilehash: e1289203177c77b3a8bcc9058c5c0b8ae50f243e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-single-sign-on-tooan-application-proxy-application"></a>Nasıl tooconfigure tek oturum açma tooan uygulama proxy'si uygulama

Çoklu oturum açma (SSO), kullanıcıların tooaccess, bir uygulamanın birden çok kez doğrulanmadan sağlar. Bu Azure Active Directory'de karşı hello bulutta hello tek bir kimlik doğrulaması toooccur ve hello hizmet veya bağlayıcı tooimpersonate hello kullanıcı toocomplete hiçbir ek kimlik doğrulama sınaması hello uygulamasından olanak sağlar.

## <a name="how-tooconfigure-single-sign-on"></a>Nasıl tooconfigure çoklu oturum açma
tooconfigure SSO, önce uygulamanızın Azure Active Directory üzerinden ön kimlik doğrulama için yapılandırıldığından emin olun. toodo Bu, Git çok**Azure Active Directory**  - &gt; **kurumsal uygulamalar**  - &gt; **tüm uygulamaları**  - &gt; Uygulamanız  **- &gt; uygulama proxy'si**. Bu sayfada, gördüğünüz hello "Ön kimlik doğrulaması" alanına ve ayarlanan çok emin olun "Azure Active Directory. 

Merhaba dört adımında hello ön kimlik doğrulama yöntemleri hakkında daha fazla bilgi için bkz: [uygulama yayımlama belge](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).

   ![Azure Portalı'nda ön kimlik doğrulama yöntemi](./media/application-proxy-config-sso-how-to/app-proxy.png)

## <a name="configuring-single-sign-on-modes-for-application-proxy-applications"></a>Çoklu oturum açma modu uygulama proxy'si uygulamalar için yapılandırma
Ardından hello belirli türde çoklu oturum açma özelliğini yapılandırın. Merhaba oturum açma yöntemleri ne tür bir kimlik doğrulama Merhaba arka uç uygulaması kullanan göre sınıflandırılır. Uygulama proxy'si uygulamaları üç tür oturum açma destekler:

-   **Parola tabanlı oturum açma**: parola tabanlı oturum açma kullanılabilir toosign üzerinde kullanıcı adı ve parola alanlarına kullanan herhangi bir uygulama için. Yapılandırma adımları bulunabilir bizim [parola SSO yapılandırma belgelerine](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#bring-your-own-password-sso-applications).

-   **Tümleşik Windows kimlik doğrulaması**: tümleşik Windows kimlik doğrulaması (IWA) kullanan uygulamalar için çoklu oturum açma Kerberos Kısıtlı temsilci (KCD) aracılığıyla etkinleştirilir. Bu Active Directory tooimpersonate kullanıcıları ve toosend uygulama Proxy bağlayıcıları izin verir ve şirket adına belirteçleri alırsınız. KCD yapılandırma hakkında ayrıntılar hello bulunabilir [çoklu oturum açma KCD belgelerine](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd).

-   **Üstbilgi tabanlı oturum açma**: üst bilgisi tabanlı oturum açma ortaklığı etkinleştirilir ve bazı ek yapılandırma gerektirmez. Merhaba hello ortaklığı ve kimlik doğrulaması için üstbilgiler kullanan tek oturum açma tooan uygulamayı yapılandırmak için adım adım yönergeler hakkında daha fazla bilgi için bkz [PingAccess Azure AD belgeleri için](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).

Bu seçeneklerin her biri tooyour uygulamada "Kurumsal uygulamalar" ve açma hello giderek bulunabilir **çoklu oturum açma** hello soldaki menüden sayfasında. Uygulamanızı hello eski Portalı'nda oluşturduysanız, tüm bu seçenekler göremeyebilirsiniz unutmayın.

Bu sayfada, ayrıca bir gördüğünüz ek oturum açma seçeneği: bağlantılı oturum açma. Bu uygulama proxy'si tarafından da desteklenir. Ancak, bu seçenek tek oturum açma toohello uygulama eklemez unutmayın. Bununla Merhaba uygulaması tek Active Directory Federasyon Hizmetleri gibi başka bir hizmet kullanılarak uygulanan oturum zaten sahip olabilir. 

Bu seçenek, bir yönetici toocreate kullanıcılar ilk üzerinde Merhaba uygulaması erişirken güden bağlantı tooan uygulaması sağlar. Örneğin, varsa tooauthenticate kullanıcıların Active Directory Federasyon Hizmetleri 2.0 kullanan bir uygulama yapılandırılmış, bir yönetici'hello erişim paneline seçeneği toocreate "bağlantılı oturum açma" Merhaba bağlantı tooit kullanabilirsiniz.

## <a name="next-steps"></a>Sonraki adımlar
[Uygulama proxy'si ile çoklu oturum açma tooyour uygulamaları sağlayın](active-directory-application-proxy-sso-using-kcd.md)
