---
title: "Bir Windows Azure portalında VM sorun giderme kullanın | Microsoft Docs"
description: "Kurtarma için Azure portalını kullanarak VM işletim sistemi diski bağlanarak azure'da Windows sanal makine sorunlarını giderme hakkında bilgi edinin"
services: virtual-machines-windows
documentationCenter: 
authors: genlin
manager: timlt
editor: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 2c1524949931d69d7553d284bb92c550a61c521a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-the-os-disk-to-a-recovery-vm-using-the-azure-portal"></a><span data-ttu-id="dd35b-103">Kurtarma için Azure portalını kullanarak VM işletim sistemi diski ekleyerek Windows VM sorun giderme</span><span class="sxs-lookup"><span data-stu-id="dd35b-103">Troubleshoot a Windows VM by attaching the OS disk to a recovery VM using the Azure portal</span></span>
<span data-ttu-id="dd35b-104">Azure, Windows sanal makine (VM) önyükleme veya disk bir hatayla karşılaştığında, sanal sabit diskin kendisinde sorun giderme adımları gerçekleştirmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="dd35b-104">If your Windows virtual machine (VM) in Azure encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="dd35b-105">Yaygın bir örnek VM başarıyla önyükleme engeller başarısız uygulama güncelleştirmesi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="dd35b-105">A common example would be a failed application update that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="dd35b-106">Bu makalede Azure portal, sanal sabit diski başka bir Windows hataları düzeltin, sonra özgün VM'yi yeniden oluşturmak için VM'e bağlanmak için nasıl kullanılacağını ayrıntılarını verir.</span><span class="sxs-lookup"><span data-stu-id="dd35b-106">This article details how to use the Azure portal to connect your virtual hard disk to another Windows VM to fix any errors, then re-create your original VM.</span></span>

## <a name="recovery-process-overview"></a><span data-ttu-id="dd35b-107">Kurtarma işlemine genel bakış</span><span class="sxs-lookup"><span data-stu-id="dd35b-107">Recovery process overview</span></span>
<span data-ttu-id="dd35b-108">Sorun giderme işlemi aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="dd35b-108">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="dd35b-109">Sorunlarla, sanal sabit diskleri tutmak VM silin.</span><span class="sxs-lookup"><span data-stu-id="dd35b-109">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="dd35b-110">Ekleme ve sorun giderme amacıyla başka bir Windows VM için sanal sabit diski bağlama.</span><span class="sxs-lookup"><span data-stu-id="dd35b-110">Attach and mount the virtual hard disk to another Windows VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="dd35b-111">Sorun giderme işlemlerini yapacağınız VM'ye bağlanın.</span><span class="sxs-lookup"><span data-stu-id="dd35b-111">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="dd35b-112">Dosyaları düzenleyin veya özgün sanal sabit diskte sorunlarını gidermek için herhangi bir aracı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="dd35b-112">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="dd35b-113">Sorun giderme işlemlerini yaptığınız VM’den sanal sabit diski çıkarın.</span><span class="sxs-lookup"><span data-stu-id="dd35b-113">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="dd35b-114">Özgün sanal sabit disk kullanan bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dd35b-114">Create a VM using the original virtual hard disk.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="dd35b-115">Önyükleme sorunlarını belirleme</span><span class="sxs-lookup"><span data-stu-id="dd35b-115">Determine boot issues</span></span>
<span data-ttu-id="dd35b-116">Neden VM'yi doğru önyükleme mümkün değil belirlemek için önyükleme tanılaması VM ekran inceleyin.</span><span class="sxs-lookup"><span data-stu-id="dd35b-116">To determine why your VM is not able to boot correctly, examine the boot diagnostics VM screenshot.</span></span> <span data-ttu-id="dd35b-117">Başarısız uygulama güncelleştirme ya da bir temel sanal sabit silindiğinde veya taşındığında disk yaygın bir örnek olacaktır.</span><span class="sxs-lookup"><span data-stu-id="dd35b-117">A common example would be a failed application update, or an underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="dd35b-118">Portalda, VM seçin ve sonra aşağı kaydırın **destek + sorun giderme** bölümü.</span><span class="sxs-lookup"><span data-stu-id="dd35b-118">Select your VM in the portal and then scroll down to the **Support + Troubleshooting** section.</span></span> <span data-ttu-id="dd35b-119">Tıklatın **önyükleme tanılama** ekran görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="dd35b-119">Click **Boot diagnostics** to view the screenshot.</span></span> <span data-ttu-id="dd35b-120">Herhangi bir özel hata iletileri veya hata kodları VM bir sorunla karşılaşan neden belirlemenize yardımcı olması için unutmayın.</span><span class="sxs-lookup"><span data-stu-id="dd35b-120">Note any specific error messages or error codes to help determine why the VM is encountering an issue.</span></span> <span data-ttu-id="dd35b-121">Aşağıdaki örnek, hizmetleri durdurma bekleniyor VM gösterir:</span><span class="sxs-lookup"><span data-stu-id="dd35b-121">The following example shows a VM waiting on stopping services:</span></span>

