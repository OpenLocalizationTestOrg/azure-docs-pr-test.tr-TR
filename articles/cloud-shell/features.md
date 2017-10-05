---
title: "Azure bulut Kabuk (Önizleme) özellikleri | Microsoft Docs"
description: "Azure bulut Kabuk özelliklerine genel bakış"
services: 
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
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 67f03d5857e37b253ac57536e289b5468d69e9b5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="features-and-tools-for-azure-cloud-shell"></a>Özellikler ve Araçlar Azure bulut Kabuğu
Azure bulut Kabuk, yönetmek ve Azure kaynaklarını geliştirmek için bir tarayıcı tabanlı kabuk deneyimidir.

Bulut Kabuk, sürümü, yükleme ve bir makineyi kendiniz koruma yükünü olmadan Azure kaynaklarını yönetmek için bir tarayıcı erişilebilir, önceden yapılandırılmış Kabuk deneyimi sunar.

İstek başına temelinde makineler bulut Kabuk sağlar ve sonuç olarak makine durumu oturumlarında kalıcı olmaz. Bulut Kabuk etkileşimli oturumları için kurulu olduğundan Kabukları Kabuğu kaldıktan 20 dakika sonra otomatik olarak sonlanır.

## <a name="bash-in-cloud-shell"></a>Bulut Kabuğu'nda bash
### <a name="tools"></a>Araçlar
|Kategori   |Ad   |
|---|---|
|Linux Kabuk yorumlayıcı|Bash<br> Paylaş               |
|Azure Araçları            |[Azure CLI 2.0](https://github.com/Azure/azure-cli) ve [1.0](https://github.com/Azure/azure-xplat-cli)<br> [AzCopy](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [Batch Shipyard](https://github.com/Azure/batch-shipyard)     |
|Metin düzenleyiciler           |VIM<br> nano<br> emacs       |
|Kaynak denetimi         |Git                    |
|Derleme araçları            |Yapma<br> maven<br> npm<br> PIP         |
|Kapsayıcılar             |[Docker CLI](https://github.com/docker/cli)/[Docker makine](https://github.com/docker/machine)<br> [Kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/)<br> [Taslak](https://github.com/Azure/draft)<br> [DC/OS CLI](https://github.com/dcos/dcos-cli)         |
|Veritabanları              |MySQL istemci<br> PostgreSql istemci<br> [SQLCMD yardımcı programı](https://docs.microsoft.com/sql/tools/sqlcmd-utility)<br> [MSSQL komut dosyası yazarları](https://github.com/Microsoft/sql-xplat-cli) |
|Diğer                  |iPython istemci<br> [Foundry CLI bulut](https://github.com/cloudfoundry/cli)<br> |

### <a name="language-support"></a>Dil desteği
|Dil   |Sürüm   |
|---|---|
|.NET       |1.01       |
|Başlayın         |1.7        |
|Java       |1.8        |
|Node.js    |6.9.4      |
|Python     |2.7 ve 3.5 (varsayılan)|

## <a name="secure-automatic-authentication"></a>Güvenli otomatik kimlik doğrulaması
Bulut Kabuğu güvenli bir şekilde ve otomatik olarak hesap erişim için Azure CLI 2.0 kimliğini doğrular.

## <a name="azure-files-persistence"></a>Azure dosyaları kalıcılığı
Bulut Kabuğu'nu kullanarak geçici bir makine bir istek başına temelinde ayrıldığından dosyaları $Home ve makine durumu dışında oturumlarında kalıcı değildir.
Dosyaları oturumlarında kalıcı hale getirmek için bulut Kabuk, ilk kez başlatıldığında Azure dosya paylaşımında ekleme aracılığıyla açıklanmaktadır.
Bir kez tamamlanmış bulut Kabuk otomatik olarak tüm sonraki oturumlar için depolama alanınızı ekleyecek.

[Azure dosya paylaşımları için bulut Kabuk ekleme hakkında daha fazla bilgi edinin.](persisting-shell-storage.md)

## <a name="next-steps"></a>Sonraki adımlar
[Bulut Kabuk hızlı başlangıç](quickstart.md) <br>
[Azure CLI 2.0 hakkında bilgi edinin](https://docs.microsoft.com/cli/azure/) <br>