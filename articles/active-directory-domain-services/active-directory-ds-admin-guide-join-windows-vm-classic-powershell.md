---
title: "Azure Active Directory etki alanı Hizmetleri: Yönetim Kılavuzu | Microsoft Docs"
description: "Windows sanal makinesi Azure PowerShell ve klasik dağıtım modeli kullanarak bir yönetilen etki alanına ekleyin."
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
ms.openlocfilehash: 1bb1546fb616131a1e1868a0d0610c4cad5d73e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-windows-server-virtual-machine-to-a-managed-domain-using-powershell"></a><span data-ttu-id="f4c78-103">Bir Windows Server sanal makine PowerShell kullanarak bir yönetilen etki alanına ekleyin</span><span class="sxs-lookup"><span data-stu-id="f4c78-103">Join a Windows Server virtual machine to a managed domain using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f4c78-104">Klasik Azure portalı - Windows</span><span class="sxs-lookup"><span data-stu-id="f4c78-104">Azure classic portal - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
> * [<span data-ttu-id="f4c78-105">PowerShell - Windows</span><span class="sxs-lookup"><span data-stu-id="f4c78-105">PowerShell - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="f4c78-106">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f4c78-106">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f4c78-107">Bu makale klasik dağıtım modelini incelemektedir.</span><span class="sxs-lookup"><span data-stu-id="f4c78-107">This article covers using the classic deployment model.</span></span> <span data-ttu-id="f4c78-108">Azure AD etki alanı Hizmetleri, Resource Manager modeli şu anda desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="f4c78-108">Azure AD Domain Services does not currently support the Resource Manager model.</span></span>
>
>

<span data-ttu-id="f4c78-109">Bu adımlar oluşturmak ve bir yapı bloğu yaklaşımını kullanarak Windows tabanlı bir Azure sanal makine önceden Azure PowerShell komut kümesini özelleştirmek nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="f4c78-109">These steps show you how to customize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="f4c78-110">Bu adımları Windows tabanlı bir Azure sanal makine oluşturun ve bir Azure AD etki alanı Hizmetleri yönetilen etki alanına katılmak yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="f4c78-110">These steps help you build a Windows-based Azure virtual machine and join it to an Azure AD Domain Services managed domain.</span></span>

<span data-ttu-id="f4c78-111">Bir doldurma-arada boşlukları yaklaşım Azure PowerShell komut kümelerini oluşturmak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="f4c78-111">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="f4c78-112">Bu yaklaşım, PowerShell için yeni olan veya ne başarılı yapılandırmayı belirtmek için değerleri bilmek istiyorsanız yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f4c78-112">This approach can be useful if you are new to PowerShell or you want to know what values to specify for successful configuration.</span></span> <span data-ttu-id="f4c78-113">Gelişmiş PowerShell kullanıcılar, komutları almak ve ("$" ile başlayan satırlar) değişkenleri için kendi değerlerinizi yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="f4c78-113">Advanced PowerShell users can take the commands and substitute their own values for the variables (the lines beginning with "$").</span></span>

<span data-ttu-id="f4c78-114">Henüz yapmadıysanız, konusundaki yönergeleri kullanın [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview) yerel bilgisayarınıza Azure PowerShell'i yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="f4c78-114">If you haven't done so already, use the instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) to install Azure PowerShell on your local computer.</span></span> <span data-ttu-id="f4c78-115">Sonra bir Windows PowerShell komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="f4c78-115">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="f4c78-116">1. adım: hesabınızı ekleme</span><span class="sxs-lookup"><span data-stu-id="f4c78-116">Step 1: Add your account</span></span>
1. <span data-ttu-id="f4c78-117">PowerShell komut isteminde yazın **Add-AzureAccount** tıklatıp **Enter**.</span><span class="sxs-lookup"><span data-stu-id="f4c78-117">At the PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span>
2. <span data-ttu-id="f4c78-118">Azure aboneliğinizle ilişkili e-posta adresini yazın ve tıklatın **devam**.</span><span class="sxs-lookup"><span data-stu-id="f4c78-118">Type in the email address associated with your Azure subscription and click **Continue**.</span></span>
3. <span data-ttu-id="f4c78-119">Hesabınızın parolasını yazın.</span><span class="sxs-lookup"><span data-stu-id="f4c78-119">Type in the password for your account.</span></span>
4. <span data-ttu-id="f4c78-120">Tıklatın **oturum**.</span><span class="sxs-lookup"><span data-stu-id="f4c78-120">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="f4c78-121">2. adım: aboneliğiniz ve depolama hesabı ayarlama</span><span class="sxs-lookup"><span data-stu-id="f4c78-121">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="f4c78-122">Azure aboneliği ve depolama hesabı Windows PowerShell komut isteminde şu komutları çalıştırarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f4c78-122">Set your Azure subscription and storage account by running these commands at the Windows PowerShell command prompt.</span></span> <span data-ttu-id="f4c78-123">Dahil olmak üzere tırnak işaretleri içindeki her şeyi değiştirin < ve > karakterleri doğru adlara sahip.</span><span class="sxs-lookup"><span data-stu-id="f4c78-123">Replace everything within the quotes, including the < and > characters, with the correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="f4c78-124">Doğru abonelik adını çıktısını varlığıyla SubscriptionName özelliğinden alabilirsiniz **Get-AzureSubscription** komutu.</span><span class="sxs-lookup"><span data-stu-id="f4c78-124">You can get the correct subscription name from the SubscriptionName property of the output of the **Get-AzureSubscription** command.</span></span> <span data-ttu-id="f4c78-125">Doğru depolama hesabı adı çıktısını etiket özelliğinden alabilirsiniz **Get-AzureStorageAccount** çalıştırdıktan sonra komut **Select-AzureSubscription** komutu.</span><span class="sxs-lookup"><span data-stu-id="f4c78-125">You can get the correct storage account name from the Label property of the output of the **Get-AzureStorageAccount** command after you run the **Select-AzureSubscription** command.</span></span>

