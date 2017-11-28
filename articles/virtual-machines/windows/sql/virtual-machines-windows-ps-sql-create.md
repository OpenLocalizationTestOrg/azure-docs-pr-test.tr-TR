---
title: bir SQL Server sanal makinesine (Resource Manager) Azure PowerShell'de aaaCreate | Microsoft Docs
description: "Bir Azure VM ile SQL Server sanal makineye Galerisi görüntüleri oluşturmak için adımlar ve PowerShell komut dosyaları sağlar."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 98d50dd8-48ad-444f-9031-5378d8270d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/17/2017
ms.author: jroth
ms.openlocfilehash: 2b8cb8f69ff9894a95eab617816a60c8674eeefa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-resource-manager"></a><span data-ttu-id="0d53e-103">Azure PowerShell (Resource Manager) kullanarak bir SQL Server sanal makine sağlama</span><span class="sxs-lookup"><span data-stu-id="0d53e-103">Provision a SQL Server virtual machine using Azure PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0d53e-104">Portal</span><span class="sxs-lookup"><span data-stu-id="0d53e-104">Portal</span></span>](virtual-machines-windows-portal-sql-server-provision.md)
> * [<span data-ttu-id="0d53e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0d53e-105">PowerShell</span></span>](virtual-machines-windows-ps-sql-create.md)
>
>

## <a name="overview"></a><span data-ttu-id="0d53e-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="0d53e-106">Overview</span></span>
<span data-ttu-id="0d53e-107">Bu öğreticide, tek bir Azure sanal makine kullanarak toocreate nasıl hello gösterilir **Azure Resource Manager** Azure PowerShell cmdlet'lerini kullanarak dağıtım modeli.</span><span class="sxs-lookup"><span data-stu-id="0d53e-107">This tutorial shows you how toocreate a single Azure virtual machine using hello **Azure Resource Manager** deployment model using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="0d53e-108">Bu öğreticide, tek bir disk sürücüsü bir görüntüden hello SQL Galerisi kullanarak tek bir sanal makine oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="0d53e-108">In this tutorial, we will create a single virtual machine using a single disk drive from an image in hello SQL Gallery.</span></span> <span data-ttu-id="0d53e-109">Merhaba depolama, ağ ve hello sanal makine tarafından kullanılacak olan işlem kaynakları için yeni sağlayıcıları oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="0d53e-109">We will create new providers for hello storage, network, and compute resources that will be used by hello virtual machine.</span></span> <span data-ttu-id="0d53e-110">Tüm bu kaynaklar için varolan sağlayıcıları varsa, bunun yerine bu sağlayıcılardan kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d53e-110">If you have existing providers for any of these resources, you can use those providers instead.</span></span>

