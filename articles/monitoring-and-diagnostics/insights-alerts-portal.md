---
title: "Azure Hizmetleri - aaaCreate uyarıları Azure portalı | Microsoft Docs"
description: "Belirttiğiniz hello koşullar karşılandığında tetikleyici e-postalar, bildirimler, Web siteleri URL'leri (Web kancaları) ya da Otomasyon çağırın."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: f7457655-ced6-4102-a9dd-7ddf2265c0e2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/23/2016
ms.author: robb
ms.openlocfilehash: 78d862d25255cda9fdfe347329e908a471c39846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---azure-portal"></a>Ölçüm uyarılar için Azure services - Azure İzleyicisi'nde oluşturma Azure portalı
> [!div class="op_single_selector"]
> * [Portal](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [CLI](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a>Genel Bakış
Bu makalede Azure portal kullanarak Azure ölçüm uyarıları tooset hello nasıl gösterilmektedir.   

İzleme ölçümlerini ya da olayları, Azure hizmetlerinizi göre bir uyarı alabilirsiniz.

* **Ölçüm değerleri** - hello belirtilen ölçüm hello değeri herhangi bir yönde atadığınız bir eşik kestiği olduğunda uyarı tetikler. Diğer bir deyişle, her ikisi de tetikler hello koşul karşılanır ilk ve ardından daha sonra ne zaman, koşul artık karşılanıp zaman.    
* **Etkinlik günlüğü olaylarını** -bir uyarıyı tetiklemek *her* olay veya yalnızca belirli bir olaylar oluşur. Etkinlik günlüğü Uyarıları hakkında daha fazla toolearn [burayı tıklatın](monitoring-activity-log-alerts.md)

Tetikler olduğunda bir uyarı ölçüm toodo hello aşağıdaki yapılandırabilirsiniz:

* e-posta bildirimleri toohello hizmet yöneticisini ve ortak Yöneticiler Gönder
* e-posta, belirttiğiniz tooadditional e-postalar gönderin.
* bir Web kancası çağırın
* bir Azure runbook'tan (yalnızca Azure portal hello) yürütülmesini Başlat

Yapılandırma ve kullanma ölçüm uyarı kuralları hakkında bilgi alın

* [Azure portal](insights-alerts-portal.md)
* [PowerShell](insights-alerts-powershell.md)
* [komut satırı arabirimi (CLI)](insights-alerts-command-line-interface.md)
* [Azure monitör REST API'si](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-hello-azure-portal"></a>Ölçüm hello Azure portal ile bir uyarı kuralı oluşturma
1. Merhaba, [portal](https://portal.azure.com/), izleme ilgilenen hello kaynak bulup seçin.

2. Seçin **uyarıları** veya **uyarı kuralları** hello izleme bölümü altında. Merhaba metin ve simge farklı kaynaklar için biraz değişebilir.  

    ![İzleme](./media/insights-alerts-portal/AlertRulesButton.png)

3. Select hello **uyarı Ekle** komut ve hello alanları doldurun.

    ![Uyarı ekleme](./media/insights-alerts-portal/AddAlertOnlyParamsPage.png)

4. **Ad** , uyarı kuralı ve seçin bir **açıklama**, bildirim e-postalarda da gösterir.

5. Select hello **ölçüm** toomonitor istediğiniz sonra seçin bir **koşulu** ve **eşik** hello ölçüm için değer. Ayrıca hello Seçtiğiniz **süresi** ölçüm hello süresini kural hello uyarı Tetikleyicileri önce yerine getirilmesi gereken. Dolayısıyla örneğin Hello CPU % 80 5 dakika boyunca sürekli olarak yukarıdaki kaldığında hello süresi "PT5M" kullanıyorsanız ve uyarıyı % 80 CPU arar hello uyarı tetikler. Merhaba ilk tetikleyici oluşur sonra hello CPU 5 dakika boyunca % 80'altında kaldığında oluşan yeniden tetikler. Merhaba CPU ölçüm, 1 dakikada oluşur.   

6. Denetleme **e-posta sahipleri... ** e-posta ile yöneticileri ve ortak Yöneticiler toobe istiyorsanız, ne zaman uyarı ateşlenir hello.

7. Ek e-postaları tooreceive hello olduğunda bir bildirim istiyorsanız uyarı ateşlenir, hello eklemek **ek yönetici email(s)** alan. Birden çok e-postaları - noktalı virgülle ayırın * email@contoso.com;email2@contoso.com*

8. Merhaba geçerli bir URI koymak **Web kancası** alan adlı istiyorsanız, ne zaman hello uyarı etkinleşir.

9. Azure Otomasyonu kullanırsanız, hello uyarı oluşturulduğunda çalıştırmak bir Runbook toobe seçebilirsiniz.

10. Seçin **Tamam** zaman Bitti'yi toocreate hello uyarı.   

Birkaç dakika içinde hello uyarı etkin ve daha önce açıklandığı şekilde tetikler.

## <a name="managing-your-alerts"></a>Uyarılarınızı yönetme
Bir uyarı oluşturduktan sonra bunu seçebilirsiniz ve:

* Önceki gün Hello ölçüm eşiği ve hello hello gerçek değerleri gösteren bir grafik görüntüleyin.
* Düzenleyin veya silin.
* **Devre dışı** veya **etkinleştirmek** onu, tootemporarily durdurma veya bu uyarı için bildirimleri almaya devam etmek istiyorsanız.

## <a name="next-steps"></a>Sonraki adımlar
* [Azure izleme genel bir bakış elde](monitoring-overview.md) hello toplamak ve izlemek bilgi türlerini de dahil olmak üzere.
* Daha fazla bilgi edinmek [Web kancalarını uyarıları yapılandırma](insights-webhooks-alerts.md).
* Daha fazla bilgi edinmek [etkinlik günlüğü olayları uyarıları yapılandırma](monitoring-activity-log-alerts.md).
* Daha fazla bilgi edinmek [Azure Automation Runbook](../automation/automation-starting-a-runbook.md).
* Alma bir [tanılama günlükleri'ne genel bakış](monitoring-overview-of-diagnostic-logs.md) hizmetinizde ayrıntılı yüksek sıklıkta ölçümleri toplamak ve.
* Alma bir [ölçümleri toplama genel bakış](insights-how-to-customize-monitoring.md) toomake hizmetinizi kullanılabilir ve yanıt verebilir durumda olduğundan emin.
