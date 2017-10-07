---
title: "Azure Ağ İzleyicisi'ni ve açık kaynaklı araçları ile aaaVisualize ağ trafiği desenlerini | Microsoft Docs"
description: "Bu sayfa, vm'lerden Capanalysis toovisualize trafiği desenlerini tooand toouse Ağ İzleyicisi paket nasıl yakalama açıklar."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 936d881b-49f9-4798-8e45-d7185ec9fe89
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fca9a226729162cd90d412c7b699ac54d2257a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-network-traffic-patterns-tooand-from-your-vms-using-open-source-tools"></a>Ağ trafiği desenlerini tooand açık kaynaklı araçları kullanarak, vm'lerden Görselleştirme

Paket yakalama tooperform ağ hukuk ve derin paket incelemesi izin ağ verileri içerir. Kaynak araç ağınız hakkında tooanalyze paket yakalamaları toogain Öngörüler kullanabileceğiniz birçok açılır vardır. Böyle bir araç CapAnalysis, bir açık kaynak paket yakalama görselleştirme Aracı ' dir. Paket yakalama veri görselleştirme tooquickly türetilen Öngörüler modelleri ve anormallikleri ağınızdaki bir değerli yoludur. Görselleştirmeleri de böyle Öngörüler apı'lerinizi bir şekilde paylaşma olanağı sağlar.

Ağınızda tooperform paket sağlayarak bu değerli verileri yakalar özelliği toocapture hello Azure'nın Ağ İzleyicisi sağlar. Bu makalede, paket toovisualize ve kazanç bilgiler nasıl yakalar CapAnalysis ile Ağ İzleyicisi'ni kullanarak bir kılavuz sağlar.

## <a name="scenario"></a>Senaryo

Dağıtılan basit bir web uygulaması olan bir VM'de Azure istediğiniz toouse açık kaynaklı araçları toovisualize kendi ağ trafiği tooquickly tanımla akış desenleri ve tüm olası anormallikleri. Ağ İzleyicisi ile ağ ortamınızın bir paket yakalama elde ve doğrudan depolama hesabınıza saklayın. CapAnalysis hello paket yakalama doğrudan hello depolama blobu gelen alma ve içeriğini görselleştirin.

![senaryo][1]

## <a name="steps"></a>Adımlar

### <a name="install-capanalysis"></a>CapAnalysis yükleyin

