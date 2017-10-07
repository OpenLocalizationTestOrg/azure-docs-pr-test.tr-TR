---
title: "bir Linux VM üzerinde rayları Web sitesinde bir Ruby aaaHost | Microsoft Docs"
description: "Ayarlama ve Ruby kullanarak bir Linux sanal makine azure'da rayları tabanlı Web sitesinde ana bilgisayar."
services: virtual-machines-linux
documentationcenter: ruby
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: aad32685-3550-4bff-9c73-beb8d70b3291
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: ruby
ms.topic: article
ms.date: 06/27/2017
ms.author: robmcm
ms.openlocfilehash: c545c24fc6c89497854bbe55a6d0d1d0b072c386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="ruby-on-rails-web-application-on-an-azure-vm"></a><span data-ttu-id="a1d82-103">Azure VM’de Ruby on Rails Web uygulaması</span><span class="sxs-lookup"><span data-stu-id="a1d82-103">Ruby on Rails Web application on an Azure VM</span></span>
<span data-ttu-id="a1d82-104">Bu öğreticide gösterilmiştir nasıl toohost Ruby kullanarak bir Linux sanal makine azure'da rayları Web sitesinde.</span><span class="sxs-lookup"><span data-stu-id="a1d82-104">This tutorial shows how toohost a Ruby on Rails website on Azure using a Linux virtual machine.</span></span>  

<span data-ttu-id="a1d82-105">Bu öğretici, Ubuntu Server 14.04 LTS kullanılarak doğrulandı.</span><span class="sxs-lookup"><span data-stu-id="a1d82-105">This tutorial was validated using Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="a1d82-106">Başka bir Linux dağıtım kullanırsanız, toomodify gerekebilecek hello tooinstall rayları adımları.</span><span class="sxs-lookup"><span data-stu-id="a1d82-106">If you use a different Linux distribution, you might need toomodify hello steps tooinstall Rails.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a1d82-107">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a1d82-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="a1d82-108">Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="a1d82-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="a1d82-109">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="a1d82-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
>
>

## <a name="create-an-azure-vm"></a><span data-ttu-id="a1d82-110">Bir Azure VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="a1d82-110">Create an Azure VM</span></span>
<span data-ttu-id="a1d82-111">Bir Linux görüntüsüyle bir Azure VM oluşturarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="a1d82-111">Start by creating an Azure VM with a Linux image.</span></span>

<span data-ttu-id="a1d82-112">toocreate VM Merhaba, hello Azure portalında veya Azure komut satırı arabirimi (CLI) hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1d82-112">toocreate hello VM, you can use hello Azure portal or hello Azure Command-Line Interface (CLI).</span></span>

