---
title: "Azure Active Directory'deki bir gruba aaaManage hello üyeleri | Microsoft Docs"
description: "Nasıl tooadd veya Azure Active Directory'deki bir gruba kullanıcı ve cihazları kaldırma"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d399a97d-fd2a-4b2d-b73d-0975db83f41b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4cb16ee63828003da251423a04736f7174dd4896
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a>Azure Active Directory kiracınızdaki kullanıcıların Grup üyeliğini yönetme
Bu makalede nasıl toomanage hello Azure Active Directory'de (Azure AD) grubu için üyeleri açıklanmaktadır.

## <a name="how-do-i-find-hello-members-and-manage-them"></a>Nasıl hello üyeleri bulmak ve onları yönetmeyi?
1. İçinde toohello oturum [Azure portal](https://portal.azure.com) hello dizin için genel yönetici olan bir hesapla.
2. Seçin **daha fazla hizmet**, girin **kullanıcılar ve gruplar** hello metin kutusuna ve ardından **Enter**.

   ![Açılış kullanıcı yönetimi](./media/active-directory-groups-members-azure-portal/search-user-management.png)
3. Merhaba üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **tüm grupları**.

   ![Açılış hello grupları dikey penceresi](./media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. Merhaba üzerinde **kullanıcılar ve gruplar - tüm grupları** dikey penceresinde, bir grup seçin.
5. Merhaba üzerinde **grup - *groupname***  dikey penceresinde, select **üyeleri**.

   ![Açılış hello üyeleri dikey penceresi](./media/active-directory-groups-members-azure-portal/view-group-members.png)
6. Merhaba üzerinde tooadd üyeleri toohello grubu **Grup - üyeleri** dikey penceresinde, select **Add Members**.

   ![Üyeleri komut ekleme](./media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. Merhaba üzerinde **üyeleri** dikey penceresinde, seçin veya daha fazla kullanıcı veya cihazları tooadd toohello grubu ve select hello **seçin** hello hello dikey tooadd sonunda bunları toohello Grup düğme. Merhaba **kullanıcı** kutusunu filtreleri Merhaba, bir kullanıcı veya aygıt adı girişi tooany parçası eşleşmesini temel alan görüntüleme. Joker karakterler bu kutuya kabul edilir.
8. Merhaba grubundan hello tooremove üyeleri **Grup - üyeleri** dikey penceresinde, bir üye seçin.
9. Merhaba üzerinde ***membername*** dikey penceresinde, select hello **kaldırmak** komut ve hello isteminde Seçiminizi onaylayın.

   ![Üyeleri komutu kaldırın](./media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. Merhaba grubunun üyelerini değiştirmeyi tamamladığınızda seçin **kaydetmek**.

## <a name="additional-information"></a>Ek bilgiler
Bu makalelerde Azure Active Directory ile ilgili ek bilgi sağlanmıştır.

* [Var olan grupları bakın](active-directory-groups-view-azure-portal.md)
* [Yeni bir grup oluşturun ve üye ekleme](active-directory-groups-create-azure-portal.md)
* [Bir grubu ayarlarını yönetme](active-directory-groups-settings-azure-portal.md)
* [Bir grubun üyeliğini yönetme](active-directory-groups-membership-azure-portal.md)
* [Bir gruptaki kullanıcılar için dinamik kurallarını yönet](active-directory-groups-dynamic-membership-azure-portal.md)
