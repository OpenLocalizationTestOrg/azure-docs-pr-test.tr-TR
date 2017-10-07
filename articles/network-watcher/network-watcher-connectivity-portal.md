---
title: "Azure Ağ İzleyicisi - Azure portal ile aaaCheck bağlantısı | Microsoft Docs"
description: "Bu sayfayı nasıl toouse bağlantısını denetleyin Ağ İzleyicisi Merhaba Azure portal kullanarak açıklar"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: gwallace
ms.openlocfilehash: ef6ecccd688f06f70003a5b59771c15bcbe8f3e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-hello-azure-portal"></a>Hello Azure portal kullanarak Azure Ağ İzleyicisi ile bağlantısını denetleyin

> [!div class="op_single_selector"]
> - [Portal](network-watcher-connectivity-portal.md)
> - [PowerShell](network-watcher-connectivity-powershell.md)
> - [CLI 2.0](network-watcher-connectivity-cli.md)
> - [Azure REST API'si](network-watcher-connectivity-rest.md)

Toouse bağlantı tooverify doğrudan TCP bağlantısı, uç nokta verilen bir sanal makine tooa nasıl kurulabilir öğrenin.

## <a name="before-you-begin"></a>Başlamadan önce

Bu makalede, kaynakları aşağıdaki hello olduğu varsayılır:

* Bir örneği toocheck bağlantı istediğiniz Ağ İzleyicisinin hello bölgede.

* Sanal makineler toocheck bağlantısına sahip.

> [!IMPORTANT]
> Bağlantı onay gerektiren bir sanal makine uzantısı `AzureNetworkWatcherExtension`. Bir Windows VM Hello uzantısı yüklemek için ziyaret [Windows için Azure Ağ İzleyicisi Aracısı sanal makine uzantısı](../virtual-machines/windows/extensions-nwa.md) ve Linux VM ziyaret edin: [Azure Ağ İzleyicisi Aracısı sanal makine uzantısı Linuxiçin](../virtual-machines/linux/extensions-nwa.md).

## <a name="check-connectivity-tooa-virtual-machine"></a>Bağlantı tooa sanal makine kontrol edin

Bu örnekte, bağlantı noktası 80 üzerinden bağlantı tooa hedef sanal makine denetler.

Ağ İzleyicisi tooyour gidin ve tıklayın **bağlantı denetimi (Önizleme)**. Merhaba sanal makine toocheck bağlantısını seçin. Merhaba, **hedef** bölümü seçin **bir sanal makine seçin** hello doğru sanal makine ve bağlantı noktası tootest seçin.

Tıkladığınızda **denetleyin**, belirtilen başlangıç bağlantı noktası hello sanal makineler arasında hello bağlantı denetlenir. Merhaba örnekte hello hedef VM erişilemiyor, atlama listesi gösterilir.

![Bir sanal makine için denetim bağlantı sonuçları][1]

## <a name="check-remote-endpoint-connectivity"></a>Uzak uç noktada bağlantısını kontrol edin.

toocheck hello bağlantısı ve gecikme tooa uzak uç nokta, seçim hello **el ile belirtin** hello radyo düğmesini **hedef** bölümünde, giriş hello url ve başlangıç bağlantı noktası ve tıklatın **denetleyin** .  Bu, Web siteleri ve depolama uç noktaları gibi uzak uç noktalar için kullanılır.

![Bir web sitesi için bağlantı sonuçları denetleyin][2]

## <a name="next-steps"></a>Sonraki adımlar

Nasıl sanal makine uyarılarla tooautomate paket görüntüleyerek yakalar öğrenin [bir uyarı tetiklenen paket yakalama oluşturma](network-watcher-alert-triggered-packet-capture.md)

Belirli trafik içinde veya dışında VM ziyaret ederek izin verilip verilmediğini Bul [denetleyin IP akış doğrulayın](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-connectivity-portal/figure1.png
[2]: ./media/network-watcher-connectivity-portal/figure2.png
