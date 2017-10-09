---
title: aaaBackup Azure Windows VM | Microsoft Docs
description: "Windows Vm'lerinizi Azure Yedekleme kullanılarak yedekleyerek koruyun."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 1cd3e1940a83aacd160cba3c8613b63b6f3c11d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-virtual-machines-in-azure"></a><span data-ttu-id="1051b-103">Azure'da Windows sanal makineleri yedekleyin</span><span class="sxs-lookup"><span data-stu-id="1051b-103">Back up Windows virtual machines in Azure</span></span>

<span data-ttu-id="1051b-104">Düzenli aralıklarla yedekleme yaparak verilerinizi koruyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1051b-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="1051b-105">Azure yedekleme coğrafi olarak yedekli kurtarma kasalarında depolanan kurtarma noktaları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1051b-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="1051b-106">Bir kurtarma noktasından geri yüklediğinizde, geri yükleyebilirsiniz tüm VM ya da yalnızca belirli dosyaları hello.</span><span class="sxs-lookup"><span data-stu-id="1051b-106">When you restore from a recovery point, you can restore hello whole VM or just specific files.</span></span> <span data-ttu-id="1051b-107">Bu makalede, nasıl toorestore tek bir dosya tooa VM açıklanmaktadır Windows Server ve IIS çalıştırıyor.</span><span class="sxs-lookup"><span data-stu-id="1051b-107">This article explains how toorestore a single file tooa VM running Windows Server and IIS.</span></span> <span data-ttu-id="1051b-108">VM toouse zaten sahip değilseniz, birini oluşturabilirsiniz hello kullanarak [Windows Hızlı Başlangıç](quick-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1051b-108">If you don't already have a VM toouse, you can create one using hello [Windows quickstart](quick-create-portal.md).</span></span> <span data-ttu-id="1051b-109">Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1051b-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1051b-110">VM bir yedeğini oluşturun</span><span class="sxs-lookup"><span data-stu-id="1051b-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="1051b-111">Günlük yedekleme zamanlaması</span><span class="sxs-lookup"><span data-stu-id="1051b-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="1051b-112">Bir dosyayı bir yedekten geri yükleyin</span><span class="sxs-lookup"><span data-stu-id="1051b-112">Restore a file from a backup</span></span>




## <a name="backup-overview"></a><span data-ttu-id="1051b-113">Backup’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="1051b-113">Backup overview</span></span>

<span data-ttu-id="1051b-114">Hello Azure Backup hizmeti yedekleme işini başlattığında hello yedekleme uzantısını tootake zaman içinde nokta anlık görüntü tetikler.</span><span class="sxs-lookup"><span data-stu-id="1051b-114">When hello Azure Backup service initiates a backup job, it triggers hello backup extension tootake a point-in-time snapshot.</span></span> <span data-ttu-id="1051b-115">Hello Azure Backup hizmeti kullanan hello _VMSnapshot_ uzantısı.</span><span class="sxs-lookup"><span data-stu-id="1051b-115">hello Azure Backup service uses hello _VMSnapshot_ extension.</span></span> <span data-ttu-id="1051b-116">Merhaba VM çalışıyorsa hello uzantısı hello ilk VM yedekleme sırasında yüklenir.</span><span class="sxs-lookup"><span data-stu-id="1051b-116">hello extension is installed during hello first VM backup if hello VM is running.</span></span> <span data-ttu-id="1051b-117">Merhaba VM çalışır durumda değilse, hello Backup hizmeti bir anlık görüntüsünü hello bu yana (hiçbir uygulama yazma VM durduruldu hello sırasında gerçekleşir) depolama temel alır.</span><span class="sxs-lookup"><span data-stu-id="1051b-117">If hello VM is not running, hello Backup service takes a snapshot of hello underlying storage (since no application writes occur while hello VM is stopped).</span></span>

<span data-ttu-id="1051b-118">Windows VM görüntüsünü alırken, hello Backup hizmeti ile Merhaba Birim Gölge Kopyası Hizmeti (VSS) tooget tutarlı bir anlık görüntü hello sanal makinenin disklerinin düzenler.</span><span class="sxs-lookup"><span data-stu-id="1051b-118">When taking a snapshot of Windows VMs, hello Backup service coordinates with hello Volume Shadow Copy Service (VSS) tooget a consistent snapshot of hello virtual machine's disks.</span></span> <span data-ttu-id="1051b-119">Hello Azure Backup hizmeti hello anlık görüntüsünü alır sonra hello aktarılan toohello kasası verilerdir.</span><span class="sxs-lookup"><span data-stu-id="1051b-119">Once hello Azure Backup service takes hello snapshot, hello data is transferred toohello vault.</span></span> <span data-ttu-id="1051b-120">toomaximize verimliliği hello hizmeti tanımlar ve yalnızca hello hello önceki yedeklemeden bu yana değişmiş olan veri bloklarını aktarır.</span><span class="sxs-lookup"><span data-stu-id="1051b-120">toomaximize efficiency, hello service identifies and transfers only hello blocks of data that have changed since hello previous backup.</span></span>

<span data-ttu-id="1051b-121">Merhaba veri aktarımı tamamlandığında hello anlık görüntü kaldırılır ve bir kurtarma noktası oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1051b-121">When hello data transfer is complete, hello snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="1051b-122">Bir yedekleme oluşturun</span><span class="sxs-lookup"><span data-stu-id="1051b-122">Create a backup</span></span>
<span data-ttu-id="1051b-123">Bir basit zamanlanmış günlük yedekleme tooa kurtarma Hizmetleri kasası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1051b-123">Create a simple scheduled daily backup tooa Recovery Services Vault.</span></span> 

1. <span data-ttu-id="1051b-124">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1051b-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1051b-125">Merhaba soldaki Hello menüde seçin **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="1051b-125">In hello menu on hello left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="1051b-126">Merhaba listeden VM tooback seçin.</span><span class="sxs-lookup"><span data-stu-id="1051b-126">From hello list, select a VM tooback up.</span></span>
4. <span data-ttu-id="1051b-127">Merhaba, hello VM dikey **ayarları** 'yi tıklatın **yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="1051b-127">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="1051b-128">Merhaba **yedeklemeyi etkinleştir** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="1051b-128">hello **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="1051b-129">İçinde **kurtarma Hizmetleri kasası**, tıklatın **Yeni Oluştur** hello ad hello yeni kasa belirtin.</span><span class="sxs-lookup"><span data-stu-id="1051b-129">In **Recovery Services vault**, click **Create new** and provide hello name for hello new vault.</span></span> <span data-ttu-id="1051b-130">Yeni bir kasa aynı hello oluşturulan kaynak grubunu ve konumu hello sanal makine olarak.</span><span class="sxs-lookup"><span data-stu-id="1051b-130">A new vault is created in hello same Resource Group and location as hello virtual machine.</span></span>
6. <span data-ttu-id="1051b-131">Tıklatın **yedekleme İlkesi**.</span><span class="sxs-lookup"><span data-stu-id="1051b-131">Click **Backup policy**.</span></span> <span data-ttu-id="1051b-132">Bu örneğin hello Varsayılanları tutun ve **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="1051b-132">For this example, keep hello defaults and click **OK**.</span></span>
7. <span data-ttu-id="1051b-133">Merhaba üzerinde **yedeklemeyi etkinleştir** dikey penceresinde tıklatın **yedeklemeyi etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="1051b-133">On hello **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="1051b-134">Merhaba varsayılan zamanlamaya göre günlük yedekleme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1051b-134">This creates a daily backup based on hello default schedule.</span></span>
10. <span data-ttu-id="1051b-135">toocreate bir ilk kurtarma noktasında hello **yedekleme** dikey penceresinde **Şimdi Yedekle**.</span><span class="sxs-lookup"><span data-stu-id="1051b-135">toocreate an initial recovery point, on hello **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="1051b-136">Merhaba üzerinde **Şimdi Yedekle** dikey penceresinde hello takvim simgesini tıklatın, hello Takvim denetimi tooselect hello bu kurtarma noktası korunur ve tıklatın son günü kullanmak **yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="1051b-136">On hello **Backup Now** blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="1051b-137">Merhaba, **yedekleme** dikey penceresinde, VM için tam kurtarma noktalarının sayısı hello görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="1051b-137">In hello **Backup** blade for your VM, you will see hello number of recovery points that are complete.</span></span>

    ![Kurtarma noktaları](./media/tutorial-backup-vms/backup-complete.png)
    
<span data-ttu-id="1051b-139">Merhaba ilk yedek yaklaşık 20 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="1051b-139">hello first backup takes about 20 minutes.</span></span> <span data-ttu-id="1051b-140">Yedekleme tamamlandıktan sonra bu öğreticinin sonraki bölümü toohello devam edin.</span><span class="sxs-lookup"><span data-stu-id="1051b-140">Proceed toohello next part of this tutorial after your backup is finished.</span></span>

## <a name="recover-a-file"></a><span data-ttu-id="1051b-141">Bir dosya kurtarma</span><span class="sxs-lookup"><span data-stu-id="1051b-141">Recover a file</span></span>

<span data-ttu-id="1051b-142">Yanlışlıkla silme veya değişiklikleri tooa dosyasını, dosya kurtarma toorecover hello dosyasını yedekleme Kasası'nı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1051b-142">If you accidentally delete or make changes tooa file, you can use File Recovery toorecover hello file from your backup vault.</span></span> <span data-ttu-id="1051b-143">Dosya Kurtarma kullanan VM hello üzerinde çalışan bir komut yerel sürücü olarak toomount hello kurtarma noktası.</span><span class="sxs-lookup"><span data-stu-id="1051b-143">File Recovery uses a script that runs on hello VM, toomount hello recovery point as local drive.</span></span> <span data-ttu-id="1051b-144">Merhaba kurtarma noktasından dosya kopyalayabilir ve toohello VM geri için bu sürücüler için 12 saat bağlı kalır.</span><span class="sxs-lookup"><span data-stu-id="1051b-144">These drives will remain mounted for 12 hours so that you can copy files from hello recovery point and restore them toohello VM.</span></span>  

<span data-ttu-id="1051b-145">Bu örnekte, nasıl toorecover hello hello varsayılan web sayfasında IIS için kullanılan görüntü dosyası gösterir.</span><span class="sxs-lookup"><span data-stu-id="1051b-145">In this example, we show how toorecover hello image file that is used in hello default web page for IIS.</span></span> 

1. <span data-ttu-id="1051b-146">Bir tarayıcı açın ve hello VM tooshow hello varsayılan IIS sayfası toohello IP adresine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="1051b-146">Open a browser and connect toohello IP address of hello VM tooshow hello default IIS page.</span></span>

    ![Varsayılan IIS web sayfası](./media/tutorial-backup-vms/iis-working.png)

2. <span data-ttu-id="1051b-148">Toohello VM bağlayın.</span><span class="sxs-lookup"><span data-stu-id="1051b-148">Connect toohello VM.</span></span>
3. <span data-ttu-id="1051b-149">Hello VM, açık **dosya Gezgini** too\inetpub\wwwroot gidin ve hello dosya silme **iisstart.png**.</span><span class="sxs-lookup"><span data-stu-id="1051b-149">On hello VM, open **File Explorer** and navigate too\inetpub\wwwroot and delete hello file **iisstart.png**.</span></span>
4. <span data-ttu-id="1051b-150">Yerel bilgisayarınızda hello varsayılan IIS sayfasında görüntü hello yenileme hello tarayıcı toosee kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="1051b-150">On your local computer, refresh hello browser toosee that hello image on hello default IIS page is gone.</span></span>

    ![Varsayılan IIS web sayfası](./media/tutorial-backup-vms/iis-broken.png)

5. <span data-ttu-id="1051b-152">Yerel bilgisayarınızda bir yeni sekmesine gidin hello hello açın ve [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1051b-152">On your local computer, open a new tab and go hello hello [Azure portal](https://portal.azure.com).</span></span>
6. <span data-ttu-id="1051b-153">Merhaba soldaki Hello menüde seçin **sanal makineleri** ve select hello VM form hello listesi.</span><span class="sxs-lookup"><span data-stu-id="1051b-153">In hello menu on hello left, select **Virtual machines** and select hello VM form hello list.</span></span>
8. <span data-ttu-id="1051b-154">Merhaba, hello VM dikey **ayarları** 'yi tıklatın **yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="1051b-154">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="1051b-155">Merhaba **yedekleme** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="1051b-155">hello **Backup** blade opens.</span></span> 
9. <span data-ttu-id="1051b-156">Merhaba dikey penceresinde hello üstündeki Hello menüde seçin **dosya kurtarma**.</span><span class="sxs-lookup"><span data-stu-id="1051b-156">In hello menu at hello top of hello blade, select **File Recovery**.</span></span> <span data-ttu-id="1051b-157">Merhaba **dosya kurtarma** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="1051b-157">hello **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="1051b-158">İçinde **1. adım: kurtarma noktası seçin**, hello açılan listeden bir kurtarma noktası seçin.</span><span class="sxs-lookup"><span data-stu-id="1051b-158">In **Step 1: Select recovery point**, select a recovery point from hello drop-down.</span></span>
11. <span data-ttu-id="1051b-159">İçinde **2. adım: betik toobrowse indirin ve dosyaları kurtarmak**, hello tıklatın **karşıdan yürütülebilir** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1051b-159">In **Step 2: Download script toobrowse and recover files**, click hello **Download Executable** button.</span></span> <span data-ttu-id="1051b-160">Merhaba dosya tooyour kaydetmek **indirmeleri** klasör.</span><span class="sxs-lookup"><span data-stu-id="1051b-160">Save hello file tooyour **Downloads** folder.</span></span>
12. <span data-ttu-id="1051b-161">Yerel bilgisayarınızda açın **dosya Gezgini** tooyour giderek **indirmeleri** klasörü ve kopyalama hello indirilen .exe dosyası.</span><span class="sxs-lookup"><span data-stu-id="1051b-161">On your local computer, open **File Explorer** and navigate tooyour **Downloads** folder and copy hello downloaded .exe file.</span></span> <span data-ttu-id="1051b-162">Merhaba filename VM adıyla önek alacaktır.</span><span class="sxs-lookup"><span data-stu-id="1051b-162">hello filename will be prefixed by your VM name.</span></span> 
13. <span data-ttu-id="1051b-163">VM'nizi (üzerinden RDP bağlantısı hello) üzerinde hello .exe dosyası toohello VM masaüstünün yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="1051b-163">On your VM (over hello RDP connection) paste hello .exe file toohello Desktop of your VM.</span></span> 
14. <span data-ttu-id="1051b-164">Vm'nizin toohello Masaüstü gidin ve üzerinde hello .exe dosyasını çift tıklatın.</span><span class="sxs-lookup"><span data-stu-id="1051b-164">Navigate toohello desktop of your VM and double-click on hello .exe.</span></span> <span data-ttu-id="1051b-165">Bu, bir komut istemi başlatın ve sonra erişebileceğiniz bir dosya paylaşımı bağlama hello kurtarma noktası.</span><span class="sxs-lookup"><span data-stu-id="1051b-165">This will launch a command prompt and then mount hello recovery point as a file share that you can access.</span></span> <span data-ttu-id="1051b-166">Bu tamamlandığında hello paylaşımı oluşturma, yazın **q** tooclose hello komut istemi.</span><span class="sxs-lookup"><span data-stu-id="1051b-166">When it is finished creating hello share, type **q** tooclose hello command prompt.</span></span>
15. <span data-ttu-id="1051b-167">VM'nizi üzerinde açık **dosya Gezgini** ve hello dosya paylaşımı için kullanılan toohello sürücü harfi gidin.</span><span class="sxs-lookup"><span data-stu-id="1051b-167">On your VM, open **File Explorer** and navigate toohello drive letter that was used for hello file share.</span></span>
16. <span data-ttu-id="1051b-168">Too\inetpub\wwwroot ve kopyalama gidin **iisstart.png** hello dosyasından paylaşmak ve \inetpub\wwwroot yapıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1051b-168">Navigate too\inetpub\wwwroot and copy **iisstart.png** from hello file share and paste it into \inetpub\wwwroot.</span></span> <span data-ttu-id="1051b-169">Örneğin, F:\inetpub\wwwroot\iisstart.png kopyalayın ve c:\inetpub\wwwroot toorecover hello dosyaya yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="1051b-169">For example, copy F:\inetpub\wwwroot\iisstart.png and paste it into c:\inetpub\wwwroot toorecover hello file.</span></span>
17. <span data-ttu-id="1051b-170">Yerel bilgisayarınızda bağlandığı hello tarayıcısı sekmesi açın hello VM hello IIS varsayılan sayfasını gösteren toohello IP adresidir.</span><span class="sxs-lookup"><span data-stu-id="1051b-170">On your local computer, open hello browser tab where you are connected toohello IP address of hello VM showing hello IIS default page.</span></span> <span data-ttu-id="1051b-171">CTRL + F5'e basın. toorefresh hello tarayıcı sayfası.</span><span class="sxs-lookup"><span data-stu-id="1051b-171">Press CTRL + F5 toorefresh hello browser page.</span></span> <span data-ttu-id="1051b-172">Bu hello görmelisiniz görüntüsü geri yüklendi.</span><span class="sxs-lookup"><span data-stu-id="1051b-172">You should now see that hello image has been restored.</span></span>
18. <span data-ttu-id="1051b-173">Yerel bilgisayarınızda toohello tarayıcı sekmesinde hello Azure portal için ve geri dönün **adım 3: hello diskleri kurtarma işleminden sonra çıkarın** hello tıklatın **çıkarın diskleri** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="1051b-173">On your local computer, go back toohello browser tab for hello Azure portal and in **Step 3: Unmount hello disks after recovery** click hello **Unmount Disks** button.</span></span> <span data-ttu-id="1051b-174">Bu adım toodo unutursanız, hello bağlantı toohello mountpoint 12 saat sonra otomatik olarak kapat.</span><span class="sxs-lookup"><span data-stu-id="1051b-174">If you forget toodo this step, hello connection toohello mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="1051b-175">Bu 12 saat sonra yeni bir komut dosyası toocreate yeni mountpoint toodownload gerekir.</span><span class="sxs-lookup"><span data-stu-id="1051b-175">After those 12 hours, you need toodownload a new script toocreate a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1051b-176">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1051b-176">Next steps</span></span>

<span data-ttu-id="1051b-177">Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="1051b-177">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1051b-178">VM bir yedeğini oluşturun</span><span class="sxs-lookup"><span data-stu-id="1051b-178">Create a backup of a VM</span></span>
> * <span data-ttu-id="1051b-179">Günlük yedekleme zamanlaması</span><span class="sxs-lookup"><span data-stu-id="1051b-179">Schedule a daily backup</span></span>
> * <span data-ttu-id="1051b-180">Bir dosyayı bir yedekten geri yükleyin</span><span class="sxs-lookup"><span data-stu-id="1051b-180">Restore a file from a backup</span></span>

<span data-ttu-id="1051b-181">Sanal makineler izleme hakkında toohello sonraki öğretici toolearn ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="1051b-181">Advance toohello next tutorial toolearn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1051b-182">Sanal makineleri izleme</span><span class="sxs-lookup"><span data-stu-id="1051b-182">Monitor virtual machines</span></span>](tutorial-monitoring.md)









