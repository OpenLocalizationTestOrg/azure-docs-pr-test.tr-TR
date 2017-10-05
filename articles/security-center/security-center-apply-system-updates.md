---
title: "Azure Güvenlik Merkezi'nde sistem güncelleştirmeleri uygulamak | Microsoft Docs"
description: "Bu belgede Azure Güvenlik Merkezi önerileri uygulamak gösterilmiştir ** sistem güncelleştirmeleri ** uygulamak ve ** sistem güncelleştirmeleri ** sonra yeniden başlatın."
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
ms.openlocfilehash: 50cdea437db5387813c6a3905d14b6904d2aba34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="apply-system-updates-in-azure-security-center"></a>Azure Güvenlik Merkezi'nde sistem güncelleştirmeleri uygulama
Azure Güvenlik Merkezi, Windows ve Linux işletim sistemi güncelleştirmeleri eksik makineleri (VM'ler) günlük izler. Güvenlik Merkezi hizmeti bağlı olarak bir Windows VM üzerinde yapılandırıldığı Windows Update veya Windows Server Update Services (WSUS) kullanılabilir güvenlik ve kritik güncelleştirmeler listesini alır.  Güvenlik Merkezi, ayrıca Linux sistemleri için en son güncelleştirmeleri denetler. VM'yi bir sistem güncelleştirmesi eksikse, Güvenlik Merkezi sistem güncelleştirmeleri uygulamanızı önerir

> [!NOTE]
> Bu belge, örnek bir dağıtım kullanarak hizmeti tanıtır.  Bu, adım adım ilerleyen bir kılavuz değildir.
>
>

## <a name="implement-the-recommendation"></a>Öneriyi uygulamayı
1. İçinde **önerileri** dikey penceresinde, select **sistem güncelleştirmelerini**.

   ![Sistem güncelleştirmelerini uygulayın][1]
2. **Sistem güncelleştirmelerini** eksik sistem güncelleştirmeleri VM'ler listesini görüntüleyen dikey pencere açılır. Bir VM'yi seçin.

   ![Bir VM seçin][2]
3. Bu VM için eksik güncelleştirmelerin listesini görüntüleyen bir dikey pencere açılır. Bir Sistem Güncelleştirmesi'ni seçin. Bu örnekte, şimdi KB3156016 seçin.

   ![Eksik güvenlik güncelleştirmelerini][3]

4. Adımları **güvenlik güncelleştirmesi** eksik güncelleştirmeyi uygulamak için dikey.

   ![Güvenlik güncelleştirmesi][4]

## <a name="reboot-after-system-updates"></a>Sistem güncelleştirmelerinden sonra yeniden başlatın
1. Geri dönüp **önerileri** dikey. Adlı Sistem güncelleştirmeleri uygulandıktan sonra yeni bir giriş oluşturulan **sonra sistem güncelleştirmelerini yeniden**. Bu giriş, VM sistemi güncelleştirmelerini uygulama işlemini tamamlamak için bilgisayarınızı yeniden başlatmanız gerektiğini bilmenizi sağlar.

   ![Sistem güncelleştirmelerinden sonra yeniden başlatın][5]
2. Seçin **sonra sistem güncelleştirmelerini yeniden**. Bu açılır **sistem güncelleştirmelerini tamamlamak için yeniden başlatma bekleniyor** Uygula sistem tamamlamak için yeniden başlatmanız gerekir VM'ler listesini görüntüleyen dikey işlem güncelleştirir.

   ![Beklemedeki yeniden başlatma][6]

İşlemi tamamlamak için Azure VM'yi yeniden başlatın.

## <a name="see-also"></a>Ayrıca bkz.
Güvenlik Merkezi hakkında daha fazla bilgi edinmek için şunlara bakın:

* [Azure Güvenlik Merkezi'nde güvenlik ilkelerini ayarlama](security-center-policies.md) -- Azure abonelikleriniz ve kaynak gruplarınız için güvenlik ilkelerini yapılandırma hakkında bilgi edinin.
* [Azure Güvenlik Merkezi'nde güvenlik önerilerini yönetme](security-center-recommendations.md) --nasıl önerilerin Azure kaynaklarınızı korumanıza yardımcı öğrenin.
* [Azure Güvenlik Merkezi'nde güvenlik durumunu izleme](security-center-monitoring.md) --Azure kaynaklarınızı sağlığını izlemek öğrenin.
* [Azure Güvenlik Merkezi'nde güvenlik uyarılarını yönetme ve yanıtlama](security-center-managing-and-responding-alerts.md) -- Güvenlik uyarılarını yönetme ve yanıtlama hakkında bilgi edinin.
* [Azure Güvenlik Merkezi ile iş ortağı çözümlerini izleme](security-center-partner-solutions.md) - İş ortağı çözümlerinizin sistem durumunu nasıl izleyeceğiniz hakkında bilgi edinin.
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) -- Hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
* [Azure güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) --Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.

<!--Image references-->
[1]: ./media/security-center-apply-system-updates/recommendation.png
[2]:./media/security-center-apply-system-updates/select-vm.png
[3]: ./media/security-center-apply-system-updates/missing-security-updates.png
[4]: ./media/security-center-apply-system-updates/security-update.png
[5]: ./media/security-center-apply-system-updates/reboot-after-system-updates.png
[6]: ./media/security-center-apply-system-updates/restart-pending.png
