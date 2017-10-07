---
title: "diğer Azure hizmetleriyle Azure DNS aaaUsing | Microsoft Docs"
description: "Nasıl toouse Azure DNS tooresolve ad için diğer Azure hizmetlerini anlama"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure dns
ms.assetid: e9b5eb94-7984-4640-9930-564bb9e82b78
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 09/21/2016
ms.author: gwallace
ms.openlocfilehash: 791f93d6aff2c638c08518e9f1e8ab89ac8de3f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-azure-dns-works-with-other-azure-services"></a>Azure DNS diğer Azure hizmetleriyle nasıl çalışır?

Azure DNS bir barındırılan DNS Yönetimi ve ad çözümleme hizmetidir. Bu, toocreate ortak DNS adlarını hello diğer uygulama ve hizmetlerin Azure üzerinde dağıtılan sağlar. Özel etki alanınızda bir Azure hizmeti için bir ad oluşturma, hizmetiniz için hello doğru türde bir kayıt ekleme olarak kadar basittir.

* Dinamik olarak ayrılan IP adresleri için oluşturulan Azure o eşlemeleri toohello DNS adını hizmetiniz için bir DNS CNAME kaydı oluşturmalısınız. DNS standartlarında hello bölge tepesinde CNAME kaydı kullanmanızı engelleyebilir.
* Statik olarak ayrılan IP adresleri için herhangi bir ad kullanarak bir DNS A kaydı oluşturabilirsiniz dahil olmak üzere bir *naked etki alanı* hello bölge tepesinde adresindeki adı.

Merhaba aşağıdaki tabloda ana hatlarını hello çeşitli Azure Hizmetleri için kullanılan kayıt türleri desteklenir. Bu tablodan görebileceğiniz gibi Azure DNS yalnızca Internet'e dönük ağ kaynakları için DNS kayıtlarını destekler. Azure DNS, iç, özel adresler ad çözümlemesi için kullanılamaz.

| Azure Hizmeti | Ağ arabirimi | Açıklama |
| --- | --- | --- |
| Application Gateway |[Ön uç genel IP](dns-custom-domain.md#public-ip-address) |Bir DNS A veya CNAME kaydı oluşturabilirsiniz. |
| Yük Dengeleyici |[Ön uç genel IP](dns-custom-domain.md#public-ip-address)  |Bir DNS A veya CNAME kaydı oluşturabilirsiniz. Yük Dengeleyici dinamik olarak atanmış bir IPv6 genel IP adresine sahip olabilir. Bu nedenle, bir IPv6 adresi için bir CNAME kaydı oluşturmanız gerekir. |
| Traffic Manager |Ortak ad |Yalnızca toohello trafficmanager.net adı tooyour trafik Yöneticisi profili atanmış eşleyen bir CNAME oluşturabilirsiniz. Daha fazla bilgi için bkz: [trafik Yöneticisi nasıl çalışır](../traffic-manager/traffic-manager-overview.md#traffic-manager-example). |
| Bulut hizmeti |[Genel IP](dns-custom-domain.md#public-ip-address) |Statik olarak ayrılan IP adresleri için bir DNS A kaydı oluşturabilirsiniz. Dinamik olarak ayrılan IP adresleri için toohello eşleyen bir CNAME kaydı oluşturmanız gerekir *cloudapp.net* adı. Bu kural, bir bulut hizmeti olarak dağıtılan olduğundan hello Klasik portalında oluşturulan tooVMs uygular. Daha fazla bilgi için bkz: [bulut Hizmetleri'nde bir özel etki alanı adı yapılandırma](../cloud-services/cloud-services-custom-domain-name-portal.md). |
| App Service | [Dış IP](dns-custom-domain.md#app-service-web-apps) |Dış IP adresleri için bir DNS A kaydı oluşturabilirsiniz. Aksi takdirde, toohello azurewebsites.net adı eşleyen bir CNAME kaydı oluşturmanız gerekir. Daha fazla bilgi için bkz: [özel etki alanı adı tooan Azure uygulaması eşleme](../app-service-web/web-sites-custom-domain-name.md) |
| Kaynak Yöneticisi Vm'leri |[Genel IP](dns-custom-domain.md#public-ip-address) |Kaynak Yöneticisi Vm'leri genel IP adresleri olabilir. Bir genel IP adresine sahip bir VM, bir yük dengeleyicinin arkasına de olabilir. Merhaba genel adresi için bir DNS A veya CNAME kaydı oluşturabilirsiniz. Bu özel ad kullanılan toobypass hello hello yük dengeleyici VIP olabilir. |
| Klasik VM'ler |[Genel IP](dns-custom-domain.md#public-ip-address) |PowerShell kullanarak Klasik VM'ler oluşturulduktan veya CLI dinamik veya statik (ayrılmış) sahip sanal bir adresi yapılandırılabilir. Bir DNS CNAME veya bir kayıt sırasıyla oluşturabilirsiniz. |
