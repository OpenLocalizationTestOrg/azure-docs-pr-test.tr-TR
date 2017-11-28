---
title: "Adını veya bir kuruluş uygulama Azure Active Directory'de logosunu değiştirme | Microsoft Docs"
description: "Adı veya logosu Azure Active Directory'de özel Kurumsal uygulama için nasıl değiştirileceğini"
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
ms.openlocfilehash: 3e44e876dcbac704a9809ae5b3957bf94be21c48
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-name-or-logo-of-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="c67d4-103">Adını veya bir kuruluş uygulama Azure Active Directory'de logosunu değiştirme</span><span class="sxs-lookup"><span data-stu-id="c67d4-103">Change the name or logo of an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="c67d4-104">Ad veya Azure Active Directory'de (Azure AD) bir özel Kurumsal uygulama için logosunu değiştirmek çok kolaydır.</span><span class="sxs-lookup"><span data-stu-id="c67d4-104">It's easy to change the name or logo for a custom enterprise application in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="c67d4-105">Bu değişiklikleri yapmak için uygun izinlere sahip olmalıdır ve özel uygulama oluşturucusu olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c67d4-105">You must have the appropriate permissions to make these changes, and you must be the creator of the custom app.</span></span>

## <a name="how-do-i-change-an-enterprise-apps-name-or-logo"></a><span data-ttu-id="c67d4-106">Bir kurumsal uygulamanın adı veya logosu nasıl değiştiririm?</span><span class="sxs-lookup"><span data-stu-id="c67d4-106">How do I change an enterprise app's name or logo?</span></span>
1. <span data-ttu-id="c67d4-107">Oturum [Azure portal](https://portal.azure.com) dizini için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="c67d4-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="c67d4-108">Seçin **daha fazla hizmet**, girin **Azure Active Directory** metin kutusuna ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="c67d4-108">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="c67d4-109">Üzerinde **Azure Active Directory - *directoryname***  (diğer bir deyişle, Azure AD dikey yönettiğiniz dizin için), dikey penceresinde seçin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="c67d4-109">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Açılış Kurumsal uygulamaları](./media/active-directory-coreapps-change-app-logo-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="c67d4-111">Üzerinde **kurumsal uygulamalar** dikey penceresinde, select **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="c67d4-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="c67d4-112">Yönetebileceğiniz uygulamaların bir listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c67d4-112">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="c67d4-113">Üzerinde **kurumsal uygulamalar - tüm uygulamaları** dikey penceresinde, bir uygulama seçin.</span><span class="sxs-lookup"><span data-stu-id="c67d4-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="c67d4-114">Üzerinde ***appname*** dikey penceresinde (diğer bir deyişle, dikey penceresinde seçili uygulamasının başlık adı ile) seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="c67d4-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Properties**.</span></span>

    ![Özellikler komutu seçme](./media/active-directory-coreapps-change-app-logo-azure-portal/select-app.png)
7. <span data-ttu-id="c67d4-116">Üzerinde ***appname*** **-özellikleri** dikey penceresinde, yeni bir logo olarak kullanın veya uygulama adını veya her ikisi de düzenlemek bir dosya için göz atın.</span><span class="sxs-lookup"><span data-stu-id="c67d4-116">On the ***appname*** **- Properties** blade, browse for a file to use as a new logo, or edit the app name, or both.</span></span>

    ![Uygulama logosu veya nameproperties komutu değiştirme](./media/active-directory-coreapps-change-app-logo-azure-portal/change-logo.png)
8. <span data-ttu-id="c67d4-118">Seçin **kaydetmek** komutu.</span><span class="sxs-lookup"><span data-stu-id="c67d4-118">Select the **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c67d4-119">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c67d4-119">Next steps</span></span>
* [<span data-ttu-id="c67d4-120">Tüm my gruplarının bakın</span><span class="sxs-lookup"><span data-stu-id="c67d4-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="c67d4-121">Bir kullanıcı veya grup için bir kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="c67d4-121">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="c67d4-122">Bir kullanıcı veya grup ataması Kurumsal uygulamadan Kaldır</span><span class="sxs-lookup"><span data-stu-id="c67d4-122">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="c67d4-123">Kullanıcı oturum açma işlemleri bir kurumsal uygulama için devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="c67d4-123">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
