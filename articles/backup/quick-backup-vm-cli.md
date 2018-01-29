---
title: "Azure Hızlı Başlangıç - Azure CLI ile sanal makine yedekleme | Microsoft Docs"
description: "Azure CLI ile sanal makinelerinizi nasıl yedekleyeceğinizi öğrenin"
services: backup, virtual-machines-linux
documentationcenter: virtual-machines
author: markgalioto
manager: carmonm
editor: 
tags: azure-resource-manager, virtual-machine-backup
ms.assetid: 
ms.service: backup, virtual-machines-linux
ms.devlang: azurecli
ms.topic: quickstart
ms.tgt_pltfrm: vm-linux
ms.workload: storage-backup-recovery
ms.date: 1/12/2018
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 675ebb56496846c5d00ecb5af0e4a69c092b74c6
ms.sourcegitcommit: e19f6a1709b0fe0f898386118fbef858d430e19d
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/13/2018
---
# <a name="back-up-a-virtual-machine-in-azure-with-the-cli"></a>CLI ile Azure'daki bir sanal makineyi yedekleme
Azure CLI, komut satırından veya betik içindeki Azure kaynaklarını oluşturmak ve yönetmek için kullanılır. Düzenli aralıklarla yedekleme yaparak verilerinizi koruyabilirsiniz. Azure Backup, coğrafi olarak yedekli kurtarma kasalarında saklanabilecek kurtarma noktaları oluşturur. Bu makalede Azure CLI ile Azure'daki bir sanal makinenin nasıl yedekleneceği anlatılmaktadır. Bu adımları [Azure PowerShell](quick-backup-vm-powershell.md) veya [Azure portalı](quick-backup-vm-portal.md) ile de gerçekleştirebilirsiniz.

Bu hızlı başlangıç belgesi var olan bir Azure sanal makinesinde yedeklemeyi etkinleştirir. Bir sanal makine oluşturmanız gerekiyorsa [Azure CLI ile sanal makine oluşturabilirsiniz](../virtual-machines/linux/quick-create-cli.md).

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

CLI'yı yerel ortamda yüklemek ve kullanmak için Azure CLI sürüm 2.0.18 veya üzeri çalıştırmanız gerekir. CLI sürümünü bulmak için şunu çalıştırın: `az --version`. Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme](/cli/azure/install-azure-cli). 


## <a name="create-a-recovery-services-vault"></a>Kurtarma hizmetleri kasası oluşturma
Kurtarma Hizmetleri kasası, Azure sanal makineleri gibi koruma altındaki kaynakların yedeklenen verilerini saklayan bir mantıksal kapsayıcıdır. Koruma altındaki bir kaynak için yedekleme işi çalıştığında Kurtarma Hizmetleri kasasının içinde bir kurtarma noktası oluşturulur. Daha sonra bu kurtarma noktalarından birini kullanarak verileri dilediğiniz zaman geri yükleyebilirsiniz.

