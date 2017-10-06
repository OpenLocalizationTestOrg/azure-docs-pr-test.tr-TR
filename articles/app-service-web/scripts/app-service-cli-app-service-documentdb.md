---
title: "aaaAzure CLI komut dosyası örneği - web uygulama tooCosmos DB bağlanma | Microsoft Docs"
description: "Azure CLI betik örnek - web uygulama tooCosmos DB Bağlan"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bbbdbc42-efb5-4b4f-8ba6-c03c9d16a7ea
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 1f2123378b9d5812fa793730f7fa5a5bc9ab63c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-toocosmos-db"></a>Bir web uygulaması tooCosmos DB Bağlan

Bu senaryoda, nasıl toocreate Azure Cosmos DB hesabınız ve Azure web uygulaması öğreneceksiniz. Uygulama ayarları kullanarak hello Cosmos DB toohello web uygulaması bağlantı içerir.


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos DB")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları toocreate bir kaynak grubu, web uygulaması, Cosmos DB ve tüm ilgili kaynaklar aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand belirli belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az uygulama hizmeti planı oluşturma](https://docs.microsoft.com/cli/azure/appservice/plan#create) | App Service planı oluşturur. Bu, Azure web uygulamanız için bir sunucu grubu gibidir. |
| [az webapp oluşturma](https://docs.microsoft.com/cli/azure/webapp#create) | Azure web uygulaması oluşturur. |
| [az cosmosdb oluşturma](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#create) | Cosmos DB hesabı oluşturur. Merhaba veri depolanacağı budur. |
| [az cosmosdb listesi anahtarlar](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#list-keys) | Belirtilen Cosmos DB hesaba hello hello erişim anahtarlarını listeler. |
| [az webapp config appsettings ayarlama](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | Oluşturur veya bir Azure web uygulaması için bir uygulama ayarı güncelleştirir. Uygulama ayarları uygulamanız için ortam değişkenleri olarak sunulur. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek uygulama hizmeti CLI kod örnekleri hello bulunabilir [Azure App Service belgeleri](../app-service-cli-samples.md).
