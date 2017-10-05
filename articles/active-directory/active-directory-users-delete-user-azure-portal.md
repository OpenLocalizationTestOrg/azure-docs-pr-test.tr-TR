---
title: "Azure Active Directory'de bir dizinden kullanıcı silme | Microsoft Docs"
description: "Azure Active Directory'den kullanıcı ve tüm bilgilerini silmek açıklanmaktadır"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: bd1c9ccc-2d80-42bf-82cc-db37bb1a1d67
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: curtand;jeffsta
ms.reviewer: jeffsta
ms.openlocfilehash: 19a4d2c37c785b3b56a2e0e1b6797ec56dad9835
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="delete-a-user-from-a-directory-in-azure-active-directory"></a><span data-ttu-id="371a1-103">Bir kullanıcı Azure Active Directory'de bir dizinden silin</span><span class="sxs-lookup"><span data-stu-id="371a1-103">Delete a user from a directory in Azure Active Directory</span></span>
<span data-ttu-id="371a1-104">Bu makalede, Azure Active Directory'de (Azure AD) bir dizinden bir kullanıcıyı silmek açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="371a1-104">This article explains how to delete a user from a directory in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="371a1-105">Kuruluşunuz için yeni kullanıcı ekleme hakkında daha fazla bilgi için bkz: [Azure Active Directory'ye yeni kullanıcı ekleme](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="371a1-105">For information about adding new users to your organization, see [Add new users to Azure Active Directory](active-directory-users-create-azure-portal.md).</span></span>

## <a name="to-delete-a-user"></a><span data-ttu-id="371a1-106">Bir kullanıcıyı silmek için</span><span class="sxs-lookup"><span data-stu-id="371a1-106">To delete a user</span></span>
1. <span data-ttu-id="371a1-107">Oturum [Azure portalı](https://portal.azure.com) dizini için genel yönetici olan bir hesapla.</span><span class="sxs-lookup"><span data-stu-id="371a1-107">Sign in to [the Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="371a1-108">Seçin **daha fazla hizmet**, girin **kullanıcılar ve gruplar** metin kutusuna ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="371a1-108">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Açılış kullanıcı yönetimi](./media/active-directory-users-delete-user-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="371a1-110">Üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="371a1-110">On the **Users and groups** blade, select **Users**.</span></span>

   ![Kullanıcılar dikey penceresini açma](./media/active-directory-users-delete-user-azure-portal/create-users-open-users-blade.png)
4. <span data-ttu-id="371a1-112">**Kullanıcılar ve gruplar - Kullanıcılar** dikey penceresinde, listeden bir kullanıcı seçin.</span><span class="sxs-lookup"><span data-stu-id="371a1-112">On the **Users and groups - Users** blade, select a user from the list.</span></span>
5. <span data-ttu-id="371a1-113">Seçilen kullanıcı için dikey seçin **genel bakış**ve ardından komut çubuğunda **silmek**.</span><span class="sxs-lookup"><span data-stu-id="371a1-113">On the blade for the selected user, select **Overview**, and then in the command bar, select **Delete**.</span></span>

    ![Delete komutu seçme](./media/active-directory-users-delete-user-azure-portal/create-users-delete-command.png)

## <a name="next-steps"></a><span data-ttu-id="371a1-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="371a1-115">Next steps</span></span>
* [<span data-ttu-id="371a1-116">Azure Active Directory'ye yeni kullanıcı ekleme</span><span class="sxs-lookup"><span data-stu-id="371a1-116">Add new users to Azure Active Directory</span></span>](active-directory-users-create-azure-portal.md)
* [<span data-ttu-id="371a1-117">Azure Active Directory'de bir kullanıcı parolasını sıfırlama</span><span class="sxs-lookup"><span data-stu-id="371a1-117">Reset the password for a user in Azure Active Directory</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="371a1-118">Kullanıcı Azure Active Directory'de yönetici rolleri atama</span><span class="sxs-lookup"><span data-stu-id="371a1-118">Assign a user to administrator roles in Azure Active Directory</span></span>](active-directory-users-assign-role-azure-portal.md)
* [<span data-ttu-id="371a1-119">Azure Active Directory'de bir kullanıcı için profil bilgileri ekleme veya değiştirme</span><span class="sxs-lookup"><span data-stu-id="371a1-119">Add or change profile information for a user in Azure Active Directory</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="371a1-120">Bir kullanıcı Azure Active Directory'de bir dizinden silin</span><span class="sxs-lookup"><span data-stu-id="371a1-120">Delete a user from a directory in Azure Active Directory</span></span>](active-directory-users-profile-azure-portal.md)
