---
title: Azure Otomasyonu veri aaaManaging | Microsoft Docs
description: "Bu makale bir Azure Otomasyonu ortamının yönetilmesi için birden çok konuları içerir.  Şu anda veri saklama ve Azure Automation olağanüstü durum kurtarma Azure Automation yedekleme içerir."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: 2896f129-82e3-43ce-b9ee-a3860be0423a
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/02/201
ms.author: magoedte;bwren;sngun
ms.openlocfilehash: 46a164d864c4956c90ab689ca159fff6f6c08028
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-automation-data"></a>Azure Otomasyonu verilerini yönetme
Bu makale bir Azure Otomasyonu ortamının yönetilmesi için birden çok konuları içerir.

## <a name="data-retention"></a>Veri saklama
Azure Otomasyonu'nda kaynak sildiğinizde, kalıcı olarak kaldırılmasını önce 90 gün denetim amacıyla korunur.  Bakın veya bu süre boyunca hello kaynağı kullanın.  Bu ilke silinir tooan Otomasyon hesabı ait tooresources de geçerlidir.

Azure Otomasyonu otomatik olarak siler ve işleri 90 günden daha eski kalıcı olarak kaldırır.

Aşağıdaki tablonun hello hello bekletme ilkesi farklı kaynaklar için özetler.

| Veriler | İlke |
|:--- |:--- |
| Hesaplar |Merhaba hesap bir kullanıcı tarafından silindi ettikten 90 gün sonra kalıcı olarak silinir. |
| Varlıklar |Merhaba varlık bir kullanıcı tarafından silinmiş veya 90 gün sonra hello hello varlık tutan hesap bir kullanıcı tarafından silindi ettikten 90 gün sonra kalıcı olarak silinir. |
| Modüller |Merhaba modülü bir kullanıcı tarafından silinmiş veya 90 gün sonra hello hello modülü tutan hesap bir kullanıcı tarafından silindi ettikten 90 gün sonra kalıcı olarak silinir. |
| Runbook'lar |Merhaba kaynak kullanıcı tarafından silindi veya 90 gün sonra hello hello kaynak tutan hesap bir kullanıcı tarafından silindi ettikten 90 gün sonra kalıcı olarak silinir. |
| İşler |Silinen ve kalıcı olarak kaldırılan 90 gün sonra değiştirilen son. Hello iş tamamlandığında, durduruldu veya askıya alınmış sonra bu olabilir. |
| Düğüm yapılandırmaları/MOF dosyaları |Eski düğüm yapılandırması, yeni bir düğüm yapılandırması oluşturulan ettikten 90 gün sonra kalıcı olarak kaldırılır. |
| DSC düğümleri |Merhaba düğümü Otomasyon Azure portalı veya hello kullanarak hesabından kaydı ettikten 90 gün sonra'kalıcı olarak silinir [Unregister-AzureRMAutomationDscNode](https://msdn.microsoft.com/library/mt603500.aspx) Windows PowerShell cmdlet'i. Düğümleri 90 gün sonra hello düğüm bir kullanıcı tarafından silinmiş tutan hello hesabı da kalıcı olarak kaldırılır. |
| Düğüm raporları |Bu düğüm için oluşturulan yeni bir rapor ettikten 90 gün sonra kalıcı olarak silinir |

Merhaba bekletme ilkesi tooall kullanıcılar geçerlidir ve şu anda özelleştirilemez.

Ancak, uzun bir süre için tooretain verilere gereksiniminiz varsa, runbook işi günlükleri tooLog Analytics iletebilirsiniz.  Daha fazla bilgi için gözden [Azure Otomasyonu işi veri tooOMS günlük analizi iletmek](automation-manage-send-joblogs-log-analytics.md).   

## <a name="backing-up-azure-automation"></a>Azure Otomasyonunu Yedekleme
Microsoft Azure automation hesabında sildiğinizde, runbook'ları, modüller, yapılandırmaları, ayarları, işleri ve varlıklar gibi hello hesaptaki tüm nesnelere silinir. Merhaba hesabı silindikten sonra hello nesneleri kurtarılamıyor.  Otomasyon hesabınızın bilgi toobackup hello içeriği silmeden önce aşağıdaki hello kullanabilirsiniz. 

