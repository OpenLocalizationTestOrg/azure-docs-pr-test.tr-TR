---
title: "Azure PowerShell örnekleri - App Service | Microsoft Docs"
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
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: app-service
ms.date: 03/08/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: ba2bd2b185c395e54f2f085317a424a2aa1b4421
ms.sourcegitcommit: 176c575aea7602682afd6214880aad0be6167c52
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/09/2018
---
# <a name="azure-powershell-samples"></a>Azure PowerShell örnekleri

Aşağıdaki tabloda Azure PowerShell kullanarak yerleşik PowerShell betikleri bağlantılarını içerir.

| | |
|-|-|
|**Uygulama oluşturma**||
| [Github'dan dağıtımı ile bir web uygulaması oluşturma](./scripts/app-service-powershell-deploy-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Kod Github'dan çeken bir Azure web uygulaması oluşturur. |
| [GitHub’dan sürekli dağıtım ile bir web uygulaması oluşturma](./scripts/app-service-powershell-continuous-deployment-github.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Sürekli olarak kod github'dan dağıtan bir Azure web uygulaması oluşturur. |
| [Bir web uygulaması oluşturma ve FTP koduyla dağıtma](./scripts/app-service-powershell-deploy-ftp.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Bir Azure web app ve karşıya yükleme dosyaları FTP kullanarak yerel bir dizinden oluşturur. |
| [Yerel Git deposundan web uygulaması oluşturma ve kod dağıtma](./scripts/app-service-powershell-deploy-local-git.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Azure web uygulaması oluşturur ve kodun bir yerel Git deposundan yapılandırır. |
| [Hazırlık ortamında web uygulaması oluşturma ve kod dağıtma](./scripts/app-service-powershell-deploy-staging-environment.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Kod değişiklikleri hazırlama için bir dağıtım yuvası ile bir Azure web uygulaması oluşturur. |
|**Uygulamayı yapılandırma**||
| [Özel bir etki alanını bir web uygulaması ile eşleştirme](./scripts/app-service-powershell-configure-custom-domain.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Azure web uygulaması oluşturur ve bir özel etki alanı adı için eşleştirir. |
| [Bir web uygulaması için özel bir SSL sertifikası bağlama](./scripts/app-service-powershell-configure-ssl-certificate.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Azure web uygulaması oluşturur ve SSL sertifikası özel etki alanı adı kendisine bağlar. |
|**Ölçek uygulama**||
| [Web uygulamasını el ile ölçeklendirme](./scripts/app-service-powershell-scale-manual.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Azure web uygulaması oluşturur ve bunu 2 örneklerinde ölçeklendirir. |
| [Web uygulaması dünya çapında yüksek kullanılabilirlik mimarisi ile ölçeklendirme](./scripts/app-service-powershell-scale-high-availability.md?toc=%2fpowershell%2fmodule%2ftoc.json) | İki farklı coğrafi bölgelerde iki Azure web uygulamaları oluşturur ve bunları Azure trafik Yöneticisi'ni kullanarak tek bir uç noktası aracılığıyla kullanılabilir hale getirir. |
|**Uygulama kaynaklarına bağlanma**||
| [Bir web uygulaması bir SQL veritabanına bağlanma](./scripts/app-service-powershell-connect-to-sql.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Azure web uygulaması ve SQL veritabanı oluşturur, ardından veritabanı bağlantı dizesi için uygulama ayarları ekler. |
| [Bir web uygulamasını bir depolama hesabına bağlama](./scripts/app-service-powershell-connect-to-storage.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Azure web uygulaması ve bir depolama hesabı oluşturur, ardından depolama bağlantı dizesi için uygulama ayarları ekler. |
|**Yedekleme ve geri yükleme uygulaması**||
| [Bir web uygulamasını kurup yedekleyin](./scripts/app-service-powershell-backup-onetime.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Azure web uygulaması ve bir kerelik bir yedekleme için oluşturur. |
| [Bir web uygulaması için zamanlanmış yedekleme oluşturmak](./scripts/app-service-powershell-backup-scheduled.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Azure web uygulaması ve bir zamanlanmış yedekleme için oluşturur. |
| [Bir web uygulaması için bir yedek Sil](./scripts/app-service-powershell-backup-delete.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Bir web uygulaması için mevcut bir yedekleme siler. |
|**İzleyici uygulama**||
| [Web sunucusu günlükleri ile bir web uygulamasını izleme](./scripts/app-service-powershell-monitor.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Azure web uygulaması oluşturur, bunun için günlük kaydını etkinleştirir ve yerel makinenize günlükleri indirir. |
| | |
