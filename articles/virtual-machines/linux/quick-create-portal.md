---
title: "Azure Hızlı Başlangıç - VM Portalı oluşturma | Microsoft Docs"
description: "Azure Hızlı Başlangıç - VM Portalı oluşturma"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: d009020e86fdfed6a45b5b63b9664c623bcb1843
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-linux-virtual-machine-with-the-azure-portal"></a><span data-ttu-id="890aa-103">Azure portal ile Linux sanal makinesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="890aa-103">Create a Linux virtual machine with the Azure portal</span></span>

<span data-ttu-id="890aa-104">Azure sanal makineleri, Azure portalı üzerinden oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="890aa-104">Azure virtual machines can be created through the Azure portal.</span></span> <span data-ttu-id="890aa-105">Bu yöntem, sanal makineleri ve tüm ilgili kaynakları oluşturup yapılandırmaya yönelik tarayıcı tabanlı bir kullanıcı arabirimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="890aa-105">This method provides a browser-based user interface for creating and configuring virtual machines and all related resources.</span></span> <span data-ttu-id="890aa-106">Sanal makine oluşturma ve VM’ye web sunucusu yüklemeye yönelik Hızlı Başlangıç adımları.</span><span class="sxs-lookup"><span data-stu-id="890aa-106">This Quickstart steps through creating a virtual machine and installing a webserver on the VM.</span></span>

<span data-ttu-id="890aa-107">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="890aa-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-ssh-key-pair"></a><span data-ttu-id="890aa-108">SSH anahtar çifti oluşturma</span><span class="sxs-lookup"><span data-stu-id="890aa-108">Create SSH key pair</span></span>

<span data-ttu-id="890aa-109">Bu hızlı başlangıcı tamamlamak için bir SSH anahtar çifti gerekir.</span><span class="sxs-lookup"><span data-stu-id="890aa-109">You need an SSH key pair to complete this quick start.</span></span> <span data-ttu-id="890aa-110">Bir SSH anahtar çiftiniz varsa bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="890aa-110">If you have an existing SSH key pair, this step can be skipped.</span></span>

<span data-ttu-id="890aa-111">Bir Bash kabuğundan bu komutu çalıştırın ve ekrandaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="890aa-111">From a Bash shell, run this command and follow the on-screen directions.</span></span> <span data-ttu-id="890aa-112">Komut çıktısı genel anahtar dosyasının dosya adını içerir.</span><span class="sxs-lookup"><span data-stu-id="890aa-112">The command output includes the file name of the public key file.</span></span> <span data-ttu-id="890aa-113">Ortak anahtar dosyasının içeriğini panoya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="890aa-113">Copy the contents of the public key file to the clipboard.</span></span>

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="log-in-to-azure"></a><span data-ttu-id="890aa-114">Azure'da oturum açma</span><span class="sxs-lookup"><span data-stu-id="890aa-114">Log in to Azure</span></span> 

<span data-ttu-id="890aa-115">http://portal.azure.com sayfasından Azure portalda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="890aa-115">Log in to the Azure portal at http://portal.azure.com.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="890aa-116">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="890aa-116">Create virtual machine</span></span>

1. <span data-ttu-id="890aa-117">Azure portalının sol üst köşesinde bulunan **Yeni** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="890aa-117">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="890aa-118">**İşlem**'i ve ardından **Ubuntu Server 16.04 LTS**'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="890aa-118">Select **Compute**, and then select **Ubuntu Server 16.04 LTS**.</span></span> 

3. <span data-ttu-id="890aa-119">Sanal makine bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="890aa-119">Enter the virtual machine information.</span></span> <span data-ttu-id="890aa-120">**Kimlik doğrulama türü** için **SSH ortak anahtarı**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="890aa-120">For **Authentication type**, select **SSH public key**.</span></span> <span data-ttu-id="890aa-121">SSH ortak anahtarınıza yapıştırırken, önce veya sonra gelen tüm boşlukları kaldırmaya dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="890aa-121">When pasting in your SSH public key, take care to remove any leading or trailing white space.</span></span> <span data-ttu-id="890aa-122">İşlem tamamlandığında **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="890aa-122">When complete, click **OK**.</span></span>

    ![Portal dikey penceresinde VM’niz ile ilgili temel bilgileri girin](./media/quick-create-portal/create-vm-portal-basic-blade.png)

