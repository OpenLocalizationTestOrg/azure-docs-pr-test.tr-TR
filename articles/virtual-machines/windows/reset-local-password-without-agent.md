---
title: "aaaReset Azure Aracısı olmadan yerel Windows parola | Microsoft Docs"
description: "Nasıl tooreset hello yerel Windows kullanıcı hesabının parolasını hello Azure Konuk aracısı yüklü olan veya bir VM üzerinde çalışan olmadığında"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf353dd3-89c9-47f6-a449-f874f0957013
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/07/2017
ms.author: iainfou
ms.openlocfilehash: c559c31ea142f9cf50d2c5b6182c5355fec9bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-windows-password-for-azure-vm"></a><span data-ttu-id="d4c78-103">Nasıl Azure VM için yerel Windows parola tooreset</span><span class="sxs-lookup"><span data-stu-id="d4c78-103">How tooreset local Windows password for Azure VM</span></span>
<span data-ttu-id="d4c78-104">Bir VM hello kullanarak azure'da hello yerel Windows parolasını sıfırlayabilir [Azure portalında veya Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello Azure Konuk aracısı yüklü sağlanan.</span><span class="sxs-lookup"><span data-stu-id="d4c78-104">You can reset hello local Windows password of a VM in Azure using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) provided hello Azure guest agent is installed.</span></span> <span data-ttu-id="d4c78-105">Bu yöntem hello birincil yolu tooreset bir Azure VM için bir parola kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d4c78-105">This method is hello primary way tooreset a password for an Azure VM.</span></span> <span data-ttu-id="d4c78-106">Yanıt vermiyor veya özel bir görüntü dosyalarını karşıya yükledikten sonra tooinstall başarısız hello Azure Konuk Aracısı ile sorunlarla karşılaşırsanız, el ile Windows parolanızı sıfırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4c78-106">If you encounter issues with hello Azure guest agent not responding, or failing tooinstall after uploading a custom image, you can manually reset a Windows password.</span></span> <span data-ttu-id="d4c78-107">Bu makalede nasıl tooreset ekleyerek bir yerel hesap parolası hello kaynak işletim sistemi sanal disk tooanother VM ayrıntıları verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="d4c78-107">This article details how tooreset a local account password by attaching hello source OS virtual disk tooanother VM.</span></span> 

> [!WARNING]
> <span data-ttu-id="d4c78-108">Yalnızca bu işlemi son çare olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="d4c78-108">Only use this process as a last resort.</span></span> <span data-ttu-id="d4c78-109">Her zaman tooreset hello kullanarak bir parola deneyin [Azure portalında veya Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ilk.</span><span class="sxs-lookup"><span data-stu-id="d4c78-109">Always try tooreset a password using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) first.</span></span>
> 
> 

## <a name="overview-of-hello-process"></a><span data-ttu-id="d4c78-110">Merhaba işlemine genel bakış</span><span class="sxs-lookup"><span data-stu-id="d4c78-110">Overview of hello process</span></span>
<span data-ttu-id="d4c78-111">erişim toohello Azure Konuk Aracısı olduğunda sıfırlama Azure Windows VM için yerel bir parolası gerçekleştirmek için hello çekirdek adımlar aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="d4c78-111">hello core steps for performing a local password reset for a Windows VM in Azure when there is no access toohello Azure guest agent is as follows:</span></span>

