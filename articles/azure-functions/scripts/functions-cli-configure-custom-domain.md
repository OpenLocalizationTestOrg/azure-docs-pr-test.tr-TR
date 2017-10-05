---
title: "Azure CLI komut dosyası örneği - eşlemesi bir işlev uygulaması için özel bir etki alanı | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - eşlemesi bir işlev uygulaması Azure için özel bir etki alanı."
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d127e347-7581-47d7-b289-e0f51f2fbfbc
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 6fcea6d32f9dd25b0fafb4f895f60d8320ac9df8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="map-a-custom-domain-to-a-function-app"></a>Eşlemesi bir işlev uygulaması için özel bir etki alanı

Bu örnek komut dosyası ile ilgili kaynaklar bir işlev uygulaması oluşturur ve ardından eşler `www.<yourdomain>` ona. Özel bir etki alanına eşlemek için işlevi uygulamanıza bir uygulama hizmeti planı yer alan ve tüketim planı oluşturulması gerekir. Azure işlevleri yalnızca destekleyen bir A kaydı kullanarak özel bir etki alanı eşleme.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir. Sürümü bulmak için `az --version` komutunu çalıştırın. Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 


## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli-interactive[Ana](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "bir işlev uygulaması için özel bir etki alanı eşleme")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyasını aşağıdaki komutları kullanır. Komut belirli belgeleri tablo bağlanan her komut.

| Komut | Notlar |
|---|---|
| [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az depolama hesabı oluşturma](https://docs.microsoft.com/cli/azure/storage/account#create) | İşlev uygulaması tarafından gerekli bir depolama hesabı oluşturur. |
| [az uygulama hizmeti planı oluşturma](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Özel etki alanını eşlemek için gerekli bir uygulama hizmeti planı oluşturur. |
| [az functionapp oluşturma]() | Bir işlev uygulaması oluşturur. |
| [az appservice web yapılandırma ana bilgisayar adı ekleyin](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | Özel bir etki alanı için bir işlev uygulaması eşler. |

## <a name="next-steps"></a>Sonraki adımlar

Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek işlevler CLI kod örnekleri bulunabilir [Azure işlevleri belgelerine]().
