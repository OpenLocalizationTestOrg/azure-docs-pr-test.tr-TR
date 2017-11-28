---
title: "VMware Mobility hizmeti için Azure çoğaltmayı yükleme | Microsoft Docs"
description: "Bu makalede, Azure Site Recovery hizmeti ile Azure çoğaltma VMware için Mobility hizmeti aracısı yüklemeyi açıklar."
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
ms.openlocfilehash: bc520bd2ea54208889861a7a3b275e3008a05d53
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="step-10-install-the-mobility-service"></a><span data-ttu-id="3e283-103">10. adım: mobilite hizmeti yükleme</span><span class="sxs-lookup"><span data-stu-id="3e283-103">Step 10: Install the Mobility service</span></span>


<span data-ttu-id="3e283-104">Bu makale, şirket içi VMware sanal makinelerini Azure'a çoğaltırken kaynak ve hedef ayarlarını yapılandırmak açıklamaktadır kullanarak [Azure Site Recovery](site-recovery-overview.md) Azure portalında hizmet.</span><span class="sxs-lookup"><span data-stu-id="3e283-104">This article describes how to configure source and target settings when replicating on-premises VMware virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="3e283-105">Mobility hizmetinin yakalar bir makinede veri yazar ve işlem sunucusuna gönderir.</span><span class="sxs-lookup"><span data-stu-id="3e283-105">The Mobility service captures data writes on a machine, and forwards them to the process server.</span></span> <span data-ttu-id="3e283-106">Azure'a çoğaltmak istediğiniz her makinede yüklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3e283-106">It should be installed on each machine that you want to replicate to Azure.</span></span>

<span data-ttu-id="3e283-107">Mobility hizmeti el ile çoğaltma etkin olduğunda Site kurtarma işlemi sunucusundan bir anında yükleme kullanarak yükleyin veya System Center Configuration Manager aracını kullanın.</span><span class="sxs-lookup"><span data-stu-id="3e283-107">You can install the Mobility service manual, using a push installation from the Site Recovery process server when replication is enabled, or use a tool System Center Configuration Manager.</span></span> <span data-ttu-id="3e283-108">Anında yükleme kullanırsanız, çoğaltma etkin hizmet VM yüklenir.</span><span class="sxs-lookup"><span data-stu-id="3e283-108">If you use push installation, the service is installed on the VM when replication is enabled.</span></span>

<span data-ttu-id="3e283-109">POST açıklamaları ve soruları alt bu makalenin veya üzerinde [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="3e283-109">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="install-manually"></a><span data-ttu-id="3e283-110">El ile yükleme</span><span class="sxs-lookup"><span data-stu-id="3e283-110">Install manually</span></span>

1. <span data-ttu-id="3e283-111">Denetleme [Önkoşullar](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) el ile yükleme.</span><span class="sxs-lookup"><span data-stu-id="3e283-111">Check the [prerequisites](site-recovery-vmware-to-azure-install-mob-svc.md#prerequisites) for manual installation.</span></span>
2. <span data-ttu-id="3e283-112">İzleyin [bu yönergeleri](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) Portalı'nı kullanarak el ile yükleme.</span><span class="sxs-lookup"><span data-stu-id="3e283-112">Follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui) for manual installation using the portal.</span></span>
3. <span data-ttu-id="3e283-113">Komut satırından yüklemeyi tercih ediyorsanız izleyin [bu yönergeleri](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span><span class="sxs-lookup"><span data-stu-id="3e283-113">If you prefer to install from the command line, follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt).</span></span>

## <a name="install-from-the-process-server"></a><span data-ttu-id="3e283-114">İşlem sunucusundan yükle</span><span class="sxs-lookup"><span data-stu-id="3e283-114">Install from the process server</span></span>

<span data-ttu-id="3e283-115">Bir sanal makine için çoğaltmayı etkinleştirdiğinizde mobilite hizmeti yükleme işlem sunucusundan itmek istiyorsanız, VM erişmek için işlem sunucusu tarafından kullanılan bir hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3e283-115">If you want to push the Mobility service installation from the process server when you enable replication for a VM, you need an account that can be used by the process server to access the VM.</span></span> <span data-ttu-id="3e283-116">Hesabı yalnızca gönderme yüklemesi için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3e283-116">The account is only used for the push installation.</span></span>

1. <span data-ttu-id="3e283-117">Olması [hesap oluşturup](vmware-walkthrough-prepare-vmware.md) gönderme yüklemesi için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3e283-117">You should have [created an account](vmware-walkthrough-prepare-vmware.md) that can be used for push installation.</span></span> <span data-ttu-id="3e283-118">Ardından, Site Recovery dağıtımı sırasında kaynak ayarlarını yapılandırırken kullanmak istediğiniz hesabı belirt</span><span class="sxs-lookup"><span data-stu-id="3e283-118">You then specify the account you want to use when you configure source settings during Site Recovery deployment.</span></span>
2. <span data-ttu-id="3e283-119">Ardından izleyin [bu yönergeleri](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) Mobility hizmeti Windows veya Linux çalıştıran sanal makinelerin itmek istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="3e283-119">Then follow [these instructions](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery) if you want to push the Mobility service on VMs running Windows or Linux.</span></span>

## <a name="other-methods"></a><span data-ttu-id="3e283-120">Diğer yöntemleri</span><span class="sxs-lookup"><span data-stu-id="3e283-120">Other methods</span></span>

<span data-ttu-id="3e283-121">Daha fazla bilgi edinmek [Yapılandırma Yöneticisi'ni kullanarak Mobility hizmeti yükleniyor](site-recovery-install-mobility-service-using-sccm.md), veya kullanarak [Azure Otomasyonu DSC](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="3e283-121">Learn more about [installing the Mobility service using Configuration Manager](site-recovery-install-mobility-service-using-sccm.md), or using [Azure Automation DSC](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e283-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3e283-122">Next steps</span></span>

<span data-ttu-id="3e283-123">Git [adım 11: çoğaltmasını etkinleştir](vmware-walkthrough-enable-replication.md)</span><span class="sxs-lookup"><span data-stu-id="3e283-123">Go to [Step 11: Enable replication](vmware-walkthrough-enable-replication.md)</span></span>
