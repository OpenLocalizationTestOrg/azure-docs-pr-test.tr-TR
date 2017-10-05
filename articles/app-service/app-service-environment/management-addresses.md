---
title: "Azure uygulama hizmeti ortamı yönetimi adresleri"
description: "Bir uygulama hizmeti ortamı komutu için kullanılan yönetim adreslerini listeler"
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
ms.openlocfilehash: e97a084772fd16252d925b62498d2e696629a25d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="app-service-environment-management-addresses"></a>Uygulama hizmeti ortamı yönetimi adresleri

Uygulama hizmeti Environment(ASE) Azure uygulama hizmeti dağıtımı Azure sanal ağınızda (VNet) bir alt ağ içinde ' dir.  Böylece, yönetilebilmesi için ana Azure App hizmetinden erişilebilir olması gerekir.  Bu ana yönetim trafiği, kullanıcı tarafından denetlenen ağ erişir.  Azure uygulama hizmeti yönetim sunucularından ana ile ilişkili ortak VIP için gelir.  Ana hakkında ayrıntılı bilgi için ağ okuma bağımlılıkları [ağ konuları ve uygulama hizmeti ortamı][networking].  Ana hakkında genel bilgi için ile başlatabilirsiniz [uygulama hizmeti ortamı giriş][intro].

Bu belge, yönetim trafiği için ana IP'leri kaynak listeler. Bu adreslerden gelen trafiği kilitlemek veya bunları gerektiği gibi rota tablolarda kullanmak için ağ güvenlik grupları oluşturmak için kullanabilirsiniz.  Bu bilgileri kullanmak için kullanmanız gerekir:

* Tüm bölgeler için listelenen IP adresleri
* içine, ana dağıtılan bölge için aynı IP adresleri.

Gelen yönetim trafiğini bu IP adreslerinden 454 ve 455 bağlantı noktalarına gelir.

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
