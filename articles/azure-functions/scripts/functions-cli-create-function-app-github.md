---
title: "Bir işlev uygulaması oluşturma ve işlev kodu github'dan dağıtma | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - bir işlev uygulaması oluşturma ve işlev kodu github'dan dağıtma"
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: d67e85f91c80efe464fceb1105243bedfba83a0f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-function-app-and-deploy-function-code-from-github"></a>Bir işlev uygulaması oluşturma ve işlev kodu github'dan dağıtma

Bu örnek komut dosyası kullanarak bir işlev uygulaması oluşturur [tüketim planı](../functions-scale.md#consumption-plan) ile ilgili kaynaklarını ve ortak bir GitHub deposuna (sürekli dağıtımı) olmadan işlev kodunuzdan dağıtır. İşlev kodu github'dan kesintisiz teslim okuma [bir işlev uygulaması oluşturma ve sürekli olarak Github'dan dağıtma](functions-cli-create-function-app-github-continuous.md)

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir. Sürümü bulmak için `az --version` komutunu çalıştırın. Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Örnek komut dosyası

Bu örnek bir Azure işlevi uygulamasını oluşturur ve işlev kodu github'dan dağıtır.

[!code-azurecli-interactive[Ana](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "github'dan dağıtım ile işlev uygulaması oluşturma")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Komut dosyası açıklaması

Komut belirli belgeleri tablo bağlanan her komut. Bu komut dosyasını aşağıdaki komutları kullanır:

| Komut | Notlar |
|---|---|
| [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az depolama hesabı oluşturma](https://docs.microsoft.com/cli/azure/appservice/plan#create) | App Service planı oluşturur. |
| [az functionapp oluşturma](https://docs.microsoft.com/cli/azure/appservice/web#delete) | Bir Azure işlev uygulaması oluşturur. |
| [az appservice web kaynak denetimi yapılandırma](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | Bir işlev uygulaması Git veya Mercurial deposu ile ilişkilendirir. |

## <a name="next-steps"></a>Sonraki adımlar

Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek Azure işlevleri CLI kod örnekleri bulunabilir [Azure işlevleri belgelerine](../functions-cli-samples.md).
