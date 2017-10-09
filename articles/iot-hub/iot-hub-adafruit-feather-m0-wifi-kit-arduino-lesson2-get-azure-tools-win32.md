---
title: "Arduino tooAzure IOT - Ders 2 bağlanın: Azure araçlarını (Windows) | Microsoft Docs"
description: "Python ve hello Azure komut satırı arabirimi (Azure CLI) Windows 7 ve sonraki sürümlerde yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure CLI, IOT bulut hizmeti, arduino bulut
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 70dfff14-4be1-468d-9919-e40f4bead308
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f9b891224ff3974d9ce5382eb983470d5d41bcc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="0e1c8-104">Azure araçlarını (Windows 7 ve üzeri) Al</span><span class="sxs-lookup"><span data-stu-id="0e1c8-104">Get Azure tools (Windows 7 and later)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="0e1c8-105">[Windows 7 veya üzeri][windows]</span><span class="sxs-lookup"><span data-stu-id="0e1c8-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="0e1c8-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="0e1c8-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="0e1c8-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="0e1c8-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="0e1c8-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="0e1c8-108">What you will do</span></span>

<span data-ttu-id="0e1c8-109">Python yüklemek ve Azure komut satırı arabirimi (Azure CLI) hello.</span><span class="sxs-lookup"><span data-stu-id="0e1c8-109">Install Python and hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="0e1c8-110">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) Adafruit yumuşatma M0 WiFi Arduino panonuz için.</span><span class="sxs-lookup"><span data-stu-id="0e1c8-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="0e1c8-111">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="0e1c8-111">What you will learn</span></span>
<span data-ttu-id="0e1c8-112">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="0e1c8-112">In this article, you will learn:</span></span>
* <span data-ttu-id="0e1c8-113">Nasıl tooinstall Python.</span><span class="sxs-lookup"><span data-stu-id="0e1c8-113">How tooinstall Python.</span></span>
* <span data-ttu-id="0e1c8-114">Nasıl tooinstall Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="0e1c8-114">How tooinstall hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="0e1c8-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="0e1c8-115">What you need</span></span>
* <span data-ttu-id="0e1c8-116">Bir Internet bağlantısı olan bir Windows bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="0e1c8-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="0e1c8-117">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="0e1c8-117">An active Azure subscription.</span></span> <span data-ttu-id="0e1c8-118">Bir Azure hesabınız yoksa, oluşturma bir [ücretsiz Azure deneme hesabı](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="0e1c8-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="0e1c8-119">Python yüklemek</span><span class="sxs-lookup"><span data-stu-id="0e1c8-119">Install Python</span></span>
<span data-ttu-id="0e1c8-120">[Python yüklemek](https://www.python.org/downloads/) Windows bilgisayarınızda.</span><span class="sxs-lookup"><span data-stu-id="0e1c8-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="0e1c8-121">Python 2.7, 3.4 veya 3.5 yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e1c8-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="0e1c8-122">Bu öğretici, Python 2.7 temel alır.</span><span class="sxs-lookup"><span data-stu-id="0e1c8-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="0e1c8-123">Python'ı zaten yüklediyseniz, toohello sonraki bölümüne gidin ve hello Azure CLI yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0e1c8-123">If you've already installed Python, go toohello next section and install hello Azure CLI.</span></span>

<span data-ttu-id="0e1c8-124">Tooadd hello yolu Python.exe'yi ve pip.exe nerede yüklü toohello sistem hello klasörlerinin etmeniz `PATH` ortam değişkeni.</span><span class="sxs-lookup"><span data-stu-id="0e1c8-124">You also need tooadd hello path of hello folders where python.exe and pip.exe are installed toohello system `PATH` environment variable.</span></span> <span data-ttu-id="0e1c8-125">Varsayılan olarak, Python.exe'yi yüklü `C:\Python27` ve pip.exe yüklü `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="0e1c8-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="0e1c8-126">Hello Azure CLI yükleme</span><span class="sxs-lookup"><span data-stu-id="0e1c8-126">Install hello Azure CLI</span></span>
<span data-ttu-id="0e1c8-127">Hello Azure CLI, Azure için birden çok platformlu bir komut satırı deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="0e1c8-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="0e1c8-128">Doğrudan, komut satırı tooprovision çalışma ve kaynaklarını yönetme.</span><span class="sxs-lookup"><span data-stu-id="0e1c8-128">You work directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="0e1c8-129">tooinstall hello Azure CLI, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="0e1c8-129">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="0e1c8-130">Yönetici olarak bir komut istemi penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="0e1c8-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="0e1c8-131">Merhaba aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="0e1c8-131">Run hello following commands:</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="0e1c8-132">Merhaba aşağıdaki komutu çalıştırarak Hello yüklemeyi doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="0e1c8-132">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="0e1c8-133">Merhaba yükleme başarılı olup olmadığını hello aşağıdaki çıktı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="0e1c8-133">You see hello following output if hello installation is successful.</span></span>

![Başarı belirten bir çıkış][output]

## <a name="summary"></a><span data-ttu-id="0e1c8-135">Özet</span><span class="sxs-lookup"><span data-stu-id="0e1c8-135">Summary</span></span>
<span data-ttu-id="0e1c8-136">Hello Azure CLI yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="0e1c8-136">You've installed hello Azure CLI.</span></span> <span data-ttu-id="0e1c8-137">Sonraki görev toocreate Azure IOT hub ve cihaz kimliğini hello Azure CLI kullanarak.</span><span class="sxs-lookup"><span data-stu-id="0e1c8-137">Your next task toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e1c8-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0e1c8-138">Next steps</span></span>
<span data-ttu-id="0e1c8-139">[IOT hub'ınızı oluşturun ve Arduino panonuzu kaydedin][create-your-iot-hub-and-register-your-arduino-board]</span><span class="sxs-lookup"><span data-stu-id="0e1c8-139">[Create your IoT hub and register your Arduino board][create-your-iot-hub-and-register-your-arduino-board]</span></span>


<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_win.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md