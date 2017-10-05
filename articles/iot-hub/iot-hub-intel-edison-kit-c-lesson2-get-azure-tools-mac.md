---
title: "Azure IOT - Ders 2 Connect Intel Edison (C): Azure Araçları (macOS) | Microsoft Docs"
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
ms.openlocfilehash: 97beb04781f3f9809cdafc945d9499e71cbbd9b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-macos-1010"></a><span data-ttu-id="4f034-104">Azure Araçları (macOS 10.10) alın</span><span class="sxs-lookup"><span data-stu-id="4f034-104">Get Azure tools (macOS 10.10)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="4f034-105">[Windows 7 ve üzeri][windows]</span><span class="sxs-lookup"><span data-stu-id="4f034-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="4f034-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="4f034-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="4f034-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="4f034-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="4f034-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="4f034-108">What you will do</span></span>
<span data-ttu-id="4f034-109">Azure komut satırı arabirimi (Azure CLI) yükleyin.</span><span class="sxs-lookup"><span data-stu-id="4f034-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="4f034-110">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="4f034-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="4f034-111">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="4f034-111">What you will learn</span></span>
<span data-ttu-id="4f034-112">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="4f034-112">In this article, you will learn:</span></span>
* <span data-ttu-id="4f034-113">Azure CLI yükleme.</span><span class="sxs-lookup"><span data-stu-id="4f034-113">How to install Azure CLI.</span></span>
* <span data-ttu-id="4f034-114">Azure CLI IOT GUID'sinin ekleme.</span><span class="sxs-lookup"><span data-stu-id="4f034-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4f034-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="4f034-115">What you need</span></span>
* <span data-ttu-id="4f034-116">Internet bağlantısı olan Mac.</span><span class="sxs-lookup"><span data-stu-id="4f034-116">A Mac with an Internet connection.</span></span>
* <span data-ttu-id="4f034-117">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="4f034-117">An active Azure subscription.</span></span> <span data-ttu-id="4f034-118">Bir Azure hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz Azure deneme hesabı](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="4f034-118">If you don't have an Azure account, you can create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="4f034-119">Python yüklemek</span><span class="sxs-lookup"><span data-stu-id="4f034-119">Install Python</span></span>
<span data-ttu-id="4f034-120">MacOS kutu dışı Python 2.7 ile veriliyorsa da Homebrew aracılığıyla Python yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="4f034-120">Although macOS comes with Python 2.7 out of the box, we recommend that you install Python through Homebrew.</span></span> <span data-ttu-id="4f034-121">Bkz: [yükleme Python macOS üzerinde](http://docs.python-guide.org/en/latest/starting/install/osx/).</span><span class="sxs-lookup"><span data-stu-id="4f034-121">See [Installing Python on macOS](http://docs.python-guide.org/en/latest/starting/install/osx/).</span></span>

<span data-ttu-id="4f034-122">Python ve PIP aşağıdaki komutu çalıştırarak yükleyin:</span><span class="sxs-lookup"><span data-stu-id="4f034-122">Install Python and pip by running the following command:</span></span>

```bash
brew install python
```

## <a name="install-the-azure-cli"></a><span data-ttu-id="4f034-123">Azure CLI'yı yükleme</span><span class="sxs-lookup"><span data-stu-id="4f034-123">Install the Azure CLI</span></span>
<span data-ttu-id="4f034-124">Azure CLI, Azure için birden çok platformlu bir komut satırı deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="4f034-124">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="4f034-125">Doğrudan komut satırından sağlamak için çalışır ve kaynaklarını yönetme.</span><span class="sxs-lookup"><span data-stu-id="4f034-125">You work directly from your command line to provision and manage resources.</span></span> 

<span data-ttu-id="4f034-126">En son Azure CLI yüklemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4f034-126">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="4f034-127">Bir terminal penceresi aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4f034-127">Run the following commands in a terminal window.</span></span> <span data-ttu-id="4f034-128">Azure CLI yüklemek için beş dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="4f034-128">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="4f034-129">Aşağıdaki komutu çalıştırarak yüklemeyi doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="4f034-129">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="4f034-130">Yükleme başarılı olursa aşağıdaki çıktı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f034-130">You should see the following output if the installation is successful.</span></span>

![Başarı belirten bir çıkış](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_osx.png)

## <a name="summary"></a><span data-ttu-id="4f034-132">Özet</span><span class="sxs-lookup"><span data-stu-id="4f034-132">Summary</span></span>
<span data-ttu-id="4f034-133">Azure CLI yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="4f034-133">You've installed the Azure CLI.</span></span> <span data-ttu-id="4f034-134">Sonraki göreviniz, Azure CLI kullanarak Azure IOT hub ve cihaz kimliğini oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="4f034-134">Your next task is to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f034-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4f034-135">Next steps</span></span>
<span data-ttu-id="4f034-136">[IOT hub'ınızı oluşturun ve Intel Edison'u kaydedin][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="4f034-136">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-c-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-c-lesson2-get-azure-tools-mac.md
