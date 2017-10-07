---
title: "aaaIntel Edison'u toocloud (C) - bağlanmak Intel Edison'u tooAzure IOT hub'ı | Microsoft Docs"
description: "Bilgi nasıl toosetup ve Intel Edison'u toosend veri toohello Azure bulut platformu için Intel Edison'u tooAzure IOT hub'ı Bu öğreticide bağlanın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Azure IOT Intel edison'u, Intel edison'u IOT hub, Intel edison'u Gönder veri toocloud, Intel edison'u toocloud"
ms.assetid: 4885fa2c-c2ee-4253-b37f-ccd55f92b006
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/17/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0928e6c7870d724ff2044280937a45a9e032c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-intel-edison-tooazure-iot-hub-c"></a><span data-ttu-id="72dfe-104">Intel Edison'u tooAzure IoT Hub (C) Bağlan</span><span class="sxs-lookup"><span data-stu-id="72dfe-104">Connect Intel Edison tooAzure IoT Hub (C)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="72dfe-105">Bu öğreticide, Intel Edison'u ile çalışmanın hello temelleri öğrenerek başlayın.</span><span class="sxs-lookup"><span data-stu-id="72dfe-105">In this tutorial, you begin by learning hello basics of working with Intel Edison.</span></span> <span data-ttu-id="72dfe-106">Daha sonra nasıl tooseamlessly bağlanacağını aygıtları toohello bulutunuzu kullanarak öğrenin [Azure IOT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="72dfe-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

<span data-ttu-id="72dfe-107">Bir pakete henüz yok mu?</span><span class="sxs-lookup"><span data-stu-id="72dfe-107">Don't have a kit yet?</span></span> <span data-ttu-id="72dfe-108">Başlat [burada](https://azure.microsoft.com/develop/iot/starter-kits)</span><span class="sxs-lookup"><span data-stu-id="72dfe-108">Start [here](https://azure.microsoft.com/develop/iot/starter-kits)</span></span>

## <a name="what-you-do"></a><span data-ttu-id="72dfe-109">Neler</span><span class="sxs-lookup"><span data-stu-id="72dfe-109">What you do</span></span>

* <span data-ttu-id="72dfe-110">Intel Edison'u Kurulum ve ve Grove modüller.</span><span class="sxs-lookup"><span data-stu-id="72dfe-110">Setup Intel Edison and and Grove modules.</span></span>
* <span data-ttu-id="72dfe-111">IOT hub'ı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="72dfe-111">Create an IoT hub.</span></span>
* <span data-ttu-id="72dfe-112">Bir cihaz IOT hub'ınıza Edison'u için kaydetme.</span><span class="sxs-lookup"><span data-stu-id="72dfe-112">Register a device for Edison in your IoT hub.</span></span>
* <span data-ttu-id="72dfe-113">Örnek bir uygulama Edison'u toosend algılayıcı verileri tooyour IOT hub'ına çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="72dfe-113">Run a sample application on Edison toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="72dfe-114">Oluşturduğunuz Intel Edison'u tooan IOT hub bağlayın.</span><span class="sxs-lookup"><span data-stu-id="72dfe-114">Connect Intel Edison tooan IoT hub that you create.</span></span> <span data-ttu-id="72dfe-115">Ardından, örnek bir uygulama üzerinde Edison'u toocollect sıcaklık ve nem veri Grove sıcaklık algılayıcısı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="72dfe-115">Then you run a sample application on Edison toocollect temperature and humidity data from a Grove temperature sensor.</span></span> <span data-ttu-id="72dfe-116">Son olarak, hello algılayıcı verileri tooyour IOT hub'ı gönderin.</span><span class="sxs-lookup"><span data-stu-id="72dfe-116">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="72dfe-117">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="72dfe-117">What you learn</span></span>