![Önyükleme tanılaması konsol günlükleri VM görüntüleme](./media/troubleshoot-recovery-disks-portal/screenshot-error.png)

<span data-ttu-id="dd35b-123">Tıklatarak **ekran** VM ekran yakalama karşıdan yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="dd35b-123">You can also click **Screenshot** to download a capture of the VM screenshot.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="dd35b-124">Var olan sanal sabit disk ayrıntılarını görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="dd35b-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="dd35b-125">Sanal sabit disk için başka bir VM iliştirebilirsiniz önce sanal sabit disk (VHD) adını tanımlamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd35b-125">Before you can attach your virtual hard disk to another VM, you need to identify the name of the virtual hard disk (VHD).</span></span> 

<span data-ttu-id="dd35b-126">Portal, kaynak grubunu seçin, sonra depolama hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="dd35b-126">Select your resource group from the portal, then select your storage account.</span></span> <span data-ttu-id="dd35b-127">Tıklatın **BLOB'lar**, aşağıdaki örnekte olduğu gibi:</span><span class="sxs-lookup"><span data-stu-id="dd35b-127">Click **Blobs**, as in the following example:</span></span>

![Depolama BLOB'ları seçin](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

<span data-ttu-id="dd35b-129">Adlı bir kapsayıcıya sahip genellikle **VHD'ler** sanal sabit disklerinizi depolar.</span><span class="sxs-lookup"><span data-stu-id="dd35b-129">Typically you have a container named **vhds** that stores your virtual hard disks.</span></span> <span data-ttu-id="dd35b-130">Sanal sabit disklerin listesini görüntülemek için bir kapsayıcı seçin.</span><span class="sxs-lookup"><span data-stu-id="dd35b-130">Select the container to view a list of virtual hard disks.</span></span> <span data-ttu-id="dd35b-131">(Önek genellikle VM adıdır), VHD adını not edin:</span><span class="sxs-lookup"><span data-stu-id="dd35b-131">Note the name of your VHD (the prefix is usually the name of your VM):</span></span>

![Depolama kapsayıcısı VHD tanımlayın](./media/troubleshoot-recovery-disks-portal/storage-container.png)

<span data-ttu-id="dd35b-133">Listeden, varolan bir sanal sabit diski seçin ve aşağıdaki adımlarda kullanılmak URL'yi kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="dd35b-133">Select your existing virtual hard disk from the list and copy the URL for use in the following steps:</span></span>

![Var olan sanal sabit disk URL'sini Kopyala](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a><span data-ttu-id="dd35b-135">Var olan VM silme</span><span class="sxs-lookup"><span data-stu-id="dd35b-135">Delete existing VM</span></span>
<span data-ttu-id="dd35b-136">Sanal sabit diskler ve sanal makineler Azure'da iki ayrı kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="dd35b-136">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="dd35b-137">Bir sanal sabit disk, işletim sisteminin kendisi, uygulamalar ve yapılandırmalar depolandığı ' dir.</span><span class="sxs-lookup"><span data-stu-id="dd35b-137">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="dd35b-138">VM boyutunu veya konumunu tanımlar ve bir sanal sabit disk veya sanal ağ arabirim kartı (NIC) gibi kaynakları başvuran meta verilerdir.</span><span class="sxs-lookup"><span data-stu-id="dd35b-138">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="dd35b-139">Her sanal sabit disk için bir VM eklendiğinde atanmış bir kira var.</span><span class="sxs-lookup"><span data-stu-id="dd35b-139">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="dd35b-140">Veri diskleri VM çalışırken bile eklenip çıkarılabilir, ancak VM kaynağı silinmedikçe işletim sistemi diski çıkarılamaz.</span><span class="sxs-lookup"><span data-stu-id="dd35b-140">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="dd35b-141">Bu VM durduruldu ve deallocated durumda olduğunda bile işletim sistemi diski bir VM ile ilişkilendirilecek kira sürdürür.</span><span class="sxs-lookup"><span data-stu-id="dd35b-141">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="dd35b-142">VM kurtarmak için ilk adım, VM kaynak silmektir.</span><span class="sxs-lookup"><span data-stu-id="dd35b-142">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="dd35b-143">VM’yi sildiğinizde sanal sabit diskler depolama hesabınızda kalır.</span><span class="sxs-lookup"><span data-stu-id="dd35b-143">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="dd35b-144">VM silindikten sonra sanal sabit diski ve hataları gidermek için başka bir VM'e ekleyin.</span><span class="sxs-lookup"><span data-stu-id="dd35b-144">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="dd35b-145">Portalda VM seçin ve sonra tıklatın **silmek**:</span><span class="sxs-lookup"><span data-stu-id="dd35b-145">Select your VM in the portal, then click **Delete**:</span></span>

![VM önyükleme tanılama önyükleme hatası gösteren ekran görüntüsü](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

<span data-ttu-id="dd35b-147">VM için başka bir VM sanal sabit disk eklemeden önce silme tamamlanana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="dd35b-147">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="dd35b-148">VM ile ilişkilendirir sanal sabit disk üzerindeki kira süresini sanal sabit disk için başka bir VM eklemeden önce yayımlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd35b-148">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="dd35b-149">Varolan bir sanal sabit diski başka bir VM'e ekleyin</span><span class="sxs-lookup"><span data-stu-id="dd35b-149">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="dd35b-150">Sonraki birkaç adımda için sorun giderme amacıyla başka bir VM kullanın.</span><span class="sxs-lookup"><span data-stu-id="dd35b-150">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="dd35b-151">Varolan bir sanal sabit diski bulun ve diskin içeriği düzenlemek için sorun giderme bu VM'e ekleyin.</span><span class="sxs-lookup"><span data-stu-id="dd35b-151">You attach the existing virtual hard disk to this troubleshooting VM to be able to browse and edit the disk's content.</span></span> <span data-ttu-id="dd35b-152">Bu işlem, yapılandırma hataları düzeltin ya da ek uygulama veya sistem günlük dosyalarını, örneğin gözden olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="dd35b-152">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="dd35b-153">Seçin veya sorun giderme amacıyla kullanmak için başka bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dd35b-153">Choose or create another VM to use for troubleshooting purposes.</span></span>

1. <span data-ttu-id="dd35b-154">Portaldan, kaynak grubunu seçin, sonra sorun giderme VM'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="dd35b-154">Select your resource group from the portal, then select your troubleshooting VM.</span></span> <span data-ttu-id="dd35b-155">Seçin **diskleri** ve ardından **Attach varolan**:</span><span class="sxs-lookup"><span data-stu-id="dd35b-155">Select **Disks** and then click **Attach existing**:</span></span>

    ![Portalı'nda mevcut diski kullanıma açın](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. <span data-ttu-id="dd35b-157">Mevcut sanal sabit diskinizi seçmek için **VHD Dosyası**’na tıklayın:</span><span class="sxs-lookup"><span data-stu-id="dd35b-157">To select your existing virtual hard disk, click **VHD File**:</span></span>

    ![Mevcut bir VHD'ye göz atma](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. <span data-ttu-id="dd35b-159">Depolama hesabı ve kapsayıcı seçip, varolan bir VHD'Yİ'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="dd35b-159">Select your storage account and container, then click your existing VHD.</span></span> <span data-ttu-id="dd35b-160">Tıklatın **seçin** düğmesi Seçiminizi onaylayın:</span><span class="sxs-lookup"><span data-stu-id="dd35b-160">Click the **Select** button to confirm your choice:</span></span>

    ![Mevcut VHD’nizi seçme](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. <span data-ttu-id="dd35b-162">Artık seçili, VHD ile tıklatın **Tamam** varolan bir sanal sabit diski eklemek için:</span><span class="sxs-lookup"><span data-stu-id="dd35b-162">With your VHD now selected, click **OK** to attach the existing virtual hard disk:</span></span>

    ![Varolan bir sanal sabit diski ekleme onaylayın](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. <span data-ttu-id="dd35b-164">Birkaç saniye sonra **diskleri** bölmesi, VM için varolan bir sanal sabit bir veri diski bağlı disk listeler:</span><span class="sxs-lookup"><span data-stu-id="dd35b-164">After a few seconds, the **Disks** pane for your VM lists your existing virtual hard disk connected as a data disk:</span></span>

    ![Veri diski olarak bağlı olan sanal sabit disk](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="dd35b-166">Bağlı veri diski bağlama</span><span class="sxs-lookup"><span data-stu-id="dd35b-166">Mount the attached data disk</span></span>

1. <span data-ttu-id="dd35b-167">Uzak Masaüstü Bağlantısı, VM açın.</span><span class="sxs-lookup"><span data-stu-id="dd35b-167">Open a Remote Desktop connection to your VM.</span></span> <span data-ttu-id="dd35b-168">Portal ve tıklatın, VM seçin **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="dd35b-168">Select your VM in the portal and click **Connect**.</span></span> <span data-ttu-id="dd35b-169">Karşıdan yükle ve RDP bağlantı dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="dd35b-169">Download and open the RDP connection file.</span></span> <span data-ttu-id="dd35b-170">VM'nize gibi oturum açmak için kimlik bilgilerinizi girin:</span><span class="sxs-lookup"><span data-stu-id="dd35b-170">Enter your credentials to log in to your VM as follows:</span></span>

    ![VM'nize Uzak Masaüstü kullanarak oturum açın](./media/troubleshoot-recovery-disks-portal/open-remote-desktop.png)

2. <span data-ttu-id="dd35b-172">Açık **Sunucu Yöneticisi'ni**seçeneğini belirleyip **dosya ve depolama hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="dd35b-172">Open **Server Manager**, then select **File and Storage Services**.</span></span> 

    ![Dosya ve depolama hizmetleri Sunucu Yöneticisi içinde seçin](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

3. <span data-ttu-id="dd35b-174">Veri diski otomatik olarak algılanır ve bağlı.</span><span class="sxs-lookup"><span data-stu-id="dd35b-174">The data disk is automatically detected and attached.</span></span> <span data-ttu-id="dd35b-175">Bağlı disklerin listesini görmek için seçin **diskleri**.</span><span class="sxs-lookup"><span data-stu-id="dd35b-175">To see a list of the connected disks, select **Disks**.</span></span> <span data-ttu-id="dd35b-176">Sürücü harfi birim bilgilerini görüntülemek için veri diski seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd35b-176">You can select your data disk to view volume information, including the drive letter.</span></span> <span data-ttu-id="dd35b-177">Aşağıdaki örnek, iliştirilmiş ve kullanarak veri diski gösterir **F:**:</span><span class="sxs-lookup"><span data-stu-id="dd35b-177">The following example shows the data disk attached and using **F:**:</span></span>

    ![Bağlı disk ve birim bilgileri Sunucu Yöneticisi'nde](./media/troubleshoot-recovery-disks-portal/server-manager-disk-attached.png)


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="dd35b-179">Özgün sanal sabit diskinde ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="dd35b-179">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="dd35b-180">Varolan bir sanal sabit takılı diski ile tüm bakım ve sorun giderme adımları gereken şekilde artık gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd35b-180">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="dd35b-181">Sorunları giderdikten sonra aşağıdaki adımlarla devam edin.</span><span class="sxs-lookup"><span data-stu-id="dd35b-181">Once you have addressed the issues, continue with the following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="dd35b-182">Çıkarın ve özgün sanal sabit disk ayırma</span><span class="sxs-lookup"><span data-stu-id="dd35b-182">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="dd35b-183">Hatalarınızı çözüldükten sonra sorun giderme VM varolan sanal sabit diski kullanımdan çıkarın.</span><span class="sxs-lookup"><span data-stu-id="dd35b-183">Once your errors are resolved, detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="dd35b-184">Sorun giderme VM için sanal sabit disk ekleme kira serbest kadar herhangi bir VM ile sanal sabit disk kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="dd35b-184">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="dd35b-185">VM için RDP oturumundan açmak **Sunucu Yöneticisi'ni**seçeneğini belirleyip **dosya ve depolama hizmetleri**:</span><span class="sxs-lookup"><span data-stu-id="dd35b-185">From the RDP session to your VM, open **Server Manager**, then select **File and Storage Services**:</span></span>

    ![Sunucu Yöneticisi'nde dosya ve depolama hizmetleri seçin](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

2. <span data-ttu-id="dd35b-187">Seçin **diskleri** ve veri diskinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="dd35b-187">Select **Disks** and then select your data disk.</span></span> <span data-ttu-id="dd35b-188">Veri diskinizi sağ tıklatın ve seçin **Çevrimdışına Al**:</span><span class="sxs-lookup"><span data-stu-id="dd35b-188">Right-click on your data disk and select **Take Offline**:</span></span>

    ![Sunucu Yöneticisi'nde çevrimdışı olarak veri diski ayarlayın](./media/troubleshoot-recovery-disks-portal/server-manager-set-disk-offline.png)

3. <span data-ttu-id="dd35b-190">Şimdi VM sanal sabit diski kullanımdan çıkarın.</span><span class="sxs-lookup"><span data-stu-id="dd35b-190">Now detach the virtual hard disk from the VM.</span></span> <span data-ttu-id="dd35b-191">Azure portalında, VM seçin ve tıklatın **diskleri**.</span><span class="sxs-lookup"><span data-stu-id="dd35b-191">Select your VM in the Azure portal and click **Disks**.</span></span> <span data-ttu-id="dd35b-192">Varolan bir sanal sabit diski seçin ve ardından **ayırma**:</span><span class="sxs-lookup"><span data-stu-id="dd35b-192">Select your existing virtual hard disk and then click **Detach**:</span></span>

    ![Varolan bir sanal sabit disk ayırma](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    <span data-ttu-id="dd35b-194">VM başarıyla veri diski devam etmeden önce ayrılmış kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="dd35b-194">Wait until the VM has successfully detached the data disk before continuing.</span></span>

## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="dd35b-195">Özgün sabit diskten VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="dd35b-195">Create VM from original hard disk</span></span>
<span data-ttu-id="dd35b-196">Özgün sanal sabit diskten bir VM oluşturmak için kullanmak [bu Azure Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="dd35b-196">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="dd35b-197">Önceki komutu VHD URL'yi kullanarak mevcut sanal ağda, bir VM şablonu dağıtır.</span><span class="sxs-lookup"><span data-stu-id="dd35b-197">The template deploys a VM into an existing virtual network, using the VHD URL from the earlier command.</span></span> <span data-ttu-id="dd35b-198">Tıklatın **Azure'a Dağıt** gibi düğmesi:</span><span class="sxs-lookup"><span data-stu-id="dd35b-198">Click the **Deploy to Azure** button as follows:</span></span>

![Github'dan şablondan VM dağıtma](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

<span data-ttu-id="dd35b-200">Şablon dağıtımı için Azure portal içine yüklenir.</span><span class="sxs-lookup"><span data-stu-id="dd35b-200">The template is loaded into the Azure portal for deployment.</span></span> <span data-ttu-id="dd35b-201">Yeni VM ve mevcut Azure kaynakları için adlar girin ve, varolan bir sanal sabit diski URL'sini yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="dd35b-201">Enter the names for your new VM and existing Azure resources, and paste the URL to your existing virtual hard disk.</span></span> <span data-ttu-id="dd35b-202">Dağıtımı başlatmak için tıklatın **satın alma**:</span><span class="sxs-lookup"><span data-stu-id="dd35b-202">To begin the deployment, click **Purchase**:</span></span>

![VM şablonu dağıtma](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="dd35b-204">Önyükleme tanılaması yeniden etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="dd35b-204">Re-enable boot diagnostics</span></span>
<span data-ttu-id="dd35b-205">Var olan sanal sabit diskten VM'nizi oluşturduğunuzda, önyükleme tanılaması otomatik olarak etkinleştirilmemiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="dd35b-205">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="dd35b-206">Önyükleme tanılaması durumunu denetleyin ve gerekirse etkinleştirmek için portalda, VM'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="dd35b-206">To check the status of boot diagnostics and turn on if needed, select your VM in the portal.</span></span> <span data-ttu-id="dd35b-207">Altında **izleme**, tıklatın **tanılama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="dd35b-207">Under **Monitoring**, click **Diagnostics settings**.</span></span> <span data-ttu-id="dd35b-208">Durum olduğundan emin olun **üzerinde**ve yanındaki onay işareti **önyükleme tanılama** seçilir.</span><span class="sxs-lookup"><span data-stu-id="dd35b-208">Ensure the status is **On**, and the check mark next to **Boot diagnostics** is selected.</span></span> <span data-ttu-id="dd35b-209">Herhangi bir değişiklik yaparsanız, tıklatın **kaydetmek**:</span><span class="sxs-lookup"><span data-stu-id="dd35b-209">If you make any changes, click **Save**:</span></span>

![Önyükleme tanılaması ayarları güncelleştirme](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="dd35b-211">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dd35b-211">Next steps</span></span>
<span data-ttu-id="dd35b-212">VM'nize bağlantı sorunları yaşıyorsanız, bkz: [bir Azure VM için RDP sorun giderme bağlantılarını](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dd35b-212">If you are having issues connecting to your VM, see [Troubleshoot RDP connections to an Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="dd35b-213">VM üzerinde çalışan uygulamalara erişim sorunları için bkz: [Windows VM üzerinde uygulama bağlantı sorunlarını giderme](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dd35b-213">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="dd35b-214">Kaynak Yöneticisi'ni kullanma hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dd35b-214">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>