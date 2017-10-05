---
title: "Grubunuza ait Azure Active Directory içinde grupları yönetme | Microsoft Docs"
description: "Gruplar, diğer grupları Azure Active Directory'de içerebilir. Aşağıda, bu üyeliklerin yönetme verilmiştir."
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
ms.openlocfilehash: 08e04a6590176c4084ca47b4bd6cbb22500eca2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-to-which-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a>Yönetmek için hangi grupların Azure Active Directory kiracınızda bir grup ait
Gruplar, diğer grupları Azure Active Directory'de içerebilir. Aşağıda, bu üyeliklerin yönetme verilmiştir.

## <a name="how-do-i-find-the-groups-my-group-is-a-member-of"></a>Grubunuza üye olduğu grupları nasıl bulabilirim?
1. Oturum [Azure portal](https://portal.azure.com) dizini için genel yönetici olan bir hesapla.
2. Seçin **daha fazla hizmet**, girin **kullanıcılar ve gruplar** metin kutusuna ve ardından **Enter**.

   ![Açılış kullanıcı yönetimi](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. Üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **tüm grupları**.

   ![Grupları dikey penceresini açma](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. Üzerinde **kullanıcılar ve gruplar - tüm grupları** dikey penceresinde, bir grup seçin.
5. Üzerinde **grup - *groupname***  dikey penceresinde, select **grup üyeliklerini**.

   ![Grup üyelikleri dikey penceresini açma](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. Grubunuzun başka bir grubun üyesi olarak eklemek için **Grup - grup üyeliklerini** dikey penceresinde, select **Ekle** komutu.
7. Bir grup seçin **Grup Seç** dikey ve ardından **seçin** dikey pencerenin altındaki düğmesini. Grubunuzun aynı anda yalnızca bir gruba ekleyebilirsiniz. **Kullanıcı** kutusu, bir kullanıcı veya aygıt adı herhangi bir kısmını girişe eşleşmesini temel alan görüntü filtreler. Joker karakterler bu kutuya kabul edilir.

   ![Bir grup üyeliği ekleme](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. Başka bir grubun üyesi olarak grubunuzun kaldırmak için **Grup - grup üyeliklerini** dikey penceresinde, bir grup seçin.
9. Üzerinde ***groupname*** dikey penceresinde, select **kaldırmak** komut ve komut isteminde Seçiminizi onaylayın.

   ![Üyelik komutu kaldırın](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. Grubunuz için grup üyeliklerini değiştirme işiniz bittiğinde, seçin **kaydetmek**.

## <a name="additional-information"></a>Ek bilgiler
Bu makalelerde Azure Active Directory ile ilgili ek bilgi sağlanmıştır.

* [Var olan grupları bakın](active-directory-groups-view-azure-portal.md)
* [Yeni bir grup oluşturun ve üye ekleme](active-directory-groups-create-azure-portal.md)
* [Bir grubu ayarlarını yönetme](active-directory-groups-settings-azure-portal.md)
* [Bir grubun üyelerini yönetmek](active-directory-groups-members-azure-portal.md)
* [Bir gruptaki kullanıcılar için dinamik kurallarını yönet](active-directory-groups-dynamic-membership-azure-portal.md)
