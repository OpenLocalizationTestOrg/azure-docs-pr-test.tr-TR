---
title: ilk Windows VM'nizi IIS'de aaaInstall | Microsoft Docs
description: "Denemeler ile ilk Windows sanal makine IIS yükleyerek ve 80 numaralı bağlantı noktasını kullanarak açma hello Azure portalı."
keywords: 
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6334ea45-db6b-4e08-abb5-1f98927ebc34
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: cynthn
ms.openlocfilehash: 7cfed6197df058c4569d111ee88961da7c6fe0b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="experiment-with-installing-a-role-on-your-windows-vm"></a><span data-ttu-id="c8dad-103">Windows VM üzerinde bir rolü yüklemeye denemeler</span><span class="sxs-lookup"><span data-stu-id="c8dad-103">Experiment with installing a role on your Windows VM</span></span>
<span data-ttu-id="c8dad-104">İlk sanal makine (VM) ve çalışan olduktan sonra tooinstalling yazılım ve hizmetlerinin taşıyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8dad-104">Once you have your first virtual machine (VM) up and running, you can move on tooinstalling software and services.</span></span> <span data-ttu-id="c8dad-105">Bu öğreticide, biz toouse Sunucu Yöneticisi'ni hello Windows Server VM tooinstall IIS üzerinde adımıdır.</span><span class="sxs-lookup"><span data-stu-id="c8dad-105">For this tutorial, we are going toouse Server Manager on hello Windows Server VM tooinstall IIS.</span></span> <span data-ttu-id="c8dad-106">Ardından, hello Azure portal tooopen bağlantı noktası 80 tooIIS trafiği kullanarak ağ güvenlik grubu (NSG) oluşturacağız.</span><span class="sxs-lookup"><span data-stu-id="c8dad-106">Then, we will create a Network Security Group (NSG) using hello Azure portal tooopen port 80 tooIIS traffic.</span></span> 

