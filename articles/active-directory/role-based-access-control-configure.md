---
title: "hello Azure portalı içinde aaaRole tabanlı erişim denetimi | Microsoft Docs"
description: "Erişim Yönetimi'nde hello Azure Portal'ın rol tabanlı erişim denetimi ile çalışmaya başlayın. Rol atamaları tooassign izinleri tooyour kaynağı kullanın."
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 8078f366-a2c4-4fbb-a44b-fc39fd89df81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: b87e00089b0fc93fb212b318330a6f22bfbf59e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-role-based-access-control-toomanage-access-tooyour-azure-subscription-resources"></a>Rol tabanlı erişim denetimi toomanage erişim tooyour Azure aboneliği kaynakları kullanın
> [!div class="op_single_selector"]
> * [Kullanıcı veya gruba göre erişimi yönetme](role-based-access-control-manage-assignments.md)
> * [Kaynağa göre erişimi yönetme](role-based-access-control-configure.md)

Azure Rol Tabanlı Erişim Denetimi (RBAC), Azure için ayrıntılı erişim yönetimi sağlar. RBAC kullanarak, kullanıcıların işlerini tooperform gerektiğini yalnızca hello erişim miktarını verebilirsiniz. Bu makalede, hello Azure portalında RBAC ile başlamak ve çalıştırmak yardımcı olur. RBAC'nin erişimi yönetmenize nasıl yardımcı olduğu konusunda daha fazla bilgi isterseniz bkz. [Rol Tabanlı Erişim Denetimi Nedir?](role-based-access-control-what-is.md).

Her abonelik içinde too2000 rol atamalarını verebilirsiniz. 

## <a name="view-access"></a>Erişimi görüntüleme
Hello erişim tooa kaynak, kaynak grubuna veya aboneliğe da ana dikey olanların görebilirsiniz [Azure portal](https://portal.azure.com). Örneğin, erişim tooone bizim kaynak grubuna sahip toosee isteyebilirsiniz:

1. Seçin **kaynak grupları** hello sol gezinti çubuğunda hello.  
    ![Kaynak grupları - simge](./media/role-based-access-control-configure/resourcegroups_icon.png)
2. Merhaba hello kaynak grubundan SELECT hello adını **kaynak grupları** dikey.
3. Seçin **erişim denetimi (IAM)** hello sol menüden.  
4. Merhaba erişim denetimi dikey tüm kullanıcılar, gruplar ve erişim toohello kaynak grubuna verilen uygulamaları listeler.  
   
    ![Kullanıcılar dikey penceresi - devralınmış veya atanmış erişim ekran görüntüsü](./media/role-based-access-control-configure/view-access.png)

Bazı roller çok kapsamlı fark**bu kaynak** diğerleri çalışırken **devralınan** başka bir kapsamda ondan. Erişim özellikle toohello kaynak grubuna atanmış veya bir atama toohello üst abonelikten devralındı.

> [!NOTE]
> Klasik abonelik yöneticileri ve ortak Yöneticiler hello abonelik sahipleri hello yeni RBAC modelinde olarak kabul edilir.

## <a name="add-access"></a>Erişim Ekleme
Merhaba kaynak, kaynak grubu veya hello rol ataması hello kapsamı abonelik içinden erişim verin.

1. Seçin **Ekle** hello erişim denetimi dikey.  
2. Select hello rol hello gelen tooassign istediğiniz **bir rol seçin** dikey.
3. Dizininizde toogrant erişmesini istediğiniz Hello kullanıcı, Grup veya uygulamayı seçin. Merhaba directory görünen adları, e-posta adresleri ve nesne tanımlayıcıları ile arama yapabilirsiniz.  
   
    ![Kullanıcı ekle dikey penceresi - arama ekran görüntüsü](./media/role-based-access-control-configure/grant-access2.png)
4. Seçin **Tamam** toocreate hello atama. Merhaba **kullanıcı ekleme** açılan hello ilerleme durumunu izler.  
    ![Kullanıcı ekleniyor ilerleme çubuğu - ekran görüntüsü](./media/role-based-access-control-configure/addinguser_popup.png)

Bir rol ataması başarıyla eklendikten sonra üzerinde hello görüneceği **kullanıcılar** dikey.

## <a name="remove-access"></a>Erişimi Kaldırma
1. İmlecinizi tooremove istediğiniz hello atama hello adın üzerine gelin. Bir onay kutusu sonraki toohello adı görüntülenir.
2. Merhaba onay kutularını tooselect kullanan bir veya daha fazla rol atamaları.
2. **Kaldır**’ı seçin.  
3. Seçin **Evet** tooconfirm hello kaldırma.

Devralınmış atamalar kaldırılamaz. Tooremove devralınan atama gerekiyorsa, hello adresinden kapsam hello rol ataması oluşturulduğu toodo gerekir. Merhaba, **kapsam** sütun, sonraki çok**devralınan** burada bu rolü atandı toohello kaynakları götüren bir bağlantı. Bu listede toohello kaynak Git tooremove hello rol ataması.

![Kullanıcılar dikey penceresi - devralınmış erişim kaldır düğmesini devre dışı bırakır ekran görüntüsü](./media/role-based-access-control-configure/remove-access2.png)

## <a name="other-tools-toomanage-access"></a>Diğer araçlar toomanage erişim
Roller atayabilir ve hello Azure portal dışındaki araçlarda Azure RBAC komutları ile erişimi yönetin.  Merhaba bağlantılar toolearn hello önkoşulları hakkında daha fazla izleyin ve hello Azure RBAC komutlarını kullanmaya başlayın.

* [Azure PowerShell](role-based-access-control-manage-access-powershell.md)
* [Azure Komut Satırı Arabirimi](role-based-access-control-manage-access-azure-cli.md)
* [REST API](role-based-access-control-manage-access-rest.md)

## <a name="next-steps"></a>Sonraki Adımlar
* [Erişim değişiklik geçmişi raporu oluşturma](role-based-access-control-access-change-history-report.md)
* Merhaba bkz [RBAC yerleşik rolleri](role-based-access-built-in-roles.md)
* Kendiniz için [Azure RBAC'de özel roller](role-based-access-control-custom-roles.md) tanımlama

