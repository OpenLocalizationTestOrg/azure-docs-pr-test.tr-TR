---
title: "aaaAzure sanal makine dağıtımı Chef ile | Microsoft Docs"
description: "Sanal makine dağıtımı ve yapılandırması Microsoft Azure üzerinde nasıl toouse Chef toodo otomatik öğrenin"
services: virtual-machines-windows
documentationcenter: 
author: diegoviso
manager: timlt
tags: azure-service-management,azure-resource-manager
editor: 
ms.assetid: 0b82ca70-89ed-496d-bb49-c04ae59b4523
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: diviso
ms.openlocfilehash: c5ea98c673b2ee75dd4cedf27e50330af05230d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="automating-azure-virtual-machine-deployment-with-chef"></a><span data-ttu-id="420e5-103">Chef ile Azure sanal makine dağıtımını otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="420e5-103">Automating Azure virtual machine deployment with Chef</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="420e5-104">Chef Otomasyon teslim etmek için harika bir araçtır ve durumu yapılandırmaları istenen.</span><span class="sxs-lookup"><span data-stu-id="420e5-104">Chef is a great tool for delivering automation and desired state configurations.</span></span>

<span data-ttu-id="420e5-105">En son bizim bulut API sürümüyle Chef Azure ile sorunsuz tümleştirme sağlar, veren özelliği tooprovision hello ve yapılandırma durumları arasında tek bir komut dağıtın.</span><span class="sxs-lookup"><span data-stu-id="420e5-105">With our latest cloud-api release, Chef provides seamless integration with Azure, giving you hello ability tooprovision and deploy configuration states through a single command.</span></span>

<span data-ttu-id="420e5-106">Bu makalede, t, nasıl göstereceğiz tooset yukarı Chef ortamı tooprovision Azure sanal makineleri ve bir ilke veya "Kılavuzu" oluşturma ve ardından bu kılavuzu tooan Azure sanal makine dağıtma size yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="420e5-106">In this article, I’ll show you how tooset up your Chef environment tooprovision Azure virtual machines and walk you through creating a policy or “CookBook” and then deploying this cookbook tooan Azure virtual machine.</span></span>

<span data-ttu-id="420e5-107">Başlayalım!</span><span class="sxs-lookup"><span data-stu-id="420e5-107">Let’s begin!</span></span>

## <a name="chef-basics"></a><span data-ttu-id="420e5-108">Chef temelleri</span><span class="sxs-lookup"><span data-stu-id="420e5-108">Chef basics</span></span>
<span data-ttu-id="420e5-109">Başlamadan önce ı hello Chef temel kavramlarını gözden öneririz.</span><span class="sxs-lookup"><span data-stu-id="420e5-109">Before you begin, I suggest you review hello basic concepts of Chef.</span></span> <span data-ttu-id="420e5-110">Harika malzeme yoktur <a href="http://www.chef.io/chef" target="_blank">burada</a> ve ı, bu kılavuzda denemeden önce hızlı okuma sahip öneririz.</span><span class="sxs-lookup"><span data-stu-id="420e5-110">There is great material <a href="http://www.chef.io/chef" target="_blank">here</a> and I recommend you have a quick read before you attempt this walkthrough.</span></span> <span data-ttu-id="420e5-111">Başlamadan önce ı hello temelleri ancak olduðunu.</span><span class="sxs-lookup"><span data-stu-id="420e5-111">I will however recap hello basics before we get started.</span></span>

<span data-ttu-id="420e5-112">Aşağıdaki diyagramda hello hello üst düzey Chef mimari gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="420e5-112">hello following diagram depicts hello high-level Chef architecture.</span></span>

![][2]

<span data-ttu-id="420e5-113">Chef üç ana mimari bileşeni vardır: Chef sunucusu, Chef istemcisi (düğüm) ve Chef iş istasyonu.</span><span class="sxs-lookup"><span data-stu-id="420e5-113">Chef has three main architectural components: Chef Server, Chef Client (node), and Chef Workstation.</span></span>

