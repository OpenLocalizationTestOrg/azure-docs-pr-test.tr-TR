---
title: "C üzerinde mbed kullanarak cihazı aaaConnect | Microsoft Docs"
description: "Nasıl tooconnect aygıt toohello Azure IOT paketi Uzaktan izleme çözümü mbed cihazda çalışan C yazılmış bir uygulama kullanarak önceden yapılandırılmış açıklar."
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
ms.openlocfilehash: dcd1e74635e8dec678a59bff060a73f7cfabd124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-mbed"></a><span data-ttu-id="28c6c-103">Uzaktan izleme çözümü (mbed), cihaz toohello Bağlan</span><span class="sxs-lookup"><span data-stu-id="28c6c-103">Connect your device toohello remote monitoring preconfigured solution (mbed)</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="28c6c-104">Senaryoya genel bakış</span><span class="sxs-lookup"><span data-stu-id="28c6c-104">Scenario overview</span></span>
<span data-ttu-id="28c6c-105">Bu senaryoda, telemetri toohello Uzaktan izleme aşağıdaki hello gönderir bir cihaz oluşturma [önceden yapılandırılmış çözüm][lnk-what-are-preconfig-solutions]:</span><span class="sxs-lookup"><span data-stu-id="28c6c-105">In this scenario, you create a device that sends hello following telemetry toohello remote monitoring [preconfigured solution][lnk-what-are-preconfig-solutions]:</span></span>

* <span data-ttu-id="28c6c-106">Dış ortam sıcaklığı</span><span class="sxs-lookup"><span data-stu-id="28c6c-106">External temperature</span></span>
* <span data-ttu-id="28c6c-107">İç ortam sıcaklığı</span><span class="sxs-lookup"><span data-stu-id="28c6c-107">Internal temperature</span></span>
* <span data-ttu-id="28c6c-108">Nem oranı</span><span class="sxs-lookup"><span data-stu-id="28c6c-108">Humidity</span></span>

<span data-ttu-id="28c6c-109">Basitleştirmek için örnek değerler hello cihazda hello kodu oluşturur, ancak siz tooextend hello örnek gerçek algılayıcılar tooyour aygıt bağlanma ve gerçek telemetri göndermesini öneririz.</span><span class="sxs-lookup"><span data-stu-id="28c6c-109">For simplicity, hello code on hello device generates sample values, but we encourage you tooextend hello sample by connecting real sensors tooyour device and sending real telemetry.</span></span>

<span data-ttu-id="28c6c-110">Merhaba de mümkün toorespond toomethods hello çözüm panodan çağrılır ve özellik değerleri hello çözüm panosunda istenen aygıttır.</span><span class="sxs-lookup"><span data-stu-id="28c6c-110">hello device is also able toorespond toomethods invoked from hello solution dashboard and desired property values set in hello solution dashboard.</span></span>

<span data-ttu-id="28c6c-111">toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="28c6c-111">toocomplete this tutorial, you need an active Azure account.</span></span> <span data-ttu-id="28c6c-112">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28c6c-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="28c6c-113">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="28c6c-113">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

## <a name="before-you-start"></a><span data-ttu-id="28c6c-114">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="28c6c-114">Before you start</span></span>
<span data-ttu-id="28c6c-115">Cihazınız için kod yazmadan önce, önceden yapılandırılmış uzaktan izleme çözümünüzü ve bu çözümde yeni bir özel cihaz hazırlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="28c6c-115">Before you write any code for your device, you must provision your remote monitoring preconfigured solution and provision a new custom device in that solution.</span></span>

### <a name="provision-your-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="28c6c-116">Önceden yapılandırılmış uzaktan izleme çözümünüzü sağlama</span><span class="sxs-lookup"><span data-stu-id="28c6c-116">Provision your remote monitoring preconfigured solution</span></span>
<span data-ttu-id="28c6c-117">Bu öğreticide oluşturduğunuz hello cihaz gönderir veri tooan hello örneği [Uzaktan izleme] [ lnk-remote-monitoring] çözüm önceden yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="28c6c-117">hello device you create in this tutorial sends data tooan instance of hello [remote monitoring][lnk-remote-monitoring] preconfigured solution.</span></span> <span data-ttu-id="28c6c-118">Uzaktan izleme çözümü Azure hesabınızda hello sağladığınız zaten yapmadıysanız, hello aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="28c6c-118">If you haven't already provisioned hello remote monitoring preconfigured solution in your Azure account, use hello following steps:</span></span>

