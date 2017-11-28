---
title: "aaaUpgrade Site Recovery kasası tooan Azure kurtarma Hizmetleri kasası"
description: "Nasıl tooupgrade bir Azure Site Recovery kasası tooa kurtarma Hizmetleri kasası öğrenin"
documentationcenter: 
author: rajani-janaki-ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/31/2017
ms.author: rajani-janaki-ram
ms.openlocfilehash: a18a923ee3bad91873e654c9b9b5bf8b83acc123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-site-recovery-vault-tooan-azure-resource-manager-based-recovery-services-vault"></a><span data-ttu-id="deeb8-103">Site Recovery kasası tooan Azure Resource Manager tabanlı kurtarma Hizmetleri kasası yükseltme</span><span class="sxs-lookup"><span data-stu-id="deeb8-103">Upgrade a Site Recovery vault tooan Azure Resource Manager-based Recovery Services vault</span></span>

<span data-ttu-id="deeb8-104">Bu makalede, Azure Site Recovery tooupgrade tooAzure Resource Manager tabanlı kurtarma hizmeti kasalarını devam eden çoğaltma üzerinde hiçbir etkisi olmadan nasıl kasaları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="deeb8-104">This article describes how tooupgrade Azure Site Recovery vaults tooAzure Resource Manager-based Recovery Service vaults without any impact on ongoing replication.</span></span> <span data-ttu-id="deeb8-105">Azure Kaynak Yöneticisi özellikleri ve avantajları hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="deeb8-105">For more information about Azure Resource Manager features and benefits, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="deeb8-106">Giriş</span><span class="sxs-lookup"><span data-stu-id="deeb8-106">Introduction</span></span>
<span data-ttu-id="deeb8-107">Kurtarma Hizmetleri kasası, yedekleme ve olağanüstü durum kurtarma hello bulut yerel olarak yönetmek için bir Azure Resource Manager kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="deeb8-107">A Recovery Services vault is an Azure Resource Manager resource for managing backup and disaster recovery natively in hello cloud.</span></span> <span data-ttu-id="deeb8-108">Merhaba yeni Azure Portalı'nda kullanabileceğiniz birleşik bir kasa olan ve hello Klasik yedekleme değiştirir ve Site Recovery kasaları.</span><span class="sxs-lookup"><span data-stu-id="deeb8-108">It is a unified vault that you can use in hello new Azure portal, and it replaces hello classic backup and Site Recovery vaults.</span></span>

<span data-ttu-id="deeb8-109">Kurtarma Hizmetleri kasaları dahil olmak üzere özellikleri, bir dizi sunar:</span><span class="sxs-lookup"><span data-stu-id="deeb8-109">Recovery Services vaults offer an array of features, including:</span></span>

* <span data-ttu-id="deeb8-110">Azure Resource Manager desteği: korumak ve sanal makineleri ve fiziksel makineler üzerinden bir Azure Resource Manager yığına başarısız.</span><span class="sxs-lookup"><span data-stu-id="deeb8-110">Azure Resource Manager support: You can protect and fail over your virtual machines and physical machines into an Azure Resource Manager stack.</span></span>

* <span data-ttu-id="deeb8-111">Diski dışarıda: geçici dosyalar veya tüm bant toouse istemediğiniz yüksek bir karmaşıklık verileri varsa, birimleri çoğaltma dışında bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="deeb8-111">Exclude disk: If you have temp files or high churn data that you don’t want toouse all your bandwidth for, you can exclude volumes from replication.</span></span> <span data-ttu-id="deeb8-112">Bu özellik şu anda etkin *VMware tooAzure* ve *Hyper-V tooAzure* ve tooother senaryoları genişletilir.</span><span class="sxs-lookup"><span data-stu-id="deeb8-112">This capability has been enabled currently in *VMware tooAzure* and *Hyper-V tooAzure* and is extended tooother scenarios as well.</span></span>

* <span data-ttu-id="deeb8-113">Premium ve yerel olarak yedekli depolama için destek: artık sunucuları koruyabilir premium depolama alanına müşteriler tooprotect uygulamalarla yüksek izin hesapları giriş/saniye başına işlemi (IOPS) çıkış.</span><span class="sxs-lookup"><span data-stu-id="deeb8-113">Support for premium and locally redundant storage: You can now protect servers in premium storage accounts that allow customers tooprotect applications with higher input/output operations per second (IOPS).</span></span> <span data-ttu-id="deeb8-114">Bu özellik şu anda etkin *VMware tooAzure*.</span><span class="sxs-lookup"><span data-stu-id="deeb8-114">This capability is currently enabled in *VMware tooAzure*.</span></span>

