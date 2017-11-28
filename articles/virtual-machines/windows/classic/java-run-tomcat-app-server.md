---
title: Klasik Azure VM'de aaaRun Java uygulama sunucusu | Microsoft Docs
description: "Bu öğretici hello Klasik dağıtım modeli ve programlarını nasıl oluşturulacağını kaynakları kullanır toocreate bir Windows sanal makine ve toorun Apache Tomcat uygulama sunucusu yapılandırın."
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d627aa09-f7d6-4239-8110-f8fc5111b939
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 03/16/2017
ms.author: robmcm
ms.openlocfilehash: 2d9f586c9f628d3738522b320996b95b078d7454
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-java-application-server-on-a-virtual-machine-created-with-hello-classic-deployment-model"></a><span data-ttu-id="01a87-103">Nasıl toorun bir Java uygulama sunucusu bir sanal makinede hello Klasik dağıtım modeli kullanılarak oluşturulmuş</span><span class="sxs-lookup"><span data-stu-id="01a87-103">How toorun a Java application server on a virtual machine created with hello classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="01a87-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="01a87-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="01a87-105">Bu makalede, hello Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="01a87-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="01a87-106">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="01a87-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="01a87-107">Bir Resource Manager şablonu toodeploy için Java 8 ve Tomcat webapp, bkz: [burada](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).</span><span class="sxs-lookup"><span data-stu-id="01a87-107">For a Resource Manager template toodeploy a webapp with Java 8 and Tomcat, see [here](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).</span></span>

<span data-ttu-id="01a87-108">Azure ile bir sanal makine tooprovide sunucu özelliklerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01a87-108">With Azure, you can use a virtual machine tooprovide server capabilities.</span></span> <span data-ttu-id="01a87-109">Örnek olarak, Azure üzerinde çalışan bir sanal makine yapılandırılmış toohost Apache Tomcat gibi bir Java uygulama sunucusu olabilir.</span><span class="sxs-lookup"><span data-stu-id="01a87-109">As an example, a virtual machine running on Azure can be configured toohost a Java application server, such as Apache Tomcat.</span></span>

<span data-ttu-id="01a87-110">Bu kılavuzu tamamladıktan sonra nasıl bir anlayış gerekir toocreate bir sanal makine Azure üzerinde çalışan ve toorun bir Java uygulama sunucusu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="01a87-110">After completing this guide, you will have an understanding of how toocreate a virtual machine running on Azure and configure it toorun a Java application server.</span></span> <span data-ttu-id="01a87-111">Siz öğrenin ve hello aşağıdaki görevleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="01a87-111">You will learn and perform hello following tasks:</span></span>

* <span data-ttu-id="01a87-112">Nasıl toocreate bir sanal makine, bir Java Geliştirme Seti (zaten yüklü JDK) sahiptir.</span><span class="sxs-lookup"><span data-stu-id="01a87-112">How toocreate a virtual machine that has a Java Development Kit (JDK) already installed.</span></span>
* <span data-ttu-id="01a87-113">Nasıl tooremotely tooyour sanal makinede oturum.</span><span class="sxs-lookup"><span data-stu-id="01a87-113">How tooremotely sign in tooyour virtual machine.</span></span>
* <span data-ttu-id="01a87-114">Nasıl tooinstall bir Java uygulama sunucusu--Apache Tomcat--sanal makinenizde.</span><span class="sxs-lookup"><span data-stu-id="01a87-114">How tooinstall a Java application server--Apache Tomcat--on your virtual machine.</span></span>
* <span data-ttu-id="01a87-115">Nasıl toocreate sanal makineniz için bir uç nokta.</span><span class="sxs-lookup"><span data-stu-id="01a87-115">How toocreate an endpoint for your virtual machine.</span></span>
* <span data-ttu-id="01a87-116">Nasıl tooopen hello bir bağlantı noktası güvenlik duvarı, uygulama sunucusu için.</span><span class="sxs-lookup"><span data-stu-id="01a87-116">How tooopen a port in hello firewall for your application server.</span></span>

<span data-ttu-id="01a87-117">Merhaba, bir sanal makinede çalışan Tomcat yükleme sonuçlarında tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="01a87-117">hello completed installation results in Tomcat running on a virtual machine.</span></span>

