---
title: Yedekleme Azure Linux VM'ler | Microsoft Docs
description: "Linux Vm'lerinizi Azure Yedekleme kullanılarak yedekleyerek koruyun."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 7c00392d5185a2f067f2ee2717529dcbde1e71f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-linux--virtual-machines-in-azure"></a><span data-ttu-id="e5d4b-103">Azure'daki Linux sanal makineleri yedekleyin</span><span class="sxs-lookup"><span data-stu-id="e5d4b-103">Back up Linux  virtual machines in Azure</span></span>

<span data-ttu-id="e5d4b-104">Düzenli aralıklarla yedekleme yaparak verilerinizi koruyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="e5d4b-105">Azure yedekleme coğrafi olarak yedekli kurtarma kasalarında depolanan kurtarma noktaları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="e5d4b-106">Bir kurtarma noktasından geri yüklediğinizde, geri yükleyebilirsiniz tüm VM ya da yalnızca belirli dosyaları hello.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-106">When you restore from a recovery point, you can restore hello whole VM or just specific files.</span></span> <span data-ttu-id="e5d4b-107">Bu makalede nasıl toorestore tek bir dosya tooa Linux VM çalışan nginx açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-107">This article explains how toorestore a single file tooa Linux VM running nginx.</span></span> <span data-ttu-id="e5d4b-108">VM toouse zaten sahip değilseniz, birini oluşturabilirsiniz hello kullanarak [Linux quickstart](quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e5d4b-108">If you don't already have a VM toouse, you can create one using hello [Linux quickstart](quick-create-cli.md).</span></span> <span data-ttu-id="e5d4b-109">Bu öğreticide şunların nasıl yapıldığını öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e5d4b-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e5d4b-110">VM bir yedeğini oluşturun</span><span class="sxs-lookup"><span data-stu-id="e5d4b-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="e5d4b-111">Günlük yedekleme zamanlaması</span><span class="sxs-lookup"><span data-stu-id="e5d4b-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="e5d4b-112">Bir dosyayı bir yedekten geri yükleyin</span><span class="sxs-lookup"><span data-stu-id="e5d4b-112">Restore a file from a backup</span></span>



## <a name="backup-overview"></a><span data-ttu-id="e5d4b-113">Backup’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="e5d4b-113">Backup overview</span></span>

<span data-ttu-id="e5d4b-114">Hello Azure Backup hizmeti yedekleme başlattığında hello yedekleme uzantısını tootake zaman içinde nokta anlık görüntü tetikler.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-114">When hello Azure Backup service initiates a backup, it triggers hello backup extension tootake a point-in-time snapshot.</span></span> <span data-ttu-id="e5d4b-115">Hello Azure Backup hizmeti kullanan hello _VMSnapshotLinux_ Linux uzantı.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-115">hello Azure Backup service uses hello _VMSnapshotLinux_ extension in Linux.</span></span> <span data-ttu-id="e5d4b-116">Merhaba VM çalışıyorsa hello uzantısı hello ilk VM yedekleme sırasında yüklenir.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-116">hello extension is installed during hello first VM backup if hello VM is running.</span></span> <span data-ttu-id="e5d4b-117">Merhaba VM çalışır durumda değilse, hello Backup hizmeti bir anlık görüntüsünü hello bu yana (hiçbir uygulama yazma VM durduruldu hello sırasında gerçekleşir) depolama temel alır.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-117">If hello VM is not running, hello Backup service takes a snapshot of hello underlying storage (since no application writes occur while hello VM is stopped).</span></span>

<span data-ttu-id="e5d4b-118">Varsayılan olarak, Azure Backup dosya sisteminin tutarlı bir yedeklemenin Linux VM için alır ancak yapılandırılmış tootake olabilir [uygulama tutarlı yedekleme öncesi betik ve sonrası betik framework kullanarak](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).</span><span class="sxs-lookup"><span data-stu-id="e5d4b-118">By default, Azure Backup takes a file system consistent backup for Linux VM but it can be configured tootake [application consistent backup using pre-script and post-script framework](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).</span></span> <span data-ttu-id="e5d4b-119">Hello Azure Backup hizmeti hello anlık görüntüsünü alır sonra hello aktarılan toohello kasası verilerdir.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-119">Once hello Azure Backup service takes hello snapshot, hello data is transferred toohello vault.</span></span> <span data-ttu-id="e5d4b-120">toomaximize verimliliği hello hizmeti tanımlar ve yalnızca hello hello önceki yedeklemeden bu yana değişmiş olan veri bloklarını aktarır.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-120">toomaximize efficiency, hello service identifies and transfers only hello blocks of data that have changed since hello previous backup.</span></span>

<span data-ttu-id="e5d4b-121">Merhaba veri aktarımı tamamlandığında hello anlık görüntü kaldırılır ve bir kurtarma noktası oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-121">When hello data transfer is complete, hello snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="e5d4b-122">Bir yedekleme oluşturun</span><span class="sxs-lookup"><span data-stu-id="e5d4b-122">Create a backup</span></span>
<span data-ttu-id="e5d4b-123">Bir basit zamanlanmış günlük yedekleme tooa kurtarma Hizmetleri kasası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-123">Create a simple scheduled daily backup tooa Recovery Services Vault.</span></span> 

1. <span data-ttu-id="e5d4b-124">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e5d4b-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e5d4b-125">Merhaba soldaki Hello menüde seçin **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-125">In hello menu on hello left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="e5d4b-126">Merhaba listeden VM tooback seçin.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-126">From hello list, select a VM tooback up.</span></span>
4. <span data-ttu-id="e5d4b-127">Merhaba, hello VM dikey **ayarları** 'yi tıklatın **yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-127">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="e5d4b-128">Merhaba **yedeklemeyi etkinleştir** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-128">hello **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="e5d4b-129">İçinde **kurtarma Hizmetleri kasası**, tıklatın **Yeni Oluştur** hello ad hello yeni kasa belirtin.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-129">In **Recovery Services vault**, click **Create new** and provide hello name for hello new vault.</span></span> <span data-ttu-id="e5d4b-130">Yeni bir kasa aynı hello oluşturulan kaynak grubunu ve konumu hello sanal makine olarak.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-130">A new vault is created in hello same Resource Group and location as hello virtual machine.</span></span>
6. <span data-ttu-id="e5d4b-131">Tıklatın **yedekleme İlkesi**.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-131">Click **Backup policy**.</span></span> <span data-ttu-id="e5d4b-132">Bu örneğin hello Varsayılanları tutun ve **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-132">For this example, keep hello defaults and click **OK**.</span></span>
7. <span data-ttu-id="e5d4b-133">Merhaba üzerinde **yedeklemeyi etkinleştir** dikey penceresinde tıklatın **yedeklemeyi etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-133">On hello **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="e5d4b-134">Merhaba varsayılan zamanlamaya göre günlük yedekleme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-134">This creates a daily backup based on hello default schedule.</span></span>
10. <span data-ttu-id="e5d4b-135">toocreate bir ilk kurtarma noktasında hello **yedekleme** dikey penceresinde **Şimdi Yedekle**.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-135">toocreate an initial recovery point, on hello **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="e5d4b-136">Merhaba üzerinde **Şimdi Yedekle** dikey penceresinde hello takvim simgesini tıklatın, hello Takvim denetimi tooselect hello bu kurtarma noktası korunur ve tıklatın son günü kullanmak **yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-136">On hello **Backup Now** blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="e5d4b-137">Merhaba, **yedekleme** dikey penceresinde, VM için tam kurtarma noktalarının sayısı hello görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-137">In hello **Backup** blade for your VM, you will see hello number of recovery points that are complete.</span></span>

    ![Kurtarma noktaları](./media/tutorial-backup-vms/backup-complete.png)

<span data-ttu-id="e5d4b-139">Merhaba ilk yedek yaklaşık 20 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-139">hello first backup takes about 20 minutes.</span></span> <span data-ttu-id="e5d4b-140">Yedekleme tamamlandıktan sonra bu öğreticinin sonraki bölümü toohello devam edin.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-140">Proceed toohello next part of this tutorial after your backup is finished.</span></span>

## <a name="restore-a-file"></a><span data-ttu-id="e5d4b-141">Bir dosya geri yükleme</span><span class="sxs-lookup"><span data-stu-id="e5d4b-141">Restore a file</span></span>

<span data-ttu-id="e5d4b-142">Yanlışlıkla silme veya değişiklikleri tooa dosyasını, dosya kurtarma toorecover hello dosyasını yedekleme Kasası'nı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-142">If you accidentally delete or make changes tooa file, you can use File Recovery toorecover hello file from your backup vault.</span></span> <span data-ttu-id="e5d4b-143">Dosya Kurtarma kullanan VM hello üzerinde çalışan bir komut yerel sürücü olarak toomount hello kurtarma noktası.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-143">File Recovery uses a script that runs on hello VM, toomount hello recovery point as local drive.</span></span> <span data-ttu-id="e5d4b-144">Merhaba kurtarma noktasından dosya kopyalayabilir ve toohello VM geri için bu sürücüler için 12 saat bağlı kalır.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-144">These drives will remain mounted for 12 hours so that you can copy files from hello recovery point and restore them toohello VM.</span></span>  

<span data-ttu-id="e5d4b-145">Bu örnekte, nasıl toorecover hello varsayılan nginx web sayfası /var/www/html/index.nginx-debian.html gösterir.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-145">In this example, we show how toorecover hello default nginx web page /var/www/html/index.nginx-debian.html.</span></span> <span data-ttu-id="e5d4b-146">Merhaba ortak IP adresi bu örnekte bizim VM *13.69.75.209*.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-146">hello public IP address of our VM in this example is *13.69.75.209*.</span></span> <span data-ttu-id="e5d4b-147">Başlangıç IP adresi vm kullanmanın bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e5d4b-147">You can find hello IP address of your vm using:</span></span>

 ```bash 
 az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
 ```

 
1. <span data-ttu-id="e5d4b-148">Yerel bilgisayarınızda, bir tarayıcı ve türü hello genel IP adresi VM toosee hello varsayılan nginx web sayfanızın açın.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-148">On your local computer, open a browser and type in hello public IP address of your VM toosee hello default nginx web page.</span></span>

    ![Varsayılan nginx web sayfası](./media/tutorial-backup-vms/nginx-working.png)

1. <span data-ttu-id="e5d4b-150">VM içine SSH.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-150">SSH into your VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
2. <span data-ttu-id="e5d4b-151">/Var/www/HTML/index.nginx-debian.HTML silin.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-151">Delete /var/www/html/index.nginx-debian.html.</span></span>

    ```bash
    sudo rm /var/www/html/index.nginx-debian.html
    ```
    
4. <span data-ttu-id="e5d4b-152">Yerel bilgisayarınızda CTRL tuşuna tarafından hello tarayıcıyı yenilemek + varsayılan nginx sayfa F5 toosee kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-152">On your local computer, refresh hello browser by hitting CTRL + F5 toosee that default nginx page is gone.</span></span>

    ![Varsayılan nginx web sayfası](./media/tutorial-backup-vms/nginx-broken.png)
    
1. <span data-ttu-id="e5d4b-154">Yerel bilgisayarınızda toohello içinde oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e5d4b-154">On your local computer, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
6. <span data-ttu-id="e5d4b-155">Merhaba soldaki Hello menüde seçin **sanal makineleri**.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-155">In hello menu on hello left, select **Virtual machines**.</span></span> 
7. <span data-ttu-id="e5d4b-156">Merhaba listeden hello VM seçin.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-156">From hello list, select hello VM.</span></span>
8. <span data-ttu-id="e5d4b-157">Merhaba, hello VM dikey **ayarları** 'yi tıklatın **yedekleme**.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-157">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="e5d4b-158">Merhaba **yedekleme** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-158">hello **Backup** blade opens.</span></span> 
9. <span data-ttu-id="e5d4b-159">Merhaba dikey penceresinde hello üstündeki Hello menüde seçin **dosya kurtarma**.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-159">In hello menu at hello top of hello blade, select **File Recovery**.</span></span> <span data-ttu-id="e5d4b-160">Merhaba **dosya kurtarma** dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-160">hello **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="e5d4b-161">İçinde **1. adım: kurtarma noktası seçin**, hello açılan listeden bir kurtarma noktası seçin.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-161">In **Step 1: Select recovery point**, select a recovery point from hello drop-down.</span></span>
11. <span data-ttu-id="e5d4b-162">İçinde **2. adım: betik toobrowse indirin ve dosyaları kurtarmak**, hello tıklatın **karşıdan yürütülebilir** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-162">In **Step 2: Download script toobrowse and recover files**, click hello **Download Executable** button.</span></span> <span data-ttu-id="e5d4b-163">Merhaba indirilen dosya tooyour yerel bilgisayara kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-163">Save hello downloaded file tooyour local computer.</span></span>
7. <span data-ttu-id="e5d4b-164">Tıklatın **karşıdan yükleme komut dosyası** toodownload hello komut dosyası yerel olarak.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-164">Click **Download script** toodownload hello script file locally.</span></span>
8. <span data-ttu-id="e5d4b-165">Aşağıdaki, değiştirerek bir Bash istemi hello açmak *Linux_myVM_05 05 2017.sh* yol ve dosya adı, indirdiğiniz hello komut ile Merhaba düzeltmek *azureuser* hello username hello VM için ve *13.69.75.209* hello ortak IP adresiyle VM.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-165">Open a Bash prompt and type hello following, replacing *Linux_myVM_05-05-2017.sh* with hello correct path and filename for hello script that you downloaded, *azureuser* with hello username for hello VM and *13.69.75.209* with hello public IP address for your VM.</span></span>
    
    ```bash
    scp Linux_myVM_05-05-2017.sh azureuser@13.69.75.209:
    ```
    
9. <span data-ttu-id="e5d4b-166">Yerel bilgisayarınızda, bir SSH bağlantısı toohello VM açın.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-166">On your local computer, open an SSH connection toohello VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
    
10. <span data-ttu-id="e5d4b-167">VM'nizi üzerinde eklemek izinleri toohello betiği yürütün.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-167">On your VM, add execute permissions toohello script file.</span></span>

    ```bash
    chmod +x Linux_myVM_05-05-2017.sh
    ```
    
11. <span data-ttu-id="e5d4b-168">VM'nizi üzerinde hello betik toomount hello kurtarma noktası bir dosya sistemi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-168">On your VM, run hello script toomount hello recovery point as a filesystem.</span></span>

    ```bash
    ./Linux_myVM_05-05-2017.sh
    ```
    
12. <span data-ttu-id="e5d4b-169">Hello hello bağlama noktası yolunu hello hello betik verir çıktı.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-169">hello output from hello script gives you hello path for hello mount point.</span></span> <span data-ttu-id="e5d4b-170">Merhaba çıkış benzer toothis görünür:</span><span class="sxs-lookup"><span data-stu-id="e5d4b-170">hello output looks similar toothis:</span></span>

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
                          
    Connecting toorecovery point using ISCSI service...
    
    Connection succeeded!
    
    Please wait while we attach volumes of hello recovery point toothis machine...
                         
    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath 

    1)  | /dev/sdc  |  /dev/sdc1  |  /home/azureuser/myVM-20170505191055/Volume1

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

