---
title: "aaaCreate ve karşıya yükleme OpenBSD VM görüntü tooAzure | Microsoft Docs"
description: "Toocreate ve karşıya yükleme sanal sabit içeren bir disk (VHD) OpenBSD işletim sistemi toocreate bir Azure sanal makinesini Azure CLI aracılığıyla nasıl hello öğrenin"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: kyliel
ms.openlocfilehash: 0524f45ea1ecec37e55cbe9d54438a571a831de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-an-openbsd-disk-image-tooazure"></a>Oluşturun ve bir OpenBSD disk görüntü tooAzure yükleyin
Bu makalede OpenBSD işletim sistemi toocreate ve karşıya yükleme sanal sabit içeren bir disk (VHD) nasıl hello gösterilmektedir. Karşıya yüklediğiniz sonra kendi görüntü toocreate Azure CLI aracılığıyla azure'da sanal makine (VM) olarak kullanabilirsiniz.


## <a name="prerequisites"></a>Ön koşullar
Bu makalede aşağıdaki öğelerindeki hello olduğunu varsayar:

* **Bir Azure aboneliği** -bir hesabınız yoksa yalnızca birkaç dakika içinde bir oluşturabilirsiniz. Bir MSDN aboneliğiniz varsa, bkz: [Visual Studio aboneleri için aylık Azure kredi](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/). Aksi takdirde nasıl çok öğrenin[ücretsiz bir deneme hesabı oluşturma](https://azure.microsoft.com/pricing/free-trial/).  
* **Azure CLI 2.0** -son hello sahip olduğunuzdan emin olun [Azure CLI 2.0](/cli/azure/install-azure-cli) yüklü ve tooyour içinde Azure hesabı ile oturum [az oturum açma](/cli/azure/#login).
* **Bir .vhd dosyası yüklü OpenBSD işletim sistemi** -desteklenen bir OpenBSD işletim sistemine (sürüm 6.1) yüklü tooa sanal sabit diski olması gerekir. Birden çok araç toocreate .vhd dosyaları mevcut. Örneğin, Hyper-V toocreate hello .vhd dosyası gibi bir sanallaştırma çözümü kullanın ve hello işletim sistemi yükleyin. Tooinstall ve kullanım Hyper-V, nasıl görürüm hakkında yönergeler için [Hyper-V yükleyin ve sanal makine oluşturma](http://technet.microsoft.com/library/hh846766.aspx).


## <a name="prepare-openbsd-image-for-azure"></a>Azure için OpenBSD görüntüsünü hazırlama
Merhaba hello OpenBSD işletim sistemi 6.1, Hyper-V desteği eklendi, yüklediğiniz VM üzerinde hello yordamları tamamlayın:

1. DHCP yükleme sırasında etkin değilse hello hizmeti aşağıdaki gibi etkinleştirin:

    ```sh    
    echo dhcp > /etc/hostname.hvn0
    ```

2. Bir seri Konsolu aşağıdaki gibi ayarlayın:

    ```sh
    echo "stty com0 115200" >> /etc/boot.conf
    echo "set tty com0" >> /etc/boot.conf
    ```

3. Paket yükleme işlemi aşağıdaki gibi yapılandırın:

    ```sh
    echo "https://ftp.openbsd.org/pub/OpenBSD" > /etc/installurl
    ```
   
4. Varsayılan olarak, hello `root` kullanıcı azure'daki sanal makinelerde devre dışıdır. Kullanıcılar çalışma komutları yükseltilmiş ayrıcalıklarla hello kullanarak `doas` OpenBSD VM'de komutu. Doas varsayılan olarak etkindir. Daha fazla bilgi için bkz: [doas.conf](http://man.openbsd.org/doas.conf.5). 

5. Yükleyin ve hello Azure Aracısı önkoşulları aşağıdaki gibi yapılandırın:

    ```sh
    pkg_add py-setuptools openssl git
    ln -sf /usr/local/bin/python2.7 /usr/local/bin/python
    ln -sf /usr/local/bin/python2.7-2to3 /usr/local/bin/2to3
    ln -sf /usr/local/bin/python2.7-config /usr/local/bin/python-config
    ln -sf /usr/local/bin/pydoc2.7  /usr/local/bin/pydoc
    ```

6. Merhaba hello Azure Aracısı en son sürümü her zaman bulunabilir üzerinde [Github](https://github.com/Azure/WALinuxAgent/releases). Merhaba aracıyı aşağıdaki gibi yükleyin:

    ```sh
    git clone https://github.com/Azure/WALinuxAgent 
    cd WALinuxAgent
    python setup.py install
    waagent -register-service
    ```

    > [!IMPORTANT]
    > Azure aracısını yükledikten sonra şu şekilde çalışan bir fikir tooverify şöyledir:
    >
    > ```bash
    > ps auxw | grep waagent
    > root     79309  0.0  1.5  9184 15356 p1  S      4:11PM    0:00.46 python /usr/local/sbin/waagent -daemon (python2.7)
    > cat /var/log/waagent.log
    > ```

7. Deprovision hello sistem tooclean ve yapma, sağlama işleminin için uygun. Hello aşağıdaki komut da hello son sağlanan kullanıcı hesabını ve ilişkili hello verileri siler:

    ```sh
    waagent -deprovision+user -force
    ```

Şimdi, VM kapatma.


## <a name="prepare-hello-vhd"></a>Merhaba VHD hazırlama
Merhaba VHDX biçimi, Azure'da yalnızca desteklenmiyor **VHD sabit**. Hyper-V Yöneticisi'ni kullanarak hello disk toofixed VHD biçimine Dönüştür veya Powershell hello [convert-vhd](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/convert-vhd) cmdlet'i. Örnek olarak verilebilir aşağıdaki.

```powershell
Convert-VHD OpenBSD61.vhdx OpenBSD61.vhd -VHDType Fixed
```

## <a name="create-storage-resources-and-upload"></a>Depolama kaynaklarını oluşturma ve yükleme
İlk olarak, bir kaynak grubu ile oluşturmak [az grubu oluşturma](/cli/azure/group#create). Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu:

```azurecli
az group create --name myResourceGroup --location eastus
```

tooupload, VHD ile depolama hesabı oluşturma [az depolama hesabı oluşturma](/cli/azure/storage/account#create). Depolama hesabı adları benzersiz olması gerekir, böylece kendi adını belirtin. Merhaba aşağıdaki örnek adlı bir depolama hesabı oluşturur *mystorageaccount*:

```azurecli
az storage account create --resource-group myResourceGroup \
    --name mystorageaccount \
    --location eastus \
    --sku Premium_LRS
```

toocontrol erişim toohello depolama hesabı, hello depolama anahtarla elde [az depolama hesabı anahtarları listesi](/cli/azure/storage/account/keys#list) gibi:

```azurecli
STORAGE_KEY=$(az storage account keys list \
    --resource-group myResourceGroup \
    --account-name mystorageaccount \
    --query "[?keyName=='key1']  | [0].value" -o tsv)
```

toologically ayrı hello karşıya yüklediğiniz, VHD oluşturma hello depolama hesabıyla kapsayıcıda [az depolama kapsayıcısı oluşturmak](/cli/azure/storage/container#create):

```azurecli
az storage container create \
    --name vhds \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```

Son olarak, VHD ile karşıya [az depolama blob karşıya yükleme](/cli/azure/storage/blob#upload) gibi:

```azurecli
az storage blob upload \
    --container-name vhds \
    --file ./OpenBSD61.vhd \
    --name OpenBSD61.vhd \
    --account-name mystorageaccount \
    --account-key ${STORAGE_KEY}
```


## <a name="create-vm-from-your-vhd"></a>VM, VHD'den oluştur
Bir VM ile oluşturabileceğiniz bir [örnek komut dosyası](../scripts/virtual-machines-linux-cli-sample-create-vm-vhd.md) veya doğrudan [az vm oluşturma](/cli/azure/vm#create). toospecify hello OpenBSD karşıya yüklediğiniz, VHD kullanım hello `--image` şekilde parametre:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myOpenBSD61 \
    --image "https://mystorageaccount.blob.core.windows.net/vhds/OpenBSD61.vhd" \
    --os-type linux \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

OpenBSD VM ile için başlangıç IP adresi al [az vm listesi-ip-addresses](/cli/azure/vm#list-ip-addresses) gibi:

```azurecli
az vm list-ip-addresses --resource-group myResourceGroup --name myOpenBSD61
```

Artık normal olarak SSH tooyour OpenBSD VM yapabilirsiniz:
        
```bash
ssh azureuser@<ip address>
```


## <a name="next-steps"></a>Sonraki adımlar
Hyper-V hakkında daha fazla destek OpenBSD6.1 üzerinde tooknow istiyorsanız, okuma [OpenBSD 6.1](https://www.openbsd.org/61.html) ve [hyperv.4](http://man.openbsd.org/hyperv.4).

Toocreate yönetilen diskten VM istiyorsanız, okuma [az disk](/cli/azure/disk). 
