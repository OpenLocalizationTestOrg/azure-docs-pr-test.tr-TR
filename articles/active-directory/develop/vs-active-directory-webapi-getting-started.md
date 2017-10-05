---
title: "Visual Studio Webapı projelerinde Azure AD ile çalışmaya başlama | Microsoft Docs"
description: "Azure Active Directory Webapı projelerinde bağlanma veya Visual Studio kullanarak Azure AD oluşturduktan sonra kullanmaya başlamak nasıl bağlı Hizmetleri"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: bf1eb32d-25cd-4abf-8679-2ead299fedaa
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/19/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: a756316054dd3bb63f3b0a9f59621bb1345bc693
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-active-directory-and-visual-studio-connected-services-webapi-projects"></a><span data-ttu-id="7affb-103">Azure Active Directory ve Visual Studio bağlı hizmetler (Webapı projeleri) ile Başlarken</span><span class="sxs-lookup"><span data-stu-id="7affb-103">Get Started with Azure Active Directory and Visual Studio connected services (WebApi projects)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7affb-104">Başlarken</span><span class="sxs-lookup"><span data-stu-id="7affb-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="7affb-105">Ne oldu</span><span class="sxs-lookup"><span data-stu-id="7affb-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="requiring-authentication-to-access-controllers"></a><span data-ttu-id="7affb-106">Erişim denetleyicileri kimlik doğrulaması gerektiren</span><span class="sxs-lookup"><span data-stu-id="7affb-106">Requiring authentication to access controllers</span></span>
<span data-ttu-id="7affb-107">Projenizdeki tüm denetleyicileri ile donatılan **Authorize** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="7affb-107">All controllers in your project were adorned with the **Authorize** attribute.</span></span> <span data-ttu-id="7affb-108">Bu öznitelik kullanıcıya bu denetleyicileri tarafından tanımlanan API'leri erişmeden önce kimlik doğrulaması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7affb-108">This attribute requires the user to be authenticated before accessing the APIs defined by these controllers.</span></span> <span data-ttu-id="7affb-109">Denetleyici anonim erişime izin vermek için bu öznitelik denetleyicisinden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="7affb-109">To allow the controller to be accessed anonymously, remove this attribute from the controller.</span></span> <span data-ttu-id="7affb-110">Daha ayrıntılı bir düzeyde izinleri ayarlamak istiyorsanız, denetleyici sınıfı için uygulama yerine yetkilendirme gerektiren her yöntemi için özniteliğini uygulayın.</span><span class="sxs-lookup"><span data-stu-id="7affb-110">If you want to set the permissions at a more granular level, apply the attribute to each method that requires authorization instead of applying it to the controller class.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7affb-111">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7affb-111">Next steps</span></span>
[<span data-ttu-id="7affb-112">Azure Active Directory hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="7affb-112">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

