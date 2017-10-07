---
title: "Azure CDN kaynakları aaaMonitor hello durumunu | Microsoft Docs"
description: "Nasıl toomonitor hello Azure kaynak durumu kullanarak Azure CDN kaynaklarınızın sistem durumunu öğrenin."
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: bf23bd89-35b2-4aca-ac7f-68ee02953f31
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0a77e56d2fecae4bde6c83730c05375853a6638a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hello-health-of-azure-cdn-resources"></a>Azure CDN kaynakları Hello durumunu izleme
  
Azure CDN kaynak durumu olan bir alt kümesini [Azure kaynak durumu](../resource-health/resource-health-overview.md).  Azure kaynak sistem durumu toomonitor hello CDN kaynakların durumunu kullanın ve tıklatılabilir Kılavuzu tootroubleshoot sorunları alırsınız.

>[!IMPORTANT] 
>Azure CDN kaynak durumu hello ve sistem durumu genel CDN teslim API özellikleri için yalnızca şu anda hesapları.  Azure CDN kaynak durumu tek tek CDN uç noktası doğrulamaz.
>
>Azure CDN kaynak durumu akışı hello sinyalleri too15 dakikada Gecikmeli olabilir.

## <a name="how-toofind-azure-cdn-resource-health"></a>Nasıl toofind Azure CDN kaynak durumu

1. Merhaba, [Azure portal](https://portal.azure.com), tooyour CDN profili göz atın.

2. Merhaba tıklatın **ayarları** düğmesi.

    ![Ayarlar düğmesi](./media/cdn-resource-health/cdn-profile-settings.png)

3. Altında *destek + sorun giderme*, tıklatın **kaynak durumu**.

    ![CDN kaynak durumu](./media/cdn-resource-health/cdn-resource-health3.png)

>[!TIP] 
>Hello listelenen CDN kaynakları bulabileceğiniz *kaynak durumu* döşeme hello *Yardım + Destek* dikey.  Hızlı çok alabilirsiniz*Yardım + Destek* yuvarlak içine alınmıştır hello tıklayarak **?** Merhaba sağ üst köşedeki hello portalı.
>
> ![Yardım + destek](./media/cdn-resource-health/cdn-help-support.png)

## <a name="azure-cdn-specific-messages"></a>Azure CDN özgü iletileri

Aşağıda durumları ilgili tooAzure CDN kaynak durumu bulunabilir.

|İleti | Önerilen eylem |
|---|---|
|Durdurulmuş, kaldırıldı veya bir veya daha fazla CDN uç noktalarınızı yanlış | Durduruldu, kaldırıldı veya bir veya daha fazla CDN uç noktalarınızı yanlış.|
|Özür dileriz, hello CDN yönetim hizmeti şu anda kullanılamıyor | Geri durum güncelleştirmeleri için burayı tıklatın; Çözümleme süresi Hello beklenen sonra sorun devam ederse, desteğe başvurun.|
|CDN uç noktalarınızı bazı bizim CDN sağlayıcıları ile devam eden sorunları tarafından etkilenebilir ne yazık ki | Geri durum güncelleştirmeleri için burayı tıklatın; Merhaba sorun giderme aracı toolearn kullanma tootest kaynağı ve CDN uç noktası; Çözümleme süresi Hello beklenen sonra sorun devam ederse, desteğe başvurun. |
|CDN uç noktası yapılandırma değişikliklerini yayma gecikmeleri yaşıyor ne yazık ki | Geri durum güncelleştirmeleri için burayı tıklatın; Yapılandırma değişikliklerini tam olarak beklenen hello zamanında yayılmaz ederse Destek'e başvurun.|
|Biz hello ek portal yükleme sorunları yaşamaktadır ne yazık ki | Geri durum güncelleştirmeleri için burayı tıklatın; Çözümleme süresi Hello beklenen sonra sorun devam ederse, desteğe başvurun.|
Üzgünüz, şu bizim CDN sağlayıcıları bazı sorunlar yaşıyoruz | Geri durum güncelleştirmeleri için burayı tıklatın; Çözümleme süresi Hello beklenen sonra sorun devam ederse, desteğe başvurun. |

## <a name="next-steps"></a>Sonraki adımlar

- [Azure kaynak durumu genel bir bakış okuma](../resource-health/resource-health-overview.md)
- [CDN sıkıştırma ile ilgili sorunları giderme](./cdn-troubleshoot-compression.md)
- [404 hataları ile ilgili sorunları giderme](./cdn-troubleshoot-endpoint.md)