<span data-ttu-id="420e5-114">Merhaba Chef sunucu bizim yönetim noktasıdır ve Chef sunucu Merhaba için iki seçenek vardır: barındırılan bir çözüm ya da bir şirket içi çözüm.</span><span class="sxs-lookup"><span data-stu-id="420e5-114">hello Chef Server is our management point and there are two options for hello Chef Server: a hosted solution or an on-premises solution.</span></span> <span data-ttu-id="420e5-115">Biz, barındırılan bir çözümü kullanarak.</span><span class="sxs-lookup"><span data-stu-id="420e5-115">We will be using a hosted solution.</span></span>

<span data-ttu-id="420e5-116">Merhaba Chef (düğüm) yönettiğiniz hello sunucularda bulunur hello Aracısı istemcidir.</span><span class="sxs-lookup"><span data-stu-id="420e5-116">hello Chef Client (node) is hello agent that sits on hello servers you are managing.</span></span>

<span data-ttu-id="420e5-117">Merhaba Chef iş istasyonu burada biz bizim ilkeleri oluşturma ve bizim yönetimi komutları yürütme bizim yönetim iş istasyonu ' dir.</span><span class="sxs-lookup"><span data-stu-id="420e5-117">hello Chef Workstation is our admin workstation where we create our policies and execute our management commands.</span></span> <span data-ttu-id="420e5-118">Merhaba çalıştıracağımız **Bıçak** bizim altyapı Chef iş istasyonu toomanage hello komutu.</span><span class="sxs-lookup"><span data-stu-id="420e5-118">We run hello **knife** command from hello Chef Workstation toomanage our infrastructure.</span></span>

<span data-ttu-id="420e5-119">"Cookbooks" ve "Tarif" Merhaba kavramı yoktur.</span><span class="sxs-lookup"><span data-stu-id="420e5-119">There is also hello concept of “Cookbooks” and “Recipes”.</span></span> <span data-ttu-id="420e5-120">Bunlar etkili bir şekilde tanımlamak ve tooour sunucular geçerli hello ilkelerdir.</span><span class="sxs-lookup"><span data-stu-id="420e5-120">These are effectively hello policies we define and apply tooour servers.</span></span>

## <a name="preparing-hello-workstation"></a><span data-ttu-id="420e5-121">Merhaba iş istasyonu hazırlama</span><span class="sxs-lookup"><span data-stu-id="420e5-121">Preparing hello workstation</span></span>
<span data-ttu-id="420e5-122">İlk olarak, hazırlık hello iş istasyonu sağlar.</span><span class="sxs-lookup"><span data-stu-id="420e5-122">First, lets prep hello workstation.</span></span> <span data-ttu-id="420e5-123">Standart bir Windows iş istasyonu kullanıyorum.</span><span class="sxs-lookup"><span data-stu-id="420e5-123">I’m using a standard Windows workstation.</span></span> <span data-ttu-id="420e5-124">Toocreate dizin toostore bizim yapılandırma dosyaları ve cookbooks gerekir.</span><span class="sxs-lookup"><span data-stu-id="420e5-124">We need toocreate a directory toostore our config files and cookbooks.</span></span>

<span data-ttu-id="420e5-125">İlk C:\chef adlı bir dizin oluşturun.</span><span class="sxs-lookup"><span data-stu-id="420e5-125">First create a directory called C:\chef.</span></span>

<span data-ttu-id="420e5-126">Daha sonra c:\chef\cookbooks adlı ikinci bir dizin oluşturun.</span><span class="sxs-lookup"><span data-stu-id="420e5-126">Then create a second directory called c:\chef\cookbooks.</span></span>

<span data-ttu-id="420e5-127">Şimdi, Chef bizim Azure aboneliği ile iletişim kurabilmesi toodownload bizim Azure ayarları dosyası gerekir.</span><span class="sxs-lookup"><span data-stu-id="420e5-127">We now need toodownload our Azure settings file so Chef can communicate with our Azure subscription.</span></span>