## <a name="step-3-step-by-step-walkthrough---provision-the-virtual-machine-and-join-it-to-the-managed-domain"></a><span data-ttu-id="f4c78-126">Adım 3: Adım adım - sanal makine sağlama ve yönetilen bir etki alanına katılma</span><span class="sxs-lookup"><span data-stu-id="f4c78-126">Step 3: Step-by-step walkthrough - provision the virtual machine and join it to the managed domain</span></span>
<span data-ttu-id="f4c78-127">Okunabilirlik için her bloğu arasında boş satırlar ile bu sanal makine oluşturmak için karşılık gelen Azure PowerShell komutunu aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f4c78-127">Here is the corresponding Azure PowerShell command set to create this virtual machine, with blank lines between each block for readability.</span></span>

<span data-ttu-id="f4c78-128">Sağlanacak Windows sanal makine hakkındaki bilgileri belirtin.</span><span class="sxs-lookup"><span data-stu-id="f4c78-128">Specify information about the Windows virtual machine to be provisioned.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

<span data-ttu-id="f4c78-129">D, DS veya G-serisi sanal makineler için InstanceSize değerleri için bkz: [sanal makine ve bulut hizmeti boyutları Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="f4c78-129">For the InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

<span data-ttu-id="f4c78-130">Yönetilen etki alanı hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="f4c78-130">Provide information about the managed domain.</span></span>

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

<span data-ttu-id="f4c78-131">Bulut hizmeti adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="f4c78-131">Specify the name of the cloud service.</span></span>

    $svcname="Contoso100-test"

<span data-ttu-id="f4c78-132">VM birleştirilmelidir sanal ağın adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="f4c78-132">Specify the name of the virtual network to which the VM should be joined.</span></span> <span data-ttu-id="f4c78-133">AAD DS yönetilen etki alanını bu sanal ağda kullanılabilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f4c78-133">Ensure that the AAD-DS managed domain is available in this virtual network.</span></span>

    $vnetname="MyPreviewVnet"

<span data-ttu-id="f4c78-134">VM sağlamak için kullanılacak VM görüntüsünü seçin.</span><span class="sxs-lookup"><span data-stu-id="f4c78-134">Select the VM image to be used to provision the VM.</span></span>

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="f4c78-135">VM - kümesi VM adı, örnek boyutu & kullanılacak resmi yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f4c78-135">Configure the VM - set VM name, instance size & image to be used.</span></span>

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="f4c78-136">VM için yerel yönetici kimlik bilgilerini edinin.</span><span class="sxs-lookup"><span data-stu-id="f4c78-136">Obtain local administrator credentials for the VM.</span></span> <span data-ttu-id="f4c78-137">Güçlü bir yerel yönetici parolası seçin.</span><span class="sxs-lookup"><span data-stu-id="f4c78-137">Choose a strong local administrator password.</span></span>

    $localadmincred=Get-Credential –Message "Type the name and password of the local administrator account."

<span data-ttu-id="f4c78-138">VM yönetilen etki alanına katmak için 'AAD DC Yöneticiler' grubuna ait bir kullanıcı hesabı için kimlik bilgilerini edinin.</span><span class="sxs-lookup"><span data-stu-id="f4c78-138">Obtain credentials for a user account belonging to 'AAD DC Administrators' group to join VM to the managed domain.</span></span> <span data-ttu-id="f4c78-139">Etki alanı adı - Örneğin, örneğimizde belirtmezseniz, biz 'bob' kullanıcı adı olarak belirtin.</span><span class="sxs-lookup"><span data-stu-id="f4c78-139">Do not specify the domain name - for instance, in our example, we specify 'bob' as the user name.</span></span>

    $domainadmincred=Get-Credential –Message "Now type the name (DO NOT INCLUDE THE DOMAIN) and password of an account in the AAD DC Administrators group, that has permission to add the machine to the domain."

<span data-ttu-id="f4c78-140">VM yapılandırma - etki alanı katılma gereksinim & gerekli kimlik bilgilerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="f4c78-140">Configure the VM - specify domain join requirement & required credentials.</span></span>

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="f4c78-141">Bir alt ağ için VM ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f4c78-141">Set a subnet for the VM.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

<span data-ttu-id="f4c78-142">İsteğe bağlı: etki alanı IP adresine işaret edecek.</span><span class="sxs-lookup"><span data-stu-id="f4c78-142">Optional: Point to the IP address of the domain.</span></span> <span data-ttu-id="f4c78-143">Sanal ağın DNS sunucuları olması için Azure AD etki alanı Hizmetleri yönetilen etki alanı IP adreslerini ayarlarsanız, bu adım gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="f4c78-143">If you set the IP addresses of the Azure AD Domain Services managed domain to be the DNS servers for the virtual network, this step is not required.</span></span>

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

<span data-ttu-id="f4c78-144">Şimdi, etki alanına katılmış Windows VM sağlayın.</span><span class="sxs-lookup"><span data-stu-id="f4c78-144">Now, provision the domain-joined Windows VM.</span></span>

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="script-to-provision-a-windows-vm-and-automatically-join-it-to-an-aad-domain-services-managed-domain"></a><span data-ttu-id="f4c78-145">Bir Windows VM sağlamak ve otomatik olarak bir AAD etki alanı Hizmetleri yönetilen etki alanına eklemek için komut dosyası</span><span class="sxs-lookup"><span data-stu-id="f4c78-145">Script to provision a Windows VM and automatically join it to an AAD Domain Services managed domain</span></span>
<span data-ttu-id="f4c78-146">Bu PowerShell komut kümesini iş sunucu için bir sanal makine oluşturur:</span><span class="sxs-lookup"><span data-stu-id="f4c78-146">This PowerShell command set creates a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="f4c78-147">Windows Server 2012 R2 Datacenter görüntüsü kullanır.</span><span class="sxs-lookup"><span data-stu-id="f4c78-147">Uses the Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="f4c78-148">Ek çok küçük bir sanal makine bulunuyor.</span><span class="sxs-lookup"><span data-stu-id="f4c78-148">Is an extra small virtual machine.</span></span>
* <span data-ttu-id="f4c78-149">Contoso100 test adına sahip.</span><span class="sxs-lookup"><span data-stu-id="f4c78-149">Has the name Contoso100-test.</span></span>
* <span data-ttu-id="f4c78-150">Otomatik olarak etki alanı contoso100 yönetilen etki alanına katılır.</span><span class="sxs-lookup"><span data-stu-id="f4c78-150">Is automatically domain joined to the contoso100 managed domain.</span></span>
* <span data-ttu-id="f4c78-151">Aynı sanal ağa yönetilen etki alanı olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="f4c78-151">Is added to the same virtual network as the managed domain.</span></span>

<span data-ttu-id="f4c78-152">Aşağıda, Windows sanal makine oluşturun ve otomatik olarak Azure AD etki alanı Hizmetleri yönetilen etki alanına katmak için tam örnek komut dosyası verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f4c78-152">Here is the full sample script to create the Windows virtual machine and automatically join it to the Azure AD Domain Services managed domain.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

    $svcname="Contoso100-test"
    $vnetname="MyPreviewVnet"

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $localadmincred=Get-Credential –Message "Type the name and password of the local administrator account."

    $domainadmincred=Get-Credential –Message "Now type the name (not including the domain) and password of an account in the AAD DC Administrators group, that has permission to add the machine to the domain."

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="related-content"></a><span data-ttu-id="f4c78-153">İlgili İçerik</span><span class="sxs-lookup"><span data-stu-id="f4c78-153">Related Content</span></span>
* [<span data-ttu-id="f4c78-154">Azure AD etki alanı Hizmetleri - başlangıç kılavuzu</span><span class="sxs-lookup"><span data-stu-id="f4c78-154">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="f4c78-155">Azure AD Domain Services tarafından yönetilen etki alanını yönetme</span><span class="sxs-lookup"><span data-stu-id="f4c78-155">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
