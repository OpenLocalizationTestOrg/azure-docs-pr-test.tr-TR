---
title: "Azure uygulama ağ geçidi için genel bakış izleme aaaHealth | Microsoft Docs"
description: "Azure uygulama ağ geçidi özelliklerinde izleme hello hakkında bilgi edinin"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7eeba328-bb2d-4d3e-bdac-7552e7900b7f
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: gwallace
ms.openlocfilehash: 5091d80394a354ff849ce7ccee8cc9d2fd0456db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-health-monitoring-overview"></a>Uygulama ağ geçidi sistem durumu izlemeye genel bakış

Varsayılan olarak Azure uygulama ağ geçidi arka uç havuzundaki tüm kaynakları hello durumunu izler ve hello havuzundan sağlıksız kabul herhangi bir kaynağa otomatik olarak kaldırır. Uygulama ağ geçidi toomonitor hello sağlıksız örnekleri devam eder ve bunları ekler kullanılabilir durumda olduklarında ve yanıt toohealth yoklamaları sonra toohello sağlıklı arka uç havuzu yedekleyin. Uygulama ağ geçidi hello sistem durumu araştırmalarının hello ile Merhaba arka uç HTTP Ayarları'nda tanımlanan aynı bağlantı noktasını gönderir. Bu yapılandırma bu hello araştırma müşteriler tooconnect toohello arka uç kullanarak, aynı bağlantı noktası hello sınama sağlar.

![Uygulama ağ geçidi araştırma örneği][1]

Toplama toousing varsayılan durumu araştırma izleme, uygulamanızın gereksinimleri hello sistem durumu araştırma toosuit de özelleştirebilirsiniz. Bu makalede, hem varsayılan hem de özel sistem durumu araştırmalarının ele alınmıştır.

> [!NOTE]
> Uygulama ağ geçidi alt ağı üzerinde bir NSG varsa, bağlantı noktası aralıkları 65503 65534 hello uygulama ağ geçidi alt gelen trafik için açılmalıdır. Bu bağlantı noktaları hello arka uç sistem durumu API toowork için gereklidir.

## <a name="default-health-probe"></a>Varsayılan durumu araştırması

Herhangi bir özel araştırma yapılandırma ayarladığınızda olmayan bir uygulama ağ geçidi varsayılan durumu araştırması otomatik olarak yapılandırır. davranış izlemeyi hello hello arka uç havuzu için yapılandırılmış bir HTTP isteği toohello IP adresleri yapma çalışır. Merhaba arka uç http ayarları HTTPS için yapılandırılmış olması halinde için varsayılan araştırmalar hello araştırma hello arka uçlarını iyi tootest sistem durumu HTTPS kullanır.

