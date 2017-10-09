---
title: "Merhaba kaynak ortamını (fiziksel sunucuları tooAzure) ayarlama | Microsoft Docs"
description: "Bu makalede nasıl tooset Azure'da Windows veya Linux çalıştıran fiziksel sunucuları çoğaltıyor, şirket içi ortamına toostart ayarlama."
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
ms.openlocfilehash: d4702265bf36910015685d2bba99d6e577531bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-physical-server-tooazure"></a>Merhaba kaynak ortamını (fiziksel sunucu tooAzure) ayarlama
> [!div class="op_single_selector"]
> * [VMware tooAzure](./site-recovery-set-up-vmware-to-azure.md)
> * [Fiziksel tooAzure](./site-recovery-set-up-physical-to-azure.md)

Bu makalede nasıl tooset Azure'da Windows veya Linux çalıştıran fiziksel sunucuları çoğaltıyor, şirket içi ortamına toostart ayarlama.

## <a name="prerequisites"></a>Ön koşullar

Merhaba makale, zaten sahip olduğunuz varsayılmaktadır:
1. Merhaba kurtarma Hizmetleri kasasına [Azure portal](http://portal.azure.com "Azure portal").
3. Hangi tooinstall hello yapılandırma sunucusu fiziksel bilgisayarda.

### <a name="configuration-server-minimum-requirements"></a>Yapılandırma sunucusunun en düşük gereksinimleri
Aşağıdaki tablonun hello hello en düşük donanım, yazılım ve yapılandırma sunucusu için ağ gereksinimleri listelenmektedir.
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> HTTPS tabanlı proxy sunucuları hello yapılandırma sunucusu tarafından desteklenmez.

## <a name="choose-your-protection-goals"></a>Koruma hedeflerinizi seçme

1. Toohello Hello Azure portal, Git **kurtarma Hizmetleri** dikey kasaları ve kasanızı seçin.
2. Merhaba, **kaynak** hello kasasının menüsünü **Başlarken** > **Site Recovery** > **1. adım: hazırlama Altyapı** > **koruma hedefi**.

    ![Hedefleri seçme](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. İçinde **koruma hedefi**seçin **tooAzure** ve **değil sanallaştırılmış/diğer**ve ardından **Tamam**.

    ![Hedefleri seçme](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-hello-source-environment"></a>Merhaba kaynak ortamını ayarlama

1. İçinde **kaynağı**,'ı tıklatın, bir yapılandırma sunucusu yoksa **+ yapılandırma sunucusu** tooadd biri.

  ![Kaynağı ayarlama](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. Merhaba, **Sunucu Ekle** dikey penceresinde denetleyin **yapılandırma sunucusu** görünür **sunucu türü**.
4. Merhaba Site Recovery birleşik Kurulumu yükleme dosyasını indirin.
5. Merhaba kasa kayıt anahtarını indirin. Birleşik Kurulumu çalıştırdığınızda hello kayıt anahtarı gerekir. Merhaba anahtar, oluşturulduktan sonra beş gün boyunca geçerlidir.

    ![Kaynağı ayarlama](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. Merhaba yapılandırma sunucusu olarak kullandığınız hello makine üzerinde çalışan **Azure Site Recovery birleşik Kurulumu** tooinstall hello yapılandırma sunucusu, hello işlem sunucusu ve hello ana hedef sunucusunda.

#### <a name="run-azure-site-recovery-unified-setup"></a>Kurulumu çalıştırma Azure Site Recovery birleşik

> [!TIP]
> Bilgisayarınızın sistem saati Hello saat beş dakikadan yerel saat dışına ise yapılandırma sunucusu kaydı başarısız olur. Sistem saatinizi bir [saat sunucusu](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) hello yüklemeyi başlatmadan önce.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> bir komut satırı Hello yapılandırma sunucusuna yüklenebilir. Daha fazla bilgi için bkz: [komut satırı araçlarını kullanarak yükleme yapılandırma sunucusu](http://aka.ms/installconfigsrv).


## <a name="common-issues"></a>Genel sorunlar

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a>Sonraki adımlar

Sonraki adım içerir [hedef ortamınızı ayarlarken](./site-recovery-prepare-target-physical-to-azure.md) azure'da.
