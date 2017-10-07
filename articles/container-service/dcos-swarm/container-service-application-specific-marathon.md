---
title: "aaaApplication veya kullanıcıya özel Marathon hizmeti | Microsoft Docs"
description: "Bir uygulama veya kullanıcıya özel Marathon hizmeti oluşturma"
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kapsayıcılar, Marathon, Mikro hizmetler, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 1e6f69ed64e113a3a059788a71ddb57b6d3ad8da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-or-user-specific-marathon-service"></a>Bir uygulama veya kullanıcıya özel Marathon hizmeti oluşturma
Azure Kapsayıcı Hizmeti, Apache Mesos ve Marathon’u önceden üzerinde yapılandırdığımız bir grup ana sunucu sağlar. Bunlar kullanılan tooorchestrate olabilir uygulamalarınızı hello küme, ancak buna ait toouse hello ana sunucuları bu amaç için en iyi. Örneğin, Marathon hello yapılandırmasını uyguladıkça hello ana sunucuların kendilerini günlüğü--bu değişiklik gerektirir ve biraz farklı hello standart ve gerek toobe ilgilenilmeli ve yönetilen benzersiz ana sunucuları teşvik eder bağımsız olarak. Ayrıca, bir takım tarafından istenen hello yapılandırma hello başka bir takım için en uygun yapılandırma olmayabilir.

Bu makalede, açıklayacağız nasıl tooadd bir uygulama veya kullanıcıya özel Marathon hizmeti.

Bu hizmet tooa tek bir kullanıcı veya ekibe ait olduğundan, ücretsiz tooconfigure olduklarından, istenen herhangi bir şekilde. Ayrıca, Azure kapsayıcı hizmeti hello hizmetini toorun sürdürür güvence altına alır. Merhaba hizmet başarısız olursa, Azure kapsayıcı hizmeti onu sizin için yeniden başlatılır. Başlangıç zamanının çoğunu bile kesinti yaşandığının farkına olmaz.

## <a name="prerequisites"></a>Ön koşullar
[Azure kapsayıcı hizmeti örneğini dağıtın](container-service-deployment.md) orchestrator ile DC/OS yazın ve [istemciniz tooyour küme bağlanabildiğinizden emin olun](../container-service-connect.md). Ayrıca, adımları hello.

[!INCLUDE [install hello DC/OS CLI](../../../includes/container-service-install-dcos-cli-include.md)]

## <a name="create-an-application-or-user-specific-marathon-service"></a>Bir uygulama veya kullanıcıya özel Marathon hizmeti oluşturma
Merhaba toocreate istediğiniz hello uygulama hizmeti adını tanımlayan bir JSON yapılandırma dosyası oluşturarak başlayın. Burada kullandığımız `marathon-alice` hello çerçeve adı olarak. Merhaba dosya benzeri şekilde kaydedin `marathon-alice.json`:

```json
{"marathon": {"framework-name": "marathon-alice" }}
```

Ardından, hello DC/OS CLI tooinstall hello Marathon örneğini yapılandırma dosyanızda ayarlanan hello seçenekleri ile kullanın:

```bash
dcos package install --options=marathon-alice.json marathon
```

Artık görmelisiniz, `marathon-alice` hello Hizmetleri sekmesinde DC/OS kullanıcı Arabirimi çalışan hizmeti. Merhaba UI olacaktır `http://<hostname>/service/marathon-alice/` tooaccess istiyorsanız doğrudan.

## <a name="set-hello-dcos-cli-tooaccess-hello-service"></a>Merhaba DC/OS CLI tooaccess hello hizmetini Ayarla
İsteğe bağlı olarak, DC/OS CLI tooaccess bu yeni hizmet ayarı hello tarafından yapılandırabileceğiniz `marathon.url` özelliği toopoint toohello `marathon-alice` gibi örneği:

```bash
dcos config set marathon.url http://<hostname>/service/marathon-alice/
```

Hangi, CLI ile Merhaba karşı çalıştığından Marathon örneğine doğrulayabilirsiniz `dcos config show` komutu. Merhaba komutuyla ana Marathon hizmetinizi toousing döndürebilirsiniz `dcos config unset marathon.url`.

