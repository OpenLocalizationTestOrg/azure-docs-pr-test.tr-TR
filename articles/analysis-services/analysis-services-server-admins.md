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
# <a name="manage-server-administrators"></a>Sunucu yöneticileri yönetin
Sunucu yöneticileri, hangi hello sunucusunun bulunduğu hello Kiracı için geçerli bir kullanıcı veya grup hello Azure Active Directory (Azure AD) içinde olması gerekir. Kullanabileceğiniz **Analysis Services Admins** hello denetim dikey sunucunuz Azure portalında veya sunucu özelliklerinde SSMS toomanage sunucu yöneticileri için. 

## <a name="tooadd-server-administrators-by-using-azure-portal"></a>Azure portalını kullanarak tooadd sunucu yöneticileri
1. Sunucunuz için Hello denetim dikey penceresinde tıklayın **Analysis Services Admins**.
2. Merhaba,  **\<sunucuadı >-Analysis Services Admins** dikey penceresinde tıklatın **Ekle**.
3. Merhaba, **sunucu yöneticileri ekleme** dikey penceresinde kullanıcı hesapları Azure AD'nizi seçin veya e-posta adresiyle dış kullanıcıları davet.

    ![Sunucu yöneticileri Azure portalında](./media/analysis-services-server-admins/aas-manage-users-admins.png)

## <a name="tooadd-server-administrators-by-using-ssms"></a>SSMS kullanarak tooadd sunucu yöneticileri
1. Sağ hello server > **özellikleri**.
2. İçinde **Analysis Server özellikleri**, tıklatın **güvenlik**.
3. Tıklatın **Ekle**ve ardından hello e-posta adresi, Azure AD'de kullanıcı veya grup için girin.
   
    ![Sunucu yöneticileri SSMS Ekle](./media/analysis-services-server-admins/aas-manage-users-ssms.png)

## <a name="next-steps"></a>Sonraki adımlar 
[Kimlik doğrulaması ve kullanıcı izinleri](analysis-services-manage-users.md)  
[Veritabanı rolleri ve kullanıcıları yönetme](analysis-services-database-users.md)  
[Rol Tabanlı Access Control](../active-directory/role-based-access-control-what-is.md)  

