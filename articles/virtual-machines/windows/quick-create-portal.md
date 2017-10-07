---
title: "aaaAzure hızlı başlangıç - Windows VM Portal oluştur | Microsoft Docs"
description: "Azure Hızlı Başlangıç - Windows VM Portal oluşturma"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5646ad51244db6d214c0121d1f7cc45c59f9a78b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="6cd9e-103">Hello Azure portal ile bir Windows sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="6cd9e-103">Create a Windows virtual machine with hello Azure portal</span></span>

<span data-ttu-id="6cd9e-104">Azure sanal makineleri hello Azure portal oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-104">Azure virtual machines can be created through hello Azure portal.</span></span> <span data-ttu-id="6cd9e-105">Bu yöntem, sanal makineleri ve tüm ilgili kaynakları oluşturup yapılandırmaya yönelik tarayıcı tabanlı bir kullanıcı arabirimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-105">This method provides a browser-based user interface for creating and configuring virtual machines and all related resources.</span></span> <span data-ttu-id="6cd9e-106">Bir sanal makine oluşturma ve hello VM üzerinde bir Web sunucusu yükleme ile bu hızlı başlangıç adımları.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-106">This Quickstart steps through creating a virtual machine and installing a webserver on hello VM.</span></span>

<span data-ttu-id="6cd9e-107">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="6cd9e-108">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="6cd9e-108">Log in tooAzure</span></span>

<span data-ttu-id="6cd9e-109">İçinde toohello http://portal.azure.com Azure portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-109">Log in toohello Azure portal at http://portal.azure.com.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="6cd9e-110">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="6cd9e-110">Create virtual machine</span></span>

1. <span data-ttu-id="6cd9e-111">Merhaba tıklatın **yeni** düğmesi hello sol üst köşesinin hello Azure portalı üzerinde bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-111">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="6cd9e-112">**İşlem**'i seçin ve sonra da **Windows Server 2016 Datacenter**'ı seçin.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-112">Select **Compute**, and then select **Windows Server 2016 Datacenter**.</span></span> 

3. <span data-ttu-id="6cd9e-113">Merhaba sanal makine bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-113">Enter hello virtual machine information.</span></span> <span data-ttu-id="6cd9e-114">Merhaba kullanıcı adı ve parola buraya girilen toohello sanal makinede kullanılan toolog olur.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-114">hello user name and password entered here is used toolog in toohello virtual machine.</span></span> <span data-ttu-id="6cd9e-115">İşlem tamamlandığında **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-115">When complete, click **OK**.</span></span>

    ![Merhaba portal dikey penceresinde, VM ile ilgili temel bilgileri girin](./media/quick-create-portal/create-windows-vm-portal-basic-blade.png)  

4. <span data-ttu-id="6cd9e-117">Merhaba VM boyutunu seçin.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-117">Select a size for hello VM.</span></span> <span data-ttu-id="6cd9e-118">Daha fazla boyutları toosee seçin **tüm görüntüle** veya hello değiştirme **desteklenen disk türü** Filtresi.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-118">toosee more sizes, select **View all** or change hello **Supported disk type** filter.</span></span> 

    ![VM boyutlarını gösteren ekran görüntüsü](./media/quick-create-portal/create-windows-vm-portal-sizes.png)  

5. <span data-ttu-id="6cd9e-120">Hello ayarları dikey penceresinde hello Varsayılanları tutun ve **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-120">On hello settings blade, keep hello defaults and click **OK**.</span></span>

6. <span data-ttu-id="6cd9e-121">Merhaba Özet sayfasında, tıklatın **Tamam** toostart hello sanal makine dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-121">On hello summary page, click **Ok** toostart hello virtual machine deployment.</span></span>

