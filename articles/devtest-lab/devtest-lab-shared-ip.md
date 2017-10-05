---
title: "Azure DevTest Labs paylaşılan IP adresleri anlama | Microsoft Docs"
description: "Paylaşılan IP adreslerini Azure DevTest Labs laboratuvarınız sanal makineleri erişmek için gereken genel IP adresleri en aza indirmek için nasıl kullandığını öğrenin."
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
ms.openlocfilehash: 9f6e1980bf5ea5b41da98a135d89f1c5159921a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a><span data-ttu-id="46acd-103">Azure DevTest Labs paylaşılan IP adresleri anlama</span><span class="sxs-lookup"><span data-stu-id="46acd-103">Understand shared IP addresses in Azure DevTest Labs</span></span>

<span data-ttu-id="46acd-104">Azure DevTest Labs Laboratuvar sanal makineleri tek tek laboratuvarınız sanal makineleri erişmek için gereken genel IP adresleri sayısını en aza indirmek için ortak aynı IP adresini paylaşan olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="46acd-104">Azure DevTest Labs lets lab VMs share the same public IP address to minimize the number of public IP addresses required to access your individual lab VMs.</span></span>  <span data-ttu-id="46acd-105">Bu makalede, paylaşılan IP'leri iş ve bunların ilgili yapılandırma seçenekleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="46acd-105">This article describes how shared IPs work and their related configuration options.</span></span>

## <a name="shared-ip-setting"></a><span data-ttu-id="46acd-106">IP ayarı paylaşılan</span><span class="sxs-lookup"><span data-stu-id="46acd-106">Shared IP setting</span></span>