1. <span data-ttu-id="28c6c-119">Merhaba üzerinde <https://www.azureiotsuite.com/> sayfasında, ** + ** toocreate bir çözüm.</span><span class="sxs-lookup"><span data-stu-id="28c6c-119">On hello <https://www.azureiotsuite.com/> page, click **+** toocreate a solution.</span></span>
2. <span data-ttu-id="28c6c-120">Tıklatın **seçin** hello üzerinde **Uzaktan izleme** çözümünüzü toocreate panel.</span><span class="sxs-lookup"><span data-stu-id="28c6c-120">Click **Select** on hello **Remote monitoring** panel toocreate your solution.</span></span>
3. <span data-ttu-id="28c6c-121">Hello üzerinde **Uzaktan izleme çözümü oluşturma** want bir **çözüm adı** seçiminizi, hello seçin **bölge** toodeploy için istediğiniz ve hello Azure seçin Abonelik toowant toouse.</span><span class="sxs-lookup"><span data-stu-id="28c6c-121">On hello **Create Remote monitoring solution** page, enter a **Solution name** of your choice, select hello **Region** you want toodeploy to, and select hello Azure subscription toowant toouse.</span></span> <span data-ttu-id="28c6c-122">Ardından **Çözüm oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="28c6c-122">Then click **Create solution**.</span></span>
4. <span data-ttu-id="28c6c-123">Merhaba sağlama işlemi tamamlanana kadar bekleyin.</span><span class="sxs-lookup"><span data-stu-id="28c6c-123">Wait until hello provisioning process completes.</span></span>

> [!WARNING]
> <span data-ttu-id="28c6c-124">Merhaba önceden yapılandırılmış çözümleri Faturalanabilir Azure Hizmetleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="28c6c-124">hello preconfigured solutions use billable Azure services.</span></span> <span data-ttu-id="28c6c-125">Tooremove hello aboneliğiniz önceden yapılandırılmış çözümü ile bittiğinde mutlaka tooavoid gereksiz herhangi bir ücret.</span><span class="sxs-lookup"><span data-stu-id="28c6c-125">Be sure tooremove hello preconfigured solution from your subscription when you are done with it tooavoid any unnecessary charges.</span></span> <span data-ttu-id="28c6c-126">Merhaba ziyaret ederek önceden yapılandırılmış bir çözüm aboneliğinizden tamamen kaldırabilirsiniz <https://www.azureiotsuite.com/> sayfası.</span><span class="sxs-lookup"><span data-stu-id="28c6c-126">You can completely remove a preconfigured solution from your subscription by visiting hello <https://www.azureiotsuite.com/> page.</span></span>
> 
> 

<span data-ttu-id="28c6c-127">Sağlama işlemi hello Uzaktan izleme çözümü için hello tamamlandığında, tıklatın **başlatma** tooopen hello çözüm Panosu tarayıcınızda.</span><span class="sxs-lookup"><span data-stu-id="28c6c-127">When hello provisioning process for hello remote monitoring solution finishes, click **Launch** tooopen hello solution dashboard in your browser.</span></span>

![Çözüm panosu][img-dashboard]

### <a name="provision-your-device-in-hello-remote-monitoring-solution"></a><span data-ttu-id="28c6c-129">Cihazınızı Uzaktan izleme çözümü hello sağlama</span><span class="sxs-lookup"><span data-stu-id="28c6c-129">Provision your device in hello remote monitoring solution</span></span>
> [!NOTE]
> <span data-ttu-id="28c6c-130">Çözümünüzde önceden bir cihaz hazırladıysanız bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28c6c-130">If you have already provisioned a device in your solution, you can skip this step.</span></span> <span data-ttu-id="28c6c-131">Merhaba istemci uygulaması oluşturduğunuzda tooknow hello cihaz kimlik bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="28c6c-131">You need tooknow hello device credentials when you create hello client application.</span></span>
> 
> 

