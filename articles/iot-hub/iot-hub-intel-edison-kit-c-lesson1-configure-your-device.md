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
# <a name="configure-your-intel-edison"></a>Intel Edison'u yapılandırın
## <a name="what-you-will-do"></a>Ne yapacağını
Intel Edison'u yukarı başlatırken Panosu, birleştirerek ilk kez kullanmak için yapılandırın ve yapılandırma aracını yükleme için Edison'u'nın üretici yazılımı, flash, Masaüstü OS parolasını ayarlayın ve Wi-Fi bağlayın. Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshooting].

## <a name="what-you-will-learn"></a>Bilgi edineceksiniz
Bu makalede, şunları öğreneceksiniz:

* Nasıl Edison'u Panosu derleyecek ve yukarı güç.
* Nasıl Edison'u'nın bellenim flash, parola ayarlama ve Wi-Fi bağlanın.

## <a name="what-you-need"></a>Ne gerekiyor
Bu işlemi tamamlamak için aşağıdaki bölümleri, Intel Edison'u Starter Kit gerekir:

* Intel® Edison'u Modülü
* Arduino genişletme kartı
* Bir ayırıcı çubukları veya genişletme kartı ve vida ve plastik boşluk ekleyiciler dört kümelerinin modülü fasten iki Vida dahil olmak üzere paketinde bulunan Vida.
* Tür bir USB kablosu mikro B
* Bir doğrudan geçerli (DC) güç kaynağı. Güç kaynağı gibi derecelendirilmiş:
  - 7 15V DC
  - En az 1500mA
  - Merkezi/iç PIN güç kaynağı, pozitif kutbu'na olmalıdır

  ![Starter Kit şeyler](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

Şunları da yapmanız gerekir:

* Windows, Mac veya Linux çalıştıran bir bilgisayar.
* Edison'u bağlanmak için kablosuz bağlantı.
* Yapılandırma aracını indirmek için Internet bağlantısı.

## <a name="assemble-your-board"></a>Panonuzu birleştirin

Bu bölümde Intel® Edison'u modülünüzün genişletme panonuz ekleme adımlarını içerir.

1. Beyaz Anahat içinde Intel® Edison'u modülü Modül delik genişletme panosunda Vida ile hizalama genişletme panonuzu yerleştirin.

2. Modül sözcükleri hemen altındaki aşağı basın `What will you make?` bir ek düşündüğünüz kadar.

   ![Pano 2 birleştirin](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. (Pakete dahil) iki onaltılık nasıl genişletme Panosu modülü güvenliğini sağlamak için kullanın.

   ![Pano 3 birleştirin](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. Genişletme panosunda dört köşe delik birinde bir Vidayı ekleyin. Bük ve Vidayı üzerine Beyaz Plastik boşluk ekleyiciler birini sıkılaştırabilirsiniz.

   ![Pano 4 birleştirin](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. Diğer üç köşe boşluk ekleyiciler için yineleyin.

   ![Pano 5 birleştirin](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

Panonuz artık derlenip.

   ![Birleştirilmiş Panosu](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a>Güç Edison'u ayarlama

1. Güç kaynağı takın.

   ![Güç kaynağı bağlama](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. (DS1 Arduino * genişletme panosunda etiketli) yeşil bir LED açık ve aydınlatılmış olmak gerekir.

3. Önyükleme işlemi sonlandırın panosu için bir dakika bekleyin.

   > [!NOTE]
   > DC güç kaynağı yoksa, hala bir USB bağlantı noktası üzerinden Panosu kapatabilirsiniz. Bkz: `Connect Edison to your computer` ayrıntıları bölümü. Özellikle Wi-Fi kullanarak veya yürüten motors zaman Panonuzu bu şekilde destekleyen, karttan beklenmeyen davranışlara neden olabilir.

## <a name="connect-edison-to-your-computer"></a>Edison'u bilgisayarınıza bağlayın

1. Böylece Edison'u aygıt modunda mikro düğme iki mikro USB bağlantı noktası doğru aşağı Değiştir. Cihaz mod ve ana mod arasındaki farklar için lütfen başvuru [burada](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).

   ![Mikro düğme Değiştir](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. Mikro USB kablosu üst mikro USB bağlantı noktasına takın.

   ![Üst mikro USB bağlantı noktası](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. Bilgisayarınıza bir USB kablosu sonuna takın.

   ![Bilgisayar USB](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

4. Bilgisayarınızın yeni bir sürücüye (çok SD kart bilgisayarınıza ekleme gibi) bağladığında panonuzu tam olarak başlatılmadan bilirsiniz.

## <a name="download-and-run-the-configuration-tool"></a>Karşıdan yükleme ve yapılandırma aracını çalıştırın.
En son yapılandırma aracından alma [bu bağlantıyı](https://software.intel.com/en-us/iot/hardware/edison/downloads) altında listelenen `Installers` başlığı. Aracını Yürüt ve izleyin, ekrandaki yönergeleri, gerektiğinde İleri tıklatıldığında

### <a name="flash-firmware"></a>Bellenim flash
1. Üzerinde `Set up options` sayfasında, `Flash Firmware`.
2. Aşağıdakilerden birini yaparak panonuzu Flash görüntüyü seçin:
   - Karşıdan yükle ve panonuzu Intel'in kullanılabilir en son bellenim görüntüsü ile flash için seçin `Download the latest image version xxxx`.
   - Panonuzu, önceden kaydettiğiniz bilgisayarınızda bir görüntüyle flash için seçin `Select the local image`. Göz atın ve panonuz için flash istediğiniz görüntüyü seçin.
3. Kurulum aracı panonuzu flash dener. Tüm yanıp sönen işlem 10 dakika kadar sürebilir.

### <a name="set-password"></a>Parola ayarlama
1. Üzerinde `Set up options` sayfasında, `Enable Security`.
2. Intel® Edison'u panonuz için bir özel ad ayarlayabilirsiniz. Bu isteğe bağlıdır.
3. Panonuz için bir parola yazın ve ardından `Set password`.
4. Daha sonra kullanılan parola işaretleyin.

### <a name="connect-wi-fi"></a>Wi-Fi Bağlan
1. Üzerinde `Set up options` sayfasında, `Connect Wi-Fi`. Kadar bekleyin, bilgisayarınızın olarak bir dakika için kullanılabilen Wi-Fi ağlarına tarar.
2. Gelen `Detected Networks` aşağı açılan listesinde, ağınızı seçin.
3. Gelen `Security` aşağı açılan listesinde, ağın güvenlik türü seçin.
4. Oturum açma ve parola bilgilerinizi sağlayın ve ardından `Configure Wi-Fi`.
5. Daha sonra kullanılan IP adresi işaretleyin.

> [!NOTE]
> Edison'u bilgisayarınızın aynı ağa bağlı olduğundan emin olun. Bilgisayarınız, Edison'u IP adresini kullanarak bağlanır.

Tebrikler! Edison'u başarıyla yapılandırdıktan.

## <a name="summary"></a>Özet
Bu makalede, Edison'u Panosu birleştirin, flash, üretici yazılımı, Kurulum parola ve yapılandırması aracını kullanarak Wi-Fi bağlanmak nasıl öğrendiniz. LED henüz açık değil yukarı unutmayın. Sonraki görev gerekli araçları ve yazılım üzerinde Edison'u örnek bir uygulamayı çalıştırmak için hazırlık yüklemektir.

## <a name="next-steps"></a>Sonraki adımlar
[Araçları edinin][get-the-tools]
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-c-lesson1-get-the-tools-win32.md