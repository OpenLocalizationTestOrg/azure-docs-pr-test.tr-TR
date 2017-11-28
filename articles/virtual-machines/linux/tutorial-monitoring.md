---
title: aaaMonitor Linux sanal makineleri azure'da | Microsoft Docs
description: "Nasıl toomonitor önyükleme tanılama ve performans ölçümleri azure'da bir Linux sanal makine hakkında bilgi edinin"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 282da0f03ab0bf37bd44750c22813ca8d1c89560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="bbe1e-103">Nasıl toomonitor azure'da bir Linux sanal makine</span><span class="sxs-lookup"><span data-stu-id="bbe1e-103">How toomonitor a Linux virtual machine in Azure</span></span>

<span data-ttu-id="bbe1e-104">Azure, sanal makineleri (VM'ler) düzgün çalışmasını tooensure önyükleme tanılama ve performans ölçümleri gözden geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-104">tooensure your virtual machines (VMs) in Azure are running correctly, you can review boot diagnostics and performance metrics.</span></span> <span data-ttu-id="bbe1e-105">Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="bbe1e-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bbe1e-106">Önyükleme tanılaması hello VM üzerinde etkinleştir</span><span class="sxs-lookup"><span data-stu-id="bbe1e-106">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="bbe1e-107">Önyükleme tanılamasını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="bbe1e-107">View boot diagnostics</span></span>
> * <span data-ttu-id="bbe1e-108">Ana bilgisayar metrikleri görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="bbe1e-108">View host metrics</span></span>
> * <span data-ttu-id="bbe1e-109">Merhaba VM tanılama uzantısını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="bbe1e-109">Enable diagnostics extension on hello VM</span></span>
> * <span data-ttu-id="bbe1e-110">VM metrikleri görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="bbe1e-110">View VM metrics</span></span>
> * <span data-ttu-id="bbe1e-111">Tanılama ölçümleri temel uyarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bbe1e-111">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="bbe1e-112">Gelişmiş izleme işlevini ayarlama</span><span class="sxs-lookup"><span data-stu-id="bbe1e-112">Set up advanced monitoring</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="bbe1e-113">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="bbe1e-114">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="bbe1e-115">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bbe1e-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-vm"></a><span data-ttu-id="bbe1e-116">VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="bbe1e-116">Create VM</span></span>

<span data-ttu-id="bbe1e-117">toosee tanılama ve eylem ölçümleri, VM gerekir.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-117">toosee diagnostics and metrics in action, you need a VM.</span></span> <span data-ttu-id="bbe1e-118">İlk olarak, bir kaynak grubu ile oluşturmak [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="bbe1e-118">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="bbe1e-119">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroupMonitor* hello içinde *eastus* konumu.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-119">hello following example creates a resource group named *myResourceGroupMonitor* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupMonitor --location eastus
```

<span data-ttu-id="bbe1e-120">Şimdi bir VM oluşturmak [az vm oluşturma](https://docs.microsoft.com/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="bbe1e-120">Now create a VM with [az vm create](https://docs.microsoft.com/cli/azure/vm#create).</span></span> <span data-ttu-id="bbe1e-121">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVM*:</span><span class="sxs-lookup"><span data-stu-id="bbe1e-121">hello following example creates a VM named *myVM*:</span></span>

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --image UbuntuLTS \
  --admin-username azureuser \
  --generate-ssh-keys
```

## <a name="enable-boot-diagnostics"></a><span data-ttu-id="bbe1e-122">Önyükleme tanılaması etkinleştir</span><span class="sxs-lookup"><span data-stu-id="bbe1e-122">Enable boot diagnostics</span></span>

<span data-ttu-id="bbe1e-123">Linux VM'ler önyükleme gibi hello önyükleme tanılama uzantısını önyükleme çıkış yakalar ve Azure depolama alanında depolar.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-123">As Linux VMs boot, hello boot diagnostic extension captures boot output and stores it in Azure storage.</span></span> <span data-ttu-id="bbe1e-124">Bu veriler kullanılan tootroubleshoot VM önyükleme sorunları olabilir.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-124">This data can be used tootroubleshoot VM boot issues.</span></span> <span data-ttu-id="bbe1e-125">Hello Azure CLI kullanarak bir Linux VM oluştururken önyükleme tanılaması otomatik olarak etkin değildir.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-125">Boot diagnostics are not automatically enabled when you create a Linux VM using hello Azure CLI.</span></span>

<span data-ttu-id="bbe1e-126">Önyükleme tanılaması etkinleştirmeden önce depolama hesabının önyükleme günlüklerini depolamak üzere oluşturulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-126">Before enabling boot diagnostics, a storage account needs toobe created for storing boot logs.</span></span> <span data-ttu-id="bbe1e-127">Depolama hesapları 3 ile 24 karakter arasında olması genel olarak benzersiz bir ad olmalıdır ve yalnızca sayılar ve küçük harf içermelidir.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-127">Storage accounts must have a globally unique name, be between 3 and 24 characters, and must contain only numbers and lowercase letters.</span></span> <span data-ttu-id="bbe1e-128">Merhaba ile depolama hesabı oluşturma [az depolama hesabı oluşturma](/cli/azure/storage/account#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-128">Create a storage account with hello [az storage account create](/cli/azure/storage/account#create) command.</span></span> <span data-ttu-id="bbe1e-129">Bu örnekte kullanılan toocreate benzersiz depolama hesabı adı olduğu rastgele bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-129">In this example, a random string is used toocreate a unique storage account name.</span></span> 

```azurecli-interactive 
storageacct=mydiagdata$RANDOM

az storage account create \
  --resource-group myResourceGroupMonitor \
  --name $storageacct \
  --sku Standard_LRS \
  --location eastus
```

<span data-ttu-id="bbe1e-130">Önyükleme tanılaması etkinleştirirken hello URI toohello blob depolama kapsayıcısını gereklidir.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-130">When enabling boot diagnostics, hello URI toohello blob storage container is needed.</span></span> <span data-ttu-id="bbe1e-131">Merhaba aşağıdaki komutu sorgularını depolama hesabı tooreturn bu URI hello.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-131">hello following command queries hello storage account tooreturn this URI.</span></span> <span data-ttu-id="bbe1e-132">Merhaba URI değeri değişken adlarında depolanan *bloburi*, hello sonraki adımda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-132">hello URI value is stored in a variable names *bloburi*, which is used in hello next step.</span></span>

```azurecli-interactive 
bloburi=$(az storage account show --resource-group myResourceGroupMonitor --name $storageacct --query 'primaryEndpoints.blob' -o tsv)
```

<span data-ttu-id="bbe1e-133">Önyükleme Tanılaması ile şimdi etkinleştirmek [az vm önyükleme-tanılamayı etkinleştirin](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable).</span><span class="sxs-lookup"><span data-stu-id="bbe1e-133">Now enable boot diagnostics with [az vm boot-diagnostics enable](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="bbe1e-134">Merhaba `--storage` hello blob URI'si toplanan hello önceki adımda değerdir.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-134">hello `--storage` value is hello blob URI collected in hello previous step.</span></span>

```azurecli-interactive 
az vm boot-diagnostics enable \
  --resource-group myResourceGroupMonitor \
  --name myVM \
  --storage $bloburi
```


## <a name="view-boot-diagnostics"></a><span data-ttu-id="bbe1e-135">Önyükleme tanılamasını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="bbe1e-135">View boot diagnostics</span></span>

<span data-ttu-id="bbe1e-136">Önyükleme tanılaması etkin olduğunda, her zaman durdurup hello VM başlatmak hello önyükleme işlemi hakkında bilgi tooa günlük dosyasına yazılır.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-136">When boot diagnostics are enabled, each time you stop and start hello VM, information about hello boot process is written tooa log file.</span></span> <span data-ttu-id="bbe1e-137">Bu örnekte, ilk hello VM hello ile serbest bırakma [az vm serbest bırakma](/cli/azure/vm#deallocate) gibi komut:</span><span class="sxs-lookup"><span data-stu-id="bbe1e-137">For this example, first deallocate hello VM with hello [az vm deallocate](/cli/azure/vm#deallocate) command as follows:</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="bbe1e-138">Merhaba VM ile Merhaba Şimdi Başlat [az vm başlangıç]( /cli/azure/vm#stop) gibi komut:</span><span class="sxs-lookup"><span data-stu-id="bbe1e-138">Now start hello VM with hello [az vm start]( /cli/azure/vm#stop) command as follows:</span></span>

```azurecli-interactive 
az vm start --resource-group myResourceGroupMonitor --name myVM
```

<span data-ttu-id="bbe1e-139">Merhaba önyükleme Tanılama verileri alabilirsiniz *myVM* hello ile [az vm önyükleme tanılaması get-önyükleme-günlük](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) gibi komut:</span><span class="sxs-lookup"><span data-stu-id="bbe1e-139">You can get hello boot diagnostic data for *myVM* with hello [az vm boot-diagnostics get-boot-log](https://docs.microsoft.com/cli/azure/vm/boot-diagnostics#get-boot-log) command as follows:</span></span>

```azurecli-interactive 
az vm boot-diagnostics get-boot-log --resource-group myResourceGroupMonitor --name myVM
```


## <a name="view-host-metrics"></a><span data-ttu-id="bbe1e-140">Ana bilgisayar metrikleri görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="bbe1e-140">View host metrics</span></span>

<span data-ttu-id="bbe1e-141">Bir Linux VM ayrılmış bir ana bilgisayar ile etkileşime giren Azure sahiptir.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-141">A Linux VM has a dedicated host in Azure that it interacts with.</span></span> <span data-ttu-id="bbe1e-142">Ölçümleri hello ana bilgisayar için otomatik olarak toplanır ve hello Azure portalında şu şekilde görüntülenebilir:</span><span class="sxs-lookup"><span data-stu-id="bbe1e-142">Metrics are automatically collected for hello host and can be viewed in hello Azure portal as follows:</span></span>

1. <span data-ttu-id="bbe1e-143">Hello Azure portal'ı tıklatın **kaynak grupları**seçin **myResourceGroupMonitor**ve ardından **myVM** hello kaynak listesinde.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-143">In hello Azure portal, click **Resource Groups**, select **myResourceGroupMonitor**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="bbe1e-144">Merhaba konak VM gerçekleştiriyor nasıl toosee tıklatın **ölçümleri** hello VM dikey penceresinde hello birini seçip *[ana bilgisayar]* altında ölçümleri **kullanılabilir ölçümler**.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-144">toosee how hello host VM is performing, click **Metrics** on hello VM blade, then select any of hello *[Host]* metrics under **Available metrics**.</span></span>

    ![Ana bilgisayar metrikleri görüntüleyin](./media/tutorial-monitoring/monitor-host-metrics.png)


## <a name="install-diagnostics-extension"></a><span data-ttu-id="bbe1e-146">Tanılama uzantısını yükleyin</span><span class="sxs-lookup"><span data-stu-id="bbe1e-146">Install diagnostics extension</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bbe1e-147">Bu belgede hello Linux tanılama kullanım dışı bırakılmış uzantısının 2.3 sürümü açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-147">This document describes version 2.3 of hello Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="bbe1e-148">Sürüm 2.3 30 Haziran 2018 kadar desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-148">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="bbe1e-149">Merhaba Linux tanılama uzantısını 3.0 sürümü yerine etkinleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-149">Version 3.0 of hello Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="bbe1e-150">Daha fazla bilgi için bkz: [hello belgelerine](./diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="bbe1e-150">For more information, see [hello documentation](./diagnostic-extension.md).</span></span>

<span data-ttu-id="bbe1e-151">Merhaba temel ana ölçümleri kullanılabilir, ancak toosee daha ayrıntılı ve VM özgü ölçümleri, size tooneed tooinstall hello Azure tanılama uzantısını hello VM.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-151">hello basic host metrics are available, but toosee more granular and VM-specific metrics, you tooneed tooinstall hello Azure diagnostics extension on hello VM.</span></span> <span data-ttu-id="bbe1e-152">Hello Azure tanılama uzantısını ek izleme ve tanılama veri toobe VM hello alınan sağlar.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-152">hello Azure diagnostics extension allows additional monitoring and diagnostics data toobe retrieved from hello VM.</span></span> <span data-ttu-id="bbe1e-153">Bu performans ölçümleri görüntüleyebilir ve hello VM nasıl gerçekleştireceğini temelinde uyarılar oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-153">You can view these performance metrics and create alerts based on how hello VM performs.</span></span> <span data-ttu-id="bbe1e-154">Merhaba tanılama uzantısını hello Azure portal aşağıdaki şekillerde yüklenir:</span><span class="sxs-lookup"><span data-stu-id="bbe1e-154">hello diagnostic extension is installed through hello Azure portal as follows:</span></span>

1. <span data-ttu-id="bbe1e-155">Hello Azure portal'ı tıklatın **kaynak grupları**seçin **myResourceGroup**ve ardından **myVM** hello kaynak listesinde.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-155">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="bbe1e-156">Tıklatın **tanılama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-156">Click **Diagnosis settings**.</span></span> <span data-ttu-id="bbe1e-157">Merhaba liste gösterir *önyükleme tanılama* hello önceki bölümden zaten etkin.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-157">hello list shows that *Boot diagnostics* are already enabled from hello previous section.</span></span> <span data-ttu-id="bbe1e-158">Merhaba onay kutusu için *temel ölçümleri*.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-158">Click hello check box for *Basic metrics*.</span></span>
1. <span data-ttu-id="bbe1e-159">Merhaba, *depolama hesabı* bölümünde, tooand select hello Gözat *mydiagdata [1234]* hello önceki bölümde oluşturduğunuz hesabı.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-159">In hello *Storage account* section, browse tooand select hello *mydiagdata[1234]* account created in hello previous section.</span></span>
1. <span data-ttu-id="bbe1e-160">Merhaba tıklatın **kaydetmek** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-160">Click hello **Save** button.</span></span>

    ![Tanılama metrikleri görüntüleyin](./media/tutorial-monitoring/enable-diagnostics-extension.png)


## <a name="view-vm-metrics"></a><span data-ttu-id="bbe1e-162">VM metrikleri görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="bbe1e-162">View VM metrics</span></span>

<span data-ttu-id="bbe1e-163">Hello hello VM ölçümleri görüntüleyebilir aynı şekilde hello konak VM ölçümleri görüntülenebilir:</span><span class="sxs-lookup"><span data-stu-id="bbe1e-163">You can view hello VM metrics in hello same way that you viewed hello host VM metrics:</span></span>

1. <span data-ttu-id="bbe1e-164">Hello Azure portal'ı tıklatın **kaynak grupları**seçin **myResourceGroup**ve ardından **myVM** hello kaynak listesinde.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-164">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
1. <span data-ttu-id="bbe1e-165">Merhaba VM gerçekleştiriyor nasıl toosee tıklatın **ölçümleri** üzerinde VM dikey penceresinde hello ve hello tanılama ölçümleri altında birini seçin **kullanılabilir ölçümler**.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-165">toosee how hello VM is performing, click **Metrics** on hello VM blade, and then select any of hello diagnostics metrics under **Available metrics**.</span></span>

    ![VM metrikleri görüntüleyin](./media/tutorial-monitoring/monitor-vm-metrics.png)


## <a name="create-alerts"></a><span data-ttu-id="bbe1e-167">Uyarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bbe1e-167">Create alerts</span></span>

<span data-ttu-id="bbe1e-168">Özel performans ölçümleri temelinde uyarılar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-168">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="bbe1e-169">Uyarılar, ortalama CPU kullanımını belirli bir eşiği veya kullanılabilir boş disk alanı aştığında belirli bir bir miktar düşene kullanılan toonotify örneğin olabilir.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-169">Alerts can be used toonotify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="bbe1e-170">Uyarıları hello Azure portalında görüntülenen veya e-posta ile gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-170">Alerts are displayed in hello Azure portal or can be sent via email.</span></span> <span data-ttu-id="bbe1e-171">Azure Otomasyon çalışma kitabı veya Azure Logic Apps içinde oluşturulan yanıt tooalerts tetikleyebilir.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-171">You can also trigger Azure Automation runbooks or Azure Logic Apps in response tooalerts being generated.</span></span>

<span data-ttu-id="bbe1e-172">Merhaba aşağıdaki örnek ortalama CPU kullanımı için bir uyarı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-172">hello following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="bbe1e-173">Hello Azure portal'ı tıklatın **kaynak grupları**seçin **myResourceGroup**ve ardından **myVM** hello kaynak listesinde.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-173">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="bbe1e-174">Tıklatın **uyarı kuralları** hello VM dikey penceresinde, ardından **ölçüm uyarı Ekle** hello uyarıları dikey hello üstte.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-174">Click **Alert rules** on hello VM blade, then click **Add metric alert** across hello top of hello alerts blade.</span></span>
4. <span data-ttu-id="bbe1e-175">Sağlayan bir **adı** , uyarının gibi *myAlertRule*</span><span class="sxs-lookup"><span data-stu-id="bbe1e-175">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="bbe1e-176">tootrigger CPU yüzdesi beş dakika 1.0 aştığında bir uyarı, seçili diğer Varsayılanları tüm hello bırakın.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-176">tootrigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all hello other defaults selected.</span></span>
6. <span data-ttu-id="bbe1e-177">İsteğe bağlı olarak, hello kutuyu için *sahipleri, Katkıda Bulunanlar ve okuyucular e-posta* toosend e-posta bildirimi.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-177">Optionally, check hello box for *Email owners, contributors, and readers* toosend email notification.</span></span> <span data-ttu-id="bbe1e-178">Merhaba varsayılan toopresent hello Portalı'nda bir bildirim eylemdir.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-178">hello default action is toopresent a notification in hello portal.</span></span>
7. <span data-ttu-id="bbe1e-179">Merhaba tıklatın **Tamam** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-179">Click hello **OK** button.</span></span>


## <a name="advanced-monitoring"></a><span data-ttu-id="bbe1e-180">Gelişmiş izleme</span><span class="sxs-lookup"><span data-stu-id="bbe1e-180">Advanced monitoring</span></span> 

<span data-ttu-id="bbe1e-181">Kullanarak VM'yi izleme daha gelişmiş yapabileceğiniz [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span><span class="sxs-lookup"><span data-stu-id="bbe1e-181">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="bbe1e-182">Zaten yapmadıysanız, için kaydolabilirsiniz bir [ücretsiz deneme sürümü](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-182">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="bbe1e-183">Erişim toohello OMS portalı varsa, hello çalışma alanı anahtarı ve çalışma alanı kimliği hello ayarları dikey penceresinde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-183">When you have access toohello OMS portal, you can find hello workspace key and workspace identifier on hello Settings blade.</span></span> <span data-ttu-id="bbe1e-184">Değiştir < çalışma alanı anahtarı > ve < çalışma alanı kimliği > hello için değerlerle, OMS çalışma ve ardından, kullanabilirsiniz **az vm uzantısı kümesi** tooadd hello OMS uzantısı toohello VM:</span><span class="sxs-lookup"><span data-stu-id="bbe1e-184">Replace <workspace-key> and <workspace-id> with hello values for from your OMS workspace and then you can use **az vm extension set** tooadd hello OMS extension toohello VM:</span></span>

```azurecli-interactive 
az vm extension set \
  --resource-group myResourceGroupMonitor \
  --vm-name myVM \
  --name OmsAgentForLinux \
  --publisher Microsoft.EnterpriseCloud.Monitoring \
  --version 1.3 \
  --protected-settings '{"workspaceKey": "<workspace-key>"}' \
  --settings '{"workspaceId": "<workspace-id>"}'
```

<span data-ttu-id="bbe1e-185">Merhaba günlük arama dikey penceresinde hello OMS portalı görmelisiniz *myVM* ne hello resim aşağıdaki gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="bbe1e-185">On hello Log Search blade of hello OMS portal, you should see *myVM* such as what is shown in hello following picture:</span></span>

![OMS dikey penceresi](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="bbe1e-187">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bbe1e-187">Next steps</span></span>

<span data-ttu-id="bbe1e-188">Bu öğreticide yapılandırılmış ve sanal makineleri Azure Güvenlik Merkezi ile gözden.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-188">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="bbe1e-189">Şunları öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="bbe1e-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bbe1e-190">Önyükleme tanılaması hello VM üzerinde etkinleştir</span><span class="sxs-lookup"><span data-stu-id="bbe1e-190">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="bbe1e-191">Önyükleme tanılamasını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="bbe1e-191">View boot diagnostics</span></span>
> * <span data-ttu-id="bbe1e-192">Ana bilgisayar metrikleri görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="bbe1e-192">View host metrics</span></span>
> * <span data-ttu-id="bbe1e-193">Merhaba VM tanılama uzantısını etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="bbe1e-193">Enable diagnostics extension on hello VM</span></span>
> * <span data-ttu-id="bbe1e-194">VM metrikleri görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="bbe1e-194">View VM metrics</span></span>
> * <span data-ttu-id="bbe1e-195">Tanılama ölçümleri temel uyarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bbe1e-195">Create alerts based on diagnostic metrics</span></span>
> * <span data-ttu-id="bbe1e-196">Gelişmiş izleme işlevini ayarlama</span><span class="sxs-lookup"><span data-stu-id="bbe1e-196">Set up advanced monitoring</span></span>

<span data-ttu-id="bbe1e-197">Azure Güvenlik Merkezi hakkında toohello sonraki öğretici toolearn ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="bbe1e-197">Advance toohello next tutorial toolearn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bbe1e-198">VM güvenliğini yönetme</span><span class="sxs-lookup"><span data-stu-id="bbe1e-198">Manage VM security</span></span>](./tutorial-azure-security.md)