<span data-ttu-id="28c6c-132">Bir cihaz tooconnect toohello önceden yapılandırılmış çözümü kendisini tooIoT Hub tanımlamak gerekir geçerli kimlik bilgilerini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="28c6c-132">For a device tooconnect toohello preconfigured solution, it must identify itself tooIoT Hub using valid credentials.</span></span> <span data-ttu-id="28c6c-133">Merhaba çözüm panodan hello aygıt kimlik bilgilerini alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28c6c-133">You can retrieve hello device credentials from hello solution dashboard.</span></span> <span data-ttu-id="28c6c-134">Bu öğreticide daha sonra istemci uygulamanızda hello cihaz kimlik bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="28c6c-134">You include hello device credentials in your client application later in this tutorial.</span></span>

<span data-ttu-id="28c6c-135">tooadd bir aygıt tooyour Uzaktan izleme çözümü, aşağıdaki tam hello hello çözüm panosunda adımlar:</span><span class="sxs-lookup"><span data-stu-id="28c6c-135">tooadd a device tooyour remote monitoring solution, complete hello following steps in hello solution dashboard:</span></span>

1. <span data-ttu-id="28c6c-136">Merhaba sol alt köşedeki hello Pano, tıklatın **bir cihaz ekleme**.</span><span class="sxs-lookup"><span data-stu-id="28c6c-136">In hello lower left-hand corner of hello dashboard, click **Add a device**.</span></span>
   
   ![Cihaz ekleme][1]
2. <span data-ttu-id="28c6c-138">Merhaba, **özel cihaz** öğesine tıklayın **yeni Ekle**.</span><span class="sxs-lookup"><span data-stu-id="28c6c-138">In hello **Custom Device** panel, click **Add new**.</span></span>
   
   ![Özel cihaz ekleme][2]
3. <span data-ttu-id="28c6c-140">**Kendi Cihaz Kimliğimi tanımlamama izin ver**'i seçin.</span><span class="sxs-lookup"><span data-stu-id="28c6c-140">Choose **Let me define my own Device ID**.</span></span> <span data-ttu-id="28c6c-141">Bir cihaz kimliği girin **mydevice**, tıklatın **denetleyin kimliği** tooverify bu ad zaten kullanımda olmadığından ve ardından **oluşturma** tooprovision hello aygıt.</span><span class="sxs-lookup"><span data-stu-id="28c6c-141">Enter a Device ID such as **mydevice**, click **Check ID** tooverify that name isn't already in use, and then click **Create** tooprovision hello device.</span></span>
   
   ![Cihaz kimliği ekleme][3]
4. <span data-ttu-id="28c6c-143">Kimlik bilgilerini (cihaz kimliği, IOT Hub ana bilgisayar adına ve aygıt anahtarı) not hello aygıt olun.</span><span class="sxs-lookup"><span data-stu-id="28c6c-143">Make a note hello device credentials (Device ID, IoT Hub Hostname, and Device Key).</span></span> <span data-ttu-id="28c6c-144">İstemci uygulamanız bu değerleri tooconnect toohello Uzaktan izleme çözümü gerekir.</span><span class="sxs-lookup"><span data-stu-id="28c6c-144">Your client application needs these values tooconnect toohello remote monitoring solution.</span></span> <span data-ttu-id="28c6c-145">Sonra da **Bitti**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="28c6c-145">Then click **Done**.</span></span>
   
    ![Cihaz kimlik bilgilerini görüntüleme][4]
