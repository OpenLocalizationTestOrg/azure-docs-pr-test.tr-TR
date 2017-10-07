---
title: "aaaAzure hızlı başlangıç - Windows VM CLI oluşturun | Microsoft Docs"
description: "Hızlı bir şekilde toocreate bir Windows sanal makineleri hello Azure CLI ile bilgi edinin."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 029bdecec219b12b80b958ceeedda214f1b13149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-hello-azure-cli"></a>Hello Azure CLI ile Windows sanal makine oluşturma

Hello Azure CLI kullanılan toocreate olan ve hello komut satırından veya komut dosyalarında Azure kaynaklarını yönetin. Windows Server 2016 çalışan bir sanal makine Hello Azure CLI toodeploy kullanarak bu kılavuzu ayrıntıları. Dağıtım tamamlandıktan sonra biz toohello sunucusuna bağlanmak ve IIS yükleyin.

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu hızlı başlangıç hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 


## <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

[az group create](/cli/azure/group#create) ile bir kaynak grubu oluşturun. Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır. 

Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>Sanal makine oluşturma

[az vm create](/cli/azure/vm#create) ile bir VM oluşturun. 

Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVM*. Bu örnekte *azureuser* bir yönetici kullanıcı adı ve *myPassword12* hello parola olarak. Bu değerleri toosomething uygun tooyour ortamı güncelleştirin. Bu değerleri, bir bağlantı ile Merhaba sanal makine oluştururken gereklidir.

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --admin-username azureuser --admin-password myPassword12
```

Merhaba VM oluşturduğunuzda hello Azure CLI örnek aşağıdaki bilgileri benzer toohello gösterir. Merhaba not edin `publicIpAaddress`. Kullanılan tooaccess hello VM adresidir.

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a>Web trafiği için 80 numaralı bağlantı noktasını açın 

Varsayılan olarak, Azure'da dağıtılan tooWindows sanal makineleri yalnızca RDP bağlantılara izin verilir. Bu VM toobe bir Web sunucusu olacaksa, hello Internet gelen tooopen bağlantı noktası 80 gerekir. Kullanım hello [az vm Aç-port](/cli/azure/vm#open-port) komutu tooopen hello istenen bağlantı noktası.  
 
 ```azurecli-interactive  
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```


## <a name="connect-toovirtual-machine"></a>Toovirtual makineyi bağlayın

Kullanım hello aşağıdaki hello sanal makineyle Uzak Masaüstü oturumu toocreate komutu. Başlangıç IP adresi hello genel IP adresi, sanal makine ile değiştirin. İstendiğinde, hello sanal makine oluşturulurken kullanılan hello kimlik bilgilerini girin.

```bash 
mstsc /v:<Public IP Address>
```

## <a name="install-iis-using-powershell"></a>PowerShell kullanarak IIS yükleme

Toohello Azure VM'de oturum, tek satırlık bir PowerShell tooinstall IIS kullanın ve hello yerel güvenlik duvarı kuralı tooallow web trafiği etkinleştirin. PowerShell komut istemini açın ve hello aşağıdaki komutu çalıştırın:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a>Görünüm hello IIS Karşılama sayfası

IIS yüklü ve bağlantı noktası 80, VM'den hello Internet üzerinde şimdi açık ile seçim tooview hello varsayılan IIS Karşılama sayfasını bir web tarayıcısı kullanabilirsiniz. Toovisit hello varsayılan sayfa belgelenen emin toouse hello genel IP adresi olabilir. 

![Varsayılan IIS sitesi](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a>Kaynakları temizleme

Artık gerektiğinde Merhaba kullanabilirsiniz [az grubu Sil](/cli/azure/group#delete) tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Sonraki adımlar

Bu hızlı başlangıçta basit bir sanal makine ve bir ağ güvenlik grubu kuralı dağıtıp, bir web sunucusu yüklediniz. Azure sanal makinelerde hakkında daha fazla toolearn toohello öğretici Windows VM'ler için devam edin.

> [!div class="nextstepaction"]
> [Azure Windows sanal makine öğreticileri](./tutorial-manage-vm.md)
