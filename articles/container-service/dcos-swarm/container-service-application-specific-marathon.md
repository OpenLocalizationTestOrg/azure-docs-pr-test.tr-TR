---
title: "Uygulama veya kullanıcıya özel Marathon hizmeti | Microsoft Belgeleri"
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
ms.openlocfilehash: b265763fb5dad240edd710cd8d0fb1079e3a7b51
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-or-user-specific-marathon-service"></a>Bir uygulama veya kullanıcıya özel Marathon hizmeti oluşturma
Azure Kapsayıcı Hizmeti, Apache Mesos ve Marathon’u önceden üzerinde yapılandırdığımız bir grup ana sunucu sağlar. Bunlar, uygulamalarınızı kümede düzenlemek için kullanılabilir, ancak en iyisi ana sunucuları bu amaç için kullanmamaktır. Örneğin, Marathon yapılandırmasına ince ayar yapma ana sunucuların kendilerinde oturum açmayı ve değişiklikler yapmayı gerektirir; bu, standart olandan biraz daha farklı olan benzersiz ana sunucuları teşvik eder ve bağımsız olarak ilgilenilmeli ve yönetilmelidir. Ayrıca, bir takım tarafından istenen yapılandırma başka bir takım için en uygun yapılandırma olmayabilir.

Bu makalede size bir uygulamaya veya kullanıcıya özel Marathon hizmeti ekleme açıklanmaktadır.

Bu hizmet bir tek bir kullanıcı veya ekibe ait olduğundan bunlar istenen herhangi bir şekilde yapılandırılabilir. Ayrıca, Azure Container Service hizmetin çalışmaya devam etmesini sağlar. Hizmet başarısız olursa Azure Container Service sizin için yeniden başlatır. Çoğu zaman kesinti yaşandığının farkına varmazsınız bile.

## <a name="prerequisites"></a>Ön koşullar
[DC/OS orchestrator türüyle Azure Container Service örneğini dağıtın](container-service-deployment.md) ve [istemcinizin kümenize bağlanabildiğinden emin olun](../container-service-connect.md). Ayrıca aşağıdaki adımları uygulayın.

[!INCLUDE [install the DC/OS CLI](../../../includes/container-service-install-dcos-cli-include.md)]

## <a name="create-an-application-or-user-specific-marathon-service"></a>Bir uygulama veya kullanıcıya özel Marathon hizmeti oluşturma
Oluşturmak istediğiniz uygulama hizmeti adını tanımlayan bir JSON yapılandırma dosyası oluşturarak başlayın. Burada çerçeve adı olarak `marathon-alice` kullanıyoruz. Dosyayı `marathon-alice.json` benzeri şekilde kaydedin:

```json
{"marathon": {"framework-name": "marathon-alice" }}
```

Ardından, Marathon örneğini yapılandırma dosyanızda ayarlanan seçenek grubuyla yüklemek için DC/OS CLI’yı kullanın:

```bash
dcos package install --options=marathon-alice.json marathon
```

Şimdi, DC/OS kullanıcı arabiriminizin Hizmetler sekmesinde `marathon-alice` hizmetinizin çalıştığını görmelisiniz. Doğrudan erişmek isterseniz kullanıcı arabirimi `http://<hostname>/service/marathon-alice/` olur.

## <a name="set-the-dcos-cli-to-access-the-service"></a>Hizmete erişmek için DC/OS CLI’yı ayarlama
İsteğe bağlı olarak, `marathon.url` özelliğini aşağıdaki şekilde `marathon-alice` örneğini işaret edecek şekilde ayarlayarak DC/OS CLI’nizi bu yeni hizmete erişmek üzere yapılandırabilirsiniz.

```bash
dcos config set marathon.url http://<hostname>/service/marathon-alice/
```

CLI’nizin hangi Marathon örneğine karşı çalıştığını `dcos config show` komutuyla doğrulayabilirsiniz. `dcos config unset marathon.url` komutuyla ana Marathon hizmetinizi kullanmaya geri dönebilirsiniz.

