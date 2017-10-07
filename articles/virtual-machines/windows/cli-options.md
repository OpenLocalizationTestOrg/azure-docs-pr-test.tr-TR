---
title: Windows Azure CLI aaaUsing hello | Microsoft Docs
description: Windows Hello Azure CLI kullanma
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/14/2017
ms.author: nepeters
ms.openlocfilehash: edca4a2701a7dfc0fc54df5649e8a5e7afc95490
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-on-windows"></a>Windows Hello Azure CLI kullanma

Hello Azure komut satırı arabirimi (CLI), bir komut satırı ve oluşturmak ve Azure kaynaklarınızı yönetmek için komut dosyası ortamı sağlar. Hello Azure CLI macOS, Linux ve Windows işletim sistemleri için kullanılabilir. İşletim sistemi belirli sözdiziminin farklı olabilir ancak bu işletim sistemleri arasında hello CLI komutları, aynıdır.

Azure CLI hello bu belge ayrıntıları hello yolları yüklü ve Windows ve ayrıntıları söz dizimi konuları her çalıştırın. Ayrıntılı Azure CLI belgelere bakın, [Azure CLI belgelerine]( https://docs.microsoft.com/en-us/cli/azure/overview).

## <a name="windows-subsystem-for-linux"></a>Linux için Windows alt sistem

Merhaba Windows alt sistemi için Linux (WSL), Windows 10 Anniversary ve sonraki sürümleri bir Ubuntu Linux ortam sağlar. Etkinleştirildiğinde, WSL oluşturmak ve Azure CLI komut dosyaları çalıştırmak için kullanılan bir yerel Bash deneyimi sağlar. WSL yerel bir Bash deneyimi sağladığından, Azure CLI betikleri macOS, Linux ve Windows arasında değişiklik yapmadan paylaşılabilir.

toouse hello WSL, Azure CLI hello aşağıdaki tamamlayın.

|Görev | Yönergeleri |
|---|---|
| WSL etkinleştir | [WSL belge yükleme](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) |
| Hello Azure CLI yükleme |[Merhaba CLI WSL/Ubuntu 14.04 yükleyin](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#ubuntu)|

## <a name="powershell"></a>PowerShell

Windows Hello Azure CLI yerel olarak çalıştırılabilir. Bu yapılandırmada, hello Azure CLI paketinin hello Windows işletim sisteminde yüklü olduğu ve Powershell'den komutları çalıştırabilirsiniz. Platform özel komut dosyası sözdizimi gerekli değildir ancak bu yapılandırmada, Azure CLI komutları ve komut dosyaları Windows, desteklenen tüm sürümlerinde çalıştırılabilir. Bu nedenle, komut dosyaları mutlaka macOS, Linux ve Windows arasında değişiklik yapmadan paylaşılamaz.

toouse hello Windows, Azure CLI yükleme bu yönergeleri kullanarak hello paketini [yükleme hello Windows CLI](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2#windows).

## <a name="docker-image"></a>Docker görüntüsü

Windows için Docker kullanırken, Docker görüntü hello Azure CLI içeren başlatılabilir. Bu görüntü dışına Linux tabanlı ve yerel bir Bash deneyimi içerir.  Kullanırken Windows için Docker ve hello Azure CLI görüntü, komut dosyaları toobe macOS, Linux ve Windows arasında paylaşılan. 

toouse hello Docker için Windows Azure CLI için Docker Windows çalıştıran ve hello aşağıdaki komutu çalıştırın emin olun.

```bash
docker run -it azuresdk/azure-cli-python:latest bash
```

Tamamlandığında, oturumu diğer bir deyişle başlatmak Bash hello Azure CLI araçlarını ile önceden yüklü.

## <a name="next-steps"></a>Sonraki Adımlar

[Azure sanal makineleri için CLI örnek](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Azure Web uygulamaları için CLI örnekleri](../../app-service-web/app-service-cli-samples.md)

[Azure SQL CLI örnekleri](../../sql-database/sql-database-cli-samples.md)