![Apache Tomcat çalıştıran sanal makine][virtual_machine_tomcat]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a><span data-ttu-id="01a87-119">toocreate bir sanal makine</span><span class="sxs-lookup"><span data-stu-id="01a87-119">toocreate a virtual machine</span></span>
1. <span data-ttu-id="01a87-120">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="01a87-120">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="01a87-121">' I tıklatın **yeni**, tıklatın **işlem**, ardından **tümünü görmek** hello içinde **öne çıkan uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="01a87-121">Click **New**, click **Compute**, then click **See all** in hello **Featured apps**.</span></span>
3. <span data-ttu-id="01a87-122">Tıklatın **JDK**, tıklatın **JDK 8** hello içinde **JDK** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="01a87-122">Click **JDK**, click **JDK 8** in hello **JDK** pane.</span></span>  
   <span data-ttu-id="01a87-123">Sanal makine görüntüleri destekleyen **JDK 6** ve **JDK 7** hazır toorun JDK 8 olmayan eski uygulamalarınız varsa kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="01a87-123">Virtual machine images that support **JDK 6** and **JDK 7** are available if you have legacy applications that are not ready toorun in JDK 8.</span></span>
4. <span data-ttu-id="01a87-124">Merhaba JDK 8 bölmesinde seçin **Klasik**, ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="01a87-124">In hello JDK 8 pane, select **Classic**, then click **Create**.</span></span>
5. <span data-ttu-id="01a87-125">Merhaba, **Temelleri** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="01a87-125">In hello **Basics** blade:</span></span>
   1. <span data-ttu-id="01a87-126">Merhaba sanal makine için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="01a87-126">Specify a name for hello virtual machine.</span></span>
   2. <span data-ttu-id="01a87-127">Hello Merhaba yönetici adı **kullanıcı adı** alan.</span><span class="sxs-lookup"><span data-stu-id="01a87-127">Enter a name for hello administrator in hello **User Name** field.</span></span> <span data-ttu-id="01a87-128">Merhaba sonraki alanda izleyen ilişkili parola hello ve bu ad unutmayın.</span><span class="sxs-lookup"><span data-stu-id="01a87-128">Remember this name and hello associated password that follows in hello next field.</span></span> <span data-ttu-id="01a87-129">Uzaktan toohello sanal makinede oturum açtığınızda, bunları gerekir.</span><span class="sxs-lookup"><span data-stu-id="01a87-129">You need them when you remotely sign in toohello virtual machine.</span></span>
   3. <span data-ttu-id="01a87-130">Hello bir parola girmenizi **yeni parola** alan ve hello girmek **parolayı onayla** alan.</span><span class="sxs-lookup"><span data-stu-id="01a87-130">Enter a password in hello **New password** field, and reenter it in hello **Confirm password** field.</span></span> <span data-ttu-id="01a87-131">Bu parola Merhaba yönetici hesabı değil.</span><span class="sxs-lookup"><span data-stu-id="01a87-131">This password is for hello Administrator account.</span></span>
   4. <span data-ttu-id="01a87-132">Select hello uygun **abonelik**.</span><span class="sxs-lookup"><span data-stu-id="01a87-132">Select hello appropriate **Subscription**.</span></span>
   5. <span data-ttu-id="01a87-133">Hello için **kaynak grubu**, tıklatın **Yeni Oluştur** ve yeni bir kaynak grubu hello adını girin.</span><span class="sxs-lookup"><span data-stu-id="01a87-133">For hello **Resource group**, click **Create new** and enter hello name of a new resource group.</span></span> <span data-ttu-id="01a87-134">Veya tıklatın **var olanı kullan** bir hello kullanılabilir kaynak gruplarını seçin.</span><span class="sxs-lookup"><span data-stu-id="01a87-134">Or, click **Use existing** and select one of hello available resource groups.</span></span>
   6. <span data-ttu-id="01a87-135">Merhaba sanal makinenin bulunduğu, gibi bir konum seçin **Orta Güney ABD**.</span><span class="sxs-lookup"><span data-stu-id="01a87-135">Select a location where hello virtual machine resides, such as **South Central US**.</span></span>
