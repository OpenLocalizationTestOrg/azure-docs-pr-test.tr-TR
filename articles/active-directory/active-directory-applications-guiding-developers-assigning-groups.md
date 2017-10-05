---
title: "Azure AD uygulamalarınız için grupları atama | Microsoft Docs"
description: "Grup ataması Azure uygulamaları için gerçekleştirme."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: 29b5ba89-a1c7-4f1f-a294-248a40106617
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
robots: noindex
ms.openlocfilehash: e0b0b87a454db96747f024e81882fe83d62fdbe2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="assign-azure-active-directory-groups-to-an-application"></a><span data-ttu-id="e1015-103">Bir uygulamayı Azure Active Directory grupları atama</span><span class="sxs-lookup"><span data-stu-id="e1015-103">Assign Azure Active Directory groups to an application</span></span>
<span data-ttu-id="e1015-104">Uygulamaya kullanıcılar ve gruplar atamadan önce kullanıcı ataması gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e1015-104">Before you can assign users and groups to an application, you must require user assignment.</span></span> <span data-ttu-id="e1015-105">Kullanıcı Ataması gerektirecek şekilde öğrenmek için bkz: [gerektiren kullanıcı ataması](active-directory-applications-guiding-developers-requiring-user-assignment.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="e1015-105">To learn how to require user assignment, see the [Requiring User Assignment](active-directory-applications-guiding-developers-requiring-user-assignment.md) article.</span></span>

<span data-ttu-id="e1015-106">Bu makale, zaten grupları, bu uygulama için kullandığınız active Directory'deki oluşturduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="e1015-106">This article assumes that you have already created groups in the active directory you are using for this application.</span></span>

## <a name="assigning-groups-to-an-application"></a><span data-ttu-id="e1015-107">Uygulama grupları atama</span><span class="sxs-lookup"><span data-stu-id="e1015-107">Assigning Groups to an Application</span></span>
1. <span data-ttu-id="e1015-108">Azure portalı bir yönetici hesabı ile oturum açın.</span><span class="sxs-lookup"><span data-stu-id="e1015-108">Log in to the Azure portal with an administrator account.</span></span>
2. <span data-ttu-id="e1015-109">Tıklayın **tüm öğeleri** ana menü öğesi.</span><span class="sxs-lookup"><span data-stu-id="e1015-109">Click on the **All Items** item in the main menu.</span></span>
3. <span data-ttu-id="e1015-110">Uygulama için kullanmakta olduğunuz dizini seçin.</span><span class="sxs-lookup"><span data-stu-id="e1015-110">Choose the directory you are using for the application.</span></span>
4. <span data-ttu-id="e1015-111">Tıklayın **uygulamaları** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="e1015-111">Click on the **APPLICATIONS** tab.</span></span>
5. <span data-ttu-id="e1015-112">Uygulama bu dizinle ilişkili uygulamalar listesini seçin.</span><span class="sxs-lookup"><span data-stu-id="e1015-112">Select the application from the list of applications associated with this directory.</span></span>
6. <span data-ttu-id="e1015-113">Tıklatın **kullanıcılar ve GRUPLAR** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="e1015-113">Click the **USERS AND GROUPS** tab.</span></span>
7. <span data-ttu-id="e1015-114">Kullanarak active Directory'de Grup listesini filtrelemek **grupları** açılır liste.</span><span class="sxs-lookup"><span data-stu-id="e1015-114">Filter the list of groups in your active directory by using the **Groups** dropdown list.</span></span>
8. <span data-ttu-id="e1015-115">Grubu seçin.</span><span class="sxs-lookup"><span data-stu-id="e1015-115">Select the group.</span></span>
9. <span data-ttu-id="e1015-116">Tıklatın **ATAMAK**.</span><span class="sxs-lookup"><span data-stu-id="e1015-116">Click **ASSIGN**.</span></span>
10. <span data-ttu-id="e1015-117">Tıklatın **Evet** istendiğinde.</span><span class="sxs-lookup"><span data-stu-id="e1015-117">Click **yes** when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e1015-118">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="e1015-118">Next Steps</span></span>
[!INCLUDE [active-directory-applications-guiding-developers-for-lob-applications-toc.md](../../includes/active-directory-applications-guiding-developers-for-lob-applications-toc.md)]
