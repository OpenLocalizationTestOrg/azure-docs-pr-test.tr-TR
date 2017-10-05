---
title: "C üzerinde mbed kullanarak bir cihazı bağlanma | Microsoft Docs"
description: "Bir mbed cihazda çalışan C yazılmış bir uygulama kullanarak Azure IOT paketi önceden yapılandırılmış Uzaktan izleme çözümü bir aygıt bağlanmaya açıklar."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 9551075e-dcf9-488f-943e-d0eb0e6260be
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ROBOTS: NOINDEX
ms.openlocfilehash: ef7b78f85a787f8fbe22c0e26aa34f0cd1685d58
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-your-device-to-the-remote-monitoring-preconfigured-solution-mbed"></a><span data-ttu-id="01002-103">Cihazınızı Uzaktan izleme önceden yapılandırılmış çözümü (mbed) bağlanma</span><span class="sxs-lookup"><span data-stu-id="01002-103">Connect your device to the remote monitoring preconfigured solution (mbed)</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="01002-104">Senaryoya genel bakış</span><span class="sxs-lookup"><span data-stu-id="01002-104">Scenario overview</span></span>
<span data-ttu-id="01002-105">Bu senaryoda aşağıdaki telemetriyi önceden yapılandırılmış uzaktan izleme [çözümüne][lnk-what-are-preconfig-solutions] gönderen bir cihaz oluşturacaksınız:</span><span class="sxs-lookup"><span data-stu-id="01002-105">In this scenario, you create a device that sends the following telemetry to the remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="01002-106">Dış ortam sıcaklığı</span><span class="sxs-lookup"><span data-stu-id="01002-106">External temperature</span></span>
* <span data-ttu-id="01002-107">İç ortam sıcaklığı</span><span class="sxs-lookup"><span data-stu-id="01002-107">Internal temperature</span></span>
* <span data-ttu-id="01002-108">Nem oranı</span><span class="sxs-lookup"><span data-stu-id="01002-108">Humidity</span></span>

<span data-ttu-id="01002-109">Örneği basitleştirmek amacıyla cihaz üzerindeki kod örnek değerler oluşturmaktadır. Ancak cihazınıza gerçek sensörler bağlayıp gerçek telemetri verileri göndererek örneği ileri taşımanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="01002-109">For simplicity, the code on the device generates sample values, but we encourage you to extend the sample by connecting real sensors to your device and sending real telemetry.</span></span>

<span data-ttu-id="01002-110">Cihaz ayrıca çözüm panosundan çağrılan yöntemlere ve çözüm panosunda ayarlanan istenen özellik değerlerine yanıt verebilir.</span><span class="sxs-lookup"><span data-stu-id="01002-110">The device is also able to respond to methods invoked from the solution dashboard and desired property values set in the solution dashboard.</span></span>

