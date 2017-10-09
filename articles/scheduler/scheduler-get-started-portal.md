---
title: "aaaGet Azure portalda Azure Scheduler ile başlatıldı | Microsoft Docs"
description: "Azure portalda Azure Scheduler kullanmaya başlama"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: e69542ec-d10f-4f17-9b7a-2ee441ee7d68
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: deli
ms.openlocfilehash: 58255c0ad19da65932f8b1d36cb8fef1ff6e651b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-scheduler-in-azure-portal"></a>Azure portalda Azure Scheduler kullanmaya başlama
Azure scheduler'da zamanlanmış kolay toocreate işleri olur. Bu öğreticide şunları öğreneceksiniz nasıl toocreate bir işi. Ayrıca Scheduler’ın izleme ve yönetim özelliklerini öğreneceksiniz.

## <a name="create-a-job"></a>Bir iş oluşturma
1. Çok oturum[Azure portal](https://portal.azure.com/).  
2. Tıklatın **+ yeni** > türü *Zamanlayıcı* hello arama kutusuna > seçin **Zamanlayıcı** sonuçlarında > tıklatın **oluşturma**.
   
    ![][marketplace-create]
3. Şimdi bir GET isteğiyle http://www.microsoft.com/ adresine işaret eden bir iş oluşturalım. Merhaba, **Scheduler işi** ekranında, aşağıdaki bilgilerle hello girin:
   
   1. **Ad:** `getmicrosoft`  
   2. **Abonelik:** Azure aboneliğiniz   
   3. **İş Koleksiyonu:** Mevcut bir iş koleksiyonu seçin veya tıklatın **Yeni Oluştur**’a tıklayın > bir ad girin.
4. İleri ' **eylem ayarları**, değerleri aşağıdaki hello tanımlayın:
   
   1. **Eylem Türü:** ` HTTP`  
   2. **Yöntem:** `GET`  
   3. **URL:** ` http://www.microsoft.com`  
      
      ![][action-settings]
5. Son olarak, şimdi bir zamanlama tanımlayalım. Merhaba iş bir kerelik iş olarak tanımlanabilir, ancak şimdi bir yineleme zamanlaması seçin:
   
   1. **Yineleme**: `Recurring`
   2. **Başlat**: Bugünün tarihi
   3. **Yineleme sıklığı**: `12 Hours`
   4. **Bitiş tarihi**: Bugünden itibaren iki gün  
      
      ![][recurrence-schedule]
6. **Oluştur**'a tıklayın

## <a name="manage-and-monitor-jobs"></a>İşleri yönetme ve izleme
Bir işi oluşturulduktan sonra hello ana Azure panosunda görünür. Hello iş ve yeni bir'ı sekmeleri aşağıdaki hello ile penceresi açılır:

1. Özellikler  
2. Eylem Ayarları  
3. Zamanlama  
4. Geçmiş
5. Kullanıcılar
   
   ![][job-overview]

### <a name="properties"></a>Özellikler
Bu salt okunur özellikler hello Scheduler işi için hello yönetim meta verilerini açıklar.

   ![][job-properties]

### <a name="action-settings"></a>Eylem ayarları
Hello bir projede tıklayarak **işleri** ekran iş tooconfigure sağlar. Bu, Gelişmiş ayarları yapılandırmak, hello yapılandırmadıysanız, hızlı Oluşturma sihirbazında sağlar.

Tüm eylem türleri için hello yeniden deneme ilkesi ve hello hata eylemini değiştirebilirsiniz.

HTTP ve HTTPS iş eylemi türleri için hello yöntemi tooany HTTP eylemine izin değiştirebilirsiniz. Ayrıca ekleyebilir, silmek veya hello üstbilgileri ve temel kimlik doğrulama bilgilerini değiştirin.

Depolama kuyruğu eylem türleri için hello depolama hesabı, kuyruk adı, SAS belirteci ve gövde değişebilir.

Hizmet veri yolu eylemi türleri için hello ad alanı, konu/kuyruk yolu, kimlik doğrulama ayarları, aktarım türü, ileti özellikleri ve ileti gövdesini değiştirebilirsiniz.

   ![][job-action-settings]

### <a name="schedule"></a>Zamanlama
Bu, hello zamanlamayı yeniden yapılandırın, hello oluşturulan toochange hello zamanlama isterseniz hızlı Oluşturma sihirbazında sağlar.

Bir fırsat toobuild budur [karmaşık zamanlamalar ve Gelişmiş yineleme işinizde](scheduler-advanced-complexity.md)

Hello başlangıç tarihi değiştirebilir ve zaman, yineleme zamanlamasını ve hello bitiş tarihi ve (Merhaba iş yineleniyorsa.) süresi

   ![][job-schedule]

### <a name="history"></a>Geçmiş
Merhaba **geçmişi** sekmesi hello Seçili iş için hello sistemdeki her iş yürütme için seçilen ölçümleri görüntüler. Bu ölçümler hello Scheduler sistem durumunuz ile ilgili gerçek zamanlı değerleri girin:

1. Durum  
2. Ayrıntılar  
3. Yeniden deneme sayısı
4. Oluşma 1., 2., 3., vs.
5. Yürütme başlangıç saati  
6. Yürütme bitiş saati
   
   ![][job-history]

Üzerinde çalışma tooview tıklayabilirsiniz kendi **geçmiş ayrıntıları**, hello her yürütmeye ilişkin tüm yanıtlar dahil olmak üzere. Bu iletişim kutusu ayrıca toocopy hello yanıt toohello Pano sağlar.

   ![][job-history-details]

### <a name="users"></a>Kullanıcılar
Azure Rol Tabanlı Erişim Denetimi (RBAC), Azure Scheduler için ayrıntılı erişim yönetimi sağlar. toouse hello kullanıcılar sekmesini başvurmak çok nasıl toolearn[Azure rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md)

## <a name="see-also"></a>Ayrıca bkz.
 [Scheduler nedir?](scheduler-intro.md)

 [Scheduler kavramları, terminolojisi ve varlık hiyerarşisi](scheduler-concepts-terms.md)

 [Azure Scheduler’da planlar ve faturalama](scheduler-plans-billing.md)

 [Nasıl toobuild karmaşık zamanlar ve Gelişmiş yineleme Azure Scheduler ile](scheduler-advanced-complexity.md)

 [Scheduler REST API başvurusu](https://msdn.microsoft.com/library/mt629143)

 [Scheduler PowerShell cmdlet’leri başvurusu](scheduler-powershell-reference.md)

 [Yüksek Scheduler kullanılabilirliği ve güvenilirliği](scheduler-high-availability-reliability.md)

 [Scheduler sınırları, varsayılanları ve hata kodları](scheduler-limits-defaults-errors.md)

 [Scheduler giden bağlantı kimlik doğrulaması](scheduler-outbound-authentication.md)

[marketplace-create]: ./media/scheduler-get-started-portal/scheduler-v2-portal-marketplace-create.png
[action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-action-settings.png
[recurrence-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-recurrence-schedule.png
[job-properties]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-properties.png
[job-overview]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-overview-1.png
[job-action-settings]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-action-settings.png
[job-schedule]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-schedule.png
[job-history]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history.png
[job-history-details]: ./media/scheduler-get-started-portal/scheduler-v2-portal-job-history-details.png


[1]: ./media/scheduler-get-started-portal/scheduler-get-started-portal001.png
[2]: ./media/scheduler-get-started-portal/scheduler-get-started-portal002.png
[3]: ./media/scheduler-get-started-portal/scheduler-get-started-portal003.png
[4]: ./media/scheduler-get-started-portal/scheduler-get-started-portal004.png
[5]: ./media/scheduler-get-started-portal/scheduler-get-started-portal005.png
[6]: ./media/scheduler-get-started-portal/scheduler-get-started-portal006.png
[7]: ./media/scheduler-get-started-portal/scheduler-get-started-portal007.png
[8]: ./media/scheduler-get-started-portal/scheduler-get-started-portal008.png
[9]: ./media/scheduler-get-started-portal/scheduler-get-started-portal009.png
[10]: ./media/scheduler-get-started-portal/scheduler-get-started-portal010.png
[11]: ./media/scheduler-get-started-portal/scheduler-get-started-portal011.png
[12]: ./media/scheduler-get-started-portal/scheduler-get-started-portal012.png
[13]: ./media/scheduler-get-started-portal/scheduler-get-started-portal013.png
[14]: ./media/scheduler-get-started-portal/scheduler-get-started-portal014.png
[15]: ./media/scheduler-get-started-portal/scheduler-get-started-portal015.png
