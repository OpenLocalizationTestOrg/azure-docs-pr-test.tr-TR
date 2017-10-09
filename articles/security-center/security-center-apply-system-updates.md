---
title: "Azure Güvenlik Merkezi'nde aaaApply sistem güncelleştirmelerini | Microsoft Docs"
description: "Bu belge size nasıl tooimplement hello Azure Güvenlik Merkezi önerilerini gösterir. ** Sistem güncelleştirmeleri ** uygulamak ve ** sistem güncelleştirmeleri ** sonra yeniden başlatın."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: e5bd7f55-38fd-4ebb-84ab-32bd60e9fa7a
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/03/2017
ms.author: terrylan
ms.openlocfilehash: 02024f1558b4758c09141fe1934c2e1a9845cc96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a>Azure Güvenlik Merkezi'nde sistem güncelleştirmeleri uygulama
Azure Güvenlik Merkezi, Windows ve Linux işletim sistemi güncelleştirmeleri eksik makineleri (VM'ler) günlük izler. Güvenlik Merkezi hizmeti bağlı olarak bir Windows VM üzerinde yapılandırıldığı Windows Update veya Windows Server Update Services (WSUS) kullanılabilir güvenlik ve kritik güncelleştirmeler listesini alır.  Güvenlik Merkezi, ayrıca Linux sistemlerinde hello en son güncelleştirmeleri denetler. VM'yi bir sistem güncelleştirmesi eksikse, Güvenlik Merkezi sistem güncelleştirmeleri uygulamanızı önerir

> [!NOTE]
> Bu belge, örnek bir dağıtım kullanarak hello hizmeti sunar.  Bu, adım adım ilerleyen bir kılavuz değildir.
>
>

## <a name="implement-hello-recommendation"></a>Merhaba öneriyi uygulamayı
1. Merhaba, **önerileri** dikey penceresinde, select **sistem güncelleştirmelerini**.

   ![Sistem güncelleştirmelerini uygulayın][1]
2. Merhaba **sistem güncelleştirmelerini** eksik sistem güncelleştirmeleri VM'ler listesini görüntüleyen dikey pencere açılır. Bir VM'yi seçin.

   ![Bir VM seçin][2]
3. Bu VM için eksik güncelleştirmelerin listesini görüntüleyen bir dikey pencere açılır. Bir Sistem Güncelleştirmesi'ni seçin. Bu örnekte, şimdi KB3156016 seçin.

   ![Eksik güvenlik güncelleştirmelerini][3]

4. Merhaba Hello adımları **güvenlik güncelleştirmesi** dikey tooapply hello eksik güncelleştirme.

   ![Güvenlik güncelleştirmesi][4]

## <a name="reboot-after-system-updates"></a>Sistem güncelleştirmelerinden sonra yeniden başlatın
1. Toohello iade **önerileri** dikey. Adlı Sistem güncelleştirmeleri uygulandıktan sonra yeni bir giriş oluşturulan **sonra sistem güncelleştirmelerini yeniden**. Bu giriş, sistemi güncelleştirmelerini uygulama tooreboot hello VM toocomplete hello işlemi gereksinim bilmenizi sağlar.

   ![Sistem güncelleştirmelerinden sonra yeniden başlatın][5]
2. Seçin **sonra sistem güncelleştirmelerini yeniden**. Bu açılır **bir yeniden başlatma beklemede toocomplete sistem güncelleştirmelerini var** toorestart toocomplete hello gereken sanal makineleri listesini görüntüleyen dikey sistem güncelleştirmeleri işlemi uygulayın.

   ![Beklemedeki yeniden başlatma][6]

Azure toocomplete hello işleminden Hello VM yeniden başlatın.

## <a name="see-also"></a>Ayrıca bkz.
Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) --öğrenin nasıl tooconfigure Azure Abonelikleriniz ve kaynak grupları için güvenlik ilkeleri.
* [Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) --nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.
* [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) --nasıl toomonitor hello Azure kaynaklarınızın sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi'nde Uyarıları yönetme ve yanıt toosecurity](security-center-managing-and-responding-alerts.md) --öğrenin nasıl toomanage ve yanıt toosecurity uyarıları.
* [Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) --nasıl toomonitor hello iş ortağı çözümlerinizin sistem durumunu öğrenin.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) --hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
* [Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) --Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
