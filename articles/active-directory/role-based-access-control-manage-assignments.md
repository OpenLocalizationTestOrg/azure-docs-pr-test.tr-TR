---
title: "aaaView Azure kaynak erişim atamalarını | Microsoft Docs"
description: "Görüntüleme ve herhangi bir kullanıcı veya grup hello Azure portal'ın tüm hello rol tabanlı erişim denetimi atamaları yönetme"
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: jeffsta
ms.assetid: e6f9e657-8ee3-4eec-a21c-78fe1b52a005
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: andredm
ms.openlocfilehash: ec96c9d4b9e2cb4925949b8bac78767bd564c8ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="view-access-assignments-for-users-and-groups-in-hello-azure-portal"></a>Kullanıcıları ve grupları hello Azure portalı için erişim atamalarını görüntüle
> [!div class="op_single_selector"]
> * [Kullanıcı veya gruba göre erişimi yönetme](role-based-access-control-manage-assignments.md)
> * [Kaynağa göre erişimi yönetme](role-based-access-control-configure.md)

Rol tabanlı erişim denetimi ile (RBAC) hello Azure Active Directory (Azure AD) içinde erişim tooyour Azure yönetebileceğiniz kaynakları. 

İki yolla hello izinleri kısıtla olduğundan ile RBAC atanmış erişim ayrıntılıdır:

* **Kapsam:** RBAC rolü atamalarını olan kapsamlı tooa belirli abonelik, kaynak grubu veya kaynak. Bir kullanıcı tarafından erişim tooa tek kaynak verilen hello alanındaki herhangi bir kaynağa erişemiyor aynı abonelik.
* **Rol:** hello atama hello kapsamında erişim daraltıldığı rol atama tarafından bile daha fazla. Rol sahibi gibi üst düzey ya da sanal makine okuyucu gibi belirli olabilir.

Roller yalnızca gelen hello abonelik, kaynak grubu veya hello kapsamı hello ataması için kaynak içinde atanabilir. Ancak tüm hello erişim atamalarını belirli bir kullanıcı veya grup için tek bir yerde görüntüleyebilirsiniz. Her abonelik too2000 rol atamalarında yukarı sahip olabilir. 

Çok hakkında daha fazla bilgi almak[rol atamalarını toomanage erişim tooyour Azure abonelik kaynaklarını kullanmak](role-based-access-control-configure.md).

## <a name="view-access-assignments"></a>Erişim atamalarını görüntüle
toolook tek bir kullanıcı veya grup için hello erişim atamalarını hello Azure Active Directory'de Başlat [Azure portal](http://portal.azure.com).

1. Seçin **Azure Active Directory**. Bu seçenek, gezinti listenizde görünür durumda değilse, seçin **daha Hizmetleri** toofind kaydırarak **Azure Active Directory**.
2. Seçin **kullanıcılar ve gruplar**ve sonra da **tüm kullanıcılar** veya **tüm grupları**. Bu örnekte, bireysel kullanıcılar odaklanın.
    ![Kullanıcıları ve grupları Azure Active Directory'de - ekran görüntüsü yönetin](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)
3. Merhaba kullanıcı adı veya kullanıcı adı tarafından arayın.
4. Seçin **Azure kaynaklarını** hello kullanıcı dikey. Bu kullanıcı için tüm hello erişim atamaları görüntülenir.

### <a name="read-permissions-tooview-assignments"></a>Okuma izinleri tooview atamaları
Bu sayfa yalnızca izin tooread sahip hello erişim atamalarını gösterir. Örneğin, okuma erişimi toosubscription bir sahip ve bir kullanıcının atamaları toohello Azure kaynaklarını dikey toocheck gidin. Bir abonelik için kendi erişim atamalarını görebilirsiniz, ancak kendisi de B. abonelikte erişim atamaları olduğunu göremez

## <a name="delete-access-assignments"></a>Erişim atamalarını silin
Bu dikey pencereden tooa kullanıcı veya grup doğrudan atanmış erişim atamalarını silebilirsiniz. Merhaba erişim atama üst gruptan devralınan, toogo toohello kaynak veya abonelik gerekir ve hello atama yönetin.

1. Bir kullanıcı veya grup için tüm hello erişim atamalarını Hello listeden toodelete istediğiniz hello birini seçin.
2. Seçin **kaldırmak** ve ardından **Evet** tooconfirm.
    ![Erişim atamayı - ekran görüntüsü](./media/role-based-access-control-manage-assignments/delete_assignment.png)

## <a name="next-steps"></a>Sonraki adımlar

* Rol tabanlı erişim denetimi ile çok başlamak[rol atamalarını toomanage erişim tooyour Azure aboneliği kaynakları kullanın](role-based-access-control-configure.md)
* Merhaba bkz [RBAC yerleşik rolleri](role-based-access-built-in-roles.md)