<!--Download your publish settings from [here](https://manage.windowsazure.com/publishsettings/).-->
<span data-ttu-id="420e5-128">Karşıdan yükle, yayımlama hello PowerShell Azure kullanarak ayarları [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) komutu.</span><span class="sxs-lookup"><span data-stu-id="420e5-128">Download your publish settings using hello PowerShell Azure [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) command.</span></span> 

<span data-ttu-id="420e5-129">Yayımlama ayarları dosyası içinde C:\chef Hello.</span><span class="sxs-lookup"><span data-stu-id="420e5-129">Save hello publish settings file in C:\chef.</span></span>

## <a name="creating-a-managed-chef-account"></a><span data-ttu-id="420e5-130">Yönetilen bir Chef hesap oluşturma</span><span class="sxs-lookup"><span data-stu-id="420e5-130">Creating a managed Chef account</span></span>
<span data-ttu-id="420e5-131">Barındırılan Chef hesap için kaydolabilirsiniz [burada](https://manage.chef.io/signup).</span><span class="sxs-lookup"><span data-stu-id="420e5-131">Sign up for a hosted Chef account [here](https://manage.chef.io/signup).</span></span>

<span data-ttu-id="420e5-132">Merhaba kaydolma işlemi sırasında olacak yeni bir kuruluş toocreate istedi.</span><span class="sxs-lookup"><span data-stu-id="420e5-132">During hello signup process, you will be asked toocreate a new organization.</span></span>

![][3]

<span data-ttu-id="420e5-133">Kuruluşunuz oluşturulduktan sonra hello starter kit indirin.</span><span class="sxs-lookup"><span data-stu-id="420e5-133">Once your organization is created, download hello starter kit.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="420e5-134">Anahtarlarınızı sıfırlanacak uyarı bir uyarı alırsanız, henüz yapılandırılmış hiçbir mevcut altyapısına sahip olduğumuz Tamam tooproceed olur.</span><span class="sxs-lookup"><span data-stu-id="420e5-134">If you receive a prompt warning you that your keys will be reset, it’s ok tooproceed as we have no existing infrastructure configured as yet.</span></span>
> 
> 

<span data-ttu-id="420e5-135">Bu starter kit zip dosyası kuruluş yapılandırma dosyalarını ve anahtarlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="420e5-135">This starter kit zip file contains your organization config files and keys.</span></span>

## <a name="configuring-hello-chef-workstation"></a><span data-ttu-id="420e5-136">Merhaba Chef iş istasyonu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="420e5-136">Configuring hello Chef workstation</span></span>
<span data-ttu-id="420e5-137">Merhaba chef starter.zip tooC:\chef Hello içeriğini ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="420e5-137">Extract hello content of hello chef-starter.zip tooC:\chef.</span></span>

<span data-ttu-id="420e5-138">Chef starter\chef depodaki altındaki tüm dosyaları kopyalayın\.chef tooyour c:\chef dizini.</span><span class="sxs-lookup"><span data-stu-id="420e5-138">Copy all files under chef-starter\chef-repo\.chef tooyour c:\chef directory.</span></span>

<span data-ttu-id="420e5-139">Dizininizi hello örnek aşağıdaki gibi görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="420e5-139">Your directory should now look something like hello following example.</span></span>

![][5]

<span data-ttu-id="420e5-140">Şimdi c:\chef hello kök dizininde hello Azure yayımlama dosyası dahil olmak üzere dört dosyaları olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="420e5-140">You should now have four files including hello Azure publishing file in hello root of c:\chef.</span></span>

<span data-ttu-id="420e5-141">Merhaba knife.rb dosya Bıçak yapılandırmanızı içerirken hello PEM dosyaları kuruluşunuz ve yönetici iletişimi için özel anahtarları içerir.</span><span class="sxs-lookup"><span data-stu-id="420e5-141">hello PEM files contain your organization and admin private keys for communication while hello knife.rb file contains your knife configuration.</span></span> <span data-ttu-id="420e5-142">Biz tooedit hello knife.rb dosyası gerekir.</span><span class="sxs-lookup"><span data-stu-id="420e5-142">We will need tooedit hello knife.rb file.</span></span>

<span data-ttu-id="420e5-143">Seçim düzenleyicinizde hello dosyasını açın ve hello "cookbook_path" Merhaba kaldırarak değiştirme /... / sonraki gösterildiği gibi göründüğü şekilde hello yolundan.</span><span class="sxs-lookup"><span data-stu-id="420e5-143">Open hello file in your editor of choice and modify hello “cookbook_path” by removing hello /../ from hello path so it appears as shown next.</span></span>

    cookbook_path  ["#{current_dir}/cookbooks"]

<span data-ttu-id="420e5-144">Ayrıca hello aşağıdaki Azure yansıtıcı hello adını satır ekleyin yayımlama ayarları dosyası.</span><span class="sxs-lookup"><span data-stu-id="420e5-144">Also add hello following line reflecting hello name of your Azure publish settings file.</span></span>

    knife[:azure_publish_settings_file] = "yourfilename.publishsettings"

<span data-ttu-id="420e5-145">Aşağıdaki örneğine benzer toohello knife.rb dosyanızı görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="420e5-145">Your knife.rb file should now look similar toohello following example.</span></span>

![][6]

<span data-ttu-id="420e5-146">Bu satırlar Bıçak hello cookbooks dizini c:\chef\cookbooks altında başvuruyor ve ayrıca bizim Azure yayımlama ayarları dosyasını Azure işlemleri sırasında kullanır, güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="420e5-146">These lines will ensure that Knife references hello cookbooks directory under c:\chef\cookbooks, and also uses our Azure Publish Settings file during Azure operations.</span></span>

## <a name="installing-hello-chef-development-kit"></a><span data-ttu-id="420e5-147">Yükleme hello Chef Geliştirme Seti</span><span class="sxs-lookup"><span data-stu-id="420e5-147">Installing hello Chef Development Kit</span></span>
<span data-ttu-id="420e5-148">Sonraki [yükleyip](http://downloads.getchef.com/chef-dk/windows) ChefDK (Chef Geliştirme Seti) tooset Chef istasyonunuzu yukarı hello.</span><span class="sxs-lookup"><span data-stu-id="420e5-148">Next [download and install](http://downloads.getchef.com/chef-dk/windows) hello ChefDK (Chef Development Kit) tooset up your Chef Workstation.</span></span>

![][7]

<span data-ttu-id="420e5-149">Merhaba varsayılan konumunda c:\opscode yükleyin.</span><span class="sxs-lookup"><span data-stu-id="420e5-149">Install in hello default location of c:\opscode.</span></span> <span data-ttu-id="420e5-150">Bu yükleme yaklaşık 10 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="420e5-150">This install will take around 10 minutes.</span></span>

<span data-ttu-id="420e5-151">PATH değişkeni C:\opscode\chefdk\bin için girdiler içeriyor doğrulayın; C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin</span><span class="sxs-lookup"><span data-stu-id="420e5-151">Confirm your PATH variable contains entries for C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin</span></span>

<span data-ttu-id="420e5-152">Bunlar yoksa, bu yollar eklediğinizden emin olun!</span><span class="sxs-lookup"><span data-stu-id="420e5-152">If they are not there, make sure you add these paths!</span></span>

<span data-ttu-id="420e5-153">*Hello sipariş, hello yolu önemli olduğunu unutmayın!*</span><span class="sxs-lookup"><span data-stu-id="420e5-153">*NOTE hello ORDER OF hello PATH IS IMPORTANT!*</span></span> <span data-ttu-id="420e5-154">Opscode yolları hello doğru sırada değilse sorunları sahip olur.</span><span class="sxs-lookup"><span data-stu-id="420e5-154">If your opscode paths are not in hello correct order you will have issues.</span></span>

<span data-ttu-id="420e5-155">Devam etmeden önce iş istasyonunuzu yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="420e5-155">Reboot your workstation before you continue.</span></span>

<span data-ttu-id="420e5-156">Ardından, sisteme hello Bıçak Azure uzantısı yüklenir.</span><span class="sxs-lookup"><span data-stu-id="420e5-156">Next, we will install hello Knife Azure extension.</span></span> <span data-ttu-id="420e5-157">Bu Bıçak "Azure eklentisi" Merhaba ile sağlar.</span><span class="sxs-lookup"><span data-stu-id="420e5-157">This provides Knife with hello “Azure Plugin”.</span></span>

<span data-ttu-id="420e5-158">Merhaba aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="420e5-158">Run hello following command.</span></span>

    chef gem install knife-azure ––pre

> [!NOTE]
> <span data-ttu-id="420e5-159">Merhaba – öncesi bağımsız değişkeni, en son RC sürümünü hello erişim toohello son API kümesi sağlayan Bıçak Azure eklentisi hello alma sağlar.</span><span class="sxs-lookup"><span data-stu-id="420e5-159">hello –pre argument ensures you are receiving hello latest RC version of hello Knife Azure Plugin which provides access toohello latest set of APIs.</span></span>
> 
> 

<span data-ttu-id="420e5-160">Bağımlılık sayısı da hello sırasında yüklenecek olasıdır aynı anda.</span><span class="sxs-lookup"><span data-stu-id="420e5-160">It’s likely that a number of dependencies will also be installed at hello same time.</span></span>

![][8]

<span data-ttu-id="420e5-161">her şey tooensure komutu aşağıdaki çalışma hello doğru yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="420e5-161">tooensure everything is configured correctly, run hello following command.</span></span>

    knife azure image list

<span data-ttu-id="420e5-162">Her şeyin doğru şekilde yapılandırıldıysa, mevcut Azure görüntüleri kaydırın listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="420e5-162">If everything is configured correctly, you will see a list of available Azure images scroll through.</span></span>

<span data-ttu-id="420e5-163">Tebrikler.</span><span class="sxs-lookup"><span data-stu-id="420e5-163">Congratulations.</span></span> <span data-ttu-id="420e5-164">Merhaba iş istasyonu ayarlama!</span><span class="sxs-lookup"><span data-stu-id="420e5-164">hello workstation is set up!</span></span>

## <a name="creating-a-cookbook"></a><span data-ttu-id="420e5-165">Bir kılavuzu oluşturma</span><span class="sxs-lookup"><span data-stu-id="420e5-165">Creating a Cookbook</span></span>
<span data-ttu-id="420e5-166">Bir kılavuzu Chef toodefine tarafından kullanılan yönetilen istemcide tooexecute istediğiniz komutlar kümesi.</span><span class="sxs-lookup"><span data-stu-id="420e5-166">A Cookbook is used by Chef toodefine a set of commands that you wish tooexecute on your managed client.</span></span> <span data-ttu-id="420e5-167">Bir kılavuzu oluşturma basit ve hello kullanırız **chef oluşturmak Kılavuzu** toogenerate bizim Kılavuzu şablon komutu.</span><span class="sxs-lookup"><span data-stu-id="420e5-167">Creating a Cookbook is straightforward and we use hello **chef generate cookbook** command toogenerate our Cookbook template.</span></span> <span data-ttu-id="420e5-168">IIS otomatik olarak dağıtan bir ilke ister misiniz gibi ı Kılavuzu web sunucusunu çağırma.</span><span class="sxs-lookup"><span data-stu-id="420e5-168">I will be calling my Cookbook web server as I would like a policy that automatically deploys IIS.</span></span>

<span data-ttu-id="420e5-169">C:\Chef dizini altında hello aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="420e5-169">Under your C:\Chef directory run hello following command.</span></span>

    chef generate cookbook webserver

<span data-ttu-id="420e5-170">Bu C:\Chef\cookbooks\webserver hello dizin altında dosya kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="420e5-170">This will generate a set of files under hello directory C:\Chef\cookbooks\webserver.</span></span> <span data-ttu-id="420e5-171">Şimdi toodefine hello bizim yönetilen sanal makinede bizim Chef istemci tooexecute isteriz komut kümesini ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="420e5-171">We now need toodefine hello set of commands we would like our Chef client tooexecute on our managed virtual machine.</span></span>

<span data-ttu-id="420e5-172">Merhaba komutları hello dosya default.rb içinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="420e5-172">hello commands are stored in hello file default.rb.</span></span> <span data-ttu-id="420e5-173">Bu dosyada, ı IIS yükler, IIS başlayıp bir şablon dosyası toohello wwwroot klasörüne kopyalar komut kümesini tanımlama.</span><span class="sxs-lookup"><span data-stu-id="420e5-173">In this file, I’ll be defining a set of commands that installs IIS, starts IIS and copies a template file toohello wwwroot folder.</span></span>

<span data-ttu-id="420e5-174">Merhaba C:\chef\cookbooks\webserver\recipes\default.rb dosyasını değiştirin ve satırlardan hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="420e5-174">Modify hello C:\chef\cookbooks\webserver\recipes\default.rb file and add hello following lines.</span></span>

    powershell_script 'Install IIS' do
         action :run
         code 'add-windowsfeature Web-Server'
    end

    service 'w3svc' do
         action [ :enable, :start ]
    end

    template 'c:\inetpub\wwwroot\Default.htm' do
         source 'Default.htm.erb'
         rights :read, 'Everyone'
    end

<span data-ttu-id="420e5-175">İşiniz bittiğinde hello dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="420e5-175">Save hello file once you are done.</span></span>

## <a name="creating-a-template"></a><span data-ttu-id="420e5-176">Şablon oluşturma</span><span class="sxs-lookup"><span data-stu-id="420e5-176">Creating a template</span></span>
<span data-ttu-id="420e5-177">Daha önce belirtildiği gibi toogenerate default.html sayfamızı kullanılacak bir şablon dosyası ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="420e5-177">As we mentioned previously, we need toogenerate a template file which will be used as our default.html page.</span></span>

<span data-ttu-id="420e5-178">Çalışma hello aşağıdaki toogenerate hello şablon komutu.</span><span class="sxs-lookup"><span data-stu-id="420e5-178">Run hello following command toogenerate hello template.</span></span>

    chef generate template webserver Default.htm

<span data-ttu-id="420e5-179">Şimdi toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb dosya gidin.</span><span class="sxs-lookup"><span data-stu-id="420e5-179">Now navigate toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb file.</span></span> <span data-ttu-id="420e5-180">Bazı basit "Hello World" HTML kod ekleyerek Hello dosyasını düzenleyin ve hello dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="420e5-180">Edit hello file by adding some simple “Hello World” HTML code, and then save hello file.</span></span>

## <a name="upload-hello-cookbook-toohello-chef-server"></a><span data-ttu-id="420e5-181">Merhaba Kılavuzu toohello Chef sunucu karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="420e5-181">Upload hello Cookbook toohello Chef Server</span></span>
<span data-ttu-id="420e5-182">Bu adımda, biz hello bizim yerel makinede oluşturduk Kılavuzu bir kopyasını almak ve toohello Chef barındırılan sunucu karşıya yükleme.</span><span class="sxs-lookup"><span data-stu-id="420e5-182">In this step, we are taking a copy of hello Cookbook that we have created on our local machine and uploading it toohello Chef Hosted Server.</span></span> <span data-ttu-id="420e5-183">Karşıya sonra hello Kılavuzu hello altında görünür **İlkesi** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="420e5-183">Once uploaded, hello Cookbook will appear under hello **Policy** tab.</span></span>

    knife cookbook upload webserver

![][9]

## <a name="deploy-a-virtual-machine-with-knife-azure"></a><span data-ttu-id="420e5-184">Bir sanal makine Bıçak Azure ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="420e5-184">Deploy a virtual machine with Knife Azure</span></span>
<span data-ttu-id="420e5-185">Biz şimdi bir Azure sanal makinesi dağıtır ve hello IIS web hizmeti ve varsayılan web sayfamızı yükleyecek "Web" kılavuzu uygulayın.</span><span class="sxs-lookup"><span data-stu-id="420e5-185">We will now deploy an Azure virtual machine and apply hello “Webserver” Cookbook which will install our IIS web service and default web page.</span></span>

<span data-ttu-id="420e5-186">Buna toodo Bu sipariş, hello kullan **Bıçak azure sunucusu oluşturmak** komutu.</span><span class="sxs-lookup"><span data-stu-id="420e5-186">In order toodo this, use hello **knife azure server create** command.</span></span>

<span data-ttu-id="420e5-187">Merhaba komut örneği ardından görüntülenen istiyorum.</span><span class="sxs-lookup"><span data-stu-id="420e5-187">Am example of hello command appears next.</span></span>

    knife azure server create --azure-dns-name 'diegotest01' --azure-vm-name 'testserver01' --azure-vm-size 'Small' --azure-storage-account 'portalvhdsxxxx' --bootstrap-protocol 'cloud-api' --azure-source-image 'a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201411.01-en.us-127GB.vhd' --azure-service-location 'Southeast Asia' --winrm-user azureuser --winrm-password 'myPassword123' --tcp-endpoints 80,3389 --r 'recipe[webserver]'

<span data-ttu-id="420e5-188">Merhaba parametreleri kendinden açıklamalıdır.</span><span class="sxs-lookup"><span data-stu-id="420e5-188">hello parameters are self-explanatory.</span></span> <span data-ttu-id="420e5-189">Belirli değişkenleri değiştirin ve çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="420e5-189">Substitute your particular variables and run.</span></span>

> [!NOTE]
> <span data-ttu-id="420e5-190">Hello hello komut satırı ı de uç nokta ağ filtre kuralları hello – tcp uç noktaları parametresini kullanarak otomatikleştirme.</span><span class="sxs-lookup"><span data-stu-id="420e5-190">Through hello hello command line, I’m also automating my endpoint network filter rules by using hello –tcp-endpoints parameter.</span></span> <span data-ttu-id="420e5-191">Bağlantı noktaları 80 ve 3389 tooprovide erişim toomy web sayfası ve RDP oturumu açmış olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="420e5-191">I’ve opened up ports 80 and 3389 tooprovide access toomy web page and RDP session.</span></span>
> 
> 

<span data-ttu-id="420e5-192">Merhaba komutu çalıştırdıktan sonra toohello Azure Git portal ve tooprovision başlamak makinenizi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="420e5-192">Once you run hello command, go toohello Azure portal and you will see your machine begin tooprovision.</span></span>

![][13]

<span data-ttu-id="420e5-193">sonraki Hello komut istemi belirir.</span><span class="sxs-lookup"><span data-stu-id="420e5-193">hello command prompt appears next.</span></span>

![][10]

<span data-ttu-id="420e5-194">Merhaba dağıtım tamamlandıktan sonra biz hello Bıçak Azure komutu ile Merhaba sanal makine sağladığında hello bağlantı noktası açıldı biz mümkün tooconnect toohello web hizmeti bağlantı noktası 80 üzerinden olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="420e5-194">Once hello deployment is complete, we should be able tooconnect toohello web service over port 80 as we had opened hello port when we provisioned hello virtual machine with hello Knife Azure command.</span></span> <span data-ttu-id="420e5-195">Bu sanal makine hello yalnızca sanal makine my bulut hizmetinde olduğu gibi ı hello bulut hizmet URL'si ile bağlanırsınız.</span><span class="sxs-lookup"><span data-stu-id="420e5-195">As this virtual machine is hello only virtual machine in my cloud service, I’ll connect it with hello cloud service url.</span></span>

![][11]

<span data-ttu-id="420e5-196">Gördüğünüz gibi HTML kodumu yaratıcı aldım.</span><span class="sxs-lookup"><span data-stu-id="420e5-196">As you can see, I got creative with my HTML code.</span></span>

<span data-ttu-id="420e5-197">Biz de hello Azure portalı 3389 numaralı bağlantı noktası üzerinden bir RDP oturumu üzerinden bağlanabildiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="420e5-197">Don’t forget we can also connect through an RDP session from hello Azure portal via port 3389.</span></span>

<span data-ttu-id="420e5-198">Bu yardımcı olmuştur ı umuyoruz!</span><span class="sxs-lookup"><span data-stu-id="420e5-198">I hope this has been helpful!</span></span> <span data-ttu-id="420e5-199">Git ve altyapınızı Azure ile kod gezisine olarak bugün başlayın!</span><span class="sxs-lookup"><span data-stu-id="420e5-199">Go  and start your infrastructure as code journey with Azure today!</span></span>

<!--Image references-->
[2]: media/chef-automation/2.png
[3]: media/chef-automation/3.png
[4]: media/chef-automation/4.png
[5]: media/chef-automation/5.png
[6]: media/chef-automation/6.png
[7]: media/chef-automation/7.png
[8]: media/chef-automation/8.png
[9]: media/chef-automation/9.png
[10]: media/chef-automation/10.png
[11]: media/chef-automation/11.png
[13]: media/chef-automation/13.png


<!--Link references-->