4. <span data-ttu-id="890aa-124">VM için bir boyut seçin.</span><span class="sxs-lookup"><span data-stu-id="890aa-124">Select a size for the VM.</span></span> <span data-ttu-id="890aa-125">Daha fazla boyut görmek için **Tümünü görüntüle**’yi seçin veya **Desteklenen disk türü** filtresini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="890aa-125">To see more sizes, select **View all** or change the **Supported disk type** filter.</span></span> 

    ![VM boyutlarını gösteren ekran görüntüsü](./media/quick-create-portal/create-linux-vm-portal-sizes.png)  

5. <span data-ttu-id="890aa-127">Ayarlar dikey penceresinde varsayılan değerleri koruyun ve **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="890aa-127">On the settings blade, keep the defaults and click **OK**.</span></span>

6. <span data-ttu-id="890aa-128">Özet sayfasında **Tamam**’a tıklayarak sanal makine dağıtımını başlatın.</span><span class="sxs-lookup"><span data-stu-id="890aa-128">On the summary page, click **Ok** to start the virtual machine deployment.</span></span>

7. <span data-ttu-id="890aa-129">VM, Azure portalı panosuna sabitlenir.</span><span class="sxs-lookup"><span data-stu-id="890aa-129">The VM will be pinned to the Azure portal dashboard.</span></span> <span data-ttu-id="890aa-130">Dağıtım tamamlandıktan sonra VM özeti dikey penceresi otomatik olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="890aa-130">Once the deployment has completed, the VM summary blade automatically opens.</span></span>


## <a name="connect-to-virtual-machine"></a><span data-ttu-id="890aa-131">Sanal makineye bağlanma</span><span class="sxs-lookup"><span data-stu-id="890aa-131">Connect to virtual machine</span></span>

<span data-ttu-id="890aa-132">Sanal makine ile bir SSH bağlantısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="890aa-132">Create an SSH connection with the virtual machine.</span></span>

1. <span data-ttu-id="890aa-133">Sanal makine dikey penceresindeki **Bağlan** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="890aa-133">Click the **Connect** button on the virtual machine blade.</span></span> <span data-ttu-id="890aa-134">Bağlan düğmesi, sanal makineye bağlanmak için kullanılabilen bir SSH bağlantı dizesi gösterir.</span><span class="sxs-lookup"><span data-stu-id="890aa-134">The connect button displays an SSH connection string that can be used to connect to the virtual machine.</span></span>

    ![Portal 9](./media/quick-create-portal/portal-quick-start-9.png) 

2. <span data-ttu-id="890aa-136">Bir SSH oturumu oluşturmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="890aa-136">Run the following command to create an SSH session.</span></span> <span data-ttu-id="890aa-137">Bağlantı dizesini Azure portaldan kopyaladığınız dizeyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="890aa-137">Replace the connection string with the one you copied from the Azure portal.</span></span>

```bash 
ssh azureuser@40.112.21.50
```

## <a name="install-nginx"></a><span data-ttu-id="890aa-138">NGINX yükleme</span><span class="sxs-lookup"><span data-stu-id="890aa-138">Install NGINX</span></span>

<span data-ttu-id="890aa-139">Paket kaynaklarını güncelleştirmek ve en son NGINX paketini yüklemek için aşağıdaki bash betiğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="890aa-139">Use the following bash script to update package sources and install the latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
sudo apt-get -y update

