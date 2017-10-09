---
title: AWS tooAzure gelen aaaMigrate VM'ler | Microsoft Docs
description: "Çalışan nasıl toomigrate sanal makineleri bu makalede Azure Site RECOVERY'yi kullanarak Amazon Web Hizmetleri (AWS) tooAzure içinde."
services: site-recovery
documentationcenter: 
author: bsiva
manager: jwhit
editor: 
ms.assetid: ddb412fd-32a8-4afa-9e39-738b11b91118
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: c99b781ec9cca5b8f9a847d3fc48408062b120b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-tooazure-with-azure-site-recovery"></a><span data-ttu-id="aa278-103">Amazon Web Hizmetleri (AWS) tooAzure Azure Site Recovery ile sanal makineleri geçirme</span><span class="sxs-lookup"><span data-stu-id="aa278-103">Migrate virtual machines in Amazon Web Services (AWS) tooAzure with Azure Site Recovery</span></span>

<span data-ttu-id="aa278-104">Nasıl toomigrate AWS Windows hello tooAzure sanal makinelerle örnekleri bu makalede [Azure Site Recovery](site-recovery-overview.md) hizmet.</span><span class="sxs-lookup"><span data-stu-id="aa278-104">This article describes how toomigrate AWS Windows instances tooAzure virtual machines with hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="aa278-105">Geçiş, bir yük devretmeyi AWS tooAzure etkin değil.</span><span class="sxs-lookup"><span data-stu-id="aa278-105">Migration is effectively a failover from AWS tooAzure.</span></span> <span data-ttu-id="aa278-106">Yeniden çalışma makineler tooAWS olamaz ve devam eden çoğaltılmaz.</span><span class="sxs-lookup"><span data-stu-id="aa278-106">You can't failback machines tooAWS, and there's no ongoing replication.</span></span> <span data-ttu-id="aa278-107">Bu makalede hello Azure portalı içinde geçiş için hello adımları açıklar ve hello yönergeler için temel alan [bir fiziksel makine tooAzure çoğaltma](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="aa278-107">This article describes hello steps for migration in hello Azure portal, and are based on hello instructions for [replicating a physical machine tooAzure](site-recovery-vmware-to-azure.md).</span></span>

<span data-ttu-id="aa278-108">Tüm yorumlarınızı ve sorularınızı bu makalenin veya hello hello altındaki sonrası [Azure kurtarma Hizmetleri Forumu](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="aa278-108">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="aa278-109">Desteklenen işletim sistemleri</span><span class="sxs-lookup"><span data-stu-id="aa278-109">Supported operating systems</span></span>

<span data-ttu-id="aa278-110">Site Recovery tüm işletim sistemleri aşağıdaki hello çalıştıran kullanılan toomigrate EC2 örnekleri olabilir:</span><span class="sxs-lookup"><span data-stu-id="aa278-110">Site Recovery can be used toomigrate EC2 instances running any of hello following operating systems:</span></span>

- <span data-ttu-id="aa278-111">Windows (yalnızca 64 bit)</span><span class="sxs-lookup"><span data-stu-id="aa278-111">Windows(64 bit only)</span></span>
    - <span data-ttu-id="aa278-112">Windows Server 2008 R2 SP1 + (Citrix PV sürücüleri veya yalnızca AWS PV sürücüler.</span><span class="sxs-lookup"><span data-stu-id="aa278-112">Windows Server 2008 R2 SP1+ (Citrix PV drivers or AWS PV drivers only.</span></span> <span data-ttu-id="aa278-113">**RedHat PV sürücüleri çalışan örnekleri desteklenmez**) Windows Server 2012 Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="aa278-113">**Instances running RedHat PV drivers are not supported**) Windows Server 2012 Windows Server 2012 R2</span></span>
- <span data-ttu-id="aa278-114">Linux (yalnızca 64 bit)</span><span class="sxs-lookup"><span data-stu-id="aa278-114">Linux (64 bit only)</span></span>
    - <span data-ttu-id="aa278-115">Red Hat Enterprise Linux 6.7 (yalnızca HVM sanallaştırılmış örnekleri)</span><span class="sxs-lookup"><span data-stu-id="aa278-115">Red Hat Enterprise Linux 6.7 (HVM virtualized instances only)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa278-116">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="aa278-116">Prerequisites</span></span>

<span data-ttu-id="aa278-117">İşte bu dağıtım için gerekenler:</span><span class="sxs-lookup"><span data-stu-id="aa278-117">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="aa278-118">**Yapılandırma sunucusu**: Windows Server 2012 R2 çalıştıran bir Amazon EC2 VM hello yapılandırma sunucusu olarak dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="aa278-118">**Configuration server**: An Amazon EC2 VM running Windows Server 2012 R2 is deployed as hello configuration server.</span></span> <span data-ttu-id="aa278-119">Merhaba yapılandırma sunucusu dağıtırken varsayılan olarak, hello diğer Azure Site Recovery bileşenleri (işlem sunucusu ve ana hedef sunucusu) yüklenir.</span><span class="sxs-lookup"><span data-stu-id="aa278-119">By default, hello other Azure Site Recovery components (process server and master target server) are installed when you deploy hello configuration server.</span></span> <span data-ttu-id="aa278-120">Bu makalede hello Azure portalı içinde geçiş için hello adımları açıklar ve hello yönergeler için temel alan [daha fazla bilgi edinin](site-recovery-components.md)</span><span class="sxs-lookup"><span data-stu-id="aa278-120">This article describes hello steps for migration in hello Azure portal, and are based on hello instructions for  [Learn more](site-recovery-components.md)</span></span>

* <span data-ttu-id="aa278-121">**EC2 örnekleri**: toomigrate istediğiniz Amazon EC2 sanal makineleri örnekleri hello.</span><span class="sxs-lookup"><span data-stu-id="aa278-121">**EC2 instances**: hello Amazon EC2 virtual machines instances that you want toomigrate.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="aa278-122">Dağıtım adımları</span><span class="sxs-lookup"><span data-stu-id="aa278-122">Deployment steps</span></span>

1. <span data-ttu-id="aa278-123">Kurtarma Hizmetleri kasası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="aa278-123">Create a Recovery Services vault.</span></span>
2. <span data-ttu-id="aa278-124">Merhaba EC2 örneklerinizi güvenlik grubunun yapılandırılan kuralları tooallow iletişim toomigrate ve toodeploy hello yapılandırma sunucusu planlama hello örneği istediğiniz hello EC2 örneği arasında olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="aa278-124">hello Security Group of your EC2 instances should have rules configured tooallow communication between hello EC2 instance that you want toomigrate, and hello instance on which you plan toodeploy hello Configuration Server.</span></span>

3. <span data-ttu-id="aa278-125">Merhaba üzerinde aynı Amazon sanal özel bulut olarak EC2 örneklerinizi ASR yapılandırma sunucusu dağıtın.</span><span class="sxs-lookup"><span data-stu-id="aa278-125">On hello same Amazon Virtual Private Cloud as your EC2 instances, deploy an ASR configuration server.</span></span> <span data-ttu-id="aa278-126">Merhaba VMware başvurmak / fiziksel tooAzure önkoşulları yapılandırma sunucusu dağıtım gereksinimleri.</span><span class="sxs-lookup"><span data-stu-id="aa278-126">Refer hello VMware / Physical tooAzure prerequisites for configuration server deployment requirements.</span></span>

    ![DeployCS](./media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  <span data-ttu-id="aa278-128">Yapılandırma sunucusu AWS içinde dağıtılır ve, Kurtarma Hizmetleri kasasına kayıtlı sonra hello yapılandırma sunucusu ve Site Recovery altyapısı bölümünde işlem sunucusunu aşağıda gösterildiği gibi görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="aa278-128">Once your configuration server is deployed in AWS and registered with your Recovery Services vault, you should see hello configuration server and process server under Site Recovery infrastructure as shown below:</span></span>

    ![CSinVault](./media/site-recovery-migrate-aws-to-azure/migration_pic3.png)

5. <span data-ttu-id="aa278-130">Merhaba yapılandırma sunucusu dağıttıktan sonra (Bunun için too15 minustes sürebilir tooappear), onu hello VM'ler ile toomigrate istediğiniz iletişim kurabildiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="aa278-130">After you've deployed hello configuration server (it might take up too15 minustes for it tooappear), validate that it can communicate with hello VMs that you want toomigrate.</span></span>

6. <span data-ttu-id="aa278-131">[Çoğaltma ayarlarını belirleme](site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="aa278-131">[Set up replication settings](site-recovery-setup-replication-settings-vmware.md).</span></span>

7. <span data-ttu-id="aa278-132">Çoğaltmayı etkinleştirme: Merhaba toomigrate istediğiniz VM'ler için çoğaltma etkinleştirme.</span><span class="sxs-lookup"><span data-stu-id="aa278-132">Enable replication: Enable replication for hello VMs you want toomigrate.</span></span> <span data-ttu-id="aa278-133">Merhaba EC2 Konsolu'ndan alabilirsiniz hello özel IP adresleri kullanan hello EC2 örneklerini bulabilir.</span><span class="sxs-lookup"><span data-stu-id="aa278-133">You can discover hello EC2 instances using hello private IP addresses, which you can get from hello EC2 console.</span></span>

    ![SelectVM](./media/site-recovery-migrate-aws-to-azure/migration_pic4.png)

8. <span data-ttu-id="aa278-135">Merhaba EC2 örnekleri korumalı ve hello çoğaltma tooAzure tamamlandıktan sonra [bir yük devretme testi](site-recovery-test-failover-to-azure.md) toovalidate uygulamanızın performansını azure'da.</span><span class="sxs-lookup"><span data-stu-id="aa278-135">Once hello EC2 instances have been protected and hello replication tooAzure is complete, [run a Test Failover](site-recovery-test-failover-to-azure.md) toovalidate your application's performance in Azure.</span></span>

    ![TFI](./media/site-recovery-migrate-aws-to-azure/migration_pic5.png)

9. <span data-ttu-id="aa278-137">Bir yük devretme AWS tooAzure her VM için çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="aa278-137">Run a Failover from AWS tooAzure for each VM.</span></span> <span data-ttu-id="aa278-138">İsteğe bağlı olarak, bir kurtarma planı oluşturun ve AWS tooAzure birden çok sanal makine bir yük devretme, toomigrate çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="aa278-138">Optionally, you can create a recovery plan and run a Failover, toomigrate multiple virtual machines from AWS tooAzure.</span></span> <span data-ttu-id="aa278-139">[Daha fazla bilgi edinin](site-recovery-create-recovery-plans.md) kurtarma planları hakkında.</span><span class="sxs-lookup"><span data-stu-id="aa278-139">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

10. <span data-ttu-id="aa278-140">Geçiş için bir yük devretme toocommit gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="aa278-140">For migration, you don't need toocommit a failover.</span></span> <span data-ttu-id="aa278-141">Merhaba tam geçiş seçeneği bunun yerine, seçtiğiniz her makine için toomigrate istiyor.</span><span class="sxs-lookup"><span data-stu-id="aa278-141">Instead, you select hello Complete Migration option for each machine you want toomigrate.</span></span> <span data-ttu-id="aa278-142">Geçişi tamamlamak eylemin Hello hello geçiş işlemini tamamlanır, hello makinesi için çoğaltma kaldırır ve Site Recovery hello makine için faturalama durdurur.</span><span class="sxs-lookup"><span data-stu-id="aa278-142">hello Complete Migration action finishes up hello migration process, removes replication for hello machine, and stops Site Recovery billing for hello machine.</span></span>

    ![Geçiş](./media/site-recovery-migrate-aws-to-azure/migration_pic6.png)

## <a name="next-steps"></a><span data-ttu-id="aa278-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="aa278-144">Next steps</span></span>

- <span data-ttu-id="aa278-145">[Geçirilen makinelerin tooenable çoğaltma hazırlama](site-recovery-azure-to-azure-after-migration.md) tooanother bölge olağanüstü durum kurtarma gerekir.</span><span class="sxs-lookup"><span data-stu-id="aa278-145">[Prepare migrated machines tooenable replication](site-recovery-azure-to-azure-after-migration.md) tooanother region for disaster recovery needs.</span></span>
- <span data-ttu-id="aa278-146">[Azure sanal makinelerini çoğaltarak](site-recovery-azure-to-azure.md) iş yüklerinizi korumaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="aa278-146">Start protecting your workloads by [replicating Azure virtual machines.](site-recovery-azure-to-azure.md)</span></span>
