---
title: "Azure Active Directory'de kullanıcılar için bir grubu aaaCreate | Microsoft Docs"
description: "Nasıl toocreate Azure Active Directory'deki bir grup ve üye toohello grubu Ekle"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc583a7f02ce50e7f3b2c8f97a9c032a3e2dc33a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a>Bir grup oluşturun ve Azure Active Directory'de üye ekleme
> [!div class="op_single_selector"]
> * [Azure portal](active-directory-groups-create-azure-portal.md)
> * [Klasik Azure Portalı](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

Bu makalede açıklanır nasıl toocreate ve Azure Active Directory'de yeni bir grubu doldurur. Lisans veya izinleri tooa sayısı kullanıcılardan veya aygıtlardan aynı anda atama gibi bir grup tooperform yönetim görevleri kullanın.

## <a name="how-do-i-create-a-group"></a>Nasıl grup oluşturulur?
1. İçinde toohello oturum [Azure portal](https://portal.azure.com) hello dizin için genel yönetici olan bir hesapla.
2. Seçin **daha fazla hizmet**, girin **kullanıcı ve grupları** hello metin kutusuna ve ardından **Enter**.

   ![Açılış kullanıcı yönetimi](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. Merhaba üzerinde **kullanıcılar ve gruplar** dikey penceresinde, select **tüm grupları**.

   ![Açılış hello grupları dikey penceresi](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. Merhaba üzerinde **kullanıcılar ve gruplar - tüm grupları** dikey penceresinde, select hello **Ekle** komutu.

   ![Merhaba Ekle komutu seçme](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. Merhaba üzerinde **grup** dikey penceresinde, bir ad ve açıklama hello grubu ekleyin.
6. tooselect üyeleri tooadd toohello grubu, select **atanan** hello içinde **üyelik türü** kutusuna ve ardından **üyeleri**. Nasıl toomanage hello bir grubun üyeliğini dinamik olarak hakkında daha fazla bilgi için bkz: [öznitelikleri toocreate kullanarak Gelişmiş Grup üyeliği kuralları](active-directory-groups-dynamic-membership-azure-portal.md).

   ![Üyeleri tooadd seçme](./media/active-directory-groups-create-azure-portal/select-members.png)
7. Merhaba üzerinde **üyeleri** dikey penceresinde, seçin veya daha fazla kullanıcı veya cihazları tooadd toohello grubu ve select hello **seçin** hello hello dikey tooadd sonunda bunları toohello Grup düğme. Merhaba **kullanıcı** kutusunu filtreleri Merhaba, bir kullanıcı veya aygıt adı girişi tooany parçası eşleşmesini temel alan görüntüleme. Joker karakterler bu kutuya kabul edilir.
8. Üyeler toohello grubu eklemeyi bitirdiğinizde, seçin **oluşturma** hello üzerinde **grup** dikey.    

   ![Grubu onayı oluşturma](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a>Sonraki adımlar
Bu makalelerde Azure Active Directory ile ilgili ek bilgi sağlanmıştır.

* [Var olan grupları bakın](active-directory-groups-view-azure-portal.md)
* [Bir grubu ayarlarını yönetme](active-directory-groups-settings-azure-portal.md)
* [Bir grubun üyelerini yönetmek](active-directory-groups-members-azure-portal.md)
* [Bir grubun üyeliğini yönetme](active-directory-groups-membership-azure-portal.md)
* [Bir gruptaki kullanıcılar için dinamik kurallarını yönet](active-directory-groups-dynamic-membership-azure-portal.md)
