---
title: "Azure Güvenlik Merkezi'nde güvenlik uyarılarını aaaManage | Microsoft Docs"
description: "Bu belge, toouse Azure Güvenlik Merkezi özellikleri toomanage yardımcı olur ve toosecurity uyarıları yanıt."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b88a8df7-6979-479b-8039-04da1b8737a7
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: f1cb7e4770776827b75ed15893914678c1f44216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-and-responding-toosecurity-alerts-in-azure-security-center"></a>Yönetme ve Azure Güvenlik Merkezi'nde toosecurity uyarılarını yanıt
Bu belge, Azure Güvenlik Merkezi toomanage kullanın ve toosecurity uyarıları yanıtlamanıza yardımcı olur.

> [!NOTE]
> Gelişmiş tooenable algılama, yükseltme tooAzure Güvenlik Merkezi standart. 60 günlük ücretsiz deneme sürümü mevcuttur. tooupgrade, hello select fiyatlandırma katmanı [Güvenlik İlkesi](security-center-policies.md). Bkz: [Azure Güvenlik Merkezi fiyatlandırma](security-center-pricing.md) toolearn daha fazla.
>
>

## <a name="what-are-security-alerts"></a>Güvenlik uyarıları nedir?
Güvenlik Merkezi otomatik olarak toplar, çözümler, Azure kaynaklarınızı, hello ağ günlük verilerini tümleşir ve güvenlik duvarı ve endpoint protection çözümleri toodetect gerçek tehditleri gibi iş ortağı çözümlerinden bağlı ve hatalı pozitif sonuçları azaltmak. Öncelikli güvenlik uyarıları listesi hello birlikte Güvenlik Merkezi'nde gösterilen tooquickly gereksinim duyduğunuz bilgileri araştırın hello sorun ve nasıl için öneriler tooremediate saldırının.


> [!NOTE]
> Güvenlik Merkezi algılama özelliklerinin nasıl çalıştığı hakkında daha fazla bilgi için [Azure Güvenlik Merkezi Algılama Özellikleri](security-center-detection-capabilities.md) konusunu okuyun.
>
>

## <a name="managing-security-alerts"></a>Güvenlik ilkelerini yönetme
Merhaba bakarak mevcut uyarılarınızı gözden geçirebilirsiniz **güvenlik uyarıları** döşeme. Azure Portalı'nı açın ve her uyarı hakkında daha fazla ayrıntı toosee hello adımları izleyin:

