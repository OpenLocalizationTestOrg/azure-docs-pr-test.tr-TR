---
title: "aaaAzure PowerShell örnekleri - App Service | Microsoft Docs"
description: "Azure PowerShell örnekleri - uygulama hizmeti"
services: app-service
documentationcenter: app-service
author: syntaxc4
manager: erikre
editor: ggailey777
tags: azure-service-management
ms.assetid: b48d1137-8c04-46e0-b430-101e07d7e470
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: app-service
ms.date: 03/08/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: b7b4a030364f797195522c56fbae5b7f530d4d1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-powershell-samples"></a>Azure PowerShell örnekleri

Merhaba aşağıdaki tabloda bağlantıları toobash hello Azure PowerShell kullanılarak oluşturulan komut dosyalarını içerir.

| | |
|-|-|
|**Uygulama oluşturma**||
| [Github'dan dağıtımı ile bir web uygulaması oluşturma](./scripts/app-service-powershell-deploy-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Kod Github'dan çeken bir Azure web uygulaması oluşturur. |
| [GitHub’dan sürekli dağıtım ile bir web uygulaması oluşturma](./scripts/app-service-powershell-continuous-deployment-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Sürekli olarak kod github'dan dağıtan bir Azure web uygulaması oluşturur. |
| [Bir web uygulaması oluşturma ve FTP koduyla dağıtma](./scripts/app-service-powershell-deploy-ftp.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Bir Azure web app ve karşıya yükleme dosyaları FTP kullanarak yerel bir dizinden oluşturur. |
| [Yerel Git deposundan web uygulaması oluşturma ve kod dağıtma](./scripts/app-service-powershell-deploy-local-git.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Azure web uygulaması oluşturur ve kodun bir yerel Git deposundan yapılandırır. |
| [Bir web uygulaması oluşturma ve ortam hazırlama kodu tooa dağıtma](./scripts/app-service-powershell-deploy-staging-environment.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Kod değişiklikleri hazırlama için bir dağıtım yuvası ile bir Azure web uygulaması oluşturur. |
|**Uygulamayı yapılandırma**||
| [Bir özel etki alanı tooa web uygulaması eşleme](./scripts/app-service-powershell-configure-custom-domain.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Azure web uygulaması oluşturur ve bir özel etki alanı adı tooit eşler. |
| [Özel SSL sertifika tooa web uygulama bağlama](./scripts/app-service-powershell-configure-ssl-certificate.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Azure web uygulaması oluşturur ve bir özel etki alanı adı tooit hello SSL sertifikasını bağlar. |
|**Ölçek uygulama**||
| [Web uygulamasını el ile ölçeklendirme](./scripts/app-service-powershell-scale-manual.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Azure web uygulaması oluşturur ve bunu 2 örneklerinde ölçeklendirir. |
| [Web uygulaması dünya çapında yüksek kullanılabilirlik mimarisi ile ölçeklendirme](./scripts/app-service-powershell-scale-high-availability.md?toc=%2fpowershell%2fmodule%2ftoc.json) | İki farklı coğrafi bölgelerde iki Azure web uygulamaları oluşturur ve bunları Azure trafik Yöneticisi'ni kullanarak tek bir uç noktası aracılığıyla kullanılabilir hale getirir. |
|**Uygulama tooresources Bağlan**||
| [Bir web uygulaması tooa SQL veritabanına bağlanma](./scripts/app-service-powershell-connect-to-sql.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Azure web uygulaması ve SQL veritabanı oluşturur ve ardından hello veritabanı bağlantı dizesi toohello uygulama ayarlarını ekler. |
| [Bir web uygulaması tooa depolama hesabına bağlanma](./scripts/app-service-powershell-connect-to-storage.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Azure web uygulaması ve bir depolama hesabı oluşturur, ardından hello depolama bağlantı dizesi toohello uygulama ayarları ekler. |
|**İzleyici uygulama**||
| [Web sunucusu günlükleri ile bir web uygulamasını izleme](./scripts/app-service-powershell-monitor.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Azure web uygulaması oluşturur, bunun için günlük kaydını etkinleştirir ve hello günlükleri tooyour yerel makine indirir. |
| | |
