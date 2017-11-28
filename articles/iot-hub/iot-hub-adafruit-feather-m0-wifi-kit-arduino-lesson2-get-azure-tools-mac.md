---
title: "Arduino tooAzure IOT - Ders 2 bağlanın: Azure Araçları (macOS) | Microsoft Docs"
description: "Python ve Azure komut satırı arabirimi (Azure CLI) üzerinde macOS yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure CLI, IOT bulut hizmeti, arduino bulut
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 9b719293-01d2-4a2d-9c49-476e67f4816d
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8f0ec4131e54af5475cd0b4240480c3fda497e14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-macos-1010"></a><span data-ttu-id="67659-104">Azure Araçları (macOS 10.10) alın</span><span class="sxs-lookup"><span data-stu-id="67659-104">Get Azure tools (macOS 10.10)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="67659-105">[Windows 7 veya üzeri][windows]</span><span class="sxs-lookup"><span data-stu-id="67659-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="67659-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="67659-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="67659-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="67659-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="67659-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="67659-108">What you will do</span></span>

<span data-ttu-id="67659-109">Hello Azure komut satırı arabirimi (Azure CLI) yükleyin.</span><span class="sxs-lookup"><span data-stu-id="67659-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="67659-110">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) Adafruit yumuşatma M0 WiFi Arduino panonuz için.</span><span class="sxs-lookup"><span data-stu-id="67659-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="67659-111">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="67659-111">What you will learn</span></span>
<span data-ttu-id="67659-112">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="67659-112">In this article, you will learn:</span></span>
* <span data-ttu-id="67659-113">Nasıl tooinstall Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="67659-113">How tooinstall Azure CLI.</span></span>
* <span data-ttu-id="67659-114">Nasıl tooadd hello Azure CLI IOT GUID'sinin.</span><span class="sxs-lookup"><span data-stu-id="67659-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="67659-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="67659-115">What you need</span></span>
* <span data-ttu-id="67659-116">Internet bağlantısı olan Mac.</span><span class="sxs-lookup"><span data-stu-id="67659-116">A Mac with an Internet connection.</span></span>
* <span data-ttu-id="67659-117">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="67659-117">An active Azure subscription.</span></span> <span data-ttu-id="67659-118">Bir Azure hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz Azure deneme hesabı](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="67659-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="67659-119">Python yüklemek</span><span class="sxs-lookup"><span data-stu-id="67659-119">Install Python</span></span>
<span data-ttu-id="67659-120">MacOS hello kutu dışı Python 2.7 ile veriliyorsa da Homebrew aracılığıyla Python yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="67659-120">Although macOS comes with Python 2.7 out of hello box, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="67659-121">Bkz: [yükleme Python macOS üzerinde](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="67659-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="67659-122">Python ve PIP hello aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="67659-122">Install Python and pip by running hello following command:</span></span>

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a><span data-ttu-id="67659-123">Hello Azure CLI yükleme</span><span class="sxs-lookup"><span data-stu-id="67659-123">Install hello Azure CLI</span></span>
<span data-ttu-id="67659-124">Hello Azure CLI, Azure için birden çok platformlu bir komut satırı deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="67659-124">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="67659-125">Doğrudan, komut satırı tooprovision çalışma ve kaynaklarını yönetme.</span><span class="sxs-lookup"><span data-stu-id="67659-125">You work directly from your command line tooprovision and manage resources.</span></span>

<span data-ttu-id="67659-126">tooinstall en son Azure CLI Merhaba, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="67659-126">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="67659-127">Bir terminal penceresi komutlarda aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="67659-127">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="67659-128">Beş dakika tooinstall hello Azure CLI alabilir.</span><span class="sxs-lookup"><span data-stu-id="67659-128">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="67659-129">Merhaba aşağıdaki komutu çalıştırarak Hello yüklemeyi doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="67659-129">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="67659-130">Merhaba yükleme başarılı olup olmadığını hello aşağıdaki çıktı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="67659-130">You should see hello following output if hello installation is successful.</span></span>

![Başarı belirten bir çıkış][output]

## <a name="summary"></a><span data-ttu-id="67659-132">Özet</span><span class="sxs-lookup"><span data-stu-id="67659-132">Summary</span></span>
<span data-ttu-id="67659-133">Hello Azure CLI yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="67659-133">You've installed hello Azure CLI.</span></span> <span data-ttu-id="67659-134">Sonraki göreviniz toocreate olan Azure CLI kullanarak Azure IOT hub ve cihaz kimliğinizi hello.</span><span class="sxs-lookup"><span data-stu-id="67659-134">Your next task is toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67659-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="67659-135">Next steps</span></span>
<span data-ttu-id="67659-136">[IOT hub'ınızı oluşturun ve Arduino panonuzu kaydedin][create-your-iot-hub-and-register-your-arduino-board]</span><span class="sxs-lookup"><span data-stu-id="67659-136">[Create your IoT hub and register your Arduino board][create-your-iot-hub-and-register-your-arduino-board]</span></span>


<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_osx.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md