1. Merhaba Güvenlik Merkezi panosunda hello görürsünüz **güvenlik uyarıları** döşeme.

    ![Güvenlik Merkezi'nde güvenlik uyarıları kutucuğu](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig1-ga.png)

2. Merhaba döşeme tooopen hello tıklatın **güvenlik uyarıları** hello hakkında daha fazla ayrıntı içeren dikey penceresi aşağıda gösterildiği gibi uyarır.

   ![Güvenlik Merkezi'nde Hello güvenlik uyarıları dikey penceresi](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig2-ga.png)

Merhaba alt kısmında bu dikey hello ayrıntıları her uyarı için ' dir. toosort, toosort tarafından istediğiniz hello sütunu tıklatın. Her sütunun Hello tanımı aşağıda verilmiştir:

* **Açıklama**: hello uyarının kısa bir açıklama.
* **Sayı**: Belirtilmiş türün belirli bir günde algılanan tüm uyarılarının listesi.
* **Tarafından algılanan**: Merhaba hello uyarıyı tetiklemekten sorumlu hizmet.
* **Tarih**: hello tarih hello olay oluştu.
* **Durum**: Merhaba bu uyarı için geçerli durumu. İki tür durum mevcuttur:
  * **Etkin**: hello güvenlik uyarısı algılandı.
* **Önem derecesi**: hello önem düzeyi yüksek, Orta veya düşük olabilir.

### <a name="filtering-alerts"></a>Uyarıları filtreleme
Tarihe, duruma ve önem derecesine göre uyarıları filtreleyebilirsiniz. Uyarıları filtreleme toonarrow hello güvenlik uyarıları gösterimi kapsamını ihtiyaç duyacağınız senaryoları için faydalı olabilir. Örneğin, yapabileceğiniz hello sistemde olası bir ihlali Araştırdığınız için son 24 saat hello oluşan tooaddress güvenlik uyarıları istiyor.

1. Tıklatın **filtre** hello üzerinde **güvenlik uyarıları** dikey. Merhaba **filtre** dikey penceresi açılır ve toosee istediğiniz hello tarih, durum ve önem derecesi değerlerini seçin.

    ![Güvenlik Merkezi'nde uyarıları filtreleme](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig3-2017.png)

### <a name="respond-toosecurity-alerts"></a>Yanıt toosecurity uyarıları
Bir güvenlik uyarısı toolearn seçin, adımlar varsa tetikleyen hello uyarı ve hangi hello olaylar hakkında daha fazla tootake tooremediate saldırının gerekiyor. Güvenlik uyarıları, türe ve tarihe göre gruplandırılır. Güvenlik uyarısına tıklandığında gruplanan hello uyarıları listesini içeren dikey pencere açılır.

![Azure Güvenlik Merkezi'nde toosecurity uyarılarını yanıtlama](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig5-ga.png)

Bu durumda, tetiklenen hello uyarıları toosuspicious Uzak Masaüstü Protokolü (RDP) etkinliğine bakın. Merhaba ilk sütun hangi kaynakların saldırıya gösterir; Merhaba, ikinci hello kaynak Saldırıya uğrayan kaç kez gösterir; Merhaba üçüncü hello zaman hello saldırı gösterir; Merhaba dördüncü hello uyarının durumunu gösterir; ve hello beşinci hello saldırı hello önemini gösterir. Bu bilgileri gözden geçirdikten sonra Saldırıya uğrayan hello kaynağa tıklayın ve yeni bir dikey pencere açılır.

![Azure Güvenlik Merkezi'nde güvenlik hakkında ne toodo uyarılar için öneriler](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig6-ga.png)

Merhaba, **açıklama** bu dikey pencerenin alanında bu olay hakkında daha fazla ayrıntı bulabilirsiniz. Geçerli hello kaynak IP adresi ve öneriler konusunda bu ek ayrıntılar hangi tetiklenen hello Güvenlik Uyarısı, hello hedef kaynak, bir anlayış teklif tooremediate.  Bazı durumlarda, hello kaynak IP adresi boştur (yoktur) tüm Windows güvenlik olayı günlüklerinin hello IP adresi içermediğinden.

Güvenlik Merkezi tarafından önerilen hello düzeltme according toohello güvenlik uyarısı değişir. Bazı durumlarda, diğer Azure işlevlerini tooimplement toouse olabilir hello düzeltme önerilir. Örneğin, Bu saldırının kullanarak bu saldırıyı oluşturma tooblacklist başlangıç IP adresi için düzeltme hello bir [ağ ACL'si](../virtual-network/virtual-networks-acl.md) veya [ağ güvenlik grubu](../virtual-network/virtual-networks-nsg.md) kuralı.

> [!NOTE]
> Merhaba farklı türde bir uyarı hakkında daha fazla bilgi için okuma [göre türü Azure Güvenlik Merkezi'nde güvenlik uyarılarını](security-center-alerts-type.md).
>
>

## <a name="see-also"></a>Ayrıca bkz.
Bu belgede, nasıl öğrenilen Güvenlik Merkezi'nde güvenlik ilkelerini tooconfigure. Güvenlik Merkezi hakkında daha fazla toolearn hello aşağıdaki bakın:

* [Azure Güvenlik Merkezi'nde Güvenlik Olayını İşleme](security-center-incident.md)
* [Azure Güvenlik Merkezi Algılama Özellikleri](security-center-detection-capabilities.md)
* [Azure Güvenlik Merkezi Planlama ve İşlemler Kılavuzu](security-center-planning-and-operations-guide.md)
* [Azure Güvenlik Merkezi ile ilgili SSS](security-center-faq.md) — hello hizmeti kullanımı ile ilgili sık sorulan soruları bulabilirsiniz.
* [Azure Güvenlik blogu](http://blogs.msdn.com/b/azuresecurity/) - Azure güvenliği ve uyumluluğu ile ilgili blog yazılarını bulabilirsiniz.
