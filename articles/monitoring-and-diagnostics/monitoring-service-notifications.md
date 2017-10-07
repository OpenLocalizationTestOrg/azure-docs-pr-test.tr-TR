---
title: aaaWhat olan hizmet durumu bildirimlerine | Microsoft Docs
description: "Hizmet durumu bildirimlerine izin ver, tooview hizmeti sistem durumu iletileri tarafından Microsoft Azure yayımlama."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 6f2fe72154c3e80d85062655c49dd1799b718e3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-health-notifications"></a>Hizmet durumu bildirimlerine
## <a name="overview"></a>Genel Bakış

Bu makalede Azure portal kullanarak tooview hizmet durumu bildirimlerine nasıl hello gösterilmektedir.

Hizmet durumu bildirimlerine hello aboneliğinizi hello kaynaklarınıza etkileyen Azure ekibi tarafından yayımlanan, tooview hizmeti sistem durumu iletileri izin verin. Bu bildirimler bir alt etkinlik günlüğü olaylarını ve sınıfıdır hello etkinlik günlüğü dikey penceresinde de bulunabilir. Hizmet durumu bildirimlerine bilgilendirici veya hello sınıfı bağlı olarak tıklatılabilir olabilir.

Hizmet durumu bildirimlerine beş sınıfları şunlardır:  

- **Gerekli eylem:** zaman tootime biz hesabınızdaki durum olağan dışı bir şey fark edebilirsiniz. Toowork, tooremedy ile gerekli. Size bir bildirim ya da göndereceğiz hello Eylemler ayrıntılı tootake gerekir veya hakkında ayrıntılar ile toocontact Azure mühendislik ya da destekler.  
- **Yardımlı kurtarma:** bir olay oluştu ve mühendisleri onaylanıp etkisi hala yaşıyor. Mühendislik toowork sizinle gerekir doğrudan toobring Hizmetleri toorestoration.  
- **Olay:** olay etkileyen bir hizmet şu anda bir veya daha fazla hello kaynakları söz konusu.  
- **Bakım:** , bir veya daha fazla aboneliğiniz hello kaynaklarınıza etkileyebilecek bir planlı bakım etkinliği bildiren bir bildirim budur.  
- **Bilgi:** zaman tootime size yardımcı olabilecek potansiyel iyileştirmeler hakkında iletişim kurun tooyou kaynak kullanımınızı geliştirmenize bildirimleri gönderebiliriz.  
- **Güvenlik:** Acil güvenlik ilgili Azure üzerinde çalışan, solution(s) ilgili bilgiler.

Her hizmet sistem durumu bildirimi ayrıntıları hello kapsamı ve etkisi tooyour kaynaklardaki yürütecek. Ayrıntılar içerir:

