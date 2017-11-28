---
title: "Raspberry Pi'yi (düğüm) tooAzure IOT - Ders 2 bağlanın: alma araçlarını (Windows) | Microsoft Docs"
description: "Python ve hello Azure komut satırı arabirimi (Azure CLI) Windows 7 ve sonraki sürümlerde yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: IOT bulut hizmeti, azure CLI
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: acfa13e3-6d2c-4e68-9a77-1cbc2cf3f9c1
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 25b50214322137ea32861fd1131c474e2fc7ebb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="64c64-104">Azure araçlarını (Windows 7 ve üzeri) Al</span><span class="sxs-lookup"><span data-stu-id="64c64-104">Get Azure tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="64c64-105">Windows 7 ve üzeri</span><span class="sxs-lookup"><span data-stu-id="64c64-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="64c64-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="64c64-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="64c64-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="64c64-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="64c64-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="64c64-108">What you will do</span></span>
<span data-ttu-id="64c64-109">Python yüklemek ve Azure komut satırı arabirimi (Azure CLI) hello.</span><span class="sxs-lookup"><span data-stu-id="64c64-109">Install Python and hello Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="64c64-110">Herhangi bir sorun varsa, hello çözümlerini arayın [sorun giderme sayfası](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="64c64-110">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="64c64-111">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="64c64-111">What you will learn</span></span>
<span data-ttu-id="64c64-112">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="64c64-112">In this article, you will learn:</span></span>
* <span data-ttu-id="64c64-113">Nasıl tooinstall Python.</span><span class="sxs-lookup"><span data-stu-id="64c64-113">How tooinstall Python.</span></span>
* <span data-ttu-id="64c64-114">Nasıl tooinstall Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="64c64-114">How tooinstall hello Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="64c64-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="64c64-115">What you need</span></span>
* <span data-ttu-id="64c64-116">Bir Internet bağlantısı olan bir Windows bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="64c64-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="64c64-117">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="64c64-117">An active Azure subscription.</span></span> <span data-ttu-id="64c64-118">Bir Azure hesabınız yoksa, oluşturma bir [ücretsiz Azure deneme hesabı](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="64c64-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="64c64-119">Python yüklemek</span><span class="sxs-lookup"><span data-stu-id="64c64-119">Install Python</span></span>
<span data-ttu-id="64c64-120">[Python yüklemek](https://www.python.org/downloads/) Windows bilgisayarınızda.</span><span class="sxs-lookup"><span data-stu-id="64c64-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="64c64-121">Python 2.7, 3.4 veya 3.5 yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64c64-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="64c64-122">Bu öğretici, Python 2.7 temel alır.</span><span class="sxs-lookup"><span data-stu-id="64c64-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="64c64-123">Python'ı zaten yüklediyseniz, toohello sonraki bölümüne gidin ve hello Azure CLI yükleyin.</span><span class="sxs-lookup"><span data-stu-id="64c64-123">If you've already installed Python, go toohello next section and install hello Azure CLI.</span></span>

<span data-ttu-id="64c64-124">Tooadd hello yolu Python.exe'yi ve pip.exe nerede yüklü toohello sistem hello klasörlerinin etmeniz `PATH` ortam değişkeni.</span><span class="sxs-lookup"><span data-stu-id="64c64-124">You also need tooadd hello path of hello folders where python.exe and pip.exe are installed toohello system `PATH` environment variable.</span></span> <span data-ttu-id="64c64-125">Varsayılan olarak, Python.exe'yi yüklü `C:\Python27` ve pip.exe yüklü `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="64c64-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-hello-azure-cli"></a><span data-ttu-id="64c64-126">Hello Azure CLI yükleme</span><span class="sxs-lookup"><span data-stu-id="64c64-126">Install hello Azure CLI</span></span>
<span data-ttu-id="64c64-127">Hello Azure CLI, Azure için birden çok platformlu bir komut satırı deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="64c64-127">hello Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="64c64-128">Doğrudan komut satırı, tooprovision çalışma ve kaynaklarını yönetme.</span><span class="sxs-lookup"><span data-stu-id="64c64-128">You work directly from your command-line tooprovision and manage resources.</span></span>

<span data-ttu-id="64c64-129">tooinstall hello Azure CLI, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="64c64-129">tooinstall hello Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="64c64-130">Yönetici olarak bir komut istemi penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="64c64-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="64c64-131">Merhaba aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="64c64-131">Run hello following commands:</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="64c64-132">Merhaba aşağıdaki komutu çalıştırarak Hello yüklemeyi doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="64c64-132">Verify hello installation by running hello following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="64c64-133">Merhaba yükleme başarılı olup olmadığını hello aşağıdaki çıktı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="64c64-133">You see hello following output if hello installation is successful.</span></span>

![Başarı belirten bir çıkış](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a><span data-ttu-id="64c64-135">Özet</span><span class="sxs-lookup"><span data-stu-id="64c64-135">Summary</span></span>
<span data-ttu-id="64c64-136">Hello Azure CLI yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="64c64-136">You've installed hello Azure CLI.</span></span> <span data-ttu-id="64c64-137">Sonraki görev toocreate Azure IOT hub ve cihaz kimliğini hello Azure CLI kullanarak.</span><span class="sxs-lookup"><span data-stu-id="64c64-137">Your next task toocreate your Azure IoT hub and device identity by using hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64c64-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="64c64-138">Next steps</span></span>
[<span data-ttu-id="64c64-139">IOT hub'ınızı oluşturun ve Raspberry Pi 3 kaydedin</span><span class="sxs-lookup"><span data-stu-id="64c64-139">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)

