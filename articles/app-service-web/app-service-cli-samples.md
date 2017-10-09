---
title: "aaaAzure CLI örnekler - App Service | Microsoft Docs"
description: "Azure CLI örnekler - uygulama hizmeti"
services: app-service
documentationcenter: app-service
author: syntaxc4
manager: erikre
editor: ggailey777
tags: azure-service-management
ms.assetid: 53e6a15a-370a-48df-8618-c6737e26acec
ms.service: app-service
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: app-service
ms.date: 03/08/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: a943ccffb59c5d30a44cf1ce513fd2eac46101f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples"></a>Azure CLI örnekleri

Merhaba aşağıdaki tabloda bağlantıları toobash hello Azure CLI kullanarak oluşturulan komut dosyalarını içerir.

| | |
|-|-|
|**Uygulama oluşturma**||
| [GitHub’dan web uygulaması oluşturma ve kod dağıtma](./scripts/app-service-cli-deploy-github.md?toc=%2fcli%2fazure%2ftoc.json)| Azure web uygulaması oluşturur ve genel bir GitHub depo koddan dağıtır. |
| [GitHub’dan sürekli dağıtım ile bir web uygulaması oluşturma](./scripts/app-service-cli-continuous-deployment-github.md?toc=%2fcli%2fazure%2ftoc.json)| Sahip olduğunuz bir GitHub depodan sürekli yayımlama ile bir Azure web uygulaması oluşturur. |
| [Yerel Git deposundan web uygulaması oluşturma ve kod dağıtma](./scripts/app-service-cli-deploy-local-git.md?toc=%2fcli%2fazure%2ftoc.json) | Azure web uygulaması oluşturur ve kodun bir yerel Git deposundan yapılandırır. |
| [Bir web uygulaması oluşturma ve ortam hazırlama kodu tooa dağıtma](./scripts/app-service-cli-deploy-staging-environment.md?toc=%2fcli%2fazure%2ftoc.json) | Kod değişiklikleri hazırlama için bir dağıtım yuvası ile bir Azure web uygulaması oluşturur. |
| [Bir Docker kapsayıcısında bir ASP.NET Core web uygulaması oluşturma](./scripts/app-service-cli-linux-docker-aspnetcore.md?toc=%2fcli%2fazure%2ftoc.json)| Linux üzerinde Azure web uygulaması oluşturur ve Docker hub'dan Docker resmini yükler. |
|**Uygulamayı yapılandırma**||
| [Bir özel etki alanı tooa web uygulaması eşleme](./scripts/app-service-cli-configure-custom-domain.md?toc=%2fcli%2fazure%2ftoc.json)| Azure web uygulaması oluşturur ve bir özel etki alanı adı tooit eşler. |
| [Özel SSL sertifika tooa web uygulama bağlama](./scripts/app-service-cli-configure-ssl-certificate.md?toc=%2fcli%2fazure%2ftoc.json)| Azure web uygulaması oluşturur ve bir özel etki alanı adı tooit hello SSL sertifikasını bağlar. |
|**Ölçek uygulama**||
| [Web uygulamasını el ile ölçeklendirme](./scripts/app-service-cli-scale-manual.md?toc=%2fcli%2fazure%2ftoc.json) | Azure web uygulaması oluşturur ve bunu 2 örneklerinde ölçeklendirir. |
| [Web uygulaması dünya çapında yüksek kullanılabilirlik mimarisi ile ölçeklendirme](./scripts/app-service-cli-scale-high-availability.md?toc=%2fcli%2fazure%2ftoc.json) | İki farklı coğrafi bölgelerde iki Azure web uygulamaları oluşturur ve bunları Azure trafik Yöneticisi'ni kullanarak tek bir uç noktası aracılığıyla kullanılabilir hale getirir. |
|**Uygulama tooresources Bağlan**||
| [Bir web uygulaması tooa SQL veritabanına bağlanma](./scripts/app-service-cli-app-service-sql.md?toc=%2fcli%2fazure%2ftoc.json)| Azure web uygulaması ve SQL veritabanı oluşturur ve ardından hello veritabanı bağlantı dizesi toohello uygulama ayarlarını ekler. |
| [Bir web uygulaması tooa depolama hesabına bağlanma](./scripts/app-service-cli-app-service-storage.md?toc=%2fcli%2fazure%2ftoc.json)| Azure web uygulaması ve bir depolama hesabı oluşturur, ardından hello depolama bağlantı dizesi toohello uygulama ayarları ekler. |
| [Bir web uygulaması tooa redis Önbelleği'ne bağlama](./scripts/app-service-cli-app-service-redis.md?toc=%2fcli%2fazure%2ftoc.json) | Azure web uygulaması ve redis önbelleği oluşturur, ardından hello redis bağlantı ayrıntıları toohello uygulama ayarlarını ekler.) |
| [Bir web uygulaması tooCosmos DB Bağlan](./scripts/app-service-cli-app-service-documentdb.md?toc=%2fcli%2fazure%2ftoc.json) | Azure web uygulaması ve Cosmos DB oluşturur, ardından hello Cosmos DB bağlantı ayrıntıları toohello uygulama ayarlarını ekler. |
|**İzleyici uygulama**||
| [Web sunucusu günlükleri ile bir web uygulamasını izleme](./scripts/app-service-cli-monitor.md?toc=%2fcli%2fazure%2ftoc.json) | Azure web uygulaması oluşturur, bunun için günlük kaydını etkinleştirir ve hello günlükleri tooyour yerel makine indirir. |
| | |