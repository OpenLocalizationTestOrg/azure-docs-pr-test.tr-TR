---
title: "bir kullanıcı veya grup ataması Kurumsal uygulama Azure Active Directory'de aaaRemove | Microsoft Docs"
description: "Nasıl tooremove hello erişim bir kullanıcı veya grup ataması Kurumsal uygulama Azure Active Directory'de"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7b2d365b-ae92-477f-9702-353cc6acc5ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: c067ecf59b4dedfe8f848357ca8bd545bdc610eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="96679-103">Bir kuruluş uygulama Azure Active Directory'de bir kullanıcı veya grup ataması kaldırma</span><span class="sxs-lookup"><span data-stu-id="96679-103">Remove a user or group assignment from an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="96679-104">Kolay tooremove bir kullanıcı veya Azure Active Directory'de (Azure AD), Kurumsal uygulamalarınızın erişim tooone atanmasını gelen bir grup değil.</span><span class="sxs-lookup"><span data-stu-id="96679-104">It's easy tooremove a user or a group from being assigned access tooone of your enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="96679-105">Merhaba uygun izinleri toomanage hello kuruluş uygulama olmalıdır ve başlangıç dizini için genel yönetici olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="96679-105">You must have hello appropriate permissions toomanage hello enterprise app, and you must be global admin for hello directory.</span></span>

## <a name="how-do-i-remove-a-user-or-group-assignment"></a><span data-ttu-id="96679-106">Bir kullanıcı veya grup ataması nasıl kaldırabilirim?</span><span class="sxs-lookup"><span data-stu-id="96679-106">How do I remove a user or group assignment?</span></span>
1. <span data-ttu-id="96679-107">İçinde toohello oturum [Azure portal](https://portal.azure.com) hello dizin için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="96679-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="96679-108">Seçin **daha fazla hizmet**, girin **Azure Active Directory** hello metin kutusuna ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="96679-108">Select **More services**, enter **Azure Active Directory** in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="96679-109">Merhaba üzerinde **Azure Active Directory - *directoryname***  dikey penceresinde (diğer bir deyişle, hello Azure AD dikey penceresinde hello dizin yönettiğiniz için) seçin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="96679-109">On hello **Azure Active Directory - *directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![Açılış Kurumsal uygulamaları](./media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="96679-111">Merhaba üzerinde **kurumsal uygulamalar** dikey penceresinde, select **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="96679-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="96679-112">Yönetebileceğiniz hello uygulamaların bir listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="96679-112">You'll see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="96679-113">Merhaba üzerinde **kurumsal uygulamalar - tüm uygulamaları** dikey penceresinde, bir uygulama seçin.</span><span class="sxs-lookup"><span data-stu-id="96679-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="96679-114">Merhaba üzerinde ***appname*** dikey penceresinde (diğer bir deyişle, hello dikey penceresinde hello adıyla hello başlığında hello seçilen uygulama) seçin **kullanıcıları ve grupları**.</span><span class="sxs-lookup"><span data-stu-id="96679-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Users & Groups**.</span></span>

    ![Kullanıcıları veya grupları seçme](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. <span data-ttu-id="96679-116">Merhaba üzerinde ***appname*** **-kullanıcı ve grup atama** dikey penceresinde, daha fazla kullanıcı veya grup seçin ve ardından hello seçin **kaldırmak** komutu.</span><span class="sxs-lookup"><span data-stu-id="96679-116">On hello ***appname*** **- User & Group Assignment** blade, select one of more users or groups and then select hello **Remove** command.</span></span> <span data-ttu-id="96679-117">Kararınızı hello isteminde onaylayın.</span><span class="sxs-lookup"><span data-stu-id="96679-117">Confirm your decision at hello prompt.</span></span>

    ![Merhaba Kaldır komutu seçme](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a><span data-ttu-id="96679-119">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="96679-119">Next steps</span></span>
* [<span data-ttu-id="96679-120">Tüm my gruplarının bakın</span><span class="sxs-lookup"><span data-stu-id="96679-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="96679-121">Bir kullanıcı veya grup tooan kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="96679-121">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="96679-122">Kullanıcı oturum açma işlemleri bir kurumsal uygulama için devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="96679-122">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="96679-123">Merhaba adını veya bir kuruluş uygulama logosunu değiştirme</span><span class="sxs-lookup"><span data-stu-id="96679-123">Change hello name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
