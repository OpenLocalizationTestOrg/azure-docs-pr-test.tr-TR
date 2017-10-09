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
# <a name="set-up-hello-source-environment-physical-server-tooazure"></a><span data-ttu-id="3bb8c-103">Merhaba kaynak ortamını (fiziksel sunucu tooAzure) ayarlama</span><span class="sxs-lookup"><span data-stu-id="3bb8c-103">Set up hello source environment (physical server tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3bb8c-104">VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="3bb8c-104">VMware tooAzure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="3bb8c-105">Fiziksel tooAzure</span><span class="sxs-lookup"><span data-stu-id="3bb8c-105">Physical tooAzure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="3bb8c-106">Bu makalede nasıl tooset Azure'da Windows veya Linux çalıştıran fiziksel sunucuları çoğaltıyor, şirket içi ortamına toostart ayarlama.</span><span class="sxs-lookup"><span data-stu-id="3bb8c-106">This article describes how tooset up your on-premises environment toostart replicating physical servers running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3bb8c-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3bb8c-107">Prerequisites</span></span>

<span data-ttu-id="3bb8c-108">Merhaba makale, zaten sahip olduğunuz varsayılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="3bb8c-108">hello article assumes that you already have:</span></span>
1. <span data-ttu-id="3bb8c-109">Merhaba kurtarma Hizmetleri kasasına [Azure portal](http://portal.azure.com "Azure portal").</span><span class="sxs-lookup"><span data-stu-id="3bb8c-109">A Recovery Services vault in hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
3. <span data-ttu-id="3bb8c-110">Hangi tooinstall hello yapılandırma sunucusu fiziksel bilgisayarda.</span><span class="sxs-lookup"><span data-stu-id="3bb8c-110">A physical computer on which tooinstall hello configuration server.</span></span>

### <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="3bb8c-111">Yapılandırma sunucusunun en düşük gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="3bb8c-111">Configuration server minimum requirements</span></span>
<span data-ttu-id="3bb8c-112">Aşağıdaki tablonun hello hello en düşük donanım, yazılım ve yapılandırma sunucusu için ağ gereksinimleri listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="3bb8c-112">hello following table lists hello minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="3bb8c-113">HTTPS tabanlı proxy sunucuları hello yapılandırma sunucusu tarafından desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="3bb8c-113">HTTPS-based proxy servers are not supported by hello configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="3bb8c-114">Koruma hedeflerinizi seçme</span><span class="sxs-lookup"><span data-stu-id="3bb8c-114">Choose your protection goals</span></span>

1. <span data-ttu-id="3bb8c-115">Toohello Hello Azure portal, Git **kurtarma Hizmetleri** dikey kasaları ve kasanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="3bb8c-115">In hello Azure portal, go toohello **Recovery Services** vaults blade and select your vault.</span></span>
2. <span data-ttu-id="3bb8c-116">Merhaba, **kaynak** hello kasasının menüsünü **Başlarken** > **Site Recovery** > **1. adım: hazırlama Altyapı** > **koruma hedefi**.</span><span class="sxs-lookup"><span data-stu-id="3bb8c-116">In hello **Resource** menu of hello vault, click **Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Hedefleri seçme](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. <span data-ttu-id="3bb8c-118">İçinde **koruma hedefi**seçin **tooAzure** ve **değil sanallaştırılmış/diğer**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="3bb8c-118">In **Protection goal**, select **tooAzure** and **Not virtualized/Other**, and then click **OK**.</span></span>

    ![Hedefleri seçme](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-hello-source-environment"></a><span data-ttu-id="3bb8c-120">Merhaba kaynak ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="3bb8c-120">Set up hello source environment</span></span>

1. <span data-ttu-id="3bb8c-121">İçinde **kaynağı**,'ı tıklatın, bir yapılandırma sunucusu yoksa **+ yapılandırma sunucusu** tooadd biri.</span><span class="sxs-lookup"><span data-stu-id="3bb8c-121">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** tooadd one.</span></span>

  ![Kaynağı ayarlama](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. <span data-ttu-id="3bb8c-123">Merhaba, **Sunucu Ekle** dikey penceresinde denetleyin **yapılandırma sunucusu** görünür **sunucu türü**.</span><span class="sxs-lookup"><span data-stu-id="3bb8c-123">In hello **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="3bb8c-124">Merhaba Site Recovery birleşik Kurulumu yükleme dosyasını indirin.</span><span class="sxs-lookup"><span data-stu-id="3bb8c-124">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="3bb8c-125">Merhaba kasa kayıt anahtarını indirin.</span><span class="sxs-lookup"><span data-stu-id="3bb8c-125">Download hello vault registration key.</span></span> <span data-ttu-id="3bb8c-126">Birleşik Kurulumu çalıştırdığınızda hello kayıt anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="3bb8c-126">You need hello registration key when you run Unified Setup.</span></span> <span data-ttu-id="3bb8c-127">Merhaba anahtar, oluşturulduktan sonra beş gün boyunca geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="3bb8c-127">hello key is valid for five days after you generate it.</span></span>

    ![Kaynağı ayarlama](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. <span data-ttu-id="3bb8c-129">Merhaba yapılandırma sunucusu olarak kullandığınız hello makine üzerinde çalışan **Azure Site Recovery birleşik Kurulumu** tooinstall hello yapılandırma sunucusu, hello işlem sunucusu ve hello ana hedef sunucusunda.</span><span class="sxs-lookup"><span data-stu-id="3bb8c-129">On hello machine you’re using as hello configuration server, run **Azure Site Recovery Unified Setup** tooinstall hello configuration server, hello process server, and hello master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="3bb8c-130">Kurulumu çalıştırma Azure Site Recovery birleşik</span><span class="sxs-lookup"><span data-stu-id="3bb8c-130">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="3bb8c-131">Bilgisayarınızın sistem saati Hello saat beş dakikadan yerel saat dışına ise yapılandırma sunucusu kaydı başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="3bb8c-131">Configuration server registration fails if hello time on your computer's system clock is more than five minutes off of local time.</span></span> <span data-ttu-id="3bb8c-132">Sistem saatinizi bir [saat sunucusu](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) hello yüklemeyi başlatmadan önce.</span><span class="sxs-lookup"><span data-stu-id="3bb8c-132">Synchronize your system clock with a [time server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting hello installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="3bb8c-133">bir komut satırı Hello yapılandırma sunucusuna yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="3bb8c-133">hello configuration server can be installed via a command line.</span></span> <span data-ttu-id="3bb8c-134">Daha fazla bilgi için bkz: [komut satırı araçlarını kullanarak yükleme yapılandırma sunucusu](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="3bb8c-134">For more information, see [Installing configuration server using command-line tools](http://aka.ms/installconfigsrv).</span></span>


## <a name="common-issues"></a><span data-ttu-id="3bb8c-135">Genel sorunlar</span><span class="sxs-lookup"><span data-stu-id="3bb8c-135">Common issues</span></span>

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="3bb8c-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3bb8c-136">Next steps</span></span>

<span data-ttu-id="3bb8c-137">Sonraki adım içerir [hedef ortamınızı ayarlarken](./site-recovery-prepare-target-physical-to-azure.md) azure'da.</span><span class="sxs-lookup"><span data-stu-id="3bb8c-137">Next step involves [setting up your target environment](./site-recovery-prepare-target-physical-to-azure.md) in Azure.</span></span>
