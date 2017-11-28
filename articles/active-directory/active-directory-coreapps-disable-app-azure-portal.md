---
title: "Kullanıcı oturum açma işlemlerine Azure Active Directory'de bir kurumsal uygulama için devre dışı bırakma | Microsoft Docs"
description: "Böylece hiçbir kullanıcılar için Azure Active Directory'de oturum Kurumsal uygulama devre dışı bırakma"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a27562f9-18dc-42e8-9fee-5419566f8fd7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 5d27046370eada0c371c94fb573fa1bcf536f7cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="92a94-103">Kullanıcı oturum açma işlemlerine Azure Active Directory'de bir kurumsal uygulama için devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="92a94-103">Disable user sign-ins for an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="92a94-104">Böylece hiçbir kullanıcılar için Azure Active Directory (Azure AD) oturum Kurumsal uygulama devre dışı bırakmak kolaydır.</span><span class="sxs-lookup"><span data-stu-id="92a94-104">It's easy to disable an enterprise application so that no users may sign in to it in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="92a94-105">Kuruluş uygulama yönetmek için uygun izinlere sahip olmalıdır ve dizin için genel yönetici olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="92a94-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

## <a name="how-do-i-disable-user-sign-ins"></a><span data-ttu-id="92a94-106">Kullanıcı oturum açma işlemleri nasıl devre dışı bırakabilirim?</span><span class="sxs-lookup"><span data-stu-id="92a94-106">How do I disable user sign-ins?</span></span>
1. <span data-ttu-id="92a94-107">Oturum [Azure portal](https://portal.azure.com) dizini için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="92a94-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="92a94-108">Seçin **daha fazla hizmet**, girin **Azure Active Directory** metin kutusuna ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="92a94-108">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="92a94-109">Üzerinde **Azure Active Directory** -  ***directoryname*** (diğer bir deyişle, Azure AD dikey yönettiğiniz dizin için), dikey penceresinde seçin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="92a94-109">On the **Azure Active Directory** -  ***directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Açılış Kurumsal uygulamaları](./media/active-directory-coreapps-disable-app-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="92a94-111">Üzerinde **kurumsal uygulamalar** dikey penceresinde, select **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="92a94-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="92a94-112">Yönetebileceğiniz uygulamaların bir listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="92a94-112">You see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="92a94-113">Üzerinde **kurumsal uygulamalar - tüm uygulamaları** dikey penceresinde, bir uygulama seçin.</span><span class="sxs-lookup"><span data-stu-id="92a94-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="92a94-114">Üzerinde ***appname*** dikey penceresinde (diğer bir deyişle, dikey penceresinde seçili uygulamasının başlık adı ile) seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="92a94-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Properties**.</span></span>

    ![Tüm uygulamalar komutu seçme](./media/active-directory-coreapps-disable-app-azure-portal/select-app.png)
7. <span data-ttu-id="92a94-116">Üzerinde ***appname*** - **özellikleri** dikey penceresinde, select **Hayır** için **kullanıcıların oturum açma için etkinleştirilen?**.</span><span class="sxs-lookup"><span data-stu-id="92a94-116">On the ***appname*** - **Properties** blade, select **No** for **Enabled for users to sign-in?**.</span></span>
8. <span data-ttu-id="92a94-117">Seçin **kaydetmek** komutu.</span><span class="sxs-lookup"><span data-stu-id="92a94-117">Select the **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92a94-118">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="92a94-118">Next steps</span></span>
* [<span data-ttu-id="92a94-119">My tüm grupları görmek</span><span class="sxs-lookup"><span data-stu-id="92a94-119">See all my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="92a94-120">Bir kullanıcı veya grup için bir kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="92a94-120">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="92a94-121">Bir kullanıcı veya grup ataması Kurumsal uygulamadan Kaldır</span><span class="sxs-lookup"><span data-stu-id="92a94-121">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="92a94-122">Adını veya bir kuruluş uygulama logosunu değiştirme</span><span class="sxs-lookup"><span data-stu-id="92a94-122">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
