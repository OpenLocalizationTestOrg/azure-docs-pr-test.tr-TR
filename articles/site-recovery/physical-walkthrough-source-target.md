---
title: "Merhaba kaynak ve hedef Azure Site Recovery ile fiziksel sunucu çoğaltma tooAzure için aaaSet | Microsoft Docs"
description: "Merhaba adımları tooset hello Azure Site Recovery hizmeti ile fiziksel sunucuları tooAzure depolama çoğaltma için kaynak ve hedef ayarlarını özetler"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 2e3d03bc-4e53-4590-8a01-f702d3cc9500
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: e75ef23174d77509bf54380eba8f251a7337a45f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-hello-source-and-target-for-physical-server-replication-tooazure"></a>7. adım: hello kaynak ve hedef fiziksel sunucu çoğaltma tooAzure için ayarlama

Bu makalede nasıl çoğaltırken tooconfigure kaynak ve hedef ayarları şirket içi fiziksel sunucuların tooAzure hello kullanarak [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.

POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Merhaba kaynak ortamını ayarlama

Merhaba yapılandırma sunucusunu ayarlamayı, hello kasaya kaydetmek ve makineleri Bul

1. Tıklatın **Site kurtarma** > **1. adım: altyapıyı hazırlama** > **kaynak**.
2. Yapılandırma sunucusu yoksa, tıklatın **+ yapılandırma sunucusu**.
3. İçinde **Sunucu Ekle**, denetleyin **yapılandırma sunucusu** görünür **sunucu türü**.
4. Merhaba Site Recovery birleşik Kurulumu yükleme dosyasını indirin.
5. Merhaba kasa kayıt anahtarını indirin. Birleşik Kurulum'u çalıştırdığınızda bu gerekir. Merhaba anahtar, oluşturulduktan sonra beş gün boyunca geçerlidir.

   ![Kaynağı ayarlama](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a>Merhaba kasasına Hello yapılandırma sunucusuna kaydedin

, Önce hello aşağıdaki başlayın, ardından birleşik Kurulum tooinstall hello yapılandırma sunucusu, hello işlem sunucusu ve hello ana hedef sunucusunda çalıştırın. Merhaba video hello bileşenleri VMware VM tooAzure çoğaltma için kurulacağını açıklar. Ancak, hello aynı işlem fiziksel sunucu tooAzure çoğaltma için geçerli değil.

- Merhaba yapılandırma sunucusunda VM, o hello sistem saati ile eşitlenir emin olun bir [saat sunucusu](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Eşleşmelidir. Önde 15 dakika ise veya arkasında kurulum başarısız olabilir.
- Kurulum hello configuration server makinesinde yerel yönetici olarak çalıştırın.
- TLS 1.0 hello VM etkin olduğundan emin olun.


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> Merhaba yapılandırma sunucusu da yüklenebilir [hello komut satırından](http://aka.ms/installconfigsrv).




## <a name="set-up-hello-target-environment"></a>Merhaba hedef ortamını ayarlama

Merhaba hedef ortamını ayarlama önce bir Azure depolama hesabı ve sanal ağ kurulumu olduğundan emin olun.

1. Tıklatın **altyapıyı hazırlama** > **hedef**, ve hello toouse istediğiniz Azure aboneliğini seçin.
2. Belirtin, hedef dağıtım modeli Resource Manager tabanlı veya Klasik olup.
3. Site Recovery, bir veya birden çok uyumlu Azure depolama hesabınızın ve ağınızın olup olmadığını denetler.

   ![Hedef](./media/physical-walkthrough-source-target/gs-target.png)

4. Bir depolama hesabı veya ağı oluşturmadıysanız, tıklatın **+ depolama hesabı** veya **+ ağ**, toocreate bir Resource Manager hesabı ya da ağ satır içi.

## <a name="next-steps"></a>Sonraki adımlar

Çok Git[adım 8: bir çoğaltma ilkesini ayarlayın](physical-walkthrough-replication.md)
