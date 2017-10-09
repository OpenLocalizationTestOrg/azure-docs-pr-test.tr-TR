---
title: "aaaAzure uygulama hizmeti ortamı yönetimi adresleri"
description: "Bir uygulama hizmeti ortamı toocommand kullanılan listeleri hello yönetim adresleri"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: a7738a24-89ef-43d3-bff1-77f43d5a3952
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: b34b6266dc3a35915421b14bf34eddc07c2825c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-management-addresses"></a>Uygulama hizmeti ortamı yönetimi adresleri

Merhaba App Service Environment(ASE) Azure sanal ağınızda (VNet) bir alt ağ içinde hello Azure App Service dağıtımı ' dir.  Böylece, yönetilebilmesi için hello ana hello Azure App Service ' erişilebilir olması gerekir.  Bu ana yönetim trafiği hello kullanıcı tarafından denetlenen ağ erişir.  Merhaba ana ile ilişkili Azure uygulama hizmeti yönetim sunucuları toohello genel VIP geldiği.  Bağımlılıklar ağ hello ana hakkında ayrıntılı bilgi için okuma [ağ konuları ve hello uygulama hizmeti ortamı][networking].  Merhaba ana hakkında genel bilgi için ile başlatabilirsiniz [giriş toohello uygulama hizmeti ortamı][intro].

Bu belge hello kaynağı IP'leri yönetim trafiğini toohello ana listeler. Bu adresleri toocreate ağ güvenlik grupları toolock gelen trafiği tuşunu kullanın veya bunları gerektiği gibi rota tablolarda kullanın.  toouse toouse bu gerekenler:

* Tüm bölgeler için listelenen hello IP adresleri
* içine, ana dağıtılan o eşleşme toohello bölge Hello IP adresleri.

Merhaba gelen yönetim trafiğini bu IP adreslerinden tooports 454 ve 455 gelir.

| Bölge | Adresler |
|--------|-----------|
| Tüm bölgeler | 70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141 |
| Orta Güney ABD & Kuzey Orta ABD | 23.102.188.65, 191.236.154.88 |
| Avustralya Güneydoğu & Avustralya Doğu | 23.101.234.41, 104.210.90.65 |
| ABD Batı & ABD Doğu | 104.45.227.37, 191.236.60.72 |
| Batı Avrupa & Kuzey Avrupa | 191.233.94.45, 191.237.222.191 |
| Batı Orta ABD & Batı ABD 2 | 13.78.148.75, 13.66.225.188 |
| Orta ABD & Doğu ABD 2 | 104.43.165.73, 104.46.108.135 |
| Doğu Asya & Güneydoğu Asya | 23.99.115.5, 104.215.158.33 |
| Japonya Doğu & Japonya Batı | 104.41.185.116, 191.239.104.48 |
| Kanada Orta & Doğu Kanada | 40.85.230.101, 40.86.229.100 |
| Birleşik Krallık Batı & Birleşik Krallık Güney | 51.141.8.34, 51.140.185.75 |
| Kore Güney & Kore Merkezi | 52.231.200.177, 52.231.32.117 |
| Brezilya Güney & Orta Güney ABD| 104.41.46.178, 23.102.188.65 |
| Orta Hindistan & Güney Hindistan | 104.211.98.24, 104.211.225.66 |
| Batı Hindistan & Güney Hindistan | 104.211.160.229, 104.211.225.66 |


<!-- LINKS -->
[networking]: ./network-info.md
[intro]: ./intro.md
