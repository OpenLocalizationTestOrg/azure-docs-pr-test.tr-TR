---
title: "bir Azure Windows VM görüntüsünü aaaCapture | Microsoft Docs"
description: "Merhaba Klasik dağıtım modeli kullanılarak oluşturulmuş bir Azure Windows sanal makine bir görüntüsünü yakalayın."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: a5986eac-4cf3-40bd-9b79-7c811806b880
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: b9bbc437012aa44295f90941c9d72e39509df28f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="capture-an-image-of-an-azure-windows-virtual-machine-created-with-hello-classic-deployment-model"></a>Merhaba Klasik dağıtım modeli kullanılarak oluşturulmuş bir Azure Windows sanal makine bir görüntüsünü yakalayın.
> [!IMPORTANT]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Resource Manager modeli için bilgi [genelleştirilmiş VM Azure ile yönetilen bir görüntüsünü yakalama](../capture-image-resource.md).

Bu makale size nasıl gösterir toocapture bir görüntü toocreate kullanabilmeniz için diğer sanal makineler Windows çalıştıran bir Azure sanal makine. Tüm veri disklerinin toohello sanal makineye bağlı ve bu görüntüyü hello işletim sistemi diski içerir. Merhaba görüntü kullanan diğer sanal makineleri hello oluşturduğunuzda, ağ yapılandırmaları yukarı tooset gerekir böylece ağ yapılandırmaları içermez.

Azure depoları hello altındaki görüntüyü **VM görüntüleri (Klasik)**, **işlem** tüm görüntülediğinizde listelenen hizmet hello Azure Hizmetleri. Merhaba budur karşıya görüntülerin depolandığı aynı yerde. Görüntüleri hakkında daha fazla ayrıntı için bkz: [sanal makineler için görüntüleri hakkında](about-images.md?toc=%2fazure%2fvirtual-machines%2fWindows%2fclassic%2ftoc.json).

## <a name="before-you-begin"></a>Başlamadan önce
Bu adımlarda, bir Azure sanal makinesi oluşturulur ve hello işletim sistemi, tüm veri diskleri ekleme de dahil olmak üzere yapılandırılmış varsayılmaktadır. Bunu henüz yapmadıysanız hello sanal makine hazırlanıyor ve oluşturma hakkındaki bilgi makaleleri aşağıdaki hello bakın:

* [Bir görüntüden sanal makine oluşturma](createportal.md)
* [Nasıl tooattach bir veri diski tooa sanal makine](attach-disk.md)
* Merhaba sunucu rolleri Sysprep ile desteklendiğinden emin olun. Daha fazla bilgi için bkz: [sunucu rolleri için Sysprep desteği](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).

> [!WARNING]
> Bu işlem, yakalandıktan sonra hello özgün sanal makine siler.
>
>

Önceki toocapturing bir Azure sanal makinesi görüntüsünü bir önerilir hello hedef sanal makine yedeklenebilir. Azure sanal makineleri Azure Yedekleme kullanılarak yedeklenebilir. Ayrıntılar için bkz. [Azure sanal makinelerini yedekleme](../../../backup/backup-azure-vms.md). Sertifikalı iş ortaklarının sunduğu başka çözümler vardır. şu anda kullanılabilir nedir çıkışı toofind hello Azure Marketi arayın.

## <a name="capture-hello-virtual-machine"></a>Merhaba sanal makinesi yakalama
1. Merhaba, [Azure portal](http://portal.azure.com), **Bağlan** toohello sanal makine. Yönergeler için bkz: [nasıl tooa sanal Windows Server çalıştıran makinede toosign][How toosign in tooa virtual machine running Windows Server].
2. Yönetici olarak bir komut istemi penceresi açın.
3. Merhaba dizini çok değiştirmek`%windir%\system32\sysprep`, ve ardından sysprep.exe çalıştırın.
4. Merhaba **Sistem Hazırlama aracı** iletişim kutusu görüntülenir. Aşağıdaki hello:

   * İçinde **sistem temizleme eylemi**seçin **girin sistem Out-of-Box deneyimi (OOBE)** emin olun **Generalize** denetlenir. Sysprep kullanma hakkında daha fazla bilgi için bkz: [nasıl tooUse Sysprep: Giriş][How tooUse Sysprep: An Introduction].
   * İçinde **kapatma seçenekleri**seçin **kapatma**.
   * **Tamam** düğmesine tıklayın.

   ![Sysprep'i çalıştırın](./media/capture-image/SysprepGeneral.png)
5. Sysprep kapatır hello sanal çok hello Azure portal hello sanal makinede hello durumunu Değişeni makineyi,**durduruldu**.
6. Hello Azure portal'ı tıklatın **sanal makineleri (Klasik)** ve hello toocapture istediğiniz sanal makine seçin. Merhaba **VM görüntüleri (Klasik)** grubu altında listelenen **işlem** görüntülediğinizde **daha fazla hizmet**.

7. Merhaba komut çubuğunda **yakalama**.

   ![Sanal makine yakalama](./media/capture-image/CaptureVM.png)

   Merhaba **yakalama hello sanal makine** iletişim kutusu görüntülenir.

8. İçinde **görüntü adı**, hello yeni görüntüsü için bir ad yazın. İçinde **görüntü etiketi**, hello yeni görüntüsü için bir etiket yazın.

9. Tıklatın **hello sanal makinede Sysprep çalıştırdım**. Bu onay kutusunu toohello eylemlerinde Sysprep ile 3-5 adımlarını gösterir. Bir görüntü _gerekir_ genelleştirilmiş bir Windows sunucusu eklemeden önce özel görüntü görüntü tooyour kümesi Sysprep çalıştırarak.

10. Merhaba yakalama işlemi tamamlandıktan sonra hello yeni görüntüsü hello kullanılabilir **Market**, hello içinde **işlem**, **VM görüntüleri (Klasik)** kapsayıcı.

    ![Görüntü yakalama başarılı](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a>Sonraki adımlar
Merhaba, kullanılan hazır toobe toocreate sanal makineleri görüntüdür. toodo bunu hello seçerek bir sanal makine oluşturacaksınız **daha fazla hizmet** menü öğesi hello Hizmetleri menüsü, ardından hello sonundaki **VM görüntüleri (Klasik)** hello içinde **işlem**grubu. Yönergeler için bkz: [bir görüntüden sanal makine oluşturma](createportal.md).

[How toosign in tooa virtual machine running Windows Server]:connect-logon.md
[How tooUse Sysprep: An Introduction]: http://technet.microsoft.com/library/bb457073.aspx
[Run Sysprep.exe]: ./media/virtual-machines-capture-image-windows-server/SysprepCommand.png
[Enter Sysprep.exe options]: ./media/capture-image/SysprepGeneral.png
[hello virtual machine is stopped]: ./media/virtual-machines-capture-image-windows-server/SysprepStopped.png
[Capture an image of hello virtual machine]: ./media/capture-image/CaptureVM.png
[Enter hello image name]: ./media/virtual-machines-capture-image-windows-server/Capture.png
[Image capture successful]: ./media/virtual-machines-capture-image-windows-server/CaptureSuccess.png
[Use hello captured image]: ./media/virtual-machines-capture-image-windows-server/MyImagesWindows.png