<span data-ttu-id="46acd-107">Bir laboratuvar oluşturduğunuzda, bir sanal ağ alt ağında yer alıyor.</span><span class="sxs-lookup"><span data-stu-id="46acd-107">When you create a lab, it resides in a subnet of a virtual network.</span></span>  <span data-ttu-id="46acd-108">Varsayılan olarak, bu alt ağ ile oluşturulan **etkinleştir paylaşılan ortak IP** kümesine *Evet*.</span><span class="sxs-lookup"><span data-stu-id="46acd-108">By default, this subnet is created with **Enable shared public IP** set to *Yes*.</span></span>  <span data-ttu-id="46acd-109">Bu yapılandırma tüm alt ağa bir genel IP adresi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="46acd-109">This configuration creates one public IP address for the entire subnet.</span></span>  <span data-ttu-id="46acd-110">Sanal ağlar ve alt ağları yapılandırma hakkında daha fazla bilgi için bkz: [Azure DevTest Labs'de sanal ağ yapılandırma](devtest-lab-configure-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="46acd-110">For more information about configuring virtual networks and subnets, see [Configure a virtual network in Azure DevTest Labs](devtest-lab-configure-vnet.md).</span></span>

![Yeni Laboratuvar alt ağ](media/devtest-lab-shared-ip/lab-subnet.png)

<span data-ttu-id="46acd-112">Var olan Laboratuarları için bu seçeneği seçerek etkinleştirebilirsiniz **yapılandırma ve ilkeleri > sanal ağlar**.</span><span class="sxs-lookup"><span data-stu-id="46acd-112">For existing labs, you can enable this option by selecting **Configuration and policies > Virtual Networks**.</span></span> <span data-ttu-id="46acd-113">Ardından, listeden bir sanal ağı seçin ve seçin **etkinleştirmek genel IP paylaşılan** seçilen alt ağ için.</span><span class="sxs-lookup"><span data-stu-id="46acd-113">Then, select a virtual network from the list and choose **ENABLE SHARED PUBLIC IP** for a selected subnet.</span></span> <span data-ttu-id="46acd-114">Bir ortak IP adresi Laboratuvar VM'ler arasında paylaşmak istemiyorsanız, bu seçenek, tüm laboratuvarında devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46acd-114">You can also disable this option in any lab if you don't want to share a public IP address across lab VMs.</span></span>

<span data-ttu-id="46acd-115">Bu Laboratuvar varsayılan paylaşılan IP olarak oluşturulan herhangi bir VM.</span><span class="sxs-lookup"><span data-stu-id="46acd-115">Any VMs created in this lab default to using a shared IP.</span></span>  <span data-ttu-id="46acd-116">İçinde VM oluştururken, bu ayar gösterilebilir **Gelişmiş ayarları** altında dikey **IP adresi yapılandırması**.</span><span class="sxs-lookup"><span data-stu-id="46acd-116">When creating the VM, this setting can be observed in the **Advanced settings** blade under **IP address configuration**.</span></span>

![Yeni VM](media/devtest-lab-shared-ip/new-vm.png)

- <span data-ttu-id="46acd-118">**Paylaşılan:** olarak oluşturulan tüm sanal makineleri **paylaşılan** (RG) bir kaynak grubuna yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="46acd-118">**Shared:** All VMs created as **Shared** are placed into one resource group (RG).</span></span> <span data-ttu-id="46acd-119">Tek bir IP adresi için RG ve tüm sanal makineleri rg bu IP adresini kullanacak atanır.</span><span class="sxs-lookup"><span data-stu-id="46acd-119">A single IP address is assigned for that RG and all VMs in the RG will use that IP address.</span></span>
- <span data-ttu-id="46acd-120">**Genel:** oluşturduğunuz her VM kendi IP adresi vardır ve kendi kaynak grubunda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="46acd-120">**Public:** Every VM you create has its own IP address and is created in its own resource group.</span></span>
- <span data-ttu-id="46acd-121">**Özel:** oluşturduğunuz her VM özel IP adresini kullanır.</span><span class="sxs-lookup"><span data-stu-id="46acd-121">**Private:** Every VM you create uses a private IP address.</span></span> <span data-ttu-id="46acd-122">Bu VM için Uzak Masaüstü ile internet'ten doğrudan bağlanabiliyor olmaz.</span><span class="sxs-lookup"><span data-stu-id="46acd-122">You will not be able to connect to this VM directly from the internet with Remote Desktop.</span></span>

<span data-ttu-id="46acd-123">Paylaşılan IP etkin olan bir VM alt ağına eklendiğinde DevTest Labs otomatik olarak VM için bir yük dengeleyici ekler ve VM üzerinde RDP noktasına ileten bir TCP bağlantı noktası numarası ortak IP adresini atar.</span><span class="sxs-lookup"><span data-stu-id="46acd-123">Whenever a VM with shared IP enabled is added to the subnet, DevTest Labs automatically adds the VM to a load balancer and assigns a TCP port number on the public IP address, forwarding to the RDP port on the VM.</span></span>  

## <a name="using-the-shared-ip"></a><span data-ttu-id="46acd-124">Paylaşılan IP kullanma</span><span class="sxs-lookup"><span data-stu-id="46acd-124">Using the shared IP</span></span>

- <span data-ttu-id="46acd-125">**Linux kullanıcıları:** VM IP adresini veya tam etki alanı adını, bağlantı noktası tarafından üste ve ardından kullanarak SSH.</span><span class="sxs-lookup"><span data-stu-id="46acd-125">**Linux users:** SSH to the VM by using the IP address or fully qualified domain name, followed by a colon, followed by the port.</span></span> <span data-ttu-id="46acd-126">Örneğin, aşağıdaki resimde VM'e bağlanmak için RDP adresidir `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span><span class="sxs-lookup"><span data-stu-id="46acd-126">For example, in the image below, the RDP address to connect to the VM is `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span></span>

  ![VM örneği](media/devtest-lab-shared-ip/vm-info.png)

- <span data-ttu-id="46acd-128">**Windows kullanıcıları:** seçin **Bağlan** önceden yapılandırılmış bir RDP dosyasını karşıdan yüklemek ve VM erişmek için Azure Portal'da düğmesi.</span><span class="sxs-lookup"><span data-stu-id="46acd-128">**Windows users:** Select the **Connect** button on the Azure portal to download a pre-configured RDP file and access the VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46acd-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="46acd-129">Next steps</span></span>

* [<span data-ttu-id="46acd-130">Azure DevTest Labs'de Laboratuvar ilkeleri tanımlar</span><span class="sxs-lookup"><span data-stu-id="46acd-130">Define lab policies in Azure DevTest Labs</span></span>](devtest-lab-set-lab-policy.md)
* [<span data-ttu-id="46acd-131">Azure DevTest Labs'de sanal ağ yapılandırma</span><span class="sxs-lookup"><span data-stu-id="46acd-131">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md)