* <span data-ttu-id="deeb8-115">Hızlandırıldı başlama deneyimi: Gelişmiş hello başlama deneyimi tasarlanmış toomake olağanüstü durum kurtarma Kurulumu kolay.</span><span class="sxs-lookup"><span data-stu-id="deeb8-115">Streamlined getting-started experience: hello enhanced getting-started experience has been designed toomake disaster-recovery setup easy.</span></span>

* <span data-ttu-id="deeb8-116">Yedekleme ve Site Recovery yönetimden hello aynı Kasa: şimdi olağanüstü durum kurtarma korumak veya hello yedekleme, yönetim yükünü önemli ölçüde azaltabilir aynı kasası.</span><span class="sxs-lookup"><span data-stu-id="deeb8-116">Backup and Site Recovery management from hello same vault: You can now protect servers for disaster recovery or perform backup from hello same vault, which can reduce your management overhead significantly.</span></span>

<span data-ttu-id="deeb8-117">Hello yükseltilmiş hello deneyimi ve özellikleri hakkında daha fazla bilgi için bkz: [depolama, yedekleme ve kurtarma blog](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).</span><span class="sxs-lookup"><span data-stu-id="deeb8-117">For more information about hello upgraded experience and features, see hello [Storage, Backup, and Recovery blog](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).</span></span>

## <a name="salient-features"></a><span data-ttu-id="deeb8-118">Dikkat çekici özellikleri</span><span class="sxs-lookup"><span data-stu-id="deeb8-118">Salient features</span></span>

* <span data-ttu-id="deeb8-119">Devam eden çoğaltma üzerindeki etkisi: devam eden çoğaltma sırasında herhangi bir kesintiye uğratmadan devam etmek ve yükseltme sonrası.</span><span class="sxs-lookup"><span data-stu-id="deeb8-119">No impact on ongoing replication: Ongoing replications continue without any interruption during and post upgrade.</span></span>

* <span data-ttu-id="deeb8-120">Ek ücret ödemeden: güncelleştirilmiş özellikleri kümesinin tamamını hiçbir ek ücret ödemeden.</span><span class="sxs-lookup"><span data-stu-id="deeb8-120">No additional cost: Get an entire set of updated capabilities at no additional cost.</span></span>

* <span data-ttu-id="deeb8-121">Veri kaybı: Bu işlem, yükseltme ve bir geçiş olduğundan, var olan çoğaltma kurtarma noktalarının ve ayarları sırasında ve hello yükselttikten sonra değişmeden kalır.</span><span class="sxs-lookup"><span data-stu-id="deeb8-121">No data loss: Because this process is an upgrade and not a migration, existing replication recovery points and settings remain intact during and after hello upgrade.</span></span>


## <a name="what-happens-during-hello-vault-upgrade"></a><span data-ttu-id="deeb8-122">Merhaba kasası yükseltme sırasında ne olur?</span><span class="sxs-lookup"><span data-stu-id="deeb8-122">What happens during hello vault upgrade?</span></span>

<span data-ttu-id="deeb8-123">Merhaba yükseltme sırasında yeni bir sunucu kaydetme veya bir sanal makine (VM) için çoğaltma etkinleştirme gibi işlemleri gerçekleştiremezsiniz.</span><span class="sxs-lookup"><span data-stu-id="deeb8-123">During hello upgrade, you cannot perform operations such as registering a new server or enabling replication for a virtual machine (VM).</span></span> <span data-ttu-id="deeb8-124">Verileri okuma veya yazma korumalı öğelerin toohello kasasının, devam eden çoğaltma gibi veri toohello kasası içeren işlemleri kesintisiz devam edin.</span><span class="sxs-lookup"><span data-stu-id="deeb8-124">Operations that involve reading data from or writing data toohello vault, such as ongoing replication of protected items toohello vault, continue uninterrupted.</span></span>

