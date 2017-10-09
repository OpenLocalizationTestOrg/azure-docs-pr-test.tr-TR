---
title: Windows PowerShell'de Azure bulut hizmeti aaaScale | Microsoft Docs
description: "(Klasik) Bilgi nasıl toouse PowerShell tooscale bir web rolü veya içinde veya azure'da çalışan rolü."
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: ee37dd8c-6714-4c61-adb8-03d6bbf76c9a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: mmccrory
ms.openlocfilehash: cfac6660e84f8ae24e4e9bdd5bf2016fb9cd7045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-a-cloud-service-in-powershell"></a>Nasıl tooscale bir bulut hizmeti PowerShell'de

Ekleyerek veya kaldırarak örnekleri, bir web rolü veya çalışan rolü veya Windows PowerShell tooscale kullanabilirsiniz.  

## <a name="log-in-tooazure"></a>İçinde tooAzure oturum

Aboneliğinizi PowerShell aracılığıyla herhangi bir işlem gerçekleştirmeden önce oturum gerekir:

```powershell
Add-AzureAccount
```

Hesabınızla ilişkili birden çok aboneliğiniz varsa, bulut hizmetinizin bulunduğu bağlı olarak toochange hello geçerli abonelik gerekebilir. toocheck hello geçerli abonelik, çalıştırın:

```powershell
Get-AzureSubscription -Current
```

Toochange hello geçerli abonelik gerekiyorsa, çalıştırın:

```powershell
Set-AzureSubscription -SubscriptionId <subscription_id>
```

## <a name="check-hello-current-instance-count-for-your-role"></a>Merhaba geçerli örnek sayısını rolünüz için denetleyin

toocheck hello geçerli durumunu sizin rolünüz çalıştırın:

```powershell
Get-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>'
```

Geçerli işletim sistemi sürümü ve örneğindeki sayımına dahil hello rolünün hakkında bilgi geri almanız gerekir. Bu durumda, tek bir örnek hello rolüne sahip.

![Merhaba rolü hakkında bilgi](./media/cloud-services-how-to-scale-powershell/get-azure-role.png)

## <a name="scale-out-hello-role-by-adding-more-instances"></a>Daha fazla örnekleri ekleyerek Hello rolünün ölçeğini genişletme

tooscale rolünüze çıkışı geçişi hello istenen örneklerinin sayısını hello olarak **sayısı** parametresi toohello **kümesi AzureRole** cmdlet:

```powershell
Set-AzureRole -ServiceName '<your_service_name>' -RoleName '<your_role_name>' -Slot <target_slot> -Count <desired_instances>
```

Merhaba cmdlet blokları hello yeni örnekleri sırasında kısa bir süre içinde sağlanan ve başlatıldı. Yeni bir PowerShell penceresi ve çağrı açarsanız, bu süre boyunca **Get-AzureRole** daha önce gösterildiği gibi hello yeni hedef örneği sayısını görürsünüz. Ve hello rol durumu hello portalında inceleyin, başlamasını hello yeni örnek görmelisiniz:

![VM örneği portalında başlatılıyor](./media/cloud-services-how-to-scale-powershell/role-instance-starting.png)

Merhaba yeni örnekleri başladıktan sonra hello cmdlet başarıyla döndürür:

![Rol örneği artış başarılı](./media/cloud-services-how-to-scale-powershell/set-azure-role-success.png)

## <a name="scale-in-hello-role-by-removing-instances"></a>Ölçek kaldırarak hello rolü örnekleri

Hello örnekleri kaldırarak bir rolde ölçeklendirebilirsiniz aynı şekilde. Kümesi hello **sayısı** parametresini **kümesi AzureRole** toohello numarası örneklerini hello ölçek işleminde tamamlandıktan sonra toohave istiyor.

## <a name="next-steps"></a>Sonraki adımlar

PowerShell bulut hizmetlerinden için olası tooconfigure otomatik ölçek olmadığı. bkz, toodo [nasıl tooauto ölçeklendirme bir bulut hizmeti](cloud-services-how-to-scale-portal.md).