Örneğin: bağlantı noktası 80 üzerinde uygulama ağ geçidi toouse arka uç sunucuları A, B ve C tooreceive HTTP ağ trafiğinizi yapılandırın. Merhaba varsayılan sistem durumu izleme hello üç sunucu her 30 saniyede sağlıklı bir HTTP yanıtı için sınar. Sağlıklı bir HTTP yanıtı sahip bir [durum kodu](https://msdn.microsoft.com/library/aa287675.aspx) 200 399 arasındaki.

Sunucu A Hello varsayılan araştırma denetimi başarısız olursa, isteğe bağlı olarak hello uygulama ağ geçidi, arka uç havuzundan kaldırır ve ağ trafiğini toothis sunucu akışı durur. Merhaba varsayılan araştırma, her 30 saniyede bir toocheck sunucusu için hala devam eder. Sunucu A varsayılan durumu araştırması başarıyla tooone isteğini yanıtladığında, sağlıklı toohello arka uç havuzu ve toohello sunucu yeniden akan trafik başlatır geri eklenir.

### <a name="default-health-probe-settings"></a>Varsayılan durumu araştırma ayarları

| Araştırma özelliği | Değer | Açıklama |
| --- | --- | --- |
| Araştırma URL'si |http://127.0.0.1:\<bağlantı noktası\>/ |URL yolu |
| aralığı |30 |Saniye cinsinden yoklama aralığı |
| Zaman aşımı |30 |Zaman aşımı saniye cinsinden araştırma |
| Sağlıksız durum eşiği. |3 |Yeniden deneme sayısı araştırma. Merhaba arka arkaya araştırma hatası sayısı hello sağlıksız durum eşiği ulaştıktan sonra hello arka uç sunucu işaretlenmiş. |

> [!NOTE]
> Merhaba bağlantı noktası olan hello aynı hello arka uç HTTP ayarları olarak bağlantı noktası.

Merhaba varsayılan araştırma yalnızca http://127.0.0.1 arar:\<bağlantı noktası\> toodetermine sistem durumu. Tooconfigure hello sistem durumu araştırma toogo tooa özel URL gerekir veya diğer herhangi bir ayarı değiştirmek, aşağıdaki adımları hello açıklandığı gibi özel araştırmalara kullanmanız gerekir:

## <a name="custom-health-probe"></a>Özel durum araştırması

Özel araştırmalara toohave hello sistem durumu izleme üzerinde daha ayrıntılı bir denetim sağlar. Özel araştırmalara kullanırken hello arka uç havuzu örneği sağlıksız olarak işaretleme önce hello yoklama aralığı, hello URL ve yol tootest ve kaç tane başarısız yanıtları tooaccept yapılandırabilirsiniz.

### <a name="custom-health-probe-settings"></a>Özel durum yoklama ayarları

Merhaba aşağıdaki tabloda bir özel durum araştırması hello özelliklerini için tanımları sağlar.

| Araştırma özelliği | Açıklama |
| --- | --- |
| Ad |Merhaba araştırma adı. Arka uç HTTP Ayarları'nda kullanılan toorefer toohello araştırma adıdır. |
| Protokol |Toosend hello araştırma kullanılan protokol. Merhaba araştırma hello arka uç HTTP Ayarları'nda tanımlanan hello protokolünü kullanır |
| Host |Ana bilgisayar adı toosend hello araştırma. Geçerli yalnızca çok siteli uygulama ağ geçidi üzerinde yapılandırılmış, aksi takdirde '127.0.0.1' kullanın. Bu değer, VM ana bilgisayar adından farklıdır. |
| Yol |Merhaba araştırma göreli yolu. Merhaba geçerli bir yol başlatır '/'. |
| aralığı |Aralığı saniye cinsinden araştırma. İki ardışık araştırmalar arasındaki hello zaman aralığını değerdir. |
| Zaman aşımı |Zaman aşımı saniye cinsinden araştırma. Bu zaman aşımı süresi içinde geçerli bir yanıt alınmazsa, hello araştırma başarısız olarak işaretlenir.  |
| Sağlıksız durum eşiği. |Yeniden deneme sayısı araştırma. Merhaba arka arkaya araştırma hatası sayısı hello sağlıksız durum eşiği ulaştıktan sonra hello arka uç sunucu işaretlenmiş. |

> [!IMPORTANT]
> Uygulama ağ geçidi tek bir site için yapılandırılmışsa, varsayılan hello ana bilgisayar tarafından adı '127.0.0.1', içinde özel araştırma aksi belirtilmedikçe belirtilmesi gerekir.
> Başvuru için özel bir araştırma çok gönderilir\<Protokolü\>://\<konak\>:\<bağlantı noktası\>\<yolu\>. Merhaba kullanılan bağlantı noktası olacaktır hello arka uç HTTP Ayarları'nda tanımlanan gibi hello aynı bağlantı noktası.

## <a name="next-steps"></a>Sonraki adımlar
Uygulama ağ geçidi durumunu izleme hakkında daha fazla öğrenme sonra yapılandırdığınız bir [özel durumu araştırması](application-gateway-create-probe-portal.md) hello Azure portal'ın veya [özel durumu araştırması](application-gateway-create-probe-ps.md) PowerShell ve hello Azure Resource Manager kullanarak dağıtım modeli.

[1]: ./media/application-gateway-probe-overview/appgatewayprobe.png