6. <span data-ttu-id="01a87-136">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="01a87-136">Click **Next**.</span></span>
7. <span data-ttu-id="01a87-137">Merhaba, **sanal makine görüntü boyutu** dikey penceresinde, select **A1 standart** veya başka bir uygun görüntü.</span><span class="sxs-lookup"><span data-stu-id="01a87-137">In hello **Virtual machine image size** blade, select **A1 Standard** or another appropriate image.</span></span>
8. <span data-ttu-id="01a87-138">**Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="01a87-138">Click **Select**.</span></span>

9. <span data-ttu-id="01a87-139">Merhaba, **ayarları** dikey penceresinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="01a87-139">In hello **Settings** blade, click **OK**.</span></span> <span data-ttu-id="01a87-140">Azure tarafından sağlanan hello varsayılan değerleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01a87-140">You can use hello default values provided by Azure.</span></span>  
10. <span data-ttu-id="01a87-141">Merhaba, **Özet** dikey penceresinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="01a87-141">In hello **Summary** blade, click **OK**.</span></span>

## <a name="tooremotely-sign-in-tooyour-virtual-machine"></a><span data-ttu-id="01a87-142">tooremotely oturum tooyour sanal makineyi açma</span><span class="sxs-lookup"><span data-stu-id="01a87-142">tooremotely sign in tooyour virtual machine</span></span>
1. <span data-ttu-id="01a87-143">Toohello üzerinde oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="01a87-143">Log on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="01a87-144">Tıklatın **sanal makineleri (Klasik)**.</span><span class="sxs-lookup"><span data-stu-id="01a87-144">Click **Virtual machines (classic)**.</span></span> <span data-ttu-id="01a87-145">Gerekirse, tıklatın **daha fazla hizmet** hello alt sol köşesinde hello Hizmet Kategoriler altında.</span><span class="sxs-lookup"><span data-stu-id="01a87-145">If needed, click **More services** at hello bottom left corner under hello service categories.</span></span> <span data-ttu-id="01a87-146">Merhaba **sanal makineleri (Klasik)** hello listelen giriş **işlem** grubu.</span><span class="sxs-lookup"><span data-stu-id="01a87-146">hello **Virtual machines (classic)** entry is listed in hello **Compute** group.</span></span>
3. <span data-ttu-id="01a87-147">Merhaba, toosign istediğiniz içinde hello sanal makine adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="01a87-147">Click hello name of hello virtual machine that you want toosign in to.</span></span>
4. <span data-ttu-id="01a87-148">Merhaba sanal makine başlatıldıktan sonra hello bölmesini hello üstündeki menü bağlantılara izin verir.</span><span class="sxs-lookup"><span data-stu-id="01a87-148">After hello virtual machine has started, a menu at hello top of hello pane allows connections.</span></span>
5. <span data-ttu-id="01a87-149">**Bağlan**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="01a87-149">Click **Connect**.</span></span>
6. <span data-ttu-id="01a87-150">Yanıt toohello gerekli tooconnect toohello sanal makine olarak ister.</span><span class="sxs-lookup"><span data-stu-id="01a87-150">Respond toohello prompts as needed tooconnect toohello virtual machine.</span></span> <span data-ttu-id="01a87-151">Genellikle, kaydedin veya hello bağlantı ayrıntılarını içeren hello .rdp dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="01a87-151">Typically, you save or open hello .rdp file that contains hello connection details.</span></span> <span data-ttu-id="01a87-152">Merhaba son hello .rdp dosyasının ilk satırı hello kapsamında toocopy hello url: bağlantı noktası sahip ve bir uzak oturum açma uygulamasında yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="01a87-152">You might have toocopy hello url:port as hello last part of hello first line of hello .rdp file and paste it in a remote sign-in application.</span></span>

## <a name="tooinstall-a-java-application-server-on-your-virtual-machine"></a><span data-ttu-id="01a87-153">tooinstall sanal makinenizde bir Java uygulama sunucusu</span><span class="sxs-lookup"><span data-stu-id="01a87-153">tooinstall a Java application server on your virtual machine</span></span>
<span data-ttu-id="01a87-154">Java uygulama sunucusu tooyour sanal makine kopyalayabilir veya bir yükleyici aracılığıyla bir Java uygulama sunucusu yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01a87-154">You can copy a Java application server tooyour virtual machine, or you can install a Java application server through an installer.</span></span>

<span data-ttu-id="01a87-155">Bu öğretici Tomcat hello Java uygulama sunucusu tooinstall kullanır.</span><span class="sxs-lookup"><span data-stu-id="01a87-155">This tutorial uses Tomcat as hello Java application server tooinstall.</span></span>