### <a name="azure-portal"></a><span data-ttu-id="a1d82-113">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="a1d82-113">Azure portal</span></span>
1. <span data-ttu-id="a1d82-114">Merhaba içine oturum [Azure portalı](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="a1d82-114">Sign into hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="a1d82-115">Tıklatın **yeni**, ardından "Ubuntu Server 14.04" Merhaba arama kutusuna yazın.</span><span class="sxs-lookup"><span data-stu-id="a1d82-115">Click **New**, then type "Ubuntu Server 14.04" in hello search box.</span></span> <span data-ttu-id="a1d82-116">Merhaba araması tarafından döndürülen hello girdiyi tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a1d82-116">Click hello entry returned by hello search.</span></span> <span data-ttu-id="a1d82-117">Merhaba dağıtım modelini seçin **Klasik**, "Oluştur" seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a1d82-117">For hello deployment model, select **Classic**, then click "Create".</span></span>
3. <span data-ttu-id="a1d82-118">Merhaba temel bilgileri dikey penceresinde hello gerekli alanlar için değerleri girin: (için hello VM) adı, kullanıcı adı, kimlik doğrulama türü ve hello ilgili kimlik bilgileri, Azure abonelik, kaynak grubunu ve konumu.</span><span class="sxs-lookup"><span data-stu-id="a1d82-118">In hello Basics blade, supply values for hello required fields: Name (for hello VM), User name, Authentication type and hello corresponding credentials, Azure subscription, Resource group, and Location.</span></span>

   ![Yeni bir Ubuntu görüntüsü oluşturma](./media/virtual-machines-linux-classic-ruby-rails-web-app/createvm.png)

4. <span data-ttu-id="a1d82-120">Merhaba VM sağlandıktan sonra hello VM adına tıklayın ve'ı tıklatın **uç noktaları** hello içinde **ayarları** kategorisi.</span><span class="sxs-lookup"><span data-stu-id="a1d82-120">After hello VM is provisioned, click on hello VM name, and click **Endpoints** in hello **Settings** category.</span></span> <span data-ttu-id="a1d82-121">Altında listelenen hello SSH uç noktasını Bul **tek başına**.</span><span class="sxs-lookup"><span data-stu-id="a1d82-121">Find hello SSH endpoint, listed under **Standalone**.</span></span>

   ![Varsayılan uç noktası](./media/virtual-machines-linux-classic-ruby-rails-web-app/endpointsnewportal.png)

### <a name="azure-cli"></a><span data-ttu-id="a1d82-123">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a1d82-123">Azure CLI</span></span>
<span data-ttu-id="a1d82-124">Merhaba adımları [çalıştıran bir sanal makine Linux oluşturma][vm-instructions].</span><span class="sxs-lookup"><span data-stu-id="a1d82-124">Follow hello steps in [Create a Virtual Machine Running Linux][vm-instructions].</span></span>

<span data-ttu-id="a1d82-125">Merhaba VM sağlandıktan sonra komutu aşağıdaki hello çalıştırarak hello SSH uç noktası alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a1d82-125">After hello VM is provisioned, you can get hello SSH endpoint by running hello following command:</span></span>

    azure vm endpoint list <vm-name>  

## <a name="install-ruby-on-rails"></a><span data-ttu-id="a1d82-126">Ruby rayları üzerinde yükle</span><span class="sxs-lookup"><span data-stu-id="a1d82-126">Install Ruby on Rails</span></span>
1. <span data-ttu-id="a1d82-127">SSH tooconnect toohello VM kullanın.</span><span class="sxs-lookup"><span data-stu-id="a1d82-127">Use SSH tooconnect toohello VM.</span></span>
2. <span data-ttu-id="a1d82-128">Merhaba SSH oturumundan komutları tooinstall Ruby hello VM üzerinde aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="a1d82-128">From hello SSH session, use hello following commands tooinstall Ruby on hello VM:</span></span>

        sudo apt-get update -y
        sudo apt-get upgrade -y

        sudo apt-add-repository ppa:brightbox/ruby-ng
        sudo apt-get update
        sudo apt-get install ruby2.4

        > [!TIP]
        > hello brightbox repository contains hello current Ruby distribution.

    <span data-ttu-id="a1d82-129">Merhaba yükleme birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="a1d82-129">hello installation may take a few minutes.</span></span> <span data-ttu-id="a1d82-130">Tamamlandığında, Ruby yüklendiğini komutu tooverify aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="a1d82-130">When it completes, use hello following command tooverify that Ruby is installed:</span></span>

        ruby -v

3. <span data-ttu-id="a1d82-131">Kullanım hello aşağıdaki tooinstall rayları komutu:</span><span class="sxs-lookup"><span data-stu-id="a1d82-131">Use hello following command tooinstall Rails:</span></span>

        sudo gem install rails --no-rdoc --no-ri -V

    <span data-ttu-id="a1d82-132">Merhaba--yok rdoc ve--hızlıdır hello belge yükleme Hayır RI bayrakları tooskip kullanın.</span><span class="sxs-lookup"><span data-stu-id="a1d82-132">Use hello --no-rdoc and --no-ri flags tooskip installing hello documentation, which is faster.</span></span>
    <span data-ttu-id="a1d82-133">Bu komut, büyük olasılıkla ekleme hello şekilde -V tooexecute hello yükleme ilerleme durumu hakkında bilgi görüntüler uzun bir zaman alır.</span><span class="sxs-lookup"><span data-stu-id="a1d82-133">This command will likely take a long time tooexecute, so adding hello -V will display information about hello installation progress.</span></span>

## <a name="create-and-run-an-app"></a><span data-ttu-id="a1d82-134">Oluşturma ve bir uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="a1d82-134">Create and run an app</span></span>
<span data-ttu-id="a1d82-135">SSH yoluyla hala oturum açmış olsa da, hello aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a1d82-135">While still logged in via SSH, run hello following commands:</span></span>

    rails new myapp
    cd myapp
    rails server -b 0.0.0.0 -p 3000

<span data-ttu-id="a1d82-136">Merhaba [yeni](http://guides.rubyonrails.org/command_line.html#rails-new) komut yeni bir rayları uygulaması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a1d82-136">hello [new](http://guides.rubyonrails.org/command_line.html#rails-new) command creates a new Rails app.</span></span> <span data-ttu-id="a1d82-137">Merhaba [server](http://guides.rubyonrails.org/command_line.html#rails-server) başlatır hello rayları ile birlikte gelen WEBrick web sunucusu komutu.</span><span class="sxs-lookup"><span data-stu-id="a1d82-137">hello [server](http://guides.rubyonrails.org/command_line.html#rails-server) command starts hello WEBrick web server that comes with Rails.</span></span> <span data-ttu-id="a1d82-138">(Üretim kullanımı için büyük olasılıkla toouse Unicorn veya yolcu gibi farklı bir sunucuya istersiniz.)</span><span class="sxs-lookup"><span data-stu-id="a1d82-138">(For production use, you would probably want toouse a different server, such as Unicorn or Passenger.)</span></span>

<span data-ttu-id="a1d82-139">Çıktı benzer toohello aşağıdaki görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a1d82-139">You should see output similar toohello following.</span></span>

    => Booting WEBrick
    => Rails 4.2.1 application starting in development on http://0.0.0.0:3000
    => Run `rails server -h` for more startup options
    => Ctrl-C tooshutdown server
    [2015-06-09 23:34:23] INFO  WEBrick 1.3.1
    [2015-06-09 23:34:23] INFO  ruby 1.9.3 (2013-11-22) [x86_64-linux]
    [2015-06-09 23:34:23] INFO  WEBrick::HTTPServer#start: pid=27766 port=3000

## <a name="add-an-endpoint"></a><span data-ttu-id="a1d82-140">Bir uç nokta ekleme</span><span class="sxs-lookup"><span data-stu-id="a1d82-140">Add an endpoint</span></span>
1. <span data-ttu-id="a1d82-141">Git toohello [Azure portalı] [https://portal.azure.com] ve VM'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="a1d82-141">Go toohello [Azure portal][https://portal.azure.com] and select your VM.</span></span>

2. <span data-ttu-id="a1d82-142">Seçin **uç noktaları** hello içinde **ayarları** hello sol kenarı hello sayfa boyunca.</span><span class="sxs-lookup"><span data-stu-id="a1d82-142">Select **ENDPOINTS** in hello **Settings** along hello left edge hello page.</span></span>

3. <span data-ttu-id="a1d82-143">Tıklatın **ekleme** hello sayfanın üst kısmındaki hello.</span><span class="sxs-lookup"><span data-stu-id="a1d82-143">Click **ADD** at hello top of hello page.</span></span>

4. <span data-ttu-id="a1d82-144">Merhaba, **uç nokta ekleme** iletişim sayfasında, aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="a1d82-144">In hello **Add endpoint** dialog page, enter hello following information:</span></span>

   * <span data-ttu-id="a1d82-145">**Ad**: HTTP</span><span class="sxs-lookup"><span data-stu-id="a1d82-145">**Name**: HTTP</span></span>
   * <span data-ttu-id="a1d82-146">**Protokol**: TCP</span><span class="sxs-lookup"><span data-stu-id="a1d82-146">**Protocol**: TCP</span></span>
   * <span data-ttu-id="a1d82-147">**Genel bağlantı noktası**: 80</span><span class="sxs-lookup"><span data-stu-id="a1d82-147">**Public port**: 80</span></span>
   * <span data-ttu-id="a1d82-148">**Özel bağlantı noktası**: 3000</span><span class="sxs-lookup"><span data-stu-id="a1d82-148">**Private port**: 3000</span></span>
   * <span data-ttu-id="a1d82-149">**PI adresi kayan**: devre dışı</span><span class="sxs-lookup"><span data-stu-id="a1d82-149">**Floating PI address**: Disabled</span></span>
   * <span data-ttu-id="a1d82-150">**Erişim denetimi listesi - sipariş**: Bu erişim kuralı hello önceliğini ayarlar 1001 ya da başka bir değer.</span><span class="sxs-lookup"><span data-stu-id="a1d82-150">**Access control list - Order**: 1001, or another value that sets hello priority of this access rule.</span></span>
   * <span data-ttu-id="a1d82-151">**Erişim denetimi listesi - adı**: allowHTTP</span><span class="sxs-lookup"><span data-stu-id="a1d82-151">**Access control list - Name**: allowHTTP</span></span>
   * <span data-ttu-id="a1d82-152">**Erişim denetimi listesi - eylem**: izin ver</span><span class="sxs-lookup"><span data-stu-id="a1d82-152">**Access control list - Action**: permit</span></span>
   * <span data-ttu-id="a1d82-153">**Erişim denetimi listesi - uzak alt**: 1.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="a1d82-153">**Access control list - Remote subnet**: 1.0.0.0/16</span></span>

     <span data-ttu-id="a1d82-154">Bu uç noktaya burada hello rayları sunucu dinliyor trafiğini toohello özel bağlantı noktası 3000, yönlendirecek 80 genel bir bağlantı noktası var.</span><span class="sxs-lookup"><span data-stu-id="a1d82-154">This endpoint  has a public port of 80 that will route traffic toohello private port of 3000, where hello Rails server is listening.</span></span> <span data-ttu-id="a1d82-155">Merhaba erişim denetimi listesi kuralı bağlantı noktası 80 üzerinde ortak trafiğine izin verir.</span><span class="sxs-lookup"><span data-stu-id="a1d82-155">hello access control list rule allows public traffic on port 80.</span></span>

     ![Yeni uç noktası](./media/virtual-machines-linux-classic-ruby-rails-web-app/createendpoint.png)

5. <span data-ttu-id="a1d82-157">Tamam toosave hello uç noktasına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a1d82-157">Click OK toosave hello endpoint.</span></span>

6. <span data-ttu-id="a1d82-158">Bildiren bir ileti görüntülenmelidir **sanal makine uç noktası kaydediliyor**.</span><span class="sxs-lookup"><span data-stu-id="a1d82-158">A message should appear that states **Saving virtual machine endpoint**.</span></span> <span data-ttu-id="a1d82-159">Bu ileti kaybolur sonra hello endpoint etkindir.</span><span class="sxs-lookup"><span data-stu-id="a1d82-159">Once this message disappears, hello endpoint is active.</span></span> <span data-ttu-id="a1d82-160">Şimdi, sanal makinenin DNS adı toohello giderek uygulamanızı test.</span><span class="sxs-lookup"><span data-stu-id="a1d82-160">You may now test your application by navigating toohello DNS name of your virtual machine.</span></span> <span data-ttu-id="a1d82-161">Merhaba Web sitesi toohello aşağıdaki benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="a1d82-161">hello website should appear similar toohello following:</span></span>

    ![Varsayılan rayları sayfası][default-rails-cloud]

## <a name="next-steps"></a><span data-ttu-id="a1d82-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a1d82-163">Next steps</span></span>
<span data-ttu-id="a1d82-164">Bu öğreticide, çoğu hello adımları el ile yaptınız.</span><span class="sxs-lookup"><span data-stu-id="a1d82-164">In this tutorial, you did most of hello steps manually.</span></span> <span data-ttu-id="a1d82-165">Bir üretim ortamında, uygulama geliştirme makinenizde yazmak ve toohello Azure VM dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1d82-165">In a production environment, you would write your app on a development machine and deploy it toohello Azure VM.</span></span> <span data-ttu-id="a1d82-166">Ayrıca, çoğu üretim ortamlarında Apache veya yürüten hello rayları uygulama ve statik kaynakları hizmet veren yönlendirme toomultiple örnekleri isteği NginX gibi başka bir sunucu işlemi ile birlikte Merhaba rayları uygulaması barındırır.</span><span class="sxs-lookup"><span data-stu-id="a1d82-166">Also, most production environments host hello Rails application in conjunction with another server process such as Apache or NginX, which handles request routing toomultiple instances of hello Rails application and serving static resources.</span></span> <span data-ttu-id="a1d82-167">Daha fazla bilgi için http://rubyonrails.org/deploy/ bakın.</span><span class="sxs-lookup"><span data-stu-id="a1d82-167">For more information, see http://rubyonrails.org/deploy/.</span></span>

<span data-ttu-id="a1d82-168">Ruby rayları üzerinde hakkında daha fazla toolearn ziyaret hello [rayları kılavuzları üzerinde Söyleniş][rails-guides].</span><span class="sxs-lookup"><span data-stu-id="a1d82-168">toolearn more about Ruby on Rails, visit hello [Ruby on Rails Guides][rails-guides].</span></span>

<span data-ttu-id="a1d82-169">toouse Söyleniş uygulamanızdan Azure Hizmetleri, bakın:</span><span class="sxs-lookup"><span data-stu-id="a1d82-169">toouse Azure services from your Ruby application, see:</span></span>

* <span data-ttu-id="a1d82-170">[BLOB'ları kullanarak yapılandırılmamış veri depolayın][blobs]</span><span class="sxs-lookup"><span data-stu-id="a1d82-170">[Store unstructured data using blobs][blobs]</span></span>
* <span data-ttu-id="a1d82-171">[Mağaza anahtar/değer çiftlerinin tabloları kullanma][tables]</span><span class="sxs-lookup"><span data-stu-id="a1d82-171">[Store key/value pairs using tables][tables]</span></span>
* <span data-ttu-id="a1d82-172">[İçerik teslim ağı hello ile yüksek bant genişliği içerik sunmak][cdn-howto]</span><span class="sxs-lookup"><span data-stu-id="a1d82-172">[Serve high bandwidth content with hello Content Delivery Network][cdn-howto]</span></span>

<!-- WA.com links -->
[blobs]:../../../storage/blobs/storage-ruby-how-to-use-blob-storage.md
[cdn-howto]:https://azure.microsoft.com/develop/ruby/app-services/
[tables]:../../../cosmos-db/table-storage-how-to-use-ruby.md
[vm-instructions]:createportal.md

<!-- External Links -->
[rails-guides]:http://guides.rubyonrails.org/
[sqlite3]:http://www.sqlite.org/

<!-- Images -->

[default-rails-cloud]:./media/virtual-machines-linux-classic-ruby-rails-web-app/basicrailscloud.png
[vmlist]:./media/virtual-machines-linux-classic-ruby-rails-web-app/vmlist.png
[endpoints]:./media/virtual-machines-linux-classic-ruby-rails-web-app/endpoints.png
[new-endpoint]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint.png
[new-endpoint1]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint1.png
