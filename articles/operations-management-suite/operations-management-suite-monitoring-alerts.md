---
title: "Microsoft ürünleri izleme aaaAlert yönetiminde | Microsoft Docs"
description: "Bir uyarı yöneticinin dikkat gerektiren bazı sorun olduğunu gösterir.  Bu makalede hello farklar uyarıları nasıl oluşturulduğunu ve System Center Operations Manager (SCOM) ve günlük analizi yönetilen açıklar ve hello iki ürün için bir karma uyarı Yönetimi stratejisi yararlanarak, en iyi yöntemler sağlar."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6572c3f8-78ca-4fa9-8fe1-d0b488590788
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: 526a3d92f3b6a5d6dec2f3979a934cc94c13f2e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-alerts-with-microsoft-monitoring"></a>Microsoft izleme uyarıları yönetme
Bir uyarı yöneticinin dikkat gerektiren bazı sorun olduğunu gösterir.  Ayrı arasındaki farklar System Center Operations Manager (SCOM) ve günlük analizi Operations Management Suite (OMS) uyarıları nasıl oluşturulduğunu, nasıl yönetilen analiz ve ve kritik bir sorun olduğunu nasıl bildirilir açısından vardır algıladı.

## <a name="alerts-in-operations-manager"></a>Operations Manager içindeki uyarıları
Scom'deki uyarıları, bireysel kuralları veya izleyiciler tooindicate belirli bir sorunun tarafından üretilir.  Bir kural bir uyarı tooindicate verebilir sırasında bir hata durumu girer bir izleyici bir uyarı yönetilen bir nesne doğrudan ilgili toohello durumunu olmayan bazı kritik sorun oluşturabilir.  Yönetim paketleri çeşitli Merhaba uygulaması için uyarı oluşturma iş akışı veya yönettikleri hizmeti içerir.  Yeni bir Yönetim Paketi yapılandırma hello işleminin parçası kritik düşünün olmayan sorunlar için aşırı uyarıları almadığınız tooensure ayarlamadır.

![SCOM uyarı görünümü](media/operations-management-suite-monitoring-alerts/scom-alert-view.png)

SCOM tam uyarı Yönetimi tooresolve hello sorunu çalışırken, yöneticiler tarafından değiştirilebilir bir durumu olan uyarılar sağlar.  Merhaba sorunu Çözümlendi, Merhaba yönetici aynı zamanda, artık görünür hello uyarı tooclosed etkin uyarıları görüntüleme görünümlerde ayarlar.  Merhaba izleme tooa sağlıklı duruma dönünce izlemelerden üretilen uyarıları otomatik olarak çözülebilir.

![Uyarı durumu](media/operations-management-suite-monitoring-alerts/scom-alert-status.png)

## <a name="alerts-in-log-analytics"></a>Günlük analizi uyarıları
Günlük analizi bir uyarıda, düzenli aralıklarla otomatik olarak çalışacak bir günlük sorgudan oluşturulur.  Tüm günlük sorgudan bir uyarı kuralı oluşturabilirsiniz.  Merhaba sorgu belirttiğiniz hello ölçütleriyle eşleşen sonuçları döndürürse, bir uyarı oluşturulur.  Bu belirli bir olay algılandığında bir uyarı oluşturur. belirli bir sorgu olabilir veya herhangi bir hata olayı arar tooa belirli bir uygulama ile ilgili daha fazla genel bir sorgu kullanabilirsiniz.

Günlük analizi uyarılar toohello OMS depo olarak bir olay yazılır ve bir günlük sorgu alınabilir.  Merhaba sorunu Çözümlendi, belirtmek üzere SCOM olayları gibi bir durum yok.

![OMS Uyarısı](media/operations-management-suite-monitoring-alerts/oms-alert.png)

SCOM için günlük analizi veri kaynağı olarak kullanıldığında, oluşturulan ve değiştirilen SCOM uyarıları toohello OMS deposu yazılır.  

![SCOM Uyarısı](media/operations-management-suite-monitoring-alerts/scom-alert.png)