### <a name="changes-tooautomation-and-tooling-after-hello-upgrade"></a><span data-ttu-id="deeb8-125">Değişiklikleri tooautomation ve araç hello yükselttikten sonra</span><span class="sxs-lookup"><span data-stu-id="deeb8-125">Changes tooautomation and tooling after hello upgrade</span></span>
<span data-ttu-id="deeb8-126">Merhaba Klasik dağıtım modeli toohello Resource Manager dağıtım modelinden yükseltme hello kasa türü gibi hello var olan Otomasyon veya onu toowork hello yükseltme sonrasında devam araç tooensure güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="deeb8-126">As you upgrade hello vault type from hello classic deployment model toohello Resource Manager deployment model, update hello existing automation or tooling tooensure that it continues toowork after hello upgrade.</span></span>

### <a name="prepare-your-environment-for-hello-upgrade"></a><span data-ttu-id="deeb8-127">Merhaba yükseltme için ortamınızı hazırlama</span><span class="sxs-lookup"><span data-stu-id="deeb8-127">Prepare your environment for hello upgrade</span></span>

* [<span data-ttu-id="deeb8-128">PowerShell yüklemek veya tooversion 5 veya sonraki sürümünü yükseltme</span><span class="sxs-lookup"><span data-stu-id="deeb8-128">Install PowerShell or upgrade it tooversion 5 or later</span></span>](https://www.microsoft.com/download/details.aspx?id=50395)
* [<span data-ttu-id="deeb8-129">Azure PowerShell MSI Hello en son sürümünü yükleyin</span><span class="sxs-lookup"><span data-stu-id="deeb8-129">Install hello latest version of Azure PowerShell MSI</span></span>](https://github.com/Azure/azure-powershell/releases)
* [<span data-ttu-id="deeb8-130">Merhaba kurtarma Hizmetleri kasası yükseltme betiğini indir</span><span class="sxs-lookup"><span data-stu-id="deeb8-130">Download hello Recovery Services vault upgrade script</span></span>](https://aka.ms/vaultupgradescript)

### <a name="prerequisites"></a><span data-ttu-id="deeb8-131">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="deeb8-131">Prerequisites</span></span>
<span data-ttu-id="deeb8-132">tooAzure Resource Manager tabanlı kurtarma hizmeti kasalar Site kurtarma'dan tooupgrade kasaları, hello aşağıdaki gereksinimleri karşılamalıdır:</span><span class="sxs-lookup"><span data-stu-id="deeb8-132">tooupgrade from Site Recovery vaults tooAzure Resource Manager-based Recovery Service vaults, you must meet hello following requirements:</span></span>

* <span data-ttu-id="deeb8-133">En düşük aracı sürümü: hello sunucunuzda yüklü Azure Site Recovery sağlayıcısı sürümü 5.1.1700.0 olmalıdır veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="deeb8-133">Minimum agent version: hello version of Azure Site Recovery Provider installed on your server must be 5.1.1700.0 or later.</span></span>

* <span data-ttu-id="deeb8-134">Desteklenen yapılandırma: depolama alanı ağı (SAN) veya SQL Server AlwaysOn Kullanılabilirlik grupları ile kasanızı yapılandıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="deeb8-134">Supported configuration: You cannot configure your vault with storage area network (SAN) or SQL Server AlwaysOn Availability Groups.</span></span> <span data-ttu-id="deeb8-135">Tüm diğer yapılandırmalar desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="deeb8-135">All other configurations are supported.</span></span>

    >[!NOTE]
    ><span data-ttu-id="deeb8-136">Merhaba yükseltmeden sonra depolama eşlemesi yalnızca PowerShell aracılığıyla yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="deeb8-136">After hello upgrade, you can manage storage mapping only via PowerShell.</span></span>

* <span data-ttu-id="deeb8-137">Desteklenen dağıtım senaryosu: kasanızı hello olmamalıdır *VMware tooAzure* eski dağıtım modeli.</span><span class="sxs-lookup"><span data-stu-id="deeb8-137">Supported deployment scenario: Your vault shouldn’t be hello *VMware tooAzure* legacy deployment model.</span></span> <span data-ttu-id="deeb8-138">Devam etmeden önce toohello gelişmiş dağıtım modeli taşıyın.</span><span class="sxs-lookup"><span data-stu-id="deeb8-138">Before you proceed, first move toohello enhanced deployment model.</span></span>

* <span data-ttu-id="deeb8-139">Yönetimi ile ilgili hiç etkin kullanıcı tarafından başlatılan iş düzlemine işlemleri: hello yükseltilmesini önce erişim toohello yönetim düzlemi yükseltme sırasında sınırlı olduğundan, tüm yönetim düzlemi eylemleri tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="deeb8-139">No active user-initiated jobs that involve management plane operations: Because access toohello management plane is restricted during upgrade, complete all your management plane actions before you trigger hello upgrade.</span></span> <span data-ttu-id="deeb8-140">Bu işlem, devam eden çoğaltmayı içermez.</span><span class="sxs-lookup"><span data-stu-id="deeb8-140">This process doesn’t include ongoing replication.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="deeb8-141">Sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="deeb8-141">Frequently asked questions</span></span>

<span data-ttu-id="deeb8-142">**Bu yükseltme my devam eden çoğaltma etkiliyor mu?**</span><span class="sxs-lookup"><span data-stu-id="deeb8-142">**Does this upgrade affect my ongoing replication?**</span></span>

<span data-ttu-id="deeb8-143">Hayır.</span><span class="sxs-lookup"><span data-stu-id="deeb8-143">No.</span></span> <span data-ttu-id="deeb8-144">Devam eden çoğaltmayı kesintiye uğramadan sırasında ve hello yükseltme sonrasında devam eder.</span><span class="sxs-lookup"><span data-stu-id="deeb8-144">Your ongoing replication continues uninterrupted during and after hello upgrade.</span></span>

<span data-ttu-id="deeb8-145">**Siteden siteye VPN ve IP ayarları gibi toonetwork ayarları ne olur?**</span><span class="sxs-lookup"><span data-stu-id="deeb8-145">**What happens toonetwork settings such as site-to-site VPN and IP settings?**</span></span>

<span data-ttu-id="deeb8-146">Merhaba yükseltme hello ağ ayarlarını etkilemez.</span><span class="sxs-lookup"><span data-stu-id="deeb8-146">hello upgrade doesn't affect hello network settings.</span></span> <span data-ttu-id="deeb8-147">Tüm Azure-için-şirket içi bağlantılar sürdürülür.</span><span class="sxs-lookup"><span data-stu-id="deeb8-147">All Azure-to-on-premises connections remain intact.</span></span>

<span data-ttu-id="deeb8-148">**Yakın zaman hello tooupgrade planlamıyorsanız toomy kasalarını ne olur?**</span><span class="sxs-lookup"><span data-stu-id="deeb8-148">**What happens toomy vaults if I don’t plan tooupgrade in hello near future?**</span></span>

<span data-ttu-id="deeb8-149">Eylül 2017 başlangıç hello eski Azure portalında Site Recovery kasası desteği kullanım dışı kalacaktır.</span><span class="sxs-lookup"><span data-stu-id="deeb8-149">Support for Site Recovery vault in hello old Azure portal will be deprecated starting September 2017.</span></span> <span data-ttu-id="deeb8-150">Merhaba yükseltme özelliği toomove toohello yeni portalı kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="deeb8-150">We strongly recommend that you use hello upgrade feature toomove toohello new portal.</span></span>

<span data-ttu-id="deeb8-151">**Bu geçiş planı için varolan my araç anlamı nedir?**</span><span class="sxs-lookup"><span data-stu-id="deeb8-151">**What does this migration plan mean for my existing tooling?**</span></span>  

<span data-ttu-id="deeb8-152">Araç toohello Resource Manager dağıtım modeli güncelleştirmek yükseltme planlarınızı için dikkate almalı hello en önemli değişikliklerden biri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="deeb8-152">Updating your tooling toohello Resource Manager deployment model is one of hello most important changes that you must account for in your upgrade plans.</span></span> <span data-ttu-id="deeb8-153">Merhaba kurtarma Hizmetleri kasalarının hello Resource Manager dağıtım modeline dayanır.</span><span class="sxs-lookup"><span data-stu-id="deeb8-153">hello Recovery Services vaults are based on hello Resource Manager deployment model.</span></span> 

<span data-ttu-id="deeb8-154">**Ne kadar süreyle Yönetim düzeyi kapalı kalma süresi en son hello mu?**</span><span class="sxs-lookup"><span data-stu-id="deeb8-154">**How long does hello management-plane downtime last?**</span></span>

<span data-ttu-id="deeb8-155">Merhaba yükseltmenin normalde yaklaşık 15 too30 dakika sürer ve tooa bir saatlik maksimum ele geçirebilir.</span><span class="sxs-lookup"><span data-stu-id="deeb8-155">hello upgrade ordinarily takes about 15 too30 minutes, and it could take up tooa maximum of one hour.</span></span>

<span data-ttu-id="deeb8-156">**I yükselttikten sonra geri alabilirsiniz?**</span><span class="sxs-lookup"><span data-stu-id="deeb8-156">**Can I roll back after upgrading?**</span></span>

<span data-ttu-id="deeb8-157">Hayır.</span><span class="sxs-lookup"><span data-stu-id="deeb8-157">No.</span></span> <span data-ttu-id="deeb8-158">Merhaba kaynakları başarılı bir şekilde yükselttikten sonra geri alma desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="deeb8-158">Rollback is not supported after hello resources have been successfully upgraded.</span></span>

<span data-ttu-id="deeb8-159">**Yükseltilebilmesi için olup olmadığını ı my abonelik veya kaynak toosee doğrulayabilirsiniz?**</span><span class="sxs-lookup"><span data-stu-id="deeb8-159">**Can I validate my subscription or resources toosee whether they can be upgraded?**</span></span>

<span data-ttu-id="deeb8-160">Evet.</span><span class="sxs-lookup"><span data-stu-id="deeb8-160">Yes.</span></span> <span data-ttu-id="deeb8-161">Merhaba platformu tarafından desteklenen yükseltme, hello yükseltme ilk adımda hello hello kaynakları yükseltme kapasitesi toovalidate seçenektir.</span><span class="sxs-lookup"><span data-stu-id="deeb8-161">In hello platform-supported upgrade option, hello first step in hello upgrade is toovalidate that hello resources are capable of an upgrade.</span></span> <span data-ttu-id="deeb8-162">Merhaba doğrulama başarısız olursa, ilgili hata iletisi veya uyarı alırsınız.</span><span class="sxs-lookup"><span data-stu-id="deeb8-162">If hello validation fails, you will receive appropriate error messages or warnings.</span></span>

<span data-ttu-id="deeb8-163">**Merhaba yükseltme ile ilgili bir sorunu nasıl bildirebilirim?**</span><span class="sxs-lookup"><span data-stu-id="deeb8-163">**How do I report an issue with hello upgrade?**</span></span>

<span data-ttu-id="deeb8-164">Merhaba yükseltme sırasında hatalar karşılaşırsanız, hello hata listelenen hello işlem kimliği unutmayın.</span><span class="sxs-lookup"><span data-stu-id="deeb8-164">If you experience any failures during hello upgrade, note hello operation ID that's listed in hello error.</span></span> <span data-ttu-id="deeb8-165">Microsoft Support hello sorunu çözümlemek için proaktif olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="deeb8-165">Microsoft Support will proactively work on resolving hello issue.</span></span> <span data-ttu-id="deeb8-166">Merhaba Destek ekibiyle abonelik kimliği, kasa adını ve işlem kimliği de başvurabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="deeb8-166">You can also contact hello Support team with your subscription ID, vault name, and operation ID.</span></span> <span data-ttu-id="deeb8-167">Destek tooresolve hello sorunu mümkün olan en kısa sürede çalışır.</span><span class="sxs-lookup"><span data-stu-id="deeb8-167">Support will work tooresolve hello issue as quickly as possible.</span></span> <span data-ttu-id="deeb8-168">Açıkça belirtildiği toodo olmadıkça hello işlemi yeniden deneyin değil Microsoft tarafından bunu.</span><span class="sxs-lookup"><span data-stu-id="deeb8-168">Do not retry hello operation unless you are explicitly instructed toodo so by Microsoft.</span></span>

## <a name="run-hello-script"></a><span data-ttu-id="deeb8-169">Merhaba komut dosyasını çalıştır</span><span class="sxs-lookup"><span data-stu-id="deeb8-169">Run hello script</span></span>

<span data-ttu-id="deeb8-170">PowerShell'de hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="deeb8-170">In PowerShell, run hello following command:</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionID <subscriptionID>  -VaultName <vaultname> -Location <location> -ResourceType HyperVRecoveryManagerVault -TargetResourceGroupName <rgname>

* <span data-ttu-id="deeb8-171">Subscriptionıd: yükseltme yapıyorsanız hello kasayla ilişkili hello abonelik kimliği.</span><span class="sxs-lookup"><span data-stu-id="deeb8-171">SubscriptionID: hello subscription ID that's associated with hello vault that you're upgrading.</span></span>

* <span data-ttu-id="deeb8-172">VaultName: yükseltme yapıyorsanız hello kasa hello adı.</span><span class="sxs-lookup"><span data-stu-id="deeb8-172">VaultName: hello name of hello vault that you're upgrading.</span></span>

* <span data-ttu-id="deeb8-173">Konumu: yükseltme yapıyorsanız hello kasası başlangıç konumu.</span><span class="sxs-lookup"><span data-stu-id="deeb8-173">Location: hello location of hello vault that you're upgrading.</span></span>

* <span data-ttu-id="deeb8-174">ResourceType: Site Recovery için HyperVRecoveryManagerVault kasaları.</span><span class="sxs-lookup"><span data-stu-id="deeb8-174">ResourceType: HyperVRecoveryManagerVault for Site Recovery vaults.</span></span>

* <span data-ttu-id="deeb8-175">TargetResourceGroupName: hello istediğiniz hello kaynak grubu yerleştirilen kasa toobe yükseltildi.</span><span class="sxs-lookup"><span data-stu-id="deeb8-175">TargetResourceGroupName: hello resource group into which you want hello upgraded vault toobe placed.</span></span> <span data-ttu-id="deeb8-176">Azure Resource Manager veya yeni bir tane var olan bir kaynak grubunda TargetResourceGroupName olabilir.</span><span class="sxs-lookup"><span data-stu-id="deeb8-176">TargetResourceGroupName can be an existing resource group in Azure Resource Manager or a new one.</span></span> <span data-ttu-id="deeb8-177">Merhaba sağlanan TargetResourceGroupName mevcut değilse hello yükseltmesinin bir parçası hello aynı oluşturulduğu konumu hello kasası olarak.</span><span class="sxs-lookup"><span data-stu-id="deeb8-177">If hello TargetResourceGroupName that's supplied does not exist, it is created as part of hello upgrade in hello same location as hello vault.</span></span> <span data-ttu-id="deeb8-178">Daha fazla bilgi için hello "Kaynak grupları" bölümüne bakın [Azure Resource Manager'a genel bakış](../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="deeb8-178">For more information, see hello "Resource groups" section of [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

    >[!NOTE]
    ><span data-ttu-id="deeb8-179">Kaynak grubu adlandırma konu toocertain kısıtlamaları edilir.</span><span class="sxs-lookup"><span data-stu-id="deeb8-179">Resource group naming is subject toocertain constraints.</span></span> <span data-ttu-id="deeb8-180">tooprevent kasa yükseltme hatası, adlandırma emin tooobserve hello dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="deeb8-180">tooprevent vault upgrade failure, be sure tooobserve hello naming convention carefully.</span></span>
    >
    ><span data-ttu-id="deeb8-181">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="deeb8-181">For example:</span></span>
    >
    ><span data-ttu-id="deeb8-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 - Subscriptionıd 1234-54123-354354-56416-8645 - VaultName gen2dr-konum "Kuzey Avrupa" - ResourceType hypervrecoverymanagervault - TargetResourceGroupName abc</span><span class="sxs-lookup"><span data-stu-id="deeb8-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc</span></span>

<span data-ttu-id="deeb8-183">Alternatif olarak, komut dosyası izleyen hello çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="deeb8-183">Alternatively, you can run hello following script.</span></span> <span data-ttu-id="deeb8-184">Merhaba değerleri gerekli hello parametrelerini girin.</span><span class="sxs-lookup"><span data-stu-id="deeb8-184">Enter hello values for hello required parameters.</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1
    cmdlet RecoveryServicesVaultUpgrade-1.0.0.ps1 at command pipeline position 1

    Supply values for hello following parameters:
    SubscriptionId:
    VaultName:
    Location:
    ResourceType:
    TargetResourceGroupName:

1. <span data-ttu-id="deeb8-185">Merhaba PowerShell komut dosyası, tooenter kimlik bilgilerinizi ister.</span><span class="sxs-lookup"><span data-stu-id="deeb8-185">hello PowerShell script prompts you tooenter your credentials.</span></span> <span data-ttu-id="deeb8-186">Bunları, iki kez hello Klasik dağıtım modeli hesabı için bir kez ve bir kez hello Azure Resource Manager hesabı girin.</span><span class="sxs-lookup"><span data-stu-id="deeb8-186">Enter them twice, once for hello classic deployment model account and once for hello Azure Resource Manager account.</span></span>

2. <span data-ttu-id="deeb8-187">Kimlik bilgilerinizi girdikten sonra altyapı Kurulum karşılıyor hello gereksinimleri daha önce bahsedilen bakılmaksızın hello betik onay toodetermine çalışır.</span><span class="sxs-lookup"><span data-stu-id="deeb8-187">After you've entered your credentials, hello script runs a check toodetermine whether your infrastructure setup meets hello previously mentioned requirements.</span></span>

3. <span data-ttu-id="deeb8-188">Hello önkoşulları işaretli ve onaylandıktan sonra istendiğinde tooproceed hello kasası yükseltme işlemine olursunuz.</span><span class="sxs-lookup"><span data-stu-id="deeb8-188">After hello prerequisites have been checked and confirmed, you are prompted tooproceed with hello vault upgrade.</span></span> <span data-ttu-id="deeb8-189">Merhaba yükseltme işlemi kasanızı yükseltmeyi başlatır.</span><span class="sxs-lookup"><span data-stu-id="deeb8-189">hello upgrade process starts upgrading your vault.</span></span> <span data-ttu-id="deeb8-190">Merhaba tüm yükseltme 15 too30 dakika toocomplete alabilir.</span><span class="sxs-lookup"><span data-stu-id="deeb8-190">hello entire upgrade can take 15 too30 minutes toocomplete.</span></span>

4. <span data-ttu-id="deeb8-191">Hello Yükseltme başarıyla tamamlandıktan sonra hello yükseltilmiş kasaya hello yeni Azure portalına erişebilir.</span><span class="sxs-lookup"><span data-stu-id="deeb8-191">After hello upgrade has been completed successfully, you can access hello upgraded vault in hello new Azure portal.</span></span>

## <a name="post-upgrade-vault-management"></a><span data-ttu-id="deeb8-192">Yükseltme sonrası kasa yönetimi</span><span class="sxs-lookup"><span data-stu-id="deeb8-192">Post-upgrade vault management</span></span>

### <a name="replicate-by-using-azure-site-recovery-in-hello-recovery-services-vault"></a><span data-ttu-id="deeb8-193">Kurtarma Hizmetleri kasası hello Azure Site Recovery kullanarak çoğaltma</span><span class="sxs-lookup"><span data-stu-id="deeb8-193">Replicate by using Azure Site Recovery in hello Recovery Services vault</span></span>

* <span data-ttu-id="deeb8-194">Bu gibi durumlarda, Azure Vm'leriniz artık tek bir bölge tooanother koruyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="deeb8-194">You can now protect your Azure VMs from one region tooanother.</span></span> <span data-ttu-id="deeb8-195">Daha fazla bilgi için bkz: [Azure Site Recovery ile bölgeler arasında Azure sanal makineleri çoğaltmak](site-recovery-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="deeb8-195">For more information, see [Replicate Azure VMs between regions with Azure Site Recovery](site-recovery-azure-to-azure.md).</span></span>

* <span data-ttu-id="deeb8-196">VMware Vm'lerini tooAzure çoğaltma hakkında daha fazla bilgi için bkz: [Site Recovery ile çoğaltmak VMware Vm'lerini tooAzure](vmware-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="deeb8-196">For more information about replicating VMware VMs tooAzure, see [Replicate VMware VMs tooAzure with Site Recovery](vmware-walkthrough-overview.md).</span></span>

* <span data-ttu-id="deeb8-197">Hyper-V Vm'lerini (VMM olmadan) tooAzure çoğaltma hakkında daha fazla bilgi için bkz: [çoğaltmak Hyper-V sanal makineleri (VMM olmadan) tooAzure](hyper-v-site-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="deeb8-197">For more information about replicating Hyper-V VMs (without VMM) tooAzure, see [Replicate Hyper-V virtual machines (without VMM) tooAzure](hyper-v-site-walkthrough-overview.md).</span></span>

* <span data-ttu-id="deeb8-198">Hyper-V Vm'lerini (VMM ile) tooAzure çoğaltma hakkında daha fazla bilgi için bkz: [çoğaltmak Hyper-V sanal makineleri Site RECOVERY'yi kullanarak VMM Bulutları tooAzure içinde hello Azure portal](vmm-to-azure-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="deeb8-198">For more information about replicating Hyper-V VMs (with VMM) tooAzure, see [Replicate Hyper-V virtual machines in VMM clouds tooAzure using Site Recovery in hello Azure portal](vmm-to-azure-walkthrough-overview.md).</span></span>

* <span data-ttu-id="deeb8-199">Hyper-Vm'lerini (VMM ile) tooa ikincil siteye çoğaltma hakkında daha fazla bilgi için bkz: [VMM Bulutları tooa ikincil VMM sitesi kullanarak Hyper-V çoğaltma sanal makineleri hello Azure portal](site-recovery-vmm-to-vmm.md).</span><span class="sxs-lookup"><span data-stu-id="deeb8-199">For more information about replicating Hyper-VMs (with VMM) tooa secondary site, see [Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site using hello Azure portal](site-recovery-vmm-to-vmm.md).</span></span>

* <span data-ttu-id="deeb8-200">VMware Vm'lerini tooa ikincil siteye çoğaltma hakkında daha fazla bilgi için bkz: [Replicate şirket içi VMware sanal makineleri veya fiziksel sunucuları tooa ikincil site hello Klasik Azure portalında](site-recovery-vmware-to-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="deeb8-200">For more information about replicating VMware VMs tooa secondary site, see [Replicate on-premises VMware virtual machines or physical servers tooa secondary site in hello classic Azure portal](site-recovery-vmware-to-vmware.md).</span></span>

### <a name="view-your-replicated-items"></a><span data-ttu-id="deeb8-201">Çoğaltılmış öğelerinizi görüntüleme</span><span class="sxs-lookup"><span data-stu-id="deeb8-201">View your replicated items</span></span>

<span data-ttu-id="deeb8-202">Merhaba aşağıdaki görüntüde hello kasa için anahtar varlıklar görüntüler hello kurtarma Hizmetleri kasası Pano sayfası gösterilir.</span><span class="sxs-lookup"><span data-stu-id="deeb8-202">hello following image shows hello Recovery Services vault dashboard page that displays key entities for hello vault.</span></span> <span data-ttu-id="deeb8-203">tooview hello kasadaki korunan varlıklar listesi seçin **Site Recovery** > **öğeleri çoğaltılan**.</span><span class="sxs-lookup"><span data-stu-id="deeb8-203">tooview a list of protected entities in hello vault, select **Site Recovery** > **Replicated items**.</span></span>


![Çoğaltılan öğe](./media/upgrade-site-recovery-vaults/replicateditems.png)

<span data-ttu-id="deeb8-205">Merhaba aşağıdaki görüntüde çoğaltılan öğeler ve hello görüntüleme hello iş akışı gösterilmektedir **yük devretme** bir yük devretmeyi başlatmadan için komutu.</span><span class="sxs-lookup"><span data-stu-id="deeb8-205">hello following image shows hello workflow for viewing your replicated items and hello **Failover** command for initiating a failover.</span></span>

![Çoğaltılan öğe](./media/upgrade-site-recovery-vaults/failover.png)

### <a name="view-your-replication-settings"></a><span data-ttu-id="deeb8-207">Çoğaltma ayarlarınızı görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="deeb8-207">View your replication settings</span></span>

<span data-ttu-id="deeb8-208">Merhaba Site kurtarma kasasına her koruma grubu kopyalama sıklığı, kurtarma noktası bekletme, uygulama ile tutarlı anlık görüntü sıklığı ve diğer çoğaltma ayarları ile yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="deeb8-208">In hello Site Recovery vault, each protection group is configured with copy frequency, recovery point retention, frequency of application consistent snapshots, and other replication settings.</span></span> <span data-ttu-id="deeb8-209">Merhaba kurtarma Hizmetleri kasasına bu ayarları bir çoğaltma ilkesi yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="deeb8-209">In hello Recovery Services vault, these settings are configured as a replication policy.</span></span> <span data-ttu-id="deeb8-210">Merhaba hello İlkesi adıdır hello hello koruma grubu adı veya hello *primarycloud_Policy*.</span><span class="sxs-lookup"><span data-stu-id="deeb8-210">hello name of hello policy is hello name of hello protection group or hello *primarycloud_Policy*.</span></span>

<span data-ttu-id="deeb8-211">Çoğaltma İlkesi hakkında daha fazla bilgi için bkz: [VMware tooAzure için çoğaltma ilkesini yönetme](site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="deeb8-211">For more information about replication policy, see [Manage replication policy for VMware tooAzure](site-recovery-setup-replication-settings-vmware.md).</span></span>
