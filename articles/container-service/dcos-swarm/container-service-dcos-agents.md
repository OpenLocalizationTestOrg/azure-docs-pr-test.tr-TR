---
title: "Azure kapsayıcı hizmeti için aaaDC/OS aracısı havuzları | Microsoft Docs"
description: "Merhaba ortak ve özel aracı havuzları, Azure kapsayıcı hizmeti DC/OS kümesi ile nasıl çalışır?"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Kapsayıcılar, Mikro hizmetler, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: c7d3889db07cb9908e8b68b668bd8a14ef3c2552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-agent-pools-for-azure-container-service"></a>Azure kapsayıcı hizmeti DC/OS aracısı havuzları
Azure kapsayıcı hizmeti DC/OS kümelerde iki havuzları, ortak bir havuzu ve özel bir havuzu Aracısı düğümleri içerir. Bir uygulama dağıtılabilir kapsayıcı hizmetiniz makinelerinizde arasında erişilebilirlik etkileyen tooeither havuzu. Merhaba makineler gösterilen toohello olabilir Internet (Genel) veya dahili (özel) tutulur. Bu makalede vardır neden ortak ve özel havuzları kısa bir genel bakış sağlar.


* **Özel aracılar**: özel aracı düğümleri yönlendirilemeyen bir ağ üzerinden çalıştırın. Bu ağ, yalnızca hello yönetici bölgeden veya hello genel bölge sınır yönlendiricisi aracılığıyla erişilebilir. Varsayılan olarak, DC/OS özel aracı düğümlerde uygulamaları başlatır. 

* **Ortak aracıları**: ortak aracı düğümleri, genel olarak erişilebilir bir ağ üzerinden DC/OS uygulamaları ve Hizmetleri çalıştırın. 

DC/OS ağ güvenliği hakkında daha fazla bilgi için bkz: Merhaba [DC/OS belgelerine](https://dcos.io/docs/1.7/administration/securing-your-cluster/).

## <a name="deploy-agent-pools"></a>Aracı havuzu dağıtma

Merhaba DC/OS aracısı havuzları, Azure kapsayıcı hizmeti şu şekilde oluşturulur:

* Merhaba **özel havuzu** ne zaman belirtin Aracısı düğümleri hello sayısını içerir, [hello DC/OS kümesi dağıtma](container-service-deployment.md). 

* Merhaba **ortak havuzu** başlangıçta Aracısı düğümleri sayısı önceden belirlenmiştir içerir. Merhaba DC/OS kümesi sağlandığında bu havuzu otomatik olarak eklenir.

Merhaba özel havuzu ve hello ortak havuzu Azure sanal makine ölçek kümeleridir. Dağıtımdan sonra bu havuzlarını yeniden boyutlandırabilirsiniz.

## <a name="use-agent-pools"></a>Aracı havuzlarını kullanın
Varsayılan olarak, **Marathon** herhangi yeni uygulama toohello dağıtır *özel* Aracısı düğümleri. Merhaba uygulama toohello dağıtmak tooexplicitly sahip *ortak* Merhaba uygulaması hello oluşturulması sırasında düğüm. Select hello **isteğe bağlı** sekmesinde ve girin **slave_public** hello için **kabul edilen kaynak rolleri** değeri. Bu işlem belgelenen [burada](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) ve hello [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) belgeleri.

## <a name="next-steps"></a>Sonraki adımlar
* Daha fazla bilgi edinin [DC/OS kapsayıcılarınızı yönetme](container-service-mesos-marathon-ui.md).

* Nasıl çok öğrenin[hello Güvenlik Duvarı'nı açın](container-service-enable-public-access.md) Azure tooallow genel erişim tooyour DC/OS kapsayıcıları tarafından sağlanan.