7. <span data-ttu-id="6cd9e-122">Merhaba VM sabitlenmiş toohello Azure portalı panosunun olacaktır.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-122">hello VM will be pinned toohello Azure portal dashboard.</span></span> <span data-ttu-id="6cd9e-123">Merhaba dağıtım tamamlandıktan sonra otomatik olarak hello VM Özet dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-123">Once hello deployment has completed, hello VM summary blade automatically opens.</span></span>


## <a name="connect-toovirtual-machine"></a><span data-ttu-id="6cd9e-124">Toovirtual makineyi bağlayın</span><span class="sxs-lookup"><span data-stu-id="6cd9e-124">Connect toovirtual machine</span></span>

<span data-ttu-id="6cd9e-125">Bir Uzak Masaüstü Bağlantısı toohello sanal makine oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-125">Create a remote desktop connection toohello virtual machine.</span></span>

1. <span data-ttu-id="6cd9e-126">Merhaba tıklatın **Bağlan** hello sanal makine özellikler düğmesine.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-126">Click hello **Connect** button on hello virtual machine properties.</span></span> <span data-ttu-id="6cd9e-127">Uzak Masaüstü Protokolü dosyasını (.rdp dosyası) oluşturulup indirilir.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-127">A Remote Desktop Protocol file (.rdp file) is created and downloaded.</span></span>

    ![Portal 9](./media/quick-create-portal/quick-create-portal/portal-quick-start-9.png) 

2. <span data-ttu-id="6cd9e-129">tooconnect tooyour VM, açık hello RDP dosyasını karşıdan.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-129">tooconnect tooyour VM, open hello downloaded RDP file.</span></span> <span data-ttu-id="6cd9e-130">İstenirse, **Bağlan**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-130">If prompted, click **Connect**.</span></span> <span data-ttu-id="6cd9e-131">Bunun gibi bir RDP istemcisinin gereken bir Mac üzerinde [Uzak Masaüstü İstemcisi](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) hello Mac uygulama Mağazası'ndan.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-131">On a Mac, you need an RDP client such as this [Remote Desktop Client](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) from hello Mac App Store.</span></span>

3. <span data-ttu-id="6cd9e-132">Merhaba kullanıcı adı ve hello sanal makine oluştururken belirttiğiniz parolayı girin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-132">Enter hello user name and password you specified when creating hello virtual machine, then click **Ok**.</span></span>

4. <span data-ttu-id="6cd9e-133">Merhaba oturum açma işlemi sırasında bir sertifika uyarı alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-133">You may receive a certificate warning during hello sign-in process.</span></span> <span data-ttu-id="6cd9e-134">Tıklatın **Evet** veya **devam** hello bağlantıyla tooproceed.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-134">Click **Yes** or **Continue** tooproceed with hello connection.</span></span>


## <a name="install-iis-using-powershell"></a><span data-ttu-id="6cd9e-135">PowerShell kullanarak IIS yükleme</span><span class="sxs-lookup"><span data-stu-id="6cd9e-135">Install IIS using PowerShell</span></span>

<span data-ttu-id="6cd9e-136">Merhaba sanal makinede bir PowerShell oturumu başlatın ve komutu tooinstall IIS aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-136">On hello virtual machine, start a PowerShell session and run hello following command tooinstall IIS.</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="6cd9e-137">İşiniz bittiğinde, hello RDP oturumu çıkmak ve hello VM Özellikleri'hello Azure portal döndürür.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-137">When done, exit hello RDP session and return hello VM properties in hello Azure portal.</span></span>

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="6cd9e-138">Web trafiği için 80 numaralı bağlantı noktasını açın</span><span class="sxs-lookup"><span data-stu-id="6cd9e-138">Open port 80 for web traffic</span></span> 

