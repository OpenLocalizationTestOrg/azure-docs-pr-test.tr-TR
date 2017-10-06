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
# <a name="manage-toowhich-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a>Azure Active Directory kiracınızda bir gruba ait toowhich gruplarını yönetme
Gruplar, diğer grupları Azure Active Directory'de içerebilir. İşte nasıl toomanage bu üyeliklerin.

## <a name="how-do-i-find-hello-groups-my-group-is-a-member-of"></a>Merhaba grupları grubum üyesi nasıl bulabilirim?
1. İçinde toohello oturum [Azure portal](https://portal.azure.com) hello dizin için genel yönetici olan bir hesapla.
2. Seçin **daha fazla hizmet**, girin **kullanıcılar ve gruplar** hello metin kutusuna ve ardından **Enter**.

   ![Açılış kullanıcı yönetimi](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. Merhaba üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **tüm grupları**.

   ![Açılış hello grupları dikey penceresi](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. Merhaba üzerinde **kullanıcılar ve gruplar - tüm grupları** dikey penceresinde, bir grup seçin.
5. Merhaba üzerinde **grup - *groupname***  dikey penceresinde, select **grup üyeliklerini**.

   ![Açılış hello grup üyeliklerini dikey penceresi](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. tooadd grubunuzun hello üzerinde başka bir grubun üyesi olarak **Grup - grup üyeliklerini** dikey penceresinde, select hello **Ekle** komutu.
7. Merhaba bir grubu seçin **Grup Seç** dikey penceresinde ve ardından hello **seçin** hello dikey penceresinde hello sonundaki düğmesi. Aynı anda Grup tooonly bir grup ekleyebilirsiniz. Merhaba **kullanıcı** kutusunu filtreleri Merhaba, bir kullanıcı veya aygıt adı girişi tooany parçası eşleşmesini temel alan görüntüleme. Joker karakterler bu kutuya kabul edilir.

   ![Bir grup üyeliği ekleme](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. tooremove grubunuzun hello üzerinde başka bir grubun üyesi olarak **Grup - grup üyeliklerini** dikey penceresinde, bir grup seçin.
9. Merhaba üzerinde ***groupname*** dikey penceresinde, select hello **kaldırmak** komut ve hello isteminde Seçiminizi onaylayın.

   ![Üyelik komutu kaldırın](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. Grubunuz için grup üyeliklerini değiştirme işiniz bittiğinde, seçin **kaydetmek**.

## <a name="additional-information"></a>Ek bilgiler
Bu makalelerde Azure Active Directory ile ilgili ek bilgi sağlanmıştır.

* [Var olan grupları bakın](active-directory-groups-view-azure-portal.md)
* [Yeni bir grup oluşturun ve üye ekleme](active-directory-groups-create-azure-portal.md)
* [Bir grubu ayarlarını yönetme](active-directory-groups-settings-azure-portal.md)
* [Bir grubun üyelerini yönetmek](active-directory-groups-members-azure-portal.md)
* [Bir gruptaki kullanıcılar için dinamik kurallarını yönet](active-directory-groups-dynamic-membership-azure-portal.md)
