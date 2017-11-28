---
title: "Azure Active Directory etki alanı Hizmetleri: Yönetim Kılavuzu | Microsoft Docs"
description: "Azure PowerShell ve hello Klasik dağıtım modeli kullanarak bir Windows sanal makine tooa yönetilen etki alanına katılın."
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9143b843-7327-43c3-baab-6e24a18db25e
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 21bc5930d84c5368a120f9d81f09320e2a0168fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain-using-powershell"></a><span data-ttu-id="e495f-103">PowerShell kullanarak bir Windows Server sanal makine tooa yönetilen etki alanına katılma</span><span class="sxs-lookup"><span data-stu-id="e495f-103">Join a Windows Server virtual machine tooa managed domain using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e495f-104">Klasik Azure portalı - Windows</span><span class="sxs-lookup"><span data-stu-id="e495f-104">Azure classic portal - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
> * [<span data-ttu-id="e495f-105">PowerShell - Windows</span><span class="sxs-lookup"><span data-stu-id="e495f-105">PowerShell - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="e495f-106">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e495f-106">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e495f-107">Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="e495f-107">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="e495f-108">Azure AD etki alanı Hizmetleri hello Resource Manager modeli şu anda desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="e495f-108">Azure AD Domain Services does not currently support hello Resource Manager model.</span></span>
>
>

<span data-ttu-id="e495f-109">Bu adımlar nasıl toocustomize Azure PowerShell kümesi oluşturmak ve bir yapı bloğu yaklaşımını kullanarak Windows tabanlı bir Azure sanal makine önceden komutları gösterir.</span><span class="sxs-lookup"><span data-stu-id="e495f-109">These steps show you how toocustomize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="e495f-110">Bu adımları Windows tabanlı bir Azure sanal makine oluşturun ve tooan Azure AD etki alanı Hizmetleri yönetilen etki alanına katılması yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="e495f-110">These steps help you build a Windows-based Azure virtual machine and join it tooan Azure AD Domain Services managed domain.</span></span>

<span data-ttu-id="e495f-111">Bir doldurma-arada boşlukları yaklaşım Azure PowerShell komut kümelerini oluşturmak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="e495f-111">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="e495f-112">Bu yaklaşım, yeni tooPowerShell olduğunuz veya başarılı bir yapılandırma için hangi değerlerin toospecify tooknow istiyorsanız yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="e495f-112">This approach can be useful if you are new tooPowerShell or you want tooknow what values toospecify for successful configuration.</span></span> <span data-ttu-id="e495f-113">Gelişmiş PowerShell kullanıcıları hello komutları alabilir ve hello değişkenleri ("$" ile başlayan hello satırlar) için kendi değerlerinizi yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="e495f-113">Advanced PowerShell users can take hello commands and substitute their own values for hello variables (hello lines beginning with "$").</span></span>

<span data-ttu-id="e495f-114">Henüz yapmadıysanız, hello yönergeleri kullanın [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) , yerel bilgisayarınızda Azure PowerShell tooinstall.</span><span class="sxs-lookup"><span data-stu-id="e495f-114">If you haven't done so already, use hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell on your local computer.</span></span> <span data-ttu-id="e495f-115">Sonra bir Windows PowerShell komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="e495f-115">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="e495f-116">1. adım: hesabınızı ekleme</span><span class="sxs-lookup"><span data-stu-id="e495f-116">Step 1: Add your account</span></span>
1. <span data-ttu-id="e495f-117">Merhaba PowerShell isteminde **Add-AzureAccount** tıklatıp **Enter**.</span><span class="sxs-lookup"><span data-stu-id="e495f-117">At hello PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span>
2. <span data-ttu-id="e495f-118">Azure aboneliğinizle ilişkili hello e-posta adresini yazın ve tıklatın **devam**.</span><span class="sxs-lookup"><span data-stu-id="e495f-118">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span>
3. <span data-ttu-id="e495f-119">Merhaba hesabınızın parolasını yazın.</span><span class="sxs-lookup"><span data-stu-id="e495f-119">Type in hello password for your account.</span></span>
4. <span data-ttu-id="e495f-120">Tıklatın **oturum**.</span><span class="sxs-lookup"><span data-stu-id="e495f-120">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="e495f-121">2. adım: aboneliğiniz ve depolama hesabı ayarlama</span><span class="sxs-lookup"><span data-stu-id="e495f-121">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="e495f-122">Azure aboneliği ve depolama hesabı hello Windows PowerShell komut isteminde şu komutları çalıştırarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e495f-122">Set your Azure subscription and storage account by running these commands at hello Windows PowerShell command prompt.</span></span> <span data-ttu-id="e495f-123">Merhaba < ve > karakterleri dahil olmak üzere hello tırnak içindeki her şeyi hello doğru adlarıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e495f-123">Replace everything within hello quotes, including hello < and > characters, with hello correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="e495f-124">Merhaba hello çıktısını varlığıyla SubscriptionName özelliği hello hello doğru abonelik adı alabilirsiniz **Get-AzureSubscription** komutu.</span><span class="sxs-lookup"><span data-stu-id="e495f-124">You can get hello correct subscription name from hello SubscriptionName property of hello output of hello **Get-AzureSubscription** command.</span></span> <span data-ttu-id="e495f-125">Merhaba hello çıktısını Label özelliğinin hello hello doğru depolama hesabı adı alabilirsiniz **Get-AzureStorageAccount** hello çalıştırdıktan sonra komut **Select-AzureSubscription** komutu.</span><span class="sxs-lookup"><span data-stu-id="e495f-125">You can get hello correct storage account name from hello Label property of hello output of hello **Get-AzureStorageAccount** command after you run hello **Select-AzureSubscription** command.</span></span>

## <a name="step-3-step-by-step-walkthrough---provision-hello-virtual-machine-and-join-it-toohello-managed-domain"></a><span data-ttu-id="e495f-126">3. adım: Adım adım - hello sanal makine sağlama ve toohello yönetilen etki alanına katılma</span><span class="sxs-lookup"><span data-stu-id="e495f-126">Step 3: Step-by-step walkthrough - provision hello virtual machine and join it toohello managed domain</span></span>
<span data-ttu-id="e495f-127">Okunabilirlik için her bloğu arasında boş satırlar ile bu sanal makine hello karşılık gelen Azure PowerShell komut kümesini toocreate aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="e495f-127">Here is hello corresponding Azure PowerShell command set toocreate this virtual machine, with blank lines between each block for readability.</span></span>

<span data-ttu-id="e495f-128">Sağlanan hello Windows sanal makine toobe hakkındaki bilgileri belirtin.</span><span class="sxs-lookup"><span data-stu-id="e495f-128">Specify information about hello Windows virtual machine toobe provisioned.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

<span data-ttu-id="e495f-129">D, DS veya G-serisi sanal makineler için Hello InstanceSize değerleri için bkz: [sanal makine ve bulut hizmeti boyutları Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="e495f-129">For hello InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

<span data-ttu-id="e495f-130">Merhaba yönetilen etki alanı hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="e495f-130">Provide information about hello managed domain.</span></span>

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

<span data-ttu-id="e495f-131">Merhaba hello bulut hizmeti adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="e495f-131">Specify hello name of hello cloud service.</span></span>

    $svcname="Contoso100-test"

<span data-ttu-id="e495f-132">VM birleştirilmelidir hello sanal ağ toowhich hello Hello adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="e495f-132">Specify hello name of hello virtual network toowhich hello VM should be joined.</span></span> <span data-ttu-id="e495f-133">Bu hello AAD DS yönetilen etki alanı bu sanal ağda kullanılabilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e495f-133">Ensure that hello AAD-DS managed domain is available in this virtual network.</span></span>

    $vnetname="MyPreviewVnet"

<span data-ttu-id="e495f-134">Merhaba VM görüntü kullanılan toobe tooprovision hello VM seçin.</span><span class="sxs-lookup"><span data-stu-id="e495f-134">Select hello VM image toobe used tooprovision hello VM.</span></span>

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="e495f-135">Merhaba VM - kümesi VM adı, yapılandırma kullanılan örnek boyutu & görüntü toobe.</span><span class="sxs-lookup"><span data-stu-id="e495f-135">Configure hello VM - set VM name, instance size & image toobe used.</span></span>

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="e495f-136">Merhaba VM için yerel yönetici kimlik bilgilerini edinin.</span><span class="sxs-lookup"><span data-stu-id="e495f-136">Obtain local administrator credentials for hello VM.</span></span> <span data-ttu-id="e495f-137">Güçlü bir yerel yönetici parolası seçin.</span><span class="sxs-lookup"><span data-stu-id="e495f-137">Choose a strong local administrator password.</span></span>

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

<span data-ttu-id="e495f-138">Too'AAD DC Yöneticiler grubu toojoin VM toohello yönetilen etki alanına ait bir kullanıcı hesabı için kimlik bilgilerini edinin.</span><span class="sxs-lookup"><span data-stu-id="e495f-138">Obtain credentials for a user account belonging too'AAD DC Administrators' group toojoin VM toohello managed domain.</span></span> <span data-ttu-id="e495f-139">Örneğimizde örneği belirttiğimiz 'Kemal için' hello etki alanı adı - hello kullanıcı adı olarak belirtmeyin.</span><span class="sxs-lookup"><span data-stu-id="e495f-139">Do not specify hello domain name - for instance, in our example, we specify 'bob' as hello user name.</span></span>

    $domainadmincred=Get-Credential –Message "Now type hello name (DO NOT INCLUDE hello DOMAIN) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

<span data-ttu-id="e495f-140">Merhaba VM yapılandırma - etki alanı katılma gereksinim & gerekli kimlik bilgilerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="e495f-140">Configure hello VM - specify domain join requirement & required credentials.</span></span>

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="e495f-141">Merhaba VM için bir alt ağ olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e495f-141">Set a subnet for hello VM.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

<span data-ttu-id="e495f-142">İsteğe bağlı: Noktası toohello IP adresi hello etki alanı.</span><span class="sxs-lookup"><span data-stu-id="e495f-142">Optional: Point toohello IP address of hello domain.</span></span> <span data-ttu-id="e495f-143">Merhaba sanal ağ için DNS sunucularını hello Azure AD etki alanı Hizmetleri yönetilen etki alanı toobe hello hello IP adreslerini ayarlarsanız, bu adım gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="e495f-143">If you set hello IP addresses of hello Azure AD Domain Services managed domain toobe hello DNS servers for hello virtual network, this step is not required.</span></span>

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

<span data-ttu-id="e495f-144">Şimdi, sağlama hello etki alanı Windows VM katılmış.</span><span class="sxs-lookup"><span data-stu-id="e495f-144">Now, provision hello domain-joined Windows VM.</span></span>

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="script-tooprovision-a-windows-vm-and-automatically-join-it-tooan-aad-domain-services-managed-domain"></a><span data-ttu-id="e495f-145">Bir Windows VM tooprovision komut dosyası ve otomatik olarak tooan AAD etki alanı Hizmetleri yönetilen etki alanına katılın</span><span class="sxs-lookup"><span data-stu-id="e495f-145">Script tooprovision a Windows VM and automatically join it tooan AAD Domain Services managed domain</span></span>
<span data-ttu-id="e495f-146">Bu PowerShell komut kümesini iş sunucu için bir sanal makine oluşturur:</span><span class="sxs-lookup"><span data-stu-id="e495f-146">This PowerShell command set creates a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="e495f-147">Merhaba Windows Server 2012 R2 Datacenter görüntüsü kullanır.</span><span class="sxs-lookup"><span data-stu-id="e495f-147">Uses hello Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="e495f-148">Ek çok küçük bir sanal makine bulunuyor.</span><span class="sxs-lookup"><span data-stu-id="e495f-148">Is an extra small virtual machine.</span></span>
* <span data-ttu-id="e495f-149">Merhaba adı Contoso100 test vardır.</span><span class="sxs-lookup"><span data-stu-id="e495f-149">Has hello name Contoso100-test.</span></span>
* <span data-ttu-id="e495f-150">Otomatik olarak etki alanına katılmış toohello contoso100 yönetilen etki alanıdır.</span><span class="sxs-lookup"><span data-stu-id="e495f-150">Is automatically domain joined toohello contoso100 managed domain.</span></span>
* <span data-ttu-id="e495f-151">Toohello eklenen hello aynı sanal ağ yönetilen etki alanı.</span><span class="sxs-lookup"><span data-stu-id="e495f-151">Is added toohello same virtual network as hello managed domain.</span></span>

<span data-ttu-id="e495f-152">İşte tam örnek komut dosyası toocreate hello Windows sanal makine hello ve otomatik olarak toohello Azure AD etki alanı Hizmetleri yönetilen etki alanına katılın.</span><span class="sxs-lookup"><span data-stu-id="e495f-152">Here is hello full sample script toocreate hello Windows virtual machine and automatically join it toohello Azure AD Domain Services managed domain.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

    $svcname="Contoso100-test"
    $vnetname="MyPreviewVnet"

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

    $domainadmincred=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="related-content"></a><span data-ttu-id="e495f-153">İlgili İçerik</span><span class="sxs-lookup"><span data-stu-id="e495f-153">Related Content</span></span>
* [<span data-ttu-id="e495f-154">Azure AD etki alanı Hizmetleri - başlangıç kılavuzu</span><span class="sxs-lookup"><span data-stu-id="e495f-154">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="e495f-155">Azure AD Domain Services tarafından yönetilen etki alanını yönetme</span><span class="sxs-lookup"><span data-stu-id="e495f-155">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
