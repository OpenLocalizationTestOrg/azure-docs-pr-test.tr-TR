---
title: "Azure CLI betik örnek - Batch hesabı oluşturun. | Microsoft Docs"
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
ms.openlocfilehash: 698978fd717091c49a1375e222f46f4325431223
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-batch-account-with-the-azure-cli"></a>Azure CLI ile bir toplu işlem hesabı oluşturun

Bu komut dosyasını bir Azure Batch hesabı oluşturur ve hesabın nasıl çeşitli özellikleri sorgulanan ve güncelleştirilmiş gösterir.

## <a name="prerequisites"></a>Ön koşullar

Sağlanan yönergeleri kullanarak Azure CLI yükleme [Azure CLI Yükleme Kılavuzu'na](https://docs.microsoft.com/cli/azure/install-azure-cli)zaten yapmadıysanız,.

## <a name="batch-account-sample-script"></a>Toplu işlem hesabı örnek komut dosyası

Varsayılan olarak, bir toplu işlem hesabı oluşturduğunuzda, işlem düğümlerini Batch hizmeti tarafından dahili olarak atanır. Hesap ya da paylaşılan anahtar kimlik bilgileri veya bir Azure Active Dirctory belirteci aracılığıyla doğrulanabilir ve ayrılmış işlem düğümleri ayrı çekirdek kotası tabi olacaktır.

[!code-azurecli[Ana](../../../cli_scripts/batch/create-account/create-account.sh "hesabı oluştur")]

## <a name="batch-account-using-user-subscription-sample-script"></a>Toplu işlem hesabı kullanıcı abonelik örnek komut dosyası kullanma

Toplu işlem düğümlerinden kendi Azure aboneliği oluşturmak için tercih edebilirsiniz.
Allocate hesapları işlem düğümlerin aboneliğinizi içine bir Azure Active Directory token kimlik doğrulaması gerekir ve ayrılan işlem düğümleri abonelik kotanızı sayılacaktır. Bu modda bir hesap oluşturmak için bir anahtar kasası başvuru hesabı oluştururken belirtmeniz gerekir.

[!code-azurecli[Ana](../../../cli_scripts/batch/create-account/create-account-user-subscription.sh  "kullanıcı aboneliği kullanarak hesabı oluştur")]

## <a name="clean-up-deployment"></a>Dağıtımı temizleme

Yukarıdaki örnek betikler birini çalıştırdıktan sonra kaynak grubunu kaldırmak için aşağıdaki komutu çalıştırın ve ilişkili tüm kaynaklar (toplu işlem hesabı, Azure depolama hesapları ve Azure anahtar kasalarını dahil).

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Komut dosyası açıklaması

Bu komut, bir kaynak grubu, toplu işlem hesabı ve tüm ilgili kaynaklar oluşturmak için aşağıdaki komutları kullanır. Komut özgü belgelere Tablo bağlantıları her komut.

| Komut | Notlar |
|---|---|
| [az grubu oluşturma](https://docs.microsoft.com/cli/azure/group#create) | Tüm kaynaklar depolandığı bir kaynak grubu oluşturur. |
| [az toplu işlem hesabı oluşturun](https://docs.microsoft.com/cli/azure/batch/account#create) | Toplu işlem hesabı oluşturur.  |
| [az toplu işlem hesabı ayarlama](https://docs.microsoft.com/cli/azure/batch/account#set) | Batch hesabı özelliklerini güncelleştirir.  |
| [az toplu işlem hesabı Göster](https://docs.microsoft.com/cli/azure/batch/account#show) | Belirtilen toplu işlem hesabı ayrıntılarını alır.  |
| [az batch hesabı anahtarları listesi](https://docs.microsoft.com/cli/azure/batch/account/keys#list) | Belirtilen toplu işlem hesabı erişim anahtarları alır.  |
| [az toplu işlem hesabı oturum açma](https://docs.microsoft.com/cli/azure/batch/account#login) | Daha fazla CLI etkileşim için belirtilen toplu işlem hesabı karşı doğrular.  |
| [az depolama hesabı oluşturma](https://docs.microsoft.com/cli/azure/storage/account#create) | Bir depolama hesabı oluşturur. |
| [az keyvault oluşturma](https://docs.microsoft.com/cli/azure/keyvault#create) | Bir anahtar kasası oluşturur. |
| [az keyvault-ilkesini ayarlama](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | Belirtilen anahtar kasası güvenlik ilkesini güncelleştirin. |
| [az grubu Sil](https://docs.microsoft.com/cli/azure/group#delete) | Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler. |

## <a name="next-steps"></a>Sonraki adımlar

Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).

Ek toplu CLI kod örnekleri bulunabilir [Azure Batch CLI belgelerine](../batch-cli-samples.md).
