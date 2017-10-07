---
title: "Azure Analysis Services aaaManage sunucu yöneticileri | Microsoft Docs"
description: "Bilgi nasıl toomanage Azure Analysis Services sunucusu için sunucu yöneticileri."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: e04387e48e9b9483c382ee5cc9fd65f8331fb2a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-server-administrators"></a><span data-ttu-id="75023-103">Sunucu yöneticileri yönetin</span><span class="sxs-lookup"><span data-stu-id="75023-103">Manage server administrators</span></span>
<span data-ttu-id="75023-104">Sunucu yöneticileri, hangi hello sunucusunun bulunduğu hello Kiracı için geçerli bir kullanıcı veya grup hello Azure Active Directory (Azure AD) içinde olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="75023-104">Server administrators must be a valid user or group in hello Azure Active Directory (Azure AD) for hello tenant in which hello server resides.</span></span> <span data-ttu-id="75023-105">Kullanabileceğiniz **Analysis Services Admins** hello denetim dikey sunucunuz Azure portalında veya sunucu özelliklerinde SSMS toomanage sunucu yöneticileri için.</span><span class="sxs-lookup"><span data-stu-id="75023-105">You can use **Analysis Services Admins** in hello control blade for your server in Azure portal, or Server Properties in SSMS toomanage server administrators.</span></span> 

## <a name="tooadd-server-administrators-by-using-azure-portal"></a><span data-ttu-id="75023-106">Azure portalını kullanarak tooadd sunucu yöneticileri</span><span class="sxs-lookup"><span data-stu-id="75023-106">tooadd server administrators by using Azure portal</span></span>
1. <span data-ttu-id="75023-107">Sunucunuz için Hello denetim dikey penceresinde tıklayın **Analysis Services Admins**.</span><span class="sxs-lookup"><span data-stu-id="75023-107">In hello control blade for your server, click **Analysis Services Admins**.</span></span>
2. <span data-ttu-id="75023-108">Merhaba,  **\<sunucuadı >-Analysis Services Admins** dikey penceresinde tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="75023-108">In hello **\<servername> - Analysis Services Admins** blade, click **Add**.</span></span>
3. <span data-ttu-id="75023-109">Merhaba, **sunucu yöneticileri ekleme** dikey penceresinde kullanıcı hesapları Azure AD'nizi seçin veya e-posta adresiyle dış kullanıcıları davet.</span><span class="sxs-lookup"><span data-stu-id="75023-109">In hello **Add Server Administrators** blade, select user accounts from your Azure AD or invite external users by email address.</span></span>

    ![Sunucu yöneticileri Azure portalında](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="tooadd-server-administrators-by-using-ssms"></a><span data-ttu-id="75023-111">SSMS kullanarak tooadd sunucu yöneticileri</span><span class="sxs-lookup"><span data-stu-id="75023-111">tooadd server administrators by using SSMS</span></span>
1. <span data-ttu-id="75023-112">Sağ hello server > **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="75023-112">Right-click hello server > **Properties**.</span></span>
2. <span data-ttu-id="75023-113">İçinde **Analysis Server özellikleri**, tıklatın **güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="75023-113">In **Analysis Server Properties**, click **Security**.</span></span>
3. <span data-ttu-id="75023-114">Tıklatın **Ekle**ve ardından hello e-posta adresi, Azure AD'de kullanıcı veya grup için girin.</span><span class="sxs-lookup"><span data-stu-id="75023-114">Click **Add**, and then enter hello email address for a user or group in your Azure AD.</span></span>
   
    ![Sunucu yöneticileri SSMS Ekle](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a><span data-ttu-id="75023-116">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="75023-116">Next steps</span></span> 
[<span data-ttu-id="75023-117">Kimlik doğrulaması ve kullanıcı izinleri</span><span class="sxs-lookup"><span data-stu-id="75023-117">Authentication and user permissions</span></span>](analysis-services-manage-users.md)  
[<span data-ttu-id="75023-118">Veritabanı rolleri ve kullanıcıları yönetme</span><span class="sxs-lookup"><span data-stu-id="75023-118">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="75023-119">Rol Tabanlı Access Control</span><span class="sxs-lookup"><span data-stu-id="75023-119">Role-Based Access Control</span></span>](../active-directory/role-based-access-control-what-is.md)  

