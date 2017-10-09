---
title: "aaaChange hello adı veya logosu Kurumsal uygulama Azure Active Directory'de | Microsoft Docs"
description: "Toochange nasıl hello adı veya bir özel kuruluş uygulama Azure Active Directory'de logosu"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d01303ce-e6cb-4f3b-a4d6-ec29dfd68146
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: b660e1f0f6c7ffd626e17e2e3399e7169f6e8bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-name-or-logo-of-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="32ba8-103">Merhaba adını veya bir kuruluş uygulama Azure Active Directory'de logosunu değiştirme</span><span class="sxs-lookup"><span data-stu-id="32ba8-103">Change hello name or logo of an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="32ba8-104">Kolay toochange hello veya Azure Active Directory (Azure AD) bir özel kuruluş uygulamasında logosu adıdır.</span><span class="sxs-lookup"><span data-stu-id="32ba8-104">It's easy toochange hello name or logo for a custom enterprise application in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="32ba8-105">Bu değişiklikler hello uygun izinleri toomake olmalıdır ve hello özel uygulama hello oluşturucusu olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="32ba8-105">You must have hello appropriate permissions toomake these changes, and you must be hello creator of hello custom app.</span></span>

## <a name="how-do-i-change-an-enterprise-apps-name-or-logo"></a><span data-ttu-id="32ba8-106">Bir kurumsal uygulamanın adı veya logosu nasıl değiştiririm?</span><span class="sxs-lookup"><span data-stu-id="32ba8-106">How do I change an enterprise app's name or logo?</span></span>
1. <span data-ttu-id="32ba8-107">İçinde toohello oturum [Azure portal](https://portal.azure.com) hello dizin için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="32ba8-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="32ba8-108">Seçin **daha fazla hizmet**, girin **Azure Active Directory** hello metin kutusuna ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="32ba8-108">Select **More services**, enter **Azure Active Directory** in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="32ba8-109">Merhaba üzerinde **Azure Active Directory - *directoryname***  dikey penceresinde (diğer bir deyişle, hello Azure AD dikey penceresinde hello dizin yönettiğiniz için) seçin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="32ba8-109">On hello **Azure Active Directory - *directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![Açılış Kurumsal uygulamaları](./media/active-directory-coreapps-change-app-logo-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="32ba8-111">Merhaba üzerinde **kurumsal uygulamalar** dikey penceresinde, select **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="32ba8-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="32ba8-112">Yönetebileceğiniz hello uygulamaların bir listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="32ba8-112">You'll see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="32ba8-113">Merhaba üzerinde **kurumsal uygulamalar - tüm uygulamaları** dikey penceresinde, bir uygulama seçin.</span><span class="sxs-lookup"><span data-stu-id="32ba8-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="32ba8-114">Merhaba üzerinde ***appname*** dikey penceresinde (diğer bir deyişle, hello dikey penceresinde hello adıyla hello başlığında hello seçilen uygulama) seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="32ba8-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Properties**.</span></span>

    ![Merhaba Özellikler komutu seçme](./media/active-directory-coreapps-change-app-logo-azure-portal/select-app.png)
7. <span data-ttu-id="32ba8-116">Merhaba üzerinde ***appname*** **-özellikleri** dikey penceresinde, yeni bir logo olarak dosya toouse gözatın veya hello uygulama adı ya da her ikisini düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="32ba8-116">On hello ***appname*** **- Properties** blade, browse for a file toouse as a new logo, or edit hello app name, or both.</span></span>

    ![Merhaba uygulama logosu veya nameproperties komutu değiştirme](./media/active-directory-coreapps-change-app-logo-azure-portal/change-logo.png)
8. <span data-ttu-id="32ba8-118">Select hello **kaydetmek** komutu.</span><span class="sxs-lookup"><span data-stu-id="32ba8-118">Select hello **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32ba8-119">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="32ba8-119">Next steps</span></span>
* [<span data-ttu-id="32ba8-120">Tüm my gruplarının bakın</span><span class="sxs-lookup"><span data-stu-id="32ba8-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="32ba8-121">Bir kullanıcı veya grup tooan kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="32ba8-121">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="32ba8-122">Bir kullanıcı veya grup ataması Kurumsal uygulamadan Kaldır</span><span class="sxs-lookup"><span data-stu-id="32ba8-122">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="32ba8-123">Kullanıcı oturum açma işlemleri bir kurumsal uygulama için devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="32ba8-123">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