* <span data-ttu-id="d4c78-112">Merhaba kaynak VM silin.</span><span class="sxs-lookup"><span data-stu-id="d4c78-112">Delete hello source VM.</span></span> <span data-ttu-id="d4c78-113">Merhaba sanal diskler korunur.</span><span class="sxs-lookup"><span data-stu-id="d4c78-113">hello virtual disks are retained.</span></span>
* <span data-ttu-id="d4c78-114">Merhaba kaynak sanal makinenin işletim sistemi disk tooanother VM hello ekleme, Azure aboneliğinizin aynı konumdaki.</span><span class="sxs-lookup"><span data-stu-id="d4c78-114">Attach hello source VM's OS disk tooanother VM on hello same location within your Azure subscription.</span></span> <span data-ttu-id="d4c78-115">Bu VM VM sorun giderme başvurulan tooas hello ' dir.</span><span class="sxs-lookup"><span data-stu-id="d4c78-115">This VM is referred tooas hello troubleshooting VM.</span></span>
* <span data-ttu-id="d4c78-116">VM sorun giderme hello kullanarak, bazı yapılandırma dosyalarını hello kaynak sanal makinenin işletim sistemi diski oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d4c78-116">Using hello troubleshooting VM, create some config files on hello source VM's OS disk.</span></span>
* <span data-ttu-id="d4c78-117">VM sorun giderme hello Hello VM'ın işletim sistemi diski kullanımdan çıkarın.</span><span class="sxs-lookup"><span data-stu-id="d4c78-117">Detach hello VM's OS disk from hello troubleshooting VM.</span></span>
* <span data-ttu-id="d4c78-118">Resource Manager şablonu toocreate hello özgün sanal diski kullanarak VM, kullanın.</span><span class="sxs-lookup"><span data-stu-id="d4c78-118">Use a Resource Manager template toocreate a VM, using hello original virtual disk.</span></span>
* <span data-ttu-id="d4c78-119">Merhaba yeni VM önyüklemesinde, Merhaba, yapılandırma dosyaları gerekli hello kullanıcının hello parola güncelleştirme oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d4c78-119">When hello new VM boots, hello config files you create update hello password of hello required user.</span></span>

## <a name="detailed-steps"></a><span data-ttu-id="d4c78-120">Ayrıntılı adımlar</span><span class="sxs-lookup"><span data-stu-id="d4c78-120">Detailed steps</span></span>
<span data-ttu-id="d4c78-121">Her zaman tooreset hello kullanarak bir parola deneyin [Azure portalında veya Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) aşağıdaki adımları hello denemeden önce.</span><span class="sxs-lookup"><span data-stu-id="d4c78-121">Always try tooreset a password using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before trying hello following steps.</span></span> <span data-ttu-id="d4c78-122">Başlamadan önce VM yedeği olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d4c78-122">Make sure you have a backup of your VM before you start.</span></span> 

1. <span data-ttu-id="d4c78-123">Silme hello Azure Portalı'nda VM etkilenen.</span><span class="sxs-lookup"><span data-stu-id="d4c78-123">Delete hello affected VM in Azure portal.</span></span> <span data-ttu-id="d4c78-124">Silme hello VM yalnızca hello meta verileri, hello Azure içinde VM hello başvurusu siler.</span><span class="sxs-lookup"><span data-stu-id="d4c78-124">Deleting hello VM only deletes hello metadata, hello reference of hello VM within Azure.</span></span> <span data-ttu-id="d4c78-125">Merhaba VM silindiğinde hello sanal diskler korunur:</span><span class="sxs-lookup"><span data-stu-id="d4c78-125">hello virtual disks are retained when hello VM is deleted:</span></span>
   
   * <span data-ttu-id="d4c78-126">Select hello VM hello Azure portal'ı tıklatın *silmek*:</span><span class="sxs-lookup"><span data-stu-id="d4c78-126">Select hello VM in hello Azure portal, click *Delete*:</span></span>
     
     ![Var olan VM silme](./media/reset-local-password-without-agent/delete_vm.png)