1. <span data-ttu-id="01a87-156">Tooyour sanal makinede imzalandığında bir tarayıcı oturumu çok açın[Apache Tomcat](http://tomcat.apache.org/download-80.cgi).</span><span class="sxs-lookup"><span data-stu-id="01a87-156">When you are signed in tooyour virtual machine, open a browser session too[Apache Tomcat](http://tomcat.apache.org/download-80.cgi).</span></span>
2. <span data-ttu-id="01a87-157">Merhaba bağlantı için çift **32-bit/64-bit Windows hizmeti yükleyicisini**.</span><span class="sxs-lookup"><span data-stu-id="01a87-157">Double-click hello link for **32-bit/64-bit Windows Service Installer**.</span></span> <span data-ttu-id="01a87-158">Bu yöntemi kullanarak, Tomcat bir Windows hizmeti olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="01a87-158">By using this technique, Tomcat installs as a Windows service.</span></span>
3. <span data-ttu-id="01a87-159">İstendiğinde, toorun hello yükleyici seçin.</span><span class="sxs-lookup"><span data-stu-id="01a87-159">When prompted, choose toorun hello installer.</span></span>
4. <span data-ttu-id="01a87-160">Merhaba içinde **Apache Tomcat Kurulum** Sihirbazı, izleme hello tooinstall Tomcat ister.</span><span class="sxs-lookup"><span data-stu-id="01a87-160">Within hello **Apache Tomcat Setup** wizard, follow hello prompts tooinstall Tomcat.</span></span> <span data-ttu-id="01a87-161">Bu öğreticinin Hello amaçları hello varsayılan değerleri kabul ederek uygundur.</span><span class="sxs-lookup"><span data-stu-id="01a87-161">For hello purposes of this tutorial, accepting hello defaults is fine.</span></span> <span data-ttu-id="01a87-162">Merhaba ulaştığınızda **Tamamlanıyor hello Apache Tomcat Kurulum Sihirbazı'nı** iletişim kutusu, isteğe bağlı olarak kontrol edebilirsiniz **çalıştırmak Apache Tomcat** toohave şimdi Tomcat Başlat.</span><span class="sxs-lookup"><span data-stu-id="01a87-162">When you reach hello **Completing hello Apache Tomcat Setup Wizard** dialog box, you can optionally check **Run Apache Tomcat** toohave Tomcat start now.</span></span> <span data-ttu-id="01a87-163">Tıklatın **son** toocomplete hello Tomcat Kurulum işlemi.</span><span class="sxs-lookup"><span data-stu-id="01a87-163">Click **Finish** toocomplete hello Tomcat setup process.</span></span>

## <a name="toostart-tomcat"></a><span data-ttu-id="01a87-164">toostart Tomcat</span><span class="sxs-lookup"><span data-stu-id="01a87-164">toostart Tomcat</span></span>

<span data-ttu-id="01a87-165">Sanal makine ve çalışan hello komutunu bir komut istemi'ni açarak, Tomcat el ile başlatabilirsiniz **net&nbsp;Başlat&nbsp;Tomcat8**.</span><span class="sxs-lookup"><span data-stu-id="01a87-165">You can manually start Tomcat by opening a command prompt on your virtual machine and running hello command **net&nbsp;start&nbsp;Tomcat8**.</span></span>

<span data-ttu-id="01a87-166">Tomcat çalışmaya başladıktan sonra Tomcat hello URL'yi girerek erişebileceğiniz <http://localhost: 8080> hello sanal makinenin tarayıcıda.</span><span class="sxs-lookup"><span data-stu-id="01a87-166">Once Tomcat is running, you can access Tomcat by entering hello URL <http://localhost:8080> in hello virtual machine's browser.</span></span>

<span data-ttu-id="01a87-167">toosee dış makinelerden çalıştıran Tomcat, toocreate bir uç nokta gerekir ve bir bağlantı noktası açın.</span><span class="sxs-lookup"><span data-stu-id="01a87-167">toosee Tomcat running from external machines, you need toocreate an endpoint and open a port.</span></span>

## <a name="toocreate-an-endpoint-for-your-virtual-machine"></a><span data-ttu-id="01a87-168">toocreate sanal makineniz için bir uç nokta</span><span class="sxs-lookup"><span data-stu-id="01a87-168">toocreate an endpoint for your virtual machine</span></span>
1. <span data-ttu-id="01a87-169">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="01a87-169">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="01a87-170">Tıklatın **sanal makineleri (Klasik)**.</span><span class="sxs-lookup"><span data-stu-id="01a87-170">Click **Virtual machines (classic)**.</span></span>
3. <span data-ttu-id="01a87-171">Java uygulama sunucusu çalışıyor hello sanal makine Hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="01a87-171">Click hello name of hello virtual machine that is running your Java application server.</span></span>
4. <span data-ttu-id="01a87-172">**Uç Noktalar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="01a87-172">Click **Endpoints**.</span></span>
5. <span data-ttu-id="01a87-173">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="01a87-173">Click **Add**.</span></span>
6. <span data-ttu-id="01a87-174">Merhaba, **uç nokta ekleme** iletişim kutusunda:</span><span class="sxs-lookup"><span data-stu-id="01a87-174">In hello **Add endpoint** dialog box:</span></span>
   1. <span data-ttu-id="01a87-175">Merhaba uç noktası için bir ad belirtin; Örneğin, **HttpIn**.</span><span class="sxs-lookup"><span data-stu-id="01a87-175">Specify a name for hello endpoint; for example, **HttpIn**.</span></span>
   2. <span data-ttu-id="01a87-176">Seçin **TCP** hello protokolü için.</span><span class="sxs-lookup"><span data-stu-id="01a87-176">Select **TCP** for hello protocol.</span></span>
   3. <span data-ttu-id="01a87-177">Belirtin **80** hello genel bağlantı noktası için.</span><span class="sxs-lookup"><span data-stu-id="01a87-177">Specify **80** for hello public port.</span></span>
   4. <span data-ttu-id="01a87-178">Belirtin **8080** hello özel bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="01a87-178">Specify **8080** for hello private port.</span></span>
   5. <span data-ttu-id="01a87-179">Seçin **devre dışı** hello kayan IP adresi için.</span><span class="sxs-lookup"><span data-stu-id="01a87-179">Select **Disabled** for hello floating IP address.</span></span>
   6. <span data-ttu-id="01a87-180">Merhaba erişim denetim listesi olduğu gibi bırakın.</span><span class="sxs-lookup"><span data-stu-id="01a87-180">Leave hello access control list as is.</span></span>
   7. <span data-ttu-id="01a87-181">Merhaba tıklatın **Tamam** düğmesini tooclose hello iletişim kutusu ve hello uç noktası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="01a87-181">Click hello **OK** button tooclose hello dialog box and create hello endpoint.</span></span>

## <a name="tooopen-a-port-in-hello-firewall-for-your-virtual-machine"></a><span data-ttu-id="01a87-182">tooopen hello Güvenlik Duvarı'nda, sanal makine için bir bağlantı noktası</span><span class="sxs-lookup"><span data-stu-id="01a87-182">tooopen a port in hello firewall for your virtual machine</span></span>
1. <span data-ttu-id="01a87-183">Tooyour sanal makinede oturum açın.</span><span class="sxs-lookup"><span data-stu-id="01a87-183">Sign in tooyour virtual machine.</span></span>
2. <span data-ttu-id="01a87-184">Tıklatın **Windows Başlangıç**.</span><span class="sxs-lookup"><span data-stu-id="01a87-184">Click **Windows Start**.</span></span>
3. <span data-ttu-id="01a87-185">Tıklatın **Denetim Masası**.</span><span class="sxs-lookup"><span data-stu-id="01a87-185">Click **Control Panel**.</span></span>
4. <span data-ttu-id="01a87-186">Tıklatın **sistem ve güvenlik**, tıklatın **Windows Güvenlik Duvarı**ve ardından **Gelişmiş ayarları**.</span><span class="sxs-lookup"><span data-stu-id="01a87-186">Click **System and Security**, click **Windows Firewall**, and then click **Advanced Settings**.</span></span>
5. <span data-ttu-id="01a87-187">Tıklatın **gelen kuralları**ve ardından **yeni kural**.</span><span class="sxs-lookup"><span data-stu-id="01a87-187">Click **Inbound Rules**, and then click **New Rule**.</span></span>  
   <span data-ttu-id="01a87-188">![Yeni gelen kuralı][NewIBRule]</span><span class="sxs-lookup"><span data-stu-id="01a87-188">![New inbound rule][NewIBRule]</span></span>
6. <span data-ttu-id="01a87-189">Hello için **kural türü**seçin **bağlantı noktası**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="01a87-189">For hello **Rule Type**, select **Port**, and then click **Next**.</span></span>  
   <span data-ttu-id="01a87-190">![Yeni gelen kuralı bağlantı noktası][NewRulePort]</span><span class="sxs-lookup"><span data-stu-id="01a87-190">![New inbound rule port][NewRulePort]</span></span>
7. <span data-ttu-id="01a87-191">Merhaba üzerinde **protokol ve bağlantı noktaları** ekran, select **TCP**, belirtin **8080** hello olarak **belirli yerel bağlantı noktası**ve ardından **Sonraki**.</span><span class="sxs-lookup"><span data-stu-id="01a87-191">On hello **Protocol and Ports** screen, select **TCP**, specify **8080** as hello **Specific local port**, and then click **Next**.</span></span>  
  <span data-ttu-id="01a87-192">![Yeni gelen kuralı][NewRuleProtocol]</span><span class="sxs-lookup"><span data-stu-id="01a87-192">![New inbound rule ][NewRuleProtocol]</span></span>
8. <span data-ttu-id="01a87-193">Merhaba üzerinde **eylem** ekran, select **hello bağlantıya izin verme**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="01a87-193">On hello **Action** screen, select **Allow hello connection**, and then click **Next**.</span></span>
   <span data-ttu-id="01a87-194">![Yeni gelen kuralı eylemi][NewRuleAction]</span><span class="sxs-lookup"><span data-stu-id="01a87-194">![New inbound rule action][NewRuleAction]</span></span>
9. <span data-ttu-id="01a87-195">Merhaba üzerinde **profil** ekranında, emin **etki alanı**, **özel**, ve **ortak** seçilir ve ardından **sonraki** .</span><span class="sxs-lookup"><span data-stu-id="01a87-195">On hello **Profile** screen, ensure that **Domain**, **Private**, and **Public** are selected, and then click **Next**.</span></span>
   <span data-ttu-id="01a87-196">![Yeni gelen kuralı profili][NewRuleProfile]</span><span class="sxs-lookup"><span data-stu-id="01a87-196">![New inbound rule profile][NewRuleProfile]</span></span>
10. <span data-ttu-id="01a87-197">Merhaba üzerinde **adı** ekranında, hello kuralı için bir ad belirtin **HttpIn** (Merhaba kural adı gerekli toomatch hello uç nokta adı değil, ancak) ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="01a87-197">On hello **Name** screen, specify a name for hello rule, such as **HttpIn** (hello rule name is not required toomatch hello endpoint name, however), and then click **Finish**.</span></span>  
    <span data-ttu-id="01a87-198">![Yeni gelen kuralı adı][NewRuleName]</span><span class="sxs-lookup"><span data-stu-id="01a87-198">![New inbound rule name][NewRuleName]</span></span>

<span data-ttu-id="01a87-199">Bu noktada, Tomcat Web sitenizi dış bir tarayıcıdan görüntülenebilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="01a87-199">At this point, your Tomcat website should be viewable from an external browser.</span></span> <span data-ttu-id="01a87-200">Merhaba tarayıcının adres penceresinde hello form URL'sini yazın  **http://*,\_DNS\_adı*. cloudapp.net**, burada ***,\_DNS\_adı*** hello sanal makineyi oluşturduğunuzda belirttiğiniz hello DNS adı.</span><span class="sxs-lookup"><span data-stu-id="01a87-200">In hello browser's address window, type a URL of hello form **http://*your\_DNS\_name*.cloudapp.net**, where ***your\_DNS\_name*** is hello DNS name you specified when you created hello virtual machine.</span></span>

## <a name="application-lifecycle-considerations"></a><span data-ttu-id="01a87-201">Uygulama yaşam döngüsü hakkında dikkat edilecek noktalar</span><span class="sxs-lookup"><span data-stu-id="01a87-201">Application lifecycle considerations</span></span>
* <span data-ttu-id="01a87-202">Kendi web uygulama Arşivi (WAR) oluşturun ve toohello eklemek **webapps** klasör.</span><span class="sxs-lookup"><span data-stu-id="01a87-202">You could create your own web application archive (WAR) and add it toohello **webapps** folder.</span></span> <span data-ttu-id="01a87-203">Örneğin, bir temel Java hizmet sayfa (JSP) dinamik web projesi oluşturun ve bir WAR dosyası olarak dışarı aktarma.</span><span class="sxs-lookup"><span data-stu-id="01a87-203">For example, create a basic Java Service Page (JSP) dynamic web project and export it as a WAR file.</span></span> <span data-ttu-id="01a87-204">Ardından, hello WAR toohello Apache Tomcat kopyalama **webapps** klasörü hello sanal makineye, ardından bir tarayıcıda çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="01a87-204">Next, copy hello WAR toohello Apache Tomcat **webapps** folder on hello virtual machine, then run it in a browser.</span></span>
* <span data-ttu-id="01a87-205">Merhaba Tomcat hizmeti yüklü olduğunda, varsayılan olarak toostart onu el ile ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="01a87-205">By default when hello Tomcat service is installed, it is set toostart manually.</span></span> <span data-ttu-id="01a87-206">Bu toostart otomatik olarak hello Hizmetler ek bileşenini kullanarak geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01a87-206">You can switch it toostart automatically by using hello Services snap-in.</span></span> <span data-ttu-id="01a87-207">Tıklayarak Hello Hizmetler ek bileşenini başlatın **Windows Başlat**, **Yönetimsel Araçlar**ve ardından **Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="01a87-207">Start hello Services snap-in by clicking **Windows Start**, **Administrative Tools**, and then **Services**.</span></span> <span data-ttu-id="01a87-208">Merhaba çift **Apache Tomcat** ayarlayın ve hizmeti **başlangıç türü** çok**otomatik**.</span><span class="sxs-lookup"><span data-stu-id="01a87-208">Double-click hello **Apache Tomcat** service and set **Startup type** too**Automatic**.</span></span>

    ![Bir hizmet toostart otomatik olarak ayarlama][service_automatic_startup]

    <span data-ttu-id="01a87-210">Merhaba otomatik olarak Başlat Tomcat sahip olmanın avantaj (örneğin, yeniden başlatma gerektiren yazılım güncelleştirmeleri yüklendikten sonra) hello sanal makine yeniden başlatıldığında çalışmaya başladıktan emin olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="01a87-210">hello benefit of having Tomcat start automatically is that it starts running when hello virtual machine is rebooted (for example, after software updates that require a reboot are installed).</span></span>

## <a name="next-steps"></a><span data-ttu-id="01a87-211">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="01a87-211">Next steps</span></span>
<span data-ttu-id="01a87-212">İsteyebileceğiniz diğer hizmetler hakkında (örneğin, Azure Storage, hizmet veri yolu ve SQL veritabanı) öğrenebilirsiniz tooinclude Java uygulamaları ile.</span><span class="sxs-lookup"><span data-stu-id="01a87-212">You can learn about other services (such as Azure Storage, service bus, and SQL Database) that you may want tooinclude with your Java applications.</span></span> <span data-ttu-id="01a87-213">Merhaba kullanılabilir hello bilgileri görüntüleyin [Java Geliştirici Merkezi](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="01a87-213">View hello information available at hello [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[virtual_machine_tomcat]:media/java-run-tomcat-app-server/WA_VirtualMachineRunningApacheTomcat.png

[service_automatic_startup]:media/java-run-tomcat-app-server/WA_TomcatServiceAutomaticStart.png









[NewIBRule]:media/java-run-tomcat-app-server/NewInboundRule.png
[NewRulePort]:media/java-run-tomcat-app-server/NewRulePort.png
[NewRuleProtocol]:media/java-run-tomcat-app-server/NewRuleProtocol.png
[NewRuleAction]:media/java-run-tomcat-app-server/NewRuleAction.png
[NewRuleName]:media/java-run-tomcat-app-server/NewRuleName.png
[NewRuleProfile]:media/java-run-tomcat-app-server/NewRuleProfile.png


<!-- Deleted from hello "toocreate an ednpoint for your virtual mache" 3/17/2017,
     toouse hello new portal.
6. In hello **Add endpoint** dialog box, ensure **Add standalone endpoint** is selected, and then click **Next**.
7. In hello **New endpoint details** dialog box:
-->
