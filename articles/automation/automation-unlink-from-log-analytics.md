---
title: "Azure Otomasyon hesabı günlük analizi aaaUnlink | Microsoft Docs"
description: "Bu makalede nasıl toounlink Azure Automation'ınızı hesap bir OMS çalışma alanından genel bir bakış sağlar."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: how-to-article
ms.date: 02/07/2017
ms.author: magoedte
ms.openlocfilehash: 3ec0745673f6a872538d33023a7a1d2bb1d18ec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toounlink-your-automation-account-from-a-log-analytics-workspace"></a>Nasıl toounlink, Otomasyon hesabı günlük analizi çalışma alanından

Azure Otomasyonu günlük analizi toonot yalnızca öngörülü, runbook işleri tüm Automation hesapları arasında izleme desteği ile tümleştirilir, ancak günlük analizi bağımlı çözümleri aşağıdaki hello içeri aktardığınızda de gereklidir:

* [Güncelleştirme yönetimi](../operations-management-suite/oms-solution-update-management.md)
* [Değişiklik İzleme](../log-analytics/log-analytics-change-tracking.md)
* [Yoğun olmayan saatlerde sırasında Başlat/Durdur VM'ler](automation-solution-vm-management.md)
 
Günlük analizi ile Automation hesabınız artık toointegrate istediğiniz karar verirseniz, hesabınızdan doğrudan hello Azure portal bağlantısını kaldırabilirsiniz.  Devam etmeden önce bu işlemin devam etmesini Aksi takdirde engellenir, daha önce bahsedilen tooremove hello çözümleri ilk gerekir.  Gözden geçirme hello konu hello belirli çözüm için gereken toounderstand hello adımları aktardığınız tooremove onu.  

Bu çözümlerin kaldırdıktan sonra aşağıdaki adımları toounlink hello Automation hesabınız gerçekleştirebilirsiniz.

## <a name="unlink-workspace"></a>Çalışma alanı bağlantısını Kaldır

1. Hello Azure portal, Automation hesabınızı açın ve hello Otomasyon hesabı dikey penceresinde hello hesabı dikey penceresinde, seçin **çalışma bağlantısını**.<br><br> ![Çalışma alanı seçeneği bağlantısını Kaldır](media/automation-unlink-from-log-analytics/automation-unlink-workspace-option.png)<br><br>  
2. Merhaba Bağlantıyı Kes'i çalışma dikey penceresinde **worksapce bağlantısını**.<br><br> ![Çalışma alanı dikey bağlantısını](media/automation-unlink-from-log-analytics/automation-unlink-workspace-blade.png).<br><br>  Tooproceed istediğiniz doğrulayan bir ileti alırsınız.<br><br>
3. Azure Otomasyonu toounlink hello hesabı günlük analizi çalışma alanınız çalışır, ancak altında hello ilerleme durumunu izleyebilirsiniz **bildirimleri** hello menüsünde.

İsteğe bağlı olarak hello güncelleştirme yönetimi çözümü kullandıysanız, hello çözüm kaldırdıktan sonra artık gerekli olmayan öğeleri aşağıdaki tooremove hello isteyebilirsiniz.

* Zamanlamaları güncelleştirin.  Her oluşturduğunuz hello güncelleştirme dağıtımları eşleşen adlara sahip olacaktır)

* Karma çalışan grupları Hello çözüm için oluşturulan.  Her benzer şekilde çok adlandırılacağını machine1.contoso.com_9ceb8108 - 26 c 9-4051-b6b3-227600d715c8).

İsteğe bağlı olarak sırasında yoğun olmayan saatlerde çözüm hello Başlat/Durdur VM'ler kullandıysanız, hello çözüm kaldırdıktan sonra artık gerekli olmayan öğeleri aşağıdaki tooremove hello isteyebilirsiniz.

* Başlatma ve durdurma VM runbook zamanlama 
* Başlatma ve VM runbook'ları durdurun
* Değişkenler   

## <a name="next-steps"></a>Sonraki adımlar

OMS günlük analizi ile Otomasyon hesabı toointegrate tooreconfigure bkz [Otomasyon tooLog analizi (OMS) iş durumu ve iş akışları iletmek](automation-manage-send-joblogs-log-analytics.md). 
