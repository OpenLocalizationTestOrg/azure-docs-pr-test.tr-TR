---
title: "aaaDisable kullanıcı oturum açma işlemlerine Azure Active Directory'de bir kurumsal uygulama için | Microsoft Docs"
description: "Nasıl toodisable Kurumsal uygulama böylece hiçbir kullanıcı tooit Azure Active Directory'de oturum açma"
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
ms.openlocfilehash: 4c560b59359d433b0852a7606cc2cc0204866234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="93976-103">Kullanıcı oturum açma işlemlerine Azure Active Directory'de bir kurumsal uygulama için devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="93976-103">Disable user sign-ins for an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="93976-104">Kolay toodisable Kurumsal uygulama, böylelikle kullanıcı tooit Azure Active Directory'de (Azure AD) oturum açma.</span><span class="sxs-lookup"><span data-stu-id="93976-104">It's easy toodisable an enterprise application so that no users may sign in tooit in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="93976-105">Merhaba uygun izinleri toomanage hello kuruluş uygulama olmalıdır ve başlangıç dizini için genel yönetici olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="93976-105">You must have hello appropriate permissions toomanage hello enterprise app, and you must be global admin for hello directory.</span></span>

## <a name="how-do-i-disable-user-sign-ins"></a><span data-ttu-id="93976-106">Kullanıcı oturum açma işlemleri nasıl devre dışı bırakabilirim?</span><span class="sxs-lookup"><span data-stu-id="93976-106">How do I disable user sign-ins?</span></span>
1. <span data-ttu-id="93976-107">İçinde toohello oturum [Azure portal](https://portal.azure.com) hello dizin için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="93976-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="93976-108">Seçin **daha fazla hizmet**, girin **Azure Active Directory** hello metin kutusuna ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="93976-108">Select **More services**, enter **Azure Active Directory** in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="93976-109">Merhaba üzerinde **Azure Active Directory** -  ***directoryname*** dikey penceresinde (diğer bir deyişle, hello Azure AD dikey penceresinde hello dizin yönettiğiniz için) seçin **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="93976-109">On hello **Azure Active Directory** -  ***directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![Açılış Kurumsal uygulamaları](./media/active-directory-coreapps-disable-app-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="93976-111">Merhaba üzerinde **kurumsal uygulamalar** dikey penceresinde, select **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="93976-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="93976-112">Yönetebileceğiniz hello uygulamaların bir listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="93976-112">You see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="93976-113">Merhaba üzerinde **kurumsal uygulamalar - tüm uygulamaları** dikey penceresinde, bir uygulama seçin.</span><span class="sxs-lookup"><span data-stu-id="93976-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="93976-114">Merhaba üzerinde ***appname*** dikey penceresinde (diğer bir deyişle, hello dikey penceresinde hello adıyla hello başlığında hello seçilen uygulama) seçin **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="93976-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Properties**.</span></span>

    ![Merhaba tüm uygulamaları komutu seçme](./media/active-directory-coreapps-disable-app-azure-portal/select-app.png)
7. <span data-ttu-id="93976-116">Merhaba üzerinde ***appname*** - **özellikleri** dikey penceresinde, select **Hayır** için **toosign bileşenini kullanıcılar için etkin?**.</span><span class="sxs-lookup"><span data-stu-id="93976-116">On hello ***appname*** - **Properties** blade, select **No** for **Enabled for users toosign-in?**.</span></span>
8. <span data-ttu-id="93976-117">Select hello **kaydetmek** komutu.</span><span class="sxs-lookup"><span data-stu-id="93976-117">Select hello **Save** command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93976-118">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="93976-118">Next steps</span></span>
* [<span data-ttu-id="93976-119">My tüm grupları görmek</span><span class="sxs-lookup"><span data-stu-id="93976-119">See all my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="93976-120">Bir kullanıcı veya grup tooan kuruluş uygulama atama</span><span class="sxs-lookup"><span data-stu-id="93976-120">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="93976-121">Bir kullanıcı veya grup ataması Kurumsal uygulamadan Kaldır</span><span class="sxs-lookup"><span data-stu-id="93976-121">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="93976-122">Merhaba adını veya bir kuruluş uygulama logosunu değiştirme</span><span class="sxs-lookup"><span data-stu-id="93976-122">Change hello name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
