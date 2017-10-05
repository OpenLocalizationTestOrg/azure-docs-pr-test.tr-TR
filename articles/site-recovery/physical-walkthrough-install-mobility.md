---
title: "Mobility hizmeti fiziksel sunucu için Azure çoğaltmayı yükleme | Microsoft Docs"
description: "Bu makalede, Azure Site Recovery hizmeti ile Azure'a çoğaltma fiziksel sunucularda Mobility hizmeti aracısı yüklemeyi açıklar."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 3189fbcd-6b5b-4ffb-b5a9-e2080c37f9d9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: d73267d7a64221a3138af19e9a2d5dd15809b927
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="step-9-install-the-mobility-service"></a><span data-ttu-id="de804-103">9. adım: mobilite hizmeti yükleme</span><span class="sxs-lookup"><span data-stu-id="de804-103">Step 9: Install the Mobility service</span></span>


<span data-ttu-id="de804-104">Bu makale, şirket içi Windows/Linux fiziksel sunucuları Azure'a çoğaltırken Mobility hizmeti bileşeninin yükleneceği açıklamaktadır kullanarak [Azure Site Recovery](site-recovery-overview.md) Azure portalında hizmet.</span><span class="sxs-lookup"><span data-stu-id="de804-104">This article describes how to install the Mobility service component when replicating on-premises Windows/Linux physical servers to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="de804-105">Mobility hizmetinin yakalar bir makinede veri yazar ve işlem sunucusuna gönderir.</span><span class="sxs-lookup"><span data-stu-id="de804-105">The Mobility service captures data writes on a machine, and forwards them to the process server.</span></span> <span data-ttu-id="de804-106">Azure'a çoğaltmak istediğiniz her sunucuya yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="de804-106">It should be installed on each server that you want to replicate to Azure.</span></span>

<span data-ttu-id="de804-107">Mobility hizmeti el ile yükleyebilirsiniz veya çoğaltma etkin olduğunda Site kurtarma işlemi sunucusundan bir anında yükleme veya System Center Configuration Manager gibi bir araç kullanarak.</span><span class="sxs-lookup"><span data-stu-id="de804-107">You can install the Mobility service manually, or using a push installation from the Site Recovery process server when replication is enabled, or using a tool such as System Center Configuration Manager.</span></span> <span data-ttu-id="de804-108">Anında yükleme kullanırsanız, hizmeti çoğaltma etkinleştirdiğinizde, sunucu üzerinde yüklü.</span><span class="sxs-lookup"><span data-stu-id="de804-108">If you use push installation, the service is installed on the server when you enable replication.</span></span>

<span data-ttu-id="de804-109">POST açıklamaları ve soruları alt bu makalenin veya üzerinde [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="de804-109">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="de804-110">El ile yükleme</span><span class="sxs-lookup"><span data-stu-id="de804-110">Install manually</span></span>

1. <span data-ttu-id="de804-111">Denetleme [Önkoşullar](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) el ile yükleme.</span><span class="sxs-lookup"><span data-stu-id="de804-111">Check the [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="de804-112">İzleyin [bu yönergeleri](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) Portalı'nı kullanarak el ile yükleme.</span><span class="sxs-lookup"><span data-stu-id="de804-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using the portal.</span></span>
3. <span data-ttu-id="de804-113">Komut satırından yüklemeyi tercih ediyorsanız izleyin [bu yönergeleri](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="de804-113">If you prefer to install from the command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-the-process-server"></a><span data-ttu-id="de804-114">İşlem sunucusundan yükle</span><span class="sxs-lookup"><span data-stu-id="de804-114">Install from the process server</span></span>

<span data-ttu-id="de804-115">Bir makine için çoğaltma etkinleştirdiğinizde mobilite hizmeti yükleme işlem sunucusundan itmek istiyorsanız, makine erişmek için işlem sunucusu tarafından kullanılan bir hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="de804-115">If you want to push the Mobility service installation from the process server when you enable replication for a machine, you need an account that can be used by the process server to access the machine.</span></span> <span data-ttu-id="de804-116">Hesabı yalnızca gönderme yüklemesi için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="de804-116">The account is only used for the push installation.</span></span>

1. <span data-ttu-id="de804-117">Bir hesabı oluşturmadıysanız, bu yönergeleri kullanarak bunu yapın:</span><span class="sxs-lookup"><span data-stu-id="de804-117">If you haven't created an account, do so using these guidelines:</span></span>

    - <span data-ttu-id="de804-118">Bir etki alanı veya yerel hesabı kullanın</span><span class="sxs-lookup"><span data-stu-id="de804-118">You can use a domain or local account</span></span>
    - <span data-ttu-id="de804-119">Windows, bir etki alanı hesabı kullanmıyorsanız yerel makine üzerinde uzak kullanıcı erişimi denetimini devre dışı bırakmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="de804-119">For Windows, if you're not using a domain account, you need to disable Remote User Access control on the local machine.</span></span> <span data-ttu-id="de804-120">Bu, altında kayıttaki yapmak için **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, DWORD girdisi ekleyin **LocalAccountTokenFilterPolicy**, 1 değerine sahip.</span><span class="sxs-lookup"><span data-stu-id="de804-120">To do this, in the register under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, add the DWORD entry **LocalAccountTokenFilterPolicy**, with a value of 1.</span></span>
    - <span data-ttu-id="de804-121">CLI üzerinden için Windows kayıt defteri girdisini eklemek istiyorsanız, yazın:</span><span class="sxs-lookup"><span data-stu-id="de804-121">If you want to add the registry entry for Windows from a CLI, type:</span></span>

        ```
        REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.
        ```

    - <span data-ttu-id="de804-122">Linux için hesabın kaynak Linux sunucusu kökünde olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="de804-122">For Linux, the account should be root on the source Linux server.</span></span>

2. <span data-ttu-id="de804-123">Ardından izleyin [bu yönergeleri](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) Mobility hizmeti Windows veya Linux çalıştıran sanal makinelerin itmek istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="de804-123">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want to push the Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-installation-methods"></a><span data-ttu-id="de804-124">Diğer yükleme yöntemleri</span><span class="sxs-lookup"><span data-stu-id="de804-124">Other installation methods</span></span>

- <span data-ttu-id="de804-125">[Hakkında bilgi edinin](site-recovery-install-mobility-service-using-sccm.md) Yapılandırma Yöneticisi'ni kullanarak Mobility hizmeti yükleniyor</span><span class="sxs-lookup"><span data-stu-id="de804-125">[Learn about](site-recovery-install-mobility-service-using-sccm.md) installing the Mobility service using Configuration Manager</span></span>
- <span data-ttu-id="de804-126">[Hakkında bilgi edinin](site-recovery-automate-mobility-service-install.md) Azure Otomasyonu DSC'ye yükleme.</span><span class="sxs-lookup"><span data-stu-id="de804-126">[Learn about](site-recovery-automate-mobility-service-install.md) installing with Azure Automation DSC.</span></span>


## <a name="next-steps"></a><span data-ttu-id="de804-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="de804-127">Next steps</span></span>

<span data-ttu-id="de804-128">Git [adım 10: çoğaltmasını etkinleştir](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="de804-128">Go to [Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>
