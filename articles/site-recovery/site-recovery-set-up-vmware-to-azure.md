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
# <a name="set-up-hello-source-environment-vmware-tooazure"></a><span data-ttu-id="8fe46-103">Merhaba kaynak ortamını (VMware tooAzure) ayarlama</span><span class="sxs-lookup"><span data-stu-id="8fe46-103">Set up hello source environment (VMware tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8fe46-104">VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="8fe46-104">VMware tooAzure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="8fe46-105">Fiziksel tooAzure</span><span class="sxs-lookup"><span data-stu-id="8fe46-105">Physical tooAzure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="8fe46-106">Çalışan sanal çoğaltma, şirket içi ortamına toostart yukarı tooset nasıl makineleri bu makalede VMware tooAzure üzerinde.</span><span class="sxs-lookup"><span data-stu-id="8fe46-106">This article describes how tooset up your on-premises environment toostart replicating virtual machines running on VMware tooAzure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8fe46-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8fe46-107">Prerequisites</span></span>

<span data-ttu-id="8fe46-108">Merhaba makale, zaten oluşturduğunuzu varsayar:</span><span class="sxs-lookup"><span data-stu-id="8fe46-108">hello article assumes that you have already created:</span></span>
- <span data-ttu-id="8fe46-109">Kurtarma Hizmetleri kasasına hello [Azure portal](http://portal.azure.com "Azure portal").</span><span class="sxs-lookup"><span data-stu-id="8fe46-109">A Recovery Services Vault in hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="8fe46-110">Adanmış bir hesap için kullanılan, VMware vcenter [otomatik bulma](./site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="8fe46-110">A dedicated account in your VMware vCenter that can be used for [automatic discovery](./site-recovery-vmware-to-azure.md).</span></span>
- <span data-ttu-id="8fe46-111">Hangi tooinstall hello yapılandırma sunucusunda bir sanal makine.</span><span class="sxs-lookup"><span data-stu-id="8fe46-111">A virtual machine on which tooinstall hello configuration server.</span></span>

## <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="8fe46-112">Yapılandırma sunucusunun en düşük gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="8fe46-112">Configuration server minimum requirements</span></span>
<span data-ttu-id="8fe46-113">yüksek oranda kullanılabilir bir VMware sanal makineye Hello yapılandırma sunucu yazılımı dağıtılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8fe46-113">hello configuration server software should be deployed on a highly available VMware virtual machine.</span></span> <span data-ttu-id="8fe46-114">Aşağıdaki tablonun hello hello en düşük donanım, yazılım ve yapılandırma sunucusu için ağ gereksinimleri listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="8fe46-114">hello following table lists hello minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="8fe46-115">HTTPS tabanlı proxy sunucuları hello yapılandırma sunucusu tarafından desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="8fe46-115">HTTPS-based proxy servers are not supported by hello configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="8fe46-116">Koruma hedeflerinizi seçme</span><span class="sxs-lookup"><span data-stu-id="8fe46-116">Choose your protection goals</span></span>

1. <span data-ttu-id="8fe46-117">Toohello Hello Azure portal, Git **kurtarma Hizmetleri** kasa dikey ve kasanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="8fe46-117">In hello Azure portal, go toohello **Recovery Services** vault blade and select your vault.</span></span>
2. <span data-ttu-id="8fe46-118">Merhaba kaynak menüsünde hello kasasının çok Git**Başlarken** > **Site Recovery** > **1. adım: altyapıyı hazırlama**  >  **Koruma hedefi**.</span><span class="sxs-lookup"><span data-stu-id="8fe46-118">On hello resource menu of hello vault, go too**Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Hedefleri seçme](./media/site-recovery-set-up-vmware-to-azure/choose-goals.png)
3. <span data-ttu-id="8fe46-120">İçinde **koruma hedefi**seçin **tooAzure**ve seçin **Evet, VMware vSphere hiper yönetici ile**.</span><span class="sxs-lookup"><span data-stu-id="8fe46-120">In **Protection goal**, select **tooAzure**, and choose **Yes, with VMware vSphere Hypervisor**.</span></span> <span data-ttu-id="8fe46-121">Daha sonra, **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8fe46-121">Then click **OK**.</span></span>

    ![Hedefleri seçme](./media/site-recovery-set-up-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a><span data-ttu-id="8fe46-123">Merhaba kaynak ortamını ayarlama</span><span class="sxs-lookup"><span data-stu-id="8fe46-123">Set up hello source environment</span></span>
<span data-ttu-id="8fe46-124">Merhaba kaynak ortamını ayarlama iki ana etkinlik içerir:</span><span class="sxs-lookup"><span data-stu-id="8fe46-124">Setting up hello source environment involves two main activities:</span></span>

- <span data-ttu-id="8fe46-125">Yükleme ve yapılandırma sunucusu Site Kurtarma ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="8fe46-125">Install and register a configuration server with Site Recovery.</span></span>
- <span data-ttu-id="8fe46-126">Şirket içi sanal makinelerinizi Site Recovery tooyour şirket içi VMware vCenter veya vSphere EXSi konak bağlanarak bulur.</span><span class="sxs-lookup"><span data-stu-id="8fe46-126">Discover your on-premises virtual machines by connecting Site Recovery tooyour on-premises VMware vCenter or vSphere EXSi hosts.</span></span>

### <a name="step-1-install-and-register-a-configuration-server"></a><span data-ttu-id="8fe46-127">Adım 1: Yükleme ve yapılandırma sunucusuna kaydedin</span><span class="sxs-lookup"><span data-stu-id="8fe46-127">Step 1: Install and register a configuration server</span></span>

1. <span data-ttu-id="8fe46-128">Tıklatın **1. adım: altyapıyı hazırlama** > **kaynak**.</span><span class="sxs-lookup"><span data-stu-id="8fe46-128">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span> <span data-ttu-id="8fe46-129">İçinde **kaynağı**,'ı tıklatın, bir yapılandırma sunucusu yoksa **+ yapılandırma sunucusu** tooadd biri.</span><span class="sxs-lookup"><span data-stu-id="8fe46-129">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** tooadd one.</span></span>

    ![Kaynağı ayarlama](./media/site-recovery-set-up-vmware-to-azure/set-source1.png)
2. <span data-ttu-id="8fe46-131">Merhaba üzerinde **Sunucu Ekle** dikey penceresinde denetleyin **yapılandırma sunucusu** görünür **sunucu türü**.</span><span class="sxs-lookup"><span data-stu-id="8fe46-131">On hello **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="8fe46-132">Merhaba Site Recovery birleşik Kurulumu yükleme dosyasını indirin.</span><span class="sxs-lookup"><span data-stu-id="8fe46-132">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="8fe46-133">Merhaba kasa kayıt anahtarını indirin.</span><span class="sxs-lookup"><span data-stu-id="8fe46-133">Download hello vault registration key.</span></span> <span data-ttu-id="8fe46-134">Birleşik Kurulumu çalıştırdığınızda hello kayıt anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="8fe46-134">You need hello registration key when you run Unified Setup.</span></span> <span data-ttu-id="8fe46-135">Merhaba anahtar, oluşturulduktan sonra beş gün boyunca geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="8fe46-135">hello key is valid for five days after you generate it.</span></span>

    ![Kaynağı ayarlama](./media/site-recovery-set-up-vmware-to-azure/set-source2.png)
6. <span data-ttu-id="8fe46-137">Merhaba yapılandırma sunucusu olarak kullandığınız hello makine üzerinde çalışan **Azure Site Recovery birleşik Kurulumu** tooinstall hello yapılandırma sunucusu, hello işlem sunucusu ve hello ana hedef sunucusunda.</span><span class="sxs-lookup"><span data-stu-id="8fe46-137">On hello machine you’re using as hello configuration server, run **Azure Site Recovery Unified Setup** tooinstall hello configuration server, hello process server, and hello master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="8fe46-138">Kurulumu çalıştırma Azure Site Recovery birleşik</span><span class="sxs-lookup"><span data-stu-id="8fe46-138">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="8fe46-139">Bilgisayarınızın sistem saati Hello saat beş dakikadan tarafından yerel saatten farklıysa yapılandırma sunucusu kaydı başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="8fe46-139">Configuration server registration fails if hello time on your computer's system clock differs from local time by more than five minutes.</span></span> <span data-ttu-id="8fe46-140">Sistem saatinizi bir [saat sunucusu](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) hello yüklemeyi başlatmadan önce.</span><span class="sxs-lookup"><span data-stu-id="8fe46-140">Synchronize your system clock with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting hello installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="8fe46-141">komut satırı Hello yapılandırma sunucusuna yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="8fe46-141">hello configuration server can be installed via command line.</span></span> <span data-ttu-id="8fe46-142">Daha fazla bilgi için bkz: [komut satırı araçlarını kullanarak yükleme hello yapılandırma sunucusu](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="8fe46-142">For more information, see [Installing hello configuration server using Command-line tools](http://aka.ms/installconfigsrv).</span></span>

#### <a name="add-hello-vmware-account-for-automatic-discovery"></a><span data-ttu-id="8fe46-143">Otomatik bulma için Hello VMware hesabı ekleyin</span><span class="sxs-lookup"><span data-stu-id="8fe46-143">Add hello VMware account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="step-2-add-a-vcenter"></a><span data-ttu-id="8fe46-144">2. adım: bir vCenter ekleme</span><span class="sxs-lookup"><span data-stu-id="8fe46-144">Step 2: Add a vCenter</span></span>
<span data-ttu-id="8fe46-145">tooallow Azure Site Recovery toodiscover şirket içi ortamınızda çalışan sanal makineler, VMware vCenter sunucusu veya Site Recovery ile vSphere ESXi konakları tooconnect gerekir.</span><span class="sxs-lookup"><span data-stu-id="8fe46-145">tooallow Azure Site Recovery toodiscover virtual machines running in your on-premises environment, you need tooconnect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span>

<span data-ttu-id="8fe46-146">Seçin **+ vCenter** toostart bir VMware vCenter sunucusu veya bir VMware vSphere ESXi konağı bağlanma.</span><span class="sxs-lookup"><span data-stu-id="8fe46-146">Select **+vCenter** toostart connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]


## <a name="common-issues"></a><span data-ttu-id="8fe46-147">Genel sorunlar</span><span class="sxs-lookup"><span data-stu-id="8fe46-147">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="8fe46-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8fe46-148">Next steps</span></span>
<span data-ttu-id="8fe46-149">[Hedef ortamınızı ayarlama](./site-recovery-prepare-target-vmware-to-azure.md) azure'da.</span><span class="sxs-lookup"><span data-stu-id="8fe46-149">[Set up your target environment](./site-recovery-prepare-target-vmware-to-azure.md) in Azure.</span></span>
