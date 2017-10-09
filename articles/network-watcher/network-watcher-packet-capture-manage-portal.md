---
title: "aaaManage paket yakalar Azure Ağ İzleyicisi - Azure portalı | Microsoft Docs"
description: "Bu sayfayı nasıl toomanage hello paket yakalama özelliği ağ Azure portalını kullanarak izleyicisinin açıklar"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 59edd945-34ad-4008-809e-ea904781d918
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 431b145ee215b8d9421fb2aacdce08a0de90b35e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-packet-captures-with-azure-network-watcher-using-hello-portal"></a>Paket yakalama hello portalı kullanarak Azure Ağ İzleyicisi ile yönetme

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-packet-capture-manage-portal.md)
> - [PowerShell](network-watcher-packet-capture-manage-powershell.md)
> - [CLI 1.0](network-watcher-packet-capture-manage-cli-nodejs.md)
> - [CLI 2.0](network-watcher-packet-capture-manage-cli.md)
> - [Azure REST API'si](network-watcher-packet-capture-manage-rest.md)

Ağ İzleyicisi paket yakalama toocreate yakalama oturumları tootrack trafiği tooand bir sanal makineden sağlar. Filtreler, yalnızca istediğiniz hello trafiği yakalamak hello yakalama oturum tooensure için sağlanır. Paket yakalama toodiagnose ağ anormallikleri Tepkisel ve önceden yardımcı olur. Diğer kullanımlar bilgi ağ yetkisiz erişim, toodebug istemci-sunucu iletişimleri ve daha fazlasını sağlamasını ağ istatistikleri toplama içerir. Mümkün tooremotely tetikleyici paket yakalamaları olma yoluyla bu özelliği bir paket yakalama el ile ve değerli zaman kazandırır hello istenen makine üzerinde çalışan hello yük kolaylaştırır.

Bu makalede paket yakalama için şu anda kullanılabilir farklı yönetim görevleri hello alır.

- [**Paket yakalama Başlat**](#start-a-packet-capture)
- [**Paket yakalama işlemini durdurun**](#stop-a-packet-capture)
- [**Paket yakalama Sil**](#delete-a-packet-capture)
- [**Paket yakalama indirin**](#download-a-packet-capture)

## <a name="before-you-begin"></a>Başlamadan önce

Bu makalede, kaynakları aşağıdaki hello sahibi olduğunuzu varsayar:

- Bir örneği toocreate paket yakalama istediğiniz Ağ İzleyicisinin hello bölgede
- Merhaba paket sahip bir sanal makine uzantısı etkin yakalayın.

> [!IMPORTANT]
> Paket yakalama gerektiren bir sanal makine uzantısı `AzureNetworkWatcherExtension`. Bir Windows VM Hello uzantısı yüklemek için ziyaret [Windows için Azure Ağ İzleyicisi Aracısı sanal makine uzantısı](../virtual-machines/windows/extensions-nwa.md) ve Linux VM ziyaret edin: [Azure Ağ İzleyicisi Aracısı sanal makine uzantısı Linuxiçin](../virtual-machines/linux/extensions-nwa.md).

### <a name="packet-capture-agent-extension-through-hello-portal"></a>Paket Yakalama aracı uzantısı hello portal üzerinden

tooinstall hello paket yakalama VM Aracısı hello portal üzerinden tooyour sanal makine gidin, tıklatın **uzantıları** > **Ekle** arayın ve **için Ağ İzleyicisi Aracısı Windows**

![Aracı görünümü][agent]

## <a name="packet-capture-overview"></a>Paket yakalama genel bakış

Toohello gidin [Azure portal](https://portal.azure.com) tıklatıp **ağ** > **Ağ İzleyicisi** > **paket yakalama**

Tüm paket listesini hello durumu olsun mevcut yakalar Hello genel bakış sayfasında gösterilir.

> [!NOTE]
> Paket yakalama bağlantı noktası 443 üzerinden bağlantı toohello depolama hesabı gerektirir.

![Paket yakalama genel bakış ekranı][1]

## <a name="start-a-packet-capture"></a>Paket yakalama Başlat

Tıklatın **Ekle** toocreate paket yakalama.

bir paket yakalama tanımlanabilir hello özellikleri şunlardır:

**Ana ayarları**

- **Abonelik** -bu değeri kullanılır hello abonelik, Ağ İzleyicisi örneği her abonelik için gereklidir.
- **Kaynak grubu** -hello sanal makinesinin, hedef alındığını hello kaynak grubu.
- **Hedef sanal makine** -hello paket yakalama çalıştıran hello sanal makine
- **Paket yakalama adı** -bu değer hello hello paket yakalama adıdır.

**Yapılandırma Yakalama**

- **Depolama hesabı** -paket yakalama bir depolama hesabında kaydedilip kaydedilmeyeceğini belirler.
- **Dosya** -paket yakalama hello sanal makinede yerel olarak kaydedilirse belirler.
- **Depolama hesapları** -hello seçili depolama hesabına toosave hello paket yakalama. Varsayılan konumdur https://{storage hesap name}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscription kimliği} /resourcegroups/ {kaynak grubu name}/providers/microsoft.compute/virtualmachines/{virtual makine adı} / {YY} / {MM} / {gg} / {ss} packetcapture__{MM}_{SS} _ {XXX} .cap. (Yalnızca etkin olup **depolama** seçili)
- **Yerel dosya yolu** -bir sanal makine toosave hello paket yakalama hello yerel yol. (Yalnızca etkin olup **dosya** seçilir). Geçerli bir yol sağlanmalıdır
- **Paket başına en fazla bayt** -hello numarası yakalanan bayt gelen her paket, tüm baytlar boş bırakılırsa yakalanır.
- **Oturum başına en fazla bayt** - toplam hello değeri hello paket yakalama durakları ulaşıldıktan sonra yakalanan bayt sayısı.
- **Süre (saniye)** -hello paket yakalama toostop için zaman sınırını ayarlar. Varsayılan değer 18000 saniyedir.

> [!NOTE]
> Paket depolama yakalar için premium depolama hesapları şu anda desteklenmemektedir.

**(İsteğe bağlı) filtreleme**

- **Protokol** -hello paket yakalama için Protokolü toofilter hello. Merhaba değerleri TCP, UDP ve herhangi bir kullanılabilir.
- **Yerel IP adresi** -hello yerel IP adresi bu filtre değeri eşleştiği hello paket yakalama toopackets bu değeri filtreler.
- **Yerel bağlantı noktası** -hello yerel bağlantı noktası bu filtre değeri eşleştiği hello paket yakalama toopackets bu değeri filtreler.
- **Uzak IP adresi** -hello uzak IP Bu filtre değeri eşleştiği hello paket yakalama toopackets bu değeri filtreler.
- **Uzak bağlantı noktası** -hello uzak bağlantı noktası bu filtre değeri eşleştiği hello paket yakalama toopackets bu değeri filtreler.

> [!NOTE]
> Bağlantı noktası ve IP adresi değerleri, tek bir değer, değer aralığı veya bir kümesi olabilir. (diğer bir deyişle, bağlantı noktası 80-1024 için) İstediğiniz sayıda filtreleri tanımlayabilirsiniz.

Merhaba değerleri doldurulduktan sonra tıklayın **Tamam** toocreate hello paket yakalama.

![Paket yakalama oluşturma][2]

Üzerinde Hello zaman sınırı ayarladıktan sonra hello paket yakalama süresi doldu, hello paket yakalama durdurur ve gözden geçirilebilir. El ile de hello paket yakalamaları oturumları durdurabilirsiniz.

## <a name="delete-a-packet-capture"></a>Paket yakalama Sil

Merhaba pakette görünümünü yakalama, hello tıklatın **bağlam menüsü** (...) veya sağ tıklatın ve'ı tıklatın **silmek** toostop hello paket yakalama

![Paket yakalama Sil][3]

> [!NOTE]
> Paket yakalama silindiğinde hello depolama hesabındaki hello dosya silinmez.

Bunu Sorduğunuza toodelete hello paket yakalama istediğiniz tooconfirm tıklatın **Evet**

![Onaylama][4]

## <a name="stop-a-packet-capture"></a>Paket yakalama işlemini durdurun

Merhaba pakette görünümünü yakalama, hello tıklatın **bağlam menüsü** (...) veya sağ tıklatın ve'ı tıklatın **durdurmak** toostop hello paket yakalama

## <a name="download-a-packet-capture"></a>Paket yakalama indirin

Paket yakalama oturumunuz tamamladıktan sonra hello yakalama dosyasını karşıya yüklenen tooblob depolama veya tooa yerel hello VM üzerinde bir dosyadır. Merhaba paket yakalama Hello depolama konumu hello oturum oluşturma sırasında tanımlanır. Bu yakalama uygun aracı tooaccess kaydedilmiş tooa depolama hesabıdır burada indirilebilir Microsoft Azure Storage Gezgini dosyaları: http://storageexplorer.com/

Bir depolama hesabı belirtilirse, paket yakalama dosyalarını tooa depolama hesabı konumu aşağıdaki hello kaydedilir:
```
https://{storageAccountName}.blob.core.windows.net/network-watcher-logs/subscriptions/{subscriptionId}/resourcegroups/{storageAccountResourceGroup}/providers/microsoft.compute/virtualmachines/{VMName}/{year}/{month}/{day}/packetCapture_{creationTime}.cap
```

## <a name="next-steps"></a>Sonraki adımlar

Nasıl sanal makine uyarılarla tooautomate paket görüntüleyerek yakalar öğrenin [bir uyarı tetiklenen paket yakalama oluşturma](network-watcher-alert-triggered-packet-capture.md)

Belirli trafik içinde veya dışında VM ziyaret ederek izin verilip verilmediğini Bul [denetleyin IP akış doğrulayın](network-watcher-check-ip-flow-verify-portal.md)

<!-- Image references -->
[1]: ./media/network-watcher-packet-capture-manage-portal/figure1.png
[2]: ./media/network-watcher-packet-capture-manage-portal/figure2.png
[3]: ./media/network-watcher-packet-capture-manage-portal/figure3.png
[4]: ./media/network-watcher-packet-capture-manage-portal/figure4.png
[agent]: ./media/network-watcher-packet-capture-manage-portal/agent.png













