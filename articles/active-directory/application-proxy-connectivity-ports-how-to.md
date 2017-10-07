---
title: "bir uygulama proxy'si uygulama için gerekli aaaHow tooopen hello güvenlik duvarı bağlantı noktaları | Microsoft Docs"
description: "Hangi bağlantı noktalarının tooopen hello Azure AD uygulama proxy'si toowork için doğru öğrenin"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: cdc7badb7c15591689a3bfd6bb26da182b00fb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-hello-firewall-ports-required-for-an-application-proxy-application"></a>Nasıl tooopen hello uygulama proxy'si uygulama için gerekli güvenlik duvarı bağlantı noktaları

toosee hello gerekli bağlantı noktaları ve her bağlantı noktası hello işlevi tam bir listesi hello hello Önkoşullar bölümüne bakın [uygulama proxy'si belgelerine](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable). Uygulama proxy'si yalnızca giden bağlantı noktalarını kullandığını unutmayın.

Açma hello tarafından tüm gerekli hello bağlantı noktalarının açık yüklü olup olmadığını da denetleyebilirsiniz [Bağlayıcısı bağlantı noktaları Test aracı](https://aadap-portcheck.connectorporttest.msappproxy.net/) şirket içi ağınızdan. Daha fazla yeşil onay işaretleri büyük esneklik anlamına gelir. 

## <a name="app-proxy-regions"></a>Uygulama proxy'si bölgeleri

Bu bölgeler hangisinin bildiğiniz toolet toobe yeşil sizin için gereken şekilde üzerinde çalışıyoruz. Şimdilik, tüm olduklarından emin olun. Orta ABD Ayrıca hangi bölgeyi bağımsız olarak gereklidir.

doğru sonuçlar hello toomake emin hello aracı verir için emin olun:

-   Merhaba bağlayıcısını yüklediğiniz hello sunucudan Hello aracını kullanarak bir tarayıcı açın.

-   Bağlayıcı olan ayrıca tüm proxy'leri veya güvenlik duvarları geçerli tooyour toothis sayfa uygulanan emin olun. Internet Explorer'da bu yapılabilir çok giderek**ayarları**  - &gt; **Internet Seçenekleri**  - &gt; **bağlantıları**  - &gt; **Lan ayarları**. Bu sayfada hello alan "Kullan bir Proxy sunucu için bilgisayarınızı LAN" konusuna bakın. Bu kutuyu işaretleyin ve hello proxy adresi hello "Adres" alanına yerleştirin.

## <a name="next-steps"></a>Sonraki adımlar
[Azure AD uygulama proxy'si bağlayıcılar anlama](application-proxy-understand-connectors.md)
