---
title: " İşlem içinde Azure(Classic) çalıştıran bir sunucuyu yönetmek | Microsoft Docs"
description: "Bu makalede nasıl tooset yeniden çalışma işlemi Server(Classic) Azure içinde ayarlama."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: eadcc0236c77c9ebbbc885c4a7ee81098f1f4e72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-classic"></a>Azure (Klasik) çalışan bir işlem sunucusu yönetme
> [!div class="op_single_selector"]
> * [Azure Klasik](./site-recovery-vmware-setup-azure-ps-classic.md)
> * [Resource Manager](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

Yeniden çalışma sırasında hello Azure sanal ağ ve şirket içi ağınız arasında yüksek gecikme ise toodeploy Azure işlem sunucusu önerilir. Bu makalede nasıl ayarlamak, yapılandırabilir ve Azure'da çalışan hello işlem sunucuları yönetmek açıklanmaktadır.

> [!NOTE]
> Bu makalede Klasik hello dağıtım modeli olarak hello sanal makineler için yük devretme sırasında kullandıysanız kullanılan toobe ' dir. Resource Manager dağıtım modeli izleyin hello adımlarda hello olarak kullanılan, [nasıl tooset Yukarı & bir yeniden çalışma işlem sunucusu (Kaynak Yöneticisi) yapılandırın](./site-recovery-vmware-setup-azure-ps-resource-manager.md)

## <a name="prerequisites"></a>Ön koşullar

[!INCLUDE [site-recovery-vmware-process-server-prereq](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a>Azure üzerinde bir işlem sunucusu Dağıt

1. Azure Marketi'nde hello kullanarak bir sanal makine oluşturma **Microsoft Azure Site kurtarma işlemi Server V2** </br>
    ![Marketplace_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image.png)
2. Merhaba dağıtım modeli olarak seçtiğinizden emin olun **Klasik** </br>
  ![Marketplace_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/marketplace-ps-image-classic.png)
3. Merhaba oluşturma sanal makine Sihirbazı'nda > temel ayarları sağlamak hello sanal makineler üzerinde başarısız hello abonelik ve konumda toowhere seçin.</br>
  ![create_image_1](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-basic-info.png)
4. Bu hello sanal makineye bağlı olduğundan emin olun devredilen sanal makine üzerinde toohello Azure Virtual Network toowhich hello bağlı.</br>
  ![create_image_2](./media/site-recovery-vmware-setup-azure-ps-classic/azureps-classic-settings.png)
5. Merhaba işlem sunucusu sanal makine sağlandıktan sonra toolog gerekir ve hello yapılandırma sunucusu ile kaydedin.

> [!NOTE]
> toobe mümkün toouse bu işlem sunucunun yeniden çalışma için tooregister gereksinim duyduğunuz hello şirket içi yapılandırma sunucusu ile.

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a>Merhaba (Azure'da çalışan) işlem sunucusu tooa yapılandırma (şirket içi çalıştıran) sunucusu kaydetme

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a>Merhaba işlem sunucusu toolatest sürümüne yükseltme.

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a>Kaydı siliniyor hello (şirket içi çalıştıran) bir yapılandırma sunucusundan işlem (Azure'da çalışan) sunucusu

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
