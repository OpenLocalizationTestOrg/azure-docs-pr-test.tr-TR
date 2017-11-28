---
title: "Kaynak ortamı (fiziksel sunucuları azure'a) ayarlama | Microsoft Docs"
description: "Bu makalede, Azure'da Windows veya Linux çalıştıran fiziksel sunucuları çoğaltıyor başlatmak için şirket içi ortamınızı ayarlayın açıklar."
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
ms.openlocfilehash: 49b9d2e21dbcb612828a25f21ed4382327d6f64c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-the-source-environment-physical-server-to-azure"></a><span data-ttu-id="6ba54-103">Kaynak ortamı (Azure fiziksel sunucuya) ayarlama</span><span class="sxs-lookup"><span data-stu-id="6ba54-103">Set up the source environment (physical server to Azure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6ba54-104">Vmware’den Azure’a</span><span class="sxs-lookup"><span data-stu-id="6ba54-104">VMware to Azure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="6ba54-105">Azure için fiziksel</span><span class="sxs-lookup"><span data-stu-id="6ba54-105">Physical to Azure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="6ba54-106">Bu makalede, Azure'da Windows veya Linux çalıştıran fiziksel sunucuları çoğaltıyor başlatmak için şirket içi ortamınızı ayarlayın açıklar.</span><span class="sxs-lookup"><span data-stu-id="6ba54-106">This article describes how to set up your on-premises environment to start replicating physical servers running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ba54-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6ba54-107">Prerequisites</span></span>

<span data-ttu-id="6ba54-108">Makale, zaten sahip olduğunuz varsayılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="6ba54-108">The article assumes that you already have:</span></span>
1. <span data-ttu-id="6ba54-109">Kurtarma Hizmetleri kasası [Azure portal](http://portal.azure.com "Azure portal").</span><span class="sxs-lookup"><span data-stu-id="6ba54-109">A Recovery Services vault in the [Azure portal](http://portal.azure.com "Azure portal").</span></span>
3. <span data-ttu-id="6ba54-110">Yapılandırma sunucusu yüklemek için fiziksel bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="6ba54-110">A physical computer on which to install the configuration server.</span></span>

### <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="6ba54-111">Yapılandırma sunucusunun en düşük gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="6ba54-111">Configuration server minimum requirements</span></span>
<span data-ttu-id="6ba54-112">Aşağıdaki tabloda, en düşük donanım, yazılım ve yapılandırma sunucusu için ağ gereksinimleri listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="6ba54-112">The following table lists the minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="6ba54-113">HTTPS tabanlı proxy sunucuları yapılandırma sunucusu tarafından desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="6ba54-113">HTTPS-based proxy servers are not supported by the configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="6ba54-114">Koruma hedeflerinizi seçme</span><span class="sxs-lookup"><span data-stu-id="6ba54-114">Choose your protection goals</span></span>

1. <span data-ttu-id="6ba54-115">Azure portalında Git **kurtarma Hizmetleri** dikey kasaları ve kasanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="6ba54-115">In the Azure portal, go to the **Recovery Services** vaults blade and select your vault.</span></span>
2. <span data-ttu-id="6ba54-116">İçinde **kaynak** kasasının menüsünü **Başlarken** > **Site Recovery** > **1. adım: altyapıyı hazırlama** > **koruma hedefi**.</span><span class="sxs-lookup"><span data-stu-id="6ba54-116">In the **Resource** menu of the vault, click **Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Hedefleri seçme](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. <span data-ttu-id="6ba54-118">İçinde **koruma hedefi**seçin **için Azure** ve **değil sanallaştırılmış/diğer**ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="6ba54-118">In **Protection goal**, select **To Azure** and **Not virtualized/Other**, and then click **OK**.</span></span>

    ![Hedefleri seçme](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-the-source-environment"></a><span data-ttu-id="6ba54-120">Kaynak ortamı ayarlama</span><span class="sxs-lookup"><span data-stu-id="6ba54-120">Set up the source environment</span></span>

1. <span data-ttu-id="6ba54-121">İçinde **kaynağı**,'ı tıklatın, bir yapılandırma sunucusu yoksa **+ yapılandırma sunucusu** eklemesini.</span><span class="sxs-lookup"><span data-stu-id="6ba54-121">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** to add one.</span></span>

  ![Kaynağı ayarlama](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. <span data-ttu-id="6ba54-123">İçinde **Sunucu Ekle** dikey penceresinde denetleyin **yapılandırma sunucusu** görünür **sunucu türü**.</span><span class="sxs-lookup"><span data-stu-id="6ba54-123">In the **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="6ba54-124">Site Recovery birleşik Kurulumu yükleme dosyasını indirin.</span><span class="sxs-lookup"><span data-stu-id="6ba54-124">Download the Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="6ba54-125">Kasa kayıt anahtarını indir</span><span class="sxs-lookup"><span data-stu-id="6ba54-125">Download the vault registration key.</span></span> <span data-ttu-id="6ba54-126">Birleşik Kurulum'u çalıştırdığınızda, kayıt anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="6ba54-126">You need the registration key when you run Unified Setup.</span></span> <span data-ttu-id="6ba54-127">Anahtar, oluşturulduktan sonra beş gün boyunca geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="6ba54-127">The key is valid for five days after you generate it.</span></span>

    ![Kaynağı ayarlama](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. <span data-ttu-id="6ba54-129">Yapılandırma sunucusu olarak kullandığınız makine üzerinde çalışan **Azure Site Recovery birleşik Kurulumu** yapılandırma sunucusuna işlem sunucusu ve ana hedef sunucusu yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="6ba54-129">On the machine you’re using as the configuration server, run **Azure Site Recovery Unified Setup** to install the configuration server, the process server, and the master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="6ba54-130">Kurulumu çalıştırma Azure Site Recovery birleşik</span><span class="sxs-lookup"><span data-stu-id="6ba54-130">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="6ba54-131">Bilgisayarınızın sistem saati beş dakikadan yerel saat dışına ise yapılandırma sunucusu kaydı başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="6ba54-131">Configuration server registration fails if the time on your computer's system clock is more than five minutes off of local time.</span></span> <span data-ttu-id="6ba54-132">Sistem saatinizi bir [saat sunucusu](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) yüklemeyi başlatmadan önce.</span><span class="sxs-lookup"><span data-stu-id="6ba54-132">Synchronize your system clock with a [time server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting the installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="6ba54-133">Yapılandırma sunucusu bir komut satırı yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="6ba54-133">The configuration server can be installed via a command line.</span></span> <span data-ttu-id="6ba54-134">Daha fazla bilgi için bkz: [komut satırı araçlarını kullanarak yükleme yapılandırma sunucusu](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="6ba54-134">For more information, see [Installing configuration server using command-line tools](http://aka.ms/installconfigsrv).</span></span>


## <a name="common-issues"></a><span data-ttu-id="6ba54-135">Genel sorunlar</span><span class="sxs-lookup"><span data-stu-id="6ba54-135">Common issues</span></span>

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="6ba54-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6ba54-136">Next steps</span></span>

<span data-ttu-id="6ba54-137">Sonraki adım içerir [hedef ortamınızı ayarlarken](./site-recovery-prepare-target-physical-to-azure.md) azure'da.</span><span class="sxs-lookup"><span data-stu-id="6ba54-137">Next step involves [setting up your target environment](./site-recovery-prepare-target-physical-to-azure.md) in Azure.</span></span>