* <span data-ttu-id="72dfe-118">Nasıl toocreate Azure IOT hub'ı ve yeni cihaz bağlantı dizenizi alın.</span><span class="sxs-lookup"><span data-stu-id="72dfe-118">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="72dfe-119">Nasıl tooconnect Edison'u Grove sıcaklık algılayıcısı ile.</span><span class="sxs-lookup"><span data-stu-id="72dfe-119">How tooconnect Edison with a Grove temperature sensor.</span></span>
* <span data-ttu-id="72dfe-120">Nasıl Edison'u üzerinde bir örnek uygulamayı çalıştırarak toocollect algılayıcı verileri.</span><span class="sxs-lookup"><span data-stu-id="72dfe-120">How toocollect sensor data by running a sample application on Edison.</span></span>
* <span data-ttu-id="72dfe-121">Nasıl toosend algılayıcı verileri tooyour IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="72dfe-121">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="72dfe-122">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="72dfe-122">What you need</span></span>

![Ne gerekiyor](media/iot-hub-intel-edison-kit-c-get-started/0_kit.png)

* <span data-ttu-id="72dfe-124">Merhaba Intel Edison'u Panosu</span><span class="sxs-lookup"><span data-stu-id="72dfe-124">hello Intel Edison board</span></span>
* <span data-ttu-id="72dfe-125">Arduino genişletme kartı</span><span class="sxs-lookup"><span data-stu-id="72dfe-125">Arduino expansion board</span></span>
* <span data-ttu-id="72dfe-126">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="72dfe-126">An active Azure subscription.</span></span> <span data-ttu-id="72dfe-127">Bir Azure hesabınız yoksa [ücretsiz Azure deneme hesabı oluşturma](https://azure.microsoft.com/free/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="72dfe-127">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="72dfe-128">Mac veya Windows veya Linux çalıştıran bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="72dfe-128">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="72dfe-129">Bir Internet bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="72dfe-129">An Internet connection.</span></span>
* <span data-ttu-id="72dfe-130">Mikro B tooType bir USB kablosu</span><span class="sxs-lookup"><span data-stu-id="72dfe-130">A Micro B tooType A USB cable</span></span>
* <span data-ttu-id="72dfe-131">Bir doğrudan geçerli (DC) güç kaynağı.</span><span class="sxs-lookup"><span data-stu-id="72dfe-131">A direct current (DC) power supply.</span></span> <span data-ttu-id="72dfe-132">Güç kaynağı gibi derecelendirilmiş:</span><span class="sxs-lookup"><span data-stu-id="72dfe-132">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="72dfe-133">7 15V DC</span><span class="sxs-lookup"><span data-stu-id="72dfe-133">7-15V DC</span></span>
  - <span data-ttu-id="72dfe-134">En az 1500mA</span><span class="sxs-lookup"><span data-stu-id="72dfe-134">At least 1500mA</span></span>
  - <span data-ttu-id="72dfe-135">Merhaba merkezi/iç PIN hello pozitif kutbu'na hello güç kaynağı, olmalıdır</span><span class="sxs-lookup"><span data-stu-id="72dfe-135">hello center/inner pin should be hello positive pole of hello power supply</span></span>

<span data-ttu-id="72dfe-136">Aşağıdaki öğelerindeki hello isteğe bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="72dfe-136">hello following items are optional:</span></span>

* <span data-ttu-id="72dfe-137">Grove temel kalkan V2</span><span class="sxs-lookup"><span data-stu-id="72dfe-137">Grove Base Shield V2</span></span>
* <span data-ttu-id="72dfe-138">Grove - sıcaklık algılayıcısı</span><span class="sxs-lookup"><span data-stu-id="72dfe-138">Grove - Temperature Sensor</span></span>
* <span data-ttu-id="72dfe-139">Grove kablosu</span><span class="sxs-lookup"><span data-stu-id="72dfe-139">Grove Cable</span></span>
* <span data-ttu-id="72dfe-140">Bir ayırıcı çubukları veya iki Vida toofasten hello modülü toohello genişletme kartı ve vida ve plastik boşluk ekleyiciler dört kümeleri dahil olmak üzere hello paketleme de dahil Vida.</span><span class="sxs-lookup"><span data-stu-id="72dfe-140">Any spacer bars or screws included in hello packaging, including two screws toofasten hello module toohello expansion board and four sets of screws and plastic spacers.</span></span>

> [!NOTE] 
<span data-ttu-id="72dfe-141">Merhaba kod örnek desteği algılayıcı verilerini benzetimli çünkü bu öğeler isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="72dfe-141">These items are optional because hello code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a><span data-ttu-id="72dfe-142">Intel Edison'u Kurulumu</span><span class="sxs-lookup"><span data-stu-id="72dfe-142">Setup Intel Edison</span></span>

### <a name="assemble-your-board"></a><span data-ttu-id="72dfe-143">Panonuzu birleştirin</span><span class="sxs-lookup"><span data-stu-id="72dfe-143">Assemble your board</span></span>

<span data-ttu-id="72dfe-144">Bu bölümdeki adımları tooattach Intel® Edison'u modülü tooyour genişletme panonuzu içerir.</span><span class="sxs-lookup"><span data-stu-id="72dfe-144">This section contains steps tooattach your Intel® Edison module tooyour expansion board.</span></span>

1. <span data-ttu-id="72dfe-145">Merhaba Intel® Edison'u modülü hello beyaz anahat içinde hello genişletme panosunda hello Vida ile Merhaba delik hello modül hizalama genişletme panonuzu yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="72dfe-145">Place hello Intel® Edison module within hello white outline on your expansion board, lining up hello holes on hello module with hello screws on hello expansion board.</span></span>

2. <span data-ttu-id="72dfe-146">Merhaba modül hello sözcükleri hemen altındaki aşağı basın `What will you make?` bir ek düşündüğünüz kadar.</span><span class="sxs-lookup"><span data-stu-id="72dfe-146">Press down on hello module just below hello words `What will you make?` until you feel a snap.</span></span>

   ![Pano 2 birleştirin](media/iot-hub-intel-edison-kit-c-get-started/1_assemble_board2.jpg)

3. <span data-ttu-id="72dfe-148">Merhaba iki (Merhaba paketine dahil) onaltılık nasıl toosecure hello modülü toohello genişletme kartı kullanın.</span><span class="sxs-lookup"><span data-stu-id="72dfe-148">Use hello two hex nuts (included in hello package) toosecure hello module toohello expansion board.</span></span>

   ![Pano 3 birleştirin](media/iot-hub-intel-edison-kit-c-get-started/2_assemble_board3.jpg)

4. <span data-ttu-id="72dfe-150">Merhaba dört köşe delik hello genişletme panosunda birinde bir Vidayı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="72dfe-150">Insert a screw in one of hello four corner holes on hello expansion board.</span></span> <span data-ttu-id="72dfe-151">Bük ve hello Beyaz Plastik boşluk ekleyiciler hello Vidayı üzerine birini sıkılaştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72dfe-151">Twist and tighten one of hello white plastic spacers onto hello screw.</span></span>

   ![Pano 4 birleştirin](media/iot-hub-intel-edison-kit-c-get-started/3_assemble_board4.jpg)

5. <span data-ttu-id="72dfe-153">Diğer üç köşe boşluk ekleyiciler hello için yineleyin.</span><span class="sxs-lookup"><span data-stu-id="72dfe-153">Repeat for hello other three corner spacers.</span></span>

   ![Pano 5 birleştirin](media/iot-hub-intel-edison-kit-c-get-started/4_assemble_board5.jpg)

<span data-ttu-id="72dfe-155">Panonuz artık derlenip.</span><span class="sxs-lookup"><span data-stu-id="72dfe-155">Now your board is assembled.</span></span>

   ![Birleştirilmiş Panosu](media/iot-hub-intel-edison-kit-c-get-started/5_assembled_board.jpg)

### <a name="connect-hello-grove-base-shield-and-hello-temperature-sensor"></a><span data-ttu-id="72dfe-157">Merhaba Grove temel kalkan ve hello sıcaklık algılayıcısı</span><span class="sxs-lookup"><span data-stu-id="72dfe-157">Connect hello Grove Base Shield and hello temperature sensor</span></span>

1. <span data-ttu-id="72dfe-158">Merhaba Grove temel kalkan tooyour panosunda yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="72dfe-158">Place hello Grove Base Shield on tooyour board.</span></span> <span data-ttu-id="72dfe-159">Tüm PIN'ler panonuzu sıkıca takılı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="72dfe-159">Make sure all pins are tightly plugged into your board.</span></span>
   
   ![Grove temel kalkan](media/iot-hub-intel-edison-kit-c-get-started/6_grove_base_sheild.jpg)

2. <span data-ttu-id="72dfe-161">Kullanım Grove kablo tooconnect Grove sıcaklık algılayıcısı hello Grove temel kalkan üzerine **A0** bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="72dfe-161">Use Grove Cable tooconnect Grove temperature sensor onto hello Grove Base Shield **A0** port.</span></span>

   ![Tootemperature algılayıcı Bağlan](media/iot-hub-intel-edison-kit-c-get-started/7_temperature_sensor.jpg)
   
   ![Edison'u ve algılayıcı bağlantısı](media/iot-hub-intel-edison-kit-c-get-started/16_edion_sensor.png)

<span data-ttu-id="72dfe-164">Artık, algılayıcı hazırdır.</span><span class="sxs-lookup"><span data-stu-id="72dfe-164">Now your sensor is ready.</span></span>

### <a name="power-up-edison"></a><span data-ttu-id="72dfe-165">Güç Edison'u ayarlama</span><span class="sxs-lookup"><span data-stu-id="72dfe-165">Power up Edison</span></span>

1. <span data-ttu-id="72dfe-166">Merhaba güç takın.</span><span class="sxs-lookup"><span data-stu-id="72dfe-166">Plug in hello power supply.</span></span>

   ![Güç kaynağı bağlama](media/iot-hub-intel-edison-kit-c-get-started/8_plug_power.jpg)

2. <span data-ttu-id="72dfe-168">(DS1 hello Arduino * genişletme Panosu üzerinde etiketli) yeşil bir LED açık ve aydınlatılmış olmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="72dfe-168">A green LED(labeled DS1 on hello Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="72dfe-169">Başlangıç Panosu toofinish yukarı önyükleme için bir dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="72dfe-169">Wait one minute for hello board toofinish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="72dfe-170">DC güç kaynağı yoksa, hala bir USB bağlantı noktası üzerinden Güç hello Panosu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72dfe-170">If you do not have a DC power supply, you can still power hello board through a USB port.</span></span> <span data-ttu-id="72dfe-171">Bkz: `Connect Edison tooyour computer` ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="72dfe-171">See `Connect Edison tooyour computer` section for details.</span></span> <span data-ttu-id="72dfe-172">Özellikle Wi-Fi kullanarak veya yürüten motors zaman Panonuzu bu şekilde destekleyen, karttan beklenmeyen davranışlara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="72dfe-172">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

### <a name="connect-edison-tooyour-computer"></a><span data-ttu-id="72dfe-173">Edison'u tooyour bilgisayara bağlanma</span><span class="sxs-lookup"><span data-stu-id="72dfe-173">Connect Edison tooyour computer</span></span>

1. <span data-ttu-id="72dfe-174">Böylece Edison'u aygıt modunda hello mikro düğme hello iki mikro USB bağlantı noktası doğru aşağı Değiştir.</span><span class="sxs-lookup"><span data-stu-id="72dfe-174">Toggle down hello microswitch towards hello two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="72dfe-175">Cihaz mod ve ana mod arasındaki farklar için lütfen başvuru [burada](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span><span class="sxs-lookup"><span data-stu-id="72dfe-175">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Merhaba mikro düğme Değiştir](media/iot-hub-intel-edison-kit-c-get-started/9_toggle_down_microswitch.jpg)

2. <span data-ttu-id="72dfe-177">Merhaba mikro USB kablosu hello üst mikro USB bağlantı noktasına takın.</span><span class="sxs-lookup"><span data-stu-id="72dfe-177">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![Üst mikro USB bağlantı noktası](media/iot-hub-intel-edison-kit-c-get-started/10_top_usbport.jpg)

3. <span data-ttu-id="72dfe-179">Tak bilgisayarınıza USB kablosu diğer ucundaki hello.</span><span class="sxs-lookup"><span data-stu-id="72dfe-179">Plug hello other end of USB cable into your computer.</span></span>

   ![Bilgisayar USB](media/iot-hub-intel-edison-kit-c-get-started/11_computer_usb.jpg)

4. <span data-ttu-id="72dfe-181">Bilgisayarınızın yeni bir sürücüye (çok SD kart bilgisayarınıza ekleme gibi) bağladığında panonuzu tam olarak başlatılmadan bilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72dfe-181">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-hello-configuration-tool"></a><span data-ttu-id="72dfe-182">Karşıdan yükle ve hello yapılandırma aracını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="72dfe-182">Download and run hello configuration tool</span></span>
<span data-ttu-id="72dfe-183">Merhaba en son yapılandırma aracından alma [bu bağlantıyı](https://software.intel.com/en-us/iot/hardware/edison/downloads) hello altında listelenen `Installers` başlığı.</span><span class="sxs-lookup"><span data-stu-id="72dfe-183">Get hello latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under hello `Installers` heading.</span></span> <span data-ttu-id="72dfe-184">Hello aracını Yürüt ve izleyin, ekrandaki yönergeleri, gerektiğinde İleri tıklatıldığında</span><span class="sxs-lookup"><span data-stu-id="72dfe-184">Execute hello tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="72dfe-185">Bellenim flash</span><span class="sxs-lookup"><span data-stu-id="72dfe-185">Flash firmware</span></span>
1. <span data-ttu-id="72dfe-186">Merhaba üzerinde `Set up options` sayfasında, `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="72dfe-186">On hello `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="72dfe-187">Merhaba görüntü tooflash panonuzu üzerine hello aşağıdakilerden birini yaparak seçin:</span><span class="sxs-lookup"><span data-stu-id="72dfe-187">Select hello image tooflash onto your board by doing one of hello following:</span></span>
   - <span data-ttu-id="72dfe-188">toodownload flash panonuzu görüntüsüyle hello en son bellenim Intel'in, kullanılabilir seçip `Download hello latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="72dfe-188">toodownload and flash your board with hello latest firmware image available from Intel, select `Download hello latest image version xxxx`.</span></span>
   - <span data-ttu-id="72dfe-189">panonuzu, önceden kaydettiğiniz bilgisayarınızdan bir görüntüyle tooflash seçin `Select hello local image`.</span><span class="sxs-lookup"><span data-stu-id="72dfe-189">tooflash your board with an image you already have saved on your computer, select `Select hello local image`.</span></span> <span data-ttu-id="72dfe-190">Tooflash tooyour Panosu tooand select hello görüntü göz atın.</span><span class="sxs-lookup"><span data-stu-id="72dfe-190">Browse tooand select hello image you want tooflash tooyour board.</span></span>
3. <span data-ttu-id="72dfe-191">Merhaba Kurulum aracı tooflash panonuzu deneyecek.</span><span class="sxs-lookup"><span data-stu-id="72dfe-191">hello setup tool will attempt tooflash your board.</span></span> <span data-ttu-id="72dfe-192">Merhaba tüm yanıp sönen işlem too10 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="72dfe-192">hello entire flashing process may take up too10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="72dfe-193">Parola ayarlama</span><span class="sxs-lookup"><span data-stu-id="72dfe-193">Set password</span></span>
1. <span data-ttu-id="72dfe-194">Merhaba üzerinde `Set up options` sayfasında, `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="72dfe-194">On hello `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="72dfe-195">Intel® Edison'u panonuz için bir özel ad ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72dfe-195">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="72dfe-196">Bu isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="72dfe-196">This is optional.</span></span>
3. <span data-ttu-id="72dfe-197">Panonuz için bir parola yazın ve ardından `Set password`.</span><span class="sxs-lookup"><span data-stu-id="72dfe-197">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="72dfe-198">Daha sonra kullanılan hello parola işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="72dfe-198">Mark down hello password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="72dfe-199">Wi-Fi Bağlan</span><span class="sxs-lookup"><span data-stu-id="72dfe-199">Connect Wi-Fi</span></span>
1. <span data-ttu-id="72dfe-200">Merhaba üzerinde `Set up options` sayfasında, `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="72dfe-200">On hello `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="72dfe-201">Kullanılabilir kablosuz ağlar için bilgisayar taramaları olarak tooone dakika yukarı bekleyin.</span><span class="sxs-lookup"><span data-stu-id="72dfe-201">Wait up tooone minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="72dfe-202">Merhaba gelen `Detected Networks` aşağı açılan listesinde, ağınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="72dfe-202">From hello `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="72dfe-203">Merhaba gelen `Security` aşağı açılan listesinden, select hello ağın güvenlik türü.</span><span class="sxs-lookup"><span data-stu-id="72dfe-203">From hello `Security` drop-down list, select hello network's security type.</span></span>
4. <span data-ttu-id="72dfe-204">Oturum açma ve parola bilgilerinizi sağlayın ve ardından `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="72dfe-204">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="72dfe-205">Hello daha sonra kullanılan IP adresi işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="72dfe-205">Mark down hello IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="72dfe-206">Edison'u bağlı toohello aynı bilgisayarınızda olarak ağ olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="72dfe-206">Make sure that Edison is connected toohello same network as your computer.</span></span> <span data-ttu-id="72dfe-207">Bilgisayarınızı tooyour Edison'u hello IP adresini kullanarak bağlanır.</span><span class="sxs-lookup"><span data-stu-id="72dfe-207">Your computer connects tooyour Edison by using hello IP address.</span></span>

   ![Tootemperature algılayıcı Bağlan](media/iot-hub-intel-edison-kit-c-get-started/12_configuration_tool.png)

<span data-ttu-id="72dfe-209">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="72dfe-209">Congratulations!</span></span> <span data-ttu-id="72dfe-210">Edison'u başarıyla yapılandırdıktan.</span><span class="sxs-lookup"><span data-stu-id="72dfe-210">You've successfully configured Edison.</span></span>

## <a name="run-a-sample-application-on-intel-edison"></a><span data-ttu-id="72dfe-211">Intel Edison'u üzerinde bir örnek uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="72dfe-211">Run a sample application on Intel Edison</span></span>

### <a name="prepare-hello-azure-iot-device-sdk"></a><span data-ttu-id="72dfe-212">Hello Azure IOT cihaz SDK'sı hazırlama</span><span class="sxs-lookup"><span data-stu-id="72dfe-212">Prepare hello Azure IoT Device SDK</span></span>

1. <span data-ttu-id="72dfe-213">SSH istemcilerini, ana bilgisayar tooconnect tooyour Intel Edison'u aşağıdaki hello birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="72dfe-213">Use one of hello following SSH clients from your host computer tooconnect tooyour Intel Edison.</span></span> <span data-ttu-id="72dfe-214">Başlangıç IP adresi hello yapılandırma aracından ve hello parola hello biri bu aracında ayarladınız.</span><span class="sxs-lookup"><span data-stu-id="72dfe-214">hello IP address is from hello configuration tool and hello password is hello one you've set in that tool.</span></span>
    - <span data-ttu-id="72dfe-215">[PuTTY](http://www.putty.org/) Windows için.</span><span class="sxs-lookup"><span data-stu-id="72dfe-215">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="72dfe-216">Merhaba yerleşik SSH istemcisi Ubuntu veya macOS (çalıştırmak `ssh root@"hello IP address"`).</span><span class="sxs-lookup"><span data-stu-id="72dfe-216">hello built-in SSH client on Ubuntu or macOS (run `ssh root@"hello IP address"`).</span></span>

2. <span data-ttu-id="72dfe-217">Kopya hello örnek istemci uygulaması tooyour aygıt.</span><span class="sxs-lookup"><span data-stu-id="72dfe-217">Clone hello sample client app tooyour device.</span></span> 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-intel-edison-client-app.git
   ```

3. <span data-ttu-id="72dfe-218">Komut toobuild Azure IOT SDK'sı aşağıdaki toohello deposu klasör toorun hello gidin</span><span class="sxs-lookup"><span data-stu-id="72dfe-218">Then navigate toohello repo folder toorun hello following command toobuild Azure IoT SDK</span></span>

   ```bash
   cd iot-hub-c-intel-edison-client-app
   sed -i -e 's/\r$//' buildSDK.sh
   chmod 755 buildSDK.sh
   ./buildSDK.sh
   ```

### <a name="configure-hello-sample-application"></a><span data-ttu-id="72dfe-219">Merhaba örnek uygulamayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="72dfe-219">Configure hello sample application</span></span>

1. <span data-ttu-id="72dfe-220">Merhaba yapılandırma dosyası hello aşağıdaki komutları çalıştırarak açın:</span><span class="sxs-lookup"><span data-stu-id="72dfe-220">Open hello config file by running hello following commands:</span></span>

   ```bash
   nano config.h
   ```

   ![Yapılandırma dosyası](media/iot-hub-intel-edison-kit-c-get-started/13_configure_file.png)

   <span data-ttu-id="72dfe-222">İki makroları vardır bu dosyada configurate olabilir.</span><span class="sxs-lookup"><span data-stu-id="72dfe-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="72dfe-223">Merhaba ilk biridir `INTERVAL`, toocloud Gönder iki ileti arasındaki hello zaman aralığını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="72dfe-223">hello first one is `INTERVAL`, which defines hello time interval between two messages that send toocloud.</span></span> <span data-ttu-id="72dfe-224">İkinci bir hello `SIMULATED_DATA`, veya toouse algılayıcı verilerini olup benzetimi için bir Boole değeri değil.</span><span class="sxs-lookup"><span data-stu-id="72dfe-224">hello second one `SIMULATED_DATA`,which is a Boolean value for whether toouse simulated sensor data or not.</span></span>

   <span data-ttu-id="72dfe-225">Varsa, **hello algılayıcı yok**ayarlayın hello `SIMULATED_DATA` çok değer`1` toomake Merhaba örnek uygulaması oluşturup benzetimli algılayıcı verilerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72dfe-225">If you **don't have hello sensor**, set hello `SIMULATED_DATA` value too`1` toomake hello sample application create and use simulated sensor data.</span></span>

2. <span data-ttu-id="72dfe-226">Kaydedip çıkmak denetimi O tuşlarına basarak > Enter > Denetim X.</span><span class="sxs-lookup"><span data-stu-id="72dfe-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="build-and-run-hello-sample-application"></a><span data-ttu-id="72dfe-227">Derleme ve hello örnek uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="72dfe-227">Build and run hello sample application</span></span>

1. <span data-ttu-id="72dfe-228">Merhaba örnek uygulaması hello aşağıdaki komutu çalıştırarak oluşturun:</span><span class="sxs-lookup"><span data-stu-id="72dfe-228">Build hello sample application by running hello following command:</span></span>

   ```bash
   cmake . && make
   ```
   ![Çıktı derleme](media/iot-hub-intel-edison-kit-c-get-started/14_build_output.png)

1. <span data-ttu-id="72dfe-230">Merhaba aşağıdaki komutu çalıştırarak Hello örnek uygulamayı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="72dfe-230">Run hello sample application by running hello following command:</span></span>

   ```bash
   sudo ./app '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="72dfe-231">Kopyalama hello cihaz bağlantı dizesi hello tek tırnak yapıştırma emin olun.</span><span class="sxs-lookup"><span data-stu-id="72dfe-231">Make sure you copy-paste hello device connection string into hello single quotes.</span></span>

<span data-ttu-id="72dfe-232">Gösterir tooyour IOT hub gönderilen algılayıcı verileri ve hello iletileri hello hello aşağıdaki çıktı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="72dfe-232">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

![Çıktı - Intel Edison'u tooyour IOT hub'ından gönderilen algılayıcı verileri](media/iot-hub-intel-edison-kit-c-get-started/15_message_sent.png)

## <a name="next-steps"></a><span data-ttu-id="72dfe-234">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="72dfe-234">Next steps</span></span>

<span data-ttu-id="72dfe-235">Bir örnek uygulama toocollect algılayıcı verilerini çalıştırdıktan ve tooyour IOT hub'ı gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72dfe-235">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
