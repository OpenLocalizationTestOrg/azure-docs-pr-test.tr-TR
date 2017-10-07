---
title: "aaaUnderstand paylaşılan Azure DevTest Labs IP adresleri | Microsoft Docs"
description: "Azure DevTest Labs paylaşılan IP adreslerini toominimize hello ortak IP adresleri gerekli tooaccess laboratuvarınız sanal makineleri nasıl kullandığını öğrenin."
services: devtest-lab
documentationcenter: na
author: camsoper
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: casoper
ms.openlocfilehash: 8756410117a9d550d567d372174bf1ea96703c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a><span data-ttu-id="14176-103">Azure DevTest Labs paylaşılan IP adresleri anlama</span><span class="sxs-lookup"><span data-stu-id="14176-103">Understand shared IP addresses in Azure DevTest Labs</span></span>

<span data-ttu-id="14176-104">Azure DevTest Labs sağlar Laboratuvar VM'ler paylaşımı tek tek laboratuvarınız sanal makineleri aynı ortak IP adresi toominimize hello sayıda ortak IP adresleri gerekli tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="14176-104">Azure DevTest Labs lets lab VMs share hello same public IP address toominimize hello number of public IP addresses required tooaccess your individual lab VMs.</span></span>  <span data-ttu-id="14176-105">Bu makalede, paylaşılan IP'leri iş ve bunların ilgili yapılandırma seçenekleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="14176-105">This article describes how shared IPs work and their related configuration options.</span></span>

## <a name="shared-ip-setting"></a><span data-ttu-id="14176-106">IP ayarı paylaşılan</span><span class="sxs-lookup"><span data-stu-id="14176-106">Shared IP setting</span></span>