2. <span data-ttu-id="d4c78-128">VM sorun giderme hello kaynak sanal makinenin işletim sistemi disk toohello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d4c78-128">Attach hello source VM’s OS disk toohello troubleshooting VM.</span></span> <span data-ttu-id="d4c78-129">VM sorun giderme hello hello olmalıdır hello kaynak sanal makinenin işletim sistemi diski ile aynı bölgeye (gibi `West US`):</span><span class="sxs-lookup"><span data-stu-id="d4c78-129">hello troubleshooting VM must be in hello same region as hello source VM's OS disk (such as `West US`):</span></span>
   
   * <span data-ttu-id="d4c78-130">VM hello Azure portal sorunlarını giderme hello seçin.</span><span class="sxs-lookup"><span data-stu-id="d4c78-130">Select hello troubleshooting VM in hello Azure portal.</span></span> <span data-ttu-id="d4c78-131">Tıklatın *diskleri* | *Attach varolan*:</span><span class="sxs-lookup"><span data-stu-id="d4c78-131">Click *Disks* | *Attach existing*:</span></span>
     
     ![Varolan bir diski kullanıma açın](./media/reset-local-password-without-agent/disks_attach_existing.png)
     
     <span data-ttu-id="d4c78-133">Seçin *VHD dosyasını* ve kaynağınız VM içeriyorsa hello depolama hesabı seçin:</span><span class="sxs-lookup"><span data-stu-id="d4c78-133">Select *VHD File* and then select hello storage account that contains your source VM:</span></span>
     
     ![Depolama hesabı seçme](./media/reset-local-password-without-agent/disks_select_storageaccount.PNG)
     
     <span data-ttu-id="d4c78-135">Merhaba kaynak kapsayıcısı seçin.</span><span class="sxs-lookup"><span data-stu-id="d4c78-135">Select hello source container.</span></span> <span data-ttu-id="d4c78-136">Merhaba kaynak kapsayıcıdır genellikle *VHD'ler*:</span><span class="sxs-lookup"><span data-stu-id="d4c78-136">hello source container is typically *vhds*:</span></span>
     
     ![Depolama kapsayıcısı seçin](./media/reset-local-password-without-agent/disks_select_container.png)
     
     <span data-ttu-id="d4c78-138">Merhaba OS vhd tooattach seçin.</span><span class="sxs-lookup"><span data-stu-id="d4c78-138">Select hello OS vhd tooattach.</span></span> <span data-ttu-id="d4c78-139">Tıklatın *seçin* toocomplete hello işlemi:</span><span class="sxs-lookup"><span data-stu-id="d4c78-139">Click *Select* toocomplete hello process:</span></span>
     
     ![Kaynak sanal disk seçin](./media/reset-local-password-without-agent/disks_select_source_vhd.png)
3. <span data-ttu-id="d4c78-141">VM Uzak Masaüstü kullanarak sorun giderme toohello bağlanabilir ve hello kaynak sanal makinenin işletim sistemi diski görünür olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d4c78-141">Connect toohello troubleshooting VM using Remote Desktop and ensure hello source VM's OS disk is visible:</span></span>
   
   * <span data-ttu-id="d4c78-142">VM hello Azure portal sorunlarını giderme hello tıklatıp *Bağlan*.</span><span class="sxs-lookup"><span data-stu-id="d4c78-142">Select hello troubleshooting VM in hello Azure portal and click *Connect*.</span></span>
   * <span data-ttu-id="d4c78-143">Yüklemeleri hello RDP dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="d4c78-143">Open hello RDP file that downloads.</span></span> <span data-ttu-id="d4c78-144">Merhaba kullanıcı VM sorun giderme hello adını ve parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="d4c78-144">Enter hello username and password of hello troubleshooting VM.</span></span>
   * <span data-ttu-id="d4c78-145">Dosya Gezgini'nde, bağlı hello veri diski için bakın.</span><span class="sxs-lookup"><span data-stu-id="d4c78-145">In File Explorer, look for hello data disk you attached.</span></span> <span data-ttu-id="d4c78-146">Merhaba VM'in VHD'nin olduğundan kaynak hello veriler yalnızca bağlı disk toohello VM sorun giderme hello F: sürücü olması:</span><span class="sxs-lookup"><span data-stu-id="d4c78-146">If hello source VM’s VHD is hello only data disk attached toohello troubleshooting VM, it should be hello F: drive:</span></span>
     
     ![Bağlı veri diski görüntüleme](./media/reset-local-password-without-agent/troubleshooting_vm_fileexplorer.png)
