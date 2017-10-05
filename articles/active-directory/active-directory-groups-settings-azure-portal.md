---
title: "Azure Active Directory'de Grup Özellikleri yönetme | Microsoft Docs"
description: "Özelliklerini ve diğer Azure Active Directory'deki bir gruba yapılandırma ayarlarını düzenleme"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 2f058f9a-5a8f-4b4b-b3b7-885ff10cb1be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: H1Hack27Feb2017;it-pro
ms.openlocfilehash: b4baccafc0a9178223dbf64c664fc34ab9f7f916
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="manage-the-settings-for-a-group-in-azure-active-directory"></a><span data-ttu-id="8cc93-103">Azure Active Directory'deki bir gruba ayarlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="8cc93-103">Manage the settings for a group in Azure Active Directory</span></span>
<span data-ttu-id="8cc93-104">Bu makalede, Azure Active Directory'de (Azure AD) bir grup ayarlarının nasıl değiştirileceği açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8cc93-104">This article explains how to change the settings for a group in Azure Active Directory (Azure AD).</span></span>

## <a name="how-do-i-find-and-change-the-settings"></a><span data-ttu-id="8cc93-105">Nasıl bulmak ve ayarları değiştirmek mi?</span><span class="sxs-lookup"><span data-stu-id="8cc93-105">How do I find and change the settings?</span></span>
1. <span data-ttu-id="8cc93-106">Dizin için genel yönetici olan bir hesapla [Azure AD yönetim merkezinde](https://aad.portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="8cc93-106">Sign in to the [Azure AD admin center](https://aad.portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="8cc93-107">Seçin **daha fazla hizmet**, girin **kullanıcılar ve gruplar** metin kutusuna ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="8cc93-107">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Açılış kullanıcıları ve grupları dikey penceresi](./media/active-directory-groups-settings-azure-portal/search-user-management.png)
3. <span data-ttu-id="8cc93-109">Üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **tüm grupları**.</span><span class="sxs-lookup"><span data-stu-id="8cc93-109">On the **Users and groups** blade, select **All groups**.</span></span>

   ![Tüm grupları dikey penceresini açma](./media/active-directory-groups-settings-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="8cc93-111">Üzerinde **kullanıcılar ve gruplar - tüm grupları** dikey penceresinde, bir grup seçin.</span><span class="sxs-lookup"><span data-stu-id="8cc93-111">On the **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="8cc93-112">Üzerinde **grup - *groupname***  dikey penceresinde, select **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="8cc93-112">On the **Group - *groupname*** blade, select **Properties**.</span></span>

   ![Özellikler dikey penceresini açma](./media/active-directory-groups-settings-azure-portal/select-group-properties.png)
6. <span data-ttu-id="8cc93-114">Grubun özelliklerini değiştirmeyi tamamladığınızda seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="8cc93-114">When you finish changing properties for the group, select **Save**.</span></span>    

   ![Özellikler değişiklikler kaydediliyor](./media/active-directory-groups-settings-azure-portal/save-group-properties.png)

## <a name="next-steps"></a><span data-ttu-id="8cc93-116">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8cc93-116">Next steps</span></span>
<span data-ttu-id="8cc93-117">Bu makalelerde Azure Active Directory ile ilgili ek bilgi sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8cc93-117">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="8cc93-118">Var olan grupları bakın</span><span class="sxs-lookup"><span data-stu-id="8cc93-118">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="8cc93-119">Yeni bir grup oluşturun ve üye ekleme</span><span class="sxs-lookup"><span data-stu-id="8cc93-119">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="8cc93-120">Bir grubun üyelerini yönetmek</span><span class="sxs-lookup"><span data-stu-id="8cc93-120">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="8cc93-121">Bir grubun üyeliğini yönetme</span><span class="sxs-lookup"><span data-stu-id="8cc93-121">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="8cc93-122">Bir gruptaki kullanıcılar için dinamik kurallarını yönet</span><span class="sxs-lookup"><span data-stu-id="8cc93-122">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
