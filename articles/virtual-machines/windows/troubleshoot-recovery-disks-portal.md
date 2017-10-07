---
title: bir Windows VM hello Azure portal sorun giderme aaaUse | Microsoft Docs
description: "Azure portal kullanarak bağlanan hello işletim sistemi disk tooa kurtarma VM tootroubleshoot Windows sanal makine sorunlarını Azure nasıl hello öğrenin"
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
ms.openlocfilehash: 396f70338fa39f80bb9adcb9244d3c83f2a233eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-portal"></a><span data-ttu-id="5c4dc-103">Bir Windows VM hello işletim sistemi disk tooa kurtarma VM ekleyerek sorun giderme hello Azure portalını kullanma</span><span class="sxs-lookup"><span data-stu-id="5c4dc-103">Troubleshoot a Windows VM by attaching hello OS disk tooa recovery VM using hello Azure portal</span></span>
<span data-ttu-id="5c4dc-104">Azure, Windows sanal makine (VM) önyükleme veya disk bir hatayla karşılaştığında, sorun giderme adımları hello sanal sabit diske kendisini tooperform gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-104">If your Windows virtual machine (VM) in Azure encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="5c4dc-105">Yaygın bir örnek hello VM mümkün tooboot başarıyla engeller başarısız uygulama güncelleştirmesi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-105">A common example would be a failed application update that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="5c4dc-106">Bu makale ayrıntıları toouse hello nasıl Azure portal tooconnect, sanal sabit hataları tooanother Windows VM toofix disk sonra özgün VM'yi yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-106">This article details how toouse hello Azure portal tooconnect your virtual hard disk tooanother Windows VM toofix any errors, then re-create your original VM.</span></span>

## <a name="recovery-process-overview"></a><span data-ttu-id="5c4dc-107">Kurtarma işlemine genel bakış</span><span class="sxs-lookup"><span data-stu-id="5c4dc-107">Recovery process overview</span></span>
<span data-ttu-id="5c4dc-108">sorun giderme işlemi hello aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="5c4dc-108">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="5c4dc-109">Merhaba sanal sabit diskleri tutmak hello VM karşılaşmadan sorunları, silin.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-109">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="5c4dc-110">Ekleme ve sorun giderme amacıyla hello sanal sabit disk tooanother Windows VM bağlayın.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-110">Attach and mount hello virtual hard disk tooanother Windows VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="5c4dc-111">VM sorun giderme toohello bağlayın.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-111">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="5c4dc-112">Dosyaları düzenleyin veya herhangi bir aracı toofix sorunları hello özgün sanal sabit disk üzerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-112">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="5c4dc-113">Çıkarın ve VM sorun giderme hello hello sanal sabit diski kullanımdan çıkarın.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-113">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="5c4dc-114">Merhaba özgün sanal sabit disk kullanan bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-114">Create a VM using hello original virtual hard disk.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="5c4dc-115">Önyükleme sorunlarını belirleme</span><span class="sxs-lookup"><span data-stu-id="5c4dc-115">Determine boot issues</span></span>
<span data-ttu-id="5c4dc-116">neden VM'nizi mümkün tooboot doğru değil toodetermine hello önyükleme tanılaması VM ekran inceleyin.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-116">toodetermine why your VM is not able tooboot correctly, examine hello boot diagnostics VM screenshot.</span></span> <span data-ttu-id="5c4dc-117">Başarısız uygulama güncelleştirme ya da bir temel sanal sabit silindiğinde veya taşındığında disk yaygın bir örnek olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-117">A common example would be a failed application update, or an underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="5c4dc-118">Merhaba Portalı'nda, VM seçin ve ardından toohello kaydırın **destek + sorun giderme** bölümü.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-118">Select your VM in hello portal and then scroll down toohello **Support + Troubleshooting** section.</span></span> <span data-ttu-id="5c4dc-119">Tıklatın **önyükleme tanılama** tooview hello ekran görüntüsü.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-119">Click **Boot diagnostics** tooview hello screenshot.</span></span> <span data-ttu-id="5c4dc-120">Herhangi bir özel hata iletileri veya hata kodları Not toohelp belirlemek hello VM sorunu neden karşılaşıyor.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-120">Note any specific error messages or error codes toohelp determine why hello VM is encountering an issue.</span></span> <span data-ttu-id="5c4dc-121">Merhaba aşağıdaki örnek hizmetleri durdurma bekleniyor VM gösterir:</span><span class="sxs-lookup"><span data-stu-id="5c4dc-121">hello following example shows a VM waiting on stopping services:</span></span>

