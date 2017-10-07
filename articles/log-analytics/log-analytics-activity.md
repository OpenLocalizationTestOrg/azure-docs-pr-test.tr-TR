---
title: "aaaView Azure etkinlik günlükleri ile günlük analizi | Microsoft Docs"
description: "Hello Azure etkinlik günlükleri çözüm tooanalyze ve arama hello Azure etkinlik günlüğü tüm Azure abonelikleri kullanabilirsiniz."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: dbac4c73-0058-4191-a906-e59aca8e2ee0
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.openlocfilehash: 171d0d604d03a5714a9599cc0b448fc5f6471f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="view-azure-activity-logs"></a>Azure etkinlik günlüklerini görüntüle

![Azure etkinlik günlükleri simgesi](./media/log-analytics-activity/activity-log-analytics.png)

Merhaba etkinlik günlüğü analiz çözümü arama hello ve çözümlemenize yardımcı olur [Azure etkinlik günlüğü](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) tüm Azure abonelikleri arasında. Hello Azure etkinlik günlüğü aboneliklerinizi kaynaklarında üzerinde gerçekleştirilen hello işlemleri Öngörüler sunan bir günlüktür. Merhaba etkinlik günlüğü önceden olarak biliniyordu *denetim günlüklerini* veya *işlem günlüklerini* aboneliklerinizi olaylarını raporları beri.

Merhaba etkinlik günlüğü kullanarak hello belirleyebilirsiniz *ne*, *kimin*, ve *zaman* herhangi yazma işlemleri için aboneliğinizi hello kaynaklarında yapılan (PUT, POST, DELETE) için. Merhaba durumunu hello işlemleri ve ilgili diğer özellikleri de anlayabilirsiniz. Merhaba etkinlik günlüğü okuma (GET) işlemleri veya hello Klasik dağıtım modeli kullanan kaynakları işlemlerinde içermez.

Azure etkinlik günlükleri tooLog Analytics bağlandığınızda, şunları yapabilirsiniz:

- Önceden tanımlanmış görünümleri ile Merhaba etkinlik günlüklerini analiz edin
- Analiz etmek ve birden çok Azure abonelikleri arama ve etkinlik günlükleri
- Etkinlik günlükleri 90 günden daha uzun süre tutmak<sup>1</sup>
- Etkinlik günlükleri diğer Azure ile ilişkilendirmek platform ve uygulama verileri
- Duruma göre toplanan işletimsel etkinlikleri bakın
- Her Azure hizmetlerinizi gerçekleştiği etkinliklerin eğilimleri görüntüleme
- Tüm Azure kaynaklarınızı yetkilendirme değişiklikleri hakkında rapor oluşturun.
- Kaynaklarınızın etkileyen kesintisinden veya hizmet sistem durumu sorunlarını belirle
- Günlük arama toocorrelate kullanıcı etkinliklerini, otomatik ölçeklendirme işlemleri, yetkilendirme değişiklikleri ve hizmet sistem durumu tooother günlükleri veya ölçümleri, ortamınızdan kullanın

<sup>1</sup>hello ücretsiz katmanında olsa bile, varsayılan olarak, günlük analizi Azure etkinlik günlüklerinizi 90 gün boyunca tutar. Veya 90 günden çalışma saklama ayarı varsa. Çalışma alanınızı 90 günden daha uzun bekletme varsa, hello etkinlik günlükleri için çalışma alanınızı hello bekletme süresini tutulur.

Günlük analizi etkinlik günlükleri ücretsiz toplar ve ücretsiz olarak 90 gün boyunca hello günlükleri depolar. 90 günden daha uzun süre günlüklerini saklıyorsanız 90 günden daha uzun depolanan hello verilerin veri saklama ücret uygulanabilir.

Ücretsiz fiyatlandırma katmanı hello üzerinde olduğunuzda, etkinlik günlükleri tooyour günlük veri tüketimi geçerli değildir.

## <a name="connected-sources"></a>Bağlı kaynaklar

Diğer çoğu günlük analizi çözümleri, etkinlik günlükleri için aracıları tarafından toplanan veriler değil. Merhaba çözümü tarafından kullanılan tüm verileri doğrudan Azure'dan gelir.

| Bağlı Kaynak | Destekleniyor | Açıklama |
| --- | --- | --- |
| [Windows aracıları](log-analytics-windows-agents.md) | Hayır | Merhaba çözüm Windows aracılardan bilgi toplamaz. |
| [Linux aracıları](log-analytics-linux-agents.md) | Hayır | Merhaba çözüm Linux aracılarını bilgi toplamaz. |
| [SCOM yönetim grubu](log-analytics-om-agents.md) | Hayır | Merhaba çözüm bağlı SCOM yönetim grubunda aracılardan gelen bilgiler toplamaz. |
| [Azure depolama hesabı](log-analytics-azure-storage.md) | Hayır | Merhaba çözüm, Azure depolama biriminden bilgi toplamaz. |

## <a name="prerequisites"></a>Ön koşullar

- Azure etkinlik günlüğü bilgilerini tooaccess, bir Azure aboneliğinizin olması gerekir.

## <a name="configuration"></a>Yapılandırma

Aşağıdaki adımları tooconfigure hello etkinlik günlük analizi çözümü alanlarınızı hello gerçekleştirin.

