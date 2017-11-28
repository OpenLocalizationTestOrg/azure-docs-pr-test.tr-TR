---
title: "Bir kuruluş uygulama Azure Active Directory'de bir kullanıcı veya grup atamak | Microsoft Docs"
description: "Bir kullanıcı veya grup için Azure Active Directory'de atamak için bir kuruluş uygulama seçme"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5817ad48-d916-492b-a8d0-2ade8c50a224
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: ee784704ada9238b5cd048f99aaa4cb192ec7d57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="assign-a-user-or-group-to-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="26afd-103">Bir kuruluş uygulama Azure Active Directory'de bir kullanıcı veya grup atayın</span><span class="sxs-lookup"><span data-stu-id="26afd-103">Assign a user or group to an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="26afd-104">Kurumsal uygulamalarınızda Azure Active Directory (Azure AD) bir kullanıcıya veya gruba atamak kolaydır.</span><span class="sxs-lookup"><span data-stu-id="26afd-104">It's easy to assign a user or a group to your enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="26afd-105">Kuruluş uygulama yönetmek için uygun izinlere sahip olmalıdır ve dizin için genel yönetici olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="26afd-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

## <a name="how-do-i-assign-user-access-to-an-enterprise-app"></a><span data-ttu-id="26afd-106">Bir kurumsal uygulama için nasıl kullanıcı erişimi atamak?</span><span class="sxs-lookup"><span data-stu-id="26afd-106">How do I assign user access to an enterprise app?</span></span>
1. <span data-ttu-id="26afd-107">Oturum [Azure portal](https://portal.azure.com) dizini için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="26afd-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="26afd-108">Seçin **daha fazla hizmet**, Azure Active Directory metin kutusuna girin ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="26afd-108">Select **More services**, enter Azure Active Directory in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="26afd-109">Üzerinde **Azure Active Directory - *directoryname***  (diğer bir deyişle, Azure AD dikey yönettiğiniz dizin için), dikey penceresinde seçin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="26afd-109">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Açılış Kurumsal uygulamaları](./media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="26afd-111">Üzerinde **kurumsal uygulamalar** dikey penceresinde, select **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="26afd-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="26afd-112">Yönetebileceğiniz uygulamaların bir listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="26afd-112">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="26afd-113">Üzerinde **kurumsal uygulamalar - tüm uygulamaları** dikey penceresinde, bir uygulama seçin.</span><span class="sxs-lookup"><span data-stu-id="26afd-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="26afd-114">Üzerinde ***appname*** dikey penceresinde (diğer bir deyişle, dikey penceresinde seçili uygulamasının başlık adı ile) seçin **kullanıcıları ve grupları**.</span><span class="sxs-lookup"><span data-stu-id="26afd-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Users & Groups**.</span></span>

    ![Tüm uygulamalar komutu seçme](./media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. <span data-ttu-id="26afd-116">Üzerinde ***appname*** **-kullanıcı ve grup atama** dikey penceresinde, select **Ekle** komutu.</span><span class="sxs-lookup"><span data-stu-id="26afd-116">On the ***appname*** **- User & Group Assignment** blade, select the **Add** command.</span></span>
8. <span data-ttu-id="26afd-117">Üzerinde **eklemek atama** dikey penceresinde, select **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="26afd-117">On the **Add Assignment** blade, select **Users and groups**.</span></span>

    ![Bir kullanıcı veya grup için uygulama atama](./media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. <span data-ttu-id="26afd-119">Üzerinde **kullanıcılar ve gruplar** dikey penceresinde, listeden bir veya daha fazla kullanıcı veya grup seçin ve ardından **seçin** dikey pencerenin altındaki düğmesini.</span><span class="sxs-lookup"><span data-stu-id="26afd-119">On the **Users and groups** blade, select one or more users or groups from the list and then select the **Select** button at the bottom of the blade.</span></span>
10. <span data-ttu-id="26afd-120">Üzerinde **eklemek atama** dikey penceresinde, select **rol**.</span><span class="sxs-lookup"><span data-stu-id="26afd-120">On the **Add Assignment** blade, select **Role**.</span></span> <span data-ttu-id="26afd-121">Ardından **rolü Seç** dikey penceresinde, seçilen kullanıcılarla veya gruplarla uygulayın ve ardından için rolü seçin **Tamam** dikey pencerenin altındaki düğmesini.</span><span class="sxs-lookup"><span data-stu-id="26afd-121">Then, on the **Select Role** blade, select a role to apply to the selected users or groups, and then select the **OK** button at the bottom of the blade.</span></span>
11. <span data-ttu-id="26afd-122">Üzerinde **eklemek atama** dikey penceresinde, select **atamak** dikey pencerenin altındaki düğmesini.</span><span class="sxs-lookup"><span data-stu-id="26afd-122">On the **Add Assignment** blade, select the **Assign** button at the bottom of the blade.</span></span> <span data-ttu-id="26afd-123">Atanan kullanıcılar veya gruplar bu kurumsal uygulama için seçili rol tarafından tanımlanan izinlerine sahip olacaktır.</span><span class="sxs-lookup"><span data-stu-id="26afd-123">The assigned users or groups will have the permissions defined by the selected role for this enterprise app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26afd-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="26afd-124">Next steps</span></span>
* [<span data-ttu-id="26afd-125">Tüm my gruplarının bakın</span><span class="sxs-lookup"><span data-stu-id="26afd-125">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="26afd-126">Bir kullanıcı veya grup ataması Kurumsal uygulamadan Kaldır</span><span class="sxs-lookup"><span data-stu-id="26afd-126">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="26afd-127">Kullanıcı oturum açma işlemleri bir kurumsal uygulama için devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="26afd-127">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="26afd-128">Adını veya bir kuruluş uygulama logosunu değiştirme</span><span class="sxs-lookup"><span data-stu-id="26afd-128">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
