---
title: "Azure IOT - Ders 1 Connect Intel Edison (C): cihaz yapılandırma | Microsoft Docs"
description: "Intel Edison'u ilk kez kullanmak için yapılandırın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "ayarlama, arduino bağlanmak arduino pc, Kurulum arduino, arduino Panosu"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: bb8aa45b-d3ff-4438-b9d6-a9725a45ade1
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0c92d9f7ba63b0a0929ff95599fd757ea425ef1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-intel-edison"></a><span data-ttu-id="0193d-104">Intel Edison'u yapılandırın</span><span class="sxs-lookup"><span data-stu-id="0193d-104">Configure your Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="0193d-105">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="0193d-105">What you will do</span></span>
<span data-ttu-id="0193d-106">Intel Edison'u yukarı başlatırken Panosu, birleştirerek ilk kez kullanmak için yapılandırın ve yapılandırma aracını yükleme için Edison'u'nın üretici yazılımı, flash, Masaüstü OS parolasını ayarlayın ve Wi-Fi bağlayın.</span><span class="sxs-lookup"><span data-stu-id="0193d-106">Configure Intel Edison for first-time use by assembling the board, powering it up and installing configuration tool to your desktop OS to flash Edison's firmware, set its password and connect it to Wi-Fi.</span></span> <span data-ttu-id="0193d-107">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="0193d-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="0193d-108">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="0193d-108">What you will learn</span></span>
<span data-ttu-id="0193d-109">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="0193d-109">In this article, you will learn:</span></span>

* <span data-ttu-id="0193d-110">Nasıl Edison'u Panosu derleyecek ve yukarı güç.</span><span class="sxs-lookup"><span data-stu-id="0193d-110">How to assemble Edison board and power it up.</span></span>
* <span data-ttu-id="0193d-111">Nasıl Edison'u'nın bellenim flash, parola ayarlama ve Wi-Fi bağlanın.</span><span class="sxs-lookup"><span data-stu-id="0193d-111">How to flash Edison's firmware, set password and connect Wi-Fi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0193d-112">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="0193d-112">What you need</span></span>
<span data-ttu-id="0193d-113">Bu işlemi tamamlamak için aşağıdaki bölümleri, Intel Edison'u Starter Kit gerekir:</span><span class="sxs-lookup"><span data-stu-id="0193d-113">To complete this operation, you need the following parts from your Intel Edison Starter Kit:</span></span>