5. <span data-ttu-id="28c6c-147">Merhaba çözüm Panosu hello aygıt listesinde aygıtınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="28c6c-147">Select your device in hello device list in hello solution dashboard.</span></span> <span data-ttu-id="28c6c-148">Ardından hello **cihaz ayrıntıları** öğesine tıklayın **aygıtı etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="28c6c-148">Then, in hello **Device Details** panel, click **Enable Device**.</span></span> <span data-ttu-id="28c6c-149">Merhaba Cihazınızı durumudur şimdi **çalıştıran**.</span><span class="sxs-lookup"><span data-stu-id="28c6c-149">hello status of your device is now **Running**.</span></span> <span data-ttu-id="28c6c-150">Merhaba Uzaktan izleme çözümü şimdi aygıtınızdan telemetri almasına ve hello aygıtta yöntemleri çağırma.</span><span class="sxs-lookup"><span data-stu-id="28c6c-150">hello remote monitoring solution can now receive telemetry from your device and invoke methods on hello device.</span></span>

[img-dashboard]: ./media/iot-suite-connecting-devices-mbed/dashboard.png
[1]: ./media/iot-suite-connecting-devices-mbed/suite0.png
[2]: ./media/iot-suite-connecting-devices-mbed/suite1.png
[3]: ./media/iot-suite-connecting-devices-mbed/suite2.png
[4]: ./media/iot-suite-connecting-devices-mbed/suite3.png

