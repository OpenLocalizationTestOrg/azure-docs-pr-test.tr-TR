---
title: "aaaAzure CLI komut dosyası örneği - toplu havuzlarını yönetme | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - Batch havuzlarında yönetme"
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
ms.openlocfilehash: 6c9ca9515565aff42752231a080943be8e4c810b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a>Azure Batch havuzları Azure CLI ile yönetme

Bu komut dosyası hello hello Azure CLI toocreate kullanılabilen araçların bazıları gösterir ve hello Azure Batch hizmeti işlem düğümlerine havuzlarını Yönet.

> [!NOTE]
> Bu örnek komutlarda Hello Azure sanal makine oluşturun. VM'ler çalıştıran ücretleri tooyour hesabı tahakkuk. toominimize bu ücretlerden silin hello VM'ler çalışan hello örnek bitirdiğinizde. Bkz: [havuzları temiz](#clean-up-pools).

Batch havuzları, bulut Hizmetleri Yapılandırması (yalnızca Windows) veya bir sanal makine yapılandırma (Windows ve Linux) iki şekilde yapılandırılabilir. Aşağıdaki örnek komut Hello nasıl toocreate hem yapılandırmalarla havuzları gösterir.

## <a name="prerequisites"></a>Ön koşullar

- Yükleme hello hello sağlanan hello yönergeleri kullanarak Azure CLI [Azure CLI Yükleme Kılavuzu'na](https://docs.microsoft.com/cli/azure/install-azure-cli)zaten yapmadıysanız,.
- Zaten yoksa, bir toplu işlem hesabı oluşturun. Bkz: [hello Azure CLI ile bir toplu işlem hesabı oluşturun](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) bir hesap oluşturan bir örnek komut dosyası için.
- Henüz yapmadıysanız, bir uygulama toorun başlangıç görevden yapılandırın. Bkz: [uygulamaları tooAzure Azure CLI ile toplu ekleme](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) bir uygulama oluşturur ve bir uygulama paketi tooAzure yükler bir örnek komut dosyası.

## <a name="pool-with-cloud-service-configuration-sample-script"></a>Bulut hizmeti yapılandırma örnek komut dosyası havuzuyla

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]

## <a name="pool-with-virtual-machine-configuration-sample-script"></a>Sanal makine yapılandırma örnek betiği havuzuyla

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]

## <a name="clean-up-pools"></a>Havuzları Temizle

Örnek betik yukarıdaki hello çalıştırdıktan sonra komutu toodelete hello havuzları aşağıdaki hello çalıştırın.
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları toocreate aşağıdaki hello kullanır ve Batch havuzları arabirimidir.
Her komut hello tablosundaki toocommand özgü belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az toplu işlem hesabı oturum açma](https://docs.microsoft.com/cli/azure/batch/account#login) | Toplu işlem hesabı karşı kimlik doğrulaması.  |
| [az toplu uygulama Özet listesi](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | Merhaba toplu işlem hesabı Hello kullanılabilir uygulamaları listeleyin.  |
| [az batch havuzu oluşturma](https://docs.microsoft.com/cli/azure/batch/pool#create) | Sanal makineleri havuzu oluşturun.  |
| [az batch havuzu ayarlama](https://docs.microsoft.com/cli/azure/batch/pool#set) | Bir havuz özelliklerini güncelleştirir.  |
| [az batch havuzu düğüm Aracısı SKU listesi](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | Liste kullanılabilir düğüm Aracısı SKU'ları ve görüntü bilgileri.  |
| [az batch havuzu yeniden boyutlandırma](https://docs.microsoft.com/cli/azure/batch/pool#resize) | Yeniden boyutlandırma hello sayısı, sanal makineleri hello çalışan havuzu belirtilmiş.  |
| [az batch havuzu Göster](https://docs.microsoft.com/cli/azure/batch/pool#show) | Bir havuzu Hello özelliklerini görüntüler.  |
| [az batch havuzu silme](https://docs.microsoft.com/cli/azure/batch/pool#delete) | Belirtilen hello silme havuzu.  |
| [az batch havuzu otomatik ölçeklendirme etkinleştir](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | Bir havuz üzerinde otomatik ölçeklendirmeyi etkinleştirmek ve bir formül uygulayın.  |
| [az batch havuzu otomatik ölçeklendirme devre dışı bırak](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | Bir havuz üzerinde otomatik ölçeklendirme devre dışı bırakın.  |
| [az toplu işlem düğüm listesi](https://docs.microsoft.com/cli/azure/batch/node#list) | Tüm liste hello hello işlem düğümünde belirtilen havuzu.  |
| [az toplu düğümü yeniden başlatma](https://docs.microsoft.com/cli/azure/batch/node#reboot) | Merhaba belirtilen işlem düğümü yeniden başlatın.  |
| [az toplu düğümü Sil](https://docs.microsoft.com/cli/azure/batch/node#delete) | Delete listelenen hello hello düğümlerden havuzu belirtilmiş.  |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek toplu CLI kod örnekleri hello bulunabilir [Azure Batch CLI belgelerine](../batch-cli-samples.md).

