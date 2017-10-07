---
title: "aaaCreate Azure günlük analizi özel bir Panoda | Microsoft Docs"
description: "Bu kılavuz, günlük analizi panolar tüm kaydedilmiş günlük işlemlerinizin nasıl görselleştirebilirsiniz anlamanıza yardımcı olur, size tek bir mercek tooview ortamınızı."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: abb07f6c-b356-4f15-85f5-60e4415d0ba2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 73fcf131a91c743d473f37d5a40d52eaf78a7ba3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-dashboard-for-use-in-log-analytics"></a>Günlük analizi kullanmak için özel bir pano oluşturun

>[!NOTE]
> Çalışma alanınızı yükseltilmiş toohello yüklediyse [yeni günlük analizi sorgu dili](log-analytics-log-search-upgrade.md), sonra yeni panolar oluşturun veya varolan Pano düzenleyin. 

Bu kılavuz, günlük analizi panolar tüm kaydedilmiş günlük işlemlerinizin nasıl görselleştirebilirsiniz anlamanıza yardımcı olur, size tek bir mercek tooview ortamınızı.

![Örnek Pano](./media/log-analytics-dashboards/oms-dashboards-example-dash.png)

Merhaba OMS portalında oluşturduğunuz tüm hello özel panolar hello OMS mobil uygulama de kullanılabilir. Sayfaları hello uygulamalar hakkında daha fazla bilgi için aşağıdaki hello bakın.

* [Merhaba Microsoft Store mobil uygulamadan OMS](http://www.windowsphone.com/store/app/operational-insights/4823b935-83ce-466c-82bb-bd0a3f58d865)
* [Apple iTunes mobil uygulamadan OMS](https://itunes.apple.com/app/microsoft-operations-management/id1042424859?mt=8)

![Mobil Pano](./media/log-analytics-dashboards/oms-search-mobile.png)

## <a name="how-do-i-create-my-dashboard"></a>Benim Panom nasıl oluşturulur?
toobegin, Git toohello OMS genel bakış sayfası. Merhaba görürsünüz **My Pano** hello sol bölme. Toodrill aşağı panonuza tıklatın.

![Genel Bakış](./media/log-analytics-dashboards/oms-dashboards-overview.png)

## <a name="adding-a-tile"></a>Bir kutucuk ekleme
Uygulamasındaki panolar, kutucuk tarafından kaydedilmiş günlük işlemlerinizin güç sağlar. OMS hemen başlayabilmesi için kaydedilmiş günlük aramalar, önceden yapılan çoğu ile birlikte gelir. Kullanım hello aşağıdaki adımları bu anahattı nasıl toobegin.

Hello My Pano görünümü, tıklamanız yeterlidir **Özelleştir** tooenter modu özelleştirin.

![Resimsel](./media/log-analytics-dashboards/oms-dashboards-pictorial01.png)

 Merhaba sağ tarafında hello sayfası açılır hello paneli tüm çalışma alanınızı 's kaydedilmiş günlük aramaları gösterir. kaydedilmiş günlük bir kutucuk arama toovisualize kaydedilmiş bir aramayı üzerine gelin ve hello ardından **artı** simgesi.

![Kutucuk 1 Ekle](./media/log-analytics-dashboards/oms-dashboards-pictorial02.png)

Merhaba tıkladığınızda **artı** simge, yeni bir kutucuk hello My Pano görünümü görüntülenir.

![Kutucuk 2 Ekle](./media/log-analytics-dashboards/oms-dashboards-pictorial03.png)

## <a name="edit-a-tile"></a>Bir kutucuk Düzenle
Hello My Pano görünümü, tıklamanız yeterlidir **Özelleştir** tooenter modu özelleştirin. Tooedit istediğiniz hello kutucuğa tıklayın. Merhaba sağ panelde tooedit değiştirir ve Seçenekler seçim verir:

![Döşeme Düzenle](./media/log-analytics-dashboards/oms-dashboards-pictorial04.png)

![Döşeme Düzenle](./media/log-analytics-dashboards/oms-dashboards-pictorial05.png)

### <a name="tile-visualizations"></a>Döşeme görselleştirmeleri
Döşeme görselleştirmeleri toochoose üç tür vardır:

| grafik türü | ne yapar |
| --- | --- |
| ![Çubuk grafiği](./media/log-analytics-dashboards/oms-dashboards-bar-chart.png) |Günlük arama sonuçları bir alana göre veya toplar, kaydedilmiş günlük aramanın sonuçları bir zaman çizelgesi olarak bir çubuk grafik veya bağlı olarak bir alana göre sonuçlarının bir listesini görüntüler. |
| ![Ölçüm](./media/log-analytics-dashboards/oms-dashboards-metric.png) |Toplam günlük arama sonucu isabet döşeme içinde bir sayı olarak görüntüler. Ölçüm döşeme tooset hello Eşiğe ulaşıldığında hello döşeme vurgular bir eşiği izin verin. |
| ![Satır](./media/log-analytics-dashboards/oms-dashboards-line.png) |Bir zaman çizelgesi, kaydedilmiş günlük arama sonucu isabet değerleri içeren bir çizgi grafiği görüntüler. |

### <a name="threshold"></a>Eşik
Bir eşik hello ölçüm görselleştirme kullanarak bir kutucuğu oluşturabilirsiniz. Üzerinde toocreate hello kutucuğuna bir eşik değeri seçin. Merhaba değeri üzerinden veya hello seçilen eşiğin altında olduğunda toohighlight hello döşeme sonra olup olmadığını hello eşik değeri aşağıdaki kümesini seçin.

## <a name="organizing-hello-dashboard"></a>Merhaba Pano düzenleme
tooorganize panonuz, toohello My Pano görünümüne gidin ve tıklatın **Özelleştir** tooenter modu özelleştirin. ' I tıklatın ve istediğiniz toomove ve döşeme toobe istediğiniz toowhere taşıma hello bölmesi sürükleyin.

![Pano düzenleme](./media/log-analytics-dashboards/oms-dashboards-organize.png)

## <a name="remove-a-tile"></a>Bir kutucuğunu kaldırma
tooremove bir kutucuk toohello My Pano görünümüne gidin ve'ı tıklatın **Özelleştir** tooenter modu özelleştirin. Tooremove istediğiniz, ardından hello sağ paneldeki select hello döşeme **kaldırmak döşeme**.

![Bir kutucuğunu kaldırma](./media/log-analytics-dashboards/oms-dashboards-remove-tile.png)

## <a name="next-steps"></a>Sonraki adımlar
* Oluşturma [uyarıları](log-analytics-alerts.md) günlük analizi toogenerate bildirimleri ve tooremediate sorunları.
