---
title: "aaaAzure CLI komut dosyası örneği - eşleme özel etki alanı tooa işlev uygulaması | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - harita Azure özel etki alanı tooa işlevi uygulamada."
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
ms.openlocfilehash: c7cb0a3e132b491250623b945aecf6aea4f57c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="map-a-custom-domain-tooa-function-app"></a>Özel etki alanı tooa işlev uygulaması eşleme

Bu örnek komut dosyası ile ilgili kaynaklar bir işlev uygulaması oluşturur ve ardından eşler `www.<yourdomain>` tooit. toomap tooa özel etki alanı işlev uygulamanızı tüketim planı içinde değil, bir uygulama hizmeti planındaki oluşturulması gerekir. Azure işlevleri yalnızca destekleyen bir A kaydı kullanarak özel bir etki alanı eşleme.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 


## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain tooa function app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az depolama hesabı oluşturma](https://docs.microsoft.com/cli/azure/storage/account#create) | Merhaba işlevi uygulama tarafından gerekli bir depolama hesabı oluşturur. |
| [az uygulama hizmeti planı oluşturma](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Bir uygulama hizmeti planı gerekli toomap özel bir etki alanı oluşturur. |
| [az functionapp oluşturma]() | Bir işlev uygulaması oluşturur. |
| [az appservice web yapılandırma ana bilgisayar adı ekleyin](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | Özel etki alanı tooa işlev uygulaması eşler. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek işlevler CLI kod örnekleri hello bulunabilir [Azure işlevleri belgelerine]().
