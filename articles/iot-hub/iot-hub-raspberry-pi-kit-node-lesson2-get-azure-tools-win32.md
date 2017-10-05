---
title: "Azure IOT - Ders 2 Raspberry Pi'yi (düğüm) bağlanma: alma araçlarını (Windows) | Microsoft Docs"
description: "Python ve Azure komut satırı arabirimi (Azure CLI) Windows 7 ve sonraki sürümlerde yükleyin."
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
ms.openlocfilehash: c7b927997b738f7a80b71c06d4dff2278dc7c64e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-windows-7-and-later"></a><span data-ttu-id="cab86-104">Azure araçlarını (Windows 7 ve üzeri) Al</span><span class="sxs-lookup"><span data-stu-id="cab86-104">Get Azure tools (Windows 7 and later)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cab86-105">Windows 7 ve üzeri</span><span class="sxs-lookup"><span data-stu-id="cab86-105">Windows 7 and later</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-win32.md)
> * [<span data-ttu-id="cab86-106">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="cab86-106">Ubuntu 16.04</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-ubuntu.md)
> * [<span data-ttu-id="cab86-107">macOS 10.10</span><span class="sxs-lookup"><span data-stu-id="cab86-107">macOS 10.10</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-get-azure-tools-mac.md)

## <a name="what-you-will-do"></a><span data-ttu-id="cab86-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="cab86-108">What you will do</span></span>
<span data-ttu-id="cab86-109">Python ve Azure komut satırı arabirimi (Azure CLI) yükleyin.</span><span class="sxs-lookup"><span data-stu-id="cab86-109">Install Python and the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="cab86-110">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="cab86-110">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="cab86-111">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="cab86-111">What you will learn</span></span>
<span data-ttu-id="cab86-112">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="cab86-112">In this article, you will learn:</span></span>
* <span data-ttu-id="cab86-113">Python yükleme.</span><span class="sxs-lookup"><span data-stu-id="cab86-113">How to install Python.</span></span>
* <span data-ttu-id="cab86-114">Azure CLI yükleme.</span><span class="sxs-lookup"><span data-stu-id="cab86-114">How to install the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="cab86-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="cab86-115">What you need</span></span>
* <span data-ttu-id="cab86-116">Bir Internet bağlantısı olan bir Windows bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="cab86-116">A Windows computer with an Internet connection.</span></span>
* <span data-ttu-id="cab86-117">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="cab86-117">An active Azure subscription.</span></span> <span data-ttu-id="cab86-118">Bir Azure hesabınız yoksa, oluşturma bir [ücretsiz Azure deneme hesabı](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="cab86-118">If you don't have an Azure account, create a [free Azure trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-python"></a><span data-ttu-id="cab86-119">Python yüklemek</span><span class="sxs-lookup"><span data-stu-id="cab86-119">Install Python</span></span>
<span data-ttu-id="cab86-120">[Python yüklemek](https://www.python.org/downloads/) Windows bilgisayarınızda.</span><span class="sxs-lookup"><span data-stu-id="cab86-120">[Install Python](https://www.python.org/downloads/) on your Windows computer.</span></span> <span data-ttu-id="cab86-121">Python 2.7, 3.4 veya 3.5 yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cab86-121">You can install Python 2.7, 3.4 or 3.5.</span></span> <span data-ttu-id="cab86-122">Bu öğretici, Python 2.7 temel alır.</span><span class="sxs-lookup"><span data-stu-id="cab86-122">This tutorial is based on Python 2.7.</span></span> <span data-ttu-id="cab86-123">Python'ı zaten yüklediyseniz, sonraki bölüme gidin ve Azure CLI yükleme.</span><span class="sxs-lookup"><span data-stu-id="cab86-123">If you've already installed Python, go to the next section and install the Azure CLI.</span></span>

<span data-ttu-id="cab86-124">Ayrıca Python.exe'yi ve pip.exe yüklendiği için sistem klasörlerinin yolu eklemek gereken `PATH` ortam değişkeni.</span><span class="sxs-lookup"><span data-stu-id="cab86-124">You also need to add the path of the folders where python.exe and pip.exe are installed to the system `PATH` environment variable.</span></span> <span data-ttu-id="cab86-125">Varsayılan olarak, Python.exe'yi yüklü `C:\Python27` ve pip.exe yüklü `C:\Python27\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="cab86-125">By default, python.exe is installed in `C:\Python27` and pip.exe is installed in `C:\Python27\Scripts`.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="cab86-126">Azure CLI'yı yükleme</span><span class="sxs-lookup"><span data-stu-id="cab86-126">Install the Azure CLI</span></span>
<span data-ttu-id="cab86-127">Azure CLI, Azure için birden çok platformlu bir komut satırı deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="cab86-127">The Azure CLI provides a multiplatform command-line experience for Azure.</span></span> <span data-ttu-id="cab86-128">Doğrudan, komut satırından sağlamak ve kaynakları yönetmek için çalışır.</span><span class="sxs-lookup"><span data-stu-id="cab86-128">You work directly from your command-line to provision and manage resources.</span></span>

<span data-ttu-id="cab86-129">Azure CLI yüklemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="cab86-129">To install the Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="cab86-130">Yönetici olarak bir komut istemi penceresi açın.</span><span class="sxs-lookup"><span data-stu-id="cab86-130">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="cab86-131">Aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="cab86-131">Run the following commands:</span></span>

   ```bash
   pip install --upgrade azure-cli
   pip install --upgrade azure-cli-iot
   ```
3. <span data-ttu-id="cab86-132">Aşağıdaki komutu çalıştırarak yüklemeyi doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="cab86-132">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="cab86-133">Yükleme başarılı olursa, aşağıdaki çıkış görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="cab86-133">You see the following output if the installation is successful.</span></span>

![Başarı belirten bir çıkış](media/iot-hub-raspberry-pi-lessons/lesson2/az_iot_help_win.png)

## <a name="summary"></a><span data-ttu-id="cab86-135">Özet</span><span class="sxs-lookup"><span data-stu-id="cab86-135">Summary</span></span>
<span data-ttu-id="cab86-136">Azure CLI yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="cab86-136">You've installed the Azure CLI.</span></span> <span data-ttu-id="cab86-137">Azure CLI kullanarak Azure IOT hub ve cihaz kimliğini oluşturmak için sonraki göreviniz.</span><span class="sxs-lookup"><span data-stu-id="cab86-137">Your next task to create your Azure IoT hub and device identity by using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cab86-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cab86-138">Next steps</span></span>
[<span data-ttu-id="cab86-139">IOT hub'ınızı oluşturun ve Raspberry Pi 3 kaydedin</span><span class="sxs-lookup"><span data-stu-id="cab86-139">Create your IoT hub and register Raspberry Pi 3</span></span>](iot-hub-raspberry-pi-kit-node-lesson2-prepare-azure-iot-hub.md)