<span data-ttu-id="01002-111">Bu öğreticiyi tamamlamak için etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="01002-111">To complete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="01002-112">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01002-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="01002-113">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="01002-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="01002-114">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="01002-114">Before you start</span></span>
<span data-ttu-id="01002-115">Cihazınız için kod yazmadan önce, önceden yapılandırılmış uzaktan izleme çözümünüzü ve bu çözümde yeni bir özel cihaz hazırlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="01002-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="01002-116">Önceden yapılandırılmış uzaktan izleme çözümünüzü sağlama</span><span class="sxs-lookup"><span data-stu-id="01002-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="01002-117">Bu öğreticide oluşturduğunuz cihaz, önceden yapılandırılmış bir [uzaktan izleme][lnk-remote-monitoring] çözümü örneğine veri göndermektedir.</span><span class="sxs-lookup"><span data-stu-id="01002-117">The device you create in this tutorial sends data to an instance of the [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="01002-118">Önceden yapılandırılmış uzaktan izleme çözümünüzü henüz Azure hesabınızda hazırlamadıysanız aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="01002-118">If you haven't already provisioned the remote monitoring preconfigured solution in your Azure account, use the following steps:</span></span>

1. <span data-ttu-id="01002-119"><https://www.azureiotsuite.com/> sayfasında çözüm oluşturmak için **+** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="01002-119">On the <https://www.azureiotsuite.com/> page, click **+** to create a solution.</span></span>
2. <span data-ttu-id="01002-120">Çözümünüzü oluşturmak için **Uzaktan izleme** panelindeki **Seç**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="01002-120">Click **Select** on the **Remote monitoring** panel to create your solution.</span></span>
3. <span data-ttu-id="01002-121">**Uzaktan izleme çözümü oluştur** sayfasında bir **Çözüm adı** belirleyin, dağıtmak istediğiniz **Bölgeyi** seçin ve kullanmak istediğiniz Azure aboneliğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="01002-121">On the **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select the **Region** you want to deploy to, and select the Azure subscription to want to use.</span></span> <span data-ttu-id="01002-122">Ardından **Çözüm oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="01002-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="01002-123">Sağlama işleminin tamamlanmasını bekleyin.</span><span class="sxs-lookup"><span data-stu-id="01002-123">Wait until the provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="01002-124">Önceden yapılandırılmış çözümler, faturalanabilir Azure hizmetlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="01002-124">The preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="01002-125">Gereksiz ücretlerden kaçınmak için işinizi tamamladıktan sonra önceden yapılandırılmış çözümü aboneliğinizden kaldırmayı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="01002-125">Be sure to remove the preconfigured solution from your subscription when you are done with it to avoid any unnecessary charges.</span></span> <span data-ttu-id="01002-126">Önceden yapılandırılmış çözümü aboneliğinizden tamamen kaldırmak için <https://www.azureiotsuite.com/> sayfasını ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="01002-126">You can completely remove a preconfigured solution from your subscription by visiting the <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="01002-127">Uzaktan izleme çözümü için sağlama işlemi tamamlandıktan sonra çözüm panosunu tarayıcınızda açmak için **Başlat**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="01002-127">When the provisioning process for the remote monitoring solution finishes, click **Launch** to open the solution dashboard in your browser.</span></span>

![Çözüm panosu][img-dashboard]

### <a name="provision-your-device-in-the-remote-monitoring-solution"></a><span data-ttu-id="01002-129">Cihazınızı uzaktan izleme çözümünde sağlama</span><span class="sxs-lookup"><span data-stu-id="01002-129">Provision your device in the remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="01002-130">Çözümünüzde önceden bir cihaz hazırladıysanız bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01002-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="01002-131">İstemci uygulamasını oluştururken cihaz kimlik bilgilerini bilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="01002-131">You need to know the device credentials when you create the client application.</span></span>
> 
> 

<span data-ttu-id="01002-132">Bir cihazın önceden yapılandırılmış çözüme bağlanabilmesi için geçerli kimlik bilgileriyle kendini IoT Hub üzerinde tanıtması gerekir.</span><span class="sxs-lookup"><span data-stu-id="01002-132">For a device to connect to the preconfigured solution, it must identify itself to IoT Hub using valid credentials.</span></span> <span data-ttu-id="01002-133">Cihaz kimlik bilgilerini çözüm panosundan alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01002-133">You can retrieve the device credentials from the solution dashboard.</span></span> <span data-ttu-id="01002-134">Cihaz kimlik bilgilerini bu öğreticinin sonraki adımlarında istemci uygulamanıza ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01002-134">You include the device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="01002-135">Uzaktan izleme çözümünüze cihaz eklemek için çözüm panosunda aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="01002-135">To add a device to your remote monitoring solution, complete the following steps in the solution dashboard:</span></span>

1. <span data-ttu-id="01002-136">Panonun sol alt köşesinde **Cihaz ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="01002-136">In the lower left-hand corner of the dashboard, click **Add a device**.</span></span>
   
   ![Cihaz ekleme][1]
2. <span data-ttu-id="01002-138">**Özel Cihaz** panelinde **Yeni ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="01002-138">In the **Custom Device** panel, click **Add new**.</span></span>
   
   ![Özel cihaz ekleme][2]
3. <span data-ttu-id="01002-140">**Kendi Cihaz Kimliğimi tanımlamama izin ver**'i seçin.</span><span class="sxs-lookup"><span data-stu-id="01002-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="01002-141">**cihazım** gibi bir Cihaz Kimliği girin, adın kullanımda olmadığını doğrulamak için **Kimliği denetle**'ye tıklayın ve ardından cihazı hazırlamak için **Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="01002-141">Enter a Device ID such as **mydevice**, click **Check ID** to verify that name isn't already in use, and then click **Create** to provision the device.</span></span>
   
   ![Cihaz kimliği ekleme][3]
4. <span data-ttu-id="01002-143">Cihaz kimlik bilgilerini (Cihaz Kimliği, IoT Hub Ana Bilgisayar Adı ve Cihaz Anahtarı) not edin.</span><span class="sxs-lookup"><span data-stu-id="01002-143">Make a note the device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="01002-144">İstemci uygulamanız uzaktan izleme çözümüne bağlanmak için bu değerleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="01002-144">Your client application needs these values to connect to the remote monitoring solution.</span></span> <span data-ttu-id="01002-145">Sonra da **Bitti**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="01002-145">Then click **Done**.</span></span>
   
    ![Cihaz kimlik bilgilerini görüntüleme][4]
5. <span data-ttu-id="01002-147">Çözüm panosundaki cihaz listesinden cihazınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="01002-147">Select your device in the device list in the solution dashboard.</span></span> <span data-ttu-id="01002-148">Ardından **Cihaz Ayrıntıları** panelinde **Cihazı Etkinleştir**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="01002-148">Then, in the **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="01002-149">Cihazınızın durumu **Çalışıyor** olarak değişir.</span><span class="sxs-lookup"><span data-stu-id="01002-149">The status of your device is now **Running**.</span></span> <span data-ttu-id="01002-150">Uzaktan izleme çözümü artık cihazınızdan telemetri verileri alabilir ve cihazınızda yöntemler çağırabilir.</span><span class="sxs-lookup"><span data-stu-id="01002-150">The remote monitoring solution can now receive telemetry from your device and invoke methods on the device.</span></span>

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-the-c-sample-solution"></a><span data-ttu-id="01002-151">Derleme ve C örnek çözümü çalıştırma</span><span class="sxs-lookup"><span data-stu-id="01002-151">Build and run the C sample solution</span></span>

<span data-ttu-id="01002-152">Aşağıdaki yönergeler bağlanmak için gereken adımlar anlatılmaktadır bir [mbed etkin Freescale FRDM K64F] [ lnk-mbed-home] Uzaktan izleme çözümü cihaza.</span><span class="sxs-lookup"><span data-stu-id="01002-152">The following instructions describe the steps for connecting an [mbed-enabled Freescale FRDM-K64F][lnk-mbed-home] device to the remote monitoring solution.</span></span>

### <a name="connect-the-mbed-device-to-your-network-and-desktop-machine"></a><span data-ttu-id="01002-153">Mbed aygıt ağ ve Masaüstü makinenize bağlanın</span><span class="sxs-lookup"><span data-stu-id="01002-153">Connect the mbed device to your network and desktop machine</span></span>

1. <span data-ttu-id="01002-154">Mbed aygıtı Ethernet kablosu kullanarak ağınıza bağlayın.</span><span class="sxs-lookup"><span data-stu-id="01002-154">Connect the mbed device to your network using an Ethernet cable.</span></span> <span data-ttu-id="01002-155">Örnek uygulama Internet erişimi gerektirdiğinden bu adım gereklidir.</span><span class="sxs-lookup"><span data-stu-id="01002-155">This step is necessary because the sample application requires internet access.</span></span>

1. <span data-ttu-id="01002-156">Bkz: [mbed ile çalışmaya başlama] [ lnk-mbed-getstarted] masaüstü bilgisayarınıza mbed Cihazınızı bağlamak için.</span><span class="sxs-lookup"><span data-stu-id="01002-156">See [Getting Started with mbed][lnk-mbed-getstarted] to connect your mbed device to your desktop PC.</span></span>

1. <span data-ttu-id="01002-157">Windows masaüstü bilgisayarınıza çalıştırıyorsa, bkz: [PC yapılandırma] [ lnk-mbed-pcconnect] mbed Cihazınızı seri bağlantı noktası erişimi yapılandırmak için.</span><span class="sxs-lookup"><span data-stu-id="01002-157">If your desktop PC is running Windows, see [PC Configuration][lnk-mbed-pcconnect] to configure serial port access to your mbed device.</span></span>

### <a name="create-an-mbed-project-and-import-the-sample-code"></a><span data-ttu-id="01002-158">Bir mbed projesi oluşturun ve örnek kodunu alma</span><span class="sxs-lookup"><span data-stu-id="01002-158">Create an mbed project and import the sample code</span></span>

<span data-ttu-id="01002-159">Bazı örnek kod bir mbed projeye eklemek için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="01002-159">Follow these steps to add some sample code to an mbed project.</span></span> <span data-ttu-id="01002-160">Uzaktan izleme başlangıç projesi içeri aktarıp MQTT Protokolü yerine AMQP protokolünü kullanmak için proje değiştirin.</span><span class="sxs-lookup"><span data-stu-id="01002-160">You import the remote monitoring starter project and then change the project to use the MQTT protocol instead of the AMQP protocol.</span></span> <span data-ttu-id="01002-161">Şu anda IOT Hub cihaz yönetimi özelliklerini kullanmak için MQTT Protokolü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="01002-161">Currently, you need to use the MQTT protocol to use the device management features of IoT Hub.</span></span>

1. <span data-ttu-id="01002-162">Web tarayıcınızda mbed.org Git [Geliştirici site](https://developer.mbed.org/).</span><span class="sxs-lookup"><span data-stu-id="01002-162">In your web browser, go to the mbed.org [developer site](https://developer.mbed.org/).</span></span> <span data-ttu-id="01002-163">Kaydolmuş olmasanız (ücretsiz) hesap oluşturmak için bir seçenek görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="01002-163">If you haven't signed up, you see an option to create an account (it's free).</span></span> <span data-ttu-id="01002-164">Aksi takdirde, hesap kimlik bilgileriyle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="01002-164">Otherwise, log in with your account credentials.</span></span> <span data-ttu-id="01002-165">Ardından **derleyici** sayfanın sağ üst köşesindeki.</span><span class="sxs-lookup"><span data-stu-id="01002-165">Then click **Compiler** in the upper right-hand corner of the page.</span></span> <span data-ttu-id="01002-166">Bu eylem getirir *çalışma* arabirimi.</span><span class="sxs-lookup"><span data-stu-id="01002-166">This action brings you to the *Workspace* interface.</span></span>

1. <span data-ttu-id="01002-167">Kullanmakta olduğunuz donanım platformu pencerenin sağ üst köşesinde göründüğünden emin olun veya donanım platformunuz seçmek için sağ alt köşesindeki simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="01002-167">Make sure the hardware platform you're using appears in the upper right-hand corner of the window, or click the icon in the right-hand corner to select your hardware platform.</span></span>

1. <span data-ttu-id="01002-168">Tıklatın **alma** ana menüdeki.</span><span class="sxs-lookup"><span data-stu-id="01002-168">Click **Import** on the main menu.</span></span> <span data-ttu-id="01002-169">Ardından **URL'den almak için burayı tıklatın**.</span><span class="sxs-lookup"><span data-stu-id="01002-169">Then click **Click here to import from URL**.</span></span>
   
    ![Mbed çalışma alanına alma Başlat][6]

1. <span data-ttu-id="01002-171">Açılan pencerede, bağlantı için örnek kod https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ girin'yi tıklatın **alma**.</span><span class="sxs-lookup"><span data-stu-id="01002-171">In the pop-up window, enter the link for the sample code https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ then click **Import**.</span></span>
   
    ![Örnek kod mbed çalışma alanına alma][7]

1. <span data-ttu-id="01002-173">Bu projeyi içeri aktarma, çeşitli kitaplıkları da alır, mbed derleyici penceresinde görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01002-173">You can see in the mbed compiler window that importing this project also imports various libraries.</span></span> <span data-ttu-id="01002-174">Bazı sağlanan ve Azure IOT ekibi tarafından korunan ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), diğerleri ise, üçüncü taraf kitaplıklar mbed kitaplıkları Kataloğu'nda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="01002-174">Some are provided and maintained by the Azure IoT team ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), while others are third-party libraries available in the mbed libraries catalog.</span></span>
   
    ![Görünüm mbed proje][8]

1. <span data-ttu-id="01002-176">İçinde **programın çalışma**, sağ tıklatın **ıothub\_amqp\_aktarım** kitaplığı tıklatın **silmek**ve ardından **Tamam** onaylamak için.</span><span class="sxs-lookup"><span data-stu-id="01002-176">In the **Program Workspace**, right-click the **iothub\_amqp\_transport** library, click **Delete**, and then click **OK** to confirm.</span></span>

1. <span data-ttu-id="01002-177">İçinde **Program çalışma**, sağ tıklatın **azure\_amqp\_c** kitaplığı tıklatın **silmek**ve ardından **Tamam** onaylamak için.</span><span class="sxs-lookup"><span data-stu-id="01002-177">In the **Program Workspace**, right-click the **azure\_amqp\_c** library, click **Delete**, and then click **OK** to confirm.</span></span>

1. <span data-ttu-id="01002-178">Sağ **remote_monitoring** proje **Program çalışma**seçin **içeri aktarma kitaplığını**seçeneğini belirleyip **URL'den**.</span><span class="sxs-lookup"><span data-stu-id="01002-178">Right-click the **remote_monitoring** project in the **Program Workspace**, select **Import Library**, then select **From URL**.</span></span>
   
    ![Mbed çalışma alanına kitaplığı alma Başlat][6]

1. <span data-ttu-id="01002-180">Açılan pencerede bağlantısı için MQTT taşıma kitaplığı https://developer.mbed.org/users/AzureIoTClient/code/iothub girin\_mqtt\_aktarım / ardından **alma**.</span><span class="sxs-lookup"><span data-stu-id="01002-180">In the pop-up window, enter the link for the MQTT transport library https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transport/ then click **Import**.</span></span>
   
    ![İçeri aktarma kitaplığını mbed çalışma][12]

1. <span data-ttu-id="01002-182">Https://developer.mbed.org/users/AzureIoTClient/code/azure MQTT Kitaplığı eklemek için önceki adımı yineleyin\_umqtt\_c /.</span><span class="sxs-lookup"><span data-stu-id="01002-182">Repeat the previous step to add the MQTT library from https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c/.</span></span>

1. <span data-ttu-id="01002-183">Çalışma alanınızı şimdi aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="01002-183">Your workspace now looks like the following:</span></span>

    ![Mbed çalışma alanını görüntüle][13]

1. <span data-ttu-id="01002-185">Uzak açmak\_monitoring\remote_monitoring.c dosya ve varolan Değiştir `#include` deyimleri ile aşağıdaki kodu:</span><span class="sxs-lookup"><span data-stu-id="01002-185">Open the remote\_monitoring\remote_monitoring.c file and replace the existing `#include` statements with the following code:</span></span>

    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"

    #ifdef MBED_BUILD_TIMESTAMP
    #include "certs.h"
    #endif // MBED_BUILD_TIMESTAMP
    ```
1. <span data-ttu-id="01002-186">Tüm kalan kodda uzaktan silme\_monitoring\remote\_monitoring.c dosya.</span><span class="sxs-lookup"><span data-stu-id="01002-186">Delete all the remaining code in the remote\_monitoring\remote\_monitoring.c file.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-the-sample"></a><span data-ttu-id="01002-187">Derleme ve örnek çalıştırma</span><span class="sxs-lookup"><span data-stu-id="01002-187">Build and run the sample</span></span>

<span data-ttu-id="01002-188">Çağırmak için kodu ekleyin **uzak\_izleme\_çalıştırmak** işlev oluşturmak ve cihaz uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="01002-188">Add code to invoke the **remote\_monitoring\_run** function and then build and run the device application.</span></span>

1. <span data-ttu-id="01002-189">Ekleme bir **ana** işlevi uzaktan sonuna aşağıdaki kod ile\_çağrılacak monitoring.c dosya **uzak\_izleme\_çalıştırmak** işlevi:</span><span class="sxs-lookup"><span data-stu-id="01002-189">Add a **main** function with following code at the end of the remote\_monitoring.c file to invoke the **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="01002-190">Tıklatın **derleme** program oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="01002-190">Click **Compile** to build the program.</span></span> <span data-ttu-id="01002-191">Güvenli bir şekilde tüm uyarılarını gözardı ancak derleme hataları oluşturursa devam etmeden önce düzeltin.</span><span class="sxs-lookup"><span data-stu-id="01002-191">You can safely ignore any warnings, but if the build generates errors, fix them before proceeding.</span></span>

1. <span data-ttu-id="01002-192">Yapı başarılı olursa, mbed derleyici Web sitesi projenizin adına sahip bir .bin dosyası oluşturur ve yerel makinenize indirir.</span><span class="sxs-lookup"><span data-stu-id="01002-192">If the build is successful, the mbed compiler website generates a .bin file with the name of your project and downloads it to your local machine.</span></span> <span data-ttu-id="01002-193">.Bin dosyasını aygıtına kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="01002-193">Copy the .bin file to the device.</span></span> <span data-ttu-id="01002-194">Cihaza .bin dosyasını kaydetme yeniden başlatın ve .bin dosyasında yer alan programı çalıştırmak için cihazın neden olur.</span><span class="sxs-lookup"><span data-stu-id="01002-194">Saving the .bin file to the device causes the device to restart and run the program contained in the .bin file.</span></span> <span data-ttu-id="01002-195">Mbed aygıtta Sıfırla düğmesine basarak istediğiniz zaman program el ile yeniden başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01002-195">You can manually restart the program at any time by pressing the reset button on the mbed device.</span></span>

1. <span data-ttu-id="01002-196">PuTTY gibi bir SSH istemci uygulaması kullanarak cihazı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="01002-196">Connect to the device using an SSH client application, such as PuTTY.</span></span> <span data-ttu-id="01002-197">Windows Aygıt Yöneticisi'ni denetleyerek aygıtınızın kullandığı seri bağlantı noktası belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01002-197">You can determine the serial port your device uses by checking Windows Device Manager.</span></span>
   
    ![][11]

1. <span data-ttu-id="01002-198">PuTTY içinde tıklatın **seri** bağlantı türü.</span><span class="sxs-lookup"><span data-stu-id="01002-198">In PuTTY, click the **Serial** connection type.</span></span> <span data-ttu-id="01002-199">Aygıt genellikle 9600 baud hızında bağlanır, şekilde içinde 9600 girin **hızı** kutusu.</span><span class="sxs-lookup"><span data-stu-id="01002-199">The device typically connects at 9600 baud, so enter 9600 in the **Speed** box.</span></span> <span data-ttu-id="01002-200">Ardından **açık**.</span><span class="sxs-lookup"><span data-stu-id="01002-200">Then click **Open**.</span></span>

1. <span data-ttu-id="01002-201">Program yürütme başlar.</span><span class="sxs-lookup"><span data-stu-id="01002-201">The program starts executing.</span></span> <span data-ttu-id="01002-202">Pano sıfırlamanız gerekebilir (CTRL + Break tuşlarına basın veya panosu'nın Sıfırla düğmesine basın) programı otomatik olarak bağladığınızda başlamazsa.</span><span class="sxs-lookup"><span data-stu-id="01002-202">You may have to reset the board (press CTRL+Break or press the board's reset button) if the program does not start automatically when you connect.</span></span>
   
    ![][10]

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[6]: ./media/iot-suite-connecting-devices-mbed/mbed1.png
[7]: ./media/iot-suite-connecting-devices-mbed/mbed2a.png
[8]: ./media/iot-suite-connecting-devices-mbed/mbed3a.png
[10]: ./media/iot-suite-connecting-devices-mbed/putty.png
[11]: ./media/iot-suite-connecting-devices-mbed/mbed6.png
[12]: ./media/iot-suite-connecting-devices-mbed/mbed7.png
[13]: ./media/iot-suite-connecting-devices-mbed/mbed8.png

[lnk-mbed-home]: https://developer.mbed.org/platforms/FRDM-K64F/
[lnk-mbed-getstarted]: https://developer.mbed.org/platforms/FRDM-K64F/#getting-started-with-mbed
[lnk-mbed-pcconnect]: https://developer.mbed.org/platforms/FRDM-K64F/#pc-configuration
