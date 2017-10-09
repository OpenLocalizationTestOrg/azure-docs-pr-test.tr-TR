---
title: "Kaynak ilkeleri için aaaAzure portalı | Microsoft Docs"
description: "Açıklar nasıl toouse Azure portal toocreate Resource Manager ilkeleri ve yönetin. Merhaba abonelik veya kaynak gruplarının ilkeleri uygulanabilir."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: tomfitz
ms.openlocfilehash: ce6413386317e532b63761a24458b85c996af4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-tooassign-and-manage-resource-policies"></a>Azure portal tooassign kullanın ve kaynak ilkelerini yönetme
Hello Azure portal, tooassign kaynak ilkeleri tooresource grupları ve abonelikleri etkinleştirir. Merhaba kullanıcı arabirimi tooassign istediğiniz ve o İlkesi toocustomize hello İlkesi ayarları için parametre değerlerini belirtin kolay tooselect hello İlkesi kolaylaştırır. 

tooassign İlkesi hello portal aracılığıyla, hello ilke tanımı önceden aboneliğinizde var olmalıdır. Aboneliğiniz, tooassign tooresource gruplar veya abonelikler için hazır olan birkaç yerleşik ilke tanımları sahip. Bu yerleşik ilkeleri ve hello portal tooassign ilkeleri kullanırken tanımladığınız tüm özel ilkeler bakın. Bir giriş toopolicies ve nasıl toodefine özelleştirilmiş ilke için bkz: [kaynak ilkesine genel bakış](resource-manager-policy.md).

İlkeler tüm alt kaynaklar tarafından devralınır. Bu nedenle, bir ilke uygulanmış tooa kaynak grubu ise, uygun tooall hello kaynakların kaynak grubunda olur. Bu makalede, hello terim **kapsam** toohello kaynak grubu veya hello İlkesi atanmış abonelik başvuruyor. 

İlkeleri oluşturma ve (PUT ve işlemleri düzeltme eki) kaynakları güncelleştirme değerlendirilir.

## <a name="assign-a-policy"></a>Bir ilke atama

1. tooassign İlkesi tooeither bir kaynak grubu veya abonelik, bu kaynak grubuna veya aboneliğe seçin. Hello Ayarları'nda seçin **ilkeleri**.

   ![İlkeleri'ni seçin](./media/resource-manager-policy-portal/select-policies.png)

2. toocreate bu kapsam için bir ilke atamasını seçin **atama Ekle**.

   ![atama Ekle](./media/resource-manager-policy-portal/add-assignment.png)

3. Tooassign hello ilkeyi seçin. Herhangi bir ilke tanımları tooyour abonelik eklemediniz olsa bile atama için uygun olan yerleşik ilkeleri hello bakın. Bu yerleşik ilkeleri birçok yaygın senaryolar kapsar.

   ![tanımı seçin](./media/resource-manager-policy-portal/select-definition.png)

4. Bir ilke seçildikten sonra bu ilkeye herhangi bir parametre ve bir açıklama hello İlkesi bakın. Örneğin, hello aşağıdaki görüntüde hello gösterir **konumları izin** hello kullanılabilir konumlarını kısıtlayan hello ilkesi için gerekli olan parametre.

   ![Parametreleri Göster](./media/resource-manager-policy-portal/show-parameters.png)

5. Merhaba kullanıcı arabirimi aracılığıyla hello değerleri toospecify hello İlkesi parametreler (örneğin, dağıtım için kullanılan hello konumları) için seçin.

   ![parametre değerlerini seçin](./media/resource-manager-policy-portal/select-parameters.png)

6. Değerleri hello için diğer parametreler girin. Merhaba kapsam hello dikey penceresinde hello ilke ataması başlatırken seçili otomatik olarak atanır. Tamamladığınızda **Tamam**’ı seçin.

   ![parametrelerini tanımlayın](./media/resource-manager-policy-portal/define-parameters.png)

  Hello İlkesi atadığınız toohello Belirtilen kapsam.

## <a name="view-policy-assignments"></a>İlke atamalarını görüntülemek

Bir ilke atadıktan sonra bu kapsam için ilke hello listesi konusuna bakın. Merhaba **ayrıntıları** sekmesi hello ilke ataması özetini gösterir.

![Ayrıntıları Göster](./media/resource-manager-policy-portal/show-details.png)

Merhaba **atama kuralı** sekmesi hello JSON hello ilke tanımı için gösterir.

![atama kuralı Göster](./media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a>Var olan bir ilke atamasını değiştirin

toochange bir ilke seçin **Düzenle atama** veya **Sil**

![düzenleme veya silme atama](./media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a>Özel ilkeler atayın

Özel ilkeler, aboneliğinizde tanımladıysanız, bu ilkeleri hello portal aracılığıyla kullanılabilir. Bu ilkeleri ile başlayan **[özel]**

![özel ilkeler](./media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a>Sonraki adımlar
* toolearn ilkelerini tanımlamak için hello JSON söz dizimi hakkında bkz [kaynak ilkesine genel bakış](resource-manager-policy.md).
* Kuruluşların Resource Manager tooeffectively nasıl kullanabileceğiniz hakkında rehberlik için abonelikleri yönetmek için bkz: [Azure enterprise iskele - Düzenleyici abonelik idare](resource-manager-subscription-governance.md).
* Hello İlkesi Şema konumunda yayımlanır [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json). 

