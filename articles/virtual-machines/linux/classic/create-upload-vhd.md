---
title: "aaaCreate ve Linux VHD tooAzure karşıya | Microsoft Docs"
description: "Oluşturma ve bir Azure sanal sabit hello Klasik dağıtım modeli kullanarak hello Linux işletim sistemini içeren disk (VHD) yükleme"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8058ff98-db03-4309-9bf4-69842bd64dd4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: iainfou
ms.openlocfilehash: 77b01316386c4a6eb68c129fa68d42f0a8996edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-uploading-a-virtual-hard-disk-that-contains-hello-linux-operating-system"></a>Oluşturma ve bir Sanal Sabit Disk, Linux işletim sistemi içerir hello karşıya yükleme
> [!IMPORTANT] 
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Ayrıca [Azure Kaynak Yöneticisi'ni kullanarak bir özel disk görüntüsü karşıya](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Bu makalede nasıl toocreate ve karşıya yükleme bir sanal sabit disk (VHD), kendi olarak kullanabilmek için Azure toocreate sanal makinelerde görüntü gösterilmektedir. Nasıl tooprepare hello toocreate kullanabilmesi için birden çok sanal makine üzerinde görüntü tabanlı bir işletim sistemine öğrenin. 


## <a name="prerequisites"></a>Ön koşullar
Bu makalede aşağıdaki öğelerindeki hello olduğunu varsayar:

* **Bir .vhd dosyası yüklü Linux işletim sistemi** -yüklü olduğu bir [Linux Azure destekli dağıtım](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (veya bkz [desteklenmeyen dağıtımlarla bilgi](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)) tooa sanal disk Merhaba VHD biçiminde. Birden çok araç, bir VM ve VHD toocreate mevcuttur:
  * Yükleme ve yapılandırma [QEMU](https://en.wikibooks.org/wiki/QEMU/Installing_QEMU) veya [KVM](http://www.linux-kvm.org/page/RunningKVM), toouse VHD, resim biçimi olarak ayırdığınız dikkat edin. Gerekirse, [bir görüntüyü dönüştürme](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) kullanarak `qemu-img convert`.
  * Hyper-V de kullanabilirsiniz [Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install) veya [Windows Server 2012/2012 R2 üzerinde](https://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> Azure'da Hello yeni VHDX biçimi desteklenmiyor. Bir VM oluşturun, VHD'yi hello biçiminde belirtin. Gerekirse, VHDX diskleri tooVHD kullanarak dönüştürebilirsiniz [ `qemu-img convert` ](https://en.wikibooks.org/wiki/QEMU/Images#Converting_image_formats) veya hello [ `Convert-VHD` ](https://technet.microsoft.com/library/hh848454.aspx) PowerShell cmdlet'i. Ayrıca, Azure tooconvert gerekir böylece dinamik VHD karşıya böyle diskleri toostatic VHD yüklemeden önce desteklemez. Araçları gibi kullanabilir [Git için Azure VHD yardımcı programları](https://github.com/Microsoft/azure-vhd-utils-for-go) hello tooAzure karşıya yükleme işlemi sırasında tooconvert dinamik diskler.

* **Azure komut satırı arabirimi** -son yükleme hello [Azure komut satırı arabirimi](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooupload hello VHD.

<a id="prepimage"> </a>

## <a name="step-1-prepare-hello-image-toobe-uploaded"></a>1. adım: karşıya hello görüntü toobe hazırlama
Azure çeşitli Linux dağıtımları destekler (bkz [destekli dağıtımlar](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). aşağıdaki makaleleri hello size nasıl tooprepare hello Azure üzerinde desteklenen çeşitli Linux dağıtımları yol. Kılavuzları aşağıdaki hello hello adımları tamamladıktan sonra hazır tooupload tooAzure bir VHD dosya olduktan sonra tekrar buraya gelin:

* **[CentOS tabanlı dağıtımlar](../create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Debian Linux](../debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Oracle Linux](../oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Red Hat Enterprise Linux](../redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[SLES & openSUSE](../suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Ubuntu](../create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**
* **[Diğer - desteklenmeyen dağıtımlarla](../create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)**

> [!NOTE]
> Hello Azure platformu SLA toovirtual makineleri yalnızca hello birini destekli dağıtımlar Linux OS 'Sürümleri desteklenir' altında belirtildiği gibi hello yapılandırma ayrıntılarını olarak kullanılan hello çalışır durumda geçerlidir [Azure-Endorsed dağıtımları Linux'ta ](../endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Tüm Linux dağıtımları hello Azure görüntü Galerisi içinde hello gerekli yapılandırma ile doğrulanan dağıtımları ' dir.
> 
> 

Ayrıca bkz. hello  **[Linux yükleme notları](../create-upload-generic.md#general-linux-installation-notes)**  için Azure Linux görüntüleri hazırlama hakkında daha fazla genel ipuçları için.

<a id="connect"> </a>

## <a name="step-2-prepare-hello-connection-tooazure"></a>2. adım: hello bağlantı tooAzure hazırlama
Hello Azure CLI hello Klasik dağıtım modelinde kullandığınızdan emin olun (`azure config mode asm`), tooyour hesabında oturum açın:

```azurecli
azure login
```


<a id="upload"> </a>

## <a name="step-3-upload-hello-image-tooazure"></a>3. adım: Karşıya yükleme hello görüntü tooAzure
VHD dosyasına yönelik bir depolama hesabı tooupload gerekir. Mevcut bir depolama hesabını ya da seçebilirsiniz veya [yeni bir tane oluşturun](../../../storage/common/storage-create-storage-account.md).

Hello Azure CLI tooupload hello görüntü komutu aşağıdaki hello kullanarak kullanın:

```azurecli
azure vm image create <ImageName> `
    --blob-url <BlobStorageURL>/<YourImagesFolder>/<VHDName> `
    --os Linux <PathToVHDFile>
```

Merhaba önceki örnekte:

* **BlobStorageURL** toouse planladığınız hello depolama hesabı hello URL'si
* **YourImagesFolder** hello blob depolama içinde istediğiniz yere toostore görüntülerinizi kapsayıcıdır
* **VHDName** portal tooidentify hello sanal sabit disk görünür hello etiket.
* **PathToVHDFile** hello tam yol ve makinenizde hello .vhd dosyasının adı.

komutu aşağıdaki hello tam bir örnek gösterilmektedir:

```azurecli
azure vm image create myImage `
    --blob-url https://mystorage.blob.core.windows.net/vhds/myimage.vhd `
    --os Linux /home/ahmet/myimage.vhd
```

## <a name="step-4-create-a-vm-from-hello-image"></a>4. adım: hello görüntüsünden bir VM oluşturma
Kullanarak bir VM oluşturun `azure vm create` Merhaba, normal bir VM ile aynı şekilde. Görüntünüzü hello önceki adımda verdiğiniz hello adı belirtin. Aşağıdaki örneğine hello kullanırız hello **myImage** hello önceki adımda belirtilen görüntü adı:

```azurecli
azure vm create --userName ops --password P@ssw0rd! --vm-size Small --ssh `
    --location "West US" "myDeployedVM" myImage
```

toocreate kendi sanal makineleri, kendi kullanıcı adı + parola, konum, DNS adı ve görüntü adı sağlayın.

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi için bkz: [hello Azure Klasik dağıtım modeli için Azure CLI başvurusu](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

[Step 1: Prepare hello image toobe uploaded]:#prepimage
[Step 2: Prepare hello connection tooAzure]:#connect
[Step 3: Upload hello image tooAzure]:#upload
