---
title: "Kullanıcı atama - Azure AD gerektiren | Microsoft Docs"
description: "Kullanıcı Ataması Azure uygulamaları için zorunlu kılma."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: 30b78cba-1e0f-472f-8314-f2250a9b91c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: kgremban
robots: noindex
ms.openlocfilehash: 079b806c041a4a21e9350342867aee581c57bf45
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-and-applications-require-user-assignment"></a><span data-ttu-id="161d6-103">Azure AD ve uygulamalar: kullanıcı ataması gerektirir</span><span class="sxs-lookup"><span data-stu-id="161d6-103">Azure AD and applications: Require user assignment</span></span>
## <a name="requiring-user-assignment"></a><span data-ttu-id="161d6-104">Kullanıcı Ataması gerektirme</span><span class="sxs-lookup"><span data-stu-id="161d6-104">Requiring User Assignment</span></span>
1. <span data-ttu-id="161d6-105">Azure portalı bir yönetici hesabı ile oturum açın.</span><span class="sxs-lookup"><span data-stu-id="161d6-105">Log in to the Azure portal with an administrator account.</span></span>
2. <span data-ttu-id="161d6-106">Tıklayın **tüm öğeleri** ana menü öğesi.</span><span class="sxs-lookup"><span data-stu-id="161d6-106">Click on the **All Items** item in the main menu.</span></span>
3. <span data-ttu-id="161d6-107">Uygulama için kullanmakta olduğunuz dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="161d6-107">Choose the directory you are using for the application.</span></span>
4. <span data-ttu-id="161d6-108">Tıklayın **uygulamaları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="161d6-108">Click on the **APPLICATIONS** tab.</span></span>
5. <span data-ttu-id="161d6-109">Uygulama bu dizinle ilişkili uygulamalar listesini seçin.</span><span class="sxs-lookup"><span data-stu-id="161d6-109">Select the application from the list of applications associated with this directory.</span></span>
6. <span data-ttu-id="161d6-110">Tıklatın **yapılandırma** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="161d6-110">Click the **CONFIGURE** tab.</span></span>
7. <span data-ttu-id="161d6-111">Değişiklik **atama kullanıcı gerekli erişim App** Evet Değiştir.</span><span class="sxs-lookup"><span data-stu-id="161d6-111">Change the **User Assignment Required to Access App** toggle to Yes.</span></span>
8. <span data-ttu-id="161d6-112">Tıklatın **kaydetmek** ekranın altındaki düğmesini.</span><span class="sxs-lookup"><span data-stu-id="161d6-112">Click the **Save** button at the bottom of the screen.</span></span>

<span data-ttu-id="161d6-113">Şimdi, kullanıcılara ve/veya grupları uygulamaya atamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="161d6-113">You will now have to assign users and/or groups to the application.</span></span> <span data-ttu-id="161d6-114">Bkz: [kullanıcılar için uygulama atama](active-directory-applications-guiding-developers-assigning-users.md) ve [için uygulama grupları atama](active-directory-applications-guiding-developers-assigning-groups.md).</span><span class="sxs-lookup"><span data-stu-id="161d6-114">See [Assigning users to an application](active-directory-applications-guiding-developers-assigning-users.md) and [Assigning groups to an application](active-directory-applications-guiding-developers-assigning-groups.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="161d6-115">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="161d6-115">Next Steps</span></span>
[!INCLUDE [active-directory-applications-guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]
