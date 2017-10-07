---
title: "aaaVerify Azure Traffic Manager ayarları | Microsoft Docs"
description: "Bu makalede, trafik Yöneticisi ayarlarınızı doğrulamanıza yardımcı olur"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 2180b640-596e-4fb2-be59-23a38d606d12
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: c670be6cf55e140c7ab63d5d526de08e14774d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="verify-traffic-manager-settings"></a>Trafik Yöneticisi ayarlarını doğrulayın

tootest trafik Yöneticisi ayarlarınızı içinden çalıştırabilirsiniz testlerinizi çeşitli konumlarda birden çok istemci toohave gerekir. Ardından, bir kerede aşağı Traffic Manager profilinize hello uç noktaları getirin.

* Hızlı bir şekilde (örneğin, 30 saniye) değişiklikleri yaymak şekilde hello DNS TTL değeri düşük ayarlayın.
* Hello Azure bulut hizmetlerine ve hello profilinde test ettiğiniz Web sitelerine IP adreslerini bilirsiniz.
* Bir DNS adı tooan IP adresi çözmek ve bu adresi görüntülemek olanak sağlayan araçları kullanın.

Merhaba DNS adlarını hello uç noktaları profilinizde tooIP adresleri çözümleyecek toosee denetleniyor. Merhaba adları hello trafik yönlendirme yöntemini hello trafik Yöneticisi profili tanımlanan ile tutarlı şekilde çözümlenmelidir. Merhaba araçları gibi kullanabilirsiniz **nslookup** veya **derinliklerine** tooresolve DNS adları.

Merhaba aşağıdaki örneklerde, Traffic Manager profilinizin test yardımcı olur.

### <a name="check-traffic-manager-profile-using-nslookup-and-ipconfig-in-windows"></a>Trafik Yöneticisi profili nslookup ve ipconfig Windows'da kullanma denetleyin

1. Bir komut veya Windows PowerShell komut istemini yönetici olarak açın.
2. Tür `ipconfig /flushdns` tooflush hello DNS çözümleyicisi önbelleği.
3. `nslookup <your Traffic Manager domain name>` yazın. Örneğin, denetimleri hello hello önek etki alanı adıyla komutu aşağıdaki hello *myapp.contoso*

        nslookup myapp.contoso.trafficmanager.net

    Tipik bir sonuç bilgisinden hello gösterir:

    + Merhaba DNS adı ve IP adresi hello DNS sunucusu olma tooresolve Bu trafik yöneticisi etki alanı adı erişilir.
    + Merhaba trafik yöneticisi etki alanı adı "nslookup sonra" Merhaba komut satırında yazılan ve başlangıç IP adresi toowhich hello trafik yöneticisi etki alanı giderir. Merhaba önemli bir toocheck Hello ikinci IP adresi değil. Merhaba bulut Hizmetleri veya hello trafik Yöneticisi profili test ettiğiniz Web sitelerinde biri için bir genel sanal IP (VIP) adresi eşleşmelidir.

## <a name="how-tootest-hello-failover-traffic-routing-method"></a>Nasıl tootest hello yük devretme trafik yönlendirme yöntemi

1. Yukarı tüm uç noktaları bırakın.
2. Tek bir istemci kullanarak, DNS çözümlemesi nslookup veya benzer bir yardımcı programını kullanarak, şirketinizin etki alanı adı isteyin.
3. IP adresi hello birincil uç noktayla eşleşen bu hello çözülmüş emin olun.
4. Kapalı olduğu, uygulama Merhaba trafik Yöneticisi düşündüğü böylece dosya izleme hello kaldırın veya birincil uç noktanızı getirin.
5. Merhaba DNS için-yaşam süresi (TTL) hello trafik Yöneticisi profilinin artı iki dakika bekleyin. Örneğin, DNS TTL 300 saniye (5 dakika) ise, yedi dakika beklemeniz gerekir.
6. Nslookup kullanarak DNS istemci önbelleği ve istek DNS çözümlemenizin temizlenir. Windows hello ipconfig/flushdns komutuyla, DNS önbelleğini boşaltabilirsiniz.
7. IP adresi, ikincil uç noktayla eşleşen bu hello çözülmüş emin olun.
8. Her uç noktası sırayla getiren hello işlemi yineleyin. Bu hello DNS hello IP adresi hello sonraki uç noktasının hello listesinde döndürür doğrulayın. Tüm uç noktaları kapalı olduğunda, başlangıç IP adresi hello birincil uç noktasının yeniden edinmelidir.

## <a name="how-tootest-hello-weighted-traffic-routing-method"></a>Trafik yönlendirme yöntemini nasıl tootest hello ağırlıklı

1. Yukarı tüm uç noktaları bırakın.
2. Tek bir istemci kullanarak, DNS çözümlemesi nslookup veya benzer bir yardımcı programını kullanarak, şirketinizin etki alanı adı isteyin.
3. IP adresi noktalarınızı biriyle eşleşen bu hello çözülmüş emin olun.
4. DNS istemci önbelleğini temizlemek ve her uç noktası için 2 ve 3. adımları yineleyin. Her uç noktalarınızı için döndürülen farklı IP adreslerini görmeniz gerekir.

## <a name="how-tootest-hello-performance-traffic-routing-method"></a>Nasıl tootest hello performans trafik yönlendirme yöntemi

tooeffectively test performans trafik yönlendirme yöntemini, hello world farklı bölümlerinde bulunan istemciler olması gerekir. İstemcileri hizmetlerinizi kullanılan tootest olabilir farklı Azure bölgelerinde oluşturabilirsiniz. Genel bir ağ varsa, uzaktan oturum açma tooclients Merhaba Dünya diğer bölümlerinde ve buradan testleri çalıştırın.

Alternatif olarak, ücretsiz web tabanlı DNS araması ve vardır kullanılabilir hizmetler derinliklerine. Bunlardan bazıları özelliği toocheck DNS ad çözümlemesi Merhaba Dünya çeşitli konumlardan hello verin araçları. Örnekler "DNS aramalarında" araması yapın. Gomez veya açılış konuşması gibi üçüncü taraf hizmetleri profillerinizi trafiği beklendiği gibi dağıtıyorsanız kullanılan tooconfirm olabilir.

## <a name="next-steps"></a>Sonraki adımlar

* [Traffic Manager trafik yönlendirme yöntemleri hakkında](traffic-manager-routing-methods.md)
* [Traffic Manager için performans konuları](traffic-manager-performance-considerations.md)
* [Düzeyi düşürülmüş Traffic Manager durumu için sorun giderme](traffic-manager-troubleshooting-degraded.md)
