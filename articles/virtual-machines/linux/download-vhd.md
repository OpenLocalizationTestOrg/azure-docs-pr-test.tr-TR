---
title: aaaDownload Azure Linux VHD'den | Microsoft Docs
description: Hello Azure CLI kullanarak bir Linux VHD indirin ve Azure portal hello.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: davidmu
ms.openlocfilehash: 7e08e985a64a6be581b8f5eedcce60fbd314eaf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-linux-vhd-from-azure"></a>Azure'dan Linux VHD indirin

Bu makalede, bilgi nasıl toodownload bir [Linux sanal sabit disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Azure kullanarak bir dosyadan hello Azure CLI ve Azure portalı. 

Sanal makineler (VM'ler) Azure kullanımda [diskleri](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) yer toostore bir işletim sistemini, uygulamaları ve verileri olarak. Tüm Azure VM'ler en az iki disk – bir Windows işletim sistemi diski ve geçici bir diski var. Merhaba işletim sistemi diski başlangıçta görüntüden oluşturulur ve hem hello işletim sistemi diski ve hello görüntü VHD'leri bir Azure depolama hesabında depolanır. Sanal makineler ayrıca VHD'ler olarak da depolanan bir veya daha fazla veri diski olabilir.

Zaten yapmadıysanız, yükleme [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).

## <a name="stop-hello-vm"></a>Merhaba VM Durdur

Azure'dan bir VHD onu bağlıysa indirilemiyor VM çalıştıran tooa. Toostop hello VM toodownload VHD gerekir. Bir VHD olarak toouse istiyorsanız bir [görüntü](tutorial-custom-images.md) toocreate diğer sanal makineleri yeni disklerle toodeprovision gerekir ve hello bulunan hello işletim sistemini genelleştirir dosya ve hello VM durdurun. toouse hello VHD bir var olan VM veya veri diski yeni bir örneği için bir disk olarak yalnızca toostop gerekir ve hello VM serbest bırakma.

toouse VHD görüntüsü toocreate diğer VM'ler Merhaba, aşağıdaki adımları tamamlayın:

1. SSH, hello hesap adı ve hello VM tooconnect tooit hello genel IP adresi kullanın ve onu sağlamayı sonlandırın. Merhaba + kullanıcı parametresi hello son sağlanan kullanıcı hesabının da kaldırır. Toohello VM hesabı kimlik bilgilerini Fırında pişirme bu bırakın + kullanıcı parametresi. Merhaba aşağıdaki örnek hello son sağlanan kullanıcı hesabını kaldırır:

    ```bash
    ssh azureuser@40.118.249.235
    sudo waagent -deprovision+user -force
    exit 
    ```

2. İçinde tooyour Azure hesabı ile oturum [az oturum açma](https://docs.microsoft.com/cli/azure/#login).
3. Durdurun ve hello VM serbest bırakma.

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

4. Merhaba VM genelleştirin. 

    ```azurecli
    az vm generalize --resource-group myResourceGroup --name myVM
    ``` 

toouse hello VHD bir var olan VM veya veri diski, yeni bir örneği için bir disk olarak aşağıdaki adımları tamamlayın:

1.  İçinde toohello oturum [Azure portal](https://portal.azure.com/).
2.  Merhaba Hub menüsünde **sanal makineleri**.
3.  Merhaba VM hello listeden seçin.
4.  Merhaba VM için Hello dikey penceresinde **durdurmak**.

    ![VM'yi Durdur](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a>SAS URL oluştur

toodownload hello VHD dosyasına ihtiyacınız toogenerate bir [paylaşılan erişim imzası (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL. Merhaba URL oluşturulduğunda, sona erme süresi toohello URL atanır.

1.  Merhaba VM hello dikey penceresinde Hello menüsünde tıklatın **diskleri**.
2.  Merhaba hello VM için işletim sistemi diski seçin ve ardından **verme**.
3.  Tıklatın **URL'yi oluşturmak**.

    ![URL'yi oluşturmak](./media/download-vhd/export-generate.png)

## <a name="download-vhd"></a>VHD indirin

1.  Oluşturulan hello URL altında indirme hello VHD dosyası'ı tıklatın.

    ![VHD indirin](./media/download-vhd/export-download.png)

2.  Tooclick gerekebilir **kaydetmek** hello tarayıcı toostart hello indirme içinde. Merhaba varsayılan ad hello VHD dosyası için *abcd*.

    ![Merhaba tarayıcıda Kaydet'e tıklayın.](./media/download-vhd/export-save.png)

## <a name="next-steps"></a>Sonraki adımlar

- Nasıl çok öğrenin[karşıya yükleme ve hello Azure CLI 2.0 ile özel diskten bir Linux VM oluşturma](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 
- [Azure diskleri hello Azure CLI yönetmek](tutorial-manage-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

