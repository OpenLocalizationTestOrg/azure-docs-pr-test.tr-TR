---
title: "aaaDeploy bir Node.js uygulaması tooLinux azure'da sanal makineler"
description: "Bilgi nasıl toodeploy bir Node.js uygulaması tooLinux sanal makineleri azure'da."
services: 
documentationcenter: nodejs
author: stepro
manager: dmitryr
editor: 
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: /azure
ms.assetid: 857a812d-c73e-4af7-a985-2d0baf8b6f71
ms.service: multiple
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2016
ms.author: stephpr
ms.openlocfilehash: e876c8170a06f102f7f32ec7cb930b876647a707
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-nodejs-application-toolinux-virtual-machines-in-azure"></a><span data-ttu-id="557fe-103">Bir Node.js uygulaması tooLinux azure'da sanal makineler dağıtma</span><span class="sxs-lookup"><span data-stu-id="557fe-103">Deploy a Node.js application tooLinux Virtual Machines in Azure</span></span>
<span data-ttu-id="557fe-104">Bu öğreticide gösterilmiştir nasıl tootake bir Node.js uygulaması ve Azure üzerinde çalışan tooLinux sanal makineler dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="557fe-104">This tutorial shows how tootake a Node.js application and deploy it tooLinux virtual machines running in Azure.</span></span> <span data-ttu-id="557fe-105">Bu öğreticide Hello yönergeler Node.js çalıştırabilen tüm işletim sisteminde izlenebilir.</span><span class="sxs-lookup"><span data-stu-id="557fe-105">hello instructions in this tutorial can be followed on any operating system that is capable of running Node.js.</span></span>

<span data-ttu-id="557fe-106">Bilgi edineceksiniz nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="557fe-106">You'll learn how to:</span></span>

