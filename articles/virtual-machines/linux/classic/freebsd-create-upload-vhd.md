---
title: "aaaCreate ve karşıya yükleme FreeBSD VM görüntü | Microsoft Docs"
description: "Bir sanal sabit hello FreeBSD işletim sistemi toocreate bir Azure sanal makinesini içeren disk (VHD) yüklemek ve toocreate bilgi edinin"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: kyliel
ms.openlocfilehash: f3bd155e496f1a2713d36bb66ea9824ed4c210ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-freebsd-vhd-tooazure"></a><span data-ttu-id="49917-103">Oluşturun ve FreeBSD VHD tooAzure yükleyin</span><span class="sxs-lookup"><span data-stu-id="49917-103">Create and upload a FreeBSD VHD tooAzure</span></span>
<span data-ttu-id="49917-104">Bu makalede FreeBSD işletim sistemi toocreate ve karşıya yükleme sanal sabit içeren bir disk (VHD) nasıl hello gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="49917-104">This article shows you how toocreate and upload a virtual hard disk (VHD) that contains hello FreeBSD operating system.</span></span> <span data-ttu-id="49917-105">Karşıya yüklediğiniz sonra kendi görüntü toocreate azure'da sanal makine (VM) olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49917-105">After you upload it, you can use it as your own image toocreate a virtual machine (VM) in Azure.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="49917-106">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="49917-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="49917-107">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="49917-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="49917-108">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="49917-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="49917-109">Merhaba Resource Manager modelini kullanarak bir VHD'yi karşıya yükleme hakkında daha fazla bilgi için bkz: [burada](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="49917-109">For information about uploading a VHD using hello Resource Manager model, see [here](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49917-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="49917-110">Prerequisites</span></span>
<span data-ttu-id="49917-111">Bu makalede aşağıdaki öğelerindeki hello olduğunu varsayar:</span><span class="sxs-lookup"><span data-stu-id="49917-111">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="49917-112">**Bir Azure aboneliği**--bir hesabınız yoksa yalnızca birkaç dakika içinde bir oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49917-112">**An Azure subscription**--If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="49917-113">Bir MSDN aboneliğiniz varsa, bkz: [Visual Studio aboneleri için aylık Azure kredi](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="49917-113">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="49917-114">Aksi takdirde nasıl çok öğrenin[ücretsiz bir deneme hesabı oluşturma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="49917-114">Otherwise, learn how too[create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="49917-115">**Azure PowerShell Araçları**--hello Azure PowerShell modülü yüklenmelidir ve Azure aboneliğinize toouse yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="49917-115">**Azure PowerShell tools**--hello Azure PowerShell module must be installed and configured toouse your Azure subscription.</span></span> <span data-ttu-id="49917-116">toodownload hello modülü bkz [Azure indirmeleri](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="49917-116">toodownload hello module, see [Azure downloads](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="49917-117">Açıklayan bir öğretici nasıl tooinstall ve yapılandırma hello modülü kullanılabilir burada.</span><span class="sxs-lookup"><span data-stu-id="49917-117">A tutorial that describes how tooinstall and configure hello module is available here.</span></span> <span data-ttu-id="49917-118">Kullanım hello [Azure indirmeleri](https://azure.microsoft.com/downloads/) cmdlet tooupload hello VHD.</span><span class="sxs-lookup"><span data-stu-id="49917-118">Use hello [Azure Downloads](https://azure.microsoft.com/downloads/) cmdlet tooupload hello VHD.</span></span>
* <span data-ttu-id="49917-119">**Bir .vhd dosyası yüklü FreeBSD işletim sistemi**--desteklenen FreeBSD işletim sistemi olmalıdır bir yüklü tooa sanal sabit disk.</span><span class="sxs-lookup"><span data-stu-id="49917-119">**FreeBSD operating system installed in a .vhd file**--A supported   FreeBSD operating system must be installed tooa virtual hard disk.</span></span> <span data-ttu-id="49917-120">Birden çok araç toocreate .vhd dosyaları mevcut.</span><span class="sxs-lookup"><span data-stu-id="49917-120">Multiple tools exist toocreate .vhd files.</span></span> <span data-ttu-id="49917-121">Örneğin, Hyper-V toocreate hello .vhd dosyası gibi bir sanallaştırma çözümü kullanın ve hello işletim sistemi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="49917-121">For example, you can use a virtualization solution such as Hyper-V toocreate hello .vhd file and install hello operating system.</span></span> <span data-ttu-id="49917-122">Tooinstall ve kullanım Hyper-V, nasıl görürüm hakkında yönergeler için [Hyper-V yükleyin ve sanal makine oluşturma](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="49917-122">For instructions about how tooinstall and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="49917-123">Azure'da Hello yeni VHDX biçimi desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="49917-123">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="49917-124">Hyper-V Yöneticisi'ni kullanarak hello disk tooVHD biçimine Dönüştür veya cmdlet hello [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="49917-124">You can convert hello disk tooVHD format by using Hyper-V Manager or hello cmdlet [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="49917-125">Ayrıca, bir [nasıl hakkında MSDN'de öğretici toouse FreeBSD Hyper-V ile](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span><span class="sxs-lookup"><span data-stu-id="49917-125">In addition, there is a [tutorial on MSDN about how toouse FreeBSD with Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span></span>
>
>

<span data-ttu-id="49917-126">Bu görev hello aşağıdaki beş adımları içerir:</span><span class="sxs-lookup"><span data-stu-id="49917-126">This task includes hello following five steps:</span></span>

## <a name="step-1-prepare-hello-image-for-upload"></a><span data-ttu-id="49917-127">1. adım: hello görüntü karşıya yükleme için hazırlama</span><span class="sxs-lookup"><span data-stu-id="49917-127">Step 1: Prepare hello image for upload</span></span>
<span data-ttu-id="49917-128">Merhaba sanal makinede hello FreeBSD işletim sisteminin yüklü olduğu hello yordamları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="49917-128">On hello virtual machine where you installed hello FreeBSD operating system, complete hello following procedures:</span></span>

1. <span data-ttu-id="49917-129">DHCP'yi etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="49917-129">Enable DHCP.</span></span>

        # echo 'ifconfig_hn0="SYNCDHCP"' >> /etc/rc.conf
        # service netif restart
2. <span data-ttu-id="49917-130">SSH etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="49917-130">Enable SSH.</span></span>

    <span data-ttu-id="49917-131">Bu hello SSH sunucusu yüklü olduğundan ve önyükleme sırasında toostart yapılandırılmış emin olun.</span><span class="sxs-lookup"><span data-stu-id="49917-131">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span> <span data-ttu-id="49917-132">Varsayılan olarak FreeBSD disk yüklemesinden sonra etkin.</span><span class="sxs-lookup"><span data-stu-id="49917-132">By default it is enabled after installation from FreeBSD disc.</span></span> 
3. <span data-ttu-id="49917-133">Bir seri Konsolu ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="49917-133">Set up a serial console.</span></span>

        # echo 'console="comconsole vidconsole"' >> /boot/loader.conf
        # echo 'comconsole_speed="115200"' >> /boot/loader.conf
4. <span data-ttu-id="49917-134">Sudo yükleyin.</span><span class="sxs-lookup"><span data-stu-id="49917-134">Install sudo.</span></span>

    <span data-ttu-id="49917-135">Azure'da Hello kök hesabı devre dışı.</span><span class="sxs-lookup"><span data-stu-id="49917-135">hello root account is disabled in Azure.</span></span> <span data-ttu-id="49917-136">Başka bir deyişle, yükseltilmiş ayrıcalıklarla bir ayrıcalıksız kullanıcı toorun komutlarındaki tooutilize sudo gerekir.</span><span class="sxs-lookup"><span data-stu-id="49917-136">This means you need tooutilize sudo from an unprivileged user toorun commands with elevated privileges.</span></span>

        # pkg install sudo
   
5. <span data-ttu-id="49917-137">Azure Aracısı önkoşulları.</span><span class="sxs-lookup"><span data-stu-id="49917-137">Prerequisites for Azure Agent.</span></span>

        # pkg install python27  
        # pkg install Py27-setuptools  
        # ln -s /usr/local/bin/python2.7 /usr/bin/python   
        # pkg install git
6. <span data-ttu-id="49917-138">Azure aracısını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="49917-138">Install Azure Agent.</span></span>

    <span data-ttu-id="49917-139">Merhaba hello Azure Aracısı en son sürümü her zaman bulunabilir [github](https://github.com/Azure/WALinuxAgent/releases).</span><span class="sxs-lookup"><span data-stu-id="49917-139">hello latest release of hello Azure Agent can always be found on [github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="49917-140">sürüm 2.0.10 hello + resmi olarak FreeBSD 10 & 10.1 ve 2.1.4 + (2.2.x dahil) resmi olarak destekleyen FreeBSD 10.2 ve sonraki sürümlerinde hello sürümünü destekler.</span><span class="sxs-lookup"><span data-stu-id="49917-140">hello version 2.0.10 + officially supports FreeBSD 10 & 10.1, and hello version 2.1.4 + (including 2.2.x) officially supports FreeBSD 10.2 and later releases.</span></span>

        # git clone https://github.com/Azure/WALinuxAgent.git  
        # cd WALinuxAgent  
        # git tag  
        …
        WALinuxAgent-2.0.16
        …
        v2.1.4
        v2.1.4.rc0
        v2.1.4.rc1

    <span data-ttu-id="49917-141">2.0 için 2.0.16 örnek olarak kullanalım:</span><span class="sxs-lookup"><span data-stu-id="49917-141">For 2.0, let's use 2.0.16 as an example:</span></span>

        # git checkout WALinuxAgent-2.0.16
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  

    <span data-ttu-id="49917-142">2.1 için şimdi bir örnek olarak 2.1.4 kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="49917-142">For 2.1, let's use 2.1.4 as an example:</span></span>

        # git checkout v2.1.4
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  
        # ln -sf /usr/local/sbin/waagent2.0 /usr/sbin/waagent2.0

   > [!IMPORTANT]
   > <span data-ttu-id="49917-143">Azure aracısını yükledikten sonra çalışan bir fikir tooverify şöyledir:</span><span class="sxs-lookup"><span data-stu-id="49917-143">After you install Azure Agent, it's a good idea tooverify that it's running:</span></span>
   >
   >

        # waagent -version
        WALinuxAgent-2.1.4 running on freebsd 10.3
        Python: 2.7.11
        # ps auxw | grep waagent
        root   639   0.0  0.5 104620 17520 u0- I    05:17    0:00.20 python /usr/local/sbin/waagent -daemon (python2.7)
        # cat /var/log/waagent.log
7. <span data-ttu-id="49917-144">Merhaba sistem sağlamayı sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="49917-144">Deprovision hello system.</span></span>

    <span data-ttu-id="49917-145">Deprovision hello sistem tooclean ve yapma, sağlama işleminin için uygun.</span><span class="sxs-lookup"><span data-stu-id="49917-145">Deprovision hello system tooclean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="49917-146">Hello aşağıdaki komut da hello son sağlanan kullanıcı hesabını ve ilişkili hello verileri siler:</span><span class="sxs-lookup"><span data-stu-id="49917-146">hello following command also deletes hello last provisioned user account and hello associated data:</span></span>

        # echo "y" |  /usr/local/sbin/waagent -deprovision+user  
        # echo  'waagent_enable="YES"' >> /etc/rc.conf

    <span data-ttu-id="49917-147">Şimdi, VM kapatma.</span><span class="sxs-lookup"><span data-stu-id="49917-147">Now you can shut down your VM.</span></span>

## <a name="step-2-create-a-storage-account-in-azure"></a><span data-ttu-id="49917-148">2. adım: Azure depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="49917-148">Step 2: Create a storage account in Azure</span></span>
<span data-ttu-id="49917-149">Kullanılan toocreate bir sanal makine olabilir için Azure tooupload bir .vhd dosyası depolama hesabı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="49917-149">You need a storage account in Azure tooupload a .vhd file so it can be used toocreate a virtual machine.</span></span> <span data-ttu-id="49917-150">Hello Azure Klasik portalı toocreate bir depolama hesabı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49917-150">You can use hello Azure classic portal toocreate a storage account.</span></span>

1. <span data-ttu-id="49917-151">İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="49917-151">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="49917-152">Merhaba komut çubuğunda seçin **yeni**.</span><span class="sxs-lookup"><span data-stu-id="49917-152">On hello command bar, select **New**.</span></span>
3. <span data-ttu-id="49917-153">Seçin **Veri Hizmetleri** > **depolama** > **hızlı Oluştur**.</span><span class="sxs-lookup"><span data-stu-id="49917-153">Select **Data Services** > **Storage** > **Quick Create**.</span></span>

    ![Hızlı bir depolama hesabı oluşturma](./media/freebsd-create-upload-vhd/Storage-quick-create.png)
4. <span data-ttu-id="49917-155">Aşağıdaki gibi Hello alanları doldurun:</span><span class="sxs-lookup"><span data-stu-id="49917-155">Fill out hello fields as follows:</span></span>

   * <span data-ttu-id="49917-156">Merhaba, **URL** alan, bir alt etki alanı adı toouse hello depolama hesabı URL'si yazın.</span><span class="sxs-lookup"><span data-stu-id="49917-156">In hello **URL** field, type a subdomain name toouse in hello storage account URL.</span></span> <span data-ttu-id="49917-157">Merhaba girişi 3-24 sayılar ve küçük harfleri içerebilir.</span><span class="sxs-lookup"><span data-stu-id="49917-157">hello entry can contain from 3-24 numbers and lowercase letters.</span></span> <span data-ttu-id="49917-158">Bu ad kullanılan tooaddress Azure Blob storage, Azure kuyruk depolama ya da Azure Table storage kaynaklarını hello abonelik için hello URL'de hello ana bilgisayar adı olur.</span><span class="sxs-lookup"><span data-stu-id="49917-158">This name becomes hello host name within hello URL that is used tooaddress Azure Blob storage, Azure Queue storage, or Azure Table storage resources for hello subscription.</span></span>
   * <span data-ttu-id="49917-159">Merhaba, **konum/benzeşim grubu** açılır menü hello seçin **konumu ya da benzeşim grubu** hello depolama hesabı için.</span><span class="sxs-lookup"><span data-stu-id="49917-159">In hello **Location/Affinity Group** drop-down menu, choose hello **location or affinity group** for hello storage account.</span></span> <span data-ttu-id="49917-160">Bir benzeşim grubu, bulut Hizmetleri ve depolama hello yerleştirmenizi sağlar aynı veri merkezinde.</span><span class="sxs-lookup"><span data-stu-id="49917-160">An affinity group lets you put your cloud services and storage in hello same data center.</span></span>
   * <span data-ttu-id="49917-161">Merhaba, **çoğaltma** alan, karar olup olmadığını toouse **coğrafi olarak yedekli** hello depolama hesabı için çoğaltma.</span><span class="sxs-lookup"><span data-stu-id="49917-161">In hello **Replication** field, decide whether toouse **Geo-Redundant** replication for hello storage account.</span></span> <span data-ttu-id="49917-162">Coğrafi çoğaltma varsayılan olarak açıktır.</span><span class="sxs-lookup"><span data-stu-id="49917-162">Geo-replication is turned on by default.</span></span> <span data-ttu-id="49917-163">Bu seçenek, veri tooa ikincil konumda, maliyet tooyou çoğaltır, böylece önemli bir hata durumunda toothat konum depolama alanınızın başarısız hello birincil konumda oluşur.</span><span class="sxs-lookup"><span data-stu-id="49917-163">This option replicates your data tooa secondary location, at no cost tooyou, so that your storage fails over toothat location if a major failure occurs at hello primary location.</span></span> <span data-ttu-id="49917-164">Merhaba ikincil konum otomatik olarak atanır ve değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="49917-164">hello secondary location is assigned automatically and can't be changed.</span></span> <span data-ttu-id="49917-165">Son toolegal gereksinimleri veya kuruluş ilkesi, bulut tabanlı depolama hello konumu hakkında daha fazla denetime ihtiyacınız varsa, coğrafi çoğaltma kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49917-165">If you need more control over hello location of your cloud-based storage due toolegal requirements or organizational policy, you can turn off geo-replication.</span></span> <span data-ttu-id="49917-166">Ancak, daha sonra coğrafi çoğaltma üzerinde kapatırsanız, size bir kerelik ücretlendirilir olduğunu unutmayın veri aktarımı ücreti tooreplicate, var olan veri toohello ikincil konum.</span><span class="sxs-lookup"><span data-stu-id="49917-166">However, be aware that if you later turn on geo-replication, you will be charged a one-time data transfer fee tooreplicate your existing data toohello secondary location.</span></span> <span data-ttu-id="49917-167">Depolama Hizmetleri coğrafi çoğaltma olmadan indirimli fiyatla sunulur.</span><span class="sxs-lookup"><span data-stu-id="49917-167">Storage services without geo-replication are offered at a discount.</span></span> <span data-ttu-id="49917-168">Coğrafi çoğaltma depolama hesaplarını yönetme hakkında daha fazla bilgi şurada bulunabilir: [Azure Storage çoğaltma](../../../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="49917-168">More details about managing geo-replication of storage accounts can be found here: [Azure Storage replication](../../../storage/common/storage-redundancy.md).</span></span>

     ![Depolama hesabı ayrıntılarını girin](./media/freebsd-create-upload-vhd/Storage-create-account.png)
5. <span data-ttu-id="49917-170">Seçin **depolama hesabı oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="49917-170">Select **Create Storage Account**.</span></span> <span data-ttu-id="49917-171">Merhaba hesabı artık altında görünür **depolama**.</span><span class="sxs-lookup"><span data-stu-id="49917-171">hello account now appears under **storage**.</span></span>

    ![Depolama hesabı başarıyla oluşturuldu](./media/freebsd-create-upload-vhd/Storagenewaccount.png)
6. <span data-ttu-id="49917-173">Ardından, karşıya yüklenen .vhd dosyaları için bir kapsayıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="49917-173">Next, create a container for your uploaded .vhd files.</span></span> <span data-ttu-id="49917-174">Merhaba depolama hesabı adı seçin ve ardından **kapsayıcıları**.</span><span class="sxs-lookup"><span data-stu-id="49917-174">Select hello storage account name, and then select **Containers**.</span></span>

    ![Depolama hesabı ayrıntısı](./media/freebsd-create-upload-vhd/storageaccount_detail.png)
7. <span data-ttu-id="49917-176">Seçin **bir kapsayıcı oluşturmak**.</span><span class="sxs-lookup"><span data-stu-id="49917-176">Select **Create a Container**.</span></span>

    ![Depolama hesabı ayrıntısı](./media/freebsd-create-upload-vhd/storageaccount_container.png)
8. <span data-ttu-id="49917-178">Merhaba, **adı** alanında, kapsayıcı için bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="49917-178">In hello **Name** field, type a name for your container.</span></span> <span data-ttu-id="49917-179">Ardından hello **erişim** ne tür istediğiniz erişim ilkesi aşağı açılan menüsünde seçin.</span><span class="sxs-lookup"><span data-stu-id="49917-179">Then, in hello **Access** drop-down menu, select what type of access policy you want.</span></span>

    ![Kapsayıcı adı](./media/freebsd-create-upload-vhd/storageaccount_containervalues.png)

   > [!NOTE]
   > <span data-ttu-id="49917-181">Varsayılan olarak, hello kapsayıcı özeldir ve yalnızca hello hesap sahibi tarafından erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="49917-181">By default, hello container is private and can only be accessed by hello account owner.</span></span> <span data-ttu-id="49917-182">Merhaba kapsayıcı, ancak toohello kapsayıcı özellikleri ve meta verileri, tooallow herkese okuma erişimi toohello BLOB'ları kullanmak hello **ortak Blob** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="49917-182">tooallow public read access toohello blobs in hello container, but not toohello container properties and metadata, use hello **Public Blob** option.</span></span> <span data-ttu-id="49917-183">tooallow tam ortak okuma erişiminin hello kapsayıcı ve bloblarını, kullanımı için hello **ortak kapsayıcı** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="49917-183">tooallow full public read access for hello container and blobs, use hello **Public Container** option.</span></span>
   >
   >

## <a name="step-3-prepare-hello-connection-tooazure"></a><span data-ttu-id="49917-184">3. adım: hello bağlantı tooAzure hazırlama</span><span class="sxs-lookup"><span data-stu-id="49917-184">Step 3: Prepare hello connection tooAzure</span></span>
<span data-ttu-id="49917-185">Bir .vhd dosyası yükleyebilir önce bilgisayarınız ve Azure aboneliğiniz arasında tooestablish güvenli bir bağlantı gerekir.</span><span class="sxs-lookup"><span data-stu-id="49917-185">Before you can upload a .vhd file, you need tooestablish a secure connection between your computer and your Azure subscription.</span></span> <span data-ttu-id="49917-186">Hello Azure Active Directory (Azure AD) yöntemini kullanın veya sertifika yöntemi toodo Merhaba.</span><span class="sxs-lookup"><span data-stu-id="49917-186">You can use hello Azure Active Directory (Azure AD) method or hello certificate method toodo it.</span></span>

### <a name="use-hello-azure-ad-method-tooupload-a-vhd-file"></a><span data-ttu-id="49917-187">Hello Azure AD yöntemi tooupload bir .vhd dosyası kullanın</span><span class="sxs-lookup"><span data-stu-id="49917-187">Use hello Azure AD method tooupload a .vhd file</span></span>
1. <span data-ttu-id="49917-188">Açık hello Azure PowerShell Konsolu.</span><span class="sxs-lookup"><span data-stu-id="49917-188">Open hello Azure PowerShell console.</span></span>
2. <span data-ttu-id="49917-189">Merhaba aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="49917-189">Type hello following command:</span></span>  
    `Add-AzureAccount`

    <span data-ttu-id="49917-190">Bu komut, bir oturum açma penceresi burada iş veya Okul hesabınızla oturum açar.</span><span class="sxs-lookup"><span data-stu-id="49917-190">This command opens a sign-in window where you can sign in with your work or school account.</span></span>

    ![PowerShell penceresi](./media/freebsd-create-upload-vhd/add_azureaccount.png)
3. <span data-ttu-id="49917-192">Azure kimliğini doğrular ve hello kimlik bilgileri kaydeder.</span><span class="sxs-lookup"><span data-stu-id="49917-192">Azure authenticates and saves hello credential information.</span></span> <span data-ttu-id="49917-193">Ardından hello penceresini kapatır.</span><span class="sxs-lookup"><span data-stu-id="49917-193">Then it closes hello window.</span></span>

### <a name="use-hello-certificate-method-tooupload-a-vhd-file"></a><span data-ttu-id="49917-194">Merhaba sertifika yöntemi tooupload bir .vhd dosyası kullanın</span><span class="sxs-lookup"><span data-stu-id="49917-194">Use hello certificate method tooupload a .vhd file</span></span>
1. <span data-ttu-id="49917-195">Açık hello Azure PowerShell Konsolu.</span><span class="sxs-lookup"><span data-stu-id="49917-195">Open hello Azure PowerShell console.</span></span>
2. <span data-ttu-id="49917-196">Tür: `Get-AzurePublishSettingsFile`.</span><span class="sxs-lookup"><span data-stu-id="49917-196">Type:  `Get-AzurePublishSettingsFile`.</span></span>
3. <span data-ttu-id="49917-197">Bir tarayıcı penceresi açar ve, toodownload hello .publishsettings dosyasını ister.</span><span class="sxs-lookup"><span data-stu-id="49917-197">A browser window opens and prompts you toodownload hello .publishsettings file.</span></span> <span data-ttu-id="49917-198">Bu dosya bilgileri ve Azure aboneliğiniz için bir sertifika içerir.</span><span class="sxs-lookup"><span data-stu-id="49917-198">This file contains information and a certificate for your Azure subscription.</span></span>

    ![Tarayıcı indirme sayfası](./media/freebsd-create-upload-vhd/Browser_download_GetPublishSettingsFile.png)
4. <span data-ttu-id="49917-200">Merhaba .publishsettings dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="49917-200">Save hello .publishsettings file.</span></span>
5. <span data-ttu-id="49917-201">Tür: `Import-AzurePublishSettingsFile <PathToFile>`, burada `<PathToFile>` hello tam yolu toohello .publishsettings dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="49917-201">Type:  `Import-AzurePublishSettingsFile <PathToFile>`, where `<PathToFile>` is hello full path toohello .publishsettings file.</span></span>

   <span data-ttu-id="49917-202">Daha fazla bilgi için bkz: [Azure cmdlet'leri kullanmaya başlama](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).</span><span class="sxs-lookup"><span data-stu-id="49917-202">For more information, see [Get started with Azure cmdlets](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).</span></span>

   <span data-ttu-id="49917-203">Yükleme ve PowerShell yapılandırma hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="49917-203">For more information about installing and configuring PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="step-4-upload-hello-vhd-file"></a><span data-ttu-id="49917-204">4. adım: hello .vhd dosyasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="49917-204">Step 4: Upload hello .vhd file</span></span>
<span data-ttu-id="49917-205">İçinde Blob Depolama alanınızın hello .vhd dosyasını karşıya yüklediğinde, herhangi bir yere yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49917-205">When you upload hello .vhd file, you can place it anywhere within your Blob storage.</span></span> <span data-ttu-id="49917-206">Merhaba dosyasını karşıya yüklediğinde kullanacağınız bazı şartları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="49917-206">Following are some terms you will use when you upload hello file:</span></span>

* <span data-ttu-id="49917-207">**BlobStorageURL** 2. adımda oluşturduğunuz hello depolama hesabı için hello URL'dir.</span><span class="sxs-lookup"><span data-stu-id="49917-207">**BlobStorageURL** is hello URL for hello storage account that you created in Step 2.</span></span>
* <span data-ttu-id="49917-208">**YourImagesFolder** hello Blob storage içinde istediğiniz yere toostore görüntülerinizi kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="49917-208">**YourImagesFolder** is hello container within Blob storage where you want toostore your images.</span></span>
* <span data-ttu-id="49917-209">**VHDName** hello Azure Klasik portalı tooidentify hello sanal sabit disk görünen hello etiket.</span><span class="sxs-lookup"><span data-stu-id="49917-209">**VHDName** is hello label that appears in hello Azure classic portal tooidentify hello virtual hard disk.</span></span>
* <span data-ttu-id="49917-210">**PathToVHDFile** hello .vhd dosyası hello tam yolu ve adıdır.</span><span class="sxs-lookup"><span data-stu-id="49917-210">**PathToVHDFile** is hello full path and name of hello .vhd file.</span></span>

<span data-ttu-id="49917-211">Merhaba önceki adımda kullanılan hello Azure PowerShell penceresinden yazın:</span><span class="sxs-lookup"><span data-stu-id="49917-211">From hello Azure PowerShell window you used in hello previous step, type:</span></span>

        Add-AzureVhd -Destination "<BlobStorageURL>/<YourImagesFolder>/<VHDName>.vhd" -LocalFilePath <PathToVHDFile>

## <a name="step-5-create-a-vm-with-hello-uploaded-vhd-file"></a><span data-ttu-id="49917-212">5. adım: hello karşıya yüklenen .vhd dosyası bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="49917-212">Step 5: Create a VM with hello uploaded .vhd file</span></span>
<span data-ttu-id="49917-213">Merhaba .vhd dosyası yükledikten sonra aboneliğinizle ilişkili olan ve bu özel görüntü ile bir sanal makine oluşturmak özel görüntülerin görüntü toohello listesi olarak ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="49917-213">After you upload hello .vhd file, you can add it as an image toohello list of custom images that are associated with your subscription and create a virtual machine with this custom image.</span></span>

1. <span data-ttu-id="49917-214">Merhaba önceki adımda kullanılan hello Azure PowerShell penceresinden yazın:</span><span class="sxs-lookup"><span data-stu-id="49917-214">From hello Azure PowerShell window you used in hello previous step, type:</span></span>

        Add-AzureVMImage -ImageName <Your Image's Name> -MediaLocation <location of hello VHD> -OS <Type of hello OS on hello VHD>

   > [!NOTE]
   > <span data-ttu-id="49917-215">Linux hello işletim sistemi türü olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="49917-215">Use Linux as hello OS type.</span></span> <span data-ttu-id="49917-216">Merhaba geçerli Azure PowerShell sürümü yalnızca "Linux" veya "Windows" parametre olarak kabul eder.</span><span class="sxs-lookup"><span data-stu-id="49917-216">hello current Azure PowerShell version accepts only “Linux” or “Windows” as a parameter.</span></span>
   >
   >
2. <span data-ttu-id="49917-217">Merhaba yukarıdaki adımları tamamladıktan sonra hello seçtiğinizde hello yeni görüntü listelenir **görüntüleri** hello Klasik Azure portalı sekmesinde.</span><span class="sxs-lookup"><span data-stu-id="49917-217">After you complete hello previous steps, hello new image is listed when you choose hello **Images** tab on hello Azure classic portal.</span></span>  

    ![Bir görüntü seçin](./media/freebsd-create-upload-vhd/addfreebsdimage.png)
3. <span data-ttu-id="49917-219">Bir sanal makine hello Galerisi'nden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="49917-219">Create a virtual machine from hello gallery.</span></span> <span data-ttu-id="49917-220">Bu yeni görüntüyü artık altında kullanılabilir **görüntülerim**.</span><span class="sxs-lookup"><span data-stu-id="49917-220">This new image is now available under **My Images**.</span></span>
4. <span data-ttu-id="49917-221">Merhaba yeni görüntüyü seçin.</span><span class="sxs-lookup"><span data-stu-id="49917-221">Select hello new image.</span></span> <span data-ttu-id="49917-222">Ardından, bir ana bilgisayar adı, parola, SSH anahtarı ve benzeri hello istemleri tooset geçer.</span><span class="sxs-lookup"><span data-stu-id="49917-222">Next, go through hello prompts tooset up a host name, password, SSH key, and so on.</span></span>

    ![Özel görüntü](./media/freebsd-create-upload-vhd/createfreebsdimageinazure.png)
5. <span data-ttu-id="49917-224">Merhaba sağlama tamamladıktan sonra Azure'da çalışan FreeBSD VM görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="49917-224">After you complete hello provisioning, you'll see your FreeBSD VM running in Azure.</span></span>

    ![Azure FreeBSD görüntüde](./media/freebsd-create-upload-vhd/freebsdimageinazure.png)
