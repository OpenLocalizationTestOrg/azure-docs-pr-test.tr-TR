---
title: "azure'daki Linux sanal makineleri için aaaBoot tanılama | Microsoft belge"
description: "İki hata ayıklama özelliklerini Linux sanal makineleri azure'da hello genel bakış"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: Deland-Han
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: delhan
ms.openlocfilehash: d355d512de09d2f1d7a2718e3db3fb99c9dd9e24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-boot-diagnostics-tootroubleshoot-linux-virtual-machines-in-azure"></a>Nasıl toouse önyükleme tanılama tootroubleshoot Linux sanal makineleri Azure'da

Azure’da artık iki hata ayıklama özelliği desteklenmektedir: Azure Sanal Makineler Kaynak Yöneticisi dağıtım modelinde Konsol Çıktısı ve Ekran Görüntüsü desteği vardır. 

Kendi görüntü tooAzure veya hello platform görüntüleri bile önyükleme biri getirilirken bir sanal makine önyüklenebilir olmayan bir duruma neden alır birçok nedeni olabilir. Bu özellikler, tooeasily tanılamak ve sanal makinelerinizi önyükleme hatalarını kurtarıp etkinleştir.

Linux sanal makineleri için hello Portal, konsol günlüğünden hello çıktısını kolayca görüntüleyebilirsiniz:

![Azure portalına](./media/boot-diagnostics/screenshot1.png)
 
Ancak, Windows ve Linux sanal makineleri için Azure ayrıca bir ekran görüntüsünü hello VM hello hiper yönetici gelen toosee sağlar:

![Hata](./media/boot-diagnostics/screenshot2.png)

Bu özelliklerin her ikisi de tüm bölgelerdeki Azure sanal makineler için desteklenir. Not, ekran görüntüleri ve çıktı too10 dakika tooappear depolama hesabınızdaki yukarı alabilir.

## <a name="common-boot-errors"></a>Sık karşılaşılan önyükleme hataları

- [Dosya sistemi sorunları](https://blogs.msdn.microsoft.com/linuxonazure/2016/09/13/linux-recovery-cannot-ssh-to-linux-vm-due-to-file-system-errors-fsck-inodes/)
- [Çekirdek sorunları](https://blogs.msdn.microsoft.com/linuxonazure/2016/10/09/linux-recovery-manually-fixing-non-boot-issues-related-to-kernel-problems/)
- [FSTAB hataları](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/ )

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a>Yeni bir sanal makine üzerinde tanılamayı etkinleştir
1. Önizleme portalı hello yeni bir sanal makine oluştururken, hello seçin **Azure Resource Manager** gelen hello dağıtım modeli açılır:
 
    ![Resource Manager](./media/boot-diagnostics/screenshot3.jpg)

2. Bu tanılama dosyaları Hello tooplace oluşturulacağı yeri izleme seçeneği tooselect hello depolama hesabı yapılandırın.
 
    ![VM oluşturma](./media/boot-diagnostics/screenshot4.jpg)

3. Bir Azure Resource Manager şablonu dağıtıyorsanız, tooyour sanal makine kaynağı gidin ve hello tanılama profil bölümü ekleyin. Toouse hello "2015-06-15" API sürümü üstbilgisi unutmayın.

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. Merhaba tanılama profili Bu günlükler tooput istediğiniz yere tooselect hello depolama hesabını etkinleştirir.

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

## <a name="update-an-existing-virtual-machine"></a>Mevcut bir sanal makineyi güncelleştirme

tooenable önyükleme tanılaması hello Portalı aracılığıyla mevcut bir sanal makine hello Portalı aracılığıyla güncelleştirebilirsiniz. Select hello önyükleme tanılaması seçeneği ve kaydedin. Merhaba VM tootake etkisi yeniden başlatın.

![Mevcut VM’yi güncelleştirme](./media/boot-diagnostics/screenshot5.png)