Özellik adı | Açıklama
-------- | -----------
Kanalları | Değerleri aşağıdaki hello biridir: "Yönetici", "İşlem"
correlationId | Genellikle bir hello dize biçimindeki GUID'dir. Olaylar, ile ait aynı uber eylemi genellikle paylaşmak toohello hello aynı correlationıd değeri.
eventDataId | Bir olayın Hello benzersiz tanımlayıcıdır.
EventName | Merhaba olay Hello başlığıdır
düzeyi | Merhaba olay düzeyi. Değerleri aşağıdaki hello birini: "Kritik", "Error"Uyarı",", "Bilgi" ve "Ayrıntılı"
resourceProviderName | Kaynak hello kaynak sağlayıcısının adını hello için etkilenen
Kaynak türü| Merhaba, kaynak Hello türü kaynak etkilenen
alt durum | Genellikle hello REST çağrısı karşılık gelen HTTP durum kodunu Merhaba, ancak bu ortak değerleri gibi bir alt durum açıklayan diğer dizeleri de içerir: Tamam (HTTP durum kodu: 200), oluşturulan (HTTP durum kodu: 201), kabul edilen (HTTP durum kodu: 202), içerik yok (HTTP Durum kodu: 204), hatalı istek (HTTP durum kodu: 400), bulunamadı (HTTP durum kodu: 404), çakışma (HTTP durum kodu: 409), iç sunucu hatası (HTTP durum kodu: 500), hizmet kullanılamıyor (HTTP durum kodu: 503), ağ geçidi zaman aşımı (HTTP durum kodu: 504).
eventTimestamp | Merhaba olay hello Azure hizmetini işleme hello tarafından oluşturulan zaman damgası karşılık gelen hello olay isteği.
submissionTimestamp |   Merhaba olay sorgulama için kullanılabilir duruma zaman damgası.
subscriptionId | Bu olayın günlüğe yazıldığı Azure aboneliği hello
durum | Merhaba hello işlemi durumunu açıklayan dize. Bazı genel değerler şunlardır:, ilerleme, başarılı, başarısız, etkin, çözümlenmiş başlatıldı.
operationName | Merhaba işlemin adı.
category | "ServiceHealth"
resourceId | Kaynak kimliğini hello kaynak etkilenmiş.
Properties.Title | Bu iletişim için yerelleştirilmiş hello başlığı. İngilizce hello varsayılan dildir.
Properties.Communication | Merhaba, HTML biçimlendirmesi ile Merhaba iletişim ayrıntılarını yerelleştirilmiş. İngilizce hello varsayılandır.
Properties.incidentType | Olası değerler: AssistedRecovery, ActionRequired, bilgi, olay, bakım, güvenlik
Properties.trackingId | Bu olay ile ilişkilendirilmiş hello olay tanımlar. Bu toocorrelate hello olayları ilgili tooan olayı kullanın.
Properties.impactedServices | Merhaba Hizmetleri ve hello olaydan etkilenen bölgeler açıklar bir kaçış karakterli JSON blobu. Her biri bir ServiceName ve her biri bir RegionName sahip ImpactedRegions listesini sahip hizmetlerin listesini.
Properties.defaultLanguageTitle | İngilizce Hello iletişimi
Properties.defaultLanguageContent | html biçimlendirmesi veya düz metin olarak İngilizce Hello iletişimi
Properties.Stage | AssistedRecovery, ActionRequired, bilgi, olay, güvenlik için olası değerler: etkin, olan çözümlendi. Bakım için oldukları: etkin, planlanmış, devam ediyor, iptal edildi, Rescheduled, çözümlenmiş, tamamlandı
Properties.communicationId | Bu olay Hello iletişimi ilişkilidir.


## <a name="viewing-your-service-health-notifications-in-hello-azure-portal"></a>Hizmet durumu bildirimlerine hello Azure portal görüntüleme
1.  Merhaba, [portal](https://portal.azure.com), toohello gidin **İzleyici** hizmeti

    ![İzleme](./media/monitoring-service-notifications/home-monitor.png)
2.  Merhaba tıklatın **İzleyici** seçeneği tooopen hello İzleyici dikey ayarlama. Bu dikey pencere tüm izleme ayarlarınızı ve verilerinizi tek bir birleştirilmiş görünümde gösterir. Toohello ilk açıldığında **etkinlik günlüğü** bölümü.

3.  Şimdi tıklayın **hizmet bildirimleri** bölümü

    ![İzleme](./media/monitoring-service-notifications/service-health-summary.png)
4.  Daha fazla ayrıntı hello satır öğelerini tooview birini tıklatın

5. Tıklatın hello üzerinde **+ etkinlik günlüğü uyarı Ekle** bu tür gelecekteki hizmet bildirimleri için bildirim işlem tooreceive bildirimleri tooensure. Uyarıları hizmeti bildirimlerinin yapılandırma hakkında daha fazla toolearn [burayı tıklatın](monitoring-activity-log-alerts-on-service-notifications.md)

## <a name="next-steps"></a>Sonraki Adımlar:
Alma [uyarı bildirimleri hizmeti sistem durumu bildirimi her](monitoring-activity-log-alerts-on-service-notifications.md) nakledilir  
Daha fazla bilgi edinmek [etkinlik günlüğü uyarıları](monitoring-activity-log-alerts.md)
