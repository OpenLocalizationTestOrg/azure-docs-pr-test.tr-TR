---
title: PowerShell ile bir Windows VM aaaCreate | Microsoft Docs
description: "Azure PowerShell ve hello Klasik dağıtım modeli kullanarak Windows sanal makine oluşturun."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 42c0d4be-573c-45d1-b9b0-9327537702f7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 5339f458c1f08f6e1752a53191f19402fab8ea25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell-and-hello-classic-deployment-model"></a><span data-ttu-id="1da42-103">PowerShell ve hello Klasik dağıtım modeliyle bir Windows sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="1da42-103">Create a Windows virtual machine with PowerShell and hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1da42-104">Azure portal - Windows</span><span class="sxs-lookup"><span data-stu-id="1da42-104">Azure portal - Windows</span></span>](tutorial.md)
> * [<span data-ttu-id="1da42-105">PowerShell - Windows</span><span class="sxs-lookup"><span data-stu-id="1da42-105">PowerShell - Windows</span></span>](create-powershell.md)
> 
> 

<br>

> [!IMPORTANT] 
> <span data-ttu-id="1da42-106">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="1da42-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="1da42-107">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="1da42-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="1da42-108">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="1da42-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="1da42-109">Nasıl çok öğrenin[hello Resource Manager modelini kullanarak bu adımları uygulamadan](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1da42-109">Learn how too[perform these steps using hello Resource Manager model](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="1da42-110">Bu adımlar nasıl toocustomize Azure PowerShell kümesi oluşturmak ve bir yapı bloğu yaklaşımını kullanarak Windows tabanlı bir Azure sanal makine önceden komutları gösterir.</span><span class="sxs-lookup"><span data-stu-id="1da42-110">These steps show you how toocustomize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="1da42-111">Bu işlem kullanabilirsiniz tooquickly yeni bir Windows tabanlı sanal makine için bir komut kümesi oluşturun ve var olan bir dağıtıma genişletin veya birden çok komut ayarlar, hızlı bir şekilde toocreate yapı bir özel geliştirme ve test veya BT Uzmanı ortamı.</span><span class="sxs-lookup"><span data-stu-id="1da42-111">You can use this process tooquickly create a command set for a new Windows-based virtual machine and expand an existing deployment or toocreate multiple command sets that quickly build out a custom dev/test or IT pro environment.</span></span>

<span data-ttu-id="1da42-112">Bir doldurma-arada boşlukları yaklaşım Azure PowerShell komut kümelerini oluşturmak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="1da42-112">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="1da42-113">Bu yaklaşım, yeni tooPowerShell olan veya yalnızca tooknow hangi değerleri toospecify başarılı yapılandırmasını istiyorsanız yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="1da42-113">This approach can be useful if you are new tooPowerShell or you just want tooknow what values toospecify for successful configuration.</span></span> <span data-ttu-id="1da42-114">Gelişmiş PowerShell kullanıcıları hello komutları alabilir ve hello değişkenleri ("$" ile başlayan hello satırlar) için kendi değerlerinizi yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="1da42-114">Advanced PowerShell users can take hello commands and substitute their own values for hello variables (hello lines beginning with "$").</span></span>

<span data-ttu-id="1da42-115">Henüz yapmadıysanız, hello yönergeleri kullanın [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) , yerel bilgisayarınızda Azure PowerShell tooinstall.</span><span class="sxs-lookup"><span data-stu-id="1da42-115">If you haven't done so already, use hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell on your local computer.</span></span> <span data-ttu-id="1da42-116">Sonra bir Windows PowerShell komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="1da42-116">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="1da42-117">1. adım: hesabınızı ekleme</span><span class="sxs-lookup"><span data-stu-id="1da42-117">Step 1: Add your account</span></span>
1. <span data-ttu-id="1da42-118">Merhaba PowerShell isteminde **Add-AzureAccount** tıklatıp **Enter**.</span><span class="sxs-lookup"><span data-stu-id="1da42-118">At hello PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span> 
2. <span data-ttu-id="1da42-119">Azure aboneliğinizle ilişkili hello e-posta adresini yazın ve tıklatın **devam**.</span><span class="sxs-lookup"><span data-stu-id="1da42-119">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="1da42-120">Merhaba hesabınızın parolasını yazın.</span><span class="sxs-lookup"><span data-stu-id="1da42-120">Type in hello password for your account.</span></span> 
4. <span data-ttu-id="1da42-121">Tıklatın **oturum**.</span><span class="sxs-lookup"><span data-stu-id="1da42-121">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="1da42-122">2. adım: aboneliğiniz ve depolama hesabı ayarlama</span><span class="sxs-lookup"><span data-stu-id="1da42-122">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="1da42-123">Azure aboneliği ve depolama hesabı hello Windows PowerShell komut isteminde şu komutları çalıştırarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1da42-123">Set your Azure subscription and storage account by running these commands at hello Windows PowerShell command prompt.</span></span> <span data-ttu-id="1da42-124">Merhaba < ve > karakterleri dahil olmak üzere hello tırnak içindeki her şeyi hello doğru adlarıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1da42-124">Replace everything within hello quotes, including hello < and > characters, with hello correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="1da42-125">Merhaba hello çıktısını varlığıyla SubscriptionName özelliği hello hello doğru abonelik adı alabilirsiniz **Get-AzureSubscription** komutu.</span><span class="sxs-lookup"><span data-stu-id="1da42-125">You can get hello correct subscription name from hello SubscriptionName property of hello output of hello **Get-AzureSubscription** command.</span></span> <span data-ttu-id="1da42-126">Merhaba hello çıktısını Label özelliğinin hello hello doğru depolama hesabı adı alabilirsiniz **Get-AzureStorageAccount** hello çalıştırdıktan sonra komut **Select-AzureSubscription** komutu.</span><span class="sxs-lookup"><span data-stu-id="1da42-126">You can get hello correct storage account name from hello Label property of hello output of hello **Get-AzureStorageAccount** command after you run hello **Select-AzureSubscription** command.</span></span>

## <a name="step-3-determine-hello-imagefamily"></a><span data-ttu-id="1da42-127">3. adım: Merhaba ImageFamily belirleme</span><span class="sxs-lookup"><span data-stu-id="1da42-127">Step 3: Determine hello ImageFamily</span></span>
<span data-ttu-id="1da42-128">Ardından, toodetermine hello ImageFamily veya etiket değeri hello belirli görüntü karşılık gelen toohello için toocreate istediğiniz Azure sanal makine gerekir.</span><span class="sxs-lookup"><span data-stu-id="1da42-128">Next, you need toodetermine hello ImageFamily or Label value for hello specific image corresponding toohello Azure virtual machine you want toocreate.</span></span> <span data-ttu-id="1da42-129">Bu komut kullanılabilir ImageFamily değerlerle hello listesini elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1da42-129">You can get hello list of available ImageFamily values with this command.</span></span>

    Get-AzureVMImage | select ImageFamily -Unique

<span data-ttu-id="1da42-130">Windows tabanlı bilgisayarlar için ImageFamily değeri bazı örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1da42-130">Here are some examples of ImageFamily values for Windows-based computers:</span></span>

* <span data-ttu-id="1da42-131">Windows Server 2012 R2 Datacenter</span><span class="sxs-lookup"><span data-stu-id="1da42-131">Windows Server 2012 R2 Datacenter</span></span>
* <span data-ttu-id="1da42-132">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="1da42-132">Windows Server 2008 R2 SP1</span></span>
* <span data-ttu-id="1da42-133">Windows Server 2016 Technical Preview 4</span><span class="sxs-lookup"><span data-stu-id="1da42-133">Windows Server 2016 Technical Preview 4</span></span>
* <span data-ttu-id="1da42-134">Windows Server 2012'de SQL Server 2012 SP1 Enterprise</span><span class="sxs-lookup"><span data-stu-id="1da42-134">SQL Server 2012 SP1 Enterprise on Windows Server 2012</span></span>

<span data-ttu-id="1da42-135">Aradığınız hello görüntü bulursanız, hello metin düzenleyici seçim veya hello PowerShell Tümleşik komut dosyası ortamı (ISE) yeni bir örneğini açın.</span><span class="sxs-lookup"><span data-stu-id="1da42-135">If you find hello image you are looking for, open a fresh instance of hello text editor of your choice or hello PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="1da42-136">Merhaba aşağıdaki hello yeni metin dosyası veya hello hello ImageFamily değerini değiştirerek PowerShell ISE kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="1da42-136">Copy hello following into hello new text file or hello PowerShell ISE, substituting hello ImageFamily value.</span></span>

    $family="<ImageFamily value>"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="1da42-137">Bazı durumlarda, hello etiket özelliği hello ImageFamily değeri yerine hello görüntü adı kullanılıyor.</span><span class="sxs-lookup"><span data-stu-id="1da42-137">In some cases, hello image name is in hello Label property instead of hello ImageFamily value.</span></span> <span data-ttu-id="1da42-138">Merhaba ImageFamily özelliğini kullanarak aradığınız hello görüntü bulamadıysanız, bu komutla kendi etiket özelliği tarafından hello yansımaları listeler.</span><span class="sxs-lookup"><span data-stu-id="1da42-138">If you didn't find hello image that you are looking for using hello ImageFamily property, list hello images by their Label property with this command.</span></span>

    Get-AzureVMImage | select Label -Unique

<span data-ttu-id="1da42-139">Bu komutla hello sağ görüntü bulursanız, seçim veya hello PowerShell ISE hello metin düzenleyicisi yeni bir örneğini açın.</span><span class="sxs-lookup"><span data-stu-id="1da42-139">If you find hello right image with this command, open a fresh instance of hello text editor of your choice or hello PowerShell ISE.</span></span> <span data-ttu-id="1da42-140">Merhaba aşağıdaki hello yeni metin dosyası veya hello hello etiket değeri değiştirerek PowerShell ISE kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="1da42-140">Copy hello following into hello new text file or hello PowerShell ISE, substituting hello Label value.</span></span>

    $label="<Label value>"
    $image = Get-AzureVMImage | where { $_.Label -eq $label } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

## <a name="step-4-build-your-command-set"></a><span data-ttu-id="1da42-141">4. adım: komut kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="1da42-141">Step 4: Build your command set</span></span>
<span data-ttu-id="1da42-142">Kümesi, yeni bir metin dosyası veya hello işe hello değişken değerleri doldurma ve merhaba < ve > karakterleri kaldırma içine hello uygun blokları kümesi kopyalama komutunuzu Hello kalan oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1da42-142">Build hello rest of your command set by copying hello appropriate set of blocks below into your new text file or hello ISE and then filling in hello variable values and removing hello < and > characters.</span></span> <span data-ttu-id="1da42-143">Merhaba iki bkz [örnekler](#examples) hello hello son sonucunun hakkında bir fikir için bu makalenin sonunda.</span><span class="sxs-lookup"><span data-stu-id="1da42-143">See hello two [examples](#examples) at hello end of this article for an idea of hello final result.</span></span>

<span data-ttu-id="1da42-144">(Gerekli) bu iki komut blokları birini seçerek, komutunu başlatın.</span><span class="sxs-lookup"><span data-stu-id="1da42-144">Start your command set by choosing one of these two command blocks (required).</span></span>

<span data-ttu-id="1da42-145">Seçenek 1: bir sanal makine adı ve bir boyut belirtin.</span><span class="sxs-lookup"><span data-stu-id="1da42-145">Option 1: Specify a virtual machine name and a size.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="1da42-146">Seçenek 2: bir ad, boyutu ve kullanılabilirlik kümesi adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="1da42-146">Option 2: Specify a name, size, and availability set name.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $availset="<set name>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image -AvailabilitySetName $availset

<span data-ttu-id="1da42-147">D, DS veya G-serisi sanal makineler için Hello InstanceSize değerleri için bkz: [sanal makine ve bulut hizmeti boyutları Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="1da42-147">For hello InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="1da42-148">Bir Kuruluş Sözleşmesi Yazılım Güvencesi ile varsa ve Windows Server hello tootake avantajlarından düşündüğünüz [karma kullanımı avantajı](https://azure.microsoft.com/pricing/hybrid-use-benefit/), ekleme **- LicenseType değeri** parametresi toohello  **AzureVMConfig yeni** hello değere geçirme cmdlet'ini **Windows_Server** hello tipik kullanım örneği.</span><span class="sxs-lookup"><span data-stu-id="1da42-148">If you have an Enterprise Agreement with Software Assurance, and intend tootake advantage of hello Windows Server [Hybrid Use Benefit](https://azure.microsoft.com/pricing/hybrid-use-benefit/), add the **-LicenseType** parameter toohello **New-AzureVMConfig** cmdlet, passing hello value **Windows_Server** for hello typical use case.</span></span>  <span data-ttu-id="1da42-149">Görüntüyü karşıya yüklediğiniz kullandığınızdan emin olun; Merhaba galeri standart bir görüntüden hello karma kullanma avantajı ile kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="1da42-149">Be sure you are using an image you have uploaded; you cannot use a standard image from hello Gallery with hello Hybrid Use Benefit.</span></span>
> 
> 

<span data-ttu-id="1da42-150">İsteğe bağlı olarak, bir tek başına Windows bilgisayar için hello yerel yönetici hesabı ve parolası belirtin.</span><span class="sxs-lookup"><span data-stu-id="1da42-150">Optionally, for a standalone Windows computer, specify hello local administrator account and password.</span></span>

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

<span data-ttu-id="1da42-151">Güçlü bir parola seçin.</span><span class="sxs-lookup"><span data-stu-id="1da42-151">Choose a strong password.</span></span> <span data-ttu-id="1da42-152">toocheck kendi gücü bkz [parola denetleyicisi: güçlü parolalar kullanarak](https://www.microsoft.com/security/pc-security/password-checker.aspx).</span><span class="sxs-lookup"><span data-stu-id="1da42-152">toocheck its strength, see [Password Checker: Using Strong Passwords](https://www.microsoft.com/security/pc-security/password-checker.aspx).</span></span>

<span data-ttu-id="1da42-153">İsteğe bağlı olarak, tooadd hello Windows bilgisayar tooan var olan Active Directory etki alanı, hello yerel yönetici hesabı ve parola, hello etki alanı ve hello adı ve etki alanı hesabının parolasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="1da42-153">Optionally, tooadd hello Windows computer tooan existing Active Directory domain, specify hello local administrator account and password, hello domain, and hello name and password of a domain account.</span></span>

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="<FQDN of hello domain that hello machine is joining>"
    $domacctdomain="<domain of hello account that has permission tooadd hello machine toohello domain>"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="1da42-154">Merhaba sözdizimi hello için Windows tabanlı sanal makinelere ilişkin ek öncesi yapılandırma seçenekleri için bkz **Windows** ve **WindowsDomain** parametre kümelerine [ Ekleme AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).</span><span class="sxs-lookup"><span data-stu-id="1da42-154">For additional pre-configuration options for Windows-based virtual machines, see hello syntax for hello **Windows** and **WindowsDomain** parameter sets in [Add-AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).</span></span>

<span data-ttu-id="1da42-155">İsteğe bağlı olarak, sanal makine hello statik DIP bilinen belirli bir IP adresi atayın.</span><span class="sxs-lookup"><span data-stu-id="1da42-155">Optionally, assign hello virtual machine a specific IP address, known as a static DIP.</span></span>

    $vm1 | Set-AzureStaticVNetIP -IPAddress <IP address>

<span data-ttu-id="1da42-156">Belirli bir IP adresi ile kullanılabilir olduğunu doğrulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1da42-156">You can verify that a specific IP address is available with:</span></span>

    Test-AzureStaticVNetIP –VNetName <VNet name> –IPAddress <IP address>

<span data-ttu-id="1da42-157">İsteğe bağlı olarak, bir Azure sanal ağında hello sanal makine tooa belirli alt atayın.</span><span class="sxs-lookup"><span data-stu-id="1da42-157">Optionally, assign hello virtual machine tooa specific subnet in an Azure virtual network.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "<name of hello subnet>"

<span data-ttu-id="1da42-158">İsteğe bağlı olarak, tek bir veri diski toohello sanal makine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1da42-158">Optionally, add a single data disk toohello virtual machine.</span></span>

    $disksize=<size of hello disk in GB>
    $disklabel="<hello label on hello disk>"
    $lun=<Logical Unit Number (LUN) of hello disk>
    $hcaching="<Specify one: ReadOnly, ReadWrite, None>"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

<span data-ttu-id="1da42-159">Bir Active Directory etki alanı denetleyicisi için $hcaching çok ayarlamak "None".</span><span class="sxs-lookup"><span data-stu-id="1da42-159">For an Active Directory domain controller, set $hcaching too"None".</span></span>

<span data-ttu-id="1da42-160">İsteğe bağlı olarak hello sanal makine tooan varolan yük dengeli kümesi için dış trafiğin ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1da42-160">Optionally, add hello virtual machine tooan existing load-balanced set for external traffic.</span></span>

    $protocol="<Specify one: tcp, udp>"
    $localport=<port number of hello internal port>
    $pubport=<port number of hello external port>
    $endpointname="<name of hello endpoint>"
    $lbsetname="<name of hello existing load-balanced set>"
    $probeprotocol="<Specify one: tcp, http>"
    $probeport=<TCP or HTTP port number of probe traffic>
    $probepath="<URL path for probe traffic>"
    $vm1 | Add-AzureEndpoint -Name $endpointname -Protocol $protocol -LocalPort $localport -PublicPort $pubport -LBSetName $lbsetname -ProbeProtocol $probeprotocol -ProbePort $probeport -ProbePath $probepath

<span data-ttu-id="1da42-161">Son olarak, hello sanal makine oluşturmak için bu gerekli komutu blokları birini seçin.</span><span class="sxs-lookup"><span data-stu-id="1da42-161">Finally, choose one of these required command blocks for creating hello virtual machine.</span></span>

<span data-ttu-id="1da42-162">Seçenek 1: var olan bir bulut hizmetinde hello sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1da42-162">Option 1: Create hello virtual machine in an existing cloud service.</span></span>

    New-AzureVM –ServiceName "<short name of hello cloud service>" -VMs $vm1

<span data-ttu-id="1da42-163">Merhaba kısa hello bulut hizmeti adını hello bulut hizmetlerinin listesi hello Azure portal veya Merhaba, kaynak grupları listesinde hello Azure portalında görünür hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="1da42-163">hello short name of hello cloud service is hello name that appears in hello list of Cloud Services in hello Azure portal or in hello list of Resource Groups in hello Azure portal.</span></span>

<span data-ttu-id="1da42-164">Seçenek 2: hello sanal makineyi bir bulut hizmetini ve sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1da42-164">Option 2: Create hello virtual machine in an existing cloud service and virtual network.</span></span>

    $svcname="<short name of hello cloud service>"
    $vnetname="<name of hello virtual network>"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

## <a name="step-5-run-your-command-set"></a><span data-ttu-id="1da42-165">5. adım: komut kümesini çalıştırın</span><span class="sxs-lookup"><span data-stu-id="1da42-165">Step 5: Run your command set</span></span>
<span data-ttu-id="1da42-166">Metin Düzenleyicisi'nde oluşturulan hello Azure PowerShell komut kümesini gözden geçirin veya birden çok adım 4 komutlarından bloklarını oluşan PowerShell ISE hello.</span><span class="sxs-lookup"><span data-stu-id="1da42-166">Review hello Azure PowerShell command set you built in your text editor or hello PowerShell ISE consisting of multiple blocks of commands from step 4.</span></span> <span data-ttu-id="1da42-167">Tüm gerekli hello değişkenleri belirttiniz ve hello doğru değerlerin olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="1da42-167">Ensure that you have specified all hello needed variables and that they have hello correct values.</span></span> <span data-ttu-id="1da42-168">Ayrıca tüm merhaba < ve > karakterleri kaldırdığınız emin olun.</span><span class="sxs-lookup"><span data-stu-id="1da42-168">Also make sure that you have removed all hello < and > characters.</span></span>

<span data-ttu-id="1da42-169">Bir metin düzenleyicisi kullanıyorsanız, copy hello komutu toohello Pano ayarlayın ve, Windows PowerShell komut istemini açın sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1da42-169">If you are using a text editor, copy hello command set toohello clipboard and then right-click your open Windows PowerShell command prompt.</span></span> <span data-ttu-id="1da42-170">Bu PowerShell komutlarını bir dizi olarak hello komut kümesini vermek ve Azure sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1da42-170">This will issue hello command set as a series of PowerShell commands and create your Azure virtual machine.</span></span> <span data-ttu-id="1da42-171">Alternatif olarak, hello PowerShell ISE set hello komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1da42-171">Alternately, run hello command set in hello PowerShell ISE.</span></span>

<span data-ttu-id="1da42-172">Bu sanal makineyi yeniden veya benzer bir oluşturacaksanız, şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1da42-172">If you will be creating this virtual machine again or a similar one, you can:</span></span>

* <span data-ttu-id="1da42-173">Bu komut bir PowerShell komut dosyası (*.ps1) ayarlanmış kaydedin.</span><span class="sxs-lookup"><span data-stu-id="1da42-173">Save this command set as a PowerShell script file (*.ps1).</span></span>
* <span data-ttu-id="1da42-174">Farklı Kaydet hello bir Azure Otomasyonu runbook olarak ayarla bu komutu **Automation hesapları** hello Azure portalı bölümü.</span><span class="sxs-lookup"><span data-stu-id="1da42-174">Save this command set as an Azure Automation runbook in hello **Automation Accounts** section of hello Azure portal.</span></span>

## <span data-ttu-id="1da42-175"><a id="examples"></a>Örnekler</span><span class="sxs-lookup"><span data-stu-id="1da42-175"><a id="examples"></a>Examples</span></span>
<span data-ttu-id="1da42-176">Aşağıda, Windows tabanlı Azure sanal makineler oluşturma toobuild Azure PowerShell komut kümelerini yukarıdaki hello adımları kullanarak, iki örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1da42-176">Here are two examples of using hello steps above toobuild Azure PowerShell command sets that create Windows-based Azure virtual machines.</span></span>

### <a name="example-1"></a><span data-ttu-id="1da42-177">Örnek 1</span><span class="sxs-lookup"><span data-stu-id="1da42-177">Example 1</span></span>
<span data-ttu-id="1da42-178">Bir PowerShell gereksinim toocreate hello ilk sanal makine bir Active Directory etki alanı denetleyicisi için komut kümesinin:</span><span class="sxs-lookup"><span data-stu-id="1da42-178">I need a PowerShell command set toocreate hello initial virtual machine for an Active Directory domain controller that:</span></span>

* <span data-ttu-id="1da42-179">Merhaba Windows Server 2012 R2 Datacenter görüntüsü kullanır.</span><span class="sxs-lookup"><span data-stu-id="1da42-179">Uses hello Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="1da42-180">Merhaba adı AZDC1 vardır.</span><span class="sxs-lookup"><span data-stu-id="1da42-180">Has hello name AZDC1.</span></span>
* <span data-ttu-id="1da42-181">Bir tek başına bilgisayardır.</span><span class="sxs-lookup"><span data-stu-id="1da42-181">Is a standalone computer.</span></span>
* <span data-ttu-id="1da42-182">Bir ek veri diski 20 GB sahiptir.</span><span class="sxs-lookup"><span data-stu-id="1da42-182">Has an additional data disk of 20 GB.</span></span>
* <span data-ttu-id="1da42-183">Merhaba statik IP adresi 192.168.244.4 vardır.</span><span class="sxs-lookup"><span data-stu-id="1da42-183">Has hello static IP address 192.168.244.4.</span></span>
* <span data-ttu-id="1da42-184">Merhaba AZDatacenter sanal ağın Hello arka uç alt ağda değil.</span><span class="sxs-lookup"><span data-stu-id="1da42-184">Is in hello BackEnd subnet of hello AZDatacenter virtual network.</span></span>
* <span data-ttu-id="1da42-185">Hello Azure TailspinToys bulut hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="1da42-185">Is in hello Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="1da42-186">Okunabilirlik için her bloğu arasında boş satırlar ile bu sanal makine hello karşılık gelen Azure PowerShell komut kümesini toocreate aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="1da42-186">Here is hello corresponding Azure PowerShell command set toocreate this virtual machine, with blank lines between each block for readability.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="AZDC1"
    $vmsize="Medium"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

    $vm1 | Set-AzureSubnet -SubnetNames "BackEnd"

    $vm1 | Set-AzureStaticVNetIP -IPAddress 192.168.244.4

    $disksize=20
    $disklabel="DCData"
    $lun=0
    $hcaching="None"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

### <a name="example-2"></a><span data-ttu-id="1da42-187">Örnek 2</span><span class="sxs-lookup"><span data-stu-id="1da42-187">Example 2</span></span>
<span data-ttu-id="1da42-188">Bir PowerShell gereken komut kümesini toocreate bir sanal makine için bir iş sunucu:</span><span class="sxs-lookup"><span data-stu-id="1da42-188">I need a PowerShell command set toocreate a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="1da42-189">Merhaba Windows Server 2012 R2 Datacenter görüntüsü kullanır.</span><span class="sxs-lookup"><span data-stu-id="1da42-189">Uses hello Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="1da42-190">Merhaba adı LOB1 vardır.</span><span class="sxs-lookup"><span data-stu-id="1da42-190">Has hello name LOB1.</span></span>
* <span data-ttu-id="1da42-191">Merhaba corp.contoso.com etki alanının bir üyesidir.</span><span class="sxs-lookup"><span data-stu-id="1da42-191">Is a member of hello corp.contoso.com domain.</span></span>
* <span data-ttu-id="1da42-192">Bir ek veri diski 200 GB sahiptir.</span><span class="sxs-lookup"><span data-stu-id="1da42-192">Has an additional data disk of 200 GB.</span></span>
* <span data-ttu-id="1da42-193">Merhaba AZDatacenter sanal ağın Hello ön uç alt ağda değil.</span><span class="sxs-lookup"><span data-stu-id="1da42-193">Is in hello FrontEnd subnet of hello AZDatacenter virtual network.</span></span>
* <span data-ttu-id="1da42-194">Hello Azure TailspinToys bulut hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="1da42-194">Is in hello Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="1da42-195">Bu sanal makine hello karşılık gelen Azure PowerShell komut kümesini toocreate aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="1da42-195">Here is hello corresponding Azure PowerShell command set toocreate this virtual machine.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="LOB1"
    $vmsize="Large"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="corp.contoso.com"
    $domacctdomain="CORP"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "FrontEnd"

    $disksize=200
    $disklabel="LOBData"
    $lun=0
    $hcaching="ReadWrite"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname


## <a name="next-steps"></a><span data-ttu-id="1da42-196">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1da42-196">Next steps</span></span>
<span data-ttu-id="1da42-197">127 GB'den büyük bir işletim sistemi diski gerekiyorsa, yapabilecekleriniz [hello OS sürücüyü genişletin](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1da42-197">If you need an OS disk that is larger than 127 GB, you can [expand hello OS drive](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

