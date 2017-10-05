---
title: "Azure IOT - Ders 2 Intel Edison'u (düğüm) bağlanma: Azure Araçları (Ubuntu) | Microsoft Docs"
description: "Python ve Azure komut satırı arabirimi (Azure CLI) üzerinde Ubuntu yükleyin."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure CLI, IOT bulut hizmeti, arduino bulut
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 6dcb34bf-54a3-4af0-ba89-95d5cfafceff
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 65248e14d0ea05a44efe76e66e1ef519285982b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-azure-tools-ubuntu-1604"></a><span data-ttu-id="99e31-104">Azure Araçları (Ubuntu 16.04) alın</span><span class="sxs-lookup"><span data-stu-id="99e31-104">Get Azure tools (Ubuntu 16.04)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="99e31-105">[Windows 7 ve üzeri][windows]</span><span class="sxs-lookup"><span data-stu-id="99e31-105">[Windows 7 and later][windows]</span></span>
> * <span data-ttu-id="99e31-106">[Ubuntu 16.04][ubuntu]</span><span class="sxs-lookup"><span data-stu-id="99e31-106">[Ubuntu 16.04][ubuntu]</span></span>
> * <span data-ttu-id="99e31-107">[macOS 10.10][macos]</span><span class="sxs-lookup"><span data-stu-id="99e31-107">[macOS 10.10][macos]</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="99e31-108">Ne yapacağını</span><span class="sxs-lookup"><span data-stu-id="99e31-108">What you will do</span></span>
<span data-ttu-id="99e31-109">Azure komut satırı arabirimi (Azure CLI) yükleyin.</span><span class="sxs-lookup"><span data-stu-id="99e31-109">Install the Azure command-line interface (Azure CLI).</span></span> <span data-ttu-id="99e31-110">Herhangi bir sorun varsa, çözümleri için Ara [sorun giderme sayfası][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="99e31-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="99e31-111">Bilgi edineceksiniz</span><span class="sxs-lookup"><span data-stu-id="99e31-111">What you will learn</span></span>
<span data-ttu-id="99e31-112">Bu makalede, şunları öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="99e31-112">In this article, you will learn:</span></span>
* <span data-ttu-id="99e31-113">Azure CLI yükleme.</span><span class="sxs-lookup"><span data-stu-id="99e31-113">How to install the Azure CLI.</span></span>
* <span data-ttu-id="99e31-114">Azure CLI IOT GUID'sinin ekleme.</span><span class="sxs-lookup"><span data-stu-id="99e31-114">How to add an IoT subgroup of the Azure CLI.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="99e31-115">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="99e31-115">What you need</span></span>
* <span data-ttu-id="99e31-116">Bir Internet bağlantısı olan bir Ubuntu bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="99e31-116">An Ubuntu computer with an Internet connection.</span></span>
* <span data-ttu-id="99e31-117">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="99e31-117">An active Azure subscription.</span></span> <span data-ttu-id="99e31-118">Bir hesabınız yoksa, oluşturabileceğiniz bir [ücretsiz deneme sürümü hesabı](http://azure.microsoft.com/pricing/free-trial/) yalnızca birkaç dakika içinde.</span><span class="sxs-lookup"><span data-stu-id="99e31-118">If you don't have an account, you can create a [free trial account](http://azure.microsoft.com/pricing/free-trial/) in just a few minutes.</span></span>

## <a name="install-the-azure-cli"></a><span data-ttu-id="99e31-119">Azure CLI'yı yükleme</span><span class="sxs-lookup"><span data-stu-id="99e31-119">Install the Azure CLI</span></span>
<span data-ttu-id="99e31-120">Azure CLI çok platformlu bir komut satırı deneyimi, Azure için doğrudan komut satırından sağlamak için çalışma ve kaynakları yönetmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="99e31-120">The Azure CLI provides a multiplatform command-line experience for Azure, enabling you to work directly from your command line to provision and manage resources.</span></span>

<span data-ttu-id="99e31-121">En son Azure CLI yüklemek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="99e31-121">To install the latest Azure CLI, follow these steps:</span></span>

1. <span data-ttu-id="99e31-122">Bir terminal penceresi aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="99e31-122">Run the following commands in a terminal window.</span></span> <span data-ttu-id="99e31-123">Azure CLI yüklemek için beş dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="99e31-123">It might take five minutes to install the Azure CLI.</span></span>

   ```bash
   sudo apt-get update
   sudo apt-get install -y libssl-dev libffi-dev
   sudo apt-get install -y python-dev
   sudo apt-get install -y build-essential
   sudo apt-get install -y python-pip
   sudo pip install --upgrade azure-cli
   sudo pip install --upgrade azure-cli-iot
   ```
2. <span data-ttu-id="99e31-124">Aşağıdaki komutu çalıştırarak yüklemeyi doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="99e31-124">Verify the installation by running the following command:</span></span>

   ```bash
   az iot -h
   ```

<span data-ttu-id="99e31-125">Yükleme başarılı olursa aşağıdaki çıktı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="99e31-125">You should see the following output if the installation is successful.</span></span>

![Başarı belirten bir çıkış](media/iot-hub-intel-edison-lessons/lesson2/az_iot_help_ubuntu.png)

## <a name="summary"></a><span data-ttu-id="99e31-127">Özet</span><span class="sxs-lookup"><span data-stu-id="99e31-127">Summary</span></span>
<span data-ttu-id="99e31-128">Azure CLI yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="99e31-128">You've installed the Azure CLI.</span></span> <span data-ttu-id="99e31-129">Sonraki göreviniz Azure CLI kullanarak Azure IOT hub ve cihaz kimliğinizi oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="99e31-129">Your next task is to create your Azure IoT hub and device identity using the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="99e31-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="99e31-130">Next steps</span></span>
<span data-ttu-id="99e31-131">[IOT hub'ınızı oluşturun ve Intel Edison'u kaydedin][create-your-iot-hub-and-register-intel-edison]</span><span class="sxs-lookup"><span data-stu-id="99e31-131">[Create your IoT hub and register Intel Edison][create-your-iot-hub-and-register-intel-edison]</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[create-your-iot-hub-and-register-intel-edison]: iot-hub-intel-edison-kit-node-lesson2-prepare-azure-iot-hub.md
[windows]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-win32.md
[ubuntu]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-ubuntu.md
[macos]: iot-hub-intel-edison-kit-node-lesson2-get-azure-tools-mac.md
