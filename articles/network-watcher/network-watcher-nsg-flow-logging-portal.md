---
title: "Azure Ağ İzleyicisi ile aaaManage ağ güvenlik grubu akış günlükleri | Microsoft Docs"
description: "Bu sayfayı toomanage ağ güvenlik grubu akış Azure Ağ İzleyicisi'ni nasıl günlüğe yazacağını açıklar"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 01606cbf-d70b-40ad-bc1d-f03bb642e0af
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fb250337ab9d1a0c0d0d3569c00bc221dd102a3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-group-flow-logs-in-hello-azure-portal"></a>Ağ güvenlik grubu akış günlükleri hello Azure portalı Yönet

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [CLI 1.0](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [CLI 2.0](network-watcher-nsg-flow-logging-cli.md)
> - [REST API](network-watcher-nsg-flow-logging-rest.md)

Ağ güvenlik grubu akış günlükleri, giriş ve çıkış IP trafiği bir ağ güvenlik grubu aracılığıyla tooview bilgilerini sağlayan Ağ İzleyicisi özelliğidir. Bu akış günlükleri JSON biçiminde yazılmıştır ve önemli bilgiler sağlayan dahil olmak üzere: 

- Giden ve gelen akış kuralı başına temelinde.
- Merhaba akış hello NIC uygular.
- 5-tanımlama grubu hello akış (kaynak/hedef IP, kaynak/hedef bağlantı noktası, protokol) hakkında bilgi sağlar.
- Trafik izin verilen veya reddedilen hakkında bilgi.

## <a name="before-you-begin"></a>Başlamadan önce

Bu senaryo zaten izlediğiniz hello adımlarda varsayar [bir Ağ İzleyicisi örneği oluşturmayı](network-watcher-create.md). Merhaba senaryo aynı zamanda bir sahip olduğunuz geçerli bir sanal makine ile bir kaynak grubu varsayar.

## <a name="register-insights-provider"></a>Öngörüler sağlayıcısını Kaydet

Akış günlüğü toowork başarıyla hello **Microsoft.ınsights** sağlayıcı kaydedilmelidir. tooregister hello sağlayıcısı, aşağıdaki adımları gerçekleştirin hello: 

1. Çok Git**abonelikleri**ve ardından istediğiniz tooenable akış günlükleri hello abonelik seçin. 
2. Merhaba üzerinde **abonelik** dikey penceresinde, select **kaynak sağlayıcıları**. 
3. Ara sağlayıcılarının hello listesini ve o hello doğrulayın **Microsoft.ınsights** sağlayıcı kayıtlı. Aksi takdirde, ardından **kaydetmek**.

![Görünüm sağlayıcıları][providers]

## <a name="enable-flow-logs"></a>Akış günlükleri etkinleştir

Bu adımları bir ağ güvenlik grubu akışı açtığında etkinleştirme hello işlemi uygulayın.

### <a name="step-1"></a>1. Adım

Tooa Ağ İzleyicisi örneğine gidin ve ardından **NSG akış günlükleri**.

![Akış günlükleri genel bakış][1]

### <a name="step-2"></a>2. Adım

Bir ağ güvenlik grubu hello listeden seçin.

![Akış günlükleri genel bakış][2]

### <a name="step-3"></a>3. Adım 

Merhaba üzerinde **akışı günlüklerinin ayarları** dikey penceresinde hello durumu çok Ayarla**üzerinde**ve ardından bir depolama hesabı yapılandırın.  İşiniz bittiğinde seçin **Tamam**. Ardından **kaydetmek**.

![Akış günlükleri genel bakış][3]

## <a name="download-flow-logs"></a>Akış günlükleri indirmek

Akış günlükleri, bir depolama hesabında kaydedilir. Akış günlükleri tooview karşıdan bunları.

### <a name="step-1"></a>1. Adım

toodownload akış günlükleri, seçin **akış günlükleri yapılandırılan depolama hesaplarından indirebilirsiniz**. Bu adım hangi günlükleri toodownload seçebileceğiniz tooa depolama hesabı görünümüne alır.

![Akış günlükleri ayarlarını][4]

### <a name="step-2"></a>2. Adım

Toohello doğru depolama hesabına gidin. Ardından **kapsayıcıları** > **Öngörüler günlük networksecuritygroupflowevent**.

![Akış günlükleri ayarlarını][5]

### <a name="step-3"></a>3. Adım

Merhaba akış günlüğü toohello konumuna gidin, onu seçin ve ardından **karşıdan**.

![Akış günlükleri ayarlarını][6]

Merhaba günlük hello yapısı hakkında daha fazla bilgi için ziyaret [ağ güvenlik grubu akışı günlüğü genel bakış](network-watcher-nsg-flow-logging-overview.md).

## <a name="next-steps"></a>Sonraki adımlar

Nasıl çok öğrenin[NSG akış günlüklerinizi Powerbı ile görselleştirme](network-watcher-visualize-nsg-flow-logs-power-bi.md).

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: ./media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: ./media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: ./media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: ./media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: ./media/network-watcher-nsg-flow-logging-portal/figure6.png
[providers]: ./media/network-watcher-nsg-flow-logging-portal/providers.png
