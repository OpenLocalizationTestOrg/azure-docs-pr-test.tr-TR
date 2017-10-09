---
title: "aaaHow tooreset ağ arabirimi için Azure Windows VM | Microsoft Docs"
description: "Nasıl tooreset ağ arabirimi için Azure Windows VM gösterir"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: genli
ms.openlocfilehash: 1b653820927ef4c3bb8f384a7e752846a8be3da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-network-interface-for-azure-windows-vm"></a>Nasıl tooreset ağ arabirimi için Azure Windows VM 

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Merhaba varsayılan ağ arabirim (NIC) devre dışı bıraktıktan sonra tooMicrosoft Azure Windows sanal makine (VM) bağlanılamıyor veya el ile statik bir IP hello NIC için ayarlar Bu makalede nasıl tooreset hello ağ arabirimi Azure Windows hangi hello uzak bağlantı sorunu gidermek için VM, gösterilmektedir.

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]
## <a name="reset-network-interface"></a>Ağ arabirimi Sıfırla

### <a name="for-classic-vms"></a>Klasik VM'ler için

tooreset ağ arabirimi, aşağıdaki adımları izleyin:

1.  Toohello Git [Azure portal]( https://ms.portal.azure.com).
2.  Seçin **sanal makineleri (Klasik)**.
3.  Sanal makine seçin hello etkilenen.
4.  Seçin **IP adreslerini**.
5.  Merhaba, **özel IP atama** değil **statik**, çok değiştirme**statik**.
6.  Değişiklik hello **IP adresi** hello alt kullanılabilir tooanother IP adresi.
7.  Kaydet'i seçin.
8.  Merhaba sanal makine tooinitialize hello yeni NIC toohello sistem yeniden başlatılır.
9.  TooRDP tooyour makine deneyin. İsterseniz başarılı olursa, hello özel IP adresi geri toohello özgün değiştirebilirsiniz. Aksi takdirde, tutabilirsiniz. 

### <a name="for-vms-deployed-in-resource-group-model"></a>Kaynak grubu modelde dağıtılan VM'ler için

1.  Toohello Git [Azure portal]( https://ms.portal.azure.com).
2.  Sanal makine seçin hello etkilenen.
3.  Seçin **ağ arabirimleri**.
4.  Ağ arabirimi, makineyle ilişkili hello seçin
5.  Seçin **IP yapılandırmaları**.
6.  Başlangıç IP adresi seçin. 
7.  Merhaba, **özel IP atama** değil **statik**, çok değiştirme**statik**.
8.  Değişiklik hello **IP adresi** hello alt kullanılabilir tooanother IP adresi.
9. Merhaba sanal makine tooinitialize hello yeni NIC toohello sistem yeniden başlatılır.
10. TooRDP tooyour makine deneyin. İsterseniz başarılı olursa, hello özel IP adresi geri toohello özgün değiştirebilirsiniz. Aksi takdirde, tutabilirsiniz. 

## <a name="delete-hello-unavailable-nics"></a>Silme kullanılamayan NICs hello
Uzak Masaüstü toohello makine yapabilecekleriniz sonra hello eski NIC'ler tooavoid hello olası sorunu silmeniz gerekir:

1.  Aygıt Yöneticisi'ni açın.
2.  Seçin **Görünüm** > **gizli aygıtları göster**.
3.  Seçin **ağ bağdaştırıcıları**. 
4.  "Microsoft Hyper-V ağ bağdaştırıcısı" adlı hello bağdaştırıcıları denetleyin.
5.  Gri renkte bağdaştırıcıyı kullanılamaz görebilirsiniz. Merhaba bağdaştırıcısına sağ tıklayın ve ardından Kaldır'ı seçin.

    ![Merhaba NIC Hello görüntüsü](media/reset-network-interface/nicpage.png)

    > [!NOTE]
    > Yalnızca hello adı "Microsoft Hyper-V ağ bağdaştırıcısı" Merhaba kullanılamaz bağdaştırıcıları kaldırın. Diğer gizli bağdaştırıcıları hello birini kaldırırsanız, ek sorunlar neden olabilir.
    >
    >

6.  Şimdi tüm kullanılamaz bağdaştırıcısı sisteminizden temizlenmesini.