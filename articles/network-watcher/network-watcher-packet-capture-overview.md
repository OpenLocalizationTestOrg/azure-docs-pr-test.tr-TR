---
title: "Azure Ağ İzleyicisi aaaIntroduction tooPacket yakalama | Microsoft Docs"
description: "Bu sayfa hello Ağ İzleyicisi paket yakalama özelliği genel bir bakış sağlar"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3a81afaa-ecd9-4004-b68e-69ab56913356
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2ce01b391b9c1a1c19aa29c8620628c55586df03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toovariable-packet-capture-in-azure-network-watcher"></a>Azure Ağ İzleyicisi giriş toovariable paket yakalama

Ağ İzleyicisi değişken paket yakalama toocreate paket yakalama oturumları tootrack trafiği tooand bir sanal makineden sağlar. Paket yakalama toodiagnose ağ anormallikleri hem Tepkisel yardımcı olur ve proactivity. Diğer kullanımlar bilgi ağ yetkisiz erişim, toodebug istemci-sunucu iletişimleri ve daha fazlasını sağlamasını ağ istatistikleri toplama içerir.

Paket yakalama Ağ İzleyicisi uzaktan başlatılan bir sanal makine uzantısıdır. Bu özellik, bir paket yakalama istenen hello sanal değerli zaman kazandırır makineye el ile çalışan hello yük kolaylaştırır. Paket yakalama hello portal, PowerShell'i, CLI veya REST API tetiklenebilir. Paket yakalama nasıl tetiklenebilir bir sanal makine uyarılara örnektir. Filtreler toomonitor istediğiniz trafiği yakalamak için Hello yakalama oturum tooensure sağlanır. Filtreler, 5-tanımlama grubu üzerinde (protokolü, yerel IP adresi, uzak IP adresi, yerel bağlantı noktası ve uzak bağlantı noktası) dayalı bilgileri. Merhaba Yakalanan veriler hello yerel disk veya bir depolama blob depolanır. Her Abonelikteki bölge başına 10 paket yakalama oturumu sınırı yoktur. Bu sınır yalnızca toohello oturumları uygular ve paket yakalama dosyalarını hello VM yerel olarak veya bir depolama hesabı kaydedilmiş toohello geçerli değildir.

> [!IMPORTANT]
> Paket yakalama gerektiren bir sanal makine uzantısı `AzureNetworkWatcherExtension`. Bir Windows VM Hello uzantısı yüklemek için ziyaret [Windows için Azure Ağ İzleyicisi Aracısı sanal makine uzantısı](../virtual-machines/windows/extensions-nwa.md) ve Linux VM ziyaret edin: [Azure Ağ İzleyicisi Aracısı sanal makine uzantısı Linuxiçin](../virtual-machines/linux/extensions-nwa.md).

tooreduce hello bilgileri tooonly hello bilgileri yakalamak, hello paket yakalama oturum açmak için kullanılabilen seçenekler şunlardır:

**Yapılandırma Yakalama**

|Özellik|Açıklama|
|---|---|
|**Paket (bayt) başına en fazla bayt sayısı** | Merhaba numarası yakalanan bayt gelen her paket, tüm baytlar boş bırakılırsa yakalanır. Merhaba numarası yakalanan bayt gelen her paket, tüm baytlar boş bırakılırsa yakalanır. Yalnızca hello IPv4 üst bilgisi – gerekirse burada 34 belirtin |
|**Oturum (bayt) başına en fazla bayt sayısı** | Merhaba değeri hello oturumu sonra erene ulaşıldığında, bayt toplam sayısı yakalanır.|
|**Süre (saniye)** | Hello paket zaman kısıtlama kümelerini oturum yakalayın. Merhaba varsayılan 18000 saniye veya 5 saat değeridir.|

**(İsteğe bağlı) filtreleme**

|Özellik|Açıklama|
|---|---|
|**Protokol** | Merhaba Protokolü toofilter hello paket için yakalayın. Merhaba değerleri TCP, UDP ve tüm kullanılabilir.|
|**Yerel IP adresi** | Bu değer, hello yerel IP adresi bu filtre değeri eşleştiği hello paket yakalama toopackets filtreler.|
|**Yerel bağlantı noktası** | Bu değer filtreleri hello paket hello yerel bağlantı noktası bu filtre değeri eşleştiği toopackets yakalayın.|
|**Uzak IP adresi** | Bu değer filtreleri hello paket hello uzak IP Bu filtre değeri eşleştiği toopackets yakalayın.|
|**Uzak bağlantı noktası** | Bu değer filtreleri hello paket hello uzak bağlantı noktası bu filtre değeri eşleştiği toopackets yakalayın.|

### <a name="next-steps"></a>Sonraki adımlar

Paket yakalama hello Portalı aracılığıyla ziyaret ederek nasıl yönetebileceğiniz öğrenin [paket yakalama hello Azure portalı Yönet](network-watcher-packet-capture-manage-portal.md) veya şu adresi ziyaret ederek PowerShell ile [PowerShell ile paket yakalama yönetmek](network-watcher-packet-capture-manage-powershell.md).

Sanal makine uyarılar ziyaret ederek temelinde nasıl toocreate öngörülü paket yakalar öğrenin [bir uyarı tetiklenen paket yakalama oluşturma](network-watcher-alert-triggered-packet-capture.md)

<!--Image references-->
[1]: ./media/network-watcher-packet-capture-overview/figure1.png