<span data-ttu-id="14176-107">Bir laboratuvar oluşturduğunuzda, bir sanal ağ alt ağında yer alıyor.</span><span class="sxs-lookup"><span data-stu-id="14176-107">When you create a lab, it resides in a subnet of a virtual network.</span></span>  <span data-ttu-id="14176-108">Varsayılan olarak, bu alt ağ ile oluşturulan **etkinleştir paylaşılan ortak IP** çok ayarlamak*Evet*.</span><span class="sxs-lookup"><span data-stu-id="14176-108">By default, this subnet is created with **Enable shared public IP** set too*Yes*.</span></span>  <span data-ttu-id="14176-109">Bu yapılandırma hello tüm alt ağ için bir genel IP adresi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="14176-109">This configuration creates one public IP address for hello entire subnet.</span></span>  <span data-ttu-id="14176-110">Sanal ağlar ve alt ağları yapılandırma hakkında daha fazla bilgi için bkz: [Azure DevTest Labs'de sanal ağ yapılandırma](devtest-lab-configure-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="14176-110">For more information about configuring virtual networks and subnets, see [Configure a virtual network in Azure DevTest Labs](devtest-lab-configure-vnet.md).</span></span>

![Yeni Laboratuvar alt ağ](media/devtest-lab-shared-ip/lab-subnet.png)

<span data-ttu-id="14176-112">Var olan Laboratuarları için bu seçeneği seçerek etkinleştirebilirsiniz **yapılandırma ve ilkeleri > sanal ağlar**.</span><span class="sxs-lookup"><span data-stu-id="14176-112">For existing labs, you can enable this option by selecting **Configuration and policies > Virtual Networks**.</span></span> <span data-ttu-id="14176-113">Ardından, bir sanal ağ hello listeden seçip seçin **etkinleştirmek genel IP paylaşılan** seçilen alt ağ için.</span><span class="sxs-lookup"><span data-stu-id="14176-113">Then, select a virtual network from hello list and choose **ENABLE SHARED PUBLIC IP** for a selected subnet.</span></span> <span data-ttu-id="14176-114">Laboratuvar VM'ler arasında bir ortak IP adresi tooshare istemiyorsanız, bu seçenek, tüm laboratuvarında devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14176-114">You can also disable this option in any lab if you don't want tooshare a public IP address across lab VMs.</span></span>

<span data-ttu-id="14176-115">Bu Laboratuvar varsayılan toousing paylaşılan IP oluşturulan herhangi bir VM.</span><span class="sxs-lookup"><span data-stu-id="14176-115">Any VMs created in this lab default toousing a shared IP.</span></span>  <span data-ttu-id="14176-116">Merhaba VM oluştururken, bu ayar hello gösterilebilir **Gelişmiş ayarları** altında dikey **IP adresi yapılandırması**.</span><span class="sxs-lookup"><span data-stu-id="14176-116">When creating hello VM, this setting can be observed in hello **Advanced settings** blade under **IP address configuration**.</span></span>

![Yeni VM](media/devtest-lab-shared-ip/new-vm.png)

- <span data-ttu-id="14176-118">**Paylaşılan:** olarak oluşturulan tüm sanal makineleri **paylaşılan** (RG) bir kaynak grubuna yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="14176-118">**Shared:** All VMs created as **Shared** are placed into one resource group (RG).</span></span> <span data-ttu-id="14176-119">Tek bir IP adresi için RG ve hello RG tüm Vm'lerde bu IP adresini kullanacak atanır.</span><span class="sxs-lookup"><span data-stu-id="14176-119">A single IP address is assigned for that RG and all VMs in hello RG will use that IP address.</span></span>
- <span data-ttu-id="14176-120">**Genel:** oluşturduğunuz her VM kendi IP adresi vardır ve kendi kaynak grubunda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="14176-120">**Public:** Every VM you create has its own IP address and is created in its own resource group.</span></span>
- <span data-ttu-id="14176-121">**Özel:** oluşturduğunuz her VM özel IP adresini kullanır.</span><span class="sxs-lookup"><span data-stu-id="14176-121">**Private:** Every VM you create uses a private IP address.</span></span> <span data-ttu-id="14176-122">Merhaba doğrudan mümkün tooconnect toothis VM olmaz Internet Uzak Masaüstü ile.</span><span class="sxs-lookup"><span data-stu-id="14176-122">You will not be able tooconnect toothis VM directly from hello internet with Remote Desktop.</span></span>

<span data-ttu-id="14176-123">Paylaşılan IP etkin'yle bir VM'yi toohello alt eklendiğinde DevTest Labs otomatik olarak hello VM tooa yük dengeleyici ekler ve toohello hello VM üzerinde RDP noktasına iletme hello genel IP adresi üzerinde bir TCP bağlantı noktası numarası atar.</span><span class="sxs-lookup"><span data-stu-id="14176-123">Whenever a VM with shared IP enabled is added toohello subnet, DevTest Labs automatically adds hello VM tooa load balancer and assigns a TCP port number on hello public IP address, forwarding toohello RDP port on hello VM.</span></span>  

## <a name="using-hello-shared-ip"></a><span data-ttu-id="14176-124">IP paylaşılan Hello kullanma</span><span class="sxs-lookup"><span data-stu-id="14176-124">Using hello shared IP</span></span>

- <span data-ttu-id="14176-125">**Linux kullanıcıları:** hello IP adresini veya tam etki alanı adı, izleyen iki nokta ile kullanarak SSH toohello VM hello bağlantı noktası tarafından izlenen.</span><span class="sxs-lookup"><span data-stu-id="14176-125">**Linux users:** SSH toohello VM by using hello IP address or fully qualified domain name, followed by a colon, followed by hello port.</span></span> <span data-ttu-id="14176-126">Örneğin, aşağıdaki hello görüntü içinde hello RDP adres VM tooconnect toohello `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span><span class="sxs-lookup"><span data-stu-id="14176-126">For example, in hello image below, hello RDP address tooconnect toohello VM is `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span></span>

  ![VM örneği](media/devtest-lab-shared-ip/vm-info.png)

- <span data-ttu-id="14176-128">**Windows kullanıcıları:** Select hello **Bağlan** hello Azure portal toodownload üzerinde önceden yapılandırılmış bir RDP dosyası düğmesini ve hello VM erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14176-128">**Windows users:** Select hello **Connect** button on hello Azure portal toodownload a pre-configured RDP file and access hello VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="14176-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="14176-129">Next steps</span></span>

* [<span data-ttu-id="14176-130">Azure DevTest Labs'de Laboratuvar ilkeleri tanımlar</span><span class="sxs-lookup"><span data-stu-id="14176-130">Define lab policies in Azure DevTest Labs</span></span>](devtest-lab-set-lab-policy.md)
* [<span data-ttu-id="14176-131">Azure DevTest Labs'de sanal ağ yapılandırma</span><span class="sxs-lookup"><span data-stu-id="14176-131">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md)





