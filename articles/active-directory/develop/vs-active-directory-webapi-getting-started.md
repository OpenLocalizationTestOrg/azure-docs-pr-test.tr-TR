---
title: "Visual Studio Webapı projelerinde Azure AD ile başlatıldı aaaGet | Microsoft Docs"
description: "Visual Studio kullanarak Azure AD oluşturma tooor bağlandıktan sonra Webapı projelerinde Azure Active Directory'yi kullanarak tooget nasıl başlatılacağını bağlı Hizmetleri"
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
ms.openlocfilehash: 21413a71a2fd61f31268bf6d5e4d86b8be5bd16a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-and-visual-studio-connected-services-webapi-projects"></a><span data-ttu-id="58e88-103">Azure Active Directory ve Visual Studio bağlı hizmetler (Webapı projeleri) ile Başlarken</span><span class="sxs-lookup"><span data-stu-id="58e88-103">Get Started with Azure Active Directory and Visual Studio connected services (WebApi projects)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="58e88-104">Başlarken</span><span class="sxs-lookup"><span data-stu-id="58e88-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="58e88-105">Ne oldu</span><span class="sxs-lookup"><span data-stu-id="58e88-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="requiring-authentication-tooaccess-controllers"></a><span data-ttu-id="58e88-106">Gerektiren kimlik doğrulaması tooaccess denetleyicileri</span><span class="sxs-lookup"><span data-stu-id="58e88-106">Requiring authentication tooaccess controllers</span></span>
<span data-ttu-id="58e88-107">Projenizdeki tüm denetleyicileri ile Merhaba donatılan **Authorize** özniteliği.</span><span class="sxs-lookup"><span data-stu-id="58e88-107">All controllers in your project were adorned with hello **Authorize** attribute.</span></span> <span data-ttu-id="58e88-108">Bu öznitelik hello kullanıcı toobe hello API'leri erişme bu denetleyicileri tarafından tanımlanan önce kimlik doğrulaması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="58e88-108">This attribute requires hello user toobe authenticated before accessing hello APIs defined by these controllers.</span></span> <span data-ttu-id="58e88-109">anonim olarak, erişilen tooallow hello denetleyicisi toobe bu öznitelik hello denetleyicisinden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="58e88-109">tooallow hello controller toobe accessed anonymously, remove this attribute from hello controller.</span></span> <span data-ttu-id="58e88-110">Daha ayrıntılı bir düzeyde tooset hello izinleri istiyorsanız toohello denetleyici sınıfı uygulamak yerine yetkilendirme gerektiren hello özniteliği tooeach yöntemi uygulayın.</span><span class="sxs-lookup"><span data-stu-id="58e88-110">If you want tooset hello permissions at a more granular level, apply hello attribute tooeach method that requires authorization instead of applying it toohello controller class.</span></span>

## <a name="next-steps"></a><span data-ttu-id="58e88-111">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="58e88-111">Next steps</span></span>
[<span data-ttu-id="58e88-112">Azure Active Directory hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="58e88-112">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

