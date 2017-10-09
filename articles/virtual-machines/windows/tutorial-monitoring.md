---
title: aaaAzure Windows sanal makineler ve izleme | Microsoft Docs
description: "Öğretici - Azure PowerShell ile Windows sanal makine İzleyicisi"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/04/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 191dc5a30d41c25a9e38f8ec2a32efdc05e03015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-windows-virtual-machine-with-azure-powershell"></a><span data-ttu-id="ab37a-103">Windows sanal makinesi Azure PowerShell ile izleme</span><span class="sxs-lookup"><span data-stu-id="ab37a-103">Monitor a Windows Virtual Machine with Azure PowerShell</span></span>

<span data-ttu-id="ab37a-104">Azure izleme aracıları toocollect önyükleme kullanır ve Azure VM'ler, performans verileri Azure depolama alanında bu verileri depolamak ve portal, hello Azure PowerShell modülü ve hello Azure CLI aracılığıyla erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="ab37a-104">Azure monitoring uses agents toocollect boot and performance data from Azure VMs, store this data in Azure storage, and make it accessible through portal, hello Azure PowerShell module, and hello Azure CLI.</span></span> <span data-ttu-id="ab37a-105">Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="ab37a-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ab37a-106">Bir VM üzerinde önyükleme tanılamayı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="ab37a-106">Enable boot diagnostics on a VM</span></span>
> * <span data-ttu-id="ab37a-107">Önyükleme tanılamasını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="ab37a-107">View boot diagnostics</span></span>
> * <span data-ttu-id="ab37a-108">VM konak metrikleri görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="ab37a-108">View VM host metrics</span></span>
> * <span data-ttu-id="ab37a-109">Merhaba tanılama uzantısını yükleyin</span><span class="sxs-lookup"><span data-stu-id="ab37a-109">Install hello diagnostics extension</span></span>
> * <span data-ttu-id="ab37a-110">VM metrikleri görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="ab37a-110">View VM metrics</span></span>
> * <span data-ttu-id="ab37a-111">Bir uyarı oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="ab37a-111">Create an alert</span></span>
> * <span data-ttu-id="ab37a-112">Gelişmiş izleme işlevini ayarlama</span><span class="sxs-lookup"><span data-stu-id="ab37a-112">Set up advanced monitoring</span></span>

