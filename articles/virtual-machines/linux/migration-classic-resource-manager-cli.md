---
title: "Azure CLI kullanarak kaynak yöneticisi Vm'leri geçirme | Microsoft Docs"
description: "Bu makalede kaynakları platform desteklenen geçiş Klasikten Azure Resource Manager'da Azure CLI kullanarak anlatılmaktadır"
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
ms.openlocfilehash: a63d758570b09b37b8e51c639267f729521d9ae0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-iaas-resources-from-classic-to-azure-resource-manager-by-using-azure-cli"></a><span data-ttu-id="5f5ec-103">Iaas kaynaklarını Klasikten Azure Resource Manager'da Azure CLI kullanarak geçirme</span><span class="sxs-lookup"><span data-stu-id="5f5ec-103">Migrate IaaS resources from classic to Azure Resource Manager by using Azure CLI</span></span>
<span data-ttu-id="5f5ec-104">Bu adımlar Azure komut satırı arabirimi (CLI) komutları altyapı Klasik dağıtım modeli hizmet (Iaas) kaynaklardan Azure Resource Manager dağıtım modeline olarak geçirmek için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-104">These steps show you how to use Azure command-line interface (CLI) commands to migrate infrastructure as a service (IaaS) resources from the classic deployment model to the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="5f5ec-105">Makale gerektirir [Azure CLI](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="5f5ec-105">The article requires the [Azure CLI](../../cli-install-nodejs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5f5ec-106">Burada açıklanan tüm ıdempotent işlemleridir.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-106">All the operations described here are idempotent.</span></span> <span data-ttu-id="5f5ec-107">Desteklenmeyen bir özellik veya bir yapılandırma hatası başka bir sorun varsa, hazırlama yeniden deneme öneririz, veya tamamlanmaya işlemi.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-107">If you have a problem other than an unsupported feature or a configuration error, we recommend that you retry the prepare, abort, or commit operation.</span></span> <span data-ttu-id="5f5ec-108">Platform sonra eylemi yeniden deneyecek.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-108">The platform will then try the action again.</span></span>
> 
> 

<br>
<span data-ttu-id="5f5ec-109">İşte adımları geçiş işlemi sırasında yürütülmesi gerekir siparişi tanımlamak için bir akış çizelgesi</span><span class="sxs-lookup"><span data-stu-id="5f5ec-109">Here is a flowchart to identify the order in which steps need to be executed during a migration process</span></span>

