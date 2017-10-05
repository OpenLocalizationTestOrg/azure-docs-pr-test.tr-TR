---
title: "Azure IOT - Ders 2 Arduino bağlanın: Azure Araçları (Ubuntu) | Microsoft Docs"
description: "Python ve Azure komut satırı arabirimi (Azure CLI) üzerinde Ubuntu yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure CLI, IOT bulut hizmeti, arduino bulut
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: bb5cb602-7292-4772-ac90-c0b52ebc8340
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: a2f83e59a37abc3f44e770b22ac089b88481a6a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="a0370-104">Azure Araçları (Ubuntu 16.04) alın</span><span class="sxs-lookup"><span data-stu-id="a0370-104">Get Azure tools (Ubuntu 16.04)</span></span>

> [!div class="op_single_selector"]
> * <span data-ttu-id="a0370-105">[Windows 7 veya üzeri][windows]</span><span class="sxs-lookup"><span data-stu-id="a0370-105">[Windows 7 or later][windows]</span></span>
> * <span data-ttu-id="a0370-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="a0370-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="a0370-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="a0370-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="a0370-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="a0370-108">What you will do</span></span>

<span data-ttu-id="a0370-109">Azure komut satırı arabirimi (Azure CLI) yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a0370-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="a0370-110">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) Adafruit yumuşatma M0 WiFi Arduino panonuz için.</span><span class="sxs-lookup"><span data-stu-id="a0370-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a0370-111">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="a0370-111">What you will learn</span></span>
<span data-ttu-id="a0370-112">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="a0370-112">In this article, you will learn:</span></span>
* <span data-ttu-id="a0370-113">Azure CLI yükleme.</span><span class="sxs-lookup"><span data-stu-id="a0370-113">How to install the Azure CLI.</span></span>
* <span data-ttu-id="a0370-114">Azure CLI IOT GUID'sinin ekleme.</span><span class="sxs-lookup"><span data-stu-id="a0370-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a0370-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="a0370-115">What you need</span></span>
* <span data-ttu-id="a0370-116">Bir Internet bağlantısı olan bir Ubuntu bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="a0370-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="a0370-117">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="a0370-117">An active Azure subscription.</span></span> <span data-ttu-id="a0370-118">Bir hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz deneme sürümü hesabı](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="a0370-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="a0370-119">Azure CLI'yı yükleme</span><span class="sxs-lookup"><span data-stu-id="a0370-119">Install the Azure CLI</span></span>
<span data-ttu-id="a0370-120">Azure CLI çok platformlu bir komut satırı deneyimi, Azure için doğrudan komut satırından sağlamak için çalışma ve kaynakları yönetmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="a0370-120">The Azure CLI provides a multiplatform command-line experience for Azure, enabling you to work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="a0370-121">En son Azure CLI yüklemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="a0370-121">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="a0370-122">Bir terminal penceresi aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a0370-122">Run the following commands in a terminal window.</span></span> <span data-ttu-id="a0370-123">Azure CLI yüklemek için beş dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="a0370-123">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="a0370-124">Aşağıdaki komutu çalıştırarak yüklemeyi doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="a0370-124">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="a0370-125">Yükleme başarılı olursa aşağıdaki çıktı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a0370-125">You should see the following output if the installation is successful.</span></span>

![Başarı belirten bir çıkış][output]

## <a name="summary"></a><span data-ttu-id="a0370-127">Özet</span><span class="sxs-lookup"><span data-stu-id="a0370-127">Summary</span></span>
<span data-ttu-id="a0370-128">Azure CLI yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="a0370-128">You've installed the Azure CLI.</span></span> <span data-ttu-id="a0370-129">Sonraki göreviniz Azure CLI kullanarak Azure IOT hub ve cihaz kimliğinizi oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="a0370-129">Your next task is to create your Azure IoT hub and device identity using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0370-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a0370-130">Next steps</span></span>
<span data-ttu-id="a0370-131">[IOT hub'ınızı oluşturun ve Arduino panonuzu kaydedin][create-your-iot-hub-and-register-your-arduino-board]</span><span class="sxs-lookup"><span data-stu-id="a0370-131">[Create your IoT hub and register your Arduino board][create-your-iot-hub-and-register-your-arduino-board]</span></span>
<!-- Images and links -->

[windows]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-mac.md
[output]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson2/az_iot_help_ubuntu.png
[create-your-iot-hub-and-register-your-arduino-board]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md