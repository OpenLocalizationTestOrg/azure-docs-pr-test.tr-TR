---
title: "aaaWhat Azure geçiş ve neden genel bakış kullanın | Microsoft Docs"
description: "Azure Geçiş’e Genel Bakış"
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1e3e971d-2a24-4f96-a88a-ce3ea2b1a1cd
ms.service: service-bus-relay
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: 4cfd77048210a435c446b908b7896737cad0edbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-relay"></a>Azure Geçiş nedir?

Hello Azure hizmeti, toosecurely etkinleştirerek uygulamaları kurumsal bir ağ toohello genel bulut içinde bir güvenlik duvarı bağlantı tooopen zorunda kalmadan hizmetlere kullanıma sunmak veya müdahale gerektiren karma kolaylaştıran geçiş tooa değiştirir Kurumsal ağ altyapısına. Geçiş, birçok çeşitli aktarım protokolünü ve web hizmeti standartlarını destekler.

Merhaba geçiş hizmeti, geleneksel tek yönlü, istek/yanıt ve eşler arası trafik destekler. Ayrıca artırılmış uçtan uca verimliliğe için internet kapsamında tooenable yayımlama abone ol senaryolarına ve çift yönlü yuva iletişimi olay dağıtımını destekler. 

Geçişli hello veri aktarımı düzeninde bir şirket içi hizmet toohello geçiş Hizmeti giden bir bağlantı noktası üzerinden bağlanır ve tooa belirli randevu adresine bağlanan iletişim için çift yönlü yuva oluşturur. Merhaba istemci trafiğini toohello geçiş hizmeti hello randevu adresini hedef göndererek hello şirket içi hizmetiyle sonra iletişim kurabilir. Merhaba geçiş hizmeti sonra "veri toohello şirket içi hizmeti çift yönlü yuva ayrılmış tooeach istemci üzerinden geçirir". Merhaba istemci doğrudan bağlantı toohello şirket içi hizmet gerekmez, nerede bulunduğunu hello ve hello şirket içi hizmet gelen bağlantı noktalarının gerek yoktur gerekli tooknow değil hello Güvenlik Duvarı'nda Aç.

Geçiş tarafından sağlanan hello anahtar özelliği öğeleri TCP benzeri azaltma, uç nokta bulma, bağlantı durumunun ağ sınırları boyunca çift yönlü, arabellekten çıkarılan iletişimi olan ve uç nokta güvenliğinin yayılan. Merhaba geçiş yetenekleri VPN gibi ağ düzeyinde tümleştirme teknolojileri farklılık, VPN teknolojisi hello ağ ortamı değiştirilmesine alacağından daha kullanışsız olsa da bu geçiş kapsamlı tooa tek bir uygulama uç noktası tek bir makinede olabilir .

Azure Geçiş iki özelliğe sahiptir:

1. [Karma bağlantılar](#hybrid-connections) - kullanır hello açık standart web yuvalarını birden çok platform senaryoları etkinleştirme.
2. [WCF geçişler](#wcf-relays) -kullanan Windows Communication Foundation (WCF) tooenable uzaktan yordam çağrısı. WCF geçiş hello eski geçiş birçok müşteri modellerini programlama kendi WCF ile kullandığınız sunumu ' dir.

Karma bağlantılar ve WCF geçişler bir kurumsal ağ içindeki mevcut güvenli bağlantı tooassets etkinleştirin. Aşağıdaki tablonun hello açıklandığı gibi hello diğer üzerinde kullanımını belirli gereksinimlerinize bağlı olarak bağlıdır:

|  | WCF Geçişi | Karma Bağlantılar |
| --- |:---:|:---:|
| **WCF** |x | |
| **.NET Core** | |x |
| **.NET Framework** |x |x |
| **JavaScript/NodeJS** | |x |
| **Standart Tabanlı Açık Protokol** | |x |
| **Birden Çok RPC Programlama Modeli** | |x |

## <a name="hybrid-connections"></a>Karma Bağlantılar

Merhaba [Azure geçişi karma bağlantılar](relay-hybrid-connections-protocol.md) yetenektir herhangi bir platformda ve temel WebSocket özelliğine sahip herhangi bir dil uygulanabilir geçiş özellikleri varolan hello güvenli, açık protokolü bir evrimi hangi açıkça hello WebSocket API ortak web tarayıcısında içerir. Karma Bağlantılar HTTP ve WebSocket’ları temel alır.

### <a name="service-history"></a>Hizmet geçmişi

Karma bağlantılar benzer şekilde, Azure hizmet veri yolu WCF geçiş hello üzerinde oluşturulmuş "BizTalk Services" özelliği adlı hello eski yerini alır. Merhaba yeni karma bağlantılar özelliği hello var olan WCF geçiş özelliğini tamamlar ve bu iki hizmet özellikleri yana birimi hello Azure geçiş Hizmeti'nde mevcut. Ortak bir ağ geçidine sahip bu iki özellik, diğer açılardan farklı olan uygulamalardır.

## <a name="wcf-relays"></a>WCF Geçişleri

Merhaba WCF geçiş works hello tam .NET Framework (NETFX) ve WCF için. Şirket içi hizmet WCF "geçiş" bağlamalarının bir paketini kullanarak geçiş hizmeti hello arasında hello bağlantı başlatır. Merhaba arka planda hello geçiş bağlamaları hello bulutta Service Bus ile tümleşen toonew aktarım bağlama öğeleri tasarlanmış toocreate WCF kanalı bileşenlerini eşleşir.

## <a name="architecture-processing-of-incoming-relay-requests"></a>Mimari: Gelen geçiş isteklerinin işlenmesi
Bir istemci isteği toohello gönderdiğinde [Azure geçiş](/azure/service-bus-relay/) hizmeti, hello Azure yük dengeleyici, hello ağ geçidi düğümleri tooany yönlendirir. Merhaba istek dinleme isteğiyse hello ağ geçidi düğümü yeni bir geçiş oluşturur. Merhaba istek bağlantı isteği tooa belirli bir geçiş ise hello ağ geçidi düğümü hello geçişe sahip hello bağlantı isteği toohello ağ geçidi düğümüne iletir. Merhaba geçişe sahip hello ağ geçidi düğümü hello bağlantı isteğini alan bir geçici kanal toohello ağ geçidi düğümü hello dinleyici toocreate soran bir randevu isteği toohello dinleyen istemciye gönderir.

Merhaba geçiş bağlantısı kurulduğunda hello istemcileri hello randevu için kullanılan hello ağ geçidi düğümü aracılığıyla iletileri değiştirebilir.

![Gelen WCF Geçiş İsteklerinin işlenmesi](./media/relay-what-is-it/ic690645.png)

## <a name="next-steps"></a>Sonraki adımlar

* [Geçiş hakkında SSS](relay-faq.md)
* [Ad alanı oluşturma](relay-create-namespace-portal.md)
* [.NET kullanmaya başlama](relay-hybrid-connections-dotnet-get-started.md)
* [Node kullanmaya başlama](relay-hybrid-connections-node-get-started.md)