![Önyükleme tanılaması konsol günlükleri VM görüntüleme](./media/troubleshoot-recovery-disks-portal/screenshot-error.png)

<span data-ttu-id="5c4dc-123">Tıklatarak **ekran** toodownload hello VM ekran yakalama.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-123">You can also click **Screenshot** toodownload a capture of hello VM screenshot.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="5c4dc-124">Var olan sanal sabit disk ayrıntılarını görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="5c4dc-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="5c4dc-125">Sanal sabit disk tooanother VM ekleyebilmek için tooidentify hello adı hello sanal sabit disk (VHD) gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-125">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span> 

<span data-ttu-id="5c4dc-126">Merhaba portalından, bir kaynak grubunu seçin, sonra depolama hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-126">Select your resource group from hello portal, then select your storage account.</span></span> <span data-ttu-id="5c4dc-127">Tıklatın **BLOB'lar**, aşağıdaki örneğine hello olarak:</span><span class="sxs-lookup"><span data-stu-id="5c4dc-127">Click **Blobs**, as in hello following example:</span></span>

![Depolama BLOB'ları seçin](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

<span data-ttu-id="5c4dc-129">Adlı bir kapsayıcıya sahip genellikle **VHD'ler** sanal sabit disklerinizi depolar.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-129">Typically you have a container named **vhds** that stores your virtual hard disks.</span></span> <span data-ttu-id="5c4dc-130">Merhaba kapsayıcı tooview sanal sabit disklerin listesini seçin.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-130">Select hello container tooview a list of virtual hard disks.</span></span> <span data-ttu-id="5c4dc-131">Not Merhaba, VHD adını (Merhaba önekidir genellikle VM hello adı):</span><span class="sxs-lookup"><span data-stu-id="5c4dc-131">Note hello name of your VHD (hello prefix is usually hello name of your VM):</span></span>

![Depolama kapsayıcısı VHD tanımlayın](./media/troubleshoot-recovery-disks-portal/storage-container.png)

<span data-ttu-id="5c4dc-133">Merhaba listeden, varolan bir sanal sabit diski seçin ve hello URL'sini kullanmak için aşağıdaki adımları hello kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="5c4dc-133">Select your existing virtual hard disk from hello list and copy hello URL for use in hello following steps:</span></span>

![Var olan sanal sabit disk URL'sini Kopyala](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a><span data-ttu-id="5c4dc-135">Var olan VM silme</span><span class="sxs-lookup"><span data-stu-id="5c4dc-135">Delete existing VM</span></span>
<span data-ttu-id="5c4dc-136">Sanal sabit diskler ve sanal makineler Azure'da iki ayrı kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-136">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="5c4dc-137">Bir sanal sabit disk hello işletim sisteminin kendisi, uygulamalar ve yapılandırmalar depolandığı ' dir.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-137">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="5c4dc-138">Merhaba VM kendisini hello boyutunu veya konumunu tanımlar ve bir sanal sabit disk veya sanal ağ arabirim kartı (NIC) gibi kaynakları başvuran meta verilerdir.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-138">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="5c4dc-139">Her sanal sabit diske bağlı olduğunda atanmış bir kira sahip tooa VM.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-139">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="5c4dc-140">Veri diskleri bağlı ve hatta hello VM çalışırken ayrılmış olsa da, hello VM kaynak silinmedikçe hello işletim sistemi diski ayrılamıyor.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-140">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="5c4dc-141">Bu VM durduruldu ve deallocated durumda olduğunda bile hello kira tooassociate hello işletim sistemi diski bir VM ile devam eder.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-141">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="5c4dc-142">İlk adım toorecover hello VM toodelete hello VM kendisini kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-142">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="5c4dc-143">Silme hello VM hello sanal sabit diskleri depolama hesabınızdaki bırakır.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-143">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="5c4dc-144">Merhaba, VM silinmiş sonra hello sanal sabit disk tooanother VM tootroubleshoot ekleme ve hello hataları çözümleyin.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-144">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="5c4dc-145">Hello Portalı'nda, VM seçin ve ardından **silmek**:</span><span class="sxs-lookup"><span data-stu-id="5c4dc-145">Select your VM in hello portal, then click **Delete**:</span></span>

![VM önyükleme tanılama önyükleme hatası gösteren ekran görüntüsü](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

<span data-ttu-id="5c4dc-147">Merhaba VM hello sanal sabit disk tooanother VM eklemeden önce silme tamamlanana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-147">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="5c4dc-148">Merhaba kira hello sanal sabit diskte hello VM ile ilişkilendiren hello sanal sabit disk tooanother VM iliştirebilirsiniz önce yayınlanan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-148">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="5c4dc-149">Var olan sanal sabit disk tooanother VM ekleme</span><span class="sxs-lookup"><span data-stu-id="5c4dc-149">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="5c4dc-150">Sonraki birkaç adımda için Merhaba, sorun giderme amacıyla başka bir VM kullanın.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-150">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="5c4dc-151">VM toobe mümkün toobrowse sorun giderme hello varolan sanal sabit disk toothis ekleme ve hello diskin içeriği düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-151">You attach hello existing virtual hard disk toothis troubleshooting VM toobe able toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="5c4dc-152">Bu işlem toocorrect sağlar herhangi bir yapılandırma hataları veya gözden geçirme ek uygulama veya sistem günlük dosyaları, örneğin.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-152">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="5c4dc-153">Seçin veya sorun giderme amacıyla başka bir VM toouse oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-153">Choose or create another VM toouse for troubleshooting purposes.</span></span>

1. <span data-ttu-id="5c4dc-154">Merhaba portalından, bir kaynak grubunu seçin, sonra sorun giderme VM'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-154">Select your resource group from hello portal, then select your troubleshooting VM.</span></span> <span data-ttu-id="5c4dc-155">Seçin **diskleri** ve ardından **Attach varolan**:</span><span class="sxs-lookup"><span data-stu-id="5c4dc-155">Select **Disks** and then click **Attach existing**:</span></span>

    ![Merhaba Portalı'nda mevcut diski kullanıma açın](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. <span data-ttu-id="5c4dc-157">tooselect, mevcut sanal sabit diski tıklatın **VHD dosyasını**:</span><span class="sxs-lookup"><span data-stu-id="5c4dc-157">tooselect your existing virtual hard disk, click **VHD File**:</span></span>

    ![Mevcut bir VHD'ye göz atma](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. <span data-ttu-id="5c4dc-159">Depolama hesabı ve kapsayıcı seçip, varolan bir VHD'Yİ'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-159">Select your storage account and container, then click your existing VHD.</span></span> <span data-ttu-id="5c4dc-160">Merhaba tıklatın **seçin** tooconfirm tercih ettiğiniz düğmesi:</span><span class="sxs-lookup"><span data-stu-id="5c4dc-160">Click hello **Select** button tooconfirm your choice:</span></span>

    ![Mevcut VHD’nizi seçme](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. <span data-ttu-id="5c4dc-162">Artık seçili, VHD ile tıklatın **Tamam** tooattach hello varolan bir sanal sabit disk:</span><span class="sxs-lookup"><span data-stu-id="5c4dc-162">With your VHD now selected, click **OK** tooattach hello existing virtual hard disk:</span></span>

    ![Varolan bir sanal sabit diski ekleme onaylayın](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. <span data-ttu-id="5c4dc-164">Birkaç saniye sonra hello **diskleri** bölmesi, VM için varolan bir sanal sabit bir veri diski bağlı disk listeler:</span><span class="sxs-lookup"><span data-stu-id="5c4dc-164">After a few seconds, hello **Disks** pane for your VM lists your existing virtual hard disk connected as a data disk:</span></span>

    ![Veri diski olarak bağlı olan sanal sabit disk](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="5c4dc-166">Merhaba bağlı veri diski bağlama</span><span class="sxs-lookup"><span data-stu-id="5c4dc-166">Mount hello attached data disk</span></span>

1. <span data-ttu-id="5c4dc-167">Uzak Masaüstü Bağlantısı tooyour VM açın.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-167">Open a Remote Desktop connection tooyour VM.</span></span> <span data-ttu-id="5c4dc-168">Hello Portalı'nda VM seçin ve tıklatın **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-168">Select your VM in hello portal and click **Connect**.</span></span> <span data-ttu-id="5c4dc-169">Merhaba RDP bağlantı dosyasını indirip açın.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-169">Download and open hello RDP connection file.</span></span> <span data-ttu-id="5c4dc-170">Kimlik bilgileri toolog tooyour VM aşağıdaki gibi girin:</span><span class="sxs-lookup"><span data-stu-id="5c4dc-170">Enter your credentials toolog in tooyour VM as follows:</span></span>

    ![Tooyour Uzak Masaüstü kullanarak VM oturum](./media/troubleshoot-recovery-disks-portal/open-remote-desktop.png)

2. <span data-ttu-id="5c4dc-172">Açık **Sunucu Yöneticisi'ni**seçeneğini belirleyip **dosya ve depolama hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-172">Open **Server Manager**, then select **File and Storage Services**.</span></span> 

    ![Dosya ve depolama hizmetleri Sunucu Yöneticisi içinde seçin](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

3. <span data-ttu-id="5c4dc-174">Merhaba veri diski otomatik olarak algılandı ve bağlı.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-174">hello data disk is automatically detected and attached.</span></span> <span data-ttu-id="5c4dc-175">toosee hello listesini bağlı diskler, select **diskleri**.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-175">toosee a list of hello connected disks, select **Disks**.</span></span> <span data-ttu-id="5c4dc-176">Merhaba sürücü harfi dahil olmak üzere, veri diski tooview birim bilgilerinizi seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-176">You can select your data disk tooview volume information, including hello drive letter.</span></span> <span data-ttu-id="5c4dc-177">Merhaba gösterir hello bağlı veri diski örnek ve kullanarak **F:**:</span><span class="sxs-lookup"><span data-stu-id="5c4dc-177">hello following example shows hello data disk attached and using **F:**:</span></span>

    ![Bağlı disk ve birim bilgileri Sunucu Yöneticisi'nde](./media/troubleshoot-recovery-disks-portal/server-manager-disk-attached.png)


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="5c4dc-179">Özgün sanal sabit diskinde ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="5c4dc-179">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="5c4dc-180">Merhaba varolan bir sanal sabit takılı diski ile tüm bakım ve sorun giderme adımları gereken şekilde artık gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-180">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="5c4dc-181">Merhaba sorunlar ele sonra aşağıdaki adımları hello ile devam edin.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-181">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="5c4dc-182">Çıkarın ve özgün sanal sabit disk ayırma</span><span class="sxs-lookup"><span data-stu-id="5c4dc-182">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="5c4dc-183">Hatalarınızı çözüldükten sonra hello varolan sanal sabit diskten, sorun giderme VM ayırma.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-183">Once your errors are resolved, detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="5c4dc-184">VM sorun giderme hello sanal sabit disk toohello ekleme hello kira serbest kadar herhangi bir VM ile sanal sabit disk kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-184">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="5c4dc-185">Merhaba RDP oturumu tooyour VM, açık **Sunucu Yöneticisi'ni**seçeneğini belirleyip **dosya ve depolama hizmetleri**:</span><span class="sxs-lookup"><span data-stu-id="5c4dc-185">From hello RDP session tooyour VM, open **Server Manager**, then select **File and Storage Services**:</span></span>

    ![Sunucu Yöneticisi'nde dosya ve depolama hizmetleri seçin](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

2. <span data-ttu-id="5c4dc-187">Seçin **diskleri** ve veri diskinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-187">Select **Disks** and then select your data disk.</span></span> <span data-ttu-id="5c4dc-188">Veri diskinizi sağ tıklatın ve seçin **Çevrimdışına Al**:</span><span class="sxs-lookup"><span data-stu-id="5c4dc-188">Right-click on your data disk and select **Take Offline**:</span></span>

    ![Sunucu Yöneticisi'nde çevrimdışı olarak Hello veri diski ayarlayın](./media/troubleshoot-recovery-disks-portal/server-manager-set-disk-offline.png)

3. <span data-ttu-id="5c4dc-190">Şimdi hello VM hello sanal sabit diski kullanımdan çıkarın.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-190">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="5c4dc-191">Hello Azure portal, VM seçin ve tıklatın **diskleri**.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-191">Select your VM in hello Azure portal and click **Disks**.</span></span> <span data-ttu-id="5c4dc-192">Varolan bir sanal sabit diski seçin ve ardından **ayırma**:</span><span class="sxs-lookup"><span data-stu-id="5c4dc-192">Select your existing virtual hard disk and then click **Detach**:</span></span>

    ![Varolan bir sanal sabit disk ayırma](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    <span data-ttu-id="5c4dc-194">Merhaba VM başarıyla hello veri diski devam etmeden önce ayrılmış kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-194">Wait until hello VM has successfully detached hello data disk before continuing.</span></span>

## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="5c4dc-195">Özgün sabit diskten VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="5c4dc-195">Create VM from original hard disk</span></span>
<span data-ttu-id="5c4dc-196">bir VM, özgün sanal sabit diskten toocreate kullanmak [bu Azure Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="5c4dc-196">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="5c4dc-197">Merhaba şablon hello VHD URL'si hello gelen kullanarak mevcut sanal ağda, bir VM dağıtır önceki komutu.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-197">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="5c4dc-198">Merhaba tıklatın **tooAzure dağıtmak** gibi düğmesi:</span><span class="sxs-lookup"><span data-stu-id="5c4dc-198">Click hello **Deploy tooAzure** button as follows:</span></span>

![Github'dan şablondan VM dağıtma](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

<span data-ttu-id="5c4dc-200">Merhaba şablon dağıtımı için Azure portal hello yüklenir.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-200">hello template is loaded into hello Azure portal for deployment.</span></span> <span data-ttu-id="5c4dc-201">Yeni VM ve mevcut Azure kaynaklarını Hello adlarını girin ve hello URL tooyour varolan bir sanal sabit diski yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-201">Enter hello names for your new VM and existing Azure resources, and paste hello URL tooyour existing virtual hard disk.</span></span> <span data-ttu-id="5c4dc-202">toobegin hello dağıtım tıklatın **satın alma**:</span><span class="sxs-lookup"><span data-stu-id="5c4dc-202">toobegin hello deployment, click **Purchase**:</span></span>

![VM şablonu dağıtma](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="5c4dc-204">Önyükleme tanılaması yeniden etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="5c4dc-204">Re-enable boot diagnostics</span></span>
<span data-ttu-id="5c4dc-205">Merhaba varolan sanal sabit diskten VM'nizi oluşturduğunuzda, önyükleme tanılaması otomatik olarak etkinleştirilmemiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-205">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="5c4dc-206">toocheck önyükleme tanılaması durumunu hello ve hello Portalı'nda, VM seçin gerekirse açın.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-206">toocheck hello status of boot diagnostics and turn on if needed, select your VM in hello portal.</span></span> <span data-ttu-id="5c4dc-207">Altında **izleme**, tıklatın **tanılama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-207">Under **Monitoring**, click **Diagnostics settings**.</span></span> <span data-ttu-id="5c4dc-208">Merhaba durum olduğundan emin olun **üzerinde**, ve onay işareti sonraki çok hello**önyükleme tanılama** seçilir.</span><span class="sxs-lookup"><span data-stu-id="5c4dc-208">Ensure hello status is **On**, and hello check mark next too**Boot diagnostics** is selected.</span></span> <span data-ttu-id="5c4dc-209">Herhangi bir değişiklik yaparsanız, tıklatın **kaydetmek**:</span><span class="sxs-lookup"><span data-stu-id="5c4dc-209">If you make any changes, click **Save**:</span></span>

![Önyükleme tanılaması ayarları güncelleştirme](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="5c4dc-211">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5c4dc-211">Next steps</span></span>
<span data-ttu-id="5c4dc-212">Tooyour VM bağlantı sorunları yaşıyorsanız, bkz: [sorun giderme RDP bağlantıları tooan Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5c4dc-212">If you are having issues connecting tooyour VM, see [Troubleshoot RDP connections tooan Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="5c4dc-213">VM üzerinde çalışan uygulamalara erişim sorunları için bkz: [Windows VM üzerinde uygulama bağlantı sorunlarını giderme](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5c4dc-213">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="5c4dc-214">Kaynak Yöneticisi'ni kullanma hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5c4dc-214">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>