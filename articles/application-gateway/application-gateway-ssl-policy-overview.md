---
title: "Azure uygulama ağ geçidi için aaaSSL ilkesine genel bakış | Microsoft Docs"
description: "Hakkında bilgi edinin Azure uygulama ağ geçidi tooconfigure SSL İlkesi sağlar"
services: application gateway
documentationcenter: na
author: amsriva
manager: 
editor: 
tags: azure resource manager
ms.service: application gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure services
ms.date: 08/03/2017
ms.author: amsriva
ms.openlocfilehash: 80dbc437da3dba8a558c518ecdbb5927a11a2ed9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-ssl-policy-overview"></a>Uygulama ağ geçidi SSL ilkesine genel bakış

Uygulama ağ geçidi toocentralize SSL sertifika yönetimi sağlar ve arka uç sunucu grubundan şifreleme ve şifre çözme yükünü azaltır. Ayrıca işleme bu merkezi SSL toospecify merkezi SSL verir İlkesi uygun tooyour kuruluş güvenlik gereksinimleri. Bu, hem uyumluluk gereksinimleri, hem de güvenlik yönergeleri karşılamanıza yardımcı olur ve önerilen uygulamalar.

SSL ilke SSL Protokolü sürüm hem de şifre paketleri ve şifre bir SSL el sıkışması sırasında kullanılan hello sipariş denetim içerir. Bu uygulama ağ geçidi, iki mekanizma tooallow müşteriler toocontrol SSL İlkesi, önceden tanımlanmış veya özel bir ilke sunar.

## <a name="predefined-ssl-policy"></a>Önceden tanımlanmış SSL İlkesi

Uygulama ağ geçidi üç önceden tanımlanmış güvenlik ilkeleri vardır. Ağ geçidiniz herhangi bu ilkeleri tooget hello uygun güvenlik düzeyini yapılandırabilirsiniz. Merhaba yıl ve ay yapılandırılmış olan tarafından Hello ilke adları açıklama eklendi. Her ilke teklifleri farklı SSL protokol sürümleri ve şifre paketleri. Toouse hello yeni SSL ilkeler tooensure hello en iyi SSL güvenlik önerilir. Uygulama ağ geçidi bugün kullanıcılar toochoose birinden hello aşağıdaki önceden tanımlanmış sağlar.

### <a name="appgwsslpolicy20150501"></a>AppGwSslPolicy20150501

|Özellik  |Değer  |
|---|---|
|Ad     | AppGwSslPolicy20150501        |
|MinProtocolVersion     | TLSv1_0        |
|Varsayılan| TRUE (önceden tanımlanmış hiçbir ilke belirtilen) |
|Şifreleme paketleri     |TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384<br>TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256<br>TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA<br>TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA<br>TLS_DHE_RSA_WITH_AES_256_GCM_SHA384<br>TLS_DHE_RSA_WITH_AES_128_GCM_SHA256<br>TLS_DHE_RSA_WITH_AES_256_CBC_SHA<br>TLS_DHE_RSA_WITH_AES_128_CBC_SHA<br>TLS_RSA_WITH_AES_256_GCM_SHA384<br>TLS_RSA_WITH_AES_128_GCM_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA256<br>TLS_RSA_WITH_AES_128_CBC_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_128_CBC_SHA<br>TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384<br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA<br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA<br>TLS_DHE_DSS_WITH_AES_256_CBC_SHA256<br>TLS_DHE_DSS_WITH_AES_128_CBC_SHA256<br>TLS_DHE_DSS_WITH_AES_256_CBC_SHA<br>TLS_DHE_DSS_WITH_AES_128_CBC_SHA<br>TLS_RSA_WITH_3DES_EDE_CBC_SHA<br>TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA |
  
  ### <a name="appgwsslpolicy20170401"></a>AppGwSslPolicy20170401
  
|Özellik  |Değer  |
|   ---      |  ---       |
|Ad     | AppGwSslPolicy20170401        |
|MinProtocolVersion     | TLSv1_0        |
|Varsayılan| False |
|Şifreleme paketleri     |TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA<br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384<br>TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA<br>TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_256_GCM_SHA384<br>TLS_RSA_WITH_AES_128_GCM_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA256<br>TLS_RSA_WITH_AES_128_CBC_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_128_CBC_SHA |
  
### <a name="appgwsslpolicy20170401s"></a>AppGwSslPolicy20170401S

|Özellik  |Değer  |
|---|---|
|Ad     | AppGwSslPolicy20170401        |
|MinProtocolVersion     | TLSv1_2        |
|Varsayılan| False |
|Şifreleme paketleri     |TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256 <br>    TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384 <br>    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA <br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA <br>TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256<br>TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384<br>TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384<br>TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256<br>TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA<br>TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_256_GCM_SHA384<br>TLS_RSA_WITH_AES_128_GCM_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA256<br>TLS_RSA_WITH_AES_128_CBC_SHA256<br>TLS_RSA_WITH_AES_256_CBC_SHA<br>TLS_RSA_WITH_AES_128_CBC_SHA<br> |

## <a name="custom-ssl-policy"></a>Özel SSL İlkesi

Önceden tanımlanmış bir SSL İlkesi gereksinimleriniz için yapılandırılmış toobe gerekiyorsa, kendi özel SSL ilkenizi tanımlayın gereken sahip. Bu durumda, hello minimum SSL Protokolü sürüm toosupport üzerinde tam denetime sahip yanı sıra desteklenen şifre paketleri ve bunların öncelik sırası.
 
SSL protokol sürümleri:

* SSL 2.0 ve 3.0, tüm Application Gateway'ler için varsayılan olarak devre dışı bırakılır. Bu protokol sürümleri yapılandırılabilir değildir.
* Tooselect herhangi bir hello minimum SSL Protokolü sürüm ağ geçidiniz için TLSv1_0, TLSv1_1, TLSv1_2 olarak üç protokolden aşağıdaki Merhaba, seçeneği özel SSL ilke tanımı sağlar.
* Hiçbir SSL ilkesi tanımlanmışsa, tüm üç (TLSv1_0, TLSv1_1, TLSv1_2) etkinleştirilir.

Şifre paketi:

Uygulama ağ geçidi, özel ilkeniz seçilebilir şifre paketleri aşağıdaki hello destekler. Merhaba hello şifre paketlerinin sıralama SSL anlaşması sırasında hello öncelik sırasını belirler.

Kullanılabilir şifre paketleri:

- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
- TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_DHE_RSA_WITH_AES_256_CBC_SHA
- TLS_DHE_RSA_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_AES_256_GCM_SHA384
- TLS_RSA_WITH_AES_128_GCM_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA256
- TLS_RSA_WITH_AES_128_CBC_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA
- TLS_RSA_WITH_AES_128_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_3DES_EDE_CBC_SHA
- TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA

## <a name="next-steps"></a>Sonraki adımlar

[Bir uygulama ağ geçidi üzerinde SSL ilkesini yapılandırma](application-gateway-configure-ssl-policy-powershell.md)
