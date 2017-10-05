---
title: "Bir Azure depolama alanına bağlanan bir Azure işlevi oluşturma | Microsoft Docs"
description: "Azure CLI betik örnek - bir Azure depolama alanına bağlanan bir Azure işlevi oluşturma"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: 36dbc2c181c9991a27163e3194800f63c6c0e01e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-function-app-into-azure-storage-account"></a>Azure Storage hesabınıza işlev uygulaması tümleştirme

Bu örnek betik, bir işlev uygulaması ve depolama hesabı oluşturur.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir. Sürümü bulmak için `az --version` komutunu çalıştırın. Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Örnek komut dosyası

Bu örnek bir Azure işlevi uygulamasını oluşturur ve bir uygulama ayarı için depolama bağlantı dizesi ekler.

[!code-azurecli-interactive[Ana](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "işlevi uygulamaya tümleştirmek Azure depolama hesabı")]


## <a name="clean-up-deployment"></a>Dağıtımı temizleme

Komut dosyası örneği çalıştırdıktan sonra kaynak grubu, App Service uygulaması kaldırmak için aşağıdaki komut kullanılabilir ve tüm kaynakları ilgili:

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyasını aşağıdaki komutları kullanır. Komut belirli belgeleri tablo bağlanan her komut.

| Komut | Notlar |
|---|---|
| [az oturum açma](https://docs.microsoft.com/cli/azure/#login) | Azure oturum açın. |
| [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) | Konumu ile kaynak grubu oluştur |
| [az depolama hesabı oluşturma](https://docs.microsoft.com/cli/azure/storage/account) | Depolama hesabı oluşturma |
| [az functionapp oluşturma](https://docs.microsoft.com/cli/azure/functionapp#create) | Yeni bir işlev uygulaması oluşturma |
| [az grubu Sil](https://docs.microsoft.com/cli/azure/group#delete) | Temizleme |

## <a name="next-steps"></a>Sonraki adımlar

Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek Azure işlevleri CLI kod örnekleri bulunabilir [Azure işlevleri belgelerine](../functions-cli-samples.md).
