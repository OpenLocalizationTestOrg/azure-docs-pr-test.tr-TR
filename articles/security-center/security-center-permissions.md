---
title: "Azure Güvenlik Merkezi'nde aaaPermissions | Microsoft Docs"
description: "Bu makalede Azure Güvenlik Merkezi rol tabanlı erişim denetimi tooassign izinleri toousers nasıl kullandığı açıklanmıştır ve Eylemler her rol için izin verilen hello tanımlar."
services: security-center
cloud: na
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
ms.assetid: 
ms.service: security-center
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: terrylan
ms.openlocfilehash: 03e16132dc3d951ef8ad9e86b9970b9e4d15c76b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-in-azure-security-center"></a>Azure Güvenlik Merkezi'nde izinleri

Azure Güvenlik Merkezi kullanan [rol tabanlı erişim denetimi (RBAC)](../active-directory/role-based-access-control-configure.md), sağlayan [yerleşik roller](../active-directory/role-based-access-built-in-roles.md) atanabilen toousers, grupları ve Azure Hizmetleri.

Güvenlik Merkezi kaynakları tooidentify güvenlik sorunları ve güvenlik açıkları hello yapılandırmasını değerlendirir. Güvenlik Merkezi'nde, yalnızca bilgi sahibi, katkıda bulunan veya okuyucu bir kaynağa ait hello abonelik veya kaynak grubu için hello rolüne atandığında ilgili tooa kaynak.

Toplama toothese rollerinde iki belirli Güvenlik Merkezi rolü vardır:

* **Güvenlik okuyucu**: toothis role ait olan bir kullanıcı hakları tooSecurity merkezi görüntüleme sahiptir. Merhaba kullanıcı öneriler, uyarılar, bir güvenlik ilkesi ve güvenlik durumları görüntüleyebilir ancak değişiklik yapamazsınız.
* **Güvenlik Yöneticisi**: toothis rolüne ait kullanıcı aynı hakları güvenlik okuyucu hello hello sahip ve aynı zamanda hello güvenlik ilkesi güncelleştirebilir ve uyarısı ve öneri yok sayın.

> [!NOTE]
> Merhaba güvenlik rolleri, güvenlik okuyucu ve Güvenlik Yöneticisi, yalnızca Güvenlik Merkezi'nde erişebilirsiniz. Merhaba güvenlik rolleri Azure depolama, Web ve mobil veya nesnelerin interneti gibi erişim tooother hizmet alanlarına sahip değilsiniz.
>
>

## <a name="roles-and-allowed-actions"></a>Rol ve izin verilen eylemleri

Merhaba aşağıdaki tabloda rollerini görüntüler ve Güvenlik Merkezi'nde Eylemler izin. Bir X hello eylem bu rol için izin verildiğini gösterir.

| Rol | Güvenlik ilkesini Düzenle | Bir kaynak için güvenlik önerilerini uygulama | Uyarılar ve öneriler kapatın | Uyarıları görüntüle ve öneriler |
|:--- |:---:|:---:|:---:|:---:|
| Abonelik sahibi | X | X | X | X |
| Abonelik katkıda bulunan | X | X | X | X |
| Kaynak grubunun sahibi | -- | X | -- | X |
| Kaynak grubu katkıda bulunan | -- | X | -- | X |
| Okuyucu | -- | -- | -- | X |
| Güvenlik Yöneticisi | X | -- | X | X |
| Güvenlik okuyucusu | -- | -- | -- | X |

> [!NOTE]
> Merhaba atamanızı öneririz az izin veren rol görevlerini kullanıcılar toocomplete için gerekli. Örneğin, bir kaynak hello güvenlik durumu hakkındaki bilgileri tooview yeterlidir ancak önerileri uygulamak veya ilkeleri düzenleme gibi bir eylemde bulunmamasını hello okuyucu rolü toousers atayın.
>
>

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, Güvenlik Merkezi RBAC tooassign izinleri toousers nasıl kullandığı açıklanmıştır ve Eylemler her rol için izin verilen hello tanımlanır. Toomonitor hello aboneliğinizi güvenlik durumunu hello rol atamalarını ile tanıdık, güvenlik ilkeleri, düzenleme ve önerileri geçerlidir, öğrenme nasıl yapılır:

- [Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md)
- [Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md)
- [Hello Azure kaynaklarınızın güvenlik durumunu izleme](security-center-monitoring.md)
- [Yönetme ve Güvenlik Merkezi'nde toosecurity uyarılarını yanıtlama](security-center-managing-and-responding-alerts.md)
- [İş ortağı güvenlik çözümlerini izleme](security-center-partner-solutions.md)