* <span data-ttu-id="0193d-114">Intel® Edison'u Modülü</span><span class="sxs-lookup"><span data-stu-id="0193d-114">Intel® Edison module</span></span>
* <span data-ttu-id="0193d-115">Arduino genişletme kartı</span><span class="sxs-lookup"><span data-stu-id="0193d-115">Arduino expansion board</span></span>
* <span data-ttu-id="0193d-116">Bir ayırıcı çubukları veya genişletme kartı ve vida ve plastik boşluk ekleyiciler dört kümelerinin modülü fasten iki Vida dahil olmak üzere paketinde bulunan Vida.</span><span class="sxs-lookup"><span data-stu-id="0193d-116">Any spacer bars or screws included in the packaging, including two screws to fasten the module to the expansion board and four sets of screws and plastic spacers.</span></span>
* <span data-ttu-id="0193d-117">Tür bir USB kablosu mikro B</span><span class="sxs-lookup"><span data-stu-id="0193d-117">A Micro B to Type A USB cable</span></span>
* <span data-ttu-id="0193d-118">Bir doğrudan geçerli (DC) güç kaynağı.</span><span class="sxs-lookup"><span data-stu-id="0193d-118">A direct current (DC) power supply.</span></span> <span data-ttu-id="0193d-119">Güç kaynağı gibi derecelendirilmiş:</span><span class="sxs-lookup"><span data-stu-id="0193d-119">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="0193d-120">7 15V DC</span><span class="sxs-lookup"><span data-stu-id="0193d-120">7-15V DC</span></span>
  - <span data-ttu-id="0193d-121">En az 1500mA</span><span class="sxs-lookup"><span data-stu-id="0193d-121">At least 1500mA</span></span>
  - <span data-ttu-id="0193d-122">Merkezi/iç PIN güç kaynağı, pozitif kutbu'na olmalıdır</span><span class="sxs-lookup"><span data-stu-id="0193d-122">The center/inner pin should be the positive pole of the power supply</span></span>

  ![Starter Kit şeyler](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

<span data-ttu-id="0193d-124">Şunları da yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="0193d-124">You also need:</span></span>

* <span data-ttu-id="0193d-125">Windows, Mac veya Linux çalıştıran bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="0193d-125">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="0193d-126">Edison'u bağlanmak için kablosuz bağlantı.</span><span class="sxs-lookup"><span data-stu-id="0193d-126">A wireless connection for Edison to connect to.</span></span>
* <span data-ttu-id="0193d-127">Yapılandırma aracını indirmek için Internet bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="0193d-127">An Internet connection to download configuration tool.</span></span>

## <a name="assemble-your-board"></a><span data-ttu-id="0193d-128">Panonuzu birleştirin</span><span class="sxs-lookup"><span data-stu-id="0193d-128">Assemble your board</span></span>

<span data-ttu-id="0193d-129">Bu bölümde Intel® Edison'u modülünüzün genişletme panonuz ekleme adımlarını içerir.</span><span class="sxs-lookup"><span data-stu-id="0193d-129">This section contains steps to attach your Intel® Edison module to your expansion board.</span></span>

1. <span data-ttu-id="0193d-130">Beyaz Anahat içinde Intel® Edison'u modülü Modül delik genişletme panosunda Vida ile hizalama genişletme panonuzu yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="0193d-130">Place the Intel® Edison module within the white outline on your expansion board, lining up the holes on the module with the screws on the expansion board.</span></span>

2. <span data-ttu-id="0193d-131">Modül sözcükleri hemen altındaki aşağı basın `What will you make?` bir ek düşündüğünüz kadar.</span><span class="sxs-lookup"><span data-stu-id="0193d-131">Press down on the module just below the words `What will you make?` until you feel a snap.</span></span>

   ![Pano 2 birleştirin](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. <span data-ttu-id="0193d-133">(Pakete dahil) iki onaltılık nasıl genişletme Panosu modülü güvenliğini sağlamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="0193d-133">Use the two hex nuts (included in the package) to secure the module to the expansion board.</span></span>

   ![Pano 3 birleştirin](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. <span data-ttu-id="0193d-135">Genişletme panosunda dört köşe delik birinde bir Vidayı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0193d-135">Insert a screw in one of the four corner holes on the expansion board.</span></span> <span data-ttu-id="0193d-136">Bük ve Vidayı üzerine Beyaz Plastik boşluk ekleyiciler birini sıkılaştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0193d-136">Twist and tighten one of the white plastic spacers onto the screw.</span></span>

   ![Pano 4 birleştirin](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. <span data-ttu-id="0193d-138">Diğer üç köşe boşluk ekleyiciler için yineleyin.</span><span class="sxs-lookup"><span data-stu-id="0193d-138">Repeat for the other three corner spacers.</span></span>

   ![Pano 5 birleştirin](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

<span data-ttu-id="0193d-140">Panonuz artık derlenip.</span><span class="sxs-lookup"><span data-stu-id="0193d-140">Now your board is assembled.</span></span>

   ![Birleştirilmiş Panosu](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a><span data-ttu-id="0193d-142">Güç Edison'u ayarlama</span><span class="sxs-lookup"><span data-stu-id="0193d-142">Power up Edison</span></span>

1. <span data-ttu-id="0193d-143">Güç kaynağı takın.</span><span class="sxs-lookup"><span data-stu-id="0193d-143">Plug in the power supply.</span></span>

   ![Güç kaynağı bağlama](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. <span data-ttu-id="0193d-145">(DS1 Arduino * genişletme panosunda etiketli) yeşil bir LED açık ve aydınlatılmış olmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="0193d-145">A green LED(labeled DS1 on the Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="0193d-146">Önyükleme işlemi sonlandırın panosu için bir dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="0193d-146">Wait one minute for the board to finish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0193d-147">DC güç kaynağı yoksa, hala bir USB bağlantı noktası üzerinden Panosu kapatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0193d-147">If you do not have a DC power supply, you can still power the board through a USB port.</span></span> <span data-ttu-id="0193d-148">Bkz: `Connect Edison to your computer` ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="0193d-148">See `Connect Edison to your computer` section for details.</span></span> <span data-ttu-id="0193d-149">Özellikle Wi-Fi kullanarak veya yürüten motors zaman Panonuzu bu şekilde destekleyen, karttan beklenmeyen davranışlara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="0193d-149">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

## <a name="connect-edison-to-your-computer"></a><span data-ttu-id="0193d-150">Edison'u bilgisayarınıza bağlayın</span><span class="sxs-lookup"><span data-stu-id="0193d-150">Connect Edison to your computer</span></span>

1. <span data-ttu-id="0193d-151">Böylece Edison'u aygıt modunda mikro düğme iki mikro USB bağlantı noktası doğru aşağı Değiştir.</span><span class="sxs-lookup"><span data-stu-id="0193d-151">Toggle down the microswitch towards the two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="0193d-152">Cihaz mod ve ana mod arasındaki farklar için lütfen başvuru [burada](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span><span class="sxs-lookup"><span data-stu-id="0193d-152">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Mikro düğme Değiştir](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. <span data-ttu-id="0193d-154">Mikro USB kablosu üst mikro USB bağlantı noktasına takın.</span><span class="sxs-lookup"><span data-stu-id="0193d-154">Plug the micro USB cable into the top micro USB port.</span></span>

   ![Üst mikro USB bağlantı noktası](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. <span data-ttu-id="0193d-156">Bilgisayarınıza bir USB kablosu sonuna takın.</span><span class="sxs-lookup"><span data-stu-id="0193d-156">Plug the other end of USB cable into your computer.</span></span>

   ![Bilgisayar USB](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

4. <span data-ttu-id="0193d-158">Bilgisayarınızın yeni bir sürücüye (çok SD kart bilgisayarınıza ekleme gibi) bağladığında panonuzu tam olarak başlatılmadan bilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0193d-158">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-the-configuration-tool"></a><span data-ttu-id="0193d-159">Karşıdan yükleme ve yapılandırma aracını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0193d-159">Download and run the configuration tool</span></span>
<span data-ttu-id="0193d-160">En son yapılandırma aracından alma [bu bağlantıyı](https://software.intel.com/en-us/iot/hardware/edison/downloads) altında listelenen `Installers` başlığı.</span><span class="sxs-lookup"><span data-stu-id="0193d-160">Get the latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under the `Installers` heading.</span></span> <span data-ttu-id="0193d-161">Aracını Yürüt ve izleyin, ekrandaki yönergeleri, gerektiğinde İleri tıklatıldığında</span><span class="sxs-lookup"><span data-stu-id="0193d-161">Execute the tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="0193d-162">Bellenim flash</span><span class="sxs-lookup"><span data-stu-id="0193d-162">Flash firmware</span></span>
1. <span data-ttu-id="0193d-163">Üzerinde `Set up options` sayfasında, `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="0193d-163">On the `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="0193d-164">Aşağıdakilerden birini yaparak panonuzu Flash görüntüyü seçin:</span><span class="sxs-lookup"><span data-stu-id="0193d-164">Select the image to flash onto your board by doing one of the following:</span></span>
   - <span data-ttu-id="0193d-165">Karşıdan yükle ve panonuzu Intel'in kullanılabilir en son bellenim görüntüsü ile flash için seçin `Download the latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="0193d-165">To download and flash your board with the latest firmware image available from Intel, select `Download the latest image version xxxx`.</span></span>
   - <span data-ttu-id="0193d-166">Panonuzu, önceden kaydettiğiniz bilgisayarınızda bir görüntüyle flash için seçin `Select the local image`.</span><span class="sxs-lookup"><span data-stu-id="0193d-166">To flash your board with an image you already have saved on your computer, select `Select the local image`.</span></span> <span data-ttu-id="0193d-167">Göz atın ve panonuz için flash istediğiniz görüntüyü seçin.</span><span class="sxs-lookup"><span data-stu-id="0193d-167">Browse to and select the image you want to flash to your board.</span></span>
3. <span data-ttu-id="0193d-168">Kurulum aracı panonuzu flash dener.</span><span class="sxs-lookup"><span data-stu-id="0193d-168">The setup tool will attempt to flash your board.</span></span> <span data-ttu-id="0193d-169">Tüm yanıp sönen işlem 10 dakika kadar sürebilir.</span><span class="sxs-lookup"><span data-stu-id="0193d-169">The entire flashing process may take up to 10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="0193d-170">Parola ayarlama</span><span class="sxs-lookup"><span data-stu-id="0193d-170">Set password</span></span>
1. <span data-ttu-id="0193d-171">Üzerinde `Set up options` sayfasında, `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="0193d-171">On the `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="0193d-172">Intel® Edison'u panonuz için bir özel ad ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0193d-172">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="0193d-173">Bu isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="0193d-173">This is optional.</span></span>
3. <span data-ttu-id="0193d-174">Panonuz için bir parola yazın ve ardından `Set password`.</span><span class="sxs-lookup"><span data-stu-id="0193d-174">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="0193d-175">Daha sonra kullanılan parola işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="0193d-175">Mark down the password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="0193d-176">Wi-Fi Bağlan</span><span class="sxs-lookup"><span data-stu-id="0193d-176">Connect Wi-Fi</span></span>
1. <span data-ttu-id="0193d-177">Üzerinde `Set up options` sayfasında, `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="0193d-177">On the `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="0193d-178">Kadar bekleyin, bilgisayarınızın olarak bir dakika için kullanılabilen Wi-Fi ağlarına tarar.</span><span class="sxs-lookup"><span data-stu-id="0193d-178">Wait up to one minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="0193d-179">Gelen `Detected Networks` aşağı açılan listesinde, ağınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="0193d-179">From the `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="0193d-180">Gelen `Security` aşağı açılan listesinde, ağın güvenlik türü seçin.</span><span class="sxs-lookup"><span data-stu-id="0193d-180">From the `Security` drop-down list, select the network's security type.</span></span>
4. <span data-ttu-id="0193d-181">Oturum açma ve parola bilgilerinizi sağlayın ve ardından `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="0193d-181">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="0193d-182">Daha sonra kullanılan IP adresi işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="0193d-182">Mark down the IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="0193d-183">Edison'u bilgisayarınızın aynı ağa bağlı olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="0193d-183">Make sure that Edison is connected to the same network as your computer.</span></span> <span data-ttu-id="0193d-184">Bilgisayarınız, Edison'u IP adresini kullanarak bağlanır.</span><span class="sxs-lookup"><span data-stu-id="0193d-184">Your computer connects to your Edison by using the IP address.</span></span>

<span data-ttu-id="0193d-185">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="0193d-185">Congratulations!</span></span> <span data-ttu-id="0193d-186">Edison'u başarıyla yapılandırdıktan.</span><span class="sxs-lookup"><span data-stu-id="0193d-186">You've successfully configured Edison.</span></span>

## <a name="summary"></a><span data-ttu-id="0193d-187">Özet</span><span class="sxs-lookup"><span data-stu-id="0193d-187">Summary</span></span>
<span data-ttu-id="0193d-188">Bu makalede, Edison'u Panosu birleştirin, flash, üretici yazılımı, Kurulum parola ve yapılandırması aracını kullanarak Wi-Fi bağlanmak nasıl öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="0193d-188">In this article, you’ve learned how to assemble the Edison board, flash its firmware, setup password and connect it to Wi-Fi by using configuration tool.</span></span> <span data-ttu-id="0193d-189">LED henüz açık değil yukarı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0193d-189">Note that the LED doesn't yet light up.</span></span> <span data-ttu-id="0193d-190">Sonraki görev gerekli araçları ve yazılım üzerinde Edison'u örnek bir uygulamayı çalıştırmak için hazırlık yüklemektir.</span><span class="sxs-lookup"><span data-stu-id="0193d-190">The next task is to install the necessary tools and software in preparation for running a sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0193d-191">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0193d-191">Next steps</span></span>
<span data-ttu-id="0193d-192">[Araçları edinin][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="0193d-192">[Get the tools][get-the-tools]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md