# install NGINX
sudo apt-get -y install nginx
```

<span data-ttu-id="890aa-140">İşiniz bittiğinde, SSH oturumundan çıkıp Azure portalında VM özelliklerine geri dönün.</span><span class="sxs-lookup"><span data-stu-id="890aa-140">When done, exit the SSH session and return the VM properties in the Azure portal.</span></span>


## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="890aa-141">Web trafiği için 80 numaralı bağlantı noktasını açın</span><span class="sxs-lookup"><span data-stu-id="890aa-141">Open port 80 for web traffic</span></span> 

<span data-ttu-id="890aa-142">Ağ güvenlik grubu (NSG), gelen ve giden trafiğin güvenliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="890aa-142">A Network security group (NSG) secures inbound and outbound traffic.</span></span> <span data-ttu-id="890aa-143">Azure portalından bir VM oluşturulduğunda, SSH bağlantıları için 22 numaralı bağlantı noktasında bir gelen kuralı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="890aa-143">When a VM is created from the Azure portal, an inbound rule is created on port 22 for SSH connections.</span></span> <span data-ttu-id="890aa-144">Bu VM bir web sunucusunu barındırdığından, 80 numaralı bağlantı noktası için bir NSG kuralının oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="890aa-144">Because this VM hosts a webserver, an NSG rule needs to be created for port 80.</span></span>

1. <span data-ttu-id="890aa-145">Sanal makinede **Kaynak grubunun** adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="890aa-145">On the virtual machine, click the name of the **Resource group**.</span></span>
2. <span data-ttu-id="890aa-146">**Ağ güvenlik grubu**’nu seçin.</span><span class="sxs-lookup"><span data-stu-id="890aa-146">Select the **network security group**.</span></span> <span data-ttu-id="890aa-147">NSG, **Tür** sütunu kullanılarak tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="890aa-147">The NSG can be identified using the **Type** column.</span></span> 
3. <span data-ttu-id="890aa-148">Sol menüdeki ayarlar altında **Gelen güvenlik kuralları**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="890aa-148">On the left-hand menu, under settings, click **Inbound security rules**.</span></span>
4. <span data-ttu-id="890aa-149">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="890aa-149">Click on **Add**.</span></span>
5. <span data-ttu-id="890aa-150">**Ad** alanına **http** yazın.</span><span class="sxs-lookup"><span data-stu-id="890aa-150">In **Name**, type **http**.</span></span> <span data-ttu-id="890aa-151">**Bağlantı noktası aralığı** değerinin 80, **Eylem** ayarının **İzin Ver** olarak belirlendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="890aa-151">Make sure **Port range** is set to 80 and **Action** is set to **Allow**.</span></span> 
6. <span data-ttu-id="890aa-152">**Tamam** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="890aa-152">Click **OK**.</span></span>


## <a name="view-the-nginx-welcome-page"></a><span data-ttu-id="890aa-153">NGINX karşılama sayfasını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="890aa-153">View the NGINX welcome page</span></span>

<span data-ttu-id="890aa-154">NGINX yüklüyken ve 80 numaralı bağlantı noktası sanal makineniz için açıkken, web sunucusuna İnternet üzerinden erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="890aa-154">With NGINX installed, and port 80 open to your VM, the webserver can now be accessed from the internet.</span></span> <span data-ttu-id="890aa-155">Bir web tarayıcısı açın ve VM’nin ortak IP adresini girin.</span><span class="sxs-lookup"><span data-stu-id="890aa-155">Open a web browser, and enter the public IP address of the VM.</span></span> <span data-ttu-id="890aa-156">Genel IP adresi, Azure portalındaki VM dikey penceresinde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="890aa-156">The public IP address can be found on the VM blade in the Azure portal.</span></span>

![Varsayılan NGINX sitesi](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="890aa-158">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="890aa-158">Clean up resources</span></span>

<span data-ttu-id="890aa-159">Artık gerekli olmadığında kaynak grubunu, sanal makineyi ve tüm ilişkili kaynakları silin.</span><span class="sxs-lookup"><span data-stu-id="890aa-159">When no longer needed, delete the resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="890aa-160">Bunu yapmak için sanal makine dikey penceresinden kaynak grubunu seçip **Sil**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="890aa-160">To do so, select the resource group from the virtual machine blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="890aa-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="890aa-161">Next steps</span></span>

<span data-ttu-id="890aa-162">Bu hızlı başlangıçta basit bir sanal makine ve bir ağ güvenlik grubu kuralı dağıtıp, bir web sunucusu yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="890aa-162">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="890aa-163">Azure sanal makineleri hakkında daha fazla bilgi için Linux VM’lerine yönelik öğreticiye geçin.</span><span class="sxs-lookup"><span data-stu-id="890aa-163">To learn more about Azure virtual machines, continue to the tutorial for Linux VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="890aa-164">Azure Linux sanal makine öğreticileri</span><span class="sxs-lookup"><span data-stu-id="890aa-164">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
