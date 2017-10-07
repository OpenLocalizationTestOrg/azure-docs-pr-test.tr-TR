---
title: "aaaEnabling son tooend Azure uygulama ağ geçidi SSL | Microsoft Docs"
description: "Bu sayfa SSL desteği hello uygulama ağ geçidi son tooend genel bir bakış sağlar."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 3976399b-25ad-45eb-8eb3-fdb736a598c5
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: amsriva
ms.openlocfilehash: c5cb398a1e7d9a08662a3120baad98edb5575917
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-end-tooend-ssl-with-application-gateway"></a>Son tooend SSL ile uygulama ağ geçidi'ne genel bakış

Hangi trafik genellikle akar toohello arka uç sunucularına şifrelenmemiş sonra uygulama ağ geçidi hello ağ geçidi, SSL sonlandırmanın destekler. Bu özellik web sunucuları toobe maliyetli şifreleme ve şifre çözme yükünü unburdened sağlar. Ancak bazı müşteriler için şifrelenmemiş iletişimi toohello arka uç sunucularına bir kabul edilebilir seçenek değil. Merhaba uygulaması yalnızca güvenli bir bağlantı kabul edebilir veya bu şifrelenmemiş iletişim uyumluluk gereksinimleri, toosecurity gereksinimleri olabilir. Bu tür uygulamalar için uygulama ağ geçidi son tooend SSL destekleyen şifreleme.

## <a name="overview"></a>Genel Bakış

Son tooend SSL verir toosecurely iletme hassas verileri toohello arka uç hala katman 7 Yük Dengeleme Özellikleri hello yararları hangi uygulama ağ geçidi yararlanarak sağlarken şifrelenmiş. Yönlendirme siteleri veya özelliği tooinject - iletilen - X göre için tanımlama bilgisi tabanlı oturum benzeşimi, URL tabanlı yönlendirme, destek bu özelliklerden bazıları şunlardır * üstbilgileri.

Son tooend SSL iletişimi modu ile yapılandırıldığında, uygulama ağ geçidi hello SSL oturumları hello ağ geçidinde sonlandırır ve kullanıcı trafiğinin şifresini çözer. Ardından yapılandırılmış hello kuralları tooselect bir uygun arka uç havuzu örnek tooroute trafiği için geçerlidir. Uygulama ağ geçidi, ardından yeni bir SSL bağlantısı toohello arka uç sunucu başlatır ve veri hello isteği toohello arka uç iletmeden önce hello arka uç sunucunun ortak anahtar sertifikası kullanılarak yeniden şifreler. SSL protokolünü ise BackendHTTPSetting tooHTTPS ayarlayarak etkin uç tooend tooa arka uç havuzu uygulanır. SSL etkin uç tooend ile Merhaba arka uç havuzundaki her arka uç sunucu sertifikası tooallow güvenli bir bağlantı ile yapılandırılması gerekir.

![Son tooend ssl senaryosu][1]

Bu örnekte, TLS1.2 kullanan isteklerinin son tooend SSL kullanarak yönlendirilmiş toobackend Pool1 sunucularıdır.

## <a name="end-tooend-ssl-and-whitelisting-of-certificates"></a>Tooend SSL ve uygulamaları güvenilir listeye almayı sertifikaların bitiş

Uygulama ağ geçidi, yalnızca kendi sertifika hello uygulama ağ geçidi ile Güvenilenler listesine sahip bilinen arka uç örnekleri ile iletişim kurar. tooenable uygulamaları güvenilir listeye almayı sertifikaların, arka uç sunucu sertifikaları toohello uygulama ağ geçidi (Merhaba kök sertifikanın değil) ortak anahtarı hello yüklemeniz gerekir. Yalnızca bağlantıları tooknown ve Güvenilenler listesine arka uçlarını sonra izin verilir. arka uçlarını kalan hello bir ağ geçidi hatayla sonuçlanır. Otomatik olarak imzalanan sertifikalar, yalnızca test amaçlarına yöneliktir ve üretim iş yükleri için önerilmez. Bu tür sertifikaların kullanılabilmesi için önce adımları önceki hello açıklandığı gibi hello uygulama ağ geçidi ile toobe Güvenilenler listesine vardır.

## <a name="next-steps"></a>Sonraki adımlar

Son tooend SSL hakkında daha fazla bilgi sonra çok gidin[uygulama ağ geçidi üzerinde son tooend SSL etkinleştirmek](application-gateway-end-to-end-ssl-powershell.md) kullanarak bir uygulama ağ geçidi toocreate tooend SSL bitmelidir.

<!--Image references-->

[1]: ./media/application-gateway-backend-ssl/scenario.png
