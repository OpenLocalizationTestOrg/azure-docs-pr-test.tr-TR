---
title: aaaMonitor Linux sanal makineleri azure'da | Microsoft Docs
description: "Nasıl toomonitor önyükleme tanılama ve performans ölçümleri azure'da bir Linux sanal makine hakkında bilgi edinin"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 282da0f03ab0bf37bd44750c22813ca8d1c89560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-a-linux-virtual-machine-in-azure"></a>Nasıl toomonitor azure'da bir Linux sanal makine

Azure, sanal makineleri (VM'ler) düzgün çalışmasını tooensure önyükleme tanılama ve performans ölçümleri gözden geçirebilirsiniz. Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:

> [!div class="checklist"]
> * Önyükleme tanılaması hello VM üzerinde etkinleştir
> * Önyükleme tanılamasını görüntüleme
> * Ana bilgisayar metrikleri görüntüleyin
> * Merhaba VM tanılama uzantısını etkinleştirme
> * VM metrikleri görüntüleyin
> * Tanılama ölçümleri temel uyarı oluşturma
> * Gelişmiş izleme işlevini ayarlama


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="create-vm"></a>VM oluşturma

toosee tanılama ve eylem ölçümleri, VM gerekir. İlk olarak, bir kaynak grubu ile oluşturmak [az grubu oluşturma](/cli/azure/group#create). Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroupMonitor* hello içinde *eastus* konumu.

```azurecli-interactive 
az group create --name myResourceGroupMonitor --location eastus
```

Şimdi bir VM oluşturmak [az vm oluşturma](https://docs.microsoft.com/cli/azure/vm#create). Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVM*:

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

## <a name="enable-boot-diagnostics"></a>Önyükleme tanılaması etkinleştir

Linux VM'ler önyükleme gibi hello önyükleme tanılama uzantısını önyükleme çıkış yakalar ve Azure depolama alanında depolar. Bu veriler kullanılan tootroubleshoot VM önyükleme sorunları olabilir. Hello Azure CLI kullanarak bir Linux VM oluştururken önyükleme tanılaması otomatik olarak etkin değildir.

Önyükleme tanılaması etkinleştirmeden önce depolama hesabının önyükleme günlüklerini depolamak üzere oluşturulan toobe gerekir. Depolama hesapları 3 ile 24 karakter arasında olması genel olarak benzersiz bir ad olmalıdır ve yalnızca sayılar ve küçük harf içermelidir. Merhaba ile depolama hesabı oluşturma [az depolama hesabı oluşturma](/cli/azure/storage/account#create) komutu. Bu örnekte kullanılan toocreate benzersiz depolama hesabı adı olduğu rastgele bir dizedir. 

```azurecli-interactive 
storageacct=mydiagdata$RANDOM

az storage account create \
  --resource-group myResourceGroupMonitor \
  --name $storageacct \
  --sku Standard_LRS \
  --location eastus
```

Önyükleme tanılaması etkinleştirirken hello URI toohello blob depolama kapsayıcısını gereklidir. Merhaba aşağıdaki komutu sorgularını depolama hesabı tooreturn bu URI hello. Merhaba URI değeri değişken adlarında depolanan *bloburi*, hello sonraki adımda kullanılır.

```azurecli-interactive 
bloburi=$(az storage account show --resource-group myResourceGroupMonitor --name $storageacct --query 'primaryEndpoints.blob' -o tsv)
```

Önyükleme Tanılaması ile şimdi etkinleştirmek [az vm önyükleme-tanılamayı etkinleştirin](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable). Merhaba `--storage` hello blob URI'si toplanan hello önceki adımda değerdir.

```azurecli-interactive 
az vm boot-diagnostics enable \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --storage $bloburi
```


## <a name="view-boot-diagnostics"></a>Önyükleme tanılamasını görüntüleme

Önyükleme tanılaması etkin olduğunda, her zaman durdurup hello VM başlatmak hello önyükleme işlemi hakkında bilgi tooa günlük dosyasına yazılır. Bu örnekte, ilk hello VM hello ile serbest bırakma [az vm serbest bırakma](/cli/azure/vm#deallocate) gibi komut:

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupMonitor --name myVM
```

Merhaba VM ile Merhaba Şimdi Başlat [az vm başlangıç]( /cli/azure/vm#stop) gibi komut:

```azurecli-interactive 
az vm start --resource-group myResourceGroupMonitor --name myVM
```

Merhaba önyükleme Tanılama verileri alabilirsiniz *myVM* hello ile [az vm önyükleme tanılaması get-önyükleme-günlük](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) gibi komut:

```azurecli-interactive 
az vm boot-diagnostics get-boot-log --resource-group myResourceGroupMonitor --name myVM
```


## <a name="view-host-metrics"></a>Ana bilgisayar metrikleri görüntüleyin

Bir Linux VM ayrılmış bir ana bilgisayar ile etkileşime giren Azure sahiptir. Ölçümleri hello ana bilgisayar için otomatik olarak toplanır ve hello Azure portalında şu şekilde görüntülenebilir:

1. Hello Azure portal'ı tıklatın **kaynak grupları**seçin **myResourceGroupMonitor**ve ardından **myVM** hello kaynak listesinde.
1. Merhaba konak VM gerçekleştiriyor nasıl toosee tıklatın **ölçümleri** hello VM dikey penceresinde hello birini seçip *[ana bilgisayar]* altında ölçümleri **kullanılabilir ölçümler**.

    ![Ana bilgisayar metrikleri görüntüleyin](./media/tutorial-monitoring/monitor-host-metrics.png)


## <a name="install-diagnostics-extension"></a>Tanılama uzantısını yükleyin

> [!IMPORTANT]
> Bu belgede hello Linux tanılama kullanım dışı bırakılmış uzantısının 2.3 sürümü açıklanmaktadır. Sürüm 2.3 30 Haziran 2018 kadar desteklenmez.
>
> Merhaba Linux tanılama uzantısını 3.0 sürümü yerine etkinleştirilebilir. Daha fazla bilgi için bkz: [hello belgelerine](./diagnostic-extension.md).

Merhaba temel ana ölçümleri kullanılabilir, ancak toosee daha ayrıntılı ve VM özgü ölçümleri, size tooneed tooinstall hello Azure tanılama uzantısını hello VM. Hello Azure tanılama uzantısını ek izleme ve tanılama veri toobe VM hello alınan sağlar. Bu performans ölçümleri görüntüleyebilir ve hello VM nasıl gerçekleştireceğini temelinde uyarılar oluşturabilir. Merhaba tanılama uzantısını hello Azure portal aşağıdaki şekillerde yüklenir:

1. Hello Azure portal'ı tıklatın **kaynak grupları**seçin **myResourceGroup**ve ardından **myVM** hello kaynak listesinde.
1. Tıklatın **tanılama ayarları**. Merhaba liste gösterir *önyükleme tanılama* hello önceki bölümden zaten etkin. Merhaba onay kutusu için *temel ölçümleri*.
1. Merhaba, *depolama hesabı* bölümünde, tooand select hello Gözat *mydiagdata [1234]* hello önceki bölümde oluşturduğunuz hesabı.
1. Merhaba tıklatın **kaydetmek** düğmesi.

    ![Tanılama metrikleri görüntüleyin](./media/tutorial-monitoring/enable-diagnostics-extension.png)


## <a name="view-vm-metrics"></a>VM metrikleri görüntüleyin

Hello hello VM ölçümleri görüntüleyebilir aynı şekilde hello konak VM ölçümleri görüntülenebilir:

1. Hello Azure portal'ı tıklatın **kaynak grupları**seçin **myResourceGroup**ve ardından **myVM** hello kaynak listesinde.
1. Merhaba VM gerçekleştiriyor nasıl toosee tıklatın **ölçümleri** üzerinde VM dikey penceresinde hello ve hello tanılama ölçümleri altında birini seçin **kullanılabilir ölçümler**.

    ![VM metrikleri görüntüleyin](./media/tutorial-monitoring/monitor-vm-metrics.png)


## <a name="create-alerts"></a>Uyarı oluşturma

Özel performans ölçümleri temelinde uyarılar oluşturabilirsiniz. Uyarılar, ortalama CPU kullanımını belirli bir eşiği veya kullanılabilir boş disk alanı aştığında belirli bir bir miktar düşene kullanılan toonotify örneğin olabilir. Uyarıları hello Azure portalında görüntülenen veya e-posta ile gönderilebilir. Azure Otomasyon çalışma kitabı veya Azure Logic Apps içinde oluşturulan yanıt tooalerts tetikleyebilir.

Merhaba aşağıdaki örnek ortalama CPU kullanımı için bir uyarı oluşturur.

1. Hello Azure portal'ı tıklatın **kaynak grupları**seçin **myResourceGroup**ve ardından **myVM** hello kaynak listesinde.
2. Tıklatın **uyarı kuralları** hello VM dikey penceresinde, ardından **ölçüm uyarı Ekle** hello uyarıları dikey hello üstte.
4. Sağlayan bir **adı** , uyarının gibi *myAlertRule*
5. tootrigger CPU yüzdesi beş dakika 1.0 aştığında bir uyarı, seçili diğer Varsayılanları tüm hello bırakın.
6. İsteğe bağlı olarak, hello kutuyu için *sahipleri, Katkıda Bulunanlar ve okuyucular e-posta* toosend e-posta bildirimi. Merhaba varsayılan toopresent hello Portalı'nda bir bildirim eylemdir.
7. Merhaba tıklatın **Tamam** düğmesi.


## <a name="advanced-monitoring"></a>Gelişmiş izleme 

Kullanarak VM'yi izleme daha gelişmiş yapabileceğiniz [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview). Zaten yapmadıysanız, için kaydolabilirsiniz bir [ücretsiz deneme sürümü](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) Operations Management Suite.

Erişim toohello OMS portalı varsa, hello çalışma alanı anahtarı ve çalışma alanı kimliği hello ayarları dikey penceresinde bulabilirsiniz. Değiştir < çalışma alanı anahtarı > ve < çalışma alanı kimliği > hello için değerlerle, OMS çalışma ve ardından, kullanabilirsiniz **az vm uzantısı kümesi** tooadd hello OMS uzantısı toohello VM:

```azurecli-interactive 
az vm extension set \
  --resource-group myResourceGroupMonitor \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.3 \
  --protected-settings '{"workspaceKey": "<workspace-key>"}' \
  --settings '{"workspaceId": "<workspace-id>"}'
```

Merhaba günlük arama dikey penceresinde hello OMS portalı görmelisiniz *myVM* ne hello resim aşağıdaki gösterildiği gibi:

![OMS dikey penceresi](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide yapılandırılmış ve sanal makineleri Azure Güvenlik Merkezi ile gözden. Şunları öğrendiniz:

> [!div class="checklist"]
> * Önyükleme tanılaması hello VM üzerinde etkinleştir
> * Önyükleme tanılamasını görüntüleme
> * Ana bilgisayar metrikleri görüntüleyin
> * Merhaba VM tanılama uzantısını etkinleştirme
> * VM metrikleri görüntüleyin
> * Tanılama ölçümleri temel uyarı oluşturma
> * Gelişmiş izleme işlevini ayarlama

Azure Güvenlik Merkezi hakkında toohello sonraki öğretici toolearn ilerleyin.

> [!div class="nextstepaction"]
> [VM güvenliğini yönetme](./tutorial-azure-security.md)