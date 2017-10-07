---
title: "aaaAzure CLI komut dosyası örneği - toplu işleminde bir uygulama ekleyin | Microsoft Docs"
description: "Azure CLI toplu işleminde bir uygulama eklemek örnek - komut dosyası"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: cb33b3a7b30610011b19954a987995cc5f0257c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-applications-tooazure-batch-with-azure-cli"></a>Uygulamaları tooAzure Azure CLI ile toplu ekleme

Bu komut dosyası gösterilmektedir nasıl tooset bir Azure Batch havuzu ya da görev ile kullanmak için bir uygulama ayarlama. bir uygulama yukarı tooset paketini bir .zip dosyasına tüm bağımlılıkları ile birlikte, yürütülebilir. İçinde bu örnek hello yürütülebilir zip dosyası olarak adlandırılır ' my-uygulama-exe.zip'.

## <a name="prerequisites"></a>Ön koşullar

- Yükleme hello hello sağlanan hello yönergeleri kullanarak Azure CLI [Azure CLI Yükleme Kılavuzu'na](https://docs.microsoft.com/cli/azure/install-azure-cli)zaten yapmadıysanız,.
- Zaten yoksa, bir toplu işlem hesabı oluşturun. Bkz: [hello Azure CLI ile bir toplu işlem hesabı oluşturun](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) bir hesap oluşturan bir örnek komut dosyası için.

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli[main](../../../cli_scripts/batch/add-application/add-application.sh "Add Application")]

## <a name="clean-up-application"></a>Uygulamayı oluşturan Temizle

Örnek betik yukarıdaki hello çalıştırdıktan sonra aşağıdaki komutları tooremove hello uygulama ve onun karşıya yüklenen uygulama paketleri çalıştırın.

```azurecli
az batch application package delete -g myresourcegroup -n mybatchaccount --application-id myapp --version 1.0 --yes
az batch application delete -g myresourcegroup -n mybatchaccount --application-id myapp --yes
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası, bir uygulama ve bir uygulama paketini karşıya yükleme komutları toocreate aşağıdaki hello kullanır.
Her komut hello tablosundaki toocommand özgü belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az batch uygulaması oluşturma](https://docs.microsoft.com/cli/azure/batch/application#create) | Bir uygulama oluşturur.  |
| [az toplu uygulama ayarlama](https://docs.microsoft.com/cli/azure/batch/application#set) | Bir uygulamanın özelliklerini güncelleştirir.  |
| [az toplu uygulama paketi oluşturma](https://docs.microsoft.com/cli/azure/batch/application/package#create) | Belirtilen bir uygulama paketi toohello ekler uygulama.  |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek toplu CLI kod örnekleri hello bulunabilir [Azure Batch CLI belgelerine](../batch-cli-samples.md).