4. <span data-ttu-id="d4c78-148">Oluşturma `gpt.ini` içinde `\Windows\System32\GroupPolicy` hello kaynak VM'in sürücüde (toogpt.ini.bak yeniden adlandırın gpt.ini varsa):</span><span class="sxs-lookup"><span data-stu-id="d4c78-148">Create `gpt.ini` in `\Windows\System32\GroupPolicy` on hello source VM’s drive (if gpt.ini exists, rename toogpt.ini.bak):</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="d4c78-149">Yanlışlıkla C:\Windows dosyalarında aşağıdaki hello oluşturmak işletim sistemi sürücüsü hello VM sorun giderme için hello emin olun.</span><span class="sxs-lookup"><span data-stu-id="d4c78-149">Make sure that you do not accidentally create hello following files in C:\Windows, hello OS drive for hello troubleshooting VM.</span></span> <span data-ttu-id="d4c78-150">Aşağıdaki veri diski olarak bağlı olduğu VM kaynağınız için hello işletim sistemi sürücüsündeki dosyaları hello oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d4c78-150">Create hello following files in hello OS drive for your source VM that is attached as a data disk.</span></span>
   > 
   > 
   
   * <span data-ttu-id="d4c78-151">Merhaba satırlardan hello eklemek `gpt.ini` oluşturduğunuz dosyası:</span><span class="sxs-lookup"><span data-stu-id="d4c78-151">Add hello following lines into hello `gpt.ini` file you created:</span></span>
     
     ```
     [General]
     gPCFunctionalityVersion=2
     gPCMachineExtensionNames=[{42B5FAAE-6536-11D2-AE5A-0000F87571E3}{40B6664F-4972-11D1-A7CA-0000F87571E3}]
     Version=1
     ```
     
     ![GPT.ini oluşturma](./media/reset-local-password-without-agent/create_gpt_ini.png)
