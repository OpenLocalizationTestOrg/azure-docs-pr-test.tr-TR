---
title: "Azure IOT - Ders 2 Raspberry Pi'yi (düğüm) bağlanma: Get Araçlar (Ubuntu) | Microsoft Docs"
description: "Python ve Azure komut satırı arabirimi (Azure CLI) üzerinde macOS yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: IOT bulut hizmeti, azure CLI
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 1814b703-2d81-45db-aff0-eb338c97f120
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 12a8c5b20724e747f3799960a0bd39b82d7fa6b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-macos-1010"></a><span data-ttu-id="9ae52-104">Azure Araçları (macOS 10.10) alın</span><span class="sxs-lookup"><span data-stu-id="9ae52-104">Get Azure tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9ae52-105">Windows 7 ve üzeri</span><span class="sxs-lookup"><span data-stu-id="9ae52-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="9ae52-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="9ae52-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="9ae52-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="9ae52-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="9ae52-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="9ae52-108">What you will do</span></span>
<span data-ttu-id="9ae52-109">Azure komut satırı arabirimi (Azure CLI) yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9ae52-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="9ae52-110">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="9ae52-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9ae52-111">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="9ae52-111">What you will learn</span></span>
<span data-ttu-id="9ae52-112">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="9ae52-112">In this article, you will learn:</span></span>
* <span data-ttu-id="9ae52-113">Azure CLI yükleme.</span><span class="sxs-lookup"><span data-stu-id="9ae52-113">How to install Azure CLI.</span></span>
* <span data-ttu-id="9ae52-114">Azure CLI IOT GUID'sinin ekleme.</span><span class="sxs-lookup"><span data-stu-id="9ae52-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9ae52-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="9ae52-115">What you need</span></span>
* <span data-ttu-id="9ae52-116">Internet bağlantısı olan Mac.</span><span class="sxs-lookup"><span data-stu-id="9ae52-116">A Mac with an Internet connection.</span></span>
* <span data-ttu-id="9ae52-117">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="9ae52-117">An active Azure subscription.</span></span> <span data-ttu-id="9ae52-118">Bir Azure hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz Azure deneme hesabı](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="9ae52-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="9ae52-119">Python yüklemek</span><span class="sxs-lookup"><span data-stu-id="9ae52-119">Install Python</span></span>
<span data-ttu-id="9ae52-120">MacOS kutu dışı Python 2.7 ile veriliyorsa da Homebrew aracılığıyla Python yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="9ae52-120">Although macOS comes with Python 2.7 out of the box, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="9ae52-121">Bkz: [yükleme Python macOS üzerinde](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="9ae52-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="9ae52-122">Python ve PIP aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="9ae52-122">Install Python and pip by running the following command:</span></span>

```bash
brew install python
```

## <a name="install-the-azure-cli"></a><span data-ttu-id="9ae52-123">Azure CLI'yı yükleme</span><span class="sxs-lookup"><span data-stu-id="9ae52-123">Install the Azure CLI</span></span>
<span data-ttu-id="9ae52-124">Azure CLI, Azure için birden çok platformlu bir komut satırı deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="9ae52-124">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="9ae52-125">Doğrudan, komut satırından sağlamak ve kaynakları yönetmek için çalışır.</span><span class="sxs-lookup"><span data-stu-id="9ae52-125">You work directly from your command-line to provision and manage resources.</span></span> 

<span data-ttu-id="9ae52-126">En son Azure CLI yüklemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="9ae52-126">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="9ae52-127">Bir terminal penceresi aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9ae52-127">Run the following commands in a terminal window.</span></span> <span data-ttu-id="9ae52-128">Azure CLI yüklemek için beş dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="9ae52-128">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="9ae52-129">Aşağıdaki komutu çalıştırarak yüklemeyi doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="9ae52-129">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="9ae52-130">Yükleme başarılı olursa aşağıdaki çıktı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ae52-130">You should see the following output if the installation is successful.</span></span>

![Başarı belirten bir çıkış](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a><span data-ttu-id="9ae52-132">Özet</span><span class="sxs-lookup"><span data-stu-id="9ae52-132">Summary</span></span>
<span data-ttu-id="9ae52-133">Azure CLI yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="9ae52-133">You've installed the Azure CLI.</span></span> <span data-ttu-id="9ae52-134">Sonraki göreviniz, Azure CLI kullanarak Azure IOT hub ve cihaz kimliğini oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="9ae52-134">Your next task is to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ae52-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9ae52-135">Next steps</span></span>
[<span data-ttu-id="9ae52-136">IOT hub'ınızı oluşturun ve Raspberry Pi 3 kaydedin</span><span class="sxs-lookup"><span data-stu-id="9ae52-136">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)

