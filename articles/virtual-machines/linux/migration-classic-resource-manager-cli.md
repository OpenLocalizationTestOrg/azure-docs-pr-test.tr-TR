---
title: aaaMigrate VM'ler tooResource Azure CLI kullanarak Manager | Microsoft Docs
description: "Bu makalede, Azure CLI kullanarak Klasik tooAzure Resource Manager hello platform desteklenen geçiş kaynakların anlatılmaktadır"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d6f5a877-05b6-4127-a545-3f5bede4e479
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 0b11f4bb1b4658b3e88bf7629147ed953b678556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-cli"></a><span data-ttu-id="86bab-103">Azure CLI kullanarak Klasik tooAzure Resource Manager Iaas kaynaklarını geçirme</span><span class="sxs-lookup"><span data-stu-id="86bab-103">Migrate IaaS resources from classic tooAzure Resource Manager by using Azure CLI</span></span>
<span data-ttu-id="86bab-104">Bu adımlar nasıl hello Klasik dağıtım modeli toohello Azure Resource Manager dağıtım modeli hizmet (Iaas) kaynaklardan olarak toomigrate altyapı toouse Azure komut satırı arabirimi (CLI) komutları gösterir.</span><span class="sxs-lookup"><span data-stu-id="86bab-104">These steps show you how toouse Azure command-line interface (CLI) commands toomigrate infrastructure as a service (IaaS) resources from hello classic deployment model toohello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="86bab-105">Merhaba makale gerektirir hello [Azure CLI](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="86bab-105">hello article requires hello [Azure CLI](../../cli-install-nodejs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="86bab-106">Burada açıklanan tüm hello ıdempotent işlemleridir.</span><span class="sxs-lookup"><span data-stu-id="86bab-106">All hello operations described here are idempotent.</span></span> <span data-ttu-id="86bab-107">Desteklenmeyen bir özellik veya bir yapılandırma hatası başka bir sorun varsa, hello yeniden deneme öneririz hazırlamak, iptal etmek veya yürütme işlemi.</span><span class="sxs-lookup"><span data-stu-id="86bab-107">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry hello prepare, abort, or commit operation.</span></span> <span data-ttu-id="86bab-108">Merhaba platform sonra hello eylemi yeniden deneyecek.</span><span class="sxs-lookup"><span data-stu-id="86bab-108">hello platform will then try hello action again.</span></span>
> 
> 

<br>
<span data-ttu-id="86bab-109">Adımları bir geçiş işlemi sırasında yürütülen toobe gereken bir akış çizelgesi tooidentify hello siparişi İşte</span><span class="sxs-lookup"><span data-stu-id="86bab-109">Here is a flowchart tooidentify hello order in which steps need toobe executed during a migration process</span></span>

![Merhaba geçiş adımlarını gösteren ekran görüntüsü](../windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-prepare-for-migration"></a><span data-ttu-id="86bab-111">1. adım: geçiş için hazırlama</span><span class="sxs-lookup"><span data-stu-id="86bab-111">Step 1: Prepare for migration</span></span>
<span data-ttu-id="86bab-112">Klasik tooResource Yöneticisi geçirme Iaas kaynaklardan değerlendirirken öneririz birkaç en iyi uygulamalar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="86bab-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic tooResource Manager:</span></span>

* <span data-ttu-id="86bab-113">Merhaba okuma [desteklenmeyen yapılandırmaları veya özellikleri listesi](../windows/migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="86bab-113">Read through hello [list of unsupported configurations or features](../windows/migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="86bab-114">Desteklenmeyen yapılandırmaları veya özellikleri kullanan sanal makineler varsa, hello özelliği/yapılandırma desteği toobe duyurdu için beklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="86bab-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for hello feature/configuration support toobe announced.</span></span> <span data-ttu-id="86bab-115">Alternatif olarak, bu özelliği kaldırmak veya gereksinimlerinize uygun yapılandırma tooenable geçişin dışına taşıyın.</span><span class="sxs-lookup"><span data-stu-id="86bab-115">Alternatively, you can remove that feature or move out of that configuration tooenable migration if it suits your needs.</span></span>
* <span data-ttu-id="86bab-116">Bugün, altyapı ve uygulamalarınızı dağıtma komut otomatik değilse, geçiş için bu komut dosyalarını kullanarak toocreate benzer bir test Kurulum deneyin.</span><span class="sxs-lookup"><span data-stu-id="86bab-116">If you have automated scripts that deploy your infrastructure and applications today, try toocreate a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="86bab-117">Alternatif olarak, örnek ortamları hello Azure portal kullanarak ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86bab-117">Alternatively, you can set up sample environments by using hello Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="86bab-118">Uygulama ağ geçitleri, Klasik tooResource Yöneticisi geçiş için şu anda desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="86bab-118">Application Gateways are not currently supported for migration from classic tooResource Manager.</span></span> <span data-ttu-id="86bab-119">toomigrate bir uygulama ağ geçidi ile klasik sanal ağ hazırlama işlemi toomove hello ağ çalıştırmadan önce hello ağ geçidi kaldırın.</span><span class="sxs-lookup"><span data-stu-id="86bab-119">toomigrate a classic virtual network with an Application gateway, remove hello gateway before running a Prepare operation toomove hello network.</span></span> <span data-ttu-id="86bab-120">Merhaba ağ geçidi Azure Kaynak Yöneticisi'nde hello geçişi tamamlandıktan sonra yeniden bağlanın.</span><span class="sxs-lookup"><span data-stu-id="86bab-120">After you complete hello migration, reconnect hello gateway in Azure Resource Manager.</span></span> 
>
><span data-ttu-id="86bab-121">ExpressRoute ağ geçidi başka bir Abonelikteki tooExpressRoute devreler bağlanma otomatik olarak geçirilemez.</span><span class="sxs-lookup"><span data-stu-id="86bab-121">ExpressRoute gateways connecting tooExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="86bab-122">Böyle durumlarda, hello ExpressRoute ağ geçidi kaldırın, hello sanal ağını geçirin ve hello ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="86bab-122">In such cases, remove hello ExpressRoute gateway, migrate hello virtual network and recreate hello gateway.</span></span> <span data-ttu-id="86bab-123">Lütfen bakın [geçirmek ExpressRoute bağlantı hattına ve hello Klasik toohello Resource Manager dağıtım modeli sanal ağlardan ilişkili](../../expressroute/expressroute-migration-classic-resource-manager.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="86bab-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from hello classic toohello Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
> 
> 

## <a name="step-2-set-your-subscription-and-register-hello-provider"></a><span data-ttu-id="86bab-124">2. adım: aboneliğinizi ayarlamak ve hello sağlayıcısını Kaydet</span><span class="sxs-lookup"><span data-stu-id="86bab-124">Step 2: Set your subscription and register hello provider</span></span>
<span data-ttu-id="86bab-125">Geçiş senaryoları için her iki Klasik için ortamınızı kurma tooset gerekir ve Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="86bab-125">For migration scenarios, you need tooset up your environment for both classic and Resource Manager.</span></span> <span data-ttu-id="86bab-126">[Azure CLI yükleme](../../cli-install-nodejs.md) ve [aboneliğinizi seçin](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="86bab-126">[Install Azure CLI](../../cli-install-nodejs.md) and [select your subscription](../../xplat-cli-connect.md).</span></span>

<span data-ttu-id="86bab-127">Oturum açma tooyour hesabı.</span><span class="sxs-lookup"><span data-stu-id="86bab-127">Sign-in tooyour account.</span></span>

    azure login

<span data-ttu-id="86bab-128">Komutu aşağıdaki hello kullanarak Hello Azure aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="86bab-128">Select hello Azure subscription by using hello following command.</span></span>

    azure account set "<azure-subscription-name>"

> [!NOTE]
> <span data-ttu-id="86bab-129">Kayıt bir kez, ancak ihtiyaçlarını kez geçiş işlemini denemeden önce bitti toobe adımıdır.</span><span class="sxs-lookup"><span data-stu-id="86bab-129">Registration is a one time step but it needs toobe done once before attempting migration.</span></span> <span data-ttu-id="86bab-130">Kaydettirmeden hello aşağıdaki hata iletisini görürsünüz</span><span class="sxs-lookup"><span data-stu-id="86bab-130">Without registering you'll see hello following error message</span></span> 
> 
> <span data-ttu-id="86bab-131">*BadRequest: Abonelik geçiş için kayıtlı değil.*</span><span class="sxs-lookup"><span data-stu-id="86bab-131">*BadRequest : Subscription is not registered for migration.*</span></span> 
> 
> 

<span data-ttu-id="86bab-132">Merhaba geçiş kaynak sağlayıcısı ile komutu aşağıdaki hello kullanarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="86bab-132">Register with hello migration resource provider by using hello following command.</span></span> <span data-ttu-id="86bab-133">Bazı durumlarda, bu komut zaman aşımına uğruyor olduğunu unutmayın. Ancak, hello kaydı başarılı olur.</span><span class="sxs-lookup"><span data-stu-id="86bab-133">Note that in some cases, this command times out. However, hello registration will be successful.</span></span>

    azure provider register Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="86bab-134">Merhaba kayıt toofinish için beş dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="86bab-134">Please wait five minutes for hello registration toofinish.</span></span> <span data-ttu-id="86bab-135">Komutu aşağıdaki hello kullanarak hello hello onay durumunu kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86bab-135">You can check hello status of hello approval by using hello following command.</span></span> <span data-ttu-id="86bab-136">RegistrationState olduğundan emin olun `Registered` devam etmeden önce.</span><span class="sxs-lookup"><span data-stu-id="86bab-136">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

    azure provider show Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="86bab-137">Şimdi CLI toohello geçiş `asm` modu.</span><span class="sxs-lookup"><span data-stu-id="86bab-137">Now switch CLI toohello `asm` mode.</span></span>

    azure config mode asm

## <a name="step-3-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="86bab-138">3. adım: hello geçerli dağıtım veya VNET Azure bölgesi yeterli Azure Resource Manager sanal makinesi çekirdeğe sahip olduğunuzdan emin olun</span><span class="sxs-lookup"><span data-stu-id="86bab-138">Step 3: Make sure you have enough Azure Resource Manager Virtual Machine cores in hello Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="86bab-139">Bu adımda, tooswitch çok gerekir`arm` modu.</span><span class="sxs-lookup"><span data-stu-id="86bab-139">For this step you'll need tooswitch too`arm` mode.</span></span> <span data-ttu-id="86bab-140">Bu komutu aşağıdaki hello ile yapın.</span><span class="sxs-lookup"><span data-stu-id="86bab-140">Do this with hello following command.</span></span>

```
azure config mode arm
```

<span data-ttu-id="86bab-141">CLI komutu toocheck hello geçerli miktarını Azure Kaynak Yöneticisi'nde sahip Çekirdek aşağıdaki hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="86bab-141">You can use hello following CLI command toocheck hello current amount of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="86bab-142">toolearn çekirdek kotaları hakkında daha fazla bilgi görmek [sınırları ve hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span><span class="sxs-lookup"><span data-stu-id="86bab-142">toolearn more about core quotas, see [Limits and hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span></span>

```
azure vm list-usage -l "<Your VNET or Deployment's Azure region"
```

<span data-ttu-id="86bab-143">İşiniz bittiğinde bu adımı doğrulanıyor, geri çok geçebilirsiniz`asm` modu.</span><span class="sxs-lookup"><span data-stu-id="86bab-143">Once you're done verifying this step, you can switch back too`asm` mode.</span></span>

    azure config mode asm


## <a name="step-4-option-1---migrate-virtual-machines-in-a-cloud-service"></a><span data-ttu-id="86bab-144">4. adım: 1. seçenek - sanal makineler bir bulut hizmetinde geçirme</span><span class="sxs-lookup"><span data-stu-id="86bab-144">Step 4: Option 1 - Migrate virtual machines in a cloud service</span></span>
<span data-ttu-id="86bab-145">Komutu aşağıdaki hello kullanarak bulut Hizmetleri ve çekme hello bulut hizmeti toomigrate istediğiniz Get hello listesi.</span><span class="sxs-lookup"><span data-stu-id="86bab-145">Get hello list of cloud services by using hello following command, and then pick hello cloud service that you want toomigrate.</span></span> <span data-ttu-id="86bab-146">Merhaba VM'ler hello bulut hizmetindeki bir sanal ağ veya web/çalışan rolleri varsa, bir hata iletisi alırsınız unutmayın.</span><span class="sxs-lookup"><span data-stu-id="86bab-146">Note that if hello VMs in hello cloud service are in a virtual network or if they have web/worker roles, you will get an error message.</span></span>

    azure service list

<span data-ttu-id="86bab-147">Merhaba ayrıntılı çıktı komutu tooget hello dağıtım adı hello bulut hizmeti için aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="86bab-147">Run hello following command tooget hello deployment name for hello cloud service from hello verbose output.</span></span> <span data-ttu-id="86bab-148">Çoğu durumda, hello dağıtım adı olduğu hello hello bulut hizmet adı ile aynı.</span><span class="sxs-lookup"><span data-stu-id="86bab-148">In most cases, hello deployment name is hello same as hello cloud service name.</span></span>

    azure service show <serviceName> -vv

<span data-ttu-id="86bab-149">Merhaba aşağıdaki komutları kullanarak hello bulut hizmeti geçirirseniz ilk olarak, doğrulama:</span><span class="sxs-lookup"><span data-stu-id="86bab-149">First, validate if you can migrate hello cloud service using hello following commands:</span></span>

```shell
azure service deployment validate-migration <serviceName> <deploymentName> new "" "" ""
```

<span data-ttu-id="86bab-150">Merhaba sanal makineleri hello bulut hizmetinde geçiş için hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="86bab-150">Prepare hello virtual machines in hello cloud service for migration.</span></span> <span data-ttu-id="86bab-151">Gelen iki seçenekleri toochoose sahip.</span><span class="sxs-lookup"><span data-stu-id="86bab-151">You have two options toochoose from.</span></span>

<span data-ttu-id="86bab-152">Toomigrate hello VM'ler tooa platform tarafından oluşturulan sanal ağ istiyorsanız, komutu aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="86bab-152">If you want toomigrate hello VMs tooa platform-created virtual network, use hello following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> new "" "" ""

<span data-ttu-id="86bab-153">Merhaba Resource Manager dağıtım modelinde sanal ağ varolan toomigrate tooan istiyorsanız, komutu aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="86bab-153">If you want toomigrate tooan existing virtual network in hello Resource Manager deployment model, use hello following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> existing <destinationVNETResourceGroupName> <subnetName> <vnetName>

<span data-ttu-id="86bab-154">Merhaba hazırladıktan sonra işlemi başarılı olur, hello ayrıntılı çıktı tooget hello geçiş durumunu hello VM'ler bakın ve hello olduklarından emin olun `Prepared` durumu.</span><span class="sxs-lookup"><span data-stu-id="86bab-154">After hello prepare operation is successful, you can look through hello verbose output tooget hello migration state of hello VMs and ensure that they are in hello `Prepared` state.</span></span>

    azure vm show <vmName> -vv

<span data-ttu-id="86bab-155">CLI veya hello Azure portal kullanarak kaynakları hazırlanmış hello için başlangıç yapılandırmasını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="86bab-155">Check hello configuration for hello prepared resources by using either CLI or hello Azure portal.</span></span> <span data-ttu-id="86bab-156">Geçiş için hazır olmayan ve toogo geri toohello eski durum istiyorsanız, komutu aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="86bab-156">If you are not ready for migration and you want toogo back toohello old state, use hello following command.</span></span>

    azure service deployment abort-migration <serviceName> <deploymentName>

<span data-ttu-id="86bab-157">Merhaba hazırlanan yapılandırma iyi görünüyorsa, ilerlemek ve komut aşağıdaki hello kullanarak hello kaynakları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="86bab-157">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command.</span></span>

    azure service deployment commit-migration <serviceName> <deploymentName>



## <a name="step-4-option-2----migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="86bab-158">4. adım: 2. seçenek - bir sanal ağdaki sanal makineleri geçirme</span><span class="sxs-lookup"><span data-stu-id="86bab-158">Step 4: Option 2 -  Migrate virtual machines in a virtual network</span></span>
<span data-ttu-id="86bab-159">Çekme hello sanal ağ toomigrate istiyor.</span><span class="sxs-lookup"><span data-stu-id="86bab-159">Pick hello virtual network that you want toomigrate.</span></span> <span data-ttu-id="86bab-160">Not Hello sanal ağ ile desteklenmeyen yapılandırmalar web/çalışan rolleri veya VM'ler içeriyorsa, bir doğrulama hata iletisi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="86bab-160">Note that if hello virtual network contains web/worker roles or VMs with unsupported configurations, you will get a validation error message.</span></span>

<span data-ttu-id="86bab-161">Tüm hello sanal ağlar, komutu aşağıdaki hello kullanarak hello abonelikte alın.</span><span class="sxs-lookup"><span data-stu-id="86bab-161">Get all hello virtual networks in hello subscription by using hello following command.</span></span>

    azure network vnet list

<span data-ttu-id="86bab-162">Merhaba çıktı aşağıdakine benzer görünecektir:</span><span class="sxs-lookup"><span data-stu-id="86bab-162">hello output will look something like this:</span></span>

![Vurgulanan hello tüm sanal ağ adıyla hello komut satırının ekran görüntüsü.](../media/virtual-machines-linux-cli-migration-classic-resource-manager/vnet.png)

<span data-ttu-id="86bab-164">Yukarıdaki örnek Hello hello **virtualNetworkName** hello tüm adı **"Grubu classicubuntu16 classicubuntu16"**.</span><span class="sxs-lookup"><span data-stu-id="86bab-164">In hello above example, hello **virtualNetworkName** is hello entire name **"Group classicubuntu16 classicubuntu16"**.</span></span>

<span data-ttu-id="86bab-165">İlk olarak, komutu aşağıdaki hello kullanarak hello sanal ağ geçirirseniz doğrulama:</span><span class="sxs-lookup"><span data-stu-id="86bab-165">First, validate if you can migrate hello virtual network using hello following command:</span></span>

```shell
azure network vnet validate-migration <virtualNetworkName>
```

<span data-ttu-id="86bab-166">Tercih ettiğiniz Hello sanal ağ, komutu aşağıdaki hello kullanarak geçiş için hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="86bab-166">Prepare hello virtual network of your choice for migration by using hello following command.</span></span>

    azure network vnet prepare-migration <virtualNetworkName>

<span data-ttu-id="86bab-167">CLI veya hello Azure portal kullanarak sanal makineleri hazırlanmış hello için başlangıç yapılandırmasını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="86bab-167">Check hello configuration for hello prepared virtual machines by using either CLI or hello Azure portal.</span></span> <span data-ttu-id="86bab-168">Geçiş için hazır olmayan ve toogo geri toohello eski durum istiyorsanız, komutu aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="86bab-168">If you are not ready for migration and you want toogo back toohello old state, use hello following command.</span></span>

    azure network vnet abort-migration <virtualNetworkName>

<span data-ttu-id="86bab-169">Merhaba hazırlanan yapılandırma iyi görünüyorsa, ilerlemek ve komut aşağıdaki hello kullanarak hello kaynakları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="86bab-169">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command.</span></span>

    azure network vnet commit-migration <virtualNetworkName>

## <a name="step-5-migrate-a-storage-account"></a><span data-ttu-id="86bab-170">5. adım: bir depolama hesabını geçirin</span><span class="sxs-lookup"><span data-stu-id="86bab-170">Step 5: Migrate a storage account</span></span>
<span data-ttu-id="86bab-171">Merhaba sanal makinelerin geçirilmesine bitirdiğinizde hello depolama hesabını geçirin öneririz.</span><span class="sxs-lookup"><span data-stu-id="86bab-171">Once you're done migrating hello virtual machines, we recommend you migrate hello storage account.</span></span>

<span data-ttu-id="86bab-172">Komutu aşağıdaki hello kullanarak Hello depolama hesabı geçiş için hazırlama</span><span class="sxs-lookup"><span data-stu-id="86bab-172">Prepare hello storage account for migration by using hello following command</span></span>

    azure storage account prepare-migration <storageAccountName>

<span data-ttu-id="86bab-173">Depolama hesabı CLI veya hello Azure portal kullanarak hazırlanmış hello için başlangıç yapılandırmasını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="86bab-173">Check hello configuration for hello prepared storage account by using either CLI or hello Azure portal.</span></span> <span data-ttu-id="86bab-174">Geçiş için hazır olmayan ve toogo geri toohello eski durum istiyorsanız, komutu aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="86bab-174">If you are not ready for migration and you want toogo back toohello old state, use hello following command.</span></span>

    azure storage account abort-migration <storageAccountName>

<span data-ttu-id="86bab-175">Merhaba hazırlanan yapılandırma iyi görünüyorsa, ilerlemek ve komut aşağıdaki hello kullanarak hello kaynakları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="86bab-175">If hello prepared configuration looks good, you can move forward and commit hello resources by using hello following command.</span></span>

    azure storage account commit-migration <storageAccountName>

## <a name="next-steps"></a><span data-ttu-id="86bab-176">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="86bab-176">Next steps</span></span>

* [<span data-ttu-id="86bab-177">Klasik tooAzure Resource Manager Iaas kaynaklardan platform desteklenen geçişini genel bakış</span><span class="sxs-lookup"><span data-stu-id="86bab-177">Overview of platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="86bab-178">Teknik ya ilişkin ayrıntılar platform desteklenen geçiş Klasik tooAzure Kaynak Yöneticisi'nden</span><span class="sxs-lookup"><span data-stu-id="86bab-178">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="86bab-179">Iaas kaynaklardan Klasik tooAzure Kaynak Yöneticisi geçişini planlama</span><span class="sxs-lookup"><span data-stu-id="86bab-179">Planning for migration of IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="86bab-180">Klasik tooAzure Resource Manager PowerShell toomigrate Iaas kaynakları kullanın</span><span class="sxs-lookup"><span data-stu-id="86bab-180">Use PowerShell toomigrate IaaS resources from classic tooAzure Resource Manager</span></span>](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="86bab-181">Iaas kaynaklardan Klasik tooAzure Kaynak Yöneticisi geçişini ile Yardım için topluluk araçları</span><span class="sxs-lookup"><span data-stu-id="86bab-181">Community tools for assisting with migration of IaaS resources from classic tooAzure Resource Manager</span></span>](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="86bab-182">En sık karşılaşılan geçiş hatalarını gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="86bab-182">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="86bab-183">Gözden geçirme hello en sık Klasik tooAzure Kaynak Yöneticisi geçirme Iaas kaynaklardan hakkında sorular</span><span class="sxs-lookup"><span data-stu-id="86bab-183">Review hello most frequently asked questions about migrating IaaS resources from classic tooAzure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