* <span data-ttu-id="557fe-107">Çatalı ve kopya basit bir Yapılacaklar uygulamasının içeren GitHub deposunu;</span><span class="sxs-lookup"><span data-stu-id="557fe-107">Fork and clone a GitHub repository containing a simple TODO application;</span></span>
* <span data-ttu-id="557fe-108">Oluşturma ve Azure toorun hello uygulamada iki Linux sanal makineleri yapılandırma;</span><span class="sxs-lookup"><span data-stu-id="557fe-108">Create and configure two Linux virtual machines in Azure toorun hello application;</span></span>
* <span data-ttu-id="557fe-109">Merhaba uygulama güncelleştirmeleri toohello web ön uç sanal makine ileterek yineleme.</span><span class="sxs-lookup"><span data-stu-id="557fe-109">Iterate on hello application by pushing updates toohello web frontend virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="557fe-110">toocomplete Bu öğretici, GitHub hesabı ve Microsoft Azure hesabı gerekiyor ve geliştirme makineden özelliği toouse Git hello.</span><span class="sxs-lookup"><span data-stu-id="557fe-110">toocomplete this tutorial, you need a GitHub account and a Microsoft Azure account, and hello ability toouse Git from a development machine.</span></span>
> 
> <span data-ttu-id="557fe-111">GitHub hesabı yoksa, kaydolabilirsiniz [burada](https://github.com/join).</span><span class="sxs-lookup"><span data-stu-id="557fe-111">If you don't have a GitHub account, you can sign up [here](https://github.com/join).</span></span>
> 
> <span data-ttu-id="557fe-112">Yoksa bir [Microsoft Azure](https://azure.microsoft.com/) hesabına kaydolabilirsiniz ücretsiz deneme için [burada](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="557fe-112">If you don't have a [Microsoft Azure](https://azure.microsoft.com/) account, you can sign up for a FREE trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="557fe-113">Bu ayrıca, hello kaydolma işlemini için kılavuzluk eder bir [Microsoft Account](http://account.microsoft.com) , zaten bir yoksa.</span><span class="sxs-lookup"><span data-stu-id="557fe-113">This will also lead you through hello sign up process for a [Microsoft Account](http://account.microsoft.com) if you do not already have one.</span></span> <span data-ttu-id="557fe-114">Visual Studio abone varsa, dilerseniz [MSDN Avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="557fe-114">Alternatively, if you are a Visual Studio subscriber, you can [activate your MSDN benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="557fe-115">Geliştirme makinenizde git yoksa Macintosh veya Windows makine kullanıyorsanız, ardından üzerinden yükleyin [burada](http://www.git-scm.com).</span><span class="sxs-lookup"><span data-stu-id="557fe-115">If you do not have git on your development machine, then if you are using a Macintosh or Windows machine, install git from [here](http://www.git-scm.com).</span></span> <span data-ttu-id="557fe-116">Linux kullanıyorsanız, sizin için en uygun hello mekanizması kullanılarak Git'i yükleyin `sudo apt-get install git`.</span><span class="sxs-lookup"><span data-stu-id="557fe-116">If you are using Linux, install git using hello mechanism most appropriate for you, such as `sudo apt-get install git`.</span></span>
> 
> 

## <a name="forking-and-cloning-hello-todo-application"></a><span data-ttu-id="557fe-117">Forking ve hello TODO uygulaması kopyalama</span><span class="sxs-lookup"><span data-stu-id="557fe-117">Forking and Cloning hello TODO Application</span></span>
<span data-ttu-id="557fe-118">Merhaba TODO uygulaması bu Öğreticisi tarafından kullanılan basit bir web ön uç bir Yapılacaklar listesi ve bir MongoDB örneği uygular.</span><span class="sxs-lookup"><span data-stu-id="557fe-118">hello TODO application used by this tutorial implements a simple web frontend over a MongoDB instance that keeps track of a TODO list.</span></span> <span data-ttu-id="557fe-119">İçinde tooGitHub oturum sonra Git [burada](https://github.com/stepro/node-todo) toofind hello uygulama ve sağ hello üst hello bağlantısı kullanarak çatallaştırma.</span><span class="sxs-lookup"><span data-stu-id="557fe-119">After signing in tooGitHub, go [here](https://github.com/stepro/node-todo) toofind hello application and fork it using hello link in hello top right.</span></span> <span data-ttu-id="557fe-120">Bu depo adlı hesabınızı oluşturmalısınız *accountname*/node-todo.</span><span class="sxs-lookup"><span data-stu-id="557fe-120">This should create a repository in your account named *accountname*/node-todo.</span></span>

<span data-ttu-id="557fe-121">Şimdi, geliştirme makinenizde bu depoyu kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="557fe-121">Now on your development machine, clone this repository:</span></span>

    git clone https://github.com/accountname/node-todo.git

<span data-ttu-id="557fe-122">Bu yerel bir kopya hello havuzun biraz daha sonra toohello kaynak kodu değişiklik yaparken kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="557fe-122">We'll use this local clone of hello repository a little later when making changes toohello source code.</span></span>

## <a name="creating-and-configuring-hello-linux-virtual-machines"></a><span data-ttu-id="557fe-123">Oluşturma ve hello Linux sanal makineleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="557fe-123">Creating and Configuring hello Linux Virtual Machines</span></span>
<span data-ttu-id="557fe-124">Azure Linux sanal makineleri kullanarak ham işlem için harika bir desteğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="557fe-124">Azure has great support for raw compute using Linux virtual machines.</span></span> <span data-ttu-id="557fe-125">Bu bölümü nasıl kolayca iki Linux sanal makineleri Döndür ve dağıtma hello TODO uygulaması toothem, tek ve hello hello diğer MongoDB örneğinde çalışan hello web ön uç hello öğretici gösterir.</span><span class="sxs-lookup"><span data-stu-id="557fe-125">This part of hello tutorial shows how you can easily spin up two Linux virtual machines and deploy hello TODO application toothem, running hello web frontend on one and hello MongoDB instance on hello other.</span></span>

### <a name="creating-virtual-machines"></a><span data-ttu-id="557fe-126">Sanal makineler oluşturma</span><span class="sxs-lookup"><span data-stu-id="557fe-126">Creating Virtual Machines</span></span>
<span data-ttu-id="557fe-127">Merhaba en kolay yolu toocreate azure'da yeni bir sanal makine toouse hello Azure Portal ' dir.</span><span class="sxs-lookup"><span data-stu-id="557fe-127">hello easiest way toocreate a new virtual machine in Azure is toouse hello Azure Portal.</span></span> <span data-ttu-id="557fe-128">Tıklatın [burada](https://portal.azure.com) içinde toosign ve başlatma hello Azure Portal, web tarayıcınızda.</span><span class="sxs-lookup"><span data-stu-id="557fe-128">Click [here](https://portal.azure.com) toosign in and launch hello Azure Portal in your web browser.</span></span> <span data-ttu-id="557fe-129">Hello Azure portalı yüklendikten sonra hello aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="557fe-129">Once hello Azure Portal has loaded, complete hello following steps:</span></span>

* <span data-ttu-id="557fe-130">Merhaba "+ Yeni"'i tıklatın bağlantı;</span><span class="sxs-lookup"><span data-stu-id="557fe-130">Click hello "+ New" link;</span></span>
* <span data-ttu-id="557fe-131">"İşlem" Merhaba kategori seçin ve "Ubuntu Server 14.04 LTS"; seçin</span><span class="sxs-lookup"><span data-stu-id="557fe-131">Pick hello "Compute" category and choose "Ubuntu Server 14.04 LTS";</span></span>
* <span data-ttu-id="557fe-132">Merhaba "Resource Manager" dağıtım modelini seçin ve "Oluştur";'ı tıklatın</span><span class="sxs-lookup"><span data-stu-id="557fe-132">Select hello "Resource Manager" deployment model and click "Create";</span></span>
* <span data-ttu-id="557fe-133">Bu yönergeleri izleyerek hello temel bilgileri doldurun:</span><span class="sxs-lookup"><span data-stu-id="557fe-133">Fill in hello basics following these guidelines:</span></span>
  * <span data-ttu-id="557fe-134">Daha sonra kolayca tanıyacak bir ad belirtin;</span><span class="sxs-lookup"><span data-stu-id="557fe-134">Specify a name you can easily identify later;</span></span>
  * <span data-ttu-id="557fe-135">Bu öğretici için parola kimlik doğrulaması seçin;</span><span class="sxs-lookup"><span data-stu-id="557fe-135">For this tutorial, choose Password authentication;</span></span>
  * <span data-ttu-id="557fe-136">Tanımlanabilen bir ad ile yeni bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="557fe-136">Create a new resource group with an identifiable name.</span></span>
* <span data-ttu-id="557fe-137">Merhaba sanal makine boyutu "A1" makul bir seçim Bu öğretici için standarttır.</span><span class="sxs-lookup"><span data-stu-id="557fe-137">For hello Virtual Machine size, "A1 Standard" is a reasonable choice for this tutorial.</span></span>
* <span data-ttu-id="557fe-138">Ek ayarları için "Standard" Merhaba disk türü olduğundan emin olun ve tüm kalan Varsayılanları hello kabul edin.</span><span class="sxs-lookup"><span data-stu-id="557fe-138">For additional settings, ensure hello disk type is "Standard" and accept all hello remaining defaults.</span></span>
* <span data-ttu-id="557fe-139">Merhaba Özet sayfasında hello oluşturma devre dışı tetiklersiniz.</span><span class="sxs-lookup"><span data-stu-id="557fe-139">Kick off hello creation on hello summary page.</span></span>

<span data-ttu-id="557fe-140">Yukarıdaki Hello gerçekleştirmek iki kez toocreate iki Linux sanal makineleri, hello web ön uç için diğeri hello MongoDB örneği için işlem.</span><span class="sxs-lookup"><span data-stu-id="557fe-140">Perform hello above process twice toocreate two Linux virtual machines, one for hello web frontend and one for hello MongoDB instance.</span></span> <span data-ttu-id="557fe-141">Merhaba sanal makinelerin oluşturulmasını yaklaşık 5-10 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="557fe-141">Creation of hello virtual machines will take about 5-10 minutes.</span></span>

### <a name="assigning-a-dns-entry-for-virtual-machines"></a><span data-ttu-id="557fe-142">Sanal makineler için bir DNS girişi atama</span><span class="sxs-lookup"><span data-stu-id="557fe-142">Assigning a DNS entry for Virtual Machines</span></span>
<span data-ttu-id="557fe-143">Varsayılan olarak yalnızca erişilebilir bir ortak IP adresi 1.2.3.4 gibi Azure üzerinde oluşturulan sanal makineler var.</span><span class="sxs-lookup"><span data-stu-id="557fe-143">Virtual machines created in Azure are by default only accessible through a public IP address like 1.2.3.4.</span></span> <span data-ttu-id="557fe-144">Merhaba makineler daha kolayca tanımlanabilen DNS girişlerini atayarak olalım.</span><span class="sxs-lookup"><span data-stu-id="557fe-144">Let's make hello machines more easily identifiable by assigning them DNS entries.</span></span>

<span data-ttu-id="557fe-145">Merhaba sanal makine oluşturulmadı Hello portal gösterir sonra hello sol gezinti çubuğu hello "Sanal makineler" bağlantısını tıklatın ve makinelerinizi bulun.</span><span class="sxs-lookup"><span data-stu-id="557fe-145">Once hello portal indicates that hello virtual machines have been created, click on hello "Virtual machines" link in hello left navbar and locate your machines.</span></span> <span data-ttu-id="557fe-146">Her makine için:</span><span class="sxs-lookup"><span data-stu-id="557fe-146">For each machine:</span></span>

* <span data-ttu-id="557fe-147">Merhaba temel bilgiler sekmesinde bulun ve genel IP adresi hello üzerinde tıklatın;</span><span class="sxs-lookup"><span data-stu-id="557fe-147">Locate hello Essentials tab and click on hello Public IP Address;</span></span>
* <span data-ttu-id="557fe-148">Merhaba ortak IP adresi yapılandırması, bir DNS ad etiketi atayın ve kaydedin.</span><span class="sxs-lookup"><span data-stu-id="557fe-148">In hello public IP address configuration, assign a DNS name label and save.</span></span>

<span data-ttu-id="557fe-149">Merhaba portal belirttiğiniz hello adı kullanılabilir güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="557fe-149">hello portal will ensure that hello name you specify is available.</span></span> <span data-ttu-id="557fe-150">Merhaba yapılandırma kaydedildikten sonra sanal makinelerinizi ana bilgisayar adları benzer çok olacaktır`machinename.region.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="557fe-150">After saving hello configuration, your virtual machines will have host names similar too`machinename.region.cloudapp.azure.com`.</span></span>

### <a name="connecting-toohello-virtual-machines"></a><span data-ttu-id="557fe-151">Bağlantı toohello sanal makineler</span><span class="sxs-lookup"><span data-stu-id="557fe-151">Connecting toohello Virtual Machines</span></span>
<span data-ttu-id="557fe-152">Sanal makinelerinizi sağlanan, SSH üzerinden önceden yapılandırılmış tooallow uzak bağlantıları yoktu.</span><span class="sxs-lookup"><span data-stu-id="557fe-152">When your virtual machines were provisioned, they were pre-configured tooallow remote connections over SSH.</span></span> <span data-ttu-id="557fe-153">Bu tooconfigure hello sanal makineleri kullanacağız hello mekanizmadır.</span><span class="sxs-lookup"><span data-stu-id="557fe-153">This is hello mechanism we will use tooconfigure hello virtual machines.</span></span> <span data-ttu-id="557fe-154">Windows için geliştirme kullanıyorsanız, zaten bir yoksa tooget bir SSH istemcisi gerekir.</span><span class="sxs-lookup"><span data-stu-id="557fe-154">If you are using Windows for your development, you will need tooget an SSH client if you do not already have one.</span></span> <span data-ttu-id="557fe-155">Bir ortak burada yüklenebilir PuTTY seçimdir [burada](http://www.chiark.greenend.org.uk/~sgtatham/putty/).</span><span class="sxs-lookup"><span data-stu-id="557fe-155">A common choice here is PuTTY, which can be downloaded from [here](http://www.chiark.greenend.org.uk/~sgtatham/putty/).</span></span> <span data-ttu-id="557fe-156">Macintosh ve Linux İşletim Sistemleri'ni SSH önceden yüklenmiş bir sürümü ile gelir.</span><span class="sxs-lookup"><span data-stu-id="557fe-156">Macintosh and Linux OSes come with a version of SSH pre-installed.</span></span>

### <a name="configuring-hello-web-frontend-virtual-machine"></a><span data-ttu-id="557fe-157">Merhaba Web ön uç sanal makine yapılandırma</span><span class="sxs-lookup"><span data-stu-id="557fe-157">Configuring hello Web Frontend Virtual Machine</span></span>
<span data-ttu-id="557fe-158">PuTTY, ssh komut satırı veya, diğer sık kullanılan SSH aracını kullanarak oluşturduğunuz SSH toohello web ön uç makine.</span><span class="sxs-lookup"><span data-stu-id="557fe-158">SSH toohello web frontend machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="557fe-159">Bir komut istemi tarafından izlenen bir Hoş Geldiniz iletisi görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="557fe-159">You should see a welcome message followed by a command prompt.</span></span>

<span data-ttu-id="557fe-160">İlk olarak, şirketinizdeki git ve düğüm hem yüklendiğinden emin olun:</span><span class="sxs-lookup"><span data-stu-id="557fe-160">First, let's make sure that git and node are both installed:</span></span>

    sudo apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get install -y nodejs

<span data-ttu-id="557fe-161">Hello uygulamanın web ön uç yerel bazı Node.js modülleri kullandığından, biz de tooinstall hello temel kümesi derleme araçları gerekir:</span><span class="sxs-lookup"><span data-stu-id="557fe-161">Since hello application's web frontend relies on some native Node.js modules, we also need tooinstall hello essential set of build tools:</span></span>

    sudo apt-get install -y build-essential

<span data-ttu-id="557fe-162">Son olarak, şimdi adlı bir Node.js uygulamasını yüklemek *sonsuza kadar*, toorun Node.js sunucu uygulamaları yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="557fe-162">Finally, let's install a Node.js application called *forever*, which helps toorun Node.js server applications:</span></span>

    sudo npm install -g forever

<span data-ttu-id="557fe-163">Bu sanal makine toobe mümkün toorun hello uygulamanın web ön uç üzerinde gerekli tüm hello bağımlılıkları bunlar, sağlandığından çalıştıran Al.</span><span class="sxs-lookup"><span data-stu-id="557fe-163">These are all hello dependencies needed on this virtual machine toobe able toorun hello application's web frontend, so let's get that running.</span></span> <span data-ttu-id="557fe-164">toodo Bu, ilk olarak, daha önce çatallanmış kolayca güncelleştirmeleri toohello sanal makine (biz kapsayan bu güncelleştirme senaryo daha sonra) yayımlama ve hello tam kopya tooprovide kopyalama hello GitHub deposunu tam bir kopyasını hello sürümünü oluşturacağız gerçekte yürütülebilir deposu.</span><span class="sxs-lookup"><span data-stu-id="557fe-164">toodo this, we will first create a bare clone of hello GitHub repository you previously forked so that you can easily publish updates toohello virtual machine (we'll cover this update scenario later), and then clone hello bare clone tooprovide a version of hello repository that can actually be executed.</span></span>

<span data-ttu-id="557fe-165">Merhaba giriş (~) dizininden başlayarak, aşağıdaki komutları hello çalıştırın (değiştirme *accountname* GitHub kullanıcı hesabı adı ile):</span><span class="sxs-lookup"><span data-stu-id="557fe-165">Starting from hello home (~) directory, run hello following commands (replacing *accountname* with your GitHub user account name):</span></span>

    git clone --bare https://github.com/accountname/node-todo.git
    git clone node-todo.git

<span data-ttu-id="557fe-166">Şimdi hello düğümü Yapılacaklar dizini girin ve bu komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="557fe-166">Now enter hello node-todo directory and run these commands:</span></span>

    npm install
    forever start server.js

<span data-ttu-id="557fe-167">Merhaba uygulamanın web ön uç şu anda çalışıyor, ancak bir adım daha hello uygulama bir web tarayıcısından erişmeden önce.</span><span class="sxs-lookup"><span data-stu-id="557fe-167">hello application's web frontend is now running, however there is one more step before you can access hello application from a web browser.</span></span> <span data-ttu-id="557fe-168">Merhaba, oluşturduğunuz sanal makine adlı bir Azure kaynağı tarafından korunan bir *ağ güvenlik grubu*, sağladığınız olduğunda hello sanal makine için oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="557fe-168">hello virtual machine you created is protected by an Azure resource called a *network security group*, which was created for you when you provisioned hello virtual machine.</span></span> <span data-ttu-id="557fe-169">Şu anda, bu kaynak yalnızca dış istekleri tooport yönlendirilen 22 toobe toohello sanal hello makine ancak hiçbir şey bilgisayarla SSH iletişimi sağlayan makine izin verir.</span><span class="sxs-lookup"><span data-stu-id="557fe-169">Currently, this resource only allows external requests tooport 22 toobe routed toohello virtual machine, which enables SSH communication with hello machine but nothing else.</span></span> <span data-ttu-id="557fe-170">Bu nedenle Sipariş tooview hello bağlantı noktası 8080 üzerinde yapılandırılmış toorun olan TODO uygulaması bu bağlantı noktası açılan toobe da gerekir.</span><span class="sxs-lookup"><span data-stu-id="557fe-170">So in order tooview hello TODO application, which is configured toorun on port 8080, this port also needs toobe opened up.</span></span>

<span data-ttu-id="557fe-171">Toohello Azure portalına dönün ve hello aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="557fe-171">Return toohello Azure Portal and complete hello following steps:</span></span>

* <span data-ttu-id="557fe-172">"Kaynak grubunda" Merhaba sol gezinti çubuğu; tıklayın</span><span class="sxs-lookup"><span data-stu-id="557fe-172">Click on "Resource groups" in hello left navbar;</span></span>
* <span data-ttu-id="557fe-173">Sanal makineniz içeren hello kaynak grubunu seçin;</span><span class="sxs-lookup"><span data-stu-id="557fe-173">Select hello resource group that contains your virtual machine;</span></span>
* <span data-ttu-id="557fe-174">Merhaba elde edilen listede kaynakların hello ağ güvenlik grubu (Merhaba bir kalkan simgesi ile); seçin</span><span class="sxs-lookup"><span data-stu-id="557fe-174">In hello resulting list of resources, select hello network security group (hello one with a shield icon);</span></span>
* <span data-ttu-id="557fe-175">"Gelen güvenlik kuralları"; Hello özelliklerinde seçin</span><span class="sxs-lookup"><span data-stu-id="557fe-175">In hello properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="557fe-176">Merhaba araç çubuğunda, ""; Ekle</span><span class="sxs-lookup"><span data-stu-id="557fe-176">In hello toolbar, click "Add";</span></span>
* <span data-ttu-id="557fe-177">"Varsayılan-izin ver-todo"; gibi bir ad sağlayın</span><span class="sxs-lookup"><span data-stu-id="557fe-177">Provide a name like "default-allow-todo";</span></span>
* <span data-ttu-id="557fe-178">Merhaba protokolü çok Ayarla "TCP";</span><span class="sxs-lookup"><span data-stu-id="557fe-178">Set hello protocol too"TCP";</span></span>
* <span data-ttu-id="557fe-179">Ayarlama hello hedef bağlantı noktası aralığı çok "8080";</span><span class="sxs-lookup"><span data-stu-id="557fe-179">Set hello destination port range too"8080";</span></span>
* <span data-ttu-id="557fe-180">Tamam'ı tıklatın ve hello güvenlik kuralı toobe oluşturulan için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="557fe-180">Click OK and wait for hello security rule toobe created.</span></span>

<span data-ttu-id="557fe-181">Bu güvenlik kuralı oluşturduktan sonra hello TODO uygulaması üzerinde herkese görünür Internet hello ve örneği için bir URL gibi kullanarak tooit, göz atabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="557fe-181">After creating this security rule, hello TODO application is publically visible on hello internet and you can browse tooit, for instance using a URL such as:</span></span>

    http://machinename.region.cloudapp.azure.com:8080

<span data-ttu-id="557fe-182">Biz henüz hello MongoDB sanal makine yapılandırmadınız olsa bile, hello TODO uygulaması toobe oldukça işlevsel göründüğünü fark edeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="557fe-182">You will notice that even though we have not yet configured hello MongoDB virtual machine, hello TODO application appears toobe quite functional.</span></span> <span data-ttu-id="557fe-183">Merhaba kaynak deposu sabit kodlanmış toouse önceden dağıtılan bir MongoDB örneği olmasıdır.</span><span class="sxs-lookup"><span data-stu-id="557fe-183">This is because hello source repository is hardcoded toouse a pre-deployed MongoDB instance.</span></span> <span data-ttu-id="557fe-184">Biz hello MongoDB sanal makine yapılandırdıktan sonra biz geri dönün ve bunun yerine özel bizim MongoDB örneği hello kaynak kodu tooutilize değiştirin.</span><span class="sxs-lookup"><span data-stu-id="557fe-184">Once we have configured hello MongoDB virtual machine, we will go back and change hello source code tooutilize our private MongoDB instance instead.</span></span>

### <a name="configuring-hello-mongodb-virtual-machine"></a><span data-ttu-id="557fe-185">Merhaba MongoDB sanal makine yapılandırma</span><span class="sxs-lookup"><span data-stu-id="557fe-185">Configuring hello MongoDB Virtual Machine</span></span>
<span data-ttu-id="557fe-186">PuTTY, ssh komut satırı veya, diğer sık kullanılan SSH aracını kullanarak oluşturduğunuz SSH toohello ikinci makine.</span><span class="sxs-lookup"><span data-stu-id="557fe-186">SSH toohello second machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="557fe-187">Merhaba Hoş Geldiniz iletisi ve komut istemi gördükten sonra MongoDB yükleyin (Bu yönergeleri gelen gerçekleştirilen [burada](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span><span class="sxs-lookup"><span data-stu-id="557fe-187">After seeing hello welcome message and command prompt, install MongoDB (these instructions were taken from [here](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span></span>

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
    echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
    sudo apt-get update
    sudo apt-get install -y mongodb-org

<span data-ttu-id="557fe-188">Varsayılan olarak, yalnızca de yerel olarak erişilen MongoDB yapılandırıldığından.</span><span class="sxs-lookup"><span data-stu-id="557fe-188">By default, MongoDB is configured so it can only be accessed locally.</span></span> <span data-ttu-id="557fe-189">Merhaba uygulamanın sanal makineden erişilebilmeleri adına Bu öğreticide, biz MongoDB yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="557fe-189">For this tutorial, we will configure MongoDB so it can be accessed from hello application's virtual machine.</span></span> <span data-ttu-id="557fe-190">Sudo bağlamda hello /etc/mongod.conf dosyasını açın ve hello bulun `# network interfaces` bölümü.</span><span class="sxs-lookup"><span data-stu-id="557fe-190">In a sudo context, open hello /etc/mongod.conf file and locate hello `# network interfaces` section.</span></span> <span data-ttu-id="557fe-191">Değişiklik hello `net.bindIp` yapılandırma değeri çok`0.0.0.0`.</span><span class="sxs-lookup"><span data-stu-id="557fe-191">Change hello `net.bindIp` configuration value too`0.0.0.0`.</span></span>

> [!NOTE]
> <span data-ttu-id="557fe-192">Bu yapılandırma yalnızca bu öğreticinin hello amacıyla kullanılır.</span><span class="sxs-lookup"><span data-stu-id="557fe-192">This configuration is for hello purposes of this tutorial only.</span></span> <span data-ttu-id="557fe-193">Bu **değil** bir güvenlik uygulaması önerilen ve üretim ortamlarında kullanılmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="557fe-193">It is **NOT** a recommended security practice and should not be used in production environments.</span></span>
> 
> 

<span data-ttu-id="557fe-194">Şimdi hello MongoDB hizmetinin başlatıldığından emin olun:</span><span class="sxs-lookup"><span data-stu-id="557fe-194">Now ensure hello MongoDB service has been started:</span></span>

    sudo service mongod restart

<span data-ttu-id="557fe-195">Varsayılan olarak bağlantı noktası 27017 üzerinden MongoDB çalışır.</span><span class="sxs-lookup"><span data-stu-id="557fe-195">MongoDB operates over port 27017 by default.</span></span> <span data-ttu-id="557fe-196">Biz tooopen gerektiği şekilde Hello bağlantı noktası şekilde hello web ön uç sanal makineye, 8080 hello MongoDB sanal makineye tooopen bağlantı noktası 27017 ihtiyacımız.</span><span class="sxs-lookup"><span data-stu-id="557fe-196">So, in hello same way that we needed tooopen port 8080 on hello web frontend virtual machine, we need tooopen port 27017 on hello MongoDB virtual machine.</span></span>

<span data-ttu-id="557fe-197">Toohello Azure portalına dönün ve hello aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="557fe-197">Return toohello Azure Portal and complete hello following steps:</span></span>

* <span data-ttu-id="557fe-198">"Kaynak grubunda" Merhaba sol gezinti çubuğu; tıklayın</span><span class="sxs-lookup"><span data-stu-id="557fe-198">Click on "Resource groups" in hello left navbar;</span></span>
* <span data-ttu-id="557fe-199">Merhaba MongoDB sanal makineyi içeren hello kaynak grubunu seçin;</span><span class="sxs-lookup"><span data-stu-id="557fe-199">Select hello resource group that contains hello MongoDB virtual machine;</span></span>
* <span data-ttu-id="557fe-200">Hello elde edilen listede kaynakların hello ağ güvenlik grubu (Merhaba bir kalkan simgesi ile) ile aynı toohello MongoDB sanal makine verdiğiniz ad hello seçin;</span><span class="sxs-lookup"><span data-stu-id="557fe-200">In hello resulting list of resources, select hello network security group (hello one with a shield icon) with hello same name that you gave toohello MongoDB virtual machine;</span></span>
* <span data-ttu-id="557fe-201">"Gelen güvenlik kuralları"; Hello özelliklerinde seçin</span><span class="sxs-lookup"><span data-stu-id="557fe-201">In hello properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="557fe-202">Merhaba araç çubuğunda, ""; Ekle</span><span class="sxs-lookup"><span data-stu-id="557fe-202">In hello toolbar, click "Add";</span></span>
* <span data-ttu-id="557fe-203">"Varsayılan-izin ver-mongo"; gibi bir ad sağlayın</span><span class="sxs-lookup"><span data-stu-id="557fe-203">Provide a name like "default-allow-mongo";</span></span>
* <span data-ttu-id="557fe-204">Merhaba protokolü çok Ayarla "TCP";</span><span class="sxs-lookup"><span data-stu-id="557fe-204">Set hello protocol too"TCP";</span></span>
* <span data-ttu-id="557fe-205">Ayarlama hello hedef bağlantı noktası aralığı çok "27017";</span><span class="sxs-lookup"><span data-stu-id="557fe-205">Set hello destination port range too"27017";</span></span>
* <span data-ttu-id="557fe-206">Tamam'ı tıklatın ve hello güvenlik kuralı toobe oluşturulan için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="557fe-206">Click OK and wait for hello security rule toobe created.</span></span>

## <a name="iterating-on-hello-todo-application"></a><span data-ttu-id="557fe-207">TODO uygulaması Hello üzerinde yineleme</span><span class="sxs-lookup"><span data-stu-id="557fe-207">Iterating on hello TODO application</span></span>
<span data-ttu-id="557fe-208">Şu ana kadar biz iki Linux sanal makineleri sağlamış: MongoDB örneği çalıştıran hello uygulamanızın web ön uç ve bir çalıştıran biri.</span><span class="sxs-lookup"><span data-stu-id="557fe-208">So far, we have provisioned two Linux virtual machines: one that is running hello application's web frontend and one that is running a MongoDB instance.</span></span> <span data-ttu-id="557fe-209">Ancak bir sorun oluştu - hello web ön uç gerçekte sağlanan hello MongoDB örneği henüz kullanmıyor.</span><span class="sxs-lookup"><span data-stu-id="557fe-209">But there is a problem - hello web frontend isn't actually using hello provisioned MongoDB instance yet.</span></span> <span data-ttu-id="557fe-210">Şimdi, hello web ön uç kodu toouse güncelleştirerek bir ortam değişkeni sabit kodlanmış bir örnek yerine düzeltin.</span><span class="sxs-lookup"><span data-stu-id="557fe-210">Let's fix that by updating hello web frontend code toouse an environment variable instead of a hard-coded instance.</span></span>

### <a name="changing-hello-todo-application"></a><span data-ttu-id="557fe-211">Merhaba TODO uygulaması değiştirme</span><span class="sxs-lookup"><span data-stu-id="557fe-211">Changing hello TODO application</span></span>
<span data-ttu-id="557fe-212">İlk kopyaladığınız hello düğümü Yapılacaklar deposu, geliştirme makinenizde hello açmak `node-todo/config/database.js` dosya, en sık kullandığınız düzenleyicide ve hello sabit kodlanmış değerinden gibi hello url değeri değiştirmek `mongodb://...` çok`process.env.MONGODB`.</span><span class="sxs-lookup"><span data-stu-id="557fe-212">On your development machine where you first cloned hello node-todo repository, open hello `node-todo/config/database.js` file in your favorite editor and change hello url value from hello hard-coded value like `mongodb://...` too`process.env.MONGODB`.</span></span>

<span data-ttu-id="557fe-213">Değişikliklerinizi kaydetmek ve toohello GitHub ana push:</span><span class="sxs-lookup"><span data-stu-id="557fe-213">Commit your changes and push toohello GitHub master:</span></span>

    git commit -am "Get MongoDB instance from env"
    git push origin master

<span data-ttu-id="557fe-214">Ne yazık ki, bu hello değişiklik toohello web ön uç sanal makine yayımlama değil.</span><span class="sxs-lookup"><span data-stu-id="557fe-214">Unfortunately, this doesn't publish hello change toohello web frontend virtual machine.</span></span> <span data-ttu-id="557fe-215">Birkaç daha fazla değişiklik toothat sanal makine tooenable hello Canlı ortamında hello değişikliklerine hello etkisini hızla gözleyebilirsiniz güncelleştirmeleri yayımlama için basit ancak etkili bir mekanizma olalım.</span><span class="sxs-lookup"><span data-stu-id="557fe-215">Let's make a few more changes toothat virtual machine tooenable a simple but effective mechanism for publishing updates so you can quickly observe hello effect of hello changes in hello live environment.</span></span>

### <a name="configuring-hello-web-frontend-virtual-machine"></a><span data-ttu-id="557fe-216">Merhaba Web ön uç sanal makine yapılandırma</span><span class="sxs-lookup"><span data-stu-id="557fe-216">Configuring hello Web Frontend Virtual Machine</span></span>
<span data-ttu-id="557fe-217">Daha önce hello web ön uç sanal makinede hello düğümü Yapılacaklar deposu tam bir kopyasını biz oluşturduğunuz geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="557fe-217">Recall that we previously created a bare clone of hello node-todo repository on hello web frontend virtual machine.</span></span> <span data-ttu-id="557fe-218">Bu eylem uzak toowhich değişiklikleri gönderilemez yeni bir Git oluşturulan renge.</span><span class="sxs-lookup"><span data-stu-id="557fe-218">It turns out that this action created a new Git remote toowhich changes can be pushed.</span></span> <span data-ttu-id="557fe-219">Ancak, yalnızca toothis uzak Ftp'den oldukça geliştiricilerin kendi kodlarına çalışırken aradığınız hello hızlı yineleme modeli vermez.</span><span class="sxs-lookup"><span data-stu-id="557fe-219">However, simply pushing toothis remote doesn't quite give hello rapid iteration model that developers are looking for when working on their code.</span></span>

<span data-ttu-id="557fe-220">Toobe mümkün toodo olduğundan emin olmak gibi anında toohello uzak bir depo hello sanal makinede ortaya çıktığında Merhaba çalışan TODO uygulaması otomatik olarak güncelleştirilir ne biz olacaktır.</span><span class="sxs-lookup"><span data-stu-id="557fe-220">What we would like toobe able toodo is ensure that when a push toohello remote repository on hello virtual machine occurs, hello running TODO application is automatically updated.</span></span> <span data-ttu-id="557fe-221">Neyse ki, git ile kolay tooachieve budur.</span><span class="sxs-lookup"><span data-stu-id="557fe-221">Fortunately, this is easy tooachieve with git.</span></span>

<span data-ttu-id="557fe-222">Git hello havuzda alınan belirli zamanlarda tooreact tooactions adresindeki adlı kancaları sayısını kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="557fe-222">Git exposes a number of hooks that are called at particular times tooreact tooactions taken on hello repository.</span></span> <span data-ttu-id="557fe-223">Bunlar hello deponun içinde Kabuk komut dosyalarını kullanarak belirtilen `hooks` klasör.</span><span class="sxs-lookup"><span data-stu-id="557fe-223">These are specified using shell scripts in hello repository's `hooks` folder.</span></span> <span data-ttu-id="557fe-224">Merhaba otomatik güncelleştirme senaryo için en uygun hello kanca olduğu hello `post-update` olay.</span><span class="sxs-lookup"><span data-stu-id="557fe-224">hello hook that is most applicable for hello auto-update scenario is hello `post-update` event.</span></span>

<span data-ttu-id="557fe-225">Bir SSH oturumu toohello web ön uç sanal makinede, toohello değiştirmek `~/node-todo.git/hooks` dizin ve aşağıdaki içerik tooa dosyasına adlı hello ekleyin `post-update` (değiştirme `machinename` ve `region` MongoDB sanal makine bilgileri ile):</span><span class="sxs-lookup"><span data-stu-id="557fe-225">In a SSH session toohello web frontend virtual machine, change toohello `~/node-todo.git/hooks` directory and add hello following content tooa file named `post-update` (replacing `machinename` and `region` with your MongoDB virtual machine information):</span></span>

    #!/bin/bash

    forever stopall
    unset 'GIT_DIR'
    export MONGODB="mongodb://machinename.region.cloudapp.azure.com:27017/tododb"
    cd ~/node-todo && git fetch origin && git pull origin master && npm install && forever start ~/node-todo/server.js
    exec git update-server-info

<span data-ttu-id="557fe-226">Merhaba aşağıdaki komutu çalıştırarak bu dosyayı yürütülebilir olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="557fe-226">Ensure this file is executable by running hello following command:</span></span>

    chmod 755 post-update

<span data-ttu-id="557fe-227">Bu komut dosyası hello geçerli sunucu uygulaması durduruldu, hello hello kopyalanan deposundaki güncelleştirilmiş toohello son kodudur, tüm güncelleştirilmiş bağımlılıkların ve hello sunucu yeniden sağlar.</span><span class="sxs-lookup"><span data-stu-id="557fe-227">This script ensures that hello current server application is stopped, hello code in hello cloned repository is updated toohello latest, any updated dependencies are satisfied, and hello server is restarted.</span></span> <span data-ttu-id="557fe-228">Ayrıca, bu hello ortam bizim ilk uygulama güncelleştirme tooget hello MongoDB örneği bir ortam değişkenini almak için hazırlık yapılandırılmış sağlar.</span><span class="sxs-lookup"><span data-stu-id="557fe-228">It also ensures that hello environment has been configured in preparation for receiving our first application update tooget hello MongoDB instance from an environment variable.</span></span>

### <a name="configuring-your-development-machine"></a><span data-ttu-id="557fe-229">Geliştirme makinenizde yapılandırma</span><span class="sxs-lookup"><span data-stu-id="557fe-229">Configuring your Development Machine</span></span>
<span data-ttu-id="557fe-230">Şimdi şimdi toohello web ön uç sanal Makine'yi sayfaya geliştirme makinenizde alın.</span><span class="sxs-lookup"><span data-stu-id="557fe-230">Now let's get your development machine hooked up toohello web frontend virtual machine.</span></span> <span data-ttu-id="557fe-231">Bu bir uzak hello sanal makinedeki hello tam deposu ekleme olarak gibi basit bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="557fe-231">This is as simple as adding hello bare repository on hello virtual machine as a remote.</span></span> <span data-ttu-id="557fe-232">Bu komut toodo aşağıdaki hello çalıştırın (değiştirme *kullanıcı* web ön uç sanal makine oturum açma adınızın ve *machinename* ve *bölge* uygun şekilde):</span><span class="sxs-lookup"><span data-stu-id="557fe-232">Run hello following command toodo this (replacing *user* with your web frontend virtual machine login name and *machinename* and *region* as appropriate):</span></span>

    git remote add azure user@machinename.region.cloudapp.azure.com:node-todo.git

<span data-ttu-id="557fe-233">Tüm gerekli tooenable dağıtmaya ya da geçerli yayımlama, toohello web ön uç sanal makine değiştiği budur.</span><span class="sxs-lookup"><span data-stu-id="557fe-233">This is all that is needed tooenable pushing, or in effect publishing, changes toohello web frontend virtual machine.</span></span>

### <a name="publishing-updates"></a><span data-ttu-id="557fe-234">Yayımlama güncelleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="557fe-234">Publishing Updates</span></span>
<span data-ttu-id="557fe-235">Şimdi kadarki yapılan ve böylece Merhaba uygulaması kendi MongoDB örneği kullanacak hello bir değişiklik yayımlayın:</span><span class="sxs-lookup"><span data-stu-id="557fe-235">Let's publish hello one change that has been made so far so that hello application will use our own MongoDB instance:</span></span>

    git push azure master

<span data-ttu-id="557fe-236">Çıktı benzer toothis görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="557fe-236">You should see output similar toothis:</span></span>

    Counting objects: 4, done.
    Delta compression using up too4 threads.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (4/4), 406 bytes | 0 bytes/s, done.
    Total 4 (delta 1), reused 0 (delta 0)
    remote: info:    Forever stopped processes:
    remote: data:        uid  command         script    forever pid  id logfile                         uptime
    remote: data:    [0] 0Lyh /usr/bin/nodejs server.js 9064    9301    /home/username/.forever/0Lyh.log 0:0:3:17.487
    remote: From /home/username/node-todo
    remote:    5f31fd7..5bc7be5  master     -> origin/master
    remote: From /home/username/node-todo
    remote:  * branch            master     -> FETCH_HEAD
    remote: Updating 5f31fd7..5bc7be5
    remote: Fast-forward
    remote:  config/database.js | 2 +-
    remote:  1 file changed, 1 insertion(+), 1 deletion(-)
    remote: npm WARN package.json node-todo@0.0.0 No repository field.
    remote: npm WARN package.json node-todo@0.0.0 No license field.
    remote: warn:    --minUptime not set. Defaulting to: 1000ms
    remote: warn:    --spinSleepTime not set. Your script will exit if it does not stay up for at least 1000ms
    remote: info:    Forever processing file: /home/username/node-todo/server.js
    toousername@machinename.region.cloudapp.azure.com:node-todo.git
    5f31fd7..5bc7be5  master -> master

<span data-ttu-id="557fe-237">Bu komut tamamlandıktan sonra bir web tarayıcısında Merhaba uygulaması yenilemeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="557fe-237">After this command completes, try refreshing hello application in a web browser.</span></span> <span data-ttu-id="557fe-238">Burada sunulan hello Yapılacaklar listesi boş olduğunu ve artık paylaşılan bağlı toohello MongoDB örneği dağıtıldığını mümkün toosee olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="557fe-238">You should be able toosee that hello TODO list presented here is empty and no longer tied toohello shared deployed MongoDB instance.</span></span>

<span data-ttu-id="557fe-239">toocomplete hello öğretici, başka bir, daha fazla görünen değişiklik olalım.</span><span class="sxs-lookup"><span data-stu-id="557fe-239">toocomplete hello tutorial, let's make another, more visible change.</span></span> <span data-ttu-id="557fe-240">Geliştirme makinenizde tercih ettiğiniz düzenleyicisi kullanarak hello node-todo/public/index.html dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="557fe-240">On your development machine, open hello node-todo/public/index.html file using your favorite editor.</span></span> <span data-ttu-id="557fe-241">Merhaba jumbotron üstbilgi bulun ve "Todo aholic ben" çok "Todo aholic Azure üzerinde ben!" Merhaba başlık değiştirin.</span><span class="sxs-lookup"><span data-stu-id="557fe-241">Locate hello jumbotron header and change  hello title from "I'm a Todo-aholic" too"I'm a Todo-aholic on Azure!".</span></span>

<span data-ttu-id="557fe-242">Şimdi şimdi yürüt:</span><span class="sxs-lookup"><span data-stu-id="557fe-242">Now let's commit:</span></span>

    git commit -am "Azurify hello title"

<span data-ttu-id="557fe-243">Bu kez, tooback toohello GitHub deposuna göndermeden önce hello değişiklik tooAzure Şimdi Yayımla:</span><span class="sxs-lookup"><span data-stu-id="557fe-243">This time, let's publish hello change tooAzure before pushing it tooback toohello GitHub repo:</span></span>

    git push azure master

<span data-ttu-id="557fe-244">Bu komut tamamlandığında, yenileme hello web sayfası ve hello değişiklikleri görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="557fe-244">Once this command completes, refresh hello web page and you will see hello changes.</span></span> <span data-ttu-id="557fe-245">İyi, görünen beri hello değişikliği geri toohello kaynak uzak itme getirin:</span><span class="sxs-lookup"><span data-stu-id="557fe-245">Since they look good, push hello change back toohello origin remote:</span></span> 

    git push origin master

## <a name="next-steps"></a><span data-ttu-id="557fe-246">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="557fe-246">Next Steps</span></span>
<span data-ttu-id="557fe-247">Bu makalede nasıl oluşturulacağını gösterir tootake bir Node.js uygulaması ve Azure üzerinde çalışan tooLinux sanal makineler dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="557fe-247">This article showed how tootake a Node.js application and deploy it tooLinux virtual machines running in Azure.</span></span> <span data-ttu-id="557fe-248">Linux sanal makineleri, azure'da hakkında daha fazla toolearn bkz [Azure ile ilgili giriş tooLinux](/documentation/articles/virtual-machines-linux-introduction/).</span><span class="sxs-lookup"><span data-stu-id="557fe-248">toolearn more about Linux virtual machines in Azure, see [Introduction tooLinux on Azure](/documentation/articles/virtual-machines-linux-introduction/).</span></span>

<span data-ttu-id="557fe-249">Hakkında daha fazla bilgi için bkz: Merhaba toodevelop Node.js uygulamaları Azure üzerinde [Node.js Geliştirici Merkezi](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="557fe-249">For more information about how toodevelop Node.js applications on Azure, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>