<span data-ttu-id="6cd9e-139">Ağ güvenlik grubu (NSG), gelen ve giden trafiğin güvenliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-139">A Network security group (NSG) secures inbound and outbound traffic.</span></span> <span data-ttu-id="6cd9e-140">Azure portal hello VM oluşturulduğunda, bir gelen kuralı RDP bağlantıları için 3389 numaralı bağlantı noktasında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-140">When a VM is created from hello Azure portal, an inbound rule is created on port 3389 for RDP connections.</span></span> <span data-ttu-id="6cd9e-141">Bu VM barındıran bir Web sunucusu olduğundan, bir NSG kuralı bağlantı noktası 80 için oluşturulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-141">Because this VM hosts a webserver, an NSG rule needs toobe created for port 80.</span></span>

1. <span data-ttu-id="6cd9e-142">Merhaba hello adına Hello sanal makineye tıklayın **kaynak grubu**.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-142">On hello virtual machine, click hello name of hello **Resource group**.</span></span>
2. <span data-ttu-id="6cd9e-143">Select hello **ağ güvenlik grubu**.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-143">Select hello **network security group**.</span></span> <span data-ttu-id="6cd9e-144">Merhaba NSG hello kullanılarak tanımlanabilir **türü** sütun.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-144">hello NSG can be identified using hello **Type** column.</span></span> 
3. <span data-ttu-id="6cd9e-145">Ayarlar altında hello sol menüsünde tıklatın **gelen güvenlik kuralları**.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-145">On hello left-hand menu, under settings, click **Inbound security rules**.</span></span>
4. <span data-ttu-id="6cd9e-146">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-146">Click on **Add**.</span></span>
5. <span data-ttu-id="6cd9e-147">**Ad** alanına **http** yazın.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-147">In **Name**, type **http**.</span></span> <span data-ttu-id="6cd9e-148">Emin olun **bağlantı noktası aralığı** too80 ayarlanır ve **eylem** çok ayarlanır**izin**.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-148">Make sure **Port range** is set too80 and **Action** is set too**Allow**.</span></span> 
6. <span data-ttu-id="6cd9e-149">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-149">Click **OK**.</span></span>


## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="6cd9e-150">Görünüm hello IIS Karşılama sayfası</span><span class="sxs-lookup"><span data-stu-id="6cd9e-150">View hello IIS welcome page</span></span>

<span data-ttu-id="6cd9e-151">IIS ile tooyour VM yüklü ve bağlantı noktası 80'i açın, hello Web sunucusu artık erişilebilir hello Internet.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-151">With IIS installed, and port 80 open tooyour VM, hello webserver can now be accessed from hello internet.</span></span> <span data-ttu-id="6cd9e-152">Bir web tarayıcısı açın ve hello VM hello ortak IP adresini girin.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-152">Open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="6cd9e-153">Merhaba genel IP adresi hello VM dikey penceresinde hello Azure portalında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-153">hello public IP address can be found on hello VM blade in hello Azure portal.</span></span>

![Varsayılan IIS sitesi](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="6cd9e-155">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="6cd9e-155">Clean up resources</span></span>

<span data-ttu-id="6cd9e-156">Artık gerektiğinde Merhaba kaynak grubu, sanal makine ve tüm ilişkili kaynakları silin.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-156">When no longer needed, delete hello resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="6cd9e-157">toodo bunu hello sanal makine dikey penceresinden hello kaynak grubu seçin ve tıklatın **silmek**.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-157">toodo so, select hello resource group from hello virtual machine blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6cd9e-158">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6cd9e-158">Next steps</span></span>

<span data-ttu-id="6cd9e-159">Bu hızlı başlangıçta basit bir sanal makine ve bir ağ güvenlik grubu kuralı dağıtıp, bir web sunucusu yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-159">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="6cd9e-160">Azure sanal makinelerde hakkında daha fazla toolearn toohello öğretici Windows VM'ler için devam edin.</span><span class="sxs-lookup"><span data-stu-id="6cd9e-160">toolearn more about Azure virtual machines, continue toohello tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6cd9e-161">Azure Windows sanal makine öğreticileri</span><span class="sxs-lookup"><span data-stu-id="6cd9e-161">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