[lnk-what-are-preconfig-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

## <a name="build-and-run-hello-c-sample-solution"></a><span data-ttu-id="28c6c-151">Derleme ve çalıştırma hello C örnek çözümü</span><span class="sxs-lookup"><span data-stu-id="28c6c-151">Build and run hello C sample solution</span></span>

<span data-ttu-id="28c6c-152">Merhaba aşağıdaki yönergeler açıklar hello adımları bağlanmak için bir [mbed etkin Freescale FRDM K64F] [ lnk-mbed-home] aygıt toohello Uzaktan izleme çözümü.</span><span class="sxs-lookup"><span data-stu-id="28c6c-152">hello following instructions describe hello steps for connecting an [mbed-enabled Freescale FRDM-K64F][lnk-mbed-home] device toohello remote monitoring solution.</span></span>

### <a name="connect-hello-mbed-device-tooyour-network-and-desktop-machine"></a><span data-ttu-id="28c6c-153">Merhaba mbed aygıt tooyour ağ ve Masaüstü makine Bağlan</span><span class="sxs-lookup"><span data-stu-id="28c6c-153">Connect hello mbed device tooyour network and desktop machine</span></span>

1. <span data-ttu-id="28c6c-154">Merhaba mbed aygıt tooyour ağ Ethernet kablosu kullanarak bağlanın.</span><span class="sxs-lookup"><span data-stu-id="28c6c-154">Connect hello mbed device tooyour network using an Ethernet cable.</span></span> <span data-ttu-id="28c6c-155">Bu adım gerekli çünkü Hello örnek uygulama Internet erişimi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="28c6c-155">This step is necessary because hello sample application requires internet access.</span></span>

1. <span data-ttu-id="28c6c-156">Bkz: [mbed ile çalışmaya başlama] [ lnk-mbed-getstarted] tooconnect mbed aygıt tooyour masaüstü bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="28c6c-156">See [Getting Started with mbed][lnk-mbed-getstarted] tooconnect your mbed device tooyour desktop PC.</span></span>

1. <span data-ttu-id="28c6c-157">Windows masaüstü bilgisayarınıza çalıştırıyorsa, bkz: [PC yapılandırma] [ lnk-mbed-pcconnect] tooconfigure seri bağlantı noktası erişim tooyour mbed aygıtı.</span><span class="sxs-lookup"><span data-stu-id="28c6c-157">If your desktop PC is running Windows, see [PC Configuration][lnk-mbed-pcconnect] tooconfigure serial port access tooyour mbed device.</span></span>

### <a name="create-an-mbed-project-and-import-hello-sample-code"></a><span data-ttu-id="28c6c-158">Bir mbed projesi oluşturun ve hello örnek kodunu alma</span><span class="sxs-lookup"><span data-stu-id="28c6c-158">Create an mbed project and import hello sample code</span></span>

<span data-ttu-id="28c6c-159">Bu adımları tooadd bazı örnek kod tooan mbed proje izleyin.</span><span class="sxs-lookup"><span data-stu-id="28c6c-159">Follow these steps tooadd some sample code tooan mbed project.</span></span> <span data-ttu-id="28c6c-160">Merhaba Uzaktan izleme başlangıç projesi içeri aktarıp hello proje toouse hello hello AMQP protokolünü yerine MQTT protokol değiştirin.</span><span class="sxs-lookup"><span data-stu-id="28c6c-160">You import hello remote monitoring starter project and then change hello project toouse hello MQTT protocol instead of hello AMQP protocol.</span></span> <span data-ttu-id="28c6c-161">Şu anda toouse hello MQTT Protokolü toouse hello cihaz yönetim özellikleri IOT hub'ı gerekir.</span><span class="sxs-lookup"><span data-stu-id="28c6c-161">Currently, you need toouse hello MQTT protocol toouse hello device management features of IoT Hub.</span></span>

1. <span data-ttu-id="28c6c-162">Web tarayıcınızda toohello mbed.org Git [Geliştirici site](https://developer.mbed.org/).</span><span class="sxs-lookup"><span data-stu-id="28c6c-162">In your web browser, go toohello mbed.org [developer site](https://developer.mbed.org/).</span></span> <span data-ttu-id="28c6c-163">Kaydolmuş olmasanız seçeneği toocreate (boş) bir hesap görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="28c6c-163">If you haven't signed up, you see an option toocreate an account (it's free).</span></span> <span data-ttu-id="28c6c-164">Aksi takdirde, hesap kimlik bilgileriyle oturum açın.</span><span class="sxs-lookup"><span data-stu-id="28c6c-164">Otherwise, log in with your account credentials.</span></span> <span data-ttu-id="28c6c-165">Ardından **derleyici** hello sağ üst köşesinde hello sayfa içinde.</span><span class="sxs-lookup"><span data-stu-id="28c6c-165">Then click **Compiler** in hello upper right-hand corner of hello page.</span></span> <span data-ttu-id="28c6c-166">Bu eylem toohello getirir *çalışma* arabirimi.</span><span class="sxs-lookup"><span data-stu-id="28c6c-166">This action brings you toohello *Workspace* interface.</span></span>

1. <span data-ttu-id="28c6c-167">Kullanmakta olduğunuz hello donanım platformu hello sağ üst köşesinde hello penceresi içinde görüntülenir veya hello hello sağ köşesindeki tooselect donanım platformunuz simgesini emin olun.</span><span class="sxs-lookup"><span data-stu-id="28c6c-167">Make sure hello hardware platform you're using appears in hello upper right-hand corner of hello window, or click hello icon in hello right-hand corner tooselect your hardware platform.</span></span>

1. <span data-ttu-id="28c6c-168">Tıklatın **alma** hello ana menüsündeki.</span><span class="sxs-lookup"><span data-stu-id="28c6c-168">Click **Import** on hello main menu.</span></span> <span data-ttu-id="28c6c-169">Ardından **tooimport URL'den burayı**.</span><span class="sxs-lookup"><span data-stu-id="28c6c-169">Then click **Click here tooimport from URL**.</span></span>
   
    ![Başlangıç alma toombed çalışma][6]

1. <span data-ttu-id="28c6c-171">Merhaba açılır penceresinde hello bağlantı hello örnek kodu https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ için girin'yi tıklatın **alma**.</span><span class="sxs-lookup"><span data-stu-id="28c6c-171">In hello pop-up window, enter hello link for hello sample code https://developer.mbed.org/users/AzureIoTClient/code/remote_monitoring/ then click **Import**.</span></span>
   
    ![Örnek kod toombed çalışma alma][7]

1. <span data-ttu-id="28c6c-173">Bu projeyi içeri aktarma, çeşitli kitaplıkları da alır, hello mbed derleyici penceresinde görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28c6c-173">You can see in hello mbed compiler window that importing this project also imports various libraries.</span></span> <span data-ttu-id="28c6c-174">Bazı sağlanan ve hello Azure IOT ekibi tarafından korunan ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), diğerleri ise, üçüncü taraf kitaplıklar hello mbed kitaplıkları Kataloğu'nda kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="28c6c-174">Some are provided and maintained by hello Azure IoT team ([azureiot_common](https://developer.mbed.org/users/AzureIoTClient/code/azureiot_common/), [iothub_client](https://developer.mbed.org/users/AzureIoTClient/code/iothub_client/), [iothub_amqp_transport](https://developer.mbed.org/users/AzureIoTClient/code/iothub_amqp_transport/), [azure_uamqp](https://developer.mbed.org/users/AzureIoTClient/code/azure_uamqp/)), while others are third-party libraries available in hello mbed libraries catalog.</span></span>
   
    ![Görünüm mbed proje][8]

1. <span data-ttu-id="28c6c-176">Merhaba, **Program çalışma**, sağ hello **ıothub\_amqp\_aktarım** kitaplığı,'ı tıklatın **silmek**ve ardından**Tamam** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="28c6c-176">In hello **Program Workspace**, right-click hello **iothub\_amqp\_transport** library, click **Delete**, and then click **OK** tooconfirm.</span></span>

1. <span data-ttu-id="28c6c-177">Merhaba, **Program çalışma**, sağ hello **azure\_amqp\_c** kitaplığı tıklatın **silmek**ve ardından **Tamam ** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="28c6c-177">In hello **Program Workspace**, right-click hello **azure\_amqp\_c** library, click **Delete**, and then click **OK** tooconfirm.</span></span>

1. <span data-ttu-id="28c6c-178">Sağ hello **remote_monitoring** hello bir projede **Program çalışma**seçin **içeri aktarma kitaplığını**seçeneğini belirleyip **URL'den**.</span><span class="sxs-lookup"><span data-stu-id="28c6c-178">Right-click hello **remote_monitoring** project in hello **Program Workspace**, select **Import Library**, then select **From URL**.</span></span>
   
    ![Kitaplık alma toombed çalışma Başlat][6]

1. <span data-ttu-id="28c6c-180">Merhaba açılır penceresinde hello bağlantıyı hello MQTT taşıma kitaplığı https://developer.mbed.org/users/AzureIoTClient/code/iothub için girin\_mqtt\_aktarım / ardından **alma**.</span><span class="sxs-lookup"><span data-stu-id="28c6c-180">In hello pop-up window, enter hello link for hello MQTT transport library https://developer.mbed.org/users/AzureIoTClient/code/iothub\_mqtt\_transport/ then click **Import**.</span></span>
   
    ![Kitaplık toombed çalışma alma][12]

1. <span data-ttu-id="28c6c-182">Yineleme hello önceki adım tooadd hello MQTT kitaplığındaki https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c /.</span><span class="sxs-lookup"><span data-stu-id="28c6c-182">Repeat hello previous step tooadd hello MQTT library from https://developer.mbed.org/users/AzureIoTClient/code/azure\_umqtt\_c/.</span></span>

1. <span data-ttu-id="28c6c-183">Çalışma alanınızı şimdi hello aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="28c6c-183">Your workspace now looks like hello following:</span></span>

    ![Mbed çalışma alanını görüntüle][13]

1. <span data-ttu-id="28c6c-185">Açık hello uzak\_monitoring\remote_monitoring.c dosya ve hello Değiştir varolan `#include` koddan hello ifadelerle:</span><span class="sxs-lookup"><span data-stu-id="28c6c-185">Open hello remote\_monitoring\remote_monitoring.c file and replace hello existing `#include` statements with hello following code:</span></span>

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
1. <span data-ttu-id="28c6c-186">Merhaba uzak kodda kalan tüm hello silme\_monitoring\remote\_monitoring.c dosya.</span><span class="sxs-lookup"><span data-stu-id="28c6c-186">Delete all hello remaining code in hello remote\_monitoring\remote\_monitoring.c file.</span></span>

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a><span data-ttu-id="28c6c-187">Derleme ve hello örnek çalıştırma</span><span class="sxs-lookup"><span data-stu-id="28c6c-187">Build and run hello sample</span></span>

<span data-ttu-id="28c6c-188">Kod tooinvoke hello eklemek **uzak\_izleme\_çalıştırmak** işlev oluşturmak ve hello cihaz uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="28c6c-188">Add code tooinvoke hello **remote\_monitoring\_run** function and then build and run hello device application.</span></span>

1. <span data-ttu-id="28c6c-189">Ekleme bir **ana** işlevi hello uzak hello sonuna aşağıdaki kod ile\_monitoring.c dosya tooinvoke hello **uzak\_izleme\_çalıştırmak** işlevi:</span><span class="sxs-lookup"><span data-stu-id="28c6c-189">Add a **main** function with following code at hello end of hello remote\_monitoring.c file tooinvoke hello **remote\_monitoring\_run** function:</span></span>
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. <span data-ttu-id="28c6c-190">Tıklatın **derleme** toobuild hello program.</span><span class="sxs-lookup"><span data-stu-id="28c6c-190">Click **Compile** toobuild hello program.</span></span> <span data-ttu-id="28c6c-191">Güvenli bir şekilde tüm uyarılarını gözardı ancak hello derleme hataları oluşturursa devam etmeden önce düzeltin.</span><span class="sxs-lookup"><span data-stu-id="28c6c-191">You can safely ignore any warnings, but if hello build generates errors, fix them before proceeding.</span></span>

1. <span data-ttu-id="28c6c-192">Merhaba yapı başarılı olursa, hello mbed derleyici Web projenizin hello adla .bin dosyası oluşturur ve tooyour yerel makine indirir.</span><span class="sxs-lookup"><span data-stu-id="28c6c-192">If hello build is successful, hello mbed compiler website generates a .bin file with hello name of your project and downloads it tooyour local machine.</span></span> <span data-ttu-id="28c6c-193">Merhaba .bin dosyasını toohello aygıt kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="28c6c-193">Copy hello .bin file toohello device.</span></span> <span data-ttu-id="28c6c-194">Merhaba .bin dosyasını toohello aygıt kaydetme hello aygıt toorestart neden olur ve hello .bin dosyasının içerdiği hello programını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="28c6c-194">Saving hello .bin file toohello device causes hello device toorestart and run hello program contained in hello .bin file.</span></span> <span data-ttu-id="28c6c-195">Merhaba mbed aygıtta hello sıfırlama düğmesine basarak istediğiniz zaman hello program el ile yeniden başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28c6c-195">You can manually restart hello program at any time by pressing hello reset button on hello mbed device.</span></span>

1. <span data-ttu-id="28c6c-196">PuTTY gibi bir SSH istemci uygulaması kullanarak toohello aygıtı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="28c6c-196">Connect toohello device using an SSH client application, such as PuTTY.</span></span> <span data-ttu-id="28c6c-197">Windows Aygıt Yöneticisi'ni denetleyerek aygıtınızın kullandığı hello seri bağlantı noktası belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28c6c-197">You can determine hello serial port your device uses by checking Windows Device Manager.</span></span>
   
    ![][11]

1. <span data-ttu-id="28c6c-198">PuTTY içinde hello tıklatın **seri** bağlantı türü.</span><span class="sxs-lookup"><span data-stu-id="28c6c-198">In PuTTY, click hello **Serial** connection type.</span></span> <span data-ttu-id="28c6c-199">Hello aygıt genellikle 9600 baud hızında bağlanır, böylece 9600 hello girin **hızı** kutusu.</span><span class="sxs-lookup"><span data-stu-id="28c6c-199">hello device typically connects at 9600 baud, so enter 9600 in hello **Speed** box.</span></span> <span data-ttu-id="28c6c-200">Ardından **açık**.</span><span class="sxs-lookup"><span data-stu-id="28c6c-200">Then click **Open**.</span></span>

1. <span data-ttu-id="28c6c-201">Merhaba program yürütme başlar.</span><span class="sxs-lookup"><span data-stu-id="28c6c-201">hello program starts executing.</span></span> <span data-ttu-id="28c6c-202">Merhaba programı otomatik olarak bağladığınızda başlamazsa tooreset hello Panosu (CTRL + Break veya tuşuna hello panosu'nın Sıfırla düğmesine basın) olabilir.</span><span class="sxs-lookup"><span data-stu-id="28c6c-202">You may have tooreset hello board (press CTRL+Break or press hello board's reset button) if hello program does not start automatically when you connect.</span></span>
   
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
