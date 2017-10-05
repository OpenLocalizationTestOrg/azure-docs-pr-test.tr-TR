---
title: "Belirli bir API izinlerini seçme | Microsoft Docs"
description: "Kimlik doğrulama uç noktaları geliştirme veya Azure AD ile kaydetme özel bir uygulamayı bulmak nasıl."
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
ms.openlocfilehash: 6966cf145375bf3d830d476564c428502ae40fd4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-select-permissions-for-a-given-api"></a><span data-ttu-id="13249-103">Belirli bir API izinlerini seçme</span><span class="sxs-lookup"><span data-stu-id="13249-103">How to select permissions for a given API</span></span>

<span data-ttu-id="13249-104">Uygulamanıza kimlik doğrulaması uç noktaları bulabilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="13249-104">You can find the authentication endpoints for your application in the [Azure portal](https://portal.azure.com).</span></span>

-   <span data-ttu-id="13249-105">[Azure portalına](https://portal.azure.com) gidin.</span><span class="sxs-lookup"><span data-stu-id="13249-105">Navigate to the [Azure portal](https://portal.azure.com).</span></span>

-   <span data-ttu-id="13249-106">Sol gezinti bölmesinden tıklatın **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="13249-106">From the left navigation pane, click **Azure Active Directory**.</span></span>

-   <span data-ttu-id="13249-107">Tıklatın **uygulama kayıtlar** ve **uç noktaları**.</span><span class="sxs-lookup"><span data-stu-id="13249-107">Click **App Registrations** and choose **Endpoints**.</span></span>

-   <span data-ttu-id="13249-108">Bu açık **uç noktaları** kiracınız için tüm kimlik doğrulama uç noktaları listesi sayfası.</span><span class="sxs-lookup"><span data-stu-id="13249-108">This open up the **Endpoints** page, which list all the authentication endpoints for your tenant.</span></span>

-   <span data-ttu-id="13249-109">Kimlik doğrulaması hazırlanması uygulama kimliği ile birlikte, uygulamaya özgü isteği, kullanmakta olduğunuz kimlik doğrulama protokolü belirli uç nokta kullanın.</span><span class="sxs-lookup"><span data-stu-id="13249-109">Use the endpoint specific to the authentication protocol you are using, in conjunction with the application ID to craft the authentication request specific to your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13249-110">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="13249-110">Next steps</span></span>
[<span data-ttu-id="13249-111">Azure Active Directory geliştirici kılavuzu</span><span class="sxs-lookup"><span data-stu-id="13249-111">Azure Active Directory developer's guide</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-developers-guide#authentication-and-authorization-protocols)