### <a name="runbooks"></a>Runbook'lar
Runbook'ları tooscript dosyalarınızı hello Azure Yönetim Portalı veya hello kullanarak dışa aktarabilirsiniz [Get-AzureAutomationRunbookDefinition](https://msdn.microsoft.com/library/dn690269.aspx) Windows PowerShell cmdlet'i.  Bu komut dosyaları başka bir Otomasyon hesabı içinde anlatıldığı gibi alınabilir [oluşturma veya bir Runbook'u içeri aktarma](https://msdn.microsoft.com/library/dn643637.aspx).

### <a name="integration-modules"></a>Tümleştirme modülleri
Azure Otomasyon tümleştirme modülleri dışarı aktaramazsınız.  Merhaba Otomasyon hesabı dışında kullanılabilir emin olmalısınız.

### <a name="assets"></a>Varlıklar
Dışarı aktarılamıyor [varlıklar](https://msdn.microsoft.com/library/dn939988.aspx) Azure Otomasyonu gelen.  Hello Azure Yönetim Portalı kullanarak, değişkenleri, kimlik, sertifikalar, bağlantıları ve zamanlamaları hello ayrıntılarını not almanız gerekir.  Başka bir automation'a içeri aktardığınız runbook'lar tarafından kullanılan tüm varlıkları el ile oluşturmanız gerekir.

Kullanabileceğiniz [Azure cmdlet'lerini](https://msdn.microsoft.com/library/dn690262.aspx) tooretrieve ayrıntılarını şifrelenmemiş varlıklar ve bunları kaydetmek ya da gelecek için bir başvuru veya başka bir Otomasyon hesabı eşdeğer varlıklar oluşturun.

Şifrelenmiş değişkenler veya hello parola alanı cmdlet'lerini kullanarak kimlik bilgileri için hello değeri alınamıyor.  Bu değerleri tanımadığınız sonra hello kullanarak bir runbook'tan almak [Get-AutomationVariable](https://msdn.microsoft.com/library/dn940012.aspx) ve [Get-AutomationPSCredential](https://msdn.microsoft.com/library/dn940015.aspx) etkinlikler.

Azure Otomasyon sertifikaları dışarı aktaramazsınız.  Herhangi bir sertifika Azure dışında kullanılabilir olduğundan emin olmalısınız.

### <a name="dsc-configurations"></a>DSC yapılandırmaları
Hello Azure Yönetim Portalı veya hello kullanarak yapılandırmaları tooscript dosyalarınızı verebilirsiniz [verme AzureRmAutomationDscConfiguration](https://msdn.microsoft.com/library/mt603485.aspx) Windows PowerShell cmdlet'i. Bu yapılandırmalar aktarılır ve başka bir Otomasyon hesabı kullanılır.

## <a name="geo-replication-in-azure-automation"></a>Azure automation'da coğrafi çoğaltma
Hesap verilerini tooa farklı coğrafi artıklık için coğrafi çoğaltma, standart Azure Automation hesaplarında yedekler. Bir birincil bölge hesabınızı ayarlarken seçebilir ve ardından bir ikincil bölge tooit otomatik olarak atanır. Merhaba birincil bölgesinden kopyaladığınız hello ikincil veri veri kaybı durumunda sürekli olarak güncelleştirilir.  

Aşağıdaki tablonun hello hello kullanılabilir birincil ve ikincil bölge eşleştirmeleri gösterilir.

| Birincil | İkincil |
| --- | --- |
| Orta Güney ABD |Orta Kuzey ABD |
| ABD Doğu 2 |Orta ABD |
| Batı Avrupa |Kuzey Avrupa |
| Güneydoğu Asya |Doğu Asya |
| Japonya Doğu |Japonya Batı |

Bir birincil bölge veriler kaybolur hello olası olayda, Microsoft toorecover çalışır. Merhaba birincil veriler kurtarılamaz, coğrafi yük devretme gerçekleştirilen ve hello etkilenen müşteriler bu konuda üzerinden bildirilecek.

