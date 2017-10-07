---
title: "aaaUpdate Azure Azure Automation modülleri | Microsoft Docs"
description: "Bu makalede, Azure automation'da varsayılan olarak sağlanan ortak Azure PowerShell modülleri nasıl şimdi güncelleştirebilirsiniz açıklanmaktadır."
services: automation
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: tysonn
ms.assetid: 
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2017
ms.author: magoedte
ms.openlocfilehash: afa404a643349f044e55be2280e435b575049dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-azure-powershell-modules-in-azure-automation"></a>Nasıl tooupdate Azure PowerShell modülleri Azure Automation

Merhaba en yaygın Azure PowerShell modülleri, varsayılan olarak her Automation hesabı sağlanır.  Yeni sürümler hello portalından kullanılabilir olduğunda hello Otomasyon hesabı şekilde sizin için tooupdate hello modülleri hello hesabındaki sağladığımız şekilde hello Azure ekibi güncelleştirmeleri düzenli olarak Azure modülleri hello.  

Modülleri hello ürün grubu tarafından düzenli olarak güncelleştirilen çünkü değişiklikler değişimin parametre yeniden adlandırma veya tamamen bir cmdlet onaysız kılınmadan gibi hello türüne bağlı olarak, runbook'ları olumsuz yönde etkileyebilir dahil hello cmdlet'leri oluşabilir. runbook'larınızı ve hello etkileyen tooavoid bunlar süreçlerini otomatikleştirmek, test ve doğrulama devam etmeden önce kesinlikle önerilir.  Hedeflenen bu amaç için adanmış bir Otomasyon hesabı yoksa, böylece hello güncelleştirme gibi ek tooiterative değişiklikleri, runbook'ların hello geliştirme sırasında birçok farklı senaryolar ve permütasyon sınayabilirsiniz bir oluşturmayı düşünün PowerShell modülleri.  Merhaba sonuçları doğrulanır ve gereken değişiklikleri uyguladığınız sonra değiştirilmesi gereken runbook'ları hello geçişini Eşgüdümleme ile devam etmek ve üretimde aşağıda açıklandığı gibi hello güncelleştirme gerçekleştirin.     

## <a name="updating-azure-modules"></a>Azure modülleri güncelleştiriliyor

1. Merhaba modülleri Automation hesabınız var. dikey olarak adlandırılan bir seçenektir **Update Azure modülleri**.  Her zaman etkindir.<br><br> ![Azure modülleri seçeneği modülleri dikey penceresinde Güncelleştir](media/automation-update-azure-modules/automation-update-azure-modules-option.png)

2. Tıklatın **Update Azure modülleri** ve toocontinue isteyip istemediğinizi soran bir onay bildirimi görürsünüz.<br><br> ![Azure modülleri bildirim güncelleştir](media/automation-update-azure-modules/automation-update-azure-modules-popup.png)

3. Tıklatın **Evet** ve hello modülü güncelleştirme işlemi başlayacak.  Merhaba güncelleştirme işlemini modülleri aşağıdaki 15-20 dakika tooupdate hello hakkında alır:

  * Azure
  * Azure Depolama
  * AzureRm.Automation
  * AzureRm.Compute
  * AzureRm.Profile
  * AzureRm.Resources
  * AzureRm.Sql
  * AzureRm.Storage

    Merhaba modülleri toodate zaten varsa, hello işlemini birkaç saniye içinde tamamlanır.  Merhaba güncelleştirme işlemi tamamlandığında size bildirilecek.<br><br> ![Azure modülleri güncelleştirme durumunu güncelleştir](media/automation-update-azure-modules/automation-update-azure-modules-updatestatus.png)

> [!NOTE]
> Yeni bir zamanlanan iş çalıştırdığınızda azure Automation Otomasyon hesabınızda hello son modülleri kullanın.    

Cmdlet'leri kullanıyorsanız, runbook'ları toomanage Azure içinde bu Azure PowerShell modüllerden kaynakları, sonra tooperform Bu güncelleştirme işlemi her ay veya isteyecektir böylece elinizde tooassure hello son modüller.

## <a name="next-steps"></a>Sonraki adımlar

* Tümleştirme modülleri ve nasıl toocreate özel modüller toofurther tümleştirmek Otomasyon diğer sistemler, hizmetleri veya çözümleri hakkında daha fazla toolearn bkz [tümleştirme modülleri](automation-integration-modules.md).

* Kaynak denetimi tümleştirmesi kullanmayı [GitHub Kurumsal](automation-scenario-source-control-integration-with-github-ent.md) veya [Visual Studio Team Services](automation-scenario-source-control-integration-with-vsts.md) toocentrally yönetmek ve denetlemek Otomasyon runbook ve yapılandırma Portföy sürümleri.  