<span data-ttu-id="ab37a-113">Bu öğretici hello Azure PowerShell modülü 3,6 veya sonraki bir sürümü gerektiriyor.</span><span class="sxs-lookup"><span data-stu-id="ab37a-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="ab37a-114">Çalıştırma ` Get-Module -ListAvailable AzureRM` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="ab37a-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="ab37a-115">Tooupgrade gerekirse bkz [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="ab37a-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="ab37a-116">Bu öğreticide toocomplete hello örnek, mevcut bir sanal makine olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ab37a-116">toocomplete hello example in this tutorial, you must have an existing virtual machine.</span></span> <span data-ttu-id="ab37a-117">Gerekirse, bu [komut dosyası örneği](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) sizin için bir tane oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab37a-117">If needed, this [script sample](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) can create one for you.</span></span> <span data-ttu-id="ab37a-118">Merhaba öğreticide çalışırken hello kaynak grubu, sanal makine adını ve konumunu değiştirmek gerektiğinde.</span><span class="sxs-lookup"><span data-stu-id="ab37a-118">When working through hello tutorial, replace hello resource group, VM name, and location where needed.</span></span>

## <a name="view-boot-diagnostics"></a><span data-ttu-id="ab37a-119">Önyükleme tanılamasını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="ab37a-119">View boot diagnostics</span></span>

<span data-ttu-id="ab37a-120">Windows sanal makineleri yedeklemek önyükleme gibi hello önyükleme Tanılama Aracı sorun giderme amacıyla kullanılabilir ekran çıkışına yakalar.</span><span class="sxs-lookup"><span data-stu-id="ab37a-120">As Windows virtual machines boot up, hello boot diagnostic agent captures screen output that can be used for troubleshooting purpose.</span></span> <span data-ttu-id="ab37a-121">Bu özellik varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="ab37a-121">This capability is enabled by default.</span></span> <span data-ttu-id="ab37a-122">Merhaba ekran görüntüleri de varsayılan olarak oluşturulan bir Azure depolama hesabında depolanan yakalandı.</span><span class="sxs-lookup"><span data-stu-id="ab37a-122">hello captured screen shots are stored in an Azure storage account, which is also created by default.</span></span> 

<span data-ttu-id="ab37a-123">Merhaba önyükleme Tanılama verileri hello alabilirsiniz [Get-AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) komutu.</span><span class="sxs-lookup"><span data-stu-id="ab37a-123">You can get hello boot diagnostic data with hello [Get-AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) command.</span></span> <span data-ttu-id="ab37a-124">Aşağıdaki örneğine hello önyükleme tanılaması hello indirilen toohello kökü olan * c:\* sürücü.</span><span class="sxs-lookup"><span data-stu-id="ab37a-124">In hello following example, boot diagnostics are downloaded toohello root of hello *c:\* drive.</span></span> 

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup -Name myVM -Windows -LocalPath "c:\"
```

## <a name="view-host-metrics"></a><span data-ttu-id="ab37a-125">Ana bilgisayar metrikleri görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="ab37a-125">View host metrics</span></span>

<span data-ttu-id="ab37a-126">Bir Windows VM adanmış bir konak VM ile etkileşime giren Azure sahiptir.</span><span class="sxs-lookup"><span data-stu-id="ab37a-126">A Windows VM has a dedicated Host VM in Azure that it interacts with.</span></span> <span data-ttu-id="ab37a-127">Ölçümleri hello ana bilgisayar için otomatik olarak toplanır ve hello Azure portal görüntülenebilir.</span><span class="sxs-lookup"><span data-stu-id="ab37a-127">Metrics are automatically collected for hello Host and can be viewed in hello Azure portal.</span></span>

1. <span data-ttu-id="ab37a-128">Hello Azure portal'ı tıklatın **kaynak grupları**seçin **myResourceGroup**ve ardından **myVM** hello kaynak listesinde.</span><span class="sxs-lookup"><span data-stu-id="ab37a-128">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="ab37a-129">Tıklatın **ölçümleri** üzerinde VM dikey penceresinde hello ve hello ana ölçümleri altında birini seçin **kullanılabilir ölçümler** hello konak VM gerçekleştirip nasıl toosee.</span><span class="sxs-lookup"><span data-stu-id="ab37a-129">Click **Metrics** on hello VM blade, and then select any of hello Host metrics under **Available metrics** toosee how hello Host VM is performing.</span></span>

    ![Ana bilgisayar metrikleri görüntüleyin](./media/tutorial-monitoring/tutorial-monitor-host-metrics.png)

## <a name="install-diagnostics-extension"></a><span data-ttu-id="ab37a-131">Tanılama uzantısını yükleyin</span><span class="sxs-lookup"><span data-stu-id="ab37a-131">Install diagnostics extension</span></span>

<span data-ttu-id="ab37a-132">Merhaba temel ana ölçümleri kullanılabilir, ancak toosee daha ayrıntılı ve VM özgü ölçümleri, size tooneed tooinstall hello Azure tanılama uzantısını hello VM.</span><span class="sxs-lookup"><span data-stu-id="ab37a-132">hello basic host metrics are available, but toosee more granular and VM-specific metrics, you tooneed tooinstall hello Azure diagnostics extension on hello VM.</span></span> <span data-ttu-id="ab37a-133">Hello Azure tanılama uzantısını ek izleme ve tanılama veri toobe VM hello alınan sağlar.</span><span class="sxs-lookup"><span data-stu-id="ab37a-133">hello Azure diagnostics extension allows additional monitoring and diagnostics data toobe retrieved from hello VM.</span></span> <span data-ttu-id="ab37a-134">Bu performans ölçümleri görüntüleyebilir ve hello VM nasıl gerçekleştireceğini temelinde uyarılar oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="ab37a-134">You can view these performance metrics and create alerts based on how hello VM performs.</span></span> <span data-ttu-id="ab37a-135">Merhaba tanılama uzantısını hello Azure portal aşağıdaki şekillerde yüklenir:</span><span class="sxs-lookup"><span data-stu-id="ab37a-135">hello diagnostic extension is installed through hello Azure portal as follows:</span></span>

1. <span data-ttu-id="ab37a-136">Hello Azure portal'ı tıklatın **kaynak grupları**seçin **myResourceGroup**ve ardından **myVM** hello kaynak listesinde.</span><span class="sxs-lookup"><span data-stu-id="ab37a-136">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="ab37a-137">Tıklatın **tanılama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="ab37a-137">Click **Diagnosis settings**.</span></span> <span data-ttu-id="ab37a-138">Merhaba liste gösterir *önyükleme tanılama* hello önceki bölümden zaten etkin.</span><span class="sxs-lookup"><span data-stu-id="ab37a-138">hello list shows that *Boot diagnostics* are already enabled from hello previous section.</span></span> <span data-ttu-id="ab37a-139">Merhaba onay kutusu için *temel ölçümleri*.</span><span class="sxs-lookup"><span data-stu-id="ab37a-139">Click hello check box for *Basic metrics*.</span></span>
3. <span data-ttu-id="ab37a-140">Merhaba tıklatın **Konuk düzeyinde izlemeyi etkinleştir** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ab37a-140">Click hello **Enable guest-level monitoring** button.</span></span>

    ![Tanılama metrikleri görüntüleyin](./media/tutorial-monitoring/enable-diagnostics-extension.png)

## <a name="view-vm-metrics"></a><span data-ttu-id="ab37a-142">VM metrikleri görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="ab37a-142">View VM metrics</span></span>

<span data-ttu-id="ab37a-143">Hello hello VM ölçümleri görüntüleyebilir aynı şekilde hello konak VM ölçümleri görüntülenebilir:</span><span class="sxs-lookup"><span data-stu-id="ab37a-143">You can view hello VM metrics in hello same way that you viewed hello host VM metrics:</span></span>

1. <span data-ttu-id="ab37a-144">Hello Azure portal'ı tıklatın **kaynak grupları**seçin **myResourceGroup**ve ardından **myVM** hello kaynak listesinde.</span><span class="sxs-lookup"><span data-stu-id="ab37a-144">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="ab37a-145">Merhaba VM gerçekleştiriyor nasıl toosee tıklatın **ölçümleri** üzerinde VM dikey penceresinde hello ve hello tanılama ölçümleri altında birini seçin **kullanılabilir ölçümler**.</span><span class="sxs-lookup"><span data-stu-id="ab37a-145">toosee how hello VM is performing, click **Metrics** on hello VM blade, and then select any of hello diagnostics metrics under **Available metrics**.</span></span>

    ![VM metrikleri görüntüleyin](./media/tutorial-monitoring/monitor-vm-metrics.png)

## <a name="create-alerts"></a><span data-ttu-id="ab37a-147">Uyarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ab37a-147">Create alerts</span></span>

<span data-ttu-id="ab37a-148">Özel performans ölçümleri temelinde uyarılar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab37a-148">You can create alerts based on specific performance metrics.</span></span> <span data-ttu-id="ab37a-149">Uyarılar, ortalama CPU kullanımını belirli bir eşiği veya kullanılabilir boş disk alanı aştığında belirli bir bir miktar düşene kullanılan toonotify örneğin olabilir.</span><span class="sxs-lookup"><span data-stu-id="ab37a-149">Alerts can be used toonotify you when average CPU usage exceeds a certain threshold or available free disk space drops below a certain amount, for example.</span></span> <span data-ttu-id="ab37a-150">Uyarıları hello Azure portalında görüntülenen veya e-posta ile gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="ab37a-150">Alerts are displayed in hello Azure portal or can be sent via email.</span></span> <span data-ttu-id="ab37a-151">Azure Otomasyon çalışma kitabı veya Azure Logic Apps içinde oluşturulan yanıt tooalerts tetikleyebilir.</span><span class="sxs-lookup"><span data-stu-id="ab37a-151">You can also trigger Azure Automation runbooks or Azure Logic Apps in response tooalerts being generated.</span></span>

<span data-ttu-id="ab37a-152">Merhaba aşağıdaki örnek ortalama CPU kullanımı için bir uyarı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ab37a-152">hello following example creates an alert for average CPU usage.</span></span>

1. <span data-ttu-id="ab37a-153">Hello Azure portal'ı tıklatın **kaynak grupları**seçin **myResourceGroup**ve ardından **myVM** hello kaynak listesinde.</span><span class="sxs-lookup"><span data-stu-id="ab37a-153">In hello Azure portal, click **Resource Groups**, select **myResourceGroup**, and then select **myVM** in hello resource list.</span></span>
2. <span data-ttu-id="ab37a-154">Tıklatın **uyarı kuralları** hello VM dikey penceresinde, ardından **ölçüm uyarı Ekle** hello uyarıları dikey hello üstte.</span><span class="sxs-lookup"><span data-stu-id="ab37a-154">Click **Alert rules** on hello VM blade, then click **Add metric alert** across hello top of hello alerts blade.</span></span>
4. <span data-ttu-id="ab37a-155">Sağlayan bir **adı** , uyarının gibi *myAlertRule*</span><span class="sxs-lookup"><span data-stu-id="ab37a-155">Provide a **Name** for your alert, such as *myAlertRule*</span></span>
5. <span data-ttu-id="ab37a-156">tootrigger CPU yüzdesi beş dakika 1.0 aştığında bir uyarı, seçili diğer Varsayılanları tüm hello bırakın.</span><span class="sxs-lookup"><span data-stu-id="ab37a-156">tootrigger an alert when CPU percentage exceeds 1.0 for five minutes, leave all hello other defaults selected.</span></span>
6. <span data-ttu-id="ab37a-157">İsteğe bağlı olarak, hello kutuyu için *sahipleri, Katkıda Bulunanlar ve okuyucular e-posta* toosend e-posta bildirimi.</span><span class="sxs-lookup"><span data-stu-id="ab37a-157">Optionally, check hello box for *Email owners, contributors, and readers* toosend email notification.</span></span> <span data-ttu-id="ab37a-158">Merhaba varsayılan toopresent hello Portalı'nda bir bildirim eylemdir.</span><span class="sxs-lookup"><span data-stu-id="ab37a-158">hello default action is toopresent a notification in hello portal.</span></span>
7. <span data-ttu-id="ab37a-159">Merhaba tıklatın **Tamam** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="ab37a-159">Click hello **OK** button.</span></span>

## <a name="advanced-monitoring"></a><span data-ttu-id="ab37a-160">Gelişmiş izleme</span><span class="sxs-lookup"><span data-stu-id="ab37a-160">Advanced monitoring</span></span> 

<span data-ttu-id="ab37a-161">Kullanarak VM'yi izleme daha gelişmiş yapabileceğiniz [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span><span class="sxs-lookup"><span data-stu-id="ab37a-161">You can do more advanced monitoring of your VM by using [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview).</span></span> <span data-ttu-id="ab37a-162">Zaten yapmadıysanız, için kaydolabilirsiniz bir [ücretsiz deneme sürümü](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="ab37a-162">If you haven't already done so, you can sign up for a [free trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) of Operations Management Suite.</span></span>

<span data-ttu-id="ab37a-163">Erişim toohello OMS portalı varsa, hello çalışma alanı anahtarı ve çalışma alanı kimliği hello ayarları dikey penceresinde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab37a-163">When you have access toohello OMS portal, you can find hello workspace key and workspace identifier on hello Settings blade.</span></span> <span data-ttu-id="ab37a-164">Kullanım hello [kümesi AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) dolguya tootooadd hello OMS uzantısı toohello VM.</span><span class="sxs-lookup"><span data-stu-id="ab37a-164">Use hello [Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) cmmand tootooadd hello OMS extension toohello VM.</span></span> <span data-ttu-id="ab37a-165">Güncelleştirme hello değişkeni örnek tooreflect aşağıda Merhaba, OMS çalışma alanı anahtarı ve çalışma alanı kimliği değerler</span><span class="sxs-lookup"><span data-stu-id="ab37a-165">Update hello variable values in hello below sample tooreflect you OMS workspace key and workspace Id.</span></span>  

```powershell
$omsId = "<Replace with your OMS Id>"
$omsKey = "<Replace with your OMS key>"

Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
  -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
  -VMName myVM `
  -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
  -ExtensionType "MicrosoftMonitoringAgent" `
  -TypeHandlerVersion 1.0 `
  -Settings @{"workspaceId" = $omsId} `
  -ProtectedSettings @{"workspaceKey" = $omsKey} `
  -Location eastus
```

<span data-ttu-id="ab37a-166">Birkaç dakika sonra görmelisiniz hello OMS çalışma alanında yeni bir VM hello.</span><span class="sxs-lookup"><span data-stu-id="ab37a-166">After a few minutes, you should see hello new VM in hello OMS workspace.</span></span> 

![OMS dikey penceresi](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a><span data-ttu-id="ab37a-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ab37a-168">Next steps</span></span>
<span data-ttu-id="ab37a-169">Bu öğreticide yapılandırılmış ve sanal makineleri Azure Güvenlik Merkezi ile gözden.</span><span class="sxs-lookup"><span data-stu-id="ab37a-169">In this tutorial, you configured and reviewed VMs with Azure Security Center.</span></span> <span data-ttu-id="ab37a-170">Şunları öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="ab37a-170">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ab37a-171">Sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="ab37a-171">Create a virtual network</span></span>
> * <span data-ttu-id="ab37a-172">Bir kaynak grubu ve VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="ab37a-172">Create a resource group and VM</span></span> 
> * <span data-ttu-id="ab37a-173">Önyükleme tanılaması hello VM üzerinde etkinleştir</span><span class="sxs-lookup"><span data-stu-id="ab37a-173">Enable boot diagnostics on hello VM</span></span>
> * <span data-ttu-id="ab37a-174">Önyükleme tanılamasını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="ab37a-174">View boot diagnostics</span></span>
> * <span data-ttu-id="ab37a-175">Ana bilgisayar metrikleri görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="ab37a-175">View host metrics</span></span>
> * <span data-ttu-id="ab37a-176">Merhaba tanılama uzantısını yükleyin</span><span class="sxs-lookup"><span data-stu-id="ab37a-176">Install hello diagnostics extension</span></span>
> * <span data-ttu-id="ab37a-177">VM metrikleri görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="ab37a-177">View VM metrics</span></span>
> * <span data-ttu-id="ab37a-178">Bir uyarı oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="ab37a-178">Create an alert</span></span>
> * <span data-ttu-id="ab37a-179">Gelişmiş izleme işlevini ayarlama</span><span class="sxs-lookup"><span data-stu-id="ab37a-179">Set up advanced monitoring</span></span>

<span data-ttu-id="ab37a-180">Azure Güvenlik Merkezi hakkında toohello sonraki öğretici toolearn ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="ab37a-180">Advance toohello next tutorial toolearn about Azure security center.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ab37a-181">VM güvenliğini yönetme</span><span class="sxs-lookup"><span data-stu-id="ab37a-181">Manage VM security</span></span>](./tutorial-azure-security.md)