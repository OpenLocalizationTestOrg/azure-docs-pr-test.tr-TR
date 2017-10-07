---
title: "Connect Intel Edison (C) tooAzure IOT - Ders 2: Azure Araçları (macOS) | Microsoft Docs"
description: "Python ve Azure komut satırı arabirimi (Azure CLI) üzerinde macOS yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure CLI, IOT bulut hizmeti, arduino bulut
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: d561680f-69cc-427a-820d-24f710ba05a8
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0dfc9ff90e879d5fd03040016ac71a9fe4f4a744
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-macos-1010"></a><span data-ttu-id="37239-104">Azure Araçları (macOS 10.10) alın</span><span class="sxs-lookup"><span data-stu-id="37239-104">Get Azure tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="37239-105">[Windows 7 ve üzeri][windows]</span><span class="sxs-lookup"><span data-stu-id="37239-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="37239-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="37239-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="37239-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="37239-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="37239-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="37239-108">What you will do</span></span>
<span data-ttu-id="37239-109">Hello Azure komut satırı arabirimi (Azure CLI) yükleyin.</span><span class="sxs-lookup"><span data-stu-id="37239-109">Install hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="37239-110">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="37239-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="37239-111">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="37239-111">What you will learn</span></span>
<span data-ttu-id="37239-112">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="37239-112">In this article, you will learn:</span></span>
* <span data-ttu-id="37239-113">Nasıl tooinstall Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="37239-113">How tooinstall Azure CLI.</span></span>
* <span data-ttu-id="37239-114">Nasıl tooadd hello Azure CLI IOT GUID'sinin.</span><span class="sxs-lookup"><span data-stu-id="37239-114">How tooadd an IoT subgroup of hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="37239-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="37239-115">What you need</span></span>
* <span data-ttu-id="37239-116">Internet bağlantısı olan Mac.</span><span class="sxs-lookup"><span data-stu-id="37239-116">A Mac with an Internet connection.</span></span>
* <span data-ttu-id="37239-117">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="37239-117">An active Azure subscription.</span></span> <span data-ttu-id="37239-118">Bir Azure hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz Azure deneme hesabı](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="37239-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="37239-119">Python yüklemek</span><span class="sxs-lookup"><span data-stu-id="37239-119">Install Python</span></span>
<span data-ttu-id="37239-120">MacOS hello kutu dışı Python 2.7 ile veriliyorsa da Homebrew aracılığıyla Python yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="37239-120">Although macOS comes with Python 2.7 out of hello box, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="37239-121">Bkz: [yükleme Python macOS üzerinde](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="37239-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="37239-122">Python ve PIP hello aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="37239-122">Install Python and pip by running hello following command:</span></span>

```bash
brew install python
```

## <a name="install-hello-azure-cli"></a><span data-ttu-id="37239-123">Hello Azure CLI yükleme</span><span class="sxs-lookup"><span data-stu-id="37239-123">Install hello Azure CLI</span></span>
<span data-ttu-id="37239-124">Hello Azure CLI, Azure için birden çok platformlu bir komut satırı deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="37239-124">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="37239-125">Doğrudan, komut satırı tooprovision çalışma ve kaynaklarını yönetme.</span><span class="sxs-lookup"><span data-stu-id="37239-125">You work directly from your command line tooprovision and manage resources.</span></span> 

<span data-ttu-id="37239-126">tooinstall en son Azure CLI Merhaba, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="37239-126">tooinstall hello latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="37239-127">Bir terminal penceresi komutlarda aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="37239-127">Run hello following commands in a terminal window.</span></span> <span data-ttu-id="37239-128">Beş dakika tooinstall hello Azure CLI alabilir.</span><span class="sxs-lookup"><span data-stu-id="37239-128">It might take five minutes tooinstall hello Azure CLI.</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="37239-129">Merhaba aşağıdaki komutu çalıştırarak Hello yüklemeyi doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="37239-129">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="37239-130">Merhaba yükleme başarılı olup olmadığını hello aşağıdaki çıktı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="37239-130">You should see hello following output if hello installation is successful.</span></span>

![Başarı belirten bir çıkış](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a><span data-ttu-id="37239-132">Özet</span><span class="sxs-lookup"><span data-stu-id="37239-132">Summary</span></span>
<span data-ttu-id="37239-133">Hello Azure CLI yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="37239-133">You've installed hello Azure CLI.</span></span> <span data-ttu-id="37239-134">Sonraki göreviniz toocreate olan Azure CLI kullanarak Azure IOT hub ve cihaz kimliğinizi hello.</span><span class="sxs-lookup"><span data-stu-id="37239-134">Your next task is toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37239-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="37239-135">Next steps</span></span>
<span data-ttu-id="37239-136">[IOT hub'ınızı oluşturun ve Intel Edison'u kaydedin][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="37239-136">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