<span data-ttu-id="c8dad-107">İlk VM oluşturmadıysanız, size geri çok tamamlamalıdır[hello Azure portalında, ilk Windows sanal makine oluşturma](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Bu öğretici ile devam etmeden önce.</span><span class="sxs-lookup"><span data-stu-id="c8dad-107">If you haven't already created your first VM, you should go back too[Create your first Windows virtual machine in hello Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before continuing with this tutorial.</span></span>

## <a name="make-sure-hello-vm-is-running"></a><span data-ttu-id="c8dad-108">VM'nin çalıştığından emin hello olun</span><span class="sxs-lookup"><span data-stu-id="c8dad-108">Make sure hello VM is running</span></span>
1. <span data-ttu-id="c8dad-109">Açık hello [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c8dad-109">Open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c8dad-110">Merhaba hub menüsünde **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="c8dad-110">On hello hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="c8dad-111">Merhaba sanal makine hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="c8dad-111">Select hello virtual machine from hello list.</span></span>
3. <span data-ttu-id="c8dad-112">Merhaba durumundaysa **durduruldu (Deallocated)**, hello tıklatın **Başlat** hello düğmesinde **Essentials** hello VM dikey.</span><span class="sxs-lookup"><span data-stu-id="c8dad-112">If hello status is **Stopped (Deallocated)**, click hello **Start** button on hello **Essentials** blade of hello VM.</span></span> <span data-ttu-id="c8dad-113">Merhaba durumundaysa **çalıştıran**, üzerinde toohello sonraki adıma geçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8dad-113">If hello status is **Running**, you can move on toohello next step.</span></span>

## <a name="connect-toohello-virtual-machine-and-sign-in"></a><span data-ttu-id="c8dad-114">Toohello sanal makineye bağlanın ve oturum açın</span><span class="sxs-lookup"><span data-stu-id="c8dad-114">Connect toohello virtual machine and sign in</span></span>
1. <span data-ttu-id="c8dad-115">Merhaba hub menüsünde **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="c8dad-115">On hello hub menu, click **Virtual Machines**.</span></span> <span data-ttu-id="c8dad-116">Merhaba sanal makine hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="c8dad-116">Select hello virtual machine from hello list.</span></span>
2. <span data-ttu-id="c8dad-117">Merhaba sanal makine için Hello dikey penceresinde **Bağlan**.</span><span class="sxs-lookup"><span data-stu-id="c8dad-117">On hello blade for hello virtual machine, click **Connect**.</span></span> <span data-ttu-id="c8dad-118">Bu oluşturur ve bir kısayol tooconnect tooyour makine gibi bir Uzak Masaüstü Protokolü dosyasını (.rdp dosyası) indirir.</span><span class="sxs-lookup"><span data-stu-id="c8dad-118">This creates and downloads a Remote Desktop Protocol file (.rdp file) that is like a shortcut tooconnect tooyour machine.</span></span> <span data-ttu-id="c8dad-119">Kolay erişim için toosave hello dosya tooyour Masaüstü isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8dad-119">You might want toosave hello file tooyour desktop for easy access.</span></span> <span data-ttu-id="c8dad-120">**Açık** bu dosya tooconnect tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="c8dad-120">**Open** this file tooconnect tooyour VM.</span></span>
   
    ![Hello Azure portal gösteren ekran görüntüsü nasıl tooconnect tooyour VM](./media/hero-role/connect.png)
3. <span data-ttu-id="c8dad-122">Bir uyarı almak bu hello .rdp bilinmeyen bir yayımcıdan değil.</span><span class="sxs-lookup"><span data-stu-id="c8dad-122">You get a warning that hello .rdp is from an unknown publisher.</span></span> <span data-ttu-id="c8dad-123">Bu normaldir.</span><span class="sxs-lookup"><span data-stu-id="c8dad-123">This is normal.</span></span> <span data-ttu-id="c8dad-124">Merhaba Uzak Masaüstü penceresinde **Bağlan** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="c8dad-124">In hello Remote Desktop window, click **Connect** toocontinue.</span></span>
   
    ![Bilinmeyen yayımcıya ilişkin uyarı ekran görüntüsü](./media/hero-role/rdp-warn.png)
4. <span data-ttu-id="c8dad-126">Merhaba Windows Güvenlik penceresinde türü hello kullanıcı adı ve parola oluşturduğunuz sırada oluşturduğunuz hello yerel hesap için VM hello.</span><span class="sxs-lookup"><span data-stu-id="c8dad-126">In hello Windows Security window, type hello username and password for hello local account that you created when you created hello VM.</span></span> <span data-ttu-id="c8dad-127">Merhaba kullanıcı adı olarak girilir *vmname*&#92; *Kullanıcı adı*, ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="c8dad-127">hello username is entered as *vmname*&#92;*username*, then click **OK**.</span></span>
   
    ![Merhaba VM adı, kullanıcı adı ve parola girme ekran görüntüsü](./media/hero-role/credentials.png)
5. <span data-ttu-id="c8dad-129">Bir uyarı almak bu hello sertifika doğrulanamıyor.</span><span class="sxs-lookup"><span data-stu-id="c8dad-129">You get a warning that hello certificate cannot be verified.</span></span> <span data-ttu-id="c8dad-130">Bu normaldir.</span><span class="sxs-lookup"><span data-stu-id="c8dad-130">This is normal.</span></span> <span data-ttu-id="c8dad-131">Tıklatın **Evet** tooverify hello hello sanal makine kimliğini ve oturum açmayı tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="c8dad-131">Click **Yes** tooverify hello identity of hello virtual machine and finish logging on.</span></span>
   
   ![Bir ileti gösteren ekran görüntüsü hello hello VM kimliğini doğrulamaya ilişkin](./media/hero-role/cert-warning.png)

<span data-ttu-id="c8dad-133">Tooconnect çalıştığınızda tootrouble içinde çalıştırırsanız, bkz: [sorun giderme Uzak Masaüstü bağlantıları tooa Windows tabanlı Azure sanal makine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c8dad-133">If you run in tootrouble when you try tooconnect, see [Troubleshoot Remote Desktop connections tooa Windows-based Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="install-iis-on-your-vm"></a><span data-ttu-id="c8dad-134">Sanal makinenize IIS yükleme</span><span class="sxs-lookup"><span data-stu-id="c8dad-134">Install IIS on your VM</span></span>
<span data-ttu-id="c8dad-135">Toohello VM kaydedilir, böylece daha deneyebilirsiniz biz sunucu rolünü yükler.</span><span class="sxs-lookup"><span data-stu-id="c8dad-135">Now that you are logged in toohello VM, we will install a server role so that you can experiment more.</span></span>

1. <span data-ttu-id="c8dad-136">Henüz açık değilse **Sunucu Yöneticisi**’ni açın.</span><span class="sxs-lookup"><span data-stu-id="c8dad-136">Open **Server Manager** if it isn't already open.</span></span> <span data-ttu-id="c8dad-137">Merhaba tıklatın **Başlat** menüsüne ve ardından **Sunucu Yöneticisi'ni**.</span><span class="sxs-lookup"><span data-stu-id="c8dad-137">Click hello **Start** menu, and then click **Server Manager**.</span></span>
2. <span data-ttu-id="c8dad-138">İçinde **Sunucu Yöneticisi'ni**seçin **yerel sunucu** hello sol bölmesinden.</span><span class="sxs-lookup"><span data-stu-id="c8dad-138">In **Server Manager**, select **Local Server** from hello left pane.</span></span> 
3. <span data-ttu-id="c8dad-139">Merhaba menüde seçin **Yönet** > **rol ve Özellik Ekle**.</span><span class="sxs-lookup"><span data-stu-id="c8dad-139">In hello menu, select **Manage** > **Add Roles and Features**.</span></span>
4. <span data-ttu-id="c8dad-140">Merhaba eklemek rol ve özellik Sihirbazı'nda hello **yükleme türü** sayfasında, **rol tabanlı veya özellik tabanlı yükleme**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="c8dad-140">In hello Add Roles and Features Wizard, on hello **Installation Type** page, choose **Role-based or feature-based installation**, and then click **Next**.</span></span>
   
    ![Ekran gösteren hello Ekle roller ve Özellikler Sihirbazı sekmesinde yükleme türü](./media/hero-role/role-wizard.png)
5. <span data-ttu-id="c8dad-142">Merhaba sunucu havuzundan Hello VM seçin ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="c8dad-142">Select hello VM from hello server pool and click **Next**.</span></span>
6. <span data-ttu-id="c8dad-143">Merhaba üzerinde **sunucu rolleri** sayfasında, **Web sunucusu (IIS)**.</span><span class="sxs-lookup"><span data-stu-id="c8dad-143">On hello **Server Roles** page, select **Web Server (IIS)**.</span></span>
   
    ![Ekran gösteren hello Ekle roller ve Özellikler Sihirbazı sekmesini sunucu rolleri için](./media/hero-role/add-iis.png)
7. <span data-ttu-id="c8dad-145">ISS'nin ihtiyaç duyduğu özellikleri ekleme hakkında açılır Hello içinde olduğundan emin olun **yönetim araçlarını dahil** seçilir ve ardından **Özellik Ekle**.</span><span class="sxs-lookup"><span data-stu-id="c8dad-145">In hello pop-up about adding features needed for IIS, make sure that **Include management tools** is selected and then click **Add Features**.</span></span> <span data-ttu-id="c8dad-146">Merhaba açılır kapandığında tıklatın **sonraki** hello Sihirbazı'nda.</span><span class="sxs-lookup"><span data-stu-id="c8dad-146">When hello pop-up closes, click **Next** in hello wizard.</span></span>
   
    ![Merhaba IIS rolü ekleme açılır tooconfirm gösteren ekran görüntüsü](./media/hero-role/confirm-add-feature.png)
8. <span data-ttu-id="c8dad-148">Merhaba özellikleri sayfasında, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="c8dad-148">On hello features page, click **Next**.</span></span>
9. <span data-ttu-id="c8dad-149">Merhaba üzerinde **Web sunucusu rolü (IIS)** sayfasında, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="c8dad-149">On hello **Web Server Role (IIS)** page, click **Next**.</span></span> 
10. <span data-ttu-id="c8dad-150">Merhaba üzerinde **rol hizmetlerini** sayfasında, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="c8dad-150">On hello **Role Services** page, click **Next**.</span></span> 
11. <span data-ttu-id="c8dad-151">Merhaba üzerinde **onay** sayfasında, **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="c8dad-151">On hello **Confirmation** page, click **Install**.</span></span> 
12. <span data-ttu-id="c8dad-152">Merhaba yüklemesi tamamlandıktan sonra tıklatın **Kapat** hello Sihirbazı.</span><span class="sxs-lookup"><span data-stu-id="c8dad-152">When hello installation is complete, click **Close** on hello wizard.</span></span>

## <a name="open-port-80"></a><span data-ttu-id="c8dad-153">Bağlantı noktası 80'i açın</span><span class="sxs-lookup"><span data-stu-id="c8dad-153">Open port 80</span></span>
<span data-ttu-id="c8dad-154">Bağlantı noktası 80 üzerinden gelen trafik, VM tooaccept sırada, tooadd bir gelen kuralı toohello ağ güvenlik grubu gerekir.</span><span class="sxs-lookup"><span data-stu-id="c8dad-154">In order for your VM tooaccept inbound traffic over port 80, you need tooadd an inbound rule toohello network security group.</span></span> 

1. <span data-ttu-id="c8dad-155">Açık hello [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c8dad-155">Open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c8dad-156">İçinde **sanal makineleri** hello oluşturduğunuz VM seçin.</span><span class="sxs-lookup"><span data-stu-id="c8dad-156">In **Virtual machines** select hello VM that you created.</span></span>
3. <span data-ttu-id="c8dad-157">Merhaba sanal makine ayarlarında seçin **ağ arabirimleri** ve ardından var olan ağ arabirimi seçin hello.</span><span class="sxs-lookup"><span data-stu-id="c8dad-157">In hello virtual machines settings, select **Network interfaces** and then select hello existing network interface.</span></span>
   
    ![Ağ arabirimleri hello Hello sanal makine ayarı gösteren ekran görüntüsü](./media/hero-role/network-interface.png)
4. <span data-ttu-id="c8dad-159">İçinde **Essentials** hello hello ağ arabirimi için tıklatın **ağ güvenlik grubu**.</span><span class="sxs-lookup"><span data-stu-id="c8dad-159">In **Essentials** for hello network interface, click hello **Network security group**.</span></span>
   
    ![Merhaba temel parçalar bölümünde hello ağ arabirimi için gösteren ekran görüntüsü](./media/hero-role/select-nsg.png)
5. <span data-ttu-id="c8dad-161">Merhaba, **Essentials** dikey penceresinde hello NSG için gelen kuralı için bir var olan varsayılan olmalıdır **varsayılan izin rdp** olanak sağlayan toolog toohello VM.</span><span class="sxs-lookup"><span data-stu-id="c8dad-161">In hello **Essentials** blade for hello NSG, you should have one existing default inbound rule for **default-allow-rdp** which allows you toolog in toohello VM.</span></span> <span data-ttu-id="c8dad-162">Başka bir gelen kuralı tooallow IIS trafiği ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="c8dad-162">You will add another inbound rule tooallow IIS traffic.</span></span> <span data-ttu-id="c8dad-163">**Gelen güvenlik kuralı**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c8dad-163">Click **Inbound security rule**.</span></span>
   
    ![Merhaba temel parçalar bölümünde hello NSG için gösteren ekran görüntüsü](./media/hero-role/inbound.png)
6. <span data-ttu-id="c8dad-165">**Gelen güvenlik kuralları** bölümünde **Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c8dad-165">In **Inbound security rules**, click **Add**.</span></span>
   
    ![Güvenlik kuralı Hello düğmesi tooadd gösteren ekran görüntüsü](./media/hero-role/add-rule.png)
7. <span data-ttu-id="c8dad-167">**Gelen güvenlik kuralları** bölümünde **Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c8dad-167">In **Inbound security rules**, click **Add**.</span></span> <span data-ttu-id="c8dad-168">Tür **80** hello bağlantı noktası aralığı ve emin olun **izin** seçilir.</span><span class="sxs-lookup"><span data-stu-id="c8dad-168">Type **80** in hello port range and make sure **Allow** is selected.</span></span> <span data-ttu-id="c8dad-169">İşiniz bittiğinde **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c8dad-169">When you are done, click **OK**.</span></span>
   
    ![Güvenlik kuralı Hello düğmesi tooadd gösteren ekran görüntüsü](./media/hero-role/port-80.png)

<span data-ttu-id="c8dad-171">Nsg'ler, gelen ve giden kuralları hakkında daha fazla bilgi için bkz: [izin dış erişim tooyour VM kullanarak hello Azure portalı](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="c8dad-171">For more information about NSGs, inbound and outbound rules, see [Allow external access tooyour VM using hello Azure portal](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="connect-toohello-default-iis-website"></a><span data-ttu-id="c8dad-172">Toohello varsayılan IIS Web sitesini Bağlan</span><span class="sxs-lookup"><span data-stu-id="c8dad-172">Connect toohello default IIS website</span></span>
1. <span data-ttu-id="c8dad-173">Hello Azure portal'ı tıklatın **sanal makineleri** ve VM'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="c8dad-173">In hello Azure portal, click **Virtual machines** and then select your VM.</span></span>
2. <span data-ttu-id="c8dad-174">Merhaba, **Essentials** dikey penceresinde, kopyalama, **genel IP adresi**.</span><span class="sxs-lookup"><span data-stu-id="c8dad-174">In hello **Essentials** blade, copy your **Public IP address**.</span></span>
   
    ![Burada toofind hello VM genel IP adresini gösteren ekran görüntüsü](./media/hero-role/ipaddress.png)
3. <span data-ttu-id="c8dad-176">Bir tarayıcı açın ve bu gibi ortak IP adresi hello adres çubuğunda yazın: http://<publicIPaddress> tıklatıp **Enter** toogo toothat adresi.</span><span class="sxs-lookup"><span data-stu-id="c8dad-176">Open a browser and in hello address bar, type in your public IP address like this: http://<publicIPaddress> and click **Enter** toogo toothat address.</span></span>
4. <span data-ttu-id="c8dad-177">Tarayıcınız hello varsayılan IIS web sayfası açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c8dad-177">Your browser should open hello default IIS web page.</span></span> <span data-ttu-id="c8dad-178">Şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="c8dad-178">It looks something like this:</span></span>
   
    ![Bir tarayıcıda hangi hello varsayılan IIS sayfasını gösteren ekran görüntüsü gibi görünüyor](./media/hero-role/iis-default.png)

## <a name="next-steps"></a><span data-ttu-id="c8dad-180">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c8dad-180">Next steps</span></span>
* <span data-ttu-id="c8dad-181">De deneyimleyebilirsiniz [bir veri diski eklemeyi](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooyour sanal makine.</span><span class="sxs-lookup"><span data-stu-id="c8dad-181">You can also experiment with [attaching a data disk](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooyour virtual machine.</span></span> <span data-ttu-id="c8dad-182">Veri diskleri sanal makineniz için daha fazla depolama alanı sağlar.</span><span class="sxs-lookup"><span data-stu-id="c8dad-182">Data disks provide more storage for your virtual machine.</span></span>

