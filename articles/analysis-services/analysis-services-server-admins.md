---
title: "Azure Analysis Services sunucu yöneticileri yönetme | Microsoft Docs"
description: "Azure Analysis Services sunucusu için sunucu yöneticileri yönetmeyi öğrenin."
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
ms.openlocfilehash: a1b58125dafdf73f245b6a8cd0f4917513b22ea9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-server-administrators"></a><span data-ttu-id="ee461-103">Sunucu yöneticileri yönetin</span><span class="sxs-lookup"><span data-stu-id="ee461-103">Manage server administrators</span></span>
<span data-ttu-id="ee461-104">Sunucu yöneticileri, sunucunun bulunduğu Kiracı için geçerli bir kullanıcı veya grup Azure Active Directory'de (Azure AD) olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee461-104">Server administrators must be a valid user or group in the Azure Active Directory (Azure AD) for the tenant in which the server resides.</span></span> <span data-ttu-id="ee461-105">Kullanabileceğiniz **Analysis Services Admins** denetim dikey penceresinde sunucunuz Azure portalında veya sunucu yöneticileri yönetmek için SSMS sunucu özellikleri için.</span><span class="sxs-lookup"><span data-stu-id="ee461-105">You can use **Analysis Services Admins** in the control blade for your server in Azure portal, or Server Properties in SSMS to manage server administrators.</span></span> 

## <a name="to-add-server-administrators-by-using-azure-portal"></a><span data-ttu-id="ee461-106">Azure portal kullanarak sunucu yöneticileri eklemek için</span><span class="sxs-lookup"><span data-stu-id="ee461-106">To add server administrators by using Azure portal</span></span>
1. <span data-ttu-id="ee461-107">Sunucunuz için Denetim dikey penceresinde tıklayın **Analysis Services Admins**.</span><span class="sxs-lookup"><span data-stu-id="ee461-107">In the control blade for your server, click **Analysis Services Admins**.</span></span>
2. <span data-ttu-id="ee461-108">İçinde  **\<sunucuadı >-Analysis Services Admins** dikey penceresinde tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="ee461-108">In the **\<servername> - Analysis Services Admins** blade, click **Add**.</span></span>
3. <span data-ttu-id="ee461-109">İçinde **sunucu yöneticileri ekleme** dikey penceresinde kullanıcı hesapları Azure AD'nizi seçin veya e-posta adresiyle dış kullanıcıları davet.</span><span class="sxs-lookup"><span data-stu-id="ee461-109">In the **Add Server Administrators** blade, select user accounts from your Azure AD or invite external users by email address.</span></span>

    ![Sunucu yöneticileri Azure portalında](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="to-add-server-administrators-by-using-ssms"></a><span data-ttu-id="ee461-111">SSMS kullanarak sunucu yöneticileri eklemek için</span><span class="sxs-lookup"><span data-stu-id="ee461-111">To add server administrators by using SSMS</span></span>
1. <span data-ttu-id="ee461-112">Sunucuya sağ tıklayın > **özellikleri**.</span><span class="sxs-lookup"><span data-stu-id="ee461-112">Right-click the server > **Properties**.</span></span>
2. <span data-ttu-id="ee461-113">İçinde **Analysis Server özellikleri**, tıklatın **güvenlik**.</span><span class="sxs-lookup"><span data-stu-id="ee461-113">In **Analysis Server Properties**, click **Security**.</span></span>
3. <span data-ttu-id="ee461-114">Tıklatın **Ekle**ve ardından e-posta adresi, Azure AD'de kullanıcı veya grup için girin.</span><span class="sxs-lookup"><span data-stu-id="ee461-114">Click **Add**, and then enter the email address for a user or group in your Azure AD.</span></span>
   
    ![Sunucu yöneticileri SSMS Ekle](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a><span data-ttu-id="ee461-116">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ee461-116">Next steps</span></span> 
[<span data-ttu-id="ee461-117">Kimlik doğrulaması ve kullanıcı izinleri</span><span class="sxs-lookup"><span data-stu-id="ee461-117">Authentication and user permissions</span></span>](analysis-services-manage-users.md)  
[<span data-ttu-id="ee461-118">Veritabanı rolleri ve kullanıcıları yönetme</span><span class="sxs-lookup"><span data-stu-id="ee461-118">Manage database roles and users</span></span>](analysis-services-database-users.md)  
[<span data-ttu-id="ee461-119">Rol Tabanlı Access Control</span><span class="sxs-lookup"><span data-stu-id="ee461-119">Role-Based Access Control</span></span>](../active-directory/role-based-access-control-what-is.md)  

