---
title: "grubunuza ait tooin Azure Active Directory aaaManage hello gruplarını | Microsoft Docs"
description: "Gruplar, diğer grupları Azure Active Directory'de içerebilir. İşte nasıl toomanage bu üyeliklerin."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e785c2d0-7724-47d4-a56e-c58280c08a14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0a0a1967084de0968e1e802559f9cdfd7ca6ae4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-toowhich-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a><span data-ttu-id="740a9-104">Azure Active Directory kiracınızda bir gruba ait toowhich gruplarını yönetme</span><span class="sxs-lookup"><span data-stu-id="740a9-104">Manage toowhich groups a group belongs in your Azure Active Directory tenant</span></span>
<span data-ttu-id="740a9-105">Gruplar, diğer grupları Azure Active Directory'de içerebilir.</span><span class="sxs-lookup"><span data-stu-id="740a9-105">Groups can contain other groups in Azure Active Directory.</span></span> <span data-ttu-id="740a9-106">İşte nasıl toomanage bu üyeliklerin.</span><span class="sxs-lookup"><span data-stu-id="740a9-106">Here's how toomanage those memberships.</span></span>

## <a name="how-do-i-find-hello-groups-my-group-is-a-member-of"></a><span data-ttu-id="740a9-107">Merhaba grupları grubum üyesi nasıl bulabilirim?</span><span class="sxs-lookup"><span data-stu-id="740a9-107">How do I find hello groups my group is a member of?</span></span>
1. <span data-ttu-id="740a9-108">İçinde toohello oturum [Azure portal](https://portal.azure.com) hello dizin için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="740a9-108">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="740a9-109">Seçin **daha fazla hizmet**, girin **kullanıcılar ve gruplar** hello metin kutusuna ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="740a9-109">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

   ![Açılış kullanıcı yönetimi](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. <span data-ttu-id="740a9-111">Merhaba üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **tüm grupları**.</span><span class="sxs-lookup"><span data-stu-id="740a9-111">On hello **Users and groups** blade, select **All groups**.</span></span>

   ![Açılış hello grupları dikey penceresi](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="740a9-113">Merhaba üzerinde **kullanıcılar ve gruplar - tüm grupları** dikey penceresinde, bir grup seçin.</span><span class="sxs-lookup"><span data-stu-id="740a9-113">On hello **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="740a9-114">Merhaba üzerinde **grup - *groupname***  dikey penceresinde, select **grup üyeliklerini**.</span><span class="sxs-lookup"><span data-stu-id="740a9-114">On hello **Group - *groupname*** blade, select **Group memberships**.</span></span>

   ![Açılış hello grup üyeliklerini dikey penceresi](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. <span data-ttu-id="740a9-116">tooadd grubunuzun hello üzerinde başka bir grubun üyesi olarak **Grup - grup üyeliklerini** dikey penceresinde, select hello **Ekle** komutu.</span><span class="sxs-lookup"><span data-stu-id="740a9-116">tooadd your group as a member of another group, on hello **Group - Group memberships** blade, select hello **Add** command.</span></span>
7. <span data-ttu-id="740a9-117">Merhaba bir grubu seçin **Grup Seç** dikey penceresinde ve ardından hello **seçin** hello dikey penceresinde hello sonundaki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="740a9-117">Select a group from hello **Select Group** blade, and then select hello **Select** button at hello bottom of hello blade.</span></span> <span data-ttu-id="740a9-118">Aynı anda Grup tooonly bir grup ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="740a9-118">You can add your group tooonly one group at a time.</span></span> <span data-ttu-id="740a9-119">Merhaba **kullanıcı** kutusunu filtreleri Merhaba, bir kullanıcı veya aygıt adı girişi tooany parçası eşleşmesini temel alan görüntüleme.</span><span class="sxs-lookup"><span data-stu-id="740a9-119">hello **User** box filters hello display based on matching your entry tooany part of a user or device name.</span></span> <span data-ttu-id="740a9-120">Joker karakterler bu kutuya kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="740a9-120">No wildcard characters are accepted in that box.</span></span>

   ![Bir grup üyeliği ekleme](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. <span data-ttu-id="740a9-122">tooremove grubunuzun hello üzerinde başka bir grubun üyesi olarak **Grup - grup üyeliklerini** dikey penceresinde, bir grup seçin.</span><span class="sxs-lookup"><span data-stu-id="740a9-122">tooremove your group as a member of another group, on hello **Group - Group memberships** blade, select a group.</span></span>
9. <span data-ttu-id="740a9-123">Merhaba üzerinde ***groupname*** dikey penceresinde, select hello **kaldırmak** komut ve hello isteminde Seçiminizi onaylayın.</span><span class="sxs-lookup"><span data-stu-id="740a9-123">On hello ***groupname*** blade, select hello **Remove** command, and confirm your choice at hello prompt.</span></span>

   ![Üyelik komutu kaldırın](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. <span data-ttu-id="740a9-125">Grubunuz için grup üyeliklerini değiştirme işiniz bittiğinde, seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="740a9-125">When you finish changing group memberships for your group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="740a9-126">Ek bilgiler</span><span class="sxs-lookup"><span data-stu-id="740a9-126">Additional information</span></span>
<span data-ttu-id="740a9-127">Bu makalelerde Azure Active Directory ile ilgili ek bilgi sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="740a9-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="740a9-128">Var olan grupları bakın</span><span class="sxs-lookup"><span data-stu-id="740a9-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="740a9-129">Yeni bir grup oluşturun ve üye ekleme</span><span class="sxs-lookup"><span data-stu-id="740a9-129">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="740a9-130">Bir grubu ayarlarını yönetme</span><span class="sxs-lookup"><span data-stu-id="740a9-130">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="740a9-131">Bir grubun üyelerini yönetmek</span><span class="sxs-lookup"><span data-stu-id="740a9-131">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="740a9-132">Bir gruptaki kullanıcılar için dinamik kurallarını yönet</span><span class="sxs-lookup"><span data-stu-id="740a9-132">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
