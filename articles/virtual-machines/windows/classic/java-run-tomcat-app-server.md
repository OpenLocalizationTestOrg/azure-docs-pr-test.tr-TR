---
title: "Java uygulama sunucusu bir Klasik Azure VM üzerinde çalışan | Microsoft Docs"
description: "Bu öğretici, Klasik dağıtım modeli kullanılarak oluşturulmuş kaynaklarını kullanır ve bir Windows sanal makine oluşturma ve Apache Tomcat uygulama sunucusu çalıştırmak için yapılandırın gösterir."
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
ms.openlocfilehash: 6e02f42613808bcb13c0057e9f8fcc1c02273e77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-run-a-java-application-server-on-a-virtual-machine-created-with-the-classic-deployment-model"></a><span data-ttu-id="99d4f-103">Klasik dağıtım modeliyle oluşturulan bir sanal makinede Java uygulama sunucusu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="99d4f-103">How to run a Java application server on a virtual machine created with the classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="99d4f-104">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Resource Manager ve klasik](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="99d4f-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="99d4f-105">Bu makalede, Klasik dağıtım modeli kullanarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="99d4f-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="99d4f-106">Microsoft, yeni dağıtımların çoğunun Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="99d4f-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="99d4f-107">Resource Manager şablonu webapp Java 8 ve Tomcat ile dağıtmak bkz: [burada](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).</span><span class="sxs-lookup"><span data-stu-id="99d4f-107">For a Resource Manager template to deploy a webapp with Java 8 and Tomcat, see [here](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).</span></span>

<span data-ttu-id="99d4f-108">Azure ile sunucu yetenekleri sağlamak için bir sanal makine kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99d4f-108">With Azure, you can use a virtual machine to provide server capabilities.</span></span> <span data-ttu-id="99d4f-109">Örnek olarak, Azure üzerinde çalışan bir sanal makine Apache Tomcat gibi bir Java uygulama sunucusu barındırmak için yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="99d4f-109">As an example, a virtual machine running on Azure can be configured to host a Java application server, such as Apache Tomcat.</span></span>

<span data-ttu-id="99d4f-110">Bu kılavuzu tamamladıktan sonra Azure üzerinde çalışan bir sanal makine oluşturun ve bunu bir Java uygulama sunucusu çalıştırmak için yapılandırmak üzere nasıl anlaşılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="99d4f-110">After completing this guide, you will have an understanding of how to create a virtual machine running on Azure and configure it to run a Java application server.</span></span> <span data-ttu-id="99d4f-111">Bilgi işlem ve aşağıdaki görevleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="99d4f-111">You will learn and perform the following tasks:</span></span>

* <span data-ttu-id="99d4f-112">Bir Java Geliştirme Seti (zaten yüklü JDK) sahip olan bir sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="99d4f-112">How to create a virtual machine that has a Java Development Kit (JDK) already installed.</span></span>
* <span data-ttu-id="99d4f-113">Sanal makinenize uzaktan oturum açma.</span><span class="sxs-lookup"><span data-stu-id="99d4f-113">How to remotely sign in to your virtual machine.</span></span>
* <span data-ttu-id="99d4f-114">Bir Java uygulama sunucusu--Apache Tomcat--sanal makinenizde nasıl yüklenir.</span><span class="sxs-lookup"><span data-stu-id="99d4f-114">How to install a Java application server--Apache Tomcat--on your virtual machine.</span></span>
* <span data-ttu-id="99d4f-115">Sanal makineniz için bir uç nokta oluşturma</span><span class="sxs-lookup"><span data-stu-id="99d4f-115">How to create an endpoint for your virtual machine.</span></span>
* <span data-ttu-id="99d4f-116">Güvenlik Duvarı'nda, uygulama sunucusu için bir bağlantı noktasını açmak nasıl.</span><span class="sxs-lookup"><span data-stu-id="99d4f-116">How to open a port in the firewall for your application server.</span></span>

<span data-ttu-id="99d4f-117">Bir sanal makinede çalışan Tomcat yükleme tamamlandı sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="99d4f-117">The completed installation results in Tomcat running on a virtual machine.</span></span>