12. <span data-ttu-id="e5d4b-171">Merhaba nginx varsayılan web sayfası, VM, kopyalama hello bağlama noktası geri toowhere hello dosyası silindi.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-171">On your VM, copy hello nginx default web page from hello mount point back toowhere you deleted hello file.</span></span>

    ```bash
    sudo cp ~/myVM-20170505191055/Volume1/var/www/html/index.nginx-debian.html /var/www/html/
    ```
    
17. <span data-ttu-id="e5d4b-172">Yerel bilgisayarınızda bağlandığı hello tarayıcısı sekmesi açın hello VM hello nginx varsayılan sayfasını gösteren toohello IP adresidir.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-172">On your local computer, open hello browser tab where you are connected toohello IP address of hello VM showing hello nginx default page.</span></span> <span data-ttu-id="e5d4b-173">CTRL + F5'e basın. toorefresh hello tarayıcı sayfası.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-173">Press CTRL + F5 toorefresh hello browser page.</span></span> <span data-ttu-id="e5d4b-174">Bu hello görmelisiniz varsayılan sayfa yeniden çalışma.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-174">You should now see that hello default page is working again.</span></span>

    ![Varsayılan nginx web sayfası](./media/tutorial-backup-vms/nginx-working.png)

18. <span data-ttu-id="e5d4b-176">Yerel bilgisayarınızda toohello tarayıcı sekmesinde hello Azure portal için ve geri dönün **adım 3: hello diskleri kurtarma işleminden sonra çıkarın** hello tıklatın **çıkarın diskleri** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-176">On your local computer, go back toohello browser tab for hello Azure portal and in **Step 3: Unmount hello disks after recovery** click hello **Unmount Disks** button.</span></span> <span data-ttu-id="e5d4b-177">Bu adım toodo unutursanız, hello bağlantı toohello mountpoint 12 saat sonra otomatik olarak kapat.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-177">If you forget toodo this step, hello connection toohello mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="e5d4b-178">Bu 12 saat sonra yeni bir komut dosyası toocreate yeni mountpoint toodownload gerekir.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-178">After those 12 hours, you need toodownload a new script toocreate a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e5d4b-179">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e5d4b-179">Next steps</span></span>

<span data-ttu-id="e5d4b-180">Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="e5d4b-180">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e5d4b-181">VM bir yedeğini oluşturun</span><span class="sxs-lookup"><span data-stu-id="e5d4b-181">Create a backup of a VM</span></span>
> * <span data-ttu-id="e5d4b-182">Günlük yedekleme zamanlaması</span><span class="sxs-lookup"><span data-stu-id="e5d4b-182">Schedule a daily backup</span></span>
> * <span data-ttu-id="e5d4b-183">Bir dosyayı bir yedekten geri yükleyin</span><span class="sxs-lookup"><span data-stu-id="e5d4b-183">Restore a file from a backup</span></span>

<span data-ttu-id="e5d4b-184">Sanal makineler izleme hakkında toohello sonraki öğretici toolearn ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="e5d4b-184">Advance toohello next tutorial toolearn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e5d4b-185">Sanal makineleri izleme</span><span class="sxs-lookup"><span data-stu-id="e5d4b-185">Monitor virtual machines</span></span>](tutorial-monitoring.md)

