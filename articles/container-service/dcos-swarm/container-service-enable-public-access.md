---
title: "aaaEnable erişim tooAzure DC/OS kapsayıcı uygulama | Microsoft Docs"
description: "Nasıl tooenable genel, Azure kapsayıcı hizmeti tooDC/OS kapsayıcılarında erişin."
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Docker, Kapsayıcılar, Mikro hizmetler, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 1ba251ba5a176a6a5e1c7831655164e380a62b27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-public-access-tooan-azure-container-service-application"></a>Genel erişim tooan Azure kapsayıcı hizmeti uygulamayı etkinleştir
Merhaba ACS herhangi bir DC/OS kapsayıcısına [ortak aracı havuzu](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) otomatik olarak sunulan toohello olan Internet. Varsayılan olarak, bağlantı noktaları **80**, **443**, **8080** açık olan ve bu bağlantı noktalarını dinler tüm (Genel) kapsayıcı erişilebilir. Bu makale size nasıl tooopen daha uygulamalarınızı Azure kapsayıcı hizmeti için bağlantı noktalarını gösterir.

## <a name="open-a-port-portal"></a>Bağlantı noktası (portal) açın
İlk olarak, istiyoruz tooopen hello bağlantı noktası gerekir.

1. Toohello Portalı'nda oturum açın.
2. Dağıttığınız Bul hello kaynak grubu hello Azure kapsayıcı hizmeti.
3. Merhaba aracı yük dengeleyicinin seçin (adlandırılmış benzer çok**XXXX-aracı-lb-XXXX**).
   
    ![Azure kapsayıcı hizmeti yük dengeleyici](./media/container-service-enable-public-access/agent-load-balancer.png)
4. Tıklatın **yoklamaları** ve ardından **eklemek**.
   
    ![Azure kapsayıcı hizmeti yük dengeleyici yoklamaları](./media/container-service-enable-public-access/add-probe.png)
5. Merhaba araştırma formu doldurun ve **Tamam**.
   
   | Alan | Açıklama |
   | --- | --- |
   | Ad |Merhaba araştırma, açıklayıcı bir ad. |
   | Bağlantı noktası |Merhaba kapsayıcı tootest Hello bağlantı noktası. |
   | Yol |(HTTP modunda olduğunda) göreli Web sitesi yolu tooprobe hello. HTTPS desteklenmiyor. |
   | aralığı |saniye cinsinden araştırma arasındaki süre miktarı Hello çalışır. |
   | Sağlıksız durum eşiği. |Arka arkaya araştırma sayısı hello kapsayıcı sağlıksız olduğunu düşünmeden önce çalışır. |
6. Geri hello hello aracı yük dengeleyicinin, Özellikler **Yük Dengeleme kuralları** ve ardından **Ekle**.
   
    ![Azure kapsayıcı hizmeti yük dengeleyici kuralları](./media/container-service-enable-public-access/add-balancer-rule.png)
7. Merhaba yük dengeleyici formu doldurun ve **Tamam**.
   
   | Alan | Açıklama |
   | --- | --- |
   | Ad |Merhaba yük dengeleyicinin açıklayıcı bir ad. |
   | Bağlantı noktası |Merhaba genel gelen bağlantı noktası. |
   | Arka uç bağlantı noktası |Merhaba ortak iç hello kapsayıcı tooroute trafik için bağlantı noktası. |
   | Arka uç havuzu |Bu havuz Merhaba kapsayıcılara Bu yük dengeleyici için hello hedef olacaktır. |
   | Araştırma |bir hedef durumunda hello araştırma toodetermine hello **arka uç havuzu** iyi değil. |
   | Oturum kalıcılığı |Merhaba hello oturumu süresince bir istemciden gelen trafiğin nasıl işleneceğini belirler.<br><br>**Hiçbiri**: aynı istemci tüm kapsayıcı tarafından işlenebilir hello gelen art arda gelen istekleri.<br>**İstemci IP**: aynı istemci IP tarafından işlenmesini hello gelen art arda gelen istekleri hello aynı kapsayıcı.<br>**İstemci IP ve Protokolü**: aynı istemci IP ve protokol birleşimi tarafından işlenmesini hello gelen art arda gelen istekleri hello aynı kapsayıcı. |
   | Boşta kalma zaman aşımı |(Yalnızca TCP) Dakika cinsinden süre tookeep TCP/HTTP İstemcisi'ni açmak öğesine bağlı kalmadan hello *tutma* iletileri. |

## <a name="add-a-security-rule-portal"></a>Güvenlik Kuralı (portal) Ekle
Ardından, tooadd hello güvenlik duvarı üzerinden bizim açılmış bağlantı noktasından trafiğini yönlendiren bir güvenlik kuralı gerekir.

1. Toohello Portalı'nda oturum açın.
2. Dağıttığınız Bul hello kaynak grubu hello Azure kapsayıcı hizmeti.
3. Select hello **ortak** Aracısı ağ güvenlik grubu (adlandırılmış benzer çok**XXXX-aracı-genel-nsg-XXXX**).
   
    ![Azure kapsayıcı hizmeti ağ güvenlik grubu](./media/container-service-enable-public-access/agent-nsg.png)
4. Seçin **gelen güvenlik kuralları** ve ardından **Ekle**.
   
    ![Azure kapsayıcı hizmeti ağ güvenlik grubu kuralları](./media/container-service-enable-public-access/add-firewall-rule.png)
5. Genel bağlantı noktanızın Hello güvenlik duvarı kuralı tooallow doldurun ve **Tamam**.
   
   | Alan | Açıklama |
   | --- | --- |
   | Ad |Merhaba güvenlik duvarı kuralı, açıklayıcı bir ad. |
   | Öncelik |Öncelik derecesi hello kuralı için. Merhaba alt hello sayı hello yüksek hello önceliği. |
   | Kaynak |İzin verilen veya reddedilen bu kural tarafından hello gelen IP adresi aralığı toobe kısıtlayın. Kullanım **herhangi** toonot bir kısıtlama belirtin. |
   | Hizmet |Bu güvenlik kuralı içindir önceden tanımlanmış Hizmetleri kümesi seçin. Aksi takdirde kullanmak **özel** toocreate kendi. |
   | Protokol |Temel trafiği kısıtlamak **TCP** veya **UDP**. Kullanım **herhangi** toonot bir kısıtlama belirtin. |
   | Bağlantı noktası aralığı |Zaman **hizmet** olan **özel**, bu kural etkileyen bağlantı noktalarının hello aralığını belirtir. Tek bir bağlantı noktası gibi kullanabilir **80**, veya bir aralık **1024 1500**. |
   | Eylem |İzin ver veya Reddet hello ölçütleri karşılayan trafiği. |

## <a name="next-steps"></a>Sonraki adımlar
Merhaba birbirinden hakkında bilgi edinin [ortak ve özel DC/OS aracıları](container-service-dcos-agents.md).

Hakkında daha fazla bilgi okuyun [DC/OS kapsayıcılarınızı yönetme](container-service-mesos-marathon-ui.md).