[az backup vault create](https://docs.microsoft.com/cli/azure/backup/vault#az_backup_vault_create) komutuyla bir Kurtarma Hizmetleri kasası oluşturun. Korumak istediğiniz sanal makineyle aynı kaynak grubunu ve konumu belirtin. [VM hızlı başlangıç](../virtual-machines/linux/quick-create-cli.md) adımını kullandıysanız şu öğeler oluşturulmuştur:

- *myResourceGroup* adlı bir kaynak grubu,
- *myVM* adlı bir VM,
- *eastus* konumunda bulunan kaynaklar.

```azurecli-interactive 
az backup vault create --resource-group myResourceGroup \
    --name myRecoveryServicesVault \
    --location eastus
```

Varsayılan olarak Kurtarma Hizmetleri kasasında Coğrafi Olarak Yedekli depolama özelliği etkindir. Coğrafi Olarak Yedekli depolama, yedeklenen verilerinizin birincil bölgeden yüzlerce kilometre uzaktaki ikincil bir Azure bölgesinde çoğaltılmasını sağlar.


## <a name="enable-backup-for-an-azure-vm"></a>Bir Azure sanal makinesi için yedeklemeyi etkinleştirme
Bir yedekleme işinin çalışma zamanını ve kurtarma noktalarının saklama süresini tanımlamak için bir koruma ilkesi oluşturun. Varsayılan koruma ilkesi yedekleme işini her gün çalıştırır ve kurtarma noktalarını 30 gün boyunca tutar. Sanal makinenizi hızlı bir şekilde koruma altına almak için bu varsayılan ilke değerlerini kullanabilirsiniz. Bir sanal makine için yedekleme korumasını etkinleştirmek amacıyla [az backup protection enable-for-vm](https://docs.microsoft.com/cli/azure/backup/protection#az_backup_protection_enable_for_vm) komutunu kullanın. Korumaya alınacak kaynak grubunu ve sanal makineyi belirttikten sonra kullanılacak ilkeyi seçin:

```azurecli-interactive 
az backup protection enable-for-vm \
    --resource-group myResourceGroup \
    --vault-name myRecoveryServicesVault \
    --vm myVM \
    --policy-name DefaultPolicy
```


## <a name="start-a-backup-job"></a>Bir yedekleme işi başlatma
Varsayılan ilkenin işi planlanan saatte başlatmasını beklemek yerine yedekleme işini hemen başlatmak için [az backup protection backup-now](https://docs.microsoft.com/cli/azure/backup/protection#az_backup_protection_backup_now) komutunu kullanın. İlk yedekleme işi tam kurtarma noktası oluşturur. Bu ilk yedekleme sonrasında çalıştırılan tüm yedekleme işleri artımlı kurtarma noktaları oluşturur. Yalnızca son yedekleme sonrasında yapılan değişiklikleri aktardığından artımlı kurtarma noktaları depolama alanı ve süre açısından verimlilik sağlar.

Sanal makineyi yedeklemek için aşağıdaki parametreler kullanılır:

- `--container-name`, sanal makinenizin adıdır
- `--item-name`, sanal makinenizin adıdır
- `--retain-until` değeri kurtarma noktasının kullanılabilir durumda olmasını istediğiniz son tarihe ve UTC saat biçiminde (**gg-aa-yyyy**) ayarlanmalıdır

Aşağıdaki örnekte *myVM* adlı sanal makine yedeklenmekte ve kurtarma noktasının geçerlilik sonu 18 Ekim 2017 olarak ayarlanmaktadır:

```azurecli-interactive 
az backup protection backup-now \
    --resource-group myResourceGroup \
    --vault-name myRecoveryServicesVault \
    --container-name myVM \
    --item-name myVM \
    --retain-until 18-10-2017
```


## <a name="monitor-the-backup-job"></a>Yedekleme işini izleme
Yedekleme işlerinin durumunu izlemek için [az backup job list](https://docs.microsoft.com/cli/azure/backup/job#az_backup_job_list) komutunu kullanın:

```azurecli-interactive 
az backup job list \
    --resource-group myResourceGroup \
    --vault-name myRecoveryServicesVault \
    --output table
```

Çıktı, yedekleme işinin *Sürüyor* durumda olduğunu gösteren aşağıdaki örneğe benzer olacaktır:

```
Name      Operation        Status      Item Name    Start Time UTC       Duration
--------  ---------------  ----------  -----------  -------------------  --------------
a0a8e5e6  Backup           InProgress  myvm         2017-09-19T03:09:21  0:00:48.718366
fe5d0414  ConfigureBackup  Completed   myvm         2017-09-19T03:03:57  0:00:31.191807
```

Yedekleme işinin *Durum* bilgisi *Tamamlandı* olduğunda sanal makineniz Kurtarma Hizmetleri ile koruma altına alınmış ve kayıtlı tam kurtarma noktasına sahip olmuş olur.


## <a name="clean-up-deployment"></a>Dağıtımı temizleme
Artık gerekli değilse sanal makine korumasını devre dışı bırakabilir, kurtarma noktalarını ve Kurtarma Hizmetleri kasasını kaldırabilir ve ardından sanal makine kaynaklarıyla ilişkilendirilmiş kaynak grubunu silebilirsiniz. Var olan bir sanal makineyi kullandıysanız son [az group delete](/cli/azure/group?view=azure-cli-latest#az_group_delete) komutunu atlayarak kaynak grubunu ve sanal makineyi bırakabilirsiniz.

VM verilerinizi geri yüklemeyi gösteren bir Backup öğreticisini denemek istiyorsanız [Sonraki adımlar](#next-steps) bölümüne gidin. 

```azurecli-interactive 
az backup protection disable \
    --resource-group myResourceGroup \
    --vault-name myRecoveryServicesVault \
    --container-name myVM \
    --item-name myVM \
    --delete-backup-data true
az backup vault delete \
    --resource-group myResourceGroup \
    --name myRecoveryServicesVault \
az group delete --name myResourceGroup
```


## <a name="next-steps"></a>Sonraki adımlar
Bu hızlı başlangıçta bir Kurtarma Hizmetleri kasası oluşturdunuz, bir sanal makine için koruma özelliklerini etkinleştirdiniz ve ilk kurtarma noktasını oluşturdunuz. Azure Backup ve Kurtarma Hizmetleri hakkında daha fazla bilgi edinmek için öğreticilere geçin.

> [!div class="nextstepaction"]
> [Birden fazla Azure sanal makinesini yedekleme](./tutorial-backup-vm-at-scale.md)
