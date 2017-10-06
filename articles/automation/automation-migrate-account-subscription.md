---
title: "aaaMigrate Automation hesaplarına ve kaynaklarına | Microsoft Docs"
description: "Bu makalede nasıl toomove bir Automation hesabı Azure Automation ve ilişkili kaynakları bir abonelik tooanother açıklanmaktadır."
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9c2db4a2-f324-48dc-8ce7-3343bf7230d5
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/21/2016
ms.author: magoedte
ms.openlocfilehash: 201c9091cd2d78d7ea407c1e5fb27f366bb4fa8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-automation-account-and-resources"></a>Otomasyon hesabı ve kaynakları geçirme
Automation hesapları ve hello Azure portal oluşturulup istediğiniz ilişkili kaynaklarını (yani varlıklar, runbook'ları, modüller, vb.) için bir kaynaktan toomigrate Grup tooanother veya bir abonelik tooanother bunu kolayca gerçekleştirebilirsiniz Merhaba [kaynakları taşımak](../azure-resource-manager/resource-group-move-resources.md) özelliği hello Azure portalında kullanılabilir. Ancak, bu eylemle devam etmeden önce ilk hello aşağıdakileri gözden geçirmeniz gereken [kaynakları geçmeden önce denetim listesi](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) ve ayrıca, belirli tooAutomation aşağıdaki hello liste.   

1. Merhaba hedef abonelik/kaynak grubu hello kaynağı olarak aynı bölgede olması gerekir.  Yani, Automation hesapları bölgeler arasında taşınamaz.
2. Kaynakları (örneğin runbook'ları, işleri, vb.) taşırken hello kaynak grubu ve hello hedef grubu hello hello işlemi süresince kilitlenir. Yazma ve silme işlemleri hello taşıma işlemi tamamlanana kadar hello gruplarında engellenir.  
3. Herhangi bir runbook'ları veya bir kaynak veya abonelik kimliği hello varolan abonelikten başvuran değişkenler geçiş tamamlandıktan sonra güncelleştirilmiş toobe gerekir.   

> [!NOTE]
> Bu özellik, taşıma Klasik automation kaynaklarını desteklemez.
>
>

## <a name="toomove-hello-automation-account-using-hello-portal"></a>toomove hello hello portal kullanarak Automation hesabını
1. Otomasyon hesabınızdan tıklatın **taşıma** hello dikey penceresinde hello üstünde.<br> ![Seçeneği taşıyın](media/automation-migrate-account-subscription/automation-menu-move.png)<br>
2. Merhaba üzerinde **taşıma kaynakları** dikey penceresinde, Automation hesabınızı ve kaynak gruplarını, kaynakları ilgili tooboth yansıtacak şekilde Not.  Select hello **abonelik** ve **kaynak grubu** hello açılan listeleri ya da select hello seçeneği **yeni bir kaynak grubu oluşturma** ve yeni bir kaynak grubu adı girin sağlanan hello alanı.  
3. Gözden geçirme ve seçme hello onay kutusunu tooacknowledge, *araçları ve komut dosyaları anlamanıza gerek güncelleştirilmiş toobe toouse yeni kaynak kaynakları taşındıktan sonra kimlikleri* ve ardından **Tamam**.<br> ![Kaynaklar dikey taşıma](media/automation-migrate-account-subscription/automation-move-resources-blade.png)<br>   

Bu işlem birkaç dakika toocomplete sürer.  İçinde **bildirimleri**, - doğrulama, geçiş, gerçekleşir her eylem durumuyla sunulur ve ardından son olarak, bu tamamlandı.     

## <a name="toomove-hello-automation-account-using-powershell"></a>toomove hello PowerShell kullanarak Automation hesabını
toomove var olan Otomasyon kaynakları tooanother kaynak grubu veya abonelik hello kullanın, **Get-AzureRmResource** cmdlet tooget hello belirli Otomasyon hesabı ve ardından **taşıma AzureRmResource** cmdlet tooperform hello taşıyın.

Merhaba ilk örneği, nasıl toomove bir Otomasyon hesabı tooa yeni kaynak grubu gösterir.

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

Yukarıdaki kod örneğinde hello yürüttükten sonra bu eylem tooperform istediğiniz istendiğinde tooverify olacaktır.  Tıkladığınızda **Evet** ve izin betik tooproceed Merhaba, hello geçiş yaparken, herhangi bir bildirim alırsınız.  

toomove tooa yeni abonelik, hello için bir değer dahil *DestinationSubscriptionId* parametresi.

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

Merhaba önceki örnek olarak, istendiğinde tooconfirm hello taşıma olacaktır.  

## <a name="next-steps"></a>Sonraki adımlar
* Taşıma kaynakları toonew kaynak grubuna veya aboneliğe hakkında daha fazla bilgi için bkz: [kaynakları toonew kaynak grubuna veya aboneliğe taşıma](../azure-resource-manager/resource-group-move-resources.md)
* Azure automation'da rol tabanlı erişim denetimi hakkında daha fazla bilgi için çok başvuran[Azure automation'da rol tabanlı erişim denetimi](automation-role-based-access-control.md).
* Aboneliğinizi yönetmek için PowerShell cmdlet'leri hakkında toolearn bakın [Azure PowerShell'i Resource Manager ile kullanma](../azure-resource-manager/powershell-azure-resource-manager.md)
* Aboneliğinizi yönetmek için portal özellikleri hakkında toolearn bkz [hello Azure Portal toomanage kaynakları kullanarak](../azure-resource-manager/resource-group-portal.md).
