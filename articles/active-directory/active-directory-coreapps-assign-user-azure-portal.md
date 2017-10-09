---
title: "Azure Active Directory'de bir kullanıcı veya grup tooan kuruluş uygulama aaaAssign | Microsoft Docs"
description: "Nasıl tooselect Kurumsal uygulama tooassign Azure Active Directory'de bir kullanıcı veya grup tooit"
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
ms.openlocfilehash: 86c11f19892b9c947a5331677c17759178ed2806
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-user-or-group-tooan-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="e6563-103">Azure Active Directory'de bir kullanıcı veya grup tooan kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="e6563-103">Assign a user or group tooan enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="e6563-104">Kolay tooassign bir kullanıcı veya grup tooyour kurumsal uygulamalar Azure Active Directory'de (Azure AD) değil.</span><span class="sxs-lookup"><span data-stu-id="e6563-104">It's easy tooassign a user or a group tooyour enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="e6563-105">Merhaba uygun izinleri toomanage hello kuruluş uygulama olmalıdır ve başlangıç dizini için genel yönetici olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e6563-105">You must have hello appropriate permissions toomanage hello enterprise app, and you must be global admin for hello directory.</span></span>

## <a name="how-do-i-assign-user-access-tooan-enterprise-app"></a><span data-ttu-id="e6563-106">Kullanıcı erişim tooan kuruluş uygulama nasıl atayabilirim?</span><span class="sxs-lookup"><span data-stu-id="e6563-106">How do I assign user access tooan enterprise app?</span></span>
1. <span data-ttu-id="e6563-107">İçinde toohello oturum [Azure portal](https://portal.azure.com) hello dizin için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="e6563-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="e6563-108">Seçin **daha fazla hizmet**, Azure Active Directory hello metin kutusuna girin ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="e6563-108">Select **More services**, enter Azure Active Directory in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="e6563-109">Merhaba üzerinde **Azure Active Directory - *directoryname***  dikey penceresinde (diğer bir deyişle, hello Azure AD dikey penceresinde hello dizin yönettiğiniz için) seçin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="e6563-109">On hello **Azure Active Directory - *directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![Açılış Kurumsal uygulamaları](./media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="e6563-111">Merhaba üzerinde **kurumsal uygulamalar** dikey penceresinde, select **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="e6563-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="e6563-112">Yönetebileceğiniz hello uygulamaların bir listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="e6563-112">You'll see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="e6563-113">Merhaba üzerinde **kurumsal uygulamalar - tüm uygulamaları** dikey penceresinde, bir uygulama seçin.</span><span class="sxs-lookup"><span data-stu-id="e6563-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="e6563-114">Merhaba üzerinde ***appname*** dikey penceresinde (diğer bir deyişle, hello dikey penceresinde hello adıyla hello başlığında hello seçilen uygulama) seçin **kullanıcıları ve grupları**.</span><span class="sxs-lookup"><span data-stu-id="e6563-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Users & Groups**.</span></span>

    ![Merhaba tüm uygulamaları komutu seçme](./media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. <span data-ttu-id="e6563-116">Merhaba üzerinde ***appname*** **-kullanıcı ve grup atama** dikey penceresinde, select hello **Ekle** komutu.</span><span class="sxs-lookup"><span data-stu-id="e6563-116">On hello ***appname*** **- User & Group Assignment** blade, select hello **Add** command.</span></span>
8. <span data-ttu-id="e6563-117">Merhaba üzerinde **eklemek atama** dikey penceresinde, select **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="e6563-117">On hello **Add Assignment** blade, select **Users and groups**.</span></span>

    ![Bir kullanıcı veya grup toohello uygulama atama](./media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. <span data-ttu-id="e6563-119">Merhaba üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select bir veya daha fazla bölümünden kullanıcıları veya grupları hello listelemek ve hello seçin **seçin** hello dikey penceresinde hello sonundaki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e6563-119">On hello **Users and groups** blade, select one or more users or groups from hello list and then select hello **Select** button at hello bottom of hello blade.</span></span>
10. <span data-ttu-id="e6563-120">Merhaba üzerinde **eklemek atama** dikey penceresinde, select **rol**.</span><span class="sxs-lookup"><span data-stu-id="e6563-120">On hello **Add Assignment** blade, select **Role**.</span></span> <span data-ttu-id="e6563-121">Ardından hello üzerinde **rolü Seç** dikey penceresinde, bir rol tooapply toohello Seçili kullanıcıları veya grupları ve ardından select hello **Tamam** hello dikey penceresinde hello sonundaki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e6563-121">Then, on hello **Select Role** blade, select a role tooapply toohello selected users or groups, and then select hello **OK** button at hello bottom of hello blade.</span></span>
11. <span data-ttu-id="e6563-122">Merhaba üzerinde **eklemek atama** dikey penceresinde, select hello **atamak** hello dikey penceresinde hello sonundaki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e6563-122">On hello **Add Assignment** blade, select hello **Assign** button at hello bottom of hello blade.</span></span> <span data-ttu-id="e6563-123">Kullanıcıların Hello atanan veya grupları hello seçilen rol için bu kuruluş uygulama tarafından tanımlanan hello izinlerine sahip olacaktır.</span><span class="sxs-lookup"><span data-stu-id="e6563-123">hello assigned users or groups will have hello permissions defined by hello selected role for this enterprise app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6563-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e6563-124">Next steps</span></span>
* [<span data-ttu-id="e6563-125">Tüm my gruplarının bakın</span><span class="sxs-lookup"><span data-stu-id="e6563-125">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="e6563-126">Bir kullanıcı veya grup ataması Kurumsal uygulamadan Kaldır</span><span class="sxs-lookup"><span data-stu-id="e6563-126">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="e6563-127">Kullanıcı oturum açma işlemleri bir kurumsal uygulama için devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="e6563-127">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="e6563-128">Merhaba adını veya bir kuruluş uygulama logosunu değiştirme</span><span class="sxs-lookup"><span data-stu-id="e6563-128">Change hello name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