![Apache Tomcat çalıştıran sanal makine][virtual_machine_tomcat]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="to-create-a-virtual-machine"></a><span data-ttu-id="99d4f-119">Sanal makine oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="99d4f-119">To create a virtual machine</span></span>
1. <span data-ttu-id="99d4f-120">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="99d4f-120">Sign in to the [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="99d4f-121">Tıklatın **yeni**, tıklatın **işlem**, ardından **tümünü görmek** içinde **öne çıkan uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="99d4f-121">Click **New**, click **Compute**, then click **See all** in the **Featured apps**.</span></span>
3. <span data-ttu-id="99d4f-122">Tıklatın **JDK**, tıklatın **JDK 8** içinde **JDK** bölmesi.</span><span class="sxs-lookup"><span data-stu-id="99d4f-122">Click **JDK**, click **JDK 8** in the **JDK** pane.</span></span>  
   <span data-ttu-id="99d4f-123">Sanal makine görüntüleri destekleyen **JDK 6** ve **JDK 7** JDK 8'de çalıştırmak hazır olmayan eski uygulamalarınız varsa kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="99d4f-123">Virtual machine images that support **JDK 6** and **JDK 7** are available if you have legacy applications that are not ready to run in JDK 8.</span></span>
4. <span data-ttu-id="99d4f-124">JDK 8 bölmesinde seçin **Klasik**, ardından **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="99d4f-124">In the JDK 8 pane, select **Classic**, then click **Create**.</span></span>
5. <span data-ttu-id="99d4f-125">İçinde **Temelleri** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="99d4f-125">In the **Basics** blade:</span></span>
   1. <span data-ttu-id="99d4f-126">Sanal makine için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="99d4f-126">Specify a name for the virtual machine.</span></span>
   2. <span data-ttu-id="99d4f-127">Bir yönetici adı **kullanıcı adı** alan.</span><span class="sxs-lookup"><span data-stu-id="99d4f-127">Enter a name for the administrator in the **User Name** field.</span></span> <span data-ttu-id="99d4f-128">Bu ad ve sonraki alanda izleyen ilişkili parolayı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="99d4f-128">Remember this name and the associated password that follows in the next field.</span></span> <span data-ttu-id="99d4f-129">Sanal makineye uzaktan oturum açtığınızda, bunları gerekir.</span><span class="sxs-lookup"><span data-stu-id="99d4f-129">You need them when you remotely sign in to the virtual machine.</span></span>
   3. <span data-ttu-id="99d4f-130">Bir parolayı girin **yeni parola** alan ve girin **parolayı onayla** alan.</span><span class="sxs-lookup"><span data-stu-id="99d4f-130">Enter a password in the **New password** field, and reenter it in the **Confirm password** field.</span></span> <span data-ttu-id="99d4f-131">Bu parola yönetici hesabıdır.</span><span class="sxs-lookup"><span data-stu-id="99d4f-131">This password is for the Administrator account.</span></span>
   4. <span data-ttu-id="99d4f-132">Uygun seçin **abonelik**.</span><span class="sxs-lookup"><span data-stu-id="99d4f-132">Select the appropriate **Subscription**.</span></span>
   5. <span data-ttu-id="99d4f-133">İçin **kaynak grubu**, tıklatın **Yeni Oluştur** ve yeni bir kaynak grubu adını girin.</span><span class="sxs-lookup"><span data-stu-id="99d4f-133">For the **Resource group**, click **Create new** and enter the name of a new resource group.</span></span> <span data-ttu-id="99d4f-134">Veya tıklatın **var olanı kullan** ve kullanılabilir kaynak gruplarını birini seçin.</span><span class="sxs-lookup"><span data-stu-id="99d4f-134">Or, click **Use existing** and select one of the available resource groups.</span></span>
   6. <span data-ttu-id="99d4f-135">Sanal makinenin bulunduğu, gibi bir konum seçin **Orta Güney ABD**.</span><span class="sxs-lookup"><span data-stu-id="99d4f-135">Select a location where the virtual machine resides, such as **South Central US**.</span></span>
6. <span data-ttu-id="99d4f-136">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="99d4f-136">Click **Next**.</span></span>
7. <span data-ttu-id="99d4f-137">İçinde **sanal makine görüntü boyutu** dikey penceresinde, select **A1 standart** veya başka bir uygun görüntü.</span><span class="sxs-lookup"><span data-stu-id="99d4f-137">In the **Virtual machine image size** blade, select **A1 Standard** or another appropriate image.</span></span>
8. <span data-ttu-id="99d4f-138">**Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="99d4f-138">Click **Select**.</span></span>

9. <span data-ttu-id="99d4f-139">İçinde **ayarları** dikey penceresinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="99d4f-139">In the **Settings** blade, click **OK**.</span></span> <span data-ttu-id="99d4f-140">Azure tarafından sağlanan varsayılan değerleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99d4f-140">You can use the default values provided by Azure.</span></span>  
10. <span data-ttu-id="99d4f-141">İçinde **Özet** dikey penceresinde tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="99d4f-141">In the **Summary** blade, click **OK**.</span></span>

## <a name="to-remotely-sign-in-to-your-virtual-machine"></a><span data-ttu-id="99d4f-142">Sanal makinenize uzaktan oturum açmak için</span><span class="sxs-lookup"><span data-stu-id="99d4f-142">To remotely sign in to your virtual machine</span></span>
1. <span data-ttu-id="99d4f-143">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="99d4f-143">Log on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="99d4f-144">Tıklatın **sanal makineleri (Klasik)**.</span><span class="sxs-lookup"><span data-stu-id="99d4f-144">Click **Virtual machines (classic)**.</span></span> <span data-ttu-id="99d4f-145">Gerekirse, tıklatın **daha fazla hizmet** hizmeti kategoriler altında sol alt köşedeki adresindeki.</span><span class="sxs-lookup"><span data-stu-id="99d4f-145">If needed, click **More services** at the bottom left corner under the service categories.</span></span> <span data-ttu-id="99d4f-146">**Sanal makineleri (Klasik)** girişi listelenir **işlem** grubu.</span><span class="sxs-lookup"><span data-stu-id="99d4f-146">The **Virtual machines (classic)** entry is listed in the **Compute** group.</span></span>
3. <span data-ttu-id="99d4f-147">Oturum açmak için istediğiniz sanal makinenin adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="99d4f-147">Click the name of the virtual machine that you want to sign in to.</span></span>
4. <span data-ttu-id="99d4f-148">Sanal makine başlatıldıktan sonra bölmenin üstündeki menü bağlantılara izin verir.</span><span class="sxs-lookup"><span data-stu-id="99d4f-148">After the virtual machine has started, a menu at the top of the pane allows connections.</span></span>
5. <span data-ttu-id="99d4f-149">**Bağlan**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="99d4f-149">Click **Connect**.</span></span>
6. <span data-ttu-id="99d4f-150">Sanal makineye bağlanmak için gereken şekilde yanıtlamasına.</span><span class="sxs-lookup"><span data-stu-id="99d4f-150">Respond to the prompts as needed to connect to the virtual machine.</span></span> <span data-ttu-id="99d4f-151">Genellikle, kaydedin veya bağlantı ayrıntılarını içeren .rdp dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="99d4f-151">Typically, you save or open the .rdp file that contains the connection details.</span></span> <span data-ttu-id="99d4f-152">Url: bağlantı noktası .rdp dosyasının ilk satırı son parçası olarak kopyalayın ve bir uzak oturum açma uygulamasında yapıştırmak zorunda kalabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99d4f-152">You might have to copy the url:port as the last part of the first line of the .rdp file and paste it in a remote sign-in application.</span></span>

## <a name="to-install-a-java-application-server-on-your-virtual-machine"></a><span data-ttu-id="99d4f-153">Sanal makinenizde bir Java uygulama sunucusu yüklemek için</span><span class="sxs-lookup"><span data-stu-id="99d4f-153">To install a Java application server on your virtual machine</span></span>
<span data-ttu-id="99d4f-154">Java uygulama sunucusu sanal makinenize kopyalayabilirsiniz veya bir yükleyici aracılığıyla bir Java uygulama sunucusu yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99d4f-154">You can copy a Java application server to your virtual machine, or you can install a Java application server through an installer.</span></span>

<span data-ttu-id="99d4f-155">Bu öğretici Tomcat Java uygulama sunucusu olarak yüklemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="99d4f-155">This tutorial uses Tomcat as the Java application server to install.</span></span>

1. <span data-ttu-id="99d4f-156">Sanal makinenize oturum açtığında, bir tarayıcı oturumu açın [Apache Tomcat](http://tomcat.apache.org/download-80.cgi).</span><span class="sxs-lookup"><span data-stu-id="99d4f-156">When you are signed in to your virtual machine, open a browser session to [Apache Tomcat](http://tomcat.apache.org/download-80.cgi).</span></span>
2. <span data-ttu-id="99d4f-157">Bağlantı için çift **32-bit/64-bit Windows hizmeti yükleyicisini**.</span><span class="sxs-lookup"><span data-stu-id="99d4f-157">Double-click the link for **32-bit/64-bit Windows Service Installer**.</span></span> <span data-ttu-id="99d4f-158">Bu yöntemi kullanarak, Tomcat bir Windows hizmeti olarak yükler.</span><span class="sxs-lookup"><span data-stu-id="99d4f-158">By using this technique, Tomcat installs as a Windows service.</span></span>
3. <span data-ttu-id="99d4f-159">İstendiğinde, yükleyiciyi çalıştırmak seçin.</span><span class="sxs-lookup"><span data-stu-id="99d4f-159">When prompted, choose to run the installer.</span></span>
4. <span data-ttu-id="99d4f-160">İçinde **Apache Tomcat Kurulum** Sihirbazı, Tomcat yüklemek için istemleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="99d4f-160">Within the **Apache Tomcat Setup** wizard, follow the prompts to install Tomcat.</span></span> <span data-ttu-id="99d4f-161">Bu öğreticinin amaçları doğrultusunda, varsayılan değerleri kabul ederek uygundur.</span><span class="sxs-lookup"><span data-stu-id="99d4f-161">For the purposes of this tutorial, accepting the defaults is fine.</span></span> <span data-ttu-id="99d4f-162">Ulaştığınızda **Apache Tomcat Kurulum Sihirbazı Tamamlanıyor** iletişim kutusu, isteğe bağlı olarak kontrol edebilirsiniz **çalıştırmak Apache Tomcat** Tomcat şimdi başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="99d4f-162">When you reach the **Completing the Apache Tomcat Setup Wizard** dialog box, you can optionally check **Run Apache Tomcat** to have Tomcat start now.</span></span> <span data-ttu-id="99d4f-163">Tıklatın **son** Tomcat Kurulum işlemini tamamlamak için.</span><span class="sxs-lookup"><span data-stu-id="99d4f-163">Click **Finish** to complete the Tomcat setup process.</span></span>

## <a name="to-start-tomcat"></a><span data-ttu-id="99d4f-164">Tomcat başlatmak için</span><span class="sxs-lookup"><span data-stu-id="99d4f-164">To start Tomcat</span></span>

<span data-ttu-id="99d4f-165">Sanal makinenizde bir komut istemi açmak ve komutunu çalıştırarak Tomcat el ile başlatabilirsiniz **net&nbsp;Başlat&nbsp;Tomcat8**.</span><span class="sxs-lookup"><span data-stu-id="99d4f-165">You can manually start Tomcat by opening a command prompt on your virtual machine and running the command **net&nbsp;start&nbsp;Tomcat8**.</span></span>

<span data-ttu-id="99d4f-166">Tomcat çalışmaya başladıktan sonra URL'yi girerek Tomcat erişebilirsiniz <http://localhost: 8080> sanal makinenin tarayıcıda.</span><span class="sxs-lookup"><span data-stu-id="99d4f-166">Once Tomcat is running, you can access Tomcat by entering the URL <http://localhost:8080> in the virtual machine's browser.</span></span>

<span data-ttu-id="99d4f-167">Dış makinelerden çalıştıran Tomcat görmek için bir uç noktası oluşturma ve bir bağlantı noktası açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="99d4f-167">To see Tomcat running from external machines, you need to create an endpoint and open a port.</span></span>

## <a name="to-create-an-endpoint-for-your-virtual-machine"></a><span data-ttu-id="99d4f-168">Sanal makineniz için bir uç nokta oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="99d4f-168">To create an endpoint for your virtual machine</span></span>
1. <span data-ttu-id="99d4f-169">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="99d4f-169">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="99d4f-170">Tıklatın **sanal makineleri (Klasik)**.</span><span class="sxs-lookup"><span data-stu-id="99d4f-170">Click **Virtual machines (classic)**.</span></span>
3. <span data-ttu-id="99d4f-171">Java uygulama sunucusu çalıştıran sanal makine adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="99d4f-171">Click the name of the virtual machine that is running your Java application server.</span></span>
4. <span data-ttu-id="99d4f-172">**Uç Noktalar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="99d4f-172">Click **Endpoints**.</span></span>
5. <span data-ttu-id="99d4f-173">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="99d4f-173">Click **Add**.</span></span>
6. <span data-ttu-id="99d4f-174">İçinde **uç nokta ekleme** iletişim kutusunda:</span><span class="sxs-lookup"><span data-stu-id="99d4f-174">In the **Add endpoint** dialog box:</span></span>
   1. <span data-ttu-id="99d4f-175">Uç nokta için bir ad belirtin; Örneğin, **HttpIn**.</span><span class="sxs-lookup"><span data-stu-id="99d4f-175">Specify a name for the endpoint; for example, **HttpIn**.</span></span>
   2. <span data-ttu-id="99d4f-176">Seçin **TCP** protokolü için.</span><span class="sxs-lookup"><span data-stu-id="99d4f-176">Select **TCP** for the protocol.</span></span>
   3. <span data-ttu-id="99d4f-177">Belirtin **80** genel bağlantı noktası için.</span><span class="sxs-lookup"><span data-stu-id="99d4f-177">Specify **80** for the public port.</span></span>
   4. <span data-ttu-id="99d4f-178">Belirtin **8080** özel bağlantı noktası için.</span><span class="sxs-lookup"><span data-stu-id="99d4f-178">Specify **8080** for the private port.</span></span>
   5. <span data-ttu-id="99d4f-179">Seçin **devre dışı** kayan IP adresi.</span><span class="sxs-lookup"><span data-stu-id="99d4f-179">Select **Disabled** for the floating IP address.</span></span>
   6. <span data-ttu-id="99d4f-180">Erişim denetimi listesi olduğu gibi bırakın.</span><span class="sxs-lookup"><span data-stu-id="99d4f-180">Leave the access control list as is.</span></span>
   7. <span data-ttu-id="99d4f-181">Tıklatın **Tamam** düğmesine iletişim kutusunu kapatmak ve uç noktası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="99d4f-181">Click the **OK** button to close the dialog box and create the endpoint.</span></span>

## <a name="to-open-a-port-in-the-firewall-for-your-virtual-machine"></a><span data-ttu-id="99d4f-182">Güvenlik Duvarı'nda, sanal makine için bir bağlantı noktasını açmak için</span><span class="sxs-lookup"><span data-stu-id="99d4f-182">To open a port in the firewall for your virtual machine</span></span>
1. <span data-ttu-id="99d4f-183">Sanal makinenize oturum açın.</span><span class="sxs-lookup"><span data-stu-id="99d4f-183">Sign in to your virtual machine.</span></span>
2. <span data-ttu-id="99d4f-184">Tıklatın **Windows Başlangıç**.</span><span class="sxs-lookup"><span data-stu-id="99d4f-184">Click **Windows Start**.</span></span>
3. <span data-ttu-id="99d4f-185">Tıklatın **Denetim Masası**.</span><span class="sxs-lookup"><span data-stu-id="99d4f-185">Click **Control Panel**.</span></span>
4. <span data-ttu-id="99d4f-186">Tıklatın **sistem ve güvenlik**, tıklatın **Windows Güvenlik Duvarı**ve ardından **Gelişmiş ayarları**.</span><span class="sxs-lookup"><span data-stu-id="99d4f-186">Click **System and Security**, click **Windows Firewall**, and then click **Advanced Settings**.</span></span>
5. <span data-ttu-id="99d4f-187">Tıklatın **gelen kuralları**ve ardından **yeni kural**.</span><span class="sxs-lookup"><span data-stu-id="99d4f-187">Click **Inbound Rules**, and then click **New Rule**.</span></span>  
   <span data-ttu-id="99d4f-188">![Yeni gelen kuralı][NewIBRule]</span><span class="sxs-lookup"><span data-stu-id="99d4f-188">![New inbound rule][NewIBRule]</span></span>
6. <span data-ttu-id="99d4f-189">İçin **kural türü**seçin **bağlantı noktası**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="99d4f-189">For the **Rule Type**, select **Port**, and then click **Next**.</span></span>  
   <span data-ttu-id="99d4f-190">![Yeni gelen kuralı bağlantı noktası][NewRulePort]</span><span class="sxs-lookup"><span data-stu-id="99d4f-190">![New inbound rule port][NewRulePort]</span></span>
7. <span data-ttu-id="99d4f-191">Üzerinde **protokol ve bağlantı noktaları** ekran, select **TCP**, belirtin **8080** olarak **belirli yerel bağlantı noktası**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="99d4f-191">On the **Protocol and Ports** screen, select **TCP**, specify **8080** as the **Specific local port**, and then click **Next**.</span></span>  
  <span data-ttu-id="99d4f-192">![Yeni gelen kuralı][NewRuleProtocol]</span><span class="sxs-lookup"><span data-stu-id="99d4f-192">![New inbound rule ][NewRuleProtocol]</span></span>
8. <span data-ttu-id="99d4f-193">Üzerinde **eylem** ekran, select **bağlantıya izin**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="99d4f-193">On the **Action** screen, select **Allow the connection**, and then click **Next**.</span></span>
   <span data-ttu-id="99d4f-194">![Yeni gelen kuralı eylemi][NewRuleAction]</span><span class="sxs-lookup"><span data-stu-id="99d4f-194">![New inbound rule action][NewRuleAction]</span></span>
9. <span data-ttu-id="99d4f-195">Üzerinde **profil** ekranında, emin **etki alanı**, **özel**, ve **ortak** seçilir ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="99d4f-195">On the **Profile** screen, ensure that **Domain**, **Private**, and **Public** are selected, and then click **Next**.</span></span>
   <span data-ttu-id="99d4f-196">![Yeni gelen kuralı profili][NewRuleProfile]</span><span class="sxs-lookup"><span data-stu-id="99d4f-196">![New inbound rule profile][NewRuleProfile]</span></span>
10. <span data-ttu-id="99d4f-197">Üzerinde **adı** ekranında, kural için bir ad belirtin **HttpIn** (Kural adı gerekli değildir ancak uç nokta adı eşleşecek şekilde) ve ardından **son**.</span><span class="sxs-lookup"><span data-stu-id="99d4f-197">On the **Name** screen, specify a name for the rule, such as **HttpIn** (the rule name is not required to match the endpoint name, however), and then click **Finish**.</span></span>  
    <span data-ttu-id="99d4f-198">![Yeni gelen kuralı adı][NewRuleName]</span><span class="sxs-lookup"><span data-stu-id="99d4f-198">![New inbound rule name][NewRuleName]</span></span>

<span data-ttu-id="99d4f-199">Bu noktada, Tomcat Web sitenizi dış bir tarayıcıdan görüntülenebilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="99d4f-199">At this point, your Tomcat website should be viewable from an external browser.</span></span> <span data-ttu-id="99d4f-200">Tarayıcının adres penceresinde bir URL biçiminde yazın  **http://*,\_DNS\_adı*. cloudapp.net**, burada ***,\_DNS\_adı*** sanal makineyi oluşturduğunuzda belirttiğiniz DNS adı.</span><span class="sxs-lookup"><span data-stu-id="99d4f-200">In the browser's address window, type a URL of the form **http://*your\_DNS\_name*.cloudapp.net**, where ***your\_DNS\_name*** is the DNS name you specified when you created the virtual machine.</span></span>

## <a name="application-lifecycle-considerations"></a><span data-ttu-id="99d4f-201">Uygulama yaşam döngüsü hakkında dikkat edilecek noktalar</span><span class="sxs-lookup"><span data-stu-id="99d4f-201">Application lifecycle considerations</span></span>
* <span data-ttu-id="99d4f-202">Kendi web uygulama Arşivi (WAR) oluşturun ve ona ekleyen **webapps** klasör.</span><span class="sxs-lookup"><span data-stu-id="99d4f-202">You could create your own web application archive (WAR) and add it to the **webapps** folder.</span></span> <span data-ttu-id="99d4f-203">Örneğin, bir temel Java hizmet sayfa (JSP) dinamik web projesi oluşturun ve bir WAR dosyası olarak dışarı aktarma.</span><span class="sxs-lookup"><span data-stu-id="99d4f-203">For example, create a basic Java Service Page (JSP) dynamic web project and export it as a WAR file.</span></span> <span data-ttu-id="99d4f-204">Ardından, Apache Tomcat WAR kopyalama **webapps** sanal makinede bir tarayıcıda ardından çalıştırın, klasör.</span><span class="sxs-lookup"><span data-stu-id="99d4f-204">Next, copy the WAR to the Apache Tomcat **webapps** folder on the virtual machine, then run it in a browser.</span></span>
* <span data-ttu-id="99d4f-205">Tomcat hizmeti yüklü olduğunda, varsayılan olarak el ile başlatmak için ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="99d4f-205">By default when the Tomcat service is installed, it is set to start manually.</span></span> <span data-ttu-id="99d4f-206">Hizmetler ek bileşenini kullanarak otomatik olarak başlayacak şekilde geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99d4f-206">You can switch it to start automatically by using the Services snap-in.</span></span> <span data-ttu-id="99d4f-207">Hizmetler ek bileşenini başlatın tıklayarak **Windows Başlat**, **Yönetimsel Araçlar**ve ardından **Hizmetleri**.</span><span class="sxs-lookup"><span data-stu-id="99d4f-207">Start the Services snap-in by clicking **Windows Start**, **Administrative Tools**, and then **Services**.</span></span> <span data-ttu-id="99d4f-208">Çift **Apache Tomcat** ayarlayın ve hizmeti **başlangıç türü** için **otomatik**.</span><span class="sxs-lookup"><span data-stu-id="99d4f-208">Double-click the **Apache Tomcat** service and set **Startup type** to **Automatic**.</span></span>

    ![Hizmeti otomatik olarak başlatılacak şekilde ayarlama][service_automatic_startup]

    <span data-ttu-id="99d4f-210">Otomatik olarak Başlat Tomcat sahip olmanın avantaj (örneğin, yeniden başlatma gerektiren yazılım güncelleştirmeleri yüklendikten sonra) sanal makine yeniden başlatıldığında çalışmaya başladıktan emin olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="99d4f-210">The benefit of having Tomcat start automatically is that it starts running when the virtual machine is rebooted (for example, after software updates that require a reboot are installed).</span></span>

## <a name="next-steps"></a><span data-ttu-id="99d4f-211">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="99d4f-211">Next steps</span></span>
<span data-ttu-id="99d4f-212">Java uygulamalarınızla dahil etmek istediğiniz diğer hizmetler (örneğin, Azure Storage, hizmet veri yolu ve SQL veritabanı) hakkında bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99d4f-212">You can learn about other services (such as Azure Storage, service bus, and SQL Database) that you may want to include with your Java applications.</span></span> <span data-ttu-id="99d4f-213">Kullanılabilir bilgi görüntülemek [Java Geliştirici Merkezi](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="99d4f-213">View the information available at the [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[virtual_machine_tomcat]:media/java-run-tomcat-app-server/WA_VirtualMachineRunningApacheTomcat.png

[service_automatic_startup]:media/java-run-tomcat-app-server/WA_TomcatServiceAutomaticStart.png









[NewIBRule]:media/java-run-tomcat-app-server/NewInboundRule.png
[NewRulePort]:media/java-run-tomcat-app-server/NewRulePort.png
[NewRuleProtocol]:media/java-run-tomcat-app-server/NewRuleProtocol.png
[NewRuleAction]:media/java-run-tomcat-app-server/NewRuleAction.png
[NewRuleName]:media/java-run-tomcat-app-server/NewRuleName.png
[NewRuleProfile]:media/java-run-tomcat-app-server/NewRuleProfile.png


<!-- Deleted from the "To create an ednpoint for your virtual mache" 3/17/2017,
     to use the new portal.
6. In the **Add endpoint** dialog box, ensure **Add standalone endpoint** is selected, and then click **Next**.
7. In the **New endpoint details** dialog box:
-->
