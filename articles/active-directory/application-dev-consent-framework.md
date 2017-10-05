---
title: "Uygulama onayı nasıl çalışır | Microsoft Docs"
description: "Azure AD onay framework nasıl, üzerinde Azure AD uygulamaları geliştirirken, kullanabileceğiniz görmek için nasıl çalıştığı hakkında daha fazla bilgi edinin"
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
ms.openlocfilehash: 5abddf3a8698e3eb39f118f54eeac62ce68fed39
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="how-application-consent-works"></a><span data-ttu-id="027e9-103">Uygulama onayı works nasıl</span><span class="sxs-lookup"><span data-stu-id="027e9-103">How application consent works</span></span>

<span data-ttu-id="027e9-104">Bu makalede daha etkili bir şekilde uygulamaları geliştirmek için Azure AD onay framework işleyişi hakkında daha fazla öğrenmenize yardımcı olmaktır.</span><span class="sxs-lookup"><span data-stu-id="027e9-104">This article is to help you learn more about how the Azure AD consent framework works so you can develop applications more effectively.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="027e9-105">Önerilen belgeler</span><span class="sxs-lookup"><span data-stu-id="027e9-105">Recommended documents</span></span>

- <span data-ttu-id="027e9-106">Genel düzeyde anlayın [nasıl kaynaklarına uygulamanın erişimi yönetmek bir kaynak sahibi izin verir](https://docs.microsoft.com/azure/active-directory/develop/active-directory-dev-glossary#consent).</span><span class="sxs-lookup"><span data-stu-id="027e9-106">Get a general understanding of [how consent allows a resource owner to govern an application's access to resources](https://docs.microsoft.com/azure/active-directory/develop/active-directory-dev-glossary#consent).</span></span>
- <span data-ttu-id="027e9-107">Adım adım bir bakış elde [nasıl izin Azure AD onay çerçeveyi uygulayan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#overview-of-the-consent-framework).</span><span class="sxs-lookup"><span data-stu-id="027e9-107">Get a step-by-step overview of [how the Azure AD consent framework implements consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#overview-of-the-consent-framework).</span></span>
- <span data-ttu-id="027e9-108">Daha fazla derinliği için bilgi [çok kiracılı uygulama onay framework nasıl kullanabileceğinizi](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) Gelişmiş çok katmanlı uygulama düzenleri "kullanıcı" ve "Yönetici" onay, daha fazla destek uygulamak için.</span><span class="sxs-lookup"><span data-stu-id="027e9-108">For more depth, learn [how a multi-tenant application can use the consent framework](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to implement "user" and "admin" consent, supporting more advanced multi-tier application patterns.</span></span>
- <span data-ttu-id="027e9-109">Daha fazla derinliği için bilgi [izin yetkilendirme kodu verme akışı sırasında OAuth 2.0 protokolü katmanında nasıl desteklenir.](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code#request-an-authorization-code)</span><span class="sxs-lookup"><span data-stu-id="027e9-109">For more depth, learn [how consent is supported at the OAuth 2.0 protocol layer during the authorization code grant flow.](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code#request-an-authorization-code)</span></span>

## <a name="next-steps"></a><span data-ttu-id="027e9-110">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="027e9-110">Next steps</span></span>
[<span data-ttu-id="027e9-111">Azuread'i StackOverflow</span><span class="sxs-lookup"><span data-stu-id="027e9-111">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
