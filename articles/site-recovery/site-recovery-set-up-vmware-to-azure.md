---
title: "Merhaba kaynak ortamını (VMware tooAzure) ayarlama | Microsoft Docs"
description: "Bu makalede, VMware sanal çoğaltma, şirket içi ortamına toostart yukarı tooset tooAzure nasıl makineleri açıklanmaktadır."
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
ms.openlocfilehash: cbeeffc1061b11223e12ff3e237fa7e55b999aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-vmware-tooazure"></a>Merhaba kaynak ortamını (VMware tooAzure) ayarlama
> [!div class="op_single_selector"]
> * [VMware tooAzure](./site-recovery-set-up-vmware-to-azure.md)
> * [Fiziksel tooAzure](./site-recovery-set-up-physical-to-azure.md)

Çalışan sanal çoğaltma, şirket içi ortamına toostart yukarı tooset nasıl makineleri bu makalede VMware tooAzure üzerinde.

## <a name="prerequisites"></a>Ön koşullar

Merhaba makale, zaten oluşturduğunuzu varsayar:
- Kurtarma Hizmetleri kasasına hello [Azure portal](http://portal.azure.com "Azure portal").
- Adanmış bir hesap için kullanılan, VMware vcenter [otomatik bulma](./site-recovery-vmware-to-azure.md).
- Hangi tooinstall hello yapılandırma sunucusunda bir sanal makine.

## <a name="configuration-server-minimum-requirements"></a>Yapılandırma sunucusunun en düşük gereksinimleri
yüksek oranda kullanılabilir bir VMware sanal makineye Hello yapılandırma sunucu yazılımı dağıtılmalıdır. Aşağıdaki tablonun hello hello en düşük donanım, yazılım ve yapılandırma sunucusu için ağ gereksinimleri listelenmektedir.
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> HTTPS tabanlı proxy sunucuları hello yapılandırma sunucusu tarafından desteklenmez.

## <a name="choose-your-protection-goals"></a>Koruma hedeflerinizi seçme

1. Toohello Hello Azure portal, Git **kurtarma Hizmetleri** kasa dikey ve kasanızı seçin.
2. Merhaba kaynak menüsünde hello kasasının çok Git**Başlarken** > **Site Recovery** > **1. adım: altyapıyı hazırlama**  >  **Koruma hedefi**.

    ![Hedefleri seçme](./media/site-recovery-set-up-vmware-to-azure/choose-goals.png)
3. İçinde **koruma hedefi**seçin **tooAzure**ve seçin **Evet, VMware vSphere hiper yönetici ile**. Daha sonra, **Tamam**'a tıklayın.

    ![Hedefleri seçme](./media/site-recovery-set-up-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>Merhaba kaynak ortamını ayarlama
Merhaba kaynak ortamını ayarlama iki ana etkinlik içerir:

- Yükleme ve yapılandırma sunucusu Site Kurtarma ile kaydedin.
- Şirket içi sanal makinelerinizi Site Recovery tooyour şirket içi VMware vCenter veya vSphere EXSi konak bağlanarak bulur.

### <a name="step-1-install-and-register-a-configuration-server"></a>Adım 1: Yükleme ve yapılandırma sunucusuna kaydedin

1. Tıklatın **1. adım: altyapıyı hazırlama** > **kaynak**. İçinde **kaynağı**,'ı tıklatın, bir yapılandırma sunucusu yoksa **+ yapılandırma sunucusu** tooadd biri.

    ![Kaynağı ayarlama](./media/site-recovery-set-up-vmware-to-azure/set-source1.png)
2. Merhaba üzerinde **Sunucu Ekle** dikey penceresinde denetleyin **yapılandırma sunucusu** görünür **sunucu türü**.
4. Merhaba Site Recovery birleşik Kurulumu yükleme dosyasını indirin.
5. Merhaba kasa kayıt anahtarını indirin. Birleşik Kurulumu çalıştırdığınızda hello kayıt anahtarı gerekir. Merhaba anahtar, oluşturulduktan sonra beş gün boyunca geçerlidir.

    ![Kaynağı ayarlama](./media/site-recovery-set-up-vmware-to-azure/set-source2.png)
6. Merhaba yapılandırma sunucusu olarak kullandığınız hello makine üzerinde çalışan **Azure Site Recovery birleşik Kurulumu** tooinstall hello yapılandırma sunucusu, hello işlem sunucusu ve hello ana hedef sunucusunda.

#### <a name="run-azure-site-recovery-unified-setup"></a>Kurulumu çalıştırma Azure Site Recovery birleşik

> [!TIP]
> Bilgisayarınızın sistem saati Hello saat beş dakikadan tarafından yerel saatten farklıysa yapılandırma sunucusu kaydı başarısız olur. Sistem saatinizi bir [saat sunucusu](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) hello yüklemeyi başlatmadan önce.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> komut satırı Hello yapılandırma sunucusuna yüklenebilir. Daha fazla bilgi için bkz: [komut satırı araçlarını kullanarak yükleme hello yapılandırma sunucusu](http://aka.ms/installconfigsrv).

#### <a name="add-hello-vmware-account-for-automatic-discovery"></a>Otomatik bulma için Hello VMware hesabı ekleyin

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="step-2-add-a-vcenter"></a>2. adım: bir vCenter ekleme
tooallow Azure Site Recovery toodiscover şirket içi ortamınızda çalışan sanal makineler, VMware vCenter sunucusu veya Site Recovery ile vSphere ESXi konakları tooconnect gerekir.

Seçin **+ vCenter** toostart bir VMware vCenter sunucusu veya bir VMware vSphere ESXi konağı bağlanma.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]


## <a name="common-issues"></a>Genel sorunlar
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a>Sonraki adımlar
[Hedef ortamınızı ayarlama](./site-recovery-prepare-target-vmware-to-azure.md) azure'da.
