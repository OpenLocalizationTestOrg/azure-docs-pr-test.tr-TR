---
title: "bir Linux VM görüntüsünü aaaCapture | Microsoft Docs"
description: "Toocapture bir Linux tabanlı Azure sanal makine (VM) görüntüsü hello Klasik dağıtım modeliyle nasıl oluşturulacağını öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17d7ffee-a58e-4290-9de1-64c3cf1ddc05
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 33c4059d5bb919a86bdc3492abca540750f365ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocapture-a-classic-linux-virtual-machine-as-an-image"></a>Nasıl toocapture klasik bir Linux sanal makinesini görüntü olarak
> [!IMPORTANT]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Nasıl çok öğrenin[hello Resource Manager modelini kullanarak bu adımları uygulamadan](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Bu makale size nasıl gösterir toocapture bir Klasik Azure Linux bir görüntü toocreate diğer sanal makineler çalıştıran sanal makine (VM). Bu görüntü hello işletim sistemi diski içerir ve veri diskleri toohello VM bağlı. Tooconfigure gereken şekilde ağ yapılandırmasını, içermez, oluşturduğunuzda hello diğer VM hello görüntüden.

Azure depoları hello altındaki görüntüyü **görüntüleri**, karşıya tüm görüntüleri yanı sıra. Görüntüleri hakkında daha fazla bilgi için bkz: [azure'da sanal makine görüntülerini hakkında][About Virtual Machine Images in Azure].

## <a name="before-you-begin"></a>Başlamadan önce
Bu adımları hello Klasik dağıtım modeli ve veri diskleri ekleme de dahil olmak üzere yapılandırılmış hello işletim sistemi kullanarak bir Azure VM zaten oluşturduğunuzu varsayalım. Toocreate VM ihtiyacınız varsa okuyun [nasıl tooCreate Linux sanal makine][How tooCreate a Linux Virtual Machine].

## <a name="capture-hello-virtual-machine"></a>Merhaba sanal makinesi yakalama
1. [Toohello VM bağlanmak](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) tercih ettiğiniz bir SSH istemcisi kullanarak.
2. Merhaba SSH penceresinde hello aşağıdaki komutu yazın. Merhaba çıktı `waagent` bu yardımcı program hello sürümüne bağlı olarak biraz değişebilir:

    ```bash
    sudo waagent -deprovision+user
    ```

    Merhaba yukarıdaki komut tooclean hello sistem çalışır ve sağlama işleminin uygun yapın. Bu işlem hello aşağıdaki görevleri gerçekleştirir:

   * (Provisioning.RegenerateSshHostKeyPair hello yapılandırma dosyasındaki ' y' ise) SSH ana bilgisayar anahtarlarını kaldırır
   * Ad sunucusu yapılandırmasında /etc/resolv.conf temizler
   * Kaldırır hello `root` (Provisioning.DeleteRootPassword 'y' hello yapılandırma dosyasında ise) / etc/gölge kullanıcı parolasından
   * Önbelleğe alınan istemci kiralamalarını kaldırır
   * Sıfırlama ana bilgisayar adı toolocalhost.localdomain
   * Merhaba (/var/lib/waagent elde edilen) son sağlanan kullanıcının hesabını siler **ve veri ilişkili**.

     > [!NOTE]
     > Sağlama kaldırmayı dosyalarını siler ve veri çok "Merhaba görüntü generalize". Yalnızca yeni bir görüntü şablon olarak toocapture düşündüğünüz bu komutu bir VM üzerinde çalıştırın. Bu hello görüntüyü tüm hassas bilgilerin temizlenmiş veya yeniden dağıtımı toothird taraflar için uygun garanti etmez.

3. Tür **y** toocontinue. Merhaba ekleyebilirsiniz `-force` parametresi tooavoid bu onay adımı.
4. Tür **çıkış** tooclose hello SSH istemcisi.

   > [!NOTE]
   > Merhaba Kalan adımların zaten sahip olduğu varsayılır [hello Azure CLI yüklenmiş](../../../cli-install-nodejs.md) istemci bilgisayarınızda. Aşağıdaki adımları tüm hello hello de yapılabilir [Azure portal](http://portal.azure.com).

5. İstemci bilgisayarından, Azure CLI ve oturum açma tooyour Azure aboneliği açın. Ayrıntılar için [tooan Azure aboneliği hello Azure CLI ' bağlanma](../../../xplat-cli-connect.md).

   > [!NOTE]
   > Hello Azure portal, toohello Portalı'nda oturum açın.

6. Hizmet Yönetimi modunda olduğundan emin olun:

    ```azurecli
    azure config mode asm
    ```

7. Zaten sağlaması kaldırılıyor. sağlaması VM Hello kapatın. Merhaba aşağıdaki örnek kapatır adlı VM hello `myVM`:

    ```azurecli
    azure vm shutdown myVM
    ```
   Gerekirse, tüm hello VM'ler aboneliğinizde kullanılarak oluşturulan bir listesini görüntüleyebilirsiniz`azure vm list`

   > [!NOTE]
   > Hello Azure portalını kullanıyorsanız, hello VM seçin ve tıklatın **durdurmak** VM hello kapatılamadı.

8. Merhaba VM durdurulduğunda hello görüntüsünü yakalayın. Örnek yakalamaları aşağıdaki hello hello adlı VM `myVM` ve adlı genelleştirilmiş bir yansıma oluşturur `myNewVM`:

    ```azurecli
    azure vm capture -t myVM myNewVM
    ```

    Merhaba `-t` siler hello özgün sanal makine alt.

    > [!NOTE]
    > Hello Azure portal, seçerek bir görüntüsünü yakalayabilirsiniz **görüntü** hello hub menüsünde. Aşağıdaki bilgilerle hello görüntüsü için toosupply hello gerekir: adı, kaynak grubu, konum, işletim sistemi türü ve depolama blob yolu.

9. artık yeni bir VM olabilir görüntülerinin hello listesinde kullanılabilir tooconfigure kullanılan hello yeni görüntüdür. Merhaba komutuyla görüntüleyebilirsiniz:

   ```azurecli
   azure vm image list
   ```

   Merhaba üzerinde [Azure portal](http://portal.azure.com), hello yeni görüntüsü görünür hello **VM görüntüleri (Klasik)** toohello ait **işlem** Hizmetleri. Erişebileceğiniz **VM görüntüleri (Klasik)** tıklayarak _daha fazla hizmet_ listesi hello Azure hello alt kısmındaki hizmet ve hello arayan **işlem** Hizmetleri.   

   ![Görüntü yakalama başarılı](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a>Sonraki adımlar
Merhaba, kullanılan hazır toobe toocreate VM'ler görüntüdür. Hello Azure CLI komutunu kullanabilirsiniz `azure vm create` ve oluşturduğunuz kaynağı hello görüntü adı. Daha fazla bilgi için bkz: [Klasik dağıtım modeli ile Azure CLI kullanarak hello](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

Alternatif olarak, hello kullanın [Azure portal](http://portal.azure.com) toocreate hello kullanarak özel bir VM **görüntü** yöntemi ve hello seçerek görüntü oluşturduğunuz. Daha fazla bilgi için bkz: [nasıl tooCreate özel VM][How tooCreate a Custom Virtual Machine].

**Ayrıca bkz:** [Azure Linux Aracısı Kullanıcı Kılavuzu](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[About Virtual Machine Images in Azure]:../../virtual-machines-linux-classic-about-images.md
[How tooCreate a Custom Virtual Machine]:create-custom.md
[How tooAttach a Data Disk tooa Virtual Machine]:attach-disk.md
[How tooCreate a Linux Virtual Machine]:create-custom.md