tooinstall CapAnalysis bir sanal makinede toohello resmi yönergeleri başvurabilir burada https://www.capanalysis.net/ca/how-to-install-capanalysis.
CapAnalysis uzaktan erişim, yeni bir gelen güvenlik kuralı ekleyerek tooopen bağlantı noktası 9877 VM ihtiyacımız. Ağ güvenlik grupları kuralları oluşturma hakkında daha fazla bilgi için çok başvurmak[içinde varolan bir NSG kuralları oluşturma](../virtual-network/virtual-networks-create-nsg-arm-pportal.md#create-rules-in-an-existing-nsg). Merhaba kural başarıyla eklendikten sonra mümkün tooaccess CapAnalysis olmalıdır gelen`http://<PublicIP>:9877`

### <a name="use-azure-network-watcher-toostart-a-packet-capture-session"></a>Bir paket yakalama oturum Azure Ağ İzleyicisi toostart kullanın

Ağ İzleyicisi toocapture paketleri tootrack ve giden trafiği filtrelemek bir sanal makine sağlar. Toohello yönergeleri başvurabilir [Yönet paket yakalar Ağ İzleyicisi ile](network-watcher-packet-capture-manage-portal.md) bir paket yakalama oturumunu toostart. Bu paket yakalama CapAnalysis tarafından erişilen bir depolama blob toobe depolanabilir.

### <a name="upload-a-packet-capture-toocapanalysis"></a>Paket yakalama tooCapAnalysis karşıya yükle
Doğrudan hello paket yakalama depolandığı hello "URL'den alma" sekmesini kullanarak ve bir bağlantı toohello depolama blobu sağlayarak Ağ İzleyicisi tarafından gerçekleştirilen bir paket yakalama karşıya yükleyebilirsiniz.

Bir bağlantı tooCapAnalysis sağlanırken emin tooappend bir SAS belirteci toohello depolama blob URL'si olun.  toodo Bu, tooShared erişim imzası hello depolama hesabından gidin, iznine hello atamak ve bir belirteç hello SAS Oluştur düğmesine toocreate tuşuna basın. Ardından bu SAS belirteci toohello paket yakalama depolama blob URL'si ekleyebilirsiniz.

Hello elde edilen URL şöyle görünecektir: http://storageaccount.blob.core.windows.net/container/location?addSASkeyhere


### <a name="analyzing-packet-captures"></a>Analiz etme paket yakalar

CapAnalysis çeşitli seçenekler toovisualize paket yakalama, farklı açısından sağlayan her analizi sunar. Bu görsel özetler ile ağ trafiği eğilimleri anlamak ve hızlı bir şekilde tüm olağandışı nokta. Bu özelliklerden bazılarını listesi aşağıdaki hello gösterilmektedir:

1. Akış tabloları

    Bu tablo, hello paket veri akışlarında listesi Merhaba, zaman damgası başlangıç akışları ile ilişkili hello ve hello akış yanı sıra ile kaynak ve hedef IP ilişkili çeşitli protokoller hello sağlar.

    ![capanalysis akış sayfası][5]

1. Protokolü'ne genel bakış

    Bu bölme sağlar tooquickly çeşitli protokolleri ve coğrafyalara bu hello dağıtım ağ trafiği hello bakın.

    ![capanalysis Protokolü'ne genel bakış][6]

1. İstatistikler

    Bu bölme, tooview ağ trafiği istatistikleri – bayt gönderildi ve kaynak ve hedef IP, Akışlar hello kaynak ve hedef IP, her birinin için alınan Protokolü çeşitli akışları ve hello süre akışları için kullanılan sağlar.

    ![capanalysis istatistikleri][7]

1. geomap

    Bu bölme toohello hacimli trafik her ülkedeki ölçeklendirme renkler, ağ trafiğinizi olan bir harita görünümü sağlar. Gönderilen ve bu ülkede IP'leri alınan veriler hello oranını gibi vurgulanan ülkelerde tooview ek akış istatistikleri seçebilirsiniz.

    ![geomap][8]

1. Filtreler

    CapAnalysis belirli paketlerin hızlı çözümleme için bir filtre kümesi sağlar. Örneğin, bu alt trafik üzerinde Protokolü toogain belirli Öngörüler tarafından toofilter hello veri seçebilirsiniz.

    ![filtreleri][11]

    Ziyaret [https://www.capanalysis.net/ca/#about](https://www.capanalysis.net/ca/#about) toolearn tüm CapAnalysis özellikleri hakkında daha fazla.

## <a name="conclusion"></a>Sonuç

Ağ İzleyicisi'nin paket yakalama özelliği, ağ trafiğinizi daha iyi anlamak ve toocapture hello veri gerekli tooperform ağ hukuk sağlar. Bu senaryoda, nasıl Ağ İzleyicisi paket görüntüleri kolayca açık kaynak görselleştirme araçları ile tümleştirilebilir gösterdi. CapAnalysis toovisualize paketleri yakalar gibi açık kaynaklı araçları kullanarak, ayrıntılı paket incelemesi gerçekleştiren ve hızlı bir şekilde ağ trafiğinizi içinde eğilimleri belirlemek.

## <a name="next-steps"></a>Sonraki adımlar

NSG akış günlükleri, hakkında daha fazla toolearn ziyaret [NSG akış günlükleri](network-watcher-nsg-flow-logging-overview.md)

Toovisualize NSG akışınız Power BI ile ziyaret ederek nasıl oturum öğrenin [görselleştirmek NSG akar Power BI ile günlükleri](network-watcher-visualize-nsg-flow-logs-power-bi.md)
<!--Image references-->

[1]: ./media/network-watcher-using-open-source-tools/figure1.png
[2]: ./media/network-watcher-using-open-source-tools/figure2.png
[3]: ./media/network-watcher-using-open-source-tools/figure3.png
[4]: ./media/network-watcher-using-open-source-tools/figure4.png
[5]: ./media/network-watcher-using-open-source-tools/figure5.png
[6]: ./media/network-watcher-using-open-source-tools/figure6.png
[7]: ./media/network-watcher-using-open-source-tools/figure7.png
[8]: ./media/network-watcher-using-open-source-tools/figure8.png
[9]: ./media/network-watcher-using-open-source-tools/figure9.png
[10]: ./media/network-watcher-using-open-source-tools/figure10.png
[11]: ./media/network-watcher-using-open-source-tools/figure11.png
