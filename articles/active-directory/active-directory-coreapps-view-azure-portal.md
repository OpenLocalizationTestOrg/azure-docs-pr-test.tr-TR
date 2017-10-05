---
title: "Azure Active Directory'de yönetebilmeniz için tüm kurumsal uygulamaları görüntüleme | Microsoft Docs"
description: "Azure Active Directory'de Yönetme iznine sahip kurumsal uygulamaların bir listesini görmek nasıl"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: c4fb6f94-34f8-4323-8bd7-a3ee44901f7d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 14b335d14d893640d469508d6f34b4e7ec6bee8b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="view-all-the-enterprise-apps-that-i-can-manage-in-azure-active-directory"></a><span data-ttu-id="9e9c2-103">Azure Active Directory'de yönetebilmeniz için tüm kurumsal uygulamaları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="9e9c2-103">View all the enterprise apps that I can manage in Azure Active Directory</span></span>
<span data-ttu-id="9e9c2-104">Azure Active Directory'de (Azure AD), Kurumsal uygulamaları yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e9c2-104">You can manage your enterprise applications in the Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="9e9c2-105">Bu, sizin yönettiğiniz uygulamalar, atama kullanıcıları veya bir uygulama için uygulama adı/logosu gibi uygulama özelliklerini koruma ve böylece hiçbir kullanıcı için oturum açabilir bile bir uygulama devre dışı bırakma grupları görüntüleme içerir.</span><span class="sxs-lookup"><span data-stu-id="9e9c2-105">This includes viewing the apps you can manage, assigning users or groups to an app, maintaining properties for the app such as the application name/logo, and even disabling an application so that no users can sign in to it.</span></span>

## <a name="how-do-i-view-all-my-apps"></a><span data-ttu-id="9e9c2-106">Tüm uygulamalarım nasıl görüntüleyebilirim?</span><span class="sxs-lookup"><span data-stu-id="9e9c2-106">How do I view all my apps?</span></span>
1. <span data-ttu-id="9e9c2-107">Oturum [Azure portal](https://portal.azure.com) dizini için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="9e9c2-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="9e9c2-108">Seçin **daha fazla hizmet**, girin **Azure Active Directory** metin kutusuna ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="9e9c2-108">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="9e9c2-109">Üzerinde **Azure Active Directory -** ***directoryname*** (diğer bir deyişle, Azure AD dikey yönettiğiniz dizin için), dikey penceresinde seçin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="9e9c2-109">On the **Azure Active Directory -** ***directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Açılış Kurumsal uygulamaları](./media/active-directory-coreapps-view-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="9e9c2-111">Üzerinde **kurumsal uygulamalar** dikey penceresinde, select **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="9e9c2-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="9e9c2-112">Bu dikey pencereden yönetmek, görüntülenen sütunları değiştirmek veya (uygulamaları devre dışı yalnızca görüntülemek için örneğin,) bu uygulamayı bulmak için listeyi filtrelemek için uygulamaları seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e9c2-112">From this blade you can select apps to manage, change the displayed columns, or filter the list to find that app you want (for example, to view only disabled apps).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e9c2-113">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9e9c2-113">Next steps</span></span>
* [<span data-ttu-id="9e9c2-114">Bir kullanıcı veya grup için bir kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="9e9c2-114">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="9e9c2-115">Bir kullanıcı veya grup ataması Kurumsal uygulamadan Kaldır</span><span class="sxs-lookup"><span data-stu-id="9e9c2-115">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="9e9c2-116">Kullanıcı oturum açma işlemleri bir kurumsal uygulama için devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="9e9c2-116">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="9e9c2-117">Adını veya bir kuruluş uygulama logosunu değiştirme</span><span class="sxs-lookup"><span data-stu-id="9e9c2-117">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
