---
title: "Otomasyon hesabı ve kaynakları geçirmek | Microsoft Docs"
description: "Bu makalede, Azure Automation ve ilişkili kaynakları Automation hesabında bir aboneliği taşımak açıklar."
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
ms.openlocfilehash: 687da15bdaf854254321b59350f47549781676f5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-automation-account-and-resources"></a>Otomasyon hesabı ve kaynakları geçirme
Automation hesapları ve Azure portalında oluşturduğunuz ve bir kaynak grubundan diğerine veya bir abonelik diğerine geçirmek istiyorsanız, ilişkili kaynakları (yani varlıklar, runbook'ları, modüller, vb.) için bunu kolayca gerçekleştirebilirsiniz [kaynakları taşımak](../azure-resource-manager/resource-group-move-resources.md) Özelliği Azure portalında kullanılabilir. Ancak, bu eylem işlemine devam etmeden önce önce aşağıdakileri gözden geçirmeniz gereken [kaynakları geçmeden önce denetim listesi](../azure-resource-manager/resource-group-move-resources.md#checklist-before-moving-resources) ve Otomasyon özgü ek olarak, aşağıdaki listeye.   

1. Hedef abonelik/kaynak grubu kaynağı olarak aynı bölgede olması gerekir.  Yani, Automation hesapları bölgeler arasında taşınamaz.
2. Kaynakları (örneğin runbook'ları, işleri, vb.) taşırken, hem kaynak grubu hem de hedef grup işlemi boyunca kilitlenir. Yazma ve silme işlemleri taşıma işlemi tamamlanana kadar gruplarında engellenir.  
3. Herhangi bir runbook'ları veya varolan abonelikten bir kaynak veya abonelik kimliği başvuran değişkenler, geçiş tamamlandıktan sonra güncelleştirilmesi gerekir.   

> [!NOTE]
> Bu özellik, taşıma Klasik automation kaynaklarını desteklemez.
>
>

## <a name="to-move-the-automation-account-using-the-portal"></a>Portal kullanarak Automation hesabını taşımak için
1. Otomasyon hesabınızdan tıklatın **taşıma** dikey pencerenin üstündeki.<br> ![Seçeneği taşıyın](media/automation-migrate-account-subscription/automation-menu-move.png)<br>
2. Üzerinde **taşıma kaynakları** dikey penceresinde, Automation hesabınız ve kaynak grubu ile ilgili kaynaklara sunar unutmayın.  Seçin **abonelik** ve **kaynak grubu** açılan listeleri ya da seçeneği **yeni bir kaynak grubu oluşturma** ve sağlanan alana yeni bir kaynak grubu adı girin.  
3. Gözden geçirin ve size kabul etmek için onay kutusunu işaretleyin *araçları anlamanız ve komut dosyaları kaynakları taşındıktan sonra yeni kaynak kimlikleri kullanacak şekilde güncelleştirilmesi gerekecek* ve ardından **Tamam**.<br> ![Kaynaklar dikey taşıma](media/automation-migrate-account-subscription/automation-move-resources-blade.png)<br>   

Bu eylemin tamamlanması birkaç dakika sürer.  İçinde **bildirimleri**, - doğrulama, geçiş, gerçekleşir her eylem durumuyla sunulur ve ardından son olarak, bu tamamlandı.     

## <a name="to-move-the-automation-account-using-powershell"></a>PowerShell kullanarak Automation hesabını taşımak için
Başka bir kaynak grubuna veya aboneliğe mevcut Automation kaynaklarını taşımak için kullanın **Get-AzureRmResource** cmdlet'ini belirli Otomasyonu hesabını alın ve ardından **taşıma AzureRmResource** taşımayı gerçekleştirmek için cmdlet.

İlk örnek bir Otomasyon hesabı yeni bir kaynak grubuna taşımak nasıl gösterir.

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup"
   ```

Yukarıdaki kod örneğinde yürüttükten sonra bu eylemi gerçekleştirmek istediğiniz doğrulamak için istenir.  Tıkladığınızda **Evet** ve devam etmek komut dosyası izin, geçiş işlemi gerçekleştirirken, herhangi bir bildirim alırsınız.  

Yeni bir aboneliği taşımak için bir değer dahil *DestinationSubscriptionId* parametresi.

   ```
    $resource = Get-AzureRmResource -ResourceName "TestAutomationAccount" -ResourceGroupName "ResourceGroup01"
    Move-AzureRmResource -ResourceId $resource.ResourceId -DestinationResourceGroupName "NewResourceGroup" -DestinationSubscriptionId "SubscriptionId"
   ```

Önceki örnekte olduğu gibi taşıma onaylamanız istenir.  

## <a name="next-steps"></a>Sonraki adımlar
* Kaynakları yeni kaynak grubuna veya aboneliğe taşıma hakkında daha fazla bilgi için bkz: [yeni kaynak grubu veya abonelik kaynaklarını taşıma](../azure-resource-manager/resource-group-move-resources.md)
* Azure Automation’da Rol Tabanlı Erişim Denetimi hakkında daha fazla bilgi için bkz. [Azure Automation’da rol tabanlı erişim denetimi](automation-role-based-access-control.md).
* Aboneliğinizi yönetmek için PowerShell cmdlet'leri hakkında bilgi edinmek için [Azure PowerShell'i Resource Manager ile kullanma](../azure-resource-manager/powershell-azure-resource-manager.md)
* Aboneliğinizi yönetmeye yönelik portal özellikleri hakkında bilgi edinmek için [kaynakları yönetmek için Azure Portalı'nı kullanarak](../azure-resource-manager/resource-group-portal.md).