1. Merhaba etkinlik günlük analizi hello çözümden etkinleştirmek [Azure Market](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureActivityOMS?tab=Overview) veya açıklanan hello işlemi kullanarak [hello Çözümleri Galerisi eklemek günlük analizi çözümleri](log-analytics-add-solutions.md).
2. Etkinlik günlükleri toogo tooyour günlük analizi çalışma alanı yapılandırın.
    1. Azure portal Merhaba, çalışma alanınızı seçin ve ardından **Azure etkinlik günlüğü**.
    2. Her abonelik için hello abonelik adını tıklatın.  
        ![Abonelik Ekle](./media/log-analytics-activity/add-subscription.png)
    3. Merhaba, *varlığıyla SubscriptionName* dikey penceresinde tıklatın **Bağlan**.  
        ![Abonelik Bağlan](./media/log-analytics-activity/subscription-connect.png)

Merhaba OMS portalı kullanarak hello çözüm eklerseniz, döşeme hello aşağıdaki görürsünüz. Bir Azure aboneliği tooyour çalışma toohello Azure portal tooconnect imzalayın.  
![değerlendirme gerçekleştirme](./media/log-analytics-activity/tile-performing-assessment.png)

## <a name="using-hello-solution"></a>Merhaba çözümünü kullanarak

Merhaba etkinlik günlük analizi çözüm tooyour çalışma alanı eklediğinizde, hello **Azure etkinlik günlükleri** döşeme tooyour genel bakış Panosu'na eklenir. Merhaba hello çözümü olan Azure abonelikleri erişmek için bu kutucuğu Azure etkinlik kayıtlarını hello sayısı sayısını görüntüler.

![Azure etkinlik günlükleri döşeme](./media/log-analytics-activity/azure-activity-logs-tile.png)

### <a name="view-azure-activity-logs"></a>Görünüm Azure etkinliğini günlüğe kaydeder

Merhaba tıklatın **Azure etkinlik günlükleri** döşeme tooopen hello **Azure etkinlik günlükleri** Pano. Merhaba Pano aşağıdaki tablonun hello hello Kanatlar içerir. Her dikey penceresinde hello dikey'nın ölçütlerine kapsam ve zaman aralığını belirtilen eşleşen too10 öğeleri listeler. Tıklayarak tüm kayıtları döndüren bir günlük arama çalıştırabilirsiniz **tümünü görmek** hello altındaki hello dikey veya hello dikey penceresi Başlığı tıklatarak.

Etkinlik günlüğü verileri yalnızca görünür *sonra* daha önce verileri görüntüleyemezsiniz şekilde, etkinlik günlükleri toogo toohello çözümünüzün, yapılandırdığınız.

| Dikey penceresi | Açıklama |
| --- | --- |
| Azure etkinlik günlüğü girişleri | Bir çubuk grafik hello üst Azure etkinlik günlüğü girişi, seçtiğiniz hello tarih aralığı kayıt toplamlarını gösterir ve üst 10 etkinlik arayanlar hello listesini gösterir. Tıklatın günlük arama için çubuk grafik toorun hello <code>Type=AzureActivity</code>. Arayan öğesi toorun bu öğe için tüm etkinlik günlüğü girişleri döndüren bir günlük Ara'yı tıklatın. |
| Duruma göre etkinlik günlükleri | Azure etkinlik günlüğü durumu seçmiş olduğunuz hello tarih aralığı için bir halka grafik gösterir. Ayrıca bir liste hello üst on durum kayıtların listesini gösterir. Bir günlük Ara Hello grafik toorun <code>Type=AzureActivity &#124; measure count() by ActivityStatus</code>. Durum öğesi toorun bu durum kaydı tüm etkinlik günlüğü girişlerini döndüren bir günlük Ara'yı tıklatın. |
| Kaynak tarafından etkinlik günlükleri | Etkinlik günlükleri kaynaklarla Hello toplam sayısını gösterir ve kaydıyla on kaynakları sayar her kaynak için hello üst listeler. Bir günlük Ara Hello toplam alan toorun <code>Type=AzureActivity &#124; measure count() by Resource</code>, kullanılabilir toohello çözüm tüm Azure kaynakları gösterir. Bir kaynak toorun kaynağı için tüm etkinlik kayıtlarını döndüren bir günlük Ara'yı tıklatın. |
| Kaynak sağlayıcısı tarafından etkinlik günlükleri | Gösterir hello toplam sayısı etkinlik üretmek kaynak sağlayıcıları günlüğe kaydeder ve hello ilk on listeler. Bir günlük Ara Hello toplam alan toorun <code>Type=AzureActivity &#124; measure count() by ResourceProvider</code>, tüm Azure kaynak sağlayıcıları gösterir. Bir kaynak sağlayıcısı toorun hello sağlayıcısı için tüm etkinlik kayıtlarını döndüren bir günlük arama tıklayın. |

![Azure etkinlik günlükleri Panosu](./media/log-analytics-activity/activity-log-dash.png)

## <a name="next-steps"></a>Sonraki adımlar

- Oluşturma bir [uyarı](log-analytics-alerts-creating.md) zaman belirli bir etkinliğe olur.
- Kullanım [günlük arama](log-analytics-log-searches.md) tooview ayrıntılı bilgileri, etkinlik günlükleri.
