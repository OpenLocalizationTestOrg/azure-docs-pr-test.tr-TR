---
title: "aaaInstall hello VMware tooAzure çoğaltma için Mobility hizmetini | Microsoft Docs"
description: "Bu makalede nasıl Mobility Hizmeti Aracısı VMware tooAzure çoğaltma hello Azure Site Recovery hizmeti ile Merhaba tooinstall açıklanmaktadır."
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
ms.openlocfilehash: d3b7bc9c4d84d13317e0b0b47adcf38e8c41d0bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-install-hello-mobility-service"></a><span data-ttu-id="aabef-103">10. adım: hello Mobility hizmetini yükleme</span><span class="sxs-lookup"><span data-stu-id="aabef-103">Step 10: Install hello Mobility service</span></span>


<span data-ttu-id="aabef-104">Bu makalede nasıl çoğaltırken tooconfigure kaynak ve hedef ayarları şirket içi VMware sanal makineleri tooAzure hello kullanarak [Azure Site Recovery](site-recovery-overview.md) hello Azure portal hizmeti.</span><span class="sxs-lookup"><span data-stu-id="aabef-104">This article describes how tooconfigure source and target settings when replicating on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="aabef-105">Merhaba Mobility hizmeti bir makinede veri Yazar yakalar ve bunları toohello işlem sunucusuna iletir.</span><span class="sxs-lookup"><span data-stu-id="aabef-105">hello Mobility service captures data writes on a machine, and forwards them toohello process server.</span></span> <span data-ttu-id="aabef-106">Tooreplicate tooAzure istediğiniz her makinede yüklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="aabef-106">It should be installed on each machine that you want tooreplicate tooAzure.</span></span>

<span data-ttu-id="aabef-107">Çoğaltma etkin olduğunda hello Site kurtarma işlemi sunucusundan bir anında yükleme kullanarak hello Mobility hizmeti el ile yükleyin veya System Center Configuration Manager aracını kullanın.</span><span class="sxs-lookup"><span data-stu-id="aabef-107">You can install hello Mobility service manual, using a push installation from hello Site Recovery process server when replication is enabled, or use a tool System Center Configuration Manager.</span></span> <span data-ttu-id="aabef-108">Anında yükleme kullanırsanız, çoğaltma etkin olduğunda hello hizmeti hello VM üzerinde yüklendi.</span><span class="sxs-lookup"><span data-stu-id="aabef-108">If you use push installation, hello service is installed on hello VM when replication is enabled.</span></span>

<span data-ttu-id="aabef-109">POST açıklamaları ve soruları hello altındaki bu makalenin veya hello [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="aabef-109">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="aabef-110">El ile yükleme</span><span class="sxs-lookup"><span data-stu-id="aabef-110">Install manually</span></span>

1. <span data-ttu-id="aabef-111">Merhaba denetleyin [Önkoşullar](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) el ile yükleme.</span><span class="sxs-lookup"><span data-stu-id="aabef-111">Check hello [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="aabef-112">İzleyin [bu yönergeleri](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) hello portal'ı kullanarak el ile yükleme.</span><span class="sxs-lookup"><span data-stu-id="aabef-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using hello portal.</span></span>
3. <span data-ttu-id="aabef-113">Merhaba komut satırından tooinstall tercih ederseniz, izleyin [bu yönergeleri](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="aabef-113">If you prefer tooinstall from hello command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-hello-process-server"></a><span data-ttu-id="aabef-114">Merhaba işlem sunucusundan yükle</span><span class="sxs-lookup"><span data-stu-id="aabef-114">Install from hello process server</span></span>

<span data-ttu-id="aabef-115">Bir sanal makine için çoğaltmayı etkinleştirdiğinizde toopush hello Mobility hizmeti yüklemesi hello işlem sunucusundan istiyorsanız, hello işlem sunucusu tooaccess hello VM tarafından kullanılan bir hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="aabef-115">If you want toopush hello Mobility service installation from hello process server when you enable replication for a VM, you need an account that can be used by hello process server tooaccess hello VM.</span></span> <span data-ttu-id="aabef-116">Merhaba hesabı yalnızca hello gönderme yüklemesi için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="aabef-116">hello account is only used for hello push installation.</span></span>

1. <span data-ttu-id="aabef-117">Olması [hesap oluşturup](vmware-walkthrough-prepare-vmware.md) gönderme yüklemesi için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="aabef-117">You should have [created an account](vmware-walkthrough-prepare-vmware.md) that can be used for push installation.</span></span> <span data-ttu-id="aabef-118">Ardından, Site Recovery dağıtımı sırasında kaynak ayarlarını yapılandırırken toouse istediğiniz hello hesabının de belirtin.</span><span class="sxs-lookup"><span data-stu-id="aabef-118">You then specify hello account you want toouse when you configure source settings during Site Recovery deployment.</span></span>
2. <span data-ttu-id="aabef-119">Ardından izleyin [bu yönergeleri](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) toopush hello Mobility hizmeti Windows veya Linux çalıştıran sanal makineleri üzerinde istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="aabef-119">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want toopush hello Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-methods"></a><span data-ttu-id="aabef-120">Diğer yöntemleri</span><span class="sxs-lookup"><span data-stu-id="aabef-120">Other methods</span></span>

<span data-ttu-id="aabef-121">Daha fazla bilgi edinmek [hello Mobility hizmetinin Yapılandırma Yöneticisi'ni kullanarak yükleme](site-recovery-install-mobility-service-using-sccm.md), veya kullanarak [Azure Otomasyonu DSC](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="aabef-121">Learn more about [installing hello Mobility service using Configuration Manager](site-recovery-install-mobility-service-using-sccm.md), or using [Azure Automation DSC](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aabef-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="aabef-122">Next steps</span></span>

<span data-ttu-id="aabef-123">Çok Git[adım 11: çoğaltmasını etkinleştir](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="aabef-123">Go too[Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>
