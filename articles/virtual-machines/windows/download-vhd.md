---
title: aaaDownload Azure Windows VHD'den | Microsoft Docs
description: Windows hello Azure portal kullanarak VHD indirin.
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
ms.openlocfilehash: d0ca8842db98f22751f01648c0ba4e5cde090043
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="download-a-windows-vhd-from-azure"></a>VHD Windows Azure'dan indirin

Bu makalede, bilgi nasıl toodownload bir [Windows sanal sabit disk (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Azure kullanarak bir dosyadan hello Azure portalı. 

Sanal makineler (VM'ler) Azure kullanımda [diskleri](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) yer toostore bir işletim sistemini, uygulamaları ve verileri olarak. Tüm Azure VM'ler en az iki disk – bir Windows işletim sistemi diski ve geçici bir diski var. Merhaba işletim sistemi diski başlangıçta görüntüden oluşturulur ve hem hello işletim sistemi diski ve hello görüntü VHD'leri bir Azure depolama hesabında depolanır. Sanal makineler ayrıca VHD'ler olarak da depolanan bir veya daha fazla veri diski olabilir.

## <a name="stop-hello-vm"></a>Merhaba VM Durdur

Azure'dan bir VHD onu bağlıysa indirilemiyor VM çalıştıran tooa. Toostop hello VM toodownload VHD gerekir. Bir VHD'yi kullanılabilir olarak toouse istiyorsanız bir [görüntü](tutorial-custom-images.md) toocreate kullandığınız diğer sanal makineleri yeni disklerle [Sysprep](https://docs.microsoft.com/windows-hardware/manufacture/desktop/sysprep--generalize--a-windows-installation) toogeneralize hello işletim sistemi hello dosyasında yer alan ve hello VM durdurun. toouse hello VHD bir var olan VM veya veri diski yeni bir örneği için bir disk olarak yalnızca toostop gerekir ve hello VM serbest bırakma.

toouse VHD görüntüsü toocreate diğer VM'ler Merhaba, aşağıdaki adımları tamamlayın:

1.  Zaten yapmadıysanız, toohello içinde oturum [Azure portal](https://portal.azure.com/).
2.  [Toohello VM bağlanmak](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 
3.  Hello VM, bir yönetici olarak hello komut istemi penceresi açın.
4.  Merhaba dizini çok değiştirmek*%windir%\system32\sysprep* ve sysprep.exe çalıştırın.
5.  Merhaba Sistem Hazırlama Aracı iletişim kutusunda seçin **girin sistem Out-of-Box deneyimi (OOBE)**, emin olun **Generalize** seçilir.
6.  Kapatma seçenekleri belirleyin **kapatma**ve ardından **Tamam**. 

toouse hello VHD bir var olan VM veya veri diski, yeni bir örneği için bir disk olarak aşağıdaki adımları tamamlayın:

1.  Merhaba Hub menüsünde hello Azure portal'ın **sanal makineleri**.
2.  Merhaba VM hello listeden seçin.
3.  Merhaba VM için Hello dikey penceresinde **durdurmak**.

    ![VM'yi Durdur](./media/download-vhd/export-stop.png)

## <a name="generate-sas-url"></a>SAS URL oluştur

toodownload hello VHD dosyasına ihtiyacınız toogenerate bir [paylaşılan erişim imzası (SAS)](../../storage/common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) URL. Merhaba URL oluşturulduğunda, sona erme süresi toohello URL atanır.

1.  Merhaba VM hello dikey penceresinde Hello menüsünde tıklatın **diskleri**.
2.  Merhaba hello VM için işletim sistemi diski seçin ve ardından **verme**.
3.  Merhaba sona erme süresini hello URL'nin çok ayarlamak*36000*.
4.  Tıklatın **URL'yi oluşturmak**.

    ![URL'yi oluşturmak](./media/download-vhd/export-generate.png)

> [!NOTE]
> Merhaba süre sonu zamanı hello varsayılan tooprovide toodownload hello büyük VHD dosyasını bir Windows Server işletim sistemi için yeterli süre artar. Bağlantınızı bağlı olarak birkaç saat toodownload hello Windows Server işletim sistemi tootake içeren bir VHD dosyası bekleyebilirsiniz. Veri diski için bir VHD yüklüyorsanız hello varsayılan süre yeterli olur. 
> 
> 

## <a name="download-vhd"></a>VHD indirin

1.  Oluşturulan hello URL altında indirme hello VHD dosyası'ı tıklatın.

    ![VHD indirin](./media/download-vhd/export-download.png)

2.  Tooclick gerekebilir **kaydetmek** hello tarayıcı toostart hello indirme içinde. Merhaba varsayılan ad hello VHD dosyası için *abcd*.

    ![Merhaba tarayıcıda Kaydet'e tıklayın.](./media/download-vhd/export-save.png)

## <a name="next-steps"></a>Sonraki adımlar

- Nasıl çok öğrenin[bir VHD dosyası tooAzure karşıya](upload-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 
- [Bir depolama hesabı yönetilmeyen disklerden yönetilen diskleri oluşturma](attach-disk-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
- [PowerShell ile Azure diskleri yönetme](tutorial-manage-data-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

