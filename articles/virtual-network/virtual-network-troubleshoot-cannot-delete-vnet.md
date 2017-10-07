---
title: "aaaCannot Sil Azure sanal ağında | Microsoft Docs"
description: "Nasıl tootroubleshoot hello Azure sanal ağında silemezsiniz sorun hakkında bilgi edinin."
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: genli
ms.openlocfilehash: a9050ab238ccb0380fd46130430222efb8f42388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-failed-toodelete-a-virtual-network-in-azure"></a>Sorun giderme: toodelete Azure sanal ağında başarısız oldu

Microsoft Azure sanal ağında toodelete çalıştığınızda hata alabilirsiniz. Bu makalede, sorun giderme adımları toohelp sağlanmaktadır. Bu sorunu çözün. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a>Sorun giderme rehberi 

1. [Bir sanal ağ geçidi hello sanal ağda çalışır durumda olup olmadığını denetleyin](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).
2. [Bir uygulama ağ geçidi hello sanal ağda çalışır durumda olup olmadığını denetleyin](#check-whether-an-application-gateway-is-running-in-the-virtual-network).
3. [Azure Active Directory etki alanı hizmeti hello sanal ağında etkinleştirilip etkinleştirilmediğini kontrol](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).
4. [Merhaba sanal ağ bağlantılı tooother kaynak olup olmadığını denetleyin](#check-whether-the-virtual-network-is-connected-to-other-resource).
5. [Bir sanal makine hello sanal ağında hala çalışıp çalışmadığını denetleyin](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).
6. [Merhaba sanal ağ içinde geçiş takıldı olup olmadığını denetleyin](#check-whether-the-virtual-network-is-stuck-in-migration).

## <a name="troubleshooting-steps"></a>Sorun giderme adımları

### <a name="check-whether-a-virtual-network-gateway-is-running-in-hello-virtual-network"></a>Bir sanal ağ geçidi hello sanal ağda çalışır durumda olup olmadığını denetleyin

tooremove hello sanal ağ, hello sanal ağ geçidi önce kaldırmanız gerekir.

Klasik sanal ağlar için toohello Git **genel bakış** sayfa hello Azure Portalı'nda hello Klasik sanal ağ. Merhaba, **VPN bağlantıları** bölümünde, hello ağ geçidi hello sanal ağda çalışıyorsa, hello IP görürsünüz hello ağ geçidi adresi. 

![Ağ geçidi çalışır durumda olup olmadığını denetleyin](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

Sanal ağlar için toohello Git **genel bakış** hello sanal ağ sayfası. Denetleme **bağlı cihazları** hello sanal ağ geçidi için.

![Merhaba bağlı aygıt denetleyin](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

Hello ağ geçidi kaldırmadan önce ilk herhangi kaldırın **bağlantı** hello ağ geçidi nesneleri. 

### <a name="check-whether-an-application-gateway-is-running-in-hello-virtual-network"></a>Bir uygulama ağ geçidi hello sanal ağda çalışır durumda olup olmadığını denetleyin

Toohello Git **genel bakış** hello sanal ağ sayfası. Merhaba denetleyin **bağlı cihazları** hello uygulama ağ geçidi için.

![Merhaba bağlı aygıt denetleyin](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

Bir uygulama ağ geçidi ise hello sanal ağı silmeden önce onu kaldırmanız gerekir.

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-hello-virtual-network"></a>Azure Active Directory etki alanı hizmeti hello sanal ağda etkin olup olmadığını denetleyin

Merhaba Active Directory etki alanı hizmeti etkin ve bağlı toohello sanal ağ ise, bu sanal ağ silinemiyor. 

![Merhaba bağlı aygıt denetleyin](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

toodisable Merhaba hizmeti, şu adımları izleyin:

1. Toohello Git [Klasik Azure portalı](https://manage.windowsazure.com).
2. Merhaba sol bölmesinde seçin **Active Directory**.
3. Active Directory etki alanı hizmeti etkin olan hello Azure Active Directory (Azure AD) dizini seçin.
4. Select hello **yapılandırma** sekmesi.
5. Altında **etki alanı Hizmetleri**, hello değiştirme **bu dizin için etki alanı Hizmetleri'ni etkinleştirme** çok seçenek**Hayır**.  

### <a name="check-whether-hello-virtual-network-is-connected-tooother-resource"></a>Merhaba sanal ağ bağlantılı tooother kaynak olup olmadığını denetleyin

Bağlantı hattı bağlantıları, bağlantıları ve sanal ağ eşlemesi bulunabilir denetleyin. Bunlardan herhangi bir sanal ağ silme toofail neden olabilir. 

Merhaba önerilen silme sipariş şu şekildedir:

1. Ağ Geçidi bağlantıları
2. Ağ geçitleri
3. IP'leri
4. Sanal Ağ eşlemesi bulunabilir
5. Uygulama hizmeti ortamı (ana)

### <a name="check-whether-a-virtual-machine-is-still-running-in-hello-virtual-network"></a>Bir sanal makine hello sanal ağında hala çalışıp çalışmadığını denetleyin

Hiçbir sanal makine hello sanal ağda olduğundan emin olun.

### <a name="check-whether-hello-virtual-network-is-stuck-in-migration"></a>Merhaba sanal ağ içinde geçiş takıldı olup olmadığını denetleyin

Merhaba sanal ağ bir geçiş durumunda takılıyorsa silinemiyor. Komut tooabort hello geçiş aşağıdaki hello çalıştırın ve hello sanal ağ silin.

    Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort

## <a name="next-steps"></a>Sonraki adımlar

- [Azure Sanal Ağ](virtual-networks-overview.md)
- [Azure Sanal Ağ hakkında sık sorulan sorular (SSS)](virtual-networks-faq.md)