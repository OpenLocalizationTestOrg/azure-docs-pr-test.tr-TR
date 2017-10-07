---
title: "aaaCreate tooan Azure Cosmos DB bağlanan bir Azure işlevi | Microsoft Docs"
description: "Azure CLI betik örnek - tooan Azure Cosmos DB bağlanan bir Azure işlevi oluşturma"
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
ms.openlocfilehash: 0fbc1ebec2dfd480e0cf3ca64f9febcec8af9a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-that-connects-tooan-azure-cosmos-db"></a>Tooan Azure Cosmos DB bağlanan bir Azure işlevi oluşturma

Bu örnek betik, bir Azure işlevi uygulaması oluşturur ve tooan Azure Cosmos DB veritabanı bağlanır.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Örnek komut dosyası

Bu örnek bir Azure işlevi uygulamasını oluşturur ve bir Cosmos DB endpoint ve erişim anahtarı tooapp ayarları ekler.

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Create an Azure Function that connects tooan Azure Cosmos DB")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme

Hello komut dosyası örneği çalıştırdıktan sonra hello izleyin komutu kullanılan tooremove hello kaynak grubu olabilir ve tüm kaynakları ilgili.

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az oturum açma](https://docs.microsoft.com/cli/azure/#login) | Oturum açma tooAzure. |
| [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) | Konumu ile kaynak grubu oluştur |
| [az depolama hesabı oluşturma](https://docs.microsoft.com/cli/azure/storage/account) | Depolama hesabı oluşturma |
| [az functionapp oluşturma](https://docs.microsoft.com/cli/azure/functionapp#create) | Yeni bir işlev uygulaması oluşturma |
| [az documentdb oluşturma](https://docs.microsoft.com/cli/azure/documentdb#create) | Documentdb veritabanı oluşturma |
| [az grubu Sil](https://docs.microsoft.com/cli/azure/group#delete) | Temizleme |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek Azure işlevleri CLI kod örnekleri hello bulunabilir [Azure işlevleri belgelerine](../functions-cli-samples.md).