Merhaba [uyarı yönetimi çözümü](http://technet.microsoft.com/library/mt484092.aspx) tooretrieve farklı uyarıları etkin uyarıları ve birkaç genel sorgular özetini sağlar.  Bu, daha etkili bir şekilde analiz uyarılarınızın SCOM raporda daha sağlar.  Üzerinde hello özetleri toodetailed verilerden ayrıntıya ve geçici sorguları tooretrieve farklı uyarıları kümesi oluşturun.

![Uyarı yönetimi çözümü](media/operations-management-suite-monitoring-alerts/alert-management.png)

## <a name="notifications"></a>Bildirimler
Scom'deki bildirimleri belirli ölçütlere uyan yanıt tooalerts içinde bir posta ya da metin gönderin.  İzlenmekte olan hello nesnesi gibi ölçütlere bağlı olarak bildirim farklı kişilerin sahip, hello hello uyarı, algılanan sorun hello tür ya da hello önemini farklı bildirim abonelikleri oluşturabilirsiniz günün zaman.

Birkaç abonelikleri kullanılan tooimplement çok sayıda yönetim paketleri için bir tam bildirim stratejisi olabilir.

![SCOM uyarıları](media/operations-management-suite-monitoring-alerts/alerts-overview-scom.png)

Günlük analizi size bildirebilir aracılığıyla posta her bir e-posta bildirim eylemi ayarlayarak bir uyarı oluşturuldu [uyarı kuralı](http://technet.microsoft.com/library/mt614775.aspx).  Merhaba yeteneklerini tek bir kural toomultiple uyarılarla abone SCOM hello yok.  OMS sağlamaz beri ayrıca toocreate uyarı kurallarınızı herhangi önceden yapılandırılmış gerekir.

![Log Analytics uyarıları](media/operations-management-suite-monitoring-alerts/alerts-overview-oms.png)

Bunları hello Operations Konsolu değiştirebilmeniz için bu yana tamamen günlük analizi SCOM uyarılar ancak yönetemez.  Günlük analizi yararlı bir uyarı Yönetimi parçası işlem ancak Çözümleme Araçları tek başına bu SCOM sağlama yok.

## <a name="alert-remediation"></a>Uyarı düzeltme
[Düzeltme](http://technet.microsoft.com/library/mt614775.aspx) tooan girişimi tooautomatically doğru hello sorun bir uyarı tarafından tanımlanan başvuruyor.

SCOM sağlıksız bir duruma girme yanıt tooa İzleyicisi'nde toorun tanılama ve kurtarma sağlar.  Eşzamanlı toohello İzleyicisi Merhaba uyarı oluşturma meydana gelir.  Tanılama ve kurtarma işlemleri genellikle hello aracı üzerinde çalışan bir komut olarak uygulanır.  Bir kurtarma toocorrect hello sorun denemeleri sırasında tanılama girişimleri toogather hello hakkında daha fazla bilgi sorun algıladı.

Günlük analizi toostart sağlayan bir [Azure Otomasyonu runbook](https://azure.microsoft.com/documentation/services/automation/) veya bir Web kancası yanıt tooa günlük analizi uyarıda çağırın.  Runbook'ları, PowerShell içinde uygulanan karmaşık mantık içerebilir.  Merhaba komut dosyası Azure üzerinde çalışır ve herhangi bir Azure kaynaklarını veya dış kaynaklar hello buluttan erişebilir.  Azure Otomasyonu hello özelliği tooexecute runbook'ları bir sunucuda yerel veri merkezinizdeki sahip, ancak bu özellik yanıt tooLog Analytics uyarıları hello runbook başlatma sırasında şu anda kullanılamıyor.

Scom'deki kurtarmaları hem OMS runbook'larda PowerShell Betiği içerebilir, ancak kurtarma işlemleri daha zor toocreate ve bir yönetim paketi içinde yer almalıdır çünkü yönetin.  Runbook'ları yazma, test ve runbook'ları yönetmek için özellikler sağlayan bir Azure Otomasyonu depolanır.

Günlük analizi için bir veri kaynağı olarak SCOM kullanırsanız, OMS deposu hello depolanan SCOM uyarıları günlük sorgu tooretrieve kullanarak bir günlük analizi uyarı oluşturabilirsiniz.  Bu, bir Azure Otomasyonu runbook'u toorun yanıt tooa SCOM uyarıda olanak tanır.  Azure'da Hello runbook çalışır olduğundan, doğal olarak, bu şirket içi sorunların kurtarma işlemleri için uygun bir strateji olmayacaktır.

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba ayrıntılarını öğrenmek [uyarılar System Center Operations Manager (SCOM)](https://technet.microsoft.com/library/hh212913.aspx).