<span data-ttu-id="0d53e-111">Bu konunun Klasik sürümü hello varsa bkz [Klasik Azure PowerShell kullanarak bir SQL Server sanal makine sağlama](../classic/ps-sql-create.md).</span><span class="sxs-lookup"><span data-stu-id="0d53e-111">If you need hello classic version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Classic](../classic/ps-sql-create.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d53e-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0d53e-112">Prerequisites</span></span>
<span data-ttu-id="0d53e-113">Bu öğretici için ihtiyacınız vardır:</span><span class="sxs-lookup"><span data-stu-id="0d53e-113">For this tutorial you'll need:</span></span>

* <span data-ttu-id="0d53e-114">Bir Azure hesabı ve başlamadan önce abonelik.</span><span class="sxs-lookup"><span data-stu-id="0d53e-114">An Azure account and subscription before you start.</span></span> <span data-ttu-id="0d53e-115">Yoksa, kaydolun bir [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0d53e-115">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="0d53e-116">[Azure PowerShell)](/powershell/azure/overview), en düşük sürüm 1.4.0 veya üzeri (sürüm 1.5.0 kullanılarak yazılmış Bu öğretici).</span><span class="sxs-lookup"><span data-stu-id="0d53e-116">[Azure PowerShell)](/powershell/azure/overview), minimum version of 1.4.0 or later (this tutorial written using version 1.5.0).</span></span>
  * <span data-ttu-id="0d53e-117">tooretrieve sürümü, türü **Azure Get-Module - listavailable birlikte**.</span><span class="sxs-lookup"><span data-stu-id="0d53e-117">tooretrieve your version, type **Get-Module Azure -ListAvailable**.</span></span>

## <a name="configure-your-subscription"></a><span data-ttu-id="0d53e-118">Aboneliğinizi yapılandırın</span><span class="sxs-lookup"><span data-stu-id="0d53e-118">Configure your subscription</span></span>
<span data-ttu-id="0d53e-119">Windows PowerShell'i açın ve aşağıdaki cmdlet'i hello çalıştırarak erişim tooyour Azure hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0d53e-119">Open Windows PowerShell and establish access tooyour Azure account by running hello following cmdlet.</span></span> <span data-ttu-id="0d53e-120">Bir oturum açma ekranı tooenter kimlik bilgilerinizi sunulur.</span><span class="sxs-lookup"><span data-stu-id="0d53e-120">You will be presented with a sign in screen tooenter your credentials.</span></span> <span data-ttu-id="0d53e-121">Kullanım hello aynı e-posta ve parola toosign toohello Azure portalını kullanın.</span><span class="sxs-lookup"><span data-stu-id="0d53e-121">Use hello same email and password that you use toosign in toohello Azure portal.</span></span>

    Add-AzureRmAccount

<span data-ttu-id="0d53e-122">Başarıyla oturum açtıktan sonra bazı bilgiler imzalı içinde hello Subscriptionıd içeren ekran görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="0d53e-122">After successfully signing in you will see some information on screen that includes hello SubscriptionId with which you signed in.</span></span> <span data-ttu-id="0d53e-123">Merhaba abonelik tooa farklı bir abonelik değiştirmediğiniz sürece, Bu öğretici için hello kaynakların oluşturulacağını budur.</span><span class="sxs-lookup"><span data-stu-id="0d53e-123">This is hello subscription in which hello resources for this tutorial will be created unless you change tooa different subscription.</span></span> <span data-ttu-id="0d53e-124">Birden çok SubscriptionIds varsa, aşağıdaki cmdlet'i tooreturn hello, SubscriptionIds tümünün listesini çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="0d53e-124">If you have multiple SubscriptionIds, run hello following cmdlet tooreturn a list of all of your SubscriptionIds:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="0d53e-125">toochange tooanother Subscriptionıd, cmdlet istenen Subscriptionıd ile aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0d53e-125">toochange tooanother SubscriptionID, run hello following cmdlet with your desired SubscriptionId.</span></span>

    Select-AzureRmSubscription -SubscriptionId xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="define-image-variables"></a><span data-ttu-id="0d53e-126">Görüntü değişkenleri tanımlayın</span><span class="sxs-lookup"><span data-stu-id="0d53e-126">Define image variables</span></span>
<span data-ttu-id="0d53e-127">toosimplify kullanılabilirliğini ve bu öğreticinin tamamlanan hello betikten anlayış, biz bir dizi değişken tanımlayarak başlar.</span><span class="sxs-lookup"><span data-stu-id="0d53e-127">toosimplify usability and understanding of hello completed script from this tutorial, we will start by defining a number of variables.</span></span> <span data-ttu-id="0d53e-128">Uygun gördüğünüz ancak adlandırma kısıtlamaları ilgili tooname uzunlukları ve özel karakterler sağlanan hello değerlerini değiştirirken dikkatli olun gibi hello parametre değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0d53e-128">Change hello parameter values as you see fit, but beware of naming restrictions related tooname lengths and special characters when modifying hello values provided.</span></span>

### <a name="location-and-resource-group"></a><span data-ttu-id="0d53e-129">Konum ve kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="0d53e-129">Location and Resource Group</span></span>
<span data-ttu-id="0d53e-130">Hello hello sanal makine için diğer kaynaklar oluşturacak iki değişkenleri toodefine hello veri bölgesi ve hello kaynak grubunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="0d53e-130">Use two variables toodefine hello data region and hello resource group into which you will create hello other resources for hello virtual machine.</span></span>

<span data-ttu-id="0d53e-131">İstediğiniz şekilde değiştirin ve sonra bu değişkenleri cmdlet'leri tooinitialize aşağıdaki hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="0d53e-131">Modify as desired and then execute hello following cmdlets tooinitialize these variables.</span></span>

    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"

### <a name="storage-properties"></a><span data-ttu-id="0d53e-132">Depolama özellikleri</span><span class="sxs-lookup"><span data-stu-id="0d53e-132">Storage properties</span></span>
<span data-ttu-id="0d53e-133">Değişkenleri toodefine hello depolama hesabı ve hello türü hello sanal makine tarafından kullanılan depolama toobe aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="0d53e-133">Use hello following variables toodefine hello storage account and hello type of storage toobe used by hello virtual machine.</span></span>

<span data-ttu-id="0d53e-134">İstediğiniz şekilde değiştirin ve sonra bu değişkenleri cmdlet tooinitialize aşağıdaki hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="0d53e-134">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span> <span data-ttu-id="0d53e-135">Bu örnekte, biz kullanıyoruz Not [Premium depolama](../../../storage/common/storage-premium-storage.md), üretim iş yükleri için önerilir.</span><span class="sxs-lookup"><span data-stu-id="0d53e-135">Note that in this example, we are using [Premium Storage](../../../storage/common/storage-premium-storage.md), which is recommended for production workloads.</span></span> <span data-ttu-id="0d53e-136">Bu kılavuz ve diğer öneriler hakkında daha fazla bilgi için bkz: [Azure Virtual Machines'de SQL Server için performans en iyi uygulamaları](virtual-machines-windows-sql-performance.md).</span><span class="sxs-lookup"><span data-stu-id="0d53e-136">For details on this guidance and other recommendations, see [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span></span>

    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

### <a name="network-properties"></a><span data-ttu-id="0d53e-137">Ağ Özellikleri</span><span class="sxs-lookup"><span data-stu-id="0d53e-137">Network properties</span></span>
<span data-ttu-id="0d53e-138">Aşağıdaki değişkenler toodefine hello ağ arabirimi, hello TCP/IP'yi ayırma yöntemi, hello sanal ağ adı, hello sanal alt ağ adı, başlangıç IP adresi aralığı hello sanal ağ için başlangıç IP adresi aralığı hello alt ağı ve hello için hello kullanın Genel etki alanı adı etiketi toobe hello ağında hello sanal makine tarafından kullanılan.</span><span class="sxs-lookup"><span data-stu-id="0d53e-138">Use hello following variables toodefine hello network interface, hello TCP/IP allocation method, hello virtual network name, hello virtual subnet name, hello range of IP addresses for hello virtual network, hello range of IP addresses for hello subnet, and hello public domain name label toobe used by hello network in hello virtual machine.</span></span>

<span data-ttu-id="0d53e-139">İstediğiniz şekilde değiştirin ve sonra bu değişkenleri cmdlet tooinitialize aşağıdaki hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="0d53e-139">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $TCPIPAllocationMethod = "Dynamic"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $DomainName = "sqlvm1"

### <a name="virtual-machine-properties"></a><span data-ttu-id="0d53e-140">Sanal makine özellikleri</span><span class="sxs-lookup"><span data-stu-id="0d53e-140">Virtual machine properties</span></span>
<span data-ttu-id="0d53e-141">Değişkenleri toodefine hello sanal makine adı, hello bilgisayar adı, hello sanal makine boyutu ve hello işletim sistemi disk adı hello sanal makine için aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="0d53e-141">Use hello following variables toodefine hello virtual machine name, hello computer name, hello virtual machine size, and hello operating system disk name for hello virtual machine.</span></span>

<span data-ttu-id="0d53e-142">İstediğiniz şekilde değiştirin ve sonra bu değişkenleri cmdlet tooinitialize aşağıdaki hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="0d53e-142">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

### <a name="image-properties"></a><span data-ttu-id="0d53e-143">Görüntü Özellikleri</span><span class="sxs-lookup"><span data-stu-id="0d53e-143">Image properties</span></span>
<span data-ttu-id="0d53e-144">Değişkenleri toodefine hello görüntü toouse hello sanal makine için aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="0d53e-144">Use hello following variables toodefine hello image toouse for hello virtual machine.</span></span> <span data-ttu-id="0d53e-145">Bu örnekte, hello SQL Server 2016 Enterprise görüntü kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0d53e-145">In this example, hello SQL Server 2016 Enterprise image is used.</span></span>

<span data-ttu-id="0d53e-146">İstediğiniz şekilde değiştirin ve sonra bu değişkenleri cmdlet tooinitialize aşağıdaki hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="0d53e-146">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

<span data-ttu-id="0d53e-147">SQL Server görüntüsü tekliflerinin hello Get-AzureRmVMImageOffer komutuyla tam bir liste alabilir dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="0d53e-147">Note that you can get a full list of SQL Server image offerings with hello Get-AzureRmVMImageOffer command:</span></span>

    Get-AzureRmVMImageOffer -Location 'East US' -Publisher 'MicrosoftSQLServer'

<span data-ttu-id="0d53e-148">Ve hello SKU'ları hello Get-AzureRmVMImageSku komutuyla bir sunum için kullanılabilir görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d53e-148">And you can see hello Skus available for an offering with hello Get-AzureRmVMImageSku command.</span></span> <span data-ttu-id="0d53e-149">Merhaba aşağıdaki komut gösterir tüm SKU'ları Merhaba kullanılabilir **SQL2014SP1 WS2012R2** sunar.</span><span class="sxs-lookup"><span data-stu-id="0d53e-149">hello following command shows all Skus available for hello **SQL2014SP1-WS2012R2** offer.</span></span>

    Get-AzureRmVMImageSku -Location 'East US' -Publisher 'MicrosoftSQLServer' -Offer 'SQL2014SP1-WS2012R2' | Select Skus

## <a name="create-a-resource-group"></a><span data-ttu-id="0d53e-150">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="0d53e-150">Create a resource group</span></span>
<span data-ttu-id="0d53e-151">Merhaba Resource Manager dağıtım modeli ile oluşturduğunuz hello ilk hello kaynak grubu nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="0d53e-151">With hello Resource Manager deployment model, hello first object that you create is hello resource group.</span></span> <span data-ttu-id="0d53e-152">Merhaba kullanacağız [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet toocreate bir Azure kaynak grubu ve kaynaklarına hello kaynakla grup adını ve konumunu daha önce başlatılmış hello değişkenleri tarafından tanımlanmış.</span><span class="sxs-lookup"><span data-stu-id="0d53e-152">We will use hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet toocreate an Azure resource group and its resources with hello resource group name and location defined by hello variables that you previously initialized.</span></span>

<span data-ttu-id="0d53e-153">Cmdlet toocreate aşağıdaki hello yeni kaynak grubunuz yürütün.</span><span class="sxs-lookup"><span data-stu-id="0d53e-153">Execute hello following cmdlet toocreate your new resource group.</span></span>

    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

## <a name="create-a-storage-account"></a><span data-ttu-id="0d53e-154">Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0d53e-154">Create a storage account</span></span>
<span data-ttu-id="0d53e-155">Merhaba sanal makine hello işletim sistemi diski ve hello SQL Server veri ve günlük dosyaları için depolama kaynaklarını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="0d53e-155">hello virtual machine requires storage resources for hello operating system disk and for hello SQL Server data and log files.</span></span> <span data-ttu-id="0d53e-156">Kolaylık olması için tek bir disk için her ikisini de oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="0d53e-156">For simplicity, we will create a single disk for both.</span></span> <span data-ttu-id="0d53e-157">Daha sonra hello kullanarak ek diskleri iliştirebilirsiniz [Ekle-Azure diski](/powershell/module/azure/add-azuredisk) cmdlet'ini tooplace, SQL Server verilerini sıralama ve günlük dosyalarını adanmış diskler üzerinde.</span><span class="sxs-lookup"><span data-stu-id="0d53e-157">You can attach additional disks later using hello [Add-Azure Disk](/powershell/module/azure/add-azuredisk) cmdlet in order tooplace your SQL Server data and log files on dedicated disks.</span></span> <span data-ttu-id="0d53e-158">Merhaba kullanacağız [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet toocreate standart depolama hesabı yeni kaynak grubunuz ve hello depolama hesabı adı, depolama Sku adı ve konumu hello değişkenleri kullanılarak tanımlanan aldığınız daha önce başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="0d53e-158">We will use hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet toocreate a standard storage account in your new resource group and with hello storage account name, storage Sku name, and location defined using hello variables that you previously initialized.</span></span>

<span data-ttu-id="0d53e-159">Cmdlet toocreate aşağıdaki hello yeni depolama hesabınız yürütün.</span><span class="sxs-lookup"><span data-stu-id="0d53e-159">Execute hello following cmdlet toocreate your new storage account.</span></span>

    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

## <a name="create-network-resources"></a><span data-ttu-id="0d53e-160">Ağ kaynakları oluşturun</span><span class="sxs-lookup"><span data-stu-id="0d53e-160">Create network resources</span></span>
<span data-ttu-id="0d53e-161">ağ kaynaklarının sayısını Hello sanal makine için ağ bağlantısı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="0d53e-161">hello virtual machine requires a number of network resources for network connectivity.</span></span>

* <span data-ttu-id="0d53e-162">Her sanal makine bir sanal ağ gerektirir.</span><span class="sxs-lookup"><span data-stu-id="0d53e-162">Each virtual machine requires a virtual network.</span></span>
* <span data-ttu-id="0d53e-163">Bir sanal ağ en az bir alt ağ tanımlanmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0d53e-163">A virtual network must have at least one subnet defined.</span></span>
* <span data-ttu-id="0d53e-164">Bir ağ arabirimi genel veya özel bir IP adresi ile tanımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0d53e-164">A network interface must be defined with either a public or a private IP address.</span></span>

### <a name="create-a-virtual-network-subnet-configuration"></a><span data-ttu-id="0d53e-165">Bir sanal ağ alt ağ yapılandırması oluştur</span><span class="sxs-lookup"><span data-stu-id="0d53e-165">Create a virtual network subnet configuration</span></span>
<span data-ttu-id="0d53e-166">Biz bizim sanal ağ için bir alt ağ yapılandırması oluşturarak başlar.</span><span class="sxs-lookup"><span data-stu-id="0d53e-166">We will start by creating a subnet configuration for our virtual network.</span></span> <span data-ttu-id="0d53e-167">Bizim öğretici için hello kullanarak bir varsayılan alt ağ oluşturacağız [yeni AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0d53e-167">For our tutorial, we will create a default subnet using hello [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet.</span></span> <span data-ttu-id="0d53e-168">Daha önce başlatılmış hello değişkenleri kullanılarak tanımlanan hello alt ağ ad ve adres ön eki ile sanal ağ alt ağı yapılandırmamızın oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="0d53e-168">We will create our virtual network subnet configuration with hello subnet name and address prefix defined using hello variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="0d53e-169">Bu cmdlet kullanılarak hello sanal ağ alt ağ yapılandırması ek özelliklerini tanımlayabilirsiniz, ancak hello Bu öğretici kapsamında değildir.</span><span class="sxs-lookup"><span data-stu-id="0d53e-169">You can define additional properties of hello virtual network subnet configuration using this cmdlet, but that is beyond hello scope of this tutorial.</span></span>
>
>

<span data-ttu-id="0d53e-170">Merhaba cmdlet toocreate aşağıdaki sanal alt ağ yapılandırmanızı yürütün.</span><span class="sxs-lookup"><span data-stu-id="0d53e-170">Execute hello following cmdlet toocreate your virtual subnet configuration.</span></span>

    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix

### <a name="create-a-virtual-network"></a><span data-ttu-id="0d53e-171">Sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="0d53e-171">Create a virtual network</span></span>
<span data-ttu-id="0d53e-172">Ardından, hello kullanarak bizim sanal ağ oluşturacağız [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0d53e-172">Next, we will create our virtual network using hello [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet.</span></span> <span data-ttu-id="0d53e-173">Merhaba adını, konumunu ve daha önce başlatılmış hello değişkenleri kullanma ve hello önceki adımda tanımlanan hello alt ağ yapılandırması kullanma tanımlanan adres öneki ile yeni, kaynak grubundaki bizim sanal ağ oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="0d53e-173">We will create our virtual network in your new resource group, with hello name, location, and address prefix defined using hello variables that you previously initialized, and using hello subnet configuration that you defined in hello previous step.</span></span>

<span data-ttu-id="0d53e-174">Cmdlet toocreate aşağıdaki hello sanal ağınızı yürütün.</span><span class="sxs-lookup"><span data-stu-id="0d53e-174">Execute hello following cmdlet toocreate your virtual network.</span></span>

    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig

### <a name="create-hello-public-ip-address"></a><span data-ttu-id="0d53e-175">Merhaba ortak IP adresi oluştur</span><span class="sxs-lookup"><span data-stu-id="0d53e-175">Create hello public IP address</span></span>
<span data-ttu-id="0d53e-176">Tanımlanan bizim sanal ağ sahibiz, bağlantı toohello sanal makine için bir IP adresi tooconfigure ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="0d53e-176">Now that we have our virtual network defined, we need tooconfigure an IP address for connectivity toohello virtual machine.</span></span> <span data-ttu-id="0d53e-177">Bu öğretici için dinamik IP adresi toosupport Internet bağlantısını kullanarak genel bir IP adresi oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="0d53e-177">For this tutorial, we will create a public IP address using dynamic IP addressing toosupport Internet connectivity.</span></span> <span data-ttu-id="0d53e-178">Merhaba kullanacağız [yeni AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet toocreate hello genel IP adresi hello kaynak grubu oluşturulan prevously ve hello adını, konumunu, ayırma yöntemi ve hello kullanılarak tanımlanmış DNS etki alanı adı etiketi daha önce başlatılmış değişkenleri.</span><span class="sxs-lookup"><span data-stu-id="0d53e-178">We will use hello [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet toocreate hello public IP address in hello resource group created prevously and with hello name, location, allocation method, and DNS domain name label defined using hello variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="0d53e-179">Bu cmdlet kullanılarak hello ortak IP adresinin ek özellikler tanımlayabilirsiniz, ancak hello ilk Bu öğretici kapsamında değildir.</span><span class="sxs-lookup"><span data-stu-id="0d53e-179">You can define additional properties of hello public IP address using this cmdlet, but that is beyond hello scope of this initial tutorial.</span></span> <span data-ttu-id="0d53e-180">Statik adresi ile özel bir adres veya adresi de oluşturabilir, ancak, aynı zamanda hello Bu öğretici kapsamında değildir.</span><span class="sxs-lookup"><span data-stu-id="0d53e-180">You could also create a private address or an address with a static address, but that is also beyond hello scope of this tutorial.</span></span>
>
>

<span data-ttu-id="0d53e-181">Cmdlet toocreate aşağıdaki hello ortak IP adresi yürütün.</span><span class="sxs-lookup"><span data-stu-id="0d53e-181">Execute hello following cmdlet toocreate your public IP address.</span></span>

    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName

### <a name="create-hello-network-interface"></a><span data-ttu-id="0d53e-182">Merhaba ağ arabirimi oluştur</span><span class="sxs-lookup"><span data-stu-id="0d53e-182">Create hello network interface</span></span>
<span data-ttu-id="0d53e-183">Şimdi, sanal makinenin kullanacağı hazır toocreate hello ağ arabirimi duyuyoruz.</span><span class="sxs-lookup"><span data-stu-id="0d53e-183">We are now ready toocreate hello network interface that our virtual machine will use.</span></span> <span data-ttu-id="0d53e-184">Merhaba kullanacağız [yeni AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet toocreate bizim ağ arabirimi hello kaynak grubunda daha önce oluşturduğunuz ve hello adını, konumunu, alt ağ ve genel IP adresi ile önceden tanımlanmış.</span><span class="sxs-lookup"><span data-stu-id="0d53e-184">We will use hello [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet toocreate our network interface in hello resource group created earlier and with hello name, location, subnet and public IP address previously defined.</span></span>

<span data-ttu-id="0d53e-185">Cmdlet toocreate aşağıdaki Merhaba, ağ arabiriminin yürütün.</span><span class="sxs-lookup"><span data-stu-id="0d53e-185">Execute hello following cmdlet toocreate your network interface.</span></span>

    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

## <a name="configure-a-vm-object"></a><span data-ttu-id="0d53e-186">Bir VM nesnesine yapılandırın</span><span class="sxs-lookup"><span data-stu-id="0d53e-186">Configure a VM object</span></span>
<span data-ttu-id="0d53e-187">Biz tanımlanan depolama ve ağ kaynaklarına sahip olduğunuza göre hello sanal makine için hazır toodefine işlem kaynakları duyuyoruz.</span><span class="sxs-lookup"><span data-stu-id="0d53e-187">Now that we have storage and network resources defined, we are ready toodefine compute resources for hello virtual machine.</span></span> <span data-ttu-id="0d53e-188">Bizim öğretici için size hello sanal makine boyutu ve çeşitli işletim sistemi özelliklerini belirtin, daha önce oluşturduğumuz hello ağ arabirimi belirtin, blob depolama alanını tanımlayın ve hello işletim sistemi diski belirtin.</span><span class="sxs-lookup"><span data-stu-id="0d53e-188">For our tutorial, we will specify hello virtual machine size and various operating system properties, specify hello network interface that we previously created, define blob storage, and then specify hello operating system disk.</span></span>

### <a name="create-hello-vm-object"></a><span data-ttu-id="0d53e-189">Merhaba VM nesnesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="0d53e-189">Create hello VM object</span></span>
<span data-ttu-id="0d53e-190">Biz hello sanal makine boyutu belirterek başlar.</span><span class="sxs-lookup"><span data-stu-id="0d53e-190">We will start by specifying hello virtual machine size.</span></span> <span data-ttu-id="0d53e-191">Bu öğretici için size bir DS13 belirlersiniz.</span><span class="sxs-lookup"><span data-stu-id="0d53e-191">For this tutorial, we are specifying a DS13.</span></span> <span data-ttu-id="0d53e-192">Merhaba kullanacağız [yeni AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet toocreate hello adı daha önce başlatılmış hello değişkenleri kullanılarak tanımlanan boyutu ile yapılandırılabilir sanal makine nesnesi.</span><span class="sxs-lookup"><span data-stu-id="0d53e-192">We will use hello [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet toocreate a configurable virtual machine object with hello name and size defined using hello variables that you previously initialized.</span></span>

<span data-ttu-id="0d53e-193">Cmdlet toocreate hello sanal makine nesnesini aşağıdaki hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="0d53e-193">Execute hello following cmdlet toocreate hello virtual machine object.</span></span>

    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize

### <a name="create-a-credential-object-toohold-hello-name-and-password-for-hello-local-administrator-credentials"></a><span data-ttu-id="0d53e-194">Bir kimlik bilgisi nesnesi toohold hello adı ve parola hello yerel yönetici kimlik bilgileri oluşturun</span><span class="sxs-lookup"><span data-stu-id="0d53e-194">Create a credential object toohold hello name and password for hello local administrator credentials</span></span>
<span data-ttu-id="0d53e-195">Merhaba hello sanal makine için işletim sistemi özelliklerini ayarlayabilmeniz için önce kimliğinizi toosupply hello kimlik hello yerel yönetici hesabı için güvenli bir dize gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="0d53e-195">Before we can set hello operating system properties for hello virtual machine, we need toosupply hello credentials for hello local administrator account as a secure string.</span></span> <span data-ttu-id="0d53e-196">tooaccomplish bunu hello kullanacağız [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0d53e-196">tooaccomplish this, we will use hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

<span data-ttu-id="0d53e-197">Cmdlet aşağıdaki hello yürütün ve hello Windows PowerShell kimlik bilgisi isteği penceresinde hello hello Windows sanal makinesinde yerel yönetici hesabı için hello adı ve parola toouse yazın.</span><span class="sxs-lookup"><span data-stu-id="0d53e-197">Execute hello following cmdlet and, in hello Windows PowerShell credential request window, type hello name and password toouse for hello local administrator account in hello Windows virtual machine.</span></span>

    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."

### <a name="set-hello-operating-system-properties-for-hello-virtual-machine"></a><span data-ttu-id="0d53e-198">Merhaba hello sanal makine için işletim sistemi özelliklerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="0d53e-198">Set hello operating system properties for hello virtual machine</span></span>
<span data-ttu-id="0d53e-199">Artık hazır tooset hello sanal makinenin işletim sistemi özellikleri bulunur.</span><span class="sxs-lookup"><span data-stu-id="0d53e-199">Now we are ready tooset hello virtual machine's operating system properties.</span></span> <span data-ttu-id="0d53e-200">Merhaba kullanacağız [kümesi AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) işletim sistemi olarak Windows, cmdlet tooset hello türü gerektiren hello [sanal makine aracısını](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) yüklü toobe belirtin, hello cmdlet'i otomatik sağlar Güncelleştirme ve hello sanal makine adı, hello bilgisayar adı ve daha önce başlatılmış hello değişkenler kullanarak hello kimlik bilgilerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="0d53e-200">We will use hello [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) cmdlet tooset hello type of operating system as Windows, require hello [virtual machine agent](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toobe installed, specify that hello cmdlet enables auto update and set hello virtual machine name, hello computer name, and hello credential using hello variables that you previously initialized.</span></span>

<span data-ttu-id="0d53e-201">Aşağıdaki cmdlet'i tooset hello işletim sistemi özelliklere sanal makineniz için hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="0d53e-201">Execute hello following cmdlet tooset hello operating system properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate

### <a name="add-hello-network-interface-toohello-virtual-machine"></a><span data-ttu-id="0d53e-202">Merhaba ağ arabirimi toohello sanal makine ekleyin</span><span class="sxs-lookup"><span data-stu-id="0d53e-202">Add hello network interface toohello virtual machine</span></span>
<span data-ttu-id="0d53e-203">Ardından, daha önce toohello sanal makine oluşturduğumuz hello ağ arabirimi ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="0d53e-203">Next, we will add hello network interface that we created previously toohello virtual machine.</span></span> <span data-ttu-id="0d53e-204">Merhaba kullanacağız [Ekle AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) daha önce tanımlanan hello ağ arabirimi değişkeni kullanarak cmdlet tooadd hello ağ arabirimi.</span><span class="sxs-lookup"><span data-stu-id="0d53e-204">We will use hello [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) cmdlet tooadd hello network interface using hello network interface variable that you defined earlier.</span></span>

<span data-ttu-id="0d53e-205">Cmdlet tooset hello ağ arabirimi sanal makineniz için aşağıdaki hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="0d53e-205">Execute hello following cmdlet tooset hello network interface for your virtual machine.</span></span>

    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id

### <a name="set-hello-blob-storage-location-for-hello-disk-toobe-used-by-hello-virtual-machine"></a><span data-ttu-id="0d53e-206">Merhaba sanal makine tarafından kullanılan hello disk toobe için Hello blob depolama konumu ayarlayın</span><span class="sxs-lookup"><span data-stu-id="0d53e-206">Set hello blob storage location for hello disk toobe used by hello virtual machine</span></span>
<span data-ttu-id="0d53e-207">Ardından, daha önce tanımlanan hello değişkenleri kullanarak hello sanal makine tarafından kullanılan hello disk toobe için hello blob depolama konumu ayarlarız.</span><span class="sxs-lookup"><span data-stu-id="0d53e-207">Next, we will set hello blob storage location for hello disk toobe used by hello virtual machine using hello variables that you defined earlier.</span></span>

<span data-ttu-id="0d53e-208">Cmdlet tooset hello blob depolama konumu aşağıdaki hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="0d53e-208">Execute hello following cmdlet tooset hello blob storage location.</span></span>

    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"

### <a name="set-hello-operating-system-disk-properties-for-hello-virtual-machine"></a><span data-ttu-id="0d53e-209">Merhaba işletim sistemi hello sanal makine disk özelliklerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="0d53e-209">Set hello operating system disk properties for hello virtual machine</span></span>
<span data-ttu-id="0d53e-210">Ardından, biz hello işletim sistemi hello sanal makine için disk özelliklerini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="0d53e-210">Next, we will set hello operating system disk properties for hello virtual machine.</span></span> <span data-ttu-id="0d53e-211">Merhaba kullanacağız [kümesi AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) hello sanal makine için işletim sistemini hello cmdlet toospecify görüntüden tooread yalnızca önbelleğe alma tooset gelen (SQL Server üzerinde hello yüklendiği aynı disk) ve tanımlayın Merhaba sanal makine adı ve daha önce tanımladığımız hello değişkenleri kullanılarak tanımlanan hello işletim sistemi diski.</span><span class="sxs-lookup"><span data-stu-id="0d53e-211">We will use hello [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) cmdlet toospecify that hello operating system for hello virtual machine will come from an image, tooset caching tooread only (because SQL Server is being installed on hello same disk) and define hello virtual machine name and hello operating system disk defined using hello variables that we defined earlier.</span></span>

<span data-ttu-id="0d53e-212">Aşağıdaki cmdlet'i tooset hello işletim sistemi disk özelliklere sanal makineniz için hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="0d53e-212">Execute hello following cmdlet tooset hello operating system disk properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

### <a name="specify-hello-platform-image-for-hello-virtual-machine"></a><span data-ttu-id="0d53e-213">Merhaba sanal makine için Hello platform görüntüsü belirtin</span><span class="sxs-lookup"><span data-stu-id="0d53e-213">Specify hello platform image for hello virtual machine</span></span>
<span data-ttu-id="0d53e-214">Bizim son yapılandırma adımı toospecify hello platform görüntüsü bizim sanal makine için ' dir.</span><span class="sxs-lookup"><span data-stu-id="0d53e-214">Our last configuration step is toospecify hello platform image for our virtual machine.</span></span> <span data-ttu-id="0d53e-215">Merhaba en son SQL Server 2016 CTP görüntü öğreticimizi için kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="0d53e-215">For our tutorial, we are using hello latest SQL Server 2016 CTP image.</span></span> <span data-ttu-id="0d53e-216">Merhaba kullanacağız [kümesi AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet toouse daha önce tanımlanan hello değişkenleri tarafından tanımlandığı şekilde bu görüntü.</span><span class="sxs-lookup"><span data-stu-id="0d53e-216">We will use hello [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet toouse this image as defined by hello variables that you defined earlier.</span></span>

<span data-ttu-id="0d53e-217">Cmdlet toospecify hello platform görüntüsü sanal makineniz için aşağıdaki hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="0d53e-217">Execute hello following cmdlet toospecify hello platform image for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

## <a name="create-hello-sql-vm"></a><span data-ttu-id="0d53e-218">Merhaba SQL VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="0d53e-218">Create hello SQL VM</span></span>
<span data-ttu-id="0d53e-219">Şimdi hello yapılandırma adımlarını tamamladıktan hazır toocreate hello sanal makine demektir.</span><span class="sxs-lookup"><span data-stu-id="0d53e-219">Now that you have finished hello configuration steps, you are ready toocreate hello virtual machine.</span></span> <span data-ttu-id="0d53e-220">Merhaba kullanacağız [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) biz tanımladığınız hello değişkenleri kullanarak cmdlet toocreate hello sanal makine.</span><span class="sxs-lookup"><span data-stu-id="0d53e-220">We will use hello [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) cmdlet toocreate hello virtual machine using hello variables that we have defined.</span></span>

<span data-ttu-id="0d53e-221">Cmdlet toocreate aşağıdaki hello sanal makineniz yürütün.</span><span class="sxs-lookup"><span data-stu-id="0d53e-221">Execute hello following cmdlet toocreate your virtual machine.</span></span>

    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

<span data-ttu-id="0d53e-222">Merhaba sanal makine oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0d53e-222">hello virtual machine is created.</span></span> <span data-ttu-id="0d53e-223">Merhaba depolama hesabı hello sanal makinenin disk için belirtilen çünkü standart depolama hesabı için önyükleme tanılaması oluşturduğunuz bildirim premium depolama hesabı anlamına gelmektedir.</span><span class="sxs-lookup"><span data-stu-id="0d53e-223">Notice that a standard storage account is created for boot diagnostics because hello specified storage account for hello virtual machine's disk is a premium storage account.</span></span>

<span data-ttu-id="0d53e-224">Bu makinenin hello Azure Portal toosee görüntüleyebiliyorum [ortak IP adresini ve tam etki alanı adını](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="0d53e-224">You can now view this machine in hello Azure Portal toosee [its public IP address and its fully qualified domain name](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="example-script"></a><span data-ttu-id="0d53e-225">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="0d53e-225">Example script</span></span>
<span data-ttu-id="0d53e-226">Merhaba aşağıdaki betiği hello tam PowerShell komut dosyası Bu öğretici için içerir.</span><span class="sxs-lookup"><span data-stu-id="0d53e-226">hello following script contains hello complete PowerShell script for this tutorial.</span></span> <span data-ttu-id="0d53e-227">Kurulum hello Azure aboneliği toouse hello ile zaten sahip olduğunuzu varsayar **Add-AzureRmAccount** ve **Select-AzureRmSubscription** komutları.</span><span class="sxs-lookup"><span data-stu-id="0d53e-227">It assumes that you have already setup hello Azure subscription toouse with hello **Add-AzureRmAccount** and **Select-AzureRmSubscription** commands.</span></span>

    # Variables
    ## Global
    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"
    ## Storage
    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

    ## Network
    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $TCPIPAllocationMethod = "Dynamic"
    $DomainName = "sqlvm1"

    ##Compute
    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

    ##Image
    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

    # Resource Group
    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

    # Storage
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

    # Network
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix
    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig
    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName
    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

    # Compute
    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize
    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."
    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate #-TimeZone = $TimeZone
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

    # Image
    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

    ## Create hello VM in Azure
    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

## <a name="next-steps"></a><span data-ttu-id="0d53e-228">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0d53e-228">Next steps</span></span>
<span data-ttu-id="0d53e-229">Merhaba sanal makine oluşturulduktan sonra RDP ve Kurulum bağlantısı kullanarak hazır tooconnect toohello sanal makine olursunuz.</span><span class="sxs-lookup"><span data-stu-id="0d53e-229">After hello virtual machine is created, you are ready tooconnect toohello virtual machine using RDP and setup connectivity.</span></span> <span data-ttu-id="0d53e-230">Daha fazla bilgi için bkz: [tooa Azure (Kaynak Yöneticisi) üzerinde SQL Server sanal makinesine bağlanmak](virtual-machines-windows-sql-connect.md).</span><span class="sxs-lookup"><span data-stu-id="0d53e-230">For more information, see [Connect tooa SQL Server Virtual Machine on Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).</span></span>

