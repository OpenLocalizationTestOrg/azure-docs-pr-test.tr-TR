---
title: " Azure (Kaynak Yöneticisi) çalışan bir işlem sunucusu yönetme | Microsoft Docs"
description: "Bu makalede Azure içinde bir yeniden çalışma yukarı tooset sunucu (Resource Manager) işleminin nasıl açıklanmaktadır."
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
ms.openlocfilehash: 70426b96095cc42befff6c4114fb56536284a667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-process-server-running-in-azure-resource-manager"></a>Azure (Kaynak Yöneticisi) çalışan bir işlem sunucusu yönetme
> [!div class="op_single_selector"]
> * [Resource Manager](./site-recovery-vmware-setup-azure-ps-resource-manager.md)
> * [Klasik](./site-recovery-vmware-setup-azure-ps-classic.md)

Yeniden çalışma sırasında hello Azure sanal ağ ve şirket içi ağınız arasında yüksek gecikme ise toodeploy işlem sunucusu azure'da önerilir. Bu makalede nasıl ayarlamak, yapılandırabilir ve Azure'da çalışan hello işlem sunucuları yönetmek açıklanmaktadır.

> [!NOTE]
> Bu makalede kullandıysanız kullanılan toobe olan **Resource Manager** hello sanal makineler yük devretme sırasında hello dağıtım modeli olarak. Kullandıysanız **Klasik** hello dağıtım modeli hello adımları [nasıl tooset Yukarı & bir yeniden çalışma işlem sunucusu (Klasik) yapılandırma](./site-recovery-vmware-setup-azure-ps-classic.md)

## <a name="prerequisites"></a>Ön koşullar

[!INCLUDE [site-recovery-vmware-process-server-prerequ](../../includes/site-recovery-vmware-azure-process-server-prereq.md)]

## <a name="deploy-a-process-server-on-azure"></a>Azure üzerinde bir işlem sunucusu Dağıt
1. Merhaba kasa içinde > **Site Recovery altyapısı** (altında hello "Manage" Başlık) > **yapılandırma sunucularına** ("İçin VMware ve fiziksel makineler" başlığı altında), hello yapılandırma sunucusu seçin.
2. Açılan hello yapılandırma sunucusu Ayrıntıları sayfasında tıklayın "+ sunucu işlemleri"

  ![İşlem sunucusu Galeri Ekle](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps.png)

3.  Merhaba üzerinde **işlem Sunucu Ekle** sayfasında, aşağıdaki değerleri seçin hello

  ![İşlem sunucusu galeri öğesi ekleme](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-1.png)
|**Alan adı**|**Değer**|
|-|-|
|İşlem sunucunuzu toodeploy istediğiniz yeri seçin|Merhaba değeri seçin **azure'da yeniden çalışma işlem sunucusu Dağıt** |
|Abonelik|Hello Azure hello sanal makineler üzerinde başarısız olduğu abonelik seçin|
|Kaynak Grubu|Bu işlem sunucusu bir kaynak grubu toodeploy oluşturabilir veya varolan bir kaynak grubunda toodeploy hello işlem sunucusu seçin|
|Konum|Hangi hello sanal makinelerine Hello Azure veri merkezi seçin içine devredilir burada|
|Azure Ağı|Select hello sanal makineleri hello Azure sanal Network(VNet) içine yük devredildi durumunda. Sanal makineler üzerinde birden fazla Azure Vnet başarısız olduysa, sonra VNet dağıtılan bir işlem sunucusu gerekir|

4. Merhaba rest hello işlem sunucusu için hello özelliklerinin doldurun

  ![İşlem sunucusu Özet ekleme](./media/site-recovery-vmware-setup-azure-ps-arm/add-ps-page-2.png)
|**Alan adı**|**Değer**|
|-|-|
|Sunucu adı|Görünen ad & işlem sunucusu sanal makinesi için ana bilgisayar adı|
| User Name|Bu sanal makinede yönetici hale bir kullanıcı adı|
|Depolama Hesabı|Merhaba hello sanal makinenin sanal diskin yerleştirildiği depolama hesabı adı|
|Alt ağ|Merhaba alt hello Azure VNet toowhich hello sanal makinenin bağlı|
| IP Adresi|Yukarı önyüklenir hello işlem sunucusu tooassume kez istediğiniz IP adresi|
5. Merhaba işlem sunucusu sanal makine dağıtma hello Tamam düğmesine toostart'ı tıklatın.

> [!NOTE]
> toobe mümkün toouse bu işlem sunucunun yeniden çalışma için tooregister gereksinim duyduğunuz hello şirket içi yapılandırma sunucusu ile.

## <a name="registering-hello-process-server-running-in-azure-tooa-configuration-server-running-on-premises"></a>Merhaba işlem (Azure'da çalışan) server tooa yapılandırma (şirket içi çalıştıran) sunucusu kaydetme

[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

## <a name="upgrading-hello-process-server-toolatest-version"></a>Merhaba işlem sunucusu toolatest sürümüne yükseltme.

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-upgrade-process-server.md)]

## <a name="unregistering-hello-process-server-running-in-azure-from-a-configuration-server-running-on-premises"></a>(Azure'da çalışan) hello işlem sunucusunu yapılandırma (şirket içi çalıştıran) bir sunucudan kaydı siliniyor

[!INCLUDE [site-recovery-vmware-unregister-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]
