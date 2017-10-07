---
title: "aaaView ve bir sanal makinenin Azure Resource Manager şablonu kullanma | Microsoft Docs"
description: "Nasıl toouse hello Azure Resource Manager şablonu kullanarak bir sanal makine toocreate diğer VM'ler öğrenin"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a759d9ce-655c-4ac6-8834-cb29dd7d30dd
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: tarcher
ms.openlocfilehash: b79f7eb4171793681a0b654e6e72a83191c76bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-virtual-machines-azure-resource-manager-template"></a>Bir sanal makinenin Azure Resource Manager şablonu kullanın

Oluştururken bir sanal makine (VM) DevTest Labs'de hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), hello VM kaydetmeden önce hello Azure Resource Manager şablonu görüntüleyebilirsiniz. Merhaba şablonu sonra temel toocreate daha kullanılabilir olan Laboratuvar VM'ler hello aynı ayarları.

Nasıl tooview hello Resource Manager şablonu bir VM oluşturma ne zaman ve nasıl bu makalede toodeploy, sonraki tooautomate oluşturulmasını hello aynı VM.

## <a name="multi-vm-vs-single-vm-resource-manager-templates"></a>Çoklu VM tek VM Resource Manager şablonları karşılaştırması
Resource Manager şablonu kullanarak DevTest Labs'de toocreate VM'ler iki yolu vardır: Merhaba Microsoft.DevTestLab/labs/virtualmachines kaynak sağlamak veya hello Microsoft.Commpute/virtualmachines kaynak sağlanamadı. Her farklı senaryolarda kullanılır ve farklı izinleri gerektirir.

- (Merhaba "kaynak" özelliği hello şablonunda bildirilen gibi) bir Microsoft.DevTestLab/labs/virtualmachines kaynak türünü kullanan resource Manager şablonları tek tek Laboratuvar VM'ler sağlayabilirsiniz. Her VM sonra hello DevTest Labs sanal makineler listesindeki tek bir öğe olarak görüntülenir:

   ![Sanal makineleri tek öğeleri hello DevTest Labs sanal makineler listesi olarak listesi](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-item.png)

   Bu tür bir Resource Manager şablonu hello Azure PowerShell komutu sağlanabilir **New-AzureRmResourceGroupDeployment** veya hello Azure CLI komutu aracılığıyla **az grup dağıtımı oluşturmak** . Bir DevTest Labs kullanıcı rolünün atandığı kullanıcılar hello dağıtım gerçekleştiremezler yönetici izinleri gerektirir. 

- Bir Microsoft.Compute/virtualmachines kaynak türünü kullanan resource Manager şablonları hello DevTest Labs sanal makineler listesi tek bir ortamda olarak birden çok VM sağlayabilirsiniz:

   ![Sanal makineleri tek öğeleri hello DevTest Labs sanal makineler listesi olarak listesi](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-environment.png)

   Aynı ortama birlikte yönetilebilir hello ve Paylaşım VM'ler aynı yaşam döngüsü hello. Bir DevTest Labs kullanıcı rolünün atandığı kullanıcılar hello yönetici hello Laboratuvar bu şekilde yapılandırılan olduğu sürece bu şablonları kullanarak ortamları oluşturabilirsiniz.

Bu makalenin sonraki bölümlerinde Hello Mirosoft.DevTestLab/labs/virtualmachines kullanan Resource Manager şablonları açıklanır. Bu Laboratuvar admins tooautomate Laboratuvar VM oluşturma (örneğin, claimable VM'ler) veya altın görüntü oluşturma (örneğin, görüntü fabrikada) tarafından kullanılır.

[En iyi uygulamalar Azure Resource Manager şablonları oluşturmak için](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) birçok kılavuzları ve önerileri toohelp sunar güvenilir ve kolay toouse olan Azure Resource Manager şablonları oluşturun.

## <a name="view-and-save-a-virtual-machines-resource-manager-template"></a>Görüntüleme ve bir sanal makinenin Resource Manager şablonu kaydetme
1. Merhaba adımları izleyin [bir laboratuar ortamında ilk VM oluşturma](devtest-lab-create-first-vm.md) toobegin bir sanal makine oluşturma.
1. Sanal makineniz için hello gerekli bilgileri girin ve bu VM için istediğiniz herhangi bir yapı ekleyin.
1. Merhaba yapılandırma ayarları penceresi Hello altındaki seçin **görünüm ARM şablonu**.

   ![Görünüm ARM şablonu düğmesi](./media/devtest-lab-use-arm-template/devtestlab-lab-view-rm-template.png)
1. Kopyalayın ve hello Resource Manager şablonu toouse kaydedin sonraki toocreate başka bir sanal makine.

   ![Resource manager şablonu toosave daha sonra kullanmak için](./media/devtest-lab-use-arm-template/devtestlab-lab-copy-rm-template.png)

Merhaba Resource Manager şablonu kaydettikten sonra kullanmadan önce hello parametreleri hello şablon bölümünü güncelleştirmeniz gerekir. Merhaba gerçek Resource Manager şablonu dışında hello parametreleri yalnızca özelleştirir parameter.json oluşturabilirsiniz. 

![Bir JSON dosyası kullanarak parametre özelleştirme](./media/devtest-lab-use-arm-template/devtestlab-lab-custom-params.png)

## <a name="deploy-a-resource-manager-template-toocreate-a-vm"></a>Resource Manager şablonu toocreate VM dağıtma
Resource Manager şablonu kaydedilir ve gereksinimlerinize göre özelleştirilmiş sonra tooautomate VM oluşturmayı kullanabilirsiniz. [Resource Manager şablonları ve Azure PowerShell ile kaynakları dağıtmak](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy) açıklar nasıl toouse Azure PowerShell'i Resource Manager şablonları toodeploy ile kaynakları tooAzure. [Resource Manager şablonları ve Azure CLI kaynaklarla dağıtmak](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy-cli) açıklar nasıl Resource Manager şablonları toodeploy ile Azure CLI toouse kaynakları tooAzure.

> [!NOTE]
> Yalnızca Laboratuvar sahip izinlerine sahip bir kullanıcı Azure PowerShell kullanarak sanal makineleri bir Resource Manager şablonu oluşturabilirsiniz. Resource Manager şablonu kullanarak tooautomate VM oluşturmak istiyorsanız ve yalnızca kullanıcı izinlerine sahip hello kullanabilirsiniz [ **az Laboratuvar vm oluşturma** hello CLI komutunu](https://docs.microsoft.com/cli/azure/lab/vm#create).

### <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[Resource Manager şablonları ile çoklu VM ortamları oluşturma](devtest-lab-create-environment-from-arm.md).
* DevTest Labs Otomasyon için daha fazla hızlı başlangıç Resource Manager şablonları hello keşfedin [ortak DevTest Labs GitHub deposuna](https://github.com/Azure/azure-quickstart-templates).