5. <span data-ttu-id="d4c78-153">Oluşturma `scripts.ini` içinde `\Windows\System32\GroupPolicy\Machine\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="d4c78-153">Create `scripts.ini` in `\Windows\System32\GroupPolicy\Machine\Scripts`.</span></span> <span data-ttu-id="d4c78-154">Gizli klasörlere gösterilen emin olun.</span><span class="sxs-lookup"><span data-stu-id="d4c78-154">Make sure hidden folders are shown.</span></span> <span data-ttu-id="d4c78-155">Gerekirse, hello oluşturma `Machine` veya `Scripts` klasörler.</span><span class="sxs-lookup"><span data-stu-id="d4c78-155">If needed, create hello `Machine` or `Scripts` folders.</span></span>
   
   * <span data-ttu-id="d4c78-156">Aşağıdaki satırları hello hello eklemek `scripts.ini` oluşturduğunuz dosyası:</span><span class="sxs-lookup"><span data-stu-id="d4c78-156">Add hello following lines hello `scripts.ini` file you created:</span></span>
     
     ```
     [Startup]
     0CmdLine=C:\Windows\System32\FixAzureVM.cmd
     0Parameters=
     ```
     
     ![Scripts.ini oluşturma](./media/reset-local-password-without-agent/create_scripts_ini.png)
6. <span data-ttu-id="d4c78-158">Oluşturma `FixAzureVM.cmd` içinde `\Windows\System32` içeriği izleyerek, değiştirme hello ile `<username>` ve `<newpassword>` kendi değerlerinizi ile:</span><span class="sxs-lookup"><span data-stu-id="d4c78-158">Create `FixAzureVM.cmd` in `\Windows\System32` with hello following contents, replacing `<username>` and `<newpassword>` with your own values:</span></span>
   
    ```
    net user <username> <newpassword> /add
    net localgroup administrators <username> /add
    net localgroup "remote desktop users" <username> /add

    ```

    ![FixAzureVM.cmd oluşturma](./media/reset-local-password-without-agent/create_fixazure_cmd.png)
   
    <span data-ttu-id="d4c78-160">Merhaba yeni parola tanımlarken, VM için yapılandırılmış hello parola karmaşıklığı gereksinimlerini karşılamalıdır.</span><span class="sxs-lookup"><span data-stu-id="d4c78-160">You must meet hello configured password complexity requirements for your VM when defining hello new password.</span></span>
7. <span data-ttu-id="d4c78-161">Azure Portalı'nda VM sorun giderme hello hello diski kullanımdan çıkarın:</span><span class="sxs-lookup"><span data-stu-id="d4c78-161">In Azure portal, detach hello disk from hello troubleshooting VM:</span></span>
   
   * <span data-ttu-id="d4c78-162">VM hello Azure portal sorunlarını giderme hello seçin, *diskleri*.</span><span class="sxs-lookup"><span data-stu-id="d4c78-162">Select hello troubleshooting VM in hello Azure portal, click *Disks*.</span></span>
   * <span data-ttu-id="d4c78-163">Select hello veri diski 2. adımda eklenen, tıklatın *ayırma*:</span><span class="sxs-lookup"><span data-stu-id="d4c78-163">Select hello data disk attached in step 2, click *Detach*:</span></span>
     
     ![Disk ayırma](./media/reset-local-password-without-agent/detach_disk.png)
8. <span data-ttu-id="d4c78-165">Bir VM oluşturmadan önce hello URI tooyour kaynak işletim sistemi diski alın:</span><span class="sxs-lookup"><span data-stu-id="d4c78-165">Before you create a VM, obtain hello URI tooyour source OS disk:</span></span>
   
   * <span data-ttu-id="d4c78-166">Select hello depolama hesabında hello Azure portal'ı tıklatın *BLOB'lar*.</span><span class="sxs-lookup"><span data-stu-id="d4c78-166">Select hello storage account in hello Azure portal, click *Blobs*.</span></span>
   * <span data-ttu-id="d4c78-167">Merhaba kapsayıcısı seçin.</span><span class="sxs-lookup"><span data-stu-id="d4c78-167">Select hello container.</span></span> <span data-ttu-id="d4c78-168">Merhaba kaynak kapsayıcıdır genellikle *VHD'ler*:</span><span class="sxs-lookup"><span data-stu-id="d4c78-168">hello source container is typically *vhds*:</span></span>
     
     ![Depolama hesabı blob seçin](./media/reset-local-password-without-agent/select_storage_details.png)
     
     <span data-ttu-id="d4c78-170">Kaynağınız VM OS VHD seçin ve hello tıklatın *kopya* düğmesine bir sonraki toohello *URL* adı:</span><span class="sxs-lookup"><span data-stu-id="d4c78-170">Select your source VM OS VHD and click hello *Copy* button next toohello *URL* name:</span></span>
     
     ![Kopya disk URI](./media/reset-local-password-without-agent/copy_source_vhd_uri.png)
9. <span data-ttu-id="d4c78-172">Bir VM hello kaynak sanal makinenin işletim sistemi diski oluşturun:</span><span class="sxs-lookup"><span data-stu-id="d4c78-172">Create a VM from hello source VM’s OS disk:</span></span>
   
   * <span data-ttu-id="d4c78-173">Kullanım [bu Azure Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate özel bir VHD VM'den.</span><span class="sxs-lookup"><span data-stu-id="d4c78-173">Use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate a VM from a specialized VHD.</span></span> <span data-ttu-id="d4c78-174">Merhaba tıklatın `Deploy tooAzure` düğmesini tooopen hello Azure portalıyla hello şablonlu ayrıntılarını sizin için doldurulur.</span><span class="sxs-lookup"><span data-stu-id="d4c78-174">Click hello `Deploy tooAzure` button tooopen hello Azure portal with hello templated details populated for you.</span></span>
   * <span data-ttu-id="d4c78-175">Merhaba VM için tüm hello önceki ayarlarını tooretain istiyorsanız seçin *Düzen şablonu* tooprovide var olan sanal ağ, alt ağ, ağ bağdaştırıcısı veya genel IP.</span><span class="sxs-lookup"><span data-stu-id="d4c78-175">If you want tooretain all hello previous settings for hello VM, select *Edit template* tooprovide your existing VNet, subnet, network adapter, or public IP.</span></span>
   * <span data-ttu-id="d4c78-176">Merhaba, `OSDISKVHDURI` parametresi metin kutusu, VHD Kaynak URI elde adım önceki hello Yapıştır hello:</span><span class="sxs-lookup"><span data-stu-id="d4c78-176">In hello `OSDISKVHDURI` parameter text box, paste hello URI of your source VHD obtain in hello preceding step:</span></span>
     
     ![Bir VM şablonu oluşturma](./media/reset-local-password-without-agent/create_new_vm_from_template.png)
10. <span data-ttu-id="d4c78-178">Yeni VM çalıştıran hello sonra toohello VM hello yeni parolayla hello belirttiğiniz Uzak Masaüstü kullanarak bağlanmak `FixAzureVM.cmd` komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="d4c78-178">After hello new VM is running, connect toohello VM using Remote Desktop with hello new password you specified in hello `FixAzureVM.cmd` script.</span></span>
11. <span data-ttu-id="d4c78-179">Uzak oturum toohello yeni VM, aşağıdaki Kaldır hello hello çevresi tooclean dosyalar:</span><span class="sxs-lookup"><span data-stu-id="d4c78-179">From your remote session toohello new VM, remove hello following files tooclean up hello environment:</span></span>
    
    * <span data-ttu-id="d4c78-180">%Windir%\System32</span><span class="sxs-lookup"><span data-stu-id="d4c78-180">From %windir%\System32</span></span>
      * <span data-ttu-id="d4c78-181">FixAzureVM.cmd Kaldır</span><span class="sxs-lookup"><span data-stu-id="d4c78-181">remove FixAzureVM.cmd</span></span>
    * <span data-ttu-id="d4c78-182">%Windir%\System32\GroupPolicy\Machine\\</span><span class="sxs-lookup"><span data-stu-id="d4c78-182">From %windir%\System32\GroupPolicy\Machine\\</span></span>
      * <span data-ttu-id="d4c78-183">scripts.ini Kaldır</span><span class="sxs-lookup"><span data-stu-id="d4c78-183">remove scripts.ini</span></span>
    * <span data-ttu-id="d4c78-184">%Windir%\System32\GroupPolicy</span><span class="sxs-lookup"><span data-stu-id="d4c78-184">From %windir%\System32\GroupPolicy</span></span>
      * <span data-ttu-id="d4c78-185">(önce gpt.ini var ve toogpt.ini.bak, yeniden adlandırma hello .bak dosya geri toogpt.ini yeniden adlandırılmış varsa) GPT.ini Kaldır</span><span class="sxs-lookup"><span data-stu-id="d4c78-185">remove gpt.ini (if gpt.ini existed before, and you renamed it toogpt.ini.bak, rename hello .bak file back toogpt.ini)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4c78-186">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d4c78-186">Next steps</span></span>
<span data-ttu-id="d4c78-187">Uzak Masaüstü kullanarak hala bağlanamazsa, hello bkz [RDP sorun giderme kılavuzu](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d4c78-187">If you still cannot connect using Remote Desktop, see hello [RDP troubleshooting guide](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="d4c78-188">Merhaba [sorun giderme kılavuzu RDP ayrıntılı](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) belirli adımları yerine yöntemleri sorun giderme sırasında arar.</span><span class="sxs-lookup"><span data-stu-id="d4c78-188">hello [detailed RDP troubleshooting guide](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) looks at troubleshooting methods rather than specific steps.</span></span> <span data-ttu-id="d4c78-189">Ayrıca [Azure destek isteği açma](https://azure.microsoft.com/support/options/) uygulamalı Yardım için.</span><span class="sxs-lookup"><span data-stu-id="d4c78-189">You can also [open an Azure support request](https://azure.microsoft.com/support/options/) for hands-on assistance.</span></span>

