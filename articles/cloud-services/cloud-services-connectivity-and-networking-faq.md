---
title: "aaaConnectivity ve ağ iletişimi sorunları için Microsoft Azure bulut Hizmetleri ile ilgili SSS | Microsoft Docs"
description: "Bu makalede bağlantısı ve Microsoft Azure bulut Hizmetleri için ağ hakkında sık sorulan sorular hello listelenmektedir."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: e725dbbf585a76807362c59299d0a31f511afd3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connectivity-and-networking-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Azure bulut Hizmetleri için bağlantı ve ağ sorunları: sık sorulan sorular (SSS)

Bu makale için bağlantı ve ağ sorunları hakkında sık sorulan sorular içerir [Microsoft Azure bulut Hizmetleri](https://azure.microsoft.com/services/cloud-services). Merhaba de başvurabilirsiniz [bulut Hizmetleri VM boyutu sayfa](cloud-services-sizes-specs.md) boyutu bilgi.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a>Bir çoklu VIP bulut hizmetindeki bir IP rezerve edilemez
Öncelikle, tooreserve hello IP için çalıştığınız bu hello sanal makine örneğini açık olduğundan emin olun. İkinci olarak, her ikisi de hazırlama ve üretim dağıtımları hello için ayrılmış IP kullandığınızdan emin olun. **Sağlamadığı** hello dağıtım yükseltme sırasında hello ayarlarını değiştirin.

## <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a>Nasıl yedeklerim Uzak Masaüstü bir NSG olduğunda?
Kuralları toohello noktalarında trafiğine izin veren NSG ekleme **3389** ve **20000**.  Uzak Masaüstü bağlantı noktasını kullanır **3389**.  Bulut hizmeti örnekleri yükü dengelenmiş, olduğundan, hangi örneğinin tooconnect doğrudan denetleyemezsiniz.  Merhaba *RemoteForwarder* ve *RemoteAccess* aracıları RDP trafiği yönetmek ve hello istemci toosend bir RDP izin ver ve bir tek tek örnek tooconnect belirtin.  Merhaba *RemoteForwarder* ve *RemoteAccess* aracıları gerektiren bu bağlantı noktasını **20000** açılıp, hangi engellenmiş olabilir bir NSG varsa.

## <a name="can-i-ping-a-cloud-service"></a>Bir bulut hizmeti ping işlemi yapabilirsiniz?

Merhaba normal "ping" kullanarak değil Hayır'ı / ICMP protokolü. Merhaba ICMP Protokolü hello Azure yük dengeleyici izin verilmez.

tootest bağlantısı, bir bağlantı noktası ping yapmanızı öneririz. ICMP ping.exe kullanıyor, ancak PSPing, Nmap ve telnet gibi diğer araçları tootest bağlantı tooa belirli TCP bağlantı noktası izin verin.

Daha fazla bilgi için bkz: [ICMP tootest Azure VM bağlantısı yerine bağlantı noktasına ping kullanmak](https://blogs.msdn.microsoft.com/mast/2014/06/22/use-port-pings-instead-of-icmp-to-test-azure-vm-connectivity/).

## <a name="how-do-i-prevent-receiving-thousands-of-hits-from-unknown-ip-addresses-that-indicate-some-sort-of-malicious-attack-toohello-cloud-service"></a>Ne ı önlemek alma binlerce isabet kötü amaçlı saldırı toohello çeşit belirtmek bilinmeyen IP adreslerinden bulut hizmeti?
Azure platform hizmetlerini dağıtılmış hizmet engelleme (DDoS) saldırıları karşı çok katmanlı ağ güvenlik tooprotect uygular. Hello Azure DDoS savunma sistemi sürekli sızma testi aracılığıyla geliştirilmiş Azure'un sürekli izleme işleminin bir parçasıdır. Bu DDoS savunma sistemi tasarlanmış toowithstand yalnızca saldırıları hello dışında ancak aynı zamanda diğer Azure kiracılar. Daha fazla ayrıntı için [Microsoft Azure ağ güvenliği](http://download.microsoft.com/download/C/A/3/CA3FC5C0-ECE0-4F87-BF4B-D74064A00846/AzureNetworkSecurity_v3_Feb2015.pdf).

Bir başlangıç görevi tooselectively bloğu bazı belirli IP adreslerini de oluşturabilirsiniz. Daha fazla bilgi için bkz: [belirli bir IP adres bloğu](cloud-services-startup-tasks-common.md#block-a-specific-ip-address).

## <a name="when-i-try-toordp-toomy-cloud-service-instance-i-get-hello-message-hello-user-account-has-expired"></a>TooRDP toomy bulut hizmeti örneği çalıştığınızda, selamlama iletisine almak için "Merhaba kullanıcı hesabının süresi doldu."
RDP ayarlarında hello sona erme tarihi atlama, "Bu kullanıcı hesabının süresi doldu" Merhaba hata iletisini alabilirsiniz. Aşağıdaki adımları izleyerek hello portalından hello sona erme tarihi değiştirebilirsiniz:
1. Toohello Azure Yönetim Konsolu (https://manage.windowsazure.com) oturum açın, tooyour bulut hizmetine gidin ve seçin hello **yapılandırma** sekmesi.
2. Seçin **uzak**.
3. "Expires On" Merhaba tarih değiştirin ve hello yapılandırmayı kaydedin.

Artık mümkün tooRDP tooyour makine olması gerekir.

## <a name="why-is-loadbalancer-not-balancing-traffic-equally"></a>Neden LoadBalancer eşit Dengeleme trafiğini olduğu değil mi?
Nasıl iç yük dengeleyici çalıştığı hakkında daha fazla bilgi için bkz: [Azure yük dengeleyici yeni dağıtım modu](https://azure.microsoft.com/blog/azure-load-balancer-new-distribution-mode/).

kullanılan hello dağıtım algoritmasıdır 5-tanımlama grubu (kaynak IP, kaynak bağlantı noktası, hedef IP, hedef bağlantı noktası, protokol türü) toomap trafiği tooavailable sunucuları karma. Bu, yalnızca bir aktarım oturumu içinde sürekliliği sağlar. Aynı TCP veya UDP oturum olacak hello paketlerinde aynı veri merkezi IP (DIP) örneği hello yük dengeli uç nokta toohello yönlendirilmiş. Merhaba istemci kapatır ve hello bağlantı yeniden açar veya hello yeni bir oturum başlatıldığında, aynı kaynak IP, hello kaynak bağlantı noktası değiştirir ve hello trafiği toogo tooa farklı DIP endpoint neden olur.
