---
title: "Azure Ağ İzleyicisi - Azure portal ile bağlantısını kontrol edin. | Microsoft Docs"
description: "Bu sayfayı Ağ İzleyicisi Azure portalını kullanarak bağlantı denetimi kullanımı açıklanmaktadır"
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
ms.openlocfilehash: 84774d0f40e06a819ca6de6cf0be68e17ba474e4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-the-azure-portal"></a>Azure portalını kullanarak Azure Ağ İzleyicisi ile bağlantısını denetleyin

> [!div class="op_single_selector"]
> - [Portal](network-watcher-connectivity-portal.md)
> - [PowerShell](network-watcher-connectivity-powershell.md)
> - [CLI 2.0](network-watcher-connectivity-cli.md)
> - [Azure REST API'si](network-watcher-connectivity-rest.md)

Bir doğrudan belirli bir uç noktası TCP bağlantısı bir sanal makineden oluşturulan olmadığını doğrulamak için bağlantı kullanmayı öğrenin.

## <a name="before-you-begin"></a>Başlamadan önce

Bu makalede, aşağıdaki kaynaklara sahip olduğunuz varsayılmaktadır:

* Ağ İzleyicisi bağlantı denetlemek istediğiniz bölgede bir örneği.

* Sanal makineler ile bağlantılarını denetlemek için.

> [!IMPORTANT]
> Bağlantı onay gerektiren bir sanal makine uzantısı `AzureNetworkWatcherExtension`. Bir Windows VM uzantısı yüklemek için ziyaret [Windows için Azure Ağ İzleyicisi Aracısı sanal makine uzantısı](../virtual-machines/windows/extensions-nwa.md) ve Linux VM ziyaret edin: [Linux için Azure Ağ İzleyicisi Aracısı sanal makine uzantısı](../virtual-machines/linux/extensions-nwa.md).

## <a name="check-connectivity-to-a-virtual-machine"></a>Bir sanal makineye bağlantısını kontrol edin.

Bu örnekte, bağlantı noktası 80 üzerinden bir hedef sanal makine bağlantısı denetler.

Ağ İzleyicisi gidin ve tıklayın **bağlantı denetimi (Önizleme)**. Bağlantısını denetlemek için sanal makineyi seçin. İçinde **hedef** bölümü seçin **bir sanal makine seçin** ve doğru sanal makine ve test etmek için bağlantı noktası seçin.

Tıkladığınızda **denetleyin**, belirtilen bağlantı noktası sanal makineleri arasındaki bağlantıyı denetlenir. Örnekte, hedef VM erişilemiyor, atlama listesi gösterilir.

![Bir sanal makine için denetim bağlantı sonuçları][1]

## <a name="check-remote-endpoint-connectivity"></a>Uzak uç noktada bağlantısını kontrol edin.

Bağlantısını ve uzak uç nokta için gecikme süresini denetlemek için seçin **el ile belirt** radyo düğmesini **hedef** bölümünde, url ve bağlantı noktasını girin ve tıklatın **denetleyin**.  Bu, Web siteleri ve depolama uç noktaları gibi uzak uç noktalar için kullanılır.

![Bir web sitesi için bağlantı sonuçları denetleyin][2]

## <a name="next-steps"></a>Sonraki adımlar

Sanal makine uyarılarla paket yakalamaları görüntüleyerek otomatikleştirmeyi öğrenin [bir uyarı tetiklenen paket yakalama oluşturma](network-watcher-alert-triggered-packet-capture.md)

Belirli trafik içinde veya dışında VM ziyaret ederek izin verilip verilmediğini Bul [denetleyin IP akış doğrulayın](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-connectivity-portal/figure1.png
[2]: ./media/network-watcher-connectivity-portal/figure2.png