![Geçiş adımlarını gösteren ekran görüntüsü](../windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-prepare-for-migration"></a><span data-ttu-id="5f5ec-111">1. adım: geçiş için hazırlama</span><span class="sxs-lookup"><span data-stu-id="5f5ec-111">Step 1: Prepare for migration</span></span>
<span data-ttu-id="5f5ec-112">Geçirme Iaas kaynaklardan Klasik Kaynak Yöneticisi değerlendirirken öneririz birkaç en iyi uygulamalar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="5f5ec-112">Here are a few best practices that we recommend as you evaluate migrating IaaS resources from classic to Resource Manager:</span></span>

* <span data-ttu-id="5f5ec-113">Okuyun [desteklenmeyen yapılandırmaları veya özellikleri listesi](../windows/migration-classic-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5f5ec-113">Read through the [list of unsupported configurations or features](../windows/migration-classic-resource-manager-overview.md).</span></span> <span data-ttu-id="5f5ec-114">Desteklenmeyen yapılandırmaları veya özellikleri kullanan sanal makineler varsa, duyurdu özellik/yapılandırma desteği beklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-114">If you have virtual machines that use unsupported configurations or features, we recommend that you wait for the feature/configuration support to be announced.</span></span> <span data-ttu-id="5f5ec-115">Alternatif olarak, bu özelliği kaldırmak veya gereksinimlerinize uygun değilse, geçiş etkinleştirmek için bu yapılandırma dışında taşıyın.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-115">Alternatively, you can remove that feature or move out of that configuration to enable migration if it suits your needs.</span></span>
* <span data-ttu-id="5f5ec-116">Bugün, altyapı ve uygulamalarınızı dağıtma komut otomatik değilse, geçiş için bu komut dosyalarını kullanarak benzer bir test Kurulum oluşturmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-116">If you have automated scripts that deploy your infrastructure and applications today, try to create a similar test setup by using those scripts for migration.</span></span> <span data-ttu-id="5f5ec-117">Alternatif olarak, Azure portalını kullanarak örnek ortamları ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-117">Alternatively, you can set up sample environments by using the Azure portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5f5ec-118">Uygulama ağ geçitleri, Klasik geçiş için kaynak yöneticisi için şu anda desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-118">Application Gateways are not currently supported for migration from classic to Resource Manager.</span></span> <span data-ttu-id="5f5ec-119">Bir uygulama ağ geçidi Klasik sanal ağla geçirmek için ağ taşımak için bir hazırlama işlemi çalıştırmadan önce ağ geçidi kaldırın.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-119">To migrate a classic virtual network with an Application gateway, remove the gateway before running a Prepare operation to move the network.</span></span> <span data-ttu-id="5f5ec-120">Geçişi tamamladıktan sonra Azure Kaynak Yöneticisi'nde ağ geçidi yeniden bağlanın.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-120">After you complete the migration, reconnect the gateway in Azure Resource Manager.</span></span> 
>
><span data-ttu-id="5f5ec-121">ExpressRoute ağ geçidi başka bir Abonelikteki ExpressRoute bağlantı hatları bağlanma otomatik olarak geçirilemez.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-121">ExpressRoute gateways connecting to ExpressRoute circuits in another subscription cannot be migrated automatically.</span></span> <span data-ttu-id="5f5ec-122">Böyle durumlarda, ExpressRoute ağ geçidi kaldırın, sanal ağ geçirmek ve ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-122">In such cases, remove the ExpressRoute gateway, migrate the virtual network and recreate the gateway.</span></span> <span data-ttu-id="5f5ec-123">Lütfen bakın [geçirmek ExpressRoute bağlantı hattına ve Resource Manager dağıtım modeli için Klasik sanal ağlar ilişkili](../../expressroute/expressroute-migration-classic-resource-manager.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-123">Please see [Migrate ExpressRoute circuits and associated virtual networks from the classic to the Resource Manager deployment model](../../expressroute/expressroute-migration-classic-resource-manager.md) for more information.</span></span>
> 
> 

## <a name="step-2-set-your-subscription-and-register-the-provider"></a><span data-ttu-id="5f5ec-124">2. adım: aboneliğinizi ayarlamak ve sağlayıcısını Kaydet</span><span class="sxs-lookup"><span data-stu-id="5f5ec-124">Step 2: Set your subscription and register the provider</span></span>
<span data-ttu-id="5f5ec-125">Geçiş senaryoları için her iki Klasik ortamınızı ayarlamanız gerekir ve Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-125">For migration scenarios, you need to set up your environment for both classic and Resource Manager.</span></span> <span data-ttu-id="5f5ec-126">[Azure CLI yükleme](../../cli-install-nodejs.md) ve [aboneliğinizi seçin](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="5f5ec-126">[Install Azure CLI](../../cli-install-nodejs.md) and [select your subscription](../../xplat-cli-connect.md).</span></span>

<span data-ttu-id="5f5ec-127">Oturum hesabınıza açın.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-127">Sign-in to your account.</span></span>

    azure login

<span data-ttu-id="5f5ec-128">Aşağıdaki komutu kullanarak Azure aboneliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-128">Select the Azure subscription by using the following command.</span></span>

    azure account set "<azure-subscription-name>"

> [!NOTE]
> <span data-ttu-id="5f5ec-129">Kayıt olan bir zaman adım ancak kez geçiş işlemini denemeden önce yapılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-129">Registration is a one time step but it needs to be done once before attempting migration.</span></span> <span data-ttu-id="5f5ec-130">Kaydettirmeden aşağıdaki hata iletisini görürsünüz</span><span class="sxs-lookup"><span data-stu-id="5f5ec-130">Without registering you'll see the following error message</span></span> 
> 
> <span data-ttu-id="5f5ec-131">*BadRequest: Abonelik geçiş için kayıtlı değil.*</span><span class="sxs-lookup"><span data-stu-id="5f5ec-131">*BadRequest : Subscription is not registered for migration.*</span></span> 
> 
> 

<span data-ttu-id="5f5ec-132">Geçiş kaynak sağlayıcısı ile aşağıdaki komutu kullanarak kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-132">Register with the migration resource provider by using the following command.</span></span> <span data-ttu-id="5f5ec-133">Bazı durumlarda, bu komut zaman aşımına uğruyor olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-133">Note that in some cases, this command times out.</span></span> <span data-ttu-id="5f5ec-134">Ancak, kayıt başarılı olur.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-134">However, the registration will be successful.</span></span>

    azure provider register Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="5f5ec-135">Kaydın son beş dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-135">Please wait five minutes for the registration to finish.</span></span> <span data-ttu-id="5f5ec-136">Aşağıdaki komutu kullanarak onay durumunu kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-136">You can check the status of the approval by using the following command.</span></span> <span data-ttu-id="5f5ec-137">RegistrationState olduğundan emin olun `Registered` devam etmeden önce.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-137">Make sure that RegistrationState is `Registered` before you proceed.</span></span>

    azure provider show Microsoft.ClassicInfrastructureMigrate

<span data-ttu-id="5f5ec-138">Şimdi için CLI geçiş `asm` modu.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-138">Now switch CLI to the `asm` mode.</span></span>

    azure config mode asm

## <a name="step-3-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-the-azure-region-of-your-current-deployment-or-vnet"></a><span data-ttu-id="5f5ec-139">3. adım: Geçerli dağıtım veya VNET Azure bölgesinde yeterli Azure Resource Manager sanal makinesi çekirdeğe sahip olduğunuzdan emin olun</span><span class="sxs-lookup"><span data-stu-id="5f5ec-139">Step 3: Make sure you have enough Azure Resource Manager Virtual Machine cores in the Azure region of your current deployment or VNET</span></span>
<span data-ttu-id="5f5ec-140">Bu adım için geçiş gerekir `arm` modu.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-140">For this step you'll need to switch to `arm` mode.</span></span> <span data-ttu-id="5f5ec-141">Aşağıdaki komutla bunu.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-141">Do this with the following command.</span></span>

```
azure config mode arm
```

<span data-ttu-id="5f5ec-142">Azure Kaynak Yöneticisi'nde sahip Çekirdek geçerli miktarını denetlemek için aşağıdaki CLI komutu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-142">You can use the following CLI command to check the current amount of cores you have in Azure Resource Manager.</span></span> <span data-ttu-id="5f5ec-143">Çekirdek kotaları hakkında daha fazla bilgi için bkz: [sınırları ve Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span><span class="sxs-lookup"><span data-stu-id="5f5ec-143">To learn more about core quotas, see [Limits and the Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)</span></span>

```
azure vm list-usage -l "<Your VNET or Deployment's Azure region"
```

<span data-ttu-id="5f5ec-144">İşiniz bittiğinde bu adımı doğrulanıyor, size geri dönebilirsiniz `asm` modu.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-144">Once you're done verifying this step, you can switch back to `asm` mode.</span></span>

    azure config mode asm


## <a name="step-4-option-1---migrate-virtual-machines-in-a-cloud-service"></a><span data-ttu-id="5f5ec-145">4. adım: 1. seçenek - sanal makineler bir bulut hizmetinde geçirme</span><span class="sxs-lookup"><span data-stu-id="5f5ec-145">Step 4: Option 1 - Migrate virtual machines in a cloud service</span></span>
<span data-ttu-id="5f5ec-146">Aşağıdaki komutu kullanarak bulut Hizmetleri listesini almak ve geçirmek istediğiniz bulut hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-146">Get the list of cloud services by using the following command, and then pick the cloud service that you want to migrate.</span></span> <span data-ttu-id="5f5ec-147">Bulut hizmetindeki sanal makineleri bir sanal ağ veya web/çalışan rolleri varsa, bir hata iletisi alırsınız unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-147">Note that if the VMs in the cloud service are in a virtual network or if they have web/worker roles, you will get an error message.</span></span>

    azure service list

<span data-ttu-id="5f5ec-148">Bulut hizmeti için dağıtım adı ayrıntılı çıktısını almak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-148">Run the following command to get the deployment name for the cloud service from the verbose output.</span></span> <span data-ttu-id="5f5ec-149">Çoğu durumda, dağıtım adı bulut hizmet adı ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-149">In most cases, the deployment name is the same as the cloud service name.</span></span>

    azure service show <serviceName> -vv

<span data-ttu-id="5f5ec-150">İlk olarak, aşağıdaki komutları kullanarak bulut hizmeti geçirirseniz doğrulama:</span><span class="sxs-lookup"><span data-stu-id="5f5ec-150">First, validate if you can migrate the cloud service using the following commands:</span></span>

```shell
azure service deployment validate-migration <serviceName> <deploymentName> new "" "" ""
```

<span data-ttu-id="5f5ec-151">Sanal makine bulut hizmeti geçiş için hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-151">Prepare the virtual machines in the cloud service for migration.</span></span> <span data-ttu-id="5f5ec-152">Aralarından seçim yapabileceğiniz iki seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-152">You have two options to choose from.</span></span>

<span data-ttu-id="5f5ec-153">Platform tarafından oluşturulan bir sanal ağ sanal makineleri geçirmek istiyorsanız, aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-153">If you want to migrate the VMs to a platform-created virtual network, use the following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> new "" "" ""

<span data-ttu-id="5f5ec-154">Resource Manager dağıtım modelinde var olan bir sanal ağa geçirmek istiyorsanız, aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-154">If you want to migrate to an existing virtual network in the Resource Manager deployment model, use the following command.</span></span>

    azure service deployment prepare-migration <serviceName> <deploymentName> existing <destinationVNETResourceGroupName> <subnetName> <vnetName>

<span data-ttu-id="5f5ec-155">Hazırlama işlemi başarılı olduktan sonra sanal makineleri geçiş durumunu alma ve içinde olduklarından emin olmak için ayrıntılı çıktı aracılığıyla bakabilirsiniz `Prepared` durumu.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-155">After the prepare operation is successful, you can look through the verbose output to get the migration state of the VMs and ensure that they are in the `Prepared` state.</span></span>

    azure vm show <vmName> -vv

<span data-ttu-id="5f5ec-156">CLI veya Azure portalını kullanarak hazırlanmış kaynakların yapılandırmasını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-156">Check the configuration for the prepared resources by using either CLI or the Azure portal.</span></span> <span data-ttu-id="5f5ec-157">Geçiş için hazır olmayan ve eski durumuna geri dönmek istiyorsanız aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-157">If you are not ready for migration and you want to go back to the old state, use the following command.</span></span>

    azure service deployment abort-migration <serviceName> <deploymentName>

<span data-ttu-id="5f5ec-158">Hazırlanan yapılandırma iyi görünüyorsa, ilerlemek ve aşağıdaki komutu kullanarak kaynakları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-158">If the prepared configuration looks good, you can move forward and commit the resources by using the following command.</span></span>

    azure service deployment commit-migration <serviceName> <deploymentName>



## <a name="step-4-option-2----migrate-virtual-machines-in-a-virtual-network"></a><span data-ttu-id="5f5ec-159">4. adım: 2. seçenek - bir sanal ağdaki sanal makineleri geçirme</span><span class="sxs-lookup"><span data-stu-id="5f5ec-159">Step 4: Option 2 -  Migrate virtual machines in a virtual network</span></span>
<span data-ttu-id="5f5ec-160">Geçirmek istediğiniz sanal ağ seçin.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-160">Pick the virtual network that you want to migrate.</span></span> <span data-ttu-id="5f5ec-161">Sanal ağ ile desteklenmeyen yapılandırmalar web/çalışan rolleri veya VM'ler içeriyorsa, bir doğrulama hata iletisi alırsınız unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-161">Note that if the virtual network contains web/worker roles or VMs with unsupported configurations, you will get a validation error message.</span></span>

<span data-ttu-id="5f5ec-162">Tüm sanal ağları, aşağıdaki komutu kullanarak abonelikte alın.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-162">Get all the virtual networks in the subscription by using the following command.</span></span>

    azure network vnet list

<span data-ttu-id="5f5ec-163">Çıktı aşağıdakine benzer görünecektir:</span><span class="sxs-lookup"><span data-stu-id="5f5ec-163">The output will look something like this:</span></span>

![Vurgulanan tüm sanal ağ adıyla komut satırının ekran görüntüsü.](../media/virtual-machines-linux-cli-migration-classic-resource-manager/vnet.png)

<span data-ttu-id="5f5ec-165">Yukarıdaki örnekte, **virtualNetworkName** tüm adı **"Grubu classicubuntu16 classicubuntu16"**.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-165">In the above example, the **virtualNetworkName** is the entire name **"Group classicubuntu16 classicubuntu16"**.</span></span>

<span data-ttu-id="5f5ec-166">İlk olarak, aşağıdaki komutu kullanarak sanal ağ geçirirseniz doğrulama:</span><span class="sxs-lookup"><span data-stu-id="5f5ec-166">First, validate if you can migrate the virtual network using the following command:</span></span>

```shell
azure network vnet validate-migration <virtualNetworkName>
```

<span data-ttu-id="5f5ec-167">Seçtiğiniz sanal ağ, aşağıdaki komutu kullanarak geçiş için hazırlayın.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-167">Prepare the virtual network of your choice for migration by using the following command.</span></span>

    azure network vnet prepare-migration <virtualNetworkName>

<span data-ttu-id="5f5ec-168">CLI veya Azure portalını kullanarak hazırlanmış sanal makineler için yapılandırmayı denetleyin.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-168">Check the configuration for the prepared virtual machines by using either CLI or the Azure portal.</span></span> <span data-ttu-id="5f5ec-169">Geçiş için hazır olmayan ve eski durumuna geri dönmek istiyorsanız aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-169">If you are not ready for migration and you want to go back to the old state, use the following command.</span></span>

    azure network vnet abort-migration <virtualNetworkName>

<span data-ttu-id="5f5ec-170">Hazırlanan yapılandırma iyi görünüyorsa, ilerlemek ve aşağıdaki komutu kullanarak kaynakları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-170">If the prepared configuration looks good, you can move forward and commit the resources by using the following command.</span></span>

    azure network vnet commit-migration <virtualNetworkName>

## <a name="step-5-migrate-a-storage-account"></a><span data-ttu-id="5f5ec-171">5. adım: bir depolama hesabını geçirin</span><span class="sxs-lookup"><span data-stu-id="5f5ec-171">Step 5: Migrate a storage account</span></span>
<span data-ttu-id="5f5ec-172">İşiniz bittiğinde sanal makineleri geçiriyorsanız, depolama hesabı geçir öneririz.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-172">Once you're done migrating the virtual machines, we recommend you migrate the storage account.</span></span>

<span data-ttu-id="5f5ec-173">Aşağıdaki komutu kullanarak depolama hesabı geçiş için hazırlama</span><span class="sxs-lookup"><span data-stu-id="5f5ec-173">Prepare the storage account for migration by using the following command</span></span>

    azure storage account prepare-migration <storageAccountName>

<span data-ttu-id="5f5ec-174">CLI veya Azure portalını kullanarak hazırlanmış depolama hesabı için yapılandırmasını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-174">Check the configuration for the prepared storage account by using either CLI or the Azure portal.</span></span> <span data-ttu-id="5f5ec-175">Geçiş için hazır olmayan ve eski durumuna geri dönmek istiyorsanız aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-175">If you are not ready for migration and you want to go back to the old state, use the following command.</span></span>

    azure storage account abort-migration <storageAccountName>

<span data-ttu-id="5f5ec-176">Hazırlanan yapılandırma iyi görünüyorsa, ilerlemek ve aşağıdaki komutu kullanarak kaynakları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="5f5ec-176">If the prepared configuration looks good, you can move forward and commit the resources by using the following command.</span></span>

    azure storage account commit-migration <storageAccountName>

## <a name="next-steps"></a><span data-ttu-id="5f5ec-177">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5f5ec-177">Next steps</span></span>

* [<span data-ttu-id="5f5ec-178">Platform desteklenen geçişi Iaas Klasik kaynaklardan Azure Resource Manager'a genel bakış</span><span class="sxs-lookup"><span data-stu-id="5f5ec-178">Overview of platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="5f5ec-179">Teknik ya ilişkin ayrıntılar platform desteklenen geçiş Klasik'ten Azure Kaynak Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="5f5ec-179">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="5f5ec-180">IaaS kaynaklarının Klasik’ten Azure Resource Manager’a geçişini planlama</span><span class="sxs-lookup"><span data-stu-id="5f5ec-180">Planning for migration of IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="5f5ec-181">Iaas kaynaklarına Klasikten Azure Resource Manager geçirmek için PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="5f5ec-181">Use PowerShell to migrate IaaS resources from classic to Azure Resource Manager</span></span>](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="5f5ec-182">Iaas Klasik kaynaklardan Azure Resource Manager için geçiş ile Yardım için topluluk araçları</span><span class="sxs-lookup"><span data-stu-id="5f5ec-182">Community tools for assisting with migration of IaaS resources from classic to Azure Resource Manager</span></span>](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="5f5ec-183">En sık karşılaşılan geçiş hatalarını gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="5f5ec-183">Review most common migration errors</span></span>](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="5f5ec-184">Gözden geçirme Iaas kaynaklardan Klasik Azure Kaynak Yöneticisi hakkında en sık sorulan sorular</span><span class="sxs-lookup"><span data-stu-id="5f5ec-184">Review the most frequently asked questions about migrating IaaS resources from classic to Azure Resource Manager</span></span>](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
