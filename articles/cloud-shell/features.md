---
title: "Azure bulut Kabuk özelliklerinde bash | Microsoft Docs"
description: "Azure bulut Kabuk Bash'te özelliklerine genel bakış"
services: Azure
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/15/2017
ms.author: juluk
ms.openlocfilehash: a6627ab6febc763ae3f1cd464f26ad641f7c717d
ms.sourcegitcommit: 5ac112c0950d406251551d5fd66806dc22a63b01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/23/2018
---
# <a name="features--tools-for-bash-in-azure-cloud-shell"></a>Özellikler ve Azure bulut Kabuk Bash'te için araçları

[!INCLUDE [features-introblock](../../includes/cloud-shell-features-introblock.md)]

> [!TIP]
> Özellikleri & araçlarla [PowerShell](features-powershell.md) da kullanılabilir.

Bulut Kabuk çalışır bash `Ubuntu 16.04 LTS`.

## <a name="features"></a>Özellikler

### <a name="secure-automatic-authentication"></a>Güvenli otomatik kimlik doğrulaması

Bulut Kabuk bash'te güvenli bir şekilde ve otomatik olarak hesap erişim için Azure CLI 2.0 kimliğini doğrular.

### <a name="ssh-into-azure-linux-virtual-machines"></a>Azure Linux sanal makineleri içine SSH

Azure CLI 2. 0 bir Linux VM oluşturma varsayılan SSH anahtarı oluşturabilir ve yerleştirileceği, `$Home` dizin. SSH yerleştirme anahtarlar `$Home` etkinleştirir doğrudan SSH bağlantılar Azure Linux VM'ler için bulut Kabuğu'ndan doğrudan. Anahtarları acc_ içinde tutulur<user>dosya paylaşımınızı .img kullanırken veya dosya paylaşımı veya anahtarları erişimi paylaşımı en iyi uygulamaları kullanın.

### <a name="home-persistence-across-sessions"></a>Oturumlar arasında $Home kalıcılığı

Dosyaları oturumlarında kalıcı hale getirmek için bulut Kabuk, ilk kez başlatıldığında Azure dosya paylaşımında ekleme aracılığıyla açıklanmaktadır.
Tamamlandığında, bulut Kabuk otomatik olarak depolama ihtiyaçlarınızı ekleme (olarak takılı `$Home\clouddrive`) gelecekteki tüm oturumları için.
Ayrıca, bulut Kabuk Bash'te içinde `$Home` directory, Azure dosya paylaşımında bir .img olarak kalıcıdır.
Dışında dosyaları `$Home` ve makine durumunu oturumlar arasında sürdürülmez.

[Bulut Kabuk Bash'te kalıcı dosyaları hakkında daha fazla bilgi edinin.](persisting-shell-storage.md)

## <a name="tools"></a>Araçlar

|Kategori   |Ad   |
|---|---|
|Linux araçları            |Bash<br> Paylaş<br> tmux<br> dıg<br>               |
|Azure Araçları            |[Azure CLI 2.0](https://github.com/Azure/azure-cli) ve [1.0](https://github.com/Azure/azure-xplat-cli)<br> [AzCopy](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [Batch Shipyard](https://github.com/Azure/batch-shipyard) <br> [Service Fabric CLI](https://docs.microsoft.com/azure/service-fabric/service-fabric-cli) <br> [blobxfer](https://github.com/Azure/blobxfer#blobxfer) |
|Metin düzenleyiciler           |vim<br> nano<br> emacs       |
|Kaynak denetimi         |git                    |
|Derleme araçları            |Yapma<br> maven<br> npm<br> PIP         |
|Kapsayıcılar             |[Docker CLI](https://github.com/docker/cli)/[Docker Machine](https://github.com/docker/machine)<br> [Kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [Helm](https://github.com/kubernetes/helm)<br> [DC/OS CLI](https://github.com/dcos/dcos-cli)         |
|Veritabanları              |MySQL istemci<br> PostgreSql istemci<br> [sqlcmd Utility](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [mssql-scripter](https://github.com/Microsoft/sql-xplat-cli) |
|Diğer                  |iPython istemci<br> [Cloud Foundry CLI](https://github.com/cloudfoundry/cli)<br> [Terraform](https://www.terraform.io/docs/providers/azurerm/) |

## <a name="language-support"></a>Dil desteği

|Dil   |Sürüm   |
|---|---|
|.NET       |2.0.0       |
|Başlayın         |1.7        |
|Java       |1.8        |
|Node.js    |6.9.4      |
|PowerShell |[6.0 (beta)](https://github.com/PowerShell/powershell/releases)       |
|Python     |2.7 ve 3.5 (varsayılan)|

## <a name="next-steps"></a>Sonraki adımlar
[Bulut Kabuk hızlı başlangıcı bash](quickstart.md) <br>
[Azure CLI 2.0 hakkında bilgi edinin](https://docs.microsoft.com/cli/azure/)
