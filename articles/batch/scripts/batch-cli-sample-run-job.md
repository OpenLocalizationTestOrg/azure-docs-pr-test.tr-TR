---
title: "aaaAzure CLI komut dosyası örneği ile toplu işi - | Microsoft Docs"
description: "Azure CLI komut dosyası örneği ile toplu işi-"
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
ms.openlocfilehash: f73a7cb341e550fd1c92f92201e20b27fa20d238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a>Azure CLI ile Azure batch işleri çalıştırma

Bu komut dosyası toplu iş oluşturur ve bir dizi görevleri toohello iş ekler. Ayrıca gösterir nasıl toomonitor bir işi ve görevleri. Son olarak, nasıl tooquery hello Batch hizmeti hello işin görevler hakkında bilgi için verimli bir şekilde gösterir.

## <a name="prerequisites"></a>Ön koşullar

- Yükleme hello hello sağlanan hello yönergeleri kullanarak Azure CLI [Azure CLI Yükleme Kılavuzu'na](https://docs.microsoft.com/cli/azure/install-azure-cli)zaten yapmadıysanız,.
- Zaten yoksa, bir toplu işlem hesabı oluşturun. Bkz: [hello Azure CLI ile bir toplu işlem hesabı oluşturun](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) bir hesap oluşturan bir örnek komut dosyası için.
- Henüz yapmadıysanız, bir uygulama toorun başlangıç görevden yapılandırın. Bkz: [uygulamaları tooAzure Azure CLI ile toplu ekleme](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) bir uygulama oluşturur ve bir uygulama paketi tooAzure yükler bir örnek komut dosyası.
- Hangi hello üzerinde iş çalıştırılır havuzunu yapılandırın. Bkz: [Azure CLI ile yönetme Azure Batch havuzları](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) bir bulut hizmet yapılandırması veya bir sanal makine yapılandırması ile bir havuz oluşturur bir örnek komut dosyası için.

## <a name="sample-script"></a>Örnek komut dosyası

[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]

## <a name="clean-up-job"></a>İş temizleme

Örnek betik yukarıdaki hello çalıştırdıktan sonra iş ve tüm görevleri komutu tooremove aşağıdaki hello çalıştırın. Merhaba havuzu ayrı ayrı silinmiş toobe gerektiğini unutmayın. Bkz: [Azure CLI ile yönetme Azure Batch havuzları](./batch-cli-sample-manage-pool.md) oluşturma ve havuzların silinmesi hakkında daha fazla bilgi.

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası, bir toplu işi ve görevleri komutları toocreate aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand özgü belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az toplu işlem hesabı oturum açma](https://docs.microsoft.com/cli/azure/batch/account#login) | Toplu işlem hesabı karşı kimlik doğrulaması.  |
| [az toplu işlem işi oluşturma](https://docs.microsoft.com/cli/azure/batch/job#create) | Bir toplu işi oluşturur.  |
| [az toplu işi ayarlama](https://docs.microsoft.com/cli/azure/batch/job#set) | Toplu iş özelliklerini güncelleştirir.  |
| [az toplu işi Göster](https://docs.microsoft.com/cli/azure/batch/job#show) | Belirtilen toplu iş ayrıntılarını alır.  |
| [az toplu görev oluşturma](https://docs.microsoft.com/cli/azure/batch/task#create) | Toplu Görev toohello belirtilen ekler.  |
| [az toplu görev Göster](https://docs.microsoft.com/cli/azure/batch/task#show) | Merhaba görevden alır hello ayrıntılarını toplu işlem belirtildi.  |
| [az toplu görev listesi](https://docs.microsoft.com/cli/azure/batch/task#list) | Merhaba belirtilen işlemle ilişkili hello görevleri listeler.  |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek toplu CLI kod örnekleri hello bulunabilir [Azure Batch CLI belgelerine](../batch-cli-samples.md).
