---
title: "aaaAzure CLI komut dosyası örneği - sunucusuz yürütme için bir işlev uygulaması oluşturma | Microsoft Docs"
description: "Azure CLI betik örnek - sunucusuz yürütme için bir işlev uygulaması oluşturma"
services: functions
documentationcenter: functions
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0e221db6-ee2d-4e16-9bf6-a456cd05b6e7
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 04/11/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 7ec872b642e50827896a73a9e43bcc87233e15c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-for-serverless-execution"></a>Sunucusuz yürütme için bir işlev uygulaması oluşturma

Bu örnek betik işlevlerinizi için bir kapsayıcı olan bir Azure işlevi uygulaması oluşturur. Merhaba işlev uygulaması hello kullanılarak oluşturulan [tüketim planı](../functions-scale.md#consumption-plan), olay denetimli sunucusuz iş yükleri için ideal olduğu.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Örnek komut dosyası

Bir Azure işlevi uygulamasına hello'ı kullanarak bu betiği oluşturur [tüketim planı](../functions-scale.md#consumption-plan).

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "Create an Azure Function on a consumption plan")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Komut dosyası açıklaması

Her komut hello tablosundaki toocommand belirli belgeleri bağlar. Bu komut dosyası komutları aşağıdaki hello kullanır:

| Komut | Notlar |
|---|---|
| [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az depolama hesabı oluşturma](/cli/azure/storage/account#create) | Bir Azure Storage hesabı oluşturur. |
| [az functionapp oluşturma](https://docs.microsoft.com/cli/azure/functionapp#create) | Bir Azure işlevi oluşturur. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek Azure işlevleri CLI kod örnekleri hello bulunabilir [Azure işlevleri belgelerine](../functions-cli-samples.md).
