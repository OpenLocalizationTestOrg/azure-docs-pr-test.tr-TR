---
title: "aaaAzure CLI komut dosyası örneği - Batch hesabı oluşturma | Microsoft Docs"
description: "Azure CLI betik örnek - Batch hesabı oluşturma"
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
ms.openlocfilehash: 62b640eebbafdd1081822a638fd0720121ef067a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-batch-account-with-hello-azure-cli"></a>Hello Azure CLI ile bir toplu işlem hesabı oluşturun

Bu komut dosyasını bir Azure Batch hesabı oluşturur ve hello hesabının nasıl çeşitli özelliklerini sorgulanan ve güncelleştirilmiş gösterir.

## <a name="prerequisites"></a>Ön koşullar

Yükleme hello hello sağlanan hello yönergeleri kullanarak Azure CLI [Azure CLI Yükleme Kılavuzu'na](https://docs.microsoft.com/cli/azure/install-azure-cli)zaten yapmadıysanız,.

## <a name="batch-account-sample-script"></a>Toplu işlem hesabı örnek komut dosyası

Varsayılan olarak, bir toplu işlem hesabı oluşturduğunuzda, işlem düğümlerini hello Batch hizmeti tarafından dahili olarak atanır. Ayrılmış işlem düğümleri konu tooa ayrı çekirdek kotası olacaktır ve hello hesabı ya da paylaşılan anahtar kimlik bilgileri veya bir Azure Active Dirctory belirteci aracılığıyla doğrulanabilir.

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account.sh "Create Account")]

## <a name="batch-account-using-user-subscription-sample-script"></a>Toplu işlem hesabı kullanıcı abonelik örnek komut dosyası kullanma

Ayrıca seçebilirsiniz toohave toplu işlem düğümlerinden kendi Azure aboneliği oluşturun.
Allocate hesapları işlem düğümlerin aboneliğinizi içine bir Azure Active Directory token kimlik doğrulaması gerekir ve ayrılan hello işlem düğümleri abonelik kotanızı sayılacaktır. toocreate hesabınız bu modda, bir anahtar kasası başvuru hello hesabını oluştururken belirtmeniz gerekir.

[!code-azurecli[main](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "Create Account using User Subscription")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme

Yukarıdaki örnek betikler hello birini çalıştırdıktan sonra komutu tooremove aşağıdaki hello kaynak grubu ve tüm ilgili kaynaklar (toplu işlem hesabı, Azure depolama hesapları ve Azure anahtar kasalarını dahil) çalıştırın.

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut dosyası komutları toocreate bir kaynak grubu, toplu işlem hesabı ve tüm ilişkili kaynakları aşağıdaki hello kullanır. Her komut hello tablosundaki toocommand özgü belgeleri bağlar.

| Komut | Notlar |
|---|---|
| [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az toplu işlem hesabı oluşturun](https://docs.microsoft.com/cli/azure/batch/account#create) | Merhaba toplu işlem hesabı oluşturur.  |
| [az toplu işlem hesabı ayarlama](https://docs.microsoft.com/cli/azure/batch/account#set) | Merhaba Batch hesabı özelliklerini güncelleştirir.  |
| [az toplu işlem hesabı Göster](https://docs.microsoft.com/cli/azure/batch/account#show) | Belirtilen toplu hesaba hello ayrıntılarını alır.  |
| [az batch hesabı anahtarları listesi](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | Merhaba alır hello erişim anahtarlarını toplu işlem hesabı belirtildi.  |
| [az toplu işlem hesabı oturum açma](https://docs.microsoft.com/cli/azure/batch/account#login) | Belirtilen hello karşı doğrular Batch hesabı başka CLI etkileşim için.  |
| [az depolama hesabı oluşturma](https://docs.microsoft.com/cli/azure/storage/account#create) | Bir depolama hesabı oluşturur. |
| [az keyvault oluşturma](https://docs.microsoft.com/cli/azure/keyvault#create) | Bir anahtar kasası oluşturur. |
| [az keyvault-ilkesini ayarlama](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | Belirtilen anahtar kasası hello Hello güvenlik ilkesini güncelleştirin. |
| [az grubu Sil](https://docs.microsoft.com/cli/azure/group#delete) | Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler. |

## <a name="next-steps"></a>Sonraki adımlar

Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek toplu CLI kod örnekleri hello bulunabilir [Azure Batch CLI belgelerine](../batch-cli-samples.md).
