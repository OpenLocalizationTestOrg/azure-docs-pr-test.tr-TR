---
title: "aaaInstall hello fiziksel sunucu tooAzure çoğaltma için Mobility hizmetini | Microsoft Docs"
description: "Bu makalede nasıl tooinstall hello Mobility Hizmeti Aracısı tooAzure hello Azure Site Recovery hizmeti ile çoğaltma fiziksel sunucularda açıklanmaktadır."
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
ms.openlocfilehash: 48fd2c0ffe67875ed446c8167c2ae7f90d3f537c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-install-hello-mobility-service"></a><span data-ttu-id="aeb20-103">9. adım: hello Mobility hizmetini yükleme</span><span class="sxs-lookup"><span data-stu-id="aeb20-103">Step 9: Install hello Mobility service</span></span>


<span data-ttu-id="aeb20-104">Bu makalede nasıl çoğaltırken tooinstall hello Mobility hizmeti bileşeninin Windows/Linux fiziksel sunucuları tooAzure hello kullanarak, şirket içi [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.</span><span class="sxs-lookup"><span data-stu-id="aeb20-104">This article describes how tooinstall hello Mobility service component when replicating on-premises Windows/Linux physical servers tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="aeb20-105">Merhaba Mobility hizmeti bir makinede veri Yazar yakalar ve bunları toohello işlem sunucusuna iletir.</span><span class="sxs-lookup"><span data-stu-id="aeb20-105">hello Mobility service captures data writes on a machine, and forwards them toohello process server.</span></span> <span data-ttu-id="aeb20-106">Tooreplicate tooAzure istediğiniz her sunucuda yüklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="aeb20-106">It should be installed on each server that you want tooreplicate tooAzure.</span></span>

<span data-ttu-id="aeb20-107">Merhaba Mobility hizmeti el ile yükleyebilirsiniz veya hello anında yüklemesinden kullanarak Site Recovery işlem çoğaltma etkinleştirildiğinde, sunucu veya System Center Configuration Manager gibi bir araç kullanarak.</span><span class="sxs-lookup"><span data-stu-id="aeb20-107">You can install hello Mobility service manually, or using a push installation from hello Site Recovery process server when replication is enabled, or using a tool such as System Center Configuration Manager.</span></span> <span data-ttu-id="aeb20-108">Anında yükleme kullanırsanız, çoğaltmayı etkinleştirme hello hizmet hello sunucusuna yüklenir.</span><span class="sxs-lookup"><span data-stu-id="aeb20-108">If you use push installation, hello service is installed on hello server when you enable replication.</span></span>

<span data-ttu-id="aeb20-109">POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="aeb20-109">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="aeb20-110">El ile yükleme</span><span class="sxs-lookup"><span data-stu-id="aeb20-110">Install manually</span></span>

1. <span data-ttu-id="aeb20-111">Merhaba denetleyin [Önkoşullar](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) el ile yükleme.</span><span class="sxs-lookup"><span data-stu-id="aeb20-111">Check hello [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="aeb20-112">İzleyin [bu yönergeleri](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) hello portal'ı kullanarak el ile yükleme.</span><span class="sxs-lookup"><span data-stu-id="aeb20-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using hello portal.</span></span>
3. <span data-ttu-id="aeb20-113">Merhaba komut satırından tooinstall tercih ederseniz, izleyin [bu yönergeleri](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="aeb20-113">If you prefer tooinstall from hello command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-hello-process-server"></a><span data-ttu-id="aeb20-114">Merhaba işlem sunucusundan yükle</span><span class="sxs-lookup"><span data-stu-id="aeb20-114">Install from hello process server</span></span>

<span data-ttu-id="aeb20-115">Bir makine için çoğaltma etkinleştirdiğinizde toopush hello Mobility hizmeti yüklemesi hello işlem sunucusundan istiyorsanız, hello işlem sunucusu tooaccess hello makine tarafından kullanılan bir hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="aeb20-115">If you want toopush hello Mobility service installation from hello process server when you enable replication for a machine, you need an account that can be used by hello process server tooaccess hello machine.</span></span> <span data-ttu-id="aeb20-116">Merhaba hesabı yalnızca hello gönderme yüklemesi için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="aeb20-116">hello account is only used for hello push installation.</span></span>

1. <span data-ttu-id="aeb20-117">Bir hesabı oluşturmadıysanız, bu yönergeleri kullanarak bunu yapın:</span><span class="sxs-lookup"><span data-stu-id="aeb20-117">If you haven't created an account, do so using these guidelines:</span></span>

    - <span data-ttu-id="aeb20-118">Bir etki alanı veya yerel hesabı kullanın</span><span class="sxs-lookup"><span data-stu-id="aeb20-118">You can use a domain or local account</span></span>
    - <span data-ttu-id="aeb20-119">Windows, bir etki alanı hesabı kullanmıyorsanız toodisable hello yerel makine üzerinde uzak kullanıcı erişim denetimi gerekir.</span><span class="sxs-lookup"><span data-stu-id="aeb20-119">For Windows, if you're not using a domain account, you need toodisable Remote User Access control on hello local machine.</span></span> <span data-ttu-id="aeb20-120">Bu, hello kaydetmek altında toodo **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, hello DWORD girdisi eklemek **LocalAccountTokenFilterPolicy**, 1 değerine sahip.</span><span class="sxs-lookup"><span data-stu-id="aeb20-120">toodo this, in hello register under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System**, add hello DWORD entry **LocalAccountTokenFilterPolicy**, with a value of 1.</span></span>
    - <span data-ttu-id="aeb20-121">CLI Windows'dan tooadd hello kayıt defteri girdisini isterseniz, yazın:</span><span class="sxs-lookup"><span data-stu-id="aeb20-121">If you want tooadd hello registry entry for Windows from a CLI, type:</span></span>

        ```
        REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1.
        ```

    - <span data-ttu-id="aeb20-122">Linux için kök hello kaynak Linux sunucuda hello hesabı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="aeb20-122">For Linux, hello account should be root on hello source Linux server.</span></span>

2. <span data-ttu-id="aeb20-123">Ardından izleyin [bu yönergeleri](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) toopush hello Mobility hizmeti Windows veya Linux çalıştıran sanal makineleri üzerinde istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="aeb20-123">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want toopush hello Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-installation-methods"></a><span data-ttu-id="aeb20-124">Diğer yükleme yöntemleri</span><span class="sxs-lookup"><span data-stu-id="aeb20-124">Other installation methods</span></span>

- <span data-ttu-id="aeb20-125">[Hakkında bilgi edinin](site-recovery-install-mobility-service-using-sccm.md) hello Mobility hizmetinin Yapılandırma Yöneticisi'ni kullanarak yükleme</span><span class="sxs-lookup"><span data-stu-id="aeb20-125">[Learn about](site-recovery-install-mobility-service-using-sccm.md) installing hello Mobility service using Configuration Manager</span></span>
- <span data-ttu-id="aeb20-126">[Hakkında bilgi edinin](site-recovery-automate-mobility-service-install.md) Azure Otomasyonu DSC'ye yükleme.</span><span class="sxs-lookup"><span data-stu-id="aeb20-126">[Learn about](site-recovery-automate-mobility-service-install.md) installing with Azure Automation DSC.</span></span>


## <a name="next-steps"></a><span data-ttu-id="aeb20-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="aeb20-127">Next steps</span></span>

<span data-ttu-id="aeb20-128">Çok Git[adım 10: çoğaltmasını etkinleştir](physical-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="aeb20-128">Go too[Step 10: Enable replication](physical-walkthrough-enable-replication.md)</